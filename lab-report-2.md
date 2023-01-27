# Lab Report 2 - Servers and Bugs (Week 3)
January 26, 2023
## Part 1 - StringServer

StringServer.java Code:
```
import java.io.IOException;
import java.net.URI;
import java.util.*;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    // int num = 0;
    List<String> arr = new ArrayList<String>();

    public String handleRequest(URI url) {
        System.out.println("Path: " + url.getPath());
        if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                arr.add(parameters[1]);
                // return String.format("Number increased by %s! It's now %d", parameters[1], num);
                String out = "";
                for (int i = 0; i < arr.size(); i  = i + 1){
                    out = out + arr.get(i) + "\n";
                }
                return out;
            }
        }
        return "404 Not Found!";
        // }
    }
}

class StringServer {
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

Usage: 

Requests should look like:

```
  /add-message?s=<string>
```

where "string" is the message to display and the server used along with the provided Server.java file. 
  

### Example
  
So after entering the request: 
  
```
  /add-message?s=hello
```
  
 The page should show:
  
<img width="502" alt="Screen Shot 2023-01-26 at 4 20 36 PM" src="https://user-images.githubusercontent.com/43154527/214979512-eec4f272-700c-4f3b-a7a5-43d1af13df41.png">

And with this:  
  
```
  /add-message?s=this
```
<img width="505" alt="Screen Shot 2023-01-26 at 4 24 24 PM" src="https://user-images.githubusercontent.com/43154527/214979929-d90ea4f5-5b0e-474b-9d9d-bc0f9e7d1dfb.png">


And with this:  

```
  /add-message?s=is cool
```

<img width="567" alt="Screen Shot 2023-01-26 at 4 25 01 PM" src="https://user-images.githubusercontent.com/43154527/214979991-8cba0bdc-fda4-4a9c-9d13-e0cde05745e1.png">

### What is happening?
  
  The handleRequest processes each URI where a valid URI must end in ".../add-message?s=<string>",
  where <string> is the string to be inputed. Each request will enter string s into our
  storage, which is the array arr. 
  
  In the first image, the URI "/add-message?s=hello" is passed into the handleRequest, which is
  a valid request URI. The string "hello" gets parsed from the URI and added to the array for storage.
  Finally, we generate the running list of strings currently being stored in the server and it is return to be
  displayed on the side. The only thing that changes from this action is that the array gains a string,
  and the site's text gets updated with the extra item to be displayed. 
  
  In the second image, the URI "/add-message?s=this" is passed into the handleRequest, which is
  a valid request URI. The string "this" gets parsed from the URI and added to the array for storage.
  Finally, we generate the running list of strings currently being stored in the server and it is return to be
  displayed on the side. The only thing that changes from this action is that the array gains a string,
  and the site's text gets updated with the extra item to be displayed. 
  
  In the last image, the URI "/add-message?s=is cool" is passed into the handleRequest, which is
  a valid request URI. The string "is cool" gets parsed from the URI and added to the array for storage.
  Finally, we generate the list of strings currently being stored in the server and it is return to be
  displayed on the side. The only thing that changes from this action is that the array gains a string,
  and the site's text gets updated with the extra item to be displayed. 
  
  
  Every time the page is refreshed with a new URI, the page gets updated with the updated list
  of items being stored. All of the entered strings gets added into List arr. So then with every addition 
  we make, arr increases in size, and no value is deleted (until the server is closed and everything is cleared).
  

  
  
## Part 2 - Debugging
  
  
Here is a buggy program. 
  
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
  
```
                                  
Here is a JUnit test that does not catch this bug. This input is the empty array. 
                                  
                                  
```
  @Test
  public void testReversed1() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```

This is the other test that does catch bugs for this program.
  
```
  @Test
  public void testReversed2() {
    int[] input1 = { 1, 2, 3, 4 };
    assertArrayEquals(new int[]{4, 3, 2, 1}, ArrayExamples.reversed(input1));
  }
                                  
```
                                  
                                  
Here is the results of these tests. 

  <img width="756" alt="Screen Shot 2023-01-26 at 8 04 18 PM" src="https://user-images.githubusercontent.com/43154527/215007180-11bead04-2191-423f-9363-90bfffc56705.png">

As we can see, testReversed failed because the values of our result did not match the expected results. 
  
  
  
Here are the corresponding changes that I made to fix the bugs. 
  
```
  // BEFORE
    static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
      for(int i = 0; i < arr.length; i += 1) {
        arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
```
  // AFTER
    static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
      for(int i = 0; i < arr.length; i += 1) {
        newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
  ### What is happening?
The main issue with the code is that we swapped the old array with the new array in the logic of our code.
  Inside the for loop, we were reading from the empty new array and filling the old array with the reverse of 
  the empty array (which means none of the items in the new array are properly placed from the old array. In addition
  we are returning the old array when we should be returning the new array. To fix this, I swapped the two arrays in the line 
  inside the for loop and changed the return statement to return our new array. Now our function properly iterates through
  the old array and places it in reverse in our new array. 
  
  
                                  
## Part 3 - What did I learn?
  
I learned how to host a server, both locally and from the UCSD remote server. Inside a server, I learned how to parse and 
  process requests in order to either display information and/or store information that is desired. The most interesting 
  part of servers is people from other computers can open servers that I host on the UCSD server with the same link. 
                                  
                                  

