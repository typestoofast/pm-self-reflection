# Evidence Allocation Algorithm

The self-reflection form has multiple sections that draw from the same pool of accomplishments. The core constraint: **no piece of evidence may appear in more than one section.** An "example" = a specific project, initiative, document, decision, or measurable outcome.

This algorithm ensures every section gets strong evidence while respecting the no-reuse rule.

---

## Step 1: Build the Master Evidence Pool

Collect ALL evidence from all sources into one list. For each item, capture:

| Field | Description |
|-------|-------------|
| **What** | Brief description (1-2 sentences) |
| **Impact** | Quantified where possible (revenue, users, time saved, quality improvement) |
| **Date** | When it happened |
| **Link** | URL to the Google Doc, GSD project, or other artifact |
| **People** | Who was involved, which teams |
| **Tags** | Which form sections this evidence COULD support (may be multiple) |

Tag each item with ALL sections it could potentially support:
- `highlight` -- Could be a top highlight
- `craft-skill:[specific skill]` -- Demonstrates a specific craft skill
- `craft-responsibility:[specific responsibility]` -- Demonstrates a craft responsibility
- `shopify-responsibility:[specific responsibility]` -- Demonstrates a Shopify responsibility
- `quality` -- Supports "work quality raises the bar" self-rating
- `team-outcomes` -- Supports "take responsibility for team outcomes" self-rating
- `trust-battery` -- Supports "charge trust battery" self-rating
- `speed` -- Supports "execute with speed" self-rating

---

## Step 2: Score and Rank

For each evidence item, compute a composite score:

```
Score = Impact(1-5) * 2 + Visibility(1-3) + Uniqueness(1-3)
```

**Impact (1-5):** How significant was this? 5 = large measurable business outcome. 1 = minor improvement.

**Visibility (1-3):** How well-known is this? 3 = leadership saw it, discussed in team-wide forums. 1 = only the immediate team knows.

**Uniqueness (1-3):** How distinct is this from other evidence? 3 = completely different domain/skill. 1 = overlaps heavily with another item.

Maximum score = 16. Sort descending.

---

## Step 3: Allocate to Highlights (Priority 1)

Highlights are the most visible section -- the first thing a manager reads. They get first pick.

1. Take the top 3 scoring items
2. Prefer diversity: if all 3 are the same type (e.g., all product launches), swap the lowest for a different type (e.g., process improvement, cross-functional win)
3. If the PM provided GSD project links, at least one highlight should connect to a GSD project
4. Remove these 3 from the available pool

---

## Step 4: Allocate to Level Requirements (Priority 2)

Level requirements need specific behavioral evidence. For each requirement at the PM's level:

1. Scan the remaining pool for items tagged with the matching requirement
2. Select the highest-scoring match
3. One piece of evidence may cover multiple requirements ONLY if they are in the same category (e.g., two Craft Skills demonstrated by one initiative). Mark this clearly.
4. Remove allocated items from the pool

If a requirement has no matching evidence:
- Note the gap explicitly: "No strong evidence found for [requirement]. Consider whether you have examples from meetings, decisions, or informal leadership moments not captured in documents."
- Do NOT fabricate or stretch evidence to fill the gap

---

## Step 5: Allocate to Self-Ratings (Priority 3)

Self-ratings accept softer evidence. For each of the 4 dimensions:

1. **"My work quality raises the bar"** -- Look for: quality improvements, high standards enforced, craft excellence
2. **"I take responsibility for team outcomes"** -- Look for: owning failures, celebrating team wins, cross-functional accountability
3. **"I constantly charge my trust battery"** -- Look for: mentoring, trust-building, making teams better, reliability
4. **"I execute with speed and set the pace"** -- Look for: fast delivery, unblocking others, setting cadence

Select 2-3 items per dimension from the remaining pool. Softer evidence (meeting patterns, feedback received, process contributions) works well here.

---

## Step 6: Forward-Looking Uses NO Allocated Evidence

The "What would unlock greater impact?" section is future-oriented. Do NOT use any evidence from the pool. Instead, synthesize from:

- **Gaps in evidence**: If few items tagged `team-outcomes`, growth area might be "broader ownership beyond my direct work"
- **Concentration patterns**: If all evidence is from Q1, growth area might be "sustaining impact across the full half"
- **Level requirements without evidence**: These are natural growth targets
- **Feedback themes**: If docs show recurring challenges, frame as growth opportunities

---

## Step 7: Verify Zero Overlap

Print an allocation table:

```
| # | Evidence Item | Allocated To | Score |
|---|---------------|-------------|-------|
| 1 | Launched dispute system | Highlight 1 | 14 |
| 2 | Cross-team pricing alignment | Highlight 2 | 13 |
| 3 | Merchant dashboard | Highlight 3 | 12 |
| 4 | Reduced chargeback review time | Craft: Simplify for team | 11 |
| 5 | Mentored 3 junior PMs | Self-rating: Trust battery | 9 |
| ... | ... | ... | ... |
```

Verify: every item appears EXACTLY ONCE. If any item appears in two places, move the weaker usage and find a replacement.

---

## Step 8: Present to PM for Approval

Show the allocation table. The PM may:
- **Swap items** between sections (e.g., move a highlight to a level requirement)
- **Add new evidence** not in the pool
- **Remove items** they don't want included
- **Override scores** based on context you can't see

After any swap, re-run the zero-overlap verification.

---

## Handling Thin Evidence (<10 items)

For junior PMs (C4/C5), new hires, or PMs with limited doc output:

1. Reduce highlights from 3 to 2 (better to have 2 strong ones than 3 weak ones)
2. Allow one evidence item to cover up to 3 level requirements in the same category
3. For self-ratings, accept general patterns (e.g., "consistently delivered on time across all projects") rather than requiring specific items
4. Actively prompt the PM: "Your evidence pool is smaller than typical. Are there accomplishments from meetings, Slack discussions, or informal leadership moments that aren't captured in your documents?"
5. Search more broadly -- expand Drive search to docs where the PM is mentioned (not just authored)
