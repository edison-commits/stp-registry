# STP Concept Registry

The canonical concept registry for the [Semantic Transfer Protocol](https://github.com/edison-commits/stp-protocol).

**Live at:** [semanticweb.dev](https://semanticweb.dev)

---

## What this is

Every STP block published on the web references concept IDs like `stp:ai.ml.006`. This registry is the authoritative source for what those IDs mean — their canonical labels, aliases, definitions, and relations.

An agent encountering `stp:ai.ml.006` fetches:
```
GET https://semanticweb.dev/concepts/ai/ml/006-large_language_model.json
```
And receives the full structured definition, enabling unified knowledge graphs across any site using STP.

---

## Structure

```
index.json          — full concept index, machine-readable
aliases.json        — 193 alias → canonical ID mappings
domains.json        — domain taxonomy + protected namespace rules
concepts/
  ai/
    ml/             — 15 concepts (neural_network → reasoning)
    agents/         — 5 concepts (agent → planning)
    search/         — 3 concepts (RAG → knowledge_graph)
  ecommerce/        — 5 concepts (product → order)
  systems/
    network/        — 3 concepts (api → protocol)
  science/
    general/        — 2 concepts (confidence → provenance)
.well-known/
  stp-registry.json — machine discovery endpoint
  stp-keys.json     — public key registry for block verification
```

**Current count:** 33 concepts across 6 domains, 193 alias mappings.

---

## Quick lookup

```bash
# Resolve a concept ID
curl https://semanticweb.dev/concepts/ai/ml/006-large_language_model.json

# Get all aliases
curl https://semanticweb.dev/aliases.json

# Full index
curl https://semanticweb.dev/index.json

# Domain taxonomy
curl https://semanticweb.dev/domains.json
```

---

## Concept file format

```json
{
  "id":         "stp:ai.ml.006",
  "ref":        "large_language_model",
  "domain":     "ai.ml",
  "label":      "Large Language Model",
  "aliases":    ["LLM", "language model", "GPT", "foundation model"],
  "definition": "A neural language model trained on large-scale text corpora...",
  "related":    ["stp:ai.ml.004", "stp:ai.ml.001"],
  "protected":  false,
  "added":      "2026-03-06",
  "version":    1
}
```

---

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for how to propose new concepts.

**Protected namespaces** (`medical.*`, `legal.*`, `finance.*`) require expert review.  
All other domains welcome PRs following the template.

---

## License

MIT — use freely in any STP implementation.
