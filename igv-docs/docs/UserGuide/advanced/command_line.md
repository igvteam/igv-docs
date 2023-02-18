
<!---
The page title should not go in the menu
-->
<p class="page-title"> IGV from the command line </p>

The [Download IGV](../../downloadPage.md) page includes an option to download a version of IGV that includes scripts for launching it on the command line, as well as launching the igvtools utilities. 

# The IGV application

### Usage

``` 
igv.sh [flags] [file]
```

* **file** 
 
    * Optional file path or URL, or space delimited list of file paths or URL, to data files to load on startup

* **flags**

    * ```-o --preferences```    File path or URL to the user's preferences property file

    * ```-b --batch```   File path or URL to a batch command file

    * ```-p --port```    Port number for IGV command listener (default 60151)

    * ```-g --genome```    Genome ID, file path, or URL to a .genome or indexed FASTA file

    * ```-d --dataServerURL```   File path or URL to a data server configuration file

    * ```-u --genomeServerURL```   File path or URL to a genome server configuration file

    * ```-i --indexFile```   File path or URL to an index file, or comma delimited list of index files, corresponding to the file parameter

    * ```-n --name```    Track name corresponding to the file parameter

    * ```-l --locus```   Initial locus

    * ```-H --header```   HTTP header to include with all data requests

    * ```--igvDirectory```    Full path to the *igv* directory (default *<user home\>/igv*)

    * ```--version```    Print the IGV version to stdout

    * ```--help```    Print this description to stdout


### Example 
Supply an oAuth token for a Google hosted file:
```
igv.sh  -H "Authorization: Bearer <token>" gs://genomics-public-data/platinum-genomes/bam/NA12877_S1.bam
```

# igvtools

igvtools provides a number of utilities to preprocess data files.

### Launching the scripts

The igvtools utilities can be invoked, with or without the graphical user interface (GUI), from one of the following
scripts:

* _igvtools_ - MacOS and Linux command-line version 

* _igvtools\_gui_ - MacOS and Linux GUI version 

* _igvtools\_gui.command_ - MacOS alternate double-clickable GUI version 

* _igvtools.bat_ - Windows command-line version 
 
* _igvtools\_gui.bat_ - Windows GUI version 

The **GUI version** is launched without any options or arguments. Once it has been launched, everything is the same as when you run *igvtools* from the IGV interface. See [igvtools in the Tools Menu](../../tools/igvtools_ui) for more information.

The general form of the **command-line version** is:

```
igvtools [command] [options] [arguments]
```
```
igvtools.bat [command] [options] [arguments]
```

Recognized tools, options, arguments, and file types are described below.

#### Memory settings

The igvtools scripts allocate a fixed amount of memory. If this is more than the amoount available on your platform, you
will get an error along the lines of "Could not start the Virtual Machine". If this happens you will need to edit the
scripts to reduce the amount of memory requested, or use the option to start igvtools directly with Java (see below). The memory is set via a ```-Xmx```
parameter. For example  ```-Xmx1500m```requests 1500 MB,  ```-Xmx1g``` requests 1 gigabyte.


### Launching with Java

!!! note " "
    The command line has become more complex with Java 11 compared to Java 8. We recommend the scripts above for most users.

igvtools can also be started directly using Java. This option allows more control over Java parameters, such as the
maximum memory to allocate. In the example shown below, igvtools is started with 1500 MB of memory allocated and
launched in the location where you have unpacked igvtools.

```
java -Xmx1500m --module-path=lib @igv.args --module=org.igv/org.broad.igv.tools.IgvTools [command] [options] [arguments]
```

To start with a GUI the command is

```
java -Xmx1500m --module-path=lib @igv.args --module=org.igv/org.broad.igv.tools.IgvTools gui
```

For more information about **other settings**, see the downloaded file _igvtools\_readme.txt._

### Commands

