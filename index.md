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
- They ship in a single unit system, so they drop at the wrong physical size onto a drawing that uses the other one.

These shortcomings are the difference between *Azure icons inside Visio* and *an Azure stencil for Visio*.

## The Solution

**Visio-Azure** is a fully-equipped, programmatically-built Visio stencil set covering **1,773 masters** across 17 groups -- Azure services, configuration items, and on-prem / IaaS workloads -- shipped in both **Metric** and **US** measurement units. Every master ships with:

- Nine named connection points (N / E / S / W / four corners / SouthOfText).
- A pre-positioned caption field that lives below the icon, capped to wrap on long names.
- 20 mm normalised sizing on the longer side so a drawing of 50 services looks like one drawing, not a collage.
- Seven Shape Data fields populated and ready for resource metadata.
- Working shape search -- keywords written into every cell Visio indexes.
- 27 dark-mode (`-DM`) variants of solid-black logos, so they stay visible on a dark canvas.
- A drawing-resources companion stencil with annotation shapes, glow effects, connector arrows, and colour palettes.

[Choose your units](units){: .btn } [Setup guide](getting-started){: .btn } [Icon features](icon-features){: .btn } [Sponsor](https://github.com/sponsors/xeeva){: .btn }

## Step 1: pick your units

Before downloading, decide which measurement system your Visio drawings use. We ship two identical sets:

| Your Visio drawing uses… | Download |
| --- | --- |
| **Centimetres / millimetres** (most of the world) | [Metric stencils (.zip)](https://github.com/xeeva/Visio-Azure/raw/main/Visio-Azure-Stencils-Metric-V5.zip) |
| **Inches / feet** (US templates) | [US stencils (.zip)](https://github.com/xeeva/Visio-Azure/raw/main/Visio-Azure-Stencils-US-V5.zip) |

Only the internal units differ -- the artwork, connection points, shape data, and search are identical. [Full explanation and how to check your units →](units)

## Quick Start

1. Download the **Metric** or **US** zip above (or just the [All-Icons stencil](https://github.com/xeeva/Visio-Azure/raw/main/M/Azure_All-Icons_V-5_m.vssx) for metric / [US](https://github.com/xeeva/Visio-Azure/raw/main/U/Azure_All-Icons_V-5_u.vssx)).
2. Double-click a `.vssx`. Visio opens it in the **Shapes** panel.
3. Drag an icon onto the canvas; hover near an edge to find a connection point; draw a connector to another icon's anchor.
4. Type a service name into the search box at the top of the Shapes panel -- the broken-search fix means it actually finds something.
5. On a dark canvas, search for the `-DM` twin of a black logo (e.g. `OpenAI -DM`) for a white version.

The [full setup guide](getting-started) covers Visio versions, importing the stencil into a custom My Shapes location, and how to turn on Visio's shape search if it isn't already.

## What's New in V-5

- **Metric *and* US-unit builds.** Pick the set that matches your drawing. [Why two?](units)
- **27 dark-mode `-DM` variants.** Solid-black logos (OpenAI, GitHub, Kafka, action glyphs, …) get a white-fill twin that stays visible on dark backgrounds.
- **Expanded API Management coverage** and consolidated naming (no more duplicate `APIM …` vs `API Management …`).
- **Rescaled custom Workload icons** so on-prem / IaaS shapes sit at the same visual size as the Azure icons.
- Plus the full V-5.0 rendering-correctness sweep below.

### Carried over from the V-5.0 pipeline rewrite

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

## Found a problem, or want an icon?

- [Request an icon](https://github.com/xeeva/Visio-Azure/issues/new?template=icon_request.yml) -- missing a service? Ask.
- [Report a bug](https://github.com/xeeva/Visio-Azure/issues/new?template=bug_report.yml) -- a wrong-looking icon, search miss, or scaling glitch.
- [Discussions](https://github.com/xeeva/Visio-Azure/discussions) -- questions, ideas, and show-and-tell.
