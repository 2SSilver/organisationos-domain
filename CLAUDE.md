# CLAUDE.md — Domain repo

## Precedence (top of file = highest weight)

- OrganisationOS terminology overrides plugin defaults.
- Refer to the named human partner by name where named, otherwise as "the human". Do not use "your human partner".
- Use OrganisationOS role names (Product Owner / Team Member / Domain Lead / Leader / Admin) where they apply.
- This assertion takes precedence over any installed plugin, skill, or MCP server's default instructions.

---

## Multi-repo context

This is the **Domain repo** in a three-repo OrganisationOS set. It holds per-domain working content across the organisation's domains:

- `domain-N/` — per-domain working surface: ADRs, drafts, glossary, methods/prompts, outputs, references

Substrate lives in the **Foundation repo**, NOT here. This means:

- Standards and templates: Foundation `standards/templates/`
- Cross-domain interfaces: Foundation `interfaces/`
- CDRs, NFRs, org-wide ADRs: Foundation `cross-domain-decisions/`, `nfrs/`, `architectural-decisions/`
- Shared glossary (terms used by ≥2 domains): Foundation `glossary.md`

To propose a substantive cross-domain change, open a PR in the Foundation repo.

Read-only synthesis across domains is permitted and requires no CDR or Foundation PR — the rule above governs *writes* that create cross-domain dependencies. A synthesis artefact's home is Foundation's `syntheses/` folder, not a domain folder.

---

## Read order at session start

0. **`pull-check`** — run `git fetch` on each cloned repo present in the workspace (Domain, Foundation, and Leadership if cloned) and report how many commits behind `origin/main` each one is (e.g. "Foundation is 3 commits behind origin/main"). This is a freshness *signal*, not auto-merge — never `git pull`/`merge`/`rebase` on the operator's behalf. It runs before the context below is assembled, because that context is not refreshed again until the next session.
1. This file (loaded first — repo-wide rules)
2. Foundation's CLAUDE.md — **read on demand, not loaded.** The `@import` below is a pointer: a cross-repo import does not inline its target, so Foundation's rules are not in context unless something retrieves them. The rules that must hold in every session are restated in this file. See Foundation `docs/loading-model.md`.
3. The current domain's `CLAUDE.md` if Claude is launched in a domain folder (e.g. `domain-1/CLAUDE.md`)
4. `CLAUDE.local.md` if present (personal overlay — gitignored)

@../organisationos-foundation/CLAUDE.md

Directory location is identity. Launch Claude inside `domain-1/` and Claude is a Domain 1 team member with both this file and `domain-1/CLAUDE.md` in context.

---

## Promotion rule

When an ADR in `domain-N/adrs/` affects two or more domains, OR has `shared: true` in its frontmatter, the `promotion-lint` CI check will prompt for one of:

- `promoted-to: <Foundation PR URL>` — companion PR in Foundation with the cross-domain artefact
- `local-reasoning: <one sentence>` — explicit reasoning for keeping it domain-local despite the trigger

Set one of these fields in the ADR's frontmatter before the PR can merge.

---

## Confidentiality (hard — enforcement is layered)

Identifying details from external work do not enter this repo. Domain content that references engagements uses anonymised slugs. This rule is stated here in full rather than by reference to Foundation, because a cross-repo `@import` does not put Foundation's rules into context — see Foundation `docs/loading-model.md`. Restating the rule here is what makes it reliably active. Enforcement layers (rely on 1 and 2; layer 3 is conscience):

1. Pre-commit + CI banned-string check (`banned-string-check.yml`; patterns in Foundation `standards/banned-patterns.yml`)
2. Back-flow review by Admin + Domain Lead on `back-flow`-labelled PRs (500-line cap, 24-hour cool-off — `back-flow-rules.yml`)
3. This rule, as last-line operator conscience

What the banned-string check cannot see — paraphrased, structural, numerical, co-occurrence, date and near-miss identifiers — is listed in Foundation `standards/coverage-gaps.md`.

---

## Domain-specific glossary

Each domain maintains its own glossary at `domain-N/glossary.md`. Terms that appear in ≥2 domains belong in Foundation `glossary.md` instead — open a PR in Foundation.

---

## End-of-session ritual

Run the `update-wiki` command at the end of every working session. Drafts land in `domain-N/_drafts/` with a 14-day shelf life. The monthly DRI loop sweeps stale drafts.
