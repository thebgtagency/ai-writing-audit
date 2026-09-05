# Discourse layer: reference

Source: Russell, Rajendhran, Pham, Iyyer, Wieting. "StoryScope: Investigating
idiosyncrasies in AI fiction." COLM 2026.

## What the study actually did

Verbatim from the abstract:

> we ask instead whether AI-generated stories can be distinguished from human ones
> without relying on stylistic signals, focusing on discourse-level narrative choices
> such as character agency and chronological discontinuity.

> We apply STORYSCOPE to a parallel corpus of 10,272 writing prompts, each written by a
> human author and five LLMs (Claude, DeepSeek, Gemini, GPT, and Kimi), yielding 61,608
> stories, each ~5,000 words, and 304 extracted features per story.

Arithmetic check, September 2026: six sources times 10,272 prompts minus 11 dropped Gemini
stories minus 13 dropped Claude stories equals 61,608.

> Narrative features alone achieve 93.2% macro-F1 for human vs. AI detection and 68.4%
> macro-F1 for six-way authorship attribution, retaining over 97% of the performance of
> models that include stylistic cues.

> A compact set of 30 core narrative features captures much of this signal: AI stories
> over-explain themes and favor tidy, single-track plots while human stories frame
> protagonists' choices as more morally ambiguous and have increased temporal complexity
> (e.g., flashbacks, nonlinear structure).

The sentence that justifies having this layer at all, from the conclusion:

> As surface-level signatures become increasingly transient, often removed by newer model
> versions or simple post-hoc edits, narrative features offer a more durable basis for
> authorship analysis, since altering them requires significant structural rewrites.

Measured performance of the layer, Table 2: narrative features only, 257 features, 93.2
macro-F1. Core only, 30 features, 84.8. Style only, 39 features, 85.8. Narrative plus
style, 304 features, 96.0. Zero-shot Binoculars, 55.9.

The 304 feature set came from 408 discovery candidates reduced by deduplication. Two more
baselines from the same paper: a supervised transformer (ModernBERT) reaches 99.9 in
domain, and a trivial always-AI classifier scores 83.3 accuracy on the 5:1 imbalanced test
set, which is why the paper reports macro-F1 and never accuracy.

Read the middle two numbers together. A pure style model and a 30 feature narrative model
score within one point of each other. Neither layer wins alone.

## The measured rates

From section 4.1 and Table 16. Human value first, AI value second. These are the numbers
behind the checks, and they show why every check is a rate rather than a switch.

All 30, in the paper's own seven groups. Rows marked s are means on a 1 to 5 Likert scale,
o are means over integer codes, and the rest are the share of stories carrying that value.
Gap is human minus AI. Three features appear twice because the same feature points one way
on one option value and the other way on another, which is why 33 rows hold 30 features.

**AI-elevated, thematic over-determination**

| Feature | Human | AI | Gap |
|---|---|---|---|
| Thematic explicitness and moralizing, s | 3.28 | 3.94 | -0.65 |
| Moral and philosophical weighting, s | 3.26 | 3.68 | -0.42 |
| Thematic unity, s | 4.41 | 4.74 | -0.33 |
| Narratorial thematic commentary, yes | 52% | 77% | -25 |
| Dialogue function, philosophical debate | 34% | 59% | -25 |
| Reference explicitness, implicit echoes | 50% | 72% | -22 |

**AI-elevated, sensory and embodied performativity**

| Feature | Human | AI | Gap |
|---|---|---|---|
| Emotional expression, embodied | 38% | 81% | -42 |
| Setting as psychological mirror, s | 3.58 | 4.07 | -0.49 |
| Environmental and ecological emphasis, s | 2.83 | 3.21 | -0.38 |
| Sensory modalities, olfactory | 57% | 82% | -26 |
| Sensory density, s | 3.66 | 3.93 | -0.26 |
| Depth of interior access, s | 3.67 | 3.93 | -0.26 |

**AI-elevated, structural streamlining**

