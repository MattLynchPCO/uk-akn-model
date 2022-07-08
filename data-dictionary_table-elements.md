## Table elements

AKN includes a subset of the XHTML table markup for tables. Despite AKN
being an OASIS standard, it inexplicably does not use the obvious
competing table markup created by OASIS. The major missing elements from
XHTML are //thead, //tbody and //tfoot. Some XML tools also are unable
to apply the column and row merging attributes of XHTML if the same
element names are used with a different namespace (this is particularly
true of CSS-driven styling). We therefore propose to use //foreign to
wrap XHTML table namespace elements rather than the AKN //table
elements. On import into LDAPP, AKN tables can be mapped to XHTML tables
relatively reliably although the conversion back is somewhat lossy.

Elements from the XHTML table model include:

  - //table: This is the top level element surrounding a table and
    associated caption.
  - //caption: We will not use this element as tables will appear within
    a //tblock\[@class="table"\] with an optional //num and //header
    which should be preferred to the XHTML caption
  - //col: This element is used to specify attributes across a whole
    column
  - //colgroup: This element is used to group sets of //col - legacy
    data may not always have reliable markup for this concept
  - //thead: This element groups //tr which would normally not scroll at
    the top of the table view (or repeat at the top of each page of the
    multipage table - not to be confused with //th)
  - //tbody: This element groups //tr for the body of the table which
    would normally scroll or appear only on a single page for a
    multipage table
  - //tfoot: This element groups //tr which would normally not scroll at
    the bottom of the table view (or repeat at the bottom of each page
    of a multipage table)
  - //tr: This element is for a row in the table.
  - //td: This element appears as a data cell within a table row
  - //th: This element appears as a header cell within a table row (note
    that a //th may not appear necessarily within a //thead)

Documentation on these elements and their attributes is available at
[W3C XHTML2 Table
elements](https://www.w3.org/TR/xhtml2/mod-tables.html)
