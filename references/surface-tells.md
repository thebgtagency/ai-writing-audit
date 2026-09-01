# Surface layer: reference

Catalogue of word, sentence, punctuation, and formatting tells. Built from Wikipedia's
"Signs of AI writing" (WikiProject AI Cleanup). Attribution and licence note at the end of
this file.

Weights are set here, not by the catalogue. Weight 2 is a hard finding. Weight 1 is real
but common in human writing and needs company before it means anything. Weight 0 items live
in `false-positives.md` and are never raised.

The source calls itself descriptive rather than prescriptive, and says a pattern is a
potential sign of a problem rather than the problem. Both cautions apply to every entry
below.

## How the layer is scored

One hit is not a finding. The source's own summary of the vocabulary tell states the
principle for the whole layer: one or two of these words may be coincidental, while a text
introducing many of them, many times, is one of the strongest tells available.

So run it as density. Count hits, weight them, divide by words, and read the ratio. A single
weight 2 hit in a long page is a note. Four weight 1 hits in forty words is a verdict.

## Content tells

### Significance inflation, weight 2

The text puffs up its subject by tying arbitrary details to a larger trend, a legacy, or a
broader debate. Appears even on mundane material.

Watch: stands as, serves as, is a testament to, is a reminder of, plays a crucial role,
plays a pivotal role, plays a vital role, plays a key role, underscores its importance,
highlights its significance, reflects broader, symbolizing its enduring, contributing to
the, setting the stage for, marking a shift, represents a shift, key turning point,
evolving landscape, focal point, indelible mark, deeply rooted.

Real example from the source, a 2024 article revision:

> The founding of Idescat represented a significant shift toward regional statistical
> independence

In marketing text the same move appears as a closing paragraph explaining why the product
matters to the industry.

### Credential and coverage stacking, weight 2

Proving importance by listing where the subject was covered, and by characterizing those
outlets rather than saying anything.

Watch: independent coverage, regional media outlets, national media outlets, trade
publications, featured in, profiled in, cited in, written by a leading expert, maintains an
active social media presence.

The source notes this wording became common in tools released from 2025 onward, and that
"active social media presence" was uncommon in human text before about 2024.

### Superficial analysis in participial form, weight 2

A trailing "-ing" clause that looks like a conclusion and states nothing. The most portable
tell on this list, because it survives translation into any register.

Watch: highlighting, underscoring, emphasizing, ensuring, reflecting, symbolizing,
contributing to, cultivating, fostering, encompassing, enhancing, valuable insights, aligns
with, resonates with.

From the source, a census sentence turned into atmosphere:

> the population of Douera stood at approximately 56,998 inhabitants, creating a lively
> community within its borders

Repair: cut the clause. If the claim inside it is worth making, make it as a sentence with
a subject.

### Promotional register, weight 2

Advertisement or travel-guide tone appearing where it was not asked for, including in edits
whose stated purpose was to remove promotional tone.

Watch: boasts a, vibrant, rich, profound, enhancing, showcasing, exemplifies, commitment
to, natural beauty, nestled, in the heart of, groundbreaking, renowned, featuring, diverse
array.

The source records that older models were blatantly positive while newer ones are subtly
positive and avoid obvious superlatives. So the current form of this tell is a paragraph of
mild approval with no fact in it, not the word "best".

### Vague attribution, weight 2

Opinions handed to an unnamed authority, or one source presented as many.

Watch: industry reports, observers have cited, experts argue, some critics argue, studies
have shown, several publications, it is widely believed, is often regarded as.

The source also flags "such as" placed in front of a list that is actually exhaustive,
implying more examples exist.

### The challenges and future prospects outline, weight 2

A closing section built on a fixed formula: despite its strengths the subject faces
challenges, followed by a hopeful line about ongoing initiatives.

Watch: despite its success, faces several challenges, despite these challenges, challenges
and legacy, future outlook, future directions, continues to evolve.

The source is explicit that the tell is the formula and not the mention of challenges. A
text that names a real difficulty and leaves it unresolved is doing the opposite thing.

## Language tells

### The vocabulary list, weight 2 at density, weight 1 for one hit

The words models overuse, grouped by era, because the list moves and an old list produces
false positives on current text.

2023 to mid-2024: additionally, boasts, bolstered, crucial, delve, emphasizing, enduring,
garner, intricate, intricacies, interplay, key, landscape, meticulous, meticulously,
pivotal, underscore, tapestry, testament, valuable, vibrant.

Mid-2024 to mid-2025: align with, bolstered, crucial, emphasizing, enhance, enduring,
fostering, highlighting, pivotal, showcasing, underscore, vibrant.

Mid-2025 onward: emphasizing, enhance, highlighting, showcasing, plus the credential
stacking vocabulary above.

