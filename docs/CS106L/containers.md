---
comments: true
---

# Containers

## sequence containers

provides access to **sequences** of elements. includes:  

* `std::vector<T>` elements stored in continueous memory
* `std::deque<T>` elements don't stored in continueous memory
* `std::list<T>`
* `std::array<T>`
* `std::forward_list<T>`

deques support fast `push_front` operations. However, for other common operations like **element access**, vector will always outperform a deque.  
deque slower to access middle elements, however.  
> vector is the type of sequence that should be used by default... deque is the data structure of choice when most insertions and deletions take place at the beginning or at the end of the sequences.

Uniform initialization.

container adaptors

## associative containers & iterators

have no idea of a sequence  
data is accessed using the **key** instead of **indexes**.  
includes:  

* `std::map<T1, T2>`  
* `std::set<T>`  
* `std::unordered_map<T1, T2>`
* `std::unordered_set<T>`

Iterators let us view a ***non-linear*** colleciton in a ***linear*** manner  
`auto elems.end()` does not point anything in the elems, it point to the last element + 1, so it out of the container  

![20240704003557](https://s2.loli.net/2024/07/04/TsawPgikUeuRbC7.png)
![20240704010957](https://s2.loli.net/2024/07/04/Ec1HtpKFM7Be3j6.png)
![20240704011256](https://s2.loli.net/2024/07/04/odrjRCY2kBUlaHJ.png)
![20240704011342](https://s2.loli.net/2024/07/04/s3hnxMFbkS6AqjT.png)
![20240704011512](https://s2.loli.net/2024/07/04/35ATqfcZeiGI9OF.png)
![20240704011710](https://s2.loli.net/2024/07/04/yVx8CaFlzS3g5AB.png)
![20240704011808](https://s2.loli.net/2024/07/04/3zR2hqNPQuKdWjt.png)

## container adaptors  

* std::queue  

    > the class template acts as a wrapper to the underlying container - only a specific set of functions is provided. The queue pushes the elements on the back of the underlying container and pops them from the front.  

* std::stack  

    > the class template acts as a wrapper to the underlying container - only a specific set of functions is provided. The stack pushes and pops the element from the back of the underlying container, known as the top of the stack.  

 