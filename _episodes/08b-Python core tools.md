---
title: "Variables and Basic Data Types"
author: "Dr. Eyal Soreq" 
date: "01/06/2021"
teaching: 30
exercises: 20
questions:
- How can I store data in python?
- What types of Data can I store? 
- What is a variable in Python?
objectives:
- Cover the different core data types in python
- Learn about and how to use introspective functions
- Understand what variables are 
keypoints:
- So in this section we covered most of the basic data types Python has 
- We learned how to use data types using variables 
- We also covered how to combine them using various operators 
---

# Variables and Basic Data Types

A variable implies change and is a way of referring to some space in your computer memory that is allocated by your computer program to store a specific type of information. In other words, it is a symbolic name for a physical address in memory that contains static or dynamic values. Python supports many different Data Types, and in contrast to other programming languages where you need to specify the data type of a variable, python will automatically find out the data type at the process of allocation.


- None (aka null object or variable) 
- Boolean Type (True or False)
- Strings (strings in Python are arrays of bytes representing unicode characters)
- Integers $$\pm\mathbb{Z}$$
- Floats $$\pm\mathbb{R}$$
- Complex $$\pm\mathbb{C}$$

~~~python
my_none_variable = None 
my_bool_variable = True 
my_string_variable = 'STRING'
my_int_variable = 1
my_float_variable = 1.1
my_complex_variable = 1.1+1j
~~~

# Variables Naming Styles

1. lowercase/UPPERCASE
    - single letter - b/B
    - single name - var/VAR
    - lower_with_underscores/UPPER_WITH_UNDERSCORES
1. mixed cases
    - CamelCase - capitalize all the starting letters
    - mixedCase - initial lowercase character



# Introspective functions 

- Introspection is the ability to interrogate objects at runtime.
- Everything in python is an object. 
- Every object in Python may have attributes and methods. 
- By using introspection, we can dynamically examine python objects. 

~~~python
type(None) # This function returns the type of an object.
dir(None) # This function return list of methods and attributes associated with that object.
id(None) # This function returns a special id of an object representing a specific location in memory.
help(None) # This function is used to find what other functions do
print(None) # prints the specified message to the screen, or other standard output devices.
~~~


# Variables are just skins to a place in memory

- The id of a variable returns a unique integer representing the identity of an object
- This is also the address of the object in memory
- When you change the variable, you are creating a new object 


~~~python
some_var = None
print(id(some_var))
some_var = 'some different data'
print(id(some_var))
~~~

~~~
4305322280
4397182208
~~~
{: .output}


# Basic Data Types

We can use type to examine the different classes these variables are instances of 

~~~python
print(f'{type(my_none_variable)}')
print(f'{type(my_bool_variable)}')
print(f'{type(my_string_variable)}')
print(f'{type(my_int_variable)}')
print(f'{type(my_float_variable)}')
print(f'{type(my_complex_variable)}')
~~~

~~~
<class 'NoneType'>
<class 'bool'>
<class 'str'>
<class 'int'>
<class 'float'>
<class 'complex'>
~~~
{: .output}

# Immutable vs Mutable Objects

- In Python, there are two types of objects:
    - Immutable objects can't be changed
    - Mutable objects can be changed
    
- All the basic data types are immutable!!!  


# Basic Arithmetic operations on integers (whole numbers)

- As we already saw, Python has various "types" of numbers (numeric literals).
- It also has many different operators. 
- Arithmetic Operators perform various arithmetic calculations on these.
- Run these following examples in your own notebook:

~~~python
x,y = 5,4
print(f"+ Addition :\t{x}+{y}={x+y}") 
print(f"- Substraction :\t {x}-{y}={x-y}")
print(f"* Multiplication :\t {x}*{y}={x*y}")
print(f"/ Division :\t {x}/{y}={x/y}")
print(f"% Modulus :\t {x}%{y}={x%y}")
print(f"** Exponent :\t {x}^{y}={x**y}")
print(f"// Floor Division :\t {x}/{y}={x//y}")
print(f"() Use parentheses to specify order:\t {x}*({x}/{y}-{y})={x*(x/y-y)}")
~~~

