---
layout: default
title: Enabling Search
---

# Enabling Visio Shape Search

Visio's **Shape Search** is the search box at the top of the Shapes panel. Typing anything into it does a full-text query across every open stencil's masters -- name, keywords, prompts, descriptions. When it works it's the single fastest way to find one of 1,259 icons.

The catch: the legacy community Azure stencils didn't write keywords into the cells Visio actually indexes, so shape search appeared **broken** for users on those stencils. Visio-Azure fixes this. But you also need Visio's own search feature enabled to make use of the fix.

## What we did to make search work

Every master in Visio-Azure carries the service name, group, and a handful of useful search terms written into **every** location Visio's indexer reads:

| Location | What's stored | Why it matters |
| --- | --- | --- |
| `Master/@NameU` and `@Name` | Display name | The canonical name visible in the panel |
| `Master/Prompt` | Comma-separated keyword string | Shape Search reads this directly |
| `MasterContents/PageSheet/Section[ShapeKeywords]/Row/Cell` | Legacy ShapeKeywords cell | Required for older Visio versions |
| `Master/Description` | Long-form description | Indexed in some Visio releases |
| Document-level `<Keywords>` in `docProps/app.xml` | All masters' keywords joined | Stencil-wide search |
| `<dc:subject>` in `docProps/core.xml` | Same as above | Backup index |

The legacy Azure-Design stencils (now archived) wrote keywords into only one of these (the PageSheet `ShapeKeywords` cell), which is **not** what Visio's shape search reads on modern Visio versions. Visio-Azure writes to all six.

## Verifying it works on your machine

1. Open any Visio-Azure stencil.
2. Click into the search box at the top of the **Shapes** panel.
3. Type **vmss** -- you should see *Virtual Machine Scale Set* show up immediately.
4. Try other shortcut queries: **key vault**, **cosmos**, **app gateway**, **front door**.

If nothing happens when you type, your Visio's search index may be off. The next section covers turning it on.

## Turning on Visio's shape search

Shape Search is on by default on most Visio installs. If your search box is missing or queries return nothing across **all** stencils (not just this one):

### Visio for Microsoft 365 (Windows)

1. **File → Options → Advanced**.
2. Scroll to **Shape Search**.
3. Check **Show Shape Search panel**.
4. **OK**.

### Visio 2019 / 2021 desktop

1. **File → Options → Advanced**.
2. Find **Shape search options**.
3. Ensure **Enable shape search** is checked, and (optionally) **Search Visio.com** if you also want the online catalogue.
4. **OK**.

### Visio for Mac

The Mac version of Visio has Shape Search built-in and visible by default in the Shapes panel. There is no toggle.

## Reindexing if results are stale

Visio caches its keyword index for performance. If you've just installed a fresh stencil and search results look stale:

1. **File → Close** the drawing.
2. Reopen Visio.
3. Open the stencil again -- the index rebuilds on first use.

On Windows you can also force a full reindex by deleting `%USERPROFILE%\AppData\Roaming\Microsoft\Visio\ShapeSearch.idx` and restarting Visio.

## Why the legacy stencils' search "worked but didn't"

The original PowerShell + Visio-COM pipeline set `Shapekeywords` on the **PageSheet** of each master. The PageSheet is the per-master settings sheet that holds size, fill style, layer membership, and miscellaneous cells. It looked like the right place to put keywords -- but Visio's shape-search indexer reads the `Prompt` attribute on the master element itself and the `Description`, *not* an arbitrary cell inside the PageSheet. So the keywords were stored, but never queried.

Visio-Azure writes the same keyword string to every reasonable location. If a future Visio version changes which cell its indexer reads, search will still work because the data is in all of them.

## Known issue: search may fail on metric-units pages

On some Visio installations (under investigation; first reported in Visio for Microsoft 365 on Windows), shape search returns no results when the active drawing's measurement units are set to **Metric**, but works correctly on the **same stencil** when the drawing is in **US units**.

### Workaround

Create the drawing in US units, search and drop the icons you need, then change the page to metric:

1. **File → New → Blank Drawing (US Units)**.
2. Open the Visio-Azure stencil. Search and drop icons normally.
3. **Design → Page Setup → Page Properties → Measurement Units → Millimetres**. (Or right-click the page tab → **Page Setup**.)

Existing dropped icons retain their geometry; subsequent drops are sized in mm.

### Why it happens

We don't have a confirmed root cause yet. The stencil's `PageScale` / `DrawingScale` cells are emitted with `V='0.03937007874015748' U='MM'` -- byte-for-byte identical to what Visio writes natively for a metric stencil and to what the legacy Azure-Design V-4.7 stencils used. Master attributes, keyword cells (`ShapeKeywords`, `Keywords`, `Prompt`, document-level `Keywords`), and PageSheet structure all match canonical Visio output.

This points at a Visio-side behaviour rather than a stencil bug, but we want to confirm before closing the investigation. If you can reproduce the issue, please add detail to the tracking issue at [github.com/xeeva/Visio-Azure/issues](https://github.com/xeeva/Visio-Azure/issues) including:

- Visio version (Help → About Microsoft Visio -- include the build number)
- OS and locale
- Whether the drawing was created from a metric template or converted later
- A screenshot of the empty search panel

## Still no results?

If you see `vmss` failing on Visio-Azure stencils specifically (not on Visio's built-in shapes), and you're already on a US-units drawing:

1. Re-download the stencil from the [releases page](https://github.com/xeeva/Visio-Azure/releases) -- a truncated download leaves the keyword index missing.
2. Force a Visio shape-search reindex by deleting `%APPDATA%\Microsoft\Visio\ShapeSearch.idx` and restarting Visio.
3. Open an issue at [github.com/xeeva/Visio-Azure/issues](https://github.com/xeeva/Visio-Azure/issues) with your Visio version, OS, and the search term that didn't return anything.
