---
layout: default
title: Drawing Resources
---

# Drawing Resources

`Azure_Drawing-Resources_V-5.0.vssx` ships alongside the icon set as a companion stencil with 93 hand-authored shapes for annotating diagrams: dashed boxes, lines of every flavour, callouts, bubbles, glow effects, and connector arrows.

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

The three colours in **bold** are new in V-5.0.

### Palettes

| Category | Variants | Use |
| --- | --- | --- |
| **Z_Colours-01** | Single reference master | Visio colour palette swatch for picking consistent fills |
| **Z_Gradients-01** | Single reference master | Visio gradient palette swatch |

## Using the connector arrows

The new **I_Arrow** masters are 1-D connector shapes -- you drop one onto the canvas, grab its endpoints, and drag them onto the connection points of two icons. The line bridges the icons; the filled-triangle arrowhead sits at the End anchor.

If you find yourself wanting a curved arrow, glue a **C_PathLine** between two icons -- the legacy "PathLine" masters are all double-headed arrows.

## Glow shapes for emphasis

Drop a **H_GlowBox-Red-01** behind a group of icons to highlight them in a red halo. The glow size is configurable via the shape's right-click → **Edit shape data** if you want it tighter or looser. Pair with a matching **G_GlowLine** of the same colour for a connector that visually "ties" two highlighted areas.

## Origin

The drawing-resources stencil is the same hand-authored collection that shipped with the legacy Azure-Design stencils (now archived) for years -- vendored verbatim in V-5.0 plus the new colour and arrow variants. The legacy file is preserved in the build pipeline's `resources/Stencil-Drawing-Resources-source.vssx` and the extended copy is regenerated via `scripts/extend_drawing_stencil.py`.

If you have a request for a new variant (different glow colour, specific connector style, a custom callout), open a [Discussion](https://github.com/xeeva/Visio-Azure/discussions).
