---
title: "Anaconda environment 101"
author: "Dr. Eyal Soreq" 
date: "31/05/2021"
teaching: 20
exercises: 20
questions:
- What is Conda?
- Why should I use a package and environment management system as part of my research workflow?
- What is an environment? 
- How do I create my own environment in the gwdg jupyter cloud 
objectives:
- Understand what Conda is and how it can simplify analysis pipelines.
- Learn how to configure Conda on the gwdg jupyter cloud 
- Make sure you can run FSL commands from a notebook 

keypoints:
- Conda is a Python-based environment and package manager
- It enables us to use 
---

# Conda in Theory?

## What is Conda?
Conta is a package and environment manager based on Python. It assists in the development of reproducible analysis pipelines using crowd-sourced and version-controlled packages. It might be a bit confusing for an individual who is new to this type of approach. In order to make sure we all understand each other, let's establish some quick vocabulary:

## What is an environment?

In a computing environment, people use an assortment of programs, language libraries, etc. to operate a computer.  
Depending on the context, the word environment can have many different meanings, like a generalized term for an ecological ecosystem that can refer to anything from a puddle to a continent.  
As far as we're concerned, an environment is simply a set of tools that are put together to assist us in exploring data-driven questions in a reproducible manner.

## What is an package?
As the name implies, a package is a collection of software, including things like programs  (e.g. Python), programming libraries (e.g. Bash), or other useful tools.  
Using the Conda package management system, you can combine packages and make complex environments.  
It can be summed up like this: Conda creates self-contained modules that contain all of the necessary programs, etc, in order to complete a specific task of computing.


## What is dependency hell
The term dependency hell refers to the problems that users generally face when they rely on many interdependent packages.  
The main source of complications or bugs in dependency hell are changes made to third-party packages that are no longer compatible with one another.


## How does Conda manage dependencies
Conda helps manage dependencies in two primary ways:
Allows the creation of environments that isolate each project, thereby preventing dependency conflicts between projects.  
Provides identification of dependency conflicts at time of package installation, thereby preventing conflicts within projects/environments.

## What is version control 
Version control is what, exactly? Version control tools allow you to keep track of the changes you make to your work over time.  
This feature is a little like "track changes" in Google Docs, but with the difference that you can save changes across several files, not just within one.

## Why is Conda useful?

Using Conda as part of analysis workflows has a lot of advantages:

1. It helps keep your computing environment organized so you're less likely to end up in "dependency hell".
1. Since packages are version-controlled, you can easily switch versions if one doesn't work.
1. Operating systems aren't really an issue (it runs on Mac, Windows, Linux). However, not every package is available for every OS.
1. We can replicate and share environments, so our analysis is more accurate.

## Conda in Practice over the gwdg
1. One thing we ultimately want is having full control over the environment
1. The following is true to your local computer as well as the cluster
1. Anaconda gives us this power exactly


## Our first job extending our `.profile` 

Our *.profile* is the place where all our settings are kept, so it will come as no surprise that we will also use it to configure Anaconda.
We will open terminal instance in the jupyter cloud and append `source /opt/conda/etc/profile.d/conda.sh` to the end of our `.profile` file. 
Remember that we must source the `.profile` file for any changes we make to take  effect.

> # Copy and run the following code 
> ~~~bash
> echo source /opt/conda/etc/profile.d/conda.sh >> ~/.profile
> source ~/.profile
> ~~~
> 
> ~~~
> running my .profile
> ~~~
> {: .output}
{: .challenge}

## Test conda

Run the following code to verify conda is running and configured correctly

~~~bash
conda info
~~~

## You should get an output that resembles this.

~~~
     active environment : base
    active env location : /opt/conda
            shell level : 1
       user config file : /home/jovyan/.condarc
 populated config files : /opt/conda/.condarc
                          /home/jovyan/.condarc
          conda version : 4.10.0
    conda-build version : not installed
         python version : 3.8.8.final.0
       virtual packages : __linux=4.15.0=0
                          __glibc=2.31=0
                          __unix=0=0
                          __archspec=1=x86_64
       base environment : /opt/conda  (writable)
      conda av data dir : /opt/conda/etc/conda
  conda av metadata url : https://repo.anaconda.com/pkgs/main
           channel URLs : https://conda.anaconda.org/conda-forge/linux-64
                          https://conda.anaconda.org/conda-forge/noarch
          package cache : /opt/conda/pkgs
                          /home/jovyan/.conda/pkgs
       envs directories : /home/jovyan/env
                          /opt/conda/envs
                          /home/jovyan/.conda/envs
               platform : linux-64
             user-agent : conda/4.10.0 requests/2.25.1 CPython/3.8.8 Linux/4.15.0-140-generic ubuntu/20.04.2 glibc/2.31
                UID:GID : 1000:100
             netrc file : None
           offline mode : False
~~~
{: .output}           


## Creating and Managing Environments

### Environments 101

Now that we've made sure Conda is working, we're ready to start learning how to use it as an environment-based package manager.   
Environments are an integral part of Conda-based workflows.   
They are customizable, reproducible, and shareable modules that contain the resources for a specific task or set of tasks.   
Environments also help avoid "dependency hell" where required programs are incompatible with previously installed programs or program versions.  
Our objective for today is to set up an FSL bash notebook and configure the conda environments. We will continue this journey tomorrow when we dive into Python, where conda really shines. 


