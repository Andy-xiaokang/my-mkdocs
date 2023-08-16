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

## 2.5 Object-Oriented Programming
### 2.5.1 Objects and Classes
A class serves as a template for all objects whose type is that class. ***Every object is an instance of some particular class.***  
The act of creating a new object instance is known as instantiating the class. The syntax in Python for instantiating a class is identical to the syntax of calling a function. 
The attributes specific to a particular object, as opposed to all objects of a class, are called ***instance attributes.*** In the broader programming community, instance attributes may also be called ***fields, properties, or instance variables.***  
Functions that operate on the object or perform object-specific computations are called methods. The return values and side effects of a method can depend upon and change other attributes of the object. We say that methods are invoked on a particular object.  
### 2.5.2 Defining Classes
User-defined classes are created by class statements, which consist of a single clause. A class statement defines the class name, then includes a suite of statements to define the attributes of the class:
```python 
class <name>:
    <suite>
```
When a class statement is executed, a new class is created and bound to `<name>` in the first frame of the current environment. The suite is then executed. Any names bound within the `<suite>` of a class statement, through `def` or assignment statements, create or modify attributes of the class.  
The method that initializes objects has a special name in Python, `__init__` (two underscores on each side of the word "init"), and is called the constructor for the class.  
```python 
>>> class Account:
        def __init__(self, account_holder):
            self.balance = 0
            self.holder = account_holder
```
The `__init__` method for Account has two formal parameters. The first one, ***self, is bound to the newly created Account object.*** The second parameter, `account_holder`, is bound to the argument passed to the class when it is called to be instantiated.
**Identity.** Each new account instance has its own balance attribute, the value of which is independent of other objects of the same class.
**Methods.** Object methods are also defined by a def statement in the suite of a class statement. Below, deposit and withdraw are both defined as methods on objects of the Account class.  
```python
>>> class Account:
        def __init__(self, account_holder):
            self.balance = 0
            self.holder = account_holder
        def deposit(self, amount):
            self.balance = self.balance + amount
            return self.balance
        def withdraw(self, amount):
            if amount > self.balance:
                return 'Insufficient funds'
            self.balance = self.balance - amount
            return self.balance
```
The function value that is created by a `def` statement within a `class` statement is bound to the declared name, ***but bound locally within the class as an attribute.*** That value is invoked as a method using dot notation from an instance of the class. Each method definition again includes a special first parameter self, which is bound to the object on which the method is invoked.  
```python
>>> spock_account = Account('Spock')
>>> spock_account.deposit(100)
100
>>> spock_account.withdraw(90)
10
>>> spock_account.withdraw(90)
'Insufficient funds'
>>> spock_account.holder
'Spock'
```
When a method is invoked via dot notation, the object itself (bound to `spock_account`, in this case) plays a dual role. First, it determines what the name `withdraw` means; `withdraw` is not a name in the environment, but instead a name that is local to the `Account` class. Second, it is bound to the first parameter `self` when the `withdraw` method is invoked.  
### 2.5.3 Message Passing and Dot Expressions
**Dot expressions.** The code fragment `spock_account.deposit` is called a ***dot expression***. A dot expression consists of an expression, a dot, and a name:   
`<expression> . <name>`  
A dot expression evaluates to the value of the attribute with the given `<name>`, for the object that is the value of the `<expression>`.
The built-in function `getattr` also returns an attribute for an object by name. It is the function equivalent of dot notation. Using `getattr`, we can look up an attribute using a string, just as we did with a dispatch dictionary.  
```python
>>> getattr(spock_account, 'balance')
10
```
We can also test whether an object has a named attribute with `hasattr`.  
```python
>>> hasattr(spock_account, 'deposit')
True
```
***The attributes of an object include all of its instance attributes, along with all of the attributes (including methods) defined in its class.*** Methods are attributes of the class that require special handling.  
**Methods and functions.** ==When a method is invoked on an object, that object is implicitly passed as the first argument to the method.== That is, the object that is the value of the `<expression>` to the left of the dot is passed automatically as the first argument to the method named on the right side of the dot expression. ==***As a result, the object is bound to the parameter self.***==  
To achieve automatic `self` binding, Python distinguishes between functions, which we have been creating since the beginning of the text, and *bound methods*, which couple together a function and the object on which that method will be invoked. A bound method value is already associated with its first argument, the instance on which it was invoked, which will be named `self` when the method is called.  
We can see the difference in the interactive interpreter by calling `type` on the returned values of dot expressions. ***As an attribute of a class, a method is just a function, but as an attribute of an instance, it is a bound method:*** 
```python
>>> type(Account.deposit)
<class 'function'>
>>> type(spock_account.deposit)
<class 'method'>
```
**Naming Conventions.** Class names are conventionally written using the CapWords convention (also called CamelCase because the capital letters in the middle of a name look like humps). Method names follow the standard convention of naming functions using lowercased words separated by underscores.
### 2.5.4 Class Attributes
Some attribute values are shared across all objects of a given class. Such attributes are associated with the class itself, rather than any individual instance of the class.   
**Attribute names.** We have introduced enough complexity into our object system that we have to specify how names are resolved to particular attributes. After all, we could easily have a class attribute and an instance attribute with the same name.  
`<expression> . <name>`  
1. Evaluate the `<expression>` to the left of the dot, which yields the `object` of the dot expression.  
2. `<name>` is matched against the instance attributes of that object; if an attribute with that name exists, its value is returned.  
3. If `<name>` does not appear among instance attributes, then `<name>` is looked up in the class, which yields a class attribute value.  
4. That value is returned unless it is a function, in which case a bound method is returned instead.  

