# Hosting reference genomes on your own server.

There are many ways to create the required files, this is just one.  In this example we'll host a single genome, human hg38.

1. Download the IGV genome list from  [https://s3.amazonaws.com/igv.org.genomes/genomes.txt](https://s3.amazonaws.com/igv.org.genomes/genomes.txt)

2. Open the downloaded genomes.txt file in a plain text editor and eliminate all lines except the first and the genome(s) of interest.  For this example the file contents should be as shown below.  Note the format is 3-column tab delimited: descriptive name, url to .genome file, and ID.   The ID is arbitrary but for UCSC hosted genomes please use their ID.  This is important for the blat tool, which uses the UCSC blat server.

```
<Server-Side Genome List>
Human hg38	https://s3.amazonaws.com/igv.org.genomes/hg38/hg38.genome	hg38
```

3. Download the ".genome" file from the URL (second field in genomes.txt).  In this example ```https://s3.amazonaws.com/igv.org.genomes/hg38/hg38.genome```.  

4. Move the .genome file to an empty working directory.  This is important for the next steps

5. The .genome file is a zip archive, unzip it.  The exact command might vary by platform.

```
unzip hg38.genome
```

Contents of the working directory should now be

```
cytoBandIdeo.txt	
hg38_alias.tab		
refGene.txt
hg38.genome		
property.txt
```

6. Discard the hg38.genome file

```
rm hg38.genome
```

7. Open or view ('cat') the property.txt file

```
fasta=true
fastaDirectory=false
ordered=true
id=hg38
name=Human (hg38)
cytobandFile=cytoBandIdeo.txt
geneFile=refGene.txt
chrAliasFile=hg38_alias.tab
sequenceLocation=http://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa
compressedSequencePath=https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa.gz
```

8. Download the fasta file from the "sequenceLocation" 

[https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa](https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa)

9. Download the implied index from the "sequenceLocation".fai

[https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa.fai](https://s3.amazonaws.com/igv.broadinstitute.org/genomes/seq/hg38/hg38.fa.fai)

10. Upload the fasta and its index file to your server.  They must be in the same directory.

11. Edit the property.txt file with a plain text editor.  
    * Replace the "sequenceLocation" value with the URL to the hg38.fa file on your server.
    * Delete the line starting with "compressedSequencePath

12. Zip everything in the temp working directory to a new archive.  You can use a "gui" tool to do this, but rename the extension from "zip" to "genome".  From the command line this can be done in 1 step.

```
zip hg38.genome *
```

13. Upload the new hg38.genome to your server

14. Edit the genomes.txt file with a plain text editor.  Replace the second column value, ```https://s3.amazonaws.com/igv.org.genomes/hg38/hg38.genome```, to the URL on your server.

15. Upload the modified ```genomes.txt``` to your server.

15. Start IGV.
    * Select View > Preferences > Advanced
    * Set the Genome server URL to the url to your ```genomes.txt``` file. 
    * Click ```Save```

16. Shutdown IGV.  Upon restart your hosted genome list should be available.  



