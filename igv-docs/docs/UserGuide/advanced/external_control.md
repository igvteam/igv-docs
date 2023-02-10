# Port commands

IGV can optionally listen for http requests over a port. By default the port number is 60151, this can be changed (or the port disabled)
int the Advanced tab of the Preferences window.

**Note:**  IGV will write a response back to the port socket upon completion of each command. It is good practice to
read this response before sending the next command. Failure to do so can overflow the socket buffer and cause IGV to
freeze. See the example below for the recommended pattern.

## Commands

See [Batch Scripting](../tools/batch.md) for the complete list of commands.

## Example

Example java code:

Socket socket = new Socket("127.0.0.1", 60151);  
PrintWriter out = new PrintWriter(socket.getOutputStream(), true);  
BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

out.println("load na12788.bam,n12788.tdf");  
String response = in.readLine();  
System.out.println(response);

out.println("genome hg18");  
response = in.readLine();  
System.out.println(response);

out.println("goto chr1:65,827,301");  
//out.println("goto chr1:65,839,697");  
response = in.readLine();  
System.out.println(response);

out.println("snapshotDirectory /screenshots");  
response = in.readLine();  
System.out.println(response);

out.println("snapshot");  
response = in.readLine();  
System.out.println(response);

# HTML Links

Data and session files can be loaded into IGV from a web browser or other application supporting hyperlinks. This makes
use of the listener port.  **To use this option you must enable the port listener on the Advanced tab of the Preferences
window, accessed from the View menu.**   Links can be created to load data or jump to a locus as follows.

http://localhost:_port_/load?file=_URL_&locus=_locus_&genome=_genome&_merge_\=\[__true|false\]&_name_\=name_

http://localhost:_port_/goto?locus=_locus_

* The **_file_** parameter value can be a URL or a comma-delimited list of URLs to most IGV-supported data file types (
  exceptions listed below), or a session file.
* The **_merge_** parameter (optional) controls whether or not the loaded data is merged with the existing IGV session,
  or a loaded into a new session. If false, any data currently loaded will be unloaded after clicking this link. The
  default value is true. The **_merge_** paramater is ignored if loading a session; loading a session will alway unload
  the previous session.
* The **_name_** parameter (optional) specifies a name or names for the track. If multiple tracks are loaded as a
  comma-delimited list, the name parameter value should also be a comma-delimited list of the same size. The _**name**_
  parameter is ignored if loading a session.

## Examples:

[http://localhost:60151/load?file=http://www.broadinstitute.org/igvdata/annotations/hg18/conservation/pi.12mer.wig.tdf&locus=egfr&genome=hg18](http://localhost:60151/load?file=http://www.broadinstitute.org/igvdata/annotations/hg18/conservation/pi.12mer.wig.tdf&locus=egfr&genome=hg18)

[http://localhost:60151/load?file=http://www.broadinstitute.org/igvdata/exampleFiles/gbm\_session.xml&merge=true](http://localhost:60151/load?file=http://www.broadinstitute.org/igvdata/exampleFiles/gbm_session.xml&merge=true)

[http://localhost:60151/goto?locus=egfr](http://localhost:60151/goto?locus=egfr)

# Batch scripts

As of version 1.5, a user can load a text file to execute a series of sequential tasks by using Tools>Run Batch Script. The user loads a TXT file that contains a list of commands, one per line, that will be run by IGV. Arguments are delimited by spaces (NOTE: not tabs). Lines beginning with # or // are are skipped. 
See [Batch Scripts in the Tools Menu](../tools/batch.md) for further details.
