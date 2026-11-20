---
name: humanizer
description: |
  Remove AI writing patterns from text and put a real person back in. Use when
  editing, reviewing or writing anything a human will read: emails, reports,
  posts, docs. Catches em dashes, AI vocabulary ("delve", "seamless"),
  "not just X, it's Y" lines, inflated claims, filler and tidy wrap-up endings,
  then adds first person, real opinions, varied rhythm and true specifics.
license: MIT
metadata:
  version: 1.0.0
---


# Humanizer

## Philosophy

Avoiding AI patterns is half the job. The other half is adding a pulse. Sterile, voiceless writing is just as obvious as slop. Good writing has a human behind it: someone with opinions, rhythm, and the occasional tangent.

The goal is not merely clean writing. The goal is writing that sounds like a person wrote it.

## When to Use

Use this skill when the user asks to humanize, de-AI, de-slop, un-ChatGPT, rewrite, polish, edit, or review text for AI tells.

Also apply it to user-facing prose when writing summaries, recommendations, documentation, reports, client-facing notes, PR descriptions, long explanations, or external-facing content.

When another voice skill or project voice guide applies, preserve that voice. Humanizing should remove AI tells, not replace the intended author.

## Step 1: cut the giveaways

### AI tells to remove

**Significance inflation:** "serves as a testament," "pivotal moment," "evolving landscape," "indelible mark," "deeply rooted," "setting the stage for."

**Promotional language:** "vibrant," "breathtaking," "groundbreaking," "nestled," "in the heart of," "stunning," "must-visit," "boasts a," "showcasing," "renowned."

**Copula avoidance:** "serves as," "stands as," "functions as," "marks a," "represents a." Usually, use "is."

**AI vocabulary:** additionally, align with, crucial, delve, emphasizing, enduring, enhance, fostering, garner, highlight (verb), interplay, intricate, intricacies, key (adjective), landscape (abstract), leverage, multifaceted, navigate (metaphorical), paramount, pivotal, realm, robust, seamless, showcase, tapestry (abstract), testament, underscore (verb), valuable, vibrant.

**Over-formal transitions:** "Furthermore," "Moreover," "Additionally," "In conclusion," or "Ultimately" when they merely signpost a template.

**Superficial -ing phrases:** "highlighting the importance of," "underscoring its significance," "reflecting the community's," "contributing to broader," "symbolizing the ongoing."

**Negative parallelisms:** "It is not just X, it is Y" or "Not only A but also B" when used as a stock rhetorical device.

**Antithesis templates:** Avoid "This is not about X, it is about Y," "More than just X, this is Y," and similar constructions unless the contrast is sharp and necessary.

**Rule-of-three abuse:** Forcing ideas into triplets such as "innovation, inspiration, and industry insights."

**Synonym cycling:** Swapping words such as "protagonist," "main character," "central figure," and "hero" across consecutive sentences instead of repeating the clearest term.

**False ranges:** "From X to Y" where X and Y are not points on a meaningful scale.

**Formulaic structure:** Stock sections such as "Despite challenges... continues to thrive" or "Challenges and Future Prospects."

**Over-balanced structure:** Forcing the writing into a broad introduction, three evenly weighted sections, and a summary conclusion regardless of what the material needs.

**Communication artifacts:** "I hope this helps," "Great question," "Here is a," or "Let me know if" when they add no value.

**Stock pleasantries:** "I hope this message finds you well," "I am writing to," "Please let me know if you have any questions," "We appreciate your continued partnership," "We look forward to sharing further progress," "Please don't hesitate to reach out." Delete them outright. Do not swap one for a shorter version of the same line ("Questions? Just ask," "Questions are welcome"). The reader already knows they can reply. A real person opens with the point and stops when the point is made. A plain greeting and sign-off ("Hello Dana," "Best regards, Sam") can stay.

**Hedging stacks:** "could potentially possibly be argued that it might."

**Both-sidesism:** Neutralizing every claim with "however," "on the other hand," or "the right choice depends" instead of taking the position supported by the evidence.

**Low information density:** Paragraphs that restate the same point with new synonyms instead of adding a fact, reason, decision, example, or next step.

**Fake anecdotes:** Invented personal stories, dramatic examples, or lived experience. Use real observed details or keep it direct.

**Generic endings:** "the future looks bright," "exciting times lie ahead," or "a step in the right direction."

**Tidy-bow closers:** Final sentences that restate the obvious or thank the reader for nothing, such as "Ultimately, understanding X is key to navigating Y" or "These results reflect a strong start." Test the last sentence: if it adds no fact, decision or next step, delete it.

