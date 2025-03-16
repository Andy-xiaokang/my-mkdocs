---
comments: true
---

# Chapter 9 Virtual Memory

1. It uses main memory efficiently by treating it as a cache for an address space stored on disk, keeping only the active areas in main memory and transferring data back and
forth between disk and memory as needed.
2. It simplifies memory management by providing each process with a uniform address space.
3. It protects the address space of each process from corruption by other processes.

## 9.1 Physical and Virtual Addressing

Early PCs used physical addressing, and systems such as digital signal processors,
embedded microcontrollers, and Cray supercomputers continue to do so. However, modern processors use a form of addressing known as *virtual addressing*, as shown in Figure 9.2.
![20241223005553](https://s2.loli.net/2024/12/23/Ya8PKkNRFCG3gXz.png)
![20241223011728](https://s2.loli.net/2024/12/23/6WVfeouKHQnG8NZ.png)

## 9.2 Address Spaces

![20241223012353](https://s2.loli.net/2024/12/23/zIXDC8y2uva1nfQ.png)

## 9.3 VM as a Tool for Caching

![20241223160648](https://s2.loli.net/2024/12/23/2gsBthDaN3OZmwi.png)
![20241223161611](https://s2.loli.net/2024/12/23/soWM1g9DFlmKBYX.png)

### 9.3.1 DRAM Cache Organizaiton

![20241223163808](https://s2.loli.net/2024/12/23/oSmBOI27gJXTzdN.png)

### 9.3.2 Page Tables

Each page in the virtual address space has a PTE at a fixed offset in the page table. For our purposes, we will assume that each PTE consists of a valid bit and an n-bit address field. The valid bit indicates whether the virtual page is currently cached in DRAM.  
If the valid bit is set, the address field indicates the start of the corresponding physical page in DRAM where the virtual page is cached. If the valid bit is not set, then a null address indicates that the virtual page has not yet been allocated. Otherwise, the address points to the start of the virtual page on disk.
![20241223170903](https://s2.loli.net/2024/12/23/DyW87dfbCoU12Hq.png)

### 9.3.3 Page Hits

Consider what happens when the CPU reads a word of virtual memory contained
in VP2, which is cached in DRAM(Figure 9.5). Using a technique we will describe
in detail in Section 9.6, the address translation hardware uses the virtual address
as an index to locate PTE 2 and read it from memory. Since the valid bit is set, the
address translation hardware knows that VP 2 is cached in memory. So it uses the
physical memory address in the PTE (which points to the start of the cached page
in PP 1) to construct the physical address of the word.
![20241223223450](https://s2.loli.net/2024/12/23/rYL6cWO9gXStvIu.png)

### 9.3.4 Page Faults

![20241223232758](https://s2.loli.net/2024/12/23/2wqLSnQg3jc1AP5.png)

The activity of transferring a page between disk and memory is known as *swapping* or *paging*. Pages are *swapped in* (*paged in*) from disk to DRAM, and *swapped out* (*paged out*) from DRAM to disk.

### 9.3.5 Allocating Pages

Figure 9.8 shows the effect on our example page table when the operating system
allocates a new page of virtual memory—for example, as a result of calling `malloc`.
In the example, VP 5 is allocated by creating room on disk and updating PTE 5
to point to the newly created page on disk.

![20241225013608](https://s2.loli.net/2024/12/25/OFBR9DTQis2PShn.png)

### 9.3.6 Locality to the Rescue Again

![20241225015736](https://s2.loli.net/2024/12/25/zLetViJDyqPWCZk.png)

## 9.4 VM as a Tool for Memory Management

![20241225160241](https://s2.loli.net/2024/12/25/aO9VQSgqkAzpNXx.png)

In fact, operating systems provide a separate page table, and thus a separate virtual address space, for each process. Notice that multiple virtual pages can be mapped to
the same shared physical page.

![20241225165342](https://s2.loli.net/2024/12/25/W4X6i8B2JDrVTHL.png)
![20241225170000](https://s2.loli.net/2024/12/25/1hiuCQzXg3paZYU.png)

## 9.5 VM as a Tool for Memory Protection

![20241225233658](https://s2.loli.net/2024/12/25/b69qrGXT1CjeRwY.png)
![20241225233727](https://s2.loli.net/2024/12/25/NzeZFxuTAofyd8t.png)

## 9.6 Address Translation

![20241226003022](https://s2.loli.net/2024/12/26/8una95MUvqGdO3s.png)
![20241226004906](https://s2.loli.net/2024/12/26/jQSca8I5lTwkzZD.png)
![20241226005203](https://s2.loli.net/2024/12/26/kfXCVyHaOs2lpSr.png)
![20241226010217](https://s2.loli.net/2024/12/26/pcw8o3Y7NtKMjng.png)
![20241226010259](https://s2.loli.net/2024/12/26/sbYujAk2iq7nCeV.png)

### 9.6.1 Integrating Caches and VM

![20241226011004](https://s2.loli.net/2024/12/26/VyMA6so8G7xeCTp.png)
The main idea is that the address translation occurs before the cache lookup. Notice that page table entries can be cached, just like any other data words.

### 9.6.2 Speeding Up Address Translation with a TLB

A TLB is a small, virtually addressed cache where each line holds a block consisting of a single PTE.
![20241227010737](https://s2.loli.net/2024/12/27/8RlYkVQ9psEzNUv.png)

### 9.6.3 Multi-Level Page Tables

This scheme reduces memory requirements in two ways. First, if a PTE in the
level 1 table is null, then the corresponding level 2 page table does not even have
to exist. This represents a significant potential savings, since most of the 4 GB
virtual address space for a typical program is unallocated. Second, only the level
1 table needs to be in main memory at all times. The level 2 page tables can be
created and paged in and out by theVMsystem as they are needed, which reduces
pressure on main memory. Only the most heavily used level 2 page tables need to
be cached in main memory.

![20241227171024](https://s2.loli.net/2024/12/27/QGd3jZaXoip1lt9.png)

Figure 9.18 summarizes address translation with a k-level page table hierarchy.
The virtual address is partitioned into k VPNs and a VPO. Each VPN i, 1 ≤ i ≤ k,
is an index into a page table at level i. Each PTE in a level j table, 1 ≤ j ≤ k − 1,
points to the base of some page table at level j + 1. Each PTE in a level k table
contains either the PPN of some physical page or the address of a disk block.
To construct the physical address, the MMU must access k PTEs before it can determine the PPN. As with a single-level hierarchy, the PPO is identical to the
VPO.  

Accessing k PTEs may seem expensive and impractical at first glance. However, the TLB comes to the rescue here by caching PTEs from the page tables at
the different levels. In practice, address translation with multi-level page tables is not significantly slower than with single-level page tables.  

### 9.6.4 Putting it Together: End-to-End Address Translation

## 9.7 Case Study: The Intel Core i7/Linux Memory System

![20241230223017](https://s2.loli.net/2024/12/30/kLJubEsrACFozZw.png)

### 9.7.1 Core i7 Address Translation

![20241231004907](https://s2.loli.net/2024/12/31/g7N2LY3X6BjE9Di.png)
![20241231004946](https://s2.loli.net/2024/12/31/24xaV9l5HpfKTIi.png)
![20241231005015](https://s2.loli.net/2024/12/31/P3ERCFw2XN1QJxB.png)

### 9.7.2 Linux Virtual Memory System

![20250102172218](https://s2.loli.net/2025/01/02/Wow1TIHpxecCj48.png)
![20250102223635](https://s2.loli.net/2025/01/02/FhZ6JlroRP1AwvY.png)
![20250102223735](https://s2.loli.net/2025/01/02/9NhrmAZl3Tv6L7u.png)
![20250103005457](https://s2.loli.net/2025/01/03/GBsHf8Lqamoj9bl.png)
![20250103005512](https://s2.loli.net/2025/01/03/RlmFesvxZHh2WC7.png)
![20250103005528](https://s2.loli.net/2025/01/03/ZfGjTMa69Yv3ytP.png)

## 9.8 Memory Mapping

Linux initializes the contents of a virtual memory area by associating it with an
object on disk, a process known as `memory mapping`.

![20250107015933](https://s2.loli.net/2025/01/07/gIKAXPNsr1iYfb2.png)
![20250107015953](https://s2.loli.net/2025/01/07/BLfMwKOSq5THFIr.png)

## 9.9 Dynamic Memory Allocation

* *Explicit allocators* require the application to explicitly free any allocated
blocks. For example, the C standard library provides an explicit allocator called the `malloc` package. C programs allocate a block by calling the `malloc` function, and free a block by calling the `free` function. The `new` and `delete` calls in C++ are comparable.
* *Implicit allocators*, on the other hand, require the allocator to detect when
an allocated block is no longer being used by the program and then free the block. Implicit allocators are also known as *garbage collectors*, and the process of automatically freeing unused allocated blocks is known as *garbage collection*. For example, higher-level languages such as Lisp, ML, and Java rely on garbage collection to free allocated blocks.

## 9.10 Garbage Colleciton

### 9.9.1 The `malloc` and `free` Functions

### 9.9.2 Why Dynamic Memory Allocation

### 9.9.3 Allocator Requirements and Goals

![20250108170320](https://s2.loli.net/2025/01/08/2fOcFR36bIDvzhK.png)

### 9.9.4 Fragmentation

The primary cause of poor heap utilization is a phenomenon known as fragmentation,
which occurs when otherwise unused memory is not available to satisfy
allocate requests. There are two forms of fragmentation: *internal fragmentation*
and *external fragmentation*.

*Internal fragmentation* occurs when an allocated block is larger than the payload.
![20250108172540](https://s2.loli.net/2025/01/08/vZkuqlKMUGmOoYi.png)

*External fragmentation* occurs when there is enough aggregate free memory
to satisfy an allocate request, but no single free block is large enough to handle
the request.
![20250108172602](https://s2.loli.net/2025/01/08/nMde851bJCUfa2k.png)
if the request in Figure 9.34(e) were for eight words
rather than two words, then the request could not be satisfied without requesting
additional virtual memory from the kernel, even though there are eight free words
remaining in the heap.

### 9.9.5 Implementation Issues



## 9.11 Common Memory-Related Bugs in C Programs
