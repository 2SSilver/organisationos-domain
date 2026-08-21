## What changed

One paragraph. What is different now?

## Why

One paragraph. What problem does this solve? What changed in the world that made this change necessary?

## Domain(s) affected

- [ ] domain-1
- [ ] domain-2
- [ ] domain-3
- [ ] domain-4
- [ ] `.github/` or `.claude/` harness (two-approver: Admin + Leader required)

> **ADR promotion check:** If this PR adds or edits a file under `domain-N/adrs/`, promotion-lint will check for cross-domain triggers. If a trigger fires, set `promoted-to:` (companion Foundation PR URL) or `local-reasoning:` in the ADR's frontmatter before merging.

## Cross-domain implications

None | <list, with one line each>. If cross-domain, has a CDR been raised in Foundation? (See `../organisationos-foundation/standards/templates/cdr-template.md`)

## Approval checklist (cross-domain / substrate PRs only)

Canonical rule (spec §10/§11.2/§12): the Leader + the Domain Lead of each
affected domain (+ Product Owner and Admin where the CDR template lists
them). CODEOWNERS lists the fallback superset; this checklist records the
actual affected set.

- [ ] Affected domain(s) named: <list>
- [ ] Each affected Domain Lead approved
- [ ] Leader approved
- [ ] Product Owner approved (where the CDR template lists PO for this artefact type)
- [ ] Admin approved (where the CDR template lists Admin for this artefact type)

Manual affordance; the completeness check is CI-enforced in the Foundation repo, where cross-domain artefacts live.

## Reviewer affordances

- [ ] Rendered preview opened: <link auto-posted by CI>
- [ ] Banned-string check passed locally (pre-commit + CI)
- [ ] Promotion-lint passed (or `promoted-to:` / `local-reasoning:` set in ADR frontmatter)
- [ ] Glossary check run? (advisory — review any flagged terms against `organisationos-foundation/glossary.md`)
- [ ] I read the artefact, not just the agent's review

## CDR linkage (if this PR closes a propagation action)

Closes CDR-XXX — `promoted-to:` set in `domain-N/adrs/<file>.md`

## Reviewers

- Domain Lead: @<handle>
- Cross-domain reviewer (if applicable): @<handle>
- Second reviewer (mandatory if this is a `back-flow` PR or proposer wears multiple roles): @<handle>