### Style tells

- Avoid em dashes and semicolons. Replace them with commas, periods, colons, or parentheses.
- Do not mechanically bold every key term.
- Avoid vertical lists where every bullet uses a bold label followed by an explanation.
- Avoid fake-consultant lists where every bullet has the same polished rhythm.
- Do not put every word in headings in title case.
- Do not decorate headings or bullets with emojis.
- Use straight quotation marks unless the destination requires typographic quotes.
- Vary sentence length and structure.
- Do not pack everything into one block. Cutting filler must not flatten the layout.
- Take a position when the evidence supports one.

### Soulless writing

- No first-person perspective when it would be natural.
- No acknowledgment of uncertainty or mixed feelings.
- No voice, edge, or personality.
- Writing that reads like a generic encyclopedia entry or press release.

## Step 2: put a real person back in

Deleting AI words alone still reads dead. Do these too.

1. **Have opinions.** Do not merely report facts. React when the context calls for it.
2. **Vary rhythm.** Mix short, punchy sentences with longer ones.
3. **Acknowledge real complexity.** Name mixed evidence or tension without adding empty caveats.
4. **Use first person when it fits.** First person is not inherently unprofessional. When one person signs the message, write as that person: "I have the wheels in stock," not "The wheels are in stock and will be shipped." Use "we" only when a team really is speaking, as in a company report.
5. **Allow some texture.** Perfectly symmetrical structure often feels mechanical.
6. **Be specific about reactions.** Replace broad labels such as "concerning" with the concrete reason.
7. **Prefer direct verbs.** Use "is" over "serves as." Cut filler such as "in order to."
8. **Replace vague attributions.** Name the actual source or remove the claim.
9. **End on a specific fact or next step.** Do not manufacture an inspirational conclusion.
10. **Add human specificity.** Use exact fields, systems, numbers, names, failure modes, or observed behavior when available. Never invent details.
11. **Use lists when they improve scanning.** Keep useful steps, fields, options, checks, risks, and recommendations as lists.
12. **Do not force a tidy ending.** It is fine to end on the last substantive point.
13. **Take the stance the evidence supports.** Add a caveat only when a real tradeoff exists.
14. **Make every sentence earn its place.** Each should add a fact, reason, decision, example, risk, or next step.
15. **Let structure follow priority.** Important ideas can take more space. Minor points can remain one line.
16. **Give it room to breathe.** Write short paragraphs with a blank line between them, the way a person types an email. One idea per paragraph: what it is, then what happens next or what the reader should do. In an email, keep the greeting, each paragraph and the sign-off on their own lines. Keep the paragraph breaks and headings the original had unless one is now empty. A single short paragraph is fine only when there is one idea.
17. **Preserve the intended voice.** Follow the applicable personal, brand, or project voice guide.
18. **Keep operational writing precise.** Preserve exact names, risks, useful bullets, and next steps.

## Procedure

1. Read the input and identify its meaning, audience, intended tone, and any voice guide that applies.
2. Cut empty openers, throat-clearing, recap sentences, and closing lines that add nothing.
3. Cut low-density sentences that repeat a point without adding useful information.
4. Scan for the patterns listed above.
5. Rewrite the problem sections while preserving facts, intent, and important terminology.
6. Produce a draft rewrite.
7. Self-audit the draft by asking, "What still makes this sound AI-generated?"
8. Revise those remaining tells.
9. Check the layout: short paragraphs, blank lines between them, nothing crammed into one block.
10. Present the final version.

## Output

For ordinary responses, apply these rules silently and return only the final writing.

When the user explicitly asks for an audit, rewrite, edit, review, or Humanizer pass, return:

1. Draft rewrite
2. A brief "What still reads as AI?" audit
3. Final rewrite
4. A short summary of material changes when useful

## Quick Reference

| Before | After |
| --- | --- |
| "In order to achieve this" | "To achieve this" |
| "Due to the fact that" | "Because" |
| "At this point in time" | "Now" |
| "Has the ability to" | "Can" |
| "It is important to note that" | Cut it and start with the point |
| "Serves as a catalyst for" | "Drives" or "causes" |
| "A rich tapestry of" | Describe the actual thing |
| "In today's rapidly evolving landscape" | Cut it |

## Reference

Based on [blader/humanizer](https://github.com/blader/humanizer) (MIT, by Siqi Chen) and Wikipedia's ["Signs of AI writing"](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide maintained by WikiProject AI Cleanup.
