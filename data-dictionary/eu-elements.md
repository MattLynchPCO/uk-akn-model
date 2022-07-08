# EU Legislation elements

EU legislation has been incorporated into or adopted as UK legislation
at various times. While LDAPP does not need to create new EU
legislation, it does need to amend existing legislation.

We therefore expect EU-specific tags to appear only in //quotedStructure
elements with @ukl:docName set to one of the EU legislation types.

These elements include:

  - //title - see [Grouping
    elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_grouping-elements),
  - //article\[@class="EUProv1"\] - see below,
  - //paragraph\[@class="EUProv2"\] - see below,
  - //hcontainer\[@name="annex"\] - see below,
  - //point\[@class="para1"\] - see below, and
  - //hcontainer\[@name="annex"\] - see below.

## //title

See [Grouping
elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_grouping-elements).

## //article\[@class="EUProv1"\]

Articles in EU legislation occupy the same semantic role as sections in
UK and Scottish Acts. However, they typically appear in documents more
like grouping elements with a centred //num containing the contents
"Article *N*" with a centred heading directly beneath that (if one
exists).

For this reason we have created a distinct @class value for them
("EUProv1") so formatting can easily be distinguished in CSS and for PDF
generation. Otherwise, they are largely the same as //section in Acts.

See generally [Section level and below
elements](https://ldapp.teratext.leidos.com.au/doku.php?id=data-dictionary_section-elements).

## //paragraph\[@class="EUProv2"\]

Like sections in UK and Scottish Acts, articles can be optionally broken
into subsection-like elements which are normally called "paragraph". The
formatting is similar to but slightly different from subsections so
again we use a distinct but similar @class value "EUProv2". The
numbering scheme is identical to subsections in Acts.

While the English convention is that subsections are complete sentences
in their own right, this convention is not as strongly adhered to in EU
drafting so there may be an //intro in an //article preceding the first
//paragraph. For the purposes of this system, these provisions are
likely to only appear in //quotedStructure elements as newly inserted
provisions so are more likely to follow standard English drafting
conventions than provisions drafted elsewhere in the EU.

\===== *point\[@class="para*N*"\] ===== Below the optional //paragraph
level, EU legislation creates nested points so we use the existing
//point element to model these and, since the formatting is virtually
identical to paragraphing in UK Acts, we adopt @class values with the
pattern "para*N//" where *N* is one of 1, 2, or 3. Numbering conventions
are the paragraphing in SIs and SSIs although the auto-numbering could
be manually overwritten by a drafter editting the contents of the //num
element where other numbering schemes need to be perpetuated.

## //hcontainer\[@name="annex"\]

EU legislation as amended may insert whole schedule-like structures that
are called in EU legislation, "Annex". We use an
//hcontainer\[@name="annex"\] for these.

The provision- and paragraph-like elements are all called "point" in EU
legislation. This suggests using //point as we do for elements below
//article.

``` 
<hcontainer name="annex">
 <num>Annex 1</num>
 <point class="annexProv1">
  <num>1.</num>
  <content>
   <p>This is some content.</p>
  </content>
 </point>
 <point class="annexProv1">
  <num>2.</num>
  <content>
   <p>This is some content.</p>
  </content>
 </point>
</hcontainer>
<hcontainer name="annex">
 <num>Annex 2</num>
 <intro>
  <p>In this annex-</p>
 </intro>
 <point class="para1">
  <num>(a)</num>
  <content>
   <p>there is a portion, and</p>
  </content>
 </point>
 <point class="para1">
  <num>(b)</num>
  <content>
   <p>another.</p>
  </content>
 </point>
</hcontainer>

```
