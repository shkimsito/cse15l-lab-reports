# Lab Report 2
# Part 1 - The Simplest Search Engine
<details>
    <summary>
        Source Code
    </summary>
    
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

class Handler implements URLHandler {
    // This list will hold the list of strings to be added/queried
    List<String> list = new ArrayList<>();

    public String handleRequest(URI url) {
        System.out.println(url);
        if (url.getPath().equals("/")) {
            return String.format("Enter a query!");
        } else {
            System.out.println("Path: " + url.getPath());
            // /add?s=anewstringtoadd
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    list.add(parameters[1]);
                    return String.format("String \'%s\' has been added.", parameters[1]);
                }
            } else if (url.getPath().contains("/search")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    List<String> fetched = new ArrayList<>();
                    for (String s: list){
                        if (s.contains(parameters[1])) fetched.add(s);
                    }
                    return fetched.toString();
                }
            }
            return "404 Not Found!";
        }
    }
}

class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        if(args[0].equals("22")){
            System.out.println("Did you know that port 22 is the one used by ssh? We can't use it for a web server.");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
    
</details>

## Adding apple in the search list
![Adding Apple](./7.png)
Upon request url request, the handleRequest() receives the url path and stores in "url" variable. Then, it checks for the request type after the slash which is "/add". The question mark in the path signals beginning of query and getQuery() returns the query field "s=apple". The field (which is a string) gets split() which is converted into array of substrings splitted by "=", which results ["s", "apple"]. The second if statement checks to make sure "s" is the first element of the splitted list and adds the second parameter, "apple" to the list of strings to store. Lastly, return string is printed in the screen notifying the user that the string that has been added.

Method, Values of Relevant args and fields, How they change.
 
## Searching for non-unique substring
![Searching Apple](./8.png)
Exact same process to adding, the "/search" request is caught by the same handleRequest() method and checks for the query field "s=apple" in get.Query(). The second if statement checks to make sure "s" is the first element of the splitted list. But this time, the list variable (which is a List object) is iterated by a for each loop to check if it contains the second element of the splitted list (from the query field) and checks there are any words that contain the query as a substring. The words that do are stored in fetched list, and returned eventually. Here we can see Apple, Pineapple, Applepie because they all contain apple as a substring.

## Searching for a unique substring
![Searching Pineapple](./9.png)
    
