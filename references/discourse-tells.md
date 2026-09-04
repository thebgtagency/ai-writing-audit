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

| Feature | Human | AI |
|---|---|---|
| Narrator explicitly explains the story's theme | 52% | 77% |
| Emotion conveyed through physical sensation or bodily metaphor | 38% | 81% |
| Emotion conveyed by an explicit label | 29% | 8% |
| Smell-based imagery | 57% | 82% |
| References a specific named text or author | 47% | 24% |
| Breaks the fourth wall | 67% | 39% |
| Addresses the reader directly | 28% | 7% |
| Morally ambivalent protagonist | 59%, see note | 38%, see note |
| Resolution driven by protagonist choice | 46% | 69% |
| Intertextual gestures stay vague allusions | 50% | 72% |
| No subplots at all | 57% | 79% |
| Resolution by internal understanding or acceptance | 27% | 47% |
| Depth of interior access, mean on a 1 to 5 scale | 3.67 | 3.93 |
| Sensory density, mean | 3.66 | 3.93 |
| Setting as psychological mirror, mean | 3.58 | 4.07 |

Note on the ambivalence row: the paper states humans "present morally ambivalent
protagonists more often (59% vs. 38%)", so the human rate is the 59.

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

## The pipeline changes the tell set

The corpus stories came from a template-based extraction pipeline, and a direct pipeline
variant produces a different feature ranking: "comparing the top-20 discriminative
features, only 6 overlap". A draft produced through a different workflow may carry a
different tell set, which caps how far any fixed list should be trusted.

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

Caveat on direct reader address: in fiction it is rare and therefore informative. In a
direct message, a caption, or an ad, second person is the native register and carries no
signal at all. Use it as a positive signal only in text where third person would have been
the default.

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

Useful as a reminder that tells are model specific and move. Not useful as a check, because
you rarely know which model produced the draft.

## The clustering result

> We find that AI-generated stories cluster in a shared region of narrative space, while
> human-authored stories exhibit greater diversity.

Operationally: a draft can be free of every listed tell and still sit inside the cluster,
because the cluster is defined by the absence of oddity. The closing question of an audit
is not "did I remove the tells" but "is there anything here that another draft would not
have had".

Numbers behind the clustering: human stories average a rarity percentile of 0.71 against
0.49 for AI (Cohen's d 0.83), and in the top 10 percent rarest stories humans hold 24.7
percent against 7.1 for AI. The most confused model cluster is DeepSeek, Gemini, and Kimi,
and the single most common human misclassification is Human to Kimi (46 stories), which is
the measured version of the generic-model lesson: the least distinctive output is the
hardest to sort.