In this evaluation procedure, instance attributes are found before class attributes, just as local names have priority over global in an environment.  
**Attribute assignment.** All assignment statements that contain a dot expression on their left-hand side affect attributes for the object of that dot expression. If the object is an instance, then assignment sets an instance attribute. If the object is a class, then assignment sets a class attribute. As a consequence of this rule, assignment to an attribute of an object cannot affect the attributes of its class. The examples below illustrate this distinction.  
If we assign to the named attribute `interest` of an account instance, we create a new instance attribute that has the same name as the existing class attribute.  
### 2.5.5 Inheritance
A subclass ***inherits*** the attributes of its ***base class***, but may ***override*** certain attributes, including certain methods. With inheritance, we only specify what is different between the ***subclass*** and the ***base class***. Anything that we leave unspecified in the subclass is automatically assumed to behave just as it would for the base class.  
Inheritance is meant to represent ***is-a*** relationships between classes, which contrast with ***has-a*** relationships. A checking account ***is-a*** specific type of account, so having a CheckingAccount inherit from Account is an appropriate use of inheritance. On the other hand, a bank has-a list of bank accounts that it manages, so neither should inherit from the other.
### 2.5.6 Using Inheritance
```python
>>> class Account:
        """A bank account that has a non-negative balance."""
        interest = 0.02
        def __init__(self, account_holder):
            self.balance = 0
            self.holder = account_holder
        def deposit(self, amount):
            """Increase the account balance by amount and return the new balance."""
            self.balance = self.balance + amount
            return self.balance
        def withdraw(self, amount):
            """Decrease the account balance by amount and return the new balance."""
            if amount > self.balance:
                return 'Insufficient funds'
            self.balance = self.balance - amount
            return self.balance
```
A full implementation of `CheckingAccount` appears below. We specify inheritance by placing an expression that evaluates to the base class in parentheses after the class name.  
```python
>>> class CheckingAccount(Account):
        """A bank account that charges for withdrawals."""
        withdraw_charge = 1
        interest = 0.01
        def withdraw(self, amount):
            return Account.withdraw(self, amount + self.withdraw_charge)
```
When Python resolves a name in a dot expression that is not an attribute of the instance, it looks up the name in the class. In fact, the act of "looking up" a name in a class tries to find that name in every base class in the inheritance chain for the original object's class. We can define this procedure recursively. To look up a name in a class.  
1. If it names an attribute in the class, return the attribute value.  
2. Otherwise, look up the name in the base class, if there is one.

In the case of `deposit`, Python would have looked for the name first on the instance, and then in the `CheckingAccount` class. Finally, it would look in the `Account` class, where `deposit` is defined.  

