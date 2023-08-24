<!---
The page title should not go in the menu
-->
<p class="page-title"> Sample attributes</p>

Attributes can be associated with tracks and used for filtering, sorting, and grouping data. By default all tracks have 
at least 3 attributes: Data File, Data Type, and Name. To display additional attributes, [load a sample attribute file](../FileFormats/SampleInfo.md). 
IGV displays attribute names and values in the attributes panel between the name panel and the data panel.

## Color-coded attribute values

IGV uses color-coded blocks to represent the attribute values. If two samples have the same color block for a particular attribute, both samples have the same value for that attribute. However, the colors are chosen at random and different sessions of IGV may not use the same colors.

![](img/attributes.jpg)

* Hover over a colored block to **display the attribute value**.

* Click a colored block to **select all tracks with that attribute value**. IGV indicates a selected track by highlighting the track name.  Keep in mind that clicking an attribute *may select tracks that are not visible in the data panel*. Scroll down the data panel to view all the selected tracks.
        
* Click an attribute name at the top of the panel to **sort tracks based on that attribute value**.

## Showing and hiding attributes

To show or hide **selected** attributes:

* Select _View > Select Attributes to Show..._ to see the list of attributes. Check (or clear) an attribute’s check box to show (or hide) the attribute.

To show or hide **all** attributes:

*   Select _View > Show Attribute Display_ to toggle the setting. A check mark next to the menu item indicates that the attribute panel is displayed. No check mark indicates that it is hidden. 

!!! note " "  
    This is a persistent setting. Toggling the menu item also toggles the corresponding setting on the *General* tab of the _View > Preferences_ window.