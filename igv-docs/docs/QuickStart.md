
<!---
The page title should not go in the menu
-->
<p class="page-title">Quick Start </p>


### 1. Download and launch IGV

The IGV desktop application is a Java program that runs on your computer. To run IGV, go to the [**Download** page](DownloadPage.md) and download the installer that is appropriate for your system. 

When you first launch IGV, it will create a folder named **igv** in your user's home folder. In this folder, IGV will store:

* A log file used to record important information about each IGV run, including any error information;
* Information about your user preferences; and
* Information about the reference genomes you have loaded.

!!! note " " 
    IGV is also available as a web application that runs in a web browser and requires no downloads. See [https://igv.org/app](https://igv.org/app). Click on the Help link in the app for more information about using IGV-Web. 

### 2. Load a reference genome
IGV displays data mapped to the genomic coordinates of a reference genome. The datasets you load must correspond to the same reference genome as the one you have loaded into IGV; and so it is important you load the correct one. When you first launch the IGV application, it will load the default reference genome (as of this writing **hg19**). See the section on [Reference genomes](UserGuide/reference_genome.md) for details on how to switch to a different reference genome. You can either select one of IGV's hosted genomes or provide your own genome files. When you re-launch IGV, it will load the reference genome you were using when you last closed down the IGV application.

!!! tip " "
    You must first load the desired reference genome, before loading data tracks. Switching genomes will clear out any loaded tracks.

### 3. Load data

Data and genome annotations are loaded via the *File* menu, from the local file system, via URL, or from a hosted IGV server. See the section on [Loading and removing data](UserGuide/loading_data.md) for the details. 

The data files are displayed as horizontal tracks stacked on top of the reference genome. The display attributes of the tracks depend on the data type. IGV determines the data type based on the filename extension of the file that was loaded. See [File Formats](../FileFormats/DataTracks.md) for information about the file formats IGV accepts for data tracks and the ***Tracks and Data Types*** section of the  ***User Guide*** describes the attributes of the various track types.

!!! tip " " 
    Make sure to load only data files that correspond to the current reference genome. In general, a genomic data file does not include information about the particular genome assembly it was aligned to, which means IGV cannot automatically check if they match.

### 4. Navigate

IGV-Web provides several navigation controls for specifying the genomic region to view. A ruler indicating the extent of the current region is displayed below the toolbar, and the size of the region and its genomic coordinates are displayed in the toolbar. See [Navigating the view](UserGuide/navigation.md) for details.

### 5. Save the IGV view

Saving a [session](UserGuide/sessions.md) file will allow you to **save the state of your current IGV view** so you can reproduce it at another time and continue where you left off. The data files themselves are not stored in the session, but rather the information needed to reload them. You can also share session files with others, as long as they also have access to the same data files.

Select *File > Save PNG image...* or *File > Save SVG image...* to **create a static image** of the IGV window. Alternatively, you can create an image of only selected tracks via the track pop-up menu.

