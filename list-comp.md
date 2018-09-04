
# Python List Comprehension

## Objectives
* Understand and explain list comprehensions as alternatives to for loops.
* Describe correct syntax for list comprehensions with required components. 
* Implement list comprehensions with conditionals and nested loops.
* Write basic nested list comprehensions. 


## Introduction

Python's list comprehensions provide us with an easy way to write `for` loops more concisely. List comprehensions are very useful towards creating new lists from existing lists or other iterables (dictionaries etc). The name *"list comprehensions"* can be a bit misleading because apparently it suggests that the comprehensions only work with lists. In reality, we can loop over any iterable object in Python. The output, at the end of execution will always be a list. 

For example, you can use list comprehensions to create a list of squares from a list of numbers. Have a look at this example below that uses for loops as well as list comprehension to create a new list from an existing one.


```python
# Use For Loop

x1 = [1,2,3,4,5]
x2 = []

for x in x1:
    x2.append(x**2)

print (x2)    
```

    [1, 4, 9, 16, 25]


The for loop above can be replaced by a single line list comprehension, which outputs a new list. The new list does not need initialization as empty list above.


```python
x1 = [1,2,3,4,5]
x2 = [x**2 for x in x1] # List comprehension 
print(x2, type(x2))
```

    [1, 4, 9, 16, 25] <class 'list'>


## List Comprehension Syntax

The for loop, as we have seen before in our lessons and labs, has the following structure:

> **for ELEMENT in ITERABLE:**

    > **EXPRESSION**

As seen in above example, basic list comprehensions can be defined using following syntax:

> **[EXPRESSION for ELEMENT in ITERABLE]**

In above example, `x**2` is the expression, `x` is the current element of the iterable and `x1` is the iterable. 

Let's another simple example of writing a basic for loop to create list of first 10 multiples of 8. We shall perform following tasks to achieve this:

* Create an empty list.
* Iterate over a range of numbers and multiply them by 8. 

The new sequence of numbers that we get will consist of multiples of 8.


```python
lst = []

for n in range(1,11):
    lst.append(n*8)
     
print(lst)
```

    [8, 16, 24, 32, 40, 48, 56, 64, 72, 80]


For list comprehensions, current **ELEMENT** is `n`, the **ITERABLE** is a list outpurt by `range(1,11)`, and the **EXPRESSION** is `n x 8`. Let's try to reproduce above results using list comprehension:


```python
# [EXPRESSION for ELEMENT in ITERABLE]
[n*8 for n in range(1,11)]
```




    [8, 16, 24, 32, 40, 48, 56, 64, 72, 80]



You can easily replace the expression above with any other expression and the comprehension will work fine. Let's try to take square of all numbers in our list. 


```python
# [EXPRESSION for ELEMENT in ITERABLE]
[n**2 for n in range(1,11)]
```




    [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]



## List Comprehension with Conditions

We can also use a conditional structure with list comprehensions to apply filtering to certain values from the final list. In this case, the list comprehension has following syntax:

> **[EXPRESSION for ELEMENT in ITERABLE if CONDITION]**

A basic example of this type of comprehension would be to get all the odd numbers in a given list. 
Let's see how a `for` loop would achieve this:


```python
odds = []
 
for n in range(1,11):
    if n%2 != 0:
        odds.append(n)
         
print(odds)
```

    [1, 3, 5, 7, 9]


Achieving similar output using list comprehension takes the following form:


```python
# [EXPRESSION for ELEMENT in ITERABLE if CONDITION]
[n for n in range(1,11) if n%2 != 0]
```




    [1, 3, 5, 7, 9]



So you see how list comprehension can be used to simply code while getting the same `for` loop functionality. A more complex example of using list comprehensions would be adding `if .. else ..` conditional expressions. For this, the order in which we structure the list comprehension will be slightly different from usual `if` conditions. When we have a single `if` condition, the condition goes to the end of the comprehension. In the case of an `if .. else ..` expression, the positions of the for loop and the conditional expression are interchanged. The general syntax for such statements is:

>**[EXPRESSION_1 if CONDITION else EXPRESSION_2 for ELEMENT in ITERABLE]**

Let's write a for loop which will take the squares of even numbers and cubes of odd numbers for the elements in a given list.


```python
powers = []
 
for n in range(1,11):
    if n%2 == 0:
        powers.append(n**2)
    else:
        powers.append(n**3)
         
print(powers)
```

    [1, 4, 27, 16, 125, 36, 343, 64, 729, 100]


