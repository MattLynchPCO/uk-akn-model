# Schedule elements

These elements are those specific to schedules. A number of elements
used elsewhere are reused within schedules. Their entries here are
specific to their usage within schedules.

## //hcontainer\[@name="schedules"\]

All schedules (and similar constructs with different names if they exist
such as appendices, annexes, etc.) will appear within //body after any
signature block (if present) and within an
//hcontainer\[@name="schedules"\]. The optional
//hcontainer\[@name="schedules"\]/heading element will only be present
in UK Bills and SIs and then only if there are multiple schedules (as
children of the //hcontainer\[@name="schedules"\] element). Normally,
the content of //hcontainer\[@name="schedules"\]/heading will be
"Schedules" if present.

Note that, although English references will distinguish between
provisions in the body and provisions within the schedule, the AKN usage
of body is more broad and all content with legal effect is supposed to
be in the body. The other obvious alternative, //attachments presumes
the contents are whole separate documents which, in many cases schedules
are not. We therefore place //hctonainer\[@name="schedules"\] within the
//body element.

See [Oasis AKN documentation for *hcontainer\]\] (see also
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_body.html|Oasis
AKN documentation for *body\]\] and
\[\[http:*docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs\_xsd\_Element\_attachments.html|Oasis
AKN documentation for
//attachments](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html)).

## //hcontainer\[@name="schedule"\]

Despite being quite common in English-speaking jurisdictions, there is
no //schedule element defined in standard AKN so introduce a new named
//hcontainer.

Schedules, like the body can contain grouping elements like part,
chapter, crossheading and subheading but normally the section-like
elements within schedules are referred to as paragraphs.

See [Oasis AKN documentation for
//hcontainer](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html)

## //part

Within a schedule, a //part will normally be @class="schGroup2".

See [grouping
elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_grouping-elements)

## //chapter

Within a schedule, a //chapter will normally be @class="schGroup3".

See [grouping
elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_grouping-elements)

## //hcontainer\[@name="crossheading"\]

Within a schedule, a crossheading will normally be @class="schGroup4".

See [grouping
elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_grouping-elements)

## //hcontainer\[@name="subheading"\]

Within a schedule, a subheading will normally be @class="schGroup5".

See [grouping
elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_grouping-elements)

## //section\[@class="schGroup4"\]

While sections typically appear within the body of Bills and Acts (as
section-level elements with @class="prov1"), within schedules they are
more likely to be used as grouping elements with centred formatting like
other grouping elements. In this case, the //num often contains "Section
*no*", is centred and the //heading if any appears centred immediately
below it.

These elements can appear within schedule grouping elements including
//part and //chapter. They would normally contain either
//paragraph\[@class="schProv1"\] or cross headings.

See [Oasis AKN documentation for *section\]\]. Contrast with
\[\[https:*ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary\_section-elements|section-level
elements](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_section.html)

## //article\[@class="euStyleArticle"\]

While articles can appear within Orders (in SIs/SSIs) typically as
section-level elements, within schedules they are more likely to be
quoted from EU legislation or treaties. In this case, the //num often
contains "Article *no*", is centred and the //heading if any appears
centred immediately below it. These European-style articles have a
similar content to //section but distinctly different formatting. We
introduce this custom @class value to distinguish this type of article
from the more often found form in Orders.

These elements can appear within schedule grouping elements including
//part, //chapter, //section, and cross heading.

See [Oasis AKN documentation for *article\]\] and
\[\[https:*ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary\_grouping-elements|grouping
elements](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_article.html).
Contrast with [section-level
elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_section-elements)

## //paragraph" and @class="schProv1"\]

As we are avoiding the use of //paragraph because of the ambiguity of
whether UK users use "paragraph" or "sub-paragraph" depending on the
context, we use the paragraph element for what looks a little like a
//section but within a schedule. For a more normal paragraph (typically
starting number of "(a)") we use //level\[@class="para1"\] anywhere in a
Schedule (as in the body).

What are commonly referred to as schedule paragraphs are
@class="schProv1" and have a //num preceded by an optional //heading.
Care should be taken to distinguish between headings that group schedule
paragraphs (use //hcontainer\[@name="subheading"\]) and headings that
apply to exactly one schedule paragraph.

See [Oasis AKN documentation for *hcontainer\]\] and
\[\[https:*ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary\_section-elements|section-level
elements](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_paragraph.html)

## //subparagraph" and @class="schProv2"\]

Consistent with using //paragraph for schedule paragraphs, although UK
tends to use "sub-paragraph" rather than "subparagraph", because there
is already an AKN element, //subparagraph, that seems the most
appropriate for a schedule sub-paragraph (what looks a little like a
//subsection but within a schedule paragraph). For something that looks
more like a paragraph in the body of an Act typically starting with
"(a)" or "(i)", we adopt //level\[@class="para1"\] given the ambiguity
in the UK of whether these are paragraph or sub-paragraph depending on
the context.

What are commonly referred to as schedule sub-paragraphs are
@class="schProv2" and have a //num preceded by an optional //heading
(the heading is rare).

See [Oasis AKN documentation for *hcontainer\]\] and
\[\[https:*ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary\_section-elements|section-level
elements](http://docs.oasis-open.org/legaldocml/akn-core/v1.0/csd02/part2-specs/materials/akn-core-v1.0-csd02-part2-specs_xsd_Element_hcontainer.html)
