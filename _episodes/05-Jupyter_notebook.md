---
title: "Introduction to Bash Jupyter notebook"
author: "Dr. Eyal Soreq" 
date: "05/03/2021"
teaching: 30
exercises: 20
questions:
- What is Jupyter Notebook?
- What are key benefits of the Jupyter Notebook
- What is FSL and how can we make our notebook run FSL commands? 
- What is the `.profile` good for?
objectives:
- List the components and functionality of Jupyter Notebook.
- Launch and navigate the Jupyter Notebook dashboard.
- Open, create and save Jupyter Notebook files.
- Learn how to setup FSL to be usable in a Jupyter notebook
- Learn how to setup and use Bash environment variables in the `.profile` file
- Learn how to use a notebook to run bash code snippets.

keypoints:
- Jupyter notebook is a tool designed to simplify and improve data science projects
- Jupyter notebooks are Human readable way to document any complex process that relies on a mixture of code and text 
- In a notebook, kernels are programs that run and inspect the code section. They are not specific to one language
- FSL is a set of programs designed to support the analysis of neuroimaging data
- In the `.profile` file we can store a set of variables that our operating system will need when it runs certain programs.

---


## What is Jupyter notebook?

- Jupyter notebook is a modern web-based open-source tool specifically designed to support data science projects. 
- You can use Jupyter Notebooks to document workflows and to share code for data processing, analysis and visualization.

## Jupyter Notebook Overview

This course makes extensive use of notebooks, which allow you to document code and thoughts while being able to follow your work. This section explains how to use Jupyter Notebook to facilitate open reproducible science workflows and introduces you to the interface that you will use for running and editing code and Markdown cells. 


## Jupyter Notebook for Open Reproducible Science

- The Jupyter Notebook file format (.ipynb ) is constructed from linearly stacked cells allowing you to construct a single project-oriented file that combines descriptive text, code blocks and code output in a single file. 
- The code cells have output cells associated with them, allowing you to include plots, tables, and textual outputs to communicate your findings, within the notebook file. 
- You can then export the notebook to a .pdf or .html that can then be shared with anyone.


## Key benefits of the Jupyter Notebook
1. **Human readable**: Using Jupyter, you can bridge ideas and concepts with methodology and results, creating a notebook that can be understood by different types of researchers. By adding Markdown text around your code, your project becomes more user-friendly and easier to understand. 
1. **Simple syntax:**  Markdown is simple to learn and use reducing the learning curve needed to produce well-documented Jupyter reports.
1. **Documenting your ideas:** Research is all about creating logical steps based on assumptions followed by tests. However, actual Research is messy, and many things will be left on your digital workbench. Forming the habit of documenting your workflow, making inline references when needed, and explaining the logical workflow, will be priceless to the future you. Just imagine changing or adapting specific parts of a study two years after it was created, without some comments.
1. **Easy to Modify:** analyses contained within a Jupyter Notebook can be easily extended, improved or refined by adding or editing the workflow and rerunning the notebook.
1. **Simple to share:** Sharing your workflow with colleague or supervisor is in the core of the Jupyter DNA. A notebook can be shared using file-sharing services like Dropbox or Google Drive or more sophisticated approaches such as Github. This simplifies the process of validating, replicating, extending, refining and communicating your workflow.
1. **Flexible export formats:** Notebooks can be exported into various formats including HTML, PDF and slideshows.

## Jupyter Notebook types

There are four kinds of notebooks you would want to create:  

- **The lab** - a historical (and dated) record of your analysis
- **The report** - a polished version of some study, intended for collaboration and review 
- **The presentation** - a slideshow designed to communicate ideas with collaborators  
- **The book** - Multi-notebook scientific project presented in book format


##  What are Jupyter kernels 
A kernel is a computer program that runs and inspects the user's code. IPython includes a kernel for Python code. Others have written kernels for various other languages. We will begin by using the bash built-in kernel today. Tomorrow, we will cover how to set up a project-specific environment and start our journy into python.


## So let's open a notebook using the Bash kernel
press <kbd>Shift + CMD + L</kbd> to open a new launcher (or open the file menu and select new Launcher). If you select the bash notebook, a new notebook tab named `Untitled.ipynb` will appear.

