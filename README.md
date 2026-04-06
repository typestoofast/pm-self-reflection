# PM Self-Reflection

Are you having trouble doing self-reflections in the ~3 days we have? Point Claude Code at this repo. It will ask you for some basic info like name/level/team/channels you want it to pay attention to, and go dig through Slack/Vault/Google Drive and output the answers to self-reflection in markdown.

This is a good V1 if you're like "what did I do?" or "I did sooo much I forgot what I did." It also pulls your team's impact, which is one major way we ship (leading through others). If you see bugs, DM me.

## Install

```
git clone https://github.com/typestoofast/pm-self-reflection.git ~/.claude/plugins/installed/pm-self-reflection
```

Then in Claude Code:

```
/reload-plugins
```

## Prerequisites

1. **Claude Code** installed and working
2. **Google Workspace MCP** configured with Drive permissions (built into Claude Code)
3. **Vault CLI**: `devx agent-tools vault auth setup`
4. **Slack CLI**: `devx agent-tools slack auth setup`

Do you need to set up MCPs? That's ideal, but if not the skill helps you set everything up.

## Usage

Just tell Claude Code you want to write your self-reflection:

```
help me write my self-reflection
```

Or any variation: "start my perf review", "gather evidence for my review", "what did I ship this half", "help with my self-ratings", "map my work to level requirements".

## What it asks for

**Required:**
1. Your name
2. PM level: C4 (Apprentice), C5 (PM), C6 (Senior), C7 (Staff), C8 (Senior Staff), C9 (Principal), C10 (Distinguished)
3. Review period (defaults to last 6 months, H1/H2 options)
4. Vault team URL (e.g. `https://vault.shopify.io/teams/13801`)
5. 2-4 Slack channels that show your impact (e.g. wins channel, fecta channel, PM channel)

**Optional:**
- GSD project links (can find via Vault)
- Pre-selected highlights

## How it works

| Phase | What happens |
|-------|-------------|
| 0. Setup | Collects your info. Hard-gates on Drive, Vault, and Slack auth before proceeding. |
| 1. Writing Style | Checks for an existing style file at `~/.claude/{name}-writing-style.md` or reads 3-5 of your Google Docs to learn your voice. |
| 2. Evidence | Searches Drive for your docs, Vault for team roster and GSD projects, Slack for shipped wins across all channels you provided. Builds a master evidence pool and presents it for your approval. |
| 3. Allocate | Scores each item and allocates to Highlights > Level Requirements > Self-Ratings with zero reuse. Shows you the allocation table. |
| 4. Write | Drafts the full self-reflection in your voice as pasteable markdown. |
| 5. Review | Walks through each section with you. Iterates until you approve. |

## Tips

Point it to relevant Slack channels like your fecta channel, #pcb-wins, #pclt-pairing so the AI doesn't overrotate on the random incident you helped with (unless you're Dikshant, in which case it's all channels that are #inc lol).

## FAQ

**Will it work for managers?** Maybe, not really a problem I have.

**Will it sound like AI?** No. Part of the prompt is it learns how you write based on your Google Docs.

**Why did you build this?** Solving my own problems.

## Key design decisions

- **No evidence reuse.** Each accomplishment appears in exactly one section. Managers notice repetition.
- **Team contributions required.** The Vault team roster is the authoritative source for who is on your team. Every team member's shipped work is woven into the reflection. Your strategy translating into team execution is what managers want to see.
- **Slack channels are specific.** You provide 2-4 channels upfront so searches are targeted, not broad. Wins channels capture shipped work, fecta channels capture technical decisions, PM channels capture strategic discussions.
- **Writing style matched.** If you have a style file at `~/.claude/{name}-writing-style.md`, it uses that. Otherwise it learns from your Google Docs. The output should sound like you, not like AI.
- **All tools hard-gated.** Won't proceed without Drive, Vault, and Slack. A partial reflection is worse than waiting 5 minutes to auth.

## Supported levels

C4 (Apprentice PM) through C10 (Distinguished PM). Level requirements are cumulative and sourced from the official Shopify PM ladder. The skill loads only your level's section.
