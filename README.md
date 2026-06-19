# Conceptual Model Pass

An agent skill for making AI explain the **language of a system before defending
decisions**.

Use it for ontology-first planning, domain modeling, event modeling,
ubiquitous-language clarification, architecture/design discussions, permissions,
workflows, integrations, and data-model decisions where vague terms keep making the
conversation fuzzy.

Works with any [`skills.sh`](https://skills.sh/)-compatible agent: Claude Code,
Codex, Cursor, Gemini CLI, opencode, and others.

## The problem it solves

AI agents often jump into implementation recommendations before the vocabulary is
settled. Words like **policy**, **role**, **permission**, **workflow**,
**integration**, **task**, **rule**, **config**, **event**, or **resource** can hide
several different concepts.

For example, "policy" might mean a reusable policy definition, a policy assignment,
a runtime policy evaluation, or the effective result of that evaluation. Those are
different things with different owners, lifecycles, storage needs, and failure
modes.

This skill forces the agent to settle the language first so planning can happen on
solid ground.

## What it does

When invoked, the agent runs a **conceptual model pass** before recommending
anything:

1. Names the modeling purpose and bounded context.
2. Surfaces only the terms that carry architectural, ownership, lifecycle,
   persistence, runtime, permission, workflow, or product meaning.
3. Splits overloaded words into concrete subterms.
4. Classifies each term by what kind of thing it is.
5. Separates domain model from implementation choice.
6. Uses competency questions to check whether the model answers the real planning
   question.
7. Adds review gates so glossary terms, event flows, and bounded contexts are
   confirmed before later architecture decisions.
8. Then states the decision and explains why it follows from the model.

The order matters:

> **Language first, model second, decision third.**

## Not just tables

Tables are optional. The skill chooses the smallest clear representation:

- **Micro pass** for a few important terms.
- **Compact table** when many related terms need scanning.
- **Glossary** when the goal is shared ubiquitous language.
- **Event map** when the system is lifecycle-heavy.
- **Deep pass** when bounded contexts, term collisions, or competency questions are
  central.

For event modeling, the agent may use this shape:

```text
Actor -> Command -> Event -> State change -> Policy/Rule -> Read model
```

For DDD-style work, the skill follows a review-gated progression:

```text
Ubiquitous language -> Event model -> Bounded contexts -> Aggregates -> Technical architecture
```

It treats the agent as a collaborative sparring partner, not a full automation
engine. Early glossary and event-modeling work is usually where the agent helps
most; aggregates and technical architecture should be reviewed carefully because
small early mistakes can compound.

## Install

```bash
npx skills add fabriqaai/conceptual-model-pass
```

Install directly from GitHub:

```bash
npx skills add https://github.com/fabriqaai/conceptual-model-pass --skill conceptual-model-pass
```

Install globally and skip prompts:

```bash
npx skills add fabriqaai/conceptual-model-pass -g -y
```

View the skill page on
[skills.sh](https://www.skills.sh/fabriqaai/conceptual-model-pass/conceptual-model-pass).

## How to use it

Ask directly:

- "Do a **conceptual model pass** on this design."
- "Explain the **language of the system** first."
- "Use **ontology-first planning**."
- "Clarify the **ubiquitous language** before we decide."
- "Do an **event modeling** pass for this workflow."
- "**Classify these terms** before recommending an implementation."

It can also be used when a planning or architecture request contains ambiguous
decision-carrying vocabulary such as policy, workflow, integration, role,
permission, event, state, connector, rule, configuration, or resource.

## Useful mindset cues

Use these phrases when you want the agent to enter the right modeling posture:

- **Language first**
- **Ubiquitous language**
- **Bounded context**
- **Domain model**
- **Domain event**
- **Event storming** / **event modeling**
- **Event storming mindset**
- **Domain-vs-implementation**
- **Aggregate** / **invariant**
- **Competency questions**
- **Split overloaded terms**

## License

[MIT](./LICENSE)
