### Part 1: Creating a Web Server
I created a simple web server which remembers the strings that you enter into the url. The code is below:

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
