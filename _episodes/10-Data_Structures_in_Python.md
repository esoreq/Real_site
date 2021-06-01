---
title: "Data structures in Python"
author: "Dr. Eyal Soreq" 
date: "01/06/2021"
teaching: 30
exercises: 20
questions:
- What are Data structures?
- What types of data structures are there?
- How and when to use the different data structures?

objectives:
- Understand the differences between Python's data structures
- Learn how to create and use different data structures
- Understand the limitations of each data structures

keypoints:
- Lists are the basic sequence building block in Python.
- Tuples are immutable lists 
- Sets are a stack of unique data types
- A dictionary key is unique
- Items in dictionaries consist of key and value pairs
---

# What are Data structures?

Data structures organize and store data so that it's easy to access and use. The data and the operations on the data are defined by them. In data science and computer science, there are a variety of different data structures that make it easy for the researchers and engineers to concentrate on the basics and not get lost in the details of data description or access.

In fact all the Basic Data Types we just covered are considered Primitive Data Structures
The non-primitive types are the more sophisticated data structures. Instead of just storing one value, they store a whole bunch of them.

# What are Lists?
- Lists are the basic sequence building block in Python.
- They are mutable, therefore lists elements can be changed!
- Lists are constructed with brackets \[\]
- Every element in the list is separated by commas

# Constructing lists

- Lists can hold any basic data type
- They can also hold mixed types

~~~python
empty_list = []
print(empty_list)
some_list = ['frontal', 'parietal', 'temporal', 'occipital']
print(some_list)
another_list = [1, 2, 3, 4]
print(another_list)
mixed_list = ['frontal', 2.1, 0.112e-2, 2-2j,True,'a']
print(mixed_list)
~~~

> ## Output
> > ~~~
[]
['frontal', 'parietal', 'temporal', 'occipital']
[1, 2, 3, 4]
['frontal', 2.1, 0.00112, (2-2j), True, 'a']
> > ~~~
> > {: .output}
{: .solution}


# lists have length

~~~python
print(f"some_list length is \t:{len(some_list)}")
print(f"another_list length is \t:{len(another_list)}")
print(f"mixed_list length is \t:{len(mixed_list)}")  
~~~

> ## Output
> > ~~~
some_list length is 	:4
another_list length is 	:4
mixed_list length is 	:6
> > ~~~
> > {: .output}
{: .solution}


# lists have indices

- Indexing and slicing works just like in strings 

~~~python
print(f"Access start index using [0]\t\t\t= {mixed_list[0]} \n\
Access end index using  [-1] \t\t\t= {mixed_list[-1]} \n\
Use the colon [start:end] to perform slicing \t= {mixed_list[1:3]} \n\
Get everything UPTO [:end] \t\t\t= {mixed_list[:4]} \n\
Get everything FROM [start:] \t\t\t= {mixed_list[3:]} " )
print(f"Get everything [:]\t\t= {mixed_list[:]} \n\
Get every second element [::2] \t= {mixed_list[::2]} \n\
Get list in reverse [::-1]\t= {mixed_list[::-1]}" )
~~~

> ## Output
> > ~~~
Access start index using [0]			        = frontal 
Access end index using  [-1] 			        = a 
Use the colon [start:end] to perform slicing 	= [2.1, 0.00112] 
Get everything UPTO [:end] 			            = ['frontal', 2.1, 0.00112, (2-2j)] 
Get everything FROM [start:] 			        = [(2-2j), True, 'a'] 
Get everything [:]				                = ['frontal', 2.1, 0.00112, (2-2j), True, 'a'] 
Get every second element [::2] 			        = ['frontal', 0.00112, True] 
Get list in reverse [::-1]			             = ['a', True, (2-2j), 0.00112, 2.1, 'frontal']
> > ~~~
> > {: .output}
{: .solution}


# lists can be also be concatenated

- You can combine two lists together 
- And you can multiply lists using integers

~~~python
print(f"some_list + mixed_list length is \t:{len(some_list+mixed_list)}")
print(some_list*2)
~~~

> ## Output
> > ~~~
some_list + mixed_list length is 	:10
['frontal', 'parietal', 'temporal', 'occipital', 'frontal', 'parietal', 'temporal', 'occipital']
> > ~~~
> > {: .output}
{: .solution}


# lists can be generated 


