# Command Line Options

``` igv.sh [flags] [file]```

## flags

```
-o --preferences    File path or URL to a users preferences property file

-b --batch    File path or URL to a batch command file

-p --port    Port number for IGV command listener (default 60151)

-g --genome    Genome ID, file path, or URL to a .genome or indexed fasta file

-d --dataServerURL   File path or URL to a data server configuration file

-u --genomeServerURL   File path or URL to a genome server configuration file

-i --indexFile   File path or URL to an index file, or comma delimited list of index files, corresponding to the file parameter

-n --name    Track name corresponding to the file parameter

-l --locus   Initial locus

-H --header   HTTP header to include with all data requests

--igvDirectory    Full path to the igv directory (defaults to <user home>/igv

--version    Print the igv version to stdout

--help    Print this description to stdout

file File path or url, or space delimited list of file paths or urls, to data files to load on startup

```

Example -- supply an oAuth token for a Google hosted file
```
igv.sh  -H "Authorization: Bearer <token>" gs://genomics-public-data/platinum-genomes/bam/NA12877_S1.bam
```
