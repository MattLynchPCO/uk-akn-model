# Document metadata

UK LDAPP needs to manage general metadata but also metadata from
TeraText for Legislation (project metadata as well as metadata created
by TeraText DMS to keep track of versions etc). The mechanism for
managing this between Oxygen and TeraText is described in more detail in
the technical documentation. This page describes what we expect LDAPP to
manage within the draft AKN documents at least until they are published
by TNA.

## Document version metadata

From the Scottish Bill template:

    <meta>
     <identification source="#ldapp">
      <FRBRWork>
       <FRBRthis value="#varWork"/>
       <FRBRuri value="#varWorkUri"/>
       <FRBRdate date="9999-01-01" name="sppubb"/>
       <FRBRauthor href="#varAuthor"/>
       <FRBRcountry value="GB-SCT"/>
       <FRBRsubtype value="#varDocSubType"/>
       <FRBRnumber value="#varProjectId"/>
       <FRBRname value="#varBillTitle"/>
      </FRBRWork>
      <FRBRExpression>
       <FRBRthis value="#varExpression"/>
       <FRBRuri value="#varExpressionUri"/>
       <FRBRdate date="9999-01-01" name="draft"/>
       <FRBRauthor href="#varAuthor"/>
       <FRBRlanguage language="eng"/>
      </FRBRExpression>
      <FRBRManifestation>
       <FRBRthis value="#varManifestation"/>
       <FRBRuri value="#varManifestationUri"/>
       <FRBRdate date="9999-01-01" name="akn_xml"/>
       <FRBRauthor href="#varAuthor"/>
       <FRBRformat value="application/akn+xml"/>
      </FRBRManifestation>
     </identification>
    </meta>

Mapping these concepts from FRBR to the DMA hierarchy that TeraText DMS
uses:

  - ***FRBRWork*** is roughly equivalent to *Configuration History* -
    the entire history of a particular document

<!-- end list -->

``` 
    * FRBR assumes linear versioning so //Version Series// and //Configuration History// are conflated
* //**FRBRExpression**// is roughly equivalent to the combination of a //Version Description// (probably has a version label) and //DocVersion// (has information about the various Renditions or Manifestations available of that particular version)
    * Again because linear versioning is assumed, you don't need to distinguish between the label in a particular Version Series (Version Description) and the actual content that combines to make that instance of a version (DocVersion) which might be shared in multiple Version Series each with a corresponding Version Description
* //**FRBRManifestation**// is pretty close to a //Rendition// and so can be distinguished with a MIME type or document type extension (pdf, xml, akn, docx, ...)
* //**FRBRItem**// is pretty close to a //ContentElement// but is typically only used when the document is fragmented and information about the fragment seems to be in the //**FRBRManifestation**// metadata so best just to avoid this unless we come up with a reason to use it.
```

## Document identification markup

In each of these, they can contain (? marks optional. + one or more, and
\* 0 or more, bold marks fields we must or will use, italic marks fields
we will likely use and plain text marks fields we will likely not use):

  - ***FRBRthis*** - URI/IRI of the particular component of the document

<!-- end list -->

``` 
   * I think that means if the component is the whole document, this is identical to FRBRuri
* //**FRBRuri**// - URI/IRI of the whole document
   * Either the DMA OIID or a human readable identifier (see below)
* *//**FRBRalias**// - An alternative name or URI for the document
   * We use this to store a DMA OIID so that we can easily find this document in TeraText DMS
   * We should also store other citation forms in an instance of this (not the short title which should go in FRBRname) such as the chamber (UK only), session and bill number (qualified like the FRBRuri/FRBRthis value if it is an Expression or Manifestation) once available - this is more important in UK Bills where the bill number changes each version and a trail of FRBRalias elements showing the predecessors using the standard metadata used by Parliament
* +//**FRBRdate**// - any dates relevant to the document, each date must have a @name which could be used to distinguish between different types of date (e.g. created, lastModified, published, ...)
* +//**FRBRauthor**// - for Scottish Bills and UK Bills this will be the relevant Parliaments (so one instance only and essentially fixed by the type of document it is)
* ?//**componentinfo**// - used for managing fragmented documents:
   * only used if fragmented documents are delivered outside of the DMS/Oxygen environment - currently not envisaged
* //**preservation**// - actions taken to preserve this work, expression or manifestation
   * we are managing the draft stage, not the archival stage so not used by us but likely used by TNA once they have the documents
```