~~~python
letter_list = list('frontal')
print(f"Int lists can be created using range\t:{list(range(5))}")
print(f"This is quite flexible \t\t\t:{list(range(45,49))}")
print(f"And allows even steps \t\t\t:{list(range(56,69,3))}")
print(f"Also in reverse \t\t\t:{list(range(-56,-69,-3))}")
print(f"String can create Letters lists \t:{letter_list}")
~~~

> ## Output
> > ~~~
Int lists can be created using range	:[0, 1, 2, 3, 4]
This is quite flexible 			        :[45, 46, 47, 48]
And allows even steps 			        :[56, 59, 62, 65, 68]
Also in reverse 			            :[-56, -59, -62, -65, -68]
String can create Letters lists 	    :['f', 'r', 'o', 'n', 't', 'a', 'l']
> > ~~~
> > {: .output}
{: .solution}

# Items can be Appended or Inserted to lists

~~~python
letter_list = list('frontal')
letter_list.insert(5, 'o');
print(f"Insert a number at index\t:{letter_list}")
letter_list.pop(6);letter_list.pop(-1)
print(f"remove a letter at index\t:{letter_list}")
letter_list.extend('parietal')
print(f"remove a letter at index\t:{letter_list}")
~~~

> ## Output
> > ~~~
    Insert a number at index    :['f', 'r', 'o', 'n', 't', 'o', 'a', 'l']
    remove a letter at index    :['f', 'r', 'o', 'n', 't', 'o']
    remove a letter at index    :['f', 'r', 'o', 'n', 't', 'o', 'p', 'a', 'r', 'i', 'e', 't', 'a', 'l']
> > ~~~
> > {: .output}
{: .solution}


# lists can be sorted or reversed

~~~python
letter_list.reverse()
print(f"In both directions\t:{letter_list}")
letter_list.sort()
print(f"lists can be sorted\t:{letter_list}")
letter_list.sort(reverse=True)
print(f"In both directions\t:{letter_list}")
~~~

> ## Output
> > ~~~
    In both directions    :['l', 'a', 't', 'e', 'i', 'r', 'a', 'p', 'o', 't', 'n', 'o', 'r', 'f']
    lists can be sorted    :['a', 'a', 'e', 'f', 'i', 'l', 'n', 'o', 'o', 'p', 'r', 'r', 't', 't']
    In both directions    :['t', 't', 'r', 'r', 'p', 'o', 'o', 'n', 'l', 'i', 'f', 'e', 'a', 'a']
> > ~~~
> > {: .output}
{: .solution}


# lists items can be removed, changed, added, inserted and extended 

~~~python
letter_list = list('frontal')
letter_list[2:-1] = []
print(f"We can remove everything from index 2 till -1 :{letter_list}")
letter_list[2] = 'T'
print(f"We can change an item if it exists \t:{letter_list}")
letter_list.append('R') 
print(f"We can also add an item to the end \t:{letter_list}")
letter_list.insert(2,'B') 
print(f"We can insert and item before an item \t:{letter_list}")
letter_list.extend(some_list[::-1]) 
print(f"Or extend the list with another one \t:{letter_list}")
~~~

> ## Output
> > ~~~
We can remove everything from index 2 till -1 :['f', 'r', 'l']
We can change an item if it exists 	:['f', 'r', 'T']
We can also add an item to the end 	:['f', 'r', 'T', 'R']
We can insert and item before an item 	:['f', 'r', 'B', 'T', 'R']
Or extend the list with another one 	:['f', 'r', 'B', 'T', 'R', 'occipital', 'temporal', 'parietal', 'frontal']
> > ~~~
> > {: .output}
{: .solution}

# Tuples

- In mathematics, a tuple is a finite ordered list of elements
- And in Python tuples can be viewed as immutable lists 
- In other words, once a tuple is constructed its elements can't change


# Creating Tuples

- Use parentheses () to construct an empty tuple
- And place items separated by commas to fill it

~~~python
empty_tuple = ()
print(empty_tuple)
some_tuple = ('frontal', 'parietal', 'temporal', 'occipital')
print(some_tuple)
another_tuple = (1, 2, 3, 4)
print(another_tuple)
mixed_tuple = ('frontal', 2.1, 0.112e-2, 2-2j,True,'a','a','c')
print(mixed_tuple)
~~~

> ## Output
> > ~~~
()
('frontal', 'parietal', 'temporal', 'occipital')
(1, 2, 3, 4)
('frontal', 2.1, 0.00112, (2-2j), True, 'a', 'a', 'c')
> > ~~~
> > {: .output}
{: .solution}