> ## Output
> > ~~~
>>+ Addition :	5+4=9
>>- Substraction :	 5-4=1
>>* Multiplication :	 5*4=20
>>/ Division :	 5/4=1.25
>>% Modulus :	 5%4=1
>>** Exponent :	 5^4=625
>>// Floor Division :	 5/4=1
>>() Use parentheses to specify order:	 5*(5/4-4)=-13.75
> > ~~~
> > {: .output}
{: .solution}


# Basic Arithmetic operations on floats 

- Floating point numbers have a decimal point and/or use an exponential (e) to define the number.

~~~python
x,y,z = 5e-3,2e2,0.56e4
print(f"X={x},Y={y},Z={z}")
~~~

> ## Output
> > ~~~
> > X=0.005,Y=200.0,Z=5600.0
> > ~~~
> > {: .output}
{: .solution}


# Basic Arithmetic operations on complex numbers

- Python complex numbers are of type complex.
- Every complex number contains one real part and one imaginary part.

~~~python
x,y = 1+1j, 2-2j
print(f"Real Parts (x={x.real},y={y.real}) | Imaginary Parts = (x={x.imag},y={y.imag})") 
~~~

> ## Output
> > ~~~
> > Real Parts (x=1.0,y=2.0) | Imaginary Parts = (x=1.0,y=-2.0)
> > ~~~
> > {: .output}
{: .solution}

# Basic Arithmetic operations on strings (SAY WHAT!?)

- In general, you cannot perform mathematical operations on strings, even if the strings look like numbers.
- However, some arithmetic operators do work on strings and open up some nice options. Let's explore this. 

~~~python
x,y = 'cere','bellum'
print(f"+ Addition :                             {x}+{y}={x+y}") 
print(f"* Multiplication :                       {x}*{3}={x*3}") 
print(f"Combinations :                           {x}*{3}+{y}={x*3+y}")
print(f"() Use parentheses to specify order:     {x}+(({x}+{y})*{2})={x+((x+y)*2)}")
~~~

> ## Output
> > ~~~
> >+ Addition :                             cere+bellum=cerebellum
> >* Multiplication :                       cere*3=cerecerecere
> >Combinations :                           cere*3+bellum=cerecerecerebellum
> >() Use parentheses to specify order:     cere+((cere+bellum)*2)=cerecerebellumcerebellum
> > ~~~
> > {: .output}
{: .solution}


# Basic Numeric Comparison Operators

- Comparison operators are used to comparing two values

~~~python
x,y = 5,4
print(f" isEqual(==)          {x}=={y} is {x==y}")
print(f" notEqual(!=)         {x}!={y} is {x!=y}")
print(f" isGreater(>)         {x}>{y}  is {x>y}")
print(f" isSmaller(<)         {x}<{y}  is {x<y}")
print(f" isGreaterOrEqual(>=) {x}>={y} is {x>=y}")
print(f" isSmallerOrEqual(<=) {x}<={y} is {x<=y}")
~~~

> ## Output
> > ~~~
> > isEqual(==)          5==4 is False
> > notEqual(!=)         5!=4 is True
> > isGreater(>)         5>4  is True
> > isSmaller(<)         5<4  is False
> > isGreaterOrEqual(>=) 5>=4 is True
> > isSmallerOrEqual(<=) 5<=4 is False> > ~~~
> > {: .output}
{: .solution}


# Basic Numeric Assignment Operators

- Assignment operators are used to assigning values to variables

~~~python
y = 3
x = y ;print(f" x = y   \t| y is assigned to x\t| x={y}")
x = 19 ;print(f" x = y  \t| 17 is assigned to x\t| x={x}")
x += y ;print(f" x += y \t| y is added to x\t| x={x}")
x -= y ;print(f" x -= y \t| y subtracted from x\t| x={x}")
x *= y ;print(f" x *= y \t| x multiplied by y\t| x={x}")
x /= y ;print(f" x /= y \t| x divided by y\t| x={x}")
x %= y ;print(f" x %= y \t| x%y is assigned to x\t| x={x}")
x **= y;print(f" x **= y\t| x**y is Added to x\t| x={x}")
x //= y;print(f" x //= y\t| x//y is assigned to x\t| x={x}")
~~~

