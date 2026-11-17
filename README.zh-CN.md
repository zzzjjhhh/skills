# skills

[English](README.md) | 简体中文

一些小巧的 Claude Code 技能（skills）。

| 技能 | 用法 | 功能 |
|---|---|---|
| [`echo`](echo/SKILL.md) | `/echo <请求>` | 复述你的请求和简要做法，然后让你选择：直接执行、先盘问我、制定计划、修改，或放弃。在你做出选择之前不做任何改动。 |
| [`grill-me`](grill-me/SKILL.md) | `/grill-me` | 就一个计划向你提问，每轮几个决定，每个都附推荐答案，直到不再有任何未经确认的假设。 |
| [`later`](later/SKILL.md) | `/later <想法>` | 把想法记在项目文件夹的 `LATER.md` 里，先不执行，然后回到当前任务。也可以列出（`/later`）、开始（`/later start 01`）和删除（`/later delete 01`）已记下的想法。 |

`echo` 的选项 2（"grill me first"，先盘问我）会调用 [`grill-me`](grill-me/SKILL.md)。

## 初衷

🤝 **echo.** 适合知道自己想要什么、却不知道怎么表达，也不确定 AI 是否理解的人。AI 会复述它的理解，确保你们想的是同一件事。（灵感来自马歇尔·卢森堡（Marshall B. Rosenberg）的《非暴力沟通》（*Nonviolent Communication*））

❓ **grill-me.** 适合不确定自己是否已经想清楚的时候。每次回答几个问题，直到没有任何需要猜测的地方。

💡 **later.** 适合做事做到一半就冒出无关想法的 ADHD 大脑。先把想法存起来，专注当前任务，以后再做。

## 许可证

[MIT](LICENSE)。`grill-me` 改编自 Matt Pocock 的
[grill-me](https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me)
（MIT，见 [grill-me/LICENSE](grill-me/LICENSE)）。
