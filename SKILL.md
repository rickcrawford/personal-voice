---
name: personal-voice
description: |
  Write and edit prose so it reads like a specific person wrote it, not an AI
  agent. Use this whenever drafting or rewriting anything that will be read by
  humans (a blog post, essay, newsletter, email, README, doc, social post, or
  report) and you want it to sound personal rather than generated. Also use it
  as a pre-publish pass to strip the patterns that make text read as AI, and to
  match a particular person's voice when a writing sample is provided. Strips em
  dashes and en dashes from output by default. Built on the humanizer skill,
  Wikipedia's "Signs of AI writing," and the no-ai-slop and deslop projects.
  Works in two modes: detect (flag the tells without rewriting) or edit (rewrite
  in place). Every pass reports an ai-smell score from 0 to 100 that rates how
  machine-generated the writing reads. Triggers include
  "make this sound human," "this reads like AI," "rewrite in my voice," "clean
  this up before I post it," "write this as a person, not a bot," or any request
  for natural, personal-sounding writing.
license: MIT
compatibility: claude-code claude-ai cowork opencode
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
---

# Personal Voice

Write and edit so the result reads like a person, not an agent. This skill does two jobs: it drafts new writing in a natural personal voice, and it audits existing drafts to remove the patterns that flag text as AI-generated. It is built on the humanizer skill, which draws its pattern catalog from Wikipedia's "Signs of AI writing" (maintained by WikiProject AI Cleanup), with additional patterns observed in long-form drafting and borrowed from the no-ai-slop and deslop projects.

## Personal voice versus agent voice

Agent prose is fluent, even, and anonymous. Every sentence is roughly the same length. It reports facts without reacting to them. It reaches for the most statistically likely phrasing, which is why so much of it sounds the same. It hedges, it pads, it announces what it is about to do, and it closes on vague optimism. None of it is wrong, exactly. It just doesn't sound like anyone.

Personal voice sounds like a particular human thinking. The rhythm is uneven on purpose: a short sentence, then a long one that wanders a little before it lands. There are opinions. There is the occasional aside or half-finished thought. The writer trusts the reader and uses plain words. You can tell a person is behind it because the writing takes positions a neutral summary wouldn't.

The whole job is to move text from the first kind to the second.

## Default punctuation: no em or en dashes

This skill does not use em dashes (—) or en dashes (–) in the writing it produces or edits. That is a default feature, not an optional house style.

**When drafting.** Do not reach for an em or en dash as a connector, aside, or punch. Use a comma, a period and a new sentence, or parentheses instead.

**When auditing.** Find every em dash and en dash in the draft and rewrite each one. Common swaps:

- Aside or interruption: parentheses, or split into two sentences.
- Contrast or pivot: comma, semicolon, or a conjunction (*but*, *and*, *so*).
- Appositive: commas.
- Date or number ranges: *from 1990 to 2000*, *pages 12 to 15*, or a hyphen only when the style guide treats it as a compound modifier.

Keep hyphens only inside genuinely hyphenated words (*well-known*, *long-term*).

**Voice-sample exception.** If the user's sample clearly and consistently uses em dashes as a personal habit, match that habit sparingly. Still strip en dashes unless the sample uses them for ranges and the user wants them preserved. When in doubt, remove dashes.

**User override.** If the user explicitly asks to keep dashes, follow their instruction for that task.

## Match the writer's voice when you can

If the user gives a writing sample (their own earlier writing, or a piece whose voice they want), read it before drafting and match it. Note these things in the sample:

- Sentence length and how much it varies
- Word-choice level: casual, plain, academic, technical
- How paragraphs open: straight into the point, or some setup first
- Punctuation habits: dashes, parenthetical asides, semicolons, sentence fragments
- Recurring phrases or verbal tics
- How transitions work: explicit connectors, or just moving to the next thing