| Feature | Human | AI | Gap |
|---|---|---|---|
| Causal chain continuity, s | 3.92 | 4.20 | -0.28 |
| Spatial granularity, o | 2.27 | 2.53 | -0.26 |
| Agency in resolution, protagonist choice | 46% | 69% | -23 |
| Character introduction, external description | 30% | 52% | -22 |
| Subplot integration, no subplots | 57% | 79% | -22 |
| Resolution mode, internal understanding | 27% | 47% | -21 |
| Pre-threat character investment, s | 2.76 | 2.99 | -0.23 |
| Opening spatial grounding, o | 2.12 | 2.33 | -0.20 |

**Human-elevated, intertextual richness**

| Feature | Human | AI | Gap |
|---|---|---|---|
| Intertextual strategy, explicit named reference | 47% | 24% | +23 |
| Reference explicitness, balanced mix | 37% | 16% | +21 |

**Human-elevated, reader engagement**

| Feature | Human | AI | Gap |
|---|---|---|---|
| Fourth-wall permeability, o | 0.67 | 0.39 | +0.28 |
| Direct reader address, o | 0.28 | 0.07 | +0.21 |

**Human-elevated, temporal complexity**

| Feature | Human | AI | Gap |
|---|---|---|---|
| Depth of recontextualization after surprise, s | 3.28 | 2.95 | +0.34 |
| Chronological discontinuity, s | 2.40 | 2.12 | +0.28 |
| Nonlinear framing for delayed disclosure, s | 1.96 | 1.68 | +0.28 |
| Anachrony intensity, s | 2.58 | 2.31 | +0.27 |

**Human-elevated, narrative diversity**

| Feature | Human | AI | Gap |
|---|---|---|---|
| Location variety scope, o | 1.34 | 1.08 | +0.26 |
| Dialogue-to-narration proportion, s | 2.95 | 2.70 | +0.24 |
| Subplot integration, thematically parallel | 42% | 21% | +22 |
| Moral polarity, ambivalent or mixed | 59% | 38% | +21 |
| Emotional expression, explicit labels | 29% | 8% | +21 |

Note on the ambivalence row: the paper states humans "present morally ambivalent
protagonists more often (59% vs. 38%)", so the human rate is the 59.

Note on the two reader-engagement rows: Table 16 labels them ordinal means, while the values
are the same numbers section 4.1 states as percentages of stories, 67 against 39 and 28
against 7. The prevalence reading is used because that is how the paper's own prose puts it.

Note on the subplot rows: they are not in conflict. Having no second thread at all is the
machine-leaning value, 57 against 79. Among texts that do have one, running it parallel to
the main line is the human-leaning value, 42 against 21. So "everything connects" is not the
tell. "There is only one thing" is.

Note on the three near-tied rows: thematic unity, causal chain continuity, and moral and
philosophical weighting all sit high or mid for humans too. A hit on one of those is weak
evidence and cannot carry a verdict alone. Compare with the embodied emotion row, 38 against
81, which is the widest separation in the table.

Read the theme row first. Humans moralize in 52 percent of stories. The tell is not that a
text explains its own point, it is the rate at which it does. One explicit takeaway line
proves nothing. A text where every section closes on one is the pattern.

Verbatim, on the emotion reversal:

> Where a human author might write that a character "felt afraid," AI renders fear as a
> tightening chest, cold sweat, and dimming lamplight.

Verbatim, on order:

> Human authors subvert linearity.

> Humans use more time jumps, flashbacks and flash-forwards, and nonlinear structure to
> delay key revelations. AI favors single-track narratives with fewer loose ends

Verbatim, on reader address:

> Humans break the fourth wall far more often (67% vs. 39%) and address the reader directly
> more frequently (28% vs. 7%). ... AI writes as though no one is watching.

Verbatim, on naming things:

> Humans reference specific texts and authors at nearly double the AI rate (47% vs. 24%)
> ... whereas AI generally sticks to vague allusions and avoids naming real brands, places,
> or works.

## Why surface repair does not move this layer

> editing out clichéd phrasing or purple prose does not alter the structural narrative
> choices (causal linearity, thematic explicitness, sensory over-description) that drive
> our classifier.