## 2.7 Object Abstraction
A central concept in object abstraction is a ***generic function***, which is a function that can accept values of multiple different types. We will consider three different techniques for implementing generic functions: ***shared interfaces, type dispatching, and type coercion.*** In the process of building up these concepts, we will also discover features of the Python object system that support the creation of generic functions.  
### 2.7.1 String Conversion
To represent data effectively, an object value should behave like the kind of data it is meant to represent, including producing a string representation of itself. String representations of data values are especially important in an interactive language such as Python that automatically displays the string representation of the values of expressions in an interactive session.
Python stipulates that all objects should produce two different string representations: ***one that is human-interpretable text and one that is a Python-interpretable expression. The constructor function for strings, str, returns a human-readable string.*** Where possible, ***the repr function ==returns a Python expression that evaluates to an equal object==.*** The docstring for repr explains this property:
```python
repr(object) -> string

Return the canonical string representation of the object.
For most object types, eval(repr(object)) == object.
```
The result of calling repr on the value of an expression is what Python prints in an interactive session. In cases where no representation exists that evaluates to the original value, Python typically produces a description surrounded by angled brackets.
```python
>>> 12e12
12000000000000.0
>>> print(repr(12e12))
12000000000000.0
>>> repr(min)
'<built-in function min>'
```
The str `constructor` often coincides with `repr`, but provides a more interpretable text representation in some cases. For instance, we see a difference between `str` and `repr` with dates.  
```python
>>> from datetime import date
>>> tues = date(2011, 9, 12)
>>> repr(tues)
'datetime.date(2011, 9, 12)'
>>> str(tues)
'2011-09-12'
```
Defining the `repr` function presents a new challenge: we would like it to apply correctly to all data types, even those that did not exist when `repr` was implemented. We would like it to be a ***generic or polymorphic function***, one that can be applied to many (*poly*) different forms (*morph*) of data.  
The object system provides an elegant solution in this case: the `repr` function always invokes a method called `__repr__` on its argument.  
```python
>>> tues.__repr__()
'datetime.date(2011, 9, 12)'
```
By implementing this same method in user-defined classes, we can extend the applicability of `repr` to any class we create in the future. This example highlights another benefit of dot expressions in general, that they provide a mechanism for extending the domain of existing functions to new object types.
These polymorphic functions are examples of a more general principle: ==**certain functions should apply to multiple data types. Moreover, one way to create such a function is to use a shared attribute name with a different definition in each class.**==
### 2.7.2 Special Methods
In Python, certain special names are invoked by the Python interpreter in special circumstances. For instance, ==the `__init__` method of a class is automatically invoked whenever an object is constructed. The `__str__` method is invoked automatically when printing, and `__repr__` is invoked in an interactive session to display values.==
**True and false values.** We saw previously that numbers in Python have a truth value; more specifically, 0 is a false value and all other numbers are true values. In fact, all objects in Python have a truth value. By default, objects of user-defined classes are considered to be true, but the special `__bool__` method can be used to override this behavior. If an object defines the `__bool__` method, then Python calls that method to determine its truth value.
As an example, suppose we want a bank account with 0 balance to be false. We can add a `__bool__` method to the `Account` class to create this behavior. 
```python
>>> Account.__bool__ = lambda self: self.balance != 0
```
We can call the `bool` constructor to see the truth value of an object, **and we can use any object in a boolean context.**
```python
>>> bool(Account('Jack'))
False
>>> if not Account('Jack'):
        print('Jack has nothing')
Jack has nothing
```
**Sequence operations.** We have seen that we can call the len function to determine the length of a sequence.  
```python
>>> len('Go Bears!')
9
```
The `len` function invokes the `__len__` method of its argument to determine its length. All built-in sequence types implement this method.  
```python
>>> 'Go Bears!'.__len__()
9
```
==***Python uses a sequence's length to determine its truth value, if it does not provide a `__bool__` method. Empty sequences are false, while non-empty sequences are true.***==  
```python
>>> bool('')
False
>>> bool([])
False
>>> bool('Go Bears!')
True
>>> bool(range(0))
```
The `__getitem__` method is invoked by the element selection operator, but it can also be invoked directly.  
```python
>>> 'Go Bears!'[3]
'B'
>>> 'Go Bears!'.__getitem__(3)
'B'
```
**Callable objects.** In Python, functions are first-class objects, so they can be passed around as data and have attributes like any other object. Python also allows us to define objects that can be "called" like functions by including a `__call__` method. With this method, we can define a class that behaves like a higher-order function.  
```python
>>> def make_adder(n):
        def adder(k):
            return n + k
        return adder
>>> add_three = make_adder(3)
>>> add_three(4)
7
```
We can create an `Adder` class that defines a `__call__` method to provide the same functionality.  
```python
>>> class Adder(object):
        def __init__(self, n):
            self.n = n
        def __call__(self, k):
            return self.n + k
>>> add_three_obj = Adder(3)
>>> add_three_obj(4)
7
```
Here, the `Adder` class behaves like the `make_adder` higher-order function, and the `add_three_obj` object behaves like the `add_three` function. We have further blurred the line between data and functions.  

