# Introduction to Java
## Essentials 
### **Key Syntax Features**. Our first programs reveal several important syntax features of Java:
* All code lives inside a class.  
* The code that is executed is inside a function, a.k.a. method, called main.
* Curly braces are used to denote the beginning and end of a section of code, e.g. a class or method declaration.
* Statements end with semi-colons.  
* Variables have declared types, also called their “static type”.
* Variables must be declared before use.
* Functions must have a return type. If a function does not return anything, we use void,
* The compiler ensures type consistency. If types are inconsistent, the program will not compile.
### Static Typing
One of the most important features of Java is that all variables and expressions have a so-called static type. Java variables can contain values of that type, and only that type. Furthermore, the type of a variable can never change.  
In addition to providing additional error checking, static types also let the programmer know exactly what sort of object he or she is working with.  
To summarize, static typing has the following advantages:  

* The compiler ensures that all types are compatible, making it easier for the programmer to debug their code.
* Since the code is guaranteed to be free of type errors, users of your compiled programs will never run into type errors. For example, Android apps are written in Java, and are typically distributed only as .class files, i.e. in a compiled format. As a result, such applications should never crash due to a type error since they have already been checked by the compiler.  
* Every variable, parameter, and function has a declared type, making it easier for a programmer to understand and reason about code.
## objects 
* **Class Declaration.** Java classes can contain methods and/or variables. We say that such methods and variables are “members” of the calss. Members can be instance members or static members. Static members are declared with the static keyword. Instance members are any members without the static keyword.  
* **Class Instantiation.** Instantiating a class is almost always done using the new keyword, e.g. Dog d = new Dog(). **==An instance of a class in Java is also called an Object.==**  
* **Dot Notation.** We access members of a class using dot notation, e.g. d.bark(). Class members can be accessed from within the same class or from other classes.  
* **Constructors.** Constructors tell Java what to do when a program tries to create an instance of a class, e.g. what it should do when it executes Dog d = new Dog().  
* **Array Instantiation.** Arrays are also instantiated using the new keyword. If we have an array of Objects, e.g. Dog[] dogarray, then each element of the array must also be instantiated separately.  
* **Static vs. Instance methods.** The distinction between static and instance methods is incredibly important. **==Instance methods are actions that can only be taken by an instance of the class (i.e. a specific object), whereas static methods are taken by the class itself. An instance method is invoked using a reference to a specific instance, e.g. d.bark(), whereas static methods should be invoked using the class name, e.g. Math.sqrt().==** Know when to use each.  
* **Static variables.** Variables can also be static. Static variables should be accessed using the class name, e.g. Dog.binomen as opposed to d.binomen. Technically Java allows you to access using a specific instance, but we strongly encourage you not to do this to avoid confusion.  
* **The this keyword.** Inside a method, **==we can use the this keyword to refer to the current instance.==**  
* **Command Line Arguments.** Arguments can be provided by the operating system to your program as “command line arguments,” and can be accessed using the args parameter in main. For example if we call our program from the command line like this java ArgsDemo these are command line arguments, then the main method of ArgsDemo will have an array containing the Strings “these”, “are”, “command”, “line”, and “arguments”.

## [Java style guide](https://sp19.datastructur.es/materials/guides/style-guide.html)
### Assorted Java Style Conventions
1. Replace
    ```java
     if (condition) {
     return true;
     } else {
     return false;
     }
    ```
2. Write array types with the “[]” after the element-type name, not after the declarator. Write “`String[] names`”, not “`String names[]`”.