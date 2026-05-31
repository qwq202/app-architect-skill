# App Architect Skill

App Architect is a Codex skill for turning vague natural-language app ideas into concrete product decisions, architecture, and implementation plans.

It is designed for users who know what they want in ordinary language but do not know how to choose a stack, scope the first version, shape the data model, or make architecture tradeoffs. The skill instructs Codex to make the best reasonable choices on the user's behalf and keep moving, asking only when a decision involves hard boundaries such as money, production systems, private data, credentials, compliance, or irreversible actions.

## Install

Copy the skill folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R app-architect ~/.codex/skills/app-architect
```

Restart or refresh Codex so it can discover the skill.

## Use

Invoke it directly:

```text
Use $app-architect to make the best product and architecture decisions for this app idea, then turn them into an implementation plan.
```

Example:

```text
Use $app-architect. I want to build an app that helps small teams track customer requests and know what to work on next.
```

## What It Does

- Converts fuzzy app ideas into a product brief.
- Chooses product scope, stack, data model, UI structure, and implementation path.
- Avoids handing the user a menu of options when Codex can make a reasonable decision.
- Keeps architecture fit-for-purpose instead of overbuilt.
- Pushes toward a working vertical slice before speculative extensibility.

## Contents

```text
app-architect/
  SKILL.md
  agents/openai.yaml
  references/architecture-decision-guide.md
```