## Jupyter Notebook modes 

- There are two modes of action in Jupyter: *Command* and *Edit*.  
- Command mode allows you to edit your notebook, but you cannot type in cells
- to enter command mode you press the  <kbd>Esc</kbd>  button. 
- Pressing <kbd>Enter</kbd> will transfer you to EDIT mode where you can interact with each cell in your notebook. 

> ## Change top cell to markdown mode
> Select the top cell using your mouse 
> Press <kbd>Esc +  M</kbd>
> Write the following in that cell 
> ~~~markdown
> # FSL setup 
> Learning how to setup FSL in jupyter-cloud.gwdg.de
> ~~~
> Now press <kbd>Shift+Enter</kbd> to render the Markdown cell
> 
{: .challenge}


# COMMAND mode useful shortcuts

The same goes to COMMAND shortcuts.  
  
| Key | Function | 
| :-- | :-- |
| <kbd>Esc + Y</kbd> | Change cell to code type |
| <kbd>Esc +  M</kbd> | Change cell to markdown type |
| <kbd>Esc + SHIFT + up</kbd> | select cells above |
| <kbd>Esc + SHIFT + down</kbd> | select cells above |
| <kbd>Esc + SHIFT + M</kbd> | merge selected cells |
| <kbd>c</kbd> | copy selected cells |
| <kbd>x</kbd> | cut selected cells |
| <kbd>v</kbd> | paste selected cells |


## EDIT mode useful shortcuts

When in EDIT mode, there are several key commands it is good to know.  
You should practice using these commands until they become second nature. 


| Mac  |  Function | 
| :--  |  :--      |
|<kbd>Tab</kbd>|  code completion/indent |
|<kbd>Shift+Tab</kbd>|  function help |
|<kbd>Cmd + /</kbd>|  comment/uncomment |
|<kbd>Ctrl+Enter</kbd>| run current cell |
|<kbd>Shift+Enter</kbd>|  run current cell + select below|
|<kbd>Alt+Enter</kbd>|  run current cell + insert below|
|<kbd>Ctrl+Shift+-</kbd>|  Split cell at cursor |
|<kbd>Cmd+s</kbd>|   Save notebook |
|<kbd>D+D</kbd>|   Delete selected cells |


## Our first job setting up our profile 

Our last task in the previous episode was to create a file called `.profile`. We will now use this file to set up our environment.
At the top cell in your open notebook copy the follwoing code and run the cell using <kbd>Shift+Enter</kbd>:  

> # Copy and run the following code
> ~~~
> echo source ~/.bash_aliases >> ~/.profile
> source ~/.profile
> ~~~
> {: .language-bash}
> This time use <kbd>Ctrl+Enter</kbd> to run the new code cell 
> ~~~
> running my .profile
> ~~~
> {: .output}
{: .challenge}

## What did we just do? 
In sourcing the file, we are executing any commands inside - therefore all the aliases we added to the `.bash_aliases` file will be available in the notebook.
This means that this `.profile` is one stop place to place any settings required by any shell related software, as you will see soon. 


## Document this code using markdown
A key difference between the two shortcuts is that the first moves to the next cell and creates it if it does not exist, while the other simply runs the cell.
This shortcut <kbd>Ctrl+Shift+-</kbd> makes it easy to create a new cell, as well as a convenient way to divide a cell that contains multiple commands into independent cells so you can add comments explaining what they do.

> # Challenge
> Divide the single cell into two and add a markdown cell in front of each, and add text comments describing each command.
> 1. Go to the end of the first line and press <kbd>Ctrl+Shift+-</kbd>
> 1. Now go the begining of each of the commands and press <kbd>Ctrl+Shift+-</kbd> again 
> 1. Convert each of the new empty code cells to Markdown using <kbd>Esc +  M</kbd>
> 1. On the top empty markdown cell write the following text
> ~~~markdown
> ## Appending line to file using echo 
> The line `source ~/.bash_aliases` is added into the file `~/.profile` using `echo` and the append `>>` symbol
> ~~~
> 1. On the middle empty markdown cell write the following text
> ~~~markdown
> ## Sourcing `~/.profile` file apply the new edits  
> With the source (you can also use a dot `.` instead) command, commands are read from a specified file and executed in the current shell environment.
> ~~~
{: .challenge}


