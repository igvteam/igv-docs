<!---
The page title should not go in the menu
-->
<p class="page-title">Track hubs </p>

**NEED TO UPDATE THIS TEXT - IT WAS WRITTEN FOR RELEASE NOTES**

Hosted tracks that previously were loaded via the _File > Load from Server_ menu are now made available through the **Track Hubs** menu. The tracks are organized into categories that are listed at the top of the menu. Click on a category name to see the list of available tracks in that category. 

At the bottom of the _Track Hubs_ menu are two items for connecting to **UCSC-style track hubs**.

1. Click on _Select Track Hubs_ to open a window that lists all public track hubs from **the UCSC Track Hub Registry** that are relevant for the current reference genome. The list is retrieved in real time from the UCSC server, so it is always up to date. The list can be **filtered** by typing one or more terms in the search box at the top of the window. Or **sort** the list by clicking on any of the column headers. **Select** one or more hubs by checking the boxes by their name and then click the _OK_ button to add them to the _Track Hubs_ menu.

2. Click on _Add Track Hub from URL_ to access **any track hub by entering its URL**. This opens a window in which you can paste the URL of the hub's `hub.txt` file and clicking ok will add the hub to the *Track Hubs* menu. The URL can link to a hub on your local intranet or a public hub on the internet. 

To **load tracks from a hub** that was added to the *Track Hubs* menu by either of the above methods, click on the hub name in the menu. This opens a window that lists all tracks in the hub. A warning will be presented if the hub does not contain any tracks that are compatible with IGV. Select one or more tracks by checking the boxes by their name, and click _OK_ to load them.

To **remove hubs from the menu**, click on _Select Track Hubs_, uncheck the hubs to be removed, and click _OK_. If any hubs are added by URL, they are also added to the list in the _Select Track Hubs_ window and can be removed in the same way.

!!! Tip " " 
    The hubs remain in the _Track Hubs_ menu across IGV sessions. The state of the menu is stored in the `hubs.txt` file in the `igv` folder in your user home folder. 