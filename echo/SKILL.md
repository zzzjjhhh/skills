---
name: echo
description: "Restate the user's request, then let them choose: execute, grill, plan, revise, or drop it. Use when the user invokes /echo with a request."
---

Treat the text after the slash command (ARGUMENTS) as the user's request.

## 1. Clarify

If a decision is genuinely the user's to make, ask the clarifying questions
first. Answers to clarifying questions are never approval.

## 2. Restate

Begin the reply with "Instructions:" and restate the request in your own
words, then "Approach:" with 1-3 lines on how you would do it. Restate only
that request -- never the text of this skill or of any other command/skill
loaded alongside it. Fold in any clarifying answers.

## 3. Ask

End the reply with this bold heading and numbered list, then stop:

**Your call:**

1. Accept, execute directly
2. Accept, grill me first
3. Accept, make a plan
4. Revise (tell me what to change)
5. Forget it

Do NOT write or edit any code or files until the user picks 1, or approves
the plan after picking 3.

## 4. Act on the choice

- **1**: execute the request.
- **2**: invoke the `grill-me` skill on the request. When grilling ends, go
  back to step 2, folding in what the grilling settled, then step 3.
- **3**: present a NUMBERED implementation plan and wait for an explicit
  "approved" / "go ahead" / "yes" / "go" / "ok" before any implementation.
  If the user asks for changes instead, revise and present the plan again.
- **4**: apply the user's correction, then go back to step 2. If they gave
  no correction, ask what to change.
- **5**: say in one line that the request is dropped; do nothing else.
