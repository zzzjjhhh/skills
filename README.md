# skills

Small Claude Code skills.

| Skill | Use | What it does |
|---|---|---|
| [`echo`](echo/SKILL.md) | `/echo <request>` | Restates your request and a short approach, then lets you pick: execute, grill me first, make a plan, revise, or drop it. Nothing is changed until you choose. |
| [`grill-me`](grill-me/SKILL.md) | `/grill-me` | Questions you about a plan, a few decisions per round, each with a recommended answer, until nothing is left assumed. |
| [`later`](later/SKILL.md) | `/later <idea>` | Parks an idea in `LATER.md` in the project folder without acting on it, then returns to the current task. Also lists (`/later`), starts (`/later start 01`) and deletes (`/later delete 01`) parked ideas. |

`echo` option 2 ("grill me first") calls [`grill-me`](grill-me/SKILL.md).

## Motivations

🤝 **echo.** For anyone who knows what they want but not how to say it, and
isn't sure the AI got it. The AI says back what it understood, so you're on
the same page. (Inspired by *Nonviolent Communication* by Marshall B.
Rosenberg)

❓ **grill-me.** For when you're not sure you've thought it through. Answer a
few questions at a time until nothing is left to guess.

💡 **later.** For ADHD brains that spark unrelated ideas mid-task. Park the
idea, stay on track, and do it later.

## License

[MIT](LICENSE). `grill-me` is adapted from Matt Pocock's
[grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)
(MIT, see [grill-me/LICENSE](grill-me/LICENSE)).
