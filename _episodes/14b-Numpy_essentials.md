---
title: "Numpy essentials (with a touch of matplotlib)"
author: "Dr. Eyal Soreq" 
date: "03/06/2021"
teaching: 55
exercises: 0
questions:
- How to use Matplotlib?
- What is NumPy?
- How to create NumPy Arrays?
- How can I use NumPy Arrays?
- What are common NumPy Methods and Operations?
objectives:
- Learn how to use basic Numpy tools
- Learn how to visualize Numpy data using Matplotlib
keypoints:
- NumPy arrays are the main way to store data using the NumPy library.
---


# All about basic data 

- In this session, we will explore Python's data capabilities
- We will use two packages - Numpy and Matplotlib


# NumPy

NumPy (or Numpy) is a Linear Algebra Library for Python, the reason it is so important for Data Science with Python is that almost all of the libraries in the PyData Ecosystem rely on NumPy as one of their main building blocks.


# Numpy Basics

- NumPy is **THE** numeric library for python.
- Almost all the packages we will use from now on will rely on NumPy on some way or another.
- It is also much faster and efficient than standard Python packages 
- NumPy is even more convenient. You get a lot of vector and matrix operations for free, which sometimes allow one to avoid unnecessary work. And they are also efficiently implemented.
- We won't cover all of Numpy functions and capabilities, but instead, we will focus on using vectors and arrays (politely ignoring matrix). 
- We will also cover some of the primary functions 
- But we will start by importing it to make sure it is loaded 

~~~python
import numpy as np
~~~



# Numpy Arrays

- NumPy’s main data structure is the multidimensional array.
- Numpy arrays essentially come in two flavors: vectors and matrices. 
- Vectors are strictly 1-d arrays and matrices are at least 1-d (but with thickness of 1).

# Creating 1d vectors and Arrays

- There are many ways of creating vectors 
- The simplest would be to use the range generator 
- Importantly, a vector has no thickness
- T = transpose (i.e. fliping the array over its diagonal)

~~~python
vector_row = np.array(range(1,11))
array_1d_column = np.array([range(1,11)])
array_1d_row = np.array([range(1,11)]).T
~~~


> ## Look into shape
> > ~~~python
print(f'A vector has only one dimension: {vector_row.shape}')
print(f'An 1d column array has two dimensions: rows:{array_1d_column.shape[0]} and cols:{array_1d_column.shape[1]}')
print(f'An 1d row array has also two dimensions: rows:{array_1d_row.shape[0]} and cols:{array_1d_row.shape[1]}')
> > ~~~
{: .solution}


## Compare the shapes of the following:
~~~python
a_1 = np.array(range(2,7)) 
a_2 = np.array([range(2,7)]) 
a_3 = np.array(a_2.T)
~~~

# Creating 1d vectors and Arrays from lists or loops 

- There are many more ways of creating arrays 

~~~python
vector_row = np.array([1]*10)
array_2d_wide = np.array([range(1,11,1) for _ in range(6)])
array_2d_tall = np.array([range(1,6,1) for _ in range(11)])
array_3d_wide = np.array([[[0.5]*3]*200]*100)
array_3d_tall = np.array([[[0.5]*3]*100]*200)
~~~

# You can apply any arithmetic function to an array with a scalar 

~~~python
X = 5
display(vector_row * X)
display(array_2d_wide / X)
display(array_2d_tall % X)
display(array_2d_tall ** X)
display(array_2d_tall - X)
~~~

# Broadcasting

