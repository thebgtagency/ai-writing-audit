# Conflicts and how this skill resolves them

The material this skill is built on does not agree with itself. Two measured sources
contradict each other, each source contradicts itself in places, and the cleanup tools
built on top of them contradict both. Hiding that would leave the disagreements to be
rediscovered mid-edit, so every conflict is listed here with the ruling this skill applies.

Where a position comes from a measured source it is named. Where it comes from common
tooling practice it is described as such, without naming a particular tool, because the
same rule appears in several and the argument is with the rule.

---

## 1. Surface layer versus discourse layer

**Position A.** Style is the strong signal. Style-only classifiers separate machine from
human text at high accuracy, and word and punctuation lists are cheap to run.

**Position B.** Style is a decaying signal. Fine-tuning a model to imitate human style drops
detection on creative writing from 97 percent to 3 percent, and one recent model release cut
its em dash use sharply. Structural narrative features survive that: a rewriting pass over
cliche, redundant exposition, and purple prose moved narrative detection by 1.6 points.

**Ruling.** Both, always, and never one alone. Inside the fiction study the numbers are
almost identical: style-only 85.8 macro-F1, thirty narrative features 84.8. A pass that runs
one layer reports a partial result and must say so.

**Consequence for repair order.** Discourse findings first. Surface repairs applied to a
structurally machine-shaped text produce a polished machine-shaped text, and the study says
so directly: editing out cliche and purple prose does not alter causal linearity, thematic
explicitness, or sensory over-description.

---

## 2. The em dash

**Position A, common in tooling.** The delivered text contains zero em dashes and zero en
dashes. One hit means the draft is not finished.

**Position B, the same tools, detection half.** A single em dash means nothing. Em dashes
are evidence only when combined with sales-shaped rhythm and other tells.

**Position C, the source both positions cite.** Machine output uses the character more often
than nonprofessional human writing of the same genre, usually spaced, in a formulaic way.
The sign is most useful in combination and not by itself. Newer models were tuned to
suppress it. A July 2026 study found that among contemporary models only one used em dashes
more than professional writers, while another used them less.

**Ruling.** Split the two jobs, because they are not the same question.

- Judging whether a foreign text reads as machine written: the dash is weight 1 and never
  the lead finding. The specific pattern worth flagging is the spaced dash used for
  emphasis, repeated.
- Cleaning a text you are about to publish: a zero-dash rule is a legitimate house style
  choice and this skill will apply it on request. It is not evidence and this skill will not
  present it as evidence.

A blanket ban stated as a detection rule contradicts the source it is drawn from, and on
current model output it now points the wrong way for at least one major model family.

---

## 3. Rule of three

**Position A.** Models force ideas into groups of three to look comprehensive. Repair by
collapsing the triad.

**Position B.** Human rhetoric has used the tricolon for millennia. Do not attack every
group of three. Attack the filler triad and the stack of parallel three-item lists.

**Ruling.** Position B, with a test. A triad is filler when the three items are near
synonyms, when they are the same length and shape, or when a fourth item would have been
equally true. A triad is content when the three items are distinct and named, when the
count comes from the world rather than from the sentence, or when the medium asks for it.
Weight 1, judged by density across the text.

---

## 4. Sentence rhythm

**Position A.** Vary your rhythm. Add short punchy sentences. Let some mess in, tangents and
half-formed thoughts, because perfect structure feels algorithmic.

**Position B.** Stacked fragments are themselves a tell. An even mid-length cadence is a
tell, and so is a run of one-line paragraphs. Text that reads as a machine trying not to
read as a machine is a failure mode of its own.

**Ruling.** Position B governs, and Position A is demoted from an instruction to a
diagnosis. Rhythm variation is a repair for a metronome cadence that is already there. It is
never an additive style applied to a text that did not have it.

The operational rule: do not insert a fragment, an aside, or a rhythm break that the draft's
own voice did not already contain. The test is whether the line is what this writer would
write, rather than what a text avoiding detection would produce.

---

## 5. Invented personality

**Position A.** When no writing sample is available, fall back to a natural, varied,
opinionated voice. Add first person. Add uncertainty. An admission such as "I genuinely do
not know how to feel about this" reads more human than a neutral list.

**Position B.** Never add first person, an anecdote, an opinion, an interview, or a source
that was not in the draft.

**Ruling.** Position B, without exception, and this is the most consequential ruling in the
file.

Position A produces a text that reads more human and says things that are not true. An
invented opinion is fabrication. An invented anecdote in marketing copy is a false claim
about a real business. A tool that manufactures a personality to defeat a detector has
stopped being an editing tool.

When a text is clean, flat, and voiceless, that is a finding to report, not a hole to fill.
The repair is to ask the writer for the missing specific, or to leave the text neutral and
say why. Voice can be matched from a sample. It cannot be invented from nothing.

---

## 6. Fix every hit, or only clusters

**Position A.** One tell is weak. Flag clusters, not isolated hits.

**Position B.** In text you are about to publish, a hit is a hit. "There is only one, so it
stays" is not a standard.

**Ruling.** Both, separated by purpose, because they answer different questions.

- Assessing an unfamiliar text: clusters only. A single hit supports nothing. One published
  guideline for this material sets the bar at five or more distinct categories before an
  origin claim is reasonable, and the caution about false accusations in
  `false-positives.md` explains why.
- Cleaning your own draft: fix the single hit if the fix costs nothing. There is no accuracy
  claim at stake, only the text.