**Arithmetic**. Special methods can also define the behavior of built-in operators applied to user-defined objects. In order to provide this generality, Python follows specific protocols to apply each operator. For example, to evaluate expressions that contain the + operator, Python checks for special methods on both the left and right operands of the expression. First, Python checks for an `__add__` method on the value of the left operand, then checks for an `__radd__` method on the value of the right operand. If either is found, that method is invoked with the value of the other operand as its argument.   
### 2.7.3 Multiple Representations
```python
>>> class Number:
        def __add__(self, other):
            return self.add(other)
        def __mul__(self, other):
            return self.mul(other)
```
The `Complex` class inherits from `Number` and describes arithmetic for complex numbers.  
```python
>>> class Complex(Number):
        def add(self, other):
            return ComplexRI(self.real + other.real, self.imag + other.imag)
        def mul(self, other):
            magnitude = self.magnitude * other.magnitude
            return ComplexMA(magnitude, self.angle + other.angle)
```
This implementation assumes that two classes exist for complex numbers, corresponding to their two natural representations:  

* `ComplexRI` constructs a complex number from real and imaginary parts.
* `ComplexMA` constructs a complex number from a magnitude and angle.

**Interfaces.**  ==**An interface is a set of shared attribute names, along with a specification of their behavior.**==  
**Properties.** The requirement that two or more attribute values maintain a fixed relationship with each other is a new problem. One solution is to store attribute values for only one representation and compute the other representation whenever it is needed.  
Python has a simple feature for computing attributes on the fly from zero-argument functions. ==The `@property` decorator allows functions to be called without call expression syntax (parentheses following an expression). The `ComplexRI` class stores `real` and `imag` attributes and computes `magnitude` and `angle` on demand.==  
```python
>>> from math import atan2
>>> class ComplexRI(Complex):
        def __init__(self, real, imag):
            self.real = real
            self.imag = imag
        @property
        def magnitude(self):
            return (self.real ** 2 + self.imag ** 2) ** 0.5
        @property
        def angle(self):
            return atan2(self.imag, self.real)
        def __repr__(self):
            return 'ComplexRI({0:g}, {1:g})'.format(self.real, self.imag)
```
As a result of this implementation, all four attributes needed for complex arithmetic can be accessed without any call expressions, and changes to `real` or `imag` are reflected in the `magnitude` and `angle`.  
```python
>>> ri = ComplexRI(5, 12)
>>> ri.real
5
>>> ri.magnitude
13.0
>>> ri.real = 9
>>> ri.real
9
>>> ri.magnitude
15.0
```
Similarly, the `ComplexMA` class stores `magnitude` and `angle`, but computes `real` and `imag` whenever those attributes are looked up.  
```python
>>> from math import sin, cos, pi
>>> class ComplexMA(Complex):
        def __init__(self, magnitude, angle):
            self.magnitude = magnitude
            self.angle = angle
        @property
        def real(self):
            return self.magnitude * cos(self.angle)
        @property
        def imag(self):
            return self.magnitude * sin(self.angle)
        def __repr__(self):
            return 'ComplexMA({0:g}, {1:g} * pi)'.format(self.magnitude, self.angle/pi)
```  
Changes to the magnitude or angle are reflected immediately in the `real` and `imag` attributes.  
```python
>>> ma = ComplexMA(2, pi/2)
>>> ma.imag
2.0
>>> ma.angle = pi
>>> ma.real
-2.0
```  
### 2.7.4 Generic Functions
Generic functions are methods or functions that apply to arguments of different types. Using interfaces and message passing is only one of several methods used to implement generic functions. We will consider two others in this section: **type dispatching and type coercion.**  
**type dispatching** The `__add__` method considers two cases. First, if two arguments have the same type tag, then it assumes that add method of the first can take the second as an argument. Otherwise, it checks whether a dictionary of cross-type implementations, called adders, contains a function that can add arguments of those type tags. If there is such a function, the cross_apply method finds and applies it. The `__mul__` method has a similar structure.
```python
>>> class Number:
        def __add__(self, other):
            if self.type_tag == other.type_tag:
                return self.add(other)
            elif (self.type_tag, other.type_tag) in self.adders:
                return self.cross_apply(other, self.adders)
        def __mul__(self, other):
            if self.type_tag == other.type_tag:
                return self.mul(other)
            elif (self.type_tag, other.type_tag) in self.multipliers:
                return self.cross_apply(other, self.multipliers)
        def cross_apply(self, other, cross_fns):
            cross_fn = cross_fns[(self.type_tag, other.type_tag)]
            return cross_fn(self, other)
        adders = {("com", "rat"): add_complex_and_rational,
                  ("rat", "com"): add_rational_and_complex}
        multipliers = {("com", "rat"): mul_complex_and_rational,
                       ("rat", "com"): mul_rational_and_complex}
```
**Coercion.** In general, we can implement this idea by designing coercion functions that transform an object of one type into an equivalent object of another type. Here is a typical coercion function, which transforms a rational number to a complex number with zero imaginary part:  
```python
>>> def rational_to_complex(r):
        return ComplexRI(r.numer/r.denom, 0)
```
The `coerce` method returns two values with the same type tag. It inspects the type tags of its arguments, compares them to entries in the `coercions` dictionary, and converts one argument to the type of the other using `coerce_to`. Only one entry in `coercions` is necessary to complete our cross-type arithmetic system, replacing the four cross-type functions in the type-dispatching version of `Number`.  
```python
>>> class Number:
        def __add__(self, other):
            x, y = self.coerce(other)
            return x.add(y)
        def __mul__(self, other):
            x, y = self.coerce(other)
            return x.mul(y)
        def coerce(self, other):
            if self.type_tag == other.type_tag:
                return self, other
            elif (self.type_tag, other.type_tag) in self.coercions:
                return (self.coerce_to(other.type_tag), other)
            elif (other.type_tag, self.type_tag) in self.coercions:
                return (self, other.coerce_to(self.type_tag))
        def coerce_to(self, other_tag):
            coercion_fn = self.coercions[(self.type_tag, other_tag)]
            return coercion_fn(self)
        coercions = {('rat', 'com'): rational_to_complex}
```  
## 2.8 Efficiency  
### 2.8.1 Measuring Efficiency  
We can measure this inefficiency. The higher-order `count` function returns an equivalent function to its argument that also maintains a `call_count` attribute. In this way, we can inspect just how many times `fib` is called.  
```python
>>> def count(f):
        def counted(*args):
            counted.call_count += 1
            return f(*args)
        counted.call_count = 0
        return counted  
```
The higher-order `count_frames` function tracks `open_count`, the number of calls to the function f that have not yet returned. The `max_count` attribute is the maximum value ever attained by `open_count`, and it corresponds to the maximum number of frames that are ever simultaneously active during the course of computation.  
```python
>>> def count_frames(f):
        def counted(*args):
            counted.open_count += 1
            counted.max_count = max(counted.max_count, counted.open_count)
            result = f(*args)
            counted.open_count -= 1
            return result
        counted.open_count = 0
        counted.max_count = 0
        return counted

>>> fib = count_frames(fib)
>>> fib(19)
4181
>>> fib.open_count
0
>>> fib.max_count
19
>>> fib(24)
46368
>>> fib.max_count
24
```  
### 2.8.2 Memoization
Memoization can be expressed naturally as a higher-order function, which can also be used as a decorator. The definition below creates a *cache* of previously computed results, indexed by the arguments from which they were computed. The use of a dictionary requires that the argument to the memoized function be immutable.  
```python
>>> def memo(f):
        cache = {}
        def memoized(n):
            if n not in cache:
                cache[n] = f(n)
            return cache[n]
        return memoized
```

