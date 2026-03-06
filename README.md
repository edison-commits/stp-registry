# STP Registry

**The canonical concept namespace for the [Semantic Transfer Protocol](https://github.com/edison-commits/stp-protocol).**

Every concept referenced in an STP block uses a stable ID from this registry: `stp:domain.subdomain.NNN`

> This is a separate repo from [stp-protocol](https://github.com/edison-commits/stp-protocol) by design. The protocol defines *how* agents communicate. The registry defines *what* they're talking about. They evolve on different timescales.

---

## Why a Separate Repo?

The protocol spec changes rarely. The registry grows continuously — new domains, new concepts, new versions as fields evolve. Keeping them separate means:

- The registry can accept PRs from domain experts without touching the protocol spec
- Agents can pin to a registry version independently of the protocol version
- The registry can eventually live at its own domain (e.g. `registry.semanticweb.dev`) and be served directly as a JSON API

---

## ID Format

```
stp:domain.subdomain.NNN
```

| Part | Example | Meaning |
|------|---------|---------|
| `domain` | `ai` | Top-level category |
| `subdomain` | `ml` | Specific area within the domain |
| `NNN` | `006` | Zero-padded sequential number |

Full example: `stp:ai.ml.006` → Large Language Model

**IDs are permanent.** A retired concept gets `"deprecated": true`. IDs are never reused or reassigned.

---

## Structure

```
registry/
├── index.json                  ← Master index: all domains + concept counts
└── concepts/
    ├── ai.ml.json              ← Machine learning
    ├── ai.agents.json          ← AI agents
    ├── ai.search.json          ← Search & retrieval
    ├── data.graph.json         ← Graph & knowledge representation
    ├── systems.network.json    ← Networking & protocols
    └── physics.quantum.json    ← Quantum computing
```

---

## Current Domains (v1.0)

| Domain | Label | Concepts |
|--------|-------|:--------:|
| `ai.ml` | Machine Learning | 6 |
| `ai.agents` | AI Agents | 5 |
| `ai.search` | Search & Retrieval | 3 |
| `data.graph` | Graph & Knowledge | 2 |
| `systems.network` | Networking & Protocols | 2 |
| `physics.quantum` | Quantum Computing | 2 |
| | **Total** | **20** |

---

## Concept Format

Each entry in a domain file:

```json
{
  "id": "stp:ai.ml.006",
  "ref": "large_language_model",
  "label": "Large Language Model",
  "description": "Transformer-based model trained on large text corpora...",
  "aliases": ["LLM", "foundation model", "language model"],
  "introduced": "2018",
  "canonical_ref": "https://arxiv.org/abs/2005.14165"
}
```

| Field | Required | Notes |
|-------|----------|-------|
| `id` | ✅ | Permanent. Never reused. |
| `ref` | ✅ | snake_case slug used in STP blocks |
| `label` | ✅ | Human-readable name |
| `description` | ✅ | One sentence. Precise. |
| `aliases` | ✅ | Alternative names agents should recognize |
| `introduced` | ✅ | Year the concept was coined or formalized |
| `canonical_ref` | ✅ | Authoritative external reference (arXiv, Wikipedia, W3C) |
| `deprecated` | — | Set to `true` when retired. ID is never deleted. |

---

## Contributing

### Adding a Concept

1. Find the right domain file in `concepts/`
2. Add your concept with the next sequential ID in that domain
3. Update the `concept_count` in `index.json`
4. Open a PR with a brief justification

**Guidelines:**
- Concepts must be domain-agnostic — they describe a *thing*, not a *use of a thing*
- Cross-domain concepts go in their primary origin domain (use `aliases` to bridge)
- New concepts require a real `canonical_ref` (no Wikipedia stubs or blog posts as primary source)
- Confidence: if a concept's existence is contested in its own field, note it in `description`

### Proposing a New Domain

New domains require broader discussion — open an issue first. A domain needs at least 5 candidate concepts to be worth its own file.

### Rules

- ❌ Never delete or renumber an existing concept
- ❌ Never change an existing `id` or `ref` (these are stable references in deployed STP blocks)
- ✅ `deprecated: true` for concepts that are no longer useful
- ✅ Add `successor_id` when a concept is superseded by a better one

---

## Using the Registry

### In an STP Block

```json
{
  "stp_version": "0.1",
  "concepts": [
    { "id": "stp:ai.ml.006", "ref": "large_language_model", "weight": 1.0 }
  ]
}
```

### Fetching via GitHub

```bash
# Get all AI/ML concepts
curl https://raw.githubusercontent.com/edison-commits/stp-registry/main/concepts/ai.ml.json

# Get the master index
curl https://raw.githubusercontent.com/edison-commits/stp-registry/main/index.json
```

---

## Versioning

The registry uses a monotonic version in `index.json`. Backwards-incompatible changes (which should be extremely rare) increment the major version and are announced via GitHub releases.

Concept additions are backwards-compatible by definition — existing IDs never change meaning.

---

## Relation to stp-protocol

| Repo | Contains | Changes when |
|------|----------|-------------|
| [stp-protocol](https://github.com/edison-commits/stp-protocol) | Spec, format, security model, prototypes | Protocol semantics change |
| [stp-registry](https://github.com/edison-commits/stp-registry) | Concept IDs, domain taxonomy | New concepts are added |

---

## License

MIT — concepts are freely reusable by anyone implementing STP-compatible agents or tooling.
