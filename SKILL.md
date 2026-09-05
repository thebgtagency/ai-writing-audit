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
rewrites to change. The measured rate, weight, and repair for each discourse check are in
"Research-backed tells" below, and that section also carries the two procedure rules the
same paper measured.

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
single hit supports nothing. Spread is the bar: findings touching four or more of the seven
measured themes in "Research-backed tells" below, before the reading verdict means much. The
cautions in `references/false-positives.md` about false accusations apply in full, and so
does the measured floor: on 5,000 word fiction, with a purpose-built classifier, about one
human text in nine still came back as machine written.

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
| Under 60 | Surface | Checks 1, 5 and 6 only: self-explaining, moral polarity, named reference |
| 60 to 300 | Both, equal | The format profile's list. Check 10 needs two facts in sequence and often stays silent here, which is a silence and not a pass |
| 300 to 800 | Both, discourse rising | All ten, full carry-over table |
| Over 800 | Discourse | All ten, full carry-over table, surface as supporting evidence |

Below 60 words the seven theme bar cannot be met, because three checks cannot touch four
themes. So assessment mode has no verdict to give on a short text, and says that instead of
lowering the bar. Deliverable mode still runs and still repairs.

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

Before the checks, build the structural template. The paper measured that inducing features
from raw prose and inducing them from a structured template of the same text return
different feature sets, only 6 of the top 20 overlapping, and that the prose route returns
style features while the template route returns structural ones. Fill the template in
"Research-backed tells" below, mark every absent field null, then run the checks against the
template. Quote the prose only to evidence a finding.

Run each check as its own pass. Applying the paper's features in one call covered 68.4
percent of them against 95.4 percent one dimension at a time, and the loss concentrated in
revelation and temporal structure, which is where checks 8, 9 and 10 live. A single sweep
under-detects the human-leaning signals specifically.

Run the carry-over table in `references/discourse-tells.md` at the depth Pass 0 set. Ten
checks in full, weights from "Research-backed tells" below:

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
9. **Reader address.** Does the text know it is being read. Machine text writes as though no
   one is watching. The check has two halves and they behave differently, so run them apart.
   The *second person* half is inert in every format this skill profiles, because a message,
   caption, ad, script, email or page is already written in second person, so its presence
   and its absence both carry nothing. Score it only in a format whose default register is
   third person, and none of the nine profiles in `references/formats.md` is one. Across
   fourteen recorded runs it has never produced a finding, and that is by construction.
   The *medium naming* half does fire here: "this is a cold message", "last one from me",
   "ignore this if it is not live". It fires in the human direction, so its absence is a
   note and never a fault, and its presence belongs in WHAT IS WORKING.
10. **Recontextualization.** Does any later line change what an earlier line meant. Machine
   text discloses in the order it was assembled, so nothing arrives that forces a re-reading.
   Absence is common in human writing too, so this one is evidence and never a verdict.

Every discourse finding carries the theme it belongs to, because Pass 3 scores spread and
spread is not reproducible without this mapping. The themes are numbered as they appear in
"Research-backed tells" below.

| Check | Theme |
|---|---|
| 1. Self-explaining | 1, thematic over-determination |
| 2. Single track | 1 when the complaint is thematic unity, 3 when it is the missing second thread |
| 3. Tidy causality | 3, structural streamlining |
| 4. Internal resolution | 3, structural streamlining |
| 5. Moral polarity | 7, narrative diversity |
| 6. Named reference | 4, intertextual richness |
| 7. Emotion handling | 2 when feeling arrives as a body sensation, 7 when no feeling is named at all |
| 8. Order | 6, temporal complexity |
| 9. Reader address | 5, reader engagement |
| 10. Recontextualization | 6, temporal complexity |

Three consequences worth reading off the table. Ten checks cover seven themes, so themes 1,
3, 6 and 7 can each be reached by more than one check and a second hit inside a theme adds
density without adding spread. The three checks eligible below 60 words reach themes 1, 4 and
7 only, which is the arithmetic behind the rule in Pass 0 that assessment mode has no verdict
at that length. And theme 5 is reachable only through check 9, whose scored half is inert in
every format profiled here, so in practice the bar is four themes drawn from six rather than
seven. That makes the bar harder than it looks, which is the right direction for a threshold
that gates an origin claim.

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
4. For a discourse finding, is the human rate for that feature already high. Three of the
   highest ranked machine-leaning features sit close to the human value: thematic unity 4.41
   against 4.74, causal continuity 3.92 against 4.20, moral weighting 3.26 against 3.68, all
   on a 1 to 5 scale. Keep the finding, label it weak, and never let one of these carry a
   verdict on its own. Compare with emotion carried by the body, 38 against 81, which is a
   real separation.

