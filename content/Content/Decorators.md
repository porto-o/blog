---
draft: true
tags:
  - Python
  - Content
  - Nous
---
# What is ?

Is a design pattern in Python that allows a user to **add new functionality to an existing object without modifying its structure**.

But let's explain with code, imagine you have the following function

```Python
def square(x):
	return x**2
```

This function will return the square of the number x

But what if we need further operations after squaring a number? We could modify the function but it will have no sense the name *square*. To add this new functionality we can use **decorators**.

Let's create our decorator:

```Python
def decorator(func):
	def wrapper(x):
		print('Modifying behaviour')
		return (func(x)*3)
	return wrapper
```

At the end of the day a decorator is a **function** that will receive a function as a **parameter**. Inside of the decorator function we will have another function that is commonly named as **wrapper**. This wrapper function will be the one that actually modifies the behavior of the square function, so it must receive the data *x*. 

This wrapper function will **return** the execution of the function but with further operations or features.

After that, the decorator function must return that wrapper function

### How can we execute it?

In order to let Python know that we have a decorator for the function square, we must write something like this

```Python
@decorator
def square(x):
	return x**2
```

With the @, python knows that there is a function called *decorator* that will modify the behavior of the square function.

after that what we can do is the following:

```Python
# Save the return of the decorator (the wrapper function) inside a variable
decoration = decorator(square)
# Execute the returned function, passing the argument x
decoration(3)
# This code will return 
# 27
```

# Real use cases

* When we need to execute a function from a class without creating an instance of this class
* 