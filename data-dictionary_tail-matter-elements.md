# Bill back page elements

While there is considerable overlap with the content of //coverPage and
//preface on the back cover, there are some differences so we style
these separately and use boilerplate template text and references where
possible to avoid double entry of content.

## //conclusions

We make use of the //conclusions element to contain all of the back
cover information for Scottish and UK Bills, and where required for
Amendment Lists.

As with the //coverPage, page furniture such as the footer with the
Session and Bill number are not treated as content of the back cover but
metadata of the document. This allows them to be referenced from one
source in both the cover page and the back cover.

For Scottish Bills, the back cover includes:

  - a title block (//block\[@name="title"\])
  - a stage version block (//block\[@name="stageVersion"\] (note that no
    element for the double horizontal rule is included - it is assumed
    this will be generated from the styling of the stage version block
  - the long title (//longTitle) - this should be identical to the
    content in the //preface so we make use of a reference
  - a table showing information about the introduction and type of the
    Bill which includes:
  - copyright information (//tblock\[@class="copyrightStatement"\])
  - publishing information (//tblock\[@class="publishingStatement"\])

We anticipate that additional components will be added and removed from
this section to reflect the back cover of other document types (Scottish
Acts, UK Bills and Acts, SIs and SSIs).

### //block\[@name="title"\]

The title block appears at the top of the back cover as it does for the
cover page for Scottish Bills and is typically centred, bold in a 24pt
or 32pt font. It contains the //docTitle inline tag and should normally
contain a reference to the BillTitle metadata variable so that double
entry is not required at least during authoring.

For example:

    <block name="title" eId="bc__st"><docTitle eId="bc__st__dtitle"><ref class="placeholder" href="#varBillTitle"></ref></docTitle></block>

### //block\[@name="stageVersion"\]

The stage version block appears as on the cover page immediately below
the title block for Scottish Bills and is typically centred, and all
caps in a 16 to 18pt font. TIt contains the //docStage inline tag
between square brackets and should normally contain a reference to the
StageVersion metadata variable so that double entry is not required at
least during authoring.

For example:

    <block name="stageVersion">[<docStage eId="bc%%__%%docStage"><ref class="placeholder" href="#varStageVersion"></ref></docStage>]</block>

### //longTitle

We use the standard AKN element for the long title despite the fact that
English and Scottish long titles are typically a single block of text
and have no further structure. Since the content from the //preface is
repeated on the back cover, we use a reference rather than introducing a
copy of the content that might potentially get out of synch.

    <longTitle><p><ref class="placeholder" href="#preface__longtitle"/></p></longTitle>

### Bill information

In Scottish Bills what appears next on the back cover is a summary of
metadata about the Bill including:

  - The introducing member (//block\[@name="introducingMember"\])
  - The supporting members if any (//block\[@name="supportingMembers"\])
  - The introduction date (//block\[@name="introductionDate")
  - The type of the Bill (//block\[@name="subtype"\])

In Scottish Bills this is typically managed with references to the
document metadata so the following bolierplate text can be used
virtually unchanged (note the use of the //inline\[@name="prompt"\]
which allows us to format this as a two coumn table with a prompt in the
first column and the value in the second):

``` 
  <block name="introducingMember"><inline name="prompt">Introduced by:</inline> <docIntroducer><ref class="placeholder" href="#varIntroducingMember"/></docIntroducer></block>
  <block name="supportingMembers"><inline name="prompt">Supported by:</inline> <docProponent><ref class="placeholder" href="#varSupportingMembers"/></docProponent></block>
   <block name="introductionDate"><inline name="prompt">On:</inline> <docDate date="9999-01-01"><ref class="placeholder" href="#varIntroDate"/></docDate></block>
   <block name="subtype"><inline name="prompt">Bill type:</inline> <docType><ref class="placeholder" href="#varDocSubType"/></docType></block>
```

### Copyright statement (//tblock\[@class="copyrightStatement"\])

A block of boilerplate text describing the copyright claims of the
document appears next.

In Scottish Bills this will normally be:

``` 
   <tblock class="copyrightStatement">
    <p>&#169; Parliamentary copyright. Scottish Parliamentary Corporate Body</p>
    <p>Information on the Scottish Parliament's copyright policy can be found on the website - </p>
    <p><a href="https://www.parliament.scot/">www.parliament.scot</a></p>
   </tblock>
```

### Publishing statement (//tblock\[@class="publishingStatement"\])

A block of boilerplate text describing the published of the document
appears next.

In Scottish Bills this will normally be:

``` 
   <tblock class="publishingStatement">
    <p>Produced and published in Scotland by the Scottish Parliamentary Corporate Body.</p>
    <p>All documents are available on the Scottish Parliament website at:</p>
    <p><a href="https://www.parliament.scot/documents">www.parliament.scot/documents</a></p>
   </tblock>
```

# Act back page

Bar code, copyright and publisher information is added by the Queen's
Printer as part of the publishing process for Acts so the //conclusions
element will be removed when converting a Bill to an Act.

# SI and SSI tail matter (more than just back page)

The back matter for Statutory Instruments also makes use of the
//conclusions element but also contains the Explanatory Notes (these are
in a separate document for Bills).

## //conclusions

We make use of the //conclusions element to contain all of the
concluding information after the body for Scottish and UK Statutory
Instruments as for Bills noting that the Explanatory Notes may extend
well beyond a single page.

As with the //coverPage, page furniture such as the footer are not
treated as content of the back matter but metadata of the document. This
allows them to be referenced from one source in both the cover page and
the back matter.

Within //conclusions, as with //preface and //preamble, //hcontainer is
not permitted. See generally [Lists v
paragraphing](https://ldapp.teratext.leidos.com.au/doku.php?id=naming-conventions#lists_v_paragraphing)

### //blockContainer\[@class="explanatoryNote"\]

While for Bills, Explanatory Notes are prepared as a separate document,
for Subordinate Instruments, the Explanatory Note is essentially an
annexure to the document itself. We therefore place that content within
//conclusions. Because this is in //conclusions, //hcontainer's are not
available and we are limited to using //block elements and their
substitutes.

The entire Explanatory Note is wrapped in a single //blockContainer with
@class="explanatoryNote" (//blockContainer@name is not permitted).

Within the Explanatory Note, we use //p for blocks of text, //blockList
for numbered lists (including paragraphing that we would normally use
//paragraph for in the body), and //tblock to group content under
headings.

### //blockContainer\[@class="commencementHistory"\]

Commencement orders and regulations and similar instruments may also
contain, after the Explanatory Note a similarly formatted heading "NOTES
AS TO FORMER COMMENCEMENT REGULATIONS" with a table outlining the
commencement date and instrument for all the provisions in the target
Act.

While we could just reuse the @class="explanatoryNote", since this
always contains a table, we create a new name so that we can better
validate the documents.

## Signature blocks - //hcontainer\[@name="signatures"\]

The signature blocks in SIs and SSIs typically appear after the main
body of provisions and before any schedules. Since a document may
contain multiple signature blocks and each signature block may contain
more than one signature, we model a set of signatures as
//hcontainer\[@name="signatures"\] in the //body containing one or more
//hcontainer\[@name="signatureBlock"\].

Where required, a seal can be represented as a
//block\[@name="seal"\]/image. The system is likely to have a small
library of seal images available for reuse in multiple documents.

Relevant semantic content will use standard inline elements where they
exist and //inline to capture additional metadata where an AKN inline
element does not (e.g. use //person, //role, //location, //organization
(for ministry or department), //date or //inline where there is a
concept not supported.

``` 
 <hcontainer name="signatures" GUID="_db3f628e-6dde-4c98-a9f9-68865ab2be1b" eId="sigs">
  <hcontainer name="signatureBlock" GUID="_f700dbf9-6551-4581-8985-ce7de3689f43" eId="sigs__sigBlk">
   <content>
    <p>Signed by authority of the Secretary of State</p>
    <block name="signature"><signature refersTo="#ref-d4e2596" GUID="_1adb2ea7-c5d6-4cdc-9218-b2aeb2ff48be" eId="sigs__sig__person">Hunt</signature></block>
    <blockl name="role"><role refersTo="#ref-d4e2598" GUID="_8ace874b-62e1-4b73-8db2-e0e65c014e39" eId="sigs__sig__role">Minister of State</role></block>
    <block name="organization"><organization refersTo="#ref-d4e2600" GUID="_213cbf02-338d-4264-b88d-0e60f465cefe" eId="sigs__sig__org">Department of Health</organization></block>
    <block name="date"><date date="2007-03-08">8th March 2007</date></block>
   </content>
  </hcontainer>
  <hcontainer name="signatureBlock" GUID="_c38b65d3-944f-423c-b87c-30f2bcb93b65" eId="sigs__sigBlk__oc_2">
   <content>
    <p>Sealed with the Official Seal of the Department of Health, Social Services and Public Safety</p>
    <block name="seal"><img class="seal" src="http://www.legislation.gov.uk/uksi/2007/803/images/uksi_20070803_en_001" GUID="_4b747560-2c92-42b2-a371-121e6a25b765" eId="sigs__sigBlk__oc_2__img"/></block>
    <block name="signature"><signature refersTo="#ref-d4e2611" GUID="_ee7e8cfd-d2f1-440d-9f91-4f88323c726f" eId="sigs__sigBlk__oc_2__sig">Andrew McCormick</signature></block>
    <block name="role"><role refersTo="#ref-d4e2613" GUID="_cc6924dd-b72b-4584-b339-de089251f555" eId="sigs__sigBlk__oc_2__role">Permanent Secretary</role></block>
    <block name="organization"><organization refersTo="#ref-d4e2615" GUID="_863baf38-55f3-4a86-99a6-b30559ff0cda" eId="sigs__sigBlk__oc_2__org">Department of Health, Social Services and Public Safety</organization></p>
    <block name="date"><date date="2007-03-08">8th March 2007</date></block>
   </content>
  </hcontainer>
 
```

Note that inserting any but //date requires a @refersTo to reference a
corresponding element in //meta/references. The following table shows
how these should be populated:

|                   |             |                                                                                                         |                                                                             |
| ----------------- | ----------- | ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **Concept**       | **Value**   | **Inline tag in signature**                                                                             | \*\*Metadata tag in //references \*\*                                       |
| Name or signature | *name*      | \<signature refersTo="\#*id*"\>*name*\</signature\> *(Note: the @refersTo is optional in this element)* | \<TLCPerson eId="*id*" href="\#varOntologies" showAs="*name*"/\>            |
| Role              | *role*      | \<role refersTo="\#*id*"\>*role*\</role\>                                                               | \<TLCRole eId="*id*" href="\#varOntologies" showAs="*role*"/\>              |
| Organization      | *org\_name* | \<organization refersTo="\#*id*"\>*org\_name*\</organization\>                                          | \<TLCOrganization eId="*id*" href="\#varOntologies" showAs="*org. name*"/\> |
| Location          | *loc\_name* | \<location refersTo="\#*id*"\>*loc\_name*\</location\>                                                  | \<TLCLocation eId="*id*" href="\#varOntologies" showAs="*name*"/\>          |

Note that there may be zero, one or more signatures on a Statutory
Instrument. Draft Statutory Instruments may contain placeholders for the
signature(s).

Some more unusual examples include:

  - [UKSI 1994/102](http://www.legislation.gov.uk/uksi/1994/102/made)
    contains six signatures;
  - [UKSI 2014/1933](http://www.legislation.gov.uk/uksi/2014/1933/made)
    and
    [UKSI 2014/3257](http://www.legislation.gov.uk/uksi/2014/3257/made)
    contain four, three of which are consents/concurrences;
  - [UKSI 2007/803](http://www.legislation.gov.uk/uksi/2007/803/made)
    contains four, two of which are Seals.

Separate signature blocks also appear within schedules occasionally,
where some body is approving a scheme or rules contained the schedule
which are then wrapped and signed off in an SI. The //hcontainer
approach allows these to appear within a
//hcontainer\[@name="schedule"\]. See

  - [UKSI 2019/1189](http://www.legislation.gov.uk/uksi/2019/1189/made)
    (It is also an order in council, so although there is a clerk’s name
    in the signature block at the end of the main body, the ‘true’
    signed date/signee/location are in a crossheading underneath the SI
    title.)
  - [UKSI 1994/102](http://www.legislation.gov.uk/uksi/1994/102/made)
    containing eight seal signatures within a schedule.

Although each signature block usually contains one signee name or
signature, signing bodies can potentially have a large number of
signees. This SI contains a single set of signatures with two signature
blocks, one of which contains 9 signers:

  - [UKSI 2017/1033](http://www.legislation.gov.uk/uksi/2017/1033/made)

<!-- end list -->

``` 
 <hcontainer name="signatures" GUID="_cfb510ff-3bfc-440b-8ee6-a55a1da2a76a" eId="sigs">
  <hcontainer name="signatureBlock" GUID="_301f5737-7b6d-4f37-8f71-3961661d71f1" eId="sigs__sigBlk">
   <content>
    <block name="signature" GUID="_a46c4bc3-5f11-4ed5-a6bb-bbf2df855e1c" eId="sigs__sigBlk__sig"><signature refersTo="#ref-d6e606">James Munby, P</signature></block>
    <block name="signature" GUID="_34e2e015-622a-4a9c-92f5-b09d671a16b5" eId="sigs__sigBlk__sig__oc_2"><signature refersTo="#ref-d6e608">Marie Brock</signature></block>
    <block name="signature" GUID="_9cd6eccd-86ff-4ce2-8059-959ea3a565f9" eId="sigs__sigBlk__sig__oc_3"><signature refersTo="#ref-d6e610">Richard Burton</signature></block>
    <block name="signature" GUID="_c45beec2-da8e-4948-b729-f8f0f3ff0427" eId="sigs__sigBlk__sig__oc_4"><signature refersTo="#ref-d6e612">Melanie Carew</signature></block>
    <block name="signature" GUID="_8a6542f3-be07-44f7-a274-7ba1987809a8" eId="sigs__sigBlk__sig__oc_5"><signature refersTo="#ref-d6e614">Paul Carr</signature></block>
    <block name="signature" GUID="_21dad172-7251-40e0-a431-96364ea986d3" eId="sigs__sigBlk__sig__oc_6"><signature refersTo="#ref-d6e616">Michael Horton</signature></block>
    <block name="signature" GUID="_dd75cd96-40a7-490f-93c2-936f53d6de1f" eId="sigs__sigBlk__sig__oc_7"><signature refersTo="#ref-d6e618">Dylan Jones</signature></block>
    <block name="signature" GUID="_774e32f7-6a34-444c-86da-27037827ecb4" eId="sigs__sigBlk__sig__oc_8"><signature refersTo="#ref-d6e620">Hannah Perry</signature></block>
    <block name="signature" GUID="_cbc59c24-68e9-44e7-b32c-4dee96e5117f" eId="sigs__sigBlk__sig__oc_9"><signature refersTo="#ref-d6e622">Will Tyler</signature></block>
   </content>
  </hcontainer>
  <hcontainer name="signatureBlock" GUID="_7060caeb-1ec7-4bb5-8d61-a33ceb7a808a" eId="sigs__sigBlk__oc_2">
   <content>
    <p>I allow these Rules</p>
    <block name="signature" GUID="_b25586e6-02d4-4567-9676-3de033ca77ff" eId="sigs__sigBlk__oc_2__sig"><signature refersTo="#ref-d6e629">Dominic Raab</signature></block>
    <block name="role" GUID="_167b92f5-1b51-4911-a97f-41a68ada46ab" eId="sigs__sigBlk__oc_2__role"><role refersTo="#ref-d6e631">Minister of State</role></block>
    <block name="date"><date date="2017-10-23">23rd October 2017</date></block>
    <block name="organization" GUID="_a3250dcd-b4c4-4a4d-b9a3-8e3e38d0ef1e" eId="sigs__sigBlk__oc_2__org"><organization refersTo="#ref-d6e633">Ministry of Justice</organization></block>
   </content>
  </hcontainer>
 </hcontainer>
```

A bizarre edge case and others in its series essentially contains two
separate SIs that the drafters have welded together into one. Part 1 is
“The Traffic Signs Regulations 2016”, culminating in a signature. Part
2 is “The Traffic Signs General Directions 2016”, culminating in another
signature. This all occurs before the schedules begin:

  - [UKSI 2016/362](http://www.legislation.gov.uk/uksi/2016/362/contents/made)

This last example would require two sets of signature blocks
(//hcontainer\[@name="signatures"\]). The other examples above have a
single set of signature blocks containing multiple signatures or
signature blocks (//hcontainer\[@name="signatureBlock"\]).
