# Section-level and below standard elements

These are elements at the section level in the body of the Act which
includes Bill clauses, rules, regulations, by-laws and paragraphs in the
body of subordinate legislation (SIs, SSIs, Orders, etc).

|                                                                                                                                    |                                                         |                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------ |
| **Numbered element**                                                                                                               | **'Normal/regular' number format (in square brackets)** | **Starting 'normal/regular' value in the num element** |
| Section (including //rule, //hcontainer\[@name="regulation"\] and //article in SIs/SSIs - pretty much anything with @class="prov1" | \[arabic\]                                              | 1                                                      |
| Subsection (including //paragraph\[@class="prov2"\])                                                                               | (\[arabic\])                                            | (1)                                                    |
| Schedule paragraph (@class="schedProv1") - these are referred to as "paragraphs"                                                   | \[arabic\]                                              | 1                                                      |
| Schedule subparagraph (@class="schedProv2")                                                                                        | (\[arabic\])                                            | (1)                                                    |
| Step                                                                                                                               | Step \[arabic\]                                         | Step 1                                                 |
| Table                                                                                                                              | Table \[arabic\]                                        | Table 1                                                |
| Schedule                                                                                                                           | Schedule \[arabic\]\*                                   | Schedule                                               |

\* NB: if only one schedule, no number is assigned (the //num content is
"Schedule"); when there are 2 schedules, "Schedule *N*" appears in all
the schedule //num's including the first one e.g. “Schedule 1” and the
second is “Schedule 2”.

## Paragraphing in Acts, Bills, SIs and SSIs

Within the body of an Act or Bill, the following applies (within SI, SSI
or schedule there are some variations):

|                                                         |                                                              |                                           |
| ------------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------- |
| **Numbered element**                                    | **'Normal/regular' number format (in square brackets)**      | \*\*Starting 'normal/regular' number \*\* |
| Paragraph (including within schedules - @class="para1") | (\[lowercase alphabetical\])                                 | (a)                                       |
| Subparagraph (including within schedules)               | (\[lowercase roman\])                                        | (i)                                       |
| Subsubparagraph (including within schedules)            | (\[double lowercase alphabetical\]) - UK Bills and Acts only | (aa)                                      |
| Subsubparagraph (including within schedules)            | (\[uppercase alphabetical\]) - all other document types      | (A)                                       |

Note that the naming below "subparagraph" is not always consistent in
the body of an Act or Bill. Within SI, SSI and schedule, even for para1
and para2 examples the name alternates between "paragraph" and
"sub-paragraph" depending on the context and the usage is not always
consistent. In SI, SSI and schedules, the prov2, schProv1 and sometimes
even prov1 elements can be referred to as "paragraph" there is quite a
lot of ambiguity in the correct name for anything in the para*N*
classes.

Because the names are not agreed but the elements are hierarchical and
can contain nested hierarchical elements including definitions, tables,
as well as lower para*N* classes, we use the //level element with @class
used to identify the default numbering and relative indentation level.

In contexts that don't allow //hcontainer, we use
//blockContainer\[@class="para*N*"\] as an alternative (e.g. //preface,
//preamble, //conclusions etc.).

## @class="prov1" (section-level elements)

This is the standard section-level element within the body. In Bills and
Acts, this will be a //section element. In SIs this will be one of
//article (Orders), //rule (Rules), //hcontainer\[@name="regulation"\]
(Regulations). This list is likely to expand as we investigate SIs.

We would expect these always to have //num and //heading (in that order)
and to contain after that either:

``` 
 * @class="prov2" (%%//%%subsection if this element is %%//%%section)
 * %%//%%content (if there are no paragraphs or definitions in the content)
 * %%//%%intro followed either by:
   * %%//%%paragraph[@class="para1"]
   * %%//%%hcontainer[@name="definition"]
   * and then followed by optional %%//%%wrapUp
 * %%//%%proviso - these are rare and typically only occur in older legislation.
```

We do not expect //blockList to occur here (except possibly for bullet
lists) but prefer to make use of named hierarchical elements.

For Bills and Acts see [Oasis AKN documentation for
//section](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_section.html)

For SIs/SSIs see [Oasis AKN documentation for *rule\]\],
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_article.html|Oasis
AKN documentation for *article\]\] and, where AKN doesn't provide a
specific element (such as for "regulation"),
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_hcontainer.html|Oasis
AKN documentation for
//hcontainer](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_rule.html)

