# ai-writing-audit

A single skill for auditing and repairing text that reads as machine-written.

Most anti-AI-writing guides check one layer: word choice, punctuation, formatting. That
layer is real, but it is also cheap to fix and it ages out. One model generation removes
a tell and the checklist is stale.

This skill runs two layers.

**Surface tells** are word choice, sentence shape, punctuation, formatting.

**Discourse tells** are how the piece is built: what it explains, what it leaves implied,
how time moves, who acts, whether it acknowledges a reader. These survive a surface
cleanup, because removing them means rewriting the structure.

> "AI style is increasingly fleeting: GPT-5.4 significantly reduced em-dash usage, and
> fine-tuning to mimic human style drops AI detection rates on creative writing from 97%
> to 3%. Discourse-level narrative features are far harder to 'humanize', as changing
> them requires significant structural rewrites rather than simple post-hoc edits."

## Why it is layered by text type

The two bodies of work behind this skill state opposite scope limits, and both say so in
their own text.

Wikipedia's *Signs of AI writing* covers informational prose and notes that tells
specific to fiction are not listed. StoryScope measures narratives averaging ~5,000
words and notes that shorter texts cannot support the features it extracts.

So a flat checklist is wrong in both directions: run the discourse layer on an eight-word
slide and you get noise; run only the surface layer on a long piece and synthetic text
walks through.

Section 0 of the skill picks the layer from what the text actually is. A two-line direct
message, a carousel slide, a spoken script, and an essay do not get the same rules.

## What is in it

- 16 surface rules with repair instructions, not just a banned-word list
- 6 discourse rules drawn from measured narrative features
- 3 documented collisions between the layers, with a resolution for each
- Short-form handling for DMs, slides, captions and spoken scripts
- A "what is not a tell" section, including the non-native-writer false positives
- An anti-overfit section: the failure mode where cleaned text starts performing

## Collisions worth knowing about

One example. The surface layer bans performed intimacy openers (`Look,`, `Here's the
thing`). The discourse measurement records reader-address as a *human* signal. Both are
right about different things: the banned versions are hooks with nothing behind them, the
human signal is an actual aside. The skill resolves this rather than letting whichever
rule runs first win.

Another: "show, don't tell" is standard writing advice, and AI over-applies it. Embodied
emotional expression appeared in 81% of AI stories against 38% of human ones. For text a
model produced, naming the feeling plainly is the correction.

## Use

Drop the folder into your skills directory. The skill runs after a draft exists. Do not
compose against the checklist; composing against a blocklist produces constrained,
lifeless text, which is its own tell.

## Sources

- Wikipedia, *Signs of AI writing* (WikiProject AI Cleanup). Text available under
  CC BY-SA 4.0.
- Russell, Rajendhran, Pham, Iyyer, Wieting. *StoryScope: Investigating idiosyncrasies in
  AI fiction.* COLM 2026. arXiv:2604.03136. 10,272 prompts, 61,608 stories, 304 features
  per story, five models.

Surface repair patterns were consolidated from working style guides and deduplicated
against both sources.

## Licence

CC BY-SA 4.0. See [LICENSE](LICENSE).

Rules derived from Wikipedia's guide carry that project's share-alike terms, so the whole
skill is released under the same licence rather than a more permissive one.
