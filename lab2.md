# LAB REPORT 2

## Chat Server Code:
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    ArrayList<String> messages = new ArrayList<>();
    
    private String getAllMessages() {
        String output = "";
        for(String message : messages) {
            output += message + "\n";
        }
        return output;
    }
    
    public String handleRequest(URI url) {
        // just wanted to add a way for the user to view the chat log
        // without having to add a message
        if (url.getPath().equals("/")) {
            return getAllMessages();
        }
        else if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String[] messageParameter = parameters[0].split("=");
            String[] userParameter = parameters[1].split("=");
            if (messageParameter[0].equals("s") 
                    && userParameter[0].equals("user")) {
                String message = String.format("%s: %s", 
                        userParameter[1], messageParameter[1]);
                messages.add(message);
                return getAllMessages();
            }
            return "404 Not Found!";
        }
        else {
            return "404 Not Found!";
        }
    }
}

public class ChatServer {
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

