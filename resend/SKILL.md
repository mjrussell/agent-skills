---
name: resend
description: Manage Resend email workflows including sending email, inspecting received (inbound) messages and attachments, configuring domains, and managing contacts, broadcasts, API keys, teams, and webhooks. Use when user asks about Resend email operations or account setup.
homepage: https://resend.com
metadata:
  clawdbot:
    emoji: "📧"
    requires:
      bins: ["resend"]
      env: ["RESEND_API_KEY"]
---

# Resend CLI

Official CLI for the Resend email API.

## Installation

```bash
# Preferred install methods
brew install resend/cli/resend

# Or use the official installer
curl -fsSL https://resend.com/install.sh | bash
```

## Setup

1. Create an API key at https://resend.com/api-keys
2. Authenticate with one of:
   ```bash
   resend login
   # or
   export RESEND_API_KEY="re_your_key"
   ```
3. For sending email, verify a domain first:
   ```bash
   resend domains create --name example.com
   resend domains verify <domain-id>
   ```
4. For inbound email commands, create a domain with receiving enabled:
   ```bash
   resend domains create --name example.com --receiving
   ```
5. Optional: manage multiple accounts with team profiles:
   ```bash
   resend login --team work
   export RESEND_TEAM="work"
   ```

## Commands

### Authentication and Status

```bash
resend login                   # Store API key locally
resend logout                  # Remove stored API key
resend whoami                  # Show current auth source/team
resend doctor                  # Validate CLI setup, auth, domains, agents
resend open                    # Open the Resend dashboard
```

### Emails

```bash
resend emails send --from you@example.com --to user@example.com --subject "Hello" --text "Hi"
resend emails batch --file ./emails.json
resend emails receiving list --limit 25
resend emails receiving get <email-id>
resend emails receiving attachments <email-id>
resend emails receiving attachment <email-id> <attachment-id>
```

### Domains

```bash
resend domains list
resend domains create --name example.com --receiving
resend domains get <domain-id>
resend domains verify <domain-id>
resend domains update <domain-id> --tls enforced --open-tracking
resend domains delete <domain-id> --yes
```

### API Keys and Teams

```bash
resend api-keys list
resend api-keys create --name "CI Token"
resend api-keys delete <key-id> --yes
resend teams list
resend teams switch <team-name>
resend teams remove <team-name>
```

### Contacts, Segments, Topics, Broadcasts

```bash
resend contacts list
resend contacts create --email jane@example.com --first-name Jane
resend contacts get jane@example.com
resend contacts update jane@example.com --unsubscribed
resend contacts delete jane@example.com --yes
resend contact-properties list
resend segments list
resend topics list
resend broadcasts list
resend broadcasts create --from hello@example.com --subject "Launch" --segment-id <segment-id> --html "<p>Hi</p>"
resend broadcasts send <broadcast-id>
```

### Webhooks

```bash
resend webhooks list
resend webhooks create --endpoint https://app.example.com/hooks/resend --events all
resend webhooks get <webhook-id>
resend webhooks update <webhook-id> --status disabled
resend webhooks delete <webhook-id> --yes
```

## Usage Examples

**User: "Send a status email to the team"**
```bash
resend emails send \
  --from hello@example.com \
  --to team@example.com \
  --subject "Status update" \
  --text "Everything is green."
```

**User: "Do I have any new inbound emails?"**
```bash
resend emails receiving list --limit 5
```

**User: "Show me the latest email"**
```bash
resend emails receiving list --json | jq -r '.data[0].id'
resend emails receiving get <id>
```

**User: "What attachments are on that email?"**
```bash
resend emails receiving attachments <email_id>
```

**User: "Set up a receiving domain"**
```bash
resend domains create --name example.com --receiving
```

**User: "What domains do I have set up?"**
```bash
resend domains list
```

## Notes

- Global flags: `--api-key`, `--team`, `--json`, `--quiet`, `--version`, `--help`
- JSON output is useful for agents and scripts; piping output also switches to machine-readable mode
- Inbound email commands live under `resend emails receiving ...`, not `resend email ...`
- Received email IDs, domain IDs, broadcast IDs, webhook IDs, and contact IDs are shown in list output
- Use `resend --help` and `resend <command> --help` to inspect the latest subcommands and flags
