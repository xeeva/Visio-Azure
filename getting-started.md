---
layout: default
title: Getting Started
description: "Download Visio-Azure, install it into Visio's My Shapes, and build your first Azure diagram: dropping icons, gluing connectors, searching, and dark mode."
---

# Getting Started

A step-by-step walk-through from download to first diagram.

## Requirements

- **Microsoft Visio** -- Plan 1, Plan 2, or any of the Visio 2019 / 2021 / 2024 desktop editions. Visio for the Web is **not** supported (it cannot render custom .vssx stencils).
- **Windows** or **macOS** -- the stencil is OOXML so it loads cleanly on either.
- A few MB of disk space (the full-set zip is about 20 MB).

## 1. Download

**First, pick your units.** Visio-Azure ships in two identical builds: **Metric** (`_m`, for centimetre/millimetre drawings) and **US** (`_u`, for inch/feet drawings). Match the build to your drawing or icons drop at the wrong size and search can miss them. Unsure which you need? See [Metric vs US units](units).

### Just the all-icons stencil

The simplest place to start: one file, every Azure service.

- Metric: [`Azure_All-Icons_V-5_m.vssx`](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_All-Icons_V-5_m.vssx)
- US: [`Azure_All-Icons_V-5_u.vssx`](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_All-Icons_V-5_u.vssx)

### The full set

A ZIP of every stencil, including the per-group stencils and the drawing-resources companion.

- Metric: [`Visio-Azure-Stencils-Metric-V5.zip`](https://github.com/xeeva/Visio-Azure/raw/main/Visio-Azure-Stencils-Metric-V5.zip)
- US: [`Visio-Azure-Stencils-US-V5.zip`](https://github.com/xeeva/Visio-Azure/raw/main/Visio-Azure-Stencils-US-V5.zip)

### A specific category

If you only design for one part of Azure, grab just that group.

| Group | Metric | US |
| --- | --- | --- |
| AI | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_AI_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_AI_V-5_u.vssx) |
| Application | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Application_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Application_V-5_u.vssx) |
| Compute | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Compute_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Compute_V-5_u.vssx) |
| Data | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Data_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Data_V-5_u.vssx) |
| Deployment | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Deployment_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Deployment_V-5_u.vssx) |
| Dynamics 365 | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Dynamics%20365_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Dynamics%20365_V-5_u.vssx) |
| Endpoint | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Endpoint_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Endpoint_V-5_u.vssx) |
| Generic | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Generic_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Generic_V-5_u.vssx) |
| Identity | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Identity_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Identity_V-5_u.vssx) |
| IoT | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_IoT_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_IoT_V-5_u.vssx) |
| Management | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Management_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Management_V-5_u.vssx) |
| Networking | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Networking_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Networking_V-5_u.vssx) |
| Office365 | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Office365_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Office365_V-5_u.vssx) |
| Security | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Security_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Security_V-5_u.vssx) |
| Storage | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Storage_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Storage_V-5_u.vssx) |
| Workload | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Workload_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Workload_V-5_u.vssx) |
| Workload-Service | [Metric](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-Metric/Azure_Workload-Service_V-5_m.vssx) | [US](https://github.com/xeeva/Visio-Azure/raw/main/Stencil-US/Azure_Workload-Service_V-5_u.vssx) |

Browse the [`Stencil-Metric/`](https://github.com/xeeva/Visio-Azure/tree/main/Stencil-Metric) and [`Stencil-US/`](https://github.com/xeeva/Visio-Azure/tree/main/Stencil-US) folders for the full list of 17 group stencils plus the drawing-resources companion.

## 2. Install

Two options. The first is faster; the second persists across drawings.

### Open on demand

Double-click any `.vssx`. Visio opens it in the **Shapes** panel on the left for the current drawing only.

### Add to your My Shapes folder

Drop the `.vssx` into your Visio **My Shapes** directory:

**Windows:** `%USERPROFILE%\Documents\My Shapes`

**macOS:** `~/Library/Group Containers/UBF8T346G9.Office/User Content/My Shapes`

Restart Visio. The stencil now appears under **More Shapes → My Shapes**, available in every drawing.

## 3. Drop your first icon

1. In Visio, open your drawing (or **File → New → Blank Drawing**).
2. Open the Visio-Azure stencil if it isn't already in your **Shapes** panel.
3. Drag any icon onto the canvas.
4. Hover near an edge of the icon -- one of the nine connection points (the small blue ×) becomes active.
5. Draw a connector from that anchor to another icon's anchor. The connector glues to the exact point, not the icon's bounding box.

## 4. Search for services

Type any service name into the search box at the top of the Shapes panel. Try `vmss`, `key vault`, `cosmos db`, `front door`. Many other community stencils have a long-standing search gap here -- the [Enabling search](enabling-search) page covers why, what Visio-Azure fixes, and what to do if your Visio's shape search needs to be turned on first.

![Searching the Shapes panel for a service name and finding the matching Visio-Azure masters](images/example-search.png)

## Next steps

- **[Icon features](icon-features)** -- the full list of what each master ships with
- **[Drawing resources](drawing-resources)** -- the companion stencil with annotation shapes
- **[Sponsorship](sponsorship)** -- how to get the SVG and PNG asset files
