---
layout: default
title: Release Notes
---

# Release Notes

## V-5 -- 2026-06-09

Repackaged and expanded. The headline change is **dual-unit packaging**: every stencil now ships in a **Metric** (`_m`) and a **US** (`_u`) build so icons drop at the correct real-world size whatever your Visio drawing uses. See [Metric vs US units](units).

### Added

- **Metric and US builds.** Organised into `M/` and `U/` folders, each with a one-click zip (`Visio-Azure-Stencils-Metric-V5.zip`, `Visio-Azure-Stencils-US-V5.zip`) and the drawing-resources companion. Identical artwork, connection points, shape data, and search in both -- only the unit system differs.
- **27 dark-mode (`-DM`) variants.** Every all-black monochrome logo (Azure OpenAI, GitHub, Kafka, App Service / VM / SQL action glyphs, Resource Lock, BitLocker Key, …) now has a white-fill twin suffixed `-DM`, detected automatically across the corpus. The recolour is real fill geometry, so it scales cleanly at any size. Use the original on light canvases, the `-DM` twin on dark. See [Icon Features](icon-features#dark-mode-dm-variants).
- **14 new API Management icons** -- API Center, Workspace, MCP Server, Credential Manager, Backend, Named Value, Policy Fragment, Power Platform, Pricing Tier, Product, Schema, Location, and more.

### Changed

- **API Management naming consolidated.** Removed duplicate `APIM …` icons in favour of the canonical `API Management …` names, and refreshed the API Management Service icon to the newer brighter Azure styling.
- **Custom Workload / Workload-Service icons rescaled.** These on-prem / IaaS shapes previously filled only ~32-44% of their frame (about a third the size of the Azure icons) because their viewBox carried excess padding. Their viewBoxes were tightened to ~85% fill so they now match the Azure icons exactly.
- **1,773 masters** across 17 groups (was 1,259).

### Known issues

- `Office365 — Word` does not render in the preview export (an XML-entity quirk in the source SVG); the stencil master itself is unaffected.
- Three source SVGs remain skipped as before (no renderable paths): `Cognitive Service Knowledge`, `O365 - Power Automate`, `Storage Account Blob`.

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

Total drawing-resources masters: 84 → 93.

### Build pipeline

- Cross-platform Python (no Visio install required).
- Deterministic output -- identical input produces byte-identical `.vssx`.
- 32-test pytest suite covering the geometry, scaling, and search-cell contracts.
- Visual round-trip diff harness reports any per-icon drift from source to built.

### Group counts

| Group | Icons |
| --- | --: |
| AI | 102 |
| Application | 234 |
| Compute | 156 |
| Data | 67 |
| Deployment | 38 |
| Dynamics 365 | 56 |
| Endpoint | 32 |
| Generic | 18 |
| Identity | 48 |
| IoT | 24 |
| Management | 73 |
| Networking | 102 |
| Office365 | 28 |
| Security | 49 |
| Storage | 55 |
| Workload | 75 |
| Workload-Service | 38 |
| Iot (legacy spelling) | 4 |
| **Total** | **1,259** |

Three SVGs in the source corpus were skipped because they contain no renderable paths (Microsoft authoring artefacts): `Cognitive Services Knowledge`, `O365 - Power Automate`, `Storage Account Blob`.

## V-4.7 -- 2024-09

Final release of the legacy PowerShell + Visio-COM pipeline. 1,233 icons. Broken shape search. Intermittent rendering issues on icons with translucent overlays, rotated primitives, or gradient fills. Preserved for download but no longer maintained.

## Earlier versions

The pre-V-5.0 stencils were maintained at a now-archived repository. They are superseded by V-5.0.
