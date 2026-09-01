# Format profiles: reference

A tell is only a tell when it appears without a job. What counts as a job changes with the
medium, so the same sentence can be a finding in one format and correct in another. This
file holds the profiles. If the text in front of you is not listed, build a profile with
the four questions at the end, then run the audit.

Each profile gives: the length band, which layers run, the hard flags for that medium, the
patterns that are native and must never be flagged, and the pass bar.

Neither source measured any of these formats. See `false-positives.md`, "Confidence by
format". State the confidence line in the verdict.

## 1. Direct message, first touch

**Band.** 8 to 60 words. Two to four lines.

**Layers.** Surface, full. Discourse, reduced to three checks: is there one specific thing
in here that could only have been written to this person, is there an ask that is smaller
than the thing being sold, and does the last line explain itself.

**Hard flags.**
- An opening compliment with no object. "Love your content" flags. "Love that you shoot the
  before-and-after in one take" does not.
- A stated reason for reaching out that is a category rather than an observation. "I work
  with brands in your space" is a category.
- Any sentence whose only work is transition. At this length there is no room for one.
- The closing question that asks for permission to send more. "Would you be open to me
  sending over some ideas" is the most common machine close in this format.
- Vocabulary from the AI word list, weighted double here. In 40 words, one "leverage" is
  the whole voice.
- A dash of any kind used as the connector in two consecutive lines.
- Perfect symmetry: two lines of identical length and shape.

**Native, never flag.**
- Second person throughout.
- No greeting, or a bare first name.
- Sentence fragments.
- No citation, no source, no evidence beyond what the sender saw.
- Lowercase start, missing final period. In this medium that reads as typed by a person.

**Pass bar.** Read the message and ask what the sender would have had to look at to write
it. If the answer is "nothing", the message fails no matter how clean the prose is. This is
the whole audit at this length.

**Worked example.**

Before:
> Hi Priya, I hope this message finds you well. I came across your studio and was really
> impressed by your work and the value you provide to your community. I help businesses
> like yours streamline their booking process and unlock more revenue. Would you be open to
> a quick chat this week?

Findings: hollow compliment with no object, category reason, two AI-list items
("streamline", "unlock"), the permission close, and a discourse finding, nothing in the
message required looking at the studio.

After:
> Hi Priya, your booking page sends people to a form and then to WhatsApp. That handoff is
> where most studios lose the slot. I rebuilt that step for two ceramics studios last
> month, both fill the same day now. Want the 90 second version of what changed?

What moved: the specific observation replaces the compliment, the claim carries a number
and a timeframe, and the ask is smaller than the sale.

## 2. Automated or templated message sequence

**Band.** Same as above, times however many people receive it.

**Layers.** Surface, full. Discourse, the same three checks. Then a fourth pass that only
this format needs.

**The scale pass.** A template is read by one person at a time but written for many, and
the tells of that gap are specific.

- Merge fields sitting where a human would have written something specific. "Loved your
  post about {topic}" reads as a machine even when the field fills correctly, because the
  sentence around it is the same for everyone.
- A compliment that has to be true of every recipient. Anything that survives being sent to
  a thousand accounts is a category, not an observation.
- Follow-up messages that reference an earlier message the recipient may never have read.
  "Just following up on my note below" fails when the note below was also automated.
- Identical sentence rhythm across steps in the sequence. Audit the sequence as one
  document, not message by message. Three messages with the same shape is a stronger tell
  than any single word.
- Time references that a machine schedule betrays: "just saw", "this morning", "quick one
  before the weekend" attached to a send that fires on a timer.

**Native, never flag.**
- Merge fields themselves. The tell is the sentence around the field.
- Repeating the offer across steps. A sequence is allowed to be a sequence.
- Short follow-ups with no new content, if they are honest about being short.

**Pass bar.** Print three steps of the sequence together. If a recipient reading all three
would conclude they were the only person who got them, it passes. If any single sentence
would look absurd sent to a thousand people, rewrite that sentence, not the template.

**Repair rule specific to this format.** Do not fix a hollow line by adding another merge
field. That deepens the tell. Fix it by narrowing the audience until a true, specific
sentence is possible for everyone in it.

## 3. Objection reply

**Band.** 15 to 120 words.

**Layers.** Surface, full. Discourse, four checks: does the reply concede anything, does it
name the cost, is the resolution external, and does it end by handing the decision back
without a step.

**Hard flags.**
- The reframe with no concession. Answering "too expensive" with "it is an investment"
  concedes nothing and is the most recognizable machine move in this format.
- Three benefits in a row where the objection asked one question.
- Empathy as a preamble. "I completely understand, and that is a really fair question"
  costs nothing and delays the answer.
