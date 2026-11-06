# Editing SDDs with Quarto: presentation execution plan

## 1. Scope and delivery approach

**Deliverable:** a 22-slide PowerPoint explaining how the team edits SDD documents with Quarto, with detailed presenter notes and prepared demonstrations.

**Audience assumption:** team members understand the content of an SDD but have limited experience with Markdown or Quarto.

**Session format:** explanation and presenter demonstrations. There are no audience exercises, assignments, or practice sections.

**Timing:** approximately 61 minutes, comprising 58 minutes of planned slide time and 3 minutes of transition or rendering buffer. The final slide includes Q&A.

**Approved section order:**

| Section | Slides | Planned time |
|---|---|---|
| Introduction to Quarto format | 1-4 | 7 minutes |
| Easy editing | 5-6 | 5 minutes |
| Advanced editing, including table formats | 7-16 | 28 minutes |
| Editing QMD files in Positron | 17-19 | 9 minutes |
| Integration with Mermaid | 20-21 | 6 minutes |
| Common errors, quick reference, and Q&A | 22 | 3 minutes |

The 22-slide count includes the title and closing slides. Section changes use the title of the next content slide rather than additional divider slides. The table-formats subsection occupies slides 10-12 and compares Markdown pipe tables, Pandoc grid tables, and HTML tables using the same interface data.

### Teaching approach

- Use one fictional **Telemetry Gateway SDD** throughout. All component names, interfaces, and behaviors in the examples are training examples, not approved project requirements.
- On syntax slides, show a short source example beside its rendered result. Put longer explanations and copy-ready examples in presenter notes.
- Establish the file format before demonstrating the editor, following the approved order. Slides 1-16 use prepared examples and screenshots. The Positron walkthrough starts on slide 17.
- Use HTML to review content and navigation, then Word to inspect the delivered document's layout, styles, and fields.
- Treat the editable QMD and assets as the maintained content. Explain that rebuilding replaces generated output.

### Planned visual treatment

Use a clean 16:9 layout with a light background, dark text, and one accent color for syntax emphasis. Use approximately 32 pt slide titles, 20-24 pt body text, and 19-22 pt monospaced code. Keep source text editable in PowerPoint. Screenshots should show the actual prepared Positron and Word sessions. Crop screenshots to the controls or document region being discussed.

Use a plain two-column composition for source/result examples. Avoid decorative imagery on syntax slides. The architectural image and Mermaid diagrams serve as SDD content examples. A single code example should normally occupy no more than 8-10 visible lines. Put extra code or alternate cases in notes.

## 2. Preparation and production steps

### Step A: Prepare the teaching example

Prepare a new training project separate from working SDDs. The proposed project structure is:

```text
training-demo/
  SDD.qmd
  _quarto.yml
  reference.docx
  review.css
  assets/
    gateway-context.png
    gateway-context-revised.png
  sections/
    _architecture.qmd
    _interfaces.qmd
  table-formats/
    HTML-table-demo.qmd
  output/
```

The folders and assets above are planned materials to create during presentation production. They are not deliverables created by this execution-plan task.

Prepare the following content:

1. A short overview of a gateway that receives telemetry, validates messages, and stores accepted records.
2. An architecture section and an interface section, each with a short prose fragment for the include demonstration.
3. The same interface data expressed as a Markdown pipe table, a Pandoc grid table, and an HTML table. Use `IF-01`, `Telemetry`, `Inbound` and `IF-02`, `Record store`, `Outbound` in each version. The `IF-` values are interface identifiers, distinct from the Quarto table ID. Also prepare one grid-table cell containing two paragraphs to explain when that format helps.
4. A gateway context image and a revised version with a visible change.
5. A note about validation and one paragraph using a named Word style.
6. A small Mermaid flowchart with an accepted/rejected decision.
7. A short sequence diagram retained in notes as an alternate Mermaid example.

Keep the HTML-table example in `table-formats/HTML-table-demo.qmd` and preview that file separately as HTML. The main `SDD.qmd` uses the pipe and grid examples for the toolkit-backed Word build and does not include the HTML-table example. This arrangement lets the presenter teach all three source formats while using the existing toolkit's verified workflow for final Word export.

Use these document identifiers consistently:

| Element | Identifier | Reference syntax |
|---|---|---|
| Interface table | `tbl-interfaces` | `@tbl-interfaces` |
| Context image | `fig-gateway-context` | `@fig-gateway-context` |
| Mermaid flowchart | `fig-processing-flow` | `@fig-processing-flow` |

### Step B: Prepare and verify the toolchain

1. Record the installed Quarto and Positron versions for the presenter. Use screenshots of those versions rather than assuming every toolbar matches an online example.
2. Verify that Positron recognizes QMD files and that its Quarto support, visual editing, and HTML preview work on the presentation computer.
3. Choose a reference document containing the named paragraph style used on slide 9. Confirm its rendered appearance in Word.
4. Build the example through the existing toolkit for both HTML and Word. Use an explicit `--input-file SDD.qmd` in the demonstration commands.
5. Verify every asset, caption, cross-reference, included paragraph, and diagram in the assembled output. Check both pipe and grid tables in the toolkit-built Word document. Preview the separate HTML-table file with Quarto's HTML table processing enabled, and verify its basic table structure in HTML.
6. Check that a supported browser is available for Mermaid's Word image generation. Rehearse the diagram export before the session. [Quarto diagram rendering](https://quarto.org/docs/authoring/diagrams.html).
7. Open the generated Word document, refresh fields, and inspect the final pagination.

