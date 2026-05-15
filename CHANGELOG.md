# Changelog

All notable changes to the Visio-Azure stencil set. Follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions are semantic-ish (`<major-icon-pack>.<release>`).

## [V-5.0] -- 2026-05-16

First release under the rewritten Python build pipeline. Carries every
fix from the legacy PowerShell+COM build plus a comprehensive set of new
ones surfaced through end-to-end visual inspection against Visio's
actual render output.

### Stencils
- **1,259 Azure service icons** across 19 groups (AI, Application, Compute, Data, Deployment, Dynamics 365, Endpoint, Generic, Identity, IoT, Management, Networking, Office365, Security, Storage, Workload, Workload-Service)
- **Azure_All-Icons_V-5.0.vssx** -- every master in one file
- **18 per-group stencils** for those who prefer the smaller files
- **Azure_Drawing-Resources_V-5.0.vssx** -- 93 hand-authored drawing tools (DashBox, Line, PathLine, AngleLine, ArcLine, Callout, Bubble, GlowLine ×9 colours, GlowBox ×9 colours, single/dashed/thick connector arrows, colour and gradient palettes)

### Fixed (relative to legacy V-4.7)
- **Shape search works.** Keywords now written in every cell Visio indexes -- `Master/@NameU`, `Master/Prompt`, `MasterContents/PageSheet/ShapeKeywords`, and the document-level `Keywords` / `dc:subject` in app.xml / core.xml. The legacy stencils set `Shapekeywords` only on the PageSheet of each master and that single cell isn't what Visio reads when you type into the Shapes panel search box.
- **Uniform icon size.** Every icon's painted area now fills its master cell. Many Microsoft SVGs declare a viewBox much larger than their content (e.g. content drawn in the central 50% of a 200×200 viewBox); the legacy pipeline scaled the declared viewBox to 20 mm so half of those icons came out at 10 mm. The new pipeline uses the union of path bounding boxes as the effective viewBox.
- **Translucent overlays render translucent.** Many Microsoft icons use 50%-75% opacity overlays to model depth (the bright lid on a database cylinder, the soft highlight on a bracket face). The legacy pipeline didn't read SVG `opacity`/`fill-opacity` from CSS classes; the new pipeline composes them across attribute, style and class cascades.
- **Gradients render as gradients.** The legacy stencils set the FillGradient section but not `FillPattern=25`, so Visio rendered every gradient leaf as the solid first-stop colour. Affected almost every Microsoft icon with a gradient body. Fix touches roughly 7,400 leaves in the build.
- **Rotated primitives render rotated.** `svgelements` reifies `<path transform>` into coordinates but leaves `<rect transform>` and `<circle transform>` unreified. The slash through Function App Service Editor's bracket pair (a `<rect transform="rotate(17.752)">`) rendered as an upright vertical bar. Now reified explicitly.
- **`gradientTransform` is honoured.** 421 icons carry an explicit rotation/scale on their gradient definition; the legacy pipeline ignored it so the gradient pointed the wrong direction.
- **3-digit hex (`#fff`) expanded to 6-digit.** Visio's FillForegnd cell silently renders `#fff` as `#000000`, turning every "white screen" overlay (Intune Managed Desktop, Jenkins icon, PowerShell prompt, ...) into a black rectangle.
- **Masked icons render correctly.** Icons that wrap their content in `<g mask="url(#m)">` (the seven Dynamics 365 Mixed Reality icons) had their visible-paths' fills shifted by one because the mask's own template path was being counted differently between svgelements and the lxml fill-resolver. Aligned the two iterations.
- **Path indices inside `<defs>` / `<clipPath>` no longer pollute the fill table.** Affected 51 icons including Application Enterprise Application (which now actually renders) and Azure Cosmos DB Dedicated Gateway (white lightning bolt, cyan top band, and gradient body now all present, not all shifted one slot down the colour table).

### Pipeline
- Cross-platform Python build. No Visio install required.
- Deterministic output: same `Icon-Source` produces byte-identical `.vssx` files.
- Visual-inspection harness compares every icon's source SVG against its built master XML and flags drift.
- Per-icon round-trip comparison report against the Visio-rendered PNG export.
- Duplicate detection: aHash-based clustering across the corpus, surface in an HTML report for visual review.

## [V-4.7] -- 2024-09

Final release of the legacy PowerShell + Visio-COM pipeline. Archived; superseded by this project. 1,233 icons, broken shape search, intermittent rendering issues on icons with translucent overlays or rotated primitives.