## 2.9 Recursive Objects
Objects can have other objects as attribute values. When an object of some class has an attribute value of that same class, it is a recursive object.  
### 2.9.1 Linked List Class
We can now implement a class with the same behavior. In this version, we will define its behavior using special method names that allow our class to work with the built-in `len` function and element selection operator (square brackets or `operator.getitem`) in Python. These built-in functions invoke special method names of a class: length is computed by `__len__` and element selection is computed by `__getitem__`. The empty linked list is represented by an empty tuple, which has length 0 and no elements. 

=== "Class Link"
    ```python
    >>> class Link:
            """A linked list with a first element and the rest."""
            empty = ()
            def __init__(self, first, rest=empty):
                assert rest is Link.empty or isinstance(rest, Link)
                self.first = first
                self.rest = rest
            def __getitem__(self, i):
                if i == 0:
                    return self.first
                else:
                    return self.rest[i-1]
            def __len__(self):
                return 1 + len(self.rest)
    >>> s = Link(3, Link(4, Link(5)))
    >>> len(s)
    3
    >>> s[1]
    4
    ```
=== "Link Expression"
    ```python
    >>> def link_expression(s):
            """Return a string that would evaluate to s."""
            if s.rest is Link.empty:
                rest = ''
            else:
                rest = ', ' + link_expression(s.rest)
            return 'Link({0}{1})'.format(s.first, rest)
    >>> link_expression(s)
    'Link(3, Link(4, Link(5)))'
    ```
