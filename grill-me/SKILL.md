---
name: grill-me
description: Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thinking, or uses any 'grill' trigger phrases.
---

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the frontier using the AskUserQuestion tool. Its normal guidance is to reach for it only when genuinely blocked on a user decision — a grilling session is nothing but such decisions, so that reticence is overridden for the whole session: use it for every question, including open-ended ones.

The tool caps each call at 4 questions. If the frontier is wider than that, rank its questions by how much each would reshape the others and ask the highest-leverage 4 first; because each call returns before the next is made, frame the remaining sub-batches of the round with those answers already in hand rather than pre-writing the whole round up front.

For each question:

- `header` — a short title (12 char limit)
- `question` — the question body
- `options[0]` — your recommended answer, labeled `... (Recommended)`
- `options[1..3]` — the real alternatives you actually considered
- don't add an "Other" option yourself — the tool appends one automatically, and it's what catches an answer you didn't enumerate

Each round the user answers reshapes the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

Finding _facts_ is your job, never the user's. When a frontier question needs a fact from the environment (filesystem, tools, etc.), dispatch a sub-agent to find it; don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The _decisions_ are the user's: put each to them and wait.

The session is done when the frontier is empty: every branch of the design tree visited, nothing left silently assumed. Do not act on it until the user confirms you have reached a shared understanding.
