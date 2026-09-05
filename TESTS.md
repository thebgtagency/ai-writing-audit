# Test log

Sixteen runs across ten formats, plus three controls. Two of the ten formats are derived
profiles, built by the procedure in SKILL.md under "Adapting to a new format". Every claim the skill makes about a
format is backed by a run recorded here. Formats not listed here are covered only by the
derivation procedure in `references/formats.md`, and the skill says so rather than claiming
coverage it has not tested.

All names, businesses, and numbers in these tests are invented.

Controls exist because a tool that finds problems in every text is not a detector. Cases 9
and 10 are drafts a person wrote badly and humanly, and both must come back clean. Case 12
is the harder control: a human draft that carries three machine-leaning values on purpose,
and still has to pass. If a change to this skill makes a control fail, the change is wrong.

## Case 1. Direct message, first touch

**Input, 57 words**

> Hey Marcus! Hope you're doing well. I've been following your gym content for a while and
> I have to say, your commitment to helping people transform their lives is truly
> inspiring. I work with fitness coaches to streamline their client onboarding and unlock
> more consistent revenue. Would you be open to a quick chat this week to explore some
> ideas?

**Output**

```
MODE: deliverable
FORMAT: direct message, first touch
LENGTH: 57 words        LANGUAGE: English (vocabulary layer: run)
VOICE SAMPLE: none supplied
CONFIDENCE: argued transfer, weakest case. Neither source measured messages.
MODEL: unknown
VERDICT: reads machine (7 weighted findings, count rule for text under 60 words,
         spread 2 of 7 themes and not eligible for an origin claim at this length)

STRUCTURAL TEMPLATE
agents: Marcus, named. The sender, never named.
events: null. Nothing happens.
causality: null. Two claims sit next to each other.
revelation: null.
temporal order: null.
setting: null.

FINDINGS
1. [discourse, w2, theme 4] Check 6, named reference. Nothing here required looking at Marcus.
   Evidence: "following your gym content for a while", "commitment to helping people"
   Why: both sentences survive being sent to any coach. Named reference check fails.
   Repair: one observation about his actual content, or do not send.
2. [surface, w2] "your commitment to helping people transform their lives is truly inspiring"
   Tell: promotional register with no fact under it
   Repair: CUT
3. [surface, w2] "streamline"  Tell: vocabulary list, 2024 to 2025 era  Repair: "fix"
4. [surface, w2] "unlock more consistent revenue"  Tell: promotional register
   Repair: name the number or cut
5. [format, w2] "Would you be open to a quick chat this week"
   Tell: permission close. The ask is larger than the sale.
   Repair: an ask smaller than the sale
6. [surface, w1] "Hope you're doing well"  Tell: pleasantry opening  Repair: CUT
7. [discourse, w2, theme 7] Check 5, moral polarity. No stance. Nothing here could be
   disagreed with.

GATED
- "Hey Marcus!" exclamation mark : native to the format
- second person throughout : native
- no evidence or citation : native, nobody cites in a message
- checks 2, 3, 4, 7, 8, 9, 10 : NOT RUN. 57 words, and Pass 0 allows only checks 1, 5 and 6
  below 60. Their silence is a silence, not a pass

THEME SPREAD: themes 4 and 7. Two of seven, from the three checks the length allowed. The
assessment bar of four cannot be reached here by construction, so no origin claim is
available. Deliverable mode is unaffected and all seven findings stand.

WHAT IS WORKING
- Nothing yet. The draft has no plain verb, no specific, and no roughness to protect.

REWRITE
Marcus, your intake form asks for goals before it asks for a phone number, so people
bounce at question four. I moved that question to the end for two coaches this spring and
both stopped losing the form. Want the two lines I changed?
```

**Note.** The rewrite adds facts. In real use those facts have to come from the sender.
The skill flagged this correctly during the run: the repair for finding 1 is written as
"one observation about his actual content, or do not send", not as an instruction to
invent one. Recorded here because it is the failure mode most likely to appear in practice.

## Case 2. Automated message sequence, three steps

**Input, 3 steps, 61 words total**

> 1: Hey {{first_name}}! Loved your recent post about {{topic}}. You're clearly passionate
> about what you do.
> 2: Just following up on my message below in case it got buried!
> 3: Hey {{first_name}}, last one from me. I help brands like {{company}} scale their
> content. Worth a chat?

**Output**

```
MODE: deliverable
FORMAT: automated message sequence
LENGTH: 61 words across 3 steps
CONFIDENCE: argued transfer
MODEL: unknown
VERDICT: reads machine (8 weighted findings, spread 1 of 7 themes)

FINDINGS
1. [scale, w2] "Loved your recent post about {{topic}}"
   Tell: the sentence around the merge field is identical for everyone. The field fills, the
   observation stays empty.
   Repair: narrow the audience until a specific true sentence is possible for all of them.
2. [scale, w2] "You're clearly passionate about what you do"
   Tell: has to be true of every recipient, so it is a category, not an observation.
   Repair: CUT
3. [scale, w2] "Just following up on my message below in case it got buried"
   Tell: references an earlier message that was also automated. Nothing was buried.
   Repair: CUT the step, or make step 2 carry new content.
4. [scale, w1] All three steps open with the same shape: greeting, claim, ask.
   Repair: change the shape of one step, not its words.
5. [surface, w2] "brands like {{company}}"  Tell: category reason for reaching out
6. [surface, w2] "scale their content"  Tell: promotional register with no fact
7. [format, w2] "Worth a chat?"  Tell: permission close
8. [discourse, w2, theme 4] Check 6, named reference. Fails in all three steps.

GATED
- merge fields themselves : native. The tell is the sentence around the field.
- repeating the offer across steps : native, a sequence is allowed to be a sequence
- step 3 being short : native
- check 9, reader address : second person is native to the format, not scored
- check 10, recontextualization : silent. Three steps, no fact placed to reframe an earlier
  one. At 61 words there is not enough text to call the silence a finding

THEME SPREAD: theme 4 only. One of seven. Seven of the eight findings are scale, surface or
format tells rather than discourse, which is the honest shape of this format: a sequence
fails at the template level before it fails at the structural one.

WHAT IS WORKING
- Step 3 says "last one from me", which is honest about the medium and reads human.
  Keep it.

REWRITE
1: {{first_name}}, your last three posts are all captioned from the same template. That is
usually a scheduling problem, not a writing one.
2: The fix is about ten minutes of setup. Happy to describe it here rather than on a call.
3: Last one from me. If content is not the bottleneck right now, ignore this.
```

**Note.** Audited as one document. Step 4 finding is only visible across steps, which is
why the profile says to print the sequence together.

## Case 3. Objection reply

**Input, 62 words**

> Totally understand, and I appreciate you being upfront with me! A lot of our best clients
> said the exact same thing before they started. At the end of the day, it really comes down
> to how badly you want this. The people who see results are the ones who decide to bet on
> themselves. Let me know when you're ready to take that step!

**Output**

```
MODE: deliverable
FORMAT: objection reply ("I need to think about it")
LENGTH: 62 words
CONFIDENCE: argued transfer
MODEL: unknown
VERDICT: reads machine (7 weighted findings, density 11.3 per 100 words,
         spread 3 of 7 themes)

FINDINGS
1. [discourse, w2, theme 3] Check 4, internal resolution.
   Evidence: "comes down to how badly you want this", "decide to bet on themselves",
   "when you're ready to take that step"
   Why: three sentences resolve the exchange inside the reader's head. This is AI feature
   18 in the discourse catalogue and it is the defining move of this format's failure.
   Repair: replace with one external, small, checkable next step.
2. [discourse, w2, theme 1] Check 2, single track. Nothing is conceded and the objection
   is not answered anywhere.
3. [surface, w2] "Totally understand, and I appreciate you being upfront"
   Tell: empathy preamble that costs nothing and delays the answer  Repair: CUT
4. [surface, w2] "A lot of our best clients said the exact same thing"
   Tell: vague attribution, quantity unspecified  Repair: name how many, or cut
5. [surface, w1] "At the end of the day"  Tell: filler  Repair: CUT
6. [discourse, w2, theme 7] Check 5, moral polarity. The reader is sorted into people who
   decide and people who do not. Nothing ambivalent, no case where the answer is no.
7. [format, w2] No sentence in the reply is true and unhelpful to the sale.

GATED
- exclamation marks : native to the medium
- second person : native
- short length : native, and correct here
- check 9, reader address : second person is native, not scored
- check 10, recontextualization : silent at 62 words, and an objection reply is answering
  rather than disclosing, so a reframe is not the expected shape here

THEME SPREAD: themes 1, 3 and 7, each carrying a weight 2 hit. Three of seven, one short of
the assessment bar. In deliverable mode that changes nothing and the rewrite still runs.
Recorded because it is the closest a legacy case comes to the bar without meeting it.

WHAT IS WORKING
- Nothing. Every sentence pulls one direction.

REWRITE
Thinking about it is the right call at this price. The part people usually need to check is
whether they have four hours a week, because below that it does not work and I would rather
you find that out now. If it helps, I can send the week-one checklist so you can look at
the hours before deciding.
```

