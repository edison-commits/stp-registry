# Contributing to the STP Registry

## How to propose a new concept

1. Fork this repo
2. Copy the template below into the correct domain folder
3. Name the file `NNN-concept_ref.json` (next available number in the domain)
4. Open a PR with title: `[concept] stp:domain.sub.NNN concept_ref`
5. A maintainer will review within 7 days

## Concept template

```json
{
  "id":         "stp:DOMAIN.SUB.NNN",
  "ref":        "snake_case_name",
  "domain":     "domain.subdomain",
  "label":      "Human Readable Label",
  "aliases":    ["alias one", "alias two", "abbreviation"],
  "definition": "Clear, precise definition in 1-3 sentences. No marketing language.",
  "related":    ["stp:domain.sub.NNN"],
  "protected":  false,
  "added":      "YYYY-MM-DD",
  "version":    1
}
```

## Acceptance criteria

- Definition must be precise and domain-neutral
- At least 3 aliases covering common usage variants
- At least 1 related concept (or explicit note if truly standalone)
- ref must be snake_case, all lowercase, no hyphens
- ID must follow `stp:domain.subdomain.NNN` format with next available number

## Proposing a new domain

Open an issue with title `[domain] domain.subdomain` and explain:
- What class of concepts it covers
- Why it doesn't fit existing domains
- At least 5 seed concepts you'd add immediately

## Protected namespaces

`medical.*`, `legal.*`, `finance.*` require:
- Expert credentials in the relevant field
- At minimum 2 reviewer approvals
- 14-day staging period before merge

Do not open PRs to protected namespaces without first opening an issue.

## What gets rejected

- Concepts too specific to a single product or company
- Definitions that are opinionated or non-neutral
- Duplicate refs (check aliases.json first)
- Missing or vague definitions