The paper draws the boundary explicitly: style is sentence and phrase level texture, while
non-style covers events, causality, closure, character roles, relationship topology,
setting, and temporal arrangement, and "Sensory Density, Depth of Interior Access, and
Chronological Discontinuity fall on the non-style side of this rule". A style-dependence
audit over all 304 taxonomy features keeps 257 on the strict non-style side.

The paper tested this. It ran a span-level rewriting framework over 278 stories, targeting
seven categories of artifact including cliche, redundant exposition, and purple prose.
Detection on the edited Gemini subset came in at 93.9 macro-F1 against 95.5 on the same
stories unedited, a drop of 1.6 points, which is to say the structural signal survived the
style edit. The 93.2 figure is the general test set score, not the baseline of this
comparison. Corrected September 2026 against the paper's own wording: "detects edited
Gemini stories at 93.9% macro-F1 ... compared to 95.5% macro-F1 on the original unedited
stories, a drop of only 1.6".

Against that, the same paper records how fast surface tells decay:

> AI style is increasingly fleeting: GPT-5.4 significantly reduced em-dash usage, and
> fine-tuning to mimic human style drops AI detection rates on creative writing from 97% to
> 3%

Both facts belong in an audit tool. A word list is worth running because it is cheap and it
catches unedited drafts. It is not worth trusting, because one style pass or one model
release removes it.

## How you read a text decides which tells you find

Corrected September 2026. An earlier version of this file read the paper's templating
experiment as a claim about how the stories were generated and concluded that a different
writing workflow yields a different tell set. That is not the experiment. The stories were
generated by giving five models a prompt. The template sits in the analysis, not in the
writing, and the experiment compared two ways of looking at the same stories.

The paper ran feature discovery twice, once over raw story text and once over structured
templates of those same stories, "the only difference being whether the comparative analysis
operates on templates or raw story text". Of the top 20 discriminative features, only 6
overlap. The raw route returned style-heavy features, named in the paper as humor usage,
vocabulary register, allusion types, and dominant imagery. The template route returned
structure-heavy ones: emotional arcs, relationship trajectories, event density, and flashback
usage.

The operational reading, and it is the strongest procedural result in the paper for a tool
like this one: an auditor who reads the prose finds prose tells, and calls them structural.
To reach the discourse layer you have to stop reading the sentences first. Build the
structural template, mark absent fields null, audit the template, and quote the prose only
to evidence a finding. The paper prints its own template, and `SKILL.md` carries the
condensed field list under "Research-backed tells".

A second measured reason to slow the pass down. Applying the features in a single call
covered 68.4 percent of them; applying them one narrative dimension per call covered 95.4
percent, and the single-call dropout concentrated in revelation and temporal structure.
Those two dimensions hold most of the human-leaning checks, so a single sweep does not fail
evenly. It fails toward the machine verdict.

## What the paper does not say

It does not tell writers to avoid the AI-elevated values. It reports which values separate
sources. Turning a distribution into a rule is a step this skill takes on its own, and the
step is arguable. Where a check reads as an instruction, it is this skill instructing, not
the paper.

## Scope limit of this source, stated plainly

The strongest sentence in the paper on this point:

> Our stories average roughly 5,000 words depending on source, enabling extraction of
> fine-grained narrative features that shorter texts cannot support.

Shorter texts cannot support these features. That is the source telling you it does not
cover a caption or a message. It is the reason this skill collapses the discourse layer to
three checks below 60 words instead of pretending the other checks still work.

The corpus is fiction. The stories are about 5,000 words each. The feature set comes from
NarraBench, a taxonomy of narrative dimensions rooted in literary theory, and the paper
adopts ten of its twelve aspects: Agent, Social Network, Event, Plot, Structure, Setting,
Time, Revelation, Perspective, Style.

The AI side of the corpus came from five models: Gemini 3 Flash, Kimi K2.5, DeepSeek V3.2,
Claude Sonnet 4.6, and GPT-5.4. Findings do not automatically transfer to models outside
that set, and the human stories came from short story anthologies, not novels, essays,
journalism, or lyrics.

Three more measured limits worth carrying:

