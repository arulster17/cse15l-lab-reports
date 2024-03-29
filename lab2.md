# LAB REPORT 2

## PART 1
**ChatServer.java Code:**
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
**Message 1**
![Message 1](/message1img)
*Which methods in your code are called?*
- The ```handleRequest``` method is called first, then it goes into the ```contains("/add-message")``` path.
- This path extracts the message from the URL and calls private helper ```getAllMessages()``` to print all messages

*What are the relevant arguments to those methods, and the values of any relevant fields of the class?*
- The ```handleRequest``` takes in the URL (```http://localhost:4000/add-message?s=knock%20knock&user=srujamdave0109```) as an argument.
- ```ArrayList<String> messages``` stores the current messages. Before the code is executed, the ArrayList is empty. (```messages = {}```)
- The ```getAllMessages()``` helper takes no arguments and only uses ```messages```.

*How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.*
- ```messages``` updates to contain all of the sent messages by adding ```"srujamdave0109: knock knock"```. Now, we have ```messages = {"srujamdave0109: knock knock"}``` 

**Message 2**
![Message 2](/message2img)
*Which methods in your code are called?*
- The ```handleRequest``` method is called first, then it goes into the ```contains("/add-message")``` path.
- This path extracts the message from the URL and calls private helper ```getAllMessages()``` to print all messages

*What are the relevant arguments to those methods, and the values of any relevant fields of the class?*
- The ```handleRequest``` takes in the URL (```http://localhost:4000/add-message?s=who%27s%20there?&user=arulster17```) as an argument.
- ```ArrayList<String> messages``` stores the current messages. Before the code is executed, ```messages``` contains one message: ```messages = {"srujamdave0109: knock knock"}```
- ```The getAllMessages()``` helper takes no arguments and only uses ```messages```.

*How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.*
- The ```messages``` ArrayList updates to contain all of the sent messages by adding "arulster17: who's there?". Now, we have ```messages = {"srujamdave0109: knock knock", "arulster17: who's there?"}``` 

## PART 2

**Private Key**

![Private Key](/lab2privateKey.png)

**Public Key**

![Private Key](/lab2publicKey2.png)

**Logging into ieng6 without password**

![SSH login w/o Password](/lab2noPasswordLogin.png)

## PART 3

I learned a lot more about servers and URLs in the past two weeks. Previously, I knew nothing about how we could connect websites to Java programs, and I really enjoyed learning and making things like number and chat servers. I also learned more about ssh than I knew before, such as the scp command and saving the password in the authorized file. One thing related to this that I hope to do is to provide input through a website in a method besides the URL. I would like to make an actual little chat website in pure Java, where people can send messages just through text box inputs and send buttons. I hope we learn about this in the coming weeks. 
