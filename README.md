# bonsai/ecosystem.md

Bonsai ecosystem architecture and **declarative Repository Semantic Registry**.

## Design principle

Bonsai is a **loosely coupled semantic ecosystem**. Repository meaning is declared here first; repository facts are observed separately by `bonsai/repos` and stored as data.

```text
DECLARATION                         OBSERVATION
┌────────────────────┐              ┌────────────────────┐
│ ecosystem.md       │◄── compare ─►│ repos              │
│ declared meaning   │              │ observed repo data │
└────────────────────┘              └─────────┬──────────┘
                                             │
                                             ▼
                                          database
```

The initial ecosystem is **declarative-first**. AI inference is optional later; it is not required to establish the initial semantic map.

## Architectural layers

| Layer | Question | Examples |
|---|---|---|
| 思想層 | Why? | `bonsai/company`, `bonsai/think` |
| 定義層 | What? | `bonsai/ecosystem.md`, `bonsai/intent`, `bonsai/world-ontology`, `bonsai/wiki` |
| 実装層 | How? | `bonsai/agent`, `bonsai/soshiki`, `bonsai/aw`, `bonsai/yaml-as-agent` |
| 道具層 | With what capability? | Git, GitHub, CLI, Python, Go, MCP, BigQuery |
| データ層 | What state/evidence exists? | `bonsai/repos`, database, observations, metrics, outcomes |

通信は各層を横断する**接続方式**として扱う。

```text
思想層  WHY
   ↓
定義層  WHAT  ← ecosystem / intent / ontology
   ↓
実装層  HOW   ← agent / soshiki / aw
   ↓
道具層  WITH WHAT ← GitHub / Git / CLI / Python / Go / MCP
   ↓
データ層 STATE / EVIDENCE ← repos / database / BQML
   ↕
通信層 CONNECT ← HTTP / API / JSON / YAML / MCP
```

## Responsibility boundaries

### ecosystem — semantic registry

`ecosystem` declares what each repository **means**, its semantic layer, primary role, and explicit relationships.

It does **not** execute agents, collect runtime state, or act as the repository database.

### repos — observation

`bonsai/repos` captures repositories as **data**: README, files, language, topics, activity, dependencies, workflows, and health observations.

`repos` may reference declarations in `ecosystem`, but initially does not infer or redefine repository meaning.

### database — state and evidence

The database stores observed state, history, executions, evidence, metrics, and outcomes.

It is a **state/evidence store**, not the authority for repository meaning.

```text
ecosystem = "what we declare"
repos     = "what we observe"
database  = "what we retain"
analysis  = "what we infer"
```

### soshiki — agent organization only

`bonsai/soshiki` concerns **only the organization of agents**: roles, teams, delegation, hierarchy, and coordination.

It is not the semantic registry for all repositories.

### agent — actor

`bonsai/agent` defines the agent as an actor capable of interpreting intent, reasoning, and acting.

### aw — workflow execution

`bonsai/aw` turns approved intent and agent definitions into executable Agentic Workflows. It is not the source of business meaning.

### tools — capabilities

Tools provide capabilities to agents and workflows. A tool is not an agent.

```text
Agent    = actor / decision maker
Tool     = capability
Workflow = execution of actors + tools
```

## Declaration vs observation

```text
       DECLARE
          │
          ▼
    ┌─────────────┐
    │  ecosystem  │
    └──────┬──────┘
           │ semantic reference
           ▼
    ┌─────────────┐   GitHub observation
    │    repos    │◄───────────────────
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │  database   │
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │ analysis    │
    │ / BQML      │
    └──────┬──────┘
           │ evidence
           ▼
    human / agent decision
           │
           ▼
    ecosystem declaration review
```

This makes future self-organization possible without making AI the initial authority over repository semantics.

## Repository roles

| Repository | Primary role | Layer | Main relations |
|---|---|---|---|
| `bonsai/ecosystem.md` | Repository semantic registry | 定義 | `defines`, `references` |
| `bonsai/intent` | Intent ontology / semantic IR | 定義 | `defines` |
| `bonsai/world-ontology` | World, domain, object, context vocabulary | 定義 | `defines`, `provides` |
| `bonsai/wiki` | Human-curated concepts and knowledge | 定義 | `provides`, `consumes` |
| `bonsai/company` | Organizational purpose/context | 思想 | `provides`, `consumes` |
| `bonsai/think` | Reasoning and planning methods | 思想 / 実装境界 | `plans`, `produces` |
| `bonsai/agent` | Agent model and implementation | 実装 | `consumes`, `executes`, `produces` |
| `bonsai/soshiki` | Agent organization and coordination | 実装 | `organizes`, `coordinates`, `delegates` |
| `bonsai/aw` | Agentic Workflow generation/execution | 実装 | `generates`, `executes`, `produces` |
| `bonsai/yaml-as-agent` | Declarative agent representation / compiler boundary | 実装 | `consumes`, `generates` |
| `bonsai/repos` | Repository observatory / observed data | データ | `observes`, `produces`, `references` |
| `bonsai/ds-agent` | Data analysis / BQML evidence layer | データ / 実装境界 | `analyzes`, `produces`, `verifies` |
| `bonsai/aw.tui` | Operational interface | 実装 / 道具 | `consumes`, `observes` |

## Loose-coupling rules

1. 思想層 does not depend on concrete implementation details.
2. 定義層 defines meaning and contracts; it does not execute them.
3. 実装層 consumes definitions but does not redefine canonical meaning.
4. 道具層 provides capabilities and can be replaced independently.
5. データ層 records state/evidence; it is not semantic authority.
6. 通信層 connects components without owning their meaning.
7. `repos` may reference `ecosystem`, but the initial ecosystem remains declarative.
8. `soshiki` is limited to agent organization.
9. Database stores state/evidence; it does not become the ontology.
10. Semantic inference is an optional later process based on evidence.

## repo2agent

```text
Repository
   ↓
Repository facts / README / structure
   ↓
repos observation
   ↓
ecosystem semantic declaration
   ↓
Ontology / Intent IR
   ↓
Plan
   ↓
Agent definition
   ↓
soshiki organization
   ↓
AW workflow
   ↓
Tool execution
   ↓
Evidence / Outcome
   ↓
database
   ↓
Repository state
   ↓
Re-intent / declaration review
```

`repo2agent` starts from facts but does not confuse facts with meaning.

## Relationship vocabulary

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
| `coordinates` | Coordinates agents or capabilities |
| `organizes` | Defines relationships among agents |
| `references` | Points to another declaration without owning it |

## Core principle

> **Definitions describe meaning. Agents decide and coordinate. Tools provide capabilities. Data stores observations and evidence.**

The ecosystem registry remains declarative so ontology, agents, tools, databases, models, and workflow runtimes can evolve independently.
