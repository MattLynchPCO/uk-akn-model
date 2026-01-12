# Element ID Scheme and References

This document describes the identifier scheme used for elements in UK legislation following the [Akoma Ntoso (AKN) naming conventions](https://docs.oasis-open.org/legaldocml/akn-nc/v1.0/os/akn-nc-v1.0-os.html). It covers both the `@eId` attribute for structural identification and the `@GUID` attribute for persistent references.

## Cross-Reference Requirements

### Section-level elements and below

The most common cross-references are to section-level elements and
below. A reference to a section-level element typically does not refer
to any grouping elements that contain it. For example, ‘section 53’ is
quite common, and ‘section 53 of Chapter 3 of Part I’ is extremely rare.
Occasionally amendment wording will refer to the grouping element in
which a new section is to be inserted where there is some ambiguity as
to which grouping element the new section would belong but the different
parts of the reference are typically separated by intervening amendment
text (‘After section 53 the following section is inserted in Chapter 3’
or ‘Chapter 3 of Part I is amended by inserting the following section
after section 53’).

For elements below the section level, there is either a long form or a
short form. The long form is something like ‘paragraph (a) of subsection
(1) of section 53’ where each element in the hierarchy is identified
individually by the type of element and the number portion of the label.
The shortened form is like either ‘paragraph 53(1)(a)’ or ‘section
53(1)(a)’ (more typically the latter) where a single word identifies
only the type of element the first element or the last element (examples
of both occur in Singapore legislation). The number from the labels of
each referencable element from the section-level down to the target
element is also required.

In references to definitions or to target elements within definitions,
the number from the label is replaced with the defined term in quotes
(‘the definition of “today” in section 3’, ‘sub-paragraph (a)(ii)(C)
of the definition of “Director” in subsection 4(1)’). The shortened form
is only partially used in references to definitions because there is no
way to shorten the definition component of the cross-reference. This
breaks the cross-reference into three parts, the shortened form of
reference to the parent of the definition, the definition component, and
the shortened form of the reference to all the elements below the
definition in the document hierarchy.

### Grouping elements

For grouping elements that have a //num, the wording typically refers to
the target element and all referencable elements above the target
element. Again there is a long form and a short form. For example,
references to ‘Chapter 3 of Part I’ will always contain a reference to
the target element (Chapter 3) and the containing grouping element (Part
1) although the order may vary in different contexts (e.g. ‘Chapter I.3’
is used in some jurisdictions and these shortened forms are more common
in summaries of amendments). Any reference to ‘Chapter 3’ without the
qualifying ‘Part I’ would assume the context in which the
cross-reference occurs so the Part component is implicit.

The reference to each element typically comprises words identifying the
type of element (“Part”, “Chapter”) either explicitly or implicitly, and
the number (“3”, “I”). We include both in the //num content. Such
elements typically have only a single heading which requires no number
(e.g. ‘the heading to Part I’, ‘Chapter I.3: Heading’). Given that a
hypertext link to the heading and one to the whole element would
essentially point to the same place in the document, it is not strictly
necessary to give the heading a separate ID for reference purposes but
it can be useful for amendment wording and consolidation purposes.

The generic group elements (//hcontainer\[@name="crossheading"\] and
//hcontainer\[@name="subheading"\]) typically have a //heading but no
//num, which necessitates an alternative mechanism for identifying them.
The two major alternatives in reference wording are to quote the entire
heading (e.g. ‘the crossheading “Introduction”’) including any higher
level grouping elements with //num elements as context (e.g. ‘the
crossheading “Introduction” in Part I’), or to use the following section
to locate the heading (e.g. ‘the crossheading immediately preceding
section 53’). Reference wording to such elements rarely addresses them
as a whole (e.g. ‘the sections grouped under the crossheading
“Introduction”’). It is more typical to refer to the heading and
sections separately (e.g. ‘the crossheading “Introduction” and sections
53 to 58’ or ‘sections 53 to 58 and the crossheading immediately
preceding them’).

This suggests that such headings could be treated as siblings of the
sections without a containing element. The problem with that approach is
that the group heading would occupy the same position in the element
hierarchy as any containing element heading (i.e. if the unnumbered
heading appears within Part V, 'the heading to Part V' and the grouping
heading would both match the XPath expression //body/part/heading making
the rules for rendering horrendously complicated. AKN solves this by
introducing the //crossHeading element distinct from the //heading but
this still ignores the semantic intent that the sections underneath that
heading are somehow grouped together. Therefore we have chosen to use a
container element to reflect the logical containment even if reference
wording wouldn't always recognize the containment relationship in this
instance.

### Other elements

Elements within the front matter of legislative documents are referred
to in similar ways to section-level elements (e.g. ‘the Preamble’, ‘the
long title’, ‘the short title’). Note that there would only ever be one
of each of these elements in a given Act or Bill. These elements
occasionally are further broken down into paragraphs and lower elements.
Such lower level elements are referred to in much the same way as if
they appeared in a section (e.g. ‘sub-paragraph (b)(iii) of the
Preamble’)

Elements within Schedules, Appendices and Annexures often include
references to grouping elements above them even if they are like
section-level elements (although Codes typically behave as though the
Code itself was a separate document and don’t include the grouping
elements).

## @eId

The `@eId` attribute provides a human-readable structural identifier for elements. See the [AKN naming conventions specification](https://docs.oasis-open.org/legaldocml/akn-nc/v1.0/os/akn-nc-v1.0-os.html#_Toc531692303) including the list of standard abbreviations.

The AKN standard recommends using an optional *prefix*, an *element_ref* (essentially the name or abbreviated name of the element), and the *number* (possibly empty). The prefix is the identifier of any containing component necessary to ensure uniqueness of the ID - in practice the prefix will usually be the eId of the parent element. The default separator between the *prefix* and *element_ref* is double underscore (`__`) and between the *element_ref* and the *number* is single underscore (`_`).

Despite CLML using simpler separators, this implementation follows the AKN naming convention closely. CLML uses "-" as the separator in IDs and "/" as the separator in URIs and avoids the *element_ref* for common structures within a [`section`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_section.html) or equivalent.

### element_ref Component

Although the abbreviations listed in the AKN naming conventions documentation are not always standard in a UK context (e.g., "sec" instead of "s" for section, "dvs" instead of "div" for division, "chp" instead of "cap" for chapter), this implementation follows the AKN standard where specified for consistency and interoperability. However, to keep eIds to a reasonable length, we have adopted other abbreviations for elements for which there is not a conventional abbreviation in the documentation, in particular for provisions that are represented as `<hcontainer name="element_name">`.

The following table describes the abbreviations used in this implementation and their source:

|                       |                  |            |                                                       |
| --------------------- | ---------------- | ---------- | ----------------------------------------------------- |
| **XML element/@name** | **element\_ref** | **Source** | **Comments**                                          |
| \<amendmentBody\>     | body             | AKN        |                                                       |
| \<article\>           | art              | AKN        |                                                       |
| \<attachment\>        | att              | AKN        |                                                       |
| \<blockList\>         | list             | AKN        |                                                       |
| \<chapter\>           | chp              | AKN        |                                                       |
| \<clause\>            | cl               | AKN        |                                                       |
| \<component\>         | cmp              | AKN        |                                                       |
| \<intro\>             | intro            | AKN        |                                                       |
| \<list\>              | list             | AKN        |                                                       |
| \<listIntroduction\>  | intro            | AKN        |                                                       |
| \<listWrapUp\>        | wrapup           | AKN        |                                                       |
| \<mainBody\>          | body             | AKN        |                                                       |
| \<paragraph\>         | para             | AKN        |                                                       |
| \<quotedStructure\>   | qstr             | AKN        |                                                       |
| \<quotedText\>        | qtext            | AKN        |                                                       |
| \<section\>           | sec              | AKN        |                                                       |
| \<subchapter\>        | subchp           | AKN        |                                                       |
| \<subparagraph\>      | subpara          | AKN        |                                                       |
| \<subsection\>        | subsec           | AKN        |                                                       |
| \<wrapUp\>            | wrapup           | AKN        |                                                       |
| @name="definition"    | def              | Lawmaker   | Note that //def content will be used instead of //num |
| @name="schedule"      | sch              | Lawmaker   |                                                       |
| @name="crossheading"  | xhdg             | Lawmaker   |                                                       |
| @name="step"          | step             | Lawmaker   |                                                       |

### number Component

The [`num`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_num) element is converted into the *number* component of the `@eId` by stripping out the redundant element name component if present (the *element_ref* component already provides this information) and any non-name characters including spaces, punctuation, and brackets. For example, from "Part 1" you get "1".

For element that are numbered this is sufficient to uniquely identify the element. The two major exceptions are definitions and grouping elements without a `num`.

#### Definitions

For definitions, the *number* component is replaced with the defined term from the [`def`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_def) element, with any non-name characters (and occurrences of "-") removed (e.g., 'the definition of "captain's table"' becomes 'captainstable' in the *number* component, with a full `@eId` like 'sec_1__def__captainstable'). For bilingual publication of legislation, it is desirable to include the defined term in both languages in each language rendition. The AKN standard does not provide a standard solution for this, but when needed, the English term would be available in any Welsh or Gaelic rendition that is created.

**Example:**

```xml
<hcontainer name="definition" eId="sec_1__def__captainstable" class="definition">
  <content>
    <p><def>captain's table</def> means the table at which the captain dines;</p>
  </content>
</hcontainer>
```

#### Unnumbered Grouping Elements

To uniquely identify grouping elements without a [`num`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_num) (such as `hcontainer[@name="crossheading"]` and possibly [`level`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_level)), it is necessary to find some alternative for the *number* for each element.

Lawmaker uses the number of the first descendant section in place of the missing `num`. This approach:

- Is guaranteed unique within context
- Is based on one of the two reference forms
- Is easy for users to understand
- Can be allocated in any language rendition independently
- Won't change if the text of the heading changes, but will change if new sections are inserted or the first section is renumbered

**Example:**

For a crossheading that contains sections 15, 16, and 17, the `@eId` would be `xhdg_15`, using the number from the first section (15) within the grouping element.

```xml
<hcontainer name="crossheading" eId="part_1__xhdg_15">
  <heading>Financial Provisions</heading>
  <section eId="sec_15">
    <num>15</num>
    <heading>Funding</heading>
    <content>...</content>
  </section>
  <section eId="sec_16">
    <num>16</num>
    <heading>Payments</heading>
    <content>...</content>
  </section>
</hcontainer>
```

### Duplicate @eId values

If after all of these calculations are applied, a duplicate ID would occur
within a single document, an additional component is inserted at the level the duplication occurs in the form `oc_x' where 'x' is the number of the occurrence of the element with the ID preceding the
‘oc’ component.

For example, if there were two sections immediately following one another with the same number 15, they would be assigned eIds `sec_15__oc_1` and `sec_15__oc_2`.

## @GUID

The `@GUID` attribute in the AKN standard is described as follows:

> This attribute is an application-specific identifier that a local implementation may need to add to elements according to local rules and syntaxes. GUID is not a required attribute. Its use and specification is totally dependent on the representation and storage requirements of the author of the Manifestation. Despite the name, GUIDs do not even have to be globally unique across documents of the same collection.

This implementation requires the `@GUID` attribute on every referenceable element to ensure cross-references can be updated reliably. The values are required to be unique at least within the system and are allocated compliant with the [GUID standard](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=netframework-4.7.2) (which is Microsoft's name for a [UUID](https://tools.ietf.org/html/rfc4122)). To ensure that the `@GUID` value is a valid NMTOKEN and can therefore be treated as an XML ID, the serialized form of the GUID is prefixed with "_".
