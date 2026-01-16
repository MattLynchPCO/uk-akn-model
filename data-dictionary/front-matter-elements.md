# Front matter elements

This section includes elements that make up the cover page, table of
contents, preface, preamble, enacting words and any content that
precedes the start of the body (//body element).

It does not include the metadata that, in AKN, precedes the visible
content on the page which is dealt with in [Document metadata
elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_metadata-elements)

## //coverPage

We make use of the //coverPage element pretty much as intended by AKN
for Bills and Acts. We include the table of contents within the scope of
this element because in some prints of Scottish Bills, it starts (and
sometimes finishes) on the cover page although in later prints and UK
Bill prints, the table of contents starts on the second page (third
face). For SIs and SSIs, there is no cover page and we go straight to
the //preface.

Page furniture such as the footer with the Session and Bill number are
not treated as content of the cover page but metadata of the document.
This allows them to be referenced from one source in both the cover page
and the back cover.

For Scottish Bills, the cover page includes:

  - a title block (//block\[@name="title"\])
  - a stage version block (//block\[@name="stageVersion"\] (note that no
    element for the double horizontal rule is included - it is assumed
    this will be generated from the styling of the stage version block
  - if present the components of the table of contents (see below)

For Scottish Amendments and Amendment Lists, there is no cover page so
this element is not used.

For Scottish Acts, the cover page includes:

  - a title block (//block\[@name="title"\])
  - a number block (//block\[@name="number"\]) containing the Act year
    and number
  - *There is a page break here but the remaining content is still
    essentially cover material so remains in the //coverPage element*
  - another title block (//block\[@name="title"\])
  - another number block (//block\[@name="number"\]) containing the Act
    year and number
  - an explanatory notes statement
    (//block\[@name="explanatoryNotesStatement"\] (note that no element
    for the double horizontal rule is included - it is assumed this will
    be generated from the styling of the stage version block
  - if present the components of the table of contents (see below)

SIs and SSIs do not have a cover page.

Finance Resolutions make use of the cover page which includes:

  - a title block (//block\[@name="title"\]) typically containing the
    fixed content "Resolutions to be moved by the Chancellor of the
    Exchequer",
  - a date block (//block\[@name="date"\]),
  - a note about the measures included
    (//blockContainer\[@class="note"\]), and
  - a motion about provisional collection of taxes if required
    (//blockContainer\[@class="hcMotion"\]).

### //block\[@name="title"\]

The title block appears at the top of the cover page for Scottish Bills
and is typically centred, bold in a 24pt or 32pt font. This block is
repeated in the preface and the back cover. It contains the //docTitle
inline tag and should normally contain a reference to the BillTitle
metadata variable so that double entry is not required at least during
authoring.

    <block name="title" GUID="_17019f61-fae7-4bca-bcf1-ec689b7b77c7" eId="cp%%__%%st"><docTitle GUID="_e46bc853-dc43-4308-9ec3-c4ad26ea86df" eId="cp%%__%%st%%__%%dtitle"><ref class="placeholder" href="#varBillTitle"></ref></docTitle></block>

### //block\[@name="stageVersion"\]

The stage version block appears immediately below the title block for
Scottish Bills and is typically centred, and all caps in a 16 to 18pt
font. This block is also repeated in the preface and the back cover. It
contains the //docStage inline tag between square brackets and should
normally contain a reference to the StageVersion metadata variable so
that double entry is not required at least during authoring.

For example:

``` 
  <block name="stageVersion">[<docStage GUID="_4a596687-f298-425b-9169-6701d9e91d45" eId="cp%%__%%docStage"><ref class="placeholder" href="#varStageVersion"></ref></docStage>]</block>
```

### //block\[@name="explanatoryNoteStatement"\]

This is typically located immediately below the stage version block in
Scottish Acts. It contains a statement about the availability of an
Explanatory Note.

For example:

``` 
  <block name="explanatoryNotesStatement" GUID="_fdc12f5d-9af1-44e1-83ec-f17f6777d32d" eId="cp__explNotesStmnt">Explanatory Notes have been produced to assist in the understanding of this Act and are available separately.</block>
```

### Table of contents

The table of contents would normally be generated automatically so that
it is consistent with the structure of the //body element. The structure
of the table of contents whether a placeholder or complete should be:

  - a table of contents heading block (//block\[@name="ToCHeading"\])
  - a table of contents type block (//block\[@name="ToCType"\])
  - a (possibly empty) //toc element

#### //block\[@name="ToCHeading"\]

The table of contents heading block typically contains the word
"Contents" in all caps and is centred. We use this element because AKN
does not allow anything other than a //tocItem in the //toc element (a
//toc/heading would be preferable).

#### //block\[@name="ToCType"\]

The table of contents type block typically contains the word "Section"
and is left justified (to indicate that the numbers beneath it are
section numbers) for Bills and Acts. While SIs/SSIs might put the name
of the section-like element for those documents here, this does not
appear to be the practice so there is no such block in SIs/SSIs. While
this could potentially be dealt with using a custom attribute on //toc,
that would disobey the principal that text that appears on the page
should be XML content.

#### //toc

The //toc element contains the contents of the table of contents and is
made up of a list of //tocItems.

#### //tocItem

Each //tocItem corresponds with an element in the //body of the Act,
Bill, SI or SSI.

The @href attribute is a link to the @eId value of the corresponding
body element.

The @level attribute specifies a level within the table of contents to
help to model containment despite the fact that the table of contents is
just a list. Higher levels are contained within levels with a lower
@level value.

The @class attribute matches the @class value for the referenced body
element but with "ToC" appended. This allows a table of contents style
for each corresponding body style to be defined. Because of the
limitations of the //toc markup, we add a //tocItem\[@class="ruleToc"\]
for the horizontal rule that separates the first schedule entry in the
table of contents from the entries for the body elements.

Each //tocItem contains an optional number (//inline\[@name="tocNum"\])
and heading (//inline\[@name="tocHeading"\]) based on the //num and
//heading of the referenced body element (if they have one).

#### //inline\[@name="tocNum"\]

Following the mapping from CLML to AKN, we use this construct to
distinguish the number component of the referenced body element for
display in the table of contents.

Note that greater use of the //ref element might be possible here to
ensure that the table of contents once created is maintained but, since
we intend to auto-generate the table of contents normally, it would seem
sensible to leave this as simple as possible and just regenerate it if
there are any changes to the //body (automatically if appropriate).

#### //inline\[@name="tocHeading"\]

Following the mapping from CLML to AKN, we use this construct to
distinguish the heading component of the referenced body element for
display in the table of contents.

## //preface

Legislation in the English tradition doesn't really have a defined scope
for the preface to a legislative document - its not a standard term. We
use the //preface element to contain all the material that does not
necessarily appear on the //coverPage but appears after the table of
contents and before the preamble or enacting words for Acts and Bills or
simply before the preamble or enacting formula for SSIs/SIs. Scottish
Bills and Acts typically don't have either a preamble or enacting words
so the //preface is normally followed by the //body.

In Scottish Bills, the //preface contains:

  - an explanatory notes or accompanying documents statement
    (//tblock\[@class="explanatoryNotesStatement"\])
  - the title block (//block\[@name="title"\] similar to that on the
    //coverPage)
  - the stage version block (//block\[@name="stageVersion"\] again
    similar to that on the //coverPage)
  - the long title

In SIs and SSIs, the //preface contains:

  - Optional procedural or correction rubrics
    (//block\[@name="proceduralRubric|correctionRubric"\])
  - A banner (//block\[@name="banner"\] containing the words "SCOTTISH
    STATUTORY INSTRUMENT" or "STATUTORY INSTRUMENT" as appropriate
    (possibly further qualified by the word "DRAFT"
  - a number block (//block\[@name="number"\]) containing the SI year
    and number
  - a set of one or more subjects (//container\[@name="subjects"\])
  - a title block (//block\[@name="title"\])
  - Optional approval rubric (//block\[@name="approval"\])
  - Optional laid in draft before Parliament rubric
    (//block\[@name="laidInDraft"\])
  - Date block (//container\[@name="dates"\]
  - Optional table of contents (see above)

In Scottish Amendments, there is no preface as amendments typically
appear in published form only within an amendment list.

In Scottish Amendments lists, we use the //preface to hold the
information that appears on the front page before the first amendment.
This includes:

  - <span class="underline">TODO</span>

In Finance Resolutions, no //preface is required.

### //tblock\[@class="explanatoryNotesStatement"\] (or accompanying document statement)

For consistency with UK Bills, we adopt the name explanatory notes
statement even though the heading in Scotland is typically the more
accurate "Accompanying Documents". We use a //tblock because this has a
heading followed by one or more text blocks. The heading in Scotland is
allcaps. The content is typically bold face.

For Scottish Bills:

``` 
 <tblock class="explanatoryNotesStatement" GUID="_158cb8a1-fc8e-46bd-90bc-e3a000051dc7" eId="fnt__explNotesStmnt">
  <heading GUID="_16431ff3-0634-4d26-ace4-a65c9015d4a2" eId="fnt__explNotesStmnt__hdg">ACCOMPANYING DOCUMENTS</heading>
  <p>Explanatory Notes, together with other accompanying documents, are printed separately as <ref class="placeholder" href="#varBillNo"></ref>-EN. A Policy Memorandum is printed separately as <ref class="placeholder" href="#varBillNo"></ref>-PM.</p>
 </tblock>
 
```

For UK Bills:

``` 
 <tblock class="explanatoryNotesStatement" GUID="_fe17b740-70af-42f7-82d4-d62a6cbe6829" eId="fnt__explNotesStmnt">
  <heading GUID="_fc3b48df-b8fb-4b92-82f0-9e61fa0ec208" eId="fnt__explNotesStmnt__hdg">EXPLANATORY NOTES</heading>
  <p>Explanatory notes to the Bill, prepared by the Home Office, are published separately as Bill 8-EN.</p>
 </tblock>
```

### //longTitle

We use the standard AKN element for the long title despite the fact that
English and Scottish long titles are typically a single block of text
and have no further structure.

``` 
 <longTitle GUID="_b57a853d-55b1-407b-852c-2bd2209d8bd4" eId="fnt__longtitle">
  <p>An Act of the Scottish Parliament to allow decrofting by owner-occupier crofters; and for connected purposes.</p>
 </longTitle>
```

### //block\[@name="proceduralRubric"\]

Statutory Instruments may contain a procedural or correction rubric
before the banner. If multiple paragraphs/blocks are required, there may
be more than one such block.

``` 
 <block name="proceduralRubric" GUID="_8ca9f70e-68ed-4407-8bf4-ed73ad841717" eId="fnt__rubric">Draft Order laid before the Scottish Parliament under section 459(6)(b) of the Proceeds of Crime Act 2002, for approval by resolution of the Scottish Parliament.</block>
 <block name="banner" GUID="_49850a8c-deaa-4ae2-82e1-16a5869d0ff4" eId="fnt__banner">DRAFT SCOTTISH STATUTORY INSTRUMENT</block>
 
```

### //block\[@name="correctionRubric"\]

Example with convoluted correction headnote:

  - [The European Organization for Astronomical Research in the Southern
    Hemisphere and the European Space Agency (Immunities and Privileges)
    (Amendment)
    Order 2018](http://www.legislation.gov.uk/ukdsi/2018/9780111167984/pdfs/ukdsi_9780111167984_en.pdf)
    (note this would be coded just like the more common example below
    but with longer text)

<!-- end list -->

``` 
 <block name="correctionRubric" GUID="_e75faa87-b4a3-4b69-96db-99f47142987b" eId="fnt__rubric">This Statutory Instrument has been made in consequence of a defect in <ref href="http://www.legislation.gov.uk/id/uksi/2007/610">SI 2007/610</ref> and is being issued free of charge to all known recipients of that Statutory Instrument.</block>
 <block name="banner" GUID="_d8695178-2337-459d-a8f3-07884f09f42d" eId="fnt__banner">STATUTORY INSTRUMENT</block>
```

### //block\[@name="banner"\]

Typically contains "DRAFT STATUTORY INSTRUMENT", "STATUTORY INSTRUMENT"
or "SCOTTISH STATUTORY INSTRUMENT".

    <block name="banner" GUID="_d8695178-2337-459d-a8f3-07884f09f42d" eId="fnt__banner">STATUTORY INSTRUMENT</block>

### //container\[@name="subjects"\] and //container\[@name="subject"\]

Statutory Instruments have one or more subject blocks identifying one or
more subjects from a controlled vocabulary to which they are relevant
and, particularly for UK SIs of limited jurisdictional applicability,
these may include one or more jurisdictions (again from an even more
limited vocabulary).

We wrap all of the subjects in a container,
//container\[@name="subjects"\].

Examples with larger numbers of subjects, subtopics and extents include:

  - [The Local Policing Bodies (Consequential Amendments)
    Regulations 2011](http://www.legislation.gov.uk/uksi/2011/3058/introduction/made)
  - [The Environment, Planning and Rural Affairs (Miscellaneous
    Amendments) (Wales)
    Regulations 2018](http://www.legislation.gov.uk/wsi/2018/1216/introduction/made)
  - [The Environment, Food and Rural Affairs (Miscellaneous Amendments)
    (England)
    Regulations 2018](http://www.legislation.gov.uk/uksi/2018/575/introduction/made)

#### //container\[@name="subject"\]

Each separate subject block is contained within a
//container\[@name="subject"\] which in turn will contain exactly one
//block\[@name="subject"\] followed by an optional
//block\[@name="subsubject"\] which appears below the subject in a
smaller font.

Within the subject //block elements each distinct subject is wrapped in
an inline //concept tag followed by an optional comma separated list of
jurisdictions each of which is contained in an inline //concept tag.

For example:

``` 
 <container name="subjects">
  <container name="subject" GUID="_89b26a7e-1f5f-4653-8ae3-295d542d2b60" eId="fnt__subject">
   <block name="subject"><concept class="title" refersTo="#d4e95">Agriculture</concept>, <concept class="title" refersTo="#jurisdiction-eng">England</concept></block>
   <block name="subsubject" GUID="_64c94522-edfe-4417-ac20-8347e68d9711" eId="fnt__subject__subsubject"><concept class="subtitle" refersTo="#d4e97">Livestock Industries</concept></block>
  </container>
  <container name="subject" GUID="_d893fdf7-1f7f-4066-b2d7-19aedeeb7d4a" eId="fnt__subject__oc_2">
   <block name="subject"><concept class="title" refersTo="#d4e100">Animals</concept>, <concept class="title" refersTo="#jurisdiction-eng">England</concept></block>
   <block name="subsubject" GUID="_87d02695-2dd3-4384-aa1f-5a4da25373d2" eId="fnt__subject__oc_2__subsubject"><concept class="subtitle" refersTo="#d4e102">Animal Health</concept></block>
   <block name="subsubject" GUID="_9fc2bc4e-bcad-4cd4-97ad-178f5002903c" eId="fnt__subject__oc_2__subsubject__oc_2"><concept class="subtitle" refersTo="#d4e104">Animal Welfare</concept></block>
  </container>
 </container>
```

#### //block\[@name="subject"\]

Contains the block with the main subject - jurisdiction for that subject
is optionally included in a separate inline //concept tag - see example
above for //container\[@name="subject"\].

This is required within a //container\[@name="subject"\].

#### //block\[@name="subsubject"\]

Contains the block with the subtopic - again inline //concept tag mark
each individual subtopic - see example above for
//container\[@name="subject"\].

This is optional following a //block\[@name="subject"\] within a
//container\[@name="subject"\].

### //block\[@name="title"\]

In Statutory Instruments the title block appear at this point. It is
used identically as for Acts and Bills (see above). Note that, unlike
Acts (where the historic leading "The" has been removed), SIs titles
typically begin with "The " (in the UK - other Commonwealth
jurisdictions have extended the same change to both Acts and subordinate
legislation).

An example of an exceptionally long title is:

  - [The Attorney General’s Human Rights Guidance (The Application of
    Section 5 of the Criminal Law Act (Northern Ireland) 1967 to Rape
    Victims and Those to Whom They Make Disclosures in Connection With a
    Claim for Social Security, Child Tax Credit or Anonymous
    Registration on the Electoral Roll) Order (Northern
    Ireland) 2018](http://www.legislation.gov.uk/nisr/2018/110/contents/made)

<!-- end list -->

``` 
 <block name="title" GUID="_c657bfc1-3383-4608-bb9e-b3f311c2127e" eId="fnt__st"><docTitle GUID="_2a7c8325-6877-46b7-aef8-889dd6eb2c21" eId="fnt__st__dtitle"><ref href="#varSITitle"></ref></docTitle></block>
 
```

OR

``` 
 <block name="title" GUID="_c657bfc1-3383-4608-bb9e-b3f311c2127e" eId="fnt__st"><docTitle GUID="_2a7c8325-6877-46b7-aef8-889dd6eb2c21" eId="fnt__st__dtitle">The Environment, Food and Rural Affairs (Miscellaneous Amendments) (England) Regulations 2018</docTitle></block>
```

### //block\[@name="approval"\]

Statutory Instruments may contain an approval rubric recording the
approval by Parliament (e.g. "Approved by the House of Commons").

This will never have a date associated with it – just the centred text
itself. These are used specifically for class iii made affirmatives, aka
emergency affirmatives, which get made and can come into force
immediately, but which require Parliamentary approval to remain in force
past a certain period. These are published initially with a procedural
headnote and the usual made/laid/CIF headings. When/if the SI receives
approval, it is republished with the procedural headnote removed and the
“Approved by…” crossheading added above all of the other date
crossheadings, to indicate that it did not expire and remains an active
part of the law.

Some examples:

  - [UKSI 2019/837](http://www.legislation.gov.uk/uksi/2019/837/introduction/made);
    
  - [UKSI 2019/616](http://www.legislation.gov.uk/uksi/2019/616/made);
    and
  - [UKSI 2013/1571](http://www.legislation.gov.uk/uksi/2013/1571/made).
    

<!-- end list -->

``` 
 <block name="approval" GUID="_cfa68e39-2376-4d8d-a37c-c50ef41e9b16" eId="preamble__approval">A draft of this Order has been approved by a resolution of each House of Parliament.</block>
```

``` 
 <block name="approval" GUID="_bad34bee-358f-4703-acda-35e269c984a5" eId="fnt__approval">Approved by both Houses of Parliament</block>
 
```

### //block\[@name="laidInDraft"\]

Statutory Instruments may contain a statement "Laid in draft before
Parliament" which is formatted differently to the date block and doesn't
display a date or information about timing (although the current markup
contains this information) so we use a different //block for this and
keep it before the date block. The last example below is an instrument
made by the Archbishop's Council, laid before General Synod, and then
laid before Parliament.

Some examples include:

  - [The CRC Energy Efficiency Scheme (Revocation and Savings)
    Order 2018](http://www.legislation.gov.uk/uksi/2018/841/made)
  - [The Health and Care Professions Council (Registration and Fees)
    (Amendment) Rules Order of
    Council 2015](http://www.legislation.gov.uk/uksi/2015/93/made)
  - [The Wildlife and Countryside Act 1981 (England and Wales)
    (Amendment)
    Regulations 2016](http://www.legislation.gov.uk/uksi/2016/127)
  - [The Parochial Fees
    Order 2004](http://www.legislation.gov.uk/uksi/2004/1890)

<!-- end list -->

``` 
 <block name="laidInDraft" GUID="_389d6acc-5efe-4abf-a18f-09aa36decbb7" eId="fnt__laidInDraft"><span>Laid before Parliament in draft</span><docDate date="1970-12-23" GUID="_ff5bc21d-d72b-497c-b170-710d81dcbf0b" eId="fnt__laidInDraft__ddate">23rd December 1970</docDate></block>
```

``` 
 <block name="laidInDraft" GUID="_764fe173-3a4d-4774-9afa-e3d04199a594" eId="fnt__laidInDraft"><span>Laid before the General Synod in draft</span><docDate date="2004-01-09" GUID="_6af29b78-0621-4ab1-a273-ffdf19db0ce3" eId="fnt__laidInDraft__ddate">9th July 2004</docDate></block>
```

### //container\[@name="dates"\] and date blocks

Statutory Instruments will typically have a table after the title block
outlining significant dates for that instrument. These include:

  - Date the instrument was made (//block\[@name="madeDate"\])
  - Date the instrument was laid before Parliament
    (//block\[@name="laidDate"\])
  - Date the instrument first comes into force
    (//block\[@name="commenceDate"\])

We use //span for the prompt and //docDate for the date/time value in
each block. In situations where there is not //docDate (where the
commencement depends on particular provisions or an external event say),
the display essentially merges the columns of the table for that row.

For example:

``` 
 <container name="dates">
  <block name="madeDate"><span>Made</span><docDate date="2018-11-13" GUID="_47c8f353-4029-4eed-a9d5-09f232434575" eId="fnt__ddate">13th November 2018</docDate></block>
  <block name="laidDate"><span>Laid before the Scottish Parliament</span><docDate date="2018-11-14" GUID="_fe823961-c6ce-4b32-8a1c-a9b420f834fd" eId="fnt__ddate__oc_2">14th November 2018</docDate></block>
  <block name="commenceDate"><span>Coming into force</span><docDate date="2019-04-06" GUID="_62554940-bdd4-4f72-b9ea-7bb95aa50b17" eId="fnt__ddate__oc_3">6th April 2019</docDate></block>
  </container>
```

Some more exotic examples include:

  - Times:
      - 12 hr [The Loan Relationships and Derivative Contracts
        (Disregard and Bringing into Account of Profits and Losses)
        (Amendment No. 2)
        Regulations 2011](http://www.legislation.gov.uk/uksi/2011/2912/made)
        
      - 24 hr [The Food Protection (Emergency Prohibitions) (Scallops)
        (Irish Sea)
        Order 2004](http://www.legislation.gov.uk/uksi/2004/2040/made)
  - Coming into force:
      - Multiple ‘coming into force’ used:
          - [The Paternity and Adoption Leave (Amendment)
            Regulations 2014](http://www.legislation.gov.uk/uksi/2014/2112/made)
          - [The Alternative Dispute Resolution for Consumer Disputes
            (Amendment)
            Regulations 2015](http://www.legislation.gov.uk/uksi/2015/1392/made)
      - Format options:
          - [date
            only](http://www.legislation.gov.uk/uksi/2015/93/made); or
          - [regulation and no
            date](http://www.legislation.gov.uk/uksi/2016/636/introduction/made);
            or
          - [regulation and
            date](http://www.legislation.gov.uk/uksi/2014/2112/made)

<!-- end list -->

``` 
 <container name="dates" GUID="_7d34be92-4038-45e2-89cd-dfbde2c93579" eId="fnt__dates">
  <block name="madeDate" GUID="_e5724a77-2b01-41b9-b438-b880ec06c144" eId="fnt__dates__madeDate"><span>Made</span><docDate date="2017-03-16T09:00:00" GUID="_8f87fd62-212e-4f51-a577-93898be85bd0" eId="fnt__dates__madeDate__ddate">at 9.00 a.m. on 16th March 2017</docDate></block>
  <block name="laidDate" GUID="_f9f0e0c9-4742-4714-8c4c-745a72031c7c" eId="fnt__dates__laidDate"><span>Laid before Parliament</span><docDate date="2017-03-16T14:00:00" GUID="_347cea33-f56b-47ef-adf6-a59be8d6ac6b" eId="fnt__dates__laidDate__ddate">at 2.00 p.m. on 16th March 2017</docDate></block>
  <block name="commenceDate" GUID="_c263ba91-b799-4c76-b452-41b53edbbd9a" eId="fnt__dates__commenceDate"><span>Coming into force in accordance with articles 1(2), 2 and 3</span></block>
 </container>
```

``` 
 <container name="dates" GUID="_bb8a7cb9-271e-43ed-8171-ffab5a3f2731" eId="fnt__dates">
  <block name="madeDate" GUID="_337462e4-eeb8-4649-865f-48be478c3ddf" eId="fnt__dates__madeDate"><span>Made</span><docDate date="2016-06-09T18:29:00" GUID="_1c364201-35eb-4ea1-ac4c-c2b126a5dd94" eId="fnt__dates__madeDate__ddate">6.29 p.m. on 9th June 2016</docDate></block>
  <block name="commenceDate" GUID="_83752223-f8bf-4bcd-a013-1504c832cbf4" eId="fnt__dates__commenceDate"><span>Coming into force in accordance with <ref href="#reg_1">regulation 1</ref></span></block>
 </container>
```

``` 
 <container name="dates" GUID="_31f5e4d6-414e-4045-8f6c-20c1ebeb3a04" eId="fnt__dates">
  <block name="madeDate" GUID="_e34439b8-c0cc-4b9c-bfc3-54fae1bafcd7" eId="fnt__dates__madeDate"><span>Made</span><docDate date="2007-03-12" GUID="_72a96837-d986-4646-96b0-2d6f952d090b" eId="fnt__dates__madeDate__ddate">12th March 2007</docDate></block>
  <block name="laidDate" GUID="_683a5f2e-1eea-44dd-8def-1048634b2d91" eId="fnt__dates__laidDate"><span>Laid before Parliament</span><docDate date="2007-03-16" GUID="_1adcf9fc-ca0d-48a3-9efe-c4fe45bd3941" eId="fnt__dates__laidDate__ddate">16th March 2007</docDate></block>
  <block name="commenceDate" GUID="_c09c28a6-a3a4-4b18-88f4-b60a0822a431" eId="fnt__dates__commenceDate">Coming into force</block>
  <block name="commenceDate" class="commenceClauses" GUID="_99d162a7-f1cf-4b94-99f4-6f56e861fb3a" eId="fnt__dates__commenceDate__oc_2"><span>for the purpose of <ref href="#reg_14">regulation 14</ref></span><docDate date="2007-03-13" GUID="_982a38f0-93c5-4672-84f4-35846d9d1ec2" eId="fnt__dates__commenceDate__oc_2__ddate">13th March 2007</docDate></block>
  <block name="commenceDate" class="commenceClauses" GUID="_05e3812f-ba76-4d61-821f-2e8e821a06f1" eId="fnt__dates__commenceDate__oc_3"><span>for all other purposes</span><docDate date="2007-04-01" GUID="_1cdb0b5e-930b-4af0-9c3c-53aa763f94e9" eId="fnt__dates__commenceDate__oc_3__ddate">1st April 2007</docDate></block>
 </container>
```

``` 
 <container name="dates" GUID="_14339843-3bff-42fe-ab71-f1bcc300baa9" eId="fnt__dates">
  <block name="madeDate" GUID="_e21f4fc3-a832-45f7-a853-74b5d6e66b08" eId="fnt__dates__madeDate"><span>Made</span><docDate date="2018-05-02" GUID="_0b37164f-8201-43a4-9361-eb34ee4bee57" eId="fnt__dates__madeDate__ddate">2nd May 2018</docDate></block>
  <block name="commenceDate" GUID="_97a9f056-9f37-47b0-b90a-dff5be85cee6" eId="fnt__dates__commenceDate">Coming into force</block>
  <block name="commenceDate" class="commenceClauses" GUID="_48ef9ce6-725f-4837-b320-14084f25cf70" eId="fnt__dates__commenceDate__oc_2"><span>For the purpose of <ref href="#reg_1">regulations 1</ref> to <ref href="#reg_4">4</ref> and <ref href="#reg_15">15</ref></span><docDate date="2018-05-04" GUID="_20c214c7-bb92-40b2-9d2e-134c2a4922a0" eId="fnt__dates__commenceDate__oc_2__ddate">4th May 2018</docDate></block>
  <block name="commenceDate" class="commenceClauses" GUID="_bb0e4d3b-27b5-4878-9904-e85e0938643c" eId="fnt__dates__commenceDate__oc_3"><span>For all other purposes </span><docDate date="2018-11-05" GUID="_5154b7a9-e716-4e54-b601-7c9cfa3b9c6a" eId="fnt__dates__commenceDate__oc_3__ddate">5th November 2018</docDate></block>
 </container>
```

## //preamble (preamble and enacting words)

Scottish Bills and Acts typically contain neither a preamble nor
enacting formula/words. UK Bills and Acts (in their original form
although not commonly in reprints) typically include an enacting formula
occasionally preceded by a preamble. Following the AKN model which is
largely European in influence, we adopt the AKN's broader definition of
preamble so the //preamble element includes not only what we would
normally call a preamble (encoded using the //recitals element if
present) but also the enacting words (//formula). This follows the clear
intention of AKN if not the normal nomenclature of the English
tradition.

Therefore for UK Bills and Acts, the //preamble contains:

  - the preamble if present (encoded as //recitals)
  - the enacting words (encoded as //formula)

If neither are present, as is normally the case in Scottish Bills and
Acts, the entire //preamble is omitted as AKN does not permit an empty
//preamble. Where a preamble is used in Scottish Bills, it would be in
//preamble/recitals.

For SIs and SSIs, there is little consistency about the ordering of the
preamble and enacting words and some potential ambiguity about where
blocks of text form part of the preamble, the enacting words or are
neither. For clarity, enacting words (//formula) will be limited to just
the boilerplate wording and any preamble or other material will simply
be //p or //tblock (or possibly //blockList) elements directly as
children of the //preamble.

### //recitals (preamble)

AKN comes from a primarily European influence where the statements
typically beginning "Whereas" are referred to as recitals rather than a
preamble. Since this conceptually is identical to what we in the English
tradition would call the preamble, we adopt the AKN //recitals for what
we would normally call a preamble in Bills and Acts (see above for SIs
and SSIs) and include the enacting words within the //preamble using
//formula element adopting the broader scope of AKN (simply because we
would have to define alternative structures and AKN doesn't allow much
flexibility here).

A preamble can be a single block, a series of blocks or a mix of blocks
and paragraphs. Because //recitals can contain more than one //recital
and both //recitals and //recital have optional //num and //heading
elements, there are some different options as to how to capture
preambles with varied structure.

The simple case with a single block is obvious:

``` 
 <recitals GUID="_d3ec2b89-f6f3-4f59-a51d-51cda615adc0" eId="fnt__preamble">
  <recital GUID="_0bc716b1-d89a-4e1e-bc18-f4bd131ab96b" eId="fnt__preamble__para">
   <p>Whereas a draft of this Order has been laid before Parliament in accordance with section 10 of the International Organisations Act 1968 (hereinafter referred to as the Act) and has been approved by a resolution of each House of Parliament:</p>
  </recital>
 </recitals>
```

#### //recital

We avoid the use of multiple //recital elements unless the top level
blocks are numbered preferring to use a single //recital with multiple
//p elements and paragraphing within the single recital. See also [Lists vs Paragraphing](../general-principles.md#lists-vs-paragraphing).
>>>>>>> b5a70e3539c93a0b020e9a1f7c1c1f98b861c6d5

``` 
 <recitals>
  <recital GUID="_9091995b-b093-4c1c-a022-ab9f19fac442" eId="fnt__preamble">
   <p>Whereas the Secretary of State, the Scottish Ministers, the Welsh Ministers and the Department of Agriculture, Environment and Rural Affairs of Northern Ireland have in accordance with section 48 of and paragraph 10 of Schedule 3 to the Climate Change Act 2008&#8212;</p>
   <tblock class="para1" GUID="_e59bbcd8-1a37-432c-88d0-adbf1fa98437" eId="fnt__preamble__para_a">
     <num>(a)</num>
     <p>obtained and taken into account the advice of the Committee on Climate Change in respect of this Order; and</p>
    </tblock>
    <tblock class="para1" GUID="_b26aef3f-0547-46d5-b1c6-ac0aa47c0148" eId="fnt__preamble__para_b">
     <num>(b)</num>
     <p>consulted such persons likely to be affected by this Order as they considered appropriate,</p>
    </tblock>
  </recital>
 </recitals>
```

<span class="underline">These examples are from SSIs but we won't use
//recitals in SSIs so need to find some Bill/Act examples to replace
these with</span>

### //formula (enacting words)

Although the term "formula" would normally be used in the English
tradition to refer to a mathematical equation within the body of the
legislation, the intention of this element was to capture what the
English tradition would refer to as the enacting words or enacting text
(enacting formula is the longer name for this element within AKN).
Therefore, it is entirely consistent to use this element for the
enacting words that precede any UK Bill or Act (as enacted). There are a
few different boiler-plate enacting words depending on the type of the
Bill.

Likewise, most Statutory Instruments have boilerplate wording which
adjusts based on the Act under which they are made, the document sub
type and procedural differences. These are formatted similarly to any
other constructs within //preamble or //preface.

There is one exception. In resolutions of the UK Parliament (but not
Scottish Parliament), the rubric "Resolution of the House of Commons,
dated ..., passed in pursuance of the House of Commons ..." is really
taking the role of the enacting formula but is all boldface. Since we
can distinguish this from the document subtype, we do not add any
additional markup for the //formula content other than to note that if
it is not correctly wrapped in the //formula, it will not appear in
bold.

These are a feature of House of Commons Members’ Fund Resolutions (along
with similarly titled SIs from earlier years) and will not be found in
any other type of SI. These are very rare and very different to normal
SIs in terms of their structure – a recent example is
[UKSI 2005/657](http://www.legislation.gov.uk/uksi/2005/657/pdfs/uksi_20050657_en.pdf).

#### //block\[@name="royal"\]

See also the Royal/Privy Council assent(?) rubric:

  - [The CRC Energy Efficiency Scheme (Revocation and Savings)
    Order 2018](http://www.legislation.gov.uk/uksi/2018/841/made)
  - [The General Pharmaceutical Council (Amendment of Miscellaneous
    Provisions) Rules Order of
    Council 2016](http://www.legislation.gov.uk/uksi/2016/1008/introduction/made)