One model family in the source is called out separately for overusing words that sound
scientific: causal, empirical, correlate, and for still overusing underscore in 2026.

Two rules the source attaches to this list, both of which tools routinely break:

1. Take it literally. A word being overused does not make its synonyms overused.
2. Keep context. "Underscore" as a verb is the tell. An underscore character is not, and
   neither is incidental music.

### Copula avoidance, weight 2

Replacing "is" and "are" with something that sounds more active. The source cites a study
finding a drop of more than 10 percent in the use of "is" and "are" in academic writing in
2023, with no comparable movement before that, and notes the effect is strongest in AI
copyedits.

Watch: serves as, stands as, marks, functions as, operates as, represents, boasts,
features, maintains, offers, refers to.

Also the elaborate form: "ventured into politics as a candidate" where "was a candidate"
was available, or "began his career as" for "was".

This is the tell most worth checking in text that a model was asked to improve rather than
to write.

### Vague expression of connection, weight 1

Reaching for abstraction instead of naming a relationship.

Watch: in connection with, connected to, in association with, associated with, particularly
associated, widely associated.

The source says outright that this indirection alone is not enough to allege anything, and
that it counts through abundance and combination.

### Negative parallelism, weight 2

Three shapes, all flagged.

- Not only X but also Y. Also: it is not just X, it is Y.
- Not X, but Y. Also: it's not X, it's Y. Also: no X, no Y, just Z.
- X rather than Y.

The source notes this is common in human writing too, especially in myth-busting listicles,
and is still stereotypically a machine sign. That combination is exactly why it is a
density check. One instance is a rhetorical choice. Three on a page is a shape.

In spoken hooks the A versus B contrast is a format convention, so demote it there. See the
spoken profile in `formats.md`.

### Rule of three, weight 1

Adjective, adjective, adjective. Or short phrase, short phrase, and short phrase. The
source says models use this to make superficial analysis look comprehensive.

Judge by density and by whether the three items are actually different. Three synonyms is a
tell. Three distinct claims is a list. A tricolon in a speech is rhetoric that predates the
models by millennia.

## Punctuation and typography

### Em dash, weight 1, and read the detail before flagging

The source does not say the em dash is a machine mark. It says machine output uses it more
often than nonprofessional human writing of the same genre, puts it where a comma,
parenthesis, or colon would go, and uses it in a formulaic way to over-emphasize clauses.

Two details that matter more than the count:

- Machine em dashes are usually surrounded by spaces, against typographic convention that
  most human em dash users follow.
- The source states this sign is most useful in combination and not by itself, and that it
  appears more on discussion pages than in article text.

The decay is documented. Newer models were tuned to suppress the character, and a July 2026
study cited by the source found that among contemporary models only one used em dashes more
than professional writers, while another used them less. The fiction study reports the same
movement: one recent model release significantly reduced em dash usage.

So a blanket ban on the em dash is not supported by the source it is usually justified with,
and on current text it can point the wrong way. Flag the spaced formulaic pattern at
density. Do not flag a correctly set em dash doing a job.

### Curly quotes and apostrophes, weight 1 at most

Two model families typically produce curly quotation marks and curly apostrophes, sometimes
mixing them with straight ones in the same output. Two other families typically do not.

The source lists so many innocent causes that this rarely survives the gate: word
processors with smart quotes on, the default settings on two major operating systems,
grammar tools, professional typesetting, and citation tools copying a page title. Raise it
only alongside other findings, and never as the lead finding.

### Mixed or inconsistent typography, weight 1

Straight and curly quotes in the same document. Hyphens standing in for en dashes in ranges.
Spacing that changes between paragraphs. These point to text assembled from more than one
source, which is a fact worth knowing even when nothing else is wrong.

## Formatting tells

### Title heading, weight 2

A heading repeating the document title at the top of a document that already has a title.
The model does not know the title exists.

### Title case in headings, weight 2

Capitalizing every main word in section headings. The source calls this a strong tendency.

### Headings that contain only other headings, weight 2

A section with no text of its own, holding subsections.

### Boldface overuse, weight 2

Bold applied mechanically, often to every instance of a chosen phrase, in a key-takeaways
style. The source traces the habit to readmes, fan wikis, how-tos, sales pitches, slide
decks, and listicles.

Test: if the bold were removed, would any reader notice a loss. If bold marks a defined
term the first time it appears, it is doing a job. If it marks whatever seemed important in
that sentence, it is texture.

### Inline-header vertical lists, weight 2

A list where each item opens with a bold header, then a colon, then the description. The
single most recognizable machine layout.

Also flagged: bullets typed as literal characters rather than real list markup, and numbered
lists typed as "1." by hand.

