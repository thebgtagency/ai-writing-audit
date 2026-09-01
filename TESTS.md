# Test log

Ten runs across eight formats, plus two controls. Every claim the skill makes about a
format is backed by a run recorded here. Formats not listed here are covered only by the
derivation procedure in `references/formats.md`, and the skill says so rather than claiming
coverage it has not tested.

All names, businesses, and numbers in these tests are invented.

Controls exist because a tool that finds problems in every text is not a detector. Cases 9
and 10 are drafts a person wrote badly and humanly, and both must come back clean. If a
change to this skill makes a control fail, the change is wrong.

---

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
VERDICT: reads machine (7 weighted findings, count rule for text under 60 words)

FINDINGS
1. [discourse, w2] Nothing in this message required looking at Marcus.
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
7. [discourse, w2] No stance. Nothing here could be disagreed with.

GATED
- "Hey Marcus!" exclamation mark : native to the format
- second person throughout : native
- no evidence or citation : native, nobody cites in a message

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

---

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
VERDICT: reads machine (8 weighted findings)

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
8. [discourse, w2] Named reference check fails in all three steps.

GATED
- merge fields themselves : native. The tell is the sentence around the field.
- repeating the offer across steps : native, a sequence is allowed to be a sequence
- step 3 being short : native

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

---

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
VERDICT: reads machine (7 weighted findings, density 11.3 per 100 words)

FINDINGS
1. [discourse, w2] Resolution by internal understanding.
   Evidence: "comes down to how badly you want this", "decide to bet on themselves",
   "when you're ready to take that step"
   Why: three sentences resolve the exchange inside the reader's head. This is AI feature
   18 in the discourse catalogue and it is the defining move of this format's failure.
   Repair: replace with one external, small, checkable next step.
2. [discourse, w2] Nothing is conceded. The objection is not answered anywhere.
3. [surface, w2] "Totally understand, and I appreciate you being upfront"
   Tell: empathy preamble that costs nothing and delays the answer  Repair: CUT
4. [surface, w2] "A lot of our best clients said the exact same thing"
   Tell: vague attribution, quantity unspecified  Repair: name how many, or cut
5. [surface, w1] "At the end of the day"  Tell: filler  Repair: CUT
6. [discourse, w2] Moral polarity: the reader is sorted into people who decide and people
   who do not. Nothing ambivalent, no case where the answer is no.
7. [format, w2] No sentence in the reply is true and unhelpful to the sale.

GATED
- exclamation marks : native to the medium
- second person : native
- short length : native, and correct here

WHAT IS WORKING
- Nothing. Every sentence pulls one direction.

REWRITE
Thinking about it is the right call at this price. The part people usually need to check is
whether they have four hours a week, because below that it does not work and I would rather
you find that out now. If it helps, I can send the week-one checklist so you can look at
the hours before deciding.
```

---

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
VERDICT: reads machine (8 weighted findings, density 10.3 per 100 words)

FINDINGS
1. [surface, w2] "It's not. It's about systems." and "Consistency isn't a personality
   trait. It's a decision"
   Tell: negative parallelism, twice in 78 words. Once is a rhetorical choice, twice is a
   shape.
   Repair: keep at most one, and only if the second half is concrete.
2. [discourse, w2] "Consistency isn't a personality trait. It's a decision you make once and
   then protect."
   Tell: the closing lesson line. The caption states its own moral.
   Repair: CUT. Test applied: the caption is better without the final two lines.
3. [discourse, w2] "Then I built a simple process, and everything changed."
   Tell: the causal chain has no content. The thing that changed is never named.
   Repair: name the process in one sentence, or cut the claim.
4. [surface, w2] "My stomach would drop"
   Tell: embodied emotion as the default carrier. Measured at 81 percent for machine text
   against 38 percent human.
   Repair: "I felt sick about it" or name what actually happened.
5. [surface, w1] Opening line is a "most people think X" hook that announces itself.
6. [discourse, w2] Single track. No week where the system failed, no cost named.
7. [format, w2] The closing question is rhetorical and expects no answer.
8. [surface, w1] Every paragraph is one to two lines of identical weight.

GATED
- line breaks every sentence : native
- second person : native
- contractions and fragments : native
- zero emoji : not flagged, and not required either

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

---

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
VERDICT: reads machine (9 weighted findings)

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
6. [deck, w2] No slide pulls sideways. No exception, no case where the fix failed.
7. [deck, w1] Five mistakes, five slides, five identical shapes. The count matches the
   promise too neatly.
8. [deck, w2] No slide carries a number, a name, or a date. Named reference check fails
   across the whole deck.
9. [format, w1] Slide 8 is a generic follow ask with no connection to the deck.

GATED
- fragments and missing verbs : native to slides
- bold as emphasis : native, this is a visual medium
- eight slides : not a finding. Deck length is not a tell.

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

---

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
VERDICT: reads machine (8 weighted findings)

READ-ALOUD PASS: performed. Stumbles marked below.

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
5. [discourse, w2] Single track. Nothing costs anything, nothing failed.
6. [discourse, w2] Named reference check fails. No number, no name, no case.
7. [spoken, w2] The final line summarizes and then asks for comments. An outro that
   restates what was just said.
8. [surface, w1] "immediately" and "consistently" are adverbs doing no work when spoken.

GATED
- "If you're struggling" as an opener : native to the format
- second person : native
- contractions : native
- repetition of "you're" : native, repetition is how listeners keep up
- "three things" as an announced structure : native to spoken teaching, and not flagged as
  rule of three. The count was promised to the listener, so it has a job.

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

---

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
VERDICT: reads machine (density 8.9 per 100 words)

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
10. [discourse, w2] Single causal chain from problem to solution. No paragraph costs the
    writer anything. The one section that could have (Challenges) resolves itself in the
    same paragraph.
11. [discourse, w2] Named reference check fails. No customer, no number, no product, no
    date in 213 words.

GATED
- headings and bullets on a long page : native. Structure is the product here.
- length : not a tell
- "However" once : weight 0, transition words in isolation are an ineffective indicator

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

---

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
VERDICT: reads machine (density 10.4 per 100 words)

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
9. [discourse, w2] Named reference check fails. Nothing in the email required knowing
   anything about Jennifer or her team.

GATED
- greeting and sign-off : native to email
- one link : native
- "Hi Jennifer" : native

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

---

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
VERDICT: reads human (0 weighted findings)

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
- A named location. A specific measurement. A named failure mode. An ask that is not an ask.
- The last clause admits the observation might be wrong, which is the ambivalence check
  passing.
```

**Result: pass.** If a future change to the surface layer makes this fail, the change is
wrong.

---

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
VERDICT: reads human (0 weighted findings)

FINDINGS
none

GATED
- "which is probably half true" : hedge, leans human
- "anyway." as a paragraph : the source lists no rule against it, and the gate protects
  rhythm the draft already had
- lowercase throughout : native

WHAT IS WORKING
- Named account, named month, named decision, named cost to the writer.
- Moral polarity is ambivalent and points at the writer.
- The ending does not explain itself. Delete-the-last-line test: removing "tomorrow is a
  normal day" makes it worse, which is the opposite of the machine pattern.
- No lesson stated anywhere.
```

**Result: pass.**

---

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

## What is still untested

Formats with no case here: newsletter, podcast description, job posting, product
description, documentation, chat support reply, video title, thumbnail text, subtitle file,
press release, proposal, invoice note. The skill's derivation procedure covers them by
construction, and the skill does not claim measured coverage of them.
