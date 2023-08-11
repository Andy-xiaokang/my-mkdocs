# Chapter 2: Building Abstraction with Data
## 2.1 Introduction
### 2.1.1 Native Data Types
Every value in Python has a ***class*** that determines what type of value it is. Values that share a class also share behavior. For example, the integers `1` and `2` are both instances of the `int` class. These two values can be treated similarly. For example, they can both be negated or added to another integer. The built-in **`type`** function allows us to inspect the class of any value.

```python 
>>> type(2)
<class 'int'>
```

The values we have used so far are instances of a small number of native data types that are built into the Python language. Native data types have the following properties:
1. There are expressions that evaluate to values of native types, called *literals*.
2. There are built-in functions and operators to manipulate values of native types.

Python includes three native numeric types: integers (`int`), real numbers (`float`), and complex numbers (`complex`).  
**Floats**. The name `float` comes from the way in which real numbers are represented in Python and many other programming languages: a "floating point" representation.

### 2.2.2 Pairs
The elements of a list can be accessed in two ways. The first way is via our familiar method of multiple assignment, which ***unpacks*** a list into its elements and binds each element to a different name. A second method for accessing the elements in a list is by the element selection operator, also expressed using square brackets.  
The equivalent function for the element selection operator is called `getitem`, and it also uses 0-indexed positions to select elements from a list.  
```python
>>> from operator import getitem
>>> getitem(pair, 0)
10
>>> getitem(pair, 1)
20
```

### 2.2.4 The Properties of Data
> In general, we can express abstract data using a collection of selectors and constructors, together with some behavior conditions. As long as the behavior conditions are met (such as the division property above), the selectors and constructors constitute a valid representation of a kind of data. The implementation details below an abstraction barrier may change, but if the behavior does not, then the data abstraction remains valid, and any program written using this data abstraction will remain correct.  

## 2.3 Sequences  
A sequence is an ordered collection of values. The sequence is a powerful, fundamental abstraction in computer science. **Sequences are not instances of a particular built-in type or abstract data representation**, ***but instead a collection of behaviors that are shared among several different types of data***. That is, there are many kinds of sequences, but they all share common behavior. In particular  

* **Length**. A sequence has a finite length. An empty sequence has length 0.  
* **Element selection**. A sequence has an element corresponding to any non-negative integer index less than its length, starting at 0 for the first element.  

### 2.3.1 Lists
A `list` value is a sequence that can have arbitrary length. Lists have a large set of built-in behaviors, along with specific syntax to express those behaviors. We have already seen the `list` literal, which evaluates to a `list` instance, as well as an element selection expression that evaluates to a value in the `list`. The built-in `len` function returns the length of a sequence.  
Additionally, lists can be added together and multiplied by integers. For sequences, addition and multiplication do not add or multiply elements, but instead **combine and replicate** the sequences themselves.  

### 2.3.2 Sequence Iteration
The Python for statement can simplify this function body by iterating over the element values directly without introducing the name index at all.  
A `for` statement is executed by the following procedure:

1. Evaluate the header `<expression>`, which must yield an iterable value.  
2. For each element value in that iterable value, in order:
    1. Bind `<name>` to that value in the current frame.
    2. Execute the `<suite>`.

This execution procedure refers to ***iterable*** values. Lists are a type of sequence, and sequences are iterable values. Their elements are considered in their sequential order.  
**Sequence unpacking**. A common pattern in programs is to have a sequence of elements that are themselves sequences, but all of a fixed length. A for statement may include multiple names in its header to "unpack" each element sequence into its respective elements. For example, we may have a list of two-element lists.  
```python
>>> pairs = [[1, 2], [2, 2], [2, 3], [4, 4]]
>>> same_count = 0
>>> for x, y in pairs:
        if x == y:
            same_count = same_count + 1
>>> same_count
2
```
This pattern of binding multiple names to multiple values in a fixed-length sequence is called ***sequence unpacking***  

**Ranges**. A `range` is another built-in type of sequence in Python, which represents a range of integers. Ranges are created with `range`, which takes two integer arguments: the first number and one beyond the last number in the desired range.  
Calling the `list` constructor on a range evaluates to a list with the same elements as the range, so that the elements can be easily inspected.  

```python 
>>> list(range(5, 8))
[5, 6, 7]
```
If only one argument is given, it is interpreted as one beyond the last value for a range that starts at 0.

```python
>>> list(range(4))
[0, 1, 2, 3]
```

### 2.3.3 Sequence Processing
**List Comprehensions.** 
The general form of a list comprehension is:  
`[<map expression> for <name> in <sequence expression> if <filter expression>]`  
To evaluate a list comprehension, Python evaluates the `<sequence expression>`, which must return an iterable value. Then, for each element in order, the element value is bound to `<name>`, the filter expression is evaluated, and if it yields a true value, the map expression is evaluated. The values of the map expression are collected into a list.  

