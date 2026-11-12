# Implicit State Machines

A skill for AI coding agents. It finds the bugs hiding in your app's multi-step flows, then helps you fix them.

It started as one sentence I typed into a coding agent:

> find all of the implicit state machines in my app

I didn't fully understand the phrase when I typed it. It found real bugs in five parts of my production app in one night, so I turned what happened next into this skill.

## What is an implicit state machine?

A traffic light has three states: green, yellow, red. It is only ever one of them.

Now build that light from three loose switches, one per color. Nothing stops green and red from being on together. The states are still real, but nothing enforces them.

Apps do this all the time, and mine did. A page is really "clean", "edited", "saving", "uploading" or "in conflict", but the code tracks that with separate true/false flags. Six flags allow 64 combinations. Only a handful were planned. Bugs live in the rest.

## Why the prompt works

"Find bugs" is vague. This gives the agent a method:

1. Find every hidden multi-step process.
2. List the situations each one can be in.
3. For every button and event, ask what happens in each situation.

When the answer is "nobody decided", you have found a bug.

## The kind of bugs it finds

These are from the run this skill was built on:

- A "Discard" button that still worked during a photo upload, leaving an orphaned file.
- A "Discard and leave" that cleared the unsaved flag but left the old edits on screen, ready to be saved by accident.
- A delete dialog that could confirm against the preview for a different option.
- A sign-in screen with a loading state and no "this is taking too long" state, so it waited forever when the server was down.
- A retry key reused with changed data, so every later save was rejected.

## How it runs

Three phases. How far it goes depends on what you ask for.

| Phase | You say | It does |
| --- | --- | --- |
| 1. Find | `find all of the implicit state machines in this app` | Sweeps the app, sorts findings into risky, tidy-only and leave-alone, saves the list, and stops. |
| 2. Gameplan | `what's our gameplan from here` | Ranks the risky ones, maps the first in detail, marks each problem confirmed or suspected, and stops with the plan. |
| 3. Fix | `go, fix them all` | Writes tests first, fixes each area, reviews risky changes independently, releases, verifies, then sweeps up what is left. |

You can also say `run it all`. Then it goes through all three phases without stopping and comes back only with real questions.

## How it treats you

I ran this on four apps in one night and changed it three times before morning. These rules came out of that night.

- **No-stop mode.** It decides routine things itself and writes the decision down. It asks you only about real choices: behavior, deleting data you could get back, money, or approval your project requires.
- **Multiple-choice questions.** Questions come as one numbered list with lettered choices and a recommendation. You can answer in one line: "1 A, 2 B, 3 A".
- **Leftover sweep.** Before it can say it is done, it sorts everything still open into four piles: fix now, ask the owner, belongs to another repo, or leave alone with a reason. "Found but not fixed" is not an allowed ending.
- **Clear closing message.** The first line of its last message is either "Done. Safe to close this chat." or "Not done. N things left."

## Install

Copy this `implicit-state-machines` folder into your agent's skills directory.

- **Claude Code:** `~/.claude/skills/`
- **Codex:** `~/.codex/skills/`

Then start a new session in your project and use the Phase 1 prompt above.

## What's inside

- `SKILL.md`: the three phases, how it asks questions, the leftover sweep and the closing message.
- `references/state-map-template.md`: how to map one workflow, the events to test in every state, and common bug shapes.
- `references/fix-lanes.md`: how to run parallel fix work safely, what to review before merging, and how to verify live.

## Limits

- It finds bugs in how a process flows. It does not find wrong formulas, slow pages, or undersized infrastructure.
- Phase 1 produces candidates, not confirmed bugs. Phase 2 is where each one is labeled confirmed or suspected.
- "Tests pass", "released" and "seen working live" are three different claims. The skill reports them separately. Hold it to that.
- Check that the agent is reading your current code. On my runs, three audits started from old copies and one finding was wrong because of it.
- I have run it on nine apps I build and run. Eight went through to released fixes; one was a find-only trial. Nobody outside my own setup has tried it yet. Expect to adapt it.
- It follows your project's own rules for testing, review and release. It grants the agent no authority of its own.

## License

MIT. See [LICENSE](../../LICENSE).
