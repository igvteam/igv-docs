
<!---
The page title should not go in the menu
-->
<p class="page-title">File Formats: Sample Info (Attributes)</p>

Sample information files includes Attributes files, Sample Mapping files, Attribute Color files, and files that combine information. These are tab-delimited text files with extension .txt. You load them as you would data files, via the _File_ menu. IGV can load multiple sample information files per session. When loaded into IGV, attributes display in a separate color-coded panel between sample names and tracks (see [Sample Attributes](../UserGuide/sample_attributes.md)). 

Attribute, mapping, and color information may be in **separate files,** i.e. in Attributes files, Mapping files, and Color files, **or in a single Sample Information file.**

*   To save all three types of information in a single file, list attributes first, then mapping, and then color.
    *   Between the information types, separate sections with row headers _#sampleMapping_ and _#colors_.
    *   Empty rows are not necessary and are ignored.

When loading attributes for datasets where sample names are identical across file types, no mapping information is necessary for the attributes to apply to the multiple data type tracks. However, to apply the same attribute information across datasets where sample names differ, you can use either of two different types of Sample Information sets as indicated by (b) and (c) in the table.

<table align="center" border="1" cellpadding="1" cellspacing="1" height="198" width="700">
	<tbody>
		<tr>
			<td class="rtecenter" colspan="4" style="background-color: rgb(255, 255, 153);">
				<strong>Multiple data track types?</strong></td>
		</tr>
		<tr>
			<td class="rtecenter" colspan="2" rowspan="1" style="width: 345px;">
				No</td>
			<td class="rtecenter" colspan="2" rowspan="1" style="width: 347px;">
				Yes</td>
		</tr>
		<tr>
			<td class="rtecenter" colspan="4" style="width: 345px; background-color: rgb(255, 255, 153);">
				<strong>Do attributes sample labels match data track sample names?</strong></td>
		</tr>
		<tr>
			<td style="width: 171px;">
				<p>No.</p>
				<p>(a) Edit Attributes file to include the matching data track sample names in the first column.</p>
				<p>(b) Load Attributes and Sample Mapping information.</p>
			</td>
			<td style="width: 171px;">
				<p>Yes.</p>
				<p>Attributes apply to data tracks.</p>
				<p>&nbsp;</p>
				<p>&nbsp;</p>
				<p>&nbsp;</p>
			</td>
			<td style="width: 178px;">
				<p>No.</p>
				<p>(b) Load Attributes and Sample Mapping information.</p>
				<p>&nbsp;</p>
			</td>
			<td style="width: 172px;">
				<p>Yes.</p>
				<p>Attributes apply to data tracks.</p>
				<p>&nbsp;</p>
				<p>&nbsp;</p>
				<p>&nbsp;</p>
			</td>
		</tr>
	</tbody>
</table>

## Attributes

An Attributes file lists track identifiers in the first column and attributes in subsequent columns with a single header row. IGV matches the track identifiers in a data file with the track identifiers in the Attributes file.

*   Example 1: [example_sampleinfo.txt](ExampleFiles/example_sampleinfo.txt)

**Acceptable variations to the Attributes file:**

So long as the first row contains attribute labels and the first column sample names, the remaining rows may contain information pertaining to samples in any data type and be organized in any way.

*   Because IGV can load multiple Attributes files per session, it is not necessary to merge attributes into a single file.
*   Attributes only apply to data tracks with matching names. Attribute rows without matching data tracks do not display. So the information within the Attributes file need not overlap exclusively to the data tracks.
*   For data tracks without a matching attribute row, corresponding IGV attributes panel rows remain blank.

In the case of different data sets with different sample names from the same individual, e.g. copy number and RNA expression, you may wish to apply the information within a single attributes file in duplicate to the different data types. In this case, you may (b) additionally load a Sample Mapping file as outlined in the next section or **(c) modify your Attributes file** as outlined below.

* For a single attributes file, duplicate the attributes by copy-pasting into empty rows, then modify sample names in the first column as needed for the differentially named datasets.
 	
* For multiple attributes files, duplicate the entire file and open each to modify sample names for the differentially named datasets as needed.

## Sample Mapping

A Sample Mapping section begins with the line #sampleMapping and maps track identifiers to sample identifiers.  It is useful in cases where these identifiers might differ.   For example, one might map the track identifier  "foo.bam" to sample identifier  "foo\_sample".     The format is 2 column tab delimited, the first column is the track identifier, second the sample identifier.

## Attribute Colors

