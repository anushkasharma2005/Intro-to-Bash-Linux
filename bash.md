# BASH SCRIPTING 

`SPACES MATTER HERE (IN TERMINAL)`

## Basics 
1. input  : echo hello
   output:hello                                                                // echo basically prints the same thing again…

2. input  :   cat file_name.txt <br>
   output:  // whatever is written in the file is printed in the terminal..
   
   ```
   cat basically stands for concatenation..The cat command basically takes two filenames concatenate then and display on terminal both the files.But if we give only one file name then it just displays the text in that file since it does not have anything to concat it with!
   ```
   `Remember!!` - It doesn't concatenate or merge the files and store them somewhere

3. input  :   bash file_name.sh  <br>
   output:  // whatever commands are given in the file are executed in the terminal..<br>

   ```
   .sh files contains multiple commands like echo, cat, etc whic can be executed in one go!!
   (sh== shell)
   ```

4. Input  :   echo $SHELL <br>
   output:  (it should be) bin/bash    <br>

      `We should put this in .sh file in .sh file.. This basically means which interprete you are using --- so first line of .sh file should be: #!/bin/bash `<br>
         
      ```
      to give permission to execute any sh file command is:

      chmod u+x file_name.sh

      here the u+x is just a good practice to write and is not compulsory... It basically means only the owner has the permisssion to do this and nobody else who is working on the system can access it.

      ```

5. input  :   ./file_name.sh  <br>
   output:  //executes the file.<br>
<br>
To remove a file we use rm command.  command: rm file_name<br>
'wc -w' command is use to get word count of any perticular file. It by default displys the filename again with the word count<br>

## Variables 
To take input from user we use `read` command <br>
we define variables as: x= Hello, first_name = Anushka, etc;

`syntax: variable_name = value`

if we want to use then later we use $ sign ---- $x , $first_name, etc.


## Position Arguement 
This basically refers to commandline arguements.<br>
The count of the arguements starts from 0... The 0th position is reserved for command (like echo), therefore the auguements we give as input starts from 1...
to refer to these arg in bash script we write $1 to refer to 1st arg ,$2 to refer to 2nd commandline arg etc

```
example: see bash script positional_arg.sh

command given in terminal: ./positional_arg.sh Anushka Sharma
output                   :  Hello Anushka Sharma! 
```



## Piping
The symbol of pipe is | <br>
This is used when we want to filter out something from a large amount of files.
`we sent the output of command written before the pipe symbol to the command after pipe symbol.`



## Output redirection
As the name suggest we redirect the output to some other place...
To implement this we use > symbol.
```
example: echo Hello World > hello.txt .
```
let's break this down, <br>
the output of command before > is Hello World which should have been printed in terminal but instead of printing it there we are redirecting to hello.txt file therefore this Hello World is printed in hello.txt .
Now to check it we can give command cat hello.txt, the output in terminal will be "Hello World!".

`DO REMEMBER! that if there is already some text in hello.txt then it is overwritten.`

if we want to append and not overwrite the already existing text then we use <span style="color:yellow;"> >></span> (double greater than symbol).

to take input from some already existing file we use << or <<< (double or triple less than symbol)
<br><br>

