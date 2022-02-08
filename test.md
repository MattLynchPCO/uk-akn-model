# Document level elements

These are the root level elements of LDAPP legislative documents.

## //act

This element is used not just for Acts but also subordinate legislation
in it's enacted or made form.

A full description of the AKN element is available at [Oasis //act
description](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_act.html#act)

### Required attributes

#### @name

This attribute has it's standard usage in AKN. Values in LDAPP include:

|           |                                                                                               |
| --------- | --------------------------------------------------------------------------------------------- |
| **Value** | **Interpretation**                                                                            |
| ukpga     | United Kingdom Public General Act                                                             |
| ukla      | United Kingdom Local Act                                                                      |
| asp       | Act of the Scottish Parliament                                                                |
| uksi      | UK Statutory Instrument                                                                       |
| ssi       | Scottish Statutory Instrument                                                                 |
| ukmd      | UK Ministerial Direction (note there are no examples on legislation.gov.uk)                   |
| ukmo      | UK Ministerial Order (note these may not be within scope of LDAPP)                            |
| ukcm      | UK Church Measure                                                                             |
| ukci      | UK Church Instrument (note that some subordinate church legislation \[Resolutions\] are uksi) |

European legislation types include:

|           |                    |
| --------- | ------------------ |
| **Value** | **Interpretation** |
| eudr      | EU Directive       |
| eudn      | EU decision        |
| eur       | EU regulation      |

## //bill

This element is used for draft Acts, draft SIs/SSIs (both during the
draft stage while in Parliamentary Counsel and when tabled to Parliament
as a draft or bill), and Finance Resolutions.

A full description of the AKN element is available at [Oasis //bill
description](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_bill.html#act)

#### Required attributes

#### @name

This attribute has it's standard usage in AKN. Values in LDAPP include:

|           |                                        |
| --------- | -------------------------------------- |
| **Value** | **Interpretation**                     |
| ukpubb    | United Kingdom Public Bill             |
| ukprib    | United Kingdom Private Bill            |
| ukhybb    | United Kingdom Hybrid Bill             |
| ukfinres  | United Kingdom Finance Resolution Book |
| sppubb    | Scottish Parliament Public Bill        |
| spprib    | Scottish Parliament Private Bill       |
| sphybb    | Scottish Parliament Hybrid Bill        |
| ukdsi     | Draft UK Statutory Instrument          |
| sdsi      | Draft Scottish Statutory Instrument    |
| ukdmd     | Draft UK Ministerial Direction         |
| ukdmo     | Draft UK Ministerial Order             |
| ukdcm     | Draft UK Church Measure                |
| ukdci     | Draft UK Church Instrument             |
| ukfinres  | Draft UK Finance Resolutions           |

#### @ukl:subtype

We are using //FRBRSubtype to record the subtype of the document. This
is most important for SI/SSIs but it is also used for some Bills and
Acts.

| Value               | Interpretation             | Name of section-like element (@class="prov1")        |
| ------------------- | -------------------------- | ---------------------------------------------------- |
| Government Bill     | Government Bill            | //section                                            |
| Member’s Bill       | Member’s Bill              | //section                                            |
| Committee Bill      | Committee Bill             | //section                                            |
| Consolidation Bill  | Consolidation Bill         | //section                                            |
| Finance Resolutions | Finance Resolutions Book   | //hcontainer\[@name="resolution"\]                   |
| Regulations         | Regulations                | //hcontainer\[@name="regulation"\]                   |
| Order               | Order                      | //article                                            |
| Order in Council    | Order in Council           | //article                                            |
| Rules               | Rules                      | //rule                                               |
| Scheme              | Scheme                     | //hcontainer\[@name="scheme"\] (@class="resolution") |
| Approval Instrument | Approval Instrument        | n/a                                                  |
| Direction           | Direction                  | //hcontainer\[@name="direction"\]                    |
| Warrant             | Warrant                    | //hcontainer\[@name="warrant"\]                      |
| Resolution          | Resolution (of Parliament) | //hcontainer\[@name="resolution"\]                   |
| Other               | Other (SI/SSI)             | //article                                            |

We discussed adding root level attributes but have not found an
application that requires them.

## //amendment

A single amendment for Parliament.

The main content of an //amendment will be in the //amendmentContent
which will normally contain a single //tblock where the //tblock/num is
the number of the amendment, and //tblock/block will contain a //mod
which will contain a description of the amendment including potentially
one or more //quotedStructure elements.

### Required attributes

#### @name

This attribute has it's standard usage in AKN. Values in LDAPP include:

|                                     |                                             |
| ----------------------------------- | ------------------------------------------- |
| **Value**                           | **Interpretation**                          |
| spamnd (formerly scottishAmendment) | Amendment for the Scottish Parliament       |
| spdamnd                             | Draft amendment for the Scottish Parliament |
| hlamnd                              | Amendment for the House of Lords            |
| hldamnd                             | Draft amendment for the House of Lords      |
| hcamnd                              | Amendment for the House of Commons          |
| hcdamnd                             | Draft amendment for the House of Commons    |

A full description of the AKN element is available at [Oasis //amendment
description](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_amendment.html#act)

## //amendmentList

Any list of amendments for Parliamentary use. These include the daily
list, Marshalled List and the Groupings List for Scottish Parliaments.
Similar artefacts are required for UK Parliament.

Amendments are included using the //component wrapper. Where headings
are required, this limits us to using //interstitial between each
component containing essentially a flat model treating headings as
siblings of the amendments they group.

Most of the content that is specific to the grouping type appears within
the metadata (//meta) and //preface. \_\_TODO: Need to create a page
describing the front matter/preface for each type of amendments list.
\_\_

### Required attributes

#### @name

This attribute has it's standard usage in AKN. Values in LDAPP include:

|              |                                                 |
| ------------ | ----------------------------------------------- |
| **Value**    | **Interpretation**                              |
| spdamnds     | Scottish Parliament list of draft amendments    |
| spdaily      | Scottish Parliament daily list                  |
| spmarsh      | Scottish Parliament Marshalled List             |
| spgroup      | Scottish Parliament Groupings List              |
| hcdamnds     | House of Commons list of draft amendments       |
| hldamnds     | House of Lord list of draft amendments          |
| hcmarsh      | House of Commons rolling marshalled list        |
| hcdaily      | House of Commons daily                          |
| hcproceed    | House of Commons proceedings                    |
| hcproceed    | House of Commons rolling proceedings            |
| hldaily      | House of Lords daily sheet                      |
| hlrunning    | House of Lords rolling daily sheet/running list |
| hlmarsh      | House of Lords marshalled list                  |
| hlmanuscript | House of Lords manuscript amendment             |
| cloa         | Consolidated list of amendments                 |
