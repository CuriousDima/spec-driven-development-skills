# Spec-Driven Development

Skills for spec-driven development.

## What Is Spec-Driven Development?

Specification-driven development (SDD) is a software development approach in which specifications guide the design, validation, and implementation of software. It is a form of documentation-driven development.

## Spec-Driven Development Workflow

At a high level, SDD moves through a repeating cycle: define the constitution (once), run each feature through specification, validation, and implementation, then re-plan before the next feature phase.

We create a constitution for a new or existing project **exactly once**. The `create-constitution` skill helps with this.
Once the constitution is in place, we loop over the workflow:

1. Ask the `create-feature-spec` skill to write a feature spec.
2. Review the feature spec and iterate with the agent until you are satisfied.
3. `/clear` the context and prompt the agent: `Implement the remaining task groups.` The first implementation might not be exactly what we wanted, so it is important to review what the agent implemented and ask it to make adjustments, if needed.
   - During this process, remember to ask the agent to update `plan.md` as well. This is important for keeping the specification consistent.
   - During the review process, we might add something or refactor part of the implementation ourselves. This is totally fine, but the specs and related documents can go out of sync. Because of that, it is important to ask the agent to incorporate any changes we made manually. A good strategy is to first commit whatever the agent has implemented. After making our own changes, we can ask for something like this: `Update the specs to capture the uncommitted changes I made manually.`
   - If the feature plan is too long, it is fine to ask the agent to implement only part of the plan.
4. Ask the agent to mark the phase as complete and move on: `Mark the current specs/roadmap.md phase as complete. Commit this work, switch to main, merge this branch, and then delete it.`

### Constitution

The workflow starts by creating the project constitution; the dedicated section below covers its contents and role.

### Feature Phase

Once the constitution is written, we work on each feature individually. We walk through the same process:

*specification → validation → implementation*

The validation step checks whether the specification is clear, internally consistent, and grounded in the constitution before implementation begins.

### Re-planning Phase

Between features, we enter a re-planning phase: revising the constitution, updating the roadmap, and improving the process itself.

## Included Skills

- `create-constitution`: creates the initial project constitution in `specs/mission.md`, `specs/tech-stack.md`, and `specs/roadmap.md`.
- `create-feature-spec`: finds the next roadmap phase, creates a feature branch, and drafts a dated feature spec directory with `requirements.md`, `plan.md`, and `validation.md`.
