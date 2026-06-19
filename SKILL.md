---
name: conceptual-model-pass
description: Use for ontology-first planning, domain modeling, event modeling, ubiquitous-language clarification, architecture/design discussions with ambiguous terms, permissions/workflows/integrations/data-model decisions, or when the user asks for a conceptual model pass, system-language pass, term classification, or "explain the language first." Clarifies key terms, bounded context, ownership, lifecycle, relationships, domain-vs-implementation choices, and competency questions before recommending a decision. Use compact tables only when they make the model easier to scan; do not use for trivial explanations with no decision-carrying vocabulary.
---

# Conceptual Model Pass

Explain the language of a system before arguing its details. Use the pass to
establish a shared conceptual model for planning, architecture, product design,
domain modeling, event modeling, and ubiquitous-language work.

The goal is not to create a formal ontology unless the user asks for one. The goal
is to make the important terms precise enough that design decisions can follow
from the model instead of from vague words.

## Core Rule

Language first, model second, decision third.

Before defending an implementation, clarify what the important terms mean, where
their meanings apply, how they change over time, and which parts belong to the
domain model versus the implementation.

## Mindset Cues

When these phrases appear, adopt the corresponding mindset:

- **Language first** / **system language**: define terms before deciding.
- **Ubiquitous language**: build shared domain vocabulary that can appear in
  conversation, docs, and code.
- **Bounded context**: identify where each term meaning is valid and where it may
  differ.
- **Domain model**: separate business concepts from technical mechanisms.
- **Domain event** / **event storming** / **event modeling**: model behavior over
  time through actors, commands, events, policies, and state changes.
- **Event storming mindset**: when behavior or lifecycle matters, start from what
  happened in the domain, then work backward to commands, actors, policies, and
  aggregates.
- **Aggregate** / **invariant**: look for consistency boundaries and rules that must
  hold together.
- **Competency questions**: test the model with questions it must answer.
- **Policy, role, permission, workflow, integration, resource**: split vague words
  into concrete subterms before recommending implementation.

## Workflow

1. **Name the modeling purpose.** State what the pass is trying to clarify:
   planning, architecture, workflow, permissions, integration, data model,
   explanation, glossary, or event/lifecycle behavior.
2. **Set the boundary.** Identify the bounded context: where this vocabulary is
   valid, who uses it, and where the same word may mean something else.
3. **Surface decision-carrying terms.** Pull out only terms that affect ownership,
   persistence, runtime behavior, permissions, events, workflows, architecture, or
   the user's mental model.
4. **Split overloaded words.** If one word hides multiple meanings, split it into
   concrete subterms before classifying. For example, split "policy" into
   policy definition, policy assignment, policy evaluation, and policy result when
   those are distinct things.
5. **Classify each term.** Assign one primary category and optional facets. If a
   term genuinely fits several categories, rename or split it until each subterm is
   clear.
6. **Map lifecycle and events when relevant.** For stateful or workflow-heavy
   systems, show actor -> command -> event -> state change -> rule/policy ->
   read model or result.
7. **Separate domain model from implementation.** Say which terms are conceptual
   domain language and which are tools, libraries, services, records, APIs, or
   storage choices.
8. **Add review gates.** Treat the pass as a collaborative sparring partner, not
   full automation. Ask the user or domain expert to confirm glossary terms,
   event flows, and context boundaries before relying on them for aggregates or
   technical architecture.
9. **Check with competency questions.** Ask or infer 2-5 questions the model must
   answer, then verify whether the model answers them.
10. **Then recommend.** State the decision and explain why it follows from the
   clarified model.

## Output Modes

Choose the smallest clear representation:

- **Micro pass**: 3-6 key terms, plain-language meanings, decision.
- **Standard pass**: compact term map, relationships, decision, rationale.
- **Event-model pass**: actors, commands, events, state changes, policies/rules,
  read models, open questions.
- **Event-storming pass**: domain events first, then commands, actors, policies,
  aggregates, read models, and unclear temporal boundaries.
- **Glossary pass**: shared vocabulary for a bounded context.
- **Deep pass**: bounded contexts, term collisions, competency questions, pattern
  mapping, unresolved ambiguities.
