---
name: ai-writing-audit
description: >
  Audit and repair text that reads as machine written. Any length, any format: a two line
  direct message, an automated message sequence, an objection reply, a caption, a carousel
  slide, a spoken script, a landing page, an essay. Runs two layers, surface tells and
  discourse tells, behind a false positive gate, and returns findings with a repair for
  each. Use on an existing draft. Do not use to compose a first draft.
license: CC-BY-SA-4.0
---

# AI writing audit

## What this returns, and what it will not claim

This skill answers one question: **does this text read as machine written, and where.**

It does not answer whether a machine wrote it. That is a different question and the
evidence says nobody answers it reliably. The source guide records a 2025 study finding
human accuracy at chance level, a second study at 57 percent on AI text, and a preprint
putting heavy model users at about 90 percent, which still means one false accusation in
ten. Detector tools are described in the same source as having non-trivial error rates and
as breaking under paraphrase, markup changes, or an unfamiliar model.

So the verdict is about reading, not authorship. Never write "this was AI generated". Write
"these seven patterns read as machine written, here is the repair for each".

## The two layers

**Surface layer.** Word choice, sentence shape, punctuation, formatting. Catalogued in
`references/surface-tells.md`, built from Wikipedia's "Signs of AI writing" field guide.
Cheap to detect and cheap to fix, which is also its weakness: these signatures get removed
by each new model generation and by a single editing pass.

**Discourse layer.** Theme, causality, time, agency, stance. Catalogued in
`references/discourse-tells.md`, built from StoryScope (COLM 2026), which measured 61,608
stories and reached 93.2 macro-F1 on human versus machine using narrative structure alone,
with zero style signals. Its conclusion states the reason this layer exists: surface
signatures are transient and post-editable, while narrative features require structural
rewrites to change.

Measured together in that paper: a style-only model scored 85.8 and a 30 feature narrative
model scored 84.8. Within a point of each other. Neither layer is sufficient, so run both,
and never report a pass from one layer alone.

**The gate.** `references/false-positives.md` holds the patterns that look like tells and
are not, the constructions that lean human, and the confidence each format deserves. Every
finding passes through it before it reaches the output.

The sources disagree with each other and with the tools built on them.
`references/conflicts.md` lists every disagreement and the ruling this skill applies. Four
of those rulings are load bearing and are repeated here, because getting them wrong changes
the output rather than refining it.

## Two modes, and they are not the same question

**Deliverable mode, the default.** The text belongs to the person asking. The goal is a
better text. A single hit is worth fixing when the fix costs nothing, no cluster required,
and no claim about authorship is made or needed.

**Assessment mode.** The text came from somewhere else and the question is how it reads. A
single hit supports nothing. Clusters across several distinct categories are the bar, five
or more categories before the reading verdict means much, and the cautions in
`references/false-positives.md` about false accusations apply in full.

Say which mode ran. The same text can pass one and fail the other without either being
wrong.

## The rule that outranks every other rule here

**Never add anything to a text that was not true of it.**

No invented first person. No anecdote that did not happen. No opinion the writer did not
hold. No source, statistic, name, or number that was not already there or supplied by the
writer.

Some cleanup tools, when given no writing sample, fall back on manufacturing a voice: add
uncertainty, add a personal aside, add an admission. That produces text that reads more
human and states things that are false, which in marketing copy is a false claim about a
real business.

When a draft is clean, flat, and voiceless, report it as a finding. Ask for the missing
specific. Do not fill the hole yourself. Voice can be matched from a sample, and it cannot
be invented from nothing.

## Optional input: a voice sample

If the writer supplies two or three samples of their own past writing, use them. Sample
evidence outranks every generic list in this skill.

Measure the samples before auditing: sentence length spread, dash and punctuation habits,
paragraph length, opening moves, recurring phrases, whether they use contractions,
fragments, emoji, first person. Then build a protect list from the result.

The reason this matters: a real writer's tics look like machine filler to a generic pass.
Spoken glue, a repeated stock phrase, an unusual dash habit, an "okay?" every few lines. A
generic sweep strips exactly the things that make the text theirs. Anything on the protect
list is weight 0 for that writer, and stripping it is a finding against the audit rather
than against the text.

Without samples, run the generic lists and say in the verdict that no sample was available.

## Run it

### Pass 0. Profile the text

Name the format. Open `references/formats.md` and load its profile. If the format is not
listed, answer the four questions at the end of that file and write the derived profile
into the output so the reader can argue with it.

