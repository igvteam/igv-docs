<!---
The page title should not go in the menu
-->
<p class="page-title"> Sessions </p>

You can save the current state of an IGV session to a named session file. The IGV session file contains references to the data files, 
but not the data files themselves.You can use that file to restore the IGV session yourself or share it with colleagues, 
as long as they also have access to any data files that
were loaded when the session file was saved. For example, if the data files are loaded into IGV from a shared directory
and the IGV session file is saved to that shared directory, anyone with access to the directory can restore the saved
IGV session. 

# Saving and using sessions

To save a session:

* Click _**Sessions > Save Session**_.
* Use the _Save Session_ window that pops up to select a target directory and file name for the new session file.

To restore a saved session:

* Click _**Sessions > Load Session from File**_. Use the _Open Session_ window that pops up to select a session file. IGV ends the current session and restores the saved session.

* Click _**Sessions > Load Session from URL**_. Use the _Load Session from URL_ window that pops up to enter the URL of a session file. IGV ends the current session and restores the saved session.

To reload the last loaded session:

* Click _**Sessions > Reload Session**_. This can be useful if you have made changes since you loaded a session file and want to revert to the same state as that session.

To clear the current session: 

* Click _**Sessions > New Session**_. This removes all data tracks, but does not change the view or the reference genome.


# Session autosave

IGV supports the ability to autosave your current session in the `igv/autosave` directory.  These session files can then be loaded through the *Sessions > Autosaved Sessions* menu.  

Two autosave methods are supported:

### 1. Autosave on exit
Whenever you exit IGV, a copy of your current session will be saved to the `igv/autosave` directory with the name `exit_session_autosave.xml`.  Each time you exit IGV, that file will be overwritten with a new save of the current session.

**Autosave on exit is enabled by default**.  Autosave on exit can be enabled/disabled via  the *General* tab in *View > Preferences*.

### 2. Timed autosave
You have the option of enabling a periodic autosave of your current session in IGV.  This works by saving a copy of your current session every x minutes to the `igv/autosave` directory, named in the form `session_autosave[timestamp].xml` where `[timestamp]` is the current date and time at the time of the autosave, in [ISO 8601 UTC date and time format](https://en.wikipedia.org/wiki/ISO_8601).   

**Timed autosave is disabled by default.** There are two options in the *General* tab of the *View > Preferences* window menu for timed autosave.  You can set how often the autosave should be done by setting the value for *How often, in minutes, to autosave the current session*.  You can set how many autosave files created by the timed autosave to keep by setting the value for *How many timed autosave session files to keep*.  Setting this option to 0 (which is the default) disables timed autosave.

### Autoload
IGV provides the option to automatically load your last autosave on startup.  This can be enabled in the *General* tab of the *View > Preferences* window.  If this is enabled, when you open IGV, the most recent session file in the `igv/autosave` directory will be loaded, if there is one.  This setting will be ignored if running IGV from the command line or specifying a file to open on start.

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
    * _version_ = The session file version number
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
* **<Track\>** Details information about a track
    * _color_ = The default color for the data in the track
    * _expand_ = Whether the track is expanded or not
    * _height_ = The default height of the track
    * _id_ = The id assigned by IGV to this track
    * _name_ = The display name for the track
    * _renderer_  = The renderer to be used with this Track (non-default)
    * _visible_ = Whether the track is visible or loaded in the background
    * _windowFunction_ = The function to be used when displaying data
* _**<DataRange\>**_ A set of attributes used to determine the look of the track
    * _baseline_ =
    * _drawbaseline_ =
    * _flipAxis_ =
    * _maximum_ =
    * _minimum_ =
    * _type_ =

### Example session file

The XML below is an example of a simple session created by IGV 3.0.

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Session genome="hg19" locus="chr3:34001103-55081786" nextAutoscaleGroup="2" version="8">
    <Resources>
        <Resource name="SK-N-SH SMC3 ChIP-seq signal" path="https://www.encodeproject.org/files/ENCFF000ZSX/@@download/ENCFF000ZSX.bigWig" type="bigwig"/>
        <Resource name="HepG2 POLR2A ChIP-seq raw signal" path="https://www.encodeproject.org/files/ENCFF000PNJ/@@download/ENCFF000PNJ.bigWig" type="bigwig"/>
    </Resources>
    <Panel height="263" name="DataPanel" width="1662">
        <Track attributeKey="HepG2 POLR2A ChIP-seq raw signal" autoScale="true" clazz="org.igv.track.DataSourceTrack" fontSize="10" id="https://www.encodeproject.org/files/ENCFF000PNJ/@@download/ENCFF000PNJ.bigWig" name="HepG2 POLR2A ChIP-seq raw signal" renderer="BAR_CHART" visible="true" windowFunction="mean">
            <DataRange baseline="0.0" drawBaseline="true" flipAxis="false" maximum="2.7678254" minimum="0.0" type="LINEAR"/>
        </Track>
        <Track attributeKey="SK-N-SH SMC3 ChIP-seq signal" autoScale="false" clazz="org.igv.track.DataSourceTrack" color="102,51,0" fontSize="10" id="https://www.encodeproject.org/files/ENCFF000ZSX/@@download/ENCFF000ZSX.bigWig" name="SK-N-SH SMC3 ChIP-seq signal" renderer="BAR_CHART" visible="true" windowFunction="mean">
            <DataRange baseline="0.0" drawBaseline="true" flipAxis="false" maximum="21.362701" minimum="0.0" type="LINEAR"/>
        </Track>
    </Panel>
    <Panel height="87" name="FeaturePanel" width="1662">
        <Track attributeKey="Reference sequence" clazz="org.igv.track.SequenceTrack" fontSize="10" id="Reference sequence" name="Reference sequence" sequenceTranslationStrandValue="+" shouldShowTranslation="false" visible="true"/>
        <Track attributeKey="Refseq All" clazz="org.igv.track.FeatureTrack" fontSize="10" groupByStrand="false" id="https://hgdownload.soe.ucsc.edu/goldenPath/hg19/database/ncbiRefSeq.txt.gz" name="Refseq All" visible="true"/>
    </Panel>
</Session>
```