### Emoji as formatting, weight 2 in prose, weight 0 in social captions

Emoji placed in front of headings or bullet points as decoration. This is a document
formatting tell, not a judgment about emoji. In a social caption emoji are native and their
absence can itself read as machine written.

### Heading level jumps, weight 2

Sections that start at the third level with no second level above them. The source notes
this is very unlikely in a manually formatted page, because a person building headings by
hand builds them in order.

### Level 1 headings scattered through a document, weight 2

Top level headings used for ordinary sections, where the top level normally belongs to the
document title alone. The source attributes this to a model translating markdown headings
into another markup and losing the level in the process.

### A thematic break between every section, weight 1

A horizontal rule dividing each section from the next, all the way down. Common in markdown
output, rare in a document a person laid out.

Weight 1 rather than 2, because one or two breaks in a long document is ordinary typography.
The tell is the mechanical repetition: every section, no exceptions.

### Small tables that should have been sentences, weight 1

A table with two columns and three rows holding what a sentence would have said. The source
records this as rare but distinctive. Test: read the table out loud. If it takes fewer words
as a sentence, the table is decoration.

### Markdown where markdown does not belong, weight 2

Asterisk bold, hash headings, or markdown tables pasted into a medium that does not render
them. A near-certain sign of text moved out of a chat window, and one of the few tells on
this list that is close to proof rather than inference.

## Chat leftovers

These are the highest-precision items in the catalogue. They are not stylistic. They are
fragments of a conversation with an assistant that were never removed.

### Assistant register, weight 2

Watch: I hope this helps, Of course!, Certainly!, You're absolutely right!, Would you like
me to, is there anything else, let me know if, here is a, a more detailed breakdown.

Also: text that explains what the text is about to do. "In this section, we will discuss the
background information related to the topic."

Also: instructions addressed to the person who pasted it, still sitting in the document.
"If you plan to add this information, ensure that the content is presented in a neutral
tone."

### Knowledge cutoff and unavailability disclaimers, weight 2

Watch: up to my last training update, as of my last knowledge update, while specific details
are limited, not widely documented, not publicly available, based on available information,
in the provided search results.

The source makes a sharper point about the newer form. When a model cannot find something,
it may state that the information is not documented and then speculate about what it likely
is and why that matters. Both halves are invented, including the claim that the thing is
undocumented. For a person, this often appears as a claim that they maintain a low profile
or keep personal details private.

### Placeholder text, weight 2

Fill-in-the-blank templates the user forgot to fill.

Watch: square brackets around a description rather than a value, [Your Name], [Specific
Topic], [Entertainer's Name], INSERT_URL_HERE, PASTE_LINK_HERE, dates written as 2025-XX-XX,
and parenthetical instructions such as "(Add your channel URL here)".

In a template or an automated sequence this tell has a second life: an unfilled merge field
that shipped. Check for it before every send.

### Prompt refusal fragments and abrupt cutoffs, weight 2

Leftovers of a refusal, or text that stops mid-sentence because a generation ended. The
source lists both as historical, meaning they are rarer now, and both remain conclusive when
present.

## Tells the source records as decayed

Kept for old text, not for current drafts. The source marks these as common from roughly
November 2022 to 2024 and much rarer since.

- Didactic disclaimers: it's important to note, it is crucial to note, worth noting, may
  vary.
- Section summaries: in summary, in conclusion, overall, and a Conclusion section that
  restates the piece.
- Prompt refusal boilerplate.
- Elegant variation, meaning the deliberate avoidance of repeating a word.

Note the pull between the second bullet and the discourse layer. Self-summarizing is listed
here as a decayed surface habit, and it is simultaneously the strongest live finding in the
discourse layer, where explaining your own theme was measured at 77 percent for machine text
against 52 percent for human. The resolution: the phrase "in conclusion" has decayed, the
behaviour has not. Flag the behaviour, not the phrase.

## How this list ages

Every item here is a snapshot. The source page carries its own update banner asking for the
most recent models. The fiction study puts a number on the decay: fine-tuning a model to
imitate human style dropped detection on creative writing from 97 percent to 3 percent.

Two consequences for anyone maintaining this file:

1. Date your additions. An era-tagged list stays usable. An undated list rots into false
   positives.
2. Do not add an item because it feels like AI. The source's own instruction for its
   vocabulary box is to add only what is corroborated. Follow it.

## Attribution

The tells, word lists, and quoted examples in this file are drawn from the Wikipedia page
"Signs of AI writing", maintained by WikiProject AI Cleanup, which is published under
CC BY-SA 4.0. Definitions here are restated in this file's own words. Quoted passages are
marked as quotations. Reuse of those passages carries the same licence.
