# Lab Report 2 - Servers and SSH Keys
## Part 1 
**Code for my `Chat Server`**
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String allMessages = "";

    public String handleRequest(URI url) {
        if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            String s = parameters[1].split("&")[0];
            String user = parameters[2];
            allMessages = allMessages + user + ": " + s + "\n";

            return allMessages;
        } else {
            return "404 Not Found!";
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}
```
\
**Screenshot For First Usage of `/add-message`**
![image One](https://github.com/Nakiti/cse15l-lab-reports/blob/main/Screenshot%202024-01-27%20144438.png)
- In my code, the two methods called are the `main` method of the `ChatServer` class and the `handleRequest` method of the `Handler` class
- `main` method
    - Relevant Arguments: `String[] args` which is the user's input into the program
    - Relevant Fields: `int port` which is the port number that the user specifies through the previous argument
- `handleRequest`
    - Relevant Arguments: `URI url` which is the url of the visited webpage
    - Relevant Fields
          - `String allMessages` which is a string containing every message/user input from the user in the proper format
          - `String[] parameters` which contains the query made by the user
          - `String s` which contains the user's message
          - `String user` which contains the username the user has provided
