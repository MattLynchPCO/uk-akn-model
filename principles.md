# Guiding Principles

## Use of @name and @class

Following in the spirit of the Akoma Ntoso standard, where elements had
a consistent name, we preferred to use that name in the
//hcontainer@name (or equivalent named element). The @class attribute is
used to specify consistent formatting for elements with different names
but similar formatting in different document types or contexts (e.g.
section in an Act, clause in a Bill, rule, regulation or order in an SI
all have @class="prov1" - a first level standard provision).

For reasons that aren't immediately apparent, Akoma Ntoso has a number
of elements that do not permit the @name attribute, in particular
//blockContainer and //tblock. Where a consistent name is applied to
these elements, we have sometimes used the @class attribute to hold the
name rather than introducing a new namespace attribute although strictly
not the intended use of this attribute from the Akoma Ntoso
documentation. We believe future versions of Akoma Ntoso will add @name
to these elements so this slight misuse of the standard can be remedied
in the future.

## Use of //blockContainer v //tblock

The Akoma Ntoso standard provides little guidance on the use of //tblock
and //blockContainer and when one is to be preferred over the other.
They are largely both permitted in the same contexts and have similar
structural similarities and applications. On this project, we have
adopted the consistent practice that //tblock is used consistently
between those parts of the document where //hcontainer is valid and
those where only //tblock or //blockContainer are permitted (e.g.
//preamble, //conclusions) and is used for block constructs that would
normally appear within a named provision like tables, formulas, and
similar which have optional number and heading.

In parts of the document where //hcontainer is not permitted,
//blockContainer is preferred where it is replacing what would otherwise
be an //hcontainer if permitted as it supports //intro, //wrapUp and
//content (although does not require them like //hcontainer does). If
//tblock would be used in the //body, it is appropriate to use it
whether in the //body or in parts of the document that don't allow
//hcontainer.

## Use of //level

There was a robust discussion within our team about how to deal with
hierarchical containers normally numbered lower alphabetic in brackets
(e.g. "(a)"), often but not always called "paragraph". We originally
went with using the //paragraph element (a specialization of
//hcontainer) or //subparagraph depending on the context however we
discovered that the naming conventions were not as consistent as we
would like with different documents within the same collection naming
these elements differently.

We rejected the practice of many European jurisdictions of using one of
the numbered list constructs (//blockList/item or //ol/li) which would
have avoided the naming controversy altogether. However, this approach
prevents //hcontainer being used within these constructs and, as
definitions can occur at these lower levels, we wanted to preserve the
//hcontainer model for definitions and any other similar constructs that
were more naturally //hcontainer's.

Therefore, we ended up using the //level element which is an unnamed
//hcontainer element and making use of the @class attribute to capture
the level of paragraphing in which each //level was nested (particularly
necessary within amendment wording and the //quotedStructure element).
