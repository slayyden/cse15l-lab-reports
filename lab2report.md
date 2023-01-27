### Part 1: Creating a Web Server
I created a simple web server which remembers the strings that you enter into the url. The code is below:

```java
import java.io.IOException;
import java.net.URI;

/**
 * Decides what to put on the webpage depending on the url.
 */
class StringHandler implements URLHandler {
    // stores a persistent string containing all the added messages
    String string = "";

    /**
     * Adds to the persistent string depending on the URL and prints that
     * string to the webpage.
     * 
     * @param url the url of the webpage.
     * 
     * @return The string to be printed on the webpage.
     */
    public String handleRequest(URI url) {
        
        // handles adding a message
        if (url.getPath().equals("/add-message")) {

            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                    // create a new line and put the query on that line
                    string += "\n" + parameters[1];
            }
        }

        return string;
    }
}

/**
 * Starts up and runs a server that will handle URLs based on our StringHandler
 * class. This class exists purely as a container for its main method.
 */
class StringServer {
    /**
     * Starts up and runs a server that will handle URLs based on our StringHandler
     * class. 
     * 
     * @param args an integer between 1024 and 49151 determining the port number.
     */
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new StringHandler());
    }
}
```

Here are some screenshots of its functionality. Starting with a fresh run of the server and adding the path and query "/add-message?s=Java is a boilerplace driven object oriented language" we see the following:
<img width="867" alt="image" src="https://user-images.githubusercontent.com/26509702/215205519-75edaa2b-c58b-4167-a8e7-64f7baeb2cb8.png">
The text we put in the query has been added to our persistent string, `string`. By entering this URL, the `handleReqeust` method is called. This takes as an argument the URL. It checks to see if the path, the part of the url after the domain, is equal to "/add-message", which it is. It then creates a new array of Strings called `parameters`, whose elements are derived from the part of the URL following the question mark. The first element in this case is the string "s" and the second element is the message we desire to add. Since the first elemment is "s", the if statement passes and we modify our persistent string by adding a new line and then the message. `string` is then returned, meaning it gets printed to the webpage.