- No single dimension is enough. "No dimension is individually sufficient (best: agents at
  80.2% binary macro-F1) and none is individually necessary." So a verdict resting on one
  check is not supported even inside the source domain.
- Length alone is nearly useless as a signal, 55.9 macro-F1, and matching the lengths of the
  human and AI test sets left the narrative model unchanged at 93.2.
- Topic does not decide detectability: "We find no significant topic-wise differences:
  H=4.69, p=0.46."

Nothing in the paper was measured on a direct message, a caption, a slide, an ad, an email,
or a spoken script. The transfer below is an argued analogy, not a replicated result. Every
item in the "carries over" table states the reasoning that carries it. Every item in the
"stays in fiction" list is marked so you do not apply it to a two line message and produce
nonsense.

## The 20 core AI-characterizing features

Table 14. An arrow marks the specific option value elevated for AI.

| # | Feature | Question in the paper | Dim |
|---|---------|----------------------|-----|
| 1 | Thematic Explicitness and Moralizing | How explicitly does the story articulate its themes or morals? | SIT |
| 2 | Dominant Emotional Expression -> embodied | How are characters' emotions most commonly conveyed? | AGENT |
| 3 | Thematic Unity | To what extent do subplots and flourishes serve a central thematic concern? | PLT |
| 4 | Dominant Sensory Modalities -> olfactory | Which sensory modalities does the story most frequently engage? | SET |
| 5 | Character Introduction -> external description | What narrative device primarily introduces the central character? | AGENT |
| 6 | Setting as Psychological Mirror | To what degree does physical environment mirror characters' inner states? | SET |
| 7 | Continuity of Main Causal Chain | How continuous is the single causal chain from inciting incident to ending? | EVT |
| 8 | Sensory Density | How dense is sensory description across the narrative? | SET |
| 9 | Agency in Resolution -> protagonist choice | Is resolution driven by protagonist's choices or external events? | PLT |
| 10 | Narratorial Thematic Commentary -> yes | Does the narrator explicitly comment on themes beyond characters' perspectives? | SIT |
| 11 | Opening Spatial Grounding | How clearly does the opening ground the reader in a specific physical setting? | SET |
| 12 | Dialogue Function -> philosophical debate | What main functions does dialogue serve? | PER |
| 13 | Spatial Granularity Level | How fine-grained is the story's depiction of physical space? | SET |
| 14 | Subplot Integration -> no subplots | How directly do subplots echo the central theme? | PLT |
| 15 | Moral / Philosophical Weighting | How heavily does the story foreground moral or philosophical questions? | SIT |
| 16 | Reference Explicitness -> implicit echoes | Are intertextual gestures primarily explicit or diffuse? | SIT |
| 17 | Environmental and Ecological Emphasis | How prominent is the natural environment or ecology in the narrative? | SET |
| 18 | Mode of Resolution -> internal understanding | Is the main event chain resolved through internal acceptance or external action? | EVT |
| 19 | Pre-Threat Character Investment | How much does the story build investment before major jeopardy? | REV |
| 20 | Depth of Interior Access | How deep into characters' inner life does narration go? | PER |

## The 13 core human-characterizing features

Table 15.

| # | Feature | Question in the paper | Dim |
|---|---------|----------------------|-----|
| 1 | Intertextual Strategy Types -> explicit named reference | What kinds of intertextual engagement does the story employ? | SIT |
| 2 | Frequency of Direct Reader Address | How often does the text directly address the reader? | PER |
| 3 | Reference Explicitness -> balanced mix | Are intertextual gestures explicit or diffuse? | SIT |
| 4 | Depth of Recontextualization After Surprise | How extensively does a revelation force reinterpretation of earlier scenes? | REV |
| 5 | Dialogue-to-Narration Proportion | What proportion of text is direct dialogue vs. narration? | PER |
| 6 | Fourth-Wall Permeability | To what extent does the story break the boundary between story-world and reader? | SIT |
| 7 | Subplot Integration -> thematically parallel | How directly do subplots echo the central theme? | PLT |
| 8 | Degree of Chronological Discontinuity | How often does the narrative jump across time? | TMP |
| 9 | Location Variety Scope | How many distinct physical locales does the story inhabit? | SET |
| 10 | Anachrony Intensity | How heavily does the narrative rely on flashbacks or flash-forwards? | TMP |
| 11 | Moral Polarity Toward Protagonist -> ambivalent | Does the narrative frame the protagonist's choices as morally clear or ambiguous? | PLT |
| 12 | Dominant Emotional Expression -> explicit labels | How are characters' emotions most commonly conveyed? | AGENT |
| 13 | Nonlinear Framing for Delayed Disclosure | To what extent does the story use time jumps to stage revelations? | REV |

