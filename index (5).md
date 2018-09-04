
# Lambda Functions in Python

## Objectives
* Describe and differentiate lambda functions from `def` functions.
* Define lambda functions according to the expected syntax. 
* Understand and apply lambda functions for suitable use cases.
* Use lambda functions with python's built-in functions `map()` and `filter()`.

## Introduction
So far, we have written our own python functions using the `def` approach. Python also supports the creation of anonymous functions (i.e. functions that are not bound to a name). These are usually known as **lambda functions** because we use keyword `lambda` to define these functions. A lambda function can take any number of arguments, but can only have one expression.

Like `def` , the `lambda` creates a function to be called later. It returns the function instead of assigning it to a name. This is why lambda functions are known as anonymous functions. In practice, they are used as a way to in-line a function definition, or to defer execution of a code. This lesson will help you understand the syntax and some common use cases for lambda function declaration.

First we shall see the difference between `lambda` and `def` function declaration for a simple calculation i.e. calculating and returning the square of a number passed into the function. 


```python
# Define a function using def
def function(x):
    ans = x**2
    return ans
function(3)
```




    9




```python
# Define the same function using lambda
ans = lambda x : x**2
ans(3)
```




    9



As we can see that both `def` and `lambda` function declarations result the same answer. However, Unlike `def`, `lambda` functions do not contain a return statement. These functions contain an expression which is always is returned when the function gets called. Lambda function can be introduced anywhere in a python script, and don't need variable assignments in advance.

 The general syntax of lambda functions can be shown as: 
 >** lambda arg1, arg2, .. , argN : expression using given arguments**

## Declaring lambda expressions in Python

![](lambda.png)

To declare a lambda function, you start from the `lambda` keyword.


```python
lambda x:x**2
```




    <function __main__.<lambda>>



This returns a function which can be assigned to a variable name for calling it later and providing arguments to it. 


```python
square = lambda x:x**2
```

Here, `x` is the argument, and `x**2` is the expression. You would call it like you would call a `def` Python function. You can pass in values similarly as shown below:


```python
square(10)
```




    100



### What is an expression ?

Lambda functions return `expressions`. An expression here is similar to what we would put in the return statement of a `def` function. The following are examples of expressions.

* **Arithmetic Operations** like `a+b` or `a^b`
* **Function Calls** like `multiply(a,b)`
* **Print Statement** like `print(“ Lambdas are great ”)`

Assignment statements like `(a = b)` cannot be provided as expressions because these do not return a value. 

### Expression syntax

Expressions may use variables that have been previously defined in the script. However, in the case of arguments passed to the lambda function, these **MUST** provide the expected value to lambda function, otherwise it'll throw an error. Let's see this below:


```python
x = 10
y = 5

out = lambda x,y : x*y
out()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-13-8d76aaa4b9cb> in <module>()
          3 
          4 out = lambda x,y : x*y
    ----> 5 out()
    

    TypeError: <lambda>() missing 2 required positional arguments: 'x' and 'y'


In the error above, we see that the function is missing x and y as arguments containing values for the expression. 


```python
out = lambda x : x*y
out()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-15-d5211347e660> in <module>()
          1 out = lambda x : x*y
    ----> 2 out()
    

    TypeError: <lambda>() missing 1 required positional argument: 'x'


Here the function is still missing one value , hence the error is returned. 

So how do we get it right ? Have a look below:


```python
out = lambda : x*y
out()
```




    50



So finally we have a lambda function with no missing valued arguments. We also saw that it is not necessary to provide arguments to the lambda function.

At this stage, we have learnt that:
* Lambda is an expression, not a statement.
* Lambda's body contains a single statement, not a sequence of statements. 
* Lambda functions can operate without input arguments. 

Let's now have a look at some use cases where you might want to use lambda functions.

## Lambda functions use cases ?

The lambdas can be used as a function shorthand that allows us to embed a function within the code. Following are some of the common use cases for lambda functions:

#### Single statement functions

The ideal use case for using lambda function is when we only have a single statement to execute as seen above. For example, imagine we want to print a string `"hello lambda"` in a function called `greet()`. This function would require only a single statement in its body as below:


```python
def greet():
    print ('hello lambda')
    return
greet()
```

    hello lambda


This functionality can be reproduced through a lambda function in a single line of code:


```python
greet = lambda : print ('hello lambda')
greet()
```

    hello lambda


#### Creating jump tables
A jump table is an array of pointers to functions. Lambda functions can simplify the creation of jump tables by performing actions on lists (or dictionaries) on demand. Let's have a look at following example:


```python
lst = [lambda x: x ** 2, lambda x: x ** 3, lambda x: x ** 4]
for lamb in lst:
    print (lamb(5))
```

    25
    125
    625


Above, we created a list with three lambda functions embedded inside the list. A `def` can't work inside a list because it is a statement, not an expression. 

Let's try doing it with `def` this time. We would need to define some temporary function names and definitions as below:


```python
def func1(x): 
    return x ** 2
def func2(x): 
    return x ** 3
def func3(x): 
    return x ** 4

lst = [func1, func2, func3]
for func in lst:
    print (func(5))
```

    25
    125
    625


#### Conditionals with lambda functions

Lambda functions can also embed if-else statements. the syntax for using conditionals within lambda function can be seen from the example below where the function computes and output minimum value from input arguments. Syntax used for this can be generalized as:
> **lambda arg1,arg2 : expression1 if (condition=True) else expression2**

Let's see this in action:


```python
minimum = (lambda a,b : a if a < b else b)
print(minimum(2,3))
print(minimum(25*300, 49*200))
```

    2
    7500


#### Lambda with `map()` and `filter()`

Python lambda functions can be applied to other built-in functions like `filter()` and `map()` e.g. to filter out elements from a list or dictionary. Let's see how this is achieved. First we shall create a list of numbers:


```python
nums = list(range(1,11))
nums
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]



Let's say we now want to filter the `nums` list and create another list containing only the even numbers from `nums`. We can use the `filter()` function which takes in two parameters i.e. a function and a list to process. We can write the lambda function as follows:


```python
list(filter(lambda x : x % 2 == 0, nums))
```




    [2, 4, 6, 8, 10]



We used `list()` above to convert the filter object into an array for display. Also note that this operation does not change the original list of numbers in any way. 

Another built-in python function called `map()` can also work with lambda functions. `map()` function maps every element of given list to the expression and returns the results. Let's try lambda and map for above example:


```python
list(map(lambda x:x%2==0,nums))
```




    [False, True, False, True, False, True, False, True, False, True]



Here, a True value is returned every time a list element satisfies the condition given in the expression, and returns a false otherwise. 

## Summary

In this lesson, we looked at lambda functions in python. We learnt how to declare lambda functions with the expected syntax. We also had a look at what exactly is an expression and how to define one in a lambda function. Finally we saw some common use cases for lambda functions and how they may prove more productive than `def` functions in certain circumstances. 
