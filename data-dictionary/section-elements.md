# Section-level and below standard elements

This page covers elements at or below the section level in a Bill, Act or statutory instrument etc.

"Section level" provisions are:

* In Bills and Acts: sections (sometime refered to as "clauses") and schedule paragraphs.
* In Statutory Instruments: regulations, articles, rules and schedule paragraphs.
* In EU legislation: articles.

|                                                        |                                                         |                                                        |
| ------------------------------------------------------ | ------------------------------------------------------- | ------------------------------------------------------ |
| **Numbered element**                                   | **'Normal/regular' number format (in square brackets)** | **Starting 'normal/regular' value in the num element** |
| Section, Clause (@class="prov1")                       | \[arabic\]                                              | 1                                                      |
| Rule, Regulation, Article (@class="prov1")             | \[arabic\].                                             | 1.                                                     |
| Subsection (@class="prov2")                            | (\[arabic\])                                            | (1)                                                    |
| SI paragraph (@class="prov2")                          | (\[arabic\])                                            | (1)                                                    |
| Schedule paragraph (@class="schProv1")                 | \[arabic\]                                              | 1                                                      |
| Schedule subparagraph (@class="schProv2")              | (\[arabic\])                                            | (1)                                                    |
| Step                                                   | Step \[arabic\]                                         | Step 1                                                 |
| Table                                                  | Table \[arabic\]                                        | Table 1                                                |
| Schedule                                               | Schedule \[arabic\]\*                                   | Schedule                                               |

\* NB: if only one schedule, no number is assigned (the //num content is
"Schedule"); when there are 2 schedules, "Schedule *N*" appears in all
the schedule //num's including the first one e.g. “Schedule 1” and the
second is “Schedule 2”.

## Paragraphing of provisions

When sections, subsections, regulations, articles, SI paragraphs, Schedule paragraphs etc. are further tabulated into numbered paragraphs/sub-paragraphs and so on, the following applies in terms of numbering. Naming of these provisions isn't always consistent:
they may be described as "paragraphs", "sub-paragraphs", "heads", "points" or "sub-sub-paragraph" depending on the context. In Lawmaker, the `level` element is used together with a `@class` attribute to model these kinds of paragraphs.

|                                                         |                                                              |                                           |
| ------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------- |
| **Numbered element**                                    | **'Normal/regular' number format (in square brackets)**      | \*\*Starting 'normal/regular' number \*\* |
| 1st level (@class="para1")                              | (\[lowercase alphabetical\])                                 | (a)                                       |
| 2nd level (@class="para2")                              | (\[lowercase roman\])                                        | (i)                                       |
| 3rd level (@class="para3")                              | (\[double lowercase alphabetical\])                          | (aa)                                      |
| 3rd level (@class="para3")                              | (\[uppercase alphabetical\])                                 | (A)                                       |


**Note:** In contexts that don't allow //hcontainer, we use //blockContainer\[@class="para*N*"\] as an alternative (e.g. //preface,
//preamble, //conclusions etc.).

## Section level elements - @class="prov1", "schProv1" and "EUProv1"

These classes are associated with the standard section-level element within legislative documents. The following elements are used:

* `<section class="prov1">` (Primary legislation)
* `<article class="prov1">` (Secondary legislation)
* `<hcontainer name="regulation" class="prov1">` (Secondary legislation)
* `<rule class="prov1">` (Secondary legislation)
* `<paragraph class="schProv1">` (within schedules of both Primary and Secondary legislation)
* `<article class="EUProv1">` (EU legislation)

These elements, with the exception of  `paragraph`, should normally contain both a `num` and a `heading`. A `section` in UKP, SP and SC Bills will contain these in the following order

```
<section>
   <num/>
   <heading/>
...
</section>
```

In secondary legislation, and sections in NI Bills, the order is as follows:

```
<section>
   <heading/>
   <num/>
...
</section>
```

The schedule `paragraph` should normally contain a `num` but not a `heading` (and may be unnumbered).

