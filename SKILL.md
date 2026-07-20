---
name: project-architecture-workflow
description: Design or evolve an implementation-ready software project architecture with minimal unnecessary complexity. Use when Codex needs to start a new project, plan a substantial feature, assess module boundaries, choose a directory layout, define data or service interfaces, or turn requirements into an executable architecture plan. Do not use for a small contained code change or isolated bug fix.
---

# Project Architecture Workflow

Design only the architecture needed to deliver the next valuable, verifiable vertical slice. Do not add a layer, service, abstraction, framework, or document unless it resolves a stated constraint or a demonstrated risk.

## Classify The Work

Choose one mode before exploring:

- **Greenfield**: No meaningful implementation exists. Establish the smallest viable shape before scaffolding.
- **Existing project**: Verify the current architecture from executable code, entry points, build configuration, and tests. Treat prose documentation as secondary evidence.
- **Architecture change**: Identify the current contract, the target contract, migration boundary, and compatibility requirement before proposing a new shape.

Use `surgical-coding-debug` once a scoped architecture step becomes an implementation or debugging task.

## Establish The Decision Context

Capture only the facts that influence an architectural decision:

1. User outcome and acceptance criteria.
2. Non-goals and explicit exclusions.
3. Constraints: runtime, deployment, integrations, data ownership, privacy or security, performance, team conventions, and deadline.
4. The critical user or system flow that must work first.
5. The riskiest unknown that could invalidate the plan.

Separate facts, assumptions, and open decisions. Ask the user only for an assumption that cannot be discovered safely and would materially change the architecture.

## Inspect Minimal Evidence

For an existing project, start with the project manifest or build entry, application entry point, the relevant feature path, configuration, and nearest tests. Follow direct imports or runtime paths only as needed.

Do not map the whole repository, read every document, or infer an architecture from directory names. Stop exploration when the critical flow and its boundaries are understood.

## Make Architecture Decisions

Prefer the simplest structure that satisfies the known constraints.

- Keep modules aligned to domain responsibilities and ownership, not speculative reuse.
- Define one clear public contract per boundary: input, output, error behavior, and data ownership.
- Keep transport, domain behavior, persistence, and external integrations separable only when that separation creates a real testing, change, or ownership benefit.
- Use a single deployable unit by default. Introduce a service boundary only for an independent deployment, scaling, security, ownership, or reliability requirement.
- Introduce queues, events, plugins, generic repositories, dependency injection layers, caching, or migrations only when a concrete requirement justifies their operational cost.
- Preserve existing public contracts unless the task explicitly changes them. For a change, define the migration and compatibility window before implementation.

Record a decision only when reversing it would be costly or when alternatives have materially different consequences. State the chosen option, reason, and rejected alternative in a few lines; do not create ceremony for local choices.

## Produce An Implementation-Ready Shape

Describe the architecture in the smallest useful form:

1. Goal, non-goals, and critical flow.
2. Components or modules with their responsibilities and ownership.
3. Boundary contracts, data flow, and error path for the critical flow.
4. Storage and external integration responsibilities, if applicable.
5. Directory or package layout only when creating or reorganizing files.
6. Build order of three to six vertical slices, starting with the highest-risk integration.
7. Validation for each slice: unit, integration, end-to-end, build, or manual acceptance check.

Use a diagram only when it reveals a relationship that the concise component list cannot.

## Greenfield Execution

1. Implement or scaffold the smallest end-to-end path first.
2. Keep configuration, secrets, deployment, and observability requirements proportional to the requested scope.
3. Validate the first path before generalizing it into shared abstractions.
4. Add secondary flows only after the primary contract is proven.

## Existing-Project Execution

1. Preserve repository conventions unless they block the requested outcome.
2. Compare proposed boundaries with actual imports, runtime behavior, and tests before moving code.
3. Prefer additive and reversible transitions. Isolate breaking changes behind an adapter, versioned contract, or explicit migration when needed.
4. Do not reorganize broad directory trees merely for aesthetic consistency.

## Architecture Validation

Before implementation or handoff, verify that the proposed shape answers:

- Where does each input enter, and where is it validated?
- Which component owns each business rule and each piece of persistent data?
- How do expected failures propagate to the caller or operator?
- What is the first proof that the critical flow works?
- Which assumption remains the highest risk, and how will it be tested early?

If the design cannot answer one of these questions, resolve that gap before expanding scope.

## Communication

- Report the chosen shape, key tradeoffs, first vertical slice, and validation plan.
- Surface only decisions that need user approval: product behavior, meaningful cost, external state, or irreversible compatibility changes.
- Keep detailed reasoning internal unless the user asks for an architecture document or comparison.

## Avoid

- Full-repository archaeology before identifying the critical flow.
- Framework or cloud selection without a requirement it changes.
- Microservices or elaborate layers for a single-team, single-deployment need.
- Generic abstractions before a second real use case.
- Big-bang rewrites when a staged transition can preserve working behavior.
- Architecture diagrams or documents that do not guide an implementation decision.
