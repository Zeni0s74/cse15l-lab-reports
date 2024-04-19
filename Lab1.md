#Lab 1 report
## basic filesystems commands
***
For the first week of our software tools and techniques class we mainly focused on getting a general understanding of the most common commands we would use in bash and teh related directories or files we would use them with!

first up, `cd` 
`cd` stands for "change directory" and just as the name implies, will change our current directory depending on the input we give it!
Starting from `/workspaces/lecture1/` we can choose to hand `cd` nothing, a directory, or a file as an argument, heres those entries and their results in the order they were named!

```
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ cd
@Zeni0s74 ➜ ~
```
Here, `cd` is entered alone, and surprisingly, it *does* work, it just sends us to the home directory when no argument is passed, rather than an error, its more like a fringe case of intended behavior!
(note that `~` is shorthand for the home directory)

```
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ cd messages
@Zeni0s74 ➜ /workspaces/lecture1/messages (main) $
```

Ok, this seems to work just as we'd expect! after passing a directory inside of `/lecture1` to `cd`, were moved to said directory and since this is the intended use, theres no error here!

```
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ cd Hello.java
bash: cd: Hello.java: Not a directory
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ 
```

Here it is, out first error! Since `cd` litterally stands for "change directory" its no surprise that we would run into an iussue if we pass it something that *isnt* a directory, like a **file**!

Thats it for the `cd` command, but lets say after we use `cd` want to check whats available to us! Thats what `ls` is for. `ls` stands for "list", and again, just as the name implies, its supposed to return a "list" of the contents of the directory we're working in! Here are some test cases under the same 3 inputs as we did with `cd`!

```
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ ls
Hello.class  Hello.java  README  messages
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ 
```

Just as we'd expect, `ls` gives us the contents of `/lecture1` when theres no input! afterall the nature of its description is to return whats around us in the current directory, so no error here!

```
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ ls messages
en-us.txt  es-mx.txt  zh-cn.txt
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ 
```

Look at that! Even if we arent *in* the messages file per-se, if we pass the command a directory within the directory we're currently in, the `ls` comand opens it up and tells us whats inside while staying in the 'outside' directory, another example of fringe intended behavior, not an error!

```
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ ls Hello.java
Hello.java
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ 
```

Strange, we *know* `Hello.java` contains some java code but instead, `ls` just returns the files name! While this isnt technically *wrong* since a file does indeed contain itself, it could be that we want to know the text within this java file!
Regardless, this isn't an error and we'll see why in the following section!
*(Note, this isn't particular to java files, after moving to `/messages` and calling `ls` on a `.txt` file, the files name is printed, not its contents)*

Now, concerning that last issue, what if we *want* to know a particular files contens? Well, luckily for us, that's what the `cat` comand is for! Standing for `concatinate`, it's meant to take in a file or two and return their contents as you would see them if you opened up those files! Lets look at some test cases:

```
@Zeni0s74 ➜ /workspaces/lecture1/messages (main) $ cat




^C
@Zeni0s74 ➜ /workspaces/lecture1/messages (main) $ 
```

Woahh, looks like something strange happened there! When we called `cat` with no input, it returns a blank line and keeps doing so with every hit of the `Enter` key until we force a `control C` return! This is actually intended behavior and **not an error** as I learned after speaking to a TA, but as for the reason why? I haven't the slightest clue!
*(Note, `cat` exhibits the same behavior if passed a string of text, say if you were to type `cat Hello` it would return the text Hello with every hit of the `Enter` key until forcing a return via `^C`, use cases for this are... limited to say the least)*

```
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ cat messages
cat: messages: Is a directory
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ 
```

Heres a true **error** in the sense that terminal tells us its an error! Since `cat` is meant to return a files contents, it makes sense that it would break wihen given something that isnt a file, say like, a directory!

```
@Zeni0s74 ➜ /workspaces/lecture1 (main) $ cat Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}@Zeni0s74 ➜ /workspaces/lecture1 (main) $ 
```

Finally, we see cat operating as it was described to! When we pass it `Hello.java`, its essentially prying the box open and telling us whats inside! after which it leaves us in the "room" that contained said "box" (It tells us whats in a file in the current directory while leaving us in said directory when we're done)

Now, I'm fairly sure thats all we had to do for our first lab report! Im still trying to get used to markdown so heres a picture of a bird just to be sure I know how to do that! :)

![Image](berd.jpg)