> ## Output
> > ~~~
> > x = y   	| y is assigned to x	| x=3
> > x = y  	| 17 is assigned to x	| x=19
> > x += y 	| y is added to x	| x=22
> > x -= y 	| y subtracted from x	| x=19
> > x *= y 	| x multiplied by y	| x=57
> > x /= y 	| x divided by y	| x=19.0
> > x %= y 	| x%y is assigned to x	| x=1.0
> > x **= y	| x**y is Added to x	| x=1.0
> > x //= y	| x//y is assigned to x	| x=0.0
> > {: .output}
{: .solution}


# Basic Logical Operators

- Logical operators in Python are used for conditional statements are true or false. 
- Logical operators in Python are **and**, **or** and **not**. 
- For logical operators, the following condition are applied.
- AND operator returns True if both the operands (right side and left side) are True
- OR operator returns True if either of the operand (right side or left side) is True
- NOT operator returns True if the operand is False

~~~python
x,y = True,False
print(f" When x is {x} and y is {y}")
print(f" {'='*35}")
print(f" x and y                 is {x and y}")
print(f" x or y                  is {x or y}")
print(f" not x and y             is {not x or y}")
print(f" x and not y             is {x or not y}")
print(f" {'~'*35}\n")
x,y = 10,20
print(f" When x is {x} and y is {y}")
print(f" {'='*35}")
print(f" x<y<y**2 and not y<x    is {x<y<y**2 and not y<x }")
~~~

> ## Output
> > ~~~
> > When x is True and y is False
> > ===================================
> > x and y                 is False
> > x or y                  is True
> > not x and y             is False
> > x and not y             is True
> > ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
> >
> > When x is 10 and y is 20
> > ===================================
> > x<y<y**2 and not y<x    is True
> > {: .output}
{: .solution}

# Basic Comparison operations on strings

~~~python
x,y = 'small','small'
print(f" isEqual(==)          {x}=={y}={x==y}")
print(f" notEqual(!=)         {x.upper()}!={y}={x.upper()!=y}")
x,y = 'small','SMALL'
print(f" {'='*40}")
print(f" isEqual(==)          {x}=={y}={x==y}") 
print(f" notEqual(!=)         {x}!={y.lower()}={x!=y.lower()}")
~~~

> ## Output
> > ~~~
> >isEqual(==)          small==small=True
> >notEqual(!=)         SMALL!=small=True
> >========================================
> >isEqual(==)          small==SMALL=False
> >notEqual(!=)         small!=small=False
> >~~~
> > {: .output}
{: .solution}


# Lets expand on strings 

- Every string in Python is an object containing a sequence of characters. 
- Each letter in a string has a distinct index corresponding to its specific order. 
- Indices start in 0 and end in the length of the string-1
- Spaces count as a character
- Both single and double quotes can be used to define a string

~~~python
a,b = 'test', "test"
print(f" Both tests are the same i.e. a={a} and b={b} and a==b is {a==b}") 
~~~

~~~
Both tests are the same i.e. a=test and b=test and a==b is True
~~~
{: .output}


> ## Why do we need both single `'` and double `"` quotes? 
> > 
- This simplifies using either single or double quotes within a phrase
- Consider the following code: 
> > ~~~python
some_phrash = "Did you know that 'cultivar' is synonymous with 'clone'?"
same_phrash = 'Did you know that "cultivar" is synonymous with "clone"?'
print(f"British style\t: {some_phrash}")
print(f"American style \t: {same_phrash}")
> > ~~~
> > ~~~
    British style    : Did you know that 'cultivar' is synonymous with 'clone'?
    American style     : Did you know that "cultivar" is synonymous with "clone"?
> > ~~~
> > {: .output}
{: .solution}


# What about using both?

What do we do when we want both single `'` and double `"` quotes in the same string? 
For example, try to print the following sentence using python 

>" 'The Green Hills of Earth' is one of my favourite stories," my teacher said.

> ## Solution 
> > 
- Luckily we have Escape Sequences in Python 
- An escape sequence is defined using a backslash (\\) followed by any protected word.
> > ~~~python
mixed_quote_phrash = '" \'The Green Hills of Earth\' is one of my favourite stories," my teacher said.'
print(f"We can escape the single: \n{mixed_quote_phrash}")
mixed_quote_phrash = "\" 'The Green Hills of Earth' is one of my favourite stories,\" my teacher said."
print(f"Or the double: \n{mixed_quote_phrash}")
> > ~~~
> > ~~~
We can escape the single: 
" 'The Green Hills of Earth' is one of my favourite stories," my teacher said.
Or the double: 
" 'The Green Hills of Earth' is one of my favourite stories," my teacher said.
> > ~~~
> > {: .output}
{: .solution}

