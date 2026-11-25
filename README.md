# claude-skills

Skills for [Claude Code](https://claude.com/claude-code) that question you about a plan, decision, or software design until every assumption is out in the open, before anything gets built.

## Skills

| Skill | How it starts | What it does |
|---|---|---|
| `interrogate` | Claude starts it when you ask to be interrogated, probed, or pressure-tested | The core questioning loop: models your idea as a decision map, asks in waves of numbered questions with a suggested answer for each, looks up facts itself, and waits for you to confirm before acting |
| `probe` | You type `/probe` | Runs an `interrogate` session on any subject: code, product, business, writing |
| `domain-modeling` | Claude starts it when glossary or ADR work comes up | Sharpens a project's vocabulary as you design, keeping `GLOSSARY.md` and decision records (`docs/adr/`) up to date |
| `probe-with-docs` | You type `/probe-with-docs` | `interrogate` + `domain-modeling`: the same session, recording a glossary and ADRs as it goes |
| `probe-stack` | You type `/probe-stack` | `interrogate` + `domain-modeling` for software: must cover every layer of the stack (product, data, logic, API/integration, UI, security, compliance, performance, reliability, observability, infrastructure, and testing) while recording a glossary and ADRs as it goes |

`probe`, `probe-with-docs`, and `probe-stack` call the other skills by name, so install them together.

## Install

Copy the folders in `skills/` into your personal skills folder:

```bash
git clone https://github.com/gilfoyle19/claude-skills.git
cp -r claude-skills/skills/* ~/.claude/skills/
```

On Windows the folder is `%USERPROFILE%\.claude\skills\`. To use them in a single project only, copy them into that project's `.claude/skills/` instead.

## Usage

```
/probe should we move our team from Jira to Linear?
/probe-stack a booking web app for a chain of 5 dental clinics
/probe-with-docs the new billing module
```

Answer a whole wave at once by number, for example `1 yes, 2 the second option, 3 no, because...`. Replying "yes" accepts the suggested answer.

## Credits

`interrogate`, `probe`, `domain-modeling`, and `probe-with-docs` are reworded adaptations of the `grilling`, `grill-me`, `domain-modeling`, and `grill-with-docs` skills from [Matt Pocock's skills](https://github.com/mattpocock/skills), used under the MIT License. `probe-stack` is new.

## License

MIT. See [LICENSE](./LICENSE).