as mentioned above(Basics) wc -w command prints the filename by default, now if I don't want this to be printed then I'll use <.<br>
example: if I write "wc -w < hello.txt" then the output will be just the word count.
<br>
this less than command is basically used to get input from a file. Like here instead of giving the file name as positional argument we give input from this file(The text written in it) as the arguement and hence only the number is printed.
 
 #### *Other way of feeding data to command:*

   1. USING << OPERATOR!<br>
   It's used to give multiple lines of commands... The << is immediately followed by a word which will mark the begining and ending of the input text.Generally we write 'EOF'..

      Example: cat << EOF<br>
            I will<br>
            write some<br>
            text here <br>
            EOF&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (# the text will end here)<br>

      and the input lines will be printed again because we are using cat (written in between EOF)<br>

   2. USING <<< OPERATOR!<br>
      It's used to supply single strings of text to the commandline
      Example: wc -w command reads a file or command output but not actual string given as commanline arguement...To give this string input we use <<<..

      command: wc -w <<< "Hello there! this is for wordcount"&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
      #The output is the wordcount(here 6)  <br>


## Test Operator

   1. Input: [ hello = hello ]     (hit enter)<br>
             echo $?<br>
      Output: 0   <br>           

      `$? prints the exitcode(return value) of the last command. Exitcode 0 means that the command was executed successfully. `
   2. Input: [ 1 = 0 ]     (hit enter)<br>
             echo $?<br>
      Output: 1   <br>     
   3. Input: [ 1 -eq 1 ]     (hit enter)<br>
             echo $?<br>
      Output: 0   <br>  

   4. Input: [ hello = hello ]     (hit enter)<br>
             echo $?<br>
      Output: 0   <br>        
```
-n is specific to shell scripting and is used to check if a string is not empty, while != is a more general inequality operator used in many programming languages for comparing values, including strings.
```

## Conditional Statement

To understand how to use conditional statements read the .sh file named conditional_statement.sh. It is explained below:

This script will take a positional arguement and 
if the 1st positional arguement is Anushka, "Oh, you are the boss here. Welcome!" will be printed 
if the positional arguement is help then "Just enter your username, duh!" will be printed 
if something other than this is typed then "I dont know who you are. But you are not my boss!" will be printed 

```
REMEMBER! 
[] bacically is our test operator it is used when we want to check something :)
{,,} is called a parameter expansion and it allows to ignore the uppercase and lowecase when comparing two values 
we end the test statement with a semicolon.   
fi is the closing statement of a conditional script
```


## Case Statement 

this seem to be like switch statement in c programming.<br>

To get a better idea read the login.sh file first 
```
"|" works as seperator and not as pipe here
* is catchall it is acting like default statement 
```

After the echo command we end a case by using ";;"<BR>
and we end the options(each) by ")".<br>

The advantage of case statement is that we can give multiple options like see the 1st atatement there the two options are anushka or administrator..
For doing this with conditional statements we'll have to use multiple elif statements.<br>

to end the case statement we use 'esac'.

## Arrays

to make an array, the simplest way is:<br>
variable_name=(first second third fourth fifth)<br>

The elements of the array are defined in between"()".<br>
Space is used as the seperator between two elements of the array.<br>

if we write echo $variable_name just the first element will be printed.<br>
If I want to print the whole list(array) then the command would be:<br>
echo ${variable_name[@]}<br>
or If I want to access some particular element of the array we do it exactly like we do it in c. 'echo ${variable_name[index]}'.Index starts from 0.<br>


## For Loop

to demonstrate this we'll write this beautiful command in terminal:<br>
for item in {variable_name[@]}; do echo -n $ item | wc -c; done (hit enter)<br>

the output is the wc of all the elements <br>

Here we first define the variable item that is, each element of the array during the loop. Then we write do followed by the actual action that we want to perform. $item represents the element we are at in the current iteration.Then we use pipe and wc -c; done!. <br>
`-n here is just a flag for echo command which says to ignore all the new line charaters, If you don't use the -n option with the echo command, it will append a newline character (\n) after printing the item. The -n option is used to suppress the trailing newline.`
```
look at the -c in after the wc command , wc -c: This counts the number of bytes in its input.
If I just use wc without any options or arguments, it will display three counts by default: lines, words, and bytes. 
to count number of lines we use "wc -l"
and to count number of words we use "wc -w"
```

## Functions

For better understanding read first_func.sh first.<br>
Yah you can also write some easy script :)<br>
We defined two variables(up and since) in a func called showuptime...
The up variable catches the no. of hour for which the machine has been on.<br>
The since variable stores the time at which the machine(computer) was turned on.<br>

```
DO REMEMBER! The variable inside the func is not local function this can cause problems in large scripts so to define local functions (so that the value assigned in that function is not carried outside the function) just add a word local before the variable name in the function. 
```
Functions can also take positional arguement(commandline arg).<br>
for better understanding read funcposarg.sh<br>
```
uptime command with the -p option, which displays the system uptime in a human-readable format. (Try writing uptime with and without -p on terminal) it's something like this "up 4 hours, 51 minutes" (with -p)

The cut command is used to extract sections from each line of input (or from files) and write the result to standard output.
we can use these with cut command:
-c, --characters=LIST: Select only these characters.
-f, --fields=LIST: Select only these fields.
-d, --delimiter=DELIM: Use DELIM instead of TAB as the field delimiter.

uptime -p provides information about the system's uptime.
cut -c4- takes the output of uptime -p and extracts characters starting from the fourth character onwards.
So, in this specific case, the cut -c4- command is used to remove the first three characters ("up ") from the output of uptime -p, leaving only the duration of uptime.

The uptime -s command provides the system's start time. The output is in the format YYYY-MM-DD HH:MM:SS.
```
## Exitcode
this basically means return value of any function. Read exitcodedemo.sh

## Awk
It is one of the most useful tool in bash.<br>
It basically filters part of a file or part of command output in such a way that the most essential parts are filtered .

example: we create a txt file names test.txt.
them I want to print the 1st word written in it we type the command:<br>
awk '{print $1}' test.txt.

whatever is the 1st word of the file is printed in terminal<br>
`space character is a seperator`<br>

```
if we want to change the seperator (say to ,) then we can sepcify this in our command:
awk -F, '{print $1}'
```
We can also pipe command into awk<br>
example: <br>
echo "Just get this word: Hello" | awk '{print $5}'<br>
output: Hello<br><br>

