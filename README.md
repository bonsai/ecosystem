# bonsai/ecosystem

**Bonsai Ecosystem** is the declarative semantic registry for the Bonsai repository federation.

> **Many independent repositories, one coherent ecosystem — without becoming a monolith.**

## Architecture

```text
                 SEMANTIC / DOMAINS
                 meaning / contracts
                         │
                         ▼
                 INTELLIGENCE
                 think / agents / plans
                         │
                         ▼
                   EXECUTION
                 AW / tools / FDE
                         │
                         ▼
                  REAL WORLD
              state / product / outcome
                         │
                         └──── feedback ───► semantic review

                 BQML = learning across the loop
```

| Layer | Question | Owns |
|---|---|---|
| **Semantic** | What / Why? | domains, ontology, intent, contracts |
| **Intelligence** | Who / Decide? | agents, reasoning, organizations, plans |
| **Execution** | How? | workflows, tools, operations, FDE |
| **Real World** | What happened? | observations, products, production, outcomes |
| **BQML** | What can we learn? | models, clusters, predictions, anomalies, learned evidence |

BQML is a learning layer, **not** a fifth ownership boundary and not the source of truth.

## Domains

Canonical domain definitions live in [`domains/`](./domains/).

```text
domains/
├── architecture.yaml
├── bqml.yaml
├── fashion.yaml
├── game.yaml
├── idol.yaml
├── intelligence.yaml
├── manufacturing.yaml
├── sales.yaml
└── solve.yaml
```

A **domain is a semantic cluster, not a repository container**. A repository can participate in multiple domains through explicit roles.

## Idol

[`domains/idol.yaml`](./domains/idol.yaml) defines the idol ecosystem:

```text
idol
├── discovery / portal
├── research / ontology
├── live / events
├── fan sites / archives
├── interaction / quiz
├── production / simulation
├── map / geography
├── ranking / comparison
└── fashion / styling
```

The current registry includes `bonsai/idol-fansite` with the stable idol path pattern:

```text
i100/hayakawa-momo
```

`i100` is the stable idol identifier and `hayakawa-momo` is the human-readable slug. New idols can descend as `i101`, `i102`, etc.

## Solve: the cross-domain protocol

[`domains/solve.yaml`](./domains/solve.yaml) defines the common problem-solving loop:

```text
Aware → Intent → Think ↔ Intelligence → AX → FDE
  ↑                                      ↓
  └──── Feedback ← Outcome ←────────────┘
```

Repository bindings:

| Stage | Repository |
|---|---|
| Aware | `bonsai/Aware.md` |
| Intent | `bonsai/intent` |
| Think | `bonsai/think` |
| Intelligence | `bonsai/intelligence` |
| AX | `bonsai/AX` |
| FDE | `bonsai/fde-agent`, `bonsai/fdes-orchestra` |

`solve` integrates these responsibilities; it does **not** merge the repositories.

## Intelligence

[`domains/intelligence.yaml`](./domains/intelligence.yaml) defines the intelligence cluster:

```text
repository facts + semantic contracts
              ↓
            Think
              ↓
      Intelligence / Agents
              ↓
        plan / decision
              ↓
             AW
              ↓
         real world
              ↓
           evidence
```

Representative repositories:

- `bonsai/agent` — agent model
- `bonsai/soshiki` — organization / coordination
- `bonsai/yaml-as-agent` — declarative agents / repo2agent
- `bonsai/think` — reasoning and planning methods
- `bonsai/ds-agent` — analytical agent

## repo2agent

A core ecosystem pattern is **repo2agent**:

```text
Repository
    ↓
observed facts
    ↓
semantic classification
    ↓
capabilities
    ↓
agent proposal
    ↓
validation
    ↓
agent definition
    ↓
workflow
    ↓
execution
    ↓
outcome / evidence
```

> **Observation is not meaning. Inference is not declaration.**

AI can propose classifications, agents, relationships and workflows. Canonical meaning becomes authoritative only after validation and declaration in domain YAML.

## Evidence and learning

```text
observed → inferred → proposed → validated → declared
```

Repository facts should come from `bonsai/repos`. Analytical projections belong in BigQuery. BQML can discover clusters, predict outcomes, detect anomalies and learn weights, but its output remains evidence until validated.

```text
repos → BigQuery → BQML
  ↑                  │
  └──── evidence ←──┘
```

## Domain examples

### Fashion / Manufacturing

```text
fashion
  ├── costume-generation
  ├── textile
  ├── amimono
  └── shishu
          │
          ▼
    manufacturing
          │
          ▼
         OEM
```

The registry connects these repositories semantically; it does not absorb them into one repository.

### Sales

Sales owns the commerce boundary such as product listing and fulfillment interfaces. It can consume fashion and manufacturing capabilities without owning their ontology.

### Architecture

Architecture describes structural and system-level relationships. It does not replace the repositories that implement those components.

## Design principles

1. **Repo = responsibility.** Every repository has a clear reason to exist.
2. **Domain = meaning.** Domains group responsibilities without absorbing repositories.
3. **Capability = reusable function.** Capabilities can cross domain boundaries.
4. **Many-to-many is valid.** Do not force the ecosystem into one tree.
5. **Evidence first.** Observe repository facts before classifying them.
6. **Inference is provisional.** AI/ML may propose; validation makes meaning canonical.
7. **Execution stays separate.** Semantic definitions should not become runtime coupling.
8. **Feedback closes the loop.** Outcomes improve future decisions.
9. **Optimize for value.** Measure time, cost, quality, automation, knowledge and ROI.
10. **Keep repositories independently useful.** The ecosystem coordinates; it does not create a monolith.

## Repository map

```text
bonsai/ecosystem
│
├── domains/                 # canonical domain declarations
│   ├── architecture.yaml
│   ├── bqml.yaml
│   ├── fashion.yaml
│   ├── game.yaml
│   ├── idol.yaml
│   ├── intelligence.yaml
│   ├── manufacturing.yaml
│   ├── sales.yaml
│   └── solve.yaml
│
└── README.md                # architecture, registry rules, contracts
```

## Relationship to the Bonsai federation

```text
ecosystem
   │
   ├── domains / contracts
   │
   ├──────────────► intent / think / intelligence / AX / FDE
   │
   ├──────────────► repos / ontology / synapse / matrix
   │
   └──────────────► aw / domain workflows
                         │
                         ▼
                    real world
```

`bonsai/ecosystem` is therefore a **registry and contract layer**, not an application runtime.

## Core principle

> **Meaning defines. Intelligence decides. Execution acts. Reality proves. BQML learns. Feedback improves the next decision.**

That is the Bonsai Ecosystem.
