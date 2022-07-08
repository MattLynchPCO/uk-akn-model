# Miscellaneous other block elements

These elements can appear in numerous different contexts most commonly
at or below the //section level. They tend to be more widely used within
schedules.

This list is incomplete but will be augmented as we discover new
constructs that need to be supported in the authoring environment.

## //content

Typical //hcontainers use //content to wrap content after the //num and
//heading which has no further structure (particularly since we don't
intend to use //blocklist). This element is redundant but required for
AKN compliance. It turns into //intro if a //paragraph (or whatever
equivalent structure is appropriate within the parent element) is
inserted after it.

See [Oasis documentation for
//content](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_content.html).

## //intro

Normally referred to as "opening words", typically below the section
level and preceding a sequence of //paragraph elements or their logical
equivalent at the relevant level.

The //intro element can precede other types of elements including
definitions, mathematical formulas, quoted structures, tables, and
forms.

See [Oasis documentation for
//intro](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_intro.html).

## //wrapUp

Normally referred to as "closing words", typically below the section
level and following the last sequence of //paragraph elements or their
logical equivalent at the relevant level.

See [Oasis documentation for
//wrapUp](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_wrapUp.html).

## //hcontainer\[@name="sandwich"\]

Rarely used in new text but present in legacy documents, typically
between two sequences of //paragraph elements or their logical
equivalent at the relevant level. We would prefer to have an equivalent
of //intro and //wrapUp like //sandwich or at least to use
//block\[@name="sandwich"\] however AKN does not allow either in this
context. The numbering of following paragraphs or their equivalent
should continue and not restart after sandwich text (to guarantee
uniqueness of the @eId amongst other things).

See [Oasis documentation for
//hcontainer](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html).

## //hcontainer\[@name="step"\] (Step)

AKN has a //step element but it was intended as a "metadata element
specifying facts about a workflow step occurred to the document
\[sic\]". UK legislation has blocks marked as "Step
<span class="underline">N</span>" occurring within a section, subsection
or equivalent (for examples see s 27 of [|Land Transaction Tax and
Anti-avoidance of Devolved Taxes (Wales) Act
2017](http://www.legislation.gov.uk/anaw/2017/1/pdfs/anaw_20170001_en.pdf)).
These can also have within them paragraphs and other structures (see
amendment 116 inserted s 3AC in [|Amendments to Planning (Scotland)
Bill](http://www.parliament.scot/S5_Bills/Planning%20\(Scotland\)%20Bill/SPBill23MLS052018.pdf))
so should properly be an //hcontainer.

We will therefore use //hcontainer\[@name="step" and @class="step"\].
The content of the //num child will be in the form "Step 1" etc. and the
//heading would be optional and not present for any of the above
examples.

Note that @class="step" can be used for any similarly formatted or
structured construct with a different @name value and //num contents as
appropriate.

See [Oasis documentation for
//hcontainer](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html).

## //tblock (wrapper for forms, tables, images, oaths, etc)

Since forms, tables, mathematical formulas and images can optionally be
preceded by a name, number and heading, a similar approach should be
used for each of them.

Where a //num and/or //heading is required, the //tblock can be used.
Otherwise a simple //block may suffice. The @name attribute should be
set to "form", "formula", "table", "map", "diagram" or similar to
reflect what reference wording would be used to refer to that item.

Note that //tblock can't take a @name so we use the @class attribute as
a default name.

Note also that documents that contain colour images require special
printing requirements. This is essentially a document property driven by
the nature of the included images. We presume this will be managed as a
workflow or document property.

The following table describes the content of the relevant //block or
//tblock for each case:

|                                                   |                                                                                                                                                                                    |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **tblock@class**                                  | **Content**                                                                                                                                                                        |
| table                                             | //foreign/table (note //tblock/heading should be used not //table/caption)                                                                                                         |
| form                                              | //foreign/table or one or more //img (note the //fillIn element)                                                                                                                   |
| formula                                           | An //img or //foreign/math (note that the //math@altimg provides a way of embedding a reference to an image as an alternative to rendering the MathML)                             |
| image (including alternatives map, diagram, etc.) | One or more //img elements. Note that the @class will always be "image" but may also contain space separate values after the initial "image" to further identify the type of image |
| oath or affirmation                               | //embeddedStructure                                                                                                                                                                |
| para1                                             | //num and //p or //tblock\[@class="para2"\]                                                                                                                                        |
| para2                                             | //num and //p or //tblock\[@class="para3"\]                                                                                                                                        |

See [Oasis documentation for
//tblock](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_tblock.html).

## //block

The //block element can be used for named constructs that do not have a
//num or //heading (for which //tblock is the more appropriate element).
A number of examples appear in the //coverPage and //conclusions.

Note that there are specific @name values for //block documented
elsewhere in this model in the context we expect them to appear (mostly
cover page, back page and other contexts outside of the main legislative
body.

See [Oasis documentation for *block\]\] and the discussion on the use of
//block for
\[\[https:*ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary\_front-matter-elements|front
matter](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_block.html)
and [tail
matter](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_tail-matter-elements)
elements.

## Unnumbered lists (//hcontainer\[@name="unnumberedItem"\])

AKN provides a number of different constructs for nested list
structures. These include //blockList and the borrowed HTML //ol and
//ul. Unlike the European tradition, where nested numbered and
unnumbered structures are irregular and lack standard naming
conventions, English legislation tends to prefer the "paragraphing"
tradition with distinct names and numbering schemes for items at every
level (subsection, paragraph, subparagraph, etc). In general, where a
named element exists, we prefer to use the named element (or an
//hcontainer with appropriate @name).

For bulletted lists and unnumbered lists (these are indented unlike a
series of //p elements), we therefore propose to use
//hcontainer\[@name="unnumberedItem"\] with //num containing the
appropriate bullet character for that level or without a //num for truly
unnumbered list items. Therefore no distinct containing element (like
//blockList) is required. Since the formatting for these items will
mirror English paragraphing (even if the numbering conventions are not
mirrored), we propose to use the @class="para*N*" for these elements.

Note though, that there are a number of contexts outside the body of the
legislation that don't allow //hcontainer but do have bulleted lists or
more rarely paragraphing (e.g. SI/SSI explanatory notes, preambles,
amendment list prefaces). For both we use //blockContainer with
@class="para*N*". The //num should contain the bullet character for
bullet lists and the number including enclosing parentheses for numbered
lists and be absent if the list is an unnumbered list.

See [Oasis documentation for *hcontainer\]\] noting we are not proposing
to use
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_blockList.html|*blockList\]\],
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_ul.html|*ul\]\]
or
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_ol.html|//ol](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html).

NOTE: the current functionality in LEGI uses //blockList. This is the
proposed end state.

## //blockList, //item, //ol, //ul (not used)

It is not intended for //blockList and therefore //item or the HTML
borrowed list items, //ul and //ol to be used. Named structural elements
such as //paragraph, //subparagraph, or //hcontainer (or
//blockContainer if //hcontainer is not allowed) with a suitable @name
are to be preferred in all cases or //level where the name is not
consistent (e.g. English style paragraphing).

See [Oasis documentation for
//item](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_item.html).

## //table

The AKN table model is a stripped down version of HTML tables and, since
this means that display in most XML tools is inadequate, we use
//foreign/table with the HTML namespace for full HTML table
functionality. The native AKN //table will not be used at all.

See [Oasis documentation for
//table](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_table.html).

## //img

A single image without number or caption - normally this would be
contained within a //tblock with @name set to one of "diagram", "map",
"sign" or similar.

See [Oasis documentation for *img\]\] and
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_tblock.html|//tblock](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_img.html).

## //quotedStructure, //embeddedStructure and //mod

Quoted structures can be used in a variety of settings. The most common
is in amendment wording where they capture one or more whole elements to
be inserted. AKN distinguishes between quoted structures that are part
of an amendment (which appear within //mod/quotedStructure) and those
that don't (which appear within //embeddedStructure). Essentially, there
is no difference between these other than whether or not they are part
of amendment wording or not.

//embeddedStructure should be used for:

  - footnotes and other annotations to quote provisions in other
    documents that affect the interpretation of the current provision;
  - oaths, declarations, and affirmations.

//quotedStructure should be used for:

  - amendment wording that includes a quoted provision (either to be
    inserted, as a replacement or more rarely to determine the placement
    of an amendment).

Attributes on //quotedStructure (and presumably //embeddedStructure)
include:

  - @ukl:docName the @name attribute of the bill or act from which or
    into which the quoted element is being taken or inserted
  - @ukl:indent the indent level of the quoted element (so we can
    support nested structures, paragraphs in definitions, provisos,
    steps etc.) - one of indent0, indent1, indent2, indent3, indent4,
    indent5
  - @startQuote the quotation mark to use immediately before the first
    quoted element
  - @endQuote the quotation mark to use immediately after the last
    quoted element 

We propose to:

  - handle different indent levels in a single logical block of inserted
    elements by using multiple adjacent //quotedStructure elements with
    the first //quotedStructure@startQuote set and the last
    //quotedStructure@endQuote set and the others empty and each
    @ukl:indent set differently (it should be reliable to merge adjacent
    //quotedStructure elements with the same @ukl:indent value;
  - handle quoted elements that begin with an inline text using
    //quotedText with @startQuote set but @endQuote set to empty
    followed by //quotedStructure with @startQuote set to empty
  - handle text that has multiple //quotedStructure's separated by a
    block of text using a sequence of //p elements each with a single
    //quotedStructure inside a //mod per //p

As a consequence, any text in the //p appearing after the
//quotedStructure is appended to the last content descendant of the
//quotedStructure which preserves the logical interpretation of the
single //p

See [Oasis documentation for *quotedStructure\]\],
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_mod.html|*mod\]\],
and
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_embeddedStructure.html|//embeddedStructure](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_quotedStructure.html).

## Oaths (//embeddedStructure)

Legislation in the English tradition occasionally incorporates an oath
or affirmation to be sworn or made for particular offices or roles.
Typically these are quoted like //quotedStructure. Our intention is to
use a //tblock around these where they need a name (reference wording
will potentially refer to "the oath in ...") and, either way, to use
//embeddedStructure for their content.

## Notes and footnotes (//authorialNote, //note and //blockContainer\[@ukl:name="block"\])

The //note element appears to be specifically for the content of a
footnote (with standard reference markup used for the reference number
of a footnote) added editorially after the authoring process. If the
//note content doesn't appear within the fragment where it is
referenced, this may cause issues for fragmenting.

The //authorialNote, by contrast is inline. For footnotes in legislative
drafting, //authorialNote is more strictly appropriate as these notes
are part of the authored document and not an editorial gloss added later
(for which the //meta structures and //note was really designed). While
TNA may add //note elements in preparation for publishing (see for
instance the [Criminal Procedure
Rules 2015](https://www.legislation.gov.uk/uksi/2015/1490/contents/made?text=Note#match-1)),
LDAPP does not use //note for any material that forms part of the Bill,
Draft SI, or enacted Act or SI. Therefore the LDAPP authoring
environment does not need to cater for this element. Notes that appear
as content within the text will be marked up as //authorialNote or,
where they are formatted similar to Steps, as a standard named element.
We have used //blockContainer\[@name="note"\] and, to collect a group of
notes where required, //blockContainer\[@name="notes"\] as this can be
used either within the //body or elasewhere in the document where
//hcontainer is not permitted.

A footnote within the body of legislation will normally be drafted as
//authorialNote\[@placement="bottom"\].

A number of legislative documents have footnotes for chapter/Act
number/SI number information that would already inherently be part of
the information for a //ref link. As the footnotes can interfere with
matching patterns in the text, we prefer to insert these as part of the
tag cross-references process so that all the information can be managed
as a single insertion process.

See [Oasis documentation for *authorialNote\]\],
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_note.html|*note\]\],
and
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_ref.html|//ref](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_authorialNote.html).
