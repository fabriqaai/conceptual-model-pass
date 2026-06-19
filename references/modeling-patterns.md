# Modeling Patterns

Use these lightweight patterns when a conceptual model pass needs more structure.
Load only the sections relevant to the user's task.

## Type / Instance

Use when a term confuses a reusable kind of thing with one concrete occurrence.

- **Definition or type**: reusable shape, template, schema, or rule set.
- **Instance**: one concrete occurrence created from the definition.
- **Common split**: WorkflowDefinition vs WorkflowRun, PolicyDefinition vs
  PolicyEvaluation, ConnectorType vs ConnectionInstance.

## Definition / Assignment / Effective Result

Use when a reusable rule or configuration is applied to a target and produces a
calculated outcome.

- **Definition**: what could apply.
- **Assignment / binding**: where it applies.
- **Evaluation**: runtime process that checks it.
- **Effective result**: calculated answer after all definitions and assignments are
  considered.

Example: permission policy -> policy assignment -> permission check -> effective
capability.

## Actor / Role / Capability / Permission

Use when access-control language is overloaded.

- **Actor**: person, organization, service, or agent taking action.
- **Role**: named bundle, label, or relationship; never assume it is itself a
  permission.
- **Capability**: action the actor can perform in the domain.
- **Permission**: granted or denied capability in a context.
- **Policy/rule**: logic that decides whether a permission exists or applies.

Questions to answer: who can do what, to which resource, under which context, and
because of which assignment or rule?

## Policy / Evaluation / Decision

Use when "policy" is vague.

- **Policy definition**: stored reusable rule.
- **Policy assignment**: binding between policy and target.
- **Policy evaluation**: runtime act of checking.
- **Policy decision**: allow, deny, require approval, flag, score, or explain.
- **Policy evidence**: inputs used to make the decision.

Avoid saying "the policy does X" until these are separated.

## Workflow Definition / Run / State

Use when "workflow" hides design-time and runtime meanings.

- **Workflow definition**: reusable process template.
- **Workflow run**: one execution.
- **Step definition**: reusable step in the template.
- **Step instance**: one runtime occurrence.
- **State**: current status of a run or step.
- **Transition**: allowed movement between states.
- **Event**: fact that something happened.

For lifecycle-heavy systems, prefer an event map over a term table.

## Event Modeling

Use when the user is planning behavior over time.

Adopt an event-storming mindset when behavior, lifecycle, or workflow sequence is
the confusing part. Start from domain events, then work backward to commands and
actors, and forward to policies, reactions, aggregates, state changes, and read
models.

Map:

```text
Actor -> Command -> Event -> State change -> Policy/Rule -> Read model
```

- **Actor**: initiates intent.
- **Command**: request to change something.
- **Event**: fact emitted after something happens.
- **State change**: what becomes true.
- **Policy/rule**: condition triggered by the event or command.
- **Read model**: derived view used for decisions or UI.

Keep commands imperative ("Approve invoice") and events past-tense ("Invoice
approved").

## Integration Provider / Connection / Sync Job

Use when "integration" or "connector" is vague.

- **Provider**: external product or protocol, such as Slack or OAuth.
- **Connector definition**: reusable implementation for that provider.
- **Connection instance**: one configured link for an org/workspace/user.
- **Credential**: secret or token used by the connection.
- **Webhook subscription**: inbound event binding.
- **Sync job**: runtime process that moves or reconciles data.
- **External resource mapping**: link between local and remote identifiers.

## Resource / Identifier / Representation

Use when "resource" hides API, storage, and domain meanings.

- **Domain object**: conceptual thing users care about.
- **Stored record**: persisted representation.
- **Identifier**: stable handle.
- **API resource**: interface representation exposed over a protocol.
- **View model**: derived representation for UI or reads.

Do not let API shape silently become the domain model.

## Bounded Context / Ubiquitous Language

Use when the same term can mean different things to different teams or subsystems.

- Name the bounded context.
- Define the term only inside that boundary.
- Flag same-word/different-meaning collisions.
- Map translations between contexts rather than forcing one universal meaning.

Example: "Customer" in billing may mean payer; in support it may mean contacted
account; in product analytics it may mean workspace.

## Review-Gated DDD Workflow

Use when the user wants DDD, domain modeling, event modeling, or architecture from
requirements.

Progression:

```text
Requirements -> Ubiquitous language -> Event model -> Bounded contexts -> Aggregates -> Technical architecture
```

Guidance:

- Treat ubiquitous language and event modeling as strong LLM-assisted discovery
  steps.
- Ask clarifying questions when terms are generic, artificial, or ambiguous.
- Use event modeling to uncover missing business flows, edge cases, and
  operational events.
- Validate bounded contexts against practical coupling, team boundaries, and
  operational overhead. Challenge contexts that are too broad and contexts that
  are too granular.
- Do not finalize aggregates or technical architecture until earlier artifacts are
  reviewed; errors accumulate across stages.
- Use the final architecture mapping to explain how ports, adapters, APIs,
  repositories, infrastructure, and integrations support the domain model.
