---
name: self-reflection
description: >
  Use this skill whenever a Shopify PM mentions anything related to their
  performance review, self-reflection, self-assessment, perf cycle, or review
  evidence. This includes: "write my self-reflection", "help with my perf review",
  "gather evidence for my review", "what did I ship this half", "map my work to
  level requirements", "write my highlights", "prepare my 6-month review",
  "help me with my self-ratings", "find my impact", "evidence for my level",
  "justify my ratings", or "IC+ self assessment". Also trigger on mentions of
  PM level requirements (C4-C10), GSD projects in a review context, the four
  self-rating dimensions (work quality, team outcomes, trust battery, speed),
  or the semi-annual review cycle. Use this skill even if the PM only asks about
  one section (just highlights, just ratings, just level reqs). Do NOT wait for
  the word "self-reflection" explicitly. If a PM is talking about what they
  shipped, their impact, or their level in the context of a review, use this skill.
---

# PM Self-Reflection Generator

Gather evidence from a Shopify PM's work artifacts, map it to the review form with zero reuse, and write it in their voice.

## The Cardinal Rule

**No piece of evidence may appear in more than one section of the review.** Each accomplishment earns one placement.

## The Review Form Sections

1. **Highlights** (up to 3): Impact + how AI contributed + GSD link
2. **What would unlock even greater impact?**: Forward-looking growth areas
3. **Self-Ratings** (4 dimensions, 1-5 scale): work quality, team outcomes, trust battery, speed
4. **Level Requirements**: Evidence of meeting/exceeding PM level (C4-C10)

---

## Phase 0: Setup

Ask these questions first:

1. **Name?**
2. **PM level?** (C4-C10)
3. **Review period?** (e.g., "H2 2025")
4. **Full review or specific sections?**

Also collect:
5. **Vault team URL?** (e.g. `https://vault.shopify.io/teams/13801`)
6. **Which Slack channels show your impact?** Ask for 2-4 channels. PMs typically have: a wins channel (e.g. `pcb-wins`), their team's fecta channel (e.g. `disputes-pricing-insights-fecta`), and a PM or leadership channel (e.g. `pcb-pm-team`). All three matter: wins channels capture shipped work, fecta channels capture technical decisions and day-to-day leadership, PM channels capture strategic discussions and cross-team visibility.
7. **GSD project links?** (optional, can find via Vault)
8. **Pre-selected highlights?** (optional, skip if none)

### Check Tool Availability (HARD GATE)

**All three tools below are REQUIRED. Do not proceed past Phase 0 until all three pass.** A self-reflection without Drive evidence, without the team roster from Vault, and without team wins from Slack will be incomplete. Walk the PM through setup for any that fail.

**1. Google Workspace MCP:**
Run `calendar_events`. If the response contains `permission_note` about missing Drive/Docs perms, run `read_mail(query:"from:me", max_results:1)` to trigger OAuth re-auth, then retry `search_drive` once. If still failing:

> "Google Workspace MCP needs Drive permissions. Try running `! rm ~/.gworkspace_mcp/oauth_token.pickle` and restarting Claude Code. When the browser opens, grant ALL permissions (Drive, Calendar, Mail, Sheets)."

**2. Vault CLI (`devx agent-tools vault`):**
Run `devx agent-tools vault user me`. If it fails with "No Vault credentials found":

> "Vault CLI needs auth so I can pull your team roster and GSD projects. Run this in your terminal:
> `! devx agent-tools vault auth setup`
> Or go to https://vault.shopify.io/api_token, copy the token, and run:
> `! export VAULT_API_TOKEN=your_token_here`
> Then tell me to try again."

**3. Slack CLI (`devx agent-tools slack`):**
Run `devx agent-tools slack search "test" --limit 1`. If it fails with "No Slack credentials found":

> "Slack CLI needs auth so I can search your team's wins channel. Run this in your terminal:
> `! devx agent-tools slack auth setup`
> This will open Chrome and extract credentials from your Slack session. If that doesn't work, you can also set SLACK_TOKEN and SLACK_COOKIE environment variables from your Cursor MCP config or browser DevTools."

**Do not continue until all three tools are working.** This is non-negotiable. Without Vault, you'll miss team members. Without Slack, you'll miss shipped wins. Without Drive, you'll miss the PM's actual work. A partial reflection is worse than waiting 5 minutes to set up auth.

### Load Level Requirements

Read `references/level-requirements.md`, ONLY the PM's level section (cumulative). Confirm understanding back to the PM before proceeding.

---

## Phase 1: Learn Writing Style

### Shortcut: existing style file

Check if `~/.claude/{pm-first-name}-writing-style.md` exists (non-empty, modified within 12 months). If found, read it and skip to Phase 2.

### Full extraction (no style file)

1. Search Drive for docs the PM authored in the last 6-12 months using `fullText contains '{PM name}'`
2. Read docs one at a time. Skip any under ~500 words. Continue until you have 3-5 substantive samples.
3. Follow `references/writing-style-extraction.md` end to end
4. If fewer than 3 docs found, ask the PM to share specific doc links

---

## Phase 2: Gather Evidence

### Drive Searches

Shopify uses shared drives. Personal "My Drive" is typically empty. Use `fullText contains` queries.