**Toolkit compatibility note for production:** the current toolkit counts tables by parsing the main source before Quarto expands includes. Its Word finishing step expects that table count to match the rendered document. An included file containing a table can therefore cause a count mismatch. For this training, keep the slide 16 include fragments limited to headings and prose, and keep the demonstrated pipe/grid tables in the main QMD. Rendering tables inside included files through this toolkit needs a separate compatibility check before teaching it as a supported team workflow. This limitation comes from the toolkit wrapper, while the Quarto include syntax itself supports inserting content.

**HTML-table compatibility note for production:** raw HTML tables also escape the toolkit's initial native-table count. Quarto can subsequently convert them to native tables, after which the toolkit's Word count verification can reject the result. Demonstrate HTML-table rendering in the separate HTML preview. Before including such a table in the team's toolkit-built Word deliverable, verify that the wrapper handles its converted table count and styling. Quarto's ability to process HTML tables across output formats does not by itself verify this custom build path. Keep this implementation detail in presenter preparation notes. [Quarto HTML-table processing](https://quarto.org/docs/authoring/tables.html#html-tables).

The toolkit's picture check uses a minimum expected count from source images. It does not independently establish that a Mermaid-generated diagram rendered correctly. Inspect each generated diagram visually. Do not change execution settings merely to demonstrate Mermaid without first checking the installed version's behavior.

Local implementation evidence: [toolkit source checks](C:/Users/KEFEI/Documents/sdd/quarto-docx-toolkit/scripts/toolkit.py:247), [build input selection](C:/Users/KEFEI/Documents/sdd/quarto-docx-toolkit/scripts/toolkit.py:348), and [table count verification](C:/Users/KEFEI/Documents/sdd/quarto-docx-toolkit/scripts/docx_tables.py:144).

### Step C: Capture the evidence needed for slides

- A rendered SDD page showing a heading, a table, a figure, and references.
- The sample project folder in Positron Explorer.
- The same paragraph in Source and Visual modes.
- A focused source-and-HTML-preview view.
- A Word page showing the custom paragraph style.
- Before/after table and figure numbering after inserting an earlier object.
- Pipe, grid, and HTML source examples using the same interface data, with their rendered results. Include the grid-table cell containing two paragraphs and an HTML cell-span example in backup notes.
- The include source, one included fragment, and the assembled result.
- A Mermaid source cell beside its diagram.
- A successful toolkit build and the corresponding Word output.

Save complete before/after project copies for presenter recovery. Prepare static screenshots for every demonstration so rendering delays do not disrupt the explanation.

### Step D: Author the PowerPoint

Create the 22 slides specified below. Keep the primary teaching point and the visible example on the slide. Place the narration, exact commands, alternate examples, and source links in speaker notes. Use actual editor screenshots for software controls. Maintain the approved order, including Positron after advanced editing and its table-formats subsection.

### Step E: Review and rehearse

Check the deck's slide count, order, code legibility, screenshot accuracy, and syntax consistency. Rehearse the presenter actions in order. Verify that every demonstration produces the expected output using the exact training project. Inspect the exported PowerPoint for text fit and image clarity at presentation size. Keep the final presentation, training project, and backup screenshots together for delivery.

## 3. Detailed slide specifications

### Slide 01: Editing SDDs with Quarto

**Section:** Introduction. **Time:** 1 minute.

**Purpose:** establish what the session covers and give the team a concrete picture of the result.

**On-slide content:**

- Title: **Editing SDDs with Quarto**.
- Subtitle: **Document content, references, and diagrams**.
- A compact agenda listing the five teaching sections in the approved order.

**Layout:** a large title on the left and a cropped page from the example SDD on the right. Keep the agenda short enough to scan immediately.

**Presenter sequence:** introduce the fictional Telemetry Gateway example. Point out the table, image, and diagram the team will learn to maintain. Explain that the session consists of walkthroughs and demonstrations.

**Preparation:** obtain the finished example page after the sample project passes the build checks.

### Slide 02: What Quarto does

**Section:** Introduction. **Time:** 2 minutes.

**Purpose:** explain the relationship between editable source and formatted output.

**On-slide content:**

- QMD stores document content as readable text.
- Quarto reads the source and project settings to produce output.
- The same maintained content can support HTML review and Word delivery.
- The team updates the source and rebuilds when content changes.

**Layout:** three labeled areas for source, supporting files, and generated output. Show real thumbnails or text excerpts from the sample project rather than a decorative process diagram.

**Presenter sequence:** point to a sentence in the source and its formatted counterpart in the output. Explain that the reference document supplies Word styles and that HTML has its own presentation settings. Show that a content change reaches both outputs after rebuilding.

**Expected takeaway:** a QMD file is the content the team maintains, and rendering produces the document readers receive.

**Source for notes:** [Quarto authoring overview](https://quarto.org/docs/get-started/authoring/).

### Slide 03: Anatomy of a Quarto document

**Section:** Introduction. **Time:** 2 minutes.

**Purpose:** make the structure of a QMD file recognizable before teaching individual syntax features.

**Source example:**

```markdown
---
title: "Telemetry Gateway SDD"
---

# Overview

The gateway validates incoming telemetry before storage.

## Design constraints

- Reject messages with an invalid schema.
```

**On-slide content:** label the YAML header, heading, paragraph, and list. Mention that shared output settings can live in `_quarto.yml`.

**Layout:** show the source as editable code with annotations beside the relevant lines. Reserve a small region for the formatted result.

**Presenter sequence:** explain the `---` boundaries, indentation in YAML, blank lines between blocks, and heading levels. Tell the team to preserve the existing project's settings while editing document content.

**Preparation:** use only this short example on the slide. Explain executable cells and other special blocks later, when the relevant slide introduces them.

**Source for notes:** [Quarto front matter](https://quarto.org/docs/authoring/front-matter.html).

### Slide 04: The SDD project structure

**Section:** Introduction. **Time:** 2 minutes.

**Purpose:** identify which files the team edits and which files support the build.

**On-slide content:** show the proposed project tree and a concise role for each important item:

- `SDD.qmd`: main document.
- `sections/`: included content fragments.
- `assets/`: source images.
- `_quarto.yml`: shared configuration and filters.
- `reference.docx`: Word styles and page settings.
- `output/`: generated review and delivery files.

**Layout:** project tree on the left and short file-role descriptions on the right. Keep detailed file behavior in notes.

**Presenter sequence:** explain keeping the project folder together when moving it. Show that image references depend on the asset files. Explain that content edits made only in the generated Word file are replaced by the next build.

**Preparation:** use the actual training project's filenames in the screenshot. Explain that existing team projects may use a different main filename.

**Source for notes:** [existing toolkit workflow](C:/Users/KEFEI/Documents/sdd/quarto-docx-toolkit/README.md).

### Slide 05: Text, paragraphs, and headings

**Section:** Easy editing. **Time:** 3 minutes.

**Purpose:** cover the changes most SDD editors make each day.

**Source example:**

```markdown
## Message validation

The gateway **validates** every incoming message.

Invalid messages receive an *error response*.

### Configuration

The `schema_version` field selects the message schema.
```

**On-slide content:** explain `#` through `###`, paragraph separation, bold, italic, and inline code. Use heading levels to express document structure. Let the configured project handle any automatic numbering.

**Layout:** source on the left, rendered result on the right. Highlight one syntax feature at a time in the presenter walkthrough.

**Presenter sequence:** revise the first sentence, add a paragraph, and identify the subsection boundary in the prepared before/after views. Explain that ordinary wrapped source lines can remain part of one paragraph.

**Expected result:** the output shows the intended heading hierarchy and two distinct paragraphs without extra formatting wrappers.

**Source for notes:** [Markdown text and heading syntax](https://quarto.org/docs/authoring/markdown-basics.html).

### Slide 06: Lists, links, and code examples

**Section:** Easy editing. **Time:** 2 minutes.

**Purpose:** show common structures used for constraints, procedures, and configuration examples.

**Primary source example:**

```markdown
- Validate the message schema.
- Store accepted records.

1. Load the active configuration.
2. Start the receiver.

See the [Quarto guide](https://quarto.org/docs/guide/).
```

**Secondary example for notes:**

````markdown
```json
{"schema_version": "v1", "enabled": true}
```
````

**On-slide content:** identify unordered lists, ordered lists, links, and code fences. Explain that language-tagged code blocks display examples, while later `{mermaid}` cells produce diagrams.

**Layout:** source and result, with the small JSON block below only if it fits at the target font size. Otherwise show it as the second presenter build of this slide.

**Presenter sequence:** point out list markers, consistent indentation for nested items, the bracket/parenthesis link pattern, and matching backtick fences.

**Source for notes:** [Pandoc lists, links, and code blocks](https://pandoc.org/MANUAL.html).

### Slide 07: Attributes, IDs, and captions

**Section:** Advanced editing. **Time:** 2 minutes.

**Purpose:** introduce the shared concepts behind divs, tables, images, and references.

**On-slide content:** use a small terminology table:

| Syntax | Meaning | Example use |
|---|---|---|
| `#id` | Identifies an element | `#fig-gateway-context` |
| `.class` | Assigns a class | `.callout-note` |
| `key="value"` | Supplies an option | `width="5in"` |
| Caption text | Describes the object | Gateway context |
| `@id` | Refers to a labeled object | `@fig-gateway-context` |

**Layout:** terminology on the left and one annotated image-source line on the right. Break the annotation into labels rather than displaying a long second code example.

**Presenter sequence:** explain that a generic ID identifies content, while reserved prefixes such as `fig-` and `tbl-` identify numbered reference types. Show the documented attribute order: ID, classes, then key-value options. Introduce lowercase descriptive IDs as the training convention.

**Source for notes:** [Quarto attributes](https://quarto.org/docs/authoring/markdown-basics.html#divs-and-spans) and [cross-reference labels](https://quarto.org/docs/authoring/cross-references.html).

### Slide 08: Fenced divs

**Section:** Advanced editing. **Time:** 3 minutes.

**Purpose:** show how a block groups content and applies supported behavior or formatting.

**Source example:**

```markdown
::: {.callout-note}

## Validation rule

The gateway stores a message only after validation succeeds.

:::
```

**On-slide content:** label the opening fence and attributes, the enclosed content, and the closing fence. Explain that the block can contain multiple paragraphs or lists.

**Layout:** code on the left and the rendered note on the right. Use a focused annotation to connect the two fence lines.

**Presenter sequence:** explain that at least three colons form a div fence. Show what content the block contains. Explain that `.callout-note` supplies built-in behavior, while an arbitrary class needs appropriate styling or a filter. Mention nesting in notes, using different fence lengths to make nested structure readable.

**Common error to explain:** a missing closing fence changes the structure of subsequent content. Show the corrected version without asking the audience to repair it.

**Source for notes:** [fenced divs](https://quarto.org/docs/authoring/markdown-basics.html#divs-and-spans) and [callout blocks](https://quarto.org/docs/authoring/callouts.html).

### Slide 09: Fenced divs and SDD styles

**Section:** Advanced editing. **Time:** 2 minutes.

**Purpose:** connect Quarto source markup to existing Word paragraph styles.

**Source example:**

```markdown
::: {custom-style="Body Text Indent"}

The gateway retains the last accepted configuration locally.

:::
```

**On-slide content:** the wrapper names a Word style, the reference document supplies its formatting, and ordinary paragraphs use the project's normal body style.

**Layout:** source beside a cropped Word paragraph. Annotate the paragraph's visible indentation and the selected style in Word if readable.

**Presenter sequence:** connect the exact style name in the QMD to the style in the training reference document. Explain that authors can preserve imported special-style wrappers and reuse an approved style. Explain that HTML uses its own styling and may display the paragraph differently.

**Preparation:** confirm the named style exists and has a visibly different appearance. If the team's reference uses another style name, update the example and screenshot together.

**Source for notes:** [applying Word custom styles](https://quarto.org/docs/output-formats/ms-word-templates.html#applying-custom-styles).

#### Table formats subsection: slides 10-12

This subsection teaches three ways to write a table in a QMD file. Use the same data so the audience can compare authoring syntax rather than interpret a new example each time. Explain when each format is useful and distinguish its source notation from the borders and styling of the rendered table.

### Slide 10: Markdown pipe tables

**Section:** Advanced editing / Table formats. **Time:** 3 minutes.

**Purpose:** introduce the simplest table syntax for routine interface definitions and other SDD data.

**Source example:**

```markdown
| ID    | Interface    | Direction |
|:------|:-------------|:----------|
| IF-01 | Telemetry    | Inbound   |
| IF-02 | Record store | Outbound  |
```

**On-slide content:** label the header row, required separator row, data rows, and alignment markers. Explain that adding a column requires a cell in each row and in the separator. Pipe tables are the default teaching choice for simple text, numbers, and inline formatting.

**Layout:** table source on the left and a native editable PowerPoint table representing the rendered result on the right. Highlight the new row in a prepared second view.

**Presenter sequence:** add one data row and explain alignment markers such as `:---`, `---:`, and `:---:`. Identify `IF-01` as a value inside the table, distinct from the table's Quarto ID introduced on slide 13. Explain that padding the source improves readability but pipe boundaries do not require the strict alignment used by grid tables.

**Notes:** pipe-table cells support inline content but do not express multiple block paragraphs, block lists, or merged cells. Introduce grid and HTML tables as alternatives on the next two slides. The visible table borders in Word come from the reference and toolkit styling, rather than from how many dashes the source contains.

**Sources for notes:** [Quarto Markdown tables](https://quarto.org/docs/authoring/tables.html#markdown-tables) and [Pandoc pipe tables](https://pandoc.org/MANUAL.html#extension-pipe_tables).

### Slide 11: Pandoc grid tables

**Section:** Advanced editing / Table formats. **Time:** 3 minutes.

**Purpose:** explain the fully drawn border syntax shown in the requested example and when it helps with more complex cell content.

**Source example:**

```markdown
+-------+--------------+-----------+
| ID    | Interface    | Direction |
+=======+==============+===========+
| IF-01 | Telemetry    | Inbound   |
+-------+--------------+-----------+
| IF-02 | Record store | Outbound  |
+-------+--------------+-----------+
```

**On-slide content:** name this format a **Pandoc grid table**, which is another Markdown table format. Explain that `+` marks corners and intersections, `-` draws horizontal boundaries, `|` marks vertical boundaries, and the `=` row separates the header from the body. Align the boundaries across every line in a monospaced editor.

**Layout:** show the complete grid source on the left and the same rendered data table as slide 10 on the right. Annotate the header separator and one vertical boundary. Keep the border characters in editable monospaced text.

**Presenter sequence:** connect this syntax to the user's border-style example, then walk through one complete valid table. Show that an extra source line can continue a cell's content rather than create a new table row. Explain that inserting a row includes its horizontal separator and that widening a column requires updating the corresponding boundaries consistently.

**Second example for presenter notes or a prepared slide build:**

```markdown
+-----------+-----------------------+
| Interface | Description           |
+===========+=======================+
| IF-01     | Receives telemetry.   |
|           |                       |
|           | Rejects invalid data. |
+-----------+-----------------------+
```

The blank content line divides the Description cell into two paragraphs. This example makes the reason for using grid syntax visible. Lists and code blocks are other possible cell contents. Retain merged-cell restructuring as an optional note rather than crowding the introductory example.

**Common errors:** misaligned intersections, inconsistent column widths, and using an ordinary `-` border where a header separator is intended. Grid source boundaries define table structure. Actual output borders still follow the output's styling. Quarto shortcodes are unsupported inside grid tables, so keep the include shortcode outside a grid cell.

**Expected result:** the basic grid source renders as a native table, and the extended example preserves two paragraphs inside one cell. Verify the Word result through the toolkit during preparation.

**Sources for notes:** [Pandoc grid tables](https://pandoc.org/MANUAL.html#extension-grid_tables) and [Quarto grid tables](https://quarto.org/docs/authoring/tables.html#grid-tables).

### Slide 12: HTML tables

**Section:** Advanced editing / Table formats. **Time:** 3 minutes.

**Purpose:** introduce explicit HTML structure for tables and explain the output checks needed when choosing this format.

**Copy-ready QMD example:**

````markdown
```{=html}
<table>
  <thead><tr><th>ID</th><th>Interface</th><th>Direction</th></tr></thead>
  <tbody>
    <tr><td>IF-01</td><td>Telemetry</td><td>Inbound</td></tr>
    <tr><td>IF-02</td><td>Record store</td><td>Outbound</td></tr>
  </tbody>
</table>
```
````

**On-slide content:** label `<table>`, `<tr>` for a row, `<th>` for a header cell, and `<td>` for a data cell. Mention `<thead>`, `<tbody>`, and `<caption>` in the narration. Explain that `{=html}` marks a raw HTML block, while an ordinary `html` code fence displays source code.

**Layout:** use the full slide width for the short HTML source block, with its rendered table beneath it. If the full example becomes too dense, show a one-row excerpt on the slide and retain the complete code above in notes. Use syntax emphasis to associate one HTML row with one rendered row.

**Presenter sequence:** identify the same two interface records used on slides 10-11. Change one `<td>` value and show the HTML preview. Explain `colspan="2"` and `rowspan="2"` as options for spanning columns or rows, supported by a small prepared example in notes. Keep the first visible example unmerged.

**Format-choice comparison for presenter notes:**

| Format | Best teaching use | Main editing consideration |
|---|---|---|
| Markdown pipe table | Routine tables with simple cells | Shortest source and easy row edits |
| Pandoc grid table | Multiple paragraphs or block content inside cells | Boundaries must stay aligned |
| HTML table | Explicit markup, cell spans, or an HTML-based authoring workflow | More tags and an output/toolkit compatibility check |

**Output notes:** Quarto processes supported HTML tables into its table representation for multiple output formats when HTML table processing is enabled. HTML tables are therefore not limited to HTML output. Browser CSS appearance does not automatically carry into Word, and disabling Quarto's table processing prevents the cross-format conversion. Use the normal caption/ID workflow introduced on slide 13 after verifying the chosen syntax, rather than assuming any HTML `id` automatically supplies Quarto numbering.

**Production constraint:** show this example from the separate `table-formats/HTML-table-demo.qmd` HTML preview. The current toolkit's preflight count can miss raw HTML tables and then disagree with the converted table count in Word. Keep pipe/grid examples in the demonstrated toolkit Word build until HTML-table handling has been verified. This is a presenter preparation detail, while the audience-facing message is to check the intended output before choosing the format.

**Sources for notes:** [Quarto HTML tables and table processing](https://quarto.org/docs/authoring/tables.html#html-tables) and [HTML table elements and cell spans](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/table).

### Slide 13: Table IDs and references

**Section:** Advanced editing. **Time:** 3 minutes.

**Purpose:** show how tables receive captions, numbers, and references that update with the document.

**Source example:**

```markdown
| ID    | Interface | Direction |
|:------|:----------|:----------|
| IF-01 | Telemetry | Inbound   |

: Gateway interfaces {#tbl-interfaces}

See @tbl-interfaces for the interface summary.
```

**On-slide content:** identify the caption text, the `tbl-` ID, and the reference. Keep a blank line before the caption. Explain that the caption is written after the table in source even when output settings place it above the table.

**Layout:** source and rendered table/reference. Use a second prepared state showing an earlier inserted table and the changed numbering.

**Presenter sequence:** show the original output, insert an earlier table in the prepared example, and show the updated number and reference. Explain that the ID remains stable when order changes. Avoid typing table numbers into caption text or adding an extra `Table` before `@tbl-interfaces` when the configured reference already supplies it.

**Source for notes:** [table labels and references](https://quarto.org/docs/authoring/tables.html#cross-references).

### Slide 14: Adding and replacing images

**Section:** Advanced editing. **Time:** 3 minutes.

**Purpose:** explain the relationship between an image file and its QMD markup.

**Primary source example:**

```markdown
![Gateway context](assets/gateway-context.png){width="5in"}
```

**Additional attribute for notes:** `fig-alt="A sensor sends telemetry to the gateway, which writes accepted records to storage."`

**On-slide content:** identify the visible caption, asset path, width setting, and optional alternative text. A captioned figure occupies its own paragraph in the teaching example.

**Layout:** source above a cropped asset folder view on the left, rendered image on the right. Keep the full alternative-text example in notes if the source line becomes too long.

**Presenter sequence:** place the prepared PNG in `assets/`, connect its filename to the markup, and show the effect of changing the width. Replace it with the revised file and rebuild. Explain that HTML preview does not establish Word page fit.

**Expected result:** the correct image appears with a readable caption and fits the available Word text area.

**Source for notes:** [Quarto figures and alternative text](https://quarto.org/docs/authoring/figures.html).

### Slide 15: Image IDs and references

**Section:** Advanced editing. **Time:** 3 minutes.

**Purpose:** apply the reference pattern to figures and keep prose connected to the correct image.

**Source example:**

```markdown
![Gateway context](assets/gateway-context.png){#fig-gateway-context width="5in"}

See @fig-gateway-context for the external connections.
```

**On-slide content:** use a unique `fig-` ID, refer to it with `@`, and retain the ID when replacing the same conceptual figure.

**Layout:** source and rendered figure with its reference. Use the same teaching image established on slide 14 so the audience can focus on the added ID.

**Presenter sequence:** point out the ID and the generated caption number. Show the numbering after an earlier figure is inserted. Explain that an unrelated replacement should get an appropriate ID and that deleting a figure requires removing or redirecting references.

**Notes:** ID uniqueness applies to the entire assembled document, including content brought in through includes. Distinguish these IDs from image filenames.

**Source for notes:** [figure cross-references](https://quarto.org/docs/authoring/figures.html#cross-references).

### Slide 16: Including other QMD files

**Section:** Advanced editing. **Time:** 3 minutes.

**Purpose:** show how a main QMD assembles content from separate source files.

**Main-file source example:**

```markdown
{{< include sections/_architecture.qmd >}}

{{< include sections/_interfaces.qmd >}}
```

**Example content of `sections/_architecture.qmd`:**

```markdown
# Architecture {#sec-architecture}

The gateway validates incoming telemetry before storage.
```

**On-slide content:** the include shortcode inserts a file's content at its location. File order controls content order. Prefix included filenames with `_` so normal Quarto project rendering excludes them as standalone documents.

**Layout:** a small file tree on the left, main-file include statements in the center, and the assembled headings/prose on the right. Put the full fragment example in notes if needed for legibility.

**Presenter sequence:** identify the main file, open the architecture fragment in a prepared screenshot, change a sentence, and show the rebuilt main document. Explain that the main document is the build target.

**Important notes:** put each include on its own line with blank lines around it. Keep document metadata in the main file or project configuration and omit YAML headers from content fragments. Relative asset paths inside fragments resolve from the main document's directory. Use main-relative `assets/...` paths for this toolkit. IDs must remain unique throughout the assembled source.

**Production constraint:** use headings and prose in these included fragments for the toolkit-backed demonstration, as described in Step B. Keep included-table export behavior as a presenter preparation issue rather than crowding the teaching slide with implementation details.

**Source for notes:** [Quarto includes](https://quarto.org/docs/authoring/includes.html).

### Slide 17: Opening an SDD project in Positron

**Section:** Positron. **Time:** 2 minutes.

**Purpose:** orient the team in the editor after they understand the QMD syntax.

**On-slide content:** open the project folder, select the main QMD, navigate the document outline, and locate Explorer, the editor, the Viewer, and the integrated terminal.

**Layout:** one large real Positron screenshot with a few numbered annotations. Add short labels outside the screenshot rather than small explanatory text inside it.

**Presenter sequence:** open the `training-demo` folder, expand `sections/` and `assets/`, open `SDD.qmd`, and navigate to the interface section. Explain that included fragments appear as separate source files in Explorer and that the main file remains the rendering entry point.

**Preparation:** close unrelated tabs, enlarge the editor font, and arrange the panes before capturing the screenshot. Ensure the training project can be opened without environment-selection prompts unrelated to prose editing.

**Expected takeaway:** team members know how to find the source file and the supporting assets in Positron.

**Source for notes:** [Quarto in Positron](https://quarto.org/docs/tools/positron/).

### Slide 18: Source and visual editing in Positron

**Section:** Positron. **Time:** 3 minutes.

**Purpose:** show both editing modes and explain a useful choice for each kind of change.

**On-slide content:**

- Source mode exposes the exact Markdown and Quarto syntax.
- Visual mode supports formatted editing of prose and document structures.
- Both modes edit the same QMD content.
- Inspect source when working with precise attributes, includes, and Mermaid cells.

**Layout:** focused screenshots of the same short section in both modes, with labels identifying the current mode. Keep most of the application chrome cropped away.

**Presenter sequence:** revise a sentence in Visual mode, switch to Source mode, and point to the corresponding Markdown. Show where the figure or table attributes appear. Demonstrate switching through the editor's mode command or Open With menu using the installed version's controls.

**Notes:** Visual mode is an editing surface. The rendered output remains the check for final behavior. Visual editing can normalize Markdown formatting, so review the source change when working with imported or specialized markup. Preserve the sample's IDs and attributes through the mode switch.

**Source for notes:** [Positron visual editing](https://quarto.org/docs/tools/positron/visual-editor.html).

### Slide 19: Previewing and building the document

**Section:** Positron. **Time:** 4 minutes.

**Purpose:** establish the team's repeatable content-review and final Word-export workflow.

**On-slide content:** save the edits, preview HTML beside the source, use the toolkit for the approved Word build, and inspect the resulting Word document.

**Presenter sequence:**

1. Select the main QMD and save all modified files, including fragments.
2. Run **Quarto: Preview Format** and select HTML. Use **Quarto: Preview** for subsequent previews of the selected format.
3. Show a changed paragraph and its reference in the HTML Viewer.
4. Close the previous generated Word document, open the integrated terminal, and run the toolkit Word build.
5. Open `output/SDD.docx` in Word, refresh fields with **Ctrl+A, F9**, and repeat F9 if a preceding reference needs another refresh.
6. Inspect the figure, caption, table, and page fit.

**Layout:** a focused Positron source/preview screenshot with a short workflow list. Show the Word result as a second prepared view. Keep the full command in notes.

**PowerShell command pattern for notes:**

```powershell
$toolkitBuild = 'C:\Users\KEFEI\Documents\sdd\quarto-docx-toolkit\scripts\build.bat'
$sddProject = 'C:\Users\KEFEI\Documents\sdd\training-demo'

& $toolkitBuild --project $sddProject --input-file SDD.qmd --format html
& $toolkitBuild --project $sddProject --input-file SDD.qmd --format docx
```

These paths describe the planned training-project location. Adjust them if that project is created elsewhere. The `html` command produces the toolkit's shareable review output. Positron's preview command supplies the editing preview. The `docx` command runs the toolkit's Word post-processing, which a direct Quarto render does not perform.

**Notes:** choose HTML explicitly because the configured default may be Word. Embedded previews support HTML and PDF-based output, while Word opens in an external application. Saving alone does not imply a completed rebuild. Confirm a successful build and inspect the output before distributing it.

**Sources for notes:** [Positron rendering and preview](https://quarto.org/docs/tools/positron/) and [toolkit build instructions](C:/Users/KEFEI/Documents/sdd/quarto-docx-toolkit/README.md).

### Slide 20: Mermaid diagrams inside Quarto

**Section:** Mermaid. **Time:** 3 minutes.

**Purpose:** show how a diagram can be maintained as text alongside the SDD content.

**Source example:**

````markdown
```{mermaid}
flowchart LR
  S[Sensor] --> V{Valid message?}
  V -->|Yes| D[Record store]
  V -->|No| E[Error response]
```
````

**On-slide content:** identify the `{mermaid}` cell, flow direction, node identifiers, displayed labels, and labeled connections. Explain that the cell renders a diagram.

**Layout:** editable source text on the left and a rendered Mermaid diagram on the right. Keep all diagram labels large enough to read.

**Presenter sequence:** show the diagram in Positron, change the store's label, and show the updated preview. Then add a prepared connection or node. Explain the distinction between stable node IDs such as `D` and visible labels such as `Record store`.

**Optional example in notes:** retain a four-line `sequenceDiagram` with Sensor, Gateway, and Store participants. Mention its value for request/response interactions if time permits, without adding a slide.

**Preparation:** capture the flowchart and the changed version. Avoid depending on a network service for the demonstration.

**Source for notes:** [Quarto Mermaid diagrams](https://quarto.org/docs/authoring/diagrams.html).

### Slide 21: Diagram captions, IDs, and export

**Section:** Mermaid. **Time:** 3 minutes.

**Purpose:** apply the figure-reference pattern to diagrams and verify the delivered result.

**Source example:**

````markdown
```{mermaid}
%%| label: fig-processing-flow
%%| fig-cap: "Telemetry processing flow"
flowchart LR
  S[Sensor] --> V{Valid message?}
  V -->|Yes| D[Record store]
  V -->|No| E[Error response]
```

See @fig-processing-flow for the processing sequence.
````

**On-slide content:** Mermaid cell options use `%%|`. The `fig-` label gives the diagram a figure ID, the caption describes it, and prose uses the normal `@fig-...` reference.

**Layout:** highlight the two option lines above the source. Show the captioned diagram and the rendered reference beside it. Use a small Word crop to show the exported result.

**Presenter sequence:** add the label and caption to the diagram, rebuild, and point to its generated figure number. Show that diagrams share the document's figure reference system with images. Compare the HTML rendering with the Word image, checking that labels remain readable.

**Notes:** Mermaid uses native JavaScript rendering in HTML and produces an image for Word. Browser-backed diagram image generation must work on the presentation computer. Word readers receive the diagram image, while authors maintain its editable Mermaid source in QMD. Rehearse this full path rather than treating a local diagram preview as proof of successful Word export.

**Source for notes:** [diagram options, references, and output formats](https://quarto.org/docs/authoring/diagrams.html).

### Slide 22: Common errors, quick reference, and Q&A

**Section:** Closing. **Time:** 3 minutes.

**Purpose:** leave the team with a compact reminder of the syntax and review steps.

**On-slide content:** use two short columns.

**Syntax reminder:**

- Heading: `## Interface design`.
- Div: opening attributes plus a closing `:::`.
- Tables: pipe markers, aligned grid borders, or a processed HTML table block.
- Table ID/reference: `#tbl-interfaces` and `@tbl-interfaces`.
- Figure ID/reference: `#fig-gateway-context` and `@fig-gateway-context`.
- Include: `{{< include sections/_interfaces.qmd >}}`.
- Mermaid options: `%%| label:` and `%%| fig-cap:`.

**Review reminder:**

- Save edited source and fragments.
- Check missing assets, duplicate IDs, and unresolved references.
- Confirm the build completed successfully.
- Inspect Word layout and refresh fields.

**Presenter sequence:** briefly connect each common problem to its likely cause: missing div/code fences, malformed table separators, wrong image/include paths, or a misspelled reference. Then take questions. Keep the troubleshooting detail below in speaker notes so the closing slide remains readable.

**Notes troubleshooting map:**

| Symptom | First check |
|---|---|
| Unexpected formatting extends into later text | Closing div or code fence |
| Table displays as plain text or misaligned cells | Header separator, column count, blank lines |
| Picture or included content is missing | Main-relative path, filename, saved file |
| Reference fails to resolve | Target ID, prefix, spelling, uniqueness |
| Preview and Word layout differ | Format-specific styles, image size, pagination |
| Final Word build fails while preview works | Toolkit error, output file lock, included-table or HTML-table compatibility |
| Word number appears stale | Successful rebuild followed by field refresh |

## 4. Presenter demonstration run sheet

| Slide | Action | Expected visible result | Prepared backup |
|---|---|---|---|
| 5 | Explain a sentence and heading change | Correct hierarchy and paragraph breaks | Before/after source and output crops |
| 8 | Explain the note's fences | Note contains only its intended content | Valid note screenshot |
| 9 | Apply the named style | Indented paragraph in Word | Word style screenshot |
| 10 | Add a pipe-table row | New row with consistent columns | Two table states |
| 11 | Explain grid borders and a two-paragraph cell | Same basic table, then block content inside a cell | Grid source and verified HTML/Word crops |
| 12 | Edit a cell in the separate HTML example | Changed value in the HTML preview | HTML source and rendered table crop |
| 13 | Insert an earlier table | Caption/reference numbers update | Two numbered outputs |
| 14-15 | Replace an image while retaining its figure ID | New image with a working reference | Original and revised outputs |
| 16 | Edit a prose fragment and render the main file | Included sentence changes in assembled output | Include source and output screenshots |
| 17-18 | Open the project and switch editing modes | Same QMD content in both modes | Focused Positron screenshots |
| 19 | Preview HTML, run toolkit build, inspect Word | Successful output with refreshed fields | Previously verified HTML and DOCX |
| 20-21 | Edit Mermaid, then add caption/ID and export | Updated diagram with working reference | Diagram source, HTML, and Word crops |

For slides before Positron, use prepared slide builds or screenshots. Reserve live editor interaction for slides 17-21 so the agreed narrative order remains clear. Use the backup when rendering exceeds the buffer, then continue the explanation from the verified output.

## 5. Completion criteria for the future presentation

- Exactly 22 slides in the approved order, including the expanded table-formats subsection.
- Every requested feature has its own planned coverage, including separate table-ID and image-ID slides.
- Slides 10-12 show valid pipe, grid, and HTML source for the same data, explain when each format is useful, and include a multi-paragraph grid-cell example in notes.
- The include slide uses the complete `{{< include ... >}}` shortcode and identifies the main build target.
- The Positron section follows advanced editing and shows both editing modes plus the review/export workflow.
- The training contains presenter demonstrations and no audience exercises.
- All visible source examples and rendered results agree.
- Code is editable and readable at normal presentation size.
- Software screenshots match the version used for the demonstration.
- The reference document contains the style used in the example.
- HTML and toolkit-built Word output have been checked with the exact training source.
- Included-table and HTML-table compatibility is handled during preparation, and Mermaid output is inspected visually.
- Speaker notes contain exact commands, narration, source links, and backup directions.
- The final handoff includes the PowerPoint, sample project, and demonstrated assets when the presentation is produced.

## 6. Technical references

Use these sources when building the example and authoring the speaker notes. Local toolkit behavior takes precedence over generic Quarto build instructions for this team's toolkit-produced Word deliverable.

- [Quarto authoring overview](https://quarto.org/docs/get-started/authoring/)
- [YAML front matter](https://quarto.org/docs/authoring/front-matter.html)
- [Markdown basics, attributes, and divs](https://quarto.org/docs/authoring/markdown-basics.html)
- [Callout blocks](https://quarto.org/docs/authoring/callouts.html)
- [Word templates and custom styles](https://quarto.org/docs/output-formats/ms-word-templates.html)
- [Tables](https://quarto.org/docs/authoring/tables.html)
- [Pandoc pipe tables](https://pandoc.org/MANUAL.html#extension-pipe_tables)
- [Pandoc grid tables](https://pandoc.org/MANUAL.html#extension-grid_tables)
- [Quarto HTML tables](https://quarto.org/docs/authoring/tables.html#html-tables)
- [HTML table elements and cell spans](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/table)
- [Cross-references](https://quarto.org/docs/authoring/cross-references.html)
- [Figures](https://quarto.org/docs/authoring/figures.html)
- [Includes](https://quarto.org/docs/authoring/includes.html)
- [Quarto in Positron](https://quarto.org/docs/tools/positron/)
- [Positron visual editing](https://quarto.org/docs/tools/positron/visual-editor.html)
- [Mermaid and diagram export](https://quarto.org/docs/authoring/diagrams.html)
- [Pandoc manual](https://pandoc.org/MANUAL.html)
- [Local Word-Quarto toolkit guide](C:/Users/KEFEI/Documents/sdd/quarto-docx-toolkit/README.md)
