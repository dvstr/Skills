# Skills

Reusable Codex skills by [dvstr](https://github.com/dvstr).

## Available skills

| Skill | Purpose | Output |
| --- | --- | --- |
| [PRD Creator](skills/prd-creator/SKILL.md) | Discover the problem, audience, business requirements, scope and success criteria. | A business-focused PRD in the active project. |
| [Jira Story Creator](skills/jira-story-creator/SKILL.md) | Resolve material questions, then prepare a Story Description for developer refinement and QA. | Markdown in chat, ready to paste into Jira. No Jira issues are created. |

## Installation

Clone outside your installed skills directories:

```sh
git clone https://github.com/dvstr/Skills.git
mkdir -p ~/.agents/skills
```

Copy each desired **complete folder** from `Skills/skills/` into `~/.agents/skills/`, preserving its `SKILL.md`, `agents/` and bundled resources. For example, copy `Skills/skills/jira-story-creator/` to `~/.agents/skills/jira-story-creator/`.

Before replacing an installed skill, back it up or review your local changes. Avoid a second copy with the same name in a project's `.agents/skills` directory. Codex detects local skills automatically; restart Codex if a skill does not appear.

## Use Jira Story Creator

Open the target project and invoke:

```text
$jira-story-creator Prepare a Story Description for looking up webhook delivery status by client code.
```

The skill researches available context and asks focused questions only for unresolved material decisions. It preserves agreed scope and delegated ownership, then drafts these sections:

1. User Story
2. Context / Problem
3. Functional Requirements
4. Technical Requirements
5. Design Notes
6. Out of Scope
7. Acceptance Criteria

Acceptance criteria use numbered scenario headings and separate Given/When/Then bullets, grouped by Happy path, Edge cases, Error states and Non-functional criteria where applicable. It does not invent behavior to fill empty sections, create BE/FE/QA subtasks, or publish to Jira or Confluence.

The bundled [template](skills/jira-story-creator/references/TEMPLATE.md) defines the description structure; [examples](skills/jira-story-creator/references/EXAMPLE.md) illustrate discovery and behavioral coverage. Resource paths are relative to the skill's `SKILL.md`. Examples are not product defaults.

This initial published Jira Story Creator version preserves the installed skill before the template-enforcement changes, providing a recoverable baseline in Git history.

## Use PRD Creator

Open the target project in Codex and invoke:

```text
$prd-creator Create a PRD for improving the signup flow.
```

The skill interviews you about the problem, audience, business requirements, measurable goals, scope, constraints, and dependencies. It asks for confirmation before generating the PRD, and keeps technical architecture and implementation details outside the document.

Your explicit output destination takes priority. Relative destinations are resolved against the established active project root. Otherwise, output goes to `documents/PRD/` under that root, using `YYYY-MM-DD-<epic-slug>-prd.md` unless you specify a filename. If the target project is unclear, the skill asks. Generated PRDs stay outside the installed skill folder unless explicitly requested.

Bundled [template](skills/prd-creator/references/prd-en-for-skill.md) and [guide](skills/prd-creator/references/prd-guide-for-skill.md) paths are resolved relative to the skill's `SKILL.md`.
