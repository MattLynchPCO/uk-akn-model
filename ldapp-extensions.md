# LDAPP Extensions to AKN

Aware that additional attributes that are not part of AKN but extend AKN
will be needed for UK LDAPP, we introduce an attribute name space with
the prefix “ukl” to capture these additional extensions. The URI for
this namespace will be
“<https://www.legislation.gov.uk/namespaces/UK-AKN>”.

These extensions include:

  - //quotedStructure context attributes (see [quotedStructure in the
    Data
    Dictionary](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_block-elements#quotedstructure_embeddedstructure_and_mod)):

<!-- end list -->

``` 
   * @ukl:docName the @name attribute of the //bill or //act from which or into which the quoted element is being taken or inserted
   * @ukl:indent the indent level of the quoted element (so we can support nested structures, paragraphs in definitions, provisos, steps etc) - one of indent0, indent1, indent2, indent3, indent4, indent5
* %%//%%ref@ukl:targetGuid the GUID equivalent of the @eId component of @href
* %%//%%ref@ukl:targetJref, set to the value of the @ukl:jref attribute of the target of the reference (only set if the target element itself has a @ukl:jref)
* %%//%%rref@ukl:fromGuid the GUID equivalent of @from
* %%//%%rref@ukl:upToGuid the GUID equivalent of @upTo
* %%//%%num@ukl:autonumber which is set to "no" if the contents of the %%//%%num are not to be changed when auto-numbering.
* %%//%%def@ukl:startQuote and %%//%%def@ukl:endQuote to mirror those used in %%//%%quotedStructure
* %%//%%*[@class="prov1"]@ukl:jref and %%//%%*[@class="sch"]@ukl:jref to store the user-defined J-ref string used while provision numbering is still in flux
* %%//%%*[@class="prov1|prov2|schProv1|schProv2|para1|para2|para3]@ukl:type - initially either unset or with the value "money" for financial provisions - other supported values to be determined
```

In addition, while editing, Lawmaker makes use of change track markup in
the style of TeraText for Legislation rather than the Akoma Ntoso change
track. While we use the //ins and //del inline tags, we have added
custom attributes to those tags and to //hcontainer elements to ensure
that the fragments of XML are self contained representations of the
changes rather than relying on metadata located elsewhere in the
document to interpret the change. This facilitates rendering in the
editing tool and production of PDF. We have therefore added the
following attributes:

  - //ins|del@ukl:changeStart, marking the starting character (typically
    "\[") of a group of related changes,
  - //ins|del@ukl:changeEnd, marking the ending character (typically
    "\]") of a group of related changes,
  - //ins|del@ukl:changeDnum, recording the DNum of an amendment
    associated with the first of a series of change track markup
    recording that amendment (typically on the same element as the
    @ukl:changeStart),
  - //hcontainer@ukl:change, marking change of a whole element, values
    include:
      - del, delete the whole element,
      - ins, insert the whole element,
      - delStruct, delete the structural container (typically including
        //num and //heading, start and end tags),
      - insStruct, insert the structural container (typically including
        //num and //heading, start and end tags),
  - //hcontainer@ukl:changeStart, marking the starting character
    (typically "\[") of a group of related changes, and
  - //hcontainer@ukl:changeEnd, marking the ending character (typically
    "\]") of a group of related changes.
