# bonsai/ecosystem.md

Bonsai repository ecosystem map.

## Purpose

Bonsai is organized as a network of repositories with explicit semantic responsibilities. This repository is the **ecosystem index**: it describes how repositories provide, consume, observe, analyze, generate, execute, and verify one another.

## Core loop

```text
observe → understand → intend → plan → generate → execute → evidence → evaluate → re-intend
```

## Relationship vocabulary

| Relation | Meaning |
|---|---|
| `defines` | Owns the canonical semantic model or contract |
| `provides` | Produces data, ontology, specification, or capability |
| `consumes` | Uses another repository's contract or output |
| `observes` | Reads or monitors external state |
| `analyzes` | Derives metrics, classifications, or inference |
| `specializes` | Implements a domain-specific specialization |
| `plans` | Converts intent into an executable strategy |
| `generates` | Creates agent or workflow definitions |
| `executes` | Runs plans, agents, or workflows |
| `produces` | Emits artifacts, evidence, or outcomes |
| `verifies` | Validates results against intent or constraints |

## Repository roles

| Repository | Primary role | Main relations |
|---|---|---|
| `bonsai/intent` | Intent ontology / semantic IR | `defines` |
| `bonsai/world-ontology` | World, domain, object, and context vocabulary | `provides`, `specializes` |
| `bonsai/wiki` | Human-curated knowledge and concepts | `provides`, `consumes` |
| `bonsai/repos` | Repository observatory and repository-state data | `observes`, `provides`, `produces` |
| `bonsai/think` | Reasoning and planning methods | `consumes`, `plans`, `produces` |
| `bonsai/yaml-as-agent` | Declarative agent representation / compiler boundary | `consumes`, `generates` |
| `bonsai/agent` | Agent model and execution layer | `consumes`, `executes`, `produces` |
| `bonsai/aw` | Agentic Workflow generation and execution | `generates`, `executes`, `produces` |
| `bonsai/ds-agent` | Data analysis / BQML evidence layer | `analyzes`, `produces`, `verifies` |
| `bonsai/company` | Organizational context for an agent collective | `provides`, `consumes` |
| `bonsai/aw.tui` | Operational interface for AW graphs and workflows | `consumes`, `observes` |

## Semantic architecture

```text
                         ┌──────────────────────┐
                         │    bonsai/intent     │
                         │  Semantic Control    │
                         │       Plane          │
                         └──────────┬───────────┘
                                    │
          ┌──────────────┬──────────┼──────────┬──────────────┐
          ▼              ▼          ▼          ▼              ▼
   world-ontology      wiki       repos      think         company
   context/vocab     knowledge   observe    reason        organize
          │              │          │          │              │
          └──────────────┴──────────┼──────────┴──────────────┘
                                    ▼
                            yaml-as-agent
                                    │
                                    ▼
                                  agent
                                    │
                                    ▼
                                    aw
                                    │
                                    ▼
                           GitHub Workflows
                                    │
                                    ▼
                         Evidence / Outcome
                                    │
                       ┌────────────┴────────────┐
                       ▼                         ▼
                   ds-agent                 repos / wiki
                   analyze                 feedback/index
```

## repo2agent path

The ecosystem supports the following compilation path:

```text
Repository
   ↓
Repository facts / README / structure
   ↓
Ontology
   ↓
Intent IR
   ↓
Plan
   ↓
Agent definition
   ↓
AW workflow
   ↓
Execution
   ↓
Evidence / Outcome
   ↓
Repository state
   ↓
Re-intent
```

`bonsai/aw` acts as the **Agent Midwife**: it should turn repository semantics and approved intent into executable workflow candidates rather than inventing business intent by itself.

## Boundary principle

`bonsai/intent` is not the runtime and not the repository database.

- `intent` answers **what / why / under which constraints**.
- `think` answers **how to reason and plan**.
- `yaml-as-agent` answers **how to represent/compile an agent declaratively**.
- `agent` answers **what an agent is and how it operates**.
- `aw` answers **how an approved agent/workflow is executed**.
- `repos` answers **what repository state is observed**.
- `ds-agent` answers **what can be inferred from data**.
- `world-ontology` answers **what the domain objects and contexts mean**.
- `wiki` answers **what humans have recorded as knowledge**.

This separation keeps the ontology stable while implementations evolve independently.

## Feedback loop

```text
intent
  ↓
execution
  ↓
evidence
  ↓
analysis
  ↓
evaluation
  ↓
new / revised intent
```

The ecosystem is therefore a **closed-loop agent organization**, not a static dependency graph.

## Related repositories

- [`bonsai/intent`](https://github.com/bonsai/intent)
- [`bonsai/world-ontology`](https://github.com/bonsai/world-ontology)
- [`bonsai/wiki`](https://github.com/bonsai/wiki)
- [`bonsai/repos`](https://github.com/bonsai/repos)
- [`bonsai/think`](https://github.com/bonsai/think)
- [`bonsai/yaml-as-agent`](https://github.com/bonsai/yaml-as-agent)
- [`bonsai/agent`](https://github.com/bonsai/agent)
- [`bonsai/aw`](https://github.com/bonsai/aw)
- [`bonsai/ds-agent`](https://github.com/bonsai/ds-agent)
- [`bonsai/company`](https://github.com/bonsai/company)
- [`bonsai/aw.tui`](https://github.com/bonsai/aw.tui)
