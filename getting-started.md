---
layout: default
title: Getting Started
---

# Getting Started

A step-by-step walk-through from download to first diagram.

## Requirements

- **Microsoft Visio** -- Plan 1, Plan 2, or any of the Visio 2019 / 2021 / 2024 desktop editions. Visio for the Web is **not** supported (it cannot render custom .vssx stencils).
- **Windows** or **macOS** -- the stencil is OOXML so it loads cleanly on either.
- ~35 MB of disk space for the full set in one unit system.

## 1. Pick your units

Visio-Azure ships in two identical sets that differ only in measurement units. **Choose one before downloading:**

- **Metric** (`_m`, the `M/` folder) -- if your Visio drawings use centimetres / millimetres.
- **US** (`_u`, the `U/` folder) -- if they use inches / feet.

Not sure? **Design → Page Setup → Measurement units** in Visio. [Full explanation →](units)

## 2. Download

### The full set (recommended)

A single zip of every stencil -- all 17 groups, the all-icons stencil, and the drawing-resources companion -- for your unit system:

- **[Metric — Visio-Azure-Stencils-Metric-V5.zip](https://github.com/xeeva/Visio-Azure/raw/main/Visio-Azure-Stencils-Metric-V5.zip)** (≈ 17 MB)
- **[US — Visio-Azure-Stencils-US-V5.zip](https://github.com/xeeva/Visio-Azure/raw/main/Visio-Azure-Stencils-US-V5.zip)** (≈ 17 MB)

### Just the all-icons stencil

One file, every icon:

- Metric: [`M/Azure_All-Icons_V-5_m.vssx`](https://github.com/xeeva/Visio-Azure/raw/main/M/Azure_All-Icons_V-5_m.vssx)
- US: [`U/Azure_All-Icons_V-5_u.vssx`](https://github.com/xeeva/Visio-Azure/raw/main/U/Azure_All-Icons_V-5_u.vssx)

### A specific category

If you only design for one part of Azure, grab just that group from the [`M/`](https://github.com/xeeva/Visio-Azure/tree/main/M) (metric) or [`U/`](https://github.com/xeeva/Visio-Azure/tree/main/U) (US) folder. Each holds all 17 group stencils:

`AI · Application · Compute · Data · Deployment · Dynamics 365 · Endpoint · Generic · Identity · IoT · Management · Networking · Office365 · Security · Storage · Workload · Workload-Service`

The drawing-resources companion (`Azure_Drawing-Resources_V-5.vssx`) is in both folders. A grid preview of every icon at true size is in [`Azure_All-Icons-Preview_V-5.vsdx`](https://github.com/xeeva/Visio-Azure/raw/main/Azure_All-Icons-Preview_V-5.vsdx).

## 3. Install

Two options. The first is faster; the second persists across drawings.

### Open on demand

Double-click any `.vssx`. Visio opens it in the **Shapes** panel on the left for the current drawing only.

### Add to your My Shapes folder

Drop the `.vssx` into your Visio **My Shapes** directory:

**Windows:** `%USERPROFILE%\Documents\My Shapes`

**macOS:** `~/Library/Group Containers/UBF8T346G9.Office/User Content/My Shapes`

Restart Visio. The stencil now appears under **More Shapes → My Shapes**, available in every drawing.

## 4. Drop your first icon

1. In Visio, open your drawing (or **File → New → Blank Drawing**).
2. Open the Visio-Azure stencil if it isn't already in your **Shapes** panel.
3. Drag any icon onto the canvas.
4. Hover near an edge of the icon -- one of the nine connection points (the small blue ×) becomes active.
5. Draw a connector from that anchor to another icon's anchor. The connector glues to the exact point, not the icon's bounding box.

## 5. Search for services

Type any service name into the search box at the top of the Shapes panel. Try `vmss`, `key vault`, `cosmos db`, `front door`. The legacy community stencils had a long-standing bug here -- the [Enabling search](enabling-search) page covers why, what's fixed, and what to do if your Visio's shape search needs to be turned on first.

## 6. Dark backgrounds

Designing on a dark theme or onto dark-filled shapes? The 27 solid-black logos each ship a white `-DM` twin. Search for the icon name plus `-DM` (e.g. `OpenAI -DM`, `GitHub -DM`) to find it.

## Next steps

- **[Metric vs US units](units)** -- which set to use and why there are two
- **[Icon features](icon-features)** -- the full list of what each master ships with
- **[Drawing resources](drawing-resources)** -- the companion stencil with annotation shapes
- **[Sponsorship](sponsorship)** -- how to get the SVG and PNG asset files