## The finding that reverses standard writing advice

Feature 2 of the AI list and feature 12 of the human list are the same feature pointing
opposite ways. Emotion carried by embodied metaphor is the AI-leaning value. Emotion
carried by an explicit label is the human-leaning value.

"Show, do not tell" is the most repeated instruction in writing advice, and the measurement
says the machine already obeys it by default. So the chest does not tighten, the stomach
does not drop, the breath does not catch. If the feeling matters, name it and move on.

The tell is the default, not the device. One embodied line in a page is writing. Every
emotion delivered as a body sensation is the pattern.

## What carries over to non-fiction, and why

Each row states the reasoning. If the reasoning does not hold for the text in front of you,
drop the check rather than force it.

| Fiction feature | Non-fiction form | Why it carries |
|---|---|---|
| Thematic explicitness and moralizing (AI 1) | The text states its own lesson: "the takeaway here is", "which proves that", "and that is the difference" | Genre independent. It is a habit of explaining rather than showing, and the Wikipedia guide records the same habit in informational prose as canned conclusions |
| Narratorial thematic commentary (AI 10) | The writer steps outside the point to comment on its significance | Same habit, one level up |
| Thematic unity, no subplots (AI 3, 14) | Nothing pulls sideways. No aside, no exception, no second thread | Genre neutral. Real accounts leak detail that does not serve the point |
| Continuity of main causal chain (AI 7) | Every sentence follows cleanly from the previous one. No gap, no reversal, no admitted cost | Genre neutral tidiness |
| Agency in resolution to protagonist choice (AI 9) and resolution by internal understanding (AI 18) | The close that says the reader only has to decide, realize, or commit | Direct analogue: the mindset close resolves the tension through a private act of will rather than an external step |
| Moral polarity ambivalent (human 11) | A named cost, a case where it did not work, a person it is wrong for | Same axis, opposite end |
| Explicit named reference (human 1, 3) | Real names, real numbers, real dates, the actual tool, the actual city | Same axis: concrete anchoring versus diffuse echo |
| Emotion as explicit label (human 12) | "I was annoyed" instead of a body sensation | Genre neutral |
| Direct reader address (human 2) | Second person, and a question that expects an answer | Carries, with the caveat below |
| Chronological discontinuity and anachrony (human 8, 10, 13) | Opening mid scene, telling it out of order, withholding the setup | Carries in any text long enough to have an order. Meaningless below about two sentences |
| Fourth-wall permeability (human 6) | Naming the medium: "this is a cold message", "you can ignore this" | Carries in messages, where the medium is visible to both sides |
| Depth of recontextualization after surprise (human 4) | A later fact that changes what an earlier sentence meant. The number that reframes the story above it, the admission that makes the opening read differently | Genre neutral. It is about disclosure order rather than about plot, and any text carrying two facts can put the reframing one second |
| Subplot integration to thematically parallel (human 7) | A second thread that runs alongside the main one instead of feeding it | Same axis as the no-subplots check, at the other end. Carries wherever a text is long enough to hold two threads |

Caveat on direct reader address, revised September 2026 after fourteen recorded runs. The
paper measures two things in one group and only one of them transfers.

Direct reader address is rare in fiction and therefore informative there. In a message, a
caption, an ad, a script, an email or a product page, second person is the native register,
so its presence and its absence both carry nothing. No format profiled in `formats.md` has
third person as its default, which means this half cannot be scored anywhere this skill runs
and never has been. It is carried on the paper's word, not on a hit.

