# General Principles

**Note on examples:** The XML examples in this documentation generally omit GUID attributes for clarity and readability. In practice, Lawmaker assigns a GUID attribute to all referenceable elements (see [Element ID Scheme](id-scheme.md#guid) for details).

This document describes guiding principles and naming conventions for elements and attributes in the UK implementation of the [Akoma Ntoso (AKN) XML standard](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html).

## Lower Camel Case for elements and attributes

In line with AKN, lower camel case (lowerCamelCase) is used for all element and attribute names within this implementation. The exception is for elements and attributes in namespaces from other XML vocabularies where appropriate, e.g. [MathML](https://www.w3.org/Math/) , XHTML and CLML.

## Descriptiveness and AKN design patterns

AKN is based around design patterns where elements fall into one of a limited number of content models. From [the documentation](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html#_Toc523925046):

> All elements in this schema fall under one of six content models: hierarchical container, container, subFlow, block, inline and marker. Besides named elements, the schema also provides for a generic element for each of them that can be used for markup and that fits the content models but can be specified by a precise name that is not used in this schema. The 'name' attribute must be used for naming the element. When required, the attribute name gives a name to the element.

In line with AKN's principle of descriptiveness, element names are descriptive and should match the ordinary name of the provision etc. which they represent. Where the relevant element doesn't exist in the AKN schema, generic elements with a descriptive `name` attribute can be used instead. For example:

* `<section>` is an element within the hierarchical container content model, and is used to represent a section (whether that is a section of a Bill or a section grouping within a statutory instrument).
* `<hcontainer name="regulation">` is an example of the generic element `<hcontainer>` together with a `@name` attribute, and is used to represent a regulation within a statutory instrument because `<regulation>` does not specifically exist within the hierarchical content model.

## Document-Level Elements: act and bill

The approach to `<act>` and `<bill>` represents an exception from the general principle of descriptiveness.

All primary and subordinate legislation, in enacted or made form, whether Acts, Statutory Instruments, Statutory Rules etc. use the document-level [`act`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_act.html) element. The `@name` attribute is used to provide further qualification of the document type.

All primary and subordinate legislation in draft form use the [`bill`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_bill.html) element in the AKN standard. Again, the `@name` attribute provides further qualification as to the document type.

For possible `@name` values see [document level elements](data-dictionary/document-level-elements.md).

## Structural Elements

### Use of Hierarchical Containers, Containers and Blocks

This implementation follows the AKN standard in using [the container content model](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_container.html) for whole documents, [the hierarchical container content model](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_hcontainer.html) for hierarchical pure content elements that represent a hierarchical structure within the document, and [the block content model](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_block.html) to contain mixed content displayed in Western European tradition as vertical blocks on a page.

Therefore most named or referenceable elements in a Bill, Act or statutory instrument map to hcontainer-type elements.

Text and mixed content within hierarchical containers will generally be contained within [`heading`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_heading.html) or [`p`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_p.html) elements, both block-type elements. Where such content is not a heading or an ordinary paragraph of text (mostly outside hierarchical containers e.g. on the cover page) [`block`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_block.html) elements with a `@name` attribute to describe the content are used.

### Lists vs Paragraphing

This implementation uses the [`blockList`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_blockList.html) construct for unnumbered, bulleted and numbered lists. These can be single level or nested.

The AKN standard also adopts HTML-style lists [`ul`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_ul.html), and [`ol`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_ol.html) but these are not used in Lawmaker.

However, within hcontainer-type elements, where a sentence is tabulated into numbered paragraphs and sub-paragraphs (e.g. paragraphs numbered (a), (b), (c) etc.), this implementation prefers to use hcontainers to represent those paragraphs and sub-paragraphs rather than a list construct. The [`level`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_level.html) element is used for this purpose rather than [`paragraph`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_paragraph.html) and [`subparagraph`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_subparagraph.html) because of a lack of consistency in naming conventions for these provisions (We use the `@class` attribute to capture the level of paragraphing in which each `level` is nested). The use of hcontainers here allows in particular for further hierarchical content to be represented by hcontainer-type elements within those paragraphs and sub-paragraphs (e.g. definitions).

**Example:** Using `level` for lettered paragraphs within a subsection:

```xml
<subsection class="prov2" eId="sec_1__subsec_3">
  <num>(3)</num>
  <intro eId="sec_1__subsec_3__intro">
    <p>In section 23B (entitlement to bail and the court's function)—</p>
  </intro>
  <level class="para1" eId="sec_1__subsec_3__para_a">
    <num>(a)</num>
    <content>
      <p>at the end of subsection (4) insert "(including submissions in relation to any information provided by an officer of a local authority)",</p>
    </content>
  </level>
  <level class="para1" eId="sec_1__subsec_3__para_b">
    <num>(b)</num>
    <content>
      <p>in subsection (6), after "counsel" insert "or an officer of a local authority",</p>
    </content>
  </level>
</subsection>
```

As hcontainer-type elements are not permitted outside the body of a document (e.g. in the [`preface`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_preface.html), [`preamble`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_preamble.html), and [`conclusions`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_conclusions.html)), the `blockList` construct is used for paragraphed text or [`blockContainer[@class="..."]`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_blockContainer.html) is used for hierarchical structures where, in the body, an hcontainer-type element would be used, with `@class` taking the role of `@name` in this context.

### Use of @class attribute

In addition to using the appropriate descriptive element (or descriptive `@name` attribute on a generic element), Lawmaker uses the [`@class` attribute](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#_Toc523925090) to indicate a similar role/formatting for elements with different names but with similar semantic/presentational role in different document types or contexts.

**Example:** A section in an Act, clause in a Bill, rule in an SI, regulation in an SI, or order in an SI all have `@class="prov1"` (indicating a first level standard provision), even though they have different `@name` values.

```xml
<hcontainer name="regulation" eId="reg_1" class="prov1">
  <num>1</num>
  <heading>Title of regulation</heading>
  <content>
    <p>Content of the regulation.</p>
  </content>
</hcontainer>
```

The AKN schema does not allow for a `@name` attribute for certain generic elements, in particular [`blockContainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_blockContainer) and [`tblock`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_tblock). Where these are used to represent provisions or other entities with specific names, we use the `@class` attribute to fulfil the same role. While this is not the primary intended use of `@class` according to the AKN documentation, it provides a practical solution until future versions of AKN may add `@name` to these elements.

**Example:** Using `@class` to hold the name for a `tblock` element in a preamble:

```xml
<preface eId="preface">
  <tblock class="explanatoryNotesStatement" eId="preface__explNotesStmnt">
    <p>Amendments to the Bill since the previous version are indicated by sidelining in the right margin.</p>
  </tblock>
</preface>
```

See [Element hierarchy and use of @class attribute](type.md) for more detail on specific values of the `@class` attribute.

### Use of blockContainer vs tblock

The Akoma Ntoso standard provides [`tblock`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_tblock) and [`blockContainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_blockContainer) elements with similar capabilities but limited guidance on when to use each. Both are largely permitted in the same contexts and have similar structural capabilities. This implementation adopts the following consistent practice:

**Use `tblock`:**
- For block constructs that would normally appear within a named provision, such as tables, formulas, and similar content which have optional number and heading
- For consistency when an entity may appear both in parts of the document where [`hcontainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_hcontainer) is valid and those where only `tblock` or `blockContainer` are permitted (e.g., [`preamble`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_preamble), [`conclusions`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_conclusions))

**Example:** Using `tblock` for a table structure:

```xml
<tblock class="table" eId="sec_1__subsec_2__tbl__oc_1">
  <foreign>
    <table xmlns="http://www.w3.org/1999/xhtml">
      <thead>
        <tr><th>Column 1</th><th>Column 2</th></tr>
      </thead>
      <tbody>
        <tr><td>Data 1</td><td>Data 2</td></tr>
      </tbody>
    </table>
  </foreign>
</tblock>
```

**Use `blockContainer` in parts where `hcontainer` is not permitted:**
- Where it is replacing what would otherwise be an `hcontainer` if permitted, as `blockContainer` supports [`intro`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_intro), [`wrapUp`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_wrapUp), and [`content`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_content) (although does not require them like `hcontainer` does)
- If `tblock` would be used in the [`body`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_body), it is appropriate to use it whether in the `body` or in parts of the document that don't allow `hcontainer`

## Formatting Elements

### num Elements

All `num` elements contain the number as it appears on the page including brackets, element name, and any punctuation characters if present. For instance for Part 5 the `num` element contains "Part 5" not just "5". For subsection (1) in section 5, the `num` element of the subsection should contain "(1)" (the parent `section` element would contain "5"). The case of the text in the `num` should be sentence case e.g. "Part" not "PART", "Chapter" not "CHAPTER", with the allcaps or smallcaps being treated as a matter of presentation.

To manage re-numbering, an optional attribute @ukl:autonumber="yes|no" can be added to the `num` element. See [LDAPP extensions to AKN](ldapp-extensions.md).

### eop and eol Elements

LDAPP requires the creation and application of amendment wording that makes use of line and page numbers. Therefore we make use of the native AKN elements for marking up end of page (`eop`) and end of line (`eol`) and the native @number, @breakAt and @breakWith attributes (see [section 5.6 of the AKN standard](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html#_Toc523925049)). We are likely to use within the system processing instructions and turn these into `eop` and `eol` elements on export.

### Subheadings

The `subheading` element is a `block` element in AKN intended to be used to supplement the `heading` element (typically immediately after it).

However, subheadings in UK legislation appear below the section (or equivalent) level, sometimes grouping subsections, paragraphs and subparagraphs, etc (see section 2 in the [National Insurance Contributions Act 2014](http://www.legislation.gov.uk/ukpga/2014/7/pdfs/ukpga_20140007_en.pdf)) and sometimes despite identical formatting they are really headings to a particular subsection, paragraph, sub-paragraph etc (see section 3 in the [Modern Slavery Act 2015](http://www.legislation.gov.uk/ukpga/2015/30/pdfs/ukpga_20150030_en.pdf)). We adopt a pragmatic approach to these choosing to use `subsection|level/heading` regardless of whether the heading applies to a single subsection (or lower) or a group of them. This avoids any confusion with the `subheading` element in AKN (which may be used for some schedules or EU legislation but is unlikely to be used in the main body of UK legislation).
