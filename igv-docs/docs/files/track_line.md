When IGV loads a data file, it uses the file extension to determine the file format, the file format to determine the data type, and the data type to determine the default display options (see [Default Display](<?php echo base_path(); ?>DefaultDisplay)). Adding a track line to a data file modifies IGV's default display options. This can be particularly useful for file formats not associated with any particular type of data, such as the IGV file format.

The following file formats allow track lines:

*   BED, WIG, PSL
*   IGV, CN, SNP, GFF, LOH, GFF3, SEG -- in these file formats, the track line must begin with a # symbol; i.e. #track

IGV track lines are based on WIG track lines. See the UCSC site for the WIG track line syntax: [https://genome.ucsc.edu/goldenPath/help/wiggle.html](https://genome.ucsc.edu/goldenPath/help/wiggle.html). The following table describes the track line specifiers that IGV supports. IGV includes a few options that are not part of the UCSC specification.

_**Note: IGV does not currently support multiple track lines in a single file.**_


<table class="general" width="100%">
	<thead>
		<tr>
			<th scope="col">
				Specifier</th>
			<th scope="col">
				Value</th>
			<th scope="col">
				Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>
				name</td>
			<td>
				trackLabel</td>
			<td>
				Track name (ignored when used in the IGV file format)</td>
		</tr>
		<tr>
			<td>
				description</td>
			<td>
				centerlabel</td>
			<td>
				Currently ignored</td>
		</tr>
		<tr>
			<td>
				visibility</td>
			<td>
				full | dense | hide</td>
			<td>
				Currently ignored</td>
		</tr>
		<tr>
			<td>
				color</td>
			<td>
				RRR,GGG,BBB</td>
			<td>
				Color for positive values in all tracks</td>
		</tr>
		<tr>
			<td>
				<p>altColor</p>
			</td>
			<td>
				RRR,GGG,BBB</td>
			<td>
				Color for negative values in all tracks</td>
		</tr>
		<tr>
			<td>
				priority</td>
			<td>
				N</td>
			<td>
				Currently ignored</td>
		</tr>
		<tr>
			<td>
				autoScale</td>
			<td>
				on|off</td>
			<td>
				Currently ignored.&nbsp; All tracks autoscale unless an explicit data range is defined (e.g., by including the viewlimits specifier).</td>
		</tr>
		<tr>
			<td>
				gridDefault</td>
			<td>
				on | off</td>
			<td>
				Currently ignored</td>
		</tr>
		<tr>
			<td>
				maxHeightPixels</td>
			<td>
				max:default:min</td>
			<td>
				default and min are supported<br />
				max is currently ignored</td>
		</tr>
		<tr>
			<td>
				graphType</td>
			<td>
				bar | points | heatmap</td>
			<td>
				<p>Graph type to use: chart | scatter plot | heatmap.</p>
				<p><strong>(IGV only: </strong>The <em>heatmap </em>value is an IGV addition to the specification.)</p>
			</td>
		</tr>
		<tr>
			<td>
				midRange&nbsp; <em>(IGV extension)</em></td>
			<td>
				x:y</td>
			<td>
				<p>Defines the neutral range for a 3-color heatmap.&nbsp;&nbsp;&nbsp; Values in this range are rendered with the midColor value,&nbsp; which is white by default.</p>
				<p>Example:&nbsp; midRange=20:80</p>
			</td>
		</tr>
		<tr>
			<td>
				midColor&nbsp;<em> (IGV extension</em><strong>)</strong></td>
			<td>
				RRR,GGG,BBB</td>
			<td>
				<p>Color to use in the &quot;mid range&quot; of a heatmap.</p>
				<p>Example: midColor=0,0,150</p>
			</td>
		</tr>
		<tr>
			<td>
				viewLimits</td>
			<td>
				lower:upper</td>
			<td>
				Defines the data range</td>
		</tr>
		<tr>
			<td>
				yLineMark</td>
			<td>
				real-value</td>
			<td>
				Currently ignored</td>
		</tr>
		<tr>
			<td>
				yLineOnOff</td>
			<td>
				on | off</td>
			<td>
				Currently ignored</td>
		</tr>
		<tr>
			<td>
				windowingFunction</td>
			<td>
				maximum | minimum | mean | none</td>
			<td>
				Function that summarizes the values in a window of data represented by one pixel</td>
		</tr>
		<tr>
			<td>
				smoothingWindow</td>
			<td>
				off | [2-16]</td>
			<td>
				Currently ignored</td>
		</tr>
		<tr>
			<td>
				url</td>
			<td>
				&nbsp;</td>
			<td>
				Defines a URL for an external link associated with this track.&nbsp; Any &#39;$$&#39; in this string this will be substituted with the item <strong>ID</strong> if explicitly defined, or <strong>name</strong> if <strong>ID</strong><strong> </strong>is not specified..</td>
		</tr>
		<tr>
			<td>
				coords&nbsp; <em>(IGV extension)</em></td>
			<td>
				0 | 1</td>
			<td>
				<p>Indicate whether the file uses 0 or 1 based coordinates.&nbsp;The UCSC specification for WIG files uses 1 based coordinates and for BED files uses 0 based coordinates. If data looks off by one, check for a possible 0 vs 1 based coordinate issue.</p>
			</td>
		</tr>
		<tr>
			<td>
				scaleType&nbsp; <strong>(IGV&nbsp;only)</strong></td>
			<td>
				log |&nbsp;linear</td>
			<td>
				The Y-axis scale type for charts&nbsp;</td>
		</tr>
		<tr>
			<td>
				featureVisibilityWindow <strong>(IGV&nbsp;only)</strong></td>
			<td>
				<p>integer value</p>
			</td>
			<td>
				<p>The window size in bp below which features are loaded and displayed.&nbsp; When the viewing window is above this value a message is displayed &quot;Zoom in to view features&quot;.&nbsp; This parameter is useful for&nbsp; large indexed feature tracks.</p>
				<p><strong>A negative value indicate features should be loaded for an entire chromosome (but not the whole genome)</strong></p>
			</td>
		</tr>
		<tr>
			<td>
				gffTags&nbsp; <em>(IGV extension)</em></td>
			<td>
				off |&nbsp;on</td>
			<td>
				If &quot;on&quot;&nbsp;the name field is treated as a GFF3 style attribute list (column 9 of GFF3).&nbsp; The default is &quot;off&quot;.</td>
		</tr>
	</tbody>
</table>