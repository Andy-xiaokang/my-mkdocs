# Chapter 3: Interpreting Computer Programs
## [3.2 Functional Programming](http://www.composingprograms.com/pages/32-functional-programming.html)
### [scheme specification](https://inst.eecs.berkeley.edu/~cs61a/su20/articles/scheme-spec.html)
### [Scheme Built-In Procedure Reference](https://inst.eecs.berkeley.edu/~cs61a/su20/articles/scheme-builtins.html)
## 3.3 Exceptions  
*Exceptions*, the topic of this section, provides a general mechanism for adding error-handling logic to programs. *Raising an exception* is a technique for interrupting the normal flow of execution in a program, signaling that some exceptional circumstance has arisen, and returning directly to an enclosing part of the program that was designated to react to that circumstance. The Python interpreter raises an exception each time it detects an error in an expression or statement. Users can also raise exceptions with `raise` and `assert` statements.  
**Raising exceptions.** An exception is a object instance with a class that inherits, either directly or indirectly, from the `BaseException` class. The `assert` statement introduced in Chapter 1 raises an exception with the class `AssertionError`. In general, any exception instance can be raised with the `raise` statement. The general form of raise statements are described in the Python docs. The most common use of `raise` constructs an exception instance and raises it.  
**Handling exceptions.** An exception can be handled by an enclosing `try` statement. A `try` statement consists of multiple clauses; the first begins with `try` and the rest begin with `except`:  

```python
try:
    <try suite>
except <exception class> as <name>:
    <except suite>
...
```
The `<try suite>` is always executed immediately when the `try` statement is executed. Suites of the except clauses are only executed when an exception is raised during the course of executing the `<try suite>`. Each except clause specifies the particular class of exception to handle. For instance, if the `<exception class>` is AssertionError, then any instance of a class inheriting from AssertionError that is raised during the course of executing the `<try suite>` will be handled by the following `<except suite>`. Within the `<except suite>`, the identifier `<name>` is bound to the exception object that was raised, but this binding does not persist beyond the `<except suite>`.
```python
>>> try:
        x = 1/0
    except ZeroDivisionError as e:
        print('handling a', type(e))
        x = 0
handling a <class 'ZeroDivisionError'>
>>> x
0
```