## Case 4. Caption

**Input, 78 words**

> Most people think consistency is about motivation.
>
> It's not. It's about systems.
>
> When I first started posting, I would wait until I felt inspired. Some weeks I posted six
> times. Some weeks I posted nothing. My stomach would drop every time I opened the app.
>
> Then I built a simple process, and everything changed.
>
> Consistency isn't a personality trait. It's a decision you make once and then protect.
>
> Which one are you right now?

**Output**

```
MODE: deliverable
FORMAT: caption
LENGTH: 78 words
CONFIDENCE: argued transfer
MODEL: unknown
VERDICT: reads machine (9 weighted findings, density 11.5 per 100 words,
         spread 4 of 7 themes)

STRUCTURAL TEMPLATE
agents: the writer, unnamed.
events: a posting habit changed. Undated.
causality: inspiration -> irregularity -> process -> everything changed. The last link is
  asserted and empty.
revelation: null.
temporal order: linear.
setting: null.

FINDINGS
1. [surface, w2] "It's not. It's about systems." and "Consistency isn't a personality
   trait. It's a decision"
   Tell: negative parallelism, twice in 78 words. Once is a rhetorical choice, twice is a
   shape.
   Repair: keep at most one, and only if the second half is concrete.
2. [discourse, w2, theme 1] Check 1, self-explaining. "Consistency isn't a personality
   trait. It's a decision you make once and then protect."
   Tell: the closing lesson line. The caption states its own moral.
   Repair: CUT. Test applied: the caption is better without the final two lines.
3. [discourse, w2, theme 3] Check 3, tidy causality. "Then I built a simple process, and
   everything changed."
   Tell: the causal chain has no content. The thing that changed is never named.
   Repair: name the process in one sentence, or cut the claim.
4. [discourse, w2, theme 2] Check 7, emotion handling. "My stomach would drop"
   Tell: embodied emotion as the default carrier. Measured at 81 percent for machine text
   against 38 percent human.
   Repair: "I felt sick about it" or name what actually happened.
5. [surface, w1] Opening line is a "most people think X" hook that announces itself.
6. [discourse, w2, theme 3] Check 2, single track. No week where the system failed, no
   cost named.
7. [format, w2] The closing question is rhetorical and expects no answer.
8. [surface, w1] Every paragraph is one to two lines of identical weight.
9. [discourse, w2, theme 6] Check 10, recontextualization. Added on rerun. Nothing later
   changes what an earlier line meant. "everything changed" is the place a reframe would
   sit, and it is filled with an assertion instead.
   Repair: name what the process actually was, and put it after the belief it corrects.

GATED
- line breaks every sentence : native
- second person : native
- contractions and fragments : native
- zero emoji : not flagged, and not required either
- check 9, reader address : "Which one are you right now?" addresses the reader, but second
  person is native to a caption, so it is not scored in either direction. Finding 7 handles
  the rhetorical question as a format tell instead

THEME SPREAD: themes 1, 2, 3 and 6, each carrying a weight 2 hit. Four of seven, which meets
the assessment bar. This is the shortest text in the file that reaches it, at 78 words.

WHAT IS WORKING
- "Some weeks I posted six times. Some weeks I posted nothing." Specific, uneven, and the
  only place the draft shows rather than states. Protect it.

REWRITE
When I started posting I waited until I felt like it. Some weeks that was six posts. Some
weeks nothing, and then a month of nothing.

What fixed it was writing Sunday's four captions on Saturday morning, in one sitting, badly.
The badly part matters. Three of the four are worse than what I used to post when I waited.

The fourth one usually carries the week.
```

**Note.** Finding 4 is the check that caught a line every writing course would praise. It
is recorded because it is the clearest case where this skill contradicts standard advice,
and the contradiction is the measured one in `references/conflicts.md`, item 9.

## Case 5. Carousel, eight slides

**Input**

> 1: 5 Mistakes Killing Your Client Retention
> 2: Mistake 1: You Don't Onboard Properly
> 3: Mistake 2: You Don't Communicate Enough
> 4: Mistake 3: You Don't Set Expectations
> 5: Mistake 4: You Don't Ask For Feedback
> 6: Mistake 5: You Don't Celebrate Wins
> 7: Fixing these 5 mistakes will transform your retention and unlock sustainable growth.
> 8: Follow for more client retention tips.

**Output**

```
MODE: deliverable
FORMAT: carousel, 8 slides
LENGTH: 62 words across 8 slides
CONFIDENCE: argued transfer
MODEL: unknown
VERDICT: reads machine (9 weighted findings, spread 2 of 7 themes)

FINDINGS
1. [deck, w2] Slides 2 through 6 are the same grammatical shape five times: "Mistake N: You
   Don't [verb]".
   Repair: break the pattern on at least two slides. One can be a number, one a sentence a
   client actually said.
2. [surface, w2] Title case on every slide, and every slide is a sentence.
   Repair: sentence case.
3. [surface, w2] "Mistake 1:" colon headers on five consecutive slides.
   Tell: inline-header list shape, the most recognizable machine layout.
4. [deck, w2] Slide 7 summarizes the deck. A deck that has to summarize itself did not land.
   Repair: CUT slide 7.
5. [surface, w2] "transform your retention and unlock sustainable growth"
   Tell: promotional register, two vocabulary items, no fact.
6. [deck, w2, theme 1] Check 2, single track, run on the deck. No slide pulls sideways.
   No exception, no case where the fix failed.
7. [deck, w1] Five mistakes, five slides, five identical shapes. The count matches the
   promise too neatly.
8. [deck, w2, theme 4] Check 6, named reference, run on the deck. No slide carries a
   number, a name, or a date.
9. [format, w1] Slide 8 is a generic follow ask with no connection to the deck.

GATED
- fragments and missing verbs : native to slides
- bold as emphasis : native, this is a visual medium
- eight slides : not a finding. Deck length is not a tell.
- check 9, reader address : second person is native to a slide, not scored
- check 10, recontextualization : NOT RUN as a scored check. The deck is 62 words and the
  shuffle test below covers the same ground more directly for this format

THEME SPREAD: themes 1 and 4. Two of seven. The deck fails mostly on repetition and layout,
which are deck and surface tells, and the discourse layer adds only two themes. A carousel
does not carry enough text to reach the bar, and this run is the evidence for that claim
rather than an assertion of it.

WHAT IS WORKING
- The topic is narrow and the deck knows what it is about. Keep the scope.

SHUFFLE TEST
Slides 2 through 6 can be reordered with no loss. The deck is a list wearing a narrative.
A real order would put the mistake that costs the most money first and say why.

REWRITE (slides 1 to 6, the rest cut)
1: Clients do not leave because of the work
2: They leave in week three, not month six
3: Nobody told them what week three feels like
4: Set the expectation in the intake call. One sentence.
5: "Week three is the boring one. It is supposed to be."
6: My churn went from 4 in 10 to 1 in 10 after that sentence
```

## Case 6. Spoken script, roughly 30 seconds

**Input, 76 words**

> If you're struggling to get clients, there are three things you need to fix immediately.
> First, your offer isn't specific enough. Second, you're not following up consistently.
> And third, you're not tracking your numbers. Moreover, most people focus on tactics when
> the real issue is positioning. It's not about doing more, it's about doing the right
> things. Fix these three areas and you'll see a significant improvement in your results.
> Let me know your thoughts below.

**Output**

