# Skills

Reusable Codex skills by [dvstr](https://github.com/dvstr).

## Available skills

- [PRD Creator](skills/prd-creator/SKILL.md): turn product ideas into business-focused Product Requirements Documents through a structured discovery interview. Includes a bundled PRD template and writing guide.

## Install PRD Creator

Clone this repository into a working folder outside your installed skills directories:

```sh
git clone https://github.com/dvstr/Skills.git
mkdir -p ~/.agents/skills
```

Copy the complete `Skills/skills/prd-creator/` folder to `~/.agents/skills/prd-creator/`. The installed folder must contain `SKILL.md`, `agents/`, and `references/`.

If `prd-creator` is already installed, keep your existing copy or back it up and update it deliberately. Avoid installing a second copy with the same skill name in a project's `.agents/skills` directory, as both may appear in skill selectors.

Codex detects local skills automatically. If the skill does not appear, restart Codex.

## Use PRD Creator

Open the target project in Codex and invoke:

```text
$prd-creator Create a PRD for improving the signup flow.
```

The skill interviews you about the problem, audience, business requirements, measurable goals, scope, constraints, and dependencies. It asks for confirmation before generating the PRD, and keeps technical architecture and implementation details outside the document.

Your explicit output destination takes priority. Relative destinations are resolved against the established active project root. Otherwise, output goes to `documents/PRD/` under that root, using `YYYY-MM-DD-<epic-slug>-prd.md` unless you specify a filename. If the target project is unclear, the skill asks. Generated PRDs stay outside the installed skill folder unless explicitly requested.

Bundled [template](skills/prd-creator/references/prd-en-for-skill.md) and [guide](skills/prd-creator/references/prd-guide-for-skill.md) paths are resolved relative to the skill's `SKILL.md`.
