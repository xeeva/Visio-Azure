---
layout: default
title: Troubleshooting
---

# Troubleshooting

Diagnostic steps for the most-reported issues. If something here doesn't match what you're seeing, open an issue at [github.com/xeeva/Visio-Azure/issues](https://github.com/xeeva/Visio-Azure/issues) and include your Visio build number, OS, locale, and any logs you can gather.

## Shape search returns nothing on metric pages

**Symptom:** Open a fresh drawing with metric measurement units, type into the Shapes panel search box, no results come back. Switch the drawing to US units (or open a US-units drawing instead): the same search query immediately returns the expected icons.

**Workaround:** create the drawing in US units, drop the icons you need, then change the page to metric (**Design → Page Setup → Page Properties → Measurement Units → Millimetres**). Existing icons keep their geometry; later drops are sized in mm.

**Investigation:** the stencil's `PageScale` / `DrawingScale` / `DrawingSizeType` / `DrawingScaleType` cells match canonical Visio output byte-for-byte. The keyword cells (`ShapeKeywords`, `Keywords`, `Master/@Prompt`, document-level `Keywords` in `docProps/app.xml` and `dc:subject` in `docProps/core.xml`) are all populated. This appears to be Visio-side behaviour rather than a stencil bug; see the [Enabling Search](enabling-search) page's "Known issue" section for the full investigation notes.

If you can reproduce, please add detail to the tracking issue including: Visio build number (**Help → About Microsoft Visio**), OS and locale, and whether the drawing was created from a metric template or converted later.

## Search returns nothing for a specific term

**Symptom:** searching for a shape by name (for example, "Anycast Gateway" or "Border Node") returns no results, even though the stencil is open.

**Check the units page first.** If search works for other terms but not this one, the issue may be unit-mismatch rather than a missing keyword. See the section above and [Metric vs US units](units).

**Visio shipped-content suppression.** Visio suppresses My Shapes results for any term that also matches a shape in its own bundled stencils. For example, if Visio's built-in network stencil includes a shape whose keyword overlaps with "Secure Firewall ASA FTD v2", Visio may hide the My Shapes result entirely. This is Visio's own behaviour and no stencil-side counter-measure exists.

**Stale search cache.** Visio caches keyword indexes. After installing a new stencil into My Shapes, close Visio fully (check Task Manager: `VISIO.EXE` must not be running), then reopen. On the first open after install, Visio re-indexes the stencil.

**Re-download.** A truncated or partially-extracted download can leave the keyword cells absent. Re-download the release zip, re-extract, and reinstall.

## Stencil panel goes black after dropping an icon

**Symptom:** Open a stencil; the master previews render correctly in the Shapes panel. Drag an icon onto the drawing canvas. The Shapes panel goes mostly or entirely black: the master thumbnails disappear or render as solid black rectangles. The dropped icon on the canvas usually renders normally. Behaviour is **intermittent**: not every drop triggers it, and switching between stencils or resizing the panel often clears it.

This is a Visio renderer state issue, not corruption in the stencil itself. The masters are intact; the panel's cached preview surface gets invalidated and re-paints to black instead of re-drawing the icons.

### Immediate fix

Any of these forces the Shapes panel to re-render correctly:

1. Resize the Shapes panel: drag its border slightly to trigger a layout pass.
2. Click another stencil tab and click back.
3. Press **F5** to refresh the drawing.
4. Close the stencil (right-click the title bar → **Close**) and reopen it.

### Has it been seen in other stencils?

The same intermittent rendering issue is reported on Visio's own shipped network stencils and on third-party libraries. Microsoft's troubleshooting guidance for it lives at <https://learn.microsoft.com/visio> under "Shape display issues". Common contributing factors:

- **Hardware acceleration:** older or virtualised GPUs sometimes mishandle Visio's preview cache. Try **File → Options → Advanced → Display → Disable hardware graphics acceleration**, restart Visio.
- **High-DPI scaling:** Visio on 4K displays at 200% scaling has known repaint bugs. Try setting Visio to **System DPI** under **File → Options → General → Display**.
- **Visio version:** very old Visio 2019 builds had a confirmed black-tile bug fixed in build 16.0.13127.x. Check **File → Account → About Visio** for your build number.

### What to capture if you can reproduce it reliably

Open an issue at [github.com/xeeva/Visio-Azure/issues](https://github.com/xeeva/Visio-Azure/issues) with:

- A short screen recording or a sequence of screenshots showing the panel before and after the drop
- Your Visio build number (**Help → About Microsoft Visio**)
- OS, display configuration (single / multi-monitor, DPI scaling per display)
- Whether hardware acceleration is on or off

## Stencil opens read-only

**Symptom:** Visio opens the stencil but marks it read-only; you cannot edit masters.

This is expected. `.vssx` files are stencil templates; Visio opens them read-only by design. To edit a master, right-click it in the Shapes panel → **Edit Master → Edit Master Shape**. To save a modified copy as a new stencil, use **File → Save As** and choose `.vssx` format.

## My Shapes folder not appearing

**Symptom:** after dropping the stencil into My Shapes and restarting Visio, the **More Shapes → My Shapes** menu does not appear or shows a different folder.

Check that you dropped the file into the correct location:

- Windows: `%USERPROFILE%\Documents\My Shapes` (not `Documents\Visio` and not a subfolder of My Shapes)
- macOS: `~/Library/Group Containers/UBF8T346G9.Office/User Content/My Shapes`

Visio only watches the top level of the My Shapes folder; subfolders are not indexed automatically. If the path is correct, try **File → Options → Advanced → File Locations** to confirm Visio's registered My Shapes path.

## Visio logs and where to find them

Visio doesn't write a single "everything that happened" log, but a few diagnostic surfaces are available.

### Office Telemetry Dashboard (Enterprise)

Captures crash events, add-in failures, and document-open errors across the Office suite for managed deployments. Available via your Microsoft 365 admin portal. The most reliable source if you're on a managed install.

### Visio recovery information

When Visio crashes or recovers a drawing, it writes a recovery descriptor:

- **Windows:** `%APPDATA%\Microsoft\Visio\` (look for `.~visio.recover` files plus any `.log` files in this directory).
- **macOS:** `~/Library/Containers/com.microsoft.Visio/Data/Library/Application Support/Microsoft/Visio/`.

Recovery files contain a short XML descriptor of the document state at crash time. Not detailed enough to debug a renderer glitch directly, but useful if the panel-black issue ever ends in a crash.

### Add-in error log

Failures loading or executing Visio add-ins:

- **Windows:** `%APPDATA%\Microsoft\Visio\AddInError.log`

If the file exists and is non-empty, an add-in is misbehaving and may be contributing to the rendering issue. Try disabling all add-ins (**File → Options → Add-ins → Manage: COM Add-ins → Go → uncheck all**) and reproducing.

### Application Event Log (Windows)

Run **Event Viewer → Windows Logs → Application** and filter source by `Visio` or `Office`. Look for entries timestamped around a panel-black incident. If Visio's renderer is throwing a Windows-side error you'll see it here.

### Running Visio with the /log flag

For deep debugging, launch Visio from a command prompt with `/log` to get more verbose console output:

```cmd
"C:\Program Files\Microsoft Office\root\Office16\VISIO.EXE" /log
```

The output goes to stdout (the command-prompt window); pipe to a file if you want to capture it:

```cmd
"C:\Program Files\Microsoft Office\root\Office16\VISIO.EXE" /log > visio-trace.log 2>&1
```

Includes shape sheet evaluation messages, stencil load events, and render-cache invalidation notices. Verbose: a 5-minute session produces ~50-200 lines.

### Process Monitor (ProcMon) for file-system level tracing

If you suspect Visio is failing to read part of the stencil package, [Sysinternals Process Monitor](https://learn.microsoft.com/sysinternals/downloads/procmon) captures every file-system call. Filter by `Process Name is VISIO.EXE` and watch the access pattern when you drop an icon. A `NAME NOT FOUND` or `ACCESS DENIED` on a `.vssx` part would be a strong signal.

## Reporting an issue

When in doubt, [open an issue](https://github.com/xeeva/Visio-Azure/issues) with whatever you have. Even a "I see X when I do Y on Visio build Z" without a log is useful: if multiple people report the same combination we can correlate without waiting for a perfect trace.
