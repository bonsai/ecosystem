# bonsai/ecosystem.md

Bonsai ecosystem architecture and **declarative Repository Semantic Registry**.

## Four ecosystems

Bonsai is a federation of four loosely coupled ecosystems. Each has one responsibility and a clear boundary.

```text
① SEMANTIC       ② AGENT          ③ EXECUTION       ④ REAL WORLD
Meaning / Why  →  Decide / Who  →  Act / How     →  State / Outcome
     ↑                                                    │
     └──────────────── evidence / feedback ──────────────┘
```

### ① Semantic Ecosystem — 「意味」

**Question: What is it? Why does it exist?**

Owns vocabulary, ontology, intent, concepts, domain models, and semantic contracts.

Representative repositories:
- `bonsai/ecosystem.md` — repository semantic registry
- `bonsai/intent` — intent / semantic IR
- `bonsai/world-ontology` — world and domain vocabulary
- `bonsai/wiki` — human-curated knowledge
- `bonsai/company` — organizational purpose and context
- `bonsai/think` — reasoning and planning methods

**Boundary:** defines meaning; does not execute runtime operations.

### ② Agent Ecosystem — 「知性」

**Question: Who reasons, decides, plans, and coordinates?**

Owns actors, roles, plans, delegation, organizations, and agent behavior.

Representative repositories:
- `bonsai/agent` — agent model / actor
- `bonsai/soshiki` — agent organization and coordination
- `bonsai/yaml-as-agent` — declarative agent representation
- `bonsai/ds-agent` — analytical agent / evidence interpretation

**Boundary:** agents decide and coordinate; they do not redefine canonical meaning.

### ③ Execution Ecosystem — 「実行」

**Question: How does a decision become an operation?**

Owns workflows, tool invocation, automation, and operational interfaces.

Representative repositories:
- `bonsai/aw` — Agentic Workflows
- `bonsai/aw.tui` — operational interface
- GitHub / Git / CLI / Python / Go / MCP — capabilities and interfaces

```text
Agent    = actor / decision maker
Tool     = capability
Workflow = execution
```

**Boundary:** executes approved plans; it does not own business meaning.

### ④ Real-World Ecosystem — 「現実」

**Question: What exists, changes, gets produced, and actually happened?**

Owns observations, repository state, databases, products, production processes, vendors, and outcomes.

Representative repositories:
- `bonsai/repos` — repository observatory
- database / BigQuery / BQML — state, evidence, metrics
- `bonsai/costume-generation` — product/costume composition
- `bonsai/textile` — textile production IR
- `bonsai/amimono` — knitting production
- `bonsai/shishu` — embroidery production
- external vendors / factories — production boundary

**Boundary:** supplies observed state and outcomes; it is not the authority for abstract semantics.

## Responsibility matrix

| Ecosystem | Core question | Owns | Does not own |
|---|---|---|---|
| Semantic | What / Why? | meaning, ontology, intent, contracts | runtime state, execution |
| Agent | Who / Decide? | actors, roles, plans, coordination | canonical ontology, raw state |
| Execution | How? | workflows, tools, operations | business meaning |
| Real World | What happened? | observations, products, production, outcomes | canonical meaning |

## Four-ecosystem loop

```text
┌──────────────────┐
│ ① SEMANTIC       │  meaning / intent / ontology
└────────┬─────────┘
         │ contract
         ▼
┌──────────────────┐
│ ② AGENT          │  decide / plan / coordinate
└────────┬─────────┘
         │ plan
         ▼
┌──────────────────┐
│ ③ EXECUTION      │  workflow / tool / operation
└────────┬─────────┘
         │ action
         ▼
┌──────────────────┐
│ ④ REAL WORLD     │  data / product / outcome
└────────┬─────────┘
         │ evidence
         └──────────────────► semantic review
```

This is a closed learning loop, not a tightly coupled software stack.

## Existing architectural layers

The four ecosystems are the **top-level boundaries**. Existing layers fit inside them:

| Ecosystem | Layers |
|---|---|
| Semantic | 思想層 + 定義層 |
| Agent | 実装層 / agent organization |
| Execution | 実装層 + 道具層 + 通信層 |
| Real World | データ層 + physical production |

## Manufacturing example

```text
SEMANTIC
  costume / garment / embroidery / knitting
        ↓
AGENT
  design agent / production planner
        ↓
EXECUTION
  AW → textile IR → amimono / shishu adapter
        ↓
REAL WORLD
  vendor → machine → garment → production result
        ↓
  quality / cost / lead-time evidence
```

Therefore:
- `costume-generation` = **what should be made**
- `textile` = **common production representation**
- `amimono` / `shishu` = **knitting / embroidery specialization**
- `vendor` = **who/what can make it**
- `aw` = **coordinates execution**

The vendor is an external production system, not part of the costume ontology.

## Declaration vs observation

```text
ecosystem  = what we declare
repos      = what we observe
database   = what we retain
analysis   = what we infer
```

`ecosystem` remains declarative-first. AI inference may improve the registry later, but does not become the initial authority for repository meaning.

## repo2agent

```text
Repository facts
      ↓
repos observation
      ↓
ecosystem semantic declaration
      ↓
Intent / Ontology IR
      ↓
Agent definition
      ↓
soshiki organization
      ↓
AW workflow
      ↓
Tool / vendor execution
      ↓
Evidence / outcome
      ↓
database
      ↓
semantic review
```

`repo2agent` starts from facts but does not confuse facts with meaning.

## Core principle

> **Four ecosystems, four responsibilities: meaning defines, agents decide, execution acts, reality proves.**

The ecosystems communicate through explicit contracts and evidence rather than direct ownership of one another.