Then match those patterns, not just the absence of AI tells. If they write short sentences, don't produce long ones. If they say "stuff" and "things," don't upgrade to "elements" and "components." If no sample is given, fall back to the default natural voice described under Personality and soul.

A sample can come inline ("rewrite this in my voice, here's how I write: ...") or as a file ("match the style in this file"). When voice matters a lot and no sample exists, it is fine to ask the user for one.

## The six tells that recur most

If you do nothing else, hunt these six. They are the loudest signals that a model produced a piece, and they show up far more than the rest. The first three are contrast and closer tics; the next three are structural habits.

**The X-not-Y construction.** A declarative sentence followed by a contrasting negation. "Good writing is a habit, not a talent." Once it can land. Three times in a piece it is a tic, and the contrast is doing the work that conviction should. Variants: "It's not just X, it's Y," "Not X. Y," "It's not about X. It's about Y," the "it was never X, it is Y" reveal that ends on an abstraction ("the cost was never the tool, it is the space between them"), and tailing negations like "no guessing" tacked onto the end. Fix: say what the thing is and let the reader register the contrast. If the contrast matters, give the opposing case its own developed sentence.

**The contrast-flip couplet.** Two consecutive short sentences where the second negates or inverts the first, both ending flat. "The tool works. The team doesn't use it." "The data is there. Nobody reads it." Reading three in a row is the single strongest tell. Fix: combine into one sentence with a conjunction, or develop the second sentence so it does more than negate the first, or cut the second entirely.

**The rhetorical wrap-up.** A short declarative that claims to settle the argument, paired with a clause that demotes everything else. "That's the whole game. The rest is execution." "That picture is the plan. Everything else is detail." It mimics a mic drop with no speaker behind it, and it usually substitutes for actually finishing the argument. Fix: cut the line (the paragraph above probably made the point), or replace it with a real transition, or make it specific by naming the actual thing it waves at. A related move is the circular bookend, closing a passage by restating its opening in new words (see the catalog).

**Journey and travel metaphor stacks.** Journey, arc, path, voyage, embark, navigate, and landscape applied to things that do not move. "The product has a journey." "Across that arc." "The path forward." Once one travel word lands, related ones pile up. Fix: use the literal word (process, stages, sequence, pattern). If the sentence still works after the swap, the metaphor was not earning its keep. A single anchoring travel metaphor in a title or thesis can be fine; proliferation is the tell.

**Signposting and announcements.** "Let's dive in." "Here's what you need to know." "Let's break this down." "Without further ado." The model narrates its own outline instead of writing. Fix: do the thing. "Let's look at how caching works" becomes "Caching here happens at three layers."

**Rule of three.** Forcing ideas into triplets: "faster, better, cheaper," "speed, scale, security," three parallel bullets that could be two or four. The model defaults to three because it sounds comprehensive. Fix: count what is actually there and use that number. A related move is the one-move-solves-all convergence: list N problems, then claim a single thing answers all N ("three pressures, and consolidation is the one move that answers all three"). See the catalog.