**Aggregation**. A third common pattern in sequence processing is to aggregate all values in a sequence into a single value. The built-in functions `sum`, `min`, and `max` are all examples of aggregation functions.

**Higher-Order Functions**. The common patterns we have observed in sequence processing can be expressed using higher-order functions. First, evaluating an expression for each element in a sequence can be expressed by applying a function to each element.  
```python
>>> def apply_to_all(map_fn, s):
        return [map_fn(x) for x in s]
```

Selecting only elements for which some expression is true can be expressed by applying a function to each element.  
```python
>>> def keep_if(filter_fn, s):
        return [x for x in s if filter_fn(x)]
```
Finally, many forms of aggregation can be expressed as repeatedly applying a two-argument function to the `reduced` value so far and each element in turn.  
```python
>>> def reduce(reduce_fn, s, initial):
        reduced = initial
        for x in s:
            reduced = reduce_fn(reduced, x)
        return reduced
```
**Conventional Names**. In the computer science community, the more common name for `apply_to_all` is **`map`** and the more common name for `keep_if` is **`filter`**. In Python, the built-in `map` and `filter` are generalizations of these functions that do not return lists. The definitions above are equivalent to applying the `list` constructor to the result of built-in `map` and `filter` calls.
```python
>>> apply_to_all = lambda map_fn, s: list(map(map_fn, s))
>>> keep_if = lambda filter_fn, s: list(filter(filter_fn, s))
```
The `reduce` function is built into the functools module of the Python standard library. In this version, the `initial` argument is optional.
```python 
>>> from functools import reduce
>>> from operator import mul
>>> def product(s):
        return reduce(mul, s)
>>> product([1, 2, 3, 4, 5])
120
```
### 2.3.4 Sequence Abstraction
We have introduced two native data types that satisfy the sequence abstraction: lists and ranges. Both satisfy the conditions with which we began this section: **length and element selection**. Python includes two more behaviors of sequence types that extend the sequence abstraction.  
**Membership**. A value can be tested for membership in a sequence. Python has two operators `in` and `not in` that evaluate to `True` or `False` depending on whether an element appears in a sequence.  
**Slicing**. Sequences contain smaller sequences within them. A *slice* of a sequence is any contiguous span of the original sequence, designated by a pair of integers. As with the `range` constructor, the first integer indicates the starting index of the slice and the second indicates one beyond the ending index.  
In Python, sequence slicing is expressed similarly to element selection, using square brackets. A colon separates the starting and ending indices. **Any bound that is omitted is assumed to be an extreme value: 0 for the starting index, and the length of the sequence for the ending index.**  
### 2.3.5 Strings
Text values are perhaps more fundamental to computer science than even numbers. As a case in point, Python programs are written and stored as text. The native data type for text in Python is called a string, and corresponds to the constructor str.  
**String Coercion**. A string can be created from any object in Python by calling the str constructor function with an object value as its argument. This feature of strings is useful for constructing descriptive strings from objects of various types.
```python
>>> str(2) + ' is an element of ' + str(digits)
'2 is an element of [1, 8, 2, 8]'
```

## 2.4 Mutable Data
One powerful technique for creating modular programs is to incorporate data that may change state over time. In this way, a single data object can represent something that evolves independently of the rest of the program. The behavior of a changing object may be influenced by its history, just like an entity in the world. ***Adding state to data is a central ingredient of a paradigm called object-oriented programming.***  
### 2.4.1 The Object Metaphor
Objects are both information and processes, bundled together to represent the properties, interactions, and behaviors of complex things.  
Objects have *attributes*, which are named values that are part of the object. In Python, like many other programming languages, we use dot notation to designated an attribute of an object.
> `<expression>.<name>`
above, the `<expression>` evaluates to an object, and <name> is the name of an attribute of that object  
### 2.4.2 Sequence Objects
Methods also exist for inserting, sorting, and reversing lists. All of these mutation operations change the value of the list; they do not create new list objects.  
**Sharing and Identity.** Because we have been changing a single list rather than creating new lists, the object bound to the name `chinese` has also changed, because it is the same list object that was bound to `suits`!  
This behavior is new. Previously, if a name did not appear in a statement, then its value would not be affected by that statement. With mutable data, methods called on one name can affect another name at the same time.  
Lists can be copied using the `list` constructor function. Changes to one list do not affect another, unless they share structure.  

```python
>>> nest = list(suits)  # Bind "nest" to a second list with the same elements
>>> nest[0] = suits     # Create a nested list
```
According to this environment, changing the list referenced by `suits` will affect the nested list that is the first element of `nest`, but not the other elements.  