OR<br><br>

echo "Just get this word: Hello" | awk -F: '{print $2}' | cut -c2- <br>

// this cut is to remove the 1st charater which is space

## Sed

It is used to modify values in textfile using regular expressions.

ex: let us suppose we made a text file named seddemo.txt
it contains:<br>

The fly flies like no one flies.<br>
A fly is an insect that has wings and a fly likes to eat leftovers.<br><br>

We want to replace word fly with grasshopper.<br>

COMMAND: sed 's/fly/grasshopper/g' seddemo.txt (hit enter)<br>

`Here s is for substitute, so we are defining the mode first.And g stands for globally this means we want to do this for entire text file.`<br>

now I also want to backup the previous text we can do it by writing this:<br>
sed -i.ORIGINAL 's/fly/grasshopper/g' seddemo.txt (hit enter)

now to access the original file(backup) we can type: vim seddemo.txt.ORIGINAL--- this will have fly (unchanged) <br>

whereas seddemo.txt will have (substituted) grasshopper.

## Miscellaneous

1. If you want a delay of a few seconds between two command then we us "`sleep` time"--- example: sleep 1 (will create of delay of 1 sec).<br> 
2. `$#` is a special variable that represents the number of positional parameters (i.e., the number of arguments).<br>
3. `-d` is a test operator used within square brackets ([ ]). It checks whether the given argument is a directory.<br>
4. `-l` is another test operator used within square brackets ([ ]). It checks whether the given argument is a symbolic 
   link (symlink).<br>
5. the `-f` test operator is used within square brackets ([ ]) to check if a given path refers to a regular file.<br> 
6. `$@` represents all the command-line arguments as separate words.

7. `"$@"` when double-quoted, preserves each argument as a separate word. This is particularly useful when dealing with arguments that may 
   contain spaces.    
8. `[[ ... ]]` is is a conditional construct in Bash that allows for more complex conditional expressions than the single brackets [ ... ].   
9. `-p` option with the read command is used to display a prompt message before reading input from the user. It stands for "prompt."
10. `mv` is used to move files from one dir to other.
11. If we want to print only the name of the file_name from the complete path we use `basename`. syntax: $(basename "$path_variable").
12. `-e` flag in the script is used to check if a file exists.
13. `-ne` in the script is a conditional expression used to check if the number of command-line arguments provided is not equal to something.
14. `-z` flag is used within square brackets [ ] to check if a string/variable is empty.
15. The `wc -l` command is used to count the number of lines in a file.
16. `exit 1` command is written to ends the program there and then.
17. The `=~` operator in Bash is used for pattern matching with regular expressions. When used in a conditional expression (within double square brackets [[ ... ]]), it allows you to
    check if a string on the left side matches the pattern on the right side.
18. `^` is a metacharacter that asserts the start of a line or the start of a string.
19. When used within a character class `([ ]), ^` negates the character class. For example, [^0-9] matches any character that is not a digit.    
20. `[0-9]+` matches one or more digits (0 to 9).
21. `$` can also assert the end of the line. Example: [[ "$input" =~ ^ [0-9] + $ ]]
22. `-gt` is a comparison operator that stands for "greater than."
23. `find "$directory"` This command starts the find utility, which searches for files and directories in the specified path 
24. `-exec` allows you to execute a command for each file found.
25. `du` command is used to estimate file space usage. 
26. When the `-r` option is used, the `read command` treats backslashes as literal characters, and they are not used to escape the following character. 

## IN TERMIAL
1. `-a` shows hidden files and directories. By default, files and directories whose names start with a dot (.) are considered hidden in 
   Unix-like systems. 
2. `-l` Provides a long listing format, displaying detailed information about files and directories
3. With ls command `-r` stands for reverse ,it reverses the order in which files and directories are listed.
4. With rm command `-r `stands for recursive ,-r: Recursive flag, indicating that the operation should be applied recursively to directories
   and their contents.
5. `-i` flag with rm to prompt for confirmation before deleting each file or directory command:`rm -ri directory_name`
6. With ls and rm, the -h flag is often used to display information in a "human-readable" format. 


```
Always consult the manual or help documentation for specific commands (man command or command --help) to understand the specific usage of flags like -h for each command.
```

## Fun Facts

- Tar stands for tape archive it uses Tar utility. The Tar utility is used for archiving files and directories on Unix and Linux systems.
  A ".tar" file is not compressed; it is simply an archive that bundles together multiple files and directories into a single file. The ".tar" extension is often used as part of a naming convention for such archive files.

- bashrc 
- profile: login
- exrc 

```
This combination (IFS= read -r) is commonly used when reading lines from files to avoid unexpected behavior related to whitespace and backslashes.
```