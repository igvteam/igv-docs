
Command	| Parameters | Description
------- | ----------- | ----------
collapse | trackName | 	Collapses a given track. trackName is optional, if it is not supplied all tracks are collapsed.
colorBy | option tagName | Sets the "color by" option for alignment tracks.  For option "TAG" also specify the tag name.
echo	| | Writes "echo" back to the response, primarily for testing port connections.
exit	| | Exit (close) the IGV application.
expand | trackName |	Expands a given trackName. trackName is optional, however, and if it is not supplied all tracks are expanded.
genome | genomeIdOrPath |	Selects a genome by id, or loads a genome (or indexed fasta) from the supplied path.
goto | locus or listOfLoci |	| Scrolls to a single locus or a space-delimited list of loci. If a list is provided, these loci will be displayed in a split screen view.  Use any syntax that is valid in the IGV search box.  
group |  option tagName |	Alignment tracks only.   Group alignments by the specified option.  See below for valid option values.  For option "TAG" also specify the tag name.
load |  file |	Loads data or session files.  Specify a comma-delimited list of full paths or URLs. To explicitly specify a path to an index file use the optional "index=" parameter.  load foo.bam index=bar.bai
maxPanelHeight | height | 	Sets the number of vertical pixels (height) of each panel to include in image. Images created from a port command or batch script are not limited to the data visible on the screen. Stated another way, images can include the entire panel not just the portion visible in the scrollable screen area. The default value for this setting is 1000, increase it to see more data, decrease it to create smaller images.  To capture the exact area visible on the screen set this value to -1.
new | |	Create a new session. Unloads all tracks except the default genome annotations.
preference|  key value | 	Temporarily set the preference named key to the specified value. This preference only lasts until IGV is shut down. The complete set of preference keys are listed in the file "preferences.tab" [here](https://raw.githubusercontent.com/igvteam/igv/master/src/main/resources/org/broad/igv/prefs/preferences.tab).  The first column is the key, the third column is the value type.  For ```select``` value types the permitted values follow as a list delimited by the character "\|".
region | chr start end	| Defines a region of interest bounded by the two loci (e.g., region chr1 100 200).
setLogScale  
setSleepInterval|  ms |	Sets a delay (sleep) time in milliseconds.  The sleep interval is invoked between successive commands.
snapshotDirectory | path	| Sets the directory in which to write images.
snapshot | filename	| Saves a snapshot of the IGV window to an image file.  If filename is omitted, writes a PNG file with a filename generated based on the locus.  If filename is specified, the filename extension determines the image file format, which must be either .png or .svg.
sort | option locus | Sorts alignment or segmented copy number tracks.  See below for valid option values.  If supplied,  the locus option can define a single position, or a range.  If absent sorting will be based on the region in view for segmented copy number, or the center position of the region in view for alignment tracks.
squish | trackName | 	Squish a given trackName. trackName is optional, and if it is not supplied all annotation tracks are squished.
viewaspairs | trackName | 	Set the display mode for an alignment track to "View as pairs".  trackName is optional.

### ColorBy option values

* BISULFITE
* FIRST_OF_PAIR_STRAND
* INSERT_SIZE
* LIBRARY
* LINK_STRAND
* MAPPED_SIZE
* MOVIE
* NOMESEQ
* NONE
* PAIR_ORIENTATION
* READ_GROUP
* READ_STRAND
* SAMPLE
* TAG
* UNEXPECTED_PAIR
* YC_TAG
* ZMW

### Group option values

* BASE_AT_POS <locus>
* FIRST_OF_PAIR_STRAND
* HAPLOTYPE
* LIBRARY
* MATE_CHROMOSOME
* MOVIE
* NONE
* PAIR_ORIENTATION
* PHASE
* READ_GROUP
* READ_ORDER
* REFERENCE_CONCORDANCE
* SAMPLE
* STRAND
* SUPPLEMENTARY
* TAG
* ZMW

### Sort option values

#### Segmented copy number 

* AMPLIFICATION
* DELETION

#### Alignments

* BASE 
* FIRSTOFPAIRSTRAND
* INSERSTSIZE
* MATECHR
* POSITION
* QUALITY
* READGROUP
* READORDER
* READNAME
* SAMPLE
* STRAND
