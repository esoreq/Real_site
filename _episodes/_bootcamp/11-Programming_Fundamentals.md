---
title: "Programming Fundamentals using Python"
author: "Dr. Eyal Soreq" 
date: "02/06/2021"
start: true
teaching: 35
exercises: 25
questions:
- What are conditional statements? 
- What are iterators? 
- What are loops?
- What are list comprehensions?
objectives:
- Learn about different conditional statements
- Learn how to use conditional statements 
- Learn how to create sequences using loops 
- Learn how to drive loops using iterators and iteratable objects
- Learn how to write list comprehensions
keypoints:
- Conditional statement allows us to take alternate actions based on a set of rules
- While loops are useful in situations where you want to complete an operation for an unknown amount of times and can form a conditional break statement
- For loops are useful in situations where you  want to complete an operation for a known amount of times driven by iteratable object
- The use of list comprehensions simplifies and compacts your code
- The use of iterators enables us to go over a sequence one element
- Any data structure can become iteratable using an iterator
---

# Programming Fundamentals

- In this section, we will go over the things that make programming so powerful 
- We will cover conditional statements 
- And finally, cover for and while loops 


# Conditional statements

- A conditional statement allows us to take alternate actions based on a set of rules
- In these types of procedures, `if`, `elif`, and `else` keywords are used.
- Using the "if" and "else" combinations, we can construct a rule tree to perform some logic  

~~~python
if rule1:
    do something
elif rule2:
    do something different
else: # if both are False
    do another thing
~~~

# Simple examples


~~~python
rule1 = True
if rule1:
    print(f'Rule 1 is {rule1}')
~~~

~~~
Rule 1 is True
~~~
{: .output}


> ## discussion
> If we change rule1 to *False*, what will happen?
{: .discussion}

# Add complexity

- Guess what the output will be without running the code

~~~python
rule1 = False    
if not rule1:
    print(f'Only if Rule 1 is {rule1} go here')
else: 
    print(f"Not Rule 1 is {not rule1}")
~~~

> ## Output
> > ~~~
Only if Rule 1 is False go here
> > ~~~
> > {: .output}
{: .solution}


# Multiple *if*, *elif* and *else* Branches example 

- Guess what the output will be without running the code
- Then try to change values to reach a specific branch

~~~python
rule1,rule2 = True,False    
if not rule1:
    print(f'Only if Rule 1 is {rule1} go here')
elif not rule2:
    print(f'Only if Rule 2 is {rule2} go here')
else: 
    print(f"Not Rule 1 is {not rule1}")
~~~


> ## Output
> > ~~~
Only if Rule 2 is False go here
> > ~~~
> > {: .output}
{: .solution}

# Nested *if* example (see Indentation!!!)

~~~python
var1, var2 = 'CRTX','FPN'

if var1 == 'CRTX':
    if var2 == 'FPN':
        print(f'The {var2} is part of the {var1}')
~~~


> ## Output
> > ~~~
The FPN is part of the CRTX
> > ~~~
> > {: .output}
{: .solution}

# Ternary operator

- Python supports ternary in a nice way 
- If you don't know what ternary operator and want to dive in the rabbit hole check this [link](https://en.wikipedia.org/wiki/%3F:) 
- However, for our cases, it is just a short form of conditional statements that takes the following form: 

```python
one_line = 'yes' if expression==True else 'no'
```

## Here's an example

~~~python
age = 13
teen = True if age>=13 and age <=18 else False
print(f'It is {teen} that you are a teen if you are {age}')
~~~
~~~
It is True that you are a teen if you are 13
~~~
{: .output}

# Conditional Loop *While*

- The idea of conditional statements can be combined to generate a statement that will repeat until the condition is no longer valid.
- The general syntax of a while loop is:

~~~python
while condition:
    do something until condition is False
else:
    do once and exit the loop
~~~

# Simple example

~~~python
counter = 20
while counter>0:
    print(f'{counter}',end='|')
    counter -= 1
~~~

> ## Output
> > ~~~
20|19|18|17|16|15|14|13|12|11|10|9|8|7|6|5|4|3|2|1|
> > ~~~
> > {: .output}
{: .solution}

# While loops are dangerous 
- Think what will happen if you type + instead of minus in the previous example
- Unless we add another condition, this loop will run forever 
- When this happens by mistake, you can always use the stop icon at the top to break the loop

## Lets add conditional fences

~~~python
counter = 30
while counter>0 and counter<50:
    print(f'{counter}',end='|')
    counter += 1