## @class="prov2" (subsection-level elements)

This is the standard subsection-level element within the body. In Bills
and Acts, this will be a //subsection element. In SIs this may depend on
the name of the containing @class="prov1" but is normally a //paragraph.
Note in particular that, although some English-speaking jurisdictions
would call this element within a //rule a //subrule, that is not the
current practice for LDAPP users. We therefore are unlikely to use
//subrule (except possibly in incorporated EU legislation or quoted
treaties).

We would expect these always to have //num (note that the content of
//num will include the opening and closing brackets) and rarely to have
a //heading (typically before the //num) and to contain after that
either:

  - //content (if there are no paragraphs or definitions in the content)
  - //intro followed either by:
      - //paragraph|subparagraph\[@class="para1"\]
      - //hcontainer\[@name="definition"\]
      - and then followed by optional //wrapUp
  - //proviso - these are rare and typically only occur in older
    legislation.

We do not expect //blockList to occur here (except possibly for bullet
lists) but prefer to make use of named hierarchical elements.

For Bills and Acts see [Oasis AKN documentation for
//subsection](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_subsection.html)

For SIs/SSIs see [Oasis AKN documentation for
//paragraph](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_rule.html).

## //hcontainer\[@name="definition"\]

AKN does not provide a generic element for definitions despite all
English-speaking jurisdictions and many European influenced
jurisdictions including referenceable objects that are described as
"definitions". We therefore propose to use an
//hcontainer\[@name="definition"\] to wrap what would normally be
referred to as a definition (typically within a section or subsection or
similar but they can occur elsewhere, e.g. Queensland tends to put
definitions in a "glossary" or "dictionary" schedule in more recent
Acts).

Although many jurisdictions do not indent definitions differently to
blocks within the same context, a number do (including Scotland and the
UK). A separate container element allows this flexibility. Because they
are referenceable (and deletable as a container which might include
paragraphs, formulas, and nested definitions), a //block element isn't
sufficient.

A list of definitions typically appears within a //section or
//subsection (or equivalents in SIs/SSIs) immediately after //intro text
like "In this Act—" or similar. Another common construct is intro text
followed by a formula followed by the text "where—" and a list of
definitions defining the terms used in the formula (see
//hcontainer\[@name="equation"\]). This last construct is just as likely
to appear within a //paragraph also so definitions can appear at
different indentation levels.

The first //p within a //hcontainer\[@name="definition"\] will start
with an inline //def element that should contain the term that is
defined (including the quotations within the //def tags). Some
definitions may have more than one //def element but most will contain
only one. It seems redundant to use //embeddedText for the quotation
marks - we simply use //def an quotation marks in the text. \_Query
whether //def should use the same quote attributes as //embeddedText\_\_

In reference wording to definitions, the phrase 'the definition of
"*defined term*"' should be surrounded by a single pair of //ref tags
with the quotation marks part of the text.

See [Oasis AKN documentation for
//hcontainer](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html)

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
//level](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_level.html)

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
//level](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_level.html)

## //level\[@class="para3"\] and //level\[@class="para4"\]

There are some variations in the naming of elements at this level,
nominally a sub-sub-paragraph-level element within an Act, but more
variation in other contexts. Hence we continue the use of //level at
this level and below.

We would expect these always to have //num (note that the content of
//num will include the opening and closing brackets) and rarely have a
//heading (typically before the //num) and to contain after that either:

  - //content (if there are no paragraphs or definitions in the content)
  - //intro followed by //level\[@class="para4"\] and then followed by
    optional //wrapUp.

We do not expect //blockList to occur here (except possibly for bullet
lists) but prefer to make use of named hierarchical elements.

See [Oasis AKN documentation for
//level](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_level.html)

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
//proviso](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_proviso.html)

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
//hcontainer](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html)