Naming the medium does transfer, because it is a choice in any format: "this is a cold
message", "last one from me", "ignore this if it is not live". Run it in the human direction
only. Presence belongs in WHAT IS WORKING, absence is a note and never a fault.

The consequence for scoring is in `SKILL.md`: theme 5 is reachable only as a positive, so
the assessment bar of four themes is drawn from six rather than seven.

## What stays in fiction, do not port it

Sensory density and lushness (AI 8), spatial granularity (AI 13), opening spatial grounding
(AI 11), setting as psychological mirror (AI 6), olfactory detail (AI 4), environmental and
ecological emphasis (AI 17), depth of interior access (AI 20), pre-threat investment
(AI 19), dialogue as philosophical debate (AI 12), dialogue to narration proportion
(human 5), location variety (human 9), character introduction device (AI 5).

These measure a story world. A caption has no story world. Flagging a landing page for low
olfactory variety is how an audit tool loses the reader's trust.

## Per-model fingerprints, from the abstract

> for example, Claude produces notably flat event escalation, GPT likes using gossip as a
> plot mechanism, and Gemini defaults to external character description

Useful as a reminder that tells are model specific and move. Not useful as a check in the
general case, because you rarely know which model produced the draft.

There is one case where you do know, and this skill runs inside it often: a draft the
assistant running the audit just produced. `SKILL.md` carries the Claude fingerprint list
under "Research-backed tells" for that case only, weighted 1 and never 2. The reason for the
lower weight is in the paper's own numbers. Fingerprints come from the six-way task, where
narrative features reach 68.4 macro-F1, against 93.2 on the binary task. They separate models
far less reliably than the core features separate human from machine.

Do not run a fingerprint list against a draft of unknown origin. Attributing a text to a
named model is a stronger claim than this skill makes anywhere else, and the paper's own
per-class numbers for the three weakest models, 0.55 to 0.60 F1, are close enough to noise
that the claim would not survive.

## The clustering result

> We find that AI-generated stories cluster in a shared region of narrative space, while
> human-authored stories exhibit greater diversity.

Operationally: a draft can be free of every listed tell and still sit inside the cluster,
because the cluster is defined by the absence of oddity. The closing question of an audit
is not "did I remove the tells" but "is there anything here that another draft would not
have had".

Numbers behind the clustering, and the caveat that has to travel with them. Human stories
average a rarity percentile of 0.71 against 0.49 for AI, Cohen's d 0.83, AUC 0.73. Within
each source, humans are overrepresented in the rare tail: 24.7 percent of human stories fall
in the rarest 10 percent corpus-wide against 7.1 percent of AI stories.

Corrected September 2026. An earlier version of this file stopped at those two rates, which
is the flattering half. In raw counts the rare tail is mostly machine written, because there
are five AI sources and one human one: the rarest 10 percent holds 340 human against 487 AI
stories, the rarest 5 percent 180 against 234, and the rarest 1 percent 42 against 41. The
paper says plainly that "AI stories are present throughout" and that in Figure 5 "all
distributions overlap substantially". At the prompt level the human version is the rarest of
the six only 57.8 percent of the time, so an AI version is rarer than the human one in more
than two cases in five.

So oddity shifts the odds and settles nothing about one text. The closing question of an
audit, is there anything here another draft would not have had, stays a prompt for the
writer. It never becomes a test, and it is never evidence of a human hand.

The geometry underneath is the part that does hold at the group level. Mean human-to-AI
centroid distance is 1.6 times the mean AI-to-AI distance, 6.6 against 4.3, and even the
closest human-AI pair sits farther apart than the most distant AI-AI pair, 6.2 against 6.0.
Human stories are also more spread out, mean distance to their own centroid 22 percent
greater than the average AI radius, 33.2 against 27.4.

The most confused model cluster is DeepSeek, Gemini, and Kimi, and the single most common
human misclassification is Human to Kimi (46 stories), which is the measured version of the
generic-model lesson: the least distinctive output is the hardest to sort. Kimi carries 3
fingerprint features against 32 for human writing, and the paper places it "at the generic
center of the AI distribution with no distinctive narrative choices".