# Tuples also have a length

~~~python
print(f"some_tuple length is \t:{len(some_tuple)}")
print(f"another_tuple length is \t:{len(another_tuple)}")
print(f"mixed_tuple length is \t:{len(mixed_tuple)}")  
~~~

> ## Output
> > ~~~
some_tuple length is 	    :4
another_tuple length is 	:4
mixed_tuple length is 	    :8
> > ~~~
> > {: .output}
{: .solution}

# And we can index the tuple exactly like a list

~~~python
print(f"Access start index using [0]\t\t\t= {mixed_tuple[0]} \n\
Access end index using  [-1] \t\t\t= {mixed_tuple[-1]} \n\
Use the colon [start:end] to perform slicing \t= {mixed_tuple[1:3]} \n\
Get everything UPTO [:end] \t\t\t= {mixed_tuple[:4]} \n\
Get everything FROM [start:] \t\t\t= {mixed_tuple[3:]} \n\
Get everything [:]\t\t\t\t= {mixed_tuple[:]} \n\
Get every second element [::2] \t\t\t= {mixed_tuple[::2]} \n\
Get tuple in reverse [::-1]\t\t\t= {mixed_tuple[::-1]}" )
~~~

> ## Output
> > ~~~
Access start index using [0]			= frontal 
Access end index using  [-1] 			= c 
Use the colon [start:end] to perform slicing 	= (2.1, 0.00112) 
Get everything UPTO [:end] 			= ('frontal', 2.1, 0.00112, (2-2j)) 
Get everything FROM [start:] 			= ((2-2j), True, 'a', 'a', 'c') 
Get everything [:]				= ('frontal', 2.1, 0.00112, (2-2j), True, 'a', 'a', 'c') 
Get every second element [::2] 			= ('frontal', 0.00112, True, 'a') 
Get tuple in reverse [::-1]			= ('c', 'a', 'a', True, (2-2j), 0.00112, 2.1, 'frontal')
> > ~~~
> > {: .output}
{: .solution}

# However tuple has only two basic Methods

- Use .index to get the index that matches the first occurrence of an item
- Use .count to get the number of items in a tuple
- What happens if a match isn't found?

~~~python
print(f"Where is 'a'? \t\tindex= {mixed_tuple.index('a')}")
print(f"How many 'a's? \t\tindex= {mixed_tuple.count('a')}")
print(f"Where is 'a'? \t\tindex= {mixed_tuple.index('l')}")
~~~

> ## Output
> > ~~~
Where is 'a'? 		index= 5
How many 'a's? 		index= 2
> > ~~~
> > {: .output}
> > ~~~
ValueError: tuple.index(x): x not in tuple
> > ~~~
> > {: .error}
{: .solution}

# We can combine tuples 

~~~python
combined_tuple = some_tuple + mixed_tuple
print(f"How many items are in combined_tuple \tn= {len(combined_tuple)}")
print(f"{combined_tuple}")
multiplied_tuple =some_tuple*2 
print(f"How many items are in multiplied_tuple \tn= {len(multiplied_tuple)}")
print(f"{multiplied_tuple}")
~~~

> ## Output
> > ~~~
How many items are in combined_tuple 	n= 12
('frontal', 'parietal', 'temporal', 'occipital', 'frontal', 2.1, 0.00112, (2-2j), True, 'a', 'a', 'c')
How many items are in multiplied_tuple 	n= 8
('frontal', 'parietal', 'temporal', 'occipital', 'frontal', 'parietal', 'temporal', 'occipital')
> > ~~~
> > {: .output}
{: .solution}


# What we can't do is change items 

- Tuples are immutable!!! (just like strings)

~~~python
mixed_tuple[2]= 'a'
mixed_tuple[2]=[] 
~~~

~~~
TypeError: 'tuple' object does not support item assignment
~~~
{: .error}


# What are Dictionaries?

- A dictionary is a data structure that maps keys to values
- Dictionaries are unordered (i.e. no index)
- Dictionaries rely on a data structure called hash tables
- If you don't know what a [hash table](https://www.data-structures-in-practice.com/hash-tables/) and you are dying to find out 

# Important things about Dictionaries

- Each item in a dictionary has a key and a value
- The key acts as the value index, so no two values can have the same key (i.e. keys are unique).
- Keys must also be hashable (i.e. can be used as a key by a hash table)
- Any built-in immutable data type is hashable 
- immutable data types are int, float, complex, bool, str, tuple, Unicode and even None

