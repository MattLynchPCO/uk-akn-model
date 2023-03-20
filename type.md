# Element hierarchy, @class and @refersTo

In legislation in the UK, some elements that have the same semantic role
and formatting have different names based on what document or component
of a document they appear in. For instance, the main building block of
an Act is the "section" but this is called a "clause" in a Bill
(although references within that Bill are to "section") and the
equivalent structure in an SI can be called "rule", "regulation", or
"article" (there may be others) despite being formatted very similarly.

AKN requires us to use //hcontainer\[@name="*name*"\] or the equivalent
//*name* to reflect the normal name of a referenceable element in a
document. In order to capture the similarity of formatting and semantic
role, we originally proposed to use the AKN @type attribute to represent
this similarity however, @type is not available on most //hcontainer
elements. For formatting purposes it is expedient to use the @class
attribute which vastly simplifies CSS for formatting documents while
editing. However, AKN requires that this semantic role reference an
ontology. We will therefore consider adding (at a later stage) a similar value
in the @refersTo attribute to reference an ontology either within the
document or, more likely, in an external ontology.

The following tables describe the different values and their
interpretation within the LDAPP documents.

## Grouping elements in the body

|           |                                                                     |
| --------- | ------------------------------------------------------------------- |
| **Value** | **Interpretation**                                                  |
| group0    | Extra grouping level                                                |
| group1    | 1st level grouping (e.g. group of parts)                            |
| group2    | 2nd level grouping (e.g. part)                                      |
| group3    | 3rd level grouping (e.g. title - EU legislation only)               |
| group4    | 4th level grouping (e.g. chapter \[division\])                      |
| group5    | 5th level grouping (e.g. section - SI/SSI only)                     |
| group6    | 6th level grouping (e.g. sub-section - SI/SSI only)                 |
| group7    | 7th level grouping (e.g. crossheading \[subdivision in Australia\]) |
| group8    | 8th level grouping (e.g. nested crossheading)                       |

Although we could reuse this within a schedule, the formatting tends to
be different so we have equivalents specifically for schedules below.

See [Grouping or higher division
elements](data-dictionary/grouping-elements.md)

## Section-level and below in the body

See [section-level and below elements](data-dictionary/section-elements.md)
also called "Basic Unit" and "Subdivision" elements in AKN (despite many
jurisdictions having division and subdivision as "Higher Division"
elements).

|            |                                                     |
| ---------- | --------------------------------------------------- |
| **Value**  | **Interpretation**                                  |
| prov1      | Section level in the body of an Act or equivalent   |
| prov2      | Subsection level in the body of an Act or similar   |
| definition | Definition (usually within a section or subsection) |
| para1      | Paragraph within a section or subsection            |
| para2      | Sub-paragraph within //\*\[@class="para1"\]         |
| para3      | Sub-sub-paragraph within //\*\[@class="para2"\]     |
| para4      | Sub-sub-sub-paragraph within //\*\[@class="para3"\] |
| step       | Step, usually within a section or subsection        |


## Schedule and below elements

See [Schedule and below elements](data-dictionary/schedule-elements.md)

|           |                                                                     |
| --------- | ------------------------------------------------------------------- |
| **Value** | **Interpretation**                                                  |
| sch       | A schedule (or equivalent annex, annexure, appendix)                |
| schProv1  | Section-level equivalent in a schedule (schedule paragraph)         |
| schProv2  | Subsection equivalent in a schedule (schedule sub-paragraph)        |
| schGroup0 | Extra grouping level                                                |
| schGroup1 | 1st level grouping (e.g. group of parts)                            |
| schGroup2 | 2nd level grouping (e.g. part)                                      |
| schGroup3 | 3rd level grouping (e.g. title - EU legislation only)               |
| schGroup4 | 4th level grouping (e.g. chapter \[division\])                      |
| schGroup5 | 5th level grouping (e.g. section - SI/SSI only)                     |
| schGroup6 | 6th level grouping (e.g. sub-section - SI/SSI only)                 |
| schGroup7 | 7th level grouping (e.g. crossheading \[subdivision in Australia\]) |
| schGroup8 | 8th level grouping (e.g. nested crossheading)                       |

Note that paragraphs or sub-paragraphs that are children of a schProv1
or schProv2 will use @class="para1".