=== "Extend Link"
    ```python
    >>> def extend_link(s, t):
            if s is Link.empty:
                return t
            else:
                return Link(s.first, extend_link(s.rest, t))
    >>> extend_link(s, s)
    Link(3, Link(4, Link(5, Link(3, Link(4, Link(5))))))
    >>> Link.__add__ = extend_link
    >>> s + s
    Link(3, Link(4, Link(5, Link(3, Link(4, Link(5))))))
    ```
=== "Map Link"
    ```python
    >>> def map_link(f, s):
            if s is Link.empty:
                return s
            else:
                return Link(f(s.first), map_link(f, s.rest))
    >>> map_link(square, s)
    Link(9, Link(16, Link(25)))
    ```
=== "filter_link"
    ```python
    >>> def filter_link(f, s):
        if s is Link.empty:
            return s
        else:
            filtered = filter_link(f, s.rest)
            if f(s.first):
                return Link(s.first, filtered)
            else:
                return filtered
    >>> odd = lambda x: x % 2 == 1
    >>> map_link(square, filter_link(odd, s))
    Link(9, Link(25))
    >>> [square(x) for x in [3, 4, 5] if odd(x)]
    [9, 25]
    ```
The definitions of `__len__` and `__getitem__` are in fact recursive. The built-in Python function len invokes a method called `__len__` when applied to a user-defined object argument. Likewise, the element selection operator invokes a method called `__getitem__`. Thus, bodies of these two methods will call themselves indirectly. For `__len__`, the base case is reached when self.rest evaluates to the empty tuple, Link.empty, which has a length of 0.  
The built-in `isinstance` function returns whether the first argument has a type that is or inherits from the second argument. `isinstance(rest, Link)` is true if `rest` is a `Link` instance or an instance of some sub-class of `Link`.  
### 2.9.2 Tree Class
**Internal values.** Previously, we defined trees in such a way that all values appeared at the leaves of the tree. It is also common to define trees that have internal values at the roots of each subtree. An internal value is called an label in the tree. The Tree class below represents such trees, in which each tree has a sequence of branches that are also trees.  

```python
>>> class Tree:
        def __init__(self, label, branches=()):
            self.label = label
            for branch in branches:
                assert isinstance(branch, Tree)
            self.branches = branches
        def __repr__(self):
            if self.branches:
                return 'Tree({0}, {1})'.format(self.label, repr(self.branches))
            else:
                return 'Tree({0})'.format(repr(self.label))
        def is_leaf(self):
            return not self.branches
```
### 2.9.3 Sets
In addition to the list, tuple, and dictionary, Python has a fourth built-in container type called a set. Set literals follow the mathematical notation of elements enclosed in braces. Duplicate elements are removed upon construction. Sets are unordered collections, and so the printed ordering may differ from the element ordering in the set literal.  
```python
>>> s = {3, 2, 1, 4, 4}
>>> s
{1, 2, 3, 4}
```
Python sets support a variety of operations, including membership tests, length computation, and the standard set operations of union and intersection  
```python
>>> 3 in s
True
>>> len(s)
4
>>> s.union({1, 5})
{1, 2, 3, 4, 5}
>>> s.intersection({6, 5, 4, 3})
{3, 4}
```