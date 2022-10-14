# The Simplest Search Engine
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
