# Clawdbot Starter

A ready-to-go personal assistant agent for Discord, powered by Clawdbot.

## For Claude Code

If you're Claude Code helping a human set up this agent, follow these steps:

### 1. Prerequisites Check

```bash
# Verify Node.js is installed (need v18+)
node --version

# If not installed:
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### 2. Install Clawdbot

```bash
npm install -g clawdbot
```

### 3. Discord Bot Setup

**This requires the human to do some clicking in the browser.**

Walk them through `SETUP.md` - they need to:
1. Create a Discord Application at https://discord.com/developers/applications
2. Create a bot and get the token
3. Enable required intents
4. Add the bot to their server

### 4. Configure Clawdbot

After they have the bot token:

```bash
# Initialize clawdbot in this directory
clawdbot init

# Or manually create ~/.clawdbot/config/clawdbot.yml
```

Use `example-configs/clawdbot.example.yml` as a reference.

### 5. Customize the Agent

Update these files based on conversation with the human:
- `USER.md` - Information about them
- `SOUL.md` - Agent personality (name, style, priorities)
- `IDENTITY.md` - Agent name and emoji

### 6. Start the Gateway

```bash
clawdbot gateway start
```

### 7. Test

Send a message mentioning the bot in Discord. It should respond!

---

## File Overview

| File | Purpose |
|------|---------|
| `AGENTS.md` | Core instructions for the agent |
| `SOUL.md` | Agent personality and priorities |
| `USER.md` | Information about the human |
| `TOOLS.md` | Local tool configurations |
| `HEARTBEAT.md` | Periodic check-in tasks |
| `IDENTITY.md` | Agent name and emoji |
| `memory/` | Daily notes and context |
| `data/` | Structured data files |

## Model Configuration

This setup defaults to Claude Sonnet 4.5 for cost efficiency. Change in `clawdbot.yml`:

```yaml
model: anthropic/claude-sonnet-4-5
```
