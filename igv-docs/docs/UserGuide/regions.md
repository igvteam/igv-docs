<!---
The page title should not go in the menu
-->
<p class="page-title"> Regions</p>

# Regions of Interest (ROIs)

Regions of interest (ROI) are intervals defined by the user using one of the methods described below. ROIs are marked
in red below the ruler. Hovering the mouse over this red region displays lines that demarcate the ROI down the panels.
Clicking on the red highlight pops up a menu for options that include sorting by various data-specific metrics and
copying to the clipboard or BLAT searching the corresponding reference sequence (**Screenshot** 2015.05.05).

![](img/SL_IGV_ROI_BLAT2015-05-05%2016.25.58.png)

* View a session's ROIs in the _Region Navigator_ under the _Regions_ menu. The _Region Navigator_'s list is editable,
  sortable and as the name indicates, navigable.
    * Navigate to a single locus or view multiple loci in split
      panes by selecting them and clicking _View_.
    * Distinguish overlapping ROIs using the _Region Navigator_.
    * Enter a short description for each ROI viewable in the _Region Navigator_.
* Defined ROIs persist within an IGV session. 
* Import and export ROIs as [BED](../FileFormats/DataTracks.md) files using _Regions_\>_Import
  Regions_ and _Regions_\>_Export Regions_.

## Defining an ROI

**1. By mouse:** 

First, click the **_Region of Interest_** icon in the toolbar:

![](img/icon_region_of_interest.jpg)

Then, **single** click in the data panel at the start of the region and then the end of the region. Do **NOT** click and drag. 
Lines delimiting the region of interest will be displayed for the first and second click, then marks the region in red under the
ruler.

**2. By keyboard shortcut:**

Display the region of interest to fill the entire view and press _Control_ \+ _R_.

* The entire ruler view will be marked red to indicate the region of interest fills the view.
* Does not work to select multiple regions at once in multi-locus view.

**3. Using the Region Navigator:**

