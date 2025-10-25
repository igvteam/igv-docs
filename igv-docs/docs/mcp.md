<p class="page-title"> IGV MCP Server </p>

This page contains instructions for installing an MCP (Model-Controller-Protocol) server to allow programmatic control
of the [Integrative Genomics Viewer (IGV)](https://igv.org/) via MCP-compatible clients such as Claude.

## Installation

1. Download 'igv.mcpb' from []()
2. Install the package in your MCP client (e.g., Claude Desktop) following the client's instructions for installing MCP
   packages. Instructions for Claude Desktop can be
   found [here](https://support.claude.com/en/articles/10949351-getting-started-with-local-mcp-servers-on-claude-desktop).
   Follow the instructions for installing 'custom desktop extensions'.
3. Ensure you have IGV installed and enable the port listener in IGV:
    - Open IGV
    - Go to `View > Preferences > Advanced ` and select `Enable port listener`

The Claude desktop should now be able to start the IGV MCP server and communicate with IGV. To test ask Claude to
"Summarize the tools available to interact with IGV" or similar.

## Tools

The server currently provides 22 tools for interacting with IGV. These are listed below for reference, but it's not
necessary to reference these tools explicitly. You can use natural language commands such as "Load the hg38 genome", "Go
to locus BRCA1", "Zoom in", "Take a snapshot", etc. and the MCP server will map these to the appropriate tools.

### Session Management

- `new` - Reset IGV to a clean state by unloading all data tracks
- `saveSession` - Save the current IGV session

### Genome & Data Loading

- `genome` - Load a reference genome by ID (e.g., hg38, mm10) or file path
- `load` - Load data files (BAM, SAM, VCF, etc.)

### Navigation & View Control

- `goto` - Navigate to a genomic locus
- `zoomin` - Zoom in the view
- `zoomout` - Zoom out the view

### Track Visualization

- `collapse` - Collapse track to compact representation
- `squish` - Squish track by reducing row height
- `expand` - Expand track by increasing row height
- `setColor` - Set the primary display color for tracks

### Region of Interest

- `region` - Define a region of interest

### Alignment Track Organization

- `group` - Group alignment reads by properties
- `sort` - Sort reads by various criteria
- `viewAsPairs` - Toggle paired-end read visualization mode

### Sequence Track

- `setSequenceStrand` - Set which DNA strand to display
- `setSequenceShowTranslation` - Toggle translation display

### Track Overlay

- `overlay` - Combine multiple wig tracks into a single overlaid track
- `separate` - Separate an overlaid wig track into component tracks

### Snapshots

- `snapshot` - Capture a snapshot image of the current IGV view
- `snapshotDirectory` - Set the directory where snapshots will be saved
- `maxPanelHeight` - Set maximum height for track panels in snapshots
