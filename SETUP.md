# Discord Bot Setup Guide

This guide walks through creating a Discord bot and connecting it to Clawdbot.

## Step 1: Create a Discord Application

1. Go to https://discord.com/developers/applications
2. Click **"New Application"** (top right)
3. Give it a name (this will be your bot's name, e.g., "Moltie")
4. Accept the terms and click **Create**

## Step 2: Create the Bot User

1. In the left sidebar, click **"Bot"**
2. Click **"Add Bot"** and confirm
3. Under the bot's username, click **"Reset Token"**
4. Copy the token and save it somewhere safe - **you'll need this for configuration**
   - ⚠️ Never share this token publicly!

## Step 3: Configure Bot Settings

On the same Bot page:

1. **Public Bot**: Turn OFF (only you can add it to servers)
2. **Requires OAuth2 Code Grant**: Leave OFF
3. Scroll down to **Privileged Gateway Intents** and enable:
   - ✅ **Presence Intent**
   - ✅ **Server Members Intent**
   - ✅ **Message Content Intent** (REQUIRED - bot won't see messages without this!)

4. Click **Save Changes**

## Step 4: Generate Invite Link

1. In the left sidebar, click **"OAuth2"** → **"URL Generator"**
2. Under **Scopes**, check:
   - ✅ `bot`
   - ✅ `applications.commands`
3. Under **Bot Permissions**, check:
   - ✅ Send Messages
   - ✅ Send Messages in Threads
   - ✅ Embed Links
   - ✅ Attach Files
   - ✅ Read Message History
   - ✅ Add Reactions
   - ✅ Use Slash Commands
4. Copy the generated URL at the bottom
5. Open that URL in your browser
6. Select your server and click **Authorize**

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

### Getting Your Anthropic API Key

If using Claude Pro subscription through the API:
1. Go to https://console.anthropic.com
2. Create an API key
3. Add it to the config

**Or** if you only have Claude Pro (not API access), you may need to sign up for API access separately.

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
