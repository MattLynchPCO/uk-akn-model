# Page and Line Markup

## Overview

LDAPP requires the creation and application of amendment wording that makes use of line and page numbers. This is essential for accurately referencing specific locations within legislative documents during the amendment process.

## Implementation Approach

Unlike the standard AKN approach, **we do not use AKN's `eop` (end of page) and `eol` (end of line) elements** in the working XML documents within Lawmaker.

Instead, we use **XML processing instructions** to mark page and line breaks during the drafting and editing phase. These processing instructions are then converted to the native AKN `eop` and `eol` elements only on export for final publication.

### Rationale

Using processing instructions during the editing phase provides several advantages:
- Processing instructions do not affect the document structure or validation
- They can be easily inserted and removed without disrupting the content model
- They are invisible to most XML processing tools but can be accessed when needed
- They can be converted to proper AKN elements at the point of export

## Processing Instructions

During the editing phase within Lawmaker, page and line breaks are marked using processing instructions with the format:

```xml
<?L page-line?>
```

Where:
- `page` is the page number
- `line` is the line number within that page

### Examples from UK Legislative Documents

The following examples are taken from actual UK Bill XML documents showing how processing instructions are used in practice:

```xml
<part class="group2" eId="pt_1">
  <num><?L 1-1?>Part 1</num>
  <heading eId="pt_1__hdg"><?L 1-2?>Sentencing</heading>
  <hcontainer class="group7" eId="pt_1__xhdg_1" name="crossheading">
    <heading eId="pt_1__xhdg_1__hdg"><?L 1-3?>Suspended sentences</heading>
    <section class="prov1" eId="sec_1">
      <num><?L 1-4?>1</num>
      <heading eId="sec_1__hdg">Presumption of suspended sentence order</heading>
      <subsection class="prov2" eId="sec_1__subsec_1">
        <num><?L 1-5?>(1)</num>
        <content>
          <p>This section applies where the court <?L 1-6?>imposes a sentence...</p>
        </content>
      </subsection>
    </section>
  </hcontainer>
</part>
```

In this example:
- `<?L 1-1?>` marks page 1, line 1 (at the start of "Part 1")
- `<?L 1-2?>` marks page 1, line 2 (at "Sentencing")
- `<?L 1-6?>` marks page 1, line 6 (mid-paragraph, where a line break occurs in the formatted output)

**Note:** The ellipsis (`...`) in code examples indicates that content has been abbreviated for clarity.

### Placement Within Content

Processing instructions are placed immediately before the text they mark. When a line break occurs within a paragraph, the processing instruction is inserted at that point within the text content:

```xml
<p>about the circumstances in which a person to whom a fixed penalty <?L 11-8?>notice is issued may decline the notice or otherwise object to or challenge <?L 11-9?>it (including the period within which the person may do so and the <?L 11-10?>procedure for doing so),</p>
```

This shows:
- Line 8 of page 11 starts at "notice"
- Line 9 starts at "it"
- Line 10 starts at "procedure"

### Page Transitions

When text continues from one page to the next, the processing instruction simply increments the page number:

```xml
<level class="para1" eId="sec_1__subsec_2__qstr__sec_264A__subsec_2__para_a">
  <num><?L 1-35?>(a)</num>
  <content>
    <p>must be stated in open court, and <?L 2-1?>(b) justify not making the order.</p>
  </content>
</level>
```

Here, line 35 of page 1 transitions to line 1 of page 2 mid-paragraph.

These processing instructions indicate where line and page breaks occur in the formatted PDF output without altering the document's XML structure.

## Conversion to AKN Elements on Export

The processing instructions remain in the XML throughout the editing and amendment process within Lawmaker. When documents are exported for final publication or integration with other systems:

- The processing instructions may be **retained** if the target system supports them and they are needed for downstream processing
- They may be **removed** if the target system does not require page/line information
- They may be **converted** to AKN's `eop` and `eol` elements if required by the target system to comply with strict AKN schema validation

The export configuration determines which approach is used based on the requirements of the receiving system.

The AKN standard provides `eop` and `eol` elements for representing page and line breaks:

### End of Page (eop)

The [`eop`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs_xsd_Element_eop.html) element marks the end of a page.

```xml
<eop number="1"/>
```

The `eop` element supports the following attributes:
- `@number` - The page number
- `@breakAt` - Indicates where the break occurs (e.g., "word", "char")
- `@breakWith` - Specifies the hyphenation character if a word is broken

### End of Line (eol)

The [`eol`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs_xsd_Element_eol.html) element marks the end of a line.

```xml
<eol number="12"/>
```

The `eol` element supports similar attributes:
- `@number` - The line number
- `@breakAt` - Indicates where the break occurs
- `@breakWith` - Specifies the hyphenation character if a word is broken

**Note:** The processing instruction format `<?L page-line?>` combines both page and line information in a single instruction, which differs from the AKN approach where page and line breaks are separate elements.

## Usage in Amendment Wording

Page and line numbers are critical for amendment wording, allowing precise references such as:

- "On page 5, line 12, leave out..."
- "On page 3, line 7, at end insert..."

The processing instruction approach ensures that this information is preserved throughout the drafting process and accurately converted for publication.

## Reference

For more information on the AKN standard's approach to page and line breaks, see [section 5.6 of the AKN standard](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html#_Toc523925049).
