# Element Hierarchy and Use of @class Attribute

In UK legislation, some provisions that have the same semantic role and formatting have different names based on what document or component of a document they appear in. For instance, the main building block of an Act is the "section" but this is called a "clause" in a Bill (although references within that Bill are to "section"), and the equivalent structure in an SI can be called "rule", "regulation", or "article" despite being formatted very similarly.

Equally, there are cases where the same name is used for two different provision types in different contexts. For example, "section" in subordinate legislation refers to a grouping element containing other provisions while "section" in a Bill or Act means the basic unit of legislative content.

To capture the similarity or difference of formatting and semantic role, Lawmaker additionally uses the [`@class` attribute](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#_Toc523925090). This simplifies CSS for presenting documents while editing or publishing.

The following tables describe the different `@class` values and their interpretation within UK AKN documents.

## Grouping elements in the body

|           |                                                                     |
| --------- | ------------------------------------------------------------------- |
| **Value** | **Interpretation**                                                  |
| group0    | Extra grouping level                                                |
| group1    | 1st level grouping (Group of Parts)                                 |
| group2    | 2nd level grouping (Part)                                           |
| group3    | 3rd level grouping (Title - EU legislation only)                    |
| group4    | 4th level grouping (Chapter )                                       |
| group5    | 5th level grouping (Section - SI/SSI only)                          |
| group6    | 6th level grouping (Sub-section - SI/SSI only)                      |
| group7    | 7th level grouping (Cross-heading)                                   |
| group8    | 8th level grouping (e.g. nested Cross-heading)                       |

The formatting within schedules may be different, so there are equivalents specifically for schedules below.

See [Grouping or Higher Division Elements](data-dictionary/grouping-elements.md)

## Section-Level and Below in the Body

See [Section-Level and Below Elements](data-dictionary/section-elements.md), also called "Basic Unit" and "Subdivision" elements in the [AKN standard](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html) (despite many jurisdictions having division and subdivision as "Higher Division" elements).

|            |                                                     |
| ---------- | --------------------------------------------------- |
| **Value**  | **Interpretation**                                  |
| prov1      | Section level in the body of an Act or article, rule or regulation of subordinate legislation   |
| prov2      | subdivision of a section, article, rule, or regulation, i.e. a subsection or SI paragraph   |
| definition | Definition  |
| para1      | Paragraph within a section, subsection, article, rule, regulation or SI paragraph            |
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
| sch       | A Schedule (or equivalent annex, annexure, appendix)                |
| schProv1  | a schedule paragraph      |
| schProv2  | subdivision of schedule paragraph (schedule sub-paragraph)        |
| schGroup0 | Extra grouping level                                                |
| schGroup1 | 1st level grouping (e.g. Group of Parts)                            |
| schGroup2 | 2nd level grouping (e.g. Part)                                      |
| schGroup3 | 3rd level grouping (e.g. Title - EU legislation only)               |
| schGroup4 | 4th level grouping (e.g. Chapter)                      |
| schGroup5 | 5th level grouping (e.g. Section - SI/SSI only)                     |
| schGroup6 | 6th level grouping (e.g. Sub-section - SI/SSI only)                 |
| schGroup7 | 7th level grouping (e.g. Cross-heading)                              |
| schGroup8 | 8th level grouping (e.g. nested Cross-heading)                       |

**Note:** Paragraphs or sub-paragraphs that are children of a `schProv1` or `schProv2` will use `@class="para1"`.
