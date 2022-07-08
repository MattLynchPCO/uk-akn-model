# Change tracking and alternatives

Oxygen native change tracking uses processing instructions to mark
inserted and deleted text. There is no separate markup for structural
changes so these need to be inferred from the textual changes (e.g.
changes to the content of a //num).

AKN native change tracking makes use of the //ins and //del elements and
uses metadata in //meta/analysis/activeModifications to group a series
of //ins and //del elements into a single change. While this metadata is
rich and allows easy identification of the source and destination of an
amendment, it means that a fragmented document is not self-contained and
needs to continually reference the //meta of the containing document.
This also means that any formatting that uses information from //meta is
highly inefficient.

For that reason, within the LDAPP system for managing capturing
amendments as change-track to generate traditional amendment wording, we
have adopted the TeraText for Legislation change track markup
conventions, adapting the existing AKN //ins and //del inline elements
and introducing a number of additional attributes in the ukl namespace
to support efficient formatting of changes-tracked amendments and
ensuring a set of amendments is self-contained when fragmented. We have
therefore added the following attributes:

  - //ins|del@ukl:changeStart, marking the starting character (typically
    ”\[“) of a group of related changes,
  - //ins|del@ukl:changeEnd, marking the ending character (typically
    ”\]“) of a group of related changes,
  - //ins|del@ukl:changeDnum, recording the DNum of an amendment
    associated with the first of a series of change track markup
    recording that amendment (typically on the same element as the
    @ukl:changeStart),
  - //hcontainer@ukl:change, marking change of a whole element, values
    include:
      - del, delete the whole element,
      - ins, insert the whole element,
      - delStruct, delete the structural container (typically including
        num and heading, start and end tags),
      - insStruct, insert the structural container (typically including
        num and heading, start and end tags),
  - //hcontainer@ukl:changeStart, marking the starting character
    (typically ”\[“) of a group of related changes, and
  - //hcontainer@ukl:changeEnd, marking the ending character (typically
    ”\]“) of a group of related changes.
