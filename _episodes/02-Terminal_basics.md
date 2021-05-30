---
title: "Introduction to Linux Terminal"
author: "Dr. Eyal Soreq" 
date: "05/03/2021"
teaching: 25
exercises: 5
questions:
- What is a terminal and why would I use one?
- What is the prompt and what does it indicate? 
objectives:
- Explain how the shell relates to the input and output of your computer.
- Explain the advantages of command-line interfaces over graphical interfaces.
- Explain the read, run, and print steps of the shell.
keypoints:
- "The file system is the structure of our Information."
- "Structure is formed by a directory tree."
- "Directories can store other directories and files."
- "There multiple commands that enable navigation of the filesystem"
- "A relative path specifies a location starting from the current location."
- "An absolute path specifies a location from the root of the file system."
- "`..` means 'the directory above the current one'; `.` on its own means 'the current directory'."
---

# Introduction to Linux Based Command Line Interactions


### graphical user interface (GUI)
In its most basic form, all computers have some interaction to store, process, create data, take actions, and communicate with other computers and people. There are many ways to interact with the computer. However, the most common is the GUI, which uses a mix of windows, icons, mice, and pointers to perform various tasks. This user interface type makes it easier for users to navigate through and use hundreds of programs, often from within a complex hierarchy.

### Command-line interface (CLI)
Under the hood, all computers have a command-line interface, or CLI, which distinguishes it from the more common GUI, which most people use nowadays. A CLI's heart is a read-evaluate-print loop or REPL: when a user types a command and presses enter, the computer reads the command, runs the command, and prints out the output until the user breaks the cycle. One of the programs in charge of enabling this cycle is called a shell or terminal.

### The Shell/Terminal
The shell is a program that serves as a keyboard-driven interface between the user and the operating system. It includes a command-line interpreter that accepts the user input via the keyboard, evaluates it, starts programs if necessary, and returns the output in the form of text output to the user. Each shell has its programming language, which makes it possible to write scripts that automate complex tasks. Each shell runs in a terminal.

### Why would I use a Terminal 
In the old days, independent devices, or so-called "hard copy terminals" (printer or screen plus keyboard), were used. Modern computers no longer have those, replaced by terminal emulators - programs that provide users with a graphical window for interacting with the shell. As scientists, we rely on powerful computer clusters to reveal answers to many questions and to perform many tasks automatically. There are many ways to interact with these computers. However, the fastest and most reliable way is the terminal emulators, which is the main focus of today's presentation.

### What is Bash
One of the differences between a shell and any other program is that a shell runs other programs instead of doing calculations. One of the most popular Unix shells is Bash, named for the Bourne Again Shell (derived from a shell originally written by Stephen Bourne). In most modern Unix implementations and most packages designed for Windows, Bash is the default shell.

