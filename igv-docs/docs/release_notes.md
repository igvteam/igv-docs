* [IGV 2.14.x](#igv-214x)
* [IGV 2.13.x](#igv-213x)
* [IGV 2.12.x](#igv-212x)
* [IGV 2.11.x](#igv-211x)

# IGV 2.15.x

## IGV 2.15.0

**New Features**:

* Allow setting access tokens for specific hosts from batch scripts.  [Git Issue 1199](https://github.com/igvteam/igv/issues/1110)
* Option to explicitly set maximum splice coverage from Splice Junction Track.  [Git Issue 1015](https://github.com/igvteam/igv/issues/1015)

**Updates and bug fixes**

* Change "mut" file parsing to assume 1-based coordinates by default.  [Git Issue 1226](https://github.com/igvteam/igv/issues/1226)
* Use ID attribute for feature info links if ID is explicitly set.  Fixes regression introduced post release 2.12.3.  [Git issue 1232](https://github.com/igvteam/igv/issues/1232)
* Bug fix: Images not saved from Sashimi plots [Git Issue 1214](https://github.com/igvteam/igv/issues/1110)

# IGV 2.14.x

## IGV 2.14.1, released September 2022

**Updates and bug fixes**:

*   Improvements to alignment sorting.
*   New coloring option for alignments with base modification: "Color by base modification (all C)". Color Cytosine bases by most probable modification when specified by MM/ML tags.
*   Bug fix: Issues with alignment option "Color by base modification (5mC)" in the presence of "5hmC" modifications.
*   Bug fix: View as pairs broken if combined with "Color by ZMW".

## IGV 2.14.0, released August 2022

**New options for displaying sequence alignments**:

*   Color by base modification (5mC) specified with MM/ML tags in the BAM file. For more details, see https://github.com/igvteam/igv/wiki/5mC-coloring-mode.

*   Shade by mapping quality. (Git Issue [1110](https://github.com/igvteam/igv/issues/1110))

*   Group by mapping quality. (Git Issue [1112](https://github.com/igvteam/igv/issues/1112))

*   Sort by aligned read length. (Git Issue [1159](https://github.com/igvteam/igv/issues/1159))

*   When grouping alignments by an attribute, the display order of the groups can now be reversed by selecting _Group alignments by > Reverse group sorting_ in the right-click popup menu.  (Git Issue [#1106](https://github.com/igvteam/igv/issues/1106))

**Other updates and bug fixes:**

*   The IGV application no longer checks to for new versions. (Git Issue [#1117](https://github.com/igvteam/igv/issues/1117))

*   Bug fix: Combined data tracks could not be generated via _Tools > Combine Tracks_ or restored from previously saved sessions.

*   Bug fix: Tracks generated via the BLAT and Motif finder tools were not being restored when a saved session file was loaded.

*   Bug fix: Sashimi plots displayed a maximum of one sample.

*   Bug fix: Saved _.png_ images displayed a black background with black text for alignment track group labels. A white background is now used to match the onscreen appearance. (Git Issue [#1172](https://github.com/igvteam/igv/issues/1172))

*   Bug fix: TDF files failed to load via URL when the URL had a query string. (Git Issue [#1168](https://github.com/igvteam/igv/issues/1168))


# IGV 2.13.x

## IGV 2.13.2, released July 2022

This release fixes a problem with Sashimi plots - they were not displaying any splice junctions, only the annotation track.

## IGV 2.13.1, released June 2022

This release includes the following improvements and fixes:

*   Major performance improvement for CRAM files (htsjdk 3.0).

*   CSI indexes can now be loaded from URLs (htsjdk 3.0).  (Git Issue [#843](https://github.com/igvteam/igv/issues/843))

*   New menu item for feature tracks to specify the feature property to use for the displayed name.  (Git Issue [#1089](https://github.com/igvteam/igv/issues/1089))

*   Improved support for BigBed files; extra fields are now included in the popup text.

*   _Group-by-strand_ now works for feature tracks in collapsed mode.  (Git Issue [#1151](https://github.com/igvteam/igv/issues/1151))

*   Prevent jumping beyond the end of the chromosome.  (Git Issue [#1150](https://github.com/igvteam/igv/issues/1150))



## IGV 2.13.0, released May 2022

This release includes the following improvements and fixes:

*   Support for Amazon AWS default credentials. This enables loading data from AWS S3 using s3:// URLs if Amazon credentials can be found in the default credential chain as described in AWS documentation [here](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html). In addition, if default credentials are found, the default region chain will be searched as described in AWS documentation [here](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-region-selection.html). Cognito configuration, as described at [https://umccr.org/blog/igv-amazon-frontend-setup/](https://umccr.org/blog/igv-amazon-frontend-setup/), will take precedence over default credentials.

*   Support for [bigGenePred file format](https://genome.ucsc.edu/goldenPath/help/bigGenePred.html) (Git Issue [#1130](https://github.com/igvteam/igv/issues/1130))

*   Support for [bigNarrowPeak file format](https://genome.ucsc.edu/goldenPath/help/bigNarrowPeak.html).

*   Improved support for jumping to the next/previous feature in a selected feature track (using the "f" and "b" keys).
    *   The feature is now centered in the view.
    *   A preference can now be set to automatically zoom the view to fit the feature to the window, with optional up- and downstream padding. Go to the _General_ tab in _View > Preferences_ to set this preference.
    *   A bug has been fixed where typing an "f" or "b" into text fields (e.g. the locus search box) was interepreted as a feature jump if a feature track was selected. (Git Issue [#1122](https://github.com/igvteam/igv/issues/1122))

*   Support for handling a trailing "." or "?" character in the SAM tag MM (modified bases). (Git Issue [#1131](https://github.com/igvteam/igv/issues/1131))

*   Support for GWAS files with "NA" in the p-value column, e.g. some files produced by new versions of PLINK. (Git Issue [#11](https://github.com/igvteam/igv/pull/1139)[27](https://github.com/igvteam/igv/issues/1127))

*   When loading session files that included the _showGenotypes_ property for a VCF track, the track would be displayed without the genotypes even when the property was set to "true". This has now been fixed.

# IGV 2.12.x

## IGV 2.12.3 - Mar 2022

* By default, the port listener is now enabled on IGV startup. Change the setting in View > Preferences > Advanced.

## IGV 2.12.2 - Feb 2022

This release includes the following fixes:

* Sometimes tracks would not load from S3 when IGV was configured for Amazon Cognito. (Git Issue #1101)

* VCF tracks were being placed in the Annotation panel by default, rather than the Data panel. (Git Issue #1104)

* VCF tracks with only one sample did not show the genotypes section by default. (Git Issue #1104)

* Coloring of the allele frequency bars in an alignment coverage track was not taking range thresholding into account. (Git Issue #1100)

* If an annotation track was selected, you could not enter a gene name contain 'R' or 'F' in the search box; it was being interpreted as reverse/forward jump command in the feature track. 

## IGV 2.12.0 - Jan 2022

This release includes the following updates:

**New features and improvements:**

* In this release, we introduce an integration with the IGV-JBrowse Circular View application, which provides a wrapper around the JBrowse circular view component, allowing it to be used directly from within the IGV application. The interactive circular view is useful for exploring structural variants and other long-distance interactions, and can be used with a number of different track types in IGV. See this quick start guide for more details.

* Downsampling is now available when viewing interaction tracks (.BEDPE files) in whole genome view.

* Improvements for faster loading of large .BIGBED files. (Git Issue #1085)

* Session files now support a leading tilda (~) in genome and track file paths. The ~ will be replaced by the path to the user's home folder.  (Git Issue #1056)

* New batch commands to overlay tracks and separate overlaid tracks. Batch commands are documented here. (Git Issue #118)
  
  * Tools > Run Batch Script now supports selecting multiple scripts to run. They will be executed in random order.
 
  * Color by > Insert size is now availabe with appropriate defaults for RNA-seq data.
  
* The 3rd Gen preference that enables flag clipping is now on by default, with a threshold of 20 bases.

* The options to Hide small indels and Show insertion markers (primarily used for 3rd Gen sequencing data) are now available on a per-track basis from the alignment track popup menu. Previously these were only available through View > Preferences.

* Improvements to the test that determines the experiment type (RNA / 3rd Gen / Other) from aligned sequencing data.

* Added support for "Squished" mode for variants/sites in VCF tracks (previously only available for the genotypes). 

* Improvements to better support session files that were created with older versions of IGV.

**Bug fixes:**

* Sometimes a Sashimi plot would display nothing until the view had been zoomed further in. (Git Issue #1087)

* View > Fit Data to Window would reset "Type of Graph" for overlaid tracks to the Bar Chart view. (Git Issue #1082)

* The red locus indicator on the chromosome ideogram did not update when panning. (Git Issue #1096)

* Fixed issue in parsing of track name parameters in batch/port commands - the URL encoding was not being consistently decoded.

* Fixed some issues with the layout of the attribute panel that is optionally displayed between the track names and track.

* Sometimes the gene annotation track would disappear when FIle > New Session was selected.

# IGV 2.11.x

## IGV 2.11.9 - Dec 2021

This release includes the following updates:

* The Log4j dependency has been removed from IGV and replaced with java.util.logging. Note, if you have customized Log4j settings in previous versions of IGV, these customized settings are now ignored. Open an issue in the IGV GitHub repo if you need customized log settings.

*  Loading of BAM files has been optimized to alleviate bottlenecks affecting large 3rd gen seqencing files and very deep coverage files. 

* The function to Move the IGV Directory, which is invoked from View > Preferences > Advanced, now moves the IGV directory to the target directory, rather than moving the contents of the IGV directory to the target directory.


## IGV 2.11.7 - Dec 2021

This release includes the following updates:

* By default, the port listener is disabled on IGV startup. Change the setting in View > Preferences > Advanced. 
    To use web links to IGV or control IGV from other programs, you must enable the port.

* Update to use Log4j version 2.16.0. 

* Remove the "Color by insert size" option for RNA-Seq alignment tracks.  This option cannot be meaningfully implemented or interpreted for RNA-Seq data.

* Allow symbolically linked launch scripts. (Git Issue #1060)

* Save the sequence for BLAT tracks in session files. (Git Issue #1065)

## IGV 2.11.3 - Nov 2021

This release includes the following updates:

* The IGV application now starts Java with 8GB max memory by default. The previous default was 4 GB.

* Fixes a problem with loading .gwas files. (Git Issue #1048)

## IGV 2.11.2 - Oct 2021

This release fixes the following issues:

* Selecting File > New Session would delete the reference gene annotation track. (Git Issue #1038)

* For some reference genomes, entering multiple valid gene names in the search box failed to create a multi-locus view and displayed an error message reporting the loci could not be found. (Git Issue #1037)

* Saving images did not take vertical scrolling of tracks into account. For example, when viewing a BAM file, the top alignments in the track were always displayed in the image, even when the alignments in the IGV view had been scrolled to view alignments further down in the pileup. (Git Issue #1033)

* The data range setting on overlaid tracks was not restored when loading a session file. (Git Issue #1026)

* The coverage graph corresponding to an alignment track can now be assigned a color in batch scripts.  (Git Issue #993)

## IGV 2.11.1 - Sep 2021

This release includes new batch commands and bug fixes as follows:

**New batch commands**

The following new commands were added for batch and port execution. See the commands wiki page for more details

* setColor trackName colorString
* setAltColor trackName colorString
* saveSession filename

**Bug fixes**

* Fixed a problem that caused the read view of deep coverage alignment tracks to be truncated. (Git Issue #981)
* Fixed a problem that resulted in temporary preference settings from batch and port commands to be save persistently as user preferences.

## IGV 2.11.0 - Aug 2021

This release includes new features and improvements in the following areas:

**Loading data from htsget servers**

IGV now supports loading BAM, CRAM, and VCF data from htsget servers. Note BCF is not supported.
To load data from an htsget server, use File > Load from URL and enter the full URL to the resource.
For example,

* https://htsget.ga4gh.org/reads/giab.NA12878.NIST7086.1 (hg38 alignments)
* https://htsget.ga4gh.org/variants/giab.NA12878 (hg38 variants)

**Customizing a BLAT service**

IGV supports on-the-fly alignment of short sequences by making use of a BLAT web service. For example, from the popup menu in a BAM track you can select to BLAT the read sequence of the selected alignment, or you can BLAT any short sequence by selecting Tools > BLAT in the menu bar. By default, a public service hosted at UCSC is used, This can now be customized in IGV's advanced preferences to use another BLAT service, or a locally executable command line program that returns BLAT-like results.
For more details, see https://github.com/igvteam/igv/wiki/Customizing-BLAT.

**User-defined reference genomes**

Reference genomes can now be specified and loaded as JSON files, and the previous .genome format is considered deprecated. For more details, see  https://github.com/igvteam/igv/wiki/JSON-Genomes.

**Chromosome ideograms as tracks**

UCSC cytoband files can now be loaded as separate tracks via the File menu. (Git Issue #786)

**New file format**

GenePred Extended files (.genepredext) are now supported. UCSC's gff3toGenePred utility ouputs files in this format.

**New batch command**

Tracks can now be autoscaled via a batch command: setDataRange auto <track name>

**Loading data from Amazon S3 time-gated presigned urls**

All data formats are now supported when loading from S3 time-gated presigned URLs. (Git Issue #856)
See this UMCCR page for details on configuring S3 support. 

**Bug fixes**

* Fixed a problem when displaying "expanded" junction tracks for RNA-seq BAM files. (Git Issue #1018)
* Fixed a problem on Windows when trying to select a new directory for the IGV Directory in View > Preferences > Advanced.