### Work (FRBR) or Configuration History (DMA)

In addition to these, FRBRWork has:

  - ***FRBRcountry*** - Alpha code for the country (should be ISO 3166-1
    Alpha-2 (not 3\!) - suggest this should always be "UK"
  - ***FRBRsubtype*** - the Document sub type
      - we always have one of these even if there is only one for the
        DocType which is stored in //bill|act@name

this is supposed to form part of the "Work" component of the document
IRI but I don't think that is sensible

  - \****FRBRnumber*** - a string or number which makes up the "Work"
    component of the document IRI
      - I think this corresponds with the (number component? of the)
        {projectId} referred to below but would need to be qualified by
        the {documentLabel} as there isn't a one to one correspondence
        between Works and Projects (many Projects will contain more than
        one Work)
  - ***FRBRname*** - the title of the document
      - this is supposed to make up the "Work"component of the document
        IRI but that seems silly to me
      - the short title of the bill should go in here (to be replaced
        with the Act title when it becomes an Act)
  - ***FRBRprescriptive*** - Boolean value which is true if this text
    could become prescriptive such as an Act or Bill
      - Always true for Bills, Acts and SIs whether draft or made
      - Less clear for amendments and the various lists of amendments
  - ***FRBRauthoritative*** - Boolean value which is true if the
    document contains authoritative text
      - Probably shouldn't be true unless it is true of the entire work
        so probably always false (unless we consider the Act to be a
        different FRBRWork in which case it is true for the Act but not
        the bill)

### Expression (FRBR) or DocVersion/Version Description (DMA)

In addition to these FRBRExpression has:

  - ?***FRBRversionNumber*** - a version number or label for this
    particular version (arbitrary string)

<!-- end list -->

``` 
   * while we could use something like “v01.01” like we currently use for OQPC AKN suggests we use something more meaningful like “introd”, “stage1”, “stage2”, “stage3” for Scottish Bills, "queens" and "official" for Scottish Acts, and "introd-hc", "committee-hc", "report-hc", "introd-hl", "committee-hl", "report-hl" for UK Parliament Bills and "vellum", and "enacted" for UK Acts - see tables below
   * We probably need a mix of both to manage draft and released/published versions
* ?//**FRBRauthoritative**// - Boolean value which is true if the document contains authoritative text
   * Probably shouldn't be true unless this version is either tabled or enacted (even tabled might not be authoritative)
* ?//**FRBRmasterExpression**// - reference to the master expression (for the purposes of determining @wId values)
   * Pointer to the master expression from which other expressions are derived
   * Need to set this with no @href if there is no master expression
   * Point to the previous version if we are using @wId (not clear to me what value there is in these since we have GUID)
* +//**FRBRlanguage**// - languages available in this version
   * 3 letter language - this will always have "ENG" but may in future have Scots, Gaelic or Welsh (we hope)
* ?//**FRBRtranslation**// - reference to the source from which this is a translation
   * Why is a translation from one computer language any different from a translation from a human language?  We use Rendition (equivalent of Manifestation) for both concepts.  I doubt we will ever use this or, if we do, we'll try to use it in FRBRManifestation.
```

Values for the FRBRversionNumber for published versions of a Bill/Act
are outlined below:

|                        |               |                   |
| ---------------------- | ------------- | ----------------- |
| **Parliament/Chamber** | **Stage**     | **versionNumber** |
| Scottish Parliament    | Introduction  | introd            |
|                        | Stage 1       | stage1            |
|                        | Stage 2       | stage2            |
|                        | Stage 3       | stage3            |
| (Act)                  | Queen's Print | queens            |
|                        | Official      | official          |
| House of Commons       | Introduction  | introd-hc         |
|                        | Committee     | committee-hc      |
|                        | Report        | report-hc         |
| House of Lords         | Introduction  | introd-hl         |
|                        | Committee     | committee-hl      |
|                        | Report        | report-hl         |
| UK Parliament (Act)    | Vellum        | vellum            |
|                        | Enacted       | enacted           |

For amendment lists and finance resolutions, the version label for
published lists should be the date of publication as an ISO date
(YYYY-MM-DD).

### Manifestation (FRBR) or Rendition (DMA)

In addition to these FRBRManifestation has:

  - ?***FRBRPortion*** - the @eId of the portion that this fragment is
    from

<!-- end list -->

``` 
   * It seems like this should be in FRBRItem NOT FRBRManifestation
* ?//**FRBRformat**// - MIME type of the rendition
   * This will always be "application/akn+xml"
```

### Item (FRBR) or Component Element (DMA)

In addition to these FRBRItem has:

  - Nothing but the base attributes

<!-- end list -->

``` 
   * URI's/identifiers
   * DMA OIIDs as URIs
```

### DMA OIID and FRBRuri

While we could just use the DMA OIID as the FRBRuri, this has the
following problem:

  - You can't tell from the URI what project it belongs to easily
  - You can't tell from the Manifestation URI what the URI is for the
    Expression or from the Expression URI what it is for the Work (they
    all would be in the XML so this is less of a problem)
  - You can't necessarily tell what type of document, what type of
    project, or what type of Rendition you have

We have therefore included the DMA OIID in an FRBRalias at least for the
FRBRExpression (which points to the Version Description or DocVersion),
for the FRBRWork (pointing to the Configuration History) and
FRBRManifestation (pointing to the Rendition or ContentElement). This
means that Oxygen will always have access to the identfiers it needs to
tell TeraText DMS what to update.

## Human readable URI's/identifiers

The following is the pattern for human readable URI's:

|                           |                                                                                                                                                                                                                                                                      |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Work (CH)                 | [https:%%//%%{//systemURI//}/{//projectType//}/{//projectId//}/{//docLabel//}](https:%%//%%%7B//systemURI//%7D/%7B//projectType//%7D/%7B//projectId//%7D/%7B//docLabel//%7D)                                                                                         |
| Expression (VD/DV)        | [https:%%//%%{//systemURI//}/{//projectType//}/{//projectId//}/{//docLabel//}@{//FRBRversionNumber//}](https:%%//%%%7B//systemURI//%7D/%7B//projectType//%7D/%7B//projectId//%7D/%7B//docLabel//%7D@%7B//FRBRversionNumber//%7D)                                     |
| Manifestation (Rendition) | [https:%%//%%{//systemURI//}/{//projectType//}/{//projectId//}/{//docLabel//}@{//FRBRversionNumber//}/{//extension//}](https:%%//%%%7B//systemURI//%7D/%7B//projectType//%7D/%7B//projectId//%7D/%7B//docLabel//%7D@%7B//FRBRversionNumber//%7D/%7B//extension//%7D) |

where:

  - ***systemURI*** will be legi.teratext.leidos.com.au until a UK
    government domain name is allocated (something like legi.uk or
    legi.tna.gov.uk or legi.parliament.scot or legi.parliament.uk or
    some combination of those)
  - ***projectType*** could basically be the //bill@name (see the wiki
    page for the list but not updated when it becomes an //act)
  - ***projectId*** could be a number starting at 1 (or randomly
    assigned from a pool of say 100,000) or some other random string
    that doesn’t betray how long they have been working on it, it should
    be short enough to be human readable (so not a GUID/UUID)
  - ***docLabel*** could be a combination of a type and a number/ISO
    Date – e.g. {type}{NNNN}, where {type} is one of “bill” (might want
    to make it “dsi” even if the element is bill for SIs), “amend” for a
    single amendment, “marsh” for a marshalled list of amendments,
    “group” for a grouped list of amendments and “daily” for a daily
    list of amendments.
  - ***FRBRVersionNumber*** is as described above (a version label)
  - ***extension*** is a file type extension such as "pdf", "xml",
    "akn", "docx", etc. (typically "akn" or "xml" in this instance) 

This should be used for the FRBRuri value at the Work (no version label
or extension), Expression (no extension), and Manifestation level
(includes version label and extension).

In addition to these persistent URI's, for Bills there are often
additional identifiers using some combination of the session, the
chamber (for UK) and the bill number assigned by the chamber. Scottish
Parliament assigns a single Bill number that survives all stages. UK
Parliament assigns a new Bill number (unique to that chamber) every time
the Bill is republished. To preserve the persistence of the main URI,
rather than modify the URI to this more fleeting identifier, we will
also add an FRBRalias that replaces the projectId above with session
number, chamber and bill number whenever a new combination is published
so that these can be used to find documents in a collection also.

For amendments, the amendment numbers are specific to a particular
version of a Bill so the form of the Work URI should start with the Bill
Expression ID followed by "/amnd/" and the amendment number or D number.
So of the form

<https:%%//%%legi.teratext.leidos.com.au/ukpubb/564983/bill@introd-hc/amnd/5>

or

<https:%%//%%lawmaker.gov.uk/sppubb/43225/bill@introd/amnd/D0004>

## References and variables

The examples above contain @value attributes that are essentially
references to variables (beginning "\#var..."). The intent is to capture
the metadata variables that may be used in multiple places within a
single document instances in one place and use references to those
variables so they can be kept in sync.

These values are located in the //meta/references element with:

  - element names typically begining with "TLC", 
  - @eId - the name of the variable referenced (e.g.
    @eId="varBillTitle"),
  - @showAs - contains the value of the variable,
  - @href="\#varOntologies", a reference to the variable containing the
    URL of the ontology that defines all of these values.

### Scottish Bill/Act variables

The variables for Scottish Bills are:

  - //TLCConcept\[@eId="varDocSubType"\] - the type of subdocument this
    is (one of ...)
  - //TLCConcept\[@eId="varBillTitle"\] - the short title of the Bill
  - //TLCProcess\[@eId="varStageVersion"\] - the stage version of this
    particular version of the Bill (initially "Pre-Introduction")
  - //TLCProcess\[@eId="varProjectId"\] - the identifier of the Project
    to which this Bill belongs
  - //TLCProcess\[@eId="varWork"\] - a URI for the FRBR Work (or TTfL
    Configuration History) to which this Bill version belongs
  - //TLCProcess\[@eId="varWorkURI"\] - currently identical to \#varWork
  - //TLCProcess\[@eId="varCHOiid"\] - the OIID of the Configuration
    History object within TeraText for Legislation
  - //TLCProcess\[@eId="varExpression"\] - a URI for the FRBR Expression
    (or TTfL Version Description) of this version of the Bill
  - //TLCProcess\[@eId="varExpressionUri"\] - currently identical to
    \#varExpression
  - //TLCProcess\[@eId="varVDOiid"\] - the OIID of the Version
    Description object within TeraText for Legislation
  - //TLCProcess\[@eId="varManifestation"\] - a URI for the FRBR
    Manifestation (or TTfL Rendition) of this version of the Bill -
    typically the AKN manifestation/rendition
  - //TLCProcess\[@eId="varManifestationExpressionUri"\] currently
    identical to \#varManifestation
  - //TLCConcept\[@eId="varActYear"\] - a four digit calendar year which
    is the likely year for this Bill to become an Act (if it hasn't
    already)
  - //TLCConcept\[@eId="varActTitle"\] - the likely short title of the
    resulting Act (calculated from \#varBillTitle and \#varActYear)
  - //TLCConcept\[eId="varIntroDate"\] - once introduced, the date of
    introduction (@showAs is an ISO 8601 format date with no time
    component)
  - //TLCConcept\[@eId="varBillNoComp"\] - once introduced, the Bill
    number component within the current year (a positive integer)
  - //TLCConcept\[@eId="varBillNo"\] - the full Bill number -
    @showAs="SP Bill \#varBillNoComp"
  - //TLCConcept\[@eId="varSessionNo"\] - the number component of the
    current Parliamentary session
  - //TLCConcept\[@eId="varBillYear"\] - the year the bill was
    introduced expressed as a four digit number
  - //TLCConcept\[@eId="varSession"\] - the full session -
    @showAs="Session \#varSessionNo (\#varBillYear)"
  - //TLCConcept\[@eId="varPassedDate"\] - once passed, the date the
    Bill/Act passed (@showAs is an ISO 8601 format date with no time
    component)
  - //TLCConcept\[@eId="varAssentDate"\] - once assented to, the date of
    Assent (@showAs is an ISO 8601 format date with no time component)
  - //TLCConcept\[@eId="varActNo"\] - once assented to, the Act number
    (a positive integer)
  - //TLCConcept\[@eId="varISBN"\] - once published, the assigned ISBN
    (note this will change when the Bill becomes an Act)
  - //TLCPerson\[@eId="varIntroducingMember"\] - the Member who
    introduced the Bill (@showAs is a name although it could be an ID in
    an ontology in the future)
  - //TLCPerson\[@eId="varSupportingMembers"\] - a list of Members who
    supported the Bill (@showAs is a comma separated list of names)
  - //TLCConcept\[@eId="varDocType"\] - the type of document - fixed as
    @showAs="bsp" for Bills, @showAs="asp" for Acts
  - //TLCProcess\[@eId="varSystem"\] - the system to which this document
    belongs - fixed as @showAs="LDAPP"
  - //TLCOrganization\[@eId="varAuthor"\] - the author of this document
    - fixed as @showAs="Scottish Parliament"
  - //TLCLocation\[@eId="varJurisdiction"\] - the jurisdiction to which
    this document will or does apply - fixed as @showAs="Scotland"
  - //TLCConcept\[@eId="varOntologies"\] - the ontology to which all of
    these variables belong - fixed as
    @showAs="<https://www.legislation.gov.uk/ontologies/UK-AKN>"

### UK Bill/Act variables

The following table shows variables for Scottish Bills, an example value
based on b35s4 (Criminal Justice (Scotland) Bill), the equivalent value
for ukpubb/58-01/00001 (European Union (withdrawal) Bill) and some
comments.

|                        |                                                                                                                                  |                                                                                                                                   |                                                                                                                                                                                                     |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Variable Name**      | **Value in Scottish eg**                                                                                                         | **Value in UK eg**                                                                                                                | **Comments**                                                                                                                                                                                        |
| \#varDocType           | "SP Bill"                                                                                                                        | "Bill"                                                                                                                            | Appears bottom left front page of Bill                                                                                                                                                              |
| \#varAuthor            | "Scottish Parliament"                                                                                                            | "UK Parliament"                                                                                                                   | Copyright note?                                                                                                                                                                                     |
| \#varJurisdiction      | "Scotland"                                                                                                                       | "United Kingdom"                                                                                                                  | Required                                                                                                                                                                                            |
| \#varDocSubType        | "Government Bill"                                                                                                                | "Government Bill"                                                                                                                 | What are the other possible values?                                                                                                                                                                 |
| \#varBillTitle         | "Criminal Justice (Scotland) Bill"                                                                                               | "European Union (Withdrawal) Bill"                                                                                                | Obviously different for each Bill                                                                                                                                                                   |
| \#varStageVersion      | "Pre-Introduction" or "As Introduced" or "As amended at Stage 2/3"                                                               | Variants on this theme                                                                                                            | What are the other likely values?                                                                                                                                                                   |
| \#varShortStageVersion | "introd" or "stage2" or "stage3"                                                                                                 | Variants on this theme                                                                                                            | What are the likely values?                                                                                                                                                                         |
| \#varProjectId         | "sppubb/65155"                                                                                                                   | "ukpubb/20001"                                                                                                                    | Use //bill@name followed by no assigned by the system starting at 1 (5 digit zero padded)                                                                                                           |
| \#varWork              | See [above](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_metadata-elements#human_readable_uri_s_identifiers) | See [above](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_metadata-elements#human_readable_uri_s_identifiers)  |                                                                                                                                                                                                     |
| \#varWorkURI           | "\#varWork"                                                                                                                      | "\#varWork"                                                                                                                       |                                                                                                                                                                                                     |
| \#varCHOiid            | System assigned                                                                                                                  | System assigned                                                                                                                   | The OIID of the Configuration History object within TTfL                                                                                                                                            |
| \#varExpression        | "\#varWork@\#varShortStageVersion"                                                                                               | "\#varWork@\#varShortStageVersion"                                                                                                |                                                                                                                                                                                                     |
| \#varExpressionUri     | "\#varExpression"                                                                                                                | "\#varExpression"                                                                                                                 |                                                                                                                                                                                                     |
| \#varVDOiid            | System assigned                                                                                                                  | System assigned                                                                                                                   | The OIID of the Version Description object within TTfL                                                                                                                                              |
| \#varManifestation     | "\#varExpression/akn-xml"                                                                                                        | "\#varExpression/akn-xml"                                                                                                         |                                                                                                                                                                                                     |
| \#varManifestationUri  | "\#varManifestation"                                                                                                             | "\#varManifestation"                                                                                                              |                                                                                                                                                                                                     |
| \#varActYear           | 2013                                                                                                                             | 2020                                                                                                                              | A four digit calendar year which is the likely year for this Bill to become an Act (if it hasn't already)                                                                                           |
| \#varActTitle          | "Criminal Justice (Scotland) Act 2013"                                                                                           | "European Union (Withdrawal Agreement) Act 2020"                                                                                  | The likely short title of the resulting Act (initially calculated from \#varBillTitle and \#varActYear)                                                                                             |
| \#varIntroDate         | "2013-06-20"                                                                                                                     | "2019-12-09"                                                                                                                      | Once introduced, the date of introduction (@showAs is an ISO 8601 format date with no time component)                                                                                               |
| \#varIntroducingMember | "Kenny MacAskill"                                                                                                                | "Secretary David Davis"                                                                                                           |                                                                                                                                                                                                     |
| \#varSupportingMembers | ""                                                                                                                               | "The Prime Minister, The Chancellor of the Exchequer, Secretary Damian Green, Secretary Boris Johnson, Secretary David Lidington" | Comma separated list of supporters                                                                                                                                                                  |
| \#varBillNoComp        | "35"                                                                                                                             | "5"                                                                                                                               | Once introduced, for SP the Bill number component within the current session, for UK this number changes with each version (a positive integer) so need to add aliases for multiple retrieval paths |
| \#varBillNo            | "SP Bill 35"                                                                                                                     | "Bill 5" or "HL Bill 79"                                                                                                          |                                                                                                                                                                                                     |
| \#varParliamentNo      | N/A                                                                                                                              | "57"                                                                                                                              | No of Parliaments since creation of the United Kingdom                                                                                                                                              |
| \#varSessionNo         | "4"                                                                                                                              | "1"                                                                                                                               | Sessions are typically 12-18 months in UK Parliament                                                                                                                                                |
| \#varBillYear          | "2013"                                                                                                                           | "2019"                                                                                                                            | The year the bill was introduced expressed as a four digit number                                                                                                                                   |
| \#varSession           | "Session \#varSessionNo (\#varBillYear)"                                                                                         | "\#varParliamentNo/\#varSessionNo"                                                                                                | Bottom right side of the Bill cover page                                                                                                                                                            |
| \#varPassedDate        | "2015-12-08"                                                                                                                     | "2020-01-22"                                                                                                                      | Once passed, the date the Bill/Act passed (@showAs is an ISO 8601 format date with no time component)                                                                                               |
| \#varAssentDate        | "2016-01-13"                                                                                                                     | "2020-01-23"                                                                                                                      | Once assented to, the date of Assent (@showAs is an ISO 8601 format date with no time component)                                                                                                    |
| \#varActNoComp         | "1"                                                                                                                              | "1"                                                                                                                               | Once assented to, the numeric component of the Act number                                                                                                                                           |
| \#varActNo             | "asp 1"                                                                                                                          | "Chapter 1"                                                                                                                       | The Act number including the preceding text "Chapter" or "asp"                                                                                                                                      |
| \#varISBN              | "978-1-78351-441-0"                                                                                                              | "???"                                                                                                                             | Is this used by UK Parliament?                                                                                                                                                                      |

### Statutory Instrument variables

The variables for SSIs/SIs are:

  - //TLCConcept\[@eId="varDocSubType"\] - the type of subdocument this
    is (one of ...)
  - //TLCConcept\[@eId="varSITitle"\] - the title of the SI/SSI
  - //TLCConcept\[@eId="ProcedureType"\] - the type of procedure
    applicable to the creation of this SI/SSI (on of ...)
  - //TLCProcess\[@eId="varStageVersion"\] - the stage version of this
    particular version of the SI/SSI (initially "Internal Draft")
  - //TLCProcess\[@eId="varProjectId"\] - the identifier of the Project
    to which this SI/SSI belongs
  - //TLCProcess\[@eId="varWork"\] - a URI for the FRBR Work (or TTfL
    Configuration History) to which this SI/SSI version belongs
  - //TLCProcess\[@eId="varWorkURI"\] - currently identical to \#varWork
  - //TLCProcess\[@eId="varCHOiid"\] - the OIID of the Configuration
    History object within TeraText for Legislation
  - //TLCProcess\[@eId="varExpression"\] - a URI for the FRBR Expression
    (or TTfL Version Description) of this version of the SI/SSI
  - //TLCProcess\[@eId="varExpressionUri"\] - currently identical to
    \#varExpression
  - //TLCProcess\[@eId="varVDOiid"\] - the OIID of the Version
    Description object within TeraText for Legislation
  - //TLCProcess\[@eId="varManifestation"\] - a URI for the FRBR
    Manifestation (or TTfL Rendition) of this version of the SI/SSI -
    typically the AKN manifestation/rendition
  - //TLCProcess\[@eId="varManifestationExpressionUri"\] currently
    identical to \#varManifestation
  - //TLCConcept\[@eId="varSIYear"\] - a four digit calendar year which
    is the likely year for this Draft SI/SSI to become an SI/SSI (if it
    hasn't already)
  - //TLCConcept\[eId="varMadeDate"\] - once made, the date of making
    (@showAs is an ISO 8601 format date with an optional time component)
  - //TLCConcept\[eId="varLaidDate"\] - once laid before Parliament, the
    date of being laid (@showAs is an ISO 8601 format date with a (rare)
    optional time component)
  - //TLCConcept\[eId="varCommenceDate"\] - once commenced or at least
    the commencement date is determined, the date of coming into force
    (@showAs is an ISO 8601 format date with an optional time component)
  - //TLCConcept\[@eId="varSINoComp"\] - once made, the SI/SSI number
    component within the current year (a positive integer)
  - //TLCConcept\[@eId="varSINo"\] - the full SI/SSI number -
    @showAs="S.I. \#varSIYear/\#varSINoComp"
  - //TLCConcept\[@eId="varISBN"\] - once published, the assigned ISBN
    (note this will change when the Bill becomes an Act)
  - //TLCOrganization\[@eId="varMinistryAgency"\] - the Ministry or
    agency making this SI/SSI
  - //TLCConcept\[@eId="varDocType"\] - the type of document - fixed as
    @showAs="SSI" or @showAs="UKSI" for Acts
  - //TLCProcess\[@eId="varSystem"\] - the system to which this document
    belongs - fixed as @showAs="LDAPP"
  - //TLCOrganization\[@eId="varAuthor"\] - the author of this document
    - fixed as @showAs="Scottish Government" or @showAs="UK Government"
  - //TLCLocation\[@eId="varJurisdiction"\] - the jurisdiction to which
    this document will or does apply - fixed as @showAs="Scotland" or
    @showAs="UK"
  - //TLCConcept\[@eId="varOntologies"\] - the ontology to which all of
    these variables belong - fixed as
    @showAs="<https://www.legislation.gov.uk/ontologies/UK-AKN>"

Where //date elements reference a variable that is a date, the following
formatting attributes are used:

  - <span class="underline">TO DO</span>

References to these variables will use //ref elements with
@class="placeholder" and @style using the [Java SimpleDate input
format](https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html)
to determine how the date is rendered.

### Example documents and where they depart from this

In my example Scottish Bills I have used:

``` 
  <TLCProcess eId="varWork" href="#varOntologies" showAs="https://www.parliament.scot/parliamentarybusiness/Bills/65155"/>
  <TLCProcess eId="varWorkURI" href="#varOntologies" showAs="https://www.parliament.scot/parliamentarybusiness/Bills/65155"/>
  <TLCProcess eId="varExpression" href="#varOntologies" showAs="https://www.parliament.scot/parliamentarybusiness/Bills/65155@introd"/>
  <TLCProcess eId="varExpressionUri" href="#varOntologies" showAs="https://www.parliament.scot/parliamentarybusiness/Bills/65155@introd"/>
  <TLCProcess eId="varManifestation" href="#varOntologies" showAs="https://www.parliament.scot/parliamentarybusiness/Bills/65155@introd/data.akn"/>
  <TLCProcess eId="varManifestationExpressionUri" href="#varOntologies" showAs="https://www.parliament.scot/parliamentarybusiness/Bills/65155@introd/data.akn"/>
```

Note that this approach:

``` 
 * assumes that FRBRuri and FRBRthis are identical, 
 * it adopts the Scottish Parliament's scheme for identifying a Bill project (just a 5 digit number)
 * currently does not contain a document identifier within that project (assumes incorrectly a one to one correspondence)
 * currently uses "introd" as a label (borrowing loosely from the Scottish Parliament website PDF file naming conventions)
   * while we might support the release versions such as "introd", "stage2", "stage3" this way, we would still need a more traditional version label for intermediate draft versions between each of those, and used the legislation.gov.uk mechanism for distinguishing format (I think a 3-4 letter extension like Microsoft's file system is probably okay particularly if we use existing known extensions - is "xml" too general or should we use "akn" for Akoma Ntoso allowing us to use "xml" for Crown Legislation Markup Language - although to be consistent we should probably use "clml" or "cml").
```
