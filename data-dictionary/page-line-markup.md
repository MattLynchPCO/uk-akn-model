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

During the editing phase within Lawmaker, page and line breaks are marked using processing instructions such as:

```xml
<?line number="1"?>
<?page number="1"?>
```

These processing instructions indicate where line and page breaks occur in the formatted output without altering the document's XML structure.

## Conversion to AKN Elements

On export, these processing instructions are converted to the native AKN elements:

### End of Page (eop)

The [`eop`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs_xsd_Element_eop.html) element marks the end of a page.

```xml
<eop/>
```

The `eop` element supports the following attributes (from the AKN standard):
- `@number` - The page number
- `@breakAt` - Indicates where the break occurs (e.g., "word", "char")
- `@breakWith` - Specifies the hyphenation character if a word is broken
### End of Line (eol)

The [`eol`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs_xsd_Element_eol.html) element marks the end of a line.

```xml
<eol/>
```

The `eol` element supports similar attributes:
- `@number` - The line number
- `@breakAt` - Indicates where the break occurs
- `@breakWith` - Specifies the hyphenation character if a word is broken
## Usage in Amendment Wording

Page and line numbers are critical for amendment wording, allowing precise references such as:

- "On page 5, line 12, leave out..."
- "On page 3, line 7, at end insert..."

The processing instruction approach ensures that this information is preserved throughout the drafting process and accurately converted for publication.

## Reference

For more information on the AKN standard's approach to page and line breaks, see [section 5.6 of the AKN standard](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html#_Toc523925049).
