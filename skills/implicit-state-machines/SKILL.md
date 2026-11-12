---
name: implicit-state-machines
description: "Implicit state machines: find every hidden multi-step process in an app, plan the fixes with the owner, then fix them all through tested, reviewed, released lanes. Use when asked to find implicit or hidden state machines, hunt bugs in save, upload, sync, delete or refresh flows, or continue a state-machine audit into a gameplan or fixes."
---

# Implicit State Machines

Find the places where an app tracks a multi-step process with scattered flags, then fix the ones that can lose or corrupt data.

An **implicit state machine** is a process that is really in one situation at a time (clean, edited, saving, uploading, in conflict) but is tracked by separate booleans, refs and nullable fields. Six flags allow 64 combinations; a handful are intended. Bugs live in the rest. The method is always: name the situations, then ask what every event does in each one. "Nobody decided" is a bug.

Run three phases in order, as far as the request reaches. "Find" or "audit" means Phase 1 only. "Plan" means through Phase 2. "Fix", "run it all", or a request that sets no limit means all three phases without stopping between them: save each phase's report, then keep going. Honor review-only, no-push and scope limits from the request and the project's instructions; this skill grants no authority of its own.

**Come back to the owner only with a real question.** A real question is one of the four in "When to stop and ask" in [references/fix-lanes.md](references/fix-lanes.md), or approval the project's own rules require. Decide everything else yourself and record the decision in the report. When a question comes up, do not park the run: ask it once, with a recommendation, and keep working every lane the answer does not touch. Hold all questions that can wait and ask them together at the end of the phase, in the multiple-choice format under "Asking the owner". Never ask "should I continue?".

## Phase 1 — Find

Answer the prompt "find all of the implicit state machines in this app". Read-only.

1. Sweep the whole app: UI state hooks and refs, stores, adapters, server functions, SQL, scheduled jobs, importers. Include status columns, lease and lock fields, idempotency keys, retry counters, and states derived from missing or present values. Skip generated, vendored and build output. Skim pure calculation code. Say what was skipped or skimmed.
2. Use the "Events to ask about in every state" list in [references/state-map-template.md](references/state-map-template.md) as the lens. It is the fastest way to spot a risky family.
3. Group findings into workflow families per module. A module is one of the app's own feature areas (its navigation or routes); if it has none, use top-level source folders, and keep server jobs and importers as their own modules. For each family: where it lives (`path:line`), the situations it can be in, the flags that encode them, what is at stake (data loss, double write, wrong delete, stale display, cosmetic), and one line on what reading the code suggests could go wrong.
4. Classify each family: **risky** (save, upload, sync, delete, money, merge, auth restore), **tidy-only**, or **leave alone** (simple toggles, labels that claim nothing).
5. Save the catalog as a dated report inside the project's own reports folder. If the project has none, use its docs folder or create `docs/reports/`, and say where it went. Never leave the only copy in a temp directory; later phases depend on it.
6. Report in plain English: counts by module, the risky families, and what the audit did not do (no tests run, not exhaustive, groupings are analytical, not confirmed bugs).

The catalog is a list of candidates, not a bug list. Do not label anything CONFIRMED or SUSPECTED yet; that needs the step-by-step trace Phase 2 does. Stop here only if the request ends at Phase 1.

## Phase 2 — Gameplan

Turn the catalog into an ordered plan the owner can accept or change.

1. Rank risky families by harm and likelihood. Recommend one family to do first as the proof of the pattern, then the order for the rest. Name what to leave alone and why.
2. For the first family, write a **state map** using [references/state-map-template.md](references/state-map-template.md). Label every invalid combination CONFIRMED (trace shown) or SUSPECTED. Do not overstate; nothing has been run yet.
3. Surface decisions that belong to the owner: behavior choices, anything that deletes recoverable data, paid changes, new features hiding inside a "fix" (say so and keep them out of scope).
4. Save the plan in plain English next to the catalog: what is confirmed, what is suspected, the proposed steps, and what will not be covered.

If the request ends at Phase 2, stop and present the plan. Otherwise go on to Phase 3 with every family that needs no owner decision, and send the owner decisions as one batch of questions. A recommendation is not approval: do not act on a family that waits on an answer.

## Phase 3 — Fix them all

Read [references/fix-lanes.md](references/fix-lanes.md) before starting lanes. In outline:

