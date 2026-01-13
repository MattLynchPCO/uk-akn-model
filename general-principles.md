# General Principles

**Note on examples:** The XML examples in this document omit GUID attributes for clarity and readability. In actual UK AKN implementation, every referenceable element requires a GUID attribute (see [Element ID Scheme](id-scheme.md#guid) for details).

This document describes guiding principles and naming conventions for elements and attributes in the UK implementation of the [Akoma Ntoso (AKN) XML standard](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html).

## Descriptiveness and the AKN Design Philosophy

AKN is based around design patterns where elements fall into one of a limited number of content models. From [the documentation](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html#_Toc523925046):

> All elements in this schema fall under one of six content models: hierarchical container, container, subFlow, block, inline and markerBesides named elements, the schema also provides for a generic element for each of them that can be used for markup and that fits the content models but can be specified by a precise name that is not used in this schema. The 'name' attribute must be used for naming the element. When required, the attribute name gives a name to the element.

In line with AKN's principle of descriptiveness, element names are descriptive and should match the ordinary name of the provision etc. which they represent. Where the relevant element doesn't exist in the AKN schema, generic elements with a descriptive `name` attribute can be used instead. For example:

* `<section>` is an element within the hierarchical container content model, and is used to represent a section (whether that is a section of a Bill or a section grouping within a statutory instrument).
* `<hcontainer name="regulation">` is an example of the generic element `<hcontainer>` together with a `@name` attribute, and is used to represent a regulation within a statutory instrument because `<regulation>` does not specifically exist within the hierarchical content model.

## Use of @name and @class

In line with the Akoma Ntoso standard, where a provision or other legislative entity has a consistent name, we use the matching element in Akoma Ntoso if it exists or, if it does not, we use the provision's name in the [`@name` attribute](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#_Toc523925107) of [`hcontainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_hcontainer) (or equivalent named element). The [`@class` attribute](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#_Toc523925090) is used to specify consistent formatting for elements with different names but similar formatting in different document types or contexts.

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

The AKN schema does not provide a `@name` attribute for certain elements, in particular [`blockContainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_blockContainer) and [`tblock`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_tblock). Where these are used to represent provisions or other entities with specific names, we use the `@class` attribute to hold the name rather than introducing a new namespace attribute. While this is not the primary intended use of `@class` according to the AKN documentation, it provides a practical solution until future versions of AKN may add `@name` to these elements.

**Example:** Using `@class` to hold the name for a `tblock` element in a preamble:

```xml
<preface eId="preface">
  <tblock class="explanatoryNotesStatement" eId="preface__explNotesStmnt">
    <p>Amendments to the Bill since the previous version are indicated by sidelining in the right margin.</p>
  </tblock>
</preface>
```

A [proposal for the different @class values](type.md) appears separately.

## Element Naming Conventions

### Lower Camel Case

In line with AKN, lower camel case (lowerCamelCase) is used for all element and attribute names within this implementation. The exception is for elements and attributes in namespaces from other XML vocabularies including [MathML](https://www.w3.org/Math/) and possibly XHTML and CLML (the latter primarily for metadata).

### Document-Level Elements: act and bill

The approach to `<act>` and `<bill>` represents an exception from the general principle of descriptiveness.

All primary and subordinate legislation, in enacted or made form, whether Acts, Statutory Instruments, Statutory Rules etc. use the document-level [`act`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_act.html) element. The `@name` attribute is used to provide further qualification of the document type.

All primary and subordinate legislation in draft form use the [`bill`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_bill.html) element in the AKN standard. Again, the `@name` attribute provides further qualification as to the document type.

For possible `@name` values see [document level elements](data-dictionary/document-level-elements.md).

## Structural Elements

### Use of Hierarchical Containers, Containers and Blocks

This implementation follows the AKN standard in using [the container content model](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_container.html) for whole documents, [the hierarchical container content model](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_hcontainer.html) for hierarchical pure content elements that represent a hierarchical structure within the document, and [the block content model](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_block.html) to contain mixed content displayed in Western European tradition as vertical blocks on a page.

Therefore most named or referenceable elements in a Bill, Act or statutory instrument map to hcontainer-type elements.

Text and mixed content within hierarchical containers will generally be contained within [`heading`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_heading.html) or [`p`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_p.html) elements, both block-type elements. Where such content is not a heading or an ordinary paragraph of text (mostly outside hierarchical containers e.g. on the cover page) [`block`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_block.html) elements with a `@name` attribute to describe the content are used.

### Use of blockContainer vs tblock

The Akoma Ntoso standard provides [`tblock`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_tblock) and [`blockContainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_blockContainer) elements with similar capabilities but limited guidance on when to use each. Both are largely permitted in the same contexts and have similar structural capabilities. This implementation adopts the following consistent practice:

**Use `tblock` for:**
- Block constructs that would normally appear within a named provision, such as tables, formulas, and similar content which have optional number and heading
- Consistency between parts of the document where [`hcontainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_hcontainer) is valid and those where only `tblock` or `blockContainer` are permitted (e.g., [`preamble`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_preamble), [`conclusions`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_conclusions))

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

### Lists vs Paragraphing

This implementation uses the [`blockList`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_blockList.html) construct for unnumbered, bulleted and numbered lists. These can be single level or nested.

The AKN standard also adopts HTML-style lists [`ul`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_ul.html), and [`ol`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_ol.html) but these are not used in Lawmaker.

However, within hcontainer-type elements, where a sentence is tabulated into numbered paragraphs and sub-paragraphs (e.g. paragraphs numbered (a), (b), (c) etc.), this implementation prefers to use hcontainers to represent those paragraphs and sub-paragraphs rather than a list construct. The [`level`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_level.html) element is used for this purpose rather than [`paragraph`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_paragraph.html) and [`subparagraph`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_subparagraph.html) because of a lack of consistency in naming conventions for these provisions. The use of hcontainers here allows in particular for further hierarchical content to be represented by hcontainer-type elements within those paragraphs and sub-paragraphs (e.g. definitions).

As hcontainer-type elements are not permitted outside the body of a document (e.g. in the [`preface`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_preface.html), [`preamble`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_preamble.html), and [`conclusions`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_conclusions.html)), the `blockList` construct is used for paragraphed text or [`blockContainer[@class="..."]`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_blockContainer.html) is used for hierarchical structures where, in the body, an hcontainer-type element would be used, with `@class` taking the role of `@name` in this context.

### Use of level

There was a robust discussion within our team about how to deal with hierarchical containers normally numbered with lower alphabetic characters in brackets (e.g., "(a)"), often but not always called "paragraph". We originally used the [`paragraph`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_paragraph) element (a specialization of `hcontainer`) or [`subparagraph`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_subparagraph) depending on the context. However, we discovered that the naming conventions were not as consistent as we would like, with different documents within the same collection naming these elements differently.

We considered the practice used by many European jurisdictions of using one of the numbered list constructs ([`blockList/item`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_blockList) or [`ol/li`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_ol)), which would have avoided the naming controversy altogether. However, this approach prevents `hcontainer` being used within these constructs. As definitions can occur at these lower levels, we wanted to preserve the `hcontainer` model for definitions and any other similar constructs that were more naturally represented as `hcontainer` elements.

Therefore, we use the [`level`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_level) element, which is an unnamed `hcontainer` element. We use the `@class` attribute to capture the level of paragraphing in which each `level` is nested (particularly necessary within amendment wording and the [`quotedStructure`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_quotedStructure) element).

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

**Note:** The trailing commas in the paragraph text above are intentional and reflect the legal formatting conventions used in UK legislation, where list items within amendment text are punctuated as part of a continuous sentence.

This approach allows `hcontainer` elements (such as definitions) to be nested within `level` elements while maintaining a consistent structure for lettered provisions.

The English tradition of paragraphing is far less common in European jurisdictions and AKN often uses `list` or equivalent HTML `ol` or `ul` for similar nesting constructs to those that are central to the English legislative drafting tradition. These constructs have particular names in the English tradition. In the UK, the tradition is to use "paragraph", "sub-paragraph", "sub-sub-paragraph", etc., but "paragraph" is used for elements with `@class="para1"` or `@class="prov2"` or `@class="schProv1"` and occasionally even prov1 and schProv1. While other Commonwealth jurisdictions use of the "-" varies (and Canada uses much more consistent "paragraph", "subparagraph", "clause", "subclause", "item", "subitem"), because the naming is inconsistent in the UK it was thought best to use consistent element names `level` (the unnamed hierarchical element) and use the `@class` attribute to determine formatting and context rules. Unlike the European tradition that uses unnamed and highly variant list structures, these elements are hierarchical and we reserve the use of `list` for true lists that aren't otherwise named hierarchical structures and completely avoid the redundant `ol` and `ul` HTML elements.

## Specific Element Guidelines

### "section" and Similar Constructs

The structural function (and formatting for the large part) of a rule, regulation, by-law, article or paragraph in a Statutory Instrument or clause in a Bill is pretty much identical to that for a section in an Act. However, these are variously `section` in an Act, `rule` in Rules, `hcontainer[@name="regulation"]` in Regulations, `article` (or `paragraph`) in an Order. Currently, UK Bills use `section` despite the fact that external references to these elements call them "clauses". Within the Bill itself, reference wording uses "section" reflecting the fact that, once enacted, that is what it will be called. We therefore wholly support the use of `section` within Bills.

Also sections (and their equivalents in subordinate legislation) are structurally unique and not like other `hcontainer` elements which nearly always group sections (I suspect this is largely because the European equivalent `article` is formatted much more like `part` than it is like `section`) but don't restart numbering (again unlike `article` in European legislation). Likewise all other elements that typically appear within a section or equivalent such as `subsection`, `paragraph`, and possibly `list`, `sublist`, `item` (no `subitem`?) are structurally different to grouping elements (e.g. `part`, `chapter`, and `order` - UK does not seem to use `subpart`, `division`, or `subdivision` unlike other Commonwealth jurisdictions or `title` and `subtitle` used in addition to all the others in the US). The lower level elements have distinct formatting patterns including nested indentation not normally seen in the grouping elements above the section level. These grouping elements historically have a centred number (e.g. "Part 1") with a centred heading immediately below (increasingly they are centred with the number and heading on the same line separated by a dash or left aligned separated by a tab) and group sections (or their equivalent).

We note also that Articles are likely to appear in schedules containing treaties, European legislation and some agreements. They will not be formatted like `section` in that context and `hcontainer[@name="article"]` is supposed to be logically equivalent to `article` whether in `body/article` or `hcontainer[@name="schedule"]/article`.

To complicate matters further "section" is sometimes a grouping construct within a schedule or possibly the body of an SI with formatting more like a `part` or `chapter`.

There are four potential solutions for this:

1. use the referenceable name regardless of context and use the existing @class attribute (or add a new attribute) to drive formatting (and conversion to CLML);
2. use `section` in Acts, Bills and SIs and add a @name attribute to guide the reference wording - note that in the UK unlike many English-speaking jurisdictions, the formatting and content model for section-like elements in Statutory Instruments is slightly different so formatting rules will require context and introduce a new element or elements for the grouping use of section (e.g. `si-section`, `sched-section`, `group-section`);
3. use `section` within an Act or Bill but use `si-section` with an appropriate @name attribute in Statutory Instruments so there is a simple element-driven rule for formatting (this would also require another element for the grouping use of section as above); or
4. use `section` in Act and Bill, `rule`, `regulation`, `si-article` and `si-paragraph` (or similar) so that the formatting of a body paragraph can be distinguished from lower level paragraph beginning with (a).

As we believe the first option to be most consistent with AKN and it allows for relatively efficient formatting and simpler stylesheets, we are adopting the first approach.

### "paragraph"

Paragraph is particularly problematic as, depending on the context, the referenceable object called a paragraph can appear at different structural levels. In some Statutory Instruments, it is the logical equivalent of `section` (although slightly different in formatting and content rules). Also in a Schedule, paragraph looks more like a `section` in the body of an Act. If a paragraph numbered (a) appears within a schedule paragraph that looks more like a section, there is some disagreement as to whether it is a sub-paragraph, a paragraph, or (if also within a subsection-like context) a sub-sub-paragraph.

Similar issues then present themselves for disambiguating the different usages of the name "paragraph" to that of "section" and similar looking constructs.

Because we cannot rely on the name being used consistently, we adopt `level` as an unnamed `hcontainer` and use the @class element as described above.

Given that the named element `subparagraph` exists in AKN, we will use it rather than creating a new `hcontainer[@name="sub-paragraph"]` and by analogy use `hcontainer[@name="subsubparagraph"]` and `hcontainer[@name="subsubsubparagraph"]` if nested equivalent are required.

### "formula"

The AKN element `formula` looks like it is intended for the enacting words or similar. However the name "formula" in UK legislation is more often used to refer to a mathematical equation. The recommended solution for mathematical equations is to use `foreign` to wrap MathML (see section 5.14 of the [AKN Core Version 1.0 Part 1 Vocabulary](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/akn-core-v1.0-part1-vocabulary.html)). This doesn't support inline equations as `foreign` is a block element.

This doesn't really allow us to identify something as a formula with just an image where legacy data hasn't been converted.

For normal block mathematical formulas we will use a new `tblock[@name="formula"]` which supports either an `img` or `foreign` or both.

The `subFlow` element (or a similar construct) will need to be used to code inline formulas (`tblock[@name="formula"]`) as inline formulas will still need image alternatives.

Note also that `math` (from MathML not AKN) has the following attributes which are also relevant to these issues:

- @display="block|inline" to distinguish whether the formula should be inline with text or a separate block;
- @altimg="URI" to point to an alternative image for the formula (and @altimg-width, @altimg-height and @altimg-valign for controlling the display of that image)

## Formatting Elements

### num and heading Elements

All `num` elements should contain the number as it appears on the page including brackets, element name, and any punctuation characters if present (this is consistent with the examples provided in the AKN standard). For instance for Part 5 the `num` element should contain "Part 5" not just "5". For subsection 5(1), the `num` element should contain "(1)" (the parent `section` element would contain "5" (or "5." if legacy style)). The case of the name component should be mixed case e.g. "Part" not "PART", "Chapter" not "CHAPTER".

To manage re-numbering, we introduce a new optional attribute @ukl:renumber="yes|no" (with "yes" as the default value). See [LDAPP extensions to AKN](ldapp-extensions.md).

### eop and eol Elements

LDAPP requires the creation and application of amendment wording that makes use of line and page numbers. Therefore we make use of the native AKN elements for marking up end of page (`eop`) and end of line (`eol`) and the native @number, @breakAt and @breakWith attributes (see [section 5.6 of the AKN standard](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html#_Toc523925049)). We are likely to use within the system processing instructions and turn these into `eop` and `eol` elements on export.

### Subheadings

The `subheading` element is a `block` element in AKN intended to be used to supplement the `heading` element (typically immediately after it).

However, subheadings in UK legislation appear below the section (or equivalent) level, sometimes grouping subsections, paragraphs and subparagraphs, etc (see section 2 in the [National Insurance Contributions Act 2014](http://www.legislation.gov.uk/ukpga/2014/7/pdfs/ukpga_20140007_en.pdf)) and sometimes despite identical formatting they are really headings to a particular subsection, paragraph, sub-paragraph etc (see section 3 in the [Modern Slavery Act 2015](http://www.legislation.gov.uk/ukpga/2015/30/pdfs/ukpga_20150030_en.pdf)). We adopt a pragmatic approach to these choosing to use `subsection|level/heading` regardless of whether the heading applies to a single subsection (or lower) or a group of them. This avoids any confusion with the `subheading` element in AKN (which may be used for some schedules or EU legislation but is unlikely to be used in the main body of UK legislation).
