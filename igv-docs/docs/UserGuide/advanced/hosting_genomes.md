
Some words on genome list file


### Example -- Human GRCh38 with 2 annotation tracks

**Required fields are "id", "name", "fastaURL", and "indexURL".   All other fields are optional.**

```json
{
  "id": "hg38",
  "name": "Human (GRCh38/hg38)",
  "fastaURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa",
  "indexURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa.fai",
  "cytobandURL": "https://s3.amazonaws.com/igv.org.genomes/hg38/annotations/cytoBandIdeo.txt.gz",
  "aliasURL": "https://s3.amazonaws.com/igv.org.genomes/hg38/hg38_alias.tab",
  "chromosomeOrder": [
    "chr1",
    "chr2",
    "chr3",
    "chr4",
    "chr5",
    "chr6",
    "chr7",
    "chr8",
    "chr9",
    "chr10",
    "chr11",
    "chr12",
    "chr13",
    "chr14",
    "chr15",
    "chr16",
    "chr17",
    "chr18",
    "chr19",
    "chr20",
    "chr21",
    "chr22",
    "chrX",
    "chrY"
  ],
  "tracks": [
    {
      "name": "Refseq Genes",
      "format": "refgene",
      "url": "https://s3.amazonaws.com/igv.org.genomes/hg38/ncbiRefSeq.sorted.txt.gz",
      "indexURL": "https://s3.amazonaws.com/igv.org.genomes/hg38/ncbiRefSeq.sorted.txt.gz.tbi"
    },
    {
      "name": "Gencode v24 genes",
      "format": "gtf",
      "url": "https://s3.amazonaws.com/igv.org.genomes/hg19/gencode.v24.genes.gtf.gz"
    }
  ]
}

```

### File paths

URL properties (all fields that end with ```url```) can be absolute or relative file paths.  Relative paths are interpreted as relative to the location of the genome json file.   For example, the following definition presumes an annotation file ```chr22.genes.gtf.gz``` in the same directory as the json file.

hg19_local_annotations.json
```
{
  "id": "hg19",
  "name": "Human (CRCh37/hg19)",
  "fastaURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg19/hg19.fasta",
  "indexURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg19/hg19.fasta.fai",
  "cytobandURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg19/cytoBand.txt",
  "aliasURL": "https://s3.amazonaws.com/igv.org.genomes/hg19/hg19_alias.tab",
  "tracks": [
    {
      "name": "Gencode v24 genes",
      "url": "chr22.genes.gtf.gz"
    },

  ]
}
```




### Genome with hidden annotation track

In the example below an annotation file containing protein coding genes from Gencode is loaded to support searching by Gencode gene identifiers.


```json
{
  "id": "hg19",
  "name": "Human (CRCh37/hg19)",
  "fastaURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg19/hg19.fasta",
  "indexURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg19/hg19.fasta.fai",
  "cytobandURL": "https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg19/cytoBand.txt",
  "aliasURL": "https://s3.amazonaws.com/igv.org.genomes/hg19/hg19_alias.tab",
  "tracks": [
    {
      "name": "Refseq Genes",
      "url": "https://hgdownload.soe.ucsc.edu/goldenPath/hg19/database/ncbiRefSeq.txt.gz"
    },
    {
      "url": "https://s3.amazonaws.com/igv.org.genomes/hg19/gencode.v24.genes.gtf.gz",
      "hidden": true
    }
  ]
}
```

