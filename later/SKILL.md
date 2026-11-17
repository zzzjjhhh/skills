---
name: later
description: Park an idea for later in LATER.md in the project folder without
  acting on it, then go back to the current task. Also lists, deletes and
  starts parked ideas. Use when the user invokes /later, or says "save for
  later", "note for later", "park this", "add to the wishlist / waitlist /
  backlog", "don't do it now but remember", or asks what is on the later list.
---

# later: a per-project parking lot for ideas

The list lives in `LATER.md` in the current working directory (the project
root). One list per project, so ideas stay next to the files they are about.

## Modes (decided from `$ARGUMENTS`)

The first word is a subcommand only if it is exactly one of the words below.
Any other text is an idea to add, so `add` is optional.

| Arguments                | Action                                          |
|--------------------------|-------------------------------------------------|
| `add <text>`, or `<text>`| Add it (see "Add")                              |
| empty, or `list`         | Show the items with their IDs                  |
| `start 01`               | Restate, confirm, then do it (see "Start")      |
| `start`, `next`, `pick`  | Show the items, ask which one to start         |
| `delete 01`, `drop 01`   | Remove item 01, no record kept                  |

If the user says "save that for later" with no text, the idea is whatever
they just proposed in the conversation; restate it in your own words.

## File format

`LATER.md` holds only the items, with no headings. Every item has a fixed
two-digit ID (01, 02, ...) that never changes while the item exists. Keep
the items sorted by ID. There is no checkbox and no Started section: an
item is removed from the file once it is started or deleted.

- New ID = the lowest number not used by any item in the list.
- Starting or deleting an item frees its number.
- Numbers in commands (`start 01`, `delete 01`) are these IDs, not row
  positions. `start 1` means 01.

## Add

1. Do NOT start the work. No reading, editing or running anything for the
   idea itself. The only file written is `LATER.md`.
2. Create `LATER.md` if missing (empty, no headings).
3. Add one item with the next free ID:

   - 01 -- YYYY-MM-DD -- <the idea, one or two plain sentences>
     - Files: <script/figure paths it likely touches, if known>
     - Context: <one line: what we were working on when it came up>

   Fill `Files` only from paths already mentioned in this conversation or
   named by the user; otherwise write `Files: unknown`. Don't search for them.
4. Conflict check: if any path under `Files` was edited in this session,
   add `- Overlap: <path> is being edited now; do after current task`.
5. Reply in one line ("Parked as 01 in LATER.md"), then continue exactly
   where the current task left off.

## Start

1. `start 01`: show item 01 (with its Files, Context and Overlap lines),
   restate in one or two plain sentences what you would do, and ask the user
   to confirm. Do no work before the answer.
2. If the user declines or changes the plan, leave the item in the file (edit
   the text only if they ask).
3. On confirmation, remove the item with its sub-bullets from `LATER.md`
   (no record kept). Then do the work as a normal new task.
4. `start`, `next` or `pick` with no ID: list the items numbered by ID, with
   their Files and Overlap lines, ask which to start, then continue at step 1.

## Delete

- `delete 01` (or `drop 01`): remove the item at once. Confirm
  which item first only if the ID is ambiguous or not found.

## Wrapping up

When the current task is clearly finished (user says it's done, or commits),
and `LATER.md` has items, mention in one line: "N ideas parked in
LATER.md. `/later` to review."
