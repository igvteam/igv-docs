Sample information files includes Attributes files, Sample Mapping files, Attribute Color files, and files that combine 
information. These are tab-delimited text files with extension .txt. You load them as you would data files, via the 
_File m_enu. IGV can load multiple sample information files per session.

When loaded into IGV, attributes display in a separate color-coded panel between sample names and tracks. See 
[Sample Attributes](http://www.broadinstitute.org/software/igv/DisplayOptionsAttributes) and 
[Sorting, Grouping, and Filtering](http://www.broadinstitute.org/software/igv/SortGroupFilter) 
for more information on displaying attributes and using attributes to manipulate tracks. IGV automatically 
assigns colors and heatmaps to attribute data values and what it determines are data ranges.

This page has the following sections.

*   [Overview of sample information file types](#overview)
*   [Attributes files](#attributesfile) include descriptive information such as annotations or metadata for tracks.
*   [Sample Mapping files](#samplemappingfile) match sample identifiers across datasets.
*   Optionally assign specific [Attribute Colors](#Colors), including heatmap ranges.

Sample information files allow integrating diverse data tracks from the same sample or patient.

* Tracks can be grouped based on the value of an attribute from the sample information file, such as a patient identifier. See the example in the [Attributes files](#attributesfile) section.
* Similarly, use to annotate VCF sample rows with metadata and allow grouping.

Overview of sample information file types
=========================================

Consider your data visualization needs as the various sample information sets allow for different features of IGV. 
The **decision tree table** below matches use cases to the Sample Information file types.

**Attribute, mapping, and color information may be in separate files,** i.e. in Attributes files, Mapping files, and 
Color files, **or in a single Sample Information file.**

*   To save all three types of information in a single file, list attributes first, then mapping, and then color.
    *   Between the information types, separate sections with row headers _#sampleMapping_ and _#colors_.
    *   Empty rows are not necessary and are ignored.

When loading attributes for datasets where sample names are identical across file types, no mapping information is 
necessary for the attributes to apply to the multiple data type tracks. However, to apply the same attribute information 
across datasets where sample names differ, you can use either of two different types of Sample Information sets as 
indicated by (b) and (c) in the table.

**Multiple data track types?**

No

Yes

**Do attributes sample labels match data track sample names?**

No.

(a) Edit Attributes file to include the matching data track sample names in the first column.

(b) Load Attributes and Sample Mapping information.

Yes.

Attributes apply to data tracks.

No.

(b) Load Attributes and Sample Mapping information.

Yes.

Attributes apply to data tracks.

Attributes
==========

An Attributes file lists track identifiers in the first column and attributes in subsequent columns with a single 
header row. IGV matches the track identifiers in a data file with the track identifiers in the Attributes file.

*   Example 1: [exampleSampleInfo.txt](http://www.broadinstitute.org/igvdata/exampleFiles/exampleSampleInfo.txt)
*   Example 2: [BLCA\_ClinicalAttributes.txt](https://dm.genomespace.org/datamanager/file/Home/Public/SpaceCadet/IGV%20Sample%20Information%20Files/BLCA_ClinicalAttributes.txt)

For example, load the second example file on top of IGV hg19's _CopyNumber: \[genome\_wide\_snp\_6\_\_broad\]._ 
This data is found in the hosted server data _The Cancer Genome Atlas_\>_TCGA Broad GDAC>Firehose Standard Data_\>_Broad Firehose Standard Data Run: 2015\_02\_04_\>_BLCA-TP._ 
Applying attributes to the data file allows sorting by copy number for the 22q13:32 loci _and_ the pathology.M.stage 
attribute as shown in the **Screenshot** (2015.03.05) below.

![](img/SL_IGV_loadattributes2015-03-05%2012.55.51.png)

#### Acceptable variations to the Attributes file

So long as the first row contains attribute labels and the first column sample names, the remaining rows may contain 
information pertaining to samples in any data type and be organized in any way.

* Because IGV can load multiple Attributes files per session, it is not necessary to merge attributes into a single file.
* Attributes only apply to data tracks with matching names. Attribute rows without matching data tracks do not display. 
* So the information within the Attributes file need not overlap exclusively to the data tracks.
* For data tracks without a matching attribute row, corresponding IGV attributes panel rows remain blank.

In the case of different data sets with different sample names from the same individual, e.g. copy number and RNA 
expression, you may wish to apply the information within a single attributes file in duplicate to the different data 
types. In this case, you may (b) additionally load a Sample Mapping file as outlined in the next section 
or **(c) modify your Attributes file** as outlined below.

For a single attributes file, duplicate the attributes by copy-pasting into empty rows, then modify sample names in 
the first column as needed for the differentially named datasets.

For multiple attributes files, duplicate the entire file and open each to modify sample names for the differentially 
named datasets as needed.

Sample Mapping
==============

A Sample Mapping section begins with the line #sampleMapping and maps track identifers to sample identifiers. It is 
useful in cases where these identifiers might differ. For example, one might map the track identifier "foo.bam" to 
sample identifier "foo\_sample".  The format is 2 column tab delimited, the first column is the track identifier, 
second the sample identifier.

Attribute Colors
================

By default, IGV randomly assigns colors to the attribute values. You can optionally specify the colors for attribute 
values in RGB format for a specific label, a specific value, or as a heatmap scale for numeric columns in monocolor 
or in two-color heatmap for specified ranges. Customize colors using either a separate Attribute Colors file or by 
adding a colors section to the end of a Sample Information file. Colors information is tab-delimited with three or 
four columns as shown in the example below.

**column 1**

**column 2**

**column 3**

**column 4 (optional)**

 

Indicates attribute name

Indicates attribute value or attribute range separated by a colon (:)

Indicates color in RGB format. If used with column 4, then is the first color of a two-color heatmap

Specifies the second color in RGB format in a two-color heatmap for attribute ranges

**Example**

**Explanation**

#colors

 

 

 

 

GENDER

MALE

0,0,155

 

_a value of  "MALE" for the "GENDER" column gets the color (0,0,155)_

\*

Classical

80,180,80

 

_a value of "Classical"  in any column gets the color  (80,180,80)_

KarnScore

\*

0,0,255

 

_numeric column example, monocolor heatmap_

% Tumor Nuclei

90:100

0,0,255

 

_another monocolor heatmap, this time with the range specified_

sil\_width

\-0.1:0.5

0,0,255

255,0,0

_a two-color heatmap with the range specified_

*   Colors information, either file or section, must be headed by a row with _#colors_.
*   An asterisk (\*) in either of the first two columns indicates a wildcard.
*   RGB values are separated by commas (,) without spaces and may be listed inside double quotations, e.g. _0,0,155_ or _"0,0,155"_.

Look up RGB values by color wheel at _[https://color.adobe.com/create/color-wheel/](https://color.adobe.com/create/color-wheel/)_. 
Alternatively look up RGB values on a chart at _[http://www.rapidtables.com/web/color/RGB\_Color.htm](http://www.rapidtables.com/web/color/RGB_Color.htm)_.

Briefly, **RGB** (red, green, and blue light) refers to a system of representing colors for computer display with zero 
representing absence and 255 giving maximum light for a color in comma-separated values. 