## Different ways of excuting programs 
It is possible to use conditional variables in shell to control how successive commands are treated.
You can then create scripts that continue even if a step fails, issue multiple commands simultaneously, etc.
One of the advantages of bash is that it has the capability to work asynchronously. This means that if we have a set of commands that don't depend on each other, we can execute them without waiting for them to complete. 

- Using the semicolon ';' groups commands without dependency.
- Using a double '&&' groups commands with an `AND` dependency chain .
- Using a double vertical line '||' groups commands with an `OR` dependency chain.
- Using a single and '&' runs the last command in the background.

## Let's create a notebook to setup FSL on your home 
In order to illustrate this, let's install and configure FSL, which is a neuroimaging software package which includes many functions useful for preprocessing and analysis of structural and functional fMRI.


## Step 1. 
Start by creating at your home folder two new folders named `fsl` and `temp`

> ## Create `~/temp` and `~/fsl`
> > ~~~
> > mkdir -p ~/{temp,fsl}
> > ~~~
> {: .language-bash}
{: .solution}

## Step 2. 
Goto [FSL home page](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/)
If you are involved in neuroimaging related projects and have very little or no background in neuroimaging, it would be helpful to bookmark this page.

## Step 3. 
We are going to use a bash software called `wget` that is used to download file from internet links using the command line. 
Start by copying and running the following code in your notebook 

~~~bash
FSL_TAR=fsl-6.0.4-centos7_64.tar.gz
wget -O ~/temp/$FSL_TAR https://fsl.fmrib.ox.ac.uk/fsldownloads/$FSL_TAR
~~~

### What does this mean
- We start by creating a variable that holds the target zip file 
- Then we use the `wget` command with the `-O` option to direct the download to a specific location  


> ## Discussion
> Why is it beneficial to separate the file name from the command?
{: .discussion}


### You should get the following output:
~~~
--2021-05-22 09:29:57--  https://fsl.fmrib.ox.ac.uk/fsldownloads/fsl-6.0.4-centos7_64.tar.gz
Resolving fsl.fmrib.ox.ac.uk (fsl.fmrib.ox.ac.uk)... 129.67.248.65
Connecting to fsl.fmrib.ox.ac.uk (fsl.fmrib.ox.ac.uk)|129.67.248.65|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4080459725 (3.8G) [application/x-gzip]
Saving to: ‘/home/jovyan/temp/fsl-6.0.4-centos7_64.tar.gz’
~~~
{: .output}

### This will update after around 80-130s to this 
~~~
--2021-05-22 09:29:57--  https://fsl.fmrib.ox.ac.uk/fsldownloads/fsl-6.0.4-centos7_64.tar.gz
Resolving fsl.fmrib.ox.ac.uk (fsl.fmrib.ox.ac.uk)... 129.67.248.65
Connecting to fsl.fmrib.ox.ac.uk (fsl.fmrib.ox.ac.uk)|129.67.248.65|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 4080459725 (3.8G) [application/x-gzip]
Saving to: ‘/home/jovyan/temp/fsl-6.0.4-centos7_64.tar.gz’

/home/jovyan/temp/f 100%[===================>]   3.80G  45.3MB/s    in 85s     

2021-05-22 09:31:22 (46.1 MB/s) - ‘/home/jovyan/temp/fsl-6.0.4-centos7_64.tar.gz’ saved [4080459725/4080459725]
~~~
{: .output}


## Step 4. 

We will use the tar command to unpack the file we just downloaded in our home directory. 
Due to the length of this operation, we will use the run in background option (to continue working while the unpacking is in progress).
Just copy the following and run it using <kbd>Shift+Enter</kbd>


~~~bash
tar -xf ~/temp/$FSL_TAR -C ~/ &
~~~

## Unpack the command 

- Let's unpack the tar command line from right to left

|  |  |
| :-- | :-- |
| `tar` | call the tar program |
| `-` | Add options to the program |
| `x` | extract a archive file |
| `f` | include target archive file |
| `~/temp/` | Where the target file is located |
| `$FSL_TAR` | our targer filename variable |
| `-C` | create extraction in a location  |
| `~/` | the target location is our home folder |
| `&` | Run in the background |
| | |

