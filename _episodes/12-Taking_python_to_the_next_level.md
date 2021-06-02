---
title: "Taking python to the next level"
author: "Dr. Eyal Soreq" 
date: "02/06/2021"
teaching: 40
exercises: 20
questions:
- What are Functions?
- What are Classes?
- What are Methods?
- What are Modules? 
- What are Packages?
objectives:
- Learn how to write functions 
- Understand what a class is 
- Understand how to create a module 
- Learn how to load a local module 
- Learn how to install a packages
- Create a python_sandbox conda environment with a list of packages
keypoints:
- Functions can be used for many different tasks
- Lambda or anonymous functions are used to create inline trnasformations of data
- Built-in functions are native to python
- General purpose functions that are created to do something useful
- The two most important reasons that we use functions are *reusability* and *abstraction*
- You call a function, using it's name followed by parenthesis `()`
- A parameter is a variable name declared when the function is created
- A variable is only available from inside the region it is created. This is called scope.
- Arguments are the data you pass into the method's parameters
---

# What are Functions?
Python is full of functions: we've already encountered a variety of built-in functions that can be used for many different tasks. It is likely, however, that it will be necessary for you to write your own functions to deal with problems that your data presents.

Functions in Python fall into three types:
- Built-in functions (all the functions we have used so far are considered built-in)
- Lambda or anonymous functions are very similar to the mathematical definition above; they receive input and return it after applying some rule or expression. 
- General purpose functions that are created to do something useful.

# What are Functions good for?

The two most important reasons that we use functions are *reusability* and *abstraction*

 - Reusability: Once defined, a function can be used repeatedly. By reusing functions in your program, you can save time and effort.
- Abstraction. To use a particular function, you have to know its name, its function, the arguments you need to give it, and what results you will receive.
- Writing large programs that actually work is possible because of the ability to break them up into many abstract, reusable parts.

# Creating and Calling a Function

- In Python a function is defined using the def keyword:

~~~python
def my_first_function():
  print("Hello from my first function")
type(my_first_function)  
~~~

~~~
function
~~~
{: .output}

- You call a function, useing it's name followed by parenthesis

~~~python
my_first_function()
~~~

~~~
Hello from my first function
~~~
{: .output}


# Parameters, Arguments and Function scope

- A parameter is a variable name declared when the function is created.
- A variable is only available from inside the region it is created. This is called scope.
- Parameters are specified after the function name, inside the parentheses. 
- Arguments are the data you pass into the method's parameters
- You can add as many parameters as you want, just separate them with a comma.

- Consider the following example: 

~~~python
def my_second_function(first_name):
  print(f"Hello this function is {first_name} second function")
my_second_function('Eyal')  
~~~

~~~
Hello this function is Eyal's second function
~~~
{: .output}


- What will happen if we run our function like this?


~~~python
my_second_function() 
~~~

> ## Output
> > ~~~
TypeError: my_second_function() missing 1 required positional argument: 'first_name'
> > ~~~
> > {: .error}
{: .solution}

- When creating a function you declare what is the minimum amount of data the function requires in order to run
- By adding a default value, we can fix the above problem

~~~python
def my_second_function(first_name='Eyal'):
  print(f"Hello this function is {first_name} second function")
my_second_function()  
~~~

~~~
Hello this function is Eyal's second function
~~~
{: .output}

# Number of Arguments

- What will happen if we add another argument not declared in the function scope

~~~python
my_second_function('Eyal','Soreq') 
~~~

> ## Output
> > ~~~
TypeError: my_second_function() takes from 0 to 1 positional arguments but 2 were given
> > ~~~
> > {: .error}
{: .solution}


# Consider the following example: 

~~~python
last_name = 'Soreq'
def my_third_function(first_name):
    print(f"Hello this function is {first_name} {last_name} third function")
my_third_function('Eyal')  
~~~

> ## What do you think will happen?
> > ~~~
Hello this function is Eyal Soreq third function
> > ~~~
> > {: .output}
{: .solution}

- In Python, whenever a function is called, a dictionary of name-value pairs is searched for arguments needed. The process begins with the local scope, moves to the enclosing scope, then moves to the global scope, and ends with the built-in scope. If the  variable name cannot be found, an error will be returned

# In this example, last_name is explicitly deleted

~~~python
del last_name
def my_third_function(first_name):
    print(f"Hello this function is {first_name} {last_name} third function")
my_third_function('Eyal')  
~~~