```
MODE: deliverable
FORMAT: spoken script, roughly 30 seconds at speaking pace
LENGTH: 76 words
CONFIDENCE: argued transfer, and human speech is measurably drifting toward model output
MODEL: unknown
VERDICT: reads machine (9 weighted findings, spread 4 of 7 themes)

READ-ALOUD PASS: performed. Stumbles marked below.

STRUCTURAL TEMPLATE
agents: the listener, addressed. No one else.
events: null. Three faults are asserted, none happens.
causality: null. The three items are a list, not a chain.
revelation: null.
temporal order: null.
setting: null.

FINDINGS
1. [spoken, w2] "Moreover"
   Tell: written-only connective. Stumbled on read-aloud. Nobody says this out loud.
   Repair: CUT, or "and honestly".
2. [spoken, w2] "It's not about doing more, it's about doing the right things."
   Tell: symmetrical pair. Audible balance. Second half is abstract, so the contrast is not
   paid off.
   Repair: make the second half concrete, or cut the line.
3. [spoken, w2] Bare three item list read at speed, with no beat between items.
   Repair: give one item a sentence of its own, or drop to two items.
4. [surface, w1] "significant improvement in your results"  Tell: promotional register with
   no number.
5. [discourse, w2, theme 1] Check 2, single track. Nothing costs anything, nothing failed.
6. [discourse, w2, theme 4] Check 6, named reference. No number, no name, no case.
7. [spoken, w2] The final line summarizes and then asks for comments. An outro that
   restates what was just said.
8. [surface, w1] "immediately" and "consistently" are adverbs doing no work when spoken.
9. [discourse, w2, theme 6] Check 10, recontextualization. Added on rerun. "Moreover, most
   people focus on tactics when the real issue is positioning" is placed where a reframe
   would go and does not reframe anything: positioning is never connected to the three
   items above it, so no earlier line changes meaning.
   Repair: cut the sentence, or make the third item the thing positioning corrects.

GATED
- "If you're struggling" as an opener : native to the format
- second person : native
- contractions : native
- repetition of "you're" : native, repetition is how listeners keep up
- "three things" as an announced structure : native to spoken teaching, and not flagged as
  rule of three. The count was promised to the listener, so it has a job.
- check 9, reader address : "Let me know your thoughts below" names the medium and turns to
  the listener. Second person is native to a script, so this is not scored as a positive
  either. Finding 7 handles the line as a spoken outro tell instead

THEME SPREAD: themes 1, 4 and 6 from the discourse layer, plus theme 7 by absence, since no
feeling is named anywhere in a script whose whole subject is struggling. Four of seven, and
the bar is met. Note that three of the eight original findings are spoken tells rather than
discourse ones, so the spread and the density are measuring different failures here.

WHAT IS WORKING
- The opening names a specific reader state in six words. Keep it.

REWRITE
If you're not getting clients, it's probably not your offer. I thought it was mine for about
eight months. What actually changed it was following up twice instead of once. Twice. The
second message is the one that gets answered, and it took me a spreadsheet to believe that,
because it feels like pestering and it isn't. That's it. That's the whole video.
```

**Note.** The gate cleared the three item list here while the caption case flagged a triad,
because the count was announced to the listener and therefore had a job. That distinction is
the ruling in `references/conflicts.md` item 3, and this run is where it was checked.

## Case 7. Long page section

**Input, 213 words**

> ## Why Modern Teams Choose Automated Bookkeeping
>
> In today's rapidly evolving business landscape, financial clarity has become a crucial
> differentiator for growing companies. Modern teams are increasingly recognizing that
> manual bookkeeping processes represent a significant bottleneck, underscoring the need for
> a more robust approach.
>
> Our platform serves as a comprehensive solution for businesses seeking to streamline their
> financial operations. By leveraging intelligent automation, teams can reduce
> reconciliation time, improve accuracy, and gain valuable insights into their cash
> position. Industry reports suggest that companies adopting automated workflows see
> meaningful improvements in month-end close times.
>
> ### Key Benefits
>
> - **Time Savings:** Reduce manual data entry significantly.
> - **Accuracy:** Minimize human error across your ledger.
> - **Visibility:** Access real-time financial dashboards.
>
> ### Challenges And Future Outlook
>
> Despite its many advantages, automated bookkeeping faces challenges, including integration
> complexity and change management. However, as the landscape continues to evolve, ongoing
> improvements in machine learning could further enhance accuracy and adoption.
>
> In conclusion, automated bookkeeping is not just a convenience, it's a strategic
> investment in your company's financial future.

**Output**

```
MODE: deliverable
FORMAT: long page section
LENGTH: 213 words
CONFIDENCE: medium. The Wikipedia guide names blogs and editorials as places its patterns
legitimately appear, so this is the closest format to a measured source.
MODEL: unknown
VERDICT: reads machine (density 8.9 per 100 words, spread 4 of 7 themes)

STRUCTURAL TEMPLATE
agents: null. No customer, no team, no person.
events: null. No month-end close ever happens.
causality: manual process -> bottleneck -> platform -> improvement. Unbroken, and every
  link is asserted.
revelation: null.
temporal order: null. No date anywhere in 213 words.
setting: null.

FINDINGS
1. [surface, w2] Vocabulary density: landscape (twice), crucial, robust, leveraging,
   valuable insights, streamline, comprehensive, meaningful. Eight items in 213 words.
   Tell: the strongest form of the vocabulary tell is many of them, many times.
2. [surface, w2] "underscoring the need for", "seeking to streamline"
   Tell: participial pseudo-analysis
3. [surface, w2] "Industry reports suggest that companies adopting automated workflows see
   meaningful improvements"
   Tell: vague attribution plus unquantified claim. Which reports, how much improvement.
   Repair: name one source and one number, or cut the sentence.
4. [surface, w2] "Our platform serves as a comprehensive solution"
   Tell: copula avoidance plus promotional register. "Our platform does X" was available.
5. [surface, w2] "Challenges And Future Outlook" section
   Tell: the challenges-and-future-prospects formula, including the "Despite its many
   advantages" opening and the hopeful close.
   Repair: name a real limitation and leave it unresolved, or cut the section.
6. [surface, w2] "In conclusion" closing paragraph that restates the page.
7. [surface, w2] "is not just a convenience, it's a strategic investment"
   Tell: negative parallelism, in the closing position.
8. [surface, w2] Title case in both headings.
9. [surface, w2] Inline-header bullet list: bold label, colon, description, three times.
10. [discourse, w2, theme 3, WEAK] Check 3, tidy causality. Single chain from problem to
    solution, no paragraph costs the writer anything, and the one section that could have
    (Challenges) resolves itself in the same paragraph. Labelled weak under gate question 4:
    human mean 3.92 against AI 4.20. The verdict does not rest on it, because finding 5
    covers the same span as a weight 2 surface tell.
11. [discourse, w2, theme 4] Check 6, named reference. No customer, no number, no product,
    no date in 213 words.
12. [discourse, w2, theme 1] Check 1, self-explaining. "In conclusion, automated bookkeeping
    is not just a convenience, it's a strategic investment." Finding 6 records the same span
    as a surface tell. Counted once, tagged here so the theme is visible to the spread line.
13. [discourse, w2, theme 6] Check 10, recontextualization. Added on rerun. The Challenges
    section is the one place a reframe was available, and it cancels itself inside a single
    paragraph with "However".
    Repair: let the limitation stand unresolved, which is also finding 5's repair.

GATED
- headings and bullets on a long page : native. Structure is the product here.
- length : not a tell
- "However" once : weight 0, transition words in isolation are an ineffective indicator
- check 9, reader address : the page never turns to the reader and never names its own
  medium. Not scored, because a product page addressing the reader is neither expected nor
  unexpected, and the paper's 67 against 39 was measured on fiction where third person is
  the default
- check 2, single track : ran, and its finding is the same span as finding 10. Counted once
- check 5, moral polarity : ran, found nothing. There is no actor in this text to be right
  or wrong about, which is a property of the format rather than a pass
- check 7, emotion handling : ran, found nothing. No feeling is in scope on a product page
- check 8, order : ran, found nothing. There are no events, so there is no order available
  to subvert. Again a property of the format
  Added on the September 2026 recheck. The three preceding rows were silent in the original
  run and unrecorded, which is the failure the silence map now prevents in derived profiles

THEME SPREAD: themes 1, 3, 4 and 6. Four of seven, with a weight 2 hit in 1, 4 and 6 and a
weak hit in 3. The bar is met on three themes carrying weight 2. This is the legacy case
that most closely matches case 11, which was written from scratch under the new rules, and
the two agree.

WHAT IS WORKING
- The three benefit labels are the right three benefits. The labels survive; the
  descriptions under them do not.

CUT TEST
Reduced to a quarter, nothing load bearing is lost. That is the finding behind all the
others.

REWRITE
## What automated bookkeeping actually changes

Month-end close is the bottleneck, not data entry. Most teams we work with were closing in
nine days. After moving reconciliation into the platform, six of them close in three, and
two are still at seven because their bank feeds break weekly and no software fixes that.

What the platform does: it matches transactions against your ledger overnight and flags what
it cannot match. You review the flags. That is the whole product.

Three things it does not do. It does not file your taxes. It does not work with two of the
smaller regional banks. And it takes about a week of setup where your numbers will look
wrong before they look right.
```

## Case 8. Email

**Input, 96 words**

> Subject: Unlocking Your Team's Full Potential
>
> Hi Jennifer,
>
> I hope this email finds you well. My name is David and I'm reaching out because I believe
> there's a real opportunity for us to work together.
>
> At Vantage, we help operations teams like yours eliminate inefficiencies and drive
> sustainable growth through tailored process consulting. Our clients typically see
> significant improvements within the first quarter.
>
> Would you be open to a brief 15-minute call next week to explore how we might be able to
> support your goals?
>
> Best regards,
> David Chen
> Senior Partnerships Manager, Vantage
> Book a time: [link]
>
> P.S. I'd love to hear your thoughts either way!

