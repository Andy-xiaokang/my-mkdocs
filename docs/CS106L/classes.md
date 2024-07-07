---
comments: true
---

# class Design

![20240707175754](https://s2.loli.net/2024/07/07/WkRcmnsiNOfBXjJ.png)  
![20240707175819](https://s2.loli.net/2024/07/07/taj9wIJRSGWd2OC.png)  
template classes require putting the implementation in the .h file

## Header files(.h) vs source files(.cpp)

must put a semicolon at end of class declaration  
in ClassName.cpp, we write bodies(definitons) for the member functions that were declared in the .h file:  
member functions/constructors can refer to the object's member variables.  

## Constructors

```c++
ClassName::ClassName(parameters) {
    statements to initialize the object;
}
```

constructor: Initializes state of new objects as they are created.  
**no return type is specified, implicitly "returns" the new object**  

## Destructors

destructor: called when the object is deleted by the program.  
(when the object falls out of {} scope)  
useful if your object needs to free any memory as it dies.  

* delete any pointers stored as private members
* delete[] any arrays stored as private members  

## Operator overloading

unary: + - ++ -- * & ! ~ new delete  
binary: + - * / % += -= *= /= %= & | && || ^ == != < > <= >= << >> = [] -> () ,
syntax:  
`returnType operator op(parameters)`;//in the .h file for the class  
`returnType operator op(parameters)`// in the .cpp file for the class  

## const correctness

![20240707012356](https://s2.loli.net/2024/07/07/hBPzUCIZcHqL8s2.png)
![20240707013419](https://s2.loli.net/2024/07/07/1RL6HqxaUdpMzyI.png)
![20240707013537](https://s2.loli.net/2024/07/07/ZyloOwHg8rGcmsR.png)
![20240707013755](https://s2.loli.net/2024/07/07/TbotS36QrsFzqGu.png)
![20240707013917](https://s2.loli.net/2024/07/07/ZDKdLro9Pc3mJ6p.png)
![20240707014137](https://s2.loli.net/2024/07/07/6oOIRMcCKAx32zB.png)
![20240707014403](https://s2.loli.net/2024/07/07/MxEWbOPHFZ8YRqo.png)
const on objects:  
Guarantees that the object won't change by allowing you to call only const functions and treating all public members as if they were const. This helps the programmer write safe code, and also gives the compiler more information to use to optimize.  

const on fuctions:
Guarantees that the function won't call anything but const funcitons, and won't modify any non-static, non-mutable members.  