else: 
    print(f'\n\nDone !!')
~~~

> ## Output
> > ~~~
30|31|32|33|34|35|36|37|38|39|40|41|42|43|44|45|46|47|48|49|
Done !!
> > ~~~
> ## Try to guess the output here by comparing the following code
> > ~~~
counter = 30
while counter>0 and counter<=50:
    print(f'{counter}',end='|')
    counter += 1
else: 
    print(f'\n\nDone !!')
> > ~~~
{: .solution}


# We can adjust the loop internaly using *break*, *continue* and *pass* 

- We can use control statements in our loops to add additional functionality for various cases
- `Break` Breaks out of the current loop.
- `Continue` Goes to the top of current loop
- `Pass` do nothing 

# Why do we need a control statement that does nothing? 

- Python requires that code blocks (after if, except, def, class etc.) will not be empty.
- Empty code blocks are however useful in a variety of different contexts
- One main one is during implementation as a place holder to remember to deal with
- let's test this with some silly function 


~~~python
num = -5
while num<5:
    if not num % 2: # Even numbers are divided by 3
            print(f'f({num})={num/3:.3f}')
    elif num<0: # odd negative numberes become positive
        print(f'f({num})={(num**2)**.5:.3f}')
    else: # Otherwise, I still haven't decided 
        pass
    num+=1
~~~


> ## Output
> > ~~~
f(-5)=5.000
f(-4)=-1.333
f(-3)=3.000
f(-2)=-0.667
f(-1)=1.000
f(0)=0.000
f(2)=0.667
f(4)=1.333
> > ~~~
{: .solution}


# Challenge: Add a rule that is applied on the odd positive numbers

> ## Here is one possible solution
> > ~~~python
num = -5
while num<5:
    if not num % 2: # Even numbers are divided by 3
            print(f'f({num})={num/3:.3f}')
    elif num<0: # odd negative numberes become positive
        print(f'f({num})={(num**2)**.5:.3f}')
    else: # Otherwise, I still haven't decided 
        print(f'f({num})={(-num**3)**.5:.3f}')
    num+=1
> > ~~~
> ## Output
> > ~~~
f(-5)=5.000
f(-4)=-1.333
f(-3)=3.000
f(-2)=-0.667
f(-1)=1.000
f(0)=0.000
f(1)=0.000+1.000j
f(2)=0.667
f(3)=0.000+5.196j
f(4)=1.333
> > ~~~
> > {: .output}
{: .solution}



# Challenge: Change the code to go from -50 to 50 with steps of 10

> ## Here is one possible solution
> > ~~~python
start_condition = -50
stop_condition = 50
num = start_condition
steps = 10
while num<stop_condition:
    if not num % 20: # Even numbers are divided by 3
            print(f'f({num})={num/3:.3f}')
    elif num<0: # odd negative numberes become positive
        print(f'f({num})={(num**2)**.5:.3f}')
    else: # Otherwise, I still haven't decided 
        print(f'f({num})={(-num**3)**.5:.3f}')
    num+=steps
> > ~~~
> ## Output
> > ~~~
f(-50)=50.000
f(-40)=-13.333
f(-30)=30.000
f(-20)=-6.667
f(-10)=10.000
f(0)=0.000
f(10)=0.000+31.623j
f(20)=6.667
f(30)=0.000+164.317j
f(40)=13.333
> > ~~~
> > {: .output}
{: .solution}

# Use `range()` function to **generate** a sequence 

