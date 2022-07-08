## //ref and //refs

Akoma Ntoso provides a single //ref element to manage a number of
different kinds of references including references to elements within
the document, references to metadata and change markup, and references
external to the document. The //ref element has one attribute for the
target of the reference which is a URI (URL or URN) in addition to the
attributes available on all AKN elements.

In LDAPP, we have adopted the following conventions:

  - internal references (references to referencable elements within the
    same document) always commence with "\#" followed by the @eId value
    of the target
  - references to other documents within the UK statute book use the
    published URN from legislation.gov.uk
  - references to documents in the PDR not yet published to the UK
    statute book use the document ID following a similar pattern to that
    for legislation.gov.uk 
  - references to elements within documents in the PDR use the URI of
    the document followed by "\#" and the @eid value of the target.

In particular, parliamentary amendments will often refer to documents in
the PDR rather than the UK Statute Book so this suggests that every
version of every document in the PDR needs to be uniquely referenceable.

Note that there may be references to Bills and draft SIs that are not
yet in the PDR (for instance if you are drafting a Bill and matching SIs
to be made available simultaneously). We presume that these will be
either not marked as references or the //ref markup will be incomplete
until such time as the target is available in one of those collections.

The //ref element may be augmented with the following additional
optional attributes:

  - @ukl:targetGuid - the value of the @GUID attribute of the target
    element, this supports renumbering so should always be used if the
    target element has a @GUID value
  - @ukl:targetJref - the value of the @ukl:jref attribute of the target
    element, this supports J-ref cross-references so should always be
    set if the target element as a @ukl:jref value

<span class="underline">TODO - use of @class to indicate status of
reference markup (see Confluence)</span>

<span class="underline">TODO - what does the document ID look like in
the PDR?</span>

<span class="underline">TODO - for future functionality we need to
consider the possibility of referring to a document before it reaches
the PDR especially for maintaining cross-references between related
Bills. Suggest we require the relevant projects to be linked in order to
achieve that.</span>