**Output**

```
MODE: deliverable
FORMAT: email, cold
LENGTH: 96 words
CONFIDENCE: argued transfer
MODEL: unknown
VERDICT: reads machine (density 10.4 per 100 words, spread 2 of 7 themes)

STRUCTURAL TEMPLATE
agents: Jennifer, named and not described. David, named, titled, and otherwise absent.
events: null.
causality: null.
revelation: null.
temporal order: "within the first quarter" and "next week". Two spans, no order between them.
setting: null.

FINDINGS
1. [format, w2] Subject line in title case and phrased as a benefit rather than a
   description.
   Repair: say what the email is about.
2. [surface, w2] "I hope this email finds you well"  Repair: CUT
3. [format, w2] The reason for writing arrives in sentence three. The first two sentences
   are a machine warming up.
4. [surface, w2] "eliminate inefficiencies and drive sustainable growth"
   Tell: promotional register, no fact
5. [surface, w2] "Our clients typically see significant improvements"
   Tell: vague attribution plus unquantified claim
6. [surface, w2] "teams like yours"  Tell: category reason for reaching out
7. [format, w2] Sign-off stack: close, name, title, company, booking link.
8. [format, w2] The P.S. carries a softener rather than content, which is a template
   convention rather than a person.
9. [discourse, w2, theme 4] Check 6, named reference. Nothing in the email required
   knowing anything about Jennifer or her team.
10. [discourse, w2, theme 3] Check 4, internal resolution. Added on rerun. "explore how we
   might be able to support your goals" asks the reader to arrive at the value themselves.
   The email never states what it would do.
   Repair: name the thing done, in one sentence, before the ask.

GATED
- greeting and sign-off : native to email
- one link : native
- "Hi Jennifer" : native
- check 9, reader address : second person is native to a cold email, not scored
- check 10, recontextualization : silent. A 96 word cold email has no room to place a
  reframe, and its absence here is a property of the format rather than of this draft

THEME SPREAD: themes 3 and 4. Two of seven, from ten findings. The email reads machine on
format and surface tells almost entirely, which is the useful result: a low spread does not
mean a clean text, it means the failure is not structural. Assessment mode would return no
origin claim here while deliverable mode still rewrites the whole thing.

WHAT IS WORKING
- The ask is specific about length. Fifteen minutes is a real number. Keep it.

REWRITE
Subject: your Q3 vendor list has three tools doing the same job

Jennifer, your job posting for an ops coordinator lists Asana, Monday, and Notion in the
same paragraph. That usually means three teams each picked one and nobody ever merged them.

We consolidate that. Two of the last four we did took six weeks; one took four months
because the finance team refused to move, which is a real outcome and might be yours.

Worth fifteen minutes? If it is not a live problem, say so and I will not follow up.

David Chen, Vantage
```

## Case 9. Control, human-written direct message

This draft is rough, unbalanced, and written by a person. It must pass.

**Input, 44 words**

> hey, saw your thing about the bench setup at the wallingford location. we had the same
> problem, the rack was too close to the mirror and people kept clipping it. we moved it
> like 40cm and complaints stopped. no idea if that's your issue but figured id say

**Output**

```
MODE: deliverable
FORMAT: direct message, first touch
LENGTH: 44 words
MODEL: unknown
VERDICT: reads human (0 weighted findings, spread 0 of 7 themes)

FINDINGS
none

GATED
- lowercase start, missing punctuation, "id" for "I'd" : native, and reads as typed by a
  person
- fragment "no idea if that's your issue" : hedge, and the source lists ordinary hedges as
  leaning human
- no greeting formality, no sign-off : native
- "like 40cm" : imprecise, and a person's imprecision. Not flagged.

WHAT IS WORKING
- Check 6 fires positive. A named location, a specific measurement, a named failure mode.
  47 against 24.
- Check 5 fires positive. The last clause admits the observation might be wrong.
  59 against 38.
- Check 1 passes. No lesson is stated anywhere.
- Checks 2, 3, 4, 7, 8, 9, 10 were not eligible at 44 words. The pass rests on the three
  that ran, which is the honest reading and is why this control is a control and not a
  proof.
```

**Result: pass.** If a future change to the surface layer makes this fail, the change is
wrong.

## Case 10. Control, human-written caption

**Input, 61 words**

> we lost the ceramics account today. three years. the reason given was budget which is
> probably half true.
>
> i keep going back to march when they asked for a second designer and i said we could
> stretch. we could not stretch. i knew that when i said it.
>
> anyway. invoicing is done. tomorrow is a normal day.

**Output**

```
MODE: deliverable
FORMAT: caption
LENGTH: 61 words
MODEL: unknown
VERDICT: reads human (0 weighted findings, spread 0 of 7 themes)

FINDINGS
none

GATED
- "which is probably half true" : hedge, leans human
- "anyway." as a paragraph : the source lists no rule against it, and the gate protects
  rhythm the draft already had
- lowercase throughout : native

WHAT IS WORKING
- Check 6 fires positive. Named account, named month, named decision, named cost.
- Check 5 fires positive. Moral polarity is ambivalent and points at the writer.
- Check 10 fires positive, which the original run did not record because the check did not
  exist. "we could not stretch. i knew that when i said it" changes what "i said we could
  stretch" meant one clause earlier. Human mean 3.28 against AI 2.95.
- Check 1 passes. The ending does not explain itself. Delete-the-last-line test: removing
  "tomorrow is a normal day" makes it worse, which is the opposite of the machine pattern.
- Check 9 not scored. Second person is native to a caption, and this draft uses none, which
  carries no signal in either direction.
```

**Result: pass.**

## Case 11. Long page section, run under the seven theme bar

Written to exercise the checks added in September 2026: theme spread instead of raw density,
the weak label on near-tied features, and checks 9 and 10.

**Input, 186 words**

> Most agencies lose clients in the first thirty days, and the reason is almost always the
> same. The relationship starts with enthusiasm, then the first deliverable arrives later
> than expected, and trust erodes from there. What follows is a slow drift toward silence.
>
> We rebuilt our onboarding around a single principle: certainty beats speed. Every new
> client now receives a written schedule before any work begins, and every milestone has a
> named owner. When a date moves, the client hears it from us first.
>
> The result has been a meaningful shift in how our partnerships begin. Clients who know
> what is coming ask fewer questions, and the questions they do ask are better ones. Teams
> that once spent their mornings managing anxiety now spend them doing the work.
>
> The lesson is that clarity is not a nice addition to a process. It is the process. Once
> you understand that, everything else about onboarding becomes simpler.

**Output**

```
MODE: assessment
FORMAT: long page section
LENGTH: 186 words        LANGUAGE: English (vocabulary layer: run)
VOICE SAMPLE: none supplied
CONFIDENCE: argued transfer. Neither source measured a landing page.
MODEL: unknown
VERDICT: reads machine (density 4.8 per 100 words, spread 4 of 7 themes)

STRUCTURAL TEMPLATE, filled first
agents: null. No person is named anywhere, including the writer.
events: one state change, stated as a general pattern rather than as something that happened.
causality: enthusiasm -> late deliverable -> erosion -> silence. Unbroken.
revelation: null. Nothing is withheld and nothing is disclosed late.
temporal order: linear. No jumps, no scene, no date.
setting: null.

FINDINGS
1. [discourse, w2, theme 1] "The lesson is that clarity is not a nice addition to a process."
   Check 1, self-explaining. The text states its own takeaway.
   Repair: CUT. The two paragraphs above already carry it.
2. [discourse, w2, theme 1] "Once you understand that, everything else about onboarding
   becomes simpler."
   Check 1 again, narratorial commentary on significance.
   Repair: CUT.
3. [discourse, w2, theme 4] Named reference check fails. No client, no date, no number, no
   tool, no figure. "about a third" would have been a fact. "a meaningful shift" is not.
   Repair: ask the writer for the retention number. Do not supply one.
4. [discourse, w2, theme 6] Check 10, recontextualization. Nothing arrives that changes what
   an earlier sentence meant. Disclosure order equals assembly order.
   Repair: structural. If the real story has a reversal, it belongs before the close.
5. [discourse, w1, theme 3] Check 4, internal resolution. The close asks the reader to
   understand, not to do anything.
   Repair: name the external step.
6. [discourse, w1, theme 3, WEAK] Check 3, tidy causality. Four sentences, one chain, no
   admitted cost. Labelled weak under gate question 4: human mean 3.92 against AI 4.20.
   Repair: name the case where the schedule did not help.
7. [surface, w2] "The result has been a meaningful shift in how our partnerships begin"
   Tell: promotional register with no fact under it.
   Repair: the number, or CUT.
8. [surface, w1] "a slow drift toward silence"
   Tell: significance inflation, mild.
   Repair: keep if the writer talks this way, cut otherwise.

GATED (looked like findings, are not)
- "Once you understand that" second person : native to a page, cleared by the format table
- check 9, reader address : not scored. Second person is the default register here, so its
  presence carries no signal and its absence would carry none either
- "certainty beats speed" as a three word parallel : one instance, weight 1 and no company
- checks 2 and 5 : the text has one thread and one polarity, but both readings collapse into
  findings 1 and 6 and are not double counted

THEME SPREAD: 1, 3, 4, 6. Four of seven, with a weight 2 hit in themes 1, 4 and 6. Theme 3
carries no weight 2 hit, so the bar is met on three themes and is reported that way.

WHAT IS WORKING
- "every milestone has a named owner" is the one concrete sentence. Protect it.
- No em dash, no bullet formatting, no rule of three stacking. The surface layer is nearly
  clean, which is the point: this draft would pass a word list pass and still read machine.
```

