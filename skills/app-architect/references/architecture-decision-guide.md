# Architecture Decision Guide

Use this guide only when the app request is vague enough that architecture or product direction could drift. The default behavior is autonomous choice: infer, decide, implement, and report assumptions. Questions are for hard boundaries, not normal product ambiguity.

## Intake Checklist

Capture the smallest useful version:

- User: who uses it, and how often?
- Job: what outcome do they need?
- Workflow: what is the first end-to-end task?
- Input: what data, files, prompts, or events enter the system?
- Output: what should the user see, receive, export, or trigger?
- Persistence: what must be saved after the session?
- Collaboration: single user, team, public, or admin-managed?
- Trust: private data, payments, compliance, destructive actions, or production systems?
- Scale: prototype, personal tool, small team, public product, or enterprise?
- Deadline: quick demo, production MVP, or long-lived codebase?

## Autonomous Choice Boundary

Ask the user only when Codex cannot responsibly choose because the decision involves:

- paid services, billing, purchases, or infrastructure costs
- credentials, secrets, private data, regulated data, or compliance duties
- destructive actions, irreversible deletes, migrations, or production deployments
- a specific external system that cannot be inferred or inspected
- a business constraint the user explicitly said is critical
- platform requirements that conflict with the obvious best path

Decide yourself for nearly everything else, including:

- target audience and first workflow when the request implies them
- MVP scope and non-goals
- platform and framework for a prototype or first version
- database and persistence strategy
- auth strategy when accounts are not clearly required
- route, page, and component structure
- exact component names
- minor layout details
- internal folder organization that follows the repo
- local state vs simple server state for non-critical UI
- lightweight validation and error copy
- seed data for demos

If two choices are plausible, prefer the one that is:

- easier to explain to a non-technical user
- faster to make useful end to end
- cheaper to operate
- easier to test
- more aligned with the existing repo
- less likely to require a migration soon

## Default Architecture Heuristics

For a new web app:

- Use the framework already present if inside a repo.
- If no repo exists and the user has no preference, choose a mainstream React or Next.js path for full-stack web apps.
- Keep server logic close to the UI until complexity justifies separation.
- Start with a single database unless the app clearly needs specialized storage.
- Prefer managed auth only when accounts are truly part of the first version.
- Prefer explicit schemas for persisted data and typed boundaries where the stack supports them.

For AI-assisted apps:

- Define the human workflow before the model call.
- Decide what context the model receives, what tools it may use, and what output shape is required.
- Treat prompts, schemas, eval cases, and fallback states as product code.
- Avoid agentic loops unless the task genuinely needs multi-step tool use.
- Add logging or inspection points for model inputs and outputs, without exposing secrets.

When the user only says "make it AI-powered", decide the exact AI role:

- assistant: helps users draft, analyze, or decide
- extractor: turns messy input into structured data
- recommender: ranks options with visible reasons
- automator: performs bounded actions with confirmation gates
- reviewer: checks outputs against rules or quality bars

Choose the simplest role that completes the first workflow.

For internal tools and dashboards:

- Optimize for scanning, filtering, editing, auditability, and repeat use.
- Prefer dense, predictable layouts over marketing-style pages.
- Make permissions and destructive actions explicit.
- Include empty, loading, error, and partial-data states.

For consumer apps:

- Prioritize the first successful moment.
- Keep onboarding short.
- Make state and progress visible.
- Defer accounts until they unlock a real saved or shared workflow.

## Architecture Output Template

Use this shape when the user asks for architecture or when sharing a concise plan before building:

```text
Product brief:
- User:
- Core workflow:
- Success criteria:
- Non-goals:

Decisions:
- Platform:
- Stack:
- Data:
- Auth:
- Integrations:
- Deployment:
- Autonomous assumptions:

Architecture:
- Screens/routes:
- Data model:
- Services/actions:
- State management:
- Error and loading states:
- Tests/verification:

First slice:
1. ...
2. ...
3. ...
```

## Quality Bar

Before implementing, check:

- The first workflow can be completed end to end.
- Every persisted field has a reason to exist.
- Each dependency has a job that local code cannot reasonably do.
- The implementation can be tested or manually verified.
- The architecture can survive one obvious next feature without a rewrite.

After implementing, report:

- what was built
- decisions made for the user
- how it was verified
- what remains intentionally out of scope
