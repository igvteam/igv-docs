<font size=18 color=#546e7a>igv.js Developer Guide</font>

# IGV Browser Object #

## Browser Creation     

The `igv.createBrowser` function is used to create an igv Browser object and insert it into your dom.  The function takes two arguments: (1) The parent element (usually a div); the browser object will be inserted into the DOM as a child of this element, and (2) A configuration object that defines the browser's initial state. 'igv.createBrowser' returns a promise which resolves with the browser upon completion.  The browser object should be saved by the client program for future calls to the API. 

The configuration object can be JSON, or a literal object.   In most cases these are equivalent, however configuration options which accept a function can only be specified with an object.

The example below creates an igv browser initialized with the hg19 reference genome.  

```JavaScript
    const options = {
            genome: "hg19";
        };

         igv.createBrowser(div, options) 
              .then(function (browser) {
                   // browser is initialized and can now be used
               });
```
!!! note 
	The global singleton instance "igv.browser" is no longer created by the createBrowser function. If needed this object can be created as follows.

```js
igv.createBrowser(div, options).
    then(function (browser) {
        igv.browser = browser;
   });
``` 

## Browser Removal

To remove an igv browser instance call

```
igv.removeBrowser(browser)
```
To remove all igv browsers

```
igv.removeAllBrowsers()
```


## Browser Configuration Options ##
The object that configures the browser's initial state includes details for the reference genome, track default settings, the initial set of loaded tracks, and the initial view locus. It also controls some aspects of the user interface.  All fields are optional except one of either **genome** or **reference**.

