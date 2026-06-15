---
layout: default
title: Metric vs US Units
description: "Metric or US? Why Visio-Azure ships two unit builds, how a mismatch breaks shape search and icon sizing, and how to pick the stencil that matches your drawing."
---

# Metric vs US units: which stencil set to download

Visio-Azure ships **two complete, identical icon sets**. They differ in exactly one thing: the internal **measurement unit** each stencil is authored in. Pick the one that matches the drawing you work in and everything drops at the right size, snaps to the grid, and reports sensible dimensions.

> **TL;DR:** Work in **cm / mm**? Take **Metric** (`_m`, the `Stencil-Metric/` folder). Work in **inches / feet**? Take **US** (`_u`, the `Stencil-US/` folder). The artwork is the same either way.

## Why are there two stencils?

A Visio master stores its geometry in real-world units. When you drag a master onto a page, Visio places it at that physical size and then displays its dimensions in **the page's** measurement units.

- A master authored at **20 mm** dropped onto a **metric** page reads as a clean *20 mm* and lines up with a millimetre grid.
- The same number interpreted on a **US (inches)** page does not land on a tidy imperial value, so the icon can arrive at an awkward physical size and its Shape Data measurements read oddly (e.g. *0.787 in* instead of a round figure).

Rather than force one world onto the other, we build each stencil twice:

| Build | Suffix | Folder | Authored in | Page scale |
| --- | --- | --- | --- | --- |
| **Metric** | `_m` | `Stencil-Metric/` | millimetres | metric (mm / cm) |
| **US** | `_u` | `Stencil-US/` | inches | US (in / ft) |

Everything else: the artwork, the nine connection points, the seven Shape Data fields, the caption placement, and the search keywords, is **byte-for-byte the same intent** in both. Only the unit system and page scale change.

## The unit suffix also gates Visio's shape search

The `_m` and `_u` suffixes are **load-bearing for search**, not just for sizing. Visio's Shapes-pane search only surfaces `_m` stencils when the active page uses metric units, and only surfaces `_u` (or unsuffixed) stencils when the page is in US units.

This means a unit mismatch makes the **entire stencil invisible to search**: not just wrong-sized on drop. If you load a `_m` stencil and your page is in US units (or vice versa), typing any icon name into the Shapes panel will return nothing from that stencil, even though you can still drag icons manually.

Check your page units **before** loading the stencil:

**Design → Page Setup → Page Properties → Measurement units**

- Shows **Millimetres / Centimetres** → load `_m` stencils from `Stencil-Metric/`.
- Shows **Inches / Feet** → load `_u` stencils from `Stencil-US/`.

## How do I know which my Visio uses?

A quick rule of thumb: most of the world (Australia, Europe, UK, NZ, most of Asia) defaults to metric. The United States and a few imperial-template workflows default to US. The unit usually follows the template you started your drawing from, not your Windows locale, so check the drawing itself.

## Download

<div markdown="1">

### Metric (millimetres / centimetres)

- **[Metric stencils: all groups (.zip)](https://github.com/xeeva/Visio-Azure/raw/main/Visio-Azure-Stencils-Metric-V1.zip)**
- [All-Icons only](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_All-Icons_V-5_m.vssx) · [Drawing resources](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Drawing-Resources_V-5.vssx) · [browse the `Stencil-Metric/` folder](https://github.com/xeeva/Visio-Azure/tree/main/Stencil-Metric)

### US (inches / feet)

- **[US stencils: all groups (.zip)](https://github.com/xeeva/Visio-Azure/raw/main/Visio-Azure-Stencils-US-V1.zip)**
- [All-Icons only](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_All-Icons_V-5_u.vssx) · [Drawing resources](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Drawing-Resources_V-5.vssx) · [browse the `Stencil-US/` folder](https://github.com/xeeva/Visio-Azure/tree/main/Stencil-US)

</div>

Each zip contains all 11 group stencils, the All-Icons stencil, and the drawing-resources companion for that unit system.

## "I downloaded the wrong one"

No harm done. The icons will still draw; they'll just be sized for the other unit system, and search will return nothing from those stencils on your active page. Delete the stencil from your **Shapes** panel, grab the matching build, and re-drop. Because both sets carry identical names and search keywords, your existing search habits carry straight over.

## Can I mix both in one drawing?

Stick to one unit system per drawing. Mixing a metric stencil and a US stencil on the same page means two different physical scales on one canvas, which defeats the [uniform 20 mm sizing](icon-features#twenty-millimetre-normalised-size). Pick the set that matches your page and use it throughout.

---

Next: [Setup guide](getting-started){: .btn } [Icon features](icon-features){: .btn } [Enabling search](enabling-search){: .btn }
