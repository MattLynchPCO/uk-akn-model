# Guiding Principles

## Use of @name and @class

Following in the spirit of the Akoma Ntoso standard, where elements have a consistent name, we use that name in the [`@name` attribute](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#_Toc523925107) of [`hcontainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_hcontainer) (or equivalent named element). The [`@class` attribute](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#_Toc523925090) is used to specify consistent formatting for elements with different names but similar formatting in different document types or contexts.

**Example:** A section in an Act, clause in a Bill, rule in an SI, regulation in an SI, or order in an SI all have `@class="prov1"` (indicating a first level standard provision), even though they have different `@name` values.

```xml
<hcontainer name="section" eId="sec_1" class="prov1">
  <num>1</num>
  <heading>Title of section</heading>
  <content>
    <p>Content of the section.</p>
  </content>
</hcontainer>
```

The AKN schema does not provide a `@name` attribute for certain elements, in particular [`blockContainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_blockContainer) and [`tblock`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_tblock). Where a consistent name is applied to these elements, we use the `@class` attribute to hold the name rather than introducing a new namespace attribute. While this is not the primary intended use of `@class` according to the AKN documentation, it provides a practical solution until future versions of AKN may add `@name` to these elements.

**Example:** Using `@class` to hold the name for a `tblock` element:

```xml
<tblock class="explanatoryNotesStatement" eId="preface__explNotesStmnt">
  <p>Amendments to the Bill since the previous version are indicated by sidelining in the right margin.</p>
</tblock>
```

## Use of blockContainer vs tblock

The Akoma Ntoso standard provides [`tblock`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_tblock) and [`blockContainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_blockContainer) elements with similar capabilities but limited guidance on when to use each. Both are largely permitted in the same contexts and have similar structural capabilities. This implementation adopts the following consistent practice:

**Use `tblock` for:**
- Block constructs that would normally appear within a named provision, such as tables, formulas, and similar content which have optional number and heading
- Consistency between parts of the document where [`hcontainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_hcontainer) is valid and those where only `tblock` or `blockContainer` are permitted (e.g., [`preamble`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_preamble), [`conclusions`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_conclusions))

**Example:** Using `tblock` in a preamble:

```xml
<preface eId="preface">
  <tblock class="explanatoryNotesStatement" eId="preface__explNotesStmnt">
    <p>Amendments to the Bill since the previous version are indicated by sidelining in the right margin.</p>
  </tblock>
</preface>
```

**Use `blockContainer` in parts where `hcontainer` is not permitted:**
- Where it is replacing what would otherwise be an `hcontainer` if permitted, as `blockContainer` supports [`intro`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_intro), [`wrapUp`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_wrapUp), and [`content`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_content) (although does not require them like `hcontainer` does)
- If `tblock` would be used in the [`body`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_body), it is appropriate to use it whether in the `body` or in parts of the document that don't allow `hcontainer`

## Use of level

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

This approach allows `hcontainer` elements (such as definitions) to be nested within `level` elements while maintaining a consistent structure for lettered provisions.
