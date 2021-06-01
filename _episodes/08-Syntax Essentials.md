---
title: "Syntax Essentials and Best Practices"
author: "Dr. Eyal Soreq" 
date: "01/06/2021"
teaching: 25
exercises: 0
questions:
- What do we mean when we say syntax
- What types of Data can I store? 
- What is a variable in Python?
objectives:
- Best Practices in Python
- Syntax Essentials in Python
keypoints:
- Adapt naming conventions
- Stick to consistent indentation 
- Most of the time, simplicity and transparency are more important than performance
- Try to avoid using more than one statement per line
---

# What is a syntax

Syntax is the way words work together to make sentences, clauses, and phrases. "Syntax" means "arrange together," as well as "study of the syntactic properties of a language." The syntax of a computer language is the set of rules that define the combinations of symbols that are considered correct for that language.

# Syntax Essentials and Best Practices

One of the trickiest things for Python newcomers to adapt to is the syntax. 
In this opening section, I'll go over some syntax essentials as well as some formatting best practices.
This will help you keep your code consistent and hopefully elegant.


# Syntax Essentials rules

1. A naming convention simplifies collaboration - use them
1. Code blocks are defined by indentation (can be either space or tab)
1. Try to avoid using more than one statement per line
1. Python is case sensitive : $vara \neq  varA$
1. Path specification uses forward slashes (regardless of OS): `~/user/home`
1. There is no need to add a command terminator `;`
1. You can combine two executable statements using a semicolon `;`  (but avoid that if you can)
1. String literals can be defined using single `'` double `"` or even triple `'''` quotes 
1. It is considered good conduct to keep lines of code short 
1. Backslash \\ can be used to stack lines of code together
1. Expressions enclosed in brackets i.e. (), [] or {} don't need a backslash
1. Comments in Python begin with a hash mark (#) and whitespace character and continue to the end of the line. 
1. Keywords are protected and should not be used as variables


# Naming Conventions
A naming convention is a set of rules for selecting the character sequence that should be used to name different data types and data structures. This can be confusing if you have little background. So without going into what the following are (we will discuss them as we continue) I would like to lay them out for future reflection.

| Identifier  | Example  |  Commonly used for  | 
| :--- | :--- | :--- | 
| single lowercase letter | `x` | mathematical notation variables  |  
| single uppercase letter | `X` | mathematical notation variables |  
| lowercase sequence | `lowercase` |  variables, modules, functions and package|  
| uppercase sequence  | `UPPERCASE` | Constants |  
| Snake lowercase | `lower_case_with_underscores` | Variables and functions|  
| Snake uppercase | `UPPER_CASE_WITH_UNDERSCORES` | Constants |  
| Camel case | `CamelCase` | Class |  
| mixed case | `mixedCase` | ? |  
| Camel snake case | `Camel_Snake_Case` | ? |  
| single leading underscore | `_single_leading_underscore` | weak "internal use" indicator. E.g. from M import * does not import objects whose name starts with an underscore. |  
| single trailing underscore | `single_trailing_underscore_` | Single trailing underscore naming convention is used to avoid conflicts with Python keywords. |  
| double leading underscore | `__double_leading_underscore` | private variables and methods inside a class |  
| single trailing underscore | `__double_leading_and_trailing_underscore__` | "magic" objects or attributes that are built in the language (e.g. `__init__`) |  


# One statement per line

- If you put a line break in the wrong place, you will get an error message. 
- To avoid that you should have one statement per line.
- However, as with all rules, there are some exceptions some of which we will cover later in the course


# Explicit line joining 
- Using a backslash `\`, we can break long commands across many lines 

~~~python
print \
('Multi\
 line\
 command')
~~~

~~~
Multi line command
~~~
{: .output}


# Many commands in single line 
- Using the semicolon \; we can achieve the opposite, i.e. to combine multiple commands in one line


~~~python
print('Multi');print('Line');print('Output')
~~~

~~~
Multi
Line
Output
~~~
{: .output}


#  Implicit line joining

- Expressions in parentheses, square brackets or curly braces can be split over more than one physical line without using backslashes. 


~~~python
brain_lobes = ['Frontal',
               'Parietal',
               'Occipital',
               'Temporal']
print(brain_lobes)
~~~

    
~~~
['Frontal', 'Parietal', 'Occipital', 'Temporal']
~~~
{: .output}

# Indentations for structure
- In contrast to the closing statements common in Bash (such as fi) or MATLAB (such as end) Python uses indentations to understand the structure of your code.
- So you should make sure to use indentations correctly and consistently.
- This makes code more straightforward to read and ultimately understand 
- Indentations can be created using either tabs or spaces (usually four spaces) 
- If the indentations are mixed the code will fail to excute 

~~~python
print(brain_lobes[0])
    print(brain_lobes[0])
~~~

    
~~~
  File "<ipython-input-128-dc03b7fa51d4>", line 2
    print(brain_lobes[0])
    ^
IndentationError: unexpected indent
~~~
{: .error}



# Comments Are Marked by `#`

>"Code is more often read than written."
>> Guido van Rossum

- It is important to add comments to your Python code. 
- To do this use the # character, everything that comes after it won't be executed.

~~~python
print("This will run.")  # This won't run
~~~

>"Code tells you how; Comments tell you why."
>>Jeff Atwood (aka Coding Horror)

- Commenting your code serves multiple purposes, for example:
    - Planning and Reviewing, i.e. outline of the desired functionality of some future code
    - Code Description, i.e. explain the intent of specific sections of code
    - Algorithmic description, i.e. explain how the algorithm works or how it's implemented within your code or even add a link to the source
    - Tagging, i.e. label specific sections of your code where you need to take action, e.g. BUG, FIXME, TODO, UPGRADE.
- Comments should be short, sweet, and to the point.


# Use Multiline Comments 

- Multi-line comments can be either achieved primitively using multiple stacking of hashtags #

~~~python
# This 
# is 
# stacking 
~~~

- Alternatively, docstrings can be used by combining three commas 

~~~python
def some_function(arg1): 
    '''Summary line. some_function will do some thing with arg1
  
    Extended description of the function. 
    some_function will get arg1 and do things with it
    some of the things are complex, and some are simple
    some_function will then return some value.  
    
    Parameters: 
    arg1: the thing we will do stuff to 
  
    Returns: 
    Some value back 
    '"
~~~


# Python Keywords

- Keywords are the reserved words in Python.
- You cannot use a keyword as a variable name, function name or any other identifier. 
- These 35 keywords are used to define the syntax and structure of the Python language.
- To examine them you can run the following code 


~~~python
import keyword
print(keyword.kwlist)
~~~

~~~
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
~~~
{: .output}


# Case matters

- Python is case sensitive. 
- This means the **HELP** is not equal to **help**
- Most of Python keywords are written with lowercase letters.
- Notable exceptions to this rule are True and False boolean values and the **None** variable that all use a mixture of cases. 




# Variable Names

> *Code is read much more often than it is written*
>> Guido van Rossum 2001


1. Variable names should use lowercase.
1. Variable names cannot:
    - Start with a number
    - Contain spaces
    - Use any of these symbols : `'",<>/?|\()!@#$%^&*~-+`
1. Avoid using the characters:
    - 'l' (lowercase letter el)
    - 'O' (uppercase letter oh)
    - 'I' (uppercase letter eye)
1. short_names vs long_name
1. long_names should be separated using the underscore symbol (_)
1. This makes them readable 
1. Remember that making variable names simple to understand minimizes the time spent on commenting 


# Use blank lines

- Using blank lines is the simplest way to separate code blocks visually 
- Even multiple blank lines to distinguish between different parts of the code. 
- It won't affect the result of your script.


# Use white spaces 

- Python allows white spaces in assignment 
- This makes nicer looking code 



<!-- 
# Underscore `_` in Python

Python's underscore `_` is a unique character. It can be used for many different purposes.
During this week we will use some of these cases so for the sake of completeness


1. Stores the value of the last expression executed
1. Leaving out values in different situations (in practice, we just store them on a  temporary variable) -->


<!-- # Imports best practice 

We will go over this in detail next week, but it should be stated. 

- Use **import x** for importing packages and modules.
- Use **from x import y** where x is the package prefix, and y is the module name with no prefix.
- Use **from x import y as z** if two modules named y are to be imported or if y is an inconveniently long name.
- Use **import y as z** only when z is a standard abbreviation (e.g., np for NumPy). -->

## Links to expand your understanding 

For those interested in learning more...

- [PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/)  
- [PEP 257 -- Docstring Conventions](https://www.python.org/dev/peps/pep-0257/)  
- [The Zen of Python](https://www.python.org/dev/peps/pep-0020)  
- [PEP-8 Tutorial: Code Standards in Python](https://www.datacamp.com/community/tutorials/pep8-tutorial-python-code?)

{% include links.md %}