**Result: pass.** The case exists to prove three things. Density alone would have called this
machine on findings 1, 2 and 7 without ever asking whether the spread supported it. Finding 6
would have been a weight 2 verdict carrier before gate question 4 existed. And findings 3 and
4 come from checks the skill did not have before this revision.

## Case 12. Control, human-written long form that trips three machine-leaning checks

The load bearing control for gate question 4. This draft is tidy, unified, and resolved by
the writer's own choice, which are three machine-leaning values. It must still pass.

**Input, 187 words**

> We stopped doing discovery calls in March. Not because they did not work, they worked
> fine, we closed about a third of them. We stopped because I could not do six of them in a
> week and still be any good at the actual work by Thursday.
>
> So now there is a form. Eleven questions, most of them about budget, because that was the
> thing I kept finding out on minute forty of a fifty minute call.
>
> Close rate went to about a fifth. That is worse. I know it is worse. What I did not expect
> was that the fifth who do book are people I would have wanted anyway, and the Thursdays
> came back.
>
> I would not tell a newer agency to do this. If you have the hours, take the calls, you
> learn more on a call than a form will ever give you. This was a trade I made because I ran
> out of Thursdays, not because I found a better system.

**Output**

```
MODE: assessment
FORMAT: long page section
LENGTH: 187 words
MODEL: unknown
VERDICT: reads human (0 weighted findings, spread 0 of 7 themes)

FINDINGS
none

GATED (looked like findings, are not)
- thematic unity : everything here is about one decision and nothing pulls sideways. Gate
  question 4 clears it. Human mean 4.41 against AI 4.74, and a 187 word section about one
  decision has no room for a second thread. Weak by construction, not by measurement.
- agency in resolution, protagonist choice : the writer decided and the writer acted, which
  is the machine-leaning value at 46 against 69. Cleared, because the choice is named, dated,
  costed and regretted. The tell is a resolution that turns on a private act of will with
  nothing under it. This one has a form with eleven questions under it.
- "This was a trade I made because I ran out of Thursdays, not because I found a better
  system" : reads like a stated lesson, check 1. Cleared. It is an admission against the
  writer's own case, not a takeaway offered to the reader.
- "I would not tell a newer agency to do this" : reads like moralizing. Cleared, same reason.
  It argues against the thing the page is describing.

WHAT IS WORKING
- Check 10 fires positive. "What I did not expect was that the fifth who do book are people
  I would have wanted anyway" changes what "That is worse" meant two sentences earlier. That
  is recontextualization after surprise, human mean 3.28 against AI 2.95.
- Check 9 fires positive. "If you have the hours, take the calls" addresses a reader the
  writer can picture, and the last paragraph names the situation it is written from.
- Check 5 fires positive. Moral polarity is ambivalent and points at the writer. 59 against 38.
- Check 6 fires positive, heavily. March, eleven, a third, a fifth, minute forty, fifty
  minute, Thursday. Seven concrete anchors in 187 words.
- Check 7 fires positive. "I could not be any good at the actual work by Thursday" is an
  explicit state rather than a tightening chest. 29 against 8.
- Check 3 passes. "That is worse. I know it is worse." is an admitted cost, which breaks the
  chain the machine-leaning value would have kept.
- Check 8, order, ran and found nothing. The account is told in the order it happened, and a
  flat order is not a fault on its own. Recorded so all ten checks are accounted for.
- Roughness to protect: "they worked fine" as a comma splice, "So now there is a form" as a
  plain is-phrase, the repetition of Thursday.
```

**Result: pass.** If a future change makes this draft fail, the change is wrong. It is the
only case in this file where machine-leaning values are present and the correct verdict is
still human, which is the whole content of gate question 4.

## Case 13. Direct message, under 60 words, run under the new contract

Written to test the opposite of case 11: that the September 2026 machinery goes quiet when
the text is too short to support it, instead of finding something anyway.

**Input, 54 words**

> Hi Dana, quick one. I noticed your studio has been posting client transformations
> consistently, which shows real dedication to your craft. We help boutique studios turn
> that content into a predictable booking system without adding to your workload. Worth a
> short conversation to see if there is a fit?

**Output**

```
MODE: assessment
FORMAT: direct message, first touch
LENGTH: 54 words        LANGUAGE: English (vocabulary layer: run)
VOICE SAMPLE: none supplied
CONFIDENCE: argued transfer, weakest case. Neither source measured messages.
MODEL: unknown
VERDICT: no assessment verdict available at this length
         (count rule: 5 weighted findings, spread not computable)

STRUCTURAL TEMPLATE, filled before the discourse checks
agents: Dana, named but not described. The sender, never named.
events: null. Nothing happens. A capability is asserted.
causality: null. "Consistent posting" and "predictable bookings" are placed next to each
  other, not linked.
revelation: null.
temporal order: null. No time reference of any kind.
setting: "your studio", generic.

FINDINGS
1. [discourse, w2, theme 4] Check 6, named reference. "client transformations" and
   "boutique studios" are category words. No post, no date, no number, no studio name.
   Repair: one thing only Dana's account could have prompted, or do not send.
2. [surface, w2] "which shows real dedication to your craft"
   Tell: promotional register with no fact under it, and a compliment that fits any account.
   Repair: CUT.
3. [surface, w2] "a predictable booking system without adding to your workload"
   Tell: significance inflation. The benefit is asserted, the mechanism is absent.
   Repair: name the mechanism or the number.
4. [discourse, w2, theme 1] Check 1, self-explaining. The message states why its own
   observation matters rather than letting the observation do the work.
   Repair: CUT, same span as finding 2.
5. [format, w2] "Worth a short conversation to see if there is a fit?"
   Tell: permission close. The ask is larger than the sale, and the profile flags it.
   Repair: an ask smaller than the sale.

GATED (looked like findings, are not)
- second person throughout : native to the format
- "Hi Dana, quick one." fragment : native, and reads as typed
- no citation, no source : native, nobody cites in a message
- check 9, reader address : not scored. Second person is the default register here
- check 10, recontextualization : NOT RUN. 54 words, and the length table stops the
  discourse layer at checks 1, 5 and 6. Its silence is a silence, not a pass
- checks 2, 3, 4, 7, 8 : NOT RUN, same rule

THEME SPREAD: themes 1 and 4 only. Two of seven, and only three checks were eligible to
run. The bar needs four themes, so it cannot be met at this length and is not approached.
Assessment mode returns no origin verdict here. This is the correct outcome, not a failure.

WHAT IS WORKING
- "Hi Dana, quick one" is the one line a person would type. Protect it.
```

**Result: pass.** The case exists to prove restraint. Every finding above comes from the
three checks the length table allows plus the surface layer. The seven theme bar, checks 9
and 10, and the structural template all reported their own inapplicability rather than
producing content. A tool that returns an origin verdict on 54 words is guessing, and this
one now says so in the verdict line.

## Case 14. Spoken script, model known, fingerprint block active

The only case that exercises the model-conditional block. It applies because the draft was
produced by the assistant running the audit, which is the one situation where the author is
known.

**Input, 118 words, roughly 46 seconds at speaking pace**

> Most people think the hardest part of running an agency is finding clients. It is not.
> The hardest part is the quiet stretch after you sign one, when the work is real and the
> excitement is gone.
>
> I used to fill that stretch with activity. More calls, more posts, more everything. It
> felt like progress and it was motion.
>
> What changed was small. I started writing down what I actually finished each day, not what
> I planned. Some days the list was one line. But the list was true, and a true list you can
> build on.
>
> Years later, that habit is still the thing I would keep if I had to drop everything else.

**Output**

