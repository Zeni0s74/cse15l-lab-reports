## Lab2 Report : A local ChatServer!
***
As we get more familiar with coding in java and the tools made available to us via java's built in helper methods, we have now been able to learn to start and intereact with a local server!
We've done so in a manner that by through edditing our `URL`, we can add new messages to the server and iew them at the `root` of the server! Lets take a look at the **entirety** of our code and we'll pick out bits to analyze in a moment:
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class chatInitializer{
    static String format(ArrayList<String> arr){
        
        String outString = "";
        
        for(int i = 0; i < arr.size(); i++){
            outString += arr.get(i) + "\n";
        }

        return outString;

    }
}

class Handler implements URLHandler {
    ArrayList<String> ChatLogArr = new ArrayList<>();
    String superChat = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {

            superChat = chatInitializer.format(ChatLogArr);
            if(superChat.equals("")){return "Start a new conversatin!";}
            return superChat;
            
        } 
        else if (url.getPath().equals("/add-message")) {
            
            String[] Input = url.getQuery().split("&");
            
            
            if(Input.length == 2){
                String[] message = Input[0].split("=");
                String[] user = Input[1].split("=");
                
                boolean verUser = user.length == 2 && user[0].equals("user");
                boolean verMess = message.length == 2 && message[0].equals("s");

                
                if(verUser && verMess){
                    String usermsg = user[1] + ": " + message[1];
                    ChatLogArr.add(usermsg);
                    return "Added your message: " + usermsg;
                }                
            }
            return "eerrmm something went wrong with the message extension!";

                
        }
        else{return "404 Not Found!";}
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

That looks like a lot! However, everything in the `ChatServer` class is actually just passing instructions to teh provided `Server` class to start up the local host and let us interact with it! The real meat and potatoes is in the `Handler` class.

Now, before we pick it apart, lets look at some pictures illustrating the server in use! After compiling the server and starting a local host, we get the following initial view:
