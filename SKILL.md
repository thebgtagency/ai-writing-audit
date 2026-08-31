---
name: ai-writing-audit
description: >
  Audit and repair text that reads as machine-written. Works on any length and any
  format: a two-line DM, a caption, a spoken script, a carousel slide, a landing page,
  an essay. Two layers: surface tells (word, sentence, punctuation, formatting) and
  discourse tells (theme, causality, time, agency, reader address). Use after a draft
  exists, never to compose the first draft.
---

# AI Writing Audit

Text gets flagged as machine-written for two separate reasons, and most guides only
cover the first one.

**Surface tells** are word choice, sentence shape, punctuation, formatting. They are
cheap to fix and cheap to fake. They also decay fast: one model generation removes a
tell and the checklist ages out.

**Discourse tells** are how the piece is built: what it explains, what it leaves
implied, how time moves, who acts, whether it acknowledges a reader. These survive a
surface cleanup, because removing them means rewriting the structure.

> "AI style is increasingly fleeting: GPT-5.4 significantly reduced em-dash usage, and
> fine-tuning to mimic human style drops AI detection rates on creative writing from
> 97% to 3%. Discourse-level narrative features are far harder to 'humanize', as
> changing them requires significant structural rewrites rather than simple post-hoc
> edits."
> Russell et al., *StoryScope: Investigating idiosyncrasies in AI fiction*, COLM 2026

A checklist that only knows the first layer will pass text that is obviously synthetic
to a reader, and will fail text a person actually wrote.

---

## 0. Pick the layer first

The two source bodies behind this skill have opposite scope limits, and both state them
plainly. Wikipedia's guide is about informational prose and says it does not cover
fiction. StoryScope measures ~5,000-word narratives and says shorter texts cannot
support the features it extracts.

So the layer is chosen by what the text is, not by preference.

| Text | Length | Surface layer | Discourse layer |
|---|---|---|---|
| DM, reply, comment | 1-4 lines | full | reader-address check only |
| Carousel slide, caption line | 5-25 words | reduced (see §4) | no |
| Caption block | 30-120 words | full | reader-address, over-explaining |
| Spoken script (reel, VO) | 60-200 words | spoken subset (§4) | over-explaining, agency |
| Email, landing section | 150-600 words | full | full minus time-structure |
| Essay, article, long script | 600+ words | full | full |

Applying the discourse layer to eight words is not rigor, it is noise. Applying only
the surface layer to a long piece is where synthetic text passes.

---

## 1. Surface layer

Run this on any draft. Each hit gets: rule, the exact sentence, and a replacement that
carries the same claim. Deleting is not repair. A deleted sentence takes its meaning
with it.

### 1.1 Inflation
Cosmic significance welded onto an ordinary fact. `stands as`, `serves as`, `testament
to`, `underscores the importance`, `marks a turning point`, `reflects a broader`,
`enduring legacy`, `evolving landscape`, `indelible mark`.

Repair: state what the thing is or does. Delete the significance clause.

### 1.2 Promotional register
`vibrant`, `rich` (figurative), `boasts`, `nestled`, `breathtaking`, `renowned`,
`groundbreaking`, `must-visit`, `showcasing`, `a commitment to`, `diverse array`.

Newer models rarely use open superlatives; they use quiet approval instead. Watch for a
paragraph where nothing is criticised and every adjective is mild-positive.

### 1.3 Trailing -ing analysis
`highlighting`, `underscoring`, `emphasizing`, `reflecting`, `ensuring`, `fostering`,
`contributing to`, `resonating with` appended to the end of a sentence to add depth.

Repair: cut the clause, or make it a separate sentence with a source.

### 1.4 Vague attribution
`experts argue`, `industry reports`, `observers note`, `some critics`, `several
sources`, open-ended `such as`.

Repair: name, date, document. If none exists, cut the claim.

### 1.5 Copula avoidance
`serves as`, `functions as`, `represents`, `stands as`, `operates as`, `boasts`,
`features`, `maintains`. A paragraph that never once uses `is` or `has` is the tell,
not any single instance.

### 1.6 Negative parallelism
`not only X but also Y`. `It's not X, it's Y`. `No X, no Y, just Z`. `X rather than Y`
used for false depth.

Repair: drop the rejected half, keep the claim. The contrast survives only when Y is
concrete and the text actually delivers Y.

### 1.7 Rule of three
Adjective, adjective, adjective. Short phrase, short phrase, and short phrase. The
third item is usually filler or a synonym of the second.