# Escaping the Escape Sequences

- If we need to add a backslash, we will simply use a double \\\ 
- This will print out only one backslash

# useful Escape sequence characters (ESC)

| ESC | Description |
| :-- | :-- | 
| \\\ | Prints Backslash | 
| \\'  | Prints single-quote | 
| \\"  | Prints double quote |
| \\n  | Print line break | 
| \\t  | print tab | 
| \\uxxxx | Use 16-bit hex Unicode char | 
| \\Uxxxxxxxx | Use 32-bit hex Unicode char | 
| | |


# Everything in Python is an object

- String class is an object as well.
- Every time you create a string, it comes with many functions
- After initializing a string object, all the possible functions can be accessed using dot notation

~~~python
print((" This is center ").center(40,'~'))
print((" This is upper ").upper())
print((" and this is chaining of both ").upper().center(40,'~'))
print((" can be also useful ").title().center(40,'~'))
~~~

> ## Output
> > ~~~
~~~~~~~~~~~~ This is center ~~~~~~~~~~~~
    THIS IS UPPER 
~~~~~ AND THIS IS CHAINING OF BOTH ~~~~~
~~~~~~~~~~ Can Be Also Useful ~~~~~~~~~~
> > ~~~
> > {: .output}
{: .solution}


# More than style 

- By definition, we would expect string functions to be associated with style
- But there are also more general ones 
- The string count() method returns the number of occurrences of a substring in the given string.
- The find() method returns the index of the first occurrence of the substring (if found). If not found, it returns -1.


~~~python
print((" This is center ").count("is"))
print(("some_file_name.zip").endswith("zip"))
print(("some times we want to find where some word is").find("we"))
~~~

> ## Output
> > ~~~
2
True
11
> > ~~~
> > {: .output}
{: .solution}


# Let's focus on indexing for a moment 

- Every string is a sequence of characters 
- This is an excellent opportunity to cover how indexing works
- The len() function will count all of the string characters (including spaces and punctuation)

~~~python
some_string = "Some times we want to find how long is a string"
print(f'{some_string}  = {len(some_string)}')
~~~

> ## Output
> > ~~~
Some times we want to find how long is a string  = 47
> > ~~~
> > {: .output}
{: .solution}

# So how can we navigate this sequence? 

- To go to a specific index in a string, we use brackets \[\]
- Remember that indexing starts at 0 for Python
- Consider the following:

~~~python
print(f"Access start index using [0]\t\t\t= {some_string[0].upper()} \n\
Access end index using  [-1] \t\t\t= {some_string[-1].upper()} \n\
Use the colon [start:end] to perform slicing \t= {some_string[38:40].upper()} \n\
Get everything UPTO [:end] \t\t\t= {some_string[:4].upper()} \n\
Get everything FROM TO [start:end-2] \t\t= {some_string[38:-2].upper()}" )
~~~

> ## Output
> > ~~~
Access start index using [0]			        = S 
Access end index using  [-1] 			        = G 
Use the colon [start:end] to perform slicing 	= A 
Get everything UPTO [:end] 			            = SOME 
Get everything FROM TO [start:end-2] 		    = A STRI
> > ~~~
> > {: .output}
{: .solution}


# Slicing and skipping 

- It is possible to use index and slice notation to get a sequence using a step size

~~~python
print(f"Print everything [:]\t\t= {some_string[:].upper()} \n\
Print every second word [::2] \t= {some_string[::2].upper()} \n\
Everything in reverse [::-1]\t= {some_string[::-1].upper()}" )
~~~

> ## Output
> > ~~~
Print everything [:]		    = SOME TIMES WE WANT TO FIND HOW LONG IS A STRING 
Print every second word [::2] 	= SM IE EWN OFN O OGI  TIG 
Everything in reverse [::-1]	= GNIRTS A SI GNOL WOH DNIF OT TNAW EW SEMIT EMOS
> > ~~~
> > {: .output}
{: .solution}