### View installed enviorments 

To start with, let's see what environments we currently have set up.  
This will list all of the environments available for us to use along with their locations.

~~~bash
conda env list
~~~

Should look like this:

~~~
base                  *  /opt/conda
~~~
{: .output}  

By default, an environment called `base` is created when installing and intializing Conda.  
`base` contains a number of standard Python packages that may or may not be useful.

### View installed kernels  

Remember that a kernel is just a program that runs and inspects your code: it provides computation and communication with frontend UIs, like  notebooks.  
The Jupyter Notebook Application has three main kernels: the IPython (python3), IRkernel (ir) and IJulia (julia-1.6) kernels.  
XPython and bash are two additional kernels in our gwdg cloud.  
XPython is primarily used for debugging python code, and we have been using the bash kernel since we began the course and it provides direct access to bash programs.

~~~bash
jupyter kernelspec list
~~~

Should look like this:

~~~
  bash            /opt/conda/share/jupyter/kernels/bash
  ir              /opt/conda/share/jupyter/kernels/ir
  julia-1.6       /opt/conda/share/jupyter/kernels/julia-1.6
  python3         /opt/conda/share/jupyter/kernels/python3
  xpython         /opt/conda/share/jupyter/kernels/xpython
~~~
{: .output}  


## How do we create a new environment in anaconda

1. In Anaconda, you can create an environment by typing the following: `conda create --name myenv`, where myenv is the name of your environment.
1. This creates an empty environment named myenv in `$HOME/env/`. 
1. To create an environment with a particular version of Python, simply type in `conda create --name myenv python=3.8` Keep in mind that this will create a very large folder, so be careful.
1. To create an environment with specific packages, simply list the packages you wish to include:  `conda create --name myenv numpy pandas matplotlib`
1. To specify the location of an environment (i.e. in a place different to the default location) use the `--prefix` option as follows :   `conda create --prefix ~/some_path/myenv`
1. To remove an environment, in your terminal run: `conda remove --name myenv --all`

<!-- ## Creating an environment from an environment.yml file  add tomorrow -->


## Let's create a new environment 
Armed with this information we will now create our first environment.
We will call this environment `FSL_sandbox` for reason i will explain in our next session.


~~~bash
conda create --name bash_sandbox && conda env list
~~~

Recall that using a double `&` symbol means that the next command is only executed if the first one was successful.

~~~
# conda environments:
#
FSL_sandbox             /home/jovyan/env/FSL_sandbox
base                  *  /opt/conda
~~~
{: .output}  

## We need to register our environment to Jupyter KernelSpec

It is the *KernelSpec* that determines what kernels are available on our Jupyter portal.  
If we create a new environment and want it to be available we need to install it which in essence simply means adding it in a list somewhere.  
We do that using a software called `ipykernel` which is a powerful interactive Python shell and a Jupyter kernel to work with Python code in Jupyter notebooks and other interactive frontends.  
The following code registers the new environment we created and creates a folder in your hidden `.local` folder that stores the information needed to run that kernel. 

~~~bash
python -m ipykernel install --user --name=FSL_sandbox
~~~

~~~
Installed kernelspec FSL_sandbox in /home/jovyan/.local/share/jupyter/kernels/FSL_sandbox
~~~
{: .output} 

## Look under the hood 

If we list the files in the new kenrel folder we should find three files  

~~~ bash 
ls /home/jovyan/.local/share/jupyter/kernels/FSL_sandbox
~~~

~~~
kernel.json  logo-32x32.png  logo-64x64.png
~~~
{: .output} 

The two images are two sizes of the Python logo, and that is the image Jupyter will use as an icon (Changing it, however, is not easy).  
The more intresting file is the `kernel.json` it contains all the information about the kernel.  
If we `cat` it's contents we get the following info :

~~~bash
cat ~/.local/share/jupyter/kernels/FSL_sandbox/kernel.json
~~~

~~~
{
 "argv": [
  "/opt/conda/bin/python",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "FSL_sandbox",
 "language": "python"
}
~~~
{: .output} 

The parameters need to be changed to point to a bash kernel rather than a  `ipykernel_launcher`. 

We can either open the file using `nano` in a terminal or alternatively use `tee` to overwrite the file as follows:

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
 "env": {"PS1": "$"},
 "language": "bash"
}
END
~~~

> ## What are we doing here? 
> What information are we changing and adding here and how will this  affect the new kernel?
{: .discussion}


## Now we are ready to activate our environment

To do that we use the following code: 

~~~ bash 
conda activate FSL_sandbox
~~~

## We can also deactivate our environment

Don't run this I include it only for your reference 

~~~ bash 
conda deactivate
~~~

## Open the launcher and open a new FSL_sandbox notebook 

If everything worked we should now be able to create an FSL_sandbox bash notebook. 

Something we will do just after a short break of 10 minutes (for coffee).   
 


## Links to expand your understanding 

For those interested in learning more...

- [Conda Essentials](https://learn.datacamp.com/courses/conda-essentials)
- [Building and Distributing Packages with Conda](https://learn.datacamp.com/courses/building-and-distributing-packages-with-conda)
- [Some background on ipython and jupyter](https://www.datacamp.com/community/blog/ipython-jupyter)
- [Jupyter Notebook Tutorial: The Definitive Guide](https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook)


{% include links.md %}

