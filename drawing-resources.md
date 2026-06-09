---
layout: default
title: Drawing Resources
---

# Drawing Resources

`Azure_Drawing-Resources_V-5.vssx` ships alongside the icon set (in both the `Stencil-Metric/` and `Stencil-US/` folders) as a companion stencil with 93 hand-authored shapes for annotating diagrams: dashed boxes, lines of every flavour, callouts, bubbles, glow effects, and connector arrows.

## Contents

### Containers and outlines

| Category | Variants | Use |
| --- | --- | --- |
| **A_DashBox** | 10 styles | Dashed bounding box around a logical group of icons |
| **F_Bubble** | 10 styles | Speech-bubble / annotation pop-out |

### Connectors

| Category | Variants | Use |
| --- | --- | --- |
| **B_Line** | 10 styles | Plain straight lines (no arrowheads) |
| **C_PathLine** | 10 styles | Right-angle path lines, double-headed arrows |
| **D_AngleLine** | 10 styles | Single-bend angled lines |
| **E_ArcLine** | 10 styles | Curved arc lines |
| **I_Arrow** | 3 styles | Single-end arrows: Single, Dashed, Thick |

### Callouts

| Category | Variants | Use |
| --- | --- | --- |
| **E_Callout** | 10 styles | Boxed annotations with leader lines |

### Glow effects

| Category | Variants | Use |
| --- | --- | --- |
| **G_GlowLine** | 9 colours | Coloured glow halos along a line: Red, Green, Blue, Yellow, Teal, Pink, **Purple**, **Orange**, **White** |
| **H_GlowBox** | 9 colours | Coloured glow halo around a box: same nine colours |

The three colours in **bold** are new in V-5.

### Palettes

| Category | Variants | Use |
| --- | --- | --- |
| **Z_Colours-01** | Single reference master | Visio colour palette swatch for picking consistent fills |
| **Z_Gradients-01** | Single reference master | Visio gradient palette swatch |

### Azure-Arc style set (new in V-5)

A coherent dark-theme palette reverse-engineered from the official Microsoft Azure Arc-enabled data services architecture diagram. Use to author diagrams that match the Microsoft Learn / Azure Docs visual language.

| Master | Visual | Use |
| --- | --- | --- |
| **J_Arc-Container-Navy-01** | Navy `#152549` fill, cyan `#00d4ff` border, cyan glow halo | Dark-theme grouping container -- the "Azure", "Azure Stack HCI", ... cards in Microsoft Arc diagrams. |
| **J_Arc-Container-Steel-01** | Slightly lighter `#1b3357` fill, brighter cyan border | Nested container inside a Container-Navy for visual hierarchy. |
| **J_Arc-Scope-Red-01** | Red `#dc3545` dashed border, transparent fill | "This area is Azure Arc enabled" scope marker -- the red dashed rectangle in the source diagram. |
| **J_Arc-Scope-Cyan-01** | Cyan `#00b8e6` dashed border, transparent fill | Generic logical-grouping scope marker. |
| **J_Arc-Connector-CyanGlow-01** | White line with cyan glow halo | Connector lines between dark containers -- pops visually against navy backgrounds. |
| **J_Arc-Connector-CyanThin-01** | Thin solid cyan line, no glow | Minimal connector for high-density node graphs. |
| **J_Arc-PlatformBar-Azure-01** | Solid Microsoft blue `#0078D4` | Bottom-row platform banner -- "Azure" footer. |
| **J_Arc-PlatformBar-AWS-01** | Solid Amazon orange `#FF9900` | "Amazon Web Services" footer. |
| **J_Arc-PlatformBar-GCP-01** | Solid Google blue `#4285F4` | "Google Cloud Platform" footer. |
| **J_Arc-PlatformBar-VMware-01** | Solid VMware grey-blue `#607078` | "VMware vSphere" footer. |
| **J_Arc-PlatformBar-Dark-01** | Solid navy `#152549` with cyan border | Generic dark-theme banner / header strip. |

**Composing a diagram in this style:** drop platform bars across the bottom, stack Container-Navy or -Steel boxes for the service groups, connect them with Connector-CyanGlow lines, and use a Scope-Red rectangle to mark the Arc-enabled region.

## Using the connector arrows

The new **I_Arrow** masters are 1-D connector shapes -- you drop one onto the canvas, grab its endpoints, and drag them onto the connection points of two icons. The line bridges the icons; the filled-triangle arrowhead sits at the End anchor.

If you find yourself wanting a curved arrow, glue a **C_PathLine** between two icons -- the legacy "PathLine" masters are all double-headed arrows.

## Glow shapes for emphasis

Drop a **H_GlowBox-Red-01** behind a group of icons to highlight them in a red halo. The glow size is configurable via the shape's right-click → **Edit shape data** if you want it tighter or looser. Pair with a matching **G_GlowLine** of the same colour for a connector that visually "ties" two highlighted areas.

## Origin

The drawing-resources stencil is a hand-authored collection of annotation tools, extended in V-5 with the new colour and arrow variants. It's regenerated as part of the build alongside the icon stencils.

If you have a request for a new variant (different glow colour, specific connector style, a custom callout), open a [Discussion](https://github.com/xeeva/Visio-Azure/discussions).
