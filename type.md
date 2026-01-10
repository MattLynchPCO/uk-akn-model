# Element Hierarchy and Use of @class Attribute

In UK legislation, some elements that have the same semantic role and formatting have different names based on what document or component of a document they appear in. For instance, the main building block of an Act is the "section" but this is called a "clause" in a Bill (although references within that Bill are to "section"), and the equivalent structure in an SI can be called "rule", "regulation", or "article" (there may be others) despite being formatted very similarly.

The [Akoma Ntoso (AKN) standard](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html) requires using the element name (or where the named element doesn't exist in the schema, [`hcontainer[@name="..."]`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_hcontainer)) to reflect the normal name of a referenceable element in a document. To capture the similarity of formatting and semantic role, it is appropriate to use the [`@class` attribute](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#_Toc523925090), which simplifies CSS for formatting documents while editing. 

The following tables describe the different `@class` values and their interpretation within UK AKN documents.

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
| group7    | 7th level grouping (e.g. crossheading)                              |
| group8    | 8th level grouping (e.g. nested crossheading)                       |

The formatting within schedules may be different, so there are equivalents specifically for schedules below.

See [Grouping or Higher Division Elements](data-dictionary/grouping-elements.md)

## Section-Level and Below in the Body

See [Section-Level and Below Elements](data-dictionary/section-elements.md), also called "Basic Unit" and "Subdivision" elements in the [AKN standard](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html) (despite many jurisdictions having division and subdivision as "Higher Division" elements).

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


## Schedule and Below Elements

See [Schedule and Below Elements](data-dictionary/schedule-elements.md)

The table below shows `@class` values for schedules and their nested elements:

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
| schGroup7 | 7th level grouping (e.g. crossheading)                              |
| schGroup8 | 8th level grouping (e.g. nested crossheading)                       |

**Note:** Paragraphs or sub-paragraphs that are children of a `schProv1` or `schProv2` will use `@class="para1"`.
