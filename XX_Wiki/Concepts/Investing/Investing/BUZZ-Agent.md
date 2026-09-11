---
title: "BUZZ - Agent"
type: knowledge-source
status: draft
main_topic: "JvL Invest"
creator: "Erna"
maintainer: "Erna"
content_reviewer: "Jürgen"
section: "Investing"
colorcode: "Blue"
tags:
  - MOC/Investing
sources:
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / BUZZ - Agent.md"
source_file_id: "1ZhQom0EO2J4Oqn2nhCj3rXzSJMtMFT4C"
---

# BUZZ - Agent

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

# Connect Hermes Agent to Buzz

A guide for connecting a remote Hermes Agent instance to Buzz using the standard buzz-acp external-agent flow.

## The three machines involved

- Machine 1: Buzz host — the VPS or container running Buzz/Buzz Relay.
- Machine 2: Hermes host — the VPS or container running the Hermes Agent instance you want to expose in Buzz.
- Machine 3: Client machine — your laptop/desktop with Buzz Desktop logged into the relay, used for owner-signed admin actions such as adding the bot to a room.

These can be separate VPSes, containers on one VPS, or a mixed setup. The external-agent method works as long as the Hermes host can reach the Buzz relay over its public WebSocket URL and can run buzz-acp plus hermes acp.

## Recommended architecture

```
Buzz Relay (Machine 1)  ⇄  buzz-acp on Hermes host (Machine 2)  ⇄  hermes acp  ⇄  Hermes Agent
```

Use the public relay URL for the bridge configuration. If everything is in Docker on one VPS, internal container hostnames may work, but public URLs are simpler and avoid deployment-specific assumptions.

## Prerequisites

- A reachable Buzz relay URL, preferably both HTTPS for CLI operations and WSS for buzz-acp.
- Hermes installed and working on the Hermes host.
- The Hermes ACP command works: hermes acp --check.
- Buzz CLI tools available on the Hermes host: buzz, buzz-acp, and buzz-admin.
- A Buzz owner identity on the client machine that can add members/bots to the target room.

## 1. Install Buzz CLI tools on the Hermes host

Install Buzz command-line tools from the official Buzz release appropriate for your OS/architecture. The Hermes host needs at least buzz-acp. The buzz CLI is useful for verification and profile setup. buzz-admin is used for local key generation if it is not already installed.

```bash
# Example Linux pattern; adjust version/architecture to your environment.
cd /tmp
curl -fsSL <BUZZ_RELEASE_DEB_URL> -o Buzz_amd64.deb
rm -rf /tmp/buzz-deb
dpkg-deb --extract Buzz_amd64.deb /tmp/buzz-deb
sudo install -m 0755 /tmp/buzz-deb/usr/bin/buzz /usr/local/bin/buzz
sudo install -m 0755 /tmp/buzz-deb/usr/bin/buzz-acp /usr/local/bin/buzz-acp

buzz --help
buzz-acp --help
```

If buzz-admin is not included in the release, build/install it from the Buzz source tree or use the project’s current recommended installation path.

## 2. Verify Hermes ACP on the Hermes host

```bash
command -v hermes
hermes acp --check

# Optional: if your setup provides hermes-acp directly
command -v hermes-acp && hermes-acp --check
```

## 3. Generate a dedicated Buzz/Nostr identity for Hermes

Generate the keypair on the Hermes host. Keep the secret key on that host only. Send only the public key to the Buzz workspace owner.

```bash
umask 077
buzz-admin generate-key > /tmp/hermes-buzz-key.txt
awk '/^Public key:/ {print $3}' /tmp/hermes-buzz-key.txt
# Copy the Secret key into the protected env file in the next step.
# Then securely remove /tmp/hermes-buzz-key.txt.
```

## 4. Add the Hermes bot public key to Buzz relay membership

On the Buzz host, add the generated Hermes bot public key to the relay membership list first. This is typically done inside the Buzz container or on the Buzz VPS where buzz-admin is configured.

```bash
buzz-admin add-member \
  --pubkey <hermes-bot-public-key> \
  --role member
```

Use role member for the relay-level membership. Later, add the same public key to the target room/channel as role bot.

## 5. Create a protected environment file for the bridge

On the Hermes host, create an env file readable only by the service user. Replace placeholders with your actual relay URL, generated bot secret, and owner public key.

```bash
sudo install -m 0600 /dev/null /etc/hermes-buzz-agent.env
sudo editor /etc/hermes-buzz-agent.env
```

```bash
export BUZZ_RELAY_URL=wss://<your-buzz-relay-host>
export BUZZ_PRIVATE_KEY=<generated-hermes-bot-secret>
export BUZZ_ACP_AGENT_OWNER=<owner-64-character-public-key>
export BUZZ_ACP_RESPOND_TO=owner-only
export BUZZ_ACP_AGENT_COMMAND=hermes
export BUZZ_ACP_AGENT_ARGS=acp
export HERMES_HOME=<path-to-hermes-home-if-needed>
```