The audit output must state which mode it ran in. The same text can pass one and fail the
other, and that is not an inconsistency.

---

## 7. Hedges and wordy constructions

**Position A, standard editing advice.** Cut "very", "perhaps", "in order to", "the fact
that", "all of the". Tighten.

**Position B, the Wikipedia source.** Those exact constructions are listed among the things
human writing does more than machine writing, alongside plain verbs and simple is-and-has
phrases. Machine text avoids them while reaching for a formal register.

**Ruling.** Cut the stack, keep the single. "It could potentially possibly be argued that"
is three hedges doing one job and it goes. One "perhaps" is how a person sounds. A draft
thin on these constructions gets a note in the WHAT IS WORKING section rather than a further
tightening pass, because tightening is the direction that makes text more machine-like.

---

## 8. Transition words

**Position A, common in tooling.** "Additionally" and its family are on the flagged word
list.

**Position B, the same tools elsewhere.** They are machine-coded only when piled up. One
"however" is not a tell.

**Position C, the source.** Transition words in isolation are listed explicitly as an
ineffective indicator. Only a few are known to be overused this way, the pattern has
precedent in human essay writing, and many style guides accept it.

**Ruling.** Position C. A transition word alone is weight 0 and is never raised as a
finding. Sentence-initial "Additionally" repeated across paragraphs is a pattern and is
weight 1. A tool that flags every "Additionally" is contradicting the guide it cites.

---

## 9. Show or tell

**Position A, near-universal writing advice.** Show, do not tell. Render emotion through
physical detail rather than naming it.

**Position B, the fiction study.** Machine text conveys emotion through physical sensation
or bodily metaphor 81 percent of the time against 38 percent for human text, and uses an
explicit emotion label 8 percent against 29 percent. Machine text also scores higher on
sensory density, on smell imagery, on setting as a mirror of inner state, and on depth of
interior access.

**Ruling.** Position B for auditing, Position A retired as a proxy for humanity. The tell is
the default, not the device. One embodied line is craft. Every feeling arriving as a body
sensation is the pattern, and lush sensory writing is not evidence of a human hand.

---

## 10. Descriptive source, prescriptive tool

**Position A, the source.** This list is descriptive, not prescriptive. It consists of
observations, not rules. Advice about what to avoid belongs elsewhere.

**Position B, every tool built on it.** Here are the rules.

**Ruling.** The conflict is real and cannot be dissolved, only labelled. The observations
are the source's. The thresholds, the weights, and the verdict bands are this skill's own
judgment, and they are arguable. Wherever a number appears in this skill that the sources do
not contain, the text says so.

---

## 11. Scope: fiction, or not fiction

**Position A, the Wikipedia guide.** Built for encyclopedic writing, and it says outright
that tells specific to fiction are not listed and are less relevant there.

**Position B, the fiction study.** Built on roughly 5,000 word stories, with features drawn
from literary theory, and it states that shorter texts cannot support those features.

**Ruling.** The two sources cover informational prose and long fiction, and between them
they leave uncovered the formats most text actually takes: messages, captions, slides, ads,
emails, scripts. This skill runs there anyway, because that is where the need is, and labels
every such run as an argued transfer rather than a measured result. The reasoning behind
each transfer is written down in `discourse-tells.md` so it can be checked instead of
trusted, and the parts that do not transfer are listed as fiction-only and not applied.

---

## 12. Which language

**Position A.** The vocabulary lists are English. Every study cited measured English text.

**Position B, practice.** Tools built on those lists get run on text in other languages.

**Ruling.** Split the layers by language dependence.

- The discourse layer is language independent. Explaining your own point, single track
  causality, resolution by private decision, absence of named specifics: all of it audits in
  any language.
- The formatting and chat-leftover tells are language independent. Title case headings,
  inline-header lists, placeholder text, assistant register.
- The vocabulary lists do not transfer, at all. A translated word list produces false
  positives, because the overuse was measured on English tokens.

For a language with no measured list, run the discourse layer and the formatting layer,
report the vocabulary layer as not run, and build a local list only from observed model
output in that language. Do not translate the English one.

---

## 13. Audit, or rewrite

**Position A.** Rewrite, do not delete. The deliverable is the improved text.

**Position B.** If only an audit was requested, a findings table is the deliverable and no
rewrite is offered.

**Ruling.** Position B as the default, because a rewrite that was not asked for takes the
text out of the writer's hands and quietly replaces their voice with the auditor's. Report
findings with a suggested repair per finding. Produce the full rewrite when it is requested,
and keep the findings table with it so the changes stay reviewable.

---

## 14. First draft, or existing draft

**Position A.** Use when writing or editing.

**Position B.** Never compose against the list. Writing a first draft while avoiding a
blocklist produces constrained, lifeless text.

**Ruling.** Position B. This skill runs on a draft that exists. Composing against a tell list
optimizes for the absence of tells, and the fiction study's clustering result describes
exactly where that lands: machine text clusters in a shared region defined by the absence of
oddity, while human text is dispersed. Avoiding every listed tell is a route into that
cluster, not out of it.

---

## 15. The self-application test

Common tooling in this area fails its own rules. One widely used cleanup skill mandates that
the final text contain no em dash, and its own instruction prose contains one. Another
requires that every text be run through a second skill, while a third states that it
replaces that second pass, so the two cannot both be followed on the same text.

**Ruling.** A tool in this category has to pass its own audit, and the claim has to be
checkable. This file, the skill file, and the other references are written to the rules they
set. Where a rule here is a house style choice rather than a finding, the text says which.