One piece can hold two formats. A short video ships as a spoken script plus a written
caption, and those get different passes: the script gets the spoken profile with the word
list demoted, the caption gets the full written pass. Audit them separately and say so.

Check the language. The discourse checks and the formatting checks work in any language. The
vocabulary lists were measured on English tokens and do not survive translation. For text in
another language, run both other layers, report the vocabulary layer as not run, and build a
local list only from observed output in that language rather than by translating this one.

Ask for provenance if it is unknown and cheap to get. If the text predates 30 November
2022, machine authorship is ruled out by date and the audit becomes a writing review only.

Count the words. The count sets which layer leads:

| Words | Layer that leads | Discourse checks that run |
|---|---|---|
| Under 60 | Surface | Specificity, stance, self-explaining last line |
| 60 to 300 | Both, equal | The format profile's list |
| 300 to 800 | Both, discourse rising | Full carry-over table |
| Over 800 | Discourse | Full carry-over table, surface as supporting evidence |

### Pass 1. Surface sweep

Go through `references/surface-tells.md` and mark hits with exact quotes and positions.
Mark, do not fix yet. Fixing during the sweep hides the density, and density is the finding.

Weight each hit:

- **Weight 2, hard.** Documented, specific, and rare in unedited human writing: the flagged
  vocabulary items, negative parallelism, vague attribution, participial pseudo-analysis,
  promotional register with no fact under it, self-summarizing conclusions, formatting
  artifacts from a chat interface.
- **Weight 1, weak.** Real but common in human writing: dash density, the rule of three,
  a symmetrical pair, boldface as texture, one transition word.
- **Weight 0, never counted.** The ineffective indicator list in the gate file. Perfect
  grammar, formal prose, bland prose, mixed register, a transition word on its own. Do not
  raise these as findings, in any format, at any length.

### Pass 2. Discourse sweep

Run the carry-over table in `references/discourse-tells.md` at the depth Pass 0 set. Eight
checks in full:

1. **Self-explaining.** Does the text state its own lesson, moral, or significance rather
   than leave it to the reader.
2. **Single track.** Does everything pull one way, with no aside, exception, or second
   thread.
3. **Tidy causality.** Does each sentence follow cleanly from the last, with no gap,
   reversal, or admitted cost.
4. **Internal resolution.** Does it end by asking the reader to decide, realize, or commit,
   rather than to do something external and small.
5. **Moral polarity.** Is every actor clearly right or clearly wrong, with nothing
   ambivalent.
6. **Named reference.** Are there real names, numbers, dates, places, tools. Or only
   diffuse echoes of them.
7. **Emotion handling.** Are feelings delivered as body sensations by default. The paper
   found embodied emotional expression is the machine-leaning value and an explicit label
   is the human-leaning one, which reverses the usual "show, do not tell" instruction.
   Judge the default, not one instance.
8. **Order.** Is the text told in the flattest possible order, when the material had another
   one available.

Do not run the fiction-only features on non-fiction. `references/discourse-tells.md` lists
which ones stay in fiction and why porting them produces nonsense.

### Pass 3. Gate

For every finding, three questions:

1. Is it on the ineffective list. If yes, delete the finding.
2. Does the format profile call it native. If yes, delete the finding.
3. Is it a construction the source records as leaning human. Plain verbs, "there is a",
   "in order to", "the fact that", "very", "perhaps", a superlative. If yes, delete the
   finding, and if the draft is thin on these, note it as a repair opportunity rather than
   a fault. Sanding these off makes the text more machine-like, not less.

Then score. Density is weighted findings per 100 words:

| Density | Verdict |
|---|---|
| Under 1.0 | Reads human |
| 1.0 to 3.0 | Mixed |
| Over 3.0 | Reads machine |

For text under 60 words the denominator is unstable, so score by count: 0 to 1 weighted
findings reads human, 2 to 3 mixed, 4 and above reads machine.

These cutoffs are a judgment call layered on top of descriptive sources, not a measured
threshold. The source page says of itself that it is descriptive, not prescriptive, a list
of observations rather than rules. Say so when the score is close to a boundary.

### Pass 4. Repair

The rule that governs every repair, from the source guide: the patterns are potential signs
of a problem, not the problem itself, and treating the signs as the thing to fix "could
just make detection harder".

So, in order:

1. **Cut first.** Most findings are sentences doing no work. Deleting is the repair. Do not
   replace a hollow sentence with a better hollow sentence.
