---
layout: default
title: FAQ
description: "Frequently asked questions about Visio-Azure: licensing, Visio version support, commercial use, how it compares to other Azure stencils, and how to contribute."
---

# Frequently Asked Questions

## General

### Is this an official Microsoft product?

No. Microsoft owns the **Azure service icons** themselves. This project is a community-built Visio stencil set wrapping those icons with the connection points, shape data, sizing, and search keywords that Microsoft's own publishing format (flat SVG) doesn't include. The icons are used with Microsoft's permission for community redistribution and are subject to Microsoft's usage terms (free for diagrams, attribution required for icon design).

### How is this different from the David-Summers/Azure-Design stencils?

Visio-Azure is a ground-up replacement. The older David-Summers/Azure-Design stencils were built with PowerShell + Visio COM, which required a Windows-with-Visio install just to *build* the stencil and shipped with a long-standing broken-search bug. Visio-Azure is cross-platform Python that emits the OOXML directly, ships with working search, and has comprehensively swept out the rendering bugs those stencils carried for years. It keeps the same icons and names, so it drops straight in. See [Release Notes](releases) for the full list.

### Why GPL-3 and not MIT?

GPL-3 is compatible with the Microsoft icon usage terms and prevents the stencil from being relicensed under a more restrictive licence by downstream consumers -- the work stays free for everyone who builds on it.

### Can I use these in a commercial diagram / book / course?

Yes. GPL-3 explicitly permits commercial use; the only requirement is to preserve attribution (to both Microsoft for the icon design and this project for the packaging).

## Installation and use

### What Visio versions are supported?

- Visio for Microsoft 365 (Windows + Mac)
- Visio 2024 / 2021 / 2019 desktop
- Visio Plan 1 and Plan 2

**Not** supported: Visio for the Web (it cannot render custom .vssx stencils, regardless of source).

### How do I install the stencil permanently so it's available in every drawing?

Drop the `.vssx` into your **My Shapes** folder:

- Windows: `%USERPROFILE%\Documents\My Shapes`
- macOS: `~/Library/Group Containers/UBF8T346G9.Office/User Content/My Shapes`

Restart Visio; the stencil appears under **More Shapes → My Shapes**.

### Shape search isn't returning anything

Three things to try, in order:

1. Verify it's not just this stencil -- type something into the search box that should match a Visio built-in (e.g. `process` or `rectangle`). If nothing comes back, your Visio's shape search is disabled; see [Enabling Search](enabling-search) for the toggle.
2. Reopen the stencil. Visio caches its keyword index; freshly-installed stencils sometimes need a one-time reopen to re-index.
3. Re-download the stencil. A truncated download can leave the keyword index missing.

### My icons are tiny / different sizes

This was a real bug in the legacy build but is fixed in V-5.0. If you're seeing it on a fresh V-5.0 download, please open an issue with a screenshot and the icon name -- it's worth investigating.

### Can I edit / customise a master?

Yes -- right-click any master in the Shapes panel → **Edit Master**. Be aware that editing a master rebuilds its shape sheet and you'll lose the precise connection-point formulas and shape-data fields. The recommended approach is to drag the master onto a drawing and edit the dropped instance.

## Sponsorship and assets

### Do I need to sponsor to use the stencils?

No. The `.vssx` files in this repo are free and complete -- they're everything you need to use the icons inside Visio.

### Why sponsor, then?

If the stencils save you time and you appreciate the work, sponsoring helps keep the set maintained as Microsoft refreshes its Azure icons. A separate **Premium** set (per-icon SVG/PNG files and styled Visio variants) is **coming soon**; sponsoring is the best way to register interest. See [Sponsorship](sponsorship).

## Contributing

### How do I report a wrong-looking icon?

Open an issue at <https://github.com/xeeva/Visio-Azure/issues> with:

- The icon name
- A screenshot of how it renders in Visio
- The source PNG (in `cleaned/png/` of any release; you can also find it on the Microsoft Azure icon page)

### How do I request a new icon?

If Microsoft has published an SVG for the service, link to it in a new issue. If they haven't, the request gets parked until they do -- the project policy is "ship what Microsoft publishes" rather than authoring new designs.

### Can I contribute fixes?

Pull requests welcome on the **build pipeline** at <https://github.com/xeeva/visio-azure> (the lowercase / dev repo). This repo (the release / asset distribution) is downstream output -- to fix something you fix the pipeline, then a new build replaces this repo's contents.

## Technical

### Is the build pipeline open-source too?

Yes -- the cross-platform Python pipeline that produces these stencils lives at <https://github.com/xeeva/visio-azure>. Cross-platform, no Visio install required to build, 32-test pytest suite.

### Why not Draw.io / Mermaid / Lucidchart?

Visio is what enterprise architecture documentation tends to land in. The combination of pixel-precise connection-point control, Shape Data binding (for programmatic round-tripping with Azure), and the breadth of legacy / corporate templates means Visio still owns this niche. This project respects that.

### How is the broken-search fix verified?

Every build runs a `verify` step that asserts the keyword cells are present in all six required OOXML locations on every master. The build fails if a single master is missing the cells. See `src/visio_azure/verify.py` in the pipeline repo.

### Are the builds reproducible?

Yes. Same `Icon-Source` directory produces byte-identical `.vssx` files. ZIP timestamps fixed at 1980-01-01; file lists sorted; no PIDs or wall-clock data in outputs. The `BUILD_REPORT.html` in each release folder includes SHA-256 hashes of every artefact.
