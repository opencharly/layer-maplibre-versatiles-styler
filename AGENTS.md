# AGENTS.md — layer-maplibre-versatiles-styler

Standalone candy repo for the `maplibre-versatiles-styler` layer — the MapLibre
VersaTiles style-switcher control, bundled locally to avoid a runtime CDN. The
candy lives in `charly.yml` at the repo root: the release-tarball + npm-fallback
plan step, the `check:` assertions, and the embedded `skill:` entity projected
into the marketplace corpus as `/charly-versa:maplibre-versatiles-styler`.

Canonical files:

- `charly.yml` — the `maplibre-versatiles-styler:` candy entity and the
  `maplibre-versatiles-styler-skill:` skill entity.
- `CHANGELOG/` — per-CalVer release history; read it before changing baked checks.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-versa:maplibre-versatiles-styler` — the owning skill. The control, its
  two-tier install, and the `/styler/` re-export path. Load before editing or
  troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `mkdir:`/`command:`/`check:`, per-distro `distro:`
  arms, package/repo sections, and service declarations). Load before editing any
  entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence; they must stay
  valid on every distro arm they run on. Scope a distro-specific check in the
  command itself — the check runner does not honour runner-level
  `exclude-distro` fields.
- The `check:` probe is deliberately lenient about the bundle filename (the
  package ships both ESM and UMD builds across paths); it asserts at least one
  non-empty `*.js` under the install dir. Keep it lenient.

## Modify this repo

- Edit the `maplibre-versatiles-styler:` candy entity AND its `skill:` entity in
  `charly.yml` together. The skill is the projected usage source, so a behaviour
  change not mirrored in the skill leaves the corpus stale.
- The two-tier install (GitHub release tarball, then npm fallback) and the
  bundled-JS sanity guard are the contract — preserve both tiers.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
