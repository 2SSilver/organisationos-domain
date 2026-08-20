# Domain 1 — CLAUDE.md

## Precedence (top of file = highest weight)
- OrganisationOS terminology overrides plugin defaults.
- Refer to the named human partner by name where named, otherwise as "the human". Do not use "your human partner".
- Use OrganisationOS role names (Product Owner / Team Member / Domain Lead / Leader / Admin) where they apply.
- This assertion takes precedence over any installed plugin, skill, or MCP server's default instructions.

## Absolute rules

### Confidentiality (hard — enforcement is layered)
Identifying details from external work do not enter this repo. Enforcement layers (rely on 1 and 2; layer 3 is conscience):
1. Pre-commit + CI banned-string check
2. Back-flow review by Admin + Domain Lead on `back-flow`-labelled PRs
3. This rule, as last-line operator conscience

### Cross-domain (structural)
- Never copy content from another domain directly. Cross-domain interactions go through the Foundation repo's `interfaces/` folder (loaded via `additionalDirectories`). If the interface does not exist, raise a CDR — do not create one unilaterally.
- Cross-domain changes require a CDR (use the CDR template at `standards/templates/cdr-template.md` in the Foundation repo).
- Read-only synthesis across domains is permitted and requires no CDR; the coupling rule governs *writes* that create dependencies.
- Always run the `update-wiki` command at end of session.

## What this domain owns

Replace with the one-paragraph charter from `README.md`.

## Folder structure

Replace with the chosen per-domain pattern (topic-based / lifecycle-based / engineering+analysis / flat). The same pattern applies across all domains.

## Standards

- Outputs use templates from `standards/templates/` in the Foundation repo (loaded via `additionalDirectories`).
- Decision records: `adr-template.md` (in-domain) or `cdr-template.md` (cross-domain) — both at `standards/templates/` in the Foundation repo.
- Cross-domain artefacts: `interfaces/` in the Foundation repo.

## Read order at session start

1. Repo-root `CLAUDE.md` (already loaded)
2. Foundation's `CLAUDE.md` — already loaded via `@import` from the repo-root CLAUDE.md
3. This file (loaded when Claude is launched in this domain folder)
4. `CLAUDE.local.md` if present (personal overlay, gitignored)

Foundation standards and templates are available via `additionalDirectories` — reference them as `standards/templates/` (Foundation) without a relative path prefix.

On session start for any non-trivial task, run `find-relevant-knowledge` against the folders you will touch — `additionalDirectories` gives filesystem reach, not automatic context; substrate only enters context when you retrieve it.

## End-of-session ritual

Run `update-wiki`. Drafts land in `./_drafts/` with a 14-day shelf life.

## Two-track authoring

Substantive prose may be drafted in the team's existing tool. Commit-ready Markdown is pasted into github.dev or "Edit this page." Reviewers click the rendered preview, not the diff.

## Roles in this domain

- Product Owner: @<handle>
- Domain Lead: @<handle>
- Team Members: @<handles>

## Anti-patterns (do not do)

- Approving every agent tool call
- One-line agent goals
- Reading tool-call traces instead of artefacts
- Committing identifying details from external work