The term broadcasting refers to the ability of NumPy to treat arrays of different shapes during arithmetic operations. Arithmetic operations on arrays are usually done on corresponding elements. If two arrays are of exactly the same shape, then these operations are smoothly performed[1](https://www.tutorialspoint.com/numpy/numpy_broadcasting.htm).


~~~python
a = np.array([range(2,7)]) 
b = np.array([range(-12,-7)])
c = a * b
d = a + b
~~~




# Matplotlib Basics

In Python, Matplotlib is the "grandfather" of data visualization. It was created by John Hunter. This was created to try and replicate MATLAB's plotting capabilities with Python. This is an excellent 2D and 3D graphics library for creating reproducible publication ready scientific figures.
 
Some of the major Pros of Matplotlib are:
 
* Simple plots are generally easy to create
* Each element in the figure is nicely controlled
* A variety of output formats with high quality

~~~python
import matplotlib.pyplot as plt
%matplotlib inline
plt.style.use('bmh')
~~~

# Visualization as a discovery tool
> *"The greatest value of a picture is when it forces us to notice what we never expected
to see.* **John W Tukey**



## lets look at these 

~~~python
from matplotlib import pyplot as plt 
# we import matplotlib module pyplot and name it plt
fig, (ax1, ax2) = plt.subplots(1, 2)
# we create a figure containing two side by side plots
ax1.imshow(array_3d_wide)
ax2.imshow(array_3d_tall)
# we use the function imshow to visualize these 3d matrices as images 
~~~

# Creating 1d vectors and Arrays from lists 

- Height, width, depth = array_3d.shape
- Note, however, that ndarray has matrix coordinates (i,j), which are opposite to image coordinates (x,y).

# Creating 1d vectors using numpy Built-in Methods

- linspace() creates linearly spaced values 
- logspace() creates log10 spaced values 
- arange() is similar to range (i.e. Array of values from to with steps) 

~~~python
vector_linspaced = np.linspace(0,50,60)
vector_logspace = np.logspace(0,5,60)
vector_step = 2**np.arange(0,60,1) 
~~~

## And visualize
~~~python
fig, ax = plt.subplots(3, 1)
data = [vector_linspaced,vector_logspace,vector_step]
for i,(ix,iy) in enumerate(zip([0,0,1],[1,2,2])):
    ax[i].plot(data[ix],data[iy],'r-')
plt.tight_layout() 
~~~


# Creating Arrays using numpy Built-in Methods

- Built-in methods require tuple or list to create >=2d arrays
- We can create arrays of full of zeros 
- And they can have predefined data types (which means we can sacrifice some accuracy in favour of memory 
- This process is called to preallocate a matrix 

~~~python
zeros_vector = np.zeros(10)
zeros_2d_array = np.zeros((10,10))
zeros_3d__int8_array = np.zeros((10,10,10),dtype="int8")
zeros_3d_float64_array = np.zeros([10,10,10],dtype="float64")
# we can go on and on 
print(zeros_3d__int8_array.dtype)
print(zeros_3d_float64_array.dtype)
~~~


- We can also create ones, identity matrix (i.e. ones in the lead diagonal)
- And even with predefined values using full

~~~python
ones_3d_int8_array = np.ones([10,10,3])
eye_3d_bool_array = np.eye(10,dtype="b")
full_3d_array = np.full((10,10,3),156)
~~~

## And visualize
~~~python
ones_3d_int8_array[:,3:-3,:] = 0
ones_3d_int8_array[3:-3,:,:] = 0
full_3d_array[2:,:5,:2] = 50
full_3d_array[2:,6:,1] = 120

fig, ax = plt.subplots(1, 3)
data = [ones_3d_int8_array,eye_3d_bool_array,full_3d_array]
for i,d in enumerate(data):
    ax[i].imshow(d)
plt.tight_layout() 
~~~


- And even arrays with various randome number generators (e.g. random, integers, etc)

~~~python 
for i in np.arange(0,3):
    rng = np.random.default_rng()
    print(f'Randomly sample a float{rng.random()}') # generate a random float
    print(f'Randomly sample 3 integers :{rng.integers(low=0, high=10, size=3)}') 
    # generate 3 random integers between 0 (inclusive) and 10 (exclusive)
~~~

## What about reproducible results

~~~python 
for i in np.arange(0,3):
    rng = np.random.default_rng(seed =42)
    print(f'Randomly sample a float{rng.random()}') # generate a random float
    print(f'Randomly sample 3 integers :{rng.integers(low=0, high=10, size=3)}') 
    # generate 3 random integers between 0 (inclusive) and 10 (exclusive)
~~~

## We can sample any size of array 

~~~python 
display(rng.random((5,5)))
display(rng.integers(low=0, high=10, size=(3,4)))
~~~

## We have permutations

~~~python
rng = np.random.default_rng(seed =42)
k=100
vector_a1 = rng.random( size=(1,k))
vector_b1 = rng.integers(low=6, high=16, size=(1,k))
fig, ax = plt.subplots(3, 1)
data = [vector_a1,vector_b1]
color = ['r','g','b']
for i in range(3):
    x = data[0][0,rng.permutation(data[0].shape[1])]
    y = data[1][0,rng.permutation(data[1].shape[1])]
    ax[i].scatter(x,y,color=color[i],alpha=0.5)
plt.tight_layout() 
~~~

## We can select a sample from a 1d array 

~~~python
rng = np.random.default_rng(seed =42)
k=1000
seq = [chr(x) for x in range(65, 70)]
p = [0.6,0.225,0.1,0.05,0.025]
sample_1 = rng.choice(seq,replace=True, size=(k,),p=p)
sample_2 = rng.choice(seq,replace=True, size=(k,),p=p[::-1])
~~~


### And visualize the two contrasted samples

~~~python
fig, ax = plt.subplots(1, 1)
data = [sample_1,sample_2]
labels = ['Condition_1','Condition_2']
for d,label,sign in zip(data,labels,[-1,1]):
    unique, counts = np.unique(d, return_counts=True)
    x,width = np.arange(len(seq)),0.35
    ax.bar(x+sign*(width/2+0.01),counts,width, label=label)
ax.legend(ncol=2)
ax.set_title(f'Comapring between {labels[0]} and {labels[1]}')
ax.set_xlabel('Some factor')
ax.set_ylabel('Some metric')
~~~

### Or with precentage and adding original sampling

~~~python
fig, ax = plt.subplots(1, 1)
data = [sample_1,sample_2]
labels = ['Condition_1','Condition_2']
for d,label,sign in zip(data,labels,[-1,1]):
    unique, counts = np.unique(d, return_counts=True)
    x,width = np.arange(len(seq)),0.35
    ax.bar(x+sign*(width/2+0.01),counts/sum(counts),width, label=label)
ax.legend(ncol=2)
ax.plot(x-width/2,p,'k*:')
ax.plot(x+width/2,p[::-1],'ko--')
ax.set_title(f'Comapring between {labels[0]} and {labels[1]}')
ax.set_xlabel('Some factor')
ax.set_xticks(x)
ax.set_xticklabels(seq)
ax.set_ylabel('Some metric')
~~~


# Distributions
- Very large set of distributions to choose from  
- Here I am going over the central ones


## The uniform distribution (Uniform noise)

- A uniform distribution gets its name because the results of its experiment are evenly or 'uniformly' distributed across the sample space. 

### SYNTAX = `uniform(low, high, size)`

~~~python
rng = np.random.default_rng(seed = 2021)
v_1 = rng.uniform(0,1,(1,int(1e4)))
v_2 = rng.uniform(0.5,1.5,(1,int(1e4)))
m_2d = rng.uniform(0,1,(128,128))
m_3d = rng.uniform(0,1,(128,128,3))
~~~

### And visualize
~~~python
import matplotlib.gridspec as gridspec
fig = plt.figure(tight_layout=True)
gs = gridspec.GridSpec(2, 2)
data = [[v_1,v_2],m_2d,m_3d]
for i,d in enumerate(data):
    if i:
        ax = fig.add_subplot(gs[1, i-1])   
        ax.imshow(d,aspect="auto")
    else:   
        ax = fig.add_subplot(gs[0, :])
        ax.scatter(d[0],d[1],s=5,alpha=0.5,c=d[0])
plt.tight_layout() 
~~~

## The normal distribution (white/Gaussian noise)

- A Gaussian distribution, often referred to as a normal distribution, gives a bell shaped curve with the top of the curve representing where the majority or average number of experimental results will lie. The width of the bell-curve provides a visual cue to how spread out the distribution will be from that center point.

### SYNTAX = `normal(loc, scale, size)`

~~~python
rng = np.random.default_rng(seed = 2021)
v_1 = rng.normal(0,1,(int(1e4),))
v_2 = rng.normal(0,3,(int(1e4),))
m_2d_1 = rng.normal(0,1,(128,128))
m_2d_2 = rng.normal(0,3,(128,128))
~~~

### And visualize
~~~python
import matplotlib.gridspec as gridspec
fig = plt.figure(tight_layout=True)
num_bins = 100
gs = gridspec.GridSpec(2, 6)
data = [[v_1,v_2],m_2d_1,m_2d_2]
for i,d in enumerate(data):
    if i:
        s,e = (0,3) if i==1 else (3,6)
        ax = fig.add_subplot(gs[1, s:e])   
        ax.pcolormesh(d,vmax=10,vmin=-10)
    else:
        for j in range(3):   
            ax = fig.add_subplot(gs[0, 2*j:2*j+2])
            if j==1:
              ax.scatter(d[0],d[1],s=5,alpha=0.5,c=d[1]*d[0])
              ax.set_ylim(-15,15)
              ax.set_xlim(-15,15)
            else:
              x = d[0] if j==0 else d[1]
              ax.hist(x, num_bins, density=False)
plt.tight_layout() 
~~~


## The exponential distribution 

- The exponential distribution is often concerned with the amount of time until some specific event occurs. 


### SYNTAX = `normal(loc, scale, size)`

~~~python
rng = np.random.default_rng(seed = 2021)
v_1 = rng.exponential(1,(int(1e4),))
v_2 = rng.exponential(3,(int(1e4),))
m_2d_1 = rng.exponential(1,(128,128))
m_2d_2 = rng.exponential(3,(128,128))
~~~

### And visualize
~~~python
import matplotlib.gridspec as gridspec
fig = plt.figure(tight_layout=True)
num_bins = 100
gs = gridspec.GridSpec(2, 6)
data = [[v_1,v_2],m_2d_1,m_2d_2]
for i,d in enumerate(data):
    if i:
        s,e = (0,3) if i==1 else (3,6)
        ax = fig.add_subplot(gs[1, s:e])   
        ax.pcolormesh(d,vmax=5,vmin=0)
    else:
        for j in range(3):   
            ax = fig.add_subplot(gs[0, 2*j:2*j+2])
            if j==1:
              ax.scatter(d[0],d[1],s=5,alpha=0.5,c=d[1]*d[0])
              ax.set_ylim(0,25)
              ax.set_xlim(0,20)
            else:
              x = d[0] if j==0 else d[1]
              ax.hist(x, num_bins, density=False)
plt.tight_layout() 
~~~



# Inspecting array Properties

- In Numpy array have properties
- We already saw the shape property that returns a tuple describing the length of each dimension
- We also saw Numpy has many different data types
- The last property I want to cover is Size which simple returns the number of dimensions the array has

~~~python
arr = np.array((10,20,30))
print(arr.size)
~~~

# Indexing in Numpy vectors

- Indexing in Numpy is far simpler than in multidimensional lists
- lets explore some examples


~~~python
vector = np.array(range(1,11))# 10 rows
print(f'Vector = {vector}')
print(f'First element = {vector[0]}')
print(f'Last element = {vector[-1]}')
print(f'Middle elements = {vector[len(vector)//2-1:len(vector)//2+1]}')
print(f'All elements strating from 4 = {vector[4:]}')
print(f'last 4 elements = {vector[-4:]}')
print(f'Everything but last 4 elements = {vector[:-4]}')
~~~

<!-- ADD Exercises -->



# Two-Dimensional Indexing and Slicing in Numpy arrays

- Indexing in Numpy is far simpler than in multidimensional lists
- lets explore some examples

~~~python
x = np.array([range(1,13)])
array = x.T*x # element wise multiplication
m,n = array.shape
print(f'Vector = {x}')
print(f'Array = {array}')
~~~



## Column and row specific 

~~~python
print(f'first row = {array[0]}')
print(f'first col = {array[:,0]}')
print(f'first col = {array[:,0]}')
print(f'2 columns from 3 upto 5= {array[:,3:5]}')
print(f'last 4 columns = {array[:,-4:]}')
print(f'center of array = {array[m//2-1:m//2+1,n//2-1:n//2+1]}')
print(f'First element = {array[0,0]}')
print(f'Last element = {array[-1,-1]}')
print(f'All rows above the 4th row = {array[4:,:]}')
print(f'Everything but last 4 elements = {array[:,:-4]}')
print(f'every third row and and every fourth column = {array[0::3,0::4]}')
~~~


## Reshape

- Returns an array containing the same data with a new shape.

~~~python
vector = rng.choice([True,False],replace=True, size=(256,),p=[0.75,0.25])
fig, ax = plt.subplots(1, 3)
for i in range(3):
    arr = {0:vector.reshape(8,-1),
           1:vector.reshape(16,-1),
           2:vector.reshape(32,-1) }[i]
    ax[i].pcolor(arr, edgecolors='w', linewidths=2)
fig.tight_layout()  
~~~



# What are AXES in Numpy ?
- NumPy axes are one of the hardest things to understand in the NumPy system. 
- NumPy axes are the directions along the rows and columns of the array 
- Any operation on the all the rows in each column follow the zero axis `axis=0`
- Any operation on each row **across** columns follow the first axis `axis=1`

# Why is this important 
- We can apply various aggregates and functions along different axis

## Try sum 
~~~python 
x = rng.choice(range(10),replace=True, size=(20,7))
display(np.sum(x,axis=1))
display(np.sum(x,axis=0))
display(np.sum(x))
~~~


## Links to expand your understanding 

For those interested in learning more...

- [Scipy Lecture Notes](https://scipy-lectures.org/intro/numpy/operations.html)
- [matplotlib](https://matplotlib.org/2.0.2/users/pyplot_tutorial.html)
{% include links.md %}