Option  | Description | Default
------ | ------- | ------------
genome | String identifier defining genome (e.g. "hg19").  See [Reference Genome](Reference-Genome) for details and list of supported identifiers. **Note: One (but only one) of either _genome_ or _reference_ properties must be set.**
reference | Object defining reference genome.  See [Reference Genome](Reference-Genome) for details. **Note: One (but only one) of either _genome_ or _reference_ properties must be set.**|
doubleClickDelay | Maximum between mouse clicks in milliseconds to trigger a double-click | 500
flanking  | Distance (in bp) to pad sides of gene  on successful search by gene or other annotation. | 1000
genomeList | **OPTIONAL.**  _Release 2.0.2._   URL to a json file containing an array of genome reference definitions, _or_ an inline json array.  Genomes can be specified from the list by ID with the "genome" property.  Default value is [https://s3.amazonaws.com/igv.org.genomes/genomes.json](https://s3.amazonaws.com/igv.org.genomes/genomes.json) **NOTE: the genomeList is globally shared by all igv browser instances on a page.** |
locus | Initial genomic location(s).  Either a string or an array of strings.  If an array a viewport is created for each location. | 
minimumBases | Minimum window size in base pairs when zooming in | 40
queryParametersSupported | If true support initialization by query parameters. | false
search | Object defining a web service for supporting search by gene or other annotation.  See object details below.  Optional.   Current a default service is provided for human (hg19, hg38) and mouse (mm10 assemblies. |
showAllChromosomes | Show all chromosome (sequences) in the pulldown control irrespective of size.  Set to false to filter sequences < 1/50 the mean length. | true
showChromosomeWidget | Show a chromosome (sequence) pulldown control. | true
showNavigation | Show basic navigation controls (search, zoom in, zoom out). | true
showSVGButton | Show button that saves browser as SVG file. | true
showRuler | Show a genomic ruler track. | true
showCenterGuide | Show a pair of vertical lines, or single line when zoomed out, framing the base position at the center of view | false
showCursorTrackGuide | Show a vertical line that follows the cursor | false
trackDefaults |  Embedded object defining default settings for specific track types (see table below). |
tracks | Array of configuration objects defining tracks initially displayed when app launches. |
roi | Array of track-like configuration objects defining regions of interest.  These regions will be overlaid on all tracks. |
oauthToken | oauth access token |
apiKey | Google API key.  Optional |
clientId | Google client ID.  Optional.  |
genomeList | An array of genome json objects, or url to an array of genome json objects.  If present genomes can be specified by id with the ```genome``` field above.  This list is added to the igv.js default list unless ```loadDefaultGenomes: false``` |
loadDefaultGenomes | Boolean indicating whether or not the igv.js default genome list should be loaded.  | true 
nucleotideColors | Color table for nucleotides in sequence an bam tracks.  Object with keys "A", "C", "T", "G", and "N" | 
showSampleNames | Controls display of sample names for track types that support them (VCF with genotypes, SEG, and MUT) |

### _search_ object details

The search object defines a webservice for fetching genomic location given a gene name or other symbol.  The service should return a JSON object with the following structure.  The results array is an array of objects with a chromosome, start, and end field.  The names of these fields are specified in the configuration object.   The end field is optional, if not included end = start + 1.

    {
      <resultsField> : <array of results>
    }

Option  | Description | Default
------ | ------- | ------------
url | URL to search service.  The URL must include the string $FEATURE$.  This string will be replaced by the symbol being queried.  if the URL contains the string $GENOME$ is will be replaced by the current genome ID. |
resultsField | JSON field name for property containing the array of results.  | Treats the response as an array of results.
coords | Indicates genomic coordinate convention used. Possible values are 0 and 1 | 1
chromosomeField | JSON field name for the chromosome property | chromosome
startField | JSON field name for the start position property | start
endField | JSON field name for the end position property | end

The results array contain objects with chromosome, start, and end fields named as specified above.  The type of the chromosome field is string, the type of start and end fields is integer.

E.g. a search for TP53 against hg19 using the defaults should look like this:

    [{"chromosome":"chr17","start":7572927,"end":7579912}]
    
The reference genome must be defined by specifying either the _reference_ object or _genome_ identifier for hosted genomes.  These are mutually exclusive options, do not specify both.

### _genome_ property

igv.js supports a number of genome references,  see [genomes.json](https://s3.amazonaws.com/igv.org.genomes/genomes.json)
for the current list. 
 
``` javascript
{
  ...
  genome: "hg19",
  ...
}
```


### _reference_ object 

To define or customize a reference genome the reference property can be used.  

#### Example

```javascript
{
  ...

  reference: {
    "id": "hg38",
    "name": "Human (GRCh38/hg38)",
    "fastaURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa",
    "indexURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa.fai",
    "cytobandURL": "https://s3.amazonaws.com/igv.broadinstitute.org/annotations/hg38/cytoBandIdeo.txt",
    "tracks": [
      {
        "name": "Refseq Genes",
        "url": "https://s3.amazonaws.com/igv.org.genomes/hg38/refGene.txt.gz",
        "order": 1000000,
        "indexed": false
      }
    ]
  }
  ...
}
```

### Details

All properties except fastaURL are optional.   An index is highly recommended if the fasta is > a few mb in size.   Loading a large fasta file without an index is likely to freeze the browser.

Option  | Description | Default
------ | ------- | ------------
id | UCSC or other id string.  _Optional_ |
name | A descriptive name.  _Optional_ |
fastaURL | URL to a FASTA file. **Required**. |
indexURL | URL to a FASTA index (.fai file).  An index file is optional, but if not supplied the entire fasta is read. | 
cytobandURL | URL to a cytoband ideogram file in UCSC format.  _Optional_  |
aliasURL | URL to a tab-delimited file defining aliases for chromosome names  (e.g. "1" <-> "chr1",  "MT" <-> "chrM", etc).  File should have 1 line per chromosome with all names for the chromosome listed, in arbitrary order.   _Optional_ |
indexed | Flag indicating if the FASTA is indexed.  Ignored if indexURL is supplied.  The primary purpose of this property is to indicate that the fasta is not indexed.  _Optional_ |
tracks | A list of tracks to be loaded with the genome.  See the [Tracks](#tracks) description for details.  _Optional_
chromosomeOrder | **Release 2.2** An array of chromosome names defining the order in the whole genome view and chromosome pulldown selector, if used.   _Optional_
headers | http headers to include with each request. For example {"authorization": "bearer: token"}.  _Optional_ |
wholeGenomeView | Construct a "whole genome" view from the individual sequences.  This is useful for finished assemblies with a few (< 50) large chromosomes.  Its not useful for assemblies with a single or conversely thousands of sequences. _Optional_ |  true

# Browser API #

After initialization, the browser can be controlled using the functions described below. 

* [loadGenome(config)](#loadgenomeconfig)
* [loadSessionObject(session)](#loadsessionobjectsession)
* [loadSession({url})](#loadsessionurl)
* [loadTrack(config)](#loadtrackconfig)
* [findTracks(propertyOrFunction, value)](#findtrackspropertyorfunction-value)
* [removeTrackByName(name)](#removetrackbynamename)
* [removeTrack(track)](#removetracktrack)
* [loadROI(configOrArray)](#loadroiconfigorarray)
* [clearROIs()](#clearrois)
* [search(symbol)](#searchsymbol)
* [zoomIn()](#zoomin)
* [zoomOut()](#zoomout)
* [currentLoci()](#currentloci)
* [visibilityChange()](#visibilitychange)
* [toJSON()](#tojson)
* [compressedSession()](#compressedsession)
* [toSVG()](#tosvg)
* [setCustomCursorGuideMouseHandler(handler)](#setcustomcursorguidemousehandlerhandler)

### loadGenome(config) ###

Returns a promise to load a reference genome.  
See the [Reference Genome]() for more detail on configuration options.

Example

```
browser.loadGenome(
{
    "id": "hg38",
    "name": "Human (GRCh38/hg38)",
    "fastaURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa",
    "indexURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa.fai",
    "cytobandURL": "https://s3.amazonaws.com/igv.broadinstitute.org/annotations/hg38/cytoBandIdeo.txt",
    "tracks": [
      {
        "name": "Refseq Genes",
        "url": "https://s3.amazonaws.com/igv.org.genomes/hg38/refGene.txt.gz",
        "order": 1000000,
        "indexed": false
      }
    ]
  }
}
```

### loadSessionObject(session) ##

Load a session object, also referred to as a browser configuration object.   See [Browser Creation](Browser-Creation) for more details.   Loading a session will clear the current reference genome and all tracks.

### loadSession(url) ##

Load a session by url, which should point to a valid session json object.  The json is a representation of a browser configuration object described in the [Browser Creation](#BrowserCreation) section, but does not support parameter values not representable as json such as functions and promises.

### loadTrack(config) ##

Returns a promise to load and configure a track.
See [Tracks](#tracks) for more detail on configuration options.

```
browser.loadTrack({
  url: 'http://data.broadinstitute.org/igvdata/1KG/b37/data/HG02450/alignment/HG02450.mapped.ILLUMINA.bwa.ACB.low_coverage.20120522.bam',
  label: 'HG02450'
    })
.then(function (newTrack) {
  alert("Track loaded: " + newTrack.name;
})
.catch(function (error)  {
   // Handle error
})
```

### findTracks(propertyOrFunction, value) ##

### removeTrackByName(name)  ##

Remove track(s) whose "name" property matches the given name.  

### removeTrack(track) ##

### loadROI(configOrArray) ##

Returns a promise to load an annotation file or array of annotation files to define regions of interest (ROIs).  Regions of interest are overlaid on the genome view across all tracks.  

```
browser.loadROI([
     {
        name: 'ROI set 1',
        url: 'https://s3.amazonaws.com/igv.org.test/data/roi/roi_bed_1.bed',
        indexed: false,
        color: "rgba(68, 134, 247, 0.25)"
      },
      {
        name: 'ROI set 2',
        url: 'https://s3.amazonaws.com/igv.org.test/data/roi/roi_bed_2.bed',
        indexed: false,
        color: "rgba(0, 150, 50, 0.25)"
      }
])
```
### clearROIs() ##

Remove all regions of interest.

### search(symbol) ##
       
Search by annotation symbol or locus string.

```
   browser.search('EGFR');
```
By default the search function uses a webservice to query positions of RefSeq genes for genome "hg19".  This can be overriden during initialization by supplying a url to a custom webservice.  For details see [Browser initialization](https://github.com/igvteam/igv.js/wiki/Browser).

Additionally, one or more annotation tracks can be used to back the "search" function by setting the searchable property to true.  See [Tracks](#tracks) for more details.

The search function can also be passed an explicit location,  for example
```
   browser.search('chr10:1000-2000')
```

This function returns ```true``` if the symbol was found, ```false``` otherwise.

### zoomIn() ##

Zoom in by a factor of 2 
```
    browser.zoomIn();
```

### zoomOut() ##

Zoom out by a factor of 2 
```
    browser.zoomOut();
```

### currentLoci()

Return the current genomic region as a locus string, or multiple regions if in multi-locus view

### visibilityChange() ##

Signal a change in visibility, typically from hidden  (e.g. display:none) to shown  (e.g. display:block).  This is necessary because changes in display attribute do not trigger events.
```
    igv.visibilityChange();
```
To target a specific igv browser instance
```
    browser.visibilityChange();
```     

### toJSON() ##

Return the current state of the browser as a JSON object.  This object can be loaded with loadSessionObject.

```
   const json = browser.toJSON();

   browser.loadSessionObject(json)

```

### compressedSession() ##

Return a compressed, encoded, string representing the current browser state.   This string can be used to load the session on any page hosting an igv.js instance with a url of the form

```
https://myhost/mypage?sessionURL=blob:<compressed session string>
```

Note to reinstate the session ```queryParametersSupported``` must be set to true in the igv.js configuration.

### toSVG() ##

Convert the browser contents to SVG format. This includes ideogram, ruler, and all tracks. The value returned by this function is a serialized SVG object.
```
    browser.toSVG();
```



### setCustomCursorGuideMouseHandler(handler) ##

Pass genomic location and mouse location with respect to trackContainer to the provided handler.
The data is transmitted as the cursor guide is manipulated across the track container.

Parameters:
bp - cursor-guide location. base-pair units.
start - track start location. base-pair units.
end - track end location. base-pair units.
interpolant - cursor-guide location. 0 - 1 units.
```
    browser.setCustomCursorGuideMouseHandler(({ bp, start, end, interpolant }) => {  });
```

# Tracks

## Track Types ##

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

## Configuring Tracks ##

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

## General Track Options ##
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

## Annotation Track

type = 'annotation'

### File Formats

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

### Configuration Options

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
## Alignment Track

type = 'alignment'

### Options

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

# Regions of Interest

A Region of Interest (ROI) is a genomic region to be highlighted in all tracks or a specific track, typically by overlaying a transparent color.  An ROI set is configured as an "roi" property at either the root level (for all tracks), or on a specific track.  The value of an "roi" property is an annotation track configuration object. The following snippet from a browser configuration object creates a set of ROIs for all tracks, and a second set specific to a single track, from the feature intervals specified in ".bed" files:

```
roi: [
                {
                    name: 'ROI set 1',
                    url: 'https://s3.amazonaws.com/igv.org.test/data/roi/roi_bed_1.bed',
                    indexed: false,
                    color: "rgba(68, 134, 247, 0.25)"
                }
            ],
            tracks: [
                {
                    name: 'Some features',
                    url: 'https://s3.amazonaws.com/igv.org.test/data/roi/some_features.bed',
                    indexed: false,
                    roi: [{
                        name: 'ROI set 2',
                        url: 'https://s3.amazonaws.com/igv.org.test/data/roi/roi_bed_2.bed',
                        indexed: false,
                        color: "rgba(0, 150, 50, 0.25)"
                    }]
                }
            ]
```

An ROI can be loaded dynamically with the Browser loadROI function, for example

```
 browser.loadROI([
                        {
                            name: 'ROI set 1',
                            url: 'https://s3.amazonaws.com/igv.org.test/data/roi/roi_bed_1.bed',
                            indexed: false,
                            color: "rgba(68, 134, 247, 0.25)"
                        }
                  ]);

```

A ROI can be removed from the root browser object with the removeROI function, which takes the ROI name as an argument.  For example

```
browser.removeROI('ROI set 1');
```

Currently there is no API to dynamically add or remove a ROI from a specific track.