> ## What do you think will happen now?
> > ~~~
NameError: name 'last_name' is not defined
> > ~~~
> > {: .error}
{: .solution}


~~~python
def my_fourth_function(first_name='Eyal',last_name='Soreq'):
    print(f"Hello this function is {first_name} {last_name} fourth function")
my_fourth_function()
~~~


> ## What do you think will happen now?
> > ~~~
Hello this function is Eyal Soreq fourth function
> > ~~~
> > {: .output}
{: .solution}


# Adding docstrings to functions to help you


~~~python
help(my_fourth_function)
~~~

~~~
Help on function my_fourth_function in module __main__:

my_fourth_function(first_name='Eyal', last_name='Soreq')
~~~
{: .output}


~~~python
def my_fourth_function(first_name='Eyal',last_name='Soreq'):
    """Prints "Hello from function".

    Returns:
        None
    """
    print(f"Hello this function is {first_name} {last_name} fourth function")
help(my_fourth_function)
~~~

~~~
Help on function my_fourth_function in module __main__:

my_fourth_function(first_name='Eyal', last_name='Soreq')
    Prints "Hello from function".
    
    Returns:
        None
~~~
{: .output}

# What is the map function

- The map function allows you to "map" a function to an iterable object. 
- in other words, we call the same function for every item in an iterable, such as a list. 
- For example, the function below is used to convert numeric age to a categorical age_group?




~~~python
def age_group(age):
    if age<=11:
        return 'children'
    elif age<=21:
        return 'teens'
    elif age<=65:
        return 'adults'
    else: 
        return 'elderly'
print(list(map(age_group,  list(range(1,90,3)))))
~~~


> ## Output
> > ~~~
['children', 'children', 'children', 'children', 'teens', 'teens', 'teens', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'elderly', 'elderly', 'elderly', 'elderly', 'elderly', 'elderly', 'elderly', 'elderly']
> > ~~~
{: .solution}


# what about multiple iterables?

- Map() can accept more than one iterable. 
- However, the iterables should be the same length
- If they are not, the shortest iterable will terminate the function



~~~python
def list2grid(s,e):
    return list(range(s,e))
grid = list(map(list2grid,  list(range(1,10)),list(range(2,30,3))))
grid
~~~

> ## Output
> > ~~~
[[1],
[2, 3, 4],
[3, 4, 5, 6, 7],
[4, 5, 6, 7, 8, 9, 10],
[5, 6, 7, 8, 9, 10, 11, 12, 13],
[6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16],
[7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19],
[8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22],
[9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25]]
> > ~~~
{: .solution}



# filter function

- The filter function creates an iterator containing only items for which a function(item) is true. 
- In other words, similar to map() you combine a function with a list.
- The list is then filtered returning only **True** results.


```python
def is_children(age_group):
    return age_group == 'children'
print(list(filter(is_children, age_group)))
```
```
['children', 'children', 'children', 'children']
```



# What are Lambda functions?

#### Lambda functions are anonymous functions in Python or functions with no name. It's a small and restricted function with only one  line. As with normal functions, Lambda functions can take more than one argument.

#### Python anonymous functions have three  parts:
1. The lambda keyword.
1. The parameters (or bound variables), and
1. The function body.


#### Syntax

`lambda arguments : expression`

## Try recreating the following output with a lambda function, the following expression, and list comprehension: 

$$ f(x) = x^3 + x^2 - x $$

~~~
'0,1,10,33,76,145,246,385,568,801,1090,1441,1860,2353,2926,3585,4336,5185,6138,7201'
~~~
{: .output}

> ## Here is one possible solution
> > ~~~python
f = lambda x: x**3 + x**2 - x
",".join([str(f(x)) for x in range(20)])
> > ~~~
{: .solution}


# Why are Lambda Expressions useful?

- A lambda function is used for creating small, one-time, anonymous function object in Python. 
- Because a lambda function is an expression, it can be named. 
- Multi-arguments are expressed by separating arguments with a comma (,)
- However, Lambda expressions are rarely named - these are just to make a point



### Here are some more examples 

~~~python
square = lambda x: x**2
product = lambda x,y: x*y
power = lambda x,y: x**y
~~~



# Using if else in Lambda function

- Using if-else in lambda function is little tricky, the syntax is as follows 
- if you shouted Ternary Operators pat yourself on the back


~~~python
lambda <arguments> : <Value if True> if <condition> else <Value if False>
~~~

# Consider our previous map example and compare it with this compact version