- The `range()` generates a sequence of numbers and is immutable 
- It takes one to three input arguments (i.e. start, stop and step)
- The stop is not included 
- [Click on this link to learn more about the range object](https://treyhunner.com/2018/02/python-range-is-not-an-iterator/#:~:text=Unlike%20zip%20%2C%20enumerate%20%2C%20or%20generator,range%20objects%20are%20not%20iterators.)


> ## Same concept using range
> > ~~~python
start = -50
stop = 50
step = 10
seq = range(start,stop,step)
index = 0
while index<len(seq):
    print(seq[index],end=',')
    index+=1
> > ~~~
> ## Output
> > ~~~
-50,-40,-30,-20,-10,0,10,20,30,40,
> > ~~~
> > {: .output}
{: .solution}

- But if we know in advance the sequence perhaps we don't need the condition

# Enter `for` loops using iterable objects

- A `for` loop goes through items that are in any iterable objects
- Iter-**able** objects are any data type that can be iterated over
- These include strings, lists, tuples, dictionaries, sets and range


## Same concept using `for` and `range`
~~~python
start,stop,step = -50,50,10
for number in range(start,stop,step):
    print(number,end=',')
~~~

~~~
-50,-40,-30,-20,-10,0,10,20,30,40,
~~~
{: .output}

# Iterators doing the hard work 

- Iter-**ators** are the agents that perform the iteration.
- An iterator is an object that allows us to go over a sequence one element at a time using the `iter()` function and the `next` method
- There is a big difference between an iterable object and an iterator derived from that object: the former has no memory, while the latter is like a stack -- with each use of it you have one fewer element in the stack

# An example will help illustrate this
~~~python
for i in range(3):
    for number in range(-50,50,10):
        print(number,end=',')
    print(f'- #{i} iter')   
~~~

~~~
-50,-40,-30,-20,-10,0,10,20,30,40,- #0 iter
-50,-40,-30,-20,-10,0,10,20,30,40,- #1 iter
-50,-40,-30,-20,-10,0,10,20,30,40,- #2 iter5
~~~
{: .output}

~~~python
range_iterator = iter(range(-50,50,10))
for i in range(3):
    for number in range_iterator:
        print(number,end=',')
    print(f'- #{i} iter')  
~~~

~~~
-50,-40,-30,-20,-10,0,10,20,30,40,- #0 iter
- #1 iter
- #2 iter
~~~
{: .output}

~~~python
for i in range(3):
    range_iterator = iter(range(-50,50,10))
    for number in range_iterator:
        print(number,end=',')
    print(f'- #{i} iter')  
~~~

~~~
-50,-40,-30,-20,-10,0,10,20,30,40,- #0 iter
-50,-40,-30,-20,-10,0,10,20,30,40,- #1 iter
-50,-40,-30,-20,-10,0,10,20,30,40,- #2 iter
~~~
{: .output}

# Using `enumerate()` function to keep index 
- enumerate is a function that returns an enumerate object that produces a sequence of tuples, and each of the tuples is an index-value pair.

~~~python
seq = range(5,15,2)
enumerated_seq = enumerate(seq)
list(enumerated_seq)
~~~

~~~
[(0, 5), (1, 7), (2, 9), (3, 11), (4, 13)]
~~~
{: .output}


> ## discussion
> Why do we need this? 
{: .discussion}


# lets answer with an example 

- Here we take a list of names and map out a possible abbreviation name pair 

~~~python
lobe_names = ['frontal','parietal','temporal', 'occipital','insula']
lobes_mapper = {}
for index,lobe in enumerate(lobe_names):
    lobes_mapper[index+1] = {'abbreviation':lobe[:3].upper(),'name':lobe}
lobes_mapper
~~~

~~~
{1: {'abbreviation': 'FRO', 'name': 'frontal'},
 2: {'abbreviation': 'PAR', 'name': 'parietal'},
 3: {'abbreviation': 'TEM', 'name': 'temporal'},
 4: {'abbreviation': 'OCC', 'name': 'occipital'},
 5: {'abbreviation': 'INS', 'name': 'insula'}}
~~~
{: .output}

### Let's unpack the whole thing

| Code | Explenation | Data structures  | 
| `lobe_names = ['frontal','parietal','temporal', 'occipital','insula']` | Assign list with strings to a variable | `list`, `variable` | 
| `lobes_mapper = {}` | Create an empty dictionary and assign it to a variable named lobes_mapper| `variable`,`dict` | 
| `for index,lobe in enumerate(lobe_names):` | Declare a for loop that iterates over all the elements in lobe_names using enumerate to construct an index value pair, and unpack that pair to the two variables  index and lobe | `variable`, `tuple`, `list` `iterator` |
| `lobes_mapper[index] = {'abbreviation':lobe[:3].upper(),'name':lobe}` | Create a dictionary with two keys and two values. In the first pair, we transform the first three letters into uppercase and assign them to the key abbreviation. The second pair simply adds the lobe name to the key. We can now assign this local dictionary to the lobes_mapper dictionary we created at the beginning, with the key being the current  index +1| `dict` | 
| `lobes_mapper` | print out the contents of the dict to the screen  | `dict` |



# What are list comprehensions?

- List comprehension is a way to define and create lists building on existing lists.
- The syntax is elegant `some_list = [expression for item in list]`
- Consider the following example:

~~~python
grid = []
for row in range(5):
    grid.append(list(range(5)))
grid    
~~~~

~~~
[[0, 1, 2, 3, 4],
[0, 1, 2, 3, 4],
[0, 1, 2, 3, 4],
[0, 1, 2, 3, 4],
[0, 1, 2, 3, 4]]
~~~
{: .output}


- Now compare it to this form: 

~~~python
[list(range(5)) for row in range(5)]
~~~~


# Nested List comprehensions rotated grid example 

- In the same way we can created hierarchy in for loops we can create nested lists

~~~python
grid_rot90 =[]
for col in range(5):
    tmp = []
    for row in grid:
        tmp.append(row[col])
    grid_rot90.append(tmp)   
grid_rot90  
~~~~

~~~
[[0, 0, 0, 0, 0],
 [1, 1, 1, 1, 1],
 [2, 2, 2, 2, 2],
 [3, 3, 3, 3, 3],
 [4, 4, 4, 4, 4]]
~~~
{: .output}

- Now compare it to this form: 

~~~python
[[row[col] for row in grid] for col in range(5)]
~~~~


# Using `zip()` to create complex combinations

- Zip creates an iterator of tuples, where each tuple contains the i-th element of each argument sequence or iterable. When the shortest input iterable is exhausted, the iterator stops. 

~~~python
num_list = list(range(1,7))
str_list  = list('string')
result = list(zip(num_list[::-1], str_list))
result
~~~

~~~
[(1, 's'), (2, 't'), (3, 'r'), (4, 'i'), (5, 'n'), (6, 'g')]
~~~
{: .output}

# In contrast to enumerate we are not limited to two lists 

~~~python
num_list = list(range(1,7))
str_list  = list('string')
result = list(zip(num_list[::-1], str_list,num_list))
result
~~~

~~~
[(6, 's', 1), (5, 't', 2), (4, 'r', 3), (3, 'i', 4), (2, 'n', 5), (1, 'g', 6)]
~~~
{: .output}


# Zip has the ability to unpack a list of tuples as well

~~~python
a1,a2,a3 = zip(*result)
print(a1)
print(a2)
print(a3)
~~~

~~~
(6, 5, 4, 3, 2, 1)
('s', 't', 'r', 'i', 'n', 'g')
(1, 2, 3, 4, 5, 6)
~~~
{: .output}

# Exercises for loops 

### E1.  Using steps of 46 and starting from 25 and ending with 163, print out a sequence of strings that begins with the word Week (e.g. Week_025, … , Week_163) and is on the same line seperated by commas.

~~~
Week_25, Week_71, Week_117, Week_163, 
~~~
{: .output}

> ## Here is one possible solution 
> > ## using while
> > ~~~python
index,seq = 0,range(25,190,46)
while True:
    if index<len(seq)-1:
        index+=1
        print(f'Week_{seq[index]}',end=', ')
    else:
        break   
> > ~~~
> > ## using for 
> > ~~~python
for num in range(25,190,46):
    print(f'Week_{num}',end=', ')
> > ~~~
> > ## using list comprehensions
> > ~~~python
_ = [print(f'Week_{num}',end=', ') for num in range(25,190,46)]    
> > ~~~
{: .solution}

### E2. For all the numbers from 1 to 15 (including) print if they are odd,(O) or even (E).

~~~
1-O,2-E,3-O,4-E,5-O,6-E,7-O,8-E,9-O,10-E,11-O,12-E,13-O,14-E,15-O,
~~~
{: .output}

> ## Here is one possible solution
> > ## using while
> > ~~~python
index,seq = 0,range(1,16)
while True:
    if index<len(seq):
        if seq[index]%2 == 0 : # if is number modulo 2 has no reminder it is even
            print(f'{seq[index]}-E',end=',')
        else:
            print(f'{seq[index]}-O',end=',')    
        index+=1    
    else:
        break   
> > ~~~
> > ## using for
> > ~~~python
for num in range(1,16):
    if num%2:
        print(f'{num}-O',end=',') 
    else:
        print(f'{num}-E',end=',')  
> > ~~~
> > ## using list comprehensions
> > ~~~python
print(",".join([f'{num}-{["E","O"][num%2]}' for num in range(1,16)]))
> > ~~~
{: .solution}


### E3. Using the following sequence `abcdEFGHjd0rG` print out if a single charecter is UPPER or lower case
  
~~~
a-l,b-l,c-l,d-l,E-U,F-U,G-U,H-U,j-l,d-l,0-l,r-l,G-U,
~~~
{: .output}

> ## Here is one possible solution
> > ## using while
> > ~~~python
index,seq = 0,'abcdEFGHjd0rG'
while len(seq)>index:
    char = seq[index]
    index += 1
    print(f'{char}-{["l","U"][char.isupper()]}',end=',')
> > ~~~
> > ## using for
> > ~~~python
for char in 'abcdEFGHjd0rG':
    print(f'{char}-{["l","U"][char.isupper()]}',end=',')
> > ~~~
> > ## using list comprehensions
> > ~~~python
print(",".join([f'{char}-{["l","U"][char.isupper()]}' for char in 'abcdEFGHjd0rG']))
> > ~~~
{: .solution}


### E4. Using one of the following quotes
    - "People say nothing is impossible, but I do nothing every day."
    - "The best thing about the future is that it comes one day at a time."
    - "The difference between stupidity and genius is that genius has its limits."
- And using a for loop print **on the same line** the same sentence with underscores instead of spaces    

~~~
The_best_thing_about_the_future_is_that_it_comes_one_day_at_a_time.
~~~
{: .output}


> ## Here is one possible solution
> > ## using while
> > ~~~python
index,seq = 0,list("The best thing about the future is that it comes one day at a time.")
while len(seq)>index:
    char = seq[index]
    if char.isspace():
        print(f'_',end='')
    else: 
        print(char,end='')    
    index += 1
> > ~~~
> > ## using for
> > ~~~python
for char in "The best thing about the future is that it comes one day at a time.":
    print(f'{[char,"_"][char.isspace()]}',end='')
> > ~~~
> > ## using list comprehensions
> > ~~~python
seq = "The best thing about the future is that it comes one day at a time."
print("".join([f'{[char,"_"][char.isspace()]}' for char in seq]))
> > ~~~
{: .solution}


### E5. Using the same quote print each word independently stacked

~~~
The
best
thing
about
the
future
is
that
it
comes
one
day
at
a
time.
~~~
{: .output}


> ## Here is one possible solution
> > ## using while
> > ~~~python
index,seq = 0,"The best thing about the future is that it comes one day at a time.".split()
while len(seq)>index:
    print(f'{seq[index]}')
    index += 1
> > ~~~
> > ## using for
> > ~~~python
for word in "The best thing about the future is that it comes one day at a time.".split():
    print(f'{word}')
> > ~~~
> > ## using list comprehensions
> > ~~~python
seq = "The best thing about the future is that it comes one day at a time."
[print(f'{word}') for word in seq.split()]
> > ~~~
{: .solution}


### E6. How would you create the multiplication matrix

~~~
[[1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20],
[3, 6, 9, 12, 15, 18, 21, 24, 27, 30],
[4, 8, 12, 16, 20, 24, 28, 32, 36, 40],
[5, 10, 15, 20, 25, 30, 35, 40, 45, 50],
[6, 12, 18, 24, 30, 36, 42, 48, 54, 60],
[7, 14, 21, 28, 35, 42, 49, 56, 63, 70],
[8, 16, 24, 32, 40, 48, 56, 64, 72, 80],
[9, 18, 27, 36, 45, 54, 63, 72, 81, 90],
[10, 20, 30, 40, 50, 60, 70, 80, 90, 100]]
~~~
{: .output}


> ## Here is one possible solution
> > ## using while
> > ~~~python
rows,cols=10,10
ir,ic = 1,1
prod_matrix = []
while rows>=ir:
    tmp = []
    while cols>=ic:
        tmp.append(ir*ic)
        ic += 1
    ir += 1
    ic = 1
    prod_matrix.append(tmp)  
> > ~~~
> > ## using for
> > ~~~python
prod_matrix = []
for row in range(1,11):
    tmp = []
    for col in range(1,11):
        tmp.append(row*col)
    prod_matrix.append(tmp)    
prod_matrix
> > ~~~
> > ## using list comprehensions
> > ~~~python
[[row*col for row in range(1,11)] for col in range(1,11)]
> > ~~~
{: .solution}

## Links to expand your understanding 

For those interested in learning more...

- [Python Range() Function](https://www.datacamp.com/community/tutorials/python-range-function)
- [Playing with iterators](https://campus.datacamp.com/courses/python-data-science-toolbox-part-2/using-iterators-in-pythonland)
- [Data Structures](https://docs.python.org/3/tutorial/datastructures.html)
- [list-comprehensions](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions)
- [Zip](https://docs.python.org/3/library/functions.html#zip)

{% include links.md %}