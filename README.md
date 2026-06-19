# Conceptual Model Pass

An agent skill that makes an AI explain the **language of a system before defending decisions** — naming and classifying each important term (what kind of thing it is, who owns it, its scope, lifecycle, relationships, and whether it's domain model or implementation) so you understand the ontology before you argue the details.

Works with any [`skills.sh`](https://skills.sh/)-compatible agent — Claude Code, Codex, Cursor, Gemini CLI, opencode, and others.

## The problem it solves

When you plan an architecture or compare design options with an AI agent, the conversation often goes in circles. The agent reaches for words like **policy**, **role**, **permission**, **workflow**, **integration**, **task**, **rule**, **config**, or **resource** without ever saying *what kind of thing* each one is. Is "policy" a stored record? A runtime evaluation? A reusable definition? A link that binds one thing to another? You can't tell — so you and the agent keep re-negotiating the same ambiguity.

The result is endless back-and-forth: you re-ask "but where does that live?", "is that per-user or global?", "is that the model, or just how we'd build it?" — and the design discussion stalls before it can start.

This skill forces the agent to settle the vocabulary first, so the rest of the conversation has solid ground to stand on.

## What it does

When invoked, the agent runs a **conceptual model pass** before recommending anything:

1. **Surface the important terms** — the ones that carry architectural, ownership, persistence, runtime, or permission weight (it ignores incidental words).
2. **Classify each term** into exactly one category: concept, definition/template, instance, assignment/binding, stored record, runtime state, protocol/interface, event/job/process, derived/effective result, or implementation choice.
3. **Separate domain model from implementation choice** — always saying which is which.
4. **Then** state the decision, and explain why it follows from the model.

For each important term it answers: what kind of thing it is, who owns it, its scope/cardinality (global, per-org, per-workspace, per-user, per-object, per-request, or on-demand), its lifecycle, how it relates to the other terms, and the implementation that realizes it.

It also refuses to use vague words like *policy / role / permission / workflow / integration / task / rule / configuration / resource* without first classifying what kind of thing each one is.

### The order matters

> **Language first, decision second, rationale third.**

The agent does not jump to an implementation recommendation before the ontology is clear.

## Install

```bash
npx skills add fabriqaai/conceptual-model-pass
```

Install globally (user-level, skip prompts):

```bash
npx skills add fabriqaai/conceptual-model-pass -g -y
```

Browse and discover more skills at [skills.sh](https://skills.sh/).

## How to use it

This skill is **explicit-invocation only**. It stays dormant during ordinary work and will not hijack normal planning, reviews, or explanations — you have to ask for it by name:

- "Do a **conceptual model pass** on this design"
- "Explain the **language of the system** first" / "**ontology-first**"
- "**Classify these terms** before we decide"

Once invoked, the agent stays in this mode for the rest of that design discussion until you move on.

## Decision template

When the agent makes a design decision under this skill, it presents it in a consistent shape:

```
Term:                 the name
Meaning:              what it is, plainly
Category:             concept / definition / instance / binding / record / runtime / protocol / event / derived / implementation
Scope / cardinality:  global / per-org / per-workspace / per-user / per-object / per-request / on-demand
Lifecycle:            definition / instance / assignment / runtime state / effective result
Relationships:        how it relates to the other terms
Implementation map:   the tool / library / service / custom mechanism realizing it
Concrete example:     one real instance
```

## License

[MIT](./LICENSE)
