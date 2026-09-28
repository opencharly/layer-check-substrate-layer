# AGENTS.md — layer-check-substrate-layer

Standalone candy repo for the `check-substrate-layer` layer — the deployable
member of the `check-substrate` R10 bed (C2-substrate). The candy lives in
`charly.yml` at the repo root: the `write:` marker step and the `check:`
assertions over `/etc/check-substrate-marker`. The repo declares **no `skill:`
entity**; the owning guidance is the family skill `/charly-check:check` (the gap
is tracked in `opencharly/opencharly#291`).

Canonical files:

- `charly.yml` — the `check-substrate-layer:` candy entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-check:check` — the owning (family) skill. The check bed and `plan:`
  authoring reference, incl. `check:` step verbs, the `disposable: true` bed
  model, and deploy-scope check authoring. Load before editing or troubleshooting
  this layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, and service declarations). Load before editing any entity field or
  plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence; they must stay
  valid on every distro arm they run on. Scope a distro-specific check in the
  command itself — the check runner does not honour runner-level
  `exclude-distro` fields.

## Modify this repo

- Keep the marker path `/etc/check-substrate-marker` dedicated so concurrently
  fanned-out beds do not collide.
- The deploy-scope assertion is authored on the DEPLOY NODE's plan — a composed
  candy's `plan:` never reaches a deploy-scope check runner, so do not move that
  check into this layer.
- New behaviour claims belong in the `plan:` as an observable `check:` step.
- This repo has no `skill:` entity, so there is no projected corpus to mirror.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
