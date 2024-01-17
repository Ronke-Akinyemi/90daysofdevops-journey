---
title: "Python Data Types and Data Structures for DevOps"
datePublished: Thu Oct 26 2023 11:44:27 GMT+0000 (Coordinated Universal Time)
cuid: clo749xie000e09mlaew3ds6j
slug: python-data-types-and-data-structures-for-devops
tags: python-beginner, 90daysofdevops, trainwithshubham, 90daysofdevops-chanllenge

---

# Python

Python is a flexible, high-level programming language for diverse tasks, including web development, data analysis, scientific computing, automation, and more. Python consists of vast libraries and various frameworks like Django, Tensorflow, Flask, Pandas, Keras, etc. Python is known for its simplicity and readability. Python is an open-source programming language, which means it is freely available to the public to use and modify without any restrictions.

## Basic Python Data Types

1. **Booleans (bool):** are used to represent true or false values. Booleans are used for logical operations and conditional statements.
    
    is\_true = True
    
    is\_false = False
    
2. **Integers (int):** are used to represent whole numbers, both positive and negative, without a decimal point.
    
    a = 7
    
3. **Floating-point Numbers (float):** are used to represent numbers with decimal points.
    
    b = 2.34
    
4. **Strings (str):** are used to represent text data.
    
    text = "Hello!"
    
5. **Lists (list):** are ordered collections of items. Lists can contain elements of different data types.
    
    my\_list = \[1, 2, "three"\]
    
6. **Sets (set):** are unordered collections of unique elements. They are often used to eliminate duplicates or perform mathematical set operations.
    
    unique\_numbers = {1, 2, 3, 4}
    
7. **Dictionaries (dict):** contains key-value pairs. It is useful for creating mappings and associative arrays.
    
    person = {"name": "Jane", "age": 30}
    
8. **Tuples (tuple):** are similar to lists but immutable, meaning you cannot change the elements after creation.
    
    (1, 2, 3, 4)
    
9. **NoneType (None):** Represents the absence of a value. It's often used to indicate the lack of a specific result or uninitialized variables.
    
    result = None
    

## Data Structures

Data Structures are a way of organizing data to be accessed more efficiently depending on the situation. Data Structures are fundamentals of any programming language a program uses. Python helps to learn the fundamentals of these data structures more simply than other programming languages.

* Lists Python: Lists are like the arrays declared in other languages, an ordered data collection. It is very flexible, as the items in a list do not need to be of the same type.
    
* Tuple Python: Tuple is a collection of Python objects much like a list, but Tuples are immutable, i.e., the elements in the tuple cannot be added or removed once created. Like a List, a Tuple can also contain elements of various types.
    
* Dictionary: Python dictionary is like hash tables in any other language with the time complexity of O(1). It is an unordered collection of data values used to store data values like a map, which, unlike other Data Types that hold only a single value as an element, Dictionary contains the key: value pair. Key-value is provided in the Dictionary to make it more optimized.
    

**Tasks**

1. Give the Difference between List, Tuple and set. Do Handson and put screenshots as per your understanding.
    

| **Characteristic** | **Lists** | **Tuples** | **Sets** |
| --- | --- | --- | --- |
| **Mutability** | Mutable (can be changed) | Immutable (cannot be changed) | Mutable (can be changed) |
| **Syntax** | Enclosed in square brackets \[ \] | Enclosed in parentheses ( ) | Enclosed in curly braces { } |
| **Order** | Ordered (elements maintain the order of insertion) | Ordered (elements maintain the order of insertion) | Unordered (elements have no specific order) |
| **Duplicates** | Allows duplicate elements | Allows duplicate elements | Does not allow duplicate elements |
| **Access** | Elements can be accessed by index | Elements can be accessed by index | Elements can be accessed using iteration (no index) |
| **Examples** | my\_list = \[1, 2, 3\] | my\_tuple = (1, 2, 3) | my\_set = {1, 2, 3} |

Lists

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698312899675/f97503bf-cbd6-43f5-ba24-f2bc0a1dbb38.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698312955295/c7618769-4c91-4587-99d4-92d6882c4563.png align="center")

Tuples

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698312987558/97be1005-9215-4351-ae81-fb710a39428c.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698313033699/b13b2187-d0c8-4c69-a5d4-b098b9e521e8.png align="center")

Sets

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698313084626/65366795-ade5-4c47-b29d-3614da5aba20.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698313116658/0f683c61-50a6-4c52-99ae-b03234242519.png align="center")

1. Create the below Dictionary and use Dictionary methods to print your favourite tool just by using the keys of the Dictionary.
    
    fav\_too l =
    
    { 1: "Linux", 2: "Git", 3: "Docker", 4: "Kubernetes", 5: "Terraform", 6: "Ansible", 7: "Chef" }
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698313212032/adb87a96-8bd6-476a-ad79-63525d73d09b.png align="center")
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698313231123/a982e26e-bc03-43bc-9131-4f5684c3f3ff.png align="center")
    
2. Create a List of cloud service providers eg. cloud\_providers = \["AWS", "GCP", "Azure"\]
    

Write a program to add `Digital Ocean` to the list of cloud\_providers and sort the list in alphabetical order.

\[Hint: Use keys to built-in functions for Lists\]

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698313281686/e61a5d65-bb7f-4e69-8071-e02a1062169b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698313306651/9b33ae07-774a-4f6d-ab5f-763a597ab7f7.png align="center")

Thanks for reading!