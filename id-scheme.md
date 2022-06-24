# Element ID Scheme and references

## Cross reference requirements

### Section-level elements and below

The most common cross-references are to section-level elements and
below. A reference to a section-level element typically does not refer
to any grouping elements that contain it. For example, ‘section 53’ is
quite common, and ‘section 53 of Chapter 3 of Part I’ is extremely rare.
Occasionally amendment wording will refer to the grouping element in
which a new section is to be inserted where there is some ambiguity as
to which grouping element the new section would belong but the different
parts of the reference are typically separated by intervening amendment
text (‘After section 53 the following section is inserted in Chapter 3’
or ‘Chapter 3 of Part I is amended by inserting the following section
after section 53’).

For elements below the section level, there is either a long form or a
short form. The long form is something like ‘paragraph (a) of subsection
(1) of section 53’ where each element in the hierarchy is identified
individually by the type of element and the number portion of the label.
The shortened form is like either ‘paragraph 53(1)(a)’ or ‘section
53(1)(a)’ (more typically the latter) where a single word identifies
only the type of element the first element or the last element (examples
of both occur in Singapore legislation). The number from the labels of
each referencable element from the section-level down to the target
element is also required.

In references to definitions or to target elements within definitions,
the number from the label is replaced with the defined term in quotes
(‘the definition of “today” in section 3’, ‘sub-paragraph (a)(ii)(C)
of the definition of “Director” in subsection 4(1)’). The shortened form
is only partially used in references to definitions because there is no
way to shorten the definition component of the cross-reference. This
breaks the cross-reference into three parts, the shortened form of
reference to the parent of the definition, the definition component, and
the shortened form of the reference to all the elements below the
definition in the document hierarchy.

### Grouping elements

For grouping elements that have a //num, the wording typically refers to
the target element and all referencable elements above the target
element. Again there is a long form and a short form. For example,
references to ‘Chapter 3 of Part I’ will always contain a reference to
the target element (Chapter 3) and the containing grouping element (Part
1) although the order may vary in different contexts (e.g. ‘Chapter I.3’
is used in some jurisdictions and these shortened forms are more common
in summaries of amendments). Any reference to ‘Chapter 3’ without the
qualifying ‘Part I’ would assume the context in which the
cross-reference occurs so the Part component is implicit.

The reference to each element typically comprises words identifying the
type of element (“Part”, “Chapter”) either explicitly or implicitly, and
the number (“3”, “I”). We include both in the //num content. Such
elements typically have only a single heading which requires no number
(e.g. ‘the heading to Part I’, ‘Chapter I.3: Heading’). Given that a
hypertext link to the heading and one to the whole element would
essentially point to the same place in the document, it is not strictly
necessary to give the heading a separate ID for reference purposes but
it can be useful for amendment wording and consolidation purposes.

The generic group elements (//hcontainer\[@name="crossheading"\] and
//hcontainer\[@name="subheading"\]) typically have a //heading but no
//num, which necessitates an alternative mechanism for identifying them.
The two major alternatives in reference wording are to quote the entire
heading (e.g. ‘the crossheading “Introduction”’) including any higher
level grouping elements with //num elements as context (e.g. ‘the
crossheading “Introduction” in Part I’), or to use the following section
to locate the heading (e.g. ‘the crossheading immediately preceding
section 53’). Reference wording to such elements rarely addresses them
as a whole (e.g. ‘the sections grouped under the crossheading
“Introduction”’). It is more typical to refer to the heading and
sections separately (e.g. ‘the crossheading “Introduction” and sections
53 to 58’ or ‘sections 53 to 58 and the crossheading immediately
preceding them’).

