# Changelog

All notable changes to the Visio-Azure stencil set. Follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [V-5] -- 2026-06-09

The first public release of Visio-Azure: a complete, searchable, drop-in Azure stencil set for Microsoft Visio, **generated programmatically** and shipped in both **Metric and US measurement units**.

### Highlights

- **1,773 masters across 17 groups** -- Azure services, configuration items, and on-prem / IaaS workloads.
- **Dual-unit builds.** Every stencil ships in a Metric (`_m`) and a US (`_u`) variant, organised into `Stencil-Metric/` and `Stencil-US/`, each with a one-click zip and the drawing-resources companion. Identical artwork, connection points, shape data, and search in both -- only the unit system differs. See [Metric vs US units](https://xeeva.github.io/Visio-Azure/units).
- **Working shape search.** Keywords written into every cell Visio indexes -- `Master/@NameU`, `Master/Prompt`, the `ShapeKeywords` PageSheet cell, document-level `Keywords` in `docProps/app.xml`, and `dc:subject` in `docProps/core.xml` -- so typing `vmss` or `key vault` into the Shapes panel finds the master.
- **Nine connection points, seven shape-data fields, pre-positioned captions, 20 mm normalised sizing** on every master, applied uniformly and verified against a per-master contract.
- **27 dark-mode (`-DM`) variants.** Every all-black monochrome logo (Azure OpenAI, GitHub, Kafka, App Service / VM / SQL action glyphs, Resource Lock, BitLocker Key, …) ships a white-fill twin so it stays visible on a dark canvas. The recolour is real fill geometry, so it scales cleanly at any size.
- **Drawing-resources companion** -- dashed boxes, lines, callouts, bubbles, glow lines/boxes (9 colours), single/dashed/thick connector arrows, and colour palettes.

### How it's built

Generated end-to-end by a purpose-built pipeline -- scan → normalise → scale → emit OOXML → verify -- that is cross-platform (no Visio install required) and deterministic (identical input produces byte-identical `.vssx`). This replaces an earlier PowerShell + Visio-COM method that drove Visio one shape at a time on Windows and required hand-editing broken icons; the pipeline now detects and corrects gradient drift, padded viewBoxes, broken search cells, and dark-canvas invisibility automatically, and regenerates the entire set in seconds.

### Known issues

- `Office365 — Word` does not render in the preview export (an XML-entity quirk in the source artwork); the stencil master itself is unaffected.
- Three source icons are skipped as they contain no renderable paths: `Cognitive Service Knowledge`, `O365 - Power Automate`, `Storage Account Blob`.
