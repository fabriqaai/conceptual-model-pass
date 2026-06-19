---
name: conceptual-model-pass
description: Explicit-invocation only. Use ONLY when the user literally asks for a "conceptual model pass", an ontology-first or system-language explanation, term/category classification, or names this skill directly. Do NOT auto-activate for ordinary planning, architecture, design, option comparison, reviews, or explanations — even though those overlap heavily. If the current request contains no explicit conceptual-model-pass trigger phrase, do not use this skill.
---

# Conceptual Model Pass

Explain the *language* of a system before arguing its details. When active, name and
classify each important term — what kind of thing it is, who owns it, its scope, its
lifecycle, how it relates to the others, and which parts are domain model vs.
implementation choice — so the user understands the system's ontology before any
decision is defended.

## When To Use This Skill

**Activation is explicit only.** Use this skill only when the current user request
contains a direct trigger, such as:

- "Do a conceptual model pass" / "conceptual model pass on this"
- "Explain the language of the system first" / "ontology-first" / "system-language pass"
- "Classify these terms" / "what kind of thing is each of these?"
- The user names this skill directly

Do **not** activate for ordinary planning, architecture, design, option comparison,
reviews, or explanations, even when they would clearly benefit. Overlap is not an
invitation. If no explicit trigger is present, work normally without this skill.

Once invoked, stay in this mode for the rest of that planning/design discussion until
the user moves on.

## The Pass

When active, before defending any decision:

1. **Surface the important terms.** Pull out the nouns that carry weight — the ones
   that affect architecture, ownership, persistence, runtime behavior, permissions, or
   the user's mental model. Ignore incidental words.
2. **Classify each term** into exactly one category (below).
3. **Separate domain model from implementation choice.** Always say which is which.
4. **Then** state the decision, and explain why it follows from the model.

Order matters: **language first, decision second, rationale third.** Do not jump to an
implementation recommendation before the ontology is clear.

## Term Categories

Classify each important term as exactly one of:

- **Concept** — an idea in the domain
- **Definition or template** — a reusable description of how instances should behave
- **Instance** — a concrete occurrence of a definition
- **Assignment / binding** — a link that applies one thing to another
- **Stored record** — something persisted in the system
- **Runtime state** — something that exists only while the system runs
- **Protocol / interface** — a contract for interaction
- **Event / job / process** — something that happens or runs
- **Derived / effective result** — something calculated from other things
- **Implementation choice** — a tool, library, service, or custom mechanism used to
  realize a concept

## Per-Term Explanation

For each important term, give:

1. **What kind of thing it is** — the category above
2. **Who or what owns it**
3. **Scope / cardinality** — global, per org, per workspace, per user, per object, per
   request, or calculated on demand
4. **Lifecycle** — definition, instance, assignment, runtime state, or effective result
5. **Relationships** — how it connects to the other terms
6. **Domain vs. implementation** — which parts are the model and which are
   implementation choices

## Decision Template

When making a design decision, present it in this structure:

```
Term:                 the name
Meaning:              what it is, plainly
Category:             from the term categories
Scope / cardinality:  global / per-org / per-workspace / per-user / per-object / per-request / on-demand
Lifecycle:            definition / instance / assignment / runtime state / effective result
Relationships:        how it relates to the other terms
Implementation map:   the tool / library / service / custom mechanism realizing it
Concrete example:     one real instance
```

## Banned Vague Terms

Do not use these without first classifying what kind of thing they are: *policy, role,
permission, workflow, integration, task, job, connector, rule, configuration,
resource.* Each one hides a category — name it.

## Guardrails

- **Decision-carrying terms only.** Classify terms that carry architectural,
  user-facing, persistence, runtime, ownership, permission, or workflow consequences.
  Do not produce an ontology table for every noun.
- **Compact table past a handful.** Prose per term is fine for three or four terms;
  switch to a table beyond that so the pass stays scannable.
- **Re-run only on new important terms.** Don't re-classify settled vocabulary every
  turn — extend the model when genuinely new terms appear.
- **Model before recommendation.** First the language, then the decision, then why the
  decision follows from the model.