## What does the output mean ? 

~~~
[1] <some integer>
~~~
{: .output}


In most Unix and Unix-like operating systems, the `ps` program displays the currently-running processes. 
A process has a unique ID, and by using the ps command you can see which ones are currently running.
if we run the following: 

~~~bash
ps a
~~~

We should get an output similar to this: 

~~~
PID TTY      STAT   TIME COMMAND
1543 pts/1    Ss     0:00 /opt/conda/bin/bash --rcfile /opt/conda/lib/python3.8
2012 pts/1    D      0:24 tar -xf /home/jovyan/temp/fsl-6.0.4-centos7_64.tar.gz
2013 pts/1    S      0:38 gzip -d
2017 pts/1    R+     0:00 ps a
~~~
{: .output}

## Let's unpack the output

|  |  |
| :-- | :-- |
| `PID` | Unique process ID |
| `TTY` | The terminal the command is running in |
| `STAT` | Process states that indicate what state the program is in |
| `TIME` | How long this program has been running for (H:MM) |
| `COMMAND` | The actual command  |
| | |

## What we can do now 
Once untar is running in the background, we can move on to other things that I wish to teach you, and hopefully by the end of this session the unpacking will be complete, and we can evaluate some of FSL's capabilities.

## How to test if the PID is still running? 

Global regular expression print (grep) is used to search for a specific pattern in some input. 
The veritcal line that is called pipe just passes the standard output right to the grep command searching for our pid. 
If the pattern is found the process is still running. 

~~~bash
ps a | grep pid
~~~

## Configuring your shell environment
FSL requires you to define variables, we want to do this setup once and in the process give you some foundations that will be useful when you wish to set up a similar setup in more complex environments than our jupyter sandbox.

> ## Try to print out the ~.profile contents 
> > ~~~bash
> > cat ~/.profile 
> > ~~~
> > ~~~
> > echo "running my .profile"
> > source /home/jovyan/.bash_aliases
> > ~~~
> > {: .output}
{: .solution}

## Add to our profile file some additional variables 

To instruct the computer where to find fsl, we need to tell the computer where the bin fsl folder is located. 
Bin files are executable code for your application or library, and are stored in the bin folder. Basically, the bin folder contains files that allow you to use some kind of program. 
The `$PATH` variable specifies which directories on the machine contain executable programs that can be run without knowing the full path on the command line.
If you run `echo $PATH`, you should get the following output:  

~~~
/opt/conda/bin:/opt/conda/condabin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
~~~
{: .output}