1. **Primary:** `fullText contains '{PM name}' and modifiedTime > '{period_start}'`
2. **Presentations:** Same query with `mimeType = 'application/vnd.google-apps.presentation'`
3. **Project-specific:** `fullText contains '{project name}'` for projects surfaced in step 1
4. **Spreadsheets:** Same name query with `mimeType = 'application/vnd.google-apps.spreadsheet'`
5. **Read top 10-15 docs.** Rank by: title contains known project names > doc length > recency. Prioritize proposals, aims, decision docs, analyses over meeting notes. For docs over ~3000 words, read the first 2000 words and conclusion. Skip personal/social docs.

If fewer than 5 substantive docs found, follow the thin evidence guidance in `references/evidence-allocation.md` and ask the PM to paste doc links or describe accomplishments.

### Team Contributions (required)

A reflection that only lists the PM's individual work is incomplete. Managers want to see strategy translating into team execution.

**Step 1: Get the full team roster from Vault.** This is the authoritative source for who is on the team. Do not guess from docs or Slack.
```
devx agent-tools vault team get {team_id}
devx agent-tools vault team members {team_id}
```
Record every team member's name and role. This list drives everything below.

**Step 2: Get team GSD projects from Vault.**
```
devx agent-tools vault project list --team {team_id}
devx agent-tools vault project get {project_id} --activity --activity-weeks 26
```
For each shipped project, record: what shipped, who drove it, outcome.

**Step 3: Get evidence from ALL Slack channels the PM provided.**
Search every channel. Each serves a different purpose:
- **Wins channel** (e.g. `pcb-wins`): shipped work, launch announcements, team recognition
- **Fecta/team channel** (e.g. `disputes-pricing-insights-fecta`): technical decisions, day-to-day leadership, incident response, architecture discussions
- **PM/leadership channel** (e.g. `pcb-pm-team`): strategic discussions, cross-team visibility, leadership alignment

For each channel:
```
devx agent-tools slack search "in:{channel} after:{period_start}" --limit 30
devx agent-tools slack search "in:{channel} from:{pm_handle}" --limit 20
```
Then search for posts BY each team member (from the Vault roster) across all channels:
```
devx agent-tools slack search "in:{channel} from:{member_name}" --limit 10
```
Also search for key project names across all channels. Extract: what shipped, who drove it, quantified impact, decisions made, recognition received.

**Step 4: Weave into the reflection.** Name specific team members and what they shipped in highlights, self-ratings, and level requirements. "Steven shipped POS evidence packaging because I identified we were sending irrelevant docs for in-person disputes" is stronger than "the team shipped X."

### Build the Evidence Pool

Follow Step 1 of `references/evidence-allocation.md` to build the master evidence pool. Present to the PM as a table for validation before proceeding. Do NOT proceed to allocation without PM approval.

---

## Phase 3: Allocate Evidence

Follow the full algorithm in `references/evidence-allocation.md`. Priority: Highlights > Level Requirements > Self-Ratings > Forward-Looking (uses no evidence).

Print an allocation table showing every item and its single assigned section. Verify no item appears twice. Present to the PM. After any swaps, re-verify.

If a self-rating dimension has zero remaining evidence, flag it and ask the PM for anecdotes.

---

## Phase 4: Write the Reflection

Write in the PM's voice (Phase 1). First person. Output as pasteable markdown.

### Output Structure

```markdown
# Self-Reflection: {PM Name} | {Review Period}

## Highlights

### Highlight 1: {Title}
**Impact on the outcome:** {specific, quantified. Lead with result not process.}
**How AI contributed:** {specific tools and how. Not "AI helped me work faster."}
**GSD Project:** {link or N/A}

(Repeat for Highlights 2-3, same structure)

## What would unlock even greater impact?
{2-4 paragraphs. Synthesize per Step 6 of references/evidence-allocation.md.
Frame as growth opportunities, not weaknesses.}

## Self-Ratings
For each dimension, format as:
### {Dimension text}
**Rating: {X}/5**
- {evidence bullet linking accomplishment to dimension}
- {evidence bullet}

Dimensions: (1) Work quality/craft excellence (2) Team outcomes
(3) Trust battery / making teams better (4) Speed and pace-setting

## Level Requirements: {Level}
Per category (Craft Skills, Responsibilities To Craft/Job, Responsibilities To Shopify):
| Requirement | Evidence (first person, specific) | Assessment |
|-------------|-----------------------------------|------------|
| {text} | {allocated evidence} | Meeting / Exceeding / Gap |
```

The PM makes the final rating decision. Present suggestions with reasoning but don't be prescriptive.

Write evidence in first person. For gaps, write honestly: "I don't have strong evidence for this requirement. [context or plan]."

---

## Phase 5: Review and Refine

Walk through each section with the PM:
1. Does this sound like you?
2. Is any evidence incorrectly attributed or overstated?
3. Are the self-ratings defensible to your manager?
4. Is any evidence appearing in more than one section?
5. Are there sections that feel thin?

Iterate until approved.

---

## Anti-Patterns

- **Generic AI voice.** Match the PM's style from Phase 1.
- **Fabricating impact numbers.** Only use numbers from evidence.
- **Stretching weak evidence.** An honest gap > a stretched example.
- **Overloading highlights.** 2 strong > 3 where one is weak.
