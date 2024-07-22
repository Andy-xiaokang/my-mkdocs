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

![20240707231951](https://s2.loli.net/2024/07/07/DNE4eMHZoV2CAzX.png)
![20240707232010](https://s2.loli.net/2024/07/07/CkWUZnLblHDVduv.png)

## member initializer list

``` c++
    class Queue {
    private:
        Node* front;
        Node* rear;
        int items;
        const int qsize;

    public:
        Queue(int qs);
    }

    // in cpp file
    Queue::Queue(int qs) {
        front = rear = NULL;
        items = 0;
        qsize = qs;  // not acceptable!!!
    }
```

问题在于 qsize 是常量， 所以可以对它进行初始化，但不能给它赋值。从概念来说，调用构造函数时，对象将在括号中的代码执行之前被创建。因此，调用 Queue(int qs) 构造函数将导致程序首先给 4 个成员变量分配内存。然后，程序流程进入到括号中，使用常规的赋值方式将值存储在内存中。因此对于 const 数据成员，必须在执行到构造函数体之前，==**即创建对象时进行初始化**==。C++ 提供了一种特殊的语法来完成上述工作，它叫做成员初始化列表（member initializer list）。成员初始化列表由逗号分隔的初始化列表组成（前面要带冒号）。它位于参数列表的右括号之后、函数体左括号之前。  

``` C++
    Queue::Queue(int qs) : qsize(qs) {
        front = rear = NULL;
        items = 0;
    }
```

只有构造函数可以使用这种初始化列表语法。**对于 const 类成员，必须使用这种语法。另外，对于被声明为引用的类成员，也必须使用这种语法。这是因为引用与 const 数据类似，只能在被创建时进行初始化。**

``` c++
class Agency {
    // etc ...
}

class Agent {
private:
    Agency& belong; // must use initializer list to initialize
    ...
}

Agent::Agent(Agency& a) : belong(a) { ... }
```