# Creating a dictionary

- We create an empty dictionary using braces {}
- We can use any valid key
- And we can use any kind of data as a value
- If we use the same key twice the last value counts

~~~python
empty_dict = {}
some_dict = {"SBC":"subcortical","DMN":"default mode network","ECN":"executive control", "ATT":"attentional"}
mixed_dict = {1:{"SBC":"subcortical"},2:["DMN","default mode network"], 3:("ECN","executive control"),3:{"MD":"Multiple demands"}}
print(mixed_dict)
~~~

> ## Output
> > ~~~
{1: {'MD': 'Multiple demands'}, 2: ['DMN', 'default mode network'], 3: ('ECN', 'executive control')}
> > ~~~
> > {: .output}
{: .solution}


# nesting Dictionaries
- Hierarchies can be nested in complex ways
- And extract their values if we know how 

~~~python
nested_dict = {"1":{"1.1":{"1.1.1":"Tada!!!"}}}
nested_dict["1"]["1.1"]["1.1.1"]
~~~

> ## Output
> > ~~~
'Tada!!!'
> > ~~~
> > {: .output}
{: .solution}

# And as you guessed Dictionaries have some basic methods

~~~python
lobes = {1:'frontal', 2:'parietal', 3:'temporal', 4:'occipital',5:'insula'}
print(f"lobes keys :{lobes.keys()}") 
print(f"lobes values :{lobes.values()}") 
print(f"lobes items :{lobes.items()}")
print(f"lobes length :{len(lobes)}")
~~~

> ## Output
> > ~~~
lobes keys :dict_keys([1, 2, 3, 4, 5])
lobes values :dict_values(['frontal', 'parietal', 'temporal', 'occipital', 'insula'])
lobes items :dict_items([(1, 'frontal'), (2, 'parietal'), (3, 'temporal'), (4, 'occipital'), (5, 'insula')])
lobes length :5
> > ~~~
> > {: .output}
{: .solution}

# Assigning an existing dictionary to a variable passes a reference

- That means that changes in either the source or the target variable will affect both
- To break this chain, we use the copy function 

~~~python
lobes_reference = lobes # assign the existing dict to a new variable
lobes_reference[1] = 'Changed on new'
lobes[3] = 'Changed on old'
print(f'old dict = {lobes}')
print(f'new dict = {lobes_reference}')
~~~

> ## Output
> > ~~~
old dict = {1: 'Changed on new', 2: 'parietal', 3: 'Changed on old', 4: 'occipital', 5: 'insula'}
new dict = {1: 'Changed on new', 2: 'parietal', 3: 'Changed on old', 4: 'occipital', 5: 'insula'}
> > ~~~
> > {: .output}
{: .solution}

- To break this chain, we use the copy function 

~~~python
lobes = {1:'frontal', 2:'parietal', 3:'temporal', 4:'occipital',5:'insula'}
lobes_reference = lobes.copy() # copy the existing dict to a new variable
lobes_reference[1] = 'Changed on new'
lobes[3] = 'Changed on old'
print(f'old dict = {lobes}')
print(f'new dict = {lobes_reference}')
~~~

> ## Output
> > ~~~
old dict = {1: 'frontal', 2: 'parietal', 3: 'Changed on old', 4: 'occipital', 5: 'insula'}
new dict = {1: 'Changed on new', 2: 'parietal', 3: 'temporal', 4: 'occipital', 5: 'insula'}
> > ~~~
> > {: .output}
{: .solution}

- We can update items in a dictionary using another dictionary


~~~python
lobes = {1:'frontal', 2:'parietal', 3:'temporal', 4:'occipital',5:'insula'}
lobes.update({6:'subcortical',7:'brainstem'})
lobes
~~~

> ## Output
> > ~~~
{1: 'frontal',
 2: 'parietal',
 3: 'temporal',
 4: 'occipital',
 5: 'insula',
 6: 'subcortical',
 7: 'brainstem'}
> > ~~~
> > {: .output}
{: .solution}

- Or we can just add one item at a time 

~~~python
lobes[8] = 'cerebellum'
lobes
~~~

> ## Output
> > ~~~
{1: 'frontal',
 2: 'parietal',
 3: 'temporal',
 4: 'occipital',
 5: 'insula',
 6: 'subcortical',
 7: 'brainstem',
 8: 'cerebellum'}