Because two lists may have the same contents but in fact be different lists, we require a means to test whether two objects are the same. Python includes two comparison operators, called `is` and `is not`, that test whether two expressions in fact evaluate to the identical object. Two objects are identical if they are equal in their current value, and any change to one will always be reflected in the other. **Identity is a stronger condition than equality.**  
**List comprehensions.** A list comprehension always creates a new list.
**Tuples**. A tuple, an instance of the built-in `tuple` type, is an **immutable sequence.** Tuples are created using a tuple literal that separates element expressions by commas. Parentheses are optional but used commonly in practice. Any objects can be placed within tuples.  
```python title="tuple"
>>> 1, 2 + 3
(1, 5)
>>> ("the", 1, ("and", "only"))
('the', 1, ('and', 'only'))
>>> type( (10, 20) )
<class 'tuple'>
```
Tuples are used implicitly in multiple assignment. **An assignment of two values to two names creates a two-element tuple and then unpacks it.**  
### 2.4.3 Dictionaries
Dictionaries are Python's built-in data type for storing and manipulating correspondence relationships. A dictionary contains key-value pairs, where both the keys and values are objects. The purpose of a dictionary is to provide an abstraction for storing and retrieving values that are indexed not by consecutive integers, but by descriptive keys.  
The dictionary type also supports various methods of iterating over the contents of the dictionary as a whole. The methods `keys`, `values`, and `items` all return iterable values.  
```python
>>> sum(numerals.values())
66
```
A list of key-value pairs can be converted into a dictionary by calling the dict constructor function.
```python
>>> dict([(3, 9), (4, 16), (5, 25)])
{3: 9, 4: 16, 5: 25}
```
Dictionaries do have some restrictions:

* **A key of a dictionary cannot be or contain a mutable value.**
* **There can be at most one value for a given key**

A useful method implemented by dictionaries is `get`, which returns either the value for a `key`, if the `key` is present, or a default value. The arguments to `get` are the **key and the default value.**
```python
>>> numerals.get('A', 0)
0
>>> numerals.get('V', 0)
5
```
Dictionaries also have a comprehension syntax analogous to those of lists. A key expression and a value expression are separated by a colon. Evaluating a dictionary comprehension creates a new dictionary object.
```python
>>> {x: x*x for x in range(3,6)}
{3: 9, 4: 16, 5: 25}
```
### 2.4.4 Local State
Lists and dictionaries have ***local state:*** they are changing values that have some particular contents at any point in the execution of a program. The word "state" implies an evolving process in which that state may change.
Functions can also have local state.   
```python 
>>> def make_withdraw(balance):
        """Return a withdraw function that draws down balance with each call."""
        def withdraw(amount):
            nonlocal balance                 # Declare the name "balance" nonlocal
            if amount > balance:
                return 'Insufficient funds'
            balance = balance - amount       # Re-bind the existing balance name
            return balance
        return withdraw
```
The `nonlocal` statement declares that whenever we change the binding of the name `balance`, the binding is changed in the first frame in which `balance` is already bound. **Recall that without the `nonlocal` statement, an assignment statement would always bind a name in the first frame of the current environment. The `nonlocal` statement indicates that the name appears somewhere in the environment other than the first (local) frame or the last (global) frame.**  
> By virtue of changing the binding for `balance`, we have changed the `withdraw` function as well.  

Ever since we first encountered nested def statements, ***we have observed that a locally defined function can look up names outside of its local frames. ==No nonlocal statement is required to access a non-local name. By contrast, only after a nonlocal statement can a function change the binding of names in these frames.==***  
By introducing `nonlocal` statements, we have created a dual role for assignment statements. Either they change local bindings, or they change nonlocal bindings. In fact, assignment statements already had a dual role: they either created new bindings or re-bound existing names. Assignment can also change the contents of lists and dictionaries. The many roles of Python assignment can obscure the effects of executing an assignment statement. It is up to you as a programmer to document your code clearly so that the effects of assignment can be understood by others.  
**Python Particulars.** This pattern of non-local assignment is a general feature of programming languages with higher-order functions and lexical scope. Most other languages do not require a nonlocal statement at all. Instead, **non-local assignment is often the default behavior of assignment statements.**
```python hl_lines="3"
1	def make_withdraw(balance):
2	    def withdraw(amount):
3	        if amount > balance:
4	            return 'Insufficient funds'
5	        balance = balance - amount
6	        return balance
7	    return withdraw
8	
9	wd = make_withdraw(20)
10	wd(5)
```
This `UnboundLocalError` appears because `balance` is assigned locally in line 5, and so Python assumes that all references to `balance` must appear in the local frame as well. This error occurs before line 5 is ever executed, implying that Python has considered line 5 in some way before executing line 3. As we study interpreter design, we will see that pre-computing facts about a function body before executing it is quite common. In this case, Python's pre-processing restricted the frame in which `balance` could appear, and thus prevented the name from being found. Adding a `nonlocal` statement corrects this error. The `nonlocal` statement did not exist in Python 2.  
### 2.4.5 The Benifits of Non-Local Assignment
Non-local assignment is an important step on our path to viewing a program as a collection of independent and autonomous objects, which interact with each other but each manage their own internal state.  
The key to correctly analyzing code with non-local assignment is to remember that only function calls can introduce new frames. Assignment statements always change bindings in existing frames. In this case, unless `make_withdraw` is called twice, there can be only one binding for `balance`.