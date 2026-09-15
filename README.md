# bonsai/ecosystem

**Bonsai Ecosystem** is the declarative semantic registry for the Bonsai repository federation.

> **Many independent repositories, one coherent ecosystem — without becoming a monolith.**

## Architecture

```text
                 SEMANTIC / DOMAINS
                 meaning / contracts
                         │
                         ▼
                    DOCUMENT
          repository metadata / declarations
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
| **Document** | What is declared / observed? | repository metadata, documents, declarations, evidence |
| **Intelligence** | Who / Decide? | agents, reasoning, organizations, plans |
| **Execution** | How? | workflows, tools, operations, FDE |
| **Real World** | What happened? | observations, products, production, outcomes |
| **BQML** | What can we learn? | models, clusters, predictions, anomalies, learned evidence |

BQML is a learning layer, **not** a fifth ownership boundary and not the source of truth.

## Document domain

[`domains/document.yaml`](./domains/document.yaml) defines the document layer.

A **repository is a document-bearing semantic object**, not only executable code.
Its metadata can be observed, normalized, analyzed, validated and declared.

```text
GitHub / repository
       │
       ▼
   observation
       │
       ├── identity
       ├── lifecycle
       ├── activity
       ├── technology
       ├── structure
       └── relations
       │
       ▼
 repository metadata
       │
       ▼
  repository document
       │
       ▼
 ecosystem registry
```

### Repository metadata

The document domain models:

- identity: id, full name, owner, URL
- description and purpose
- lifecycle: created / updated / pushed / archived
- visibility and default branch
- activity: stars, forks, watchers, issues
- technology: language, languages, topics
- structure: `repo.yaml`, README, docs, source files
- ecosystem: domains, roles, capabilities, relations

The distinction is important:

```text
observed fact → inference → validation → declaration
```

GitHub metadata is observation. BQML classifications are inference. `repo.yaml`
and domain YAML are declarations and sources of truth.

## Repository relations

Repositories are first-class graph nodes.

```text
Repo A ──depends_on──► Repo B
  │
  ├──implements──► Repo C
  ├──researches──► Repo D
  ├──uses───────► Repo E
  └──relates_to─► Repo F
```

The relation graph is semantic metadata; it does not create runtime coupling.

`bonsai/github-observatory` observes GitHub repositories, builds the repository
DWH and can project repository metadata and relations into a visual graph.

## Domains

Canonical domain definitions live in [`domains/`](./domains/).

```text
domains/
├── architecture.yaml
├── bqml.yaml
├── document.yaml
├── fashion.yaml
├── game.yaml
├── idol.yaml
├── intelligence.yaml
├── manufacturing.yaml
├── sales.yaml
└── solve.yaml
```

A **domain is a semantic cluster, not a repository container**. A repository can participate in multiple domains through explicit roles.

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

## Design principles

1. **Repo = responsibility.** Every repository has a clear reason to exist.
2. **Repo = metadata-bearing object.** Repository identity, structure, capabilities and relations are observable/documentable.
3. **Domain = meaning.** Domains group responsibilities without absorbing repositories.
4. **Document = symbolic interface.** Documents make repository and domain meaning persistent and shareable.
5. **Capability = reusable function.** Capabilities can cross domain boundaries.
6. **Many-to-many is valid.** Do not force the ecosystem into one tree.
7. **Evidence first.** Observe repository facts before classifying them.
8. **Inference is provisional.** AI/ML may propose; validation makes meaning canonical.
9. **Execution stays separate.** Semantic definitions should not become runtime coupling.
10. **Feedback closes the loop.** Outcomes improve future decisions.

## Core principle

> **Meaning defines. Documents represent. Intelligence decides. Execution acts. Reality proves. BQML learns. Feedback improves the next decision.**
