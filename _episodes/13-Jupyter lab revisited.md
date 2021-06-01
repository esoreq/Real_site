---
title: "Jupyter lab revisited"
author: "Dr. Eyal Soreq" 
date: "02/06/2021"
teaching: 45
exercises: 0
questions:
- What are Magic commands?
- How to setup a python_sandbox kernel?
objectives:
- Learn what magic commands are and how to use them 
- Learn how to setup a python kernel and how to set it up 
keypoints:
- Magic commands are enhancements created for the interactive Python project
- Line magics, which are denoted by a single % prefix and operate on a single line of input
- Cell magics, which are denoted by a double %% prefix and operate on multiple lines of input
---


# Jupyter notebook 

- Magic commands are enhancements created for the interactive Python project which Jupyter notebook can be viewed as a web evolution of 
- Magic commands are designed to simplify everyday tasks in the standard data analysis workflow
- There are two types of Magic commands: 
    - Line magics, which are denoted by a single % prefix and operate on a single line of input, 
    - Cell magics, which are denoted by a double %% prefix and operate on multiple lines of input. 
- For a full list of magic commands press [here](https://ipython.readthedocs.io/en/stable/interactive/magics.html#line-magics)
- Here we will explore some of the most useful ones 


# %load_ext autoreload

- This magic command is crucial for almost any actual work using Jupyter (except tutorials :)
- The  autoreload extension tracks any changes in your imports and will *auto* *reload* them to your scope 
- By running this, we allow any imported file to be updated 

~~~python
%load_ext autoreload
%autoreload 2
~~~

#  %system

- If you want access to the shell, this magic command will do it.

~~~python
%system date +%s%N
~~~

- However, using exclamation mark (!) is even more useful  

~~~python
date = !date +%s%N
date
~~~

# But %%bash can be even more useful

~~~python
%%bash 

echo "Printing text with newline"
echo -n "Printing text without newline"
echo -e "\nRemoving \t backslash \t characters\n"
~~~

# %whos

- This magic command plots a list of variables in your environment. 
- Their type and some additional info
- You can pass %whos a type to examine only variables of that type

~~~python
%whos function
~~~

~~~
Variable                Type        Data/Info
---------------------------------------------
age2group               function    <function <lambda> at 0x7fb3b57af820>
age_group               function    <function age_group at 0x7fb3b57af1f0>
anything_but_children   function    <function <lambda> at 0x7fb3b57af0d0>
is_children             function    <function <lambda> at 0x7fb3b57af670>
temporal_hello          function    <function temporal_hello at 0x7fb3b57e99d0>
~~~
{: .output}

# %who_ls 

- This magic command shows you the list of variables in your environment. 
- It also can use the type to subset the output
- Using 'type' will retrive only class objects

~~~python
class test():
  pass
%who_ls type
~~~

# %time and %%time 

- When developing a pipeline, it is useful to know how much time a specific function needs 
- Time and its variations will do precisely that 
- To measure one line of code, we will use %time
- To measure a cell, we will use %%time


# Compare %time

~~~python
age2group = lambda age: 'children' if age<=11 else 'teens' if age<=21 else 'adults' if age<=65 else 'elderly'
is_children = lambda age: age<=11 
%time print(list(map(age2group,filter(is_children, list(range(5,80,1))))))
~~~

> ## Output
> > ~~~
['children', 'children', 'children', 'children', 'children', 'children', 'children']
CPU times: user 137 µs, sys: 62 µs, total: 199 µs
Wall time: 188 µs
> > ~~~
{: .solution}


# With %%time

~~~python
%%time 
age2group = lambda age: 'children' if age<=11 else 'teens' if age<=21 else 'adults' if age<=65 else 'elderly'
is_children = lambda age: age<=11 
print(list(map(age2group,filter(is_children, list(range(5,80,1))))))
~~~


> ## Output
> > ~~~
['children', 'children', 'children', 'children', 'children', 'children', 'children']
CPU times: user 456 µs, sys: 0 ns, total: 456 µs
Wall time: 423 µs
> > ~~~
{: .solution}




#  %timeit  and %%timeit 
- %timeit will measure multiple iterations of the same line and show some stats on them
- %%timeit will do the same for the cell


~~~python
%timeit even_squares = [x**2 for x in range(1,int(1e5)) if x**2%2==0]
~~~


> ## Output
> > ~~~
44.4 ms ± 259 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)
> > ~~~
{: .solution}


~~~python
%%timeit
even_squares = [x**2 for x in range(1,int(1e5)) if x**2%2==0]
odd_squares = [x**2 for x in range(1,int(1e5)) if x**2%2!=0]
~~~