1. **Tests first.** Pin today's guarantees with characterization tests. For each defect write the correct behavior as an expected-failure test so the suite stays green and each fix visibly flips one test. Build fakes faithful enough to prove or rule out timing suspicions; a mock that never changes loading state proves nothing.
2. **One lane per family**, each mapping its own area before fixing. Lanes with disjoint files run in parallel in isolated worktrees. Work that shares a file runs in series. Lanes fix only what they can prove, one commit per fix, and return unproven items and server changes as proposals.
3. **Consolidate only where it pays.** Move decisions into one reducer or controller, effects outside, when it removes scattered flags and behavior stays equal. If each fix is a single condition, do not add a reducer.
4. **Independent review** before merging anything that touches saved user data, shared code, rewritten test expectations, or a database function. The reviewer did not write the code and gets the diff, not the conclusion.
5. **Merge, check, release** through the project's normal path. Apply backward-compatible database changes in the order that keeps the live app working.
6. **Verify live**, and say exactly what was and was not proven.
7. **Sweep what is left before you call it done.** List every item still open and sort each into one of four piles:
   - *Fix now*: needs no owner decision, including work that only needs a migration, a small guard, or a proposal you can safely build as a fix. Fix these in this run, through the same tested, reviewed, released path. A run is not finished while this pile has anything in it.
   - *Ask the owner*: one of the real questions. Ask it in the format below.
   - *Another repo or tool*: say whose it is and write a ready prompt for that project's agent.
   - *Leave alone*: tidy-only or not worth the risk. Say why in one line. Tidy-only means nobody would notice and nothing is lost or paid for. Anything that can post twice, pay twice, send twice, overwrite someone's edit or call a route that does not exist is a bug, not a tidy item, however small.
   There is no fifth pile. "Found but not fixed", "worth doing next" and "say go and I'll fix them" are not allowed endings: if an item needs no decision, fix it; if it needs one, ask it. Bugs noticed outside this skill's lens go through the same four piles.
8. **After the owner answers, finish.** Build and release what the answers unlock, then update the results report. Do not wait to be told again.

Hold back, and ask the owner about, anything that deletes recoverable data or changes behavior by choice rather than by fix. Finish everything else first, so the owner gets one short list of questions and a finished run, not a paused one.

## Asking the owner

Ask in the chat the owner is using, as one numbered list of multiple-choice questions, so the owner can answer in one line ("1 A, 2 B, 3 A"). Use another channel only when the project's rules send questions there or the owner is away, and never ask the same question in two places.

For each question:

- One plain sentence on what is wrong and who would notice. No code names without a few words of explanation.
- Two to four lettered choices. Say what each one does and what it risks or costs.
- Your recommendation first, marked "(recommended)", with one line of why.

Ask at these points: with the gameplan (decisions the plan depends on), when a blocking question comes up mid-fix, and once after the leftover sweep. Batch them; a run should put questions to the owner two or three times, not twenty. Keep working everything the answers do not touch while you wait.

## Closing message

The owner should know in five seconds whether the run is finished. End every run, and answer every "is it all done?", in this shape and nothing longer:

1. First line, one of:
   - **Done. Safe to close this chat.** Everything found is fixed and live, or deliberately left alone.
   - **Not done. N things left.** Then the lists below.
2. **Needs your answer**: the multiple-choice questions, numbered. Omit if empty.
3. **I am still doing**: what is in progress and when it will be live. Omit if empty.
4. **Belongs to someone else**: one line each, with the ready prompt. Omit if empty.
5. **Left alone on purpose**: one line each with the reason. Omit if empty.
6. One line on proof: what was seen working live and what is tests-only.

Keep it under about 15 lines. No recap of what was fixed, no lane names, no file paths: those live in the results report, linked once. If the first line cannot honestly say "Done", the run goes back to the leftover sweep, not to the owner.

## Reporting

The results report is the full record; the chat gets the closing message above. Write the report once, at the end of the last phase the request covers. Use plain English and short sentences. For every family report: fixed (with the user-visible change), ruled out (so nobody re-investigates), left open (with why and which pile from the leftover sweep it is in), and how it was checked. "Left open" should hold only items waiting on an owner answer, owned by another repo, or deliberately left alone. Keep "tests pass", "released", and "seen working live" as three separate claims. A read-only login proves pages load; it does not prove saves.

## Limits

This finds bugs in how a process flows. It does not find wrong formulas, slow pages, or undersized infrastructure. If production breaks mid-run, first separate "our release" from "the platform": check whether a clean visit loads, roll back one release as an experiment, and read platform logs before blaming or exonerating the change.

## Optional explainer

If the owner wants to understand the concept or share it, offer a short explainer: one everyday analogy (a traffic light versus three loose switches), the 64-combinations idea, the real bugs from this run drawn as clashing switches, the method, the fix, and the limit. Use drawn graphics, never real screenshots of private data.
