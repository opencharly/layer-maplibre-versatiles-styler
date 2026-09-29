# layer-maplibre-versatiles-styler

The MapLibre VersaTiles styler control, bundled locally into the image so the map
UI loads it without runtime CDN access, as a standalone OpenCharly layer repo.

`maplibre-versatiles-styler` is a MapLibre GL JS control that adds an interactive
sidebar widget for switching between VersaTiles style presets, editing color
palettes, and adjusting fonts/language. The candy installs the npm package
(GitHub release tarball, with an npm-install fallback) into
`/opt/maplibre-versatiles-styler/`, shipping the prebuilt ESM + UMD bundles so the
notebook's MapLibre cell can load the styler from the image instead of
`unpkg.com` at runtime.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `maplibre-versatiles-styler` |
| Install path | `/opt/maplibre-versatiles-styler/` |
| Re-exported at | `/opt/versatiles-frontend/styler/` (by `layer-versatiles-frontend`) |
| Distros | `arch` + `fedora` |
| Build deps | nodejs, npm, curl, jq |
| Dependencies | `layer-supervisord` (transitive) |
| Service / port | none |

## How to use it

Compose the layer as a nested `candy:` list inside a named box body:

```yaml
my-map-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-maplibre-versatiles-styler:v2026.243.0409'
```

The bundled control is loaded in the notebook cell from `/styler/`:

```javascript
window.addEventListener('load', () => {
  if (window.VersaTilesStylerControl) {
    map.addControl(new window.VersaTilesStylerControl({ open: false }));
  }
});
```

## Layout

- `charly.yml` — the `maplibre-versatiles-styler:` candy entity (the
  release-tarball + npm-fallback plan step, the `check:` assertions, and the
  embedded `maplibre-versatiles-styler-skill:` skill entity).
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-versa:maplibre-versatiles-styler` — the control, its
  two-tier install, and its re-export path.
- `/charly-versa:versatiles-style` — the style generator whose output this control mutates.
- `/charly-versa:versatiles-frontend` — re-exports this bundle at `/styler/`.
- `/charly-versa:notebook-osm` — the shortbread MapLibre cell that attaches this control.
- `/charly-image:layer` — candy authoring reference.
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
