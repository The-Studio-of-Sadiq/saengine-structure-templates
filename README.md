# saengine-structure-templates

Structure templates for [SAEngine](https://github.com/The-Studio-of-Sadiq/SAEngine): presets of
its parametric shapes (space trusses, plane trusses, arches, domes, barrel vaults, cable nets)
for special structures, installable from the app's Packages page once it exists (marketplace
round M3) and applied through the modeller's Generate panel (M4). Each top-level folder is one
package: `<id>/pack.json` with `"kind": "structureTemplate"`, `templates/*.json` and a small
`preview.png`.

| Package | What it is |
| --- | --- |
| `saengine-shapes` | The presets of SAEngine's six built-in shapes and a few named variants. A **read-only mirror** of the package built into SAEngine (`mirrors.json` names the commit): change it in SAEngine, then copy it here with `scripts/marketplace/mirror_packages.py` there. |

A preset is `{"name": ..., "description": ..., "shape": {"kind": "planeTruss", ...}}`; the
`shape` is checked against SAEngine's shape models (`structure-template.schema.json` in
SAEngine's `python/src/saengine/codes/schemas/`). New shape kinds (bridges, towers...) need
Python generators and come in a later round (M5).

## Adding or changing a package

1. One folder per package, `templates/<name>.json` per preset, a `preview.png` of at most
   256 KB and 1024 px a side.
2. `licence`: an SPDX id, `CC-BY-4.0` by default.
3. Raise `version` whenever a published package changes.
4. Check locally: `saengine codepack validate <folder> --kind structureTemplate`.
5. Open a pull request; CI (defined once in
   [saengine-index](https://github.com/The-Studio-of-Sadiq/saengine-index)) checks each changed
   package.

## Publishing

A maintainer pushes a tag `packages-YYYY-MM-DD` on main; `.github/workflows/publish.yml` builds
the zips and `packages.json` and creates an immutable GitHub Release, which saengine-index lists
in its signed `index.json`. Running the workflow by hand is a dry run.
