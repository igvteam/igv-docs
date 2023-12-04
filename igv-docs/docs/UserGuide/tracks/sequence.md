<!---
The page title should not go in the menu
-->
<p class="page-title"> Sequence </p>

When zoomed in sufficiently, the reference genome _**Sequence**_ track appears. The sequence is represented by
colored bars or colored letters, depending on zoom level, with adenine (A) in green, cytosine (C) in blue, guanine (G)
in yellow, and thymine (T) in red.
<!---
TBD describe how to change the default colors
-->

IGV displays the sequence of bases as they appear in the FASTA file for the reference genome. In addition to the upper
case letters A, C, G, and T, you may see lower case letters for these bases, and also N/n. Lower case letters often
mark repeated regions, and N/n may represent ambiguous nucleotides. However, the convention for the use of case and N,
is
not completely standardized, and depends on the creator of the genome sequence.

![](../img/SL_IGVsequencetrackzoomsm2015-04-01.png)

### Flipping the strand

You can change the strand that is displayed by clicking on the arrow in the title to the left of the track. Note that
the sequence and the arrow are only displayed when zoomed in to a sufficiently small region.

* Alternatively, right-click on _**Sequence**_ track to select _**Flip strand**_ from the pop-up menu.

![](../img/FlipStrand1.png)

The direction of the arrow indicates which strand is currently displayed. An arrow pointing left indicates that the
negative strand is showing. This strand will show the complement nucleotides and reverse complement translations.

### Sequence translation

With the reference genome sequence track, you can optionally display a 3-band track that shows a 3-frame translation of
the amino acid sequence for the corresponding nucleotide sequence. The translation is shown for the strand indicated.

* Right-click on _**Sequence**_ track to select _**Show translation**_ from the pop-up menu and to select a
  _**Translation Table**_.

![](../img/ThreeFrameTranslation.png)

Amino acids are displayed as blocks colored in alternating shades of gray. Methionines are colored green, and all stop
codons are colored red. When you zoom all the way in, the amino acid symbols will appear.

You can toggle the display of this translation track by clicking once, anywhere in the sequence or translation track, or
by toggling _**Show Translation**_ in the track popup menu.