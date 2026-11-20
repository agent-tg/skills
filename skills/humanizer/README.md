# Humanizer

A skill for AI coding agents. It rewrites what your agent writes so it doesn't sound like a robot wrote it. Same facts, less fluff.

## Based on the original

This is my slimmed-down take on [blader/humanizer](https://github.com/blader/humanizer) by Siqi Chen (MIT). Both are built on Wikipedia's guide, [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing). Go star the original. It's bigger, it can match your voice from a writing sample, and it edits files in place.

Mine is shorter and more aggressive about cutting the polite filler agents add to emails and reports.

## What it does

It works in 2 steps.

**Step 1: cut the giveaways.**
- Em dashes
- Words nobody says, like "delve" and "seamless"
- Lines like "it's not just this, it's that"
- Cheesy wrap-up sentences at the end, and stock lines like "I hope this message finds you well"

**Step 2: put a real person back in,** because deleting AI words alone still sounds dead.
- First person "I" instead of third-person fluff
- Real opinions instead of hedging every sentence
- Short and long sentences mixed together
- Real details from your chat, without making anything up
- Short paragraphs with space between them, not one packed block

## Example

These are the same before and after you see in the video.

Before (written by an agent):

> Hello Dana,
>
> I hope this message finds you well! I'm thrilled to share quote #2187 for four replacement load wheels for your pallet jack — a seamless fix to keep your operation moving. The total comes to $184.50, including shipping and tax.
>
> This isn't just a quote — it's a commitment to your success. The wheels are in stock and will ship Thursday if you approve by Wednesday.
>
> Please don't hesitate to reach out with any questions!
>
> Best regards,
> Taylor

After:

> Hello Dana,
>
> Here's quote #2187 for four replacement load wheels for your pallet jack. The total is $184.50, including shipping and tax.
>
> I have the wheels in stock. If you approve by Wednesday, I'll ship them Thursday.
>
> Best regards,
> Taylor

It also takes a position when the facts support one. Before:

> Hi Marcus,
>
> Thank you for asking about which label printer to choose. Both the Zebra ZD421 and the Rollo are solid options, and the right choice ultimately depends on your needs. The Zebra costs $449 and the Rollo costs $199. In our warehouse, the Rollo jammed about twice a week over three months, while the Zebra has not jammed once in a year. That said, some users may find the Rollo perfectly adequate for lighter workloads. It could potentially be worth considering your volume, which you mentioned is around 300 labels a day.
>
> I hope this helps you navigate your decision!
>
> Best,
> Priya

After:

> Hi Marcus,
>
> I'd go with the Zebra ZD421. It costs $449, against $199 for the Rollo.
>
> In our warehouse the Rollo jammed about twice a week over three months. The Zebra hasn't jammed once in a year.
>
> You mentioned you print around 300 labels a day. The Rollo might hold up fine at a lighter volume, but at yours I'd pay the extra $250.
>
> Best,
> Priya

I ran this skill and the original on these texts and a report closing page, 3 times each, in a clean Claude Code. Both kept every fact and removed the em dashes and AI words every time. Mine also cut the "any questions" line and the "thank you for your continued partnership" ending every time, and wrote the email as the sender ("I have the wheels in stock"). The original did neither. Both picked the Zebra. That's one small test on three short texts, not a benchmark.

## Install

1. Copy this `humanizer` folder into your agent's skills folder:
   - **Claude Code:** `~/.claude/skills/`
   - **Codex:** `~/.codex/skills/`

   Nothing else to install. If you already have the original Humanizer installed, they share the name `humanizer`, so keep one.

2. Add this 1 line to your `CLAUDE.md` or `AGENTS.md`:

   ```text
   Always run the humanizer skill on external communication where a human will read it.
   ```

   That way you don't have to ask. Your agent runs it every time it writes an email, report, post or doc for a person.

3. Start a new session. To run it by hand, say `humanize this:` and paste the text, or type `/humanizer` in Claude Code.

## Limits

- **It doesn't check facts.** If your agent got a price or a date wrong, Humanizer keeps it wrong, just in a nicer voice.
- **Check any opinion it adds.** When it takes a stance, the reasons should come from your text. An early version once added a judgment of its own. There's a rule against that now, and it held in 3 of 3 test runs, but read it before you send it.
- **It needs something real from you.** It won't make up a story to sound human. The more your agent knows about how you talk, the more it sounds like you.
- It edits for people, not for AI detectors.
- If you have your own voice guide, the skill follows it instead of replacing your voice.

## License

MIT. See [LICENSE](../../LICENSE). Credit to [blader/humanizer](https://github.com/blader/humanizer) (MIT, copyright Siqi Chen) and Wikipedia's WikiProject AI Cleanup.