> > ~~~
> > {: .output}
{: .solution}

# Sets

- Sets are a special data structure that holds **unique** unordered elements
- In a way, sets are similar to keys in the dictionary 
- Unsurprisingly, sets can only take hashable data types
- Sets can be extremely powerful if used right

# What are sets used for 

- The list is endless,
- From our narrow perspective, we will use them in the context of set theory
    - This means finding intersections between sets
    - Getting the union of several sets 
    - Or even the differences of several sets 


# creating sets 

- Sets can be created using a list 

~~~python
empty_set = set()
print(f'This is an empty {type(empty_set)}')
some_set = {'frontal', 'parietal', 'temporal', 'occipital'}
print(f'This is also a set {type(some_set)}')
another_set = set([1, 2, 3, 4])
print(f'We can use lists as constructor for sets {type(another_set)}')
mixed_set = set(['frontal', 2,'c'])
print(f'And we can used mixed sets {type(mixed_set)}')
~~~

> ## Output
> > ~~~
This is an empty <class 'set'>
This is also a set <class 'set'>
We can use lists as constructor for sets <class 'set'>
And we can used mixed sets <class 'set'>
> > ~~~
> > {: .output}
{: .solution}

# sets also have some basic methods

~~~python
print(f'Sets have length {len(mixed_set)}')
mixed_set.remove('c');print(f'Elements can be removed {mixed_set}')
print(f'And elements can be removed from a set {mixed_set.pop()}')
print(f'Until it is empty  {mixed_set.pop()}')
mixed_set.add('c');print(f'And then added {mixed_set}')
~~~

> ## Output
> > ~~~
Sets have length 3
Elements can be removed {2, 'frontal'}
And elements can be removed from a set 2
Until it is empty  frontal
And then added {'c'}
> > ~~~
> > {: .output}
{: .solution}

# sets also have unique methods

- Consider the following three numeric sets

~~~python
X = {1, 2, 5, 6, 7, 9}
Y = {1, 3, 4, 5, 6, 8} 
Z = {3, 5, 6, 7, 8, 10}
~~~

# sets can be intersected
- The intersection of two or more sets is the set of elements which are common to all sets. 
- For example, the intersection of three sets X, Y and Z is the set of elements that are common to sets X, Y and Z. 
- It is denoted by X ∩ Y ∩ Z


~~~python
XnY = X.intersection(Y) # X ∩ Y
YnX = Y.intersection(X) # X ∩ Y
print(f'Intersection is indifferent to order X ∩ Y == Y ∩ X = {XnY==YnX}')
XnYnZ = X.intersection(Y,Z) # X ∩ Y ∩ Z
print(f'Intersection function can take multiple sets X ∩ Y ∩ Z = {XnYnZ}')
print(f'Intersection can be called using the & operator X & Y & Z = {X & Y & Z}')
~~~

> ## Output
> > ~~~
Intersection is indifferent to order X ∩ Y == Y ∩ X = True
Intersection function can take multiple sets X ∩ Y ∩ Z = {5, 6}
Intersection can be called using the & operator X & Y & Z = {5, 6}
> > ~~~
> > {: .output}
{: .solution}


# Set Difference

- The (set) difference (aka relative complement) between two sets X and Y is written X∖Y, 
- This means the set that consists of the elements of X which are not elements of Y
- The key take-home is that we are after the unique elements of X. 
- Here order does matter!! 
- Difference can be called using the difference function or using the - operator



~~~python
print(f'X\Y={X-Y} and is not equal to Y\X {Y-X}')
print(f'The Difference of X\Y\Z={X.difference(Y,Z)}')
~~~

> ## Output
> > ~~~
X\Y={9, 2, 7} and is not equal to Y\X {8, 3, 4}
The Difference of X\Y\Z={9, 2}
> > ~~~
> > {: .output}
{: .solution}


# Sets are a powerful tool 

- But for this course, the above is enough

# Summary 
 
- In this section we covered the different common data structures Python has  
- We saw how Lists, Tuples, Dictionaries and Sets could be created 
- We learned about some basic methods they have 
- And we learned how to index and slice parts of them
- You deserve a break before heading out to the last Programming section 


## Links to expand your understanding 

For those interested in learning more...

- [Python Data Structures Tutorial](https://www.datacamp.com/community/tutorials/data-structures-python)



{% include links.md %}

