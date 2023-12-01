---
comments: true
---

# Chapter 4: Data Processing
## 4.1 Introduction
Modern computers can process vast amounts of data representing many aspects of the world. From these big data sets, we can learn about human behavior in unprecedented ways: how language is used, what photos are taken, what topics are discussed, and how people engage with their surroundings. To process large data sets efficiently, programs are organized into pipelines of manipulations on sequential streams of data. In this chapter, we consider a suite of techniques process and manipulate sequential data streams efficiently.  
## 4.2 Implicit Sequences
A sequence can be represented without each element being stored explicitly in the memory of the computer. **That is, we can construct an object that provides access to all of the elements of some sequential dataset without computing the value of each element in advance. Instead, we compute elements on demand.**  
An example of this idea arises in the `range` container type introduced in Chapter 2. A `range` represents a consecutive, bounded sequence of integers. However, it is not the case that each element of that sequence is represented explicitly in memory. Instead, when an element is requested from a range, it is computed. Hence, we can represent very large ranges of integers without using large blocks of memory. Only the end points of the `range` are stored as part of the range object.  
```python 
>>> r = range(10000, 1000000000)
>>> r[45006230]
45016230
```
In this example, not all 999,990,000 integers in this range are stored when the range instance is constructed. Instead, the range object adds the first element 10,000 to the index 45,006,230 to produce the element 45,016,230. Computing values on demand, rather than retrieving them from an existing representation, is an example of ***lazy computation***. ***In computer science, lazy computation describes any program that delays the computation of a value until that value is needed.***  
### 4.2.1 Iterators
Python and many other programming languages provide a unified way to process elements of a container value sequentially, called an iterator. **An iterator is an object that provides sequential access to values, one by one.**  
The iterator abstraction has two components: **a mechanism for retrieving the next element in the sequence being processed and a mechanism for signaling that the end of the sequence has been reached and no further elements remain.** For any container, such as a `list` or `range`, an iterator can be obtained by calling the built-in `iter` function. The contents of the iterator can be accessed by calling the built-in `next` function.  
```python
>>> primes = [2, 3, 5, 7]
>>> type(primes)
>>> iterator = iter(primes)
>>> type(iterator)
>>> next(iterator)
2
>>> next(iterator)
3
>>> next(iterator)
5
```  
The way that Python signals that there are no more values available is to raise a `StopIteration` exception when next is called. This exception can be handled using a `try` statement.  
```python
>>> next(iterator)
7
>>> next(iterator)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>> try:
        next(iterator)
    except StopIteration:
        print('No more values')
No more values
```
An iterator **maintains local state to represent its position in a sequence. Each time next is called, that position advances.** Two separate iterators can track two different positions in the same sequence. However, two names for the same iterator will share a position, because they share the same value.  
**Calling iter on an iterator will return that iterator, not a copy.** This behavior is included in Python so that a programmer can call iter on a value to get an iterator without having to worry about whether it is an iterator or a container.  
The usefulness of iterators is derived from the fact that the underlying series of data for an iterator may not be represented explicitly in memory. **An iterator provides a mechanism for considering each of a series of values in turn, but all of those elements do not need to be stored simultaneously. Instead, when the next element is requested from an iterator, that element may be computed on demand instead of being retrieved from an existing memory source.**  
***iterators are only required to compute the next element of the series, in order, each time another element is requested. While not as flexible as accessing arbitrary elements of a sequence (called ==random access==), ==sequential access== to sequential data is often sufficient for data processing applications.***  
### 4.2.2 Iterables
Any value that can produce iterators is called an iterable value. In Python, **an iterable value is anything that can be passed to the built-in `iter` function.** Iterables include sequence values such as strings and tuples, as well as other containers such as sets and dictionaries. **Iterators are also iterables**, because they can be passed to the iter function.  
If a dictionary changes in structure because a key is added or removed, then all iterators become invalid and future iterators may exhibit arbitrary changes to the order their contents. On the other hand, changing the value of an existing key does not change the order of the contents or invalidate iterators.  
### 4.2.3 Built-in Iterators
Several built-in functions take as arguments iterable values and return iterators. These functions are used extensively for lazy sequence processing.  
The `map` function is lazy: calling it does not perform the computation required to compute elements of its result. Instead, an iterator object is created that can return results if queried using `next`.   
```python
>>> def double_and_print(x):
        print('***', x, '=>', 2*x, '***')
        return 2*x
>>> s = range(3, 7)
>>> doubled = map(double_and_print, s)  # double_and_print not yet called
>>> next(doubled)                       # double_and_print called once
*** 3 => 6 ***
6
>>> next(doubled)                       # double_and_print called again
*** 4 => 8 ***
8
>>> list(doubled)                       # double_and_print called twice more
*** 5 => 10 ***
*** 6 => 12 ***
[10, 12]
```
The `filter` function returns an iterator over, `zip`, and `reversed` functions also return iterators. they are all special iterators.
### 4.2.4 For Statements
***The `for` statement in Python operates on iterators. ==Objects are iterable (an interface) if they have an `__iter__` method that returns an iterator.==*** Iterable objects can be the value of the `<expression>` in the header of a `for` statement:  
```python
for <name> in <expression>:
    <suite>
```
***To execute a `for` statement, Python evaluates the header `<expression>`, which must yield an iterable value. Then, the `__iter__` method is invoked on that value. Until a StopIteration exception is raised, Python repeatedly invokes the `__next__` method on that iterator and binds the result to the `<name>` in the `for` statement. Then, it executes the `<suite>`.***   
```python
>>> counts = [1, 2, 3]
>>> for item in counts:
        print(item)
1
2
3
```
In the above example, the `counts` list returns an iterator from its `__iter__()` method. The for statement then calls that iterator's `__next__()` method repeatedly, and assigns the returned value to `item` each time. **This process continues until the iterator raises a `StopIteration` exception, at which point execution of the for statement concludes.**
```python
>>> items = counts.__iter__()
>>> try:
        while True:
            item = items.__next__()
            print(item)
    except StopIteration:
        pass
1
2
3
```
Above, the iterator returned by invoking the `__iter__` method of `counts` is bound to a name `items` so that it can be queried for each element in turn. The handling clause for the `StopIteration` exception does nothing, but handling the exception provides a control mechanism for exiting the `while` loop.

