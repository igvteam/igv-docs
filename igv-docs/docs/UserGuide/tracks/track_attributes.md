
<!---
The page title should not go in the menu
-->
<p class="page-title"> Track attributes </p>


Each track has a set of attributes that varies depending on the track type. For example, alignment tracks have attributes that are specific to the display of the read alignments. Some attributes are common across track types. For example, all tracks have a track name.

# Setting track attributes
Many of the track attributes are also user settable: 

To **set a attribute value for a specific track**, right-click on the track (either in the data panel or the track name) to bring up a pop-up menu that is specific to the track type.

!!! tip " "
    Some attributes can be set on multiple tracks at the same time. First, select all the tracks of interest and then right click on one of them to bring up the pop-up menu. You can select multiple tracks either by using the normal multi-select mouse actions (e.g. `Ctrl-click` on Windows; `Cmd-click` on MacOS) or by clicking an attribute in the [sample attribute panel](../sample_attributes.md) to select all tracks tagged with that attribute value.
   
Select *View > Preferences* to **change the default value for an attribute** for a particular track type. Not all default values are user settable.

In some cases, attribute values can be set via actions in the main IGV menu.


# Common track attributes

## Track color

To change the color for tracks displayed as a heatmap:

*   Right-click the track and select _Set Heatmap Scale..._ from the pop-up menu.

To change the color for tracks that are displayed as something other than a heatmap (e.g, bar chart, scatter plot, line plot, alignments):

*   Right-click the track and from the pop-up menu select either _Change Track Color..._ or _Change Track Color (Negative Values or Strand)..._.

## Track height

To change the height of **selected** tracks:

*   Select _Change Track Height..._ from the track pop-up menu.

To change the height of **all** tracks:

*   Select _Tracks > Set Track Height..._ in the main IGV menu.

To change the **default height** of tracks:

* The *Tracks* tab in *View > Preferences* has fields to set the default height for numeric/quantitative tracks and for feature/genome annotation tracks.

## Track name

Tracks are assigned default names, typically based on the file name or the names of samples contained in the file.

If you have loaded [sample attributes](../sample_attributes.md), you can specify an attribute to define the **default track name**:

*   Enter the sample attribute name in the field *Sample attribute key for track names* in *View > Preferences > Tracks*.

To set a track name to a **specific string**:

*   Right-click the track, then select _Rename Track..._ in the pop-up menu. You can only rename one track at a time.

The track names are displayed in a panel to the left the track data, and to the left of the sample attribute panel if it is displayed.

* To **hide the name panel**, unselect *View > Show Name Panel*.

* To **resize the name panel**, select *View > Set Name Panel Width...*









