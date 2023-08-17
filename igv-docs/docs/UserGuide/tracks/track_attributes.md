
<!---
The page title should not go in the menu
-->
<p class="page-title"> Track attributes </p>


Each track has a set of attributes that varies depending on the track type. For example, alignment tracks have attributes that are specific to the display of the read alignments. Some attributes are common across track types. For example, all tracks have a track name.

# Setting track attributes
Many of the track attributes are also user settable: 

To **set a attribute value for a specific track**, right-click on the track (either in the data panel or the track name) to bring up a pop-up menu that is specific to the track type.

!!! note " "
    Some attributes can be set on multiple tracks at the same time. First, select all the tracks and then right click on one of them to bring up the pop-up menu. You can select multiple tracks either by using the normal multi-select mouse actions (e.g. CTRL-click on Windows; CMD-click on Mac) or by clicking an attribute in the [sample attribute panel](../sample_attributes.md) to select all tracks tagged with that attribute value.
   
Select *View > Preferences* to **change the default value for an attribute** for a particular track type. Not all default values are user settable.

In some cases, attribute values can be set via actions in the main IGV menu.


# Track-independent attributes

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

## Track name

Track names are displayed in a panel to the left the track data, and to the left of the sample attribute panel if it is displayed.

* To **hide the name panel**, unselect *View > Show Name Panel*.

* To **resize the name panel**, select *View > Set Name Panel Width...*

By default, tracks are assigned names based on the **name** sample attribute. If you have loaded additional [sample attributes](../sample_attributes.md), you can use a different attribute to define the **default track name**:

*   Enter the sample attribute name in the field *Sample attribute key for track names* in *View > Preferences > Tracks*.

To set a track name to a **specific string**:

*   Right-click the track, then select _Rename Track..._ in the pop-up menu.

!!! tip " "
    You can only rename one track at a time. 
    
!!! note " " 
    Name changes will be preserved if you save a [session](../../sessions).
    