See the section on the [ROI navigator](#roi-navigator), below

## ROI menu options

Click the red bar under the ruler to display the region of interest (ROI) context menu for the following options.

**Menu option**    |    **Description**
----------- | ----------
**Sort** | Sort based on data values within the ROI. Sort options vary with data type and may not be available for regions of interest for certain file types, e.g. alignment or VCF tracks, for which sort options are available via feature pop-up menu. <br><br> * For *copy number variation data*, sort by amplification, deletion, breakpoint amplitudes, and value. <br> * For *mutation data*, sort by mutation count or value. <br> * For *expression data*, sort by expression or value.
**Scatter Plot** | Available for continuous value data, e.g. gene expression, copy number, and methylation data. 
**Zoom** | Center and zoom the display to the ROI.
**Edit description**| Input a short description for the ROI.
**Copy sequence** | Copy the reference sequence to the clipboard. If the region is too large for the clipboard, nothing will be copied.
**BLAT sequence** | BLAT search the section of the reference sequence against the entire reference genome. See the [BLAT tool](tools/blat.md) page for details.
**Delete** | Remove the region of interest.

## ROI navigator

The Region Navigator lists all current regions and allows you to provide a description for each, add new regions, and delete selected regions. To open the Region Navigator select _Regions>Region Navigator_ from the menu bar. 

![](img/SL_IGV_ROI_RN_2015-05-06%2011.17.36.png){width=494}

The Description field is initially blank. To input a description, either right-click on the ROI and select _Edit description_ from the menu or double-click the field in the _Region Navigator_.

The following table summarizes the features available from the _Region Navigator_.

To select an ROI from the list, click on it. Select multiple ROIs from the list by holding down a keyboard key and
clicking by mouse, e.g. _Shift_ \+ _mouse-click_ for consecutive rows or \[Mac/PC\] _Command/Control_ + _mouse-click_ to
select individual rows.

<table border="1" cellpadding="1" cellspacing="1" height="337" width="600">
	<tbody>
		<tr>
			<td>
				&nbsp;</td>
			<td class="rtecenter" style="width: 164px;">
				<strong>Region Navigator feature</strong></td>
			<td class="rtecenter" style="width: 353px;">
				<strong>Description</strong></td>
		</tr>
		<tr>
			<td colspan="1" rowspan="3">
				<strong>Define ROIs</strong></td>
			<td style="width: 164px;">
				<em>Add</em></td>
			<td style="width: 353px;">
				Add the currently displayed region in its entirety to the list.</td>
		</tr>
		<tr>
			<td style="width: 164px;">
				<em>Delete</em></td>
			<td style="width: 353px;">
				Remove the selected ROI from the list.</td>
		</tr>
		<tr>
			<td style="width: 164px;">
				Double-click cells under <em>Start</em>, <em>End</em>, or <em>Description</em></td>
			<td style="width: 353px;">
				The cell will be boxed as shown in the <strong>Screenshot</strong> above. Edit cell content.</td>
		</tr>
		<tr>
			<td colspan="1" rowspan="3">
				<strong>Sort list</strong></td>
			<td style="width: 164px;">
				<em>Show All Chrs</em></td>
			<td style="width: 353px;">
				Uncheck or check to limit the list to loci on the displayed chromosome or all chromosomes.</td>
		</tr>
		<tr>
			<td style="width: 164px;">
				Click a column header, e.g. <em>Chr</em></td>
			<td style="width: 353px;">
				Sort table by ascending or descending alphanumeric order.</td>
		</tr>
		<tr>
			<td style="width: 164px;">
				<em>Search</em> and <em>Clear Search</em></td>
			<td style="width: 353px;">
				Type a search term on which to filter the displayed list. To remove the filter, click <em>Clear Search</em>.</td>
		</tr>
		<tr>
			<td colspan="1" rowspan="2">
				<strong>Navigate to ROIs</strong></td>
			<td style="width: 164px;">
				<em>View</em></td>
			<td style="width: 353px;">
				Navigate the display to the selected ROI. If multiple ROIs are selected in the navigator, the loci display in split panes.</td>
		</tr>
		<tr>
			<td style="width: 164px;">
				<em>Zoom to Region</em></td>
			<td style="width: 353px;">
				Uncheck to keep the current zoom level when navigating to a new ROI. Check to ensure IGV adjusts the zoom level to display the entire ROI when navigating to the new ROI.</td>
		</tr>
	</tbody>
</table>

## Importing/exporting regions

In the menu bar, select _Regions > Export Regions..._ to saves all currently defined regions of interest to a BED file. If no regions of interest are defined, no BED file is created.

Select _Regions > Import Regions..._ to select a BED file of regions to add to the set of regions of interest.

# Gene Lists

To view a gene list or define a new one, select _Regions >Gene Lists..._.

![](img/regions_gene_list.png)


This opens a window for selecting an existing list or creating a new list.

![](img/genelist_window_2.jpg)

To view an existing gene list in multi-locus view, select a name in the _List_ column of any _Group_ and click _View_. IGV informs you of items that cannot be mapped to the current reference genome and continues on to display loci with matches.

![](img/genelist_select_2.jpg)

## My gene Lists

You can click _Import_ to upload a text file containing your own gene list. Load lists of genes or loci in [GMT](https://genepattern.org/file-formats-guide#GMT), [GRP](https://genepattern.org/file-formats-guide#GRP) or [BED](../FileFormats/DataTracks.md) format. For example, find and download GMT files from the [Molecular Signatures Database (MSigDB)](https://msigdb.org).

You can also click _New_ to create a new gene list. This opens a dialog in which you can enter a name, description, and your list of genes or regions.

*   Entries in a gene list can be a gene symbol or other feature names that correspond to annotation tracks, or a locus defined as  ```<chr>:<start>-<end>```.
*   Alternatively, paste a BED format file contents.

![](img/genelist_new.jpg)

New and imported lists will appear under the _My lists_ group and are saved for continued future access in the _lists_ subfolder in the _igv_ folder installed in your home directory.

