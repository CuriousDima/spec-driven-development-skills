---
name: create-feature-spec
description: Create a feature specification for the next roadmap phase in a spec-driven development project. Use when a user asks to write, create, draft, start, or initialize a feature spec from specs/roadmap.md, including creating a branch and producing specs/YYYY-MM-DD-feature-name/plan.md, requirements.md, and validation.md guided by specs/mission.md and specs/tech-stack.md.
license: MIT
metadata:
  author: Dima Timofeev
  version: "1.0"
---

# Create Feature Spec

Use this skill to start the next feature phase after the project specs exist. The goal is to turn the next roadmap phase into a small, implementable specification package. Do not implement the feature in this skill.

## Preconditions

- `specs/mission.md`, `specs/tech-stack.md`, and `specs/roadmap.md` should exist. If they are missing, stop and ask the user to create or complete the constitution first.
- Use this skill for feature-spec creation, not for constitution creation, constitution maintenance, implementation, or post-implementation re-planning.
- If a related feature spec directory already exists, read it before asking questions and confirm whether the user wants to revise that spec or create a new follow-on spec.

## Output

Create one dated feature directory:

```text
specs/
`-- YYYY-MM-DD-feature-name/
    |-- plan.md
    |-- requirements.md
    `-- validation.md
```

- The directory name should use the current local date and a concise kebab-case feature name.
- `plan.md` is a series of numbered task groups. Keep the groups small enough to guide implementation, but do not turn the spec into a line-by-line coding script.
- `requirements.md` captures scope, decisions, context, constraints, dependencies, out-of-scope work, and open questions.
- `validation.md` explains how to know the implementation succeeded and is ready to merge: functional checks, automated tests, manual QA, non-functional expectations, and merge blockers.

## Workflow

1. Orient in the project specs.
   - Read `specs/mission.md`, `specs/tech-stack.md`, and `specs/roadmap.md` first.
   - Read existing dated feature directories under `specs/` if they exist and are relevant to the next phase.
   - Read code, tests, README files, package manifests, or issue context only as needed to understand the next phase.
   - Identify roadmap order, existing spec coverage, implementation constraints, deployment or testing expectations, and guidance from the mission and tech stack.

2. Find the next roadmap phase.
   - Treat the next phase as the first roadmap phase that is not already covered by an existing completed feature spec or implementation evidence.
   - If roadmap status is ambiguous, choose the most likely next phase and ask the user to confirm it with the feature-spec questions.
   - Derive a provisional feature name from the next phase. Keep it short and implementation-facing.
   - Check the current git branch and worktree status. Do not discard or revert user changes.

3. Create the branch.
   - Create or switch to a dedicated branch for the feature spec before writing the spec files.
   - Use the repository's branch naming convention when one exists. Otherwise prefer `codex/YYYY-MM-DD-feature-name`.
   - If the desired branch already exists, inspect it and either switch to it when it matches this work or choose a clear suffix such as `-2`.
   - Keep existing uncommitted user changes intact. If branch creation is blocked by the current worktree, explain the blocker and ask how to proceed.

4. Ask before writing the spec.
   - Before creating the dated spec directory or spec files, use the AskUserQuestion tool. If the current environment exposes the same capability under a different name, use that user-input tool rather than plain chat. Ask concise questions grouped under these exact headings and wait for answers:
     - Requirements
     - Plan
     - Validation
   - Ground the questions in the next roadmap phase and the concrete feature spec to be written. Use `specs/mission.md` and `specs/tech-stack.md` as guidance for scope, constraints, and validation expectations.
   - Include confirmation of the selected roadmap phase and feature name when either is not obvious.
   - Do not create the feature spec directory or write spec files until the user has answered all three groups.

5. Draft the feature spec.
   - Create the dated feature directory and write `requirements.md`, `plan.md`, and `validation.md` in one pass.
   - In `requirements.md`, separate confirmed decisions from assumptions and open questions.
   - In `plan.md`, use numbered task groups that flow from foundation to user-visible behavior to polish and integration. Each group should have a clear purpose and expected outcome.
   - In `validation.md`, include merge-readiness checks that match the project's testing and deployment reality. If the project has no test system yet, state the manual checks and any test-enabling work needed.
   - Defer detailed implementation code, acceptance-test code, and post-feature roadmap changes unless the user explicitly asks for them.

6. Check consistency.
   - Ensure the feature scope advances the selected roadmap phase without expanding beyond it.
   - Ensure requirements reflect mission priorities and non-goals.
   - Ensure the plan is feasible under `specs/tech-stack.md`.
   - Ensure validation can prove the feature is complete enough to merge.
   - Revise all affected spec files together when feedback changes scope, order, or validation expectations.

7. Close with next steps.
   - Summarize the branch and files created.
   - Call out assumptions, unresolved questions, and notable risks.
   - Suggest the next action: review the spec, validate it, or begin implementation.

## Suggested File Shape

Use these as compact starting points. Adjust headings to match the project language and the answers the user provided.

For `requirements.md`:

```markdown
# Requirements

## Context
## Scope
## Decisions
## Out of Scope
## Assumptions and Open Questions
```

For `plan.md`:

```markdown
# Plan

1. <Task group>
   - ...

2. <Task group>
   - ...
```

For `validation.md`:

```markdown
# Validation

## Success Criteria
## Automated Checks
## Manual Checks
## Merge Readiness
```
