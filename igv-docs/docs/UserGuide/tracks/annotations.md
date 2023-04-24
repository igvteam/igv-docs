# TBD More general stuff about viewing annotations as in our workshops


# Viewing options 

There are 3 different options for viewing the feature track. These allow you to display overlapping features, such as
different transcripts of a gene, on one line or multiple lines

To change the view of the feature track, right-click on the feature track and select one of the options:

Collapsed:

![](../img/featuretrackcollapsed.jpg)

Squished:

![](../img/featuretracksquished.jpg)

Expanded:

![](../img/featuretrackexpanded.jpg)

# Exon jumping

This feature is similar to feature jumping. To feature-jump, you select a feature track and press Ctrl-F for forward,
Ctrl-B for back. To exon-jump, you select a feature track and press SHIFT-Ctrl-F to center the next exon in your view,
SHIFT-Ctrl-B to move back one exon.

# GFF style tags for BED files


The "name" field (column 4) of a BED file can contain GFF3 style key-value attribute tags by specifying "gffTags=on" on
the track line. These attributes will be displayed in the mouse hover popup text.
