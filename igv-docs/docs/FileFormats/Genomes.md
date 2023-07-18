
<!---
The page title should not go in the menu
-->
<p class="page-title">File Formats: Genomes</p>

## chrom.sizes

igvtools uses chrom.sizes files to define the chromosome lengths for a given genome.    The file format is tab delimited, first column is chromosome name and second is its length.  There can be more columns present, but they are ignored.  Files should be named as follows:

   <genomdID>.chrom.sizes

For example,  hg18.chrom.sizes.

## Cytoband

The Cytoband file format is used to define the chromosome ideograms for a reference genome, and/or as of version 2.11.0 to create a cytoband track.

A cytoband file is a five-column tab-delimited text file. Each row of the file describes the position of a cytogenetic band. The columns in the file match the columns of the [cytoBand table](http://genome.ucsc.edu/cgi-bin/hgTables?db=hg38&hgta_group=map&hgta_track=cytoBand&hgta_table=cytoBand&hgta_doSchema=describe+table+schema) in the database underlying the UCSC Genome Browser.  These files are downloadable from the UCSC website as "cytoBandIdeo.txt.gz" for many genome assemblies, for example https://hgdownload.cse.ucsc.edu/goldenPath/hg38/database/cytoBandIdeo.txt.gz

The Cytoband file format is used to define the chromosome ideograms for a reference genome, and/or as of version 2.11.0 to create a cytoband track.

A cytoband file is a five-column tab-delimited text file. Each row of the file describes the position of a cytogenetic band. The columns in the file match the columns of the [cytoBand table](http://genome.ucsc.edu/cgi-bin/hgTables?db=hg38&hgta_group=map&hgta_track=cytoBand&hgta_table=cytoBand&hgta_doSchema=describe+table+schema) in the database underlying the UCSC Genome Browser.  These files are downloadable from the UCSC website as "cytoBandIdeo.txt.gz" for many genome assemblies, for example https://hgdownload.cse.ucsc.edu/goldenPath/hg38/database/cytoBandIdeo.txt.gz

<table class="general" width="100%">
	<tbody>
		<tr>
			<th>
				Column</th>
			<th>
				Example</th>
			<th>
				Data Type</th>
			<th>
				Description</th>
		</tr>
		<tr>
			<td>
				chrom</td>
			<td>
				chr1</td>
			<td>
				string</td>
			<td>
				Chromosome</td>
		</tr>
		<tr>
			<td>
				chromStart</td>
			<td>
				0</td>
			<td>
				integer</td>
			<td>
				<p>Start position in chromosome sequence</p>
			</td>
		</tr>
		<tr>
			<td>
				chromEnd</td>
			<td>
				2300000</td>
			<td>
				integer</td>
			<td>
				End position in chromosome sequence</td>
		</tr>
		<tr>
			<td>
				name</td>
			<td>
				p36.33</td>
			<td>
				string</td>
			<td>
				Name of cytogenetic band</td>
		</tr>
		<tr>
			<td>
				gieStain</td>
			<td>
				gneg</td>
			<td>
				string</td>
			<td>
				Giemsa stain results. Recognized stain values: gneg, gpos50, gpos75, gpos25, gpos100, acen, gvar, stalk</td>
		</tr>
	</tbody>
</table>

## FASTA

The FASTA file format (.fasta or .fa) is used to specify the reference sequence for an imported genome. Each sequence in the FASTA file represents the sequence for a chromosome. The sequence name in the FASTA file is the chromosome name that appears in the chromosome drop-down list in the IGV tool bar. IGV orders the chromosomes based on their names, not their order in the FASTA file.

A FASTA file is a text file. Each sequence begins with a single-line description, followed by lines of sequence data. The single-line description contains a greater-than (>) symbol in the first column, followed by the sequence name. For a complete description of the FASTA file format, see [http://www.ncbi.nlm.nih.gov/blast/fasta.shtml](http://www.ncbi.nlm.nih.gov/blast/fasta.shtml).

Note that FASTA files are only used for defining reference sequences, they cannot be "loaded" from the file menu.
