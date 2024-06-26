---
comments: true
---

## lecture 1

![截屏2023-12-25 21.29.37](https://s2.loli.net/2023/12/25/po7EA2KRsGaiYUX.png)
![截屏2023-12-25 21.46.04](https://s2.loli.net/2023/12/25/Z8gQ1W9UxDGYoj5.png)
variable name represents a location in memory | variable name is an alias of a M register  

## lecture 7
* **abstract data type (ADT)**: A specification of a collection of data and the operations that can be performed on it. 
    - Describes *what* a collection does, not *how* it does it.
* we don't know exactly how a stack or queue is implemented, and we don't need to. 
    - we just need to understand the idea of the collection and what operations it can perform.
   
## lecture 13
![20240115211522](https://s2.loli.net/2024/01/15/mwTfSWHRMFzP3VU.png)
![20240116001226](https://s2.loli.net/2024/01/16/5ewQtAxfoTcZghb.png)
![20240115212131](https://s2.loli.net/2024/01/15/Et8MJTNlhBaoxQu.png)
 
* **In C++** when pass by value, the argument will copy the value passed in.  
when pass by reference, the argument and the variable passed in is the same thing(the same M register in the memory).  
* **in Java** there is only one type **pass by value**, when pass the primitive type we pass the value of the data type; when pass object, we pass the address(reference) of the object, in this case, we called "pass by reference", but actually, there is only pass by value, we divide the pass circumstance into two type.  

|variable name| address in memory|
|:--:|:--:|
|(front)(list)|OX...|
||...|

***

=== "non-pointer" 

    ```C++
    void foo() {
        Date d1;
        d1.month = 7;
        d1.day = 13;
        // d1 is thrown away
    }
    ```
=== "pointer"

    ```C++ 
    void foo() {
        Date* d1 = new Date();
        d1->month = 7;  
        (*d1).month = 7; // -> = (*).   operator 
        d1->day = 13;
        // d1 is not thrown away, let user manage the memory self
    } 
    ```
![20240116014248](https://s2.loli.net/2024/01/16/5kHM8cWL4XEvgR3.png)

## lecture 14
![20240116152007](https://s2.loli.net/2024/01/16/vFQNSnZ1tlIMche.png)
![20240116155221](https://s2.loli.net/2024/01/16/OcANMgjUb1qfFhv.png)

An object is an instance of a class
[C++ 中对象占用多大内存](https://blog.csdn.net/qinghezhen/article/details/9100079)

* we refer to the variables within a class as its **member variables.**
* we refer to the functions within a class as its **member functions.**
* we often say that member variables define the **state** of an object, while member functions define the **behaviors** an object can perform. 
* a function whose name matches the name of the class where it resides is a **constructor function.**  
* As a convention, we often start member variable names with underscores. Those variables will be accessible from every function in our implementation file, and this naming convention will help us distinguish them from local variables within those functions.
* Note that it's considered best practice not to issue a using `namespace std;` statement in our `quokka.h` file. **If we did that, then that namespace would apply to every source file with an #include "quokka.h" directive**. We instead prefer to qualify anything from the std namespace in our header file using the tedious std:: syntax.

## lecture 15
* **The Ampersand Operator Means Different Things in Different Contexts!**
    * When we use `&` in a variable DECLARATION, that creates a REFERENCE.
    * When we use `&` on an ALREADY-EXISTING variable, that gives us its ADDRESS.
* **The Asterisk Operator Means Different Things in Different Contexts!**
    * When we use `*` in a variable DECLARATION, that creates a POINTER.
    * When we use `*` on an ALREADY-EXISTING variable, that DEREFERENCES our pointer. (In other words, it GOES to the address that our pointer is pointing to and then proceeds to operate on whatever variable it finds there.)
* The square brackets operator in C++ acts as an offset whether applied to an array variable or an actual pointer
* Note that while an array might look a lot like a pointer, the key difference is that a pointer can be assigned a new value, causing it to point elsewhere. An array variable name, on the other hand, is bound to the array it represents and cannot be made to point elsewhere.
* When we apply an offset to an array (that's the index in square brackets), that tells C++ to go to the beginning of the array and skip forward a certain number of places in memory.

## lecture 16
* local variables die when we leave a function.
* Here are some key points about `new`:
    * The memory we set aside with `new` exists outside the stack frame for our function call, which means it will not die when we leave our function. Cool! Instead of existing in ***stack space***, the stuff we create with `new` exists in what we call ***heap space***.
    * Because the memory set aside with `new` is not released automatically when we leave the function where that happened, it's up to us to keep track of that memory and manually release it to the system using the delete operator when we're finished with it. Failure to do so will lead to a memory leak  
    * Remember that `new` returns to us the address of the block of memory it just set aside for us in heap space. We store that address in a pointer variable.
    * The memory we set aside with `new` has behaviors that are not predicted at compile-time. If we use `new` to create an array, the length of that array might be based on some variable whose value is determined through user input or file input at runtime. Furthermore, the exact place where we finish using that memory and manually release it back to the system might be governed by user input that cannot be predicted at compile-time. The behaviors here are *dynamic*.  
    * Accordingly, when we set aside memory with new, we call that **dynamic memory allocation**. (In contrast, the creation of local variables without the use of `new` is called **static memory allocation**, which is a bit obnoxious because the word "static" had additional meanings in C++ and many other languages.)
    * you might be tremendously concerned that the immortal quokka we created in `createQuokka()` will take up memory in our system forever and ever. That's not really the case. When a program terminates -- **when we finally return from `main()` -- all memory associated with that program is reclaimed by the operating system.** So, while our quokka lived beyond the lifespan of the function where it was created, it didn't live beyond the lifespan of our whole program. (If that were possible, the consequences for memory management would be disastrous.) It's considered poor form, however, to let a program terminate without having manually released our claim to all the dynamically allocated memory we set aside over the course of our program. We should do our own bookkeeping and release dynamically allocated memory once we no longer need it. **When we fail to do so -- or when we completely lose all record of a pointer given to us by new and can therefore no longer access that memory address -- we have what we call a memory leak.**
    * A super important rule of thumb is that for every `new` statement in a program, we should have a corresponding `delete` statement to free up the dynamically allocated memory.
  * when we have a member function that isn't supposed to change the internal state of an object at all, it's conventional to put `const` after the function name in both our header file and our .cpp file. That actually ensures that the function cannot change any of our member variables, and this is considered a best practice so that no one can come along and accidentally modify the code to change member variables that shouldn't have been changed.  

## lecture 17
  * binary trees (every node has at most two children)
  * complete binary tree (every level is completely filled up, except perhaps for the bottom level, and if the bottom level is not filled up, all nodes on that level must be completely flushed to the left with no gaps)

## lecture 21 
operator overloading 

```C++
ostream& operator <<(ostream& out, const Date& d) {
    out << d.getMonth() << "/" << d.getDay();
    return out;
}
```
`std::cout` is an ostream object. and every `<<` operator will change it with another parameter.  

## lecture 22
> it's a shame to just use these blind and not understand what they're really doing and they're structures that we can understand using what we've learned     
    

```C++
type* name = new type[length];    // uninitialized
type* name = new type[length]();    // initialized to 0
```   

* if () are written after the array[], it will set all array elements to their default zero-equivalent value for the data type. (slower)
* if no () are written, the elements are uninitialized, so whatever garbage values were stored in that memory beforehand will be your elements. 

`delete[] name;`  

* release the memory associated with the given array.
* Must the done for all arrays created with new 
    - Or else the program has a *memory leak*.
    - Leaked memory will be released when the program exits, but for long-running programs, memory leaks are bad and will eventually exhaust your RAM.  

## lecture 24
* any declared values live until the end of the current function scope.
    - this is called *static allocation* or *stack allocation*.
    - if you return an object, it is copied; the original is still discarded

## lecture 25
* C++ has an entity called a *structure* (struct). smaller than class.
    - Very similar to a class; a collection of data and (maybe) behavior.
    - But has(by default) public member variable and no functions.

## lecture 26
pointers to objects  
a variable (left side of =) is an arrow (*the base of an arrow*)  
a value (right side of =) is an object (*a box; what an arrow points at*)  

## Binary Tree && Binary Search Tree
short circuit boolean evaluation  

## Graph
* this is DFS(depth first search) because when a goes and tries exploring b it explores all of the things that could come after b before it ever backtracks to try going down from a to d (another choice as to b), so it does a deep exploration of things that could follow b before it tries anything else.  
* breadth-first search(BFS): finds a path between two nodes by taking one step down all paths and then immediately backtracking. 
* BFS and DFS do not consider edge weights, dijkstra's algorithm consider edge weights.  
* dijkstra's algorithm is a *greedy algorithm*:  
    - Make choices that currently seem the best.
    - Locally optimal does not always mean globally optimal.
* It is correct because it maintains the following two properties:
    - for every marked vertex, the current recorded cost is the lowest cost to that vertex from the source vertex.
    - for every unmarked vertex v, its recorded distance is shortest path distance to *v* from source vertex, considering only currently known vertices and v. 

## hash
`hashNode** elements` `elements = new hashNode*[10]`, elements is a pointer to an array of hashNode pointer.  
  
## inheritance
* **is-a relationship**: A hierarchical connection where one category can be treated as a specialized version of another.
* **inheritance:** A way to form new classes based on existing classes, taking on their attributes/behavior.  
    - a way to group related classes】】
    - a way to share code between two or more classes
* one class can extend another, absorbing its data/behavior.
    - superclass(base class): Parent class that is being extended.
    - subclass(derived class): Child class that inherits from the superclass.
        1. subclass gets a copy of every field and method from superclass.
        2. subclass can add its own behavior, and/or change inheried behavior.  
* **virtual fuction:** One that is allowed to be overriden. must be declared with `virtual` keyword in superclass.

## Polymorphism
* **polymorphism:** Ability for the same code to be used with different types of objects and behave differently with each.  
    - templates provide *compile-time* polymorphism. inheritance provides *run-time* polymorphism.

## heapify time complexity
![1714361634077](https://s2.loli.net/2024/04/29/eFVXdjNgPWn3U9J.jpg)

## Class

* the **public keyword** indicates that the member functions listed underneath is publicly accessible by anyone using the class. This essentially means that they from the public in-terface for the class.
* the **private keyword** indicates that the data members listed underneath it are private and only accessible by the class itself. This Means that those data members ate part of the private implementation of the class and aren't something that clients should be touching.
* the `::` notion is the **scope resolution operator**. It's used to indicate what logical part of the program a given name belongs to. The case we'll primarily see it used is in the context of defining member functions in a .cpp file, where we need to incicate that the functions we're implementing are actually member functions of a class, not freestanding functions.  
* the `const` keyword appears in member functions indicates that those member functions aren't allowed to change the data members of the class. Only `const` member functions can be called on an object when in a function that accepts an object of that class by const reference. (when pass by const reference you can pass by reference but can't change the original value)  
* the statement `delete[] elements`; means "**destroy the momory pointed at by elems**" rather than "destroy the elems variable". As a result, elems is still a perfectly safe variable to reassign.  
* the address of the object is the same as the first member variable 

## debug
* use `step into` to enter the call to the funciton  
* use `step out` to return to the funciton
* use `@OX` represents an object or something