By default, IGV randomly assigns colors to the attribute values. You can optionally specify the colors for attribute values in RGB format for a specific label, a specific value, or as a heatmap scale for numeric columns in monocolor or in two-color heatmap for specified ranges. Customize colors using either a separate Attribute Colors file or by adding a colors section to the end of a Sample Information file. Colors information is tab-delimited with three or four columns as shown in the example below.
<table align="center" border="1" cellpadding="1" cellspacing="1" height="38" width="700">
	<tbody>
		<tr>
			<td style="width: 68px;">
				<strong>column 1</strong></td>
			<td style="width: 98px;">
				<strong>column 2</strong></td>
			<td style="width: 148px;">
				<strong>column 3</strong></td>
			<td style="width: 137px;">
				<strong>column 4 (optional)</strong></td>
			<td colspan="1" rowspan="2" style="width: 233px;">
				&nbsp;</td>
		</tr>
		<tr>
			<td style="width: 68px;">
				Indicates attribute name</td>
			<td style="width: 98px;">
				Indicates attribute value or attribute range separated by a colon (:)</td>
			<td style="width: 148px;">
				Indicates color in RGB format. If used with column 4, then is the first color of a two-color heatmap</td>
			<td style="width: 137px;">
				Specifies the second color in RGB format in a two-color heatmap for attribute ranges</td>
		</tr>
		<tr>
			<td class="rtecenter" colspan="4" style="width: 460px; background-color: rgb(204, 204, 204);">
				<strong>Example</strong></td>
			<td class="rtecenter" colspan="4" style="width: 460px; background-color: rgb(204, 204, 204);">
				<strong>Explanation</strong></td>
		</tr>
		<tr>
			<td style="width: 68px;">
				#colors</td>
			<td style="width: 68px;">
				&nbsp;</td>
			<td style="width: 68px;">
				&nbsp;</td>
			<td style="width: 68px;">
				&nbsp;</td>
			<td style="width: 233px; background-color: rgb(204, 204, 204);">
				&nbsp;</td>
		</tr>
		<tr>
			<td style="width: 68px;">
				GENDER</td>
			<td style="width: 68px;">
				MALE</td>
			<td style="width: 68px;">
				0,0,155</td>
			<td style="width: 68px;">
				&nbsp;</td>
			<td style="width: 233px; background-color: rgb(204, 204, 204);">
				<em>a value of&nbsp; &quot;MALE&quot; for the &quot;GENDER&quot; column gets the color (0,0,155)</em></td>
		</tr>
		<tr>
			<td style="width: 68px;">
				*</td>
			<td style="width: 68px;">
				Classical</td>
			<td style="width: 68px;">
				80,180,80</td>
			<td style="width: 68px;">
				&nbsp;</td>
			<td style="width: 233px; background-color: rgb(204, 204, 204);">
				<em>a value of &quot;Classical&quot;&nbsp; in any column gets the color&nbsp; (80,180,80)</em></td>
		</tr>
		<tr>
			<td style="width: 68px;">
				KarnScore</td>
			<td style="width: 68px;">
				*</td>
			<td style="width: 68px;">
				0,0,255</td>
			<td style="width: 68px;">
				&nbsp;</td>
			<td style="width: 233px; background-color: rgb(204, 204, 204);">
				<em>numeric column example, monocolor heatmap</em></td>
		</tr>
		<tr>
			<td style="width: 68px;">
				% Tumor Nuclei</td>
			<td style="width: 68px;">
				90:100</td>
			<td style="width: 68px;">
				0,0,255</td>
			<td style="width: 68px;">
				&nbsp;</td>
			<td style="width: 233px; background-color: rgb(204, 204, 204);">
				<em>another monocolor heatmap, this time with the range specified</em></td>
		</tr>
		<tr>
			<td style="width: 68px;">
				sil_width</td>
			<td style="width: 68px;">
				-0.1:0.5</td>
			<td style="width: 68px;">
				0,0,255</td>
			<td style="width: 68px;">
				255,0,0</td>
			<td style="width: 233px; background-color: rgb(204, 204, 204);">
				<em>a two-color heatmap with the range specified</em></td>
		</tr>
	</tbody>
</table>

*   Colors information, either file or section, must be headed by a row with _#colors_.
*   An asterisk (\*) in either of the first two columns indicates a wildcard. 
*   RGB values are separated by commas (,) without spaces and may be listed inside double quotations, e.g. _0,0,155_ or _"0,0,155"_.