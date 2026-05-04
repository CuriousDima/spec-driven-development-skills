---
name: create-constitution
description: Start a spec-driven development project constitution by collaboratively drafting specs/mission.md, specs/tech-stack.md, and specs/roadmap.md from stakeholder input and, for existing projects, current codebase reality. Use when a user asks to create, initialize, adopt, or bootstrap an initial project constitution, mission, tech stack, or roadmap for spec-driven development, including greenfield projects and existing projects without a constitution.
license: MIT
metadata:
  author: dima
  version: "1.0"
---

# Create Constitution

Use this skill to create or adopt the initial project-level constitution that guides later feature specs. Do not invent the constitution alone: derive it from stakeholder input, ask the user for missing decisions, and keep the resulting documents consistent with one another.

## Adoption Modes

- Greenfield project: use stakeholder input to define the target mission, initial stack, and first small roadmap phases before implementation begins. Let the user provide that input from a file of their choice, by answering the question groups directly, or both.
- Existing project without a constitution: inspect the current codebase and docs to capture the project's de facto mission, technical reality, shipped behavior, and constraints, then ask the user for 1-2 planned features or outcomes to anchor the roadmap. The constitution should describe what exists, what must be preserved, and where the project should evolve next.

Do not use this skill for re-planning or constitution maintenance between feature phases. Hand that work to the dedicated constitution-update skill when available.

## Output

Create or complete this initial structure:

```text
specs/
├── mission.md
├── tech-stack.md
└── roadmap.md
```

- `mission.md`: the project's why, vision, audience, user value, scope boundaries, priorities, non-goals, and success signals.
- `tech-stack.md`: the engineering team's shared understanding of application architecture, development strategy, deployment strategy, constraints, trade-offs, data, security, and operations.
- `roadmap.md`: a living sequence of very small phases. Each phase should be suitable for its own feature-spec process: specification, validation, and implementation.

## Workflow

1. Orient in the project.
   - Read stakeholder input first: the user's prompt, `README.md`, product briefs, requirements docs, existing specs, issue descriptions, or other files the user names.
   - For a greenfield project, do not assume stakeholder input must live in `README.md`. If the user has not named a source, explicitly give them the option to point to any requirements file or provide the initial details as answers to the questions.
   - For an existing project, also inspect code and operational evidence: package manifests, framework conventions, deployment configs, CI, tests, database or schema files, API boundaries, dependency choices, and user-facing entry points.
   - If `specs/` or any constitution files already exist, read them before writing. If the user is asking for re-planning, post-feature updates, or ongoing constitution maintenance, stop and defer to the dedicated constitution-update skill when available. Otherwise, treat existing files as partial initial constitution context to complete.
   - Identify assumptions, contradictions, missing stakeholder decisions, de facto choices already made by the codebase, and decisions that affect more than one constitution file.

2. Ask before writing.
   - Before creating or modifying constitution files, ask the user questions and wait for answers covering these three groups:
     - Mission: vision, primary users, user value, scope boundaries, priorities, non-goals, and success criteria.
     - Tech stack: preferred languages, frameworks, services, deployment targets, constraints, team capabilities, compliance, security, data, and operational trade-offs.
     - Roadmap: first usable milestone, 1-2 planned features or outcomes, phase order, smallest useful slices, risks, dependencies, and what should be deferred.
   - For an existing project, include questions about current users, behavior that must not regress, known technical debt, migration appetite, production constraints, and whether the roadmap should favor stabilization, planned feature work, or architecture cleanup first. Ask for 1-2 planned features or outcomes even if the codebase already reveals plenty of current-state detail; those anchors prevent the roadmap from becoming only a cleanup inventory.
   - Ask concise grouped questions. Ground them in the source material you found, and offer defaults when stakeholder input supports those defaults.
   - For a greenfield project, frame the questions so the user can either answer directly or say which file contains the answer. Treat both paths as valid inputs.
   - Do not write to disk until the user has answered these three groups, even when the existing stakeholder input looks sufficient.

3. Draft the constitution.
   - Create `specs/` if it does not exist.
   - Write or complete `mission.md`, `tech-stack.md`, and `roadmap.md` in one pass.
   - Use direct, decision-oriented language. Mark uncertain items as assumptions or open questions instead of presenting them as settled facts.
   - For an existing project, separate current state from intended direction when they differ. Do not disguise accidental architecture or legacy constraints as intentional strategy.
   - For an existing project roadmap, use the requested 1-2 planned features or outcomes as near-term anchors, then place stabilization, cleanup, and enabling work around them in small phases.
   - Keep the roadmap high-level but actionable. Prefer small phases that produce one coherent capability or foundation, rather than broad epics.
   - Defer detailed feature requirements, acceptance criteria, and implementation tasks to later feature specs.

4. Maintain consistency.
   - Check that mission priorities shape roadmap order and tech-stack choices.
   - Check that roadmap phases are feasible under the selected tech stack and project constraints.
   - During initial drafting feedback, revise every affected constitution file instead of patching only the sentence the user mentioned.
   - After the initial constitution exists, encourage the user to use the dedicated constitution-update skill for future constitution changes, because those changes often have related impacts across multiple files.

5. Close with next steps.
   - Summarize which files were created or completed.
   - Call out important assumptions and open questions.
   - Suggest the next feature-spec phase from the roadmap.

## Suggested File Shape

Keep the constitution lightweight. Use these as example shapes, not mandatory questionnaires. Omit empty sections, combine related ideas, and choose headings that fit the project language.

For `mission.md`, prefer a short narrative plus the few stakeholder sections that matter:

```markdown
# Mission

Briefly explain why the project exists and what kind of experience it should create.

## Who We Serve
## Scope
```

For `tech-stack.md`, document actual decisions and constraints. Pick a compact shape for simple projects, an expanded shape for larger or constraint-heavy projects, or blend the two. Use headings only for stack areas that exist or are clearly planned.

Compact shape:

```markdown
# Tech Stack

## Frontend & Framework
## Styling
## Database
## Testing
## Auth
## Running the App
## Deployment
```

Expanded shape:

```markdown
# Tech Stack

## Product and Engineering Constraints
## Application Platform
## Languages and Frameworks
## Data and Storage
## APIs and Integrations
## Development Workflow
## Testing Strategy
## Deployment and Operations
## Security and Compliance
## Trade-offs and Assumptions
```

For `roadmap.md`, keep phases small and shippable. Derive phase names and order from stakeholder input, existing project state, planned features, and technical constraints. Do not prescribe universal phases. Each phase should be understandable as a future feature-spec candidate.

```markdown
# Roadmap

Each phase is a small, shippable increment. Features within a phase are added one at a time.

## Phase 0 — <Smallest useful foundation or current baseline>
- ...

## Phase 1 — <Next planned capability or enabling slice>
- ...
```
