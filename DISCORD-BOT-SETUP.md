# Discord Bot Setup - Detailed Guide

This guide walks through creating a Discord bot step-by-step. 

**Who should do this?** Anyone can create the bot - it doesn't need to be the person who will use it. If you're setting this up for someone else, you can create the bot and give them the token.

---

## Option A: Creating the Bot for Someone Else

If you're a technical person setting this up for a less technical user:

1. Follow all the steps below to create the bot
2. Save the bot token securely
3. Add the bot to a Discord server you both share (or create one)
4. Either:
   - Give them the token to paste into their config, OR
   - Pre-configure the `clawdbot.json` file with the token before they start

The person using the bot will still need to:
- Run `clawdbot login` to authenticate with their Claude account
- Start the gateway

---

## Step 1: Access Discord Developer Portal

1. Open your browser and go to: **https://discord.com/developers/applications**
2. Log in with your Discord account if prompted
3. You'll see the "Applications" page (may be empty if this is your first bot)

---

## Step 2: Create a New Application

1. Click the **"New Application"** button (top right, blue button)
2. Enter a name for your bot (e.g., "Tara's Assistant" or "Moltie")
   - This name appears in Discord, so pick something friendly
3. Check the box to agree to Discord's Terms of Service
4. Click **"Create"**

You're now on your application's settings page.

---

## Step 3: Set Up the Bot User

1. In the left sidebar, click **"Bot"**
2. You'll see the Bot settings page
3. Under the bot's username, you'll see a section for the token

### Get the Bot Token

1. Click **"Reset Token"** (or "View Token" if available)
2. Discord may ask for your password or 2FA code
3. **Copy the token immediately** - you won't be able to see it again without resetting
4. Save it somewhere secure (password manager, secure note, etc.)

⚠️ **NEVER share this token publicly!** Anyone with the token can control your bot.

### Configure Bot Settings

On the same page, configure these settings:

**Public Bot:** 
- Toggle **OFF**
- This prevents others from adding your bot to their servers

**Requires OAuth2 Code Grant:**
- Leave **OFF**

---

## Step 4: Enable Privileged Gateway Intents

This is the step most people miss, and it causes the bot to silently fail!

Scroll down on the Bot page to **"Privileged Gateway Intents"**

Enable ALL THREE of these:

1. ✅ **Presence Intent**
   - Click the toggle to turn it ON (turns blue/green)

2. ✅ **Server Members Intent**
   - Click the toggle to turn it ON

3. ✅ **Message Content Intent** ← CRITICAL
   - Click the toggle to turn it ON
   - Without this, the bot cannot read message content!

4. Click **"Save Changes"** at the bottom (green button)

---

## Step 5: Generate the Bot Invite Link

1. In the left sidebar, click **"OAuth2"**
2. Then click **"URL Generator"** (submenu under OAuth2)

### Select Scopes

In the **"Scopes"** section, check these boxes:
- ✅ `bot`
- ✅ `applications.commands`

### Select Bot Permissions

After selecting scopes, a **"Bot Permissions"** section appears below.

Check these permissions:
- ✅ Send Messages
- ✅ Send Messages in Threads
- ✅ Embed Links
- ✅ Attach Files
- ✅ Read Message History
- ✅ Add Reactions
- ✅ Use Slash Commands

### Copy the URL

1. Scroll to the bottom of the page
2. You'll see **"Generated URL"**
3. Click **"Copy"**

---

## Step 6: Add the Bot to Your Server

1. Paste the copied URL into your browser
2. A Discord authorization page opens
3. Select the server where you want to add the bot
   - You must have "Manage Server" permission on that server
4. Click **"Continue"**
5. Review the permissions and click **"Authorize"**
6. Complete the CAPTCHA if prompted

The bot is now in your server! (It will appear offline until the gateway is running)

---

## Step 7: Get Your Discord User ID

The bot needs to know who can talk to it. You'll need your Discord User ID.

1. Open Discord (app or browser)
2. Go to **User Settings** (gear icon, bottom left)
3. Go to **Advanced** (in the left sidebar, under "App Settings")
4. Enable **"Developer Mode"**
5. Close settings
6. Right-click on your own username (in any server or DM)
7. Click **"Copy User ID"**

Save this ID - you'll add it to the allowlist in the config.

---

## Step 8: Create a Server (Optional)

If you need a dedicated server for the bot:

1. In Discord, click the **"+"** button (left sidebar, below server list)
2. Click **"Create My Own"**
3. Choose "For me and my friends" (or any option)
4. Name it whatever you like (e.g., "Assistant")
5. Click **"Create"**

Then add the bot to this server using the invite URL from Step 5.

---

## Summary: What You'll Need

After completing these steps, you should have:

| Item | Where to Find It | Example |
|------|------------------|---------|
| Bot Token | Bot page → Reset Token | `MTQ2NjEw...` (long string) |
| User ID | Right-click yourself → Copy User ID | `389889395983122432` |
| Server with bot | You added it in Step 6 | Visible in server list |

---

## Giving This to Someone Else

If you created this bot for someone else, give them:

1. **The bot token** (securely - don't send in plain text over insecure channels)
2. **Their User ID** (or tell them how to get it - Step 7)
3. **Access to the server** where the bot lives

They do NOT need:
- Access to the Developer Portal
- Your Discord password
- Anything else from your account

---

## Troubleshooting

### Bot doesn't respond to messages

1. **Check Message Content Intent** - Most common issue. Go to Developer Portal → Bot → Make sure "Message Content Intent" is ON
2. **Check the allowlist** - Is your User ID in the config?
3. **Check gateway logs** - Run `clawdbot gateway logs`

### "Unauthorized" or "Invalid Token" errors

- The token may have been regenerated (Discord does this sometimes)
- Go to Developer Portal → Bot → Reset Token → Get new token → Update config

### Bot shows as offline

- The gateway isn't running: `clawdbot gateway start`
- Check logs for errors: `clawdbot gateway logs`

### Can't add bot to server

- You need "Manage Server" permission
- Ask a server admin to add it, or create your own server

---

## Security Notes

- **Rotate the token** if you ever accidentally expose it
- **Don't commit tokens to git** - use environment variables or secure config
- **Limit the allowlist** - only add User IDs of people who should use the bot
- **Use a dedicated server** if you want the bot isolated from your main servers
