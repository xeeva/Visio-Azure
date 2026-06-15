---
layout: default
title: Release Notes
---

# Release Notes

## V-5.0 -- 2026-05-16

First release of the rewritten cross-platform Python build pipeline. Drops the PowerShell + Visio-COM dependency entirely; emits the OOXML directly. Every fix landed against the legacy pipeline carries forward, plus a comprehensive sweep surfaced through end-to-end visual inspection against Visio's own PNG export.

### Headline changes

- **Shape search works.** Keywords now written in every cell Visio indexes -- the legacy `ShapeKeywords` PageSheet cell, plus `Master/Prompt`, `Master/Description`, document-level `Keywords` in `docProps/app.xml`, and `dc:subject` in `docProps/core.xml`. Type `vmss` or `key vault` into the Shapes panel and the masters now surface immediately. See [Enabling Search](enabling-search).
- **Uniform icon size.** Many Microsoft SVGs declare a viewBox much larger than the painted content. The legacy pipeline scaled the declared viewBox to 20 mm, so half the icons came out at 8-12 mm. V-5.0 uses the union of path bounding boxes as the effective viewBox; every icon's painted area now fills its 20 mm cell.
- **Translucent overlays render translucent.** Reads SVG `opacity` and `fill-opacity` from element attributes, inline `style="..."`, **and** embedded CSS classes -- the form Visio-exported SVGs use heavily. Affects 394 icons that contain `<path opacity=".5">` or `.stN {fill-opacity:0.75}` overlays modelling depth and lighting.
- **Gradients render as gradients.** Adds `FillPattern=25` (linear gradient) or `26` (radial) to every gradient-bearing leaf. The legacy stencils set `FillGradientEnabled=1` and the FillGradient section, but without `FillPattern` Visio fell back to solid first-stop colour for every gradient -- meaning every "blue dashboard tile", "gradient cube face", and "soft fade body" rendered as a flat dark blue instead.
- **`gradientTransform` honoured.** 421 icons rotate their gradient direction with `gradientTransform="rotate(...)"`. The legacy pipeline read `x1,y1,x2,y2` directly and ignored the transform, so the gradient pointed the wrong way. Affects Function App Service Editor's brackets and many other icons that author dark/light shading by rotating an axis-aligned gradient.
- **Rotated primitives stay rotated.** `<path transform>` was always reified by `svgelements`, but `<rect transform>`, `<circle transform>` and friends were not. The slash through Function App Service Editor's bracket pair (a `<rect transform="rotate(17.752)">`) used to render as an upright vertical bar. Now reified explicitly.
- **3-digit hex (`#fff`) expanded to 6-digit.** Visio's `FillForegnd` silently renders `#fff` as `#000000`. Every icon with a `fill="#fff"` "white screen" overlay (Intune Managed Desktop, Jenkins's face, PowerShell's prompt, hundreds of others) used to be rendered with a black rectangle in the middle.
- **Masked icons render correctly.** Seven Dynamics 365 Mixed Reality icons wrap their visible content in `<g mask="url(#m)">`. The mask itself contains a path. `svgelements` iterates that mask path; the lxml-based fill index didn't. Result: every visible path's fill was shifted by one and the final cube layer fell off the end of the colour table, falling back to solid black. The seven Mixed Reality icons went from black silhouettes to proper coloured gradient cubes.
- **Paths inside `<defs>` / `<clipPath>` / `<pattern>` excluded from the fill index** while paths inside `<mask>` / `<symbol>` / `<marker>` are included (matching svgelements' iteration exactly). Affects 51 icons including the Cosmos DB Dedicated Gateway (which used to render with grey arrows wearing the gradient body's fill, the gradient body losing its fill, the cyan top wearing the gradient, and the white lightning bolt entirely missing).
- **Test drawing now uniformly sized.** The per-build preview drawing (a single page with every icon in a grid) renders every icon at the same scale for at-a-glance review.

### Per-master contract

Every master ships with the configuration covered in [Icon Features](icon-features). The values are pinned in `src/visio_azure/ooxml/geometry.py` as named constants in the build pipeline; nothing inlined.

### Drawing-resources companion

Inherits the legacy 84-master hand-authored stencil verbatim plus:

- **Three new GlowLine colours:** Purple (#9933FF), Orange (#FF8C00), White (#FFFFFF).
- **Three new GlowBox colours:** same three.
- **Three new single-end connector arrows:** `I_Arrow-Single-01`, `I_Arrow-Dashed-01`, `I_Arrow-Thick-01`. The existing `C_PathLine-01..10` masters are all double-headed -- these complement them.

Total drawing-resources masters: 84 → 104.

### Build pipeline

- Cross-platform Python (no Visio install required).
- Deterministic output -- identical input produces byte-identical `.vssx`.
- 32-test pytest suite covering the geometry, scaling, and search-cell contracts.
- Visual round-trip diff harness reports any per-icon drift from source to built.

### Group counts

| Group | Masters |
| --- | --: |
| AI | 101 |
| Application | 214 |
| Compute | 246 |
| Data | 146 |
| Deployment | 51 |
| Dynamics 365 | 35 |
| Endpoint | 37 |
| Generic | 77 |
| Identity | 76 |
| IoT | 45 |
| Management | 329 |
| Networking | 164 |
| Office365 | 38 |
| Security | 95 |
| Storage | 57 |
| Workload | 31 |
| Workload-Service | 22 |
| **Total** | **1,764** |

Three SVGs in the source corpus were skipped because they contain no renderable paths (Microsoft authoring artefacts): `Cognitive Services Knowledge`, `O365 - Power Automate`, `Storage Account Blob`.

## V-4.7 -- 2024-09

Final release of the legacy PowerShell + Visio-COM pipeline at [David-Summers/Azure-Design](https://github.com/David-Summers/Azure-Design). 1,233 icons. Broken shape search. Intermittent rendering issues on icons with translucent overlays, rotated primitives, or gradient fills. Preserved for download but no longer maintained.

## Earlier versions

Earlier releases are still available at the original repo: <https://github.com/David-Summers/Azure-Design/releases>.
