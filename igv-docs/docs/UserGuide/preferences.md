<!---
The page title should not go in the menu
-->
<p class="page-title"> User preferences </p>

The prefs.properties file saves IGV user settings changed during use, typically from the various Preferences panels. For example, IGV opens each new session with the last used reference genome and this information is saved in the prefs.properties file.

To restore IGV's default preferences, delete or rename the prefs.properties file. When you open IGV, a new prefs.properties file is created with default settings.
Renamed files allow you to save particular settings that you may reapply to IGV sessions by naming the file back to prefs.properties.

The table below outlines additional changes to settings made directly to the prefs.properties file that are currently unavailable from IGV's user interface.

Exercise caution when editing the prefs.properties file directly by creating a backup duplicate copy of the original, as errors in modification may cause IGV to behave in unconventional ways without informing you of such discrepancies or errors. For example, if your text editor appends a .TXT file extension to the prefs.properties file, IGV ignores this file and creates a new prefs.properties file with all settings reset to default.

Open the prefs.properties file with a plain-text editor from the IGV installation folder on your system. You can find the location of this folder listed at the bottom of View>Preferences>Advanced.
Type in new preferences and save the file before opening IGV.
RGB (red, green, and blue light) refers to a system of representing colors for computer display with zero representing absence and 255 giving maximum light for a color in comma-separated values. Look up RGB values by color wheel at https://color.adobe.com/create/color-wheel/.

| Description  | Command | Example |
|----------|----------|-----------|
| Nucleotide colors in the reference track | COLOR.A <br> COLOR.C <br> COLOR.T <br> COLOR.G <br> COLOR.N | COLOR.A=0,0,0 <br> Sets adenosine nucleotides to RGB color scheme 0,0,0 (black). |
| BAM and SAM track alignment nucleotide colors | SAM.COLOR.A <br> SAM.COLOR.C <br> SAM.COLOR.T <br> SAM.COLOR.G <br> SAM.COLOR.N | SAM.COLOR.C=255,0,255 <br> Sets cytosine nucleotides to RGB color scheme 255,0,255 (magenta).|


 

 