```
MODE: deliverable
FORMAT: spoken script, roughly 46 seconds
LENGTH: 118 words        LANGUAGE: English (vocabulary layer: run, demoted per profile)
VOICE SAMPLE: none supplied
CONFIDENCE: argued transfer, and the spoken override outranks the word list
MODEL: Claude, known. Fingerprint block active at weight 1.
VERDICT: reads machine (density 4.2 per 100 words, spread 3 of 7 themes)

STRUCTURAL TEMPLATE, filled before the discourse checks
agents: the speaker, unnamed. No second person appears in the story.
events: one habit change, undated.
causality: activity -> emptiness -> list -> durability. Unbroken.
revelation: null. Nothing lands late.
temporal order: linear, then a forward step at the close.
setting: null.

FINDINGS
1. [discourse, w2, theme 1] Check 1, self-explaining. "a true list you can build on" and
   "the thing I would keep if I had to drop everything else" both state the takeaway.
   Repair: keep one, CUT the other. The second is the weaker of the two.
2. [discourse, w2, theme 4] Check 6, named reference. No date, no number, no client, no
   tool. "Years later" is the only time marker and it is unanchored.
   Repair: the year, or the number of lines on a real day.
3. [discourse, w2, theme 6] Check 10, recontextualization. Nothing later changes what an
   earlier line meant. "It felt like progress and it was motion" is the closest, and it
   arrives before the thing it would reframe rather than after.
   Repair: structural. Put the correction after the belief, not alongside it.
4. [surface, w2] "It felt like progress and it was motion."
   Tell: negative parallelism, and the spoken profile flags symmetrical pairs specifically.
   Read aloud, the balance is audible.
   Repair: "It felt like progress. It was not."
5. [surface, w2] "Most people think the hardest part is finding clients. It is not."
   Tell: negative parallelism again, in the opening position.
   Repair: open on the quiet stretch itself.
6. [discourse, w1, theme 3, WEAK] Check 3, tidy causality. Four beats, one chain, no
   admitted cost. Weak under gate question 4: human mean 3.92 against AI 4.20.
   Repair: name what the habit cost or failed to fix.
7. [fingerprint, w1] Flat event escalation. Intensity is identical at the open and the
   close. Claude's highest ranked fingerprint, uniqueness 22.4.
   Repair: let one beat be louder than the others, or accept a level script on purpose.
8. [fingerprint, w1] "Years later, that habit is still the thing I would keep" steps outside
   the main span to report what happened after. Epilogue ending, a Claude fingerprint.
   Repair: end inside the span. The last true beat is the one line list.

GATED (looked like findings, are not)
- "More calls, more posts, more everything" : a three item list, but spoken and announced by
  rhythm, and the profile clears repetition as how listeners keep up
- "It is not." as a two word sentence : native to speech, and the profile clears fragments
- check 9, reader address : not scored, and here the absence is worth a note rather than a
  finding. A camera script is spoken to someone, and this one never turns to them
- no citation : native

THEME SPREAD: themes 1, 4 and 6, each carrying a weight 2 hit. Three of seven. Under the
assessment bar of four, so if this draft came from elsewhere the verdict line would read
mixed and no origin claim. In deliverable mode the bar does not gate anything and all eight
findings stand.

READ ALOUD: run once, timed at 46 seconds. Stumbles at "and the excitement is gone" into
"I used to fill that stretch", where two sentences meet with no breath point. Marked as
finding 9 in the working copy, not scored, because the profile treats stumbles as findings
and this one is a delivery fix rather than a text fix.

WHAT IS WORKING
- Check 7 fires positive. "the excitement is gone" is an explicit state, not a tightening
  chest. 29 against 8.
- Check 5 is neutral rather than failing. The speaker is mildly against their past self,
  which is not full ambivalence but is not clean polarity either.
- "Some days the list was one line" is the only concrete sentence in the script. Protect it,
  and build finding 2's repair around it.
```

**Result: pass.** Three things this case proves. The fingerprint block fires only with MODEL
known and lands at weight 1, so findings 7 and 8 shift the density without carrying the
verdict. The spoken profile and the discourse layer disagree productively: finding 4 is a
surface tell the read-aloud test independently confirms. And the spread line does different
work in the two modes, gating nothing here while it would have blocked an origin claim.

## Case 15. Support reply, a derived profile

The first case run against a profile that did not exist before the audit started. Profile 11
was derived from the six questions in "Adapting to a new format", starting from profile 3.

**Derivation, recorded before the findings**

Nearest listed profile: 3, objection reply. Same length, same one-to-one shape, same close.
The six questions changed two things.

- Third person by default: no. Check 9's scored half stays silent.
- Did the reader ask for this: yes, and this is the difference from profile 3. An explicit
  takeaway is native here, so check 1 fires only on a lesson nobody asked for.
- Is the structure the product: no. Check 3 stays live.
- Could the writer have known something specific: yes, the ticket and the account. Check 6
  runs at full weight, which is stricter than most formats.
- Any feeling in scope: yes, the customer is annoyed. Check 7 live.
- Order fixed by convention: no. Check 8 live.

**Input, 97 words**

> Hi Tom, thank you so much for reaching out and I completely understand your frustration
> here. I know how important it is to have your exports working reliably.
>
> Our team is aware of this issue and is working diligently to resolve it as quickly as
> possible. In the meantime, I would recommend trying to clear your browser cache, which
> resolves this for many of our users.
>
> We truly appreciate your patience and understanding as we work to improve your experience.
> Please don't hesitate to reach out if there is anything else I can help with!

**Output**

```
MODE: deliverable
FORMAT: support reply, inbound (derived profile 11, from profile 3)
LENGTH: 97 words        LANGUAGE: English (vocabulary layer: run)
VOICE SAMPLE: none supplied
CONFIDENCE: argued transfer, derived profile. Neither source measured a support reply.
MODEL: unknown
VERDICT: reads machine (density 8.2 per 100 words, spread 3 of 7 themes)

STRUCTURAL TEMPLATE
agents: Tom, named. "Our team", unnamed and uncountable.
events: null. Nothing has happened and nothing is scheduled.
causality: null. The cache suggestion is not connected to the export failure.
revelation: null.
temporal order: "as quickly as possible", "in the meantime". Two spans, neither anchored.
setting: null.

SILENCE MAP
1  self-explaining      silent : the reader asked for an answer, so a takeaway is native.
                        Question 2. Would fire only on a lesson nobody asked for
2  single track         live
3  tidy causality       live : structure is not the product here. Question 3
4  internal resolution  live
5  moral polarity       live
6  named reference      live, full weight : the writer had the ticket. Question 4
7  emotion handling     live : the customer is annoyed and the reply names it. Question 5
8  order                live : no fixed convention. Question 6
9  reader address       silent, scored half : second person is the native register.
                        Question 1. Medium-naming half stays available as a positive
10 recontextualization  live but silent in fact at 97 words, no second fact placed to
                        reframe a first

FINDINGS
1. [discourse, w2, theme 4] Check 6, named reference, at full weight per the derived
   profile. No ticket number, no version, no date, no export type. The writer had all four.
   Repair: name the ticket and the build. This is the finding the format exists to catch.
2. [surface, w2] "Our team is aware of this issue and is working diligently to resolve it as
   quickly as possible"
   Tell: vague attribution plus unquantified commitment. Which team, by when.
   Repair: a date, or "I do not have a date yet" which is also true and better.
3. [surface, w2] "I completely understand your frustration here" and "We truly appreciate
   your patience and understanding"
   Tell: empathy preamble that costs nothing, carried from profile 3. Two of them in 97
   words, one at each end.
   Repair: CUT both. The answer is the apology.
4. [discourse, w2, theme 3] Check 4, internal resolution. The reply closes on the customer
   feeling looked after rather than on what either party does next.
   Repair: name the next external step and who owns it.
5. [surface, w1] "I know how important it is to have your exports working reliably"
   Tell: restating the customer's problem back as a benefit sentence.
6. [discourse, w1, theme 1] Check 2, single track. Nothing is conceded. The cache
   suggestion is offered with no acknowledgement that it probably will not work, since the
   team already knows the bug is theirs.
   Repair: say which one it is.

GATED (looked like findings, are not)
- "Hi Tom", the sign-off, the apology : format-native table in false-positives.md
- second person throughout : native, and check 9's scored half is silent per the map
- "I would recommend trying to clear your browser cache" as an instruction : the reader
  asked for a procedure, so an imperative has a job here
- check 1, self-explaining : SILENT by question 2. The reply is allowed to state its own
  point, because that is what the customer asked for. Under profile 3 this same shape would
  have been a finding, and the derivation is what separates them

THEME SPREAD: themes 1, 3 and 4. Three of seven, one short of the bar, which is the same
result profile 3 produced on a comparable length. Deliverable mode is unaffected.

WHAT IS WORKING
- "clear your browser cache" is the one concrete instruction. Keep it, demote it.
- The reply is addressed to a named person and answers in the first paragraph, structurally.
  It is the content of that paragraph that fails, not its position.

REWRITE
Hi Tom, this is our bug, not your cache. Exports over about 5MB have been timing out since
the 3.2 release on Tuesday, ticket SUP-4471.

The fix is in review and I expect it out this week. I will not promise a day because the
last one slipped.

Until then, exporting in two halves gets under the limit. If that is not workable for your
volume, tell me and I will run the export on our side and send you the file.
```