**To use an iterator in a for loop**, the iterator must also have an `__iter__` method. suggest that an iterator have an `__iter__` method that **returns the iterator itself**, **so that all iterators are iterable.**  
### 4.2.5 Generators and Yield Statements
Generators allow us to define more complicated iterations by leveraging the features of the Python interpreter.  
A ==***generator*** is an iterator== returned by a special class of function called a ***generator function***. Generator functions are distinguished from regular functions in that rather than containing `return` statements in their body, they use `yield` statement to ==**return elements of a series**==.  
Generators do not use attributes of an object to track their progress through a series. Instead, they control the execution of the generator function, which runs until the next `yield` statement is executed each time the generator's `__next__` method is invoked. 
```python 
>>> def letters_generator():
        current = 'a'
        while current <= 'd':
            yield current
            current = chr(ord(current)+1)
>>> for letter in letters_generator():
        print(letter)
a
b
c
d
```
Even though we never explicitly defined `__iter__` or `__next__` methods, the yield statement indicates that we are defining a generator function. When called, a generator function doesn't return a particular yielded value, but instead a generator (which is a type of iterator) that itself can return the yielded values. A generator object has `__iter__` and `__next__` methods, and each call to `__next__` continues execution of the generator function from wherever it left off previously until another `yield` statement is executed.  
The first time `__next__` is called, the program executes statements from the body of the `letters_generator` function until it encounters the `yield` statement. ==**Then, it pauses and returns the value of current. `yield` statements do not destroy the newly created environment, they preserve it for later. When `__next__` is called again, execution resumes where it left off.**== The values of current and of any other bound names in the scope of letters_generator are preserved across subsequent calls to __next__.  
We can walk through the generator by manually calling `____next__()`:  
```python
>>> letters = letters_generator()
>>> type(letters)
<class 'generator'>
>>> letters.__next__()
'a'
>>> letters.__next__()
'b'
>>> letters.__next__()
'c'
>>> letters.__next__()
'd'
>>> letters.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```
The generator does not start executing any of the body statements of its generator function until the first time `__next__` is invoked. The generator raises a StopIteration exception whenever its generator function returns.  
### 4.2.6 Iterable Interface
An object is iterable if it returns an iterator when its `__iter__` method is invoked. Iterable values represent data collections  
Many built-in functions in Python take iterable arguments and return iterators. The `map` function, for example, takes a function and an iterable. It returns an iterator over the result of applying the function argument to each element in the iterable argument.  

