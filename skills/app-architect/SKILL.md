---
name: app-architect
description: Turn vague natural-language app ideas into buildable product decisions, architecture, and implementation plans, with Codex making the best reasonable choices on the user's behalf. Use when a user asks Codex to build, design, scaffold, or improve an application, website, SaaS, dashboard, internal tool, AI tool, mobile app, or full-stack system but gives fuzzy requirements, avoids key tradeoffs, asks for a "perfect architecture", or expects Codex to choose the product scope, architecture, stack, data model, and implementation path autonomously.
---

# App Architect

## Purpose

Use this skill to convert an unclear app request into a concrete, testable build path. Codex must act as the product and architecture decision maker, not as a questionnaire. Optimize for an architecture that is simple, coherent, maintainable, and appropriate to the actual product risk, not for abstract perfection.

Keep the user's language and tone. If the user is non-technical, explain decisions in product terms before implementation terms.

## Autonomy Mandate

Make the best reasonable choice on the user's behalf whenever the choice is reversible, low-risk, or inferable from the product goal. Do not ask the user to choose between stacks, architecture patterns, UI structures, databases, auth approaches, or implementation phases unless the choice crosses a hard boundary.

Ask only when proceeding would likely cause one of these problems:

- real money, billing, purchasing, or paid infrastructure
- destructive actions or irreversible data loss
- production deployment or changes to live systems
- credentials, private user data, regulated data, or legal/compliance obligations
- a required external integration that cannot be inferred or inspected
- a business constraint the user explicitly said matters

When there is uncertainty, choose the safest strong default, state the assumption briefly, and keep moving.

## Operating Mode

1. Restate the app as a product brief:
   - primary user
   - core job to be done
   - first useful workflow
   - success criteria
   - explicit non-goals

2. Make the missing decisions:
   - infer the target user, first workflow, scope, and success criteria from the request
   - choose the platform, stack, data model, state model, UI structure, and verification path
   - prefer one recommended path over option lists
   - record important assumptions without blocking on them

3. Lock the first version:
   - define the smallest complete product slice
   - list must-have screens or commands
   - list data entities and relationships
   - list integrations and external dependencies
   - list risks and validation checks

4. Choose architecture:
   - prefer the current repo's existing stack and conventions
   - for a new web app, prefer a mainstream, low-friction full-stack path unless the user specifies otherwise
   - separate product decisions from implementation details
   - avoid unnecessary microservices, custom frameworks, premature abstractions, and speculative extensibility

5. Execute:
   - inspect the existing project before changing files
   - implement a working vertical slice first
   - add structure only when it removes real complexity
   - verify with tests, builds, linters, or focused manual checks that match the project
   - report the assumptions that became code

## Decision Rules

Use the detailed checklist in `references/architecture-decision-guide.md` when:

- starting a new app from a vague idea
- choosing a stack, data model, auth model, deployment target, or AI integration
- deciding whether to ask the user or pick a default
- reviewing whether the plan is overbuilt or under-specified

Default to these rules:

- Product first: define what the user can accomplish before naming technologies.
- One coherent system: every screen, route, model, and service should serve the first useful workflow.
- Boring is good: choose proven tools over novelty unless novelty is the actual requirement.
- Reversible decisions should be made by Codex. Irreversible or costly decisions need user confirmation.
- "Architecture perfect" means fit-for-purpose, observable, testable, and easy to change.
- A good autonomous decision is specific, justified by the goal, cheap to change, and immediately actionable.

## Response Pattern

For planning-only requests, produce:

1. Product brief
2. Decisions Codex is making for the user
3. Recommended architecture
4. Implementation phases
5. Blockers only if a hard boundary prevents progress

For build requests, produce the brief internally, share only the high-signal version, then implement. Do not stop at a plan unless the user explicitly asks for planning only.

## Anti-Patterns

Avoid:

- interviewing the user about every preference
- presenting many equal options without choosing one
- asking the user to choose a stack when the product goal gives enough signal
- choosing architecture before clarifying the first workflow
- building a landing page when the user asked for an app or tool
- adding services, queues, state machines, or plugins before there is real complexity
- treating "AI-powered" as enough product definition
- hiding assumptions that shaped the implementation
