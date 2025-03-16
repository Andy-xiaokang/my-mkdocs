# Chapter 10 System-Level I/O

*Input/output(I/O)* is the process of copyign data between main memory and external devices such as disk drives, terminals, and networks. An input operation
copies data from an I/O device to main memory, and an output operation copies
data from memory to a device.

## 10.1 Unix I/O

![20241201011427](https://s2.loli.net/2024/12/01/tS5R1Gxdzo2wF9O.png)
![20241201012000](https://s2.loli.net/2024/12/01/l2uYpA1rK9yJw7T.png)

## 10.2 Files

![20241201153514](https://s2.loli.net/2024/12/01/Dp2th4dr1R3OSuB.png)
![20241201153541](https://s2.loli.net/2024/12/01/fbIG6BheyxNH4En.png)
![20241201154534](https://s2.loli.net/2024/12/01/l4dXeEYwS1kLs5j.png)

## 10.3 Opening and Closing Files

![20241202003149](https://s2.loli.net/2024/12/02/G4OoSpmc961AN2t.png)
![20241202003247](https://s2.loli.net/2024/12/02/3FRAg61fhEbqlIP.png)

## 10.4 Reading and Writing Files

![20241202012420](https://s2.loli.net/2024/12/02/1yozIfhlCvd63ua.png)

## 10.10 Standard I/O

![20241203210024](https://s2.loli.net/2024/12/03/wGgXoDJpkn6NUSI.png)

## 10.11 Putting It Together: Which I/O Functions Should I Use

![20241203222914](https://s2.loli.net/2024/12/03/FjcY32h7zorDZJw.png)
![20241203222934](https://s2.loli.net/2024/12/03/R8cbWrAuKT7E3yj.png)

we recommend that you not use the standard I/O functions for input and output on network sockets. Use the robust Rio functions instead. If you need formatted output, use the `sprintf` function to format a string in memory, and then send it to the socket using `rio_writen`. If you need formatted input, use `rio_readlineb` to read an entire text line, and then use `sscanf` to extract different fields from the text line.