Then score. Density is weighted findings per 100 words:

| Density | Verdict |
|---|---|
| Under 1.0 | Reads human |
| 1.0 to 3.0 | Mixed |
| Over 3.0 | Reads machine |

For text under 60 words the denominator is unstable, so score by count: 0 to 1 weighted
findings reads human, 2 to 3 mixed, 4 and above reads machine.

In assessment mode, density is not enough and spread decides. The paper groups its 30 core
features into seven themes, three machine-leaning and four human-leaning. Count how many of
those seven the findings touch. Hits in four or more, with at least one weight 2 hit in
each, before a reading verdict means anything about a text you did not write. A high density
inside one theme is a writing problem, not a reading verdict. The seven themes are the
paper's. The number four is this skill's.

In deliverable mode the bar does not apply and spread is reported without gating anything.
The text belongs to the person asking, no origin claim is being made, and a single weight 2
hit is worth repairing whether or not six other themes are clean. Print the spread line
anyway, because it tells the writer whether they have one habit or several.

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
MODEL: <named, if the draft's author is known> | unknown
VERDICT: reads human | mixed | reads machine
         (density <x.x> per 100 words, spread <n> of 7 themes)

STRUCTURAL TEMPLATE, filled before the discourse checks
agents: <who acts, or null>
events: <what happens, or null>
causality: <the chain, or null>
revelation: <what is withheld and when it lands, or null>
temporal order: <linear, nonlinear, mixed>
setting: <where, or null>

FINDINGS
1. [surface, w2] "<exact quote>"
   Tell: <name from the catalogue>
   Why: <one line>
   Repair: "<replacement, or CUT>"
2. [discourse, w2, theme <n>] <check number and name>
   Evidence: <quote or structural description>
   Repair: <what to restructure>
3. [discourse, w1, theme <n>, WEAK] <check number and name>
   Weak because the human mean on this feature is already high. Cannot carry a verdict.
...

GATED (looked like findings, are not)
- "<quote>" : <which gate rule cleared it>

THEME SPREAD: <which of the seven, and whether each carries a weight 2 hit>

WHAT IS WORKING
- <the human-leaning constructions present, so the next edit does not remove them>
- <every discourse check that fired in the human direction, named by number>

