# Architecture Decision Records — Domain-Local

This folder holds architectural decisions that affect only this domain.

If a decision affects 2+ domains OR proposes a shared standard, the promotion-lint CI workflow will detect the trigger and post a PR comment asking the author to either:

- **Promote** — open a companion PR in Foundation (`architectural-decisions/`), OR
- **Keep local** — record a non-empty `local-reasoning:` field on the ADR's frontmatter.

The PR cannot merge until one of the two is set.

## File naming

`adr-NNNN-slug.md` — zero-padded sequence number, then kebab-case slug (e.g. `adr-0001-anonymise-datasets.md`).

## Frontmatter

Use the ADR template at `standards/templates/adr-template.md` in the Foundation repo (loaded automatically via `additionalDirectories` when Claude is launched here — see the Domain repo `README.md` for the recommended clone layout). Add these additional fields to its frontmatter:

```yaml
---
title: <short statement>
status: proposed | accepted | superseded
authored-by: <handle>
authored-at: YYYY-MM-DD
affected-domains: [<domain-name>]  # only this domain by default; lint warns if 2+ appear in body
shared: false                     # set true to deliberately trigger promotion
local-reasoning: ""               # required (non-empty) if not promoted when trigger fires
promoted-to: ""                   # URL of Foundation PR when promoted
---
```