- Resolution by internal understanding. "It really comes down to whether you are ready to
  commit" ends the exchange inside the reader's head. The discourse layer flags this
  directly, feature 18 of the AI list.
- A rhetorical question used as an answer.
- Any claim in the reply that was not in the original pitch. Objection handling that
  invents new promises is a symptom, not a style problem.

**Native, never flag.**
- Repeating the objection back. That is how people confirm they heard it.
- Second person, imperatives, fragments.
- A direct price or a direct no. Bluntness in this format is not a tell.

**Pass bar.** The reply must contain one sentence that is true and unhelpful to the sale.
A named limit, a case it is wrong for, a number that is worse than the reader hoped. If
every sentence pulls one way, the discourse layer flags it as a single causal track, and
the reader hears it as a script whether or not any word is on a list.

**Worked example.**

Before:
> I completely understand, and that is a really fair question. I would say this is less of
> a cost and more of an investment in your growth. Most of our clients see a return within
> the first month, and the systems you get are yours forever. It really just comes down to
> whether now is the right time for you to take that step.

Findings: empathy preamble, cost-to-investment reframe with no concession, unattributed
"most of our clients", ownership benefit that answers a question nobody asked, and a close
that resolves internally.

After:
> It is a lot of money for a first project, yes. Two of the six studios I did this for made
> it back inside a month. One took four months because their list was cold, and if your
> list is cold too, that is the honest range. If you want to see the four month one, I will
> send the numbers and you can decide from those.

What moved: the price objection is conceded, the counter-evidence is named, the range
includes the bad case, and the next step is external and small.

## 4. Caption

**Band.** 20 to 220 words.

**Layers.** Surface, full. Discourse, five checks: does it state its own moral, is there
an aside that does not serve the point, is anything named, does it end by explaining
itself, and is the emotion labeled or embodied.

**Hard flags.**
- The closing lesson line. "Consistency beats talent every time." This is AI feature 1 and
  the single most common caption tell.
- The hook that announces itself. "Here is what nobody tells you about" and its family.
- A first line that could sit on top of any caption in the niche.
- Question, answer, lesson in a fixed three beat shape.
- Body-sensation emotion. "My stomach dropped."
- A call to action bolted on with no connection to the text above it.
- Hashtag blocks that restate the caption in list form.

**Native, never flag.**
- Emoji. Zero emoji can itself read as machine written in this medium.
- Line breaks every sentence.
- Sentence fragments and lowercase.
- Second person.
- A short explicit call to action, if it follows from the text.

**Pass bar.** Delete the final line. If the caption is better without it, the final line was
the machine talking. Most captions improve.

## 5. Carousel or slide

**Band.** 3 to 25 words per slide, 5 to 12 slides.

**Layers.** Surface, per slide and across the deck. Discourse runs on the deck as a whole,
never on one slide.

**Hard flags, per slide.**
- Title case on a slide that is a sentence.
- A slide that only restates the previous slide in different words.
- Parallel grammar on every slide in the deck. Six slides that all start with a verb is a
  shape, not a design.
- The final slide that summarizes the deck. A deck that has to summarize itself did not
  land.
- Colon-heavy headers: "Step 3: Build the System".
- A number claim with no unit or source.

**Hard flags, across the deck.**
- Slide count that matches the promise too neatly. Five ways, five slides, five identical
  shapes.
- No slide that pulls sideways. A deck with an exception or a case that failed reads human.
- The single causal chain: every slide follows from the last with no reversal.

**Native, never flag.**
- Fragments, no verbs, no punctuation.
- Repetition of one key phrase as a spine.
- Bold as emphasis. This is a visual medium.
- Imperatives.

**Pass bar.** Shuffle the middle slides. If the deck reads the same, it is a list wearing a
narrative. Also: read only the slide headers. If the headers alone tell the whole thing,
the body text is decoration and the deck is longer than its content.

## 6. Spoken script

Covers voiceover, reels, sales video, teleprompter, webinar, podcast notes.

**Band.** Any. Judged in seconds, not words. Roughly 140 to 160 words a minute.

**Layers.** Surface, with the word list demoted, see below. Discourse, full, because a
script has time and order.

**The spoken override.** Human speech is measurably drifting toward model output. The
Wikipedia guide records a 2024 study finding significant LLM influence in conversational
podcasts. So a phrase can be both a documented tell and ordinary current speech. In this
format the spoken test outranks the word list: read the line out loud at speaking pace. If
a person would say it, it stays, even if it is on a list. If they would not, it goes, even
if it is on no list.

