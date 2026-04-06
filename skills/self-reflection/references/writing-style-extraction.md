# Writing Style Extraction

Learn a PM's writing voice from their Google Docs before generating any prose. The self-reflection must sound like the PM wrote it, not like an AI.

---

## Step 1: Find Recent Documents

Search Google Drive for docs the PM authored in the last 6-12 months. Target these doc types (in priority order):

1. **Strategy docs / proposals** -- Most revealing of voice and argumentation style
2. **Product briefs / specs** -- Shows how they frame problems and solutions
3. **Analysis docs** -- Shows how they handle data and draw conclusions
4. **Launch docs / announcements** -- Shows how they communicate impact
5. **Decision docs (SPADEs, RFCs)** -- Shows how they structure arguments

Need at least **3 substantive docs** (500+ words each). More is better, up to 5.

If fewer than 3 found: ask the PM to provide specific doc links. Do NOT proceed with style learning from fewer than 3 docs -- the model will be unreliable.

---

## Step 2: Extract Patterns Across 5 Dimensions

Read each doc carefully. Extract patterns along these axes:

### Dimension 1: Tone
- **Formality level**: Corporate-formal ("We recommend...") vs conversational ("Here's what we should do...")
- **Contractions**: Does the PM use "we're", "can't", "don't" or spell them out?
- **Rhetorical questions**: Does the PM frame sections with questions?
- **Directness**: Does the PM hedge ("we might consider...") or assert ("we should...")?
- **Humor/personality**: Any distinctive verbal tics, running metaphors, or recurring phrases?

### Dimension 2: Structure
- **Bullet vs paragraph**: Heavy bullet usage or flowing paragraphs?
- **Table usage**: Frequent tables for comparisons, or prose-only?
- **Header conventions**: Short imperative headers ("Ship it") or descriptive ("Proposed shipping timeline")?
- **TL;DR style**: Does the PM lead with a summary? How is it formatted?
- **Section ordering**: Does the PM lead with the recommendation or build up to it?

### Dimension 3: Sentence Construction
- **Length**: Short punchy sentences or longer complex ones?
- **Punctuation**: Em-dashes, parenthetical asides, semicolons?
- **Active vs passive**: "We shipped X" vs "X was shipped"
- **First person**: "I" vs "we" vs impersonal?

### Dimension 4: Vocabulary
- **Abbreviations**: "b/w", "eng", "merch", "devs" or fully spelled out?
- **Jargon level**: Heavy Shopify/PM jargon or plain language?
- **How they refer to customers**: "merchants", "users", "customers", "shops"?
- **Repeated phrases**: Any signature phrases or frameworks they use often?

### Dimension 5: Data Presentation
- **Precision**: "$207.7M" or "~$200M"?
- **Inline vs tables**: Numbers woven into prose or broken into tables?
- **Segmentation**: Do they break data by dimensions (GMV band, time, geography)?
- **Citations**: Do they cite sources, or present numbers without attribution?

---

## Step 3: Synthesize Internally

Build a mental model of the PM's voice. DO NOT:
- Output a written style guide to the PM
- Tell the PM "I noticed you write with X style"
- Ask the PM to confirm your style assessment

Simply apply the patterns when writing the reflection. The PM will know if it sounds right.

---

## Step 4: Apply When Writing

When generating the self-reflection:
- Match the PM's tone (formal → formal, casual → casual)
- Use their sentence structure patterns (short + punchy, or longer + complex)
- Use their vocabulary (abbreviations, jargon level, customer terminology)
- Use their preferred data presentation style
- Use their structural patterns (bullets vs paragraphs, table usage)
- Write in first person ("I") -- this is a self-reflection

---

## Common Pitfalls

- **Defaulting to AI voice**: If you can't detect a clear pattern in a dimension, err on the side of direct and conversational rather than corporate
- **Over-formalizing**: Self-reflections are personal. Even PMs who write formally in proposals tend to be more personal in self-assessments
- **Inconsistent voice**: Once you've established the PM's patterns, maintain them throughout the entire reflection. Don't shift between sections
- **Ignoring the "don'ts"**: If the PM never uses certain patterns (no tables, no bullet points, no abbreviations), respect those absences