Human rhetoric uses tricolon. Attack filler triples and stacked three-item lists, not
every group of three.

### 1.8 Trailing negation
A fragment glued to a finished sentence: `..., no guessing.` `..., no wasted motion.`

Repair: real subordinate clause, or cut.

### 1.9 Em dash and en dash
`—` and `–`, spaced or unspaced.

For attribution this is weak evidence on its own; it is a house-style choice in much
human writing and recent models suppress it. For delivery, remove them: period, comma,
colon, parentheses, or split the sentence. One remaining dash means the pass is not
finished.

In languages where the em dash is not native punctuation (Turkish, for one), a hit is a
much stronger tell.

### 1.10 Formatting tells
Bold on every key term. `- **Header:** sentence` list items. Title Case headings.
Decorative emoji on headings or bullets. A `---` between every section. A one-row table
for a single statistic. Hyphenated compounds kept hyphenated in predicate position
(`the team is cross-functional`).

### 1.11 Filler and hedging
`in order to`, `due to the fact that`, `it is important to note that`, `at this point
in time`, `has the ability to`. Stacked hedges: `could potentially possibly be argued`.

One instance is human. Density is the tell.

### 1.12 Signposting and closers
`Let's dive in`, `here's what you need to know`, `without further ado`, `In today's
fast-paced world`, `In conclusion`, `The future looks bright`, `Only time will tell`.

Repair: do the work instead of announcing it. End on the last concrete point.

### 1.13 Chatbot residue
`I hope this helps`, `Certainly!`, `Would you like me to`, `Here is a`, `As an AI`,
`As of my last knowledge update`, `While specific details are limited`.
Placeholders: `[Your Name]`, `INSERT_`, `TODO`, `2026-XX-XX`.

Any of these in delivered text means the draft was never read before sending.

### 1.14 Vendor artifacts
`contentReference`, `oaicite`, `turn0search`, `[cite: 1]`, `【85†L261】`,
`utm_source=chatgpt.com`, `?referrer=grok.com`.

### 1.15 Manufactured cadence
Every sentence 15-25 words. No sentence under eight. Every paragraph the same height.
Or the opposite failure: engineered staccato, three fragments in a row for drama.

Repair: mix. Do not force fragments; even, mid-length rhythm is itself the tell.

### 1.16 Portability test
If a sentence transfers to a different company, person, or product without changing a
word, it is filler. Replace it with something only true here: a number, a name, a
mechanism, a consequence.

---

## 2. Discourse layer

Only for text long enough to have structure (see §0). These come from measurement, not
taste: narrative features alone separated human from AI text at 93.2% macro-F1, keeping
over 97% of the performance of models that also saw stylistic cues.

### 2.1 Over-explanation
The text states its own meaning instead of letting it land. The narrator, or the
writer's voice, interprets the events for the reader.

> "The pattern is one of over-determination: AI spells out meaning rather than trusting
> the reader to infer it."

Repair: cut the interpreting sentence. If the point does not survive without it, the
material underneath is too thin. Fix that instead.

### 2.2 Tidy single track
One thread, no side matter, few loose ends, everything resolved, the protagonist solves
the problem through their own effort.

> "AI favors single-track narratives with fewer loose ends; human stories are messier,
> with time jumps and disjointed causal chains."

Repair: allow one thing to stay unresolved. Let a cause come from outside the
protagonist. Do not manufacture chaos. The tell is the absence of any, not the amount.

### 2.3 Flat time
Strict chronology, evenly spaced. Human text jumps: flashback, aside, a fact recalled
out of order.

### 2.4 Moral tidiness
Choices are clearly right or clearly wrong. Human text leaves more choices genuinely
arguable.

### 2.5 Over-embodiment
This one inverts the usual advice. AI renders emotion through the body; people often
just name the feeling.

> "Where a human author might write that a character 'felt afraid', AI renders fear as
> a tightening chest, cold sweat, and dimming lamplight."

Measured: embodied emotional expression appeared in 81% of AI stories against 38% of
human ones.

Repair: for text produced by a model, "show, don't tell" is already over-applied. Name
the feeling plainly at least as often as you stage it.

### 2.6 No reader in the room
Human writing acknowledges someone is reading. AI writes as if unobserved.

> "Human writing acknowledges its audience as a co-participant; AI writes as though no
> one is watching."

See §3.1. This collides with a surface rule, and the collision has to be resolved
deliberately rather than by whichever rule is checked first.

---

## 3. Where the layers collide

