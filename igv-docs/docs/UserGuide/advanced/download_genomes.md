This page describes how to download a genome specification (json) file and configure it for use in IGV without an internet connection.  This requires downloading all dependent files, including the sequence. The following example uses C. elegans (ce11); for other genomes see the [Hosted Genomes](#hosted-genome-list) list below.

**NOTE:** Some of the more frequently used genomes are available for download 
[here](https://drive.google.com/drive/folders/16EEDgjwVZ6hPA0sLzatQ_s301HRS6M-F?usp=sharing) as a package ready for 
offline use. If you download one of these packages, skip to [step 4 below](#4-use-the-local-version-of-the-genome-in-igv).

## Example

### 1. Download the .json genome specification file

For our ce11 example: ```curl -O https://s3.amazonaws.com/igv.org.genomes/ce11/ce11.json```

```
{
  "id": "ce11",
  "name": "C. elegans (ce11)",
  "fastaURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/ce11/ce11.fa",
  "indexURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/ce11/ce11.fa.fai",
  "cytobandURL": "https://s3.amazonaws.com/igv.org.genomes/ce11/cytoBandIdeo.txt.gz",
  "tracks": [
    {
      "name": "Refseq Genes",
      "format": "refgene",
      "url": "https://s3.amazonaws.com/igv.org.genomes/ce11/refGene.sorted.txt.gz",
      "indexURL": "https://s3.amazonaws.com/igv.org.genomes/ce11/refGene.sorted.txt.gz.tbi",
      "indexed": false,
      "order": 1000000,
      "removable": false,
      "visibilityWindow": -1
    },
    {
      "name": "Genes",
      "format": "bed",
      "url": "https://s3.amazonaws.com/igv.org.genomes/locations/geneLocations_ce11.bed.gz",
      "hidden" : true,
      "searchable": true
    }
  ]
}
```

### 2. Download the files referenced in the genome specification

For our example, these files are:

* https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/ce11/ce11.fa
* https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/ce11/ce11.fa.fai
* https://s3.amazonaws.com/igv.org.genomes/ce11/cytoBandIdeo.txt.gz
* https://s3.amazonaws.com/igv.org.genomes/ce11/refGene.sorted.txt.gz
* https://s3.amazonaws.com/igv.org.genomes/ce11/refGene.sorted.txt.gz.tbi
* https://s3.amazonaws.com/igv.org.genomes/locations/geneLocations_ce11.bed.gz

### 3. Edit your local copy of the genome specification file

Your local copy of the .json file should reference the downloaded files. Reference can be by URL to a file on your local network, or by file path, which can be relative to the location of the .json file. Assuming the downloaded data files are in the same directory as the .json file, the ```ce11.json``` file will look like this:

```
{
  "id": "ce11",
  "name": "C. elegans (ce11)",
  "fastaURL": "ce11.fa",
  "indexURL": "ce11.fa.fai",
  "cytobandURL": "cytoBandIdeo.txt.gz",
  "tracks": [
    {
      "name": "Refseq Genes",
      "format": "refgene",
      "url": "refGene.sorted.txt.gz",
      "indexURL": "refGene.sorted.txt.gz.tbi",
      "indexed": false,
      "order": 1000000,
      "removable": false,
      "visibilityWindow": -1
    },
    {
      "name": "Genes",
      "format": "bed",
      "url": "geneLocations_ce11.bed.gz",
      "hidden" : true,
      "searchable": true
    }
  ]
}
```

### 4. Use the local version of the genome in IGV

Load the updated .json genome specification file into IGV using the ```Genomes > Load from File...``` menu.

**NOTE:** If you previously loaded the same genome into IGV using the regular hosted options, you may need to delete its json file to prevent conflicts with the local version. The hosted-based files can be found in the folder ```<userhome>/igv/genomes```.


## Hosted Genome list

List of specification files for IGV hosted genomes as of March 29, 2022.

[Note: Not all IGV genomes have a corresponding .json file that can be downloaded for local use.]

| Genome | JSON configuration file |
| -----------  | ----------- |
| A. thaliana (TAIR 10) | https://s3.amazonaws.com/igv.org.genomes/tair10/tair10.json |
| C. elegans (ce11) | https://s3.amazonaws.com/igv.org.genomes/ce11/ce11.json |
| Chicken (GRCg6a / galGal6) | https://s3.amazonaws.com/igv.org.genomes/galGal6/galGal6.json |
| Chimp (panTro4) | https://s3.amazonaws.com/igv.org.genomes/panTro4/panTro4.json |
| Cow (bosTau8) | https://s3.amazonaws.com/igv.org.genomes/bosTau8/bosTau8.json |
| Cow (bosTau9) | https://s3.amazonaws.com/igv.org.genomes/bosTau9/bosTau9.json |
| D. melanogaster (dm6) | https://s3.amazonaws.com/igv.org.genomes/dm6/dm6.json |
| D. melanogaster (dm3) | https://s3.amazonaws.com/igv.org.genomes/dm3/dm3.json |
| D. melanogaster (r5.9) | https://s3.amazonaws.com/igv.org.genomes/dmel_r5.9/dmel_r5.9.json |
| Dog (canFam3) | https://s3.amazonaws.com/igv.org.genomes/canFam3/canFam3.json |
| Dog (canFam5) | https://s3.amazonaws.com/igv.org.genomes/canFam5/canFam5.json |
| Human hg18 | https://s3.amazonaws.com/igv.org.genomes/hg18/hg18.json |
| Human (GRCh37/hg19) | https://s3.amazonaws.com/igv.org.genomes/hg19/hg19.json |
| Human (GRCh38/hg38) | https://s3.amazonaws.com/igv.org.genomes/hg38/hg38.json |
| Human hg38 (1kg/GATK) | https://s3.amazonaws.com/igv.org.genomes/hg38_1kg/hg38_1kg.json |
| Macaca fascicularis (macFas5) | https://s3.amazonaws.com/igv.org.genomes/macFas5/macFas5.json |
| Mouse mm10 | https://s3.amazonaws.com/igv.org.genomes/mm10/mm10.json |
| Mouse mm9 | https://s3.amazonaws.com/igv.org.genomes/mm9/mm9.json |
| Rat (rn6) | https://s3.amazonaws.com/igv.org.genomes/rn6/rn6.json |
| S. cerevisiae (sacCer3) | https://s3.amazonaws.com/igv.org.genomes/sacCer3/sacCer3.json |
| Zebrafish (GRCz10/danRer10) | https://s3.amazonaws.com/igv.org.genomes/danRer10/danRer10.json |
| Zebrafish (GRCz11/danRer11) | https://s3.amazonaws.com/igv.org.genomes/danRer11/danRer11.json |
| SARS-CoV-2 | https://s3.amazonaws.com/igv.org.genomes/ASM985889v3/ASM985889v3.json |
| S. pombe (ASM294v2) | https://s3.amazonaws.com/igv.org.genomes/ASM294v2/ASM294v2.json |
| Gorilla (gorGor4) | https://s3.amazonaws.com/igv.org.genomes/gorGor4/gorGor4.json |
| Gorilla (gorGor6) | https://s3.amazonaws.com/igv.org.genomes/gorGor6/gorGor6.json |
| Bonobo (MPI-EVA panpan1.1/panPan2) | https://s3.amazonaws.com/igv.org.genomes/panPan2/panPan2.json |
