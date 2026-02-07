# Conversation Analysis Instructions

This document tells Claude Code how to analyze exported conversation history to build understanding of the human.

## When to Run This

Run this analysis after the human has exported their Claude.ai conversations to `data/conversation-history.json`.

## How to Analyze

### 1. Load the Conversation Data

```bash
# Check if the file exists
ls -la data/conversation-history.json
```

Read the JSON file. It typically has a structure like:
- Array of conversations, each with messages
- Each message has a role (human/assistant) and content

### 2. Extract Insights

Look for patterns across all conversations:

**Communication Style:**
- How formal or casual are their messages?
- Do they use emojis? Punctuation style?
- Are messages typically short or detailed?
- Do they prefer bullet points, paragraphs, or conversational style?

**Topics & Interests:**
- What subjects come up repeatedly?
- What are they trying to learn or accomplish?
- What projects or work are they doing?
- Personal interests that appear?

**Preferences:**
- What do they explicitly ask Claude to do/not do?
- What formats do they prefer for responses?
- Any frustrations expressed with Claude's responses?
- What makes them say "perfect" or "thanks"?

**Context:**
- Job/profession hints
- Technical skill level
- Location or timezone hints
- Family/life situation mentions

**How They Use Claude:**
- Coding help?
- Writing assistance?
- Research?
- Brainstorming?
- Learning new things?
- Personal advice?

### 3. Generate Output Files

Based on your analysis, update these files:

**USER.md** - Add discovered information:
```markdown
## Discovered Preferences
- [specific preferences found]

## Common Topics
- [topics they discuss frequently]

## Communication Notes
- [style observations]
```

**MEMORY.md** - Add relevant context:
```markdown
## From Conversation History

### Topics of Interest
- [list topics]

### Projects Mentioned
- [any ongoing projects or goals]

### Preferences Learned
- [specific preferences]

### Context
- [relevant life context discovered]
```

**memory/conversation-insights.md** - Detailed analysis:
```markdown
# Conversation History Analysis
*Generated from Claude.ai export*

## Overview
- Total conversations analyzed: X
- Date range: [earliest] to [latest]
- Primary use cases: [list]

## Communication Style
[detailed observations]

## Key Topics
[organized by category]

## Notable Preferences
[specific things they like/dislike]

## Suggested Agent Behavior
Based on this analysis, the agent should:
- [specific recommendations]
```

### 4. Be Thoughtful

**DO:**
- Note patterns that will help serve them better
- Identify their technical comfort level
- Understand their goals and priorities
- Note explicit preferences

**DON'T:**
- Include sensitive personal information unnecessarily
- Make assumptions beyond what's evident
- Include information that would be awkward if they read it
- Copy full conversation content

### 5. Discuss with the Human

After generating the analysis, show them what you found and ask:
- "Does this capture you accurately?"
- "Anything I should add or remove?"
- "Any preferences I missed?"

Let them refine the understanding before finalizing.

## Example Insights

Good insight: "Prefers concise explanations with examples. Often asks follow-up questions, so anticipate next steps."

Bad insight: "Talked about relationship problems on [date]" - too personal, not actionable.

Good insight: "Works with Python frequently, intermediate skill level. Often needs help with pandas and data visualization."

Bad insight: "Seems stressed about work" - too interpretive, not helpful.

---

*This analysis creates a foundation. The agent will continue learning through ongoing interaction.*
