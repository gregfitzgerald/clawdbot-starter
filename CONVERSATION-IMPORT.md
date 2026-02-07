# Importing Your Claude Conversation History

Before setting up the agent, export your existing Claude.ai conversations. This helps your new agent understand you from day one.

## Step 1: Install Tampermonkey

Tampermonkey is a browser extension that runs custom scripts.

1. Go to https://www.tampermonkey.net/
2. Click the download link for your browser (Chrome, Firefox, Edge, Safari)
3. Install the extension

## Step 2: Install Lyra Exporter Fetch Script

1. Go to: https://greasyfork.org/en/scripts/539579-lyra-s-exporter-fetch
2. Click **"Install this script"**
3. Tampermonkey will ask to confirm - click **Install**

## Step 3: Export Your Claude Conversations

1. Go to https://claude.ai
2. You should see a new **export button** added by the script (look for it near your conversation list)
3. Click the export button
4. Choose **"Full Account"** to export ALL your conversations
5. The data will either:
   - Download as a JSON file, OR
   - Open in Lyra Exporter automatically

If it downloads as JSON:
- Save the file somewhere you can find it (e.g., Downloads folder)
- Optionally, go to https://yalums.github.io/lyra-exporter/ to view/search your conversations

## Step 4: Place the Export File

Move or copy the JSON file to your clawdbot-starter directory:

```bash
# Example - adjust the path to where your file actually is
cp ~/Downloads/claude_conversations.json ~/clawdbot-starter/data/conversation-history.json
```

## What Gets Exported

The JSON file contains:
- All your conversations with Claude
- Timestamps for each message
- Your messages and Claude's responses
- References to any attachments or artifacts
- Thinking processes (if any)

## Next Steps

Once the file is in place, Claude Code can analyze it to:
- Learn your communication style
- Understand topics you care about
- Note your preferences and how Claude has helped you
- Pre-populate MEMORY.md with relevant context

This happens automatically during setup - see the README for the full flow.
