---
name: implicit-state-machines
description: "Implicit state machines: find every hidden multi-step process in an app, plan the fixes with the owner, then fix them all through tested, reviewed, released lanes. Use when asked to find implicit or hidden state machines, hunt bugs in save, upload, sync, delete or refresh flows, or continue a state-machine audit into a gameplan or fixes."
---

# Implicit State Machines

Find the places where an app tracks a multi-step process with scattered flags, then fix the ones that can lose or corrupt data.

An **implicit state machine** is a process that is really in one situation at a time (clean, edited, saving, uploading, in conflict) but is tracked by separate booleans, refs and nullable fields. Six flags allow 64 combinations; a handful are intended. Bugs live in the rest. The method is always: name the situations, then ask what every event does in each one. "Nobody decided" is a bug.

Run three phases in order. **Stop at the end of Phase 1 and Phase 2** and wait for the owner. Honor review-only, no-push and scope limits from the request and the project's instructions; this skill grants no authority of its own.

## Phase 1 — Find

Answer the prompt "find all of the implicit state machines in this app". Read-only.

1. Sweep the whole app: UI state hooks and refs, stores, adapters, server functions, SQL, scheduled jobs, importers. Include status columns, lease and lock fields, idempotency keys, retry counters, and states derived from missing or present values. Skip generated, vendored and build output. Skim pure calculation code. Say what was skipped or skimmed.
2. Use the "Events to ask about in every state" list in [references/state-map-template.md](references/state-map-template.md) as the lens. It is the fastest way to spot a risky family.
3. Group findings into workflow families per module. A module is one of the app's own feature areas (its navigation or routes); if it has none, use top-level source folders, and keep server jobs and importers as their own modules. For each family: where it lives (`path:line`), the situations it can be in, the flags that encode them, what is at stake (data loss, double write, wrong delete, stale display, cosmetic), and one line on what reading the code suggests could go wrong.
4. Classify each family: **risky** (save, upload, sync, delete, money, merge, auth restore), **tidy-only**, or **leave alone** (simple toggles, labels that claim nothing).
5. Save the catalog as a dated report inside the project's own reports folder. If the project has none, use its docs folder or create `docs/reports/`, and say where it went. Never leave the only copy in a temp directory; later phases depend on it.
6. Report in plain English: counts by module, the risky families, and what the audit did not do (no tests run, not exhaustive, groupings are analytical, not confirmed bugs).

Stop. The catalog is a list of candidates, not a bug list. Do not label anything CONFIRMED or SUSPECTED yet; that needs the step-by-step trace Phase 2 does.

## Phase 2 — Gameplan

Turn the catalog into an ordered plan the owner can accept or change.

1. Rank risky families by harm and likelihood. Recommend one family to do first as the proof of the pattern, then the order for the rest. Name what to leave alone and why.
2. For the first family, write a **state map** using [references/state-map-template.md](references/state-map-template.md). Label every invalid combination CONFIRMED (trace shown) or SUSPECTED. Do not overstate; nothing has been run yet.
3. Surface decisions that belong to the owner: behavior choices, anything that deletes recoverable data, paid changes, new features hiding inside a "fix" (say so and keep them out of scope).
4. Present the plan in plain English: what is confirmed, what is suspected, the proposed steps, and what will not be covered.

Stop for a go-ahead. A recommendation is not approval.

## Phase 3 — Fix them all

Read [references/fix-lanes.md](references/fix-lanes.md) before starting lanes. In outline:

1. **Tests first.** Pin today's guarantees with characterization tests. For each defect write the correct behavior as an expected-failure test so the suite stays green and each fix visibly flips one test. Build fakes faithful enough to prove or rule out timing suspicions; a mock that never changes loading state proves nothing.
2. **One lane per family**, each mapping its own area before fixing. Lanes with disjoint files run in parallel in isolated worktrees. Work that shares a file runs in series. Lanes fix only what they can prove, one commit per fix, and return unproven items and server changes as proposals.
3. **Consolidate only where it pays.** Move decisions into one reducer or controller, effects outside, when it removes scattered flags and behavior stays equal. If each fix is a single condition, do not add a reducer.
4. **Independent review** before merging anything that touches saved user data, shared code, rewritten test expectations, or a database function. The reviewer did not write the code and gets the diff, not the conclusion.
5. **Merge, check, release** through the project's normal path. Apply backward-compatible database changes in the order that keeps the live app working.
6. **Verify live**, and say exactly what was and was not proven.

Hold back, and ask the owner about, anything that deletes recoverable data or changes behavior by choice rather than by fix.

## Reporting

Use plain English and short sentences. For every family report: fixed (with the user-visible change), ruled out (so nobody re-investigates), left open (with why), and how it was checked. Keep "tests pass", "released", and "seen working live" as three separate claims. A read-only login proves pages load; it does not prove saves.

## Limits

This finds bugs in how a process flows. It does not find wrong formulas, slow pages, or undersized infrastructure. If production breaks mid-run, first separate "our release" from "the platform": check whether a clean visit loads, roll back one release as an experiment, and read platform logs before blaming or exonerating the change.

## Optional explainer

If the owner wants to understand the concept or share it, offer a short explainer: one everyday analogy (a traffic light versus three loose switches), the 64-combinations idea, the real bugs from this run drawn as clashing switches, the method, the fix, and the limit. Use drawn graphics, never real screenshots of private data.