~~~python
age2group = lambda age: 'children' if age<=11 else 'teens' if age<=21 else 'adults' if age<=65 else 'elderly'
print(list(map(age2group,  list(range(1,30,1)))))
~~~


> ## Output
> > ~~~
['children', 'children', 'children', 'children', 'children', 'children', 'children', 'children', 'children', 'children', 'children', 'teens', 'teens', 'teens', 'teens', 'teens', 'teens', 'teens', 'teens', 'teens', 'teens', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults', 'adults']
> > ~~~
{: .solution}





# Python Classes and Methods

In Python, most code is implemented with a special construct called a class, which is one of the core features of object-oriented programming. Classes are used by programmers to group related items together. Classes allow us to combine methods and attributes which share a common purpose.

You create a class in Python by typing `class`.

`Instance = class(arguments)`


# How to create a class

The simplest class can be created using the class keyword. For example, let's create a simple, empty class with no functionalities.

~~~python
class My_first_class:
    name = 'my name attribute'

instance_of_mfc = My_first_class()
instance_of_mfc.name
~~~


~~~
'my name attribute'
~~~
{: .output}

# Methods

- As soon as the class has attributes, you can define functions to access the class attributes. 
- Methods are what these functions are called. 
- Methods are defined with a self keyword as the first argument.

~~~python
class My_first_class:
    name = 'my name attribute'
    
    def change_name(self, new_name): 
        self.name = new_name

mfc = My_first_class()
mfc.change_name('my new name attribute')
mfc.name
~~~

~~~
'my new name attribute'
~~~
{: .output}

# Instance attributes in python and the init method


~~~python
class My_first_class:

    def __init__(self, name):
        self.name = name
    
    def change_name(self, new_name): 
        self.name = new_name

mfc = My_first_class('my init name attribute')
mfc.name
~~~

~~~
'my init name attribute'
~~~
{: .output}


- We can define default values just like in functions
- And we can have as many instances as we like


~~~python
class My_first_class:

    def __init__(self, name='1st class',id=0):
        self.name = name
        self.id = id
    
    def change_name(self, new_name): 
        self.name = new_name

mfc_0 = My_first_class()
mfc_1 = My_first_class('my init name attribute',3)
print(f"mfc_0 name is {mfc_0.name} and it's id is {mfc_0.id}")
print(f"mfc_1 name is {mfc_1.name} and it's id is {mfc_1.id}") 
~~~

~~~
mfc_0 name is 1st class and it's id is 0
mfc_1 name is my init name attribute and it's id is 3
~~~
{: .output}


# This answers the question raised in the feedback 
 > "*For example, in Matlab you usually put the function first and then parameters/variables etc in backets. like 'Sort(variable)'. But in python, you sometimes use the "dot notation" like 'variable.sort', but also print(...variable...). What is the underlying rationale here? These are the little things that we sometimes skip ...*"

 - The distinction between the two different perspectives relate to data structures and internal methods
 - In the first case we pass a variable into some function and apply some logic on it 

 ~~~python
 some_list = list(range(1,99))
 some_generator = lambda X: [(263*x+71%100)%100 for x in X]
 some_generator(some_list)
 ~~~


 - In the second we have some internal method that was designed to provide some functionality 

~~~python
import random

class Some_generator:

    def __init__(self,seq,seed=263):
        random.seed(seed)
        self.seq = list(seq)
        self.seed = seed

    def __repr__(self):
        return f"<sequence {self.__str__()}>"

    def __str__(self):
        return ",".join([str(x) for x in self.seq])

    def scramble(self):
        random.shuffle(self.seq)
        return self
~~~

~~~python
rand_seq = Some_generator(range(10))
rand_seq.scramble() # everytime we call scramble we shuffle the list
~~~

~~~python
rand_seq = Some_generator('everytime we call scramble we shuffle the list')
"".join(rand_seq.scramble().seq) # This is not limited to numbers can use any iterable for example letters 
~~~

~~~python
rand_seq = Some_generator('everytime we call scramble we shuffle the list'.split())
" ".join(rand_seq.scramble().seq) # Or words
~~~

## Links to expand your understanding 

For those interested in learning more...

- [python-scope-legb-rule](https://realpython.com/python-scope-legb-rule/)
- [lambda-expressions](https://docs.python.org/3/tutorial/controlflow.html?highlight=lambda#lambda-expressions)
- [filter](https://docs.python.org/3/library/functions.html#filter) 
- [writing-functions-in-python](https://learn.datacamp.com/courses/writing-functions-in-python)

{% include links.md %}