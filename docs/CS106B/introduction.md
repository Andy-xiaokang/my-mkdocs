---
comments: true
---

## lecture 1

![截屏2023-12-25 21.29.37](https://s2.loli.net/2023/12/25/po7EA2KRsGaiYUX.png)
![截屏2023-12-25 21.46.04](https://s2.loli.net/2023/12/25/Z8gQ1W9UxDGYoj5.png)
variable name represents a location in memory | variable name is an alias of a M register  

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