**Result: pass.** The case exists to prove the derivation does work rather than only being
described. One question, whether the reader asked for the text, moved check 1 from a hard
flag to silent, and that single move is the difference between profile 3 and profile 11.
Every other check kept its weight, its wording and its gate.

## Case 16. Product description, and the first run where check 9 can fire

Profile 12, derived from the six questions. It is the first format in this skill whose
default register is third person, which is the condition check 9 has been waiting for
across sixteen runs.

**Derivation, recorded before the findings**

Nearest listed profile: 7, long page, at a shorter band.

- Third person by default: yes. Check 9 is LIVE, and theme 5 is reachable as a finding for
  the first time in this file.
- Did the reader ask for this: yes, a shopper opened the page. Check 1 fires only on a
  lesson nobody asked for, which in this format means a closing line about what owning the
  thing says about you.
- Is the structure the product: yes for the spec block. Check 3 is silent and the inline
  header list is native.
- Could the writer have known something specific about this reader: no. Check 6 drops to
  weight 1 and measures the format's ceiling. It can still fire about the object.
- Any feeling in scope: no. Check 7 silent.
- Order fixed by convention: no. Check 8 live.

**Input, 104 words**

> The Aurelia Carafe is more than a vessel. It is a statement about how you choose to begin
> your mornings.
>
> Hand-finished by artisans using time-honoured techniques, each piece carries the quiet
> confidence of objects made to last. The borosilicate body resists thermal shock while the
> weighted base delivers a reassuring stability that elevates the everyday ritual of pouring.
>
> - **Material:** Borosilicate glass
> - **Capacity:** 1.2L
> - **Care:** Dishwasher safe
>
> In a world of disposable objects, the Aurelia is an invitation to slow down and savour what
> matters.

**Output**

```
MODE: deliverable
FORMAT: product description, catalogue (derived profile 12, from profile 7)
LENGTH: 104 words        LANGUAGE: English (vocabulary layer: run)
VOICE SAMPLE: none supplied
CONFIDENCE: argued transfer, derived profile. Neither source measured catalogue copy.
MODEL: unknown
VERDICT: reads machine (density 7.7 per 100 words, spread 4 of 7 themes)

STRUCTURAL TEMPLATE
agents: null. "Artisans", uncountable and unnamed. No reader, no maker, no owner.
events: null.
causality: weighted base -> stability -> elevated ritual. The last link is asserted.
revelation: null.
temporal order: null.
setting: "mornings", "a world of disposable objects". Neither is a place.

SILENCE MAP
1  self-explaining      live, narrowed : the shopper asked about the object, not about
                        mornings. Question 2 clears a spec, not a moral
2  single track         live
3  tidy causality       silent : the spec block is the product's structure. Question 3
4  internal resolution  live
5  moral polarity       live
6  named reference      live at weight 1 : the writer could not know this reader.
                        Question 4. Measures the format ceiling, not the writer
7  emotion handling     silent : no feeling is in scope in catalogue copy. Question 5
8  order                live : no fixed convention. Question 6
9  reader address       LIVE, scored half : third person is the default register here, so
                        turning to the reader is a choice. Question 1. First run in this
                        file where this half can fire
10 recontextualization  live

FINDINGS
1. [surface, w2] "more than a vessel", "a statement about how you choose to begin your
   mornings", "the quiet confidence of objects made to last", "an invitation to slow down"
   Tell: significance inflation, four instances in 104 words. The object is tied to a
   lifestyle instead of described.
   Repair: CUT all four. The spec block already does the work they claim to do.
2. [discourse, w2, theme 1] Check 1, self-explaining. "In a world of disposable objects, the
   Aurelia is an invitation to slow down and savour what matters." A closing line stating
   what owning the thing means.
   Repair: CUT. The shopper asked what it is, not what it says about them.
3. [discourse, w2, theme 5] Check 9, scored half, fired. The description never acknowledges
   a person deciding whether to buy it. It has one second-person phrase, "how you choose to
   begin your mornings", and that phrase is about a lifestyle rather than about the
   decision in front of the reader. Nothing tells them who it is wrong for, what it does
   not do, or what to check before buying.
   Repair: one sentence addressed to the person deciding. "It is too heavy to pour
   one-handed" is that sentence.
4. [discourse, w1, theme 4] Check 6, named reference at weight 1 per the derived profile.
   "artisans", "time-honoured techniques" name nobody and nowhere. The format ceiling is
   low, so this is weight 1, but "hand-finished in Stoke" was available and free.
   Repair: name the place or the process, or cut the claim.
5. [discourse, w2, theme 6] Check 10, recontextualization. Nothing later changes an earlier
   claim. Every sentence restates that the carafe is good.
   Repair: put the limitation after the claim it qualifies. That is also finding 3's repair.
6. [surface, w2] "delivers a reassuring stability that elevates the everyday ritual"
   Tell: promotional register with no fact under it, plus copula avoidance. "The base is
   weighted so it does not tip" was available.
7. [surface, w1] "time-honoured", "quiet confidence", "savour what matters"
   Tell: vocabulary and register, weight 1 each, counted once as a cluster.

GATED (looked like findings, are not)
- third person and no author : native to a catalogue, from the derived profile
- the inline-header spec list : native. Check 3 is silent per the map, question 3
- repeated attribute nouns, material, capacity, care : native, the reader is scanning
- no named customer : not a finding. Question 4 already dropped check 6 to weight 1 for
  exactly this reason, and penalising the format twice would be double counting
- check 7, emotion handling : SILENT per the map. "Reassuring" and "quiet confidence" are
  register, not a character's feeling, and flagging them under check 7 would be porting a
  fiction feature into a format that has no interior

THEME SPREAD: themes 1, 4, 5 and 6. Four of seven, and the bar is met. This is the only run
in this file that reaches theme 5, and it does so because the derived profile made check 9
live rather than because the draft is worse than the others.

WHAT IS WORKING
- The spec block is the honest part of this page. Three facts, no adjectives, correctly
  formatted. Protect it and let it carry more.

REWRITE
The Aurelia is a 1.2 litre borosilicate carafe with a weighted base, so it does not tip when
it is half full and does not crack when you pour boiling water into it straight from the
kettle.

- **Material:** Borosilicate glass
- **Capacity:** 1.2L
- **Care:** Dishwasher safe

Two things to check before you buy. It is 900g full, which is more than most people expect,
and it is too heavy to pour comfortably one-handed. If you want something to leave on a
tray and pour with both hands, this is it. If you want something to carry around the
kitchen, buy the 800ml.
```

**Result: pass, and it closes a gap the test log has carried since the September 2026
alignment.** Check 9's scored half had never fired in sixteen runs, and the recorded reason
was that no profile had third person as its default register. Deriving one was the missing
test, not writing another second-person draft. Theme 5 is reachable after all, and the
condition is a property of the format rather than of the check.

## What the tests changed in the skill

1. Case 6 exposed a collision between the rule-of-three check and spoken teaching, where a
   count announced to the listener is structure rather than a tell. The spoken profile in
   `references/formats.md` now carries that carve-out explicitly.
2. Case 1 exposed that a repair can quietly become an invention. The no-invention rule was
   moved out of the repair pass and up to the top of `SKILL.md`, above the passes, so it is
   read before anything else.
3. Case 5 showed that a per-slide audit misses the deck-level findings, which were five of
   nine. The carousel profile now runs the discourse layer on the deck and never on one
   slide.
4. Cases 9 and 10 were written after the first eight, on the suspicion that the skill would
   flag anything. Both passed with zero findings. The gate carried them, which is the
   argument for printing the GATED section on every run.
5. Case 11 showed that density and spread disagree. On raw density the draft was machine at
   finding 2, before the checks that carry the real evidence had run. Assessment mode now
   scores spread across the seven measured themes and reports density as secondary.
6. Case 12 was written to break the new weighting, and did. Three machine-leaning values
   were present in a draft that is plainly human, and two of the three were high ranked
   features. Gate question 4 exists because of this case: a feature whose human mean is
   already high cannot carry a verdict, however high the paper ranks it.