This suggests that such headings could be treated as siblings of the
sections without a containing element. The problem with that approach is
that the group heading would occupy the same position in the element
hierarchy as any containing element heading (i.e. if the unnumbered
heading appears within Part V, 'the heading to Part V' and the grouping
heading would both match the XPath expression //body/part/heading making
the rules for rendering horrendously complicated. AKN solves this by
introducing the //crossHeading element distinct from the //heading but
this still ignores the semantic intent that the sections underneath that
heading are somehow grouped together. Therefore we have chosen to use a
container element to reflect the logical containment even if reference
wording wouldn't always recognize the containment relationship in this
instance.

### Other elements

Elements within the front matter of legislative documents are referred
to in similar ways to section-level elements (e.g. ‘the Preamble’, ‘the
long title’, ‘the short title’). Note that there would only ever be one
of each of these elements in a given Act or Bill. These elements
occasionally are further broken down into paragraphs and lower elements.
Such lower level elements are referred to in much the same way as if
they appeared in a section (e.g. ‘sub-paragraph (b)(iii) of the
Preamble’)

Elements within Schedules, Appendices and Annexures often include
references to grouping elements above them even if they are like
section-level elements (although Codes typically behave as though the
Code itself was a separate document and don’t include the grouping
elements).

## @eId

See [AKN id
scheme](https://docs.oasis-open.org/legaldocml/akn-nc/v1.0/os/akn-nc-v1.0-os.html#_Toc531692303)
including the list of standard abbreviations.

AKN recommends use of an optional *prefix*, an *element\_ref*
(essentially the name or abbreviated name of the element) and the
*number* (possibly empty). The prefix is the identifier of any
containing component necessary to ensure uniqueness of the ID. The
default separator between the *prefix* and *element\_ref* is double
underscore and between the *element\_ref* and the *number* is single
underscore. This broad approach was adapted from the EnAct and LEAP
approaches.

Despite CLML using simpler separators, we choose to follow the AKN
examples more closely (EnAct used "-" and ".", CLML uses "-" as the
separator in IDs and "/" as the separator in URIs and avoids the
*element\_ref* for common structures within a section or equivalent).

### element\_ref component

Although the abbreviations listed in the above AKN documentation are not
always standard in a UK context (e.g. "sec" instead of "s" for section,
"dvs" instead of "div" for division, "chp" instead of "cap" for chapter)
we choose to follow the AKN standard where specified.

The following table describes the abbreviations used by LDAPP and their
source:

|                       |                  |            |                                                       |
| --------------------- | ---------------- | ---------- | ----------------------------------------------------- |
| **XML element/@name** | **element\_ref** | **Source** | **Comments**                                          |
| \<alinea\>            | al               | AKN        | Not likely to be used                                 |
| \<amendmentBody\>     | body             | AKN        |                                                       |
| \<article\>           | art              | AKN        |                                                       |
| \<attachment\>        | att              | AKN        |                                                       |
| \<blockList\>         | list             | AKN        |                                                       |
| \<chapter\>           | chp              | AKN        | Would prefer to use "ch" or "cap"                     |
| \<citation\>          | cit              | AKN        |                                                       |
| \<citations\>         | cits             | AKN        |                                                       |
| \<clause\>            | cl               | AKN        |                                                       |
| \<component\>         | cmp              | AKN        |                                                       |
| \<components\>        | cmpnts           | AKN        |                                                       |
| \<componentRef\>      | cref             | AKN        |                                                       |
| \<debateBody\>        | body             | AKN        |                                                       |
| \<debateSection\>     | dbsect           | AKN        |                                                       |
| \<division\>          | dvs              | AKN        | Would prefer to use "div"                             |
| \<documentRef\>       | dref             | AKN        |                                                       |
| \<eventRef\>          | eref             | AKN        |                                                       |
| \<judgmentBody\>      | body             | AKN        |                                                       |
| \<intro\>             | intro            | AKN        |                                                       |
| \<list\>              | list             | AKN        |                                                       |
| \<listIntroduction\>  | intro            | AKN        |                                                       |
| \<listWrapUp\>        | wrap             | AKN        |                                                       |
| \<mainBody\>          | body             | AKN        |                                                       |
| \<paragraph\>         | para             | AKN        |                                                       |
| \<quotedStructure\>   | qstr             | AKN        |                                                       |
| \<quotedText\>        | qtext            | AKN        |                                                       |
| \<recital\>           | rec              | AKN        |                                                       |
| \<recitals\>          | recs             | AKN        |                                                       |
| \<section\>           | sec              | AKN        | Would prefer to use "s"                               |
| \<subchapter\>        | subchp           | AKN        |                                                       |
| \<subclause\>         | subcl            | AKN        |                                                       |
| \<subdivision\>       | subdvs           | AKN        | Would prefer to use "subdiv"                          |
| \<subparagraph\>      | subpara          | AKN        |                                                       |
| \<subsection\>        | subsec           | AKN        | Would prefer to use "subs"                            |
| \<temporalGroup\>     | tmpg             | AKN        |                                                       |
| \<wrapUp\>            | wrapup           | AKN        |                                                       |
| @name="definition"    | def              | LDAPP      | Note that //def content will be used instead of //num |
| @name="schedule"      | sch              | LDAPP      |                                                       |
| @name="crossheading"  | xhdg             | LDAPP      |                                                       |

<span class="underline">TODO - need to complete this list (should this
be the master or the result?) \[I have code that is more up-to-date than
this table - TJA\]</span>

### number component

To ensure a valid name attribute, to turn the //num component into the
*number* component of the @eId, we strip out the redundant @name
component if present (the *element\_ref* component should provide this
information) and any non-name characters including spaces, punctuation,
and brackets. For most elements this is sufficient to uniquely identify
the element. The two major exceptions are definitions and grouping
elements without a //num.

#### Definitions

For definitions, we propose to replace the //num component with the
defined term (//def) with any non-name characters (and occurrences of
“-”) removed (i.e. ‘the definition of “captain’s table”’ becomes
‘dfcaptainstable’). For bi-lingual publication of legislation, it will
be desirable to include the defined term in both languages in each
language rendition (AKN does not provide a standard solution for this
but we will address that when we need to) so the English term would be
available in any Welsh or Gaelic rendition that is created.

#### Unnumbered grouping elements

In order to uniquely identify grouping elements without a //num
(//hcontainer\[@name="crossheading"\] and possibly //level), it is
necessary to find some alternative for the *number* for each element.
The cross-reference wording either quotes the contents of the heading or
refers to the following section number. It would be impossible to have
an ID scheme that was guaranteed unique that could accommodate both
reference forms simultaneously. Therefore a compromise is necessary.

The following alternatives have been identified:

1.  Use the /heading text directly

<!-- end list -->

``` 
   - without modification;
     * For:   based on one of the two reference forms,
     * For:   easy for user to understand,
     * For:   almost certain to be unique within context,
     * Against:   its potentially quite long,
     * Against:   it does not accommodate the reference form based on next section,
     * Against:   IDs for different languages are usually different,
     * Against:   includes non-name characters (can’t be an XML ID),
     * Both:  the ID will change if the text of the heading changes,
   - choose one language (choose English as it avoids most character issues);
     * For:   based on one of the two reference forms,
     * For:   easy for user to understand,
     * For:   almost certain to be unique within context,
     * For:   IDs for Chinese and English are the same,
     * Against:   the choice of language is visible,
     * Against:   its potentially quite long,
     * Against:   it does not accommodate the reference form based on next section,
     * Against:   can only generate ID for other language rendition if matching English rendition is available,
     * Against:   includes non-name characters (can’t be an XML ID),
     * Both:  the ID will change if the text of the heading changes,
   - choose one language (English) and strip non-ASCII characters from the heading contents;
     * For:   based on one of the two reference forms,
     * For:   easy for user to understand,
     * For:   almost certain to be unique within context,
     * For:   IDs for all language renditions are the same,
     * Against:   the choice of language is visible,
     * Against:   its potentially quite long,
     * Against:   it does not accommodate the reference form based on next section,
     * Against:   can only generate ID for other language rendition if matching English rendition is available,
     * Both:  the ID will change if the text of the heading changes,
   - choose one language (English), calculate a checksum (we propose an MD5 checksum) based on the heading content encoded so that it contains only valid name characters;
     * For:   based on one of the two reference forms,
     * For:   language choice hidden,
     * Against:   it is always quite long,
     * Against:   it does not accommodate the reference form based on next section,
     * Against:   can only generate ID for other language rendition if matching English rendition is available,
     * Against:   cannot guarantee uniqueness;
     * Both:  the ID will change if the text of the heading changes,
- insert an additional attribute on the element which contains a unique value ===
   - use a GUID;
     * For:   guaranteed unique,
     * For/Against:   same mechanism for @eId as for @guid rendering one redundant,
     * Against:   it is always quite long (32 characters per GUID),
     * Against:   it bears no relationship to either reference wording form,
     * Against:   it must be assigned simultaneously to all language versions to guarantee the same ID for corresponding renditions,
     * Both:  the ID won't change if the text of the heading changes,
   - assign a number whenever a new element of that type is inserted into the document by finding the largest number in the document already and incrementing; 
     * For:   guaranteed unique,
     * For:   easy for user to understand,
     * Against:   it bears no relationship to either reference wording form,
     * Against:   it must be coordinated between languages so that the same number is assigned to corresponding elements in both languages,
     * Both:  the ID won't change if the text of the heading changes,
- choose the @no component of the first /provision1 that appears within the grouping element (cross-reference wording might change but not ID and ID might change but not wording):
   - just use the first descendant section number in place of the missing %%//%%num;
     * For:   guaranteed unique (within context),
     * For:   based on one of the two reference forms,
     * For:   easy for user to understand,
     * For:   can be allocated in any language rendition independently,
     * Against: may be difficult to determine from the @eId alone whether the number is from the element itself or the first descendant section
     * Both:  the ID won't change if the text of the heading changes but will change if new sections are inserted or the first section is renumbered,
   - insert a marker character immediately after the //element_ref// and before the //number//;
      * For:  guaranteed unique (within context),
      * For:  based on one of the two reference forms,
      * For:  easy for user to understand,
      * For:  can be allocated in either language rendition independently,
      * For:  can distinguish numbered grouping element (one with @no) from unlabeled grouping element.
      * Both: the ID won't change if the text of the heading changes but will change if new sections are inserted or the first section is renumbered,
```

Of these options, 1.a and 1.b are unacceptable because they are not
valid XML ID’s, 1.c and 1.d require that the attribute is assigned
simultaneously to all language renditions (which is not a problem as
multi-lingual documents in the UK are almost certainly to be translated
from existing English documents) and 2.a and 2.b can calculate the ID
from the English rendition alone but any other language rendition would
require a matching English rendition to be present before assigning ID’s
(again probably acceptable in the UK). Given that we also want to make
use of the ID’s for checking that the versions match structurally, none
of these schemes is particularly satisfactory. Items 1.b, 1.c and 1.d
may have undesirable political side-effects. Items 3.a and 3.b are the
most promising. Because cross-headings are always unnumbered, we
consider the risk that 3.b is trying to address as low, and since either
3.a or 3.b satisfies nearly all the criteria and produces short ID’s
with clear semantics, 3.a appears to be the best choice of these options
for the UK context.

### Duplicate @eId values

If after all of these calculations are applied, a duplicate ID occurs
within a single document, at the level the duplication occurs an
additional component is inserted with *prefix* 'oc’ and *number* set to
the number of the occurrence of an element with the ID preceding the
‘oc’ component.

## @GUID

Although AKN calls this a "Globally Unique Identifier" which has a quite
specific and well-understood meaning, the standard states: "This
attribute is an application-specific identifier that a local
implementation may need to add to elements according to local rules and
syntaxes. GUID is not a required attribute. Its use and specification is
totally dependent on the representation and storage requirements of the
author of the Manifestation. Despite the name, GUID\[sic\] do not even
have to be globally unique across documents of the same collection. They
are meant as a way to place ids from legacy formats and collections and
that are still in use. The usage of GUID attribute has no required
syntax and does not impact on compliance with this specification."

However, we require this value on every referencable element to ensure
cross-references can be updated and require it to be unique at least
within the system and allocate values compliant with the [GUID
standard](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=netframework-4.7.2)
(which is Microsoft's name for a
[UUID](https://tools.ietf.org/html/rfc4122)).

So that the @GUID value is a valid NMTOKEN and can therefore be treated
as an XML ID, we prefix the serialized form of the GUID by "\_".
