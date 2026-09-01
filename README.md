# ai-writing-audit

A skill for auditing and repairing text that reads as machine written. One skill, every
format: a two line direct message, an automated message sequence, an objection reply, a
caption, a carousel slide, a spoken script, a landing page, an essay, an email.

## What makes it different from a word list

Most tools in this space are a list of banned words plus a dash ban. That catches an
unedited first draft and nothing else, because those signatures are the part that gets
removed by the next model release or by a single editing pass.

This skill runs two layers.

The **surface layer** is the word, punctuation, and formatting catalogue, built from
Wikipedia's "Signs of AI writing" field guide.

The **discourse layer** asks structural questions instead: does the text explain its own
point, does everything pull one way, does it resolve by asking the reader to decide, is
anything named. It comes from StoryScope (COLM 2026), which measured 61,608 stories and
separated human from machine text at 93.2 macro-F1 using narrative structure alone, with
no style signals at all. That paper also tested what happens when you clean the surface:
running a rewriter over cliche, redundant exposition, and purple prose moved its detection
by 1.6 points. The structure survived the polish.

Both layers run behind a **false positive gate**, because the sources spend a large part of
their text warning against over-reading, and a tool that finds seven problems in every text
is not a detector.

## What it will not tell you

Whether a machine wrote it. That question has a bad evidence base: one 2025 study puts human
accuracy at chance level, another at 57 percent, and a 2025 preprint puts heavy model users
at about 90 percent, which is one false accusation in every ten. Detector tools are recorded
in the same source as having non-trivial error rates and as breaking under paraphrase.

So the output is a reading verdict, not an authorship verdict, and the skill says so on
every run.

## Install

Copy the folder into your skills directory:

```
~/.claude/skills/ai-writing-audit/
```

Then ask for an audit on a draft. The skill is for text that already exists. It is not for
writing a first draft, and `references/conflicts.md` item 14 explains why composing against
a tell list makes text worse rather than better.

## Files

```
SKILL.md                      the audit loop, the modes, the output contract
references/surface-tells.md   word, punctuation, and formatting catalogue
references/discourse-tells.md the structural layer, with the measured rates
references/false-positives.md what not to flag, and confidence by format
references/formats.md         profiles for nine formats plus a derivation procedure
references/conflicts.md       fifteen disagreements between the sources, and the rulings
TESTS.md                      ten runs across eight formats, including two controls
```

## What it has actually been tested on

Eight formats have a recorded run in `TESTS.md`: direct message, automated sequence,
objection reply, caption, carousel, spoken script, long page, email. Two controls,
human-written and rough, come back with zero findings.

Formats without a recorded run are covered by the four-question derivation procedure at the
end of `references/formats.md`, and the skill does not claim measured coverage of them.

## Honest limits

Neither source measured the formats most text actually takes. The Wikipedia guide was built
on encyclopedia articles and says outright that some of its signs may not apply outside that
context. The fiction study was built on roughly 5,000 word stories and says that shorter
texts cannot support its features. Everything between those two, meaning messages, captions,
slides, ads, emails, and scripts, is covered here by argued transfer. Each transfer states
the reasoning that carries it so the reasoning can be checked rather than trusted, and the
parts that do not transfer are listed as fiction-only and are not applied.

The vocabulary lists are English. They do not survive translation, and the skill reports the
vocabulary layer as not run on text in another language rather than translating the list.

Every word list here ages. Human writing and speech are measurably drifting toward model
output, with a 2024 study finding significant influence in conversational podcasts. The
structural layer ages more slowly, which is the argument for keeping it even though it is
the harder pass to run.

## Sources

- Wikipedia, "Signs of AI writing", maintained by WikiProject AI Cleanup. CC BY-SA 4.0.
- Russell, Rajendhran, Pham, Iyyer, Wieting. "StoryScope: Investigating idiosyncrasies in AI
  fiction." COLM 2026.

## Licence

CC BY-SA 4.0. The skill incorporates and adapts material from a CC BY-SA 4.0 source, so the
same terms carry through. See `LICENSE`.
