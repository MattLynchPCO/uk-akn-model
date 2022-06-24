# Grouping or higher division elements (above section-level)

These elements appear in the body grouping section-level elements and
are confusingly called "higher division" elements in AKN. We also
include //num and //heading here although they are used in other
contexts.

## //num

The number of the relevant //hcontainer or equivalent object. This
should include whatever is displayed on the page as the number e.g.
"Part 1", not just "1" for a //part, "1.", not just "1" for a //section,
"(3)" not just "3" for a //subsection or similar, "Schedule 1", not just
"1" for a //hcontainer\[@name="schedule"\].

|                                      |                                                         |                                                        |
| ------------------------------------ | ------------------------------------------------------- | ------------------------------------------------------ |
| **Numbered element**                 | **'Normal/regular' number format (in square brackets)** | **Starting 'normal/regular' value in the num element** |
| Group of parts                       | The \[ordinal\] Group of Parts                          | The First Group of Parts                               |
| Part (including within schedules)    | Part \[arabic\]                                         | Part 1                                                 |
| Chapter (including within schedules) | Chapter \[arabic\]                                      | Chapter 1                                              |
| Title (grouping in EU legislation)   | Title \[arabic\]                                        | Title 1                                                |
| Section (grouping in SSI/SI)         | Section \[arabic\]                                      | Section 1                                              |
| Subsection (grouping in SSI/SI)      | Sub-section \[arabic\]                                  | Sub-section 1                                          |
| Cross heading                        | *n.a.*                                                  | *n.a.*                                                 |
| Subheading                           | *n.a.*                                                  | *n.a.*                                                 |

