<!---
The page title should not go in the menu
-->
<p class="page-title"> Loading and removing data </p>

# Loading data

Data can be loaded from local files, URLs, or via the IGV hosted data menu. See [File Formats](../FileFormats/DataTracks.md) for information about the file formats IGV accepts for data tracks.

To **load data from the local file system** or other file systems you have mounted:

1.  Select _File > Load from File_. IGV displays the Select Files window.
2.  Select one or more data files or sample information files, then click _OK_.

To **load data that is accessible via URL** on a local intranet or the internet:

1.  Select _File > Load from URL_.
2.  Enter the URL for a data file or sample information file; If the file is indexed, make sure to enter the index file name in the field provided; Click _OK._

!!! note "" 
    For BAM, TDF, and indexed file formats the web server must support HTTP byte-range requests.

To **load IGV hosted data**:

1.  Select _File > Load from Server_. The Available Datasets window appears. The Available Datasets are specific to the current reference genome. Not all genomes have corresponding hosted datasets.  
    ![](img/load_from_server.jpg)
        
2.  Expand the tree to see the datasets; Click the checkboxes to select one or more dataset; Click _OK_.
!!! tip " "
    Be aware that clicking on a folder checkbox selects all of its subfolders and all of the datasets in those folders. This can potentially be a huge amount of data. To be sure you are loading only the data you want, open collapsed folders and select only the datasets of interest.


# Removing tracks 

To remove **all** tracks:

*   Select _File > New Session_. This is essentially the same as restarting IGV. The reference genome tracks are not removed.

To remove **specific** tracks, do one of the following:

*   Right-click on a track (either in the data panel or the track name) and select _Remove Tracks_ in the pop-up menu.
*   Select multiple tracks and then right-click on one of the selected tracks and select _Remove Tracks_ in the pop-up menu. You can select multiple tracks either by using the normal multi-select mouse actions (e.g. CTRL-click on Windows; CMD-click on Mac) or by clicking a sample attribute value to select all tracks tagged with that attribute value.

 

 