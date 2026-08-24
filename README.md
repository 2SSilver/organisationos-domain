# OrganisationOS — Domain repo

## 1. What this is

This is the **Domain repo** in an OrganisationOS three-repo set. It holds the per-domain working content for every domain in the organisation. Each domain has its own folder (`domain-1/` through `domain-N/`). Shared substrate lives in the Foundation repo and is loaded automatically via `additionalDirectories`.

---

## 2. What lives here

| Path | Contents |
| --- | --- |
| `domain-N/` | Per-domain working surface |
| `domain-N/adrs/` | Domain-local Architecture Decision Records |
| `domain-N/glossary.md` | Domain-specific terms (unique to this domain) |
| `domain-N/_drafts/` | Short-lived drafts (14-day shelf life; DRI loop sweeps) |
| `domain-N/methods/` | Domain methods and prompts (Pattern A back-flow) *(user-defined sub-structure — see §7)* |
| `domain-N/outputs/` | Committed outputs (Markdown, CSV, etc.) *(user-defined sub-structure — see §7)* |
| `domain-N/references.md` | Pointer log to external/live artefacts |

**NOT here:** CDRs, NFRs, cross-domain interfaces, org-wide ADRs, standards, or the shared glossary. Those live in the Foundation repo. If content affects more than one domain, open a PR in Foundation.

---

## 3. Clone layout

Recommended layout — all three repos as siblings under one parent folder:

```text
~/projects/<adopter-org>/
  organisationos-foundation/     ← must be cloned first
  organisationos-leadership/
  organisationos-domain/         ← this repo
```

**Critical:** do NOT nest these repos inside another project tree (e.g. not inside a PAI workspace or another Git repo). Cross-repo `@import` in `CLAUDE.md` resolves via `../organisationos-foundation/CLAUDE.md` — the path must be a top-level sibling.

---

## 4. Role-to-clone-set matrix

| Role | Required clones | `additionalDirectories` in `settings.local.json` |
| --- | --- | --- |
| Team Member | Domain + Foundation | `["../organisationos-foundation"]` |
| Product Owner | Domain + Foundation | `["../organisationos-foundation"]` |
| Domain Lead | Domain + Foundation | `["../organisationos-foundation"]` |
| Leader | All three | `["../organisationos-foundation", "../organisationos-leadership"]` from Domain |
| Admin | All three (+ per-domain if split) | Full set in each clone |

---

## 5. Onboarding sequence

1. Clone Foundation first (the `@import` in this repo's `CLAUDE.md` resolves to `../organisationos-foundation/`).
2. Clone this repo as a sibling.
3. Update `.github/CODEOWNERS` with real GitHub handles for each domain lead.
4. The role→`additionalDirectories` mapping has one canonical source: Foundation's `standards/templates/onboarding/` (5 role-specific files). Copy the file matching your role — `../organisationos-foundation/standards/templates/onboarding/settings.local.json.example-<role>` — to `.claude/settings.local.json`, and the matching `claude-local-<role>.example.md` to `CLAUDE.local.md`. This repo's own `.claude/settings.local.json.example`, if present, is a pointer to that folder, not a second copy of the mapping. On a role change, re-copy from the updated onboarding file (see the monthly-DRI checklist).
5. Install the pre-commit hook from Foundation: `cp ../organisationos-foundation/.github/hooks/banned-string-pre-commit .git/hooks/pre-commit && chmod +x .git/hooks/pre-commit`.

---

## 6. Promotion rule reminder

When an ADR in `domain-N/adrs/` triggers the promotion-lint check (cross-domain mentions or `shared: true` in frontmatter), the author must set one of these fields before merge:

- `promoted-to: <Foundation PR URL>` — companion PR in Foundation exists
- `local-reasoning: <one sentence>` — explicit justification for keeping it domain-local

The CI check `promotion-lint.yml` blocks merge until one field is set.

---

## 7. Generic worked example — GreenLeaf Research Lab

GreenLeaf Research Lab runs four domains: **research**, **operations**, **fundraising**, and **compliance**. A Team Member on the research domain drafts an ADR in `domain-research/adrs/` proposing how to anonymise datasets before sharing them externally. The ADR mentions both the operations and compliance domains in the context section.

The `promotion-lint` CI check fires: it detects two domain mentions. The author has two choices: (a) open a companion ADR PR in Foundation (`architectural-decisions/`) and set `promoted-to:` pointing to it, or (b) write `local-reasoning:` explaining why it stays in the research domain (rare; only valid if the other domains are mentioned informally, not substantively).

The author opens a companion ADR PR in Foundation (`architectural-decisions/`). One Leader plus the Domain Lead of research, operations, and compliance review the Foundation ADR. On merge, Admin opens a propagation log entry in Leadership and opens implementation PRs for each affected domain. Each Domain Lead merges their domain's implementation PR independently. The ADR in `domain-research/adrs/` is merged with `promoted-to: <Foundation PR URL>`.

---

## 8. Split-per-domain path

When the organisation grows and one Domain repo per domain is preferable, follow these steps to migrate from "one Domain repo with N folders" to "one Domain repo per domain":

1. **Create a new repo** from this template for the domain being extracted (e.g. `organisationos-domain-research`).
2. **Move the folder** — copy `domain-research/` contents into the new repo's root structure.
3. **Update Foundation** — in the Foundation repo, update `glossary.md`'s `## Domains` section to list the new repo, and update `.github/CODEOWNERS` to add the new Domain Lead's handle to the relevant paths.
4. **Update CI callers** — any workflow caller in the old Domain repo that referenced `domain-research/` paths should now reference the new repo. Update `additionalDirectories` in settings files across all affected clones.
5. **Archive the empty folder** — remove the now-empty `domain-research/` folder from this repo in a dedicated PR, with a pointer comment in the commit message to the new repo.
6. **Update CODEOWNERS** — remove the `domain-research/` lines from this repo's `.github/CODEOWNERS`.

This process can be done incrementally — one domain at a time.

---

## 9. Pointer to Foundation

For source of truth on standards, CDRs, NFRs, interfaces, and shared CI, see the Foundation repo (`../organisationos-foundation/`). Domain content references Foundation — it does not copy or redefine it.