- **DDD sparring pass**: ubiquitous language -> event model -> bounded contexts ->
  reviewed aggregates -> technical architecture mapping.

Tables are optional. Use prose for a few terms, a compact table for many related
terms, an event map for lifecycle-heavy systems, and a glossary when the main
problem is shared vocabulary.

## Categories

Classify decision-carrying terms with a primary category:

- **Concept** - an idea in the domain
- **Actor / party** - a person, organization, system, or agent that does something
- **Definition or template** - a reusable description of how instances should
  behave
- **Instance** - a concrete occurrence of a definition
- **Assignment / binding** - a link that applies one thing to another
- **Stored record** - something persisted in the system
- **Runtime state** - something that exists only while the system runs
- **State / transition** - a named condition or allowed change between conditions
- **Capability / permission** - something an actor may do or be allowed to do
- **Rule / constraint** - a condition that limits or shapes behavior
- **Protocol / interface** - a contract for interaction
- **Event / command / job / process** - something requested, happening, emitted, or
  running
- **Derived / effective result** - something calculated from other things
- **Context / boundary** - the scope where a model or term meaning applies
- **Implementation choice** - a tool, library, service, API, database, framework, or
  custom mechanism used to realize a concept

## Per-Term Fields

For each important term, include only the fields needed for clarity:

- **Meaning** - what it is, plainly
- **Primary category** - from the categories above
- **Owner** - who or what controls it
- **Scope / cardinality** - global, per org, per workspace, per user, per object,
  per request, or calculated on demand
- **Lifecycle** - definition, instance, assignment, runtime state, event/process,
  transition, or effective result
- **Relationships** - how it connects to the other terms
- **Context / boundary** - where this meaning is valid
- **Implementation map** - the concrete mechanism, if relevant
- **Example** - one real instance

## Competency Questions

Use competency questions to test whether the conceptual model is useful. Good
questions include:

- Who owns this term?
- Where does it live?
- Is it a definition, instance, assignment, runtime state, event, or calculated
  result?
- What event creates, updates, assigns, evaluates, completes, or deletes it?
- Can another bounded context use the same word differently?
- What breaks if its scope, owner, or lifecycle changes?
- Is this part of the domain model or just how we implement it?

## DDD Sparring Pass

When the user asks for domain-driven design, domain modeling, event modeling, or
ubiquitous language, use this sequence:

1. Establish a ubiquitous language and ask clarifying questions for generic,
   artificial, or overloaded terms.
2. Run an event-modeling or event-storming pass when behavior over time matters.
   Start with domain events, then connect actors, commands, policies/rules,
   aggregates, read models, and state changes.
3. Identify bounded contexts, but check both directions: contexts may be too large
   or too granular.
4. Propose aggregates/entities/invariants only after the language, events, and
   contexts have been reviewed.
5. Map to technical architecture last, and explain how each technical component
   supports the domain model.

Do not present later-stage outputs as final if earlier vocabulary or context
boundaries are uncertain. Small mistakes in the glossary or event flow can
compound into poor aggregates and shallow architecture.

## Vague Terms To Split

Do not use these terms as if they are self-explanatory: policy, role, permission,
workflow, integration, task, job, connector, rule, configuration, resource, state,
event, command, model, context.

When one appears, either define it precisely or split it into more concrete terms.

## References

For deeper passes, many ambiguous terms, or requests involving permissions,
workflows, integrations, event modeling, or domain modeling, read
`references/modeling-patterns.md` and reuse the relevant patterns.

## Guardrails

- Classify only decision-carrying terms; do not create an ontology for every noun.
- Prefer a short pass unless the user asks for depth or the ambiguity is blocking a
  decision.
- Do not force tables. Choose the representation that best fits the modeling
  problem.
- Re-run only for new important terms; extend the model instead of reclassifying
  settled vocabulary every turn.
- Keep the final recommendation tied to the model: first language, then decision,
  then rationale.
- Flag missing requirements, edge cases, operational events, and practical coupling
  instead of smoothing them over.
