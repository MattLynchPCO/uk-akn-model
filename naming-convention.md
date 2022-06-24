# Element and attribute naming conventions

AKN provides a template approach where particular named elements such as
//section or //part map on to //hcontainer\[@name="section"\] and
//hcontainer\[@name="part"\] respectively. Philosophically, AKN requires
you to use in the @name attribute the normal name you would use to
reference that element. This is generally fine as the context or even
the name alone can usually determine the formatting and structural place
of the element. However, there are some exceptions.

## Case for element and attribute names

AKN consistently uses camel-case with an initial lower case for all
names whether element, attribute, group, attributeGroup or complexType.
This is also consistent with the naming of elements and attributes
within the XSD Schema. We will therefore continue this tradition.

The exception is for included namespaces from other XML vocabularies
including MathML and possibly XHTML and CLML (the latter primarily for
metadata).

## //act and //bill

All primary and subordinate legislation in as made, or in force form,
whether Acts, Statutory Rules, Statutory Instruments, Orders-in-Council,
Ministerial Directions or Ministerial Orders have the document level
element //act. According to the schema, this is the same as
//container\[@name="act"\]. We note that @name is allowed on an //act
and typically provides further qualification of the document types (many
of which are demonstrably NOT Acts of Parliament). It is not clear in
AKN whether //act@name overrides the //container@name or sits in a
separate namespace. There is also a //bill element. We see no reason to
depart from the current TNA practice to use //act in the current way.

Since draft statutory instruments and orders, particularly in the UK
where some SIs are tabled in draft form, may be published as drafts, we
propose to use //bill for draft SIs/SSIs and other subordinate
legislation including when drafts are tabled in Parliament. Conversion
from //bill to //act will happen, as with Acts of Parliament, when the
instrument is being prepared for publication "as made" (i.e. in it's
final, as law form).

## //hcontainer v //container v //block general principals

AKN generally uses //container for whole documents, //hcontainer for
hierarchical pure content elements that represent a hierarchical
structure within the document, and //block to contain mixed content
displayed in Western European tradition as vertical blocks on a page.
Therefore most named or referenceable elements in an Act or subordinate
legislation map to //hcontainer.

We note also that AKN normally treats //*name* where defined as
equivalent to //hcontainer\[@name="*name*"\] (occasionally
//container\[@name="*name*"\]) so we should not use these different
serializations to distinguish between two different uses.

AKN creates a number of specific named elements. Some of the names we
would use are already available and some are not (e.g. there is a //rule
but no //regulation, //definition, //schedule, //subsubparagraph -
noting there is a //subparagraph but not //sub-paragraph). Although some
extension of the AKN namespace has been necessary to introduce
additional attributes, we have adopted elements that are native AKN
compliant rather than extending the AKN element namespace to avoid
unnecessary translation and maximise the chance that any particular
instance will validate against a standard AKN schema.

In particular we use the following:

  - //hcontainer\[@name="schedule"\] (rather than introducing a non-AKN
    //schedule),
  - //hcontainer\[@name="definition"\] (rather than introducing a
    non-AKN //definition),
  - //hcontainer\[@name="subsubparagraph"\] (rather than introducing a
    non-AKN //subsubparagraph) \[Noting that UK and Scottish parliaments
    use "sub-paragraph" and "sub-sub-paragraph" but there is already a
    //subparagraph in AKN.\],
  - //hcontainer\[@name="regulation"\] (rather than non-AKN
    //regulation),

We note that, where an element has a normal name, that name should be
used (whether in the //*name* form or the //hcontainer\[@name="*name*"\]
form). Where there is no name, //level should be used for //hcontainer
equivalents, and //p should be used for //block equivalents.

## Lists v paragraphing

AKN provides a number of different constructs for numbered and
unnumbered lists including //blockList, //ul and //ol. These can be
single level or nested. We avoid completely using the borrowed HTML
constructs of //ul and //ol. We use //blockList in the //body and also
in front matter and tail matter for bulleted lists (//num should have
the value of the bullet or dash used), unnumbered lists (formatted
basically the same as a bulletted list but without a bullet present) and
numbered lists that are not like standard English paragraphing
constructs (ie. 1., 2. , 3. but not (a), (b), (c)).

While AKN anticipates English-style paragraphing be marked up using
nested //blockList elements, although some naming conventions apply they
are not consistent across all different document types and even within
collections of the same document type. Because we wish to allow
//hcontainer within the paragraphs (specifically for definitions but
potentially other constructs) we have adopted the use of //level as an
unnamed //hcontainer and reserve //paragraph and //subparagraph for
constructs that look more like sections or subsections but have that
name because of their context (typically in a schedule or SI/SSI).

These //hcontainer templates are not permitted within //preface,
//preamble and //conclusions but English-style paragraphing occurs often
in these contexts also. We will therefore use
//blockContainer\[@class="..."\] where we would in the body use //level.
These //blockContainer's can nest. For example:

