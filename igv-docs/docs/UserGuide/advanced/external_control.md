<!---
The page title should not go in the menu
-->
<p class="page-title"> External control of IGV </p>


This section describes how a running IGV application can be controlled through a sequence of commands.


# Batch scripts

A user running the IGV application can load a text file to execute a series of commands by selecting ***Run Batch Script*** from the ***Tools*** menu. See [Batch scripts in the Tools Menu](../tools/batch.md) for further details.

# Port commands

IGV can optionally listen for commands over a port. By default the port number is 60151. The port number can be changed and the port listening can be disabled in the ***Advanced*** tab of the ***View > Preferences*** window. 

The port commands are the same as the batch script commands. See [Batch scripts in the Tools Menu](../tools/batch.md) for a full list.

!!! note " "
    The IGV application must already be running. There is no command to launch IGV.

!!! note " "
    IGV will write a response back to the port socket upon completion of each command. It is good practice to read this response before sending the next command. Failure to do so can overflow the socket buffer and cause IGV to freeze. See the example below for the recommended pattern.

### Example

An example of a Java code snippet that sends IGV commands to the listener port:

```
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
response = in.readLine();  
System.out.println(response);

out.println("snapshotDirectory/screenshots");  
response = in.readLine();  
System.out.println(response);

out.println("snapshot");  
response = in.readLine();  
System.out.println(response);
```

# HTML links

Data and session files can be loaded into IGV from a web browser or other application supporting hyperlinks. This makes
use of the listener port.  By default the port number is 60151. The port number can be changed and the port listening can be disabled in the ***Advanced*** tab of the ***View > Preferences*** window. 

Links can be created to set the reference genome, load data, or jump to a specified locus as follows.


http://localhost:_PORT_/load?file=_URL_&locus=_LOCUS_&genome=_GENOME_&merge=\[_true_|_false_\]&name=_NAME_

http://localhost:_PORT_/goto?locus=_LOCUS_


* The **_file_** parameter value can be a URL or a comma-delimited list of URLs to most IGV-supported data file types (
  exceptions listed below), or a session file.
* The **_merge_** parameter (optional) controls whether or not the loaded data is merged with the existing IGV session,
  or a loaded into a new session. 
    * If _true_, the data specified in the link will be added to the existing IGV session. This is the default behavior if the parameter is not specified.
    * If _false_, any data currently loaded will be unloaded after clicking the link.  
    * If _ask_, a dialog will pop up to ask the user whether or not to unload the current session before loading new tracks. (Available as of IGV 2.15.4)
* The **_name_** parameter (optional) specifies a name or names for the track. If multiple tracks are loaded as a
  comma-delimited list, the name parameter value should also be a comma-delimited list of the same size. The _**name**_
  parameter is ignored if loading a session.

!!! note " "
    The IGV application must already be running. The links will not launch IGV. 

### Examples

[http://localhost:60151/load?file=http://www.broadinstitute.org/igvdata/annotations/hg18/conservation/pi.12mer.wig.tdf&locus=egfr&genome=hg18](http://localhost:60151/load?file=http://www.broadinstitute.org/igvdata/annotations/hg18/conservation/pi.12mer.wig.tdf&locus=egfr&genome=hg18)

[http://localhost:60151/load?file=http://www.broadinstitute.org/igvdata/exampleFiles/gbm\_session.xml&merge=true](http://localhost:60151/load?file=http://www.broadinstitute.org/igvdata/exampleFiles/gbm_session.xml&merge=true)

[http://localhost:60151/goto?locus=egfr](http://localhost:60151/goto?locus=egfr)


