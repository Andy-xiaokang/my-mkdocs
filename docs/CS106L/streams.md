---
comments: true
---

# Streams

## overview

We often want our programs to interact with external devices. eg: console&keyboard, files, other programs(pipeline), sockets(networking)  
In general, there are two main challenges.  
![20240630231820](https://s2.loli.net/2024/06/30/UMCVN1LIOdYp27c.png)
![20240630231930](https://s2.loli.net/2024/06/30/Gcdmlu2vqpyoXC5.png)
![20240630230912](https://s2.loli.net/2024/06/30/bPjDa5gheFRIcz4.png)
![20240630232233](https://s2.loli.net/2024/06/30/pYWdksVafiD9rbe.png)

## stringstream

![20240630232451](https://s2.loli.net/2024/06/30/GdkCUvBO4gRA1pr.png)
Types matters, Stream stops reading at any whitespace or any invalid character for the type.  

key takeaways  

* `>>` extracts the next variable of a certain type, up to the next whitespace.
* the `>>` and `<<` operators return a reference to the stream itself, so in each instance the stream is the left-hand operand.  
* it's called a stringstream. Reading and writing simultaneously can often lead to subtle bugs, be careful.  

## state bits

* `G` **Good bit**: ready for read/write.  
* `F` **Fail bit**: previous operation failed, all future operations frozen.  
* `E` **EOF bit**: previous operation reached the end of buffer content.  
* `B` **Bad bit**: external error, likely irrecoverable.  

common reasons why that bit is on.  

* `G` Nothing unusual, on when other bits are off.  
* `F` Type mismatch, file can't be opened, seekg failed.
* `E` Reached the end of the buffer.  
* `B` could not move character to buffer from external source.  

G and B are not opposite, G and F are not opposite, F and E are normally the ones you will be checking.  
conclusion: you should rarely be using G

## input/output streams

there are four standard iostreams.  

* `cin` standard input stream  
* `cout` standard output stream (buffered)  
* `cerr` standard error stream (unbuffered)
* `clog` standard error stream (buffered)  

key takeaways:  
![20240701164633](https://s2.loli.net/2024/07/01/qp6CcuRgMJnXhor.png)
the position pointer skip whitespace before the token.  

streams are not copyable  
`cout << endl` = `cout << '\n' << std::flush`  
`cin` read up to the white space but it doesn't consume the white space. it's only when you call `cin` another time, then it skips the white space and it tries to read the token.  
when fail bit is on, all future `cin` operation fail.

## manipulators

## summary of Types and Streams

* Use modern C++ constructs! (auto, uniform initialization, etc)
* If you need error checking for user input, best practice is to:
  * use getline to retrieve a line from `cin`
  * create a istringstream with the line
  * parse the line using a stringstream, usually with `>>`
* Use state bits to control streams and perform error-checking.
  * fail bit can check type mismatchs
  * eof bit can check if you consumed all input

***

when to use auto?

* when you don't care what the type is (iterators)
* when its type is clear from context (templates)
* when you don't know that the type is (lambdas)
* don't use it unnecessarily for return types.

auto can not be use as type of fuction's parameter, but can be used as function's return type.  
for lambda function it must be auto, because when the compiler generates the class you have no idea what the class is called the compiler is gonna generate some name for that class.  

![20240702164907](https://s2.loli.net/2024/07/02/SgCxNJRHWQbqyGz.png)  
![20240702164936](https://s2.loli.net/2024/07/02/nY3AGLlpT4De8w1.png)  
