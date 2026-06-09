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

1. Download the **Metric** or **US** zip above (or just the [All-Icons stencil](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_All-Icons_V-5_m.vssx) for metric / [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_All-Icons_V-5_u.vssx)).
2. Double-click a `.vssx`. Visio opens it in the **Shapes** panel.
3. Drag an icon onto the canvas; hover near an edge to find a connection point; draw a connector to another icon's anchor.
4. Type a service name into the search box at the top of the Shapes panel -- the broken-search fix means it actually finds something.
5. On a dark canvas, search for the `-DM` twin of a black logo (e.g. `OpenAI -DM`) for a white version.

The [full setup guide](getting-started) covers Visio versions, importing the stencil into a custom My Shapes location, and how to turn on Visio's shape search if it isn't already.

## Built by a generation pipeline, not by hand

The whole set is **generated programmatically** -- scan → normalise → scale → emit OOXML → verify -- with every connection point, shape-data field, caption rule, search keyword, and unit variant applied automatically to all 1,773 masters and machine-checked against a per-master contract before it ships.

That's a step change from the earlier **PowerShell + Visio-COM** approach, which was Windows-only, drove a live Visio instance one shape at a time, and fixed broken icons by hand. The pipeline now handles the hard parts itself:

- **Shape search works** -- keywords written into every cell Visio indexes.
- **Uniform sizing** -- artwork fills its frame; padded source viewBoxes are tightened so nothing renders as a tiny dot.
- **Gradients, translucency, rotated primitives, masks, and `#fff` overlays** all render correctly, automatically.
- **Dark-mode `-DM` twins** generated for every all-black logo.
- **Cross-platform and deterministic** -- no Visio needed to build, and identical input produces byte-identical `.vssx`, so the set regenerates in seconds whenever the icons change.

The [release notes](releases) cover the full V-5 feature list.

## Get the asset files and styled variants

The `.vssx` stencils here are **free and GPL-licensed** -- download as many as you like. The **per-icon SVG and PNG files, and styled visual variants**, are part of **Premium** *(in build)*.

This split is deliberate. When the raw, easily-repackaged asset files were distributed freely, they were re-hosted and resold with the licence and attribution stripped -- so the functional stencils stay open and free, while the raw assets and styles are Premium. That's what keeps the project funded and maintained.

See [Premium & sponsorship](sponsorship) for what's included and how access is delivered.

## Found a problem, or want an icon?

- [Request an icon](https://github.com/xeeva/Visio-Azure/issues/new?template=icon_request.yml) -- missing a service? Ask.
- [Report a bug](https://github.com/xeeva/Visio-Azure/issues/new?template=bug_report.yml) -- a wrong-looking icon, search miss, or scaling glitch.
- [Discussions](https://github.com/xeeva/Visio-Azure/discussions) -- questions, ideas, and show-and-tell.
