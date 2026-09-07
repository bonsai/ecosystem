# bonsai/ecosystem.md

Bonsai ecosystem architecture.

## Design principle

Bonsai is a **loosely coupled semantic ecosystem**. The system is divided into three primary layers:

```text
┌──────────────────────────────────────────┐
│ DEFINITIONS / ONTOLOGY                   │
│ What things mean                         │
│ concepts · entities · relations · rules │
└────────────────────┬─────────────────────┘
                     │ semantic contract
┌────────────────────▼─────────────────────┐
│ TOOLS                                    │
│ What can be done                         │
│ APIs · CLIs · libraries · data systems  │
└────────────────────┬─────────────────────┘
                     │ capabilities
┌────────────────────▼─────────────────────┐
│ AGENTS                                   │
│ Who decides / coordinates / acts         │
│ intent · plan · policy · execution       │
└──────────────────────────────────────────┘
```

The layers communicate through **stable contracts**, not direct implementation dependencies.

## 1. Definitions / Ontology layer

The ontology layer defines vocabulary and meaning. It must not depend on a particular runtime, CLI, model, or workflow engine.

| Repository | Responsibility | Relation |
|---|---|---|
| `bonsai/intent` | Intent, Goal, Actor, Context, Constraint, Plan, Outcome, Evidence | `defines` |
| `bonsai/world-ontology` | World, domain, object, context vocabulary | `defines` / `provides` |
| `bonsai/wiki` | Human-curated concepts and knowledge | `provides` |
| `bonsai/ecosystem.md` | Ecosystem relationship vocabulary and map | `defines` |

### Ontology rule

```text
Ontology MUST NOT know:
  - which LLM is used
  - which CLI executes an action
  - which GitHub Workflow runs it
  - where runtime state is stored
```

Ontology describes **meaning**, not implementation.

## 2. Tools / Capability layer

Tools are capabilities that can be invoked by agents. A tool should have a clear input/output contract and should not contain business intent.

| Repository | Responsibility | Relation |
|---|---|---|
| `bonsai/repos` | Repository observation and repository-state data | `observes` / `provides` |
| `bonsai/ds-agent` | Data analysis and BQML capabilities | `analyzes` / `provides` |
| `bonsai/aw.tui` | Operational inspection and workflow interface | `provides` / `observes` |
| GitHub Actions / AW | Workflow execution capability | `executes` |

Tools answer:

> **What operation is available?**

They do not answer:

> **Why should we perform it?**

That decision belongs to the intent/agent layer.

## 3. Agent layer

Agents consume ontology and tools. Agents are responsible for interpreting intent, planning, selecting capabilities, coordinating work, and evaluating outcomes.

| Repository | Responsibility | Relation |
|---|---|---|
| `bonsai/think` | Reasoning and planning methods | `plans` |
| `bonsai/yaml-as-agent` | Declarative agent representation / compilation boundary | `generates` |
| `bonsai/agent` | Agent model and organizational/execution abstraction | `defines` / `coordinates` |
| `bonsai/aw` | Agentic Workflow generation and execution | `generates` / `executes` |
| `bonsai/company` | Organization / collective-agent context | `organizes` |

Agents answer:

> **What should be done, in what order, using which capabilities, and how do we know it succeeded?**

## 4. Domain agents

Domain-specific repositories should specialize the agent layer without modifying the foundational ontology.

```text
              foundational ontology
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
          intent          world-ontology
             │                   │
             └─────────┬─────────┘
                       ▼
                  domain agent
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
          tools      plans     policies
```

Examples include domain-oriented agent repositories such as `bonsai/quiz-agents`, `bonsai/bon-anima`, and `bonsai/mala-agent`.

A domain agent **specializes** the ontology; it does not fork or redefine the foundational meaning of `Intent`, `Goal`, `Actor`, etc.

## 5. Loose-coupling contract

Dependencies should point through contracts:

```text
             DEFINITIONS
             ontology
                 │
                 │ semantic contract
                 ▼
              AGENTS
                 │
                 │ capability contract
                 ▼
               TOOLS
                 │
                 │ evidence / result
                 ▼
             DEFINITIONS
```

