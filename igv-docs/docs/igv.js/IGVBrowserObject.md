
# Browser Creation     

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

!!! tip " "
    The global singleton instance "igv.browser" is no longer created by the createBrowser function. If needed, this object can be created as follows: 
	
```
    igv.createBrowser(div, options)
    .then(function (browser) {
        igv.browser = browser;
   }); 
```


# Browser Removal

To remove an igv browser instance, call

```js
igv.removeBrowser(browser);
```
To remove all igv browsers

```js
igv.removeAllBrowsers();
```


# Browser Configuration Options ##
The object that configures the browser's initial state includes details for the reference genome, track default settings, the initial set of loaded tracks, and the initial view locus. It also controls some aspects of the user interface.  All fields are optional except one of either **genome** or **reference**.

Option  | Description | Default
------ | ------- | ------------
genome | String identifier defining genome (e.g. "hg19").  See [Reference Genome](Reference-Genome) for details and list of supported identifiers. **Note: One (but only one) of either _genome_ or _reference_ properties must be set.**
reference | Object defining reference genome.  See [Reference Genome](Reference-Genome) for details. **Note: One (but only one) of either _genome_ or _reference_ properties must be set.**|
doubleClickDelay | Maximum between mouse clicks in milliseconds to trigger a double-click | 500
flanking  | Distance (in bp) to pad sides of gene  on successful search by gene or other annotation. | 1000
genomeList | **OPTIONAL.**  _Release 2.0.2._   URL to a JSON file containing an array of genome reference definitions, _or_ an inline JSON array.  Genomes can be specified from the list by ID with the "genome" property.  Default value is [https://s3.amazonaws.com/igv.org.genomes/genomes.json](https://s3.amazonaws.com/igv.org.genomes/genomes.json) **NOTE: the genomeList is globally shared by all igv browser instances on a page.** |
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
genomeList | An array of genome JSON objects, or url to an array of genome JSON objects.  If present genomes can be specified by id with the ```genome``` field above.  This list is added to the igv.js default list unless ```loadDefaultGenomes: false``` |
loadDefaultGenomes | Boolean indicating whether or not the igv.js default genome list should be loaded.  | true 
nucleotideColors | Color table for nucleotides in sequence an bam tracks.  Object with keys "A", "C", "T", "G", and "N" | 
showSampleNames | Controls display of sample names for track types that support them (VCF with genotypes, SEG, and MUT) |

## _search_ object details

The search object defines a webservice for fetching genomic location given a gene name or other symbol.  The service should return a JSON object with the following structure.  The results array is an array of objects with a chromosome, start, and end field.  The names of these fields are specified in the configuration object.   The end field is optional, if not included end = start + 1.

```JavaScript
    {
      <resultsField> : <array of results>
    }
```


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

```js
    [{"chromosome":"chr17","start":7572927,"end":7579912}]
```
    
The reference genome must be defined by specifying either the _reference_ object or _genome_ identifier for hosted genomes.  These are mutually exclusive options, do not specify both.

## _genome_ property

igv.js supports a number of genome references,  see [genomes.json](https://s3.amazonaws.com/igv.org.genomes/genomes.json)
for the current list. 
 
``` javascript
{
  ...
  genome: "hg19",
  ...
}
```


## _reference_ object 

To define or customize a reference genome the reference property can be used.  

### Example

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

## Details

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