REWRITE
<the repaired text in full, if a rewrite was asked for>
```

Always print the GATED section, even when empty. It is what stops the audit turning into a
machine that finds seven problems in every text regardless of the text.

Print WHAT IS WORKING before the rewrite. An audit that only subtracts trains the next
draft toward the safe middle, and the safe middle is where the measured machine cluster
sits.

## Research-backed tells (arXiv 2604.03136)

Source: Russell, Rajendhran, Pham, Iyyer, Wieting. "StoryScope: Investigating idiosyncrasies
in AI fiction." COLM 2026, arXiv 2604.03136v6. Page numbers below are the printed page of
that PDF.

This section does two things the rest of the skill does not. It puts a measured number and a
weight on each discourse check, taken from the paper's own ranking rather than from taste.
And it fixes two procedure defects that the paper measured directly.

Nothing here claims a text was machine written. Every rate below is a rate, and the human
column is never zero.

### How weight is set here

The paper ranks its 30 core features by a core score, mean SHAP multiplied by a stability
score and by one plus the absolute human-AI gap (Appendix I, p.23). That ranking is the
paper's. The mapping to weights is this skill's:

- **Weight 2.** Top 10 of the AI-characterizing list (Table 14, p.24) or top 6 of the
  human-characterizing list (Table 15, p.25).
- **Weight 1.** Any other member of the 30.
- **Weight 0.** Anything on the fiction-only list in `discourse-tells.md`, whatever its rank.

A human-leaning feature is never a fault. Its absence is a repair opportunity, and stripping
it is a finding against the audit.

### Read the human column, not only the gap

Three of the highest ranked AI-elevated features sit high for humans too: Thematic Unity
4.41 human against 4.74 AI, Causal Chain Continuity 3.92 against 4.20, Moral and
Philosophical Weighting 3.26 against 3.68, all on a 1 to 5 scale (Table 16, p.26). A hit on
one of these is weak evidence, because human writing does close to the same thing. Compare
that with emotion carried by the body, 38 percent human against 81 percent AI, which is the
widest separation in the whole table. Say which kind of hit you have.

### Two procedure changes the paper forces

**Run the discourse checks one dimension at a time.** The paper compared applying its
features in a single call against applying them one narrative dimension per call. Coverage
rose from 68.4 percent of features to 95.4 percent, and the single-call dropout was
concentrated in revelation and temporal structure (Appendix C, p.18). Those are the two
dimensions carrying most of the human-leaning checks, so a single-sweep audit under-detects
exactly the signals that argue a text is human. Run the ten checks as ten passes.

**Abstract the text before running the discourse pass.** The paper compared inducing
features from raw prose against inducing them from a structured template of the same story.
Of the top 20 discriminative features, only 6 overlapped: the raw-prose variant produced
style-heavy features (humor, vocabulary register, allusion types, dominant imagery), the
template variant produced structure-heavy ones (emotional arcs, relationship trajectories,
event density, flashback usage). Appendix B, p.17. Auditing the prose directly returns
surface findings wearing a structural label.

The paper prints the template it used, so the summary step does not have to be improvised.
Figure 8, p.28 to p.30, fields condensed:

| Group | Fields |
|---|---|
| agents | major characters with role, attributes, emotion trajectory, motivation trajectory, trope. Supporting characters with a one-line role |
| social network | enduring bonds, as `A-B: relationship type and quality` |
| events | ordered beats with who, where, what, when. Causal links as `event1 -> event2: explanation`. Narrative schema |
| plot | themes, summary, moral, central obstacle, central conflict, archetype, plot arc |
| setting | locations with scope, time period, atmosphere |
| revelation | what is withheld for suspense, what causal antecedents are withheld, what was revealed and when |
| temporal order | linear, nonlinear or mixed. Duration, flashbacks, time jumps, scene durations |
| perspective | point of view, focalization by section, who speaks |
| style | allusions, figurative language, imagery, sentence complexity, evaluative language |

Three instructions travel with it and matter as much as the fields. Stay inside what the
text conveys and do not interpret past it. Write `null` for anything not present. Mark each
field as story-level or section-level.

The `null` rule is the one to keep for non-fiction. A draft that returns null for revelation,
for causal links, for supporting agents and for time jumps has told you what the discourse
pass is about to find, before the pass runs. Fill the template first, then audit the
template, then quote the prose only to evidence a finding.

### AI-elevated: thematic over-determination

Table 16 group 1, p.26. Section 4.1, p.7.

| Test, answerable yes or no | Human | AI | Weight | Repair |
|---|---|---|---|---|
| Does a sentence state the text's own point, lesson, or significance | 3.28 | 3.94 | 2 | Cut it. If the point does not survive the cut, it was not in the text |
| Does the writer step outside the material to comment on what it means | 52% | 77% | 2 | Cut, or replace with the fact that would let a reader conclude it |
| Does everything pull one way, with no aside and no exception | 4.41 | 4.74 | 2 | Restore the detail that was cut for being off-point |
| Is a moral or philosophical question foregrounded | 3.26 | 3.68 | 1 | Demote it under the concrete case |
| Do quoted words exist mainly to argue a position | 34% | 59% | 1 | Give the speaker something to do besides hold a view |
| Do references stay vague allusions rather than named things | 50% | 72% | 1 | Name the source, or cut the gesture |

Scale rows are means on 1 to 5. Percentage rows are the share of stories carrying that value.

### AI-elevated: sensory and embodied performativity

Table 16 group 2, p.26. Section 4.1, p.7.

| Test, answerable yes or no | Human | AI | Weight | Repair |
|---|---|---|---|---|
| Is feeling delivered by default as a body sensation or bodily metaphor | 38% | 81% | 2 | Name the feeling and move on |
| Is the physical setting doing the work of the inner state | 3.58 | 4.07 | 2, fiction only | Not applied outside fiction |
| Is sensory description dense throughout | 3.66 | 3.93 | 2, fiction only | Not applied outside fiction |
| Is smell used as imagery | 57% | 82% | 1, fiction only | Not applied outside fiction |

The first row is the widest gap in the paper, 42 points, and it is the measured reversal of
"show, do not tell" already ruled on in `conflicts.md` item 9. This section raises the
confidence on that ruling rather than changing it. Verbatim, p.7:

> Where a human author might write that a character "felt afraid," AI renders fear as a
> tightening chest, cold sweat, and dimming lamplight.

Judge the default across the text, not one instance.

### AI-elevated: structural streamlining

Table 16 group 3, p.26. Section 4.1, p.7.

| Test, answerable yes or no | Human | AI | Weight | Repair |
|---|---|---|---|---|
| Does every sentence follow cleanly from the last, no gap, no reversal | 3.92 | 4.20 | 2 | Admit the cost, the exception, or the step that failed |
| Does the close turn on the reader's own choice or will | 46% | 69% | 2 | Ask for an external act, small and checkable |
| Does the text run one thread with no second thread at all | 57% | 79% | 1 | Restore the second thread if one existed |
| Does it end in understanding or acceptance rather than an action | 27% | 47% | 1 | End on the thing to do, not the thing to realize |
| Is the central figure introduced by outside description | 30% | 52% | 1, fiction only | Not applied outside fiction |

### Human-elevated: intertextual richness

Table 16 group 4, p.26. Section 4.1, p.7. Absence is the finding, never presence.

| Test | Human | AI | Weight | If absent |
|---|---|---|---|---|
| Does the text name a specific text, author, tool, brand, place, or number | 47% | 24% | 2 | Ask the writer for the specific. Do not supply one |
| Does it mix named references with looser ones rather than only gesturing | 37% | 16% | 2 | Same |

The paper's wording, p.7: AI "generally sticks to vague allusions and avoids naming real
brands, places, or works."

### Human-elevated: reader engagement

Table 16 group 5, p.26. Section 4.1, p.7.

| Test | Human | AI | Weight | If absent |
|---|---|---|---|---|
| Does the text name its own medium or situation | 67% | 39% | 2, positive only | Add nothing. Record as a flat register |
| Does it address the reader as a party who is present | 28% | 7% | inert here, see below | Not scored |

This is the group that does not survive the transfer intact, and check 9 in Pass 2 is split
for that reason. The paper measured both rows on fiction, where third person is the default
and turning to the reader is rare enough to mean something. In a message, caption, ad,
script, email or product page, second person is the native register, so its presence and its
absence both carry nothing. None of the nine profiles in `references/formats.md` has third
person as its default, so the second row cannot be scored anywhere this skill currently runs,
and across fourteen recorded runs it never has been.

The first row does transfer, because naming the medium is a choice in any format: "this is a
cold message", "last one from me", "ignore this if it is not live". It runs in the human
direction only. Its presence goes in WHAT IS WORKING and its absence is a note, never a
fault. Theme 5 is therefore reachable only as a positive, which is why the practical spread
ceiling is six themes and not seven.

The paper's line, p.7: "AI writes as though no one is watching."

### Human-elevated: temporal complexity

Table 16 group 6, p.26. Section 4.1, p.7.

| Test | Human | AI | Weight | If absent |
|---|---|---|---|---|
| Does a later line force a re-reading of an earlier one | 3.28 | 2.95 | 2 | Note the missing turn. Do not invent one |
| Does the text jump across time | 2.40 | 2.12 | 1 | Note flat order |
| Is any disclosure staged out of order | 1.96 | 1.68 | 1 | Same |
| Does it use a flashback or a flash-forward | 2.58 | 2.31 | 1 | Same |

The first row is new to this skill. It was in the paper's human core list (Table 15 row 4,
p.25) and had no matching check in Pass 2. Non-fiction form: a later fact that changes what
an earlier sentence meant. All four means sit in the low middle of the scale for both
sources, so absence here is common in human writing too.

### Human-elevated: narrative diversity

Table 16 group 7, p.26. Section 4.1, p.8.

| Test | Human | AI | Weight | If absent |
|---|---|---|---|---|
| Is the central figure allowed to be partly wrong | 59% | 38% | 1 | Ask for the cost or the case where it failed |
| Is any feeling named plainly rather than performed | 29% | 8% | 1 | Pair with the embodied row above, same feature |
| Where a second thread exists, does it run parallel to the main one | 42% | 21% | 1 | Note it |
| Does the text move across more than one setting | 1.34 | 1.08 | 1, fiction only | Not applied outside fiction |

The third row corrects a reading that is easy to get backwards. The AI tell is having no
second thread at all, 79 percent against 57 percent. Among texts that do have one, running
it parallel to the main line is the human-leaning value, 42 percent against 21 percent. So
"everything connects" is not by itself the tell. "There is only one thing" is.

### Scoring by cluster

The paper groups its 30 core features into seven themes, three AI-elevated and four
human-elevated (Table 16, p.26). Those seven are the categories to count in assessment mode.

This replaces an invented number. `conflicts.md` item 6 sets the assessment bar at five or
more distinct categories and states plainly that the number is this skill's, not a source's.
The seven themes above are a measured grouping, so the bar can be restated against them:
hits spread across four or more of the seven themes, with at least one weight 2 hit in each,
before a reading verdict means anything about an unfamiliar text. The number four is still
this skill's judgment. The seven themes are not.

### What this paper refuses to support

**One check is never enough, inside the source domain or outside it.** Trained on a single
NarraBench dimension, the best model reached 80.2 percent binary macro-F1, and removing any
single dimension cost at most 1.2 points (Appendix E, Table 8, p.21). The signal is
redundant and spread out. A verdict resting on one check is not supported.

**A structural audit still misreads about one human text in nine.** In the narrative-only
six-way model, genuinely human stories were classified as human 88.5 percent of the time
(Figure 3, p.9), and per-class human F1 was 0.89 without style and 0.93 with it (Table 12,
p.22). That is a purpose-built classifier on 5,000 word fiction, which is the best case.
Read it as a floor on the error rate of any reading verdict, and carry it into the
confidence line.

**Oddity raises the odds and cannot clear a single text.** Human stories are rarer in
narrative space, mean rarity percentile 0.71 against 0.49, Cohen's d 0.83, AUC 0.73. But at
the prompt level the human version was the rarest of the six only 57.8 percent of the time,
and in raw counts AI stories fill more of the rare tail than human ones: top 1 percent, 42
human against 41 AI; top 5 percent, 180 against 234; top 10 percent, 340 against 487
(Appendix H, Table 13, p.22 to p.23). The paper's own summary of Figure 5 is that "all
distributions overlap substantially." So the closing question of an audit, is there anything
here another draft would not have had, stays useful as a prompt and does not become a test.

**Length and topic are not the signal, which is a result in this skill's favour.** A
classifier on word count alone reached 55.9 macro-F1, and the narrative model held 93.2
before and after length matching, and 91.6, 94.3 and 93.7 across short, medium and long
bands (Appendix G, Table 11, p.22). Across six topics, Kruskal-Wallis H = 4.69, p = 0.46. Do
not discount a finding because the text is short, and do not add one because it is long.

**Surface repair does not move this layer.** Span-level rewriting of seven artifact
categories over 278 stories left detection at 93.9 macro-F1 against 95.5 unedited, a drop of
1.6 (Section 4.2, p.8). Structural findings are repaired by structural rewrites only, which
is the reason Pass 4 orders discourse repairs first.

### Model-conditional tells, use only when the model is known

The paper's fingerprint features are per-source and are not usable when the author is
unknown, which is the ruling `discourse-tells.md` already carries. They become usable in the
one case where the model is known, which is a draft this assistant just produced.

Claude is the most distinctive of the five models, 77.1 percent per-class F1 on narrative
features alone against 55.0 to 73.0 for the others (Table 12, p.22), and holds 26 fingerprint
features against 3 for the least distinctive model (Appendix I, p.25). Its top-ranked
fingerprints, by uniqueness ratio (Table 17, p.27), and the paper's summary at p.9:

- Event escalation is flatter than any other source, uniqueness 22.4, the highest in the
  table. Test: does intensity stay level from open to close.
- Event-type variety is low, uniqueness 10.7. Test: do the beats repeat one kind of move.
- Endings reach forward, epilogue or flash-forward. Test: does the last beat step outside
  the main span to report what happened later.
- Dream or vision as a break in time is avoided.
- Verbatim, p.9: Claude "takes a reverent/continuist approach to literary tradition,
  honoring and extending storytelling conventions rather than subverting or challenging
  them (62% of Claude stories vs. 39-56% across other sources)", and favours "quiet endings
  over 'avalanche' endings."

Weight these 1, never 2. They come from the six-way task, where narrative-only macro-F1 was
68.4 percent against 93.2 for the binary task (Table 3, p.8), so they separate models far
less reliably than the core features separate human from machine.

### Two tensions this section does not resolve

The paper lists direct reader address among the human core features, humans 28 percent
against 7 percent (Table 15 row 2, p.25), and also lists "narrator address mode -> no direct
address" among the human fingerprint features (Table 17, p.27). The two come from different
tasks, binary and six-way, and the paper does not reconcile them. Treat reader address as a
binary-task signal only.

Table 16 marks Fourth-Wall Permeability and Direct Reader Address as ordinal means, while
the values, 0.67 against 0.39 and 0.28 against 0.07, are the same numbers section 4.1 reports
as percentages of stories. The prevalence reading is used above because that is how the
paper's own prose states it.

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
curly quotation mark or apostrophe, no heading in title case, no heading level skipped, no
thematic break between sections, no section that summarizes the section above it, no
conclusion restating the page, and no vocabulary-list word outside a quoted example or the
list itself. Those are greppable and were grepped.

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