``` 
  <blockContainer class="para1" eId="backCover__explNote__para_e" GUID="_78724833-d43d-4361-b54b-8273b7e5c953">
   <num>(e)</num>
   <intro>
    <p>amending Part 61 (Admiralty Claims), in order to, amongst other matters&#8212;</p>
   </intro>
   <blockContainer class="para2" eId="backCover__explNote__para_e__subpara_i" GUID="_1ff5829f-05c5-4ad5-9b6c-7d224ee16236">
    <num>(i)</num>
    <p>address the lacuna in the present rules highlighted by <i>The Atlantik Confidence [2014] 1 Lloyd&#8217;s Rep 1 586</i>, by creating a mechanism for limitation funds to be constituted by providing security as well as, or in addition to, paying money into court; and</p>
   </blockContainer>
   <blockContainer class="para2" eId="backCover__explNote__para_e__subpara_ii" GUID="_3be33c3f-1ac2-4c6b-ac4e-fbf11e681754">
    <num>(ii)</num>
    <p>make miscellaneous changes proposed by the Admiralty Court Users Committee, including the addition of definitions of both &#8220;Admiralty Judge&#8221; and &#8220;Admiralty Registrar&#8221;, as well as including reference to claims &#8220;in personam&#8221;, as opposed to what were previously termed &#8220;other claims&#8221;, to correspond with the statutory language used in the Senior Courts Act <ref href="http://www.legislation.gov.uk/id/ukpga/1981/54">1981 (c.54)</ref>, and to reform the rules as to costs in collision claims where a party at trial equals or betters certain offers made by them.</p>
   </blockContainer>
  </blockContainer>
```

## "section" and similar constructs

The structural function (and formatting for the large part) of a rule,
regulation, by-law, article or paragraph in a Statutory Instrument or
clause in a Bill is pretty much identical to that for a //section in an
Act. However, these are variously //section in an Act, //rule in Rules,
//hcontainer\[@name="regulation"\] in Regulations, //article (or
//paragraph) in an Order. Currently, UK Bills use //section despite the
fact that external references to these elements call them "clauses".
Within the Bill itself, reference wording uses "section" reflecting the
fact that, once enacted, that is what it will be called. We therefore
wholly support the use of //section within Bills.

Also sections (and their equivalents in subordinate legislation) are
structurally unique and not like other //hcontainer elements which
nearly always group sections (I suspect this is largely because the
European equivalent //article is formatted much more like //part than it
is like //section) but don’t restart numbering (again unlike //article
in European legislation). Likewise all other elements that typically
appear within a section or equivalent such as //subsection, //paragraph,
and possibly //list, //sublist, //item (no //subitem?) are structurally
different to grouping elements (e.g. //part, //chapter, and //order - UK
does not seem to use //subpart, //division, or //subdivision unlike
other Commonwealth jurisdictions or //title and //subtitle used in
addition to all the others in the US). The lower level elements have
distinct formatting patterns including nested indentation not normally
seen in the grouping elements above the //section level. These grouping
elements historically have a centred number (e.g. "Part 1") with a
centred heading immediately below (increasingly they are centred with
the number and heading on the same line separated by a dash or left
aligned separated by a tab) and group sections (or their equivalent).

We note also that Articles are likely to appear in schedules containing
treaties, European legislation and some agreements. They will not be
formatted like //section in that context and
//hcontainer\[@name="article"\] is supposed to be logically equivalent
to //article whether in //body//article or
//hcontainer\[@name="schedule"\]//article.

To complicate matters further "section" is sometimes a grouping
construct within a schedule or possibly the body of an SI with
formatting more like a //part or //chapter.

There are four potential solutions for this:

1.   use the referenceable name regardless of context and use the
    existing @class attribute (or add a new attribute) to drive
    formatting (and conversion to CLML);
2.   use //section in Acts, Bills and SIs and add a @name attribute to
    guide the reference wording - note that in the UK unlike many
    English-speaking jurisdictions, the formatting and content model for
    section-like elements in Statutory Instruments is slightly different
    so formatting rules will require context and introduce a new element
    or elements for the grouping use of section (e.g. //si-section,
    //sched-section, //group-section);
3.   use //section within an Act or Bill but use //si-section with an
    appropriate @name attribute in Statutory Instruments so there is a
    simple element-driven rule for formatting (this would also require
    another element for the grouping use of section as above); or
4.   use //section in Act and Bill, //rule, //regulation, //si-article
    and //si-paragraph (or similar) so that the formatting of a body
    paragraph can be distinguished from lower level paragraph beginning
    with (a).

As we believe the first option to be most consistent with AKN and it
allows for relatively efficient formatting and simpler stylesheets, we
are adopting the first approach.

A [proposal for the different @class values](type) appears separately.

## "paragraph"

Paragraph is particularly problematic as, depending on the context, the
referencable object called a paragraph can appear at different
structural levels. In some Statutory Instruments, it is the logical
equivalent of //section (although slightly different in formatting and
content rules). Also in a Schedule, paragraph looks more like a
//section in the body of an Act. If a paragraph numbered (a) appears
within a schedule paragraph that looks more like a section, there is
some disagreement as to whether it is a sub-paragraph, a paragraph, or
(if also within a subsection-like context) a sub-sub-paragraph.

