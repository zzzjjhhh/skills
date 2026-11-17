# skills

Small [Claude Code](https://claude.com/claude-code) skills.

| Skill | Use | What it does |
|---|---|---|
| [`echo`](echo/SKILL.md) | `/echo <request>` | Restates your request and a short approach, then lets you pick: execute, grill me first, make a plan, revise, or drop it. Nothing is changed until you choose. |
| [`later`](later/SKILL.md) | `/later <idea>` | Parks an idea in `LATER.md` in the project folder without acting on it, then returns to the current task. Also lists (`/later`), starts (`/later start 01`) and deletes (`/later delete 01`) parked ideas. |

`echo` option 2 ("grill me first") calls a separate `grill-me` skill, which is
not in this repo.

## Motivations

🤝 **echo.** For anyone who knows what they want but not how to say it, and
isn't sure the AI got it. Claude says back what it understood, so you're on
the same page. (Inspiration: *Nonviolent Communication* by Marshall B.
Rosenberg)

💡 **later.** For ADHD brains that spark unrelated ideas mid-task. Park the
idea, stay on track, and do it later.

## Install

Copy the skill folders into your personal skills folder:

```bash
git clone https://github.com/zzzjjhhh/skills.git
mkdir -p ~/.claude/skills
cp -r skills/echo skills/later ~/.claude/skills/
```

Start a new Claude Code session; the skills then appear as `/echo` and
`/later`.

## License

[MIT](LICENSE)
