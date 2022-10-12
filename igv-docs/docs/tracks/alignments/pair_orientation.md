The orientation of paired reads can be used to detect structural events including:

*   inversions
*   duplications
*   translocations

By selecting _Color alignments>by pair orientation_, you can flag anomalous pair orientations in IGV.

Orientation is defined in terms of read-strand: left versus right, and first read versus second read of a pair.

![](../../img/readpairorientations.jpg)

_(figure courtesy of Bob Handsaker)_

These categories only apply where both mates map to the same chromosome.

Inversions
----------

An inversion is a large section of DNA that is reversed in the subject genome compared to the reference genome.

![](../../img/inversion.jpg)

When an inversion shows up in paired-end reads, the reads are distinctively variant from the reference genome.

![](../../img/inversion_reads.jpg)

This appears in IGV as shown below.

![](../../img/inversion_colors.jpg)

Inverted Duplication
--------------------

When a large section of DNA is duplicated and inserted into the genome in a reversed configuration compared to the original sequence, this is called an inverted duplication.

![](../../img/invdupe.jpg)

There will be overlapping left and right reads, and there will likely be altered coverage depth/copy number.

![](../../img/invdupe_reads.jpg)

This appears in IGV as shown below.

![](../../img/indupe_colors.jpg)

Tandem Duplication
------------------

When a large section of DNA is duplicated and inserted into the genome next to the original sequence, this is called a tandem duplication.

![](../../img/tandemdupe.jpg)

The reads will not only be duplicated, but also be arranged as shown below.

![](../../img/tandemdupe_reads.jpg)

IGV will display this rearrangement as shown below.

![](../../img/tandemdupe_colors.jpg)

Translocation on the Same Chromosome
------------------------------------

When a large section of DNA is removed from one location and inserted elsewhere, that is a translocation.

![](../../img/translocation.jpg)

Translocations on the same chromosome can be detected by color-coding for pair orientation, whereas translocations between two chromosomes can be detected by coloring by insert size.

![](../../img/translocation_reads.jpg)