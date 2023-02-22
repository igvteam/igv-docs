<!---
The page title should not go in the menu
-->
<p class="page-title"> Sessions </p>

You can save the current state of an IGV session to a named session file. You can use that file to restore the IGV
session yourself or share it with colleagues, as long as they also have access to any data files that
were loaded when the session file was saved. For example, if the data files are loaded into IGV from a shared directory
and the IGV session file is saved to that shared directory, anyone with access to the directory can restore the saved
IGV session.

# Saving and using sessions

To save a session:

* Click _**File > Save Session**_.
* Use the _Save Session_ window that pops up to select a target directory and file name for the new session file.

To restore a saved session:

* Click _**File > Open Session**_.
* Use the _Open Session_ window that pops up to select a session file. IGV ends the current session and restores the saved session.

To reload a previously loaded session:

* Click _**File  > Reload Sessio**n_.

To clear the current session: 

* Click _**File > New Session**_. This removes all data tracks and resets the view, but does not change the reference genome.


# Session file format

!!! note " "  
    The following description is for IGV version 2.1 and greater


 Session files describe the session in XML. If you wish to manually create or edit a session file, use the
information below to better understand the components of each session file.

### Session XML hierarchy

```
<Session>
     <Resources>
          <Resource>
     <Panel>
          <Track>
              <DataRange>
```

### Session components
#### Required
These elements are required in a session file. All session files must follow XML standards.

* _**<Session\>**_ Contains information about the general state of IGV when the session was saved
    * _genome_ = The genome id.
        * A file path or URL to an indexed fasta or .genome file can be used in place
          of the genome id. The path can be absolute or relative to the parent directory of the session file.
    * _locus_ = The genomic range selected when the session was saved
    * _version_ = The session version (this must equal '3')
* _**<Resources\>**_ An enclosing element for all Resource elements
* _**<Resource\>**_ Contains the location and other important information for your data files
    * _name_ = The name of the track for single track files
    * _path_ = The file path or URL to the track file
    * _index_ = An optional path or URL to an index file
    * _url_ = An optional URL to associate with features of the track

#### Optional 
These elements are optional in a session file and are added by IGV to help determine the placement of the
data and visual style choices.

* _**<Panel\>**_ Contains information about the placement of Tracks in the visual panels
    * _name_ = The display name for the Panel
    * _height_ = The default height for the Panel
    * _width_ = The default width for the Panel
* **<Track\>** Details information about every track in a session
    * _color_ = The default color for the data in the track
    * _expand_ = Whether the track is expanded or not
    * _height_ = The default height of the track
    * _id_ = The id assigned by IGV to this track
    * _name_ = The display name for the track
    * _renderer_  = The renderer to be used with this Track (non-default)
    * _visible_ = Whether the track is visible or loaded in the background
    * _windowFunction_ = The function to be used when displaying data
* _**<DataRange\>**_ A set of attributes used to determine the look of the Panel
    * _baseline_ =
    * _drawbaseline_ =
    * _flipAxis_ =
    * _maximum_ =
    * _minimum_ =
    * _type_ =

### Example session file

The XML below is an example of a simple session created by IGV.

```
<?xml version="1.0" encoding="UTF-8"?>
<Global genome="hg18" locus="All" version="3">
  <Resources>
    <Resource url="http://genome.cse.ucsc.edu/cgi-bin/hgTrackUi?g=rnaGene" label="RNA Genes" name="RNA Genes" path="http://www.broadinstitute.org/igvdata/annotations/hg18/rna\_genes.bed"/>
    <Resource url="http://genome.cse.ucsc.edu/cgi-bin/hgTrackUi?g=wgRna" label="sno/miRNA" name="sno/miRNA" path="http://www.broadinstitute.org/igvdata/annotations/hg18/sno\_mirna.bed"/>
  </Resources>
  <Panel height="445" name="DataPanel" width="1000">
    <Track color="0,0,178" colorScale="ContinuousColorScale;0.0;20.0;255,255,255;0,0,178" displayName="Non coding RNA" expand="false" height="45" id="http://www.broadinstitute.org/igvdata/annotations/hg18/rna\_genes.bed" name="RNA Genes" renderer="BASIC\_FEATURE" visible="true" windowFunction="count">
      <DataRange baseline="0.0" drawBaseline="true" flipAxis="false" maximum="20.0" minimum="0.0" type="LINEAR"/>
    </Track>
    <Track color="0,0,178" colorScale="ContinuousColorScale;0.0;20.0;255,255,255;0,0,178" displayName="sno miRNA" expand="false" height="45" id="http://www.broadinstitute.org/igvdata/annotations/hg18/sno\_mirna.bed" name="sno/miRNA" renderer="BASIC\_FEATURE" visible="true" windowFunction="count">
      <DataRange baseline="0.0" drawBaseline="true" flipAxis="false" maximum="20.0" minimum="0.0" type="LINEAR"/>
    </Track>
  </Panel>
  <Panel height="65" name="FeaturePanel" width="1000">
    <Track color="0,0,178" colorScale="ContinuousColorScale;0.0;20.0;255,255,255;0,0,178" displayName="RefSeq genes" expand="false" height="30" id="Genes" name="Genes" renderer="BASIC\_FEATURE" visible="true" windowFunction="count">
      <DataRange baseline="0.0" drawBaseline="true" flipAxis="false" maximum="20.0" minimum="0.0" type="LINEAR"/>
    </Track>
  </Panel>
</Global>
```