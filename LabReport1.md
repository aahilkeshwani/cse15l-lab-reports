Lab Report 1! - Remote Access and FileSystem

In this lab, we learned about commands `cd`, `ls` and `cat`. We learned how to use these commands and what they do. 


`cd` - Change Directory - Switches the current working directory to a given path.
    First here is an example using `cd` with a path to a directory as an argument: 
    

    [user@sahara ~]$ cd lecture1/messages
    [user@sahara ~/lecture1/messages]$


In this example, the working directory at the time of the command was `/home`. After I called the command the output showed the new working     directory changed from calling `cd`. 
    In this case, the output is not an error
    
Next, here is an example using `cd` with no arguments:

    [user@sahara ~/lecture1/messages]$ cd
    [user@sahara ~]$
    
In this example, the working directory at the time of the command was `/home/lecture1/messages/`. After I called the command without an argument, the working directory was changed to `/home/`. 

In this case, the output shows the change of the directory. Additionally, there is no error. 
    Finally here is an example using `cd` with a path to a file as an argument:

    [user@sahara ~] cd lecture1/messages/en-us.txt
    bash: cd: lecture1/messages/en-us.txt: Not a directory

    
Here the working directory when the command is run was `/home/`. We get an error message as an output that shows the path of the file, but also tells us the path does not lead to a directory.
    Hence, in this case, the reason for our error message is that `cd` can't change directories to a file. 

`ls` - List Command - Lists the files and folders in a given path.
    First here is an example using `ls` with a path to a directory as an argument:

    [user@sahara ~]$ ls lecture1/messages/ 
    en-us.txt  es-mx.txt  ur.txt  zh-cn.txt
    
In this case, the working directory is `/home/`, but in the case of having a path as an argument it wouldn't matter. 
    Next, the output here simply lists the files in the messages directory. This output is not an error.

Next, here is an example using `ls` with no argument:

    [user@sahara ~/lecture1]$ ls
    Hello.class  Hello.java  messages  README
    
Here, the working directory is `/home/lecture1/`. This means when the command `ls` is called with no arguments the command lists all files and directories under the lecture1 directory.
    The output lists all the directories and files under `lecture1` in alphabetical order. The output is not an error. 

The following example shows `ls` with a path to a file as an argument:

```
[user@sahara ~]$ ls lecture1/README
lecture1/README
```
In this example, we use the path to the file `README` as an argument. In return, the output we get is just the path to the file. This is because the command doesn't have anything to list. The output is not an error. In this case, the working directory was `/home/`. 

`cat` - Concatenate - Prints the contents of a file given by a path

First here is an example using `cat` with a path to a file as an argument:
```
[user@sahara ~]$ cat lecture1/messages/es-mx.txt
¡Hola Mundo!
```
In this example, the working directory is `/home/`. We then enter the path to `lecture1/messages/es-mx.txt` as the argument. Thus the command `cat` prints out the contents of the file `es-mx.txt`. The output is not an error.
We can use the command `cat` to print the contents of multiple files by being in a working directory containing files to print. 
For example:
```
[user@sahara ~/lecture1/messages]$ cat es-mx.txt en-us.txt
¡Hola Mundo!
Hello World!
```
In this example, the working directory is `/home/lecture1/messages`, and thus we can call multiple files in `/messages/` to `cat`. Again the output here is not an error. 
Next, we can try calling `cat` with a path to a directory as the argument:
```
[user@sahara ~]$ cat lecture1/messages
cat: lecture1/messages: Is a directory
```
Here, we are in the `/home/` working directory, and the path to the directory `/messages/` is entered as the argument. The output tells us that the path `lecture1/messages` is a directory and thus does not perform the `cat` command. The output is therefore an error message. 

Finally, let's try using `cat` with no argument:
```
[user@sahara ~/lecture1]$ cat
cd
cd
cd lecture1/messages
cd lecture1/messages
cat lecture1/messages/en-us.txt
cat lecture1/messages/en-us.txt
```
Using `cat` with no argument does not work. In the example above the working directory is `home/lecture1/` but I have tried it in other directories and have gotten this same result. After `cat` is called without an argument there is no output. The page also stops responding to inputs and just spits out whatever you enter, as you can see above. This is definitely an error, but I cannot figure out what exactly is happening.


    
