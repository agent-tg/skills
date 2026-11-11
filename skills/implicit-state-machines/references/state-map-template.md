# State map template

Write one map per workflow family, saved as a dated report in the project. Use plain English and short sentences; explain a term of art once. Use repo-relative paths with line numbers. A map is evidence for a decision, so label what was read versus what was run.

## Sections

1. **Flag inventory.** A table of every state hook, ref, derived value, storage key and server field that takes part: name, `path:line`, what it means, who sets it.
2. **States as they exist today.** Use what the code shows, not what it should be. Group into natural sub-machines, for example: editor and save, draft recovery, upload, navigation, ownership and version.
3. **Transition table per sub-machine.** State, event, guard, next state, side effects, `path:line`.
4. **Invalid or unguarded combinations.** For each: the flag combination, a concrete scenario a user could hit, the lines, and a label.
   - **CONFIRMED-by-reading**: the trace is shown step by step.
   - **SUSPECTED**: depends on timing, data, or code not traced. Say what would prove it.
5. **Guarantees a refactor must keep.** Each with the lines that implement it. Examples: an acknowledged write is never repeated on retry; archive before restore; idempotent retry; version-conflict detection; double-submit lock; drafts survive failure.
6. **Test coverage and gaps.** Which transitions have tests. Note test doubles that cannot show a real race.
7. **Proposed controller boundary.** State shape, event list, what stays outside as effects, and small separately shippable steps: tests first, pure refactors with no behavior change, then one fix per commit. Mark it a proposal.
8. **Open questions.** What the map could not settle and what evidence would.

## Events to ask about in every state

Run each of these against every state. The gaps are the findings.

- The same action fired twice (double click, Enter plus click).
- A slow reply arriving after a newer one.
- A reply that never arrives, or arrives after the user moved on.
- Leaving, closing, or switching date, tab or account mid-operation.
- The record changing on another device or tab.
- A background refresh landing during a write.
- A read-only or signed-out user reaching a write path.
- A failure in the second half of a two-part write.
- A reload after an uncertain outcome.
- The server or network being unreachable with no timeout.

## Common shapes of the bug

- A button checks one busy flag and forgets another.
- A "discard" clears the flag but not what is on screen.
- A preview or result belongs to an earlier choice and stays confirmable.
- A loading flag with no "took too long" state, so the app waits forever.
- A retry key reused with a changed body, or regenerated for the same body.
- "Newer" decided by a device clock instead of the server.
- A banner that implies progress when nothing is polling.
