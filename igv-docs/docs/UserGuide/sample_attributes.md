<!---
The page title should not go in the menu
-->
<p class="page-title"> Sample attributes</p>

Attributes can be associated with tracks and used for filtering, sorting, and grouping data. By default all tracks have 
at least 3 attributes: Data File, Data Type, and Name. To display additional attributes, [load a sample attribute file](../FileFormats/SampleInfo.md). 
IGV displays attribute names and values in the attributes panel.

## Color-coded attribute values

IGV uses color-coded blocks to represent the attribute values.

* Hover over a colored block to display the attribute value.
* Click a colored block to select all tracks with that attribute value. IGV indicates a selected track by highlighting 
* the track name.  **Tip**: Keep in mind that clicking an attribute may select tracks that are not visible in the data 
* panel. Scroll down the data panel to view all the selected tracks.
* Click an attribute name at the top of the panel to sort tracks based on that attribute value.

![](img/attributes.jpg)

## Showing and hiding Attributes

To show or hide selected attributes:

1.  Click _**View>Select Attributes to Show**_. IGV displays a list of attributes.
2.  Select (or clear) an attribute’s check box to show (or hide) the attribute.
3.  Click _**OK**_. IGV updates the display to show only the selected attributes.

To show or hide all attributes:

*   Click _**View>Show Attribute Display**_ to toggle the setting. A check mark next to the menu item indicates that the attribute panel is displayed. No check mark indicates that it is hidden. The attribute panel is hidden by default. 

!!! note " "  
    This is a persistent setting. Toggling the menu item also toggles the corresponding setting on the General tab of the _**View > Preferences**_ window and vice versa.