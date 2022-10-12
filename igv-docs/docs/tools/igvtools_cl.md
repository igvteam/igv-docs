**Downloading igvtools**

The igvtools utilities can be downloaded from the [_Downloads_](http://www.broadinstitute.org/software/igv/download)
page on the IGV website.

**Starting with shell scripts**

The igvtools utilities can be invoked, with or without the graphical user interface (GUI), from one of the following
scripts:

_igvtools_ (command-line version for Linux and MacOS 10.x)  
_igvtools\_gui_ (GUI version for Linux and MacOS 10.x)  
_igvtools\_gui.command_ (alternate double-clickable GUI version for MacOS 10.x)

_igvtools.bat_ (command-line version for Windows)  
_igvtools\_gui.bat (_GUI version for Windows)

Once the GUI version has been launched, the commands and options are the same as when
you [run igvtools from the IGV interface](igvtools_ui.md).

The general form of the command-line version is:

_igvtools \[command\] \[options\]\[arguments\] --_or--     _igvtools.bat \[command\] \[options\]\[arguments\]_

Recognized commands, options, arguments, and file types are described below.

**Starting with Java**

igvtools can also be started directly using Java. This option allows more control over Java parameters, such as the
maximum memory to allocate. In the example shown below, igvtools is started with 1500 MB of memory allocated and
launched in the location where you have unpacked IGVTools.

_java -Xmx1500m --module-path=lib @igv.args --module=org.igv/org.broad.igv.tools.IgvTools \[command\]
\[options\]\[arguments\]_

To start with a GUI the command is

_java -Xmx1500m --module-path=lib @igv.args --module=org.igv/org.broad.igv.tools.IgvTools gui_

Note that the command line has become more complex with Java 11 compared to Java 8. We recommend the shell scripts above
for most users.

**Memory settings**

The igvtools scripts allocate a fixed amount of memory. If this is more than the amoount available on your platform, you
will get an error along the lines of "Could not start the Virtual Machine". If this happens you will need to edit the
scripts to reduce the amount of memory requested, or use the Java startup option. The memory is set via a "-Xmx"
parameter. For example  _-Xmx1500m_ requests 1500 MB,  _-Xmx1g_ requests 1 gigabyte.

For more information about **other settings**, see the downloaded file _igvtools\_readme.txt._

Commands
========

toTDF
-----

The _toTDF_ command converts a sorted data input file to a binary tiled data (.tdf) file. Use this command to
pre-process large datasets for improved IGV performance.

Supported input file formats are: .wig, .cn, .snp, .igv, and .gct.

**Note:** This tool was previously known as _tile_

**Usage:**

igvtools toTDF \[options\] \[inputFile\] \[outputFile\] \[genome\]

**Required arguments:**

inputFile The input file (see supported formats above).

outputFile Binary output file. Must end in ".tdf".

genome A genome id or path to a [.chrom.sizes](http://www.broadinstitute.org/software/igv/chromSizes) or .genome file.
Default is hg18.

**Options:**

-z num

Specifies the maximum zoom level to precompute. The default value is 7 and is sufficient for most files. To reduce file
size at the expense of IGV performance this value can be reduced.

-f list

A comma delimited list specifying window functions to use when reducing the data to precomputed tiles. Possible values
are min, max, and mean. By default only the mean is calculated.

\-p file

Specifies a .bed file to be used to map probe identifiers to locations. This option is useful when preprocessing . gct
files. The .bed file should contain 4 columns:  
chr start end name  
where name is the probe name in the .gct file.

**Example:**

_igvtools toTDF -z 5 copyNumberFile.cn copyNumberFile.tdf hg18_

**Notes:**

Data file formats, with the exception of .gct files, must be sorted by start position. Files can be sorted with the _
sort_ command described below. Attempting to preprocess an unsorted file will result in an error.

Count
-----

The _count_ command computes average feature density over a specified window size across the genome. Common usages
include computing coverage for alignment files and counting hits in ChIP-seq experiments. By default, the resulting file
will be displayed as a bar chart when loaded into IGV.

Supported input file formats are: .sam, .bam, .aligned, .psl, .pslx, and .bed.

**Usage:**

igvtools count \[options\] \[inputFile\] \[outputFile\] \[genome\]

**Required arguments:**

inputFile The input file (see supported formats above).

outputFile The output file, which can be binary .tdf or ASCII .wig format.

The output filename must end in ".tdf" or ".wig", or be the special string "stdout". To indicate that you want to output
both a .tdf and a .wig file, list both output filenames as a single string, separated by a comma with no other
delimiters. If the output file is named "stdout" the output will be written to the standard output stream in .wig
format.

genome A genome id or path to a [.chrom.sizes](http://www.broadinstitute.org/software/igv/chromSizes) or .genome file.
Default is hg18.

**Options:**

\-z, --maxZoom num

Specifies the maximum zoom level to precompute.

\-w, --windowSize num

The window size over which coverage is averaged. Defaults to 25 bp.

-e, --extFactor num

The read or feature is extended by the specified distance in bp prior to counting. This option is useful for chip-seq
and rna-seq applications. The value is generally set to the average fragment length of the library minus the average
read length.

\--preExtFactor num

The read is extended upstream from the 5' end by the specified distance.

\--postExtFactor num

Effectively overrides the read length, defines the downstream extent from the 5' end. Intended for use with
preExtFactor.

\-f, --windowFunctions list

A comma delimited list specifying window functions to use when reducing the data to precomputed tiles. Possible values
are min, max, mean, median, p2, p10, p90, and p98. The "p" values represent percentile, so p2=2nd percentile, etc.

\--strands \[arg\]

By default, counting is combined among both strands. This setting outputs the count for each strand separately. Legal
argument values are 'read' or 'first'. 'read' Separates count by 'read' strand, 'first' uses the first in pair strand".
Results are saved in a separate column for .wig output, and a separate track for TDF output.

\--bases

Count the occurrence of each base (A,G,C,T,N). Takes no arguments. Results are saved in a separate column for .wig
output, and a separate track for TDF output.

\--query \[querystring\]

Only count a specific region. Query string has syntax <chr>:<start>-<end>. e.g. chr1:100-1000. Input file must be
indexed.

\--minMapQuality \[mqual\]

Set the minimum mapping quality of reads to include. Default is 0.

\--includeDuplicates

Include duplicate alignments in count. Default false. If this flag is included, duplicates are counted. Takes no
arguments

\--pairs

Compute coverage from paired alignments counting the entire insert as covered. When using this option only reads
marked "proper pairs" are used.

**Example:**

_igvtools count -z 5 -w 25 -e 250 alignments.bam alignments.cov.tdf hg18_

**Notes:**

The input file must be sorted by start position. See the _sort_ command below.

Index
-----

Creates an index for an alignment or feature file. Index files are required for loading alignment files into IGV, and
can significantly improve performance for large feature files. Note that the index file is not directly loaded into IGV.
Rather, IGV looks for the index file when the alignment or feature file is loaded. This command does not take an output
file argument. Instead, the filename is generated by appending ".sai" (for alignments) or ".idx" (for features) to the
input filename as IGV relies on this naming convention to find the index . The input file must be sorted by start
position (see sort command, below).

Supported input file formats are: .sam, .bam, .aligned, .vcf, .psl, and .bed.

**Usage:**

igvtools index \[inputFile\]

**Notes**:

The "sai" index is an IGV format, it does not work with samtools or any other application.

Sort
----

Sorts the input file by start position, as required.

Supported input file formats are: .cn, .igv, .sam, .bam, .aligned, .psl, .bed, and .vcf.

**Usage:**

igvtools sort \[options\] \[inputFile\] \[outputFile\]

**Required arguments:**

inputFile

outputFile

The special string "stdout" can be used as \[outputFile\], in which case the output will be written to the standard
output stream instead of a file.

**Options:**

-t tmpdir

Specify a temporary working directory. For large input files this directory will be used to store intermediate results
of the sort. The default is the users temp directory.

-m maxRecords

The maximum number of records to keep in memory during the sort. The default value is 500000. Increase this number if
you receive "too many open files" errors. Decrease it if you experience "out of memory" errors.

Version
-------

Prints the igvtools version number to the console.