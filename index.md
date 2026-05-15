---
layout: default
title: Visio-Azure
---

## The Problem

Microsoft maintains a comprehensive set of Azure service icons -- but they ship as flat SVGs designed for browser rendering, not as functional Visio masters. Dropping them onto a Visio canvas works visually, yet every productivity feature that makes Visio worth using disappears:

- Connectors snap to the icon edge or centre rather than a fixed N / E / S / W anchor.
- Captions land in the middle of the icon and have to be repositioned by hand on every drop.
- Import size depends on each icon's source viewBox -- one comes in at 9 mm, the next at 32 mm, and you spend more time resizing than designing.
- There's no shape data, so you cannot programmatically tag a master with the Azure resource metadata (ResourceId, SubscriptionId, ...) the icons represent.
- Shape search is broken in the legacy community stencils -- keywords were written into only one of the four cells Visio actually indexes, so typing **vmss** or **key vault** into the Shapes panel found nothing.

These shortcomings are the difference between *Azure icons inside Visio* and *an Azure stencil for Visio*.

## The Solution

**Visio-Azure** is a fully-equipped, programmatically-built Visio stencil set covering 1,259 Azure services and configuration items across 19 groups. Every master ships with:

- Nine named connection points (N / E / S / W / four corners / SouthOfText).
- A pre-positioned caption field that lives below the icon, capped to wrap on long names.
- 20 mm normalised sizing on the longer side so a drawing of 50 services looks like one drawing, not a collage.
- Seven Shape Data fields populated and ready for resource metadata.
- Working shape search -- keywords written into every cell Visio indexes.
- A 93-master drawing-resources companion stencil with annotation shapes, glow effects, connector arrows, and colour palettes.

[Setup guide](getting-started){: .btn } [Icon features](icon-features){: .btn } [Sponsor](https://github.com/sponsors/xeeva){: .btn }

## Quick Start

1. Download [`Azure_All-Icons_V-5.0.vssx`](https://github.com/xeeva/Visio-Azure/raw/main/stencils/V-5.0/Azure_All-Icons_V-5.0.vssx) from the release page.
2. Double-click the file. Visio opens it in the **Shapes** panel.
3. Drag an icon onto the canvas; hover near an edge to find a connection point; draw a connector to another icon's anchor.
4. Type a service name into the search box at the top of the Shapes panel -- the broken-search fix means it actually finds something.

The [full setup guide](getting-started) covers Visio versions, importing the stencil into a custom My Shapes location, and how to turn on Visio's shape search if it isn't already.

## What's New in V-5.0

A ground-up rewrite of the build pipeline -- cross-platform Python in place of PowerShell + Visio COM, OOXML emitted directly so no Visio install is needed at build time, plus a comprehensive sweep of rendering bugs that the legacy pipeline carried for years. Highlights:

- **Shape search works.** Keywords written in every cell Visio indexes.
- **Uniform sizing.** Icons whose painted content fills only a fraction of the declared viewBox no longer render as tiny dots.
- **Gradients render as gradients.** A missing `FillPattern=25` cell meant the legacy stencils rendered every gradient as a solid first-stop colour.
- **Translucent overlays work.** Reads `opacity` / `fill-opacity` from attributes, inline style, and embedded CSS classes.
- **Rotated primitives stay rotated.** `<rect transform="rotate(...)">` no longer renders axis-aligned.
- **Masked icons render correctly.** The seven Dynamics 365 Mixed Reality icons are no longer black silhouettes.
- **3-digit hex (`#fff`) expanded to 6-digit** so white screens stop rendering as black rectangles.
- **421 icons' gradient direction** corrected -- `gradientTransform` is now honoured.

The [release notes](releases) cover every fix.

## Get the Asset Files

The `.vssx` stencils in this repo are free and GPL-licensed -- download as many as you want. The per-icon SVG and PNG files, however, are sponsor-only. The previous Azure-Design repo distributed them freely and they were systematically re-hosted by other parties with attribution stripped. Moving the raw asset files behind a sponsor tier is what keeps this work maintained.

See [Sponsorship](sponsorship) for tiers, what each gets you, and how access is delivered.