See [Oasis AKN documentation for
//num](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_num.html)

## //heading

The heading to the parent element. Headings should not normally appear
unless associated directly with a grouping container element of some
kind (//hcontainer or //container or some instance of those templates).

Note that //num normally appears before //heading but there are some
exceptions.

See [Oasis AKN documentation for
//heading](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_heading.html)

## //body

This element is not referenced on its own (and therefore does not have
an @eId) but contains the bulk of the content of the Bill, Act, or
SI/SSI that is to have legal effect including the schedules (and
therefore by necessity, the signature blocks that appear after the main
content but before the schedules in most SIs and SSIs).

See [Oasis AKN documentation for
//body](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_body.html)

## //hcontainer\[@name="groupOfParts"\]

This is a rare grouping element above the //part level. It appears in
only 3 UK documents (2 Acts and one SI) each with exactly 3 such
elements and not at all in Scottish legislation so far. See [Armed
Forces Act 2006](https://www.legislation.gov.uk/ukpga/2006/52/contents).
Numbering is ordinal ("The First Group of Parts") and that content
should all appear within the //num element so there is no defined
insertion numbering scheme.

Typically this would appear in the body as @class="group1" and in a
schedule (no known example) as @class="schGroup1".

See [Oasis AKN documentation for
//hcontainer](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html)

## //part

Parts appear normally directly within the //body or schedule
(/hcontainer\[@name="schedule"\]) but can also be grouped on rare
occasions into group of parts (//hcontainer\[@name="groupOfParts"\]).

Parts in the body would normally contain either section (//section) or
equivalent elements (//rule, //hcontainer\[@name="regulation"\],
//article all with @class="prov1"), chapters (//chapter) or cross
headings (//hcontainer\[@name="crossheading"\].

Parts in a schedule (//hcontainer\[@name="schedule"\] would have similar
content except that section would be replaced with schedule paragraphs
(//paragraph\[@class="schProv1"\]).

Although allowed by the AKN schema, the //heading would not normally be
followed by //intro (although this has been used to place notes
appearing immediately after a part heading).

Normally in the body, part would appear with @class="group2" and, in the
schedule, @class="schGroup2".

See [Oasis AKN documentation for
//part](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_part.html)

## //title

Titles appear only in EU legislation and can appear within the //body or
schedule (/hcontainer\[@name="schedule"\]) but normally appear within a
//part.

Titles can contain section (@class="prov1") equivalent elements (//rule,
//hcontainer\[@name="regulation"\], //article), chapters (//chapter),
sections (//section\[@class="group5"\], or cross headings
(//hcontainer\[@name="crossheading"\].

Titles in a schedule (//hcontainer\[@name="schedule"\] would have
similar content except that section-level equivalent would be replaced
with schedule paragraphs (//paragraph\[@class="schProv1"\]).

Although allowed by the AKN schema, the //heading would not normally be
followed by //intro (although this has been used to place notes
appearing immediately after a part heading) except in schedules where no
shedule paragraphs appear.

Normally in the body, title would appear with @class="group3" and, in
the schedule, @class="schGroup3".

See [Oasis AKN documentation for
//title](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_title.html)

## //chapter

Chapters appear normally directly within the //part but can appear on
rare occasions directly in schedule (/hcontainer\[@name="schedule"\]) or
title (EU Legislation only - //title).

Chapters in the body would normally contain either section (//section)
or equivalent elements (//rule, //hcontainer\[@name="regulation"\],
//article all with @class="prov1"), or cross headings
(//hcontainer\[@name="crossheading"\]. In SI/SSIs and schedules,
chapters may also contain sections (//section\[@class="group4").

Chapters in a schedule (//hcontainer\[@name="schedule"\] would have
similar content except that section would be replaced with schedule
paragraphs (//paragraph\[@class="schProv1"\]).

Although allowed by the AKN schema, the //heading would not normally be
followed by //intro (although this has been used to place notes
appearing immediately after a chapter heading) and can occur in
schedules where the chapter does not contain any (numbered) schedule
paragraphs.

Normally in the body, chapter would appear with @class=“group4” and, in
the schedule, @class=“schGroup4”. \[NOTE: originally this was group3 and
schGroup3\].

See [Oasis AKN documentation for
//chapter](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_chapter.html)

## //section (grouping)

Within SIs, SSIs and (to a lesser extent) schedules, section can be used
as a grouping element with @class="group5" or @class="schGroup5" and a
//num element contents of "Section N" where N is normally an Arabic
number. These appear normally in chapters but can appear on rare
occasions directly in schedule (/hcontainer\[@name="schedule"\]) or
title (EU Legislation only - //title).

Grouping sections in the body would normally contain either section
equivalent elements (//rule, //hcontainer\[@name="regulation"\],
//article all with @class="prov1"), grouping subsections (//subsection)
or cross headings (//hcontainer\[@name="crossheading"\].

Grouping sections in a schedule (//hcontainer\[@name="schedule"\] would
have similar content except that section would be replaced with schedule
paragraphs (//paragraph\[@class="schProv1"\]).

Although allowed by the AKN schema, the //heading would not normally be
followed by //intro (although this has been used to place notes
appearing immediately after a chapter heading) and can occur in
schedules where the section does not contain any (numbered) schedule
paragraphs.

Normally in the body, grouping sections would appear with
@class=“group5” and, in the schedule, @class=“schGroup5”.

See [Oasis AKN documentation for
//section](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_section.html)

## //subsection (grouping)

Grouping sections can be further broken into sub-sections. Rather than
defining a new element name with the "-" we use the existing AKN element
//subsection consistent with sub-paragraph and other uses of
sub-section.

Sub-sections in the body would normally contain either
section-equivalent elements (//rule, //hcontainer\[@name="regulation"\],
//article all with @class="prov1"), or cross headings
(//hcontainer\[@name="crossheading"\].

Sub-sections in a schedule (//hcontainer\[@name="schedule"\] would have
similar content except that section-equivalent elements would be
replaced with schedule paragraphs (//paragraph\[@class="schProv1"\]).

Although allowed by the AKN schema, the //heading would not normally be
followed by //intro (although this has been used to place notes
appearing immediately after a chapter heading) and can occur in
schedules where the chapter does not contain any (numbered) schedule
paragraphs.

Normally in the body, sub-sections would appear with @class=“group6”
and, in the schedule, @class=“schGroup6”.

See [Oasis AKN documentation for
//subsection](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_subsection.html)

## //hcontainer\[@name="crossheading"\] (not //crossHeading)

AKN has an element //crossHeading which typically appears as a sibling
of //section in Acts in the English tradition, however, these clearly
function as containers rather than just floating headings (and that is
the behaviour expected in a collapsible table of contents also, so we
prefer to avoid the AKN //crossHeading element and instead prefer to
introduce a grouping element with that name -
//hcontainer\[@name="crossheading"\]. This is more compatible with AKN
principals that containers should wrap the elements they contain and
have a name that reflects their normal name in regular usage.

Crossheadings normally appear within a //part but can appear directly in
the //body or //schedule or, when they appear as grouping elements,
//section or //subsection.

Normally in the body, crossheadings would appear with @class=“group7”
and, in the schedule, @class=“schGroup7”. \[NOTE: formerly these were
group4 and schGroup4 respectively.\]

See [Oasis AKN documentation for *hcontainer\]\] and contrast with
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_crossHeading.html|Oasis
AKN documentation for
//crossHeading](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html)

## //hcontainer\[@name="subheading"\] (not //subheading)

There are some examples in the UK and Scottish legislation (mostly SIs
and SSIs) with multiple levels of cross heading with different
formatting and there is no current convention on distinct names for the
differing levels. These typically occur where something that looks like
a heading to a section-level element or schedule paragraph is followed
by a similar element that has no heading. Often this heading clearly
applies not just to the first provision but also the subsequent
provisions.

Like cross headings, these function more as containers rather than just
floating headings (and that is the behaviour expected in a collapsible
table of contents also, so we prefer to avoid the AKN //subheading
element and avoid nesting //hcontainer\[@name="crossheading"\] so that
we can manage and use the distinct formatting as required with or
without the cross heading context. Therefore we prefer to introduce
another grouping element with a different name -
//hcontainer\[@name="subheading"\].

While historical usage is not careful about distinguishing between
section-level headings, traditional cross-headings and these container
subheadings (which means that you can find examples of subheading
directly in the body, directly in a schedule, within a cross heading or
directly within a part), we strongly recommend the use of normal cross
headings in preference to subheadings and reserve subheadings for use
with crossheading (//hcontainer\[@name="crossheading"\]) at least in
normal usage with the possibility where amending existing legislation of
breaking this convention.

We use in the body, subheadings with @class=“group8” and, in the
schedule, @class=“schGroup8”. \[NOTE: formerly these were group5 and
schGroup5 respectively.\]

See [Oasis AKN documentation for *hcontainer\]\] and contrast with
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_subheading.html|Oasis
AKN documentation for
//subheading](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html)

Note: there may still be a use for //subheading immediately after
//heading particularly within schedules but its use should be limited to
this context where there is no subsequent grouping beyond the schedule
(or schedule grouping element) itself.