> ## Opening a terminal using jupyter cloud
> Go to [jupyter-cloud](https://jupyter-cloud.gwdg.de/), login and press on the Terminal button in the Laucher
{: .challenge}

## Command prompt
Opening the terminal for the very first time, you will be presented with a prompt `$`, indicating that the shell is waiting for your input.

~~~
$
~~~
{: .language-bash}

## Shell Commands structure
You interact with the shell via commands, which can be used to execute CLI programs with names similar to the commands. For each action that you wish to perform using the terminal, you use a program call following this basic scheme:
~~~
Command [options] [arguments] 
~~~
{: .language-bash}

> ## Use `ls` to list your home contents 
> The first command we will use is `ls`, which displays the current directory contents. <br>
> Type `ls` and press the <kbd>Enter</kbd> key to execute it.
{: .challenge}

## Managing Content in the Filesystem
The part of the operating system responsible for managing individual files and directories is called the **file system**. This part of the system categorizes our data into files or directories that contain files. 

> ## Creating a sandbox directory using mkdir
> Make a new directory by typing `mkdir sandbox` in the prompt. <br>
> Here, mkdir is the program name and sandbox is the argument, in this case the name of the directory we are creating.
{: .challenge}

## mkdir assumes no such directory exists 
Type `mkdir sandbox` again. Now the program returns an error.
~~~
$ mkdir sandbox
mkdir: cannot create directory ‘sandbox’: File exists
~~~
{: .error}


> ## mkdir options allow us to issue more advanced commands
> By adding the --help option, prints out the different options you can use to extend the mkdir program.
> Please type the following command in the prompt. <br>
> ~~~
> $ mkdir --help
> ~~~
> {: .language-bash}
{: .challenge}

> ## mkdir --parent gives us the ability to form filesystem structures
> Please type the following command in the prompt. <br>
> By adding the -p (aka parent) option, the mkdir program will create a hierarchical folder structure.
> ~~~
> $ mkdir -p sandbox/root/{dir_a,dir_b/{leaf_1,leaf_2},dir_c}
> ~~~
> {: .language-bash}
{: .challenge}


## list folder structure
In order to confirm, we could use wildcards like `ls sandbox/*/*/*` where each astrix corresponds to a different level in the hierarchy folder we created. However, there is a good chance that one of the many options of the `ls` command might be able to solve this problem in a generic way.<br>

> ## list folder structure
> Try to use the `ls --help` to figure out what option is the most sutiable. 
> > ## Solution 
> > ~~~
> > $ ls sandbox/ -R
> > ~~~
> > {: .language-bash}
> > Here we state the root folder to start listing from, and then use the recursive  option to list all subdirectories recursively to the prompt
> > > ## Output
> > >~~~
> > >sandbox/:
> > >root
> > >sandbox/root:
> > >dir_a  dir_b  dir_c
> > >sandbox/root/dir_a:
> > >sandbox/root/dir_b:
> > >leaf_1  leaf_2
> > >sandbox/root/dir_b/leaf_1:
> > >sandbox/root/dir_b/leaf_2:
> > >sandbox/root/dir_c:
> > >~~~
> > >{: .language-bash}
> > 
> {: .solution}
{: .challenge}

## Removing a directory 
If we add a folder, we should also have the ability to remove it, else we risk having a very messy file system.

> ## The `rm` command 
> If we try to use the `rm` command to remove the `sandbox/` folder we get the following error: <br>
> ~~~
> $ rm sandbox/
> rm: cannot remove 'sandbox/': Directory not empty
> ~~~
> {: .error}
> The -d option may also be selected correctly by reading the help, but this results in the following error: <br>
> ~~~
> $ rm -d sandbox/
> rm: cannot remove 'sandbox/': Directory not empty
> ~~~
> {: .error}
> > ## Solution 
> > The solution is to remove all the structure recursively (using the -r option), starting with the empty directories and moving upward in the hierarchy. We add the -f (force) option to handle directories that are not empty.
> > ~~~
> > $ rm -rf sandbox/
> > ~~~
> {: .solution}
{: .challenge}

## Why would we want to use the terminal 
Clearly, there is an elephant in the room... Why would I want to waste your time by teaching you this old interface.
> ## Solution 
> The solution lies in automation and standardization.
> If I know that the filesystem will look the same for every project I create, I can set up automatic processes that will take that into account. Look at the following line for example. 
> ~~~
> mkdir -p sandbox/My_first_project/{Data/{pkl,csv,zip},Notebooks,Code,Tmp,Report/{Tables,Figures,Text,Background/{pdf,pptx},Presentation}}
> ~~~
> {: .language-bash}
{: .solution}

## Navigating the filesystem
To move to and view directories, files, and content, we need some basic navigation skills. 

## Change Directory  `CD`
Navigation is the most fundamental skill in any computer program. The Change Directory command provides us with capability to switch from one place to another. For example, we can go to the Data folder we just created by using the following command:
~~~
cd sandbox/My_first_project/Data
~~~
{: .language-bash}

## Hash tag - add comments to your code 
- `#` the hash sign is used as the beginning of the comment in the script. In each line of the statement, the part starting with `#` is not executed.

> ### Examples using `cd` and `#`
> ~~~
> cd / # change directory to the root directory
> cd ~ # change directory to your home directory
> cd ~/sandbox/My_first_project/Report # goto Report dir
> cd "dir name"
> # if for some reason you created a folder name with spaces
> # (DONT!!!) this is how you call it
> ~~~
{: .output}

## Knowing where you are 
Another important thing is knowing where you are. The print working directory `pwd` will show you where you are currently located. Try it... 

~~~
$ pwd
~~~
{: .language-bash}

~~~
/home/jovyan/sandbox/My_first_project/Data
~~~
{: .output}


## listing all folders contents 
Recall that `ls` contains many options, among the most useful ones are `-a`  which stands for all and means that the command does not ignore entries starting with `.`. Another useful option is `-l` which tells the command to use a long listing format. 

~~~
$ ls -al
~~~
{: .language-bash}

~~~
drwxr-xr-x 5 jovyan users 4096 May 13 14:31 .
drwxr-xr-x 8 jovyan users 4096 May 13 14:31 ..
drwxr-xr-x 2 jovyan users 4096 May 13 14:31 csv
drwxr-xr-x 2 jovyan users 4096 May 13 14:31 pkl
drwxr-xr-x 2 jovyan users 4096 May 13 14:31 zip
~~~
{: .output}

## Let's unpack one line of the output from right to left 

- Let's unpack the bottom line from right to left

|  |  |
| :-- | :-- |
| `..` | file/folder name |
| `May 13 14:31` | The **last** modification time |
| `4096` | File size in bytes |
| `users` | Group name |
| `jovyan` | Owner name |
| `8` | Number of links |
| `drwxr-xr-x` | Permissions |
| | |
		
----

## Basics of permissions

- Permission settings are grouped in a string of characters (-, r, w, x)
- The characters r, w, and x stand for **read**, **write**, and **execute**.
classified into four sections:
- <span style="color:GOLD">-</span>rwxrwxrwx - File type has three possibilities:
- regular file (–)
- a directory (d)
- or a link (i)
- -<span style="color:GOLD">rwx</span>rwxrwx - File permission of the user (owner)
- -rwx<span style="color:GOLD">rwx</span>rwx - File permission of the owner’s group
- -rwxrwx<span style="color:GOLD">rwx</span> - File permission of other users

		
----

## Changing permissions

- Any Linux user, will at some point need to modify the permission settings of a file/directory.
- This can be done using the `chmod` command.
- The basic syntax is:

~~~
chmod [permission] [file_name]
# one way that is the simplest to remember
chmod u=rwx,g=rwx,o=rwx [file_name]
~~~
{: .language-bash}

- rwx stand for r(ead),w(rite) and (e)x(ecute)
- and ugo stand for u(ser), g(roup) and o(ther)
		
----

## Knowing how to go home
A program that tracks your location provides an opportunity to discuss the difference between **relative** and **absolute** locations. The `pwd` command returns the absolute path to where you are. The shell contains two important variables, both of which are subjective. The first is the environment variable `$PWD`, which specifies your current active location. The other is `$HOME`, which is the active user's home folder. We can create our own variables in the shell to make navigation easier. Try to discuss when this following code can be useful?  

~~~
ORIGIN=$PWD
cd $HOME
# do stuff
cd $ORIGIN
~~~
{: .language-bash}

 
> Here we create a variable named `ORIGIN` which represents our starting position, so we can go to other places, such as our home directory, run a program there, and eventually return to our origin.
{: .solution}

## Alias
- Shell aliases are used to reference a command. 
- They can be used to avoid typing long commands or to correct incorrect input. 
- It can reduce keystrokes for common patterns and increase efficiency. 
- Consider using it for complex commands with frequently used options, or even simple commands with commonly used options.
- The format is simple and this is a good opertunity to share with you some cool examples of using ls 

~~~
alias ls='ls -h --color'
alias ll="ls -lv --group-directories-first"
alias lm='ll | more' # Pipe through 'more'
alias lr='ll -R' # Recursive ls.
alias la='ll -A' # Show hidden files.
alias lx='ll -XB' # Sort by extension.
alias lk='ll -Sr | sr' # Sort by size, biggest first.
alias lt='ll -tr | sr' # Sort by date, most recent first.
alias # list all current aliases
~~~
{: .language-bash}


## creating content in the terminal (Old-school)
In the last section for this episode we will cover different ways to generate files via the terminal. 

## `echo`

- Prints text to the terminal window
- The most basic process in any programming language is the ability to output information.
- The `echo` command prints text to the terminal window and is typically used in shell scripts and batch files to output
status text to the screen or a computer file.
- Echo is also particularly useful for showing the values of environmental variables, which tell the shell how to behave
as a user works at the command line or in scripts.

~~~
cd ~/sandbox/My_first_project/Report 
echo $ORIGIN
echo $HOME
echo $PWD
~~~
{: .language-bash}

> ### Examples using `echo` 
> ~~~
> cd ~/sandbox
> echo Some text to print out
> # any string after the command will be printed
> echo *
> # Will Print all the files/folder using echo command
> echo *.jpeg
> # Will Print all the files of a specific kind
> echo "Some text to add to a file" > file
> # Use redirect operator > to store output to file
> echo "Some other text to add to a file" >> file
> # Use redirect append operator >> to add output to file
> ~~~
{: .output}


## `cat` — Read a file, create a file, and concatenate files
A close relative of `echo` is `cat` (short for “concatenate“) one of the more versatile commands and serves three main functions:

- Displaying files
- Combining multiple files
- Creating new files.


> ### Examples using `cat` 
> ~~~
> cat file
> # Displaying Contents of a File
> cat > file_2
> # Allows to write text interactively
> cat file_2 > file
> # It is possible to redirect > to output like echo
> # However the above command overwrites the file contents
> cat file file_1 file_2
> # We can also view contents of multiple files
> cat file_1 >> file
> # file_1 content will be appended at the end of file
> ~~~
{: .output}


## `tee` — Often we would like to write multi line files
This command reads the contents of standard input, emits them to standard output, and makes a copy of them into the specified file(s) or variables.
The purpose of this example is to create a `.bash_aliases` file containing all of your aliases and learn how to use the `tee` command. 
We understand what aliases are. However, it's vital to comprehend that the aliases you create will only remain as long as the shell is open.
Hence, it is useful to keep all aliases in one file.

> ### Example using `tee` 
> ~~~
> tee -a ~/.bash_aliases << END
> alias ls='ls -h --color'
> alias ll="ls -lv --group-directories-first"
> alias lm='ll | more' # Pipe through 'more'
> alias lr='ll -R' # Recursive ls.
> alias la='ll -A' # Show hidden files.
> alias lx='ll -XB' # Sort by extension.
> alias lk='ll -Sr | sr' # Sort by size, biggest first.
> alias lt='ll -tr | sr' # Sort by date, most recent first.
> END
> ~~~
{: .output}

You can see we are using the -a option, which appends the content between the two END statements into the filename. What might happen if we won’t use that option?

## Using the concept of relative path we can create our first generlised Bash script 


> # Is this function useful? Can you explain what it does?
> ~~~
> tee -a ~/.make_dir << END
> mkdir -p ./{Notebooks,Code,Tmp,Data,Report,Presentation}
> mkdir -p ./Data/{pkl,csv,zip}
> mkdir -p ./Report/{Tables,Figures,Text}
> mkdir -p ./Background/{pdf,pptx}
> END
> ~~~
> {: .language-bash}
{: .discussion}


> # Try it... 
> ~~~
> cd ~/sandbox
> mkdir -p test
> cd test
> source ~/.make_dir
> source ~/.bash_aliases
> ll 
> ~~~
> {: .language-bash}
{: .discussion}


## Last but not least, `nano`, the easiest editor ever

Sometimes you need to write free text in a terminal, `nano` is the simplest and most intuitive text editor out there. 

> ## Try spawning `nano` and write a `~/.profile` that prints "running my .profile" when excuted
> > ~~~
> > nano ~/.profile
> > ~~~
> {: .language-bash}
> > ### In `nano`
> > ~~~
> > echo "running my .profile"
> > ~~~
> {: .language-bash}
{: .solution}

## Links to expand your understanding 

While pursuing a PhD, you should always strive to refresh, clarify, and expand your knowledge. Here are some links to support you in that: 

- [introduction-to-shell](https://learn.datacamp.com/courses/introduction-to-shell)
- [Introduction to Bash Scripting](https://learn.datacamp.com/courses/introduction-to-bash-scripting)


{% include links.md %}