### 3.1 Addressing the reader
Surface layer bans the performed opener: `Look,` `Here's the thing`, `Let's be honest`,
`Real talk`. Discourse layer records reader-address as a human signal.

Both are right about different things. The banned versions are hooks: an intimacy
gesture with nothing behind it. The human signal is an actual aside: a concession, a
correction, an admission the reader might disagree.

Rule: an aside that carries information stays. An aside that only sets a tone goes.

### 3.2 Show versus tell
Surface guidance says be concrete. Discourse measurement says AI is already too
concrete about bodies and sensation. Concrete about facts, plain about feelings.

### 3.3 Structure versus rhythm
Surface layer wants varied sentence length. Discourse layer wants varied narrative
shape. Fixing rhythm alone produces text that reads lively and is still built like a
machine built it.

---

## 4. Short forms

Most of the surface layer assumes prose. On very short text it produces false hits.

**Direct message (1-4 lines).** Live rules: 1.6, 1.9, 1.12, 1.13, 1.16, and reader
address. Dead rules: rule of three (there is no room), cadence (too few sentences),
formatting. A DM that passes every prose rule and still opens with a compliment about
their page is a template, and the portability test is what catches it.

**Carousel slide (5-25 words).** Only 1.1, 1.2, 1.9, 1.13 apply. Judge the deck as one
unit: if every slide has the same grammatical shape, that is the tell, not any slide.

**Spoken script.** Skip formatting and citation rules entirely. Keep 1.6, 1.7, 1.11,
1.12, 1.15, 2.1. Add: read it out loud. A clause you cannot say in one breath will not
survive the camera. Written-only punctuation (semicolons, parentheticals, dashes) has
no spoken equivalent and comes out as a stumble.

**Caption.** Surface layer in full. The first line carries the whole job; apply 1.12
hard to it.

---

## 5. Process

1. Draft first. Never compose against this list. You get constrained, lifeless text.
2. Pick the layer (§0).
3. Mark hits. Rule number, exact sentence.
4. Stack overlapping hits on one sentence as a single finding, not three.
5. Repair by replacement, not deletion. Meaning is preserved; inflation is not.
6. Read it aloud.
7. Report what changed and what is still unresolved.

Output:

```
AUDIT
  Type / length: <DM | slide | script | caption | long>
  Layers run: surface [+ discourse]
  Hits:
    1.6  "It's not about the posts, it's about the follow-up."
    2.1  "This is what separates coaches who grow from coaches who stall."
  Stacked: 1.1+1.7 in one sentence, counted once
  Rewrite: <full text>
  Unresolved: <or none>
```

Never claim a count you did not count.

---

## 6. What is not a tell

Perfect grammar. Mixed register. Boring but clean prose. A single academic word. One
`however`. A single em dash in English prose. Unsourced web copy. Clean template
formatting. Text written before late 2022.

Non-native English writers get flagged by several of these rules for reasons that have
nothing to do with machines: synonym cycling to avoid repetition, formal register,
careful hedging. Weigh the cluster, never a lone hit.

## 7. What to protect

Detail too specific to invent. Unresolved tension. Mixed feeling. A defensible editorial
choice. Self-correction mid-paragraph. Plain verbs: `wrote` not `authored`, `used` not
`utilized`, `died` not `passed away`. Slang tied to a year.

Preserving these is not the same as leaving AI tells in place. Keep the human detail,
strip the vocabulary cluster.

## 8. Anti-overfit

If the word is exactly right and has no substitute, keep it. Do not turn every paragraph
into one sentence. Do not break every triple. Do not inject a fabricated anecdote,
interview, or named person to sound human. That is a worse failure than the tell it
replaces.

The test: is this what the writer would have written, or is this a machine performing
not being a machine? If the second, simplify. If it reads generic, specificity is
missing, not personality.

---

## Sources

- Wikipedia, *Signs of AI writing* (WikiProject AI Cleanup). Observation, not policy.
  Scope note in the source: the guide covers informational writing and excludes tells
  specific to fiction.
- Russell, Rajendhran, Pham, Iyyer, Wieting. *StoryScope: Investigating idiosyncrasies
  in AI fiction.* COLM 2026. 10,272 prompts, 61,608 stories, 304 features per story,
  five models. Scope note in the source: stories average ~5,000 words, and shorter texts
  cannot support the features extracted.
- Surface repair patterns consolidated from working style guides; deduplicated against
  the two sources above.

Both scope notes are load-bearing. The layer split in §0 exists because neither source
claims what this skill would otherwise assume.