**Hard flags.**
- A sentence you have to re-read to say. Any clause stack that needs a comma to survive.
- Written-only connectives: "moreover", "furthermore", "that said", "in conclusion".
- Symmetrical pairs. "It is not about the tool, it is about the system." Speech does not
  balance that neatly without effort, and the balance is audible.
- Lists of three read at speed. On the page a tricolon is rhetoric. Spoken, a bare three
  item list with no beat between items is the clearest machine tell in this format.
  Carve-out: a count announced to the listener has a job. "There are three things" followed
  by three items is structure the listener asked for and is not flagged. The finding is the
  unannounced triad delivered at speed, and the announced list where the three items are
  near synonyms.
- Numbers written as digits with no spoken form given. "$1,247/mo" has no pronunciation.
- Sentences over about 25 words with no breath point.
- An outro that summarizes what was just said.

**Native, never flag.**
- Repetition, including exact repetition of a phrase. That is how listeners keep up.
- False starts, "look", "so", "here is the thing", if they match the speaker.
- Fragments and one word sentences.
- Direct address.
- Contradicting yourself and correcting it out loud.

**Pass bar.** Read the whole script aloud once, timed. Mark every place you stumbled or ran
out of breath. Those marks are the findings. A script that has never been read aloud has
not been audited, and this skill should say so in the verdict rather than claim a pass.

## 7. Long page

Covers landing page, sales page, essay, article, documentation, newsletter.

**Band.** 300 words and up.

**Layers.** Both, full. This is the only format where the discourse layer runs at the
strength the source measured it, and even here the source measured fiction.

**Hard flags.**
- Section headers in title case, or headers that contain only other headers.
- A conclusion section that restates the page.
- Every section the same length. Even section weight is a template, not an argument.
- The negative parallelism family: "not X, but Y", "not only X but also Y", "X rather than
  Y", used more than once on a page.
- Paragraphs that all open with a transition word. Note that a transition word alone is
  listed by the source as an ineffective indicator. The finding here is the pattern across
  paragraphs, not any single instance.
- Vague attribution: "experts say", "many believe", "studies have shown", with nothing
  named.
- Promotional register with no fact under it.
- Bold scattered as texture rather than as emphasis on a specific term.
- Superficial analysis in participial form: "highlighting the importance of", "reflecting a
  broader shift toward", "underscoring the need for". These are grammatical padding that
  looks like a conclusion.
- A single tidy causal chain from problem to solution with no cost, no exception, no
  section that complicates the pitch.

**Native, never flag.**
- Headings, bullets, and tables in documentation. Structure is the product there.
- Repeated calls to action on a sales page.
- Long pages. Length is not a tell.

**Pass bar.** Two tests. First, find the paragraph that costs the writer something. If no
paragraph concedes anything, the page is a single track and the discourse layer flags it.
Second, cut the page to a quarter. Whatever you cut without loss was never load bearing.

## 8. Email

**Band.** 40 to 300 words.

**Layers.** Surface, full. Discourse, the four objection-reply checks plus one: does the
subject line describe the email or advertise it.

**Hard flags.**
- Subject line in title case, or a subject that is a benefit statement.
- "I hope this email finds you well" and the whole opening pleasantry family.
- A first paragraph that explains why the writer is writing before saying anything.
- Sign-off stack: a close, a name, a title, a company, a tagline, a booking link.
- Bullet lists inside a message under 100 words.
- P.S. lines that carry the real ask. That is a template convention, not a person.

**Native, never flag.**
- A greeting and a sign-off.
- Reference to a previous thread.
- One link.

**Pass bar.** The first sentence has to be the reason. If the reason arrives in sentence
three, the first two are a machine warming up.

## 9. Format not on this list

Answer four questions about the text, then run the audit with the answers as the profile.

1. **How long is it and how long is the reader's attention?** Under about 60 words, the
   discourse layer collapses to three checks: specificity, stance, and whether the last
   line explains itself. Over about 800 words, the discourse layer leads and the surface
   layer becomes supporting evidence.
2. **Is it read, heard, or seen?** Heard means the spoken override applies and the word list
   is demoted. Seen, meaning slides, thumbnails, packaging, means fragments and parallel
   structure are native and the audit moves to the deck level.
3. **One reader or many?** Written for many and delivered as one, meaning templates, ads,
   sequences, triggers the scale pass in profile 2: any sentence that has to be true of
   everyone is a category, and categories read as machine.
4. **What would the writer have had to know to write this?** This is the question that
   works in every format and it is the one that catches text no word list will catch. If
   the answer is "nothing in particular", no amount of surface repair will fix the reading.

Write the derived profile into the audit output so the reader can argue with the profile
rather than only with the findings.