Great, now let's try to reproduce these results using conditionals with list comprehension


```python
# [EXPRESSION_1 if CONDITION else EXPRESSION_2 for ELEMENT in ITERABLE]
[n**2 if n%2 == 0 else n**3 for n in range(1,11)]
```




    [1, 4, 27, 16, 125, 36, 343, 64, 729, 100]



## List Comprehension with Nested loops

List comprehension in python also allows embedding of nested loops and there is no limit on the number of nested for loops that you can define. We can also add an optional if condition after each for loop. 

A list comprehension with nested for loops will have the following syntax:

>**[EXPRESSION for ELEMENT_a in ITERABLE_a (optional if CONDITION_a)**

>**for ELEMENT_b in ITERABLE_b (optional if CONDITION_b)**

>**for ELEMENT_c in ITERABLE_c (optional if CONDITION_c)**

>**...]**

Let's look at an example to clear this up. There are two nested loops, and multiplying them together gives us multiplication tables for 1 - 4 for first 10 steps as shown below.


```python
tables = []
 
for i in range(1, 5):
    for n in range(1, 11):
        tables.append(i*n)
 
print(tables)
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 4, 8, 12, 16, 20, 24, 28, 32, 36, 40]


Let's now try to achieve this through list comprehension using the syntax shown above:


```python
# [EXPRESSION for ELEMENT_a in ITERABLE_a for ELEMENT_b in ITERABLE_b]

print([i*n for i in range(1,5) for n in range(1,11)])
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 4, 8, 12, 16, 20, 24, 28, 32, 36, 40]


This feature can become really helpful while flattening down a list of lists (a matrix). Let's have a look at the example below:


```python
mat     = [[1, 2, 3, 4],
          [5, 6, 7, 8],
          [9, 10, 11, 12],]

# # [EXPRESSION for ELEMENT_a in ITERABLE_a for ELEMENT_b in ITERABLE_b]
[n for row in mat for n in row]
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]



In this example, The outer for loop `n for row in mat` iterates through individual lists and stores them in the variable row. 

The inner for loop  `mat for n in row` will then iterate through all the elements in the current row.

During the first iteration, the variable row has the value [1, 2, 3, 4]. The second loop iterates through this list or row and appends all those values to the final list. As we can see the code becomes slightly difficult to read when we implement nested for loops with list comprehensions. 

## Nested List Comprehension

Nested list comprehensions are very different to list comprehensions with nested loops. For nested loops, we deal with loops within loops. However, for nested list comprehensions, we define list comprehensions within list comprehensions. 

Let's set our problem of transposing the matrix `mat` shown above to see this in action.  

Without a list comprehension expression, you will need to use two for loops to transpose the matrix as shown below:


```python
import pandas as pd
T = []
 
for i in range(4):
    temp = []
    for row in mat:
        temp.append(row[i])
    T.append(temp)

# Use dataframes for printing as matrix
print(pd.DataFrame(mat).to_string(index=False, header=False))
print('')
print (pd.DataFrame(T).to_string(index=False,  header=False))
```

    1   2   3   4
    5   6   7   8
    9  10  11  12
    
    1  5   9
    2  6  10
    3  7  11
    4  8  12


Let's now try to get the same output with nested list comprehension. We shall:

* Create a list.
* Execute nested loop as list comprehension.
* Convert the output to a dataframe. 
* Change the element types to string.
* Remove header and index.
* Print the output as a matrix 

all in one line of code.

Although we can see that the code might get a bit hard to read, but this demonstrates  how you can replace a lengthy block of code with a single line using list comprehensions with some clever programming.


```python
print(pd.DataFrame([[row[n] for row in mat] for n in range(4)]).to_string(index=False, header=False))
```

    1  5   9
    2  6  10
    3  7  11
    4  8  12


In nested list comprehension, we see  that the **EXPRESSION** in ordinary list comprehension **[EXPRESSION for ELEMENT in ITERABLE]** is yet another list comprehension i.e. **[row[n] for row in mat]**.

This nested list comprehension itself is in the form of a basic for loop.

## Summary 

In this lesson, we learnt what list comprehensions are and how to use them in place of basic for loops to write brief yet faster code while creating lists.  We also looked at list comprehensions with conditionals, loops and nested loops. Creating list comprehensions for nested loops OR creating nested list comprehensions makes the code less readable as we saw above. In such cases, we can break down the list comprehension into multiple list comprehensions to improve readability.
