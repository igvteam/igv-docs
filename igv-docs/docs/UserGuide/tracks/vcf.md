<!---
The page title should not go in the menu
-->
<p class="page-title"> Variants (VCF) </p>

VCF, which stands for Variant Call Format, is a standardized text file format used for representing SNP, indel, and structural variation calls. The full specification of the format can be found at [https://samtools.github.io/hts-specs](https://samtools.github.io/hts-specs).

In addition to the variant calls, VCF files can include genotype information for the samples underlying the calls.

A consistent color scheme is used in the variant display row, which is the top row, for files with or without geneotypes.

* blue - minor allele frequency/fraction is known from annotation or genotype data
* grey - minor allele frequency is not known
* red - height is proportional to minor allele frequency

# VCF files with genotypes

[![](../img/vcfwgenotypes.jpg)](../img/vcfwgenotypes.jpg)

![](../img/callout_1.jpg) Each bar across the top of the plot shows the allele fraction for a single locus.

![](../img/callout_2.jpg) The genotypes for each locus in each sample. Dark blue = heterozygous, Cyan = homozygous
variant, Grey = reference. Filtered entries are transparent.

If a file has more than 10 genotypes, the VCF file will be opened in its own pane, with a scroll bar, as shown below.

[![](../img/vcf_panes.jpg)](../img/vcf_panes.jpg)

### VCF Popup Menu

To see the options for changing the view of your VCF file, right-click on a variant. Some of the options are specific to
the variant selected. Find more details on the menu options on
the [Pop-up Menu](http://www.broadinstitute.org/software/igv/PopupMenus#VCF) page.

![](../img/vcf_rcpopup.jpg)

The window size at which VCF data is loaded is proportional to the number of samples. To change this, right-click and
select _Set Feature Visibility Window..._

To change the color coding of the plot, select _Color By>Allele_.

The _Sort Variant By_ options allow you to sort the set by a trait of a specific variant. You can select the sort twice
for the same variant to flip it, i.e., if you sort depth, it sorts from high to low; select the depth sort a second time
to sort from low to high.

The Display Mode changes what you can see of the data:

Collapsed removes all the genotypes, leaving only the allele frequency bars.

[![](../img/vcf_collapsed.jpg)](../img/vcf_collapsed.jpg)

Expanded shows the genotypes at the usual row height, with the sample names in the first column.

[![](../img/vcf_expanded.jpg)](../img/vcf_expanded.jpg)

Squished shows the genotypes with the rows compressed to maximize the data visible on the page.

[![](../img/vcf_squished.jpg)](../img/vcf_squished.jpg)

You can also adjust the height of the squished row by right-clicking and selecting _Change Squished Row Height_. You can
change the height of the rows in the window provided.

![](../img/vcf_squishedrowht.jpg)

# VCF files without genotypes

If you open a VCF file that does not contain genotypes data, the view will be different, displaying only the bars
marking the calls, as shown below.

![](../img/vcf_nogeno.jpg)

Similarly, the popup menu will be more limited, with only the _Set Feature Visibility Window..._ and _Remove Track_
options functional.