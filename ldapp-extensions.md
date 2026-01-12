# LDAPP Extensions to AKN

This document describes extensions to the [Akoma Ntoso (AKN) XML standard](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html) that are specific to the UK Lawmaker (LDAPP) implementation.

## Namespace Declaration

Additional attributes that extend AKN are placed in a dedicated namespace (URI: `https://www.legislation.gov.uk/namespaces/UK-AKN`). In practice Lawmaker uses the prefix `ukl` for this namespace.  

These extensions are necessary to support specific requirements of UK legislative drafting and publishing that are not covered by the standard AKN schema. They are mostly intended to be used for transient purposes during the drafting phase.

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

Lawmaker uses change track markup which extends the Akoma Ntoso change track vocabulary, enabling both structural and textual changes to be marked up.

The [`ins`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_ins) and [`del`](https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html#element_del) inline tags are used for textual changes, while custom attributes are used on structural elements (e.g. `hcontainer` elements) to represent the equivalent changes. In addition, custom attributes have been added in both cases to capture richer information about the change and ensure that the fragments of XML are self-contained representations of the changes rather than relying on metadata located elsewhere in the document to interpret the change. This facilitates rendering in the editing tool and production of PDF.

The following change tracking attributes are used:

### For ins and del Elements

- `ukl:changeStart` - True if the element is the first part of the change
- `ukl:changeEnd` - True if the element is the last part of the change
- `ukl:changeDnum` - value of any amendment ID (Dnum) associated with the change (typically on the same element as the `@ukl:changeStart`)
- `ukl:change` - applied to a structural element (e.g. `hcontainer`) to indicate a change to the whole element (where `<ins>` and `<del>` elements are not used). Possible include:
  - `del` - Delete the whole element
  - `ins` - Insert the whole element
  - `delStruct` - ?
  - `insStruct` - ?
  - `insReplace` - Insert whole element as part of substitution
  - `delReplace` - Delete whole element as part of substitution