Similar issues then present themselves for disambiguating the different
usages of the name "paragraph" to that of "section" and similar looking
constructs.

Because we cannot rely on the name being used consistently, we adopt
//level as an unnamed //hcontainer and use the @class element as
described above.

Given that the named element //subparagraph exists in AKN, we will use
it rather than creating a new //hcontainer\[@name="sub-paragraph"\] and
by analogy use //hcontainer\[@name="subsubparagraph"\] and
//hcontainer\[@name="subsubsubparagraph"\] if nested equivalent are
required.

## "formula"

The AKN element //formula looks like it is intended for the enacting
words or similar. However the name "formula" in UK legislation is always
used to refer to some kind of mathematical equation. The recommended
solution for mathematical equations is to use //foreign to wrap MathML
(see section 5.14 of the [AKN Core Version 1.0 Part 1
Vocabulary](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/akn-core-v1.0-part1-vocabulary.html)).
This doesn't support inline equations as //foreign is a block element.

This doesn't really allow us to identify something as a formula with
just an image where legacy data hasn't been converted.

For normal block mathematical formulas we will use a new
//tblock\[@name="formula"\] which supports either an //img or //foreign
or both.

The //subFlow element (or a similar construct) will need to be used to
code inline formulas (//tblock\[@name="formula"\]) as inline formulas
will still need image alternatives.

Note also that //math (from MathML not AKN) has the following attributes
which are also relevant to these issues:

  - @display="block|inline" to distinguish whether the formula should be
    inline with text or a separate block;
  - @altimg="<span class="underline">URI</span>" to point to an
    alternative image for the formula (and @altimg-width, @altimg-height
    and @altimg-valign for controlling the display of that image)

## Paragraphing and list elements

The English tradition of paragraphing is far less common in European
jurisdictions and AKN often uses //list or equivalent HTML //ol or //ul
for similar nesting constructs to those that are central to the English
legislative drafting tradition. These constructs have particular names
in the English tradition. In the UK, the tradition is to use
"paragraph", "sub-paragraph", "sub-sub-paragraph", etc., but "paragraph"
is used for elements with @class="para1" or @class="prov2" or
@class="schProv1" and occassionally even prov1 and schProv1. While other
Commonwealth jurisdictions use of the "-" varies (and Canada uses much
more consistent "paragraph", "subparagraph", "clause", "subclause",
"item", "subitem"), because the naming is inconsistent in the UK it was
thought best to use consistent element names //level (the unnamed
hierarchical element) and use the @class attribute to determine
formatting and context rules. Unlike the European tradition that uses
unnamed and highly variant list structures, these elements are
hierarchical and we reserve the use of //list for true lists that aren't
otherwise named hierarchical structures and completely avoid the
redundant //ol and //ul HTML elements.

## //num and //heading elements

All //num elements should contain the number as it appears on the page
including brackets, element name, and any punctuation characters if
present (this is consistent with the examples provided in the AKN
standard). For instance for Part 5 the //num element should contain
"Part 5" not just "5". For subsection 5(1), the //num element should
contain "(1)" (the parent //section element would contain "5" (or "5."
if legacy style)). The case of the name component should be mixed case
e.g. "Part" not "PART", "Chapter" not "CHAPTER".

To manage re-numbering, we introduce a new optional attribute
@ukl:renumber="yes|no" (with "yes" as the default value). See [LDAPP
extensions to AKN](LDAPP-extensions).

## //eop and //eol elements

LDAPP requires the creation and application of amendment wording that
makes use of line and page numbers. Therefore we make use of the native
AKN elements for marking up end of page (//eop) and end of line (//eol)
and the native @number, @breakAt and @breakWith attributes (see
[section 5.6 of the AKN
standard](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html#_Toc523925049)).
We are likely to use within the system processing instructions and turn
these into //eop and //eol elements on export.

## Subheadings

The //subheading element is a //block element in AKN intended to be used
to supplement the //heading element (typically immediately after it).

However, subheadings in UK legislation appear below the section (or
equivalent) level, sometimes grouping subsections, paragraphs and
subparagraphs, etc (see section 2 in the [National Insurance
Contributions
Act 2014](http://www.legislation.gov.uk/ukpga/2014/7/pdfs/ukpga_20140007_en.pdf))
and sometimes despite identical formatting they are really headings to a
particular subsection, paragraph, sub-paragraph etc (see section 3 in
the [Modern Slavery
Act 2015](http://www.legislation.gov.uk/ukpga/2015/30/pdfs/ukpga_20150030_en.pdf)).
We adopt a pragmatic approach to these choosing to use
//subsection|level/heading regardless of whether the heading applies to
a single subsection (or lower) or a group of them. This avoids any
confusion with the //subheading element in AKN (which may be used for
some schedules or EU legislation but is unlikely to be used in the main
body of UK legislation).