**Scan next:** significance inflation (*stands as, testament, pivotal*), superficial `-ing` endings (*highlighting, underscoring, ensuring*), fragmented headers (heading followed by a one-line restatement), colon reveals (*the best part: it learns*), faux-insight openers (*here's the thing, what nobody tells you*), empty intensifiers (*just, really, actually, simply*), AI vocabulary clusters (*delve, tapestry, robust, leverage* when three or more appear close together), and em or en dashes.

The full catalog of every other tell (promotional language, vague attributions, false ranges, copula avoidance, persuasive authority tropes, filler phrases, hedging, generic positive conclusions, conjunctive-adverb crutches, em dashes, inline-header lists, title case, emojis, curly quotes, temporal inflation openers, balanced both-sides pivots, and more) lives in `references/ai-tells.md`. Read that file when drafting or auditing anything substantial.

## Personality and soul

Removing tells is only half the job. Clean but voiceless prose still reads as AI. Signs of soulless writing: every sentence the same length, no opinions, no acknowledged complexity, no first person where it fits, reads like a press release.

How to put a pulse in it:

- Have opinions and react to facts instead of just listing them. "I still don't know how to feel about this" is more human than a balanced pro-con list.
- Vary rhythm hard. Short hits next to longer sentences that take their time getting where they're going.
- Acknowledge real complexity. "This is useful and a little unsettling" beats "this is useful."
- Use "I" when it fits. First person is honest, not unprofessional.
- Let some mess in. A tangent, an aside, a half-formed thought. Perfect structure feels algorithmic.
- Be specific about feelings and details instead of reaching for an abstraction.

## Optional house style

A user or repo may layer constraints on top of the natural voice. When the user states any of these, treat them as binding for the task and apply them throughout:

- Dash policy override. The default is no em or en dashes (see above). If the user wants dashes allowed or banned even more strictly, follow that for the task.
- Banned words or phrases. Keep the user's list and strip every instance.
- Formatting limits. For example, no bold, no headers, plain prose only, or a length cap.
- Point of view, tense, or audience constraints.

If the user gives no house style, use the defaults in this skill and the catalog.

## Two modes: detect or edit

Decide which the user wants before touching the text.

**Detect.** The user asks "is this AI slop?", "does this read like AI?", or "what tells are in here?" They want a diagnosis, not a rewrite. Name each tell using the catalog's vocabulary, quote the exact line it appears in, and give a one-line fix. Do not rewrite the piece. Order the findings by how loud they are (top six first). If the text is genuinely clean, say so and stop.

**Edit.** The user asks you to rewrite, clean up, or humanize. Follow the editing workflow below and return the revised text.

When it is ambiguous, ask, or lead with a short detect pass and offer to do the edit.

## How hard to edit

Match the size of your changes to whose voice the text carries and how much voice the piece needs.

- **The user's own draft.** Make the minimum effective edits. Fix the tells and leave the rest of their words, cadence, and structure alone. The edit should feel invisible: the writer should read the result and recognize it as theirs, only cleaner. Do not upgrade their vocabulary, even out their rhythm, or add flourishes. Over-polishing a person's draft is its own kind of slop.
- **A voiceless AI draft the user will publish as their own.** Edit freely. Strip the tells and add the personality described under Personality and soul.
- **Functional writing where voice barely matters** (a form, a compliance doc, a status update). Removing tells is the whole job; you do not need to inject personality. Be direct and be done.

## Writing a new piece

1. Get the angle straight first. What does the writer actually think about this, and why is it worth saying? Lead from that, not from a definition.
2. Match the sample voice if one was given; otherwise use the natural voice above.
3. Draft with plain verbs, varied rhythm, and real opinions. Do not use em or en dashes.
4. Run the audit below before calling it done.

## Editing or auditing a draft

1. Read it once for content and meaning.
2. Read it again hunting the top six: X-not-Y, contrast-flip couplets, rhetorical wrap-ups, journey/travel metaphor stacks, signposting, and rule of three.
3. Scan headings for title case and for warm-up lines that just restate the heading.
4. Scan paragraphs for significance inflation, superficial `-ing` endings, colon reveals ("the best part: ..."), faux-insight openers ("here's the thing," "what nobody tells you"), empty intensifiers (just, really, actually, literally, simply), and clusters of inflated AI vocabulary (three or more watch-words close together).
5. Remove every em dash and en dash. Rewrite each with commas, parentheses, conjunctions, or new sentences.
6. Rewrite each problem in place, making the smallest change that fixes the tell (see How hard to edit). Preserve meaning, and preserve the writer's voice if a sample was given or the draft is already theirs.
7. Re-audit after any rewrite. Tidy triplets (rule of three) and circular bookends are the tells most likely to creep back in when a sentence gets edited.

## The ai-smell score

The judge pass produces a number: an ai-smell score from 0 to 100, where 0 reads fully human and 100 reads obviously machine-generated. Lower is better. It is a structured self-assessment of how the writing reads, not a detector verdict and not proof of authorship. Its main value is relative: comparing a draft before and after a pass, and forcing the judge to point at specific tells instead of waving at "feels AI."

Score five dimensions, each capped as shown, then sum them. The caps weight the loudest signals highest.

| Dimension | Cap | What it measures | Maps to |
|-----------|-----|------------------|---------|
| Structural tics | 30 | X-not-Y, contrast-flip couplets, rhetorical wrap-ups, travel-metaphor stacks, signposting, rule of three, colon reveals, faux-insight openers, false-depth reveals, one-move-solves-all, circular bookends | Top six plus entries 42 to 46 |
| Rhythm and burstiness | 20 | Sentence-length variation and paragraph shape. Uniform, metronomic cadence scores high | Entry 35 |
| Voice and stance | 20 | Opinions, first person where it fits, landing a position, acknowledged complexity. Neutral press-release tone scores high | Entries 35, 37, 21 |
| Lexical tells | 20 | AI-vocabulary clusters, significance inflation, promotional language, empty intensifiers, copula avoidance, superficial `-ing`, filler, vague attributions | Entries 4, 6 to 11, 18, 19, 47 |
| Formatting artifacts | 10 | Em/en dashes, boldface overuse, inline-header lists, title case, emojis, curly quotes, takeaway boxes | Entries 23 to 28, 40 |

Rough anchors within a dimension: 0 means none of its tells appear; roughly a third of the cap means one or two isolated instances; roughly two-thirds means a recurring habit; the cap means the writing is built on that category.

Scoring rules, so the number stays honest:

- **Reason first, then score.** Do the "what makes this AI" pass and cite instances before you assign any number. Scoring after explicit reasoning tracks human judgment far better than a snap holistic rating; this is the core finding behind G-Eval and rubric-based LLM judges (see the research note in the catalog).
- **Cite or it doesn't count.** Every point added to a dimension must point at an actual instance, quoted or named with catalog vocabulary. A score with no evidence is invalid; when in doubt, score lower.
- **Score as a skeptic, not the author.** LLM judges reliably under-rate tells written in their own style (self-preference bias) and reward length and surface fluency (verbosity bias). You will be partly blind to your own tics. Counter it: hunt harder than feels necessary, and never add or subtract points for length or polish alone.
- **Be consistent run to run** so before/after deltas mean something.
- **Voice and stance is not applicable to functional writing** (a form, a compliance doc, a status update). For those, drop that dimension, score out of 80, and say so. A bland voice is not a defect when voice was never the point.

Bands:

- **0 to 15, clean.** Reads human. Ship it.
- **16 to 35, faint.** Mostly clean; a few tells linger. One more targeted pass is worth it.
- **36 to 60, noticeable.** Reads as AI in places. Needs real revision.
- **61 to 100, strong.** Obviously machine-generated. Rework.

## The final pass: read it aloud and score

If you can't read a paragraph aloud without hearing the cadence of a model, it still reads as AI. After the draft, run this pass explicitly:

1. Ask: "What would make this so obviously AI-generated?" Answer honestly with the specific remaining tells, naming them with the vocabulary from the catalog.
2. Score the draft on the ai-smell rubric above, citing evidence per dimension.
3. Revise to fix the tells, heaviest dimensions first.
4. Re-score the revised version.
5. Present the final version and report the score.

## Output format

Every mode reports the ai-smell score. Report it as the headline number plus the per-dimension breakdown with cited evidence, so the score is explainable rather than a black box:

```
AI-smell: 12/100 (faint)
  Structural tics   4/30  one X-not-Y in paragraph 2
  Rhythm            4/20  middle section runs even
  Voice and stance  2/20  lands a clear position
  Lexical tells     2/20  "leverage" once
  Formatting        0/10  clean
```

In **detect** mode, lead with the score, then provide the findings: each tell named with catalog vocabulary, the quoted line, and a one-line fix, loudest first. No rewrite.

In **edit** mode, provide the draft rewrite, a short honest answer to "what still reads as AI here," and the final version after fixing those. Report the score as a before to after delta ("AI-smell: 58/100 noticeable, to 12/100 faint"). A brief bullet summary of changes is optional when it helps; when you edited the user's own draft, that summary doubles as a "what changed" list so they can see every touch.

For fresh writing, provide the finished piece and its final score, having already run the read-aloud and scoring pass internally.

## Reference files

- `references/ai-tells.md`: the full catalog of AI writing patterns with before-and-after examples for each. Read it for any substantial draft or audit.

## External sources

These are worth consulting when updating the catalog or when a piece needs deeper pattern-matching than the skill alone provides. Treat them as descriptive field guides, not proof of AI authorship. No single word or pattern is definitive; clusters of weak signals matter more than any one hit. Automated detectors (GPTZero, Turnitin, etc.) are unreliable on their own; Wikipedia's guide explicitly warns against relying on them.

| Source | What it contributes |
|--------|---------------------|
| [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) | Primary catalog. Maintained by WikiProject AI Cleanup from thousands of flagged submissions. Covers content inflation, formatting tics, negative parallelisms, AI vocabulary, and more. |
| [WikiProject AI Cleanup / Guide](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup/Guide) | Operational cleanup guide: how to spot AI content, fix sourcing problems, and handle tagged articles. |
| [no-ai-slop (Peter Yang)](https://github.com/petergyang/no-ai-slop) | The detect-vs-edit split, the minimum-effective-edit principle, and specific tells: colon reveals, throat-clearing openers, banned intensifiers. |
| [deslop (Stephen Turner)](https://blog.stephenturner.us/p/deslop) | Dramatic-pause directives ("let that sink in"), a scoring-rubric approach, and calibrating edit aggressiveness to how voice-critical the piece is. |
| [G-Eval (Liu et al. 2023)](https://arxiv.org/abs/2303.16634) | Rubric-based LLM-as-a-judge. Grounds the ai-smell score's reason-first, score-per-dimension design. |
| [Self-Preference Bias in LLM Judges (Wataoka et al. 2024)](https://arxiv.org/abs/2410.21819) | Judges under-rate tells in their own style. Grounds the "score as a skeptic" rule. |
| [Excess vocabulary (Kobak et al. 2024)](https://arxiv.org/abs/2406.07016) | Measured LLM word overuse across 14M abstracts. Empirical backbone for the lexical dimension. `references/ai-tells.md` has the fuller research note. |
| [GPTZero AI Vocabulary](https://gptzero.me/news/most-common-ai-vocabulary/) | Statistical word-frequency list updated from millions of human vs. AI comparisons. Good for lexical tells (*delve, showcasing, today's fast-paced world*). |
| [Pangram Labs: Spotting AI Writing Patterns](https://www.pangram.com/blog/comprehensive-guide-to-spotting-ai-writing-patterns) | Practical guide on rhythm (low burstiness), em dashes, organized paragraphs, and "Overall"/"In conclusion" closers. |
| [Google Cloud: Statistical tells (Weinmeister)](https://medium.com/google-cloud/detecting-ai-generated-text-by-uncovering-its-statistical-tells-042c8d0e3a24) | Data-driven analysis of signposting (*here's, let's, break down*), authoritative qualifiers (*crucial, comprehensive*), and sycophantic openers (*great question*). |
| [VU Amsterdam ALP Guide](https://vu.nl/en/about-vu/more-about/alp-guide-spotting-ai-writing) | Academic framing: boosters vs. hedges, bland/robotic style, overly poetic language (*rich tapestry*), low perplexity. |
| [ACL 2025: LLM Fingerprints (Sarvazyan et al.)](https://aclanthology.org/2025.genaidetect-1.6/) | Research showing models leave persistent lexical and syntactic fingerprints across domains. Supports treating structural patterns as more durable tells than individual words. |