We have different folder paths separated by colons (`:`) we need to add the fsl bin path to that line.
We will do that by creating an environment variable named `FSLDIR` pointing to the new fsl folder we just created.
Then we add `$FSLDIR/bin` to the path, which gives us (and all fsl functions) access to all the entire package.
We also need to configure the FSL default output type to be NIFTI_GZ, which means that MRI volumes will be stored using the [NIfTI](https://nifti.nimh.nih.gov/)
data format with [gzip](https://www.gzip.org/) compression.

To do all that we just need to add to our `.profile` file the following lines: 

~~~bash
export FSLDIR=$HOME/fsl
export PATH=$PATH:$FSLDIR/bin
export FSLOUTPUTTYPE=NIFTI_GZ
~~~

## Use what we learned in the previous session to solve this.

> ## Solution
> > ~~~bash
> > tee -a ~/.profile << END
> > export FSLDIR=\$HOME/fsl
> > export PATH=\$PATH:\$FSLDIR/bin
> > export FSLOUTPUTTYPE=NIFTI_GZ
> > END
> > ~~~
> > Important - If a variable is included in a script, the $ sign must be "escaped" to tell bash not to interpret it.
> > ## Test if worked 
> > ~~~bash
> > cat  ~/.profile
> > ~~~
> > ~~~
> > echo "running my .profile"
> > source /home/jovyan/.bash_aliases
> > export FSLDIR=$HOME/fsl
> > export PATH=$PATH:$FSLDIR/bin
> > export FSLOUTPUTTYPE=NIFTI_GZ
> > ~~~
> > {: .output}
{: .solution}

## Step 5. 

We will try to use one of the fsl programs just to make sure we did everything correctly. 
To begin, let's call a program called `fslinfo` and confirm that it is accessible.

~~~bash
fslinfo
~~~

Which should produce the following error: 

~~~
bash: fslinfo: command not found
: 127
~~~
{: .output}


> ## What went wrong?
> 
> In order to make these programs we need to source our updated `.profile` file.  Here I am sourcing the `.profile` file and calling slicer after it. 
> ~~~bash
> source ~/.profile && fslinfo
> ~~~
> ### This should output the following: 
>  ~~~ 
>  running my .profile
> Usage: /home/jovyan/fsl/bin/fslinfo <filename>
> ~~~
> {: .output}
{: .solution}

## Step 6. 
Let's conclude this session by using fslinfo to make sure we can do more than just print the help output.
Run the following line in your notebook.

~~~bash
fslinfo ~/fsl/data/standard/MNI152_T1_1mm_brain.nii.gz
~~~ 

The output should be as follows:

~~~
data_type	INT16
dim1		182
dim2		218
dim3		182
dim4		1
datatype	4
pixdim1		1.000000
pixdim2		1.000000
pixdim3		1.000000
pixdim4		1.000000
cal_max		8000.000000
cal_min		3000.000000
file_type	NIFTI-1+
~~~
{: .output}




## Step 7. 

The current setup requires us to run `.profile` every time we use the notebook (or even every time we restart the kernel), a better solution would be to embed the environment variables into the kernel.json. The following code implements that.

~~~bash
tee ~/.local/share/jupyter/kernels/FSL_sandbox/kernel.json << END
{
 "argv": [
  "/opt/conda/bin/python",
  "-m",
  "bash_kernel",
  "-f",
  "{connection_file}"
 ],
 "codemirror_mode": "shell",
 "display_name": "FSL_sandbox",
 "env": {
     "PS1": "$",
     "FSLDIR":"$HOME/fsl",
     "PATH":"$PATH:$FSLDIR/bin",
     "FSLOUTPUTTYPE":"NIFTI_GZ"
},
 "language": "bash"
}
END
~~~

## Test that your FSL_sandbox has access to fsl comands even 

Open the kernel menu and select `Restart Kernel and Clear All Outputs...`
Now add a new cell and write `slicer` and run the cell
If everything worked as planned you should have the following output

~~~
Usage: slicer <input> [input2] [main options] [output options - any number of these]

Main options: [-L] [-l <lut>] [-s <scale>] [-i <intensitymin> <intensitymax>] [-e <thr>] [-t] [-n] [-u]
These must be before output options.
-L       : Label slices with slice number.
-l <lut> : use a different colour map from that specified in the header.
-i <min> <max> : specify intensity min and max for display range.
-e <thr> : use the specified threshold for edges (if >0 use this proportion of max-min, if <0, use the absolute value) 
-t       : produce semi-transparent (dithered) edges.
-n       : use nearest-neighbour interpolation for output.
-u       : do not put left-right labels in output.

-c       : add a red dot marker to top right of imageOutput options:
[-x/y/z <slice> <filename>]      : output sagittal, coronal or axial slice
     (if <slice> >0 it is a fraction of image dimension, if <0, it is an absolute slice number)
[-a <filename>]                  : output mid-sagittal, -coronal and -axial slices into one image
[-A <width> <filename>]          : output _all_ axial slices into one image of _max_ width <width>
[-S <sample> <width> <filename>] : as -A but only include every <sample>'th slice
~~~
{: .output}

# Done 

Congratulations on setting up your notebook to run FSL programs natively.
Now we need to learn how to include comments to document your learning experience


## Links to expand your understanding 

For those interested in using FSL, you might find the following tutorials useful.

- [introduction-to-shell-fsl-style](https://www.youtube.com/playlist?list=PLvgasosJnUVnnFifxecbyEno7jnqrl8fQ)
- [FSL Tutorial: Part 1 (of many)](http://andysbrainblog.blogspot.com/2012/07/fsl-tutorial-part-1-of-many.html)


{% include links.md %}