7. Case 13 exposed that the new machinery had no way to report its own inapplicability. At
   54 words only three checks are eligible, so the seven theme bar cannot be met by
   construction, and the run was producing a verdict anyway. Pass 0 now states that
   assessment mode returns no origin verdict below 60 words, and the verdict line says so
   instead of printing a number the length cannot support.
8. Cases 11 and 12 used output fields the contract in Pass 5 did not define: a theme tag on
   discourse findings, a WEAK label, the structural template block, and a spread line. The
   tests were demonstrating a format the skill did not specify. Pass 5 now carries all four,
   plus a MODEL line, which case 14 needs.
9. Case 14 is the only run where the author is known, and it showed the fingerprint block
   behaving as intended: two findings at weight 1 that move density without reaching the
   verdict. It also produced the first case where the surface layer and the read-aloud test
   independently flag the same span, which is the spoken profile and the discourse layer
   agreeing rather than competing.
10. Cases 1 to 10 were rerun under the new contract, which the previous alignment had
   explicitly not done. Check 10 produced a new finding in cases 4, 6 and 7, and check 4
   produced one in case 8, so the two additions earn their place on legacy drafts rather
   than only on drafts written to exercise them. No verdict changed direction.
11. The rerun made the spread line reproducible, and that required a mapping from the ten
   checks to the seven themes which did not exist. Without it, two runs of the same draft
   could report different spreads. Pass 2 now carries the table.
12. Case 10, a control, got stronger on rerun rather than weaker. Check 10 fires positive on
   "i knew that when i said it", which the original run could not record because the check
   did not exist. A new check that only ever adds faults would be a bad check.
13. Case 4 reaches the bar at 78 words, the shortest text in this file to do so, while case 5
   at 62 words across eight slides reaches two themes and case 2 at 61 words reaches one.
   The bar is not simply a length threshold: a caption carries one continuous argument and a
   deck carries eight fragments, and only the first can fail structurally.
14. Case 8 reads machine at density 10.4 with a spread of two. Low spread does not mean a
   clean text. It means the failure is not structural, and the report now says which.
15. Check 9 never produced a finding in any of fourteen runs. Investigated rather than left
   as a curiosity, and the cause is structural: its scored half needs a format whose default
   register is third person, and none of the nine profiles was one. Check 9 is now split in
   Pass 2, with the second person half marked silent and the medium-naming half kept as a
   positive signal.
16. Cases 15 and 16 are the first runs against profiles that did not exist when the audit
   started, both derived by the six questions in "Adapting to a new format". Case 15 shows
   one answer, whether the reader asked for the text, moving check 1 from a hard flag to
   silent, which is the entire difference between profile 3 and profile 11.
17. Case 16 closed the check 9 gap that entry 15 recorded. The missing test was never
   another second person draft. It was a third person format, and deriving one produced the
   first firing of check 9's scored half and the first run to reach theme 5. The lesson
   generalises: a check that cannot fire is telling you which format profile is missing,
   not that the check is wrong.
18. Deriving profiles forced one new output block, the silence map, which is a contract
   change. Scoped to derived profiles only, because listed profiles already state their
   silenced checks in GATED, and all fourteen earlier cases were checked mechanically for
   that. No case needed a rerun.

## What is still untested

Formats with no case here: newsletter, podcast description, job posting, product
description, documentation, chat support reply, video title, thumbnail text, subtitle file,
press release, proposal, invoice note. The skill's derivation procedure covers them by
construction, and the skill does not claim measured coverage of them.

Every format profiled in `references/formats.md` now has a run under the current contract.
All fourteen cases carry a MODEL line, a spread figure, theme tags on every discourse
finding, and an explicit statement of which checks were ineligible and why. What remains
untested is listed below and nothing else is claimed.

**Check 9, scored half.** Closed. It fired for the first time in case 16, against derived
profile 12, whose default register is third person. It remains untested in the other third
person formats that have no profile here: case study, report, press release, about page.

**Theme 5.** Reachable, in third person formats only, and reached once. In a second person
format it survives only as a positive signal and the practical spread ceiling stays at six
of seven.

**The derivation procedure itself.** Two profiles derived, 11 and 12, from six questions.
The questions that have never been answered "yes" in a recorded run are the structure
question at profile 11 and the order question anywhere, so two of the six changes are
described rather than demonstrated.

**The fingerprint block.** One run, case 14, one model. The other four models in the paper
have fingerprint lists this skill does not carry, because the situation where their identity
is known does not arise here.

**Formats with no profile and no run.** Newsletter, podcast description, job posting,
product description, documentation, chat support reply, video title, thumbnail text,
subtitle file, press release, proposal, invoice note. Covered by the derivation procedure at
the end of `references/formats.md` and by nothing else.

**Language.** Every run in this file is English. The vocabulary layer is English by
measurement and the skill reports it as not run otherwise.

**Ageing.** No run here is older than September 2026. The surface catalogue is the half that
decays, and the paper itself records a model release cutting em dash use and fine tuning
dropping detection from 97 percent to 3.

## Source alignment, September 2026

The Wikipedia source was reread in full (revision 1373016987, 2026-09-03) and the surface
catalogue aligned with it. Added: assistant artifact codes and utm_source parameters;
deep dive, robust, and highlight as a verb in the vocabulary list; the Markdown-alone
caution carried into the gate; the specific-to-generic test on significance inflation;
procedural self-narration; the Grok note on X rather than Y; the source's own update
banner and em dash proposal box in the aging notes; the two word heading family in the
long page profile. Relabelled: the five category bar is now stated as this skill's own
threshold, because the recheck found no such number in the source.

The StoryScope paper (arXiv 2604.03136v6, 30 pages) was then reread in full and the
discourse layer aligned with it. Corrected two errors: the LAMP comparison baseline is
95.5 on the unedited subset, not 93.2, and the morally ambivalent protagonist row had its
human and AI rates swapped. Added: three missing measured rates (vague allusions 50/72, no
subplots 57/79, internal understanding 27/47), the style boundary rule with the 257 of 304
audit, the clustering numbers (rarity 0.71/0.49, d 0.83, 24.7/7.1 in the rarest decile,
Human to Kimi as the top confusion), the pipeline note (top 20 features, only 6 overlap),
the 408 to 304 dedup, the ModernBERT 99.9 and trivial 83.3 baselines, the 61,608
arithmetic, and the annotator agreement numbers (human to model 0.84, human to human 0.74,
expert humans near perfect) in the false positives file.

No existing case was rerun. The controls in cases 9 and 10 cover none of the new tells,
so the additions rest on the sources' word only and are untested against human drafts.

## Second alignment against the same paper, September 2026

The entry above says the StoryScope paper was reread in full. It was reread as prose. A
second pass walked every table, figure and appendix cell instead, and found that the first
pass had captured almost exactly the numbers the authors chose to narrate in running text,
and almost none of the numbers that exist only in a table.

Two errors corrected:

1. `discourse-tells.md` read the paper's templating experiment as a claim about how the
   stories were generated, and concluded that a different writing workflow yields a different
   tell set. The experiment is about the analysis, not the writing: features induced from raw
   prose against features induced from structured templates of the same stories. The correct
   reading is a procedure rule, and it is now the strongest one in the file. Read prose, find
   prose tells. To reach the discourse layer, build the template first.
2. The clustering section reported human rarity as two rates, 0.71 against 0.49 and 24.7
   percent against 7.1 in the rarest decile, and stopped there. Table 13 gives the counts, and
   they run the other way: 340 human against 487 AI in the rarest tenth, 42 against 41 in the
   rarest hundredth. Rarity is now stated as a group-level shift that settles nothing about
   one text.

Added: the remaining 15 of the 30 core features, with human and AI means from Table 16, which
completes a table that previously held only the rows section 4.1 happens to narrate. The
paper's own seven theme grouping, now the unit of assessment scoring. The one-dimension-at-a-
time rule, 95.4 percent feature coverage against 68.4 for a single sweep, with the dropout
concentrated in revelation and temporal structure. The structural template from Figure 8,
condensed. The human misclassification floor, 88.5 percent recall on human stories, into
`false-positives.md`. Two checks the skill did not have, reader address and
recontextualization, now checks 9 and 10. The Claude fingerprint list, gated behind a known
model. The centroid geometry, 6.6 against 4.3.

Weights on the discourse layer are new and are this skill's own. They map the paper's core
score ranking onto the 2, 1, 0 scale the surface layer already used. Before this pass the
report format printed a weight on discourse findings that nothing in the skill assigned.

Cases 11 to 14 were written for this revision, and cases 1 to 10 were rerun under the new
contract, which is the difference from the entry above. Every case in this file now carries a
MODEL line, a spread figure, and a theme tag on every discourse finding. Fifteen numbered
entries in the section above record what the runs changed.
The new checks are no longer resting on the source's word alone. Case 12 in particular is the
first control in this file that carries machine-leaning values and still has to pass.