> ## Output
> > ~~~
88.5 ms ± 543 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)
> > ~~~
{: .solution}

# %reset 

- Use %reset to Clear All Variables in IPython - Requires User Confirmation.
- Use %reset -f to Clear All Variables in IPython - No User Confirmation.

# %xdel

- Delete a variable, clearing only it from memory.

~~~python
even_squares = [x**2 for x in range(1,int(1e5)) if x**2%2==0]
%whos list
%xdel even_squares
%whos list
~~~

> ## Output
> > ~~~
Variable       Type    Data/Info
/--------------------------------
even_squares   list    n=49999
No variables match your requested type.
> > ~~~
{: .solution}


# %%svg is cool 

- render a cell using some external programing languaege in thsi case scalable vector graphics 
- Try this :)

~~~python
%%svg
<svg width="800" height="200">
  <g transform="translate(100,100)"> 
    <text id="TextElement" x="0" y="0" style="font-family:Verdana;font-size:24; visibility:hidden"> It's MAGIC!
      <set attributeName="visibility" attributeType="CSS" to="visible" begin="1s" dur="6s" fill="freeze" repeatCount="indefinite" />
      <animateMotion path="M 0 0 L 100 100" begin="1s" dur="3s" fill="freeze" repeatCount="indefinite" />
      <animateTransform attributeName="transform" attributeType="XML" type="rotate" from="-30" to="0" begin="1s" dur="3s" fill="freeze" repeatCount="indefinite"/> 
      <animateTransform attributeName="transform" attributeType="XML" type="scale" from="1" to="3" additive="sum" begin="1s" dur="3s" fill="freeze" repeatCount="indefinite" /> 
    </text> 
  </g> 
  Sorry, your browser does not support inline SVG.
</svg>
~~~


#  %%writefile Hello_world.py

- Write the contents of a cell to a file in the same folder 

~~~python
%%writefile Hello_world.py
print('Hello World')
Hello = 'World'
~~~

> ## Output
> > ~~~
Writing Hello_world.py
> > ~~~
{: .solution}

## What will happen if we run ot again?

> ## Output
> > ~~~
Overwriting Hello_world.py
> > ~~~
{: .solution}

## What about appending?  

~~~python
%%writefile setup.py
first_name = 'Eyal'
iter_num = 50
~~~
~~~
Writing setup.py
~~~

{: .output}
~~~python
%%writefile -a setup.py

last_name = 'Soreq'
small_num = -1e12
~~~
~~~
Appending to setup.py
~~~
{: .output}



#  %run Hello_world.py
- If we can write we can also run

~~~python
%run Hello_world.py
print(f'{"*"*30}')
%whos str
~~~

~~~
Hello World
******************************
Variable   Type    Data/Info
----------------------------
Hello      str     World
~~~
{: .output}


~~~python
%reset -f
%run setup.py
%whos str
~~~

~~~
Variable     Type    Data/Info
------------------------------
first_name   str     Eyal
last_name    str     Soreq
~~~
{: .output}



# How do we setup our new kernel 

- Open a terminal and run the following commands

~~~python
conda create --name python_sandbox
conda activate python_sandbox
python -m ipykernel install --user --name=python_sandbox
~~~

- Now use your newly acquired magic power to add FSL bash environment variables

~~~python
%%writefile ~/.local/share/jupyter/kernels/python_sandbox/kernel.json
{
 "argv": [
  "/opt/conda/bin/python",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "python_sandbox",
  "env": {
     "FSLDIR":"/home/jovyan/fsl",
     "PATH":"$PATH:/home/jovyan/fsl/bin",
     "FSLOUTPUTTYPE":"NIFTI_GZ"
},
 "language": "python"
}
~~~

# Test that fsl is accessible 

~~~python
hdr = !fslinfo ~/fsl/data/standard/MNI152_T1_1mm_brain.nii.gz
[line.split('\t') for line in hdr]
~~~

~~~
[['data_type', 'INT16'],
 ['dim1', '', '182'],
 ['dim2', '', '218'],
 ['dim3', '', '182'],
 ['dim4', '', '1'],
 ['datatype', '4'],
 ['pixdim1', '', '1.000000'],
 ['pixdim2', '', '1.000000'],
 ['pixdim3', '', '1.000000'],
 ['pixdim4', '', '1.000000'],
 ['cal_max', '', '8000.000000'],
 ['cal_min', '', '3000.000000'],
 ['file_type', 'NIFTI-1+']]
~~~
{: .output}



{% include links.md %}