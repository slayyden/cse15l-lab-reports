## Part 1: Creating a Web Server
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

The text we put in the query has been added to our persistent string, `string`. By entering this URL, the `handleReqeust` method is called. This takes as an argument the URL. It checks to see if the path, the part of the url after the domain, is equal to "/add-message", which it is. It then creates a new array of Strings called `parameters`, whose elements are derived from the part of the URL following the question mark. The first element in this case is the string "s" and the second element is the message we desire to add. Since the first elemment is "s", the if statement passes and we modify our persistent string by adding a new line and then the message. This new line is why there is a gap of line height between the top bar and the line of text. `string` is then returned, meaning it gets printed to the webpage.

We can add another line by modfying the url and pressing enter. This is the result:

<img width="843" alt="image" src="https://user-images.githubusercontent.com/26509702/215207291-571b73c4-b3a4-4292-99c7-1027c53c0e43.png">

Similarly to last time, `string` is modified to add our message on a new line. The `handleRequest` method is called with the argument being the URL once again. This URL is checked and parsed once again. `string` gets a new line and the message is concatenated to it. It is also returned, printing the updated `string` to the webpage.

## Part 2: Debugging
ArrayExamples.averageWithoutLowest() is a method with the following intended function:
>Averages the numbers in the array (takes the mean), but leaves out the lowest number when calculating. Returns 0 if there are no elements or just 1 element in the array. 

Below are two JUnit tests for ArrayExamples.averageWithoutLowest(). 

```java
@Test 
public void testAverageWithoutLowest() {
    double[] input1 = {};
    assertEquals(0, ArrayExamples.averageWithoutLowest(input1), .00001);

    double[] input2 = {2, 2};
    assertEquals(2, ArrayExamples.averageWithoutLowest(input2), .00001);
}
```


`input1` passes while `input2` fails:

<img width="580" alt="image" src="https://user-images.githubusercontent.com/26509702/215214192-8437277e-80cd-4e4e-b057-52dad0a2675e.png">

The average without the lowest with respect to `input2` is 2, since only one number is supposed to be removed for the average calculation. However, the method returns 0. 

Before bug fix:
```java
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
```

After bug fix:
```java
static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    double lowest_index = 0;
    for (int i = 1; i < arr.length; ++i) {
      if (arr[i] < lowest) {
        lowest = arr[i];
        lowest_index = i;
      }
    }
    double sum = 0;
    for (int i = 0; i < arr.length; ++i) {
      if (i != lowest_index) {
        sum += arr[i];
      }
    }
    return sum / (arr.length - 1);
}
```
Now, all of our tests pass:

<img width="208" alt="image" src="https://user-images.githubusercontent.com/26509702/215216283-bff7adb8-a868-40c8-8503-e70f6f8eda6e.png">


All we had to do was store the lowest index in addition to the lowest value and exclude the element with the lowest index in our average calculation. This caueses the lowest value to only be exclduded once.

## Part 3: What did I learn?
I have two main takeaways from weeks 2 and 3. The first being how to make a web server in Java. I didn't really get the appeal of web development until now, but it's pretty cool to write some code and have it able to run on almost any device through a web browser. The second takeaway is that debugging code that someone else wrote is so much harder than code that I wrote. When I debug code, I look for mistakes that I would make, not all mistakes that could be made. This meanas that I didn't check for bugs that I considered to be so trivial that I would (probably) never make them. However, this is also a strength in collaborative debugging. Everyone has different blind spots and collaborative debugging can help with that.