The important rule is:

```text
Ontology ← Agent → Tool
```

rather than:

```text
Ontology → Tool implementation → Agent implementation
```

This allows any layer to evolve independently.

## 6. Canonical contracts

### Intent contract

`bonsai/intent` defines the semantic contract:

```yaml
intent:
  actor: Actor
  goal: Goal
  object: Object
  context: Context
  constraints: Constraint[]
  plan: Plan
  actions: Action[]
  expected_outcomes: Outcome[]
  evidence: Evidence[]
```

### Tool contract

Tools expose capabilities independently of the agent that calls them:

```yaml
tool:
  id: repository.observe
  input: Repository
  output: RepositoryObservation
  side_effects: read-only
```

### Agent contract

Agents consume intents and capabilities:

```yaml
agent:
  id: repository-observer
  accepts: Intent
  uses:
    - repository.observe
  produces:
    - Evidence
    - Outcome
```

## 7. repo2agent

`repo2agent` is a transformation across the boundaries:

```text
Repository
    │
    ▼
Repository facts
    │
    ▼
Ontology / Definitions
    │
    ▼
Intent IR
    │
    ▼
Agent definition
    │
    ▼
Tool selection
    │
    ▼
AW Workflow
    │
    ▼
Evidence / Outcome
```

`bonsai/aw` should act as the **Agent Midwife**: it turns approved semantic intent and agent definitions into executable workflow candidates. It should not invent the underlying business intent.

## 8. Closed-loop organization

```text
observe
   ↓
understand
   ↓
intent
   ↓
plan
   ↓
agent
   ↓
tool
   ↓
execute
   ↓
evidence
   ↓
evaluate
   ↓
re-intent
```

The loop is closed through evidence and outcomes, while the ontology remains stable.

## 9. Boundary rules

### Ontology

- Defines meaning.
- Owns canonical vocabulary.
- Is implementation-independent.
- Does not execute actions.
- Does not select an LLM.

### Tools

- Provide capabilities.
- Have explicit input/output contracts.
- May read or modify external systems.
- Do not own business intent.
- Should be replaceable.

### Agents

- Interpret and pursue intents.
- Select and coordinate tools.
- Create or follow plans.
- Evaluate evidence and outcomes.
- May be replaced without changing the ontology.

### Workflow runtime

- Executes approved plans.
- Provides operational guarantees.
- Emits execution evidence.
- Is not the semantic source of truth.

## 10. Ecosystem relationship vocabulary

| Relation | Meaning |
|---|---|
| `defines` | Owns a canonical definition or semantic contract |
| `provides` | Provides a capability, data, vocabulary, or artifact |
| `consumes` | Uses another layer's contract or output |
| `observes` | Reads external state |
| `analyzes` | Derives metrics, classifications, or inference |
| `specializes` | Extends a foundational definition for a domain |
| `plans` | Converts intent into strategy |
| `generates` | Creates an agent or workflow definition |
| `executes` | Performs an operation or workflow |
| `produces` | Emits an artifact, evidence, or outcome |
| `verifies` | Validates a result against intent or constraints |
| `coordinates` | Orchestrates agents or capabilities |
| `organizes` | Defines relationships among agents |

## 11. Repository map

```text
DEFINITIONS / ONTOLOGY
├── bonsai/intent
├── bonsai/world-ontology
├── bonsai/wiki
└── bonsai/ecosystem.md

TOOLS / CAPABILITIES
├── bonsai/repos
├── bonsai/ds-agent
├── bonsai/aw.tui
└── GitHub Actions / AW runtime

AGENTS / ORGANIZATION
├── bonsai/think
├── bonsai/yaml-as-agent
├── bonsai/agent
├── bonsai/aw
├── bonsai/company
└── domain agents
    ├── bonsai/quiz-agents
    ├── bonsai/bon-anima
    └── bonsai/mala-agent
```

## Core principle

> **Definitions describe the world. Tools provide capabilities. Agents choose and coordinate capabilities to realize intent.**

Keeping these three concerns separate is the foundation of Bonsai's loose coupling and allows ontology, tooling, agents, models, and workflow runtimes to evolve independently.
