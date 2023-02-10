IGV can optionally listen for http requests over a port. By default the port number is 60151, this can be changed (or the port disabled)
int the Advanced tab of the Preferences window.

**Note:**  IGV will write a response back to the port socket upon completion of each command. It is good practice to
read this response before sending the next command. Failure to do so can overflow the socket buffer and cause IGV to
freeze. See the example below for the recommended pattern.

Commands
--------

See [Batch Scripting](../tools/batch.md) for the complete list of commands.

Example
-------

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