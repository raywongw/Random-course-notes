

[[COMP2396 Chapter 10 - Serialization and File IO|Last Chapter]] [[COMP2396 Chapter 12 - Life and Death of an Object |Next Chapter]]


- connect with other people
- client server model
	1. launch client on his own pc
	2. connect to server
		- client send a message to request connection
	3. one client send a message to server
	4. server broadcast the message to all participants in server (incl. original client)
	-  socket programming

- peer to peer model


### Socket Connection
`import java.net.*;`
- Client and Server application communicate through **Socket Connection**
##### Socket
- Object representing a connection between 2 applications
- `Socket socket = new Socket(String "IP Address",int TCP port number );`

- **TCP Port** 
	- a 16 bit unsigned number
	- 0 to 1023 are reserved for specific services
		- HTTP: 80
		- Telnet: 23
		- FTP: 20
		- SMTP: 25
		- POP3 mail server: 110
	- utilize 1024 to 65535
	- 1 program can only use 1 port number


##### Reading data from Server
- Make a socket connection to server
- Make a `InputStreamReader`
- Make a Buffered Reader
- Read data

```Java
Socket s = new Socket("127.0.0.1", 5000);
InputStreamReader isr = new InputStreamReader(sock.getInputStream());
BufferedReader reader - new BufferedReader(isr);
String line = reader.readline();
```


##### Writing data to server
- Make a socket connection
- Make a `PrintWriter`
- Write data

```Java
Socket s = new Socket("127.0.0.1", 5000);
PrintWriter w = new PrintWriter(s.getOutputStream());

writer.println("message to be sent");
```



Example code for Daily Advice Client
```Java
import java.io.*;
import java.net.*;
public class DailyAdviceClient {
	Socket sock;
	public void go() {
		try{
			sock = new Socket(Socket(" 127.0.0.1", 5000);
			InputStreamReader streamReader = new InputStreamReader(sock.getInputStream());
			BufferedReader reader = new BufferedReader(streamReader);
			String advice = reader .readLine ();
			System. out .println (("Today's advice: " + advice );
			reader .close
		} catch (Exception ex) {ex .printStackTrace();}
	// code for main()...
}
```



#### Writing a Simple Server Program
- Create a ServerSocket on a specific port
- Wait for new client connection
- Upon a client make connection

Example code for daily Advice Server
```Java
import java.io.*;
import java.net.*;

public class DailyAdviceServer {
	ServerSocket serverSock;
    String[] adviceList = {"Practice makes perfect", "Never give up", "Focus on the task at hand", "Don't look back", "Be yourself", "Believe in your own"};

    public String getAdvice() {
        int random = (int) (Math.random() * adviceList.length);
        return adviceList[random];
    }

    public static void main(String[] args) {
        DailyAdviceServer server = new DailyAdviceServer();
        server.go();
    }

	public void go() {
	    try {
		    // server listens for client requests on port 5000
	        serverSock = new ServerSocket(5000);
	        while (true) {
	            Socket sock = serverSock.accept();
	            PrintWriter writer = new PrintWriter(sock.getOutputStream());
	            String advice = getAdvice();
	            writer.println(advice);
	            writer.close();
	            System.out.println(advice);
	        }
	    } catch (Exception ex) {
	        ex.printStackTrace();
	    }
	}
}
```



### Multi-Threading
- way for server to handle different client's action and message
	- e.g. send and receive message at once
- **Thread**
	- a line of eecution


##### Runnable
- Interface
- a desired job to be taken up by Thread

##### Thread
- Takes a `runnable` job to do work
- use `thread.start();` to start the thread

Following program may have different output
```java
public class MyRunnable implements Runnable {
    public void run() {
        go();
    }

    public void go() {
        doMore();
    }

    public void doMore() {
        System.out.println("top of the stack");
    }

    public static void main(String[] args) {
        Runnable threadJob = new MyRunnable();
        Thread myThread = new Thread(threadJob);
        myThread.start();
        System.out.println("back in main");
    }
}
```


##### Race condition
- JVM scedule priority of tasks at random
- below code may have 2 possible output
	- first possible output
		1. Thread start
		2. JVM let the job in thread continue
		3. `println("top of the stack");`
		4. back to main
		5. `println("back in main");`
	- second possible output
		1. Thread start
		2. JVM stop the thread to facilitate jobs in main
		3. `println("back in main");`
		4. back to jobs in thread
		5. `println("top of the stack");`


##### Putting thread to sleep
- `Thread.sleep(int second);`
- The second is not exact
- Only force it to leave running state
	- let other threads to run


##### Concurrency problem in Multi-threading
- 2 thread access a same object on heap
- accessing on same time cause [[#Race condition]] and hence data corruption
- Solution: Make sure only one thread can access it at a time by `synchronized`
```Java
private synchronized void makeWithdrawal( int amount )
	// ...
}
```


##### Deadlock Problem
- each java object has a lock and key pair for all synchronized method in it
- a thread can hold 1 key
- all worker threads holding a key of other thread
- solvable by good programming skills




