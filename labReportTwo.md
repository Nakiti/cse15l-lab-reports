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
!["image One"]("C:\Users\nakit\Downloads\Screenshot 2024-01-27 144515.png")