### 4.2.7  Creating Iterables with Yield
```python 
>>> def all_pairs(s):
        for item1 in s:
            for item2 in s:
                yield (item1, item2)
>>> list(all_pairs([1, 2, 3]))
[(1, 1), (1, 2), (1, 3), (2, 1), (2, 2), (2, 3), (3, 1), (3, 2), (3, 3)]
```
Sequences are not themselves iterators, but instead iterable objects. The iterable interface in Python consists of a single message, `__iter__`, that returns an iterator. The built-in sequence types in Python return new instances of iterators when their `__iter__` methods are invoked. **If an iterable object returns a fresh instance of an iterator each time `__iter__` is called, then it can be iterated over multiple times.**  
New iterable classes can be defined by implementing the iterable interface. For example, the *iterable* LettersWithYield class below returns a new iterator over letters each time __iter__ is invoked.  
```python 
>>> class LettersWithYield:
        def __init__(self, start='a', end='e'):
            self.start = start
            self.end = end
        def __iter__(self):
            next_letter = self.start
            while next_letter < self.end:
                yield next_letter
                next_letter = chr(ord(next_letter)+1)
```
The `__iter__` method is a generator function; it returns a generator object that yields the letters `'a'` through `'d'` and then stops. Each time we invoke this method, a new generator starts a fresh pass through the sequential data.  
```python
>>> letters = LettersWithYield()
>>> list(all_pairs(letters))[:5]
[('a', 'a'), ('a', 'b'), ('a', 'c'), ('a', 'd'), ('b', 'a')]
```
### 4.2.8 Iterator Interface
The LetterIter class below iterates over an underlying series of letters from some start letter up to but not including some end letter. The instance attribute `next_letter` stores the next letter to be returned. The `__next__` method returns this letter and uses it to compute a new next_letter.  
```python 
>>> class LetterIter:
        """An iterator over letters of the alphabet in ASCII order."""
        def __init__(self, start='a', end='e'):
            self.next_letter = start
            self.end = end
        def __next__(self):
            if self.next_letter == self.end:
                raise StopIteration
            letter = self.next_letter
            self.next_letter = chr(ord(letter)+1)
            return letter
```
Using this class, we can access letters in sequence using either the `__next__` method or the built-in `next` function, which invokes `__next__` on its argument.  
```python
>>> letter_iter = LetterIter()
>>> letter_iter.__next__()
'a'
>>> letter_iter.__next__()
'b'
>>> next(letter_iter)
'c'
>>> letter_iter.__next__()
'd'
>>> letter_iter.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 12, in next
StopIteration
```
Iterators are mutable: they track the position in some underlying sequence of values as they progress.  
Iterators also allow us to represent infinite series by implementing a `__next__` method that never raises a `StopIteration` exception. For example, the Positives class below iterates over the infinite series of positive integers. The built-in next function in Python invokes the `__next__` method on its argument.  
```python 
>>> class Positives:
        def __init__(self):
            self.next_positive = 1;
        def __next__(self):
            result = self.next_positive
            self.next_positive += 1
            return result
>>> p = Positives()
>>> next(p)
1
>>> next(p)
2
>>> next(p)
3
```