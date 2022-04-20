
# Track Types #

Tracks in igv.js are categorized by type.  Each type is designed to display a
particular class of genomic data, such as read alignments or annotations.
Current track types include:

Track Type | Description | Associated File Formats
---------|-------------|----------
[annotation](Annotation-Track) | Non-quantitative genome annotations such as genes. This is the most generic track type. | bed, gff, gff3, gtf, bedpe, and others
[wig](Wig-Track) | Quantitative genomic data, such as ChIP peaks and alignment coverage. | wig, bigWig, bedGraph
[alignment](Alignment-Track) | Sequencing ead alignments. | bam, cram
[variant](Variant-Track) | Genomic variants. | vcf
[seg](Seg-Track) | Segmented copy number data. | seg
mut | Mutation data, primarily from cancer studies. | [maf](https://docs.gdc.cancer.gov/Data/File_Formats/MAF_Format/), mut
[interact](https://github.com/igvteam/igv.js/wiki/Interact) | Arcs representing associations or interactions between 2 genomic loci.  | bedpe, [interact](https://genome.ucsc.edu/goldenPath/help/interact.html), bigInteract
[gwas](https://github.com/igvteam/igv.js/wiki/GWAS) | Genome wide association data (manhattan plots) | [gwas](https://software.broadinstitute.org/software/igv/GWAS), bed
arc | RNA secondary structure | [bp](https://software.broadinstitute.org/software/igv/RNAsecStructure), [bed](https://software.broadinstitute.org/software/igv/node/284)
[junction](https://github.com/igvteam/igv.js/wiki/Splice-Junctions) | RNA splice junctions | bed

# Configuring Tracks #

Tracks can be added during initial browser configuration, or via the browser
API with the `loadTrack` function. In both cases a track is configured
with an options object.  For example, the following object creates a
gene annotation track from an indexed BED file. The track will
open initially in "expanded" mode.

```JavaScript 
{
      name: "Genes",
      type: "annotation",
      format: "bed",
      sourceType: "file",
      url: "//igv.broadinstitute.org/annotations/hg19/genes/gencode.v18.collapsed.bed",
      indexURL: "//igv.broadinstitute.org/annotations/hg19/genes/gencode.v18.collapsed.bed.idx",
      displayMode: "EXPANDED"
    }
``` 


Most options can be configured with either JSON
or "plain old javascript" objects,  the exception being options that
take fuctions.

# General Track Options ##
The following properties are for all track types.

Property | Description | Default
---------|-------------|----------
type | Track type | No default. If not specified, type is inferred from file format
sourceType | Type of data source.  Valid values are "file" and "htsget" | file
format | File format | No default. If not specified format is inferred from file name extension
name | Display name (label).  **Required** |
url | URL to the track data resource, such as a file or webservice, or a [data URI](Data-URIs).  As of release 2.5.2 the url property can be a function or promise that returns or resolves to a url string.  | 
indexURL | URL to a file index, such as a BAM .bai, tabix .tbi, or tribble .idx file.  **Notes:** For indexed file access the index URL is required, if absent the entire file will be read.  As of release 2.5.2 the indexURL property can be a function or promise that resolves to a URL string.|
indexed | Flag used to indicate if a file is indexed or not.  If indexURL is provided this flag is redundant.  This flag can be used to load small BAM files without an index by setting to false|
order | Integer value specifying relative order of track position on the screen.  To pin a track to the bottom use Number.MAX_VALUE.  If no order is specified, tracks appear in order of their addition.
color | CSS color value for track features, e.g. "#ff0000" or "rgb(100,0,100)". |
height | Initial height of track viewport in pixels | 50
autoHeight | If true, then track height is adjusted dynamically, within the bounds set by minHeight and maxHeight, to accomdodate features in view | false
minHeight | Minimum height of track in pixels | 50
maxHeight | Maximum height of track in pixels | 500
visibilityWindow | Maximum window size in base pairs for which indexed annotations or variants are displayed | 1 MB for variants, 30 KB for alignments, whole chromosome for other track types  
removable | If true a "remove" item is included in the track menu. | true
headers | http headers to include with each request.  For example {"foo": "fooValue", "bar": "barValue"} |
oauthToken  | OAuth token, or function returning an OAuth token.  The value will be included as a Bearer token with each request.  See [Oauth Support](Oauth-Support) |

# Annotation Track

type = 'annotation'

## File Formats

* bed
* gff3
* gtf
* genePred
* genePredExt
* peaks
* narrowPeak
* broadPeak
* bigBed
* bedpe

## Configuration Options

Configuration options specific to annotation tracks.  All properties below are optional.

Property  | Description | Default
------ | ------- | ------------
displayMode | Annotation display mode, one of "COLLAPSED", "EXPANDED", "SQUISHED" | "COLLAPSED"
expandedRowHeight | Height of each row of features in "EXPANDED" mode | 30
squishedRowHeight | Height of each row of features in "SQUISHED" mode | 15
nameField | For GFF/GTF file formats.  Name of column 9 property to be used for feature label. | 
maxRows | Maximum number of rows of features to display | 500
searchable | If true, feature names for this track can be searched for.  Use this option with caution, it is memory intensive.  This option **will not work** with indexed tracks. | false
searchableFields | For use with the ```searchable``` option in conjunction with GFF files.  An array of field (column 9) names to be included in feature searches.  When searching for feature attributes spaces need to be escaped with a "+" sign or percent encoded ("%20). |
filterTypes | Array of gff feature types to filter from display. | ['chromosome, 'gene']
color | CSS color value for track features, e.g. "#ff0000" or "rgb(100,0,100)".  |  rgb(0,0,150)
altColor | If supplied, used for features on negative strand | 
colorBy | Used with GFF/GTF files.  Name of column 9 attribute to color features by. | |
colorTable | Used in conjunction with colorBy property.  Maps attribute values to CSS colors.  See example below. |


### colorBy example

The ```colorBy``` property takes an object specifying the name of the field to color by, used in conjunction with the ```colorTable``` property.  Fields are defined in GFF column 9.

```
{
    name: "Color by attribute biotype",
    type: "annotation",
    format: "gff3",
    displayMode: "expanded",
    height: 300,
    url: "https://s3.amazonaws.com/igv.org.genomes/hg38/Homo_sapiens.GRCh38.94.chr.gff3.gz",
    indexURL: "https://s3.amazonaws.com/igv.org.genomes/hg38/Homo_sapiens.GRCh38.94.chr.gff3.gz.tbi",
    visibilityWindow: 1000000,
    colorBy: "biotype",
    colorTable: {
       "antisense": "blueviolet",
       "protein_coding": "blue",
       "retained_intron": "rgb(0, 150, 150)",
       "processed_transcript": "purple",
       "processed_pseudogene": "#7fff00",
       "unprocessed_pseudogene": "#d2691e",
       "*": "black"
    }
},
```


### color function (igv.js version 2.10.1)

Beginning with igv.js version 2.10.1 the color and altColor properties can be specified with a function that takes a feature object
as an argument and returns a CSS color string (e.g. "blue", "rgb(0,150,150)",  "#d2691e").   

Example

```
{
    name: "Color by function",
    format: "gff3",
    displayMode: "expanded",
    height: 300,
    url: "https://s3.amazonaws.com/igv.org.genomes/hg38/Homo_sapiens.GRCh38.94.chr.gff3.gz",
    indexURL: "https://s3.amazonaws.com/igv.org.genomes/hg38/Homo_sapiens.GRCh38.94.chr.gff3.gz.tbi",
    visibilityWindow: 1000000,
    color: (feature) => {
        switch (feature.getAttributeValue("biotype")) {
            case "antisense":
                return "blueviolet"
            case "protein_coding":
                return "blue"
            case "retained_intron":
                return "rgb(0, 150, 150)"
            case "processed_transcript":
                return "purple"
            case "processed_pseudogene":
                return "#7fff00"
            case "unprocessed_pseudogene":
                return "#d2691e"
            default:
                return "black"
        }
    }
}
```

The feature object passed to the color function is described below


```javascript
{
  chr: chr,
  start: integer,   
  end: integer,
  name: string
  score: float,
  strand: string,
  cdStart: integer,
  cdEnd: integer,
  color: string,
  exons: array
  getAttributeValue(attributeName): function -- returns value of a GFF/GTF column 9 attribute
}

\\ Exon array
[
{
  start: integer,
  end: integer,
  cdStart: integer,
  cdEnd: integer,
  utr: boolean
}
]
```
# Alignment Track

type = 'alignment'

## Configuration Options

Property  | Description | Default
------ | ------- | ------------
viewAsPairs | If true, paired reads are drawn connected with a line.  | false
pairsSupported | If false, mate information in paired reads is ignored during downsampling and the 'View as Pairs' option is removed from the alignment track menu. | true
coverageColor | Color of coverage track | rgb(150, 150, 150)
color | Default color of alignment blocks | rgb(170, 170, 170)
deletionColor | Color of line representing a deletion | black
skippedColor | Color of line representing a skipped region (e.g. splice junction) | rgb(150, 170, 170)
insertionColor | Color of marker for insertions |  rgb(138, 94, 161)
negStrandColor | Color of alignment on negative strand.  Applicable if colorBy = "strand" | rgba(150, 150, 230, 0.75)
posStrandColor  | Color of alignment or position strand.  Applicable if colorBy = "strand" | rgba(230, 150, 150, 0.75)
pairConnectorColor | Color of connector line between read pairs ("view as pairs" mode).  Optional. | alignment color
colorBy | Alignment color option:  one of "none", "strand", "firstOfPairStrand", "pairOrientation", "tlen", "unexpectedPair", or "tag".  If colorBy = "tag" specify tag with colorByTag | "unexpectedPair"
colorByTag | Specific tag to color alignment by.  |
bamColorTag | Specifies a special tag that explicitly encodes an r,g,b color value.  Default value is "YC".  If "YC" does not encode an r,g,b color value set bamColorTag to null.  Must also set "colorBy" to "tag" to enable this option.  | "YC"
samplingWindowSize | Window (bucket) size for alignment downsampling in base pairs | 100
samplingDepth | Number of alignments to keep per bucket.  WARNING:  Setting this sampling depth to a high value will likely freeze the browser when viewing areas of deep coverage. | 100.
alignmentRowHeight | Height in pixels of an alignment row when in expanded mode | 14
readgroup | Readgroup ID value (tag 'RG').  |
sort | Initial sort option.  See table below. |
showSoftClips | Show soft-clipped regions | false
showMismatches | Highlight alignment bases which do not match the reference | true

### Paired-end and mate-pair coloring options

Property | Description | Default
-------- | ----------- | -------
pairOrientation | Expected orientation of pairs, one of ff, fr, or rf.  | Computed
minTLEN | Minimum expected absolute "TLEN" value.  Pairs below this value are colored blue if colorBy == "tlen" or "unexpectedPair" | 
maxTLEN | Maximum expected absolute "TLEN" value.   Pairs above this value are colored red if colorBy == "tlen" or "unexpectedPair" | Computed
minTLENPercentile | The percentile threshold for expected insert size.  If minTLEN is not specified this value is used to compute one. See notes below. | 0.1
maxTLENPercentile | The percentile maximum for expected insert size.  If maxTLEN is not specified this value is used to compute one. See notes below.| 99.9


If minTLEN or maxTLEN are not specified a value is computed from a sampling of the first data loaded for the track.  Specifically, the values are taken from a percentile of the sample data as specified by minPercentile and maxPercentile.  It is possible to specify an explicit value for one.

!!! note 
    TLEN refers to column 9 of an alignment record from the SAM specification. It has variously been called "template length", "insert size", and "fragment length". There is no agreement on a precise definition, and aligner interpretations differ, but generally it can be thought of as the distance between start and end of an aligned pair.   Pairs with TLEN outside the expected range can be indicative of a deletion, or more rarely and insertion.

### Sort options

Property | Description | Default
-------- | ----------- | -------
chr  | Sequence (chromosome) name  |
position    | Genomic position (integer) |
option   | Parameter to sort by.  One of 'BASE', 'STRAND', 'INSERT_SIZE', 'MATE_CHR', 'MQ', 'TAG' | 
tag      | Tag name to sort by.  Include only if option = 'TAG |   
direction | Sort directions.  ASC = ascending, DESC = descending | "ASC"

!!! note 
    Prior to release 2.7.0, the "position" property was named "locus", and 'BASE' was named 'NUCELOTIDE'

### Example: BAM file on Google Cloud Storage

```javascript
{
  type: "alignment",
  format: "bam",
  name: "NA12889",
  url: "gs://genomics-public-data/platinum-genomes/bam/NA12878_S1.bam",
  indexURL: "gs://genomics-public-data/platinum-genomes/bam/NA12878_S1.bam.bai",
  sort: {
    chr: "chr1",
    position: 155155358
    option": "BASE",
    direction: "ASC"
  }
}
```



### Example: [htsget](http://samtools.github.io/hts-specs/htsget.html) resource

Available in igv.js versions > 2.9.0

```javascript
{
   type: 'alignment',
   sourceType: 'htsget',
   format: 'bam',
   url: 'https://htsget.ga4gh.org/reads/giab.NA12878.NIST7086.1',
   name: 'NA12878'
}
```
