# Running the fix lanes

Read this before Phase 3. The parent owns scope, review, merging, database changes, release and the answer to the owner. Follow the host's model and delegation rules; the parent synthesizes and does not grind files.

## Lane work order

Give each lane a brief that stands alone. Include:

- **Finished means:** a state map for its area, tests for risky transitions, every CONFIRMED defect fixed one commit each, checks clean. State that the owner authorized the work.
- **Scope:** the exact files it owns, and the files other lanes own that it must not touch. Shared files (common libraries, app shell) belong to one lane only.
- **Hypotheses to verify, not assume:** the suspicions from the catalog, each to be confirmed or ruled out.
- **Method:** map, characterization tests, then failing test, minimal fix, same visible design and saved-data format. No new dependencies. No new features; a missing feature is a proposal.
- **Limits:** no push, no deploy, no production data, no applying migrations, no spawning agents. Server changes come back as a new migration file plus tests for the parent to review, written to be backward compatible with the currently deployed client.
- **Checks:** typecheck, lint, format on touched files, and that module's tests only. The parent runs the full suite at merge.
- **Return:** branch and commits, each defect confirmed or ruled out with its fix and test, items left for the owner, real output tails, and exact live-check steps.

## Parallel lanes without collisions

- Isolated worktrees, branched from the current release, one writer per file set.
- If the test runner globs the repo, exclude the worktree folder first. Otherwise one lane's run executes every other lane's half-written tests and the failure counts are meaningless.
- Several full suites at once cause timeouts that look like regressions. Rerun on a quiet machine before believing a failure, and check whether a failing test also fails alone on untouched code.
- A test that fails at certain hours usually mixes two clocks (client UTC versus database local date). Fix the test; do not carry it as "known flaky".

## Review before merge

Send a reviewer that did not write the code when the change touches saved user data, shared code, or database functions. Ask it to check:

- Every guarantee from the map still holds after any reducer move, including same-tick double submit when a synchronous lock became reducer state.
- Rewritten test assertions are intended behavior changes, not weakened tests.
- Shared-code changes cannot resurrect deleted rows, keep stale rows over newer ones, or leak across account changes.
- For a replaced database function: diff the **live** definition against the new body. A migration built from a stale repo copy silently regresses live behavior. Confirm callers of any dropped signature still resolve, grants and ownership match live, and a rejected path changes nothing.
- No change to saved-row or local-draft formats.

If the review finds the canonical schema file out of date with the migration, fix it in the same change.

## Merge and release

1. Bring lane commits onto the current release branch in order; run format, typecheck, lint, the full suite and the build.
2. Apply each database change in one transaction, register it in migration history, then verify it directly (for a trigger, a write inside a rolled-back transaction). A transient API error may mean nothing applied; check state before retrying.
3. Deploy changed server functions only after reading their diff. Keep response shapes compatible with the client that is live now.
4. Release through the project's normal path. Record migrations, decisions and open items in the project's own records.
5. Remove merged worktrees. Keep a branch only while it holds an undecided change.

## Live verification

- A read-only verification login proves pages load and write controls are hidden or locked. It cannot prove a save.
- To prove saves, ask the owner before using any writable path. One safe pattern: temporarily make the test login a normal account with its own empty data, run the save, discard, switch and two-tab conflict cases on a blank record, delete the test rows and local drafts, restore the original access exactly, and confirm the read-only state is back.
- Never exercise hard-to-undo actions (merge, removal, money posting) on real data to prove a fix. Open the preview, confirm it loads, and close without confirming.
- A focus or visibility refresh may briefly lock fields each time automation touches a tab; wait for the fields to re-enable before typing.
- Report three things separately: tests pass, released, seen working live. Name each path that is test-only.

## When to stop and ask

- Deleting data the user could still recover (backups, drafts, history).
- A behavior choice with no single correct answer.
- Any paid change, and any change of plan or size on shared infrastructure. Gather evidence first; the owner will ask whether it is needed.
- Work that turns out to be a new feature.