# Strings are immutable

- Remember, immutable means that you cannot change the object itself
- This means that we cannot change a single letter in the string 
- If you run this, you will get an error 

~~~python
some_string[4]='a'
~~~

~~~
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-37-8856a305a25f> in <module>
----> 1 some_string[4]='a'

TypeError: 'str' object does not support item assignment
~~~
{: .error}


# We can also use split to break a long string

- The split() and rsplit() methods splits string from the left or right at the specified separator and returns a list of strings.

~~~python
print("some times we would like to split long text".split())
print("It,can,use any,kind of, delimiter".split(','))
print("You,can,also,define,how,many,splits".split(',',3))
print("As,well,as,direction,of,splits".rsplit(',',2))
~~~

> ## Output
> > ~~~
['some', 'times', 'we', 'would', 'like', 'to', 'split', 'long', 'text']
['It', 'can', 'use any', 'kind of', ' delimiter']
['You', 'can', 'also', 'define,how,many,splits']
['As,well,as,direction', 'of', 'splits']
> > ~~~
> > {: .output}
{: .solution}


# Strings can be concatenated 

- We already saw that we could combine different strings together 
- But this is not very easy to understand


~~~python
a,b,c,d = 'some','times', 'we', 'would'
print(a+b+d*2+c)
~~~
~~~
sometimeswouldwouldwe
~~~
{: .output}

- For those paying attention to the code, you can see that I am constantly combining strings with variables 
- This operation is called string formatting, and it is useful to know the different kinds it can be used 


# String Formatting

- From python 3.6 string formatting is done using f-strings, these simplify this process and make the code easier to understand  
- For those interested (and for completeness) [here is a link explaining the older methods](https://realpython.com/python-string-formatting/)


# f-strings examples

~~~python
some_str = "Malarkey"
print(f"Do you know what {some_str} means?\n") 
# using !r will keep the string
print(f"{some_str!r} refers to talk that is particularly foolish") 
~~~

> ## Output
> > ~~~
Do you know what Malarkey means?

'Malarkey' refers to talk that is particularly foolish
> > ~~~
> > {: .output}
{: .solution}


# f-strings Float formatting 

- Float formatting is used like this "result: {value:{total width in char}.{total number of digits}}"

~~~python
some_number = 45.35678
print(f"My models accuracy is:{some_number:{6}.{4}}")
~~~

> ## Output
> > ~~~
My model's accuracy is: 45.36
> > ~~~
> > {: .output}
{: .solution}


# f-strings zero padding

- Some times (more often then you would think) you need to have zeros padded numbers

~~~python
print(f'length = {5:07}')
~~~

> ## Output
> > ~~~
length = 0000005
> > ~~~
> > {: .output}
{: .solution}

# f-strings dates and time

- Dates are also simpler to define (however I am cheating here as I am using some Python package)

~~~python
from datetime import date
from datetime import time
some_date = date(year=2020, month=5, day=26)
some_time = time(hour=13, minute=30,second=10)
print(f"{some_date:%B %d, %Y} {some_time:%H:%M:%S}") 
~~~

> ## Output
> > ~~~
May 26, 2020 13:30:10
> > ~~~
> > {: .output}
{: .solution}


# f-string can do numeric notations

- We often would like to use different notations in different occasions


~~~python
some_number = 240

print(f"{some_number} in Hexadecimal is {some_number:x}") 
print(f"{some_number} in octal is {some_number:o}")
print(f"{some_number} in scientific is {some_number:e}") 
print(f"{some_number} in binary is {some_number:>08b}")
~~~

> ## Output
> > ~~~
240 in Hexadecimal is f0
240 in octal is 360
240 in scientific is 2.400000e+02
240 in binary is 11110000
> > ~~~
> > {: .output}
{: .solution}



## Links to expand your understanding 

For those interested in learning more...

- [realpython - Basic Data Types in Python](https://realpython.com/python-data-types/)
- [Variables and Types](https://www.learnpython.org/en/Variables_and_Types)
- [Python String Tutorial](https://www.datacamp.com/community/tutorials/python-string-tutorial)
- [Python For Data Science - A Cheat Sheet For Beginners](https://www.datacamp.com/community/tutorials/python-data-science-cheat-sheet-basics)

{% include links.md %}

