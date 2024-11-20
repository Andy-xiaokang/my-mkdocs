---
comments: true
---

# Chapter6 The Memory Hierarchy

## 6.1 Storage technologies

![20241003205452](https://s2.loli.net/2024/10/03/2zhjpXLWJ5T1Nuo.png)
![20241003211118](https://s2.loli.net/2024/10/03/G2w5ZSigRCNvAQM.png)
![20241003211139](https://s2.loli.net/2024/10/03/bnP6kydt9fWI3Q2.png)
![20241004001843](https://s2.loli.net/2024/10/04/rfdGoNu891CaF7L.png)
One reason circuit designers organize DRAMs as two-dimensional arrays
instead of linear arrays is to **reduce the number of address pins** on the chip. For
example, if our example 128-bit DRAM were organized as a linear array of 16
supercells with addresses 0 to 15, then the chip would need four address pins
instead of two. The disadvantage of the two-dimensional array organization is
that addresses must be sent in two distinct steps, which increases the access time.

Accessing Main Memory  
A bus is a collection of parallel wires that carry address, data, and control
signals. Depending on the particular bus design, data and address signals can share
the same set of wires or can use different sets. Also, more than two devices can
share the same bus.The control wires carry signals that synchronize the transaction
and identify what kind of transaction is currently being performed. For example,
is this transaction of interest to the main memory, or to some other I/O device
such as a disk controller? Is the transaction a read or a write? Is the information
on the bus an address or a data item?
![20241006011935](https://s2.loli.net/2024/10/06/a6BnEjwOHiQb7Yc.png)
The I/O bridge translates the electrical signals of the
system bus into the electrical signals of the memory bus. As we will see, the I/O
bridge also connects the system bus and memory bus to an I/O bus that is shared
by I/O devices such as disks and graphics cards. For now, though, we will focus on
the memory bus.

Connecting I/O Devices

![20241007012748](https://s2.loli.net/2024/10/07/fvcruwk7gDs1azV.png)
![20241007012807](https://s2.loli.net/2024/10/07/IPWzDqifKOerJEb.png)
![20241007012823](https://s2.loli.net/2024/10/07/t78OfkdYFri56D2.png)

## 6.2 Locality

Well-written computer programs tend to exhibit good ***locality***. That is, they tend
to reference data items that are near other recently referenced data items or
that were recently referenced themselves. This tendency, known as the ***principle of locality***, is an enduring concept that has enormous impact on the design and
performance of hardware and software systems.  
Locality is typically described as having two distinct forms: ***temporal locality and spatial locality***. **In a program with good temporal locality, a memory location that is referenced once is likely to be referenced again multiple times in the near future. In a program with good spatial locality, if a memory location is referenced once, then the program is likely to reference a nearby memory location in the near future.**

## 6.3 The Memory Hierarchy

![20241008174503](https://s2.loli.net/2024/10/08/GRDVESlzLOJNf58.png)
![20241010003148](https://s2.loli.net/2024/10/10/X4otmfHOCWhQSTM.png)

## 6.4 Cache Memories

![20241010011811](https://s2.loli.net/2024/10/10/4aOSNk8WqHPRhB1.png)
![20241010011839](https://s2.loli.net/2024/10/10/q7fxT3ONPdVB5ML.png)

### 6.4.2 Direct-Mapped Caches

The process that a cache goes through of determining whether a request is a
hit or a miss and then extracting the requested word consists of three steps: (1) set
selection, (2) line matching, and (3) word extraction.
![20241010014458](https://s2.loli.net/2024/10/10/tSZE78JyT4zPNka.png)

## 6.5 Writing Cache-Friendly Code

Here is the basic approach we use to try to ensure that our code is cache friendly.

1. *Make the common case go fast.* Programs often spend most of their time in a
few core functions. These functions often spend most of their time in a few
loops. So focus on the inner loops of the core functions and ignore the rest.
2. *Minimize the number of cache misses in each inner loop.* All other things being
equal, such as the total number of loads and stores, loops with better miss rates
will run faster.

- Repeated references to local variables are good because the compiler can
cache them in the register file (temporal locality).
- Stride-1 reference patterns are good because caches at all levels of the memory
hierarchy store data as contiguous blocks (spatial locality).

## 6.6 Putting It together: The impact of caches on program performance

### 6.6.1 the memory mountain

![20241013003039](https://s2.loli.net/2024/10/13/rlEUa6DQLIwSsPJ.png)
![20241013003149](https://s2.loli.net/2024/10/13/ztoFfwL28JdUxWO.png)