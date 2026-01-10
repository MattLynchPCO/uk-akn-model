# LDAPP Extensions to AKN

This document describes extensions to the [Akoma Ntoso (AKN) XML standard](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html) that are specific to the UK Lawmaker (LDAPP) implementation.

## Namespace Declaration

Additional attributes that extend AKN are placed in a dedicated namespace with the prefix `ukl:`. The URI for this namespace is:

```
https://www.legislation.gov.uk/namespaces/UK-AKN
```

These extensions are necessary to support specific requirements of UK legislative drafting and publishing that are not covered by the standard AKN schema.

## Extension Attributes

### quotedStructure Context Attributes

For the [`quotedStructure`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_quotedStructure) element, the following UK-specific attributes are used:

- `@ukl:docName` - The `@name` attribute of the [`bill`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_bill) or [`act`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_act) from which or into which the quoted element is being taken or inserted
- `@ukl:indent` - The indent level of the quoted element (to support nested structures, paragraphs in definitions, provisos, steps, etc.) - one of: `indent0`, `indent1`, `indent2`, `indent3`, `indent4`, `indent5`

### Reference Attributes

For [`ref`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_ref) and [`rref`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_rref) elements:

- `ref@ukl:targetGuid` - The GUID equivalent of the `@eId` component of `@href`
- `ref@ukl:targetJref` - Set to the value of the `@ukl:jref` attribute of the target of the reference (only set if the target element itself has a `@ukl:jref`)
- `rref@ukl:fromGuid` - The GUID equivalent of `@from`
- `rref@ukl:upToGuid` - The GUID equivalent of `@upTo`

### Other Element Attributes

- `num@ukl:autonumber` - Set to "no" if the contents of the [`num`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_num) are not to be changed when auto-numbering
- `def@ukl:startQuote` and `def@ukl:endQuote` - Mirror those used in `quotedStructure` for the [`def`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_def) element
- `*[@class="prov1"]@ukl:jref` and `*[@class="sch"]@ukl:jref` - Store the user-defined J-ref string used while provision numbering is still in flux
- `*[@class="prov1|prov2|schProv1|schProv2|para1|para2|para3"]@ukl:type` - Initially either unset or with the value "money" for financial provisions - other supported values to be determined

## Change Tracking Attributes

While editing, Lawmaker uses change track markup in the style of TeraText for Legislation rather than the standard Akoma Ntoso change track. While the [`ins`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_ins) and [`del`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_del) inline tags are used, custom attributes have been added to those tags and to [`hcontainer`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_hcontainer) elements to ensure that the fragments of XML are self-contained representations of the changes rather than relying on metadata located elsewhere in the document to interpret the change. This facilitates rendering in the editing tool and production of PDF.

The following change tracking attributes are used:

### For ins and del Elements

- `ins|del@ukl:changeStart` - Marking the starting character (typically "[") of a group of related changes
- `ins|del@ukl:changeEnd` - Marking the ending character (typically "]") of a group of related changes
- `ins|del@ukl:changeDnum` - Recording the DNum of an amendment associated with the first of a series of change track markup recording that amendment (typically on the same element as the `@ukl:changeStart`)

### For hcontainer Elements

- `hcontainer@ukl:change` - Marking change of a whole element, values include:
  - `del` - Delete the whole element
  - `ins` - Insert the whole element
  - `delStruct` - Delete the structural container (typically including [`num`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_num) and [`heading`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_heading), start and end tags)
  - `insStruct` - Insert the structural container (typically including `num` and `heading`, start and end tags)
- `hcontainer@ukl:changeStart` - Marking the starting character (typically "[") of a group of related changes
- `hcontainer@ukl:changeEnd` - Marking the ending character (typically "]") of a group of related changes