Use owner-only unless you intentionally want the agent to respond to anyone. The owner public key is the human Buzz identity that is allowed to control or invoke the agent under this policy.

## 6. Run buzz-acp on the Hermes host

You can run buzz-acp under systemd, Docker Compose, supervisord, or your container runtime. The important part is that the process gets the env vars above and can execute the configured Hermes ACP command.

```bash
# Minimal foreground smoke test
set -a
source /etc/hermes-buzz-agent.env
set +a
buzz-acp
```

### Example systemd shape

```bash
# /usr/local/bin/hermes-buzz-agent
#!/usr/bin/env bash
set -euo pipefail
source /etc/hermes-buzz-agent.env
exec /usr/local/bin/buzz-acp
```

```bash
# /etc/systemd/system/hermes-buzz-agent.service
[Unit]
Description=Hermes bridge for Buzz
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=root
WorkingDirectory=/root
ExecStart=/usr/local/bin/hermes-buzz-agent
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

### Example Docker shape

```yaml
services:
  hermes-buzz-agent:
    image: <image-with-buzz-acp-and-hermes>
    restart: unless-stopped
    env_file:
      - ./hermes-buzz-agent.env
    command: ["buzz-acp"]
    volumes:
      - hermes-home:/root/.hermes
```

If Hermes and buzz-acp are in separate containers, the command still must speak ACP over stdio. A wrapper using docker exec -i can work, but keep stdout clean because ACP uses stdio as its protocol transport.

## 7. Add the Hermes bot public key to a Buzz room

From the client machine where the human owner identity is available, add the generated Hermes bot public key to the target room as a bot. The CLI needs the owner private key locally for this admin action. Hermes does not need the owner private key to reply.

```bash
buzz   --relay https://<your-buzz-relay-host>   channels add-member   --channel <target-room-id>   --pubkey <hermes-bot-public-key>   --role bot
```

If the CLI does not automatically use the desktop login, provide the owner key using the method appropriate for your OS/client. Keep that owner key on the client machine; donot copy it to the Hermes host.

## 8. Set the Hermes Buzz profile

After the bot key exists on the relay, set a readable profile using the bot identity from the Hermes host. This prevents the agent from showing up as a truncated public key.

```bash
set -a
source /etc/hermes-buzz-agent.env
set +a

buzz --relay https://<your-buzz-relay-host> users set-profile   --name "Hermes"   --about "Hermes Agent"
```

To set an avatar, upload an image to the relay media store and use the returned URL as the avatar.

```bash
AVATAR_URL=$(buzz --relay https://<your-buzz-relay-host> upload file --file ./hermes-avatar.jpg | jq -r .url)

buzz --relay https://<your-buzz-relay-host> users set-profile   --name "Hermes"   --avatar "$AVATAR_URL"   --about "Hermes Agent"
```

## 9. Verify

```bash
# On Hermes host
systemctl status hermes-buzz-agent.service --no-pager
journalctl -u hermes-buzz-agent.service -n 100 --no-pager

# Or, in Docker
docker logs --tail=100 <hermes-buzz-agent-container>
```

Healthy logs should show relay connection, ACP initialization, channel subscription, and presence/typing activity when the bot is mentioned.

```bash
# Useful Buzz-side checks from the Hermes host using the bot identity
set -a
source /etc/hermes-buzz-agent.env
set +a

buzz --relay https://<your-buzz-relay-host> channels list
buzz --relay https://<your-buzz-relay-host> channels members --channel <target-room-id>
buzz --relay https://<your-buzz-relay-host> users get --pubkey <hermes-bot-public-key>
```

## What changes if Buzz and Hermes are Docker containers on the same VPS?

- The same external buzz-acp method still works.
- Use the public relay URL unless you are certain about internal container names and ports.
- Replace systemd with Docker restart policies if you run the bridge as a container.
- Mount or bake in the Hermes runtime and Hermes home so buzz-acp can execute hermes acp.
- A local custom harness may also be possible if the Buzz runtime can execute hermes-acp directly, but the command must exist inside the environment where Buzz starts agents.

The key rule: Buzz custom harnesses speak ACP over stdio. A network service alone is not enough unless you wrap it with a stdio-compatible adapter.

## Troubleshooting notes

- Relay reachable but idle: the bot may be missing either relay membership or target room/channel membership. Both are required.
- Typing/reaction but no final reply: the event reached buzz-acp and Hermes started; check publish errors and response policy.
- Shows as a public key: publish a bot profile with buzz users set-profile.
- Mention autocomplete says not in channel while membership is correct: refresh/reopen the client; profile/member caches can lag after adding or renaming an external bot.
- Do not put the human owner private key on the Hermes host. The bot has its own key for replies.
