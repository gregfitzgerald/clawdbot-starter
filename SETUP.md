# Setup Guide

This guide walks through setting up Clawdbot with Discord.

## Discord Bot Setup

**See `DISCORD-BOT-SETUP.md` for the complete step-by-step guide.**

That document covers:
- Creating the Discord application and bot
- Getting the bot token
- Enabling required intents (critical!)
- Generating the invite link
- Adding the bot to a server
- Getting your User ID
- Troubleshooting common issues

**Note:** The Discord bot can be created by anyone - if someone technical is helping you set up, they can create the bot and give you the token. You don't need to do it yourself.

## Step 5: Create Clawdbot Config

Create the file `~/.clawdbot/config/clawdbot.yml`:

```yaml
# Clawdbot Configuration
version: "1.0"

# Model settings - using Sonnet 4.5 for efficiency
model: anthropic/claude-sonnet-4-5

# Your workspace directory (where AGENTS.md, SOUL.md, etc. live)
workdir: /path/to/your/clawdbot-starter

# Discord configuration
discord:
  enabled: true
  token: "YOUR_BOT_TOKEN_HERE"  # Paste the token from Step 2
  
  # Who can talk to the bot
  allowlist:
    - "YOUR_DISCORD_USER_ID"  # Right-click yourself → Copy User ID
  
  # Optional: specific channels only
  # channels:
  #   - "channel_id_here"

# Heartbeat (periodic check-ins)
heartbeat:
  enabled: true
  intervalMinutes: 30

# API key for Claude
anthropic:
  apiKey: "YOUR_ANTHROPIC_API_KEY"  # From console.anthropic.com
```

### Finding Your Discord User ID

1. In Discord, go to Settings → Advanced → Enable **Developer Mode**
2. Right-click on yourself in any server
3. Click **Copy User ID**

### Authenticating with Claude

Clawdbot uses the same OAuth authentication as Claude Code. No separate API key needed!

```bash
# This will open a browser to authenticate with your Claude account
clawdbot login
```

Sign in with your Claude Pro/Max account and you're set.

## Step 6: Start Clawdbot

```bash
# Start the gateway
clawdbot gateway start

# Check status
clawdbot gateway status

# View logs
clawdbot gateway logs
```

## Step 7: Test It!

In Discord, mention your bot:

```
@YourBotName hello!
```

It should respond!

## Troubleshooting

### Bot doesn't respond
- Check `clawdbot gateway logs` for errors
- Verify the bot token is correct
- Make sure Message Content Intent is enabled
- Confirm your user ID is in the allowlist

### "Unauthorized" errors
- Your Anthropic API key may be invalid
- Check https://console.anthropic.com for usage/billing

### Bot is online but ignores messages
- The allowlist might not include your user ID
- The bot might not have permission to read the channel

## Next Steps

Once the bot is responding:
1. Customize `SOUL.md` with the agent's personality
2. Fill in `USER.md` with information about yourself
3. Start adding notes to `memory/` as you work together
