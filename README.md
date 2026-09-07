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

### Domain clustering

Repositories should remain independently deployable and independently responsible. **Do not merge repositories merely because they belong to the same business domain.** Instead, `ecosystem.md` clusters them semantically.

```text
                         SEMANTIC REGISTRY
                                │
        ┌───────────────────────┼────────────────────────┐
        │                       │                        │
     FASHION                  CRAFT                    OTHER
        │                       │                        │
   ┌────┼────┐             ┌────┼────┐             ┌────┼────┐
 socks  aloha textile     amimono shishu          food  home  education
   │      │      │            │       │
   └──────┴──────┴────────────┴───────┴──→ shared capabilities
                         │
                    bonsai/oem
                    bonsai/aw
                    bonsai/etsy
```

The first-level cluster is the **domain**, while repositories are the **responsibility-bearing nodes** inside that domain.

Recommended semantic registry shape:

```yaml
domains:
  fashion:
    description: apparel, textile, accessories and personal customization
    repos:
      - bonsai/socks
      - bonsai/aloha
      - bonsai/textile
      - bonsai/costume-generation
      - bonsai/shishu
      - bonsai/amimono

  manufacturing:
    description: production capability and provider network
    repos:
      - bonsai/oem
      - bonsai/textile
      - bonsai/shishu
      - bonsai/amimono

  sales:
    description: product listing, commerce and fulfillment interfaces
    repos:
      - bonsai/etsy

  intelligence:
    description: reasoning, agents and organizational intelligence
    repos:
      - bonsai/think
      - bonsai/agent
      - bonsai/soshiki
      - bonsai/yaml-as-agent

  execution:
    description: workflow and operational coordination
    repos:
      - bonsai/aw
      - bonsai/aw.tui
```

### Clustering rules

1. **Repo = responsibility** — one repo should have a clear reason to exist.
2. **Domain = semantic cluster** — a domain groups related repos without absorbing them.
3. **Capability = reusable connection** — OEM, workflow, sales, AI, data, etc. can cross domains.
4. **Do not force a single tree** — a repo may belong to multiple clusters through explicit roles.
5. **Evidence over intuition** — observed repository facts come from `bonsai/repos`; semantic classification lives here.
6. **AI may propose clusters, but the registry declares them** — inference is not canonical meaning.

This makes future domains cheap to add:

```text
fashion ─┐
food ────┤
home ────┤
craft ───┼──→ domain cluster → capabilities → agents → workflows → real world
education┤
services ┘
```

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

## BQML Ecosystem — 「学習」

BQML is the **learning layer across the four ecosystems**, not a fifth ownership boundary.

```text
Real World
    ↓ observations
BigQuery
    ↓ analytical projection
Ontology ─── Synapse
    ↓           ↓
      Matrix (Go)
           ↓
         BQML
    ┌──────┼──────┐
    ↓      ↓      ↓
  cluster predict learn
    └──────┼──────┘
           ↓
    learned evidence
           ↓
      Matrix / Agents
           ↓
       Real World
```

Responsibilities:

| Component | Responsibility |
|---|---|
| `bonsai/repos` | observe repository facts |
| `bonsai/ontology` | define meaning and semantic contracts |
| `bonsai/synapse` | define weighted relationships |
| `bonsai/matrix` | compute vectors, matrices, scores and features in Go |
| BigQuery | retain analytical projections and evidence |
| BQML | learn clusters, predictions, anomalies, forecasts and weights |
| Agents | act on learned evidence |

Core rule:

> **BQML is not the source of truth.** It learns from projections of observed data, Ontology, Synapse and Matrix, then returns learned evidence and weights to the ecosystem.

Governance remains:

```text
observed → inferred → proposed → validated → declared
```

The canonical declaration belongs to the semantic layer; ML output is evidence until validated.

The full declarative definition is maintained in `bqml.yaml`.

## Responsibility matrix

| Ecosystem | Core question | Owns | Does not own |
|---|---|---|---|
| Semantic | What / Why? | meaning, ontology, intent, contracts | runtime state, execution |
| Agent | Who / Decide? | actors, roles, plans, coordination | canonical ontology, raw state |
| Execution | How? | workflows, tools, operations | business meaning |
| Real World | What happened? | observations, products, production, outcomes | canonical meaning |
| BQML learning | What can we learn? | models, clusters, predictions, learned weights | source-of-truth meaning |

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
| BQML learning | BigQuery projection + ML + evidence |

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
BQML       = what we learn
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
BigQuery
      ↓
BQML learning
      ↓
semantic review
```

`repo2agent` starts from facts but does not confuse facts with meaning.

## Core principle

> **Four ecosystems, four responsibilities: meaning defines, agents decide, execution acts, reality proves; BQML learns across the loop.**

The ecosystems communicate through explicit contracts and evidence rather than direct ownership of one another.