2. **If it stays, put something under it.** A flagged promotional line needs a fact, a
   number, a name, or a cut. A synonym pass leaves the text empty and clean, which is the
   failure mode this skill exists to prevent.
3. **Repair the discourse findings before the surface findings.** Surface repairs on a
   single-track text produce a polished single-track text. The reverse order wastes work,
   because restructuring rewrites the sentences anyway.
4. **Change one thing per finding.** Keep the writer's voice, the argument, the offer, and
   the facts. This skill has no mandate to change what the text says.
5. **Do not add a tell while removing one.** The common accident is replacing a banned word
   with a rhetorical flourish, replacing a dash with a colon everywhere, or replacing a
   summary line with a rhetorical question.
6. **Leave the roughness.** If the draft has a plain verb, an abrupt sentence, a small
   digression, or an unbalanced rhythm, that is the human signal. Protect it.
7. **Never insert rhythm the draft did not have.** Varying sentence length is a repair for a
   metronome cadence that is already present. It is not a style to apply on top. Do not add
   a fragment, an aside, or a one-line paragraph that this writer's voice did not already
   contain. A text that reads as a machine trying not to read as a machine has traded one
   pattern for a worse one.
8. **Add nothing that was not true.** See the rule above the passes. This is where it gets
   broken, and it is the one repair failure this skill treats as disqualifying.

### Pass 5. Report

```
MODE: deliverable | assessment
FORMAT: <name> (<derived / from profile list>)
LENGTH: <n> words        LANGUAGE: <name> (vocabulary layer: run / not run)
VOICE SAMPLE: yes, <n> samples | none supplied
CONFIDENCE: <from the confidence table in false-positives.md>
VERDICT: reads human | mixed | reads machine   (density <x.x> per 100 words)

FINDINGS
1. [surface, w2] "<exact quote>"
   Tell: <name from the catalogue>
   Why: <one line>
   Repair: "<replacement, or CUT>"
2. [discourse, w2] <check name>
   Evidence: <quote or structural description>
   Repair: <what to restructure>
...

GATED (looked like findings, are not)
- "<quote>" : <which gate rule cleared it>

WHAT IS WORKING
- <the human-leaning constructions present, so the next edit does not remove them>

REWRITE
<the repaired text in full, if a rewrite was asked for>
```

Always print the GATED section, even when empty. It is what stops the audit turning into a
machine that finds seven problems in every text regardless of the text.

Print WHAT IS WORKING before the rewrite. An audit that only subtracts trains the next
draft toward the safe middle, and the safe middle is where the measured machine cluster
sits.

## Where this skill is guessing

Say this out loud in the verdict rather than hiding it.

The surface catalogue was built on Wikipedia articles and openly states that some of its
signs may not apply outside that context, and that it is less useful for text which is not
informational writing. The discourse layer was built on roughly 5,000 word fiction and its
features come from a narratological taxonomy. Neither source measured a direct message, a
caption, a slide, an ad, an email, or a spoken script.

For those formats this skill is running an argued transfer. Each carry-over in
`references/discourse-tells.md` states the reasoning that carries it, so the reasoning can
be checked. Anything that does not transfer is listed as fiction-only and is not applied.

One more limit that grows over time: human writing and speech are measurably drifting
toward model output, with a 2024 study finding significant influence in conversational
podcasts. Every word list on this page ages. The structural checks age more slowly, which
is the argument for keeping the discourse layer even when it is the harder pass to run.

## This file follows its own rules

Checkable, and checked. Across this file and the four references: no em dash, no en dash, no
curly quotation mark or apostrophe, no heading in title case, no section that summarizes the
section above it, no conclusion restating the page, and no vocabulary-list word outside a
quoted example or the list itself. Those are greppable and were grepped.

One tell does appear here, deliberately. These files use inline-header lists, a bold label
followed by a description, which the catalogue scores weight 2 in prose. The gate clears it
for reference documents, and the reason is in the source: the guide traces the habit to
readmes, how-tos, and specifications, meaning the models copied it from documents where it
was already the convention. That is the honest version. Claiming the files contain no flagged
pattern at all would have been the dishonest one.

Note also that this file does not ban the em dash. It contains none as a demonstration that
the constraint is livable, while the rule it hands you is a density rule. The reasoning is
in `references/conflicts.md`, item 2.

If you extend this skill, run the audit on your addition first, and add a case to `TESTS.md`
for any format you make a claim about. A tool that fails its own check is evidence against
every claim it makes.