igvtools includes the following commands: [sort](./#sort), [index](./#index), [count](./#count), [toTDF](./#totdf), and [version](./#version).  

#### **sort**

Sorts a file by start position.

```
igvtools sort [options] [inputFile] [outputFile]
```
* **inputFile** 

    * Required argument.
    
    * Supported input file formats are: .cn, .igv, .sam, .bam, .aligned, .psl, .bed, and .vcf.

* **outputFile**

    * Required argument

    * The special string "stdout" can be used as *outputFile*, in which case the output will be written to the standard output stream instead of a file.

* **options**

    * ```-t tmpdir``` Specify a temporary working directory. For large input files this directory will be used to store intermediate results of the sort. The default is the user's temp directory.

    * ```-m maxRecords``` The maximum number of records to keep in memory during the sort. The default value is 500000. Increase this number if
you receive "too many open files" errors. Decrease it if you experience "out of memory" errors.

#### **index**

Creates an index for an alignment or feature file. Index files are required for loading alignment files into IGV, and
can significantly improve performance for large feature files. Note that the index file is not directly loaded into IGV.
Rather, IGV looks for the index file when the alignment or feature file is loaded. This command does not take an output
file argument. Instead, the filename is generated by appending ".sai" (for alignments) or ".idx" (for features) to the
input filename as IGV relies on this naming convention to find the index. 


```
igvtools index [inputFile]
```

* **inputFile**

    * Required argument

    * Supported input file formats are: .sam, .bam, .aligned, .vcf, .psl, and .bed.

    * The input file must be sorted by start position (see *sort* command).

!!! note " "
    The "sai" index is an IGV format, it does not work with samtools or any other application.


#### **count**

Computes average feature density over a specified window size across the genome. Common usages
include computing coverage for alignment files and counting hits in ChIP-seq experiments. By default, the resulting file
will be displayed as a bar chart when loaded into IGV.

```
igvtools count [options] [inputFile] [outputFile] [genome]
```

* **inputFile**

    * Required argument

    * Supported input file formats are: .sam, .bam, .aligned, .psl, .pslx, and .bed

    * The input file must be sorted by start position. See the _sort_ command.

* **outputFile**

    * Required argument

    * The output filename must end in .tdf or ".wig", or be the special string "stdout". To indicate that you want to output both a .tdf and a .wig file, list both output filenames as a single string, separated by a comma with no other delimiters. If the output file is named "stdout" the output will be written to the standard output stream in .wig format.

* **genome** 
    * A genome id or path to a [.chrom.sizes](http://www.broadinstitute.org/software/igv/chromSizes) or .genome file.

    * Default is hg18.

* **Options:**

    * ```-z, --maxZoom num``` Specifies the maximum zoom level to precompute.

    * ```-w, --windowSize num``` The window size over which coverage is averaged. Defaults to 25 bp.

    * ```-e, --extFactor num``` The read or feature is extended by the specified distance in bp prior to counting. This option is useful for chip-seq
and rna-seq applications. The value is generally set to the average fragment length of the library minus the average
read length.

    * ```--preExtFactor num``` The read is extended upstream from the 5' end by the specified distance.

    * ```--postExtFactor num``` Effectively overrides the read length, defines the downstream extent from the 5' end. Intended for use with *preExtFactor*.

    * ```-f, --windowFunctions list``` A comma delimited list specifying window functions to use when reducing the data to precomputed tiles. Possible values are min, max, mean, median, p2, p10, p90, and p98. The "p" values represent percentile, so p2=2nd percentile, etc.

    * ```--strands [arg]``` By default, counting is combined among both strands. This setting outputs the count for each strand separately. Legal argument values are 'read' or 'first'. 'read' Separates count by 'read' strand, 'first' uses the first in pair strand". Results are saved in a separate column for .wig output, and a separate track for TDF output.

    * ```--bases``` Count the occurrence of each base (A,G,C,T,N). Takes no arguments. Results are saved in a separate column for .wig output, and a separate track for TDF output.

    * ```--query [querystring]``` Only count a specific region. Query string has syntax <chr>:<start>-<end>. e.g. chr1:100-1000. Input file must be indexed.

    * ```--minMapQuality [mqual]``` Set the minimum mapping quality of reads to include. Default is 0.

    * ```--includeDuplicates``` Include duplicate alignments in count. Default false. If this flag is included, duplicates are counted. Takes no arguments

    * ```--pairs``` Compute coverage from paired alignments counting the entire insert as covered. When using this option only reads marked "proper pairs" are used.

**Example:**

```
igvtools count -z 5 -w 25 -e 250 alignments.bam alignments.cov.tdf hg18
```

#### **toTDF**

Converts a sorted data input file to a binary tiled data (.tdf) file. Use this command to
pre-process large datasets for improved IGV performance. This tool was previously known as _tile_.

```
igvtools toTDF [options] [inputFile] [outputFile] [genome]
```

* **inputFile** 

    * Required argument

    * Supported input file formats are: .wig, .cn, .snp, .igv, and .gct

    * Input files, with the exception of .gct files, must be sorted by start position. Files can be sorted with the _sort_ command. Attempting to preprocess an unsorted file will result in an error.

    
* **outputFIle**

    * Must end in ".tdf".

* **genome**

    * A genome id or path to a [.chrom.sizes](http://www.broadinstitute.org/software/igv/chromSizes) or .genome file.

    * Default is hg18.

* **Options:**

    * ```-z num``` Specifies the maximum zoom level to precompute. The default value is 7 and is sufficient for most files. To reduce file size at the expense of IGV performance this value can be reduced.

    * ```-f list``` A comma delimited list specifying window functions to use when reducing the data to precomputed tiles. Possible values are min, max, and mean. By default only the mean is calculated.

    * ```-p file``` Specifies a .bed file to be used to map probe identifiers to locations. This option is useful when preprocessing .gct files. The .bed file should contain 4 columns: chr start end name where name is the probe name in the .gct file.

**Example:**

```
igvtools toTDF -z 5 copyNumberFile.cn copyNumberFile.tdf hg18
```
    
#### **version**

Prints the igvtools version number to the console.

```
igvtools version
```
