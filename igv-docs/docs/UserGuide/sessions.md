# Saving and Restoring Sessions


You can save the current state of an IGV session to a named session file. You can use that file to restore the IGV
session yourself or share it with colleagues, as long as they have access to the session file and any data files that
were loaded when the session file was saved. For example, if the data files are loaded into IGV from a shared directory
and the IGV session file is saved to that shared directory, anyone with access to the directory can restore the saved
IGV session.

To save a session:

1. Click _File>Save Session_.
2. In the Save Session window, select a directory and session file name and click _OK_.

To restore a saved session:

1. Click _File>Open Session_.
2. In the Open Session window, select a session file and click _OK_. IGV ends the current session and restores the saved
   session.

To reload a previously loaded session:

# Session File Format

## IGV Version 1.5 and Greater

### Overview

Sessions are an integral part of IGV, allowing users to share their data and views with other users simply and
accurately. Session files describe the session in XML. If you wish to manually create or edit a session file, use the
information below to better understand the components of each session file.

### Session XML Hierarchy

*   <Session>
    *   <Resources>
        *   <Resource>
    *   <Panel>
        *   <Track>
            *   <DataRange>

### Description of Session Components

Required - These elements are required in a session file. All session files must follow XML standards.

* <Session>: Contains information about the general state of IGV when the session was saved
    * genome= The genome id.
        * _**New - IGV 2.1or later only**_. A file path or URL to an indexed fasta or .genome file can be used in place
          of the genome id. The path can be absolute or relative to the parent directory of the session file.
    * locus= The genomic range selected when the session was saved
    * version= The session version (this must equal '3')
* <Resources>: An enclosing element for all Resource elements
* <Resource>: Contains the location and other important information for your data files; for instance, a Resource could
  be a DAS server, BED file, or sequence alignment
    * name= The name of the track for single track files
    * path= The path or URL to the track file
    * index= An option path or URL to an index file
    * url= An optional url to associate with features of the track

Optional - These elements are optional in a session file and are added by IGV to help determine the placement of the
data and visual style choices.

* <Panel>: Contains information about the placement of Tracks in the visual panels
    * name= The display name for the Panel
    * height= The default height for the Panel
    * width= The default width for the Panel
* <Track>: Details information about every track in a session
    * color= The default color for the data in the track
    * expand= Whether the track is expanded or not
    * height= The default height of the track
    * id= The id assigned by IGV to this track
    * name= The display name for the track
    * renderer= The renderer to be used with this Track (non-default)
    * visible= Whether the track is visible or loaded in the background
    * windowFunction= The function to be used when displaying data
* <DataRange>: A set of attributes used to determine the look of the Panel
    * baseline=
    * drawbaseline=
    * flipAxis=
    * maximum=
    * minimum=
    * type=

### Example Session File

The XML below is an example of a simple Session created by IGV

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