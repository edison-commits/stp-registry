# Contributing to STP Registry

Thanks for helping grow the registry. A few things to know before you open a PR.

## What belongs here

The registry is a **shared vocabulary** — concepts that are stable, well-defined, and likely to appear in STP blocks across many different sites and agents. It is not:

- A glossary of every term in a field
- A collection of product names or brand concepts
- A place for contested or speculative concepts (those belong in block-level claims with low confidence)

If a concept is specific to one site or one use case, it doesn't belong in the shared registry. Authors can use arbitrary `ref` strings in their blocks — they just won't benefit from cross-site interoperability for those concepts.

## Before you open a PR

1. **Search first.** The concept may already exist under a different `ref`. Check `aliases` in each domain file.

2. **Pick the right domain.** Cross-domain concepts go in their primary origin domain, not all domains. Use `aliases` to bridge.

3. **Write a real description.** One sentence. Precise. Avoids circular definitions ("X is a type of X").

4. **Include a real `canonical_ref`.** arXiv papers, W3C specs, and Wikipedia articles with solid sourcing are good. Blog posts are not.

5. **Check the ID sequence.** IDs are sequential within a domain. If the last concept in `ai.ml.json` is `stp:ai.ml.006`, your new concept is `stp:ai.ml.007`. Never skip, never reuse.

## What a good PR looks like

```json
{
  "id": "stp:ai.ml.007",
  "ref": "mixture_of_experts",
  "label": "Mixture of Experts",
  "description": "Architecture where a router selects a sparse subset of specialized sub-networks (experts) per input, enabling large model capacity at lower inference cost",
  "aliases": ["MoE", "sparse MoE", "expert routing"],
  "introduced": "1991",
  "canonical_ref": "https://arxiv.org/abs/1701.06538"
}
```

And update `concept_count` in `index.json`.

## Deprecating a concept

If a concept becomes obsolete or is superseded:

```json
{
  "id": "stp:ai.ml.003",
  "ref": "rag",
  "deprecated": true,
  "deprecated_reason": "Superseded by more precise concepts",
  "successor_id": "stp:ai.search.001"
}
```

The entry stays. The ID stays. Only `deprecated: true` is added.

## New domains

Open an issue before writing any code. A domain proposal needs:

- At least 5 candidate concepts ready to add
- A clear boundary (what's in, what's out)
- A short argument for why this domain is distinct from existing ones