For Bills and Acts see [Oasis AKN documentation for
//section](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_section.html)

For SIs/SSIs see [Oasis AKN documentation for //rule](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_rule.html), [Oasis AKN documentation for //article](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_article.html), and, where AKN doesn't provide a specific element (such as for "regulation"), [Oasis AKN documentation for //hcontainer](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_hcontainer.html)

## Subsection level elements - @class="prov2", "schProv2" and "EUProv2"

These classes are associated with the standard subsection-level element within legislative documents. The following elements are used:

* `<subsection class="prov2">` (Primary legislation)
* `<paragraph class="prov2">` (Secondary legislation)
* `<subparagraph class="schProv2">` (within schedules of both Primary and Secondary legislation)
* `<paragraph class="EUProv2">` (EU legislation)

These elements should normally contain a `num` but not usually a `heading`.

* [Oasis AKN documentation for
//subsection](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_subsection.html)
* [Oasis AKN documentation for
//paragraph](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_paragraph.html)

## Subheadings
Section-level elements are occasionally divided by subheadings in addition to the standard subdivsions (e.g. subsections). See, for example, [section 2 of the National Insurance Contributions Act 2014](https://www.legislation.gov.uk/ukpga/2014/7/section/2) and section 3 of the [Modern Slavery Act 2015](http://www.legislation.gov.uk/ukpga/2015/30/pdfs/ukpga_20150030_en.pdf).

Lawmaker implements a pragmatic approach and treats these subheadings as headings of the subdivision they proceed rather than as headings of a separate grouping element. For example:

```
<section>
   <num>2</num>
   <heading>Exceptions</heading>
   <subsection>
      <heading>Public authorities</heading>
      <num>(1)</num>
      <content>
         <p>A person cannot qualify for an employment allowance for a tax year if, at any time in the tax year, the person is a public authority which is not a charity.</p>
      </content>
   </subsection>
   <subsection>
      <num>(2)</num>
      <intro>
         <p>In subsection (1)—</p>
      </intro>
      <hcontainer name="definition">
         <content>
            <p>“<def>charity</def>” has the same meaning as in the Small Charitable Donations Act 2012 (see section 18(1) of that Act), and</p>
         </content>
      </hcontainer>
      <hcontainer name="definition">
         <content>
            <p>“<def>public authority</def>” includes any person whose activities involve, wholly or mainly, the performance of functions (whether or not in the United Kingdom) which are of a public nature.</p>
         </content>
      </hcontainer>
   </subsection>
   <subsection>
      <heading>Personal, family or household affairs</heading>
      <num>(3)</num>
      <content>
         <p>Liabilities to pay secondary Class 1 contributions incurred by a person (“P”) are “excluded liabilities” if they are incurred in respect of an employed earner who is employed (wholly or partly) for purposes connected with P's personal, family or household affairs.</p>
      </content>
   </subsection>
   ...
</section>
```

Note that there is a `subheading` element in the AKN schema which is not used in this case.

## Definitions - `//hcontainer[@name="definition"]`

Given the tradition in UK legislation of referring to certain provisions as "definitions", Lawmaker models such provisions using the element `<hcontainer name="definition">`.

Any defined term within the definition is represented by a `def` element. Additonal attributes `@ukl:startQuote` and `@ukl:endQuote` are used on the `def` element, mirroring those used in `quotedText`, to make the authoring process simpler but can be transformed into literal characters for publication.

For example:

```
<hcontainer name="definition" class="definition">
   <content>
      <p><def ukl:endQuote="”" ukl:startQuote="“">damage</def>, in relation to livestock, includes suffering, injury or disease,</p>
   </content>
</hcontainer>
```

Such definitions should usually be a child of a section-level element or a subsection-level element and the definition element will usually appear in groups of two or more.

The `def` element can also be used in other provisions (e.g. `subsection') to indicate a defined term, reflecting the fact that definitions can occur within other named provisions, not just the specific definition element.

* [Oasis AKN documentation for
`hcontainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_hcontainer.html)
* [Oasis AKN documentation for
`def`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_def.html)

## //level\[@class="para1"\]

This is the standard paragraph-level element typical of the first level
of English paragraphing. As explained above, we use the //level element
(to allow consistent usage in all contexts as the name is not standard
or agreed within the UK across different document types).

We would expect these always to have //num (note that the content of
//num will include the opening and closing brackets) and sometimes have
a //heading (typically before the //num) and to contain after that
either:

  - //content (if there are no paragraphs or definitions in the content)
  - //intro followed by //subparagraph\[@class="para2"\] and then an
    optional //wrapUp

We do not expect //blockList to occur here (except possibly for bullet
lists) but prefer to make use of named hierarchical elements. We would
only expect //hcontainer\[@name="definition"\] to occur within a
paragraph if preceded by //tblock\[@class="formula"\].

See [Oasis AKN documentation for
//level](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_level.html)

## //level\[@class="para2"\]

This is the standard sub-paragraph-level element within the body of an
Act. As explained above we use nested //level elements for this level We
would expect these always to have //num (note that the content of //num
will include the opening and closing brackets) and rarely have a
//heading (typically before the //num) and to contain after that either:

  - //content (if there are no paragraphs or definitions in the content)
  - //intro followed either by:
  - //level\[@class="para3"\]
  - and then followed by optional //wrapUp

We do not expect //blockList to occur here (except possibly for bullet
lists) but prefer to make use of hierarchical elements to allows for
nested hierarchical elements.

See [Oasis AKN documentation for
//level](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_level.html)

## //level\[@class="para3"\] and //level\[@class="para4"\]

There are some variations in the naming of elements at this level,
nominally a sub-sub-paragraph-level element within an Act, but more
variation in other contexts. Hence we continue the use of //level at
this level and below.

**Note:** The current example files contain //level\[@class="para3"\] elements (found in the Land Reform Bill), demonstrating the third level of paragraph nesting. However, //level\[@class="para4"\] is not present in the current examples, though the framework supports deeper nesting if required.

We would expect these always to have //num (note that the content of
//num will include the opening and closing brackets) and rarely have a
//heading (typically before the //num) and to contain after that either:

  - //content (if there are no paragraphs or definitions in the content)
  - //intro followed by //level\[@class="para4"\] and then followed by
    optional //wrapUp.

We do not expect //blockList to occur here (except possibly for bullet
lists) but prefer to make use of named hierarchical elements.

See [Oasis AKN documentation for
//level](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_level.html)

## //proviso

This is the standard proviso element within the body. Provisos typically
start with "Provided that .." or similar and have their own context as
they may in turn have paragraphs which start numbering again within the
proviso.

We would expect these not to have either a //num or a //heading
(typically before the //num) and to contain after that either:

  - //content (if there are no paragraphs or definitions in the content)
  - //intro followed by 2 or more //paragraph\[@class="para1"\] and then
    followed by optional //wrapUp

We do not expect //blockList to occur here (except possibly for bullet
lists) but prefer to make use of named hierarchical elements.

See [Oasis AKN documentation for
//proviso](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_proviso.html)

**Note:** Proviso elements are rare and typically only occur in older legislation. They are not present in the current example files.

## Finance Resolutions

Unique to Finance Resolutions, instead of a //section equivalent, the
bulk of the content of these documents is contained in resolutions. Each
of these is represented in the XML by an
//hcontainer\[@name="resolution"\]. These typically contain a number
(//num) and heading (//heading) followed by an //intro with the main
content of the resolution, optionally follwed by subsections
(//subsection) or paragraphs (//level), then followed by a //wrapUp
which contains the boilerplate text "And it is declared that it is
expedient in the public interest that this Resolution should have
statutory effect under the provisions of the Provisional Collection of
Taxes Act 1968."

See [Oasis AKN documentation for
//hcontainer](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/os-part2-specs_xsd_Element_hcontainer.html)

**Note:** Finance Resolutions are a specialized document type. They are not present in the current example files, which contain only Bills.
