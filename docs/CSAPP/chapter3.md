---
comments: true
---

# Chapter 3 Machine-Level Representation of Programs

## 3.4 accessing informaition

![20240826171859](https://s2.loli.net/2024/08/26/1t2NpHJWMFyclg4.png)
![20240826173305](https://s2.loli.net/2024/08/26/QwXhp9igqo7UJPO.png)
![20240826212550](https://s2.loli.net/2024/08/26/GHDL7safkCAW9du.png)

## 3.5 Arithmetic and Logical Operations

![20240828013314](https://s2.loli.net/2024/08/28/6UoizuvIn2RQEMe.png)

Naming convention: word(2 bytes), double word(4 bytes), quad word(8 bytes)

![20240828230523](https://s2.loli.net/2024/08/28/5wOdL4hFMuWTtvl.png)

## 3.6 Control

![20240829012423](https://s2.loli.net/2024/08/29/hb5oY2uzmtIKNpr.png)
The leaq instruction does not alter any condition codes, since it is intended
to be used in address computations. Otherwise, all of the instructions listed in
Figure 3.10 cause the condition codes to be set. For the logical operations, such
as xor, the carry and overflow flags are set to zero. For the shift operations, the
carry flag is set to the last bit shifted out, while the overflow flag is set to zero. For
reasons that we will not delve into, the inc and dec instructions set the overflow
and zero flags, but they leave the carry flag unchanged.  
![20240829013039](https://s2.loli.net/2024/08/29/wmoYs2hnWApgQX8.png)

* The cmp instructions set the condition codes according to the differences of their
two operands. They behave in the same way as the sub instructions, except that
* they set the condition codes without updating their destinations  
The test instructions behave in the same manner as the and instructions, except that they
set the condition codes without altering their destinations.

### 3.6.2 Accessing the Condition codes

![20240829015045](https://s2.loli.net/2024/08/29/rIHCktzaYjSRgsV.png)

### 3.6.3 Jump Instrucitons

![20240829155511](https://s2.loli.net/2024/08/29/O1sNdc6zU7vMEmL.png)
Direct jumps are written in assembly code by
giving a label as the jump target, for example, the label .L1 in the code shown.
Indirect jumps are written using ‘*’ followed by an operand specifier using one of
the memory operand formats described in Figure 3.3. As examples, the instruction  
`jmp *%rax`  
uses the value in register %rax as the jump target, and the instruction  
`jmp *(%rax)`  
reads the jump target from memory, using the value in %rax as the read address  

### 3.6.6 implementing conditional branches with conditional moves

![20240830222947](https://s2.loli.net/2024/08/30/V4ozh1Iqb6MnkCl.png)

### 3.6.7 Loops

## 3.7 Procedures

Procedures are a key abstraction in software. They provide a way to package code
that implements some functionality with a designated set of arguments and an
optional return value. This function can then be invoked from different points in
a program.Well-designed software uses procedures as an abstraction mechanism,
hiding the detailed implementation of some action while providing a clear and
concise interface definition of what values will be computed and what effects
the procedure will have on the program state.

### 3.7.1 The Run-Time Stack

Using our example of procedure P calling procedure Q, we can see that while Q is executing, P, along with any of the procedures in the chain of calls up to P, is temporarily suspended. While Q is running, only it will need the ability to allocate new storage for its local variables or to set up a call to another procedure. On the other hand, when Q returns, any local storage it has allocated can be freed.

![20240831213857](https://s2.loli.net/2024/08/31/tCPoG4xwbsLe182.png)
When procedure P calls procedure Q, it will push the return address onto the stack, indicating where within P the program should resume execution once Q returns. We consider the return address to be part of P’s stack frame, since it holds state relevant to P.  

### 3.7.3 Data transfer

![20240901174652](https://s2.loli.net/2024/09/01/Azs1owJ5TyY3Q7S.png)

![20240901221044](https://s2.loli.net/2024/09/01/9IVrEMsPCc1Snip.png)

## 3.8 Array Allocaiton and Access

### 3.8.1 Basic Principles

![20240903001727](https://s2.loli.net/2024/09/03/PX5KSDt7MeEjbsT.png)
![20240903001819](https://s2.loli.net/2024/09/03/mrO687iFNC9hHqS.png)

### 3.8.2 Pointer Arithmetic

![20240903005514](https://s2.loli.net/2024/09/03/zsJFmfCOEqu56kD.png)
![20240903012015](https://s2.loli.net/2024/09/03/uRdFB8jGUpAHwqT.png)

### 3.8.3 Nested Arrays

![20240903224916](https://s2.loli.net/2024/09/03/ZkvGxi7dPVKgDw5.png)
![20240903225256](https://s2.loli.net/2024/09/03/w4l5E2FjJCRdmnt.png)

## 3.9 Heterogeneous Data Structures

The implementation of structures is similar to that of arrays
in that all of the components of a structure are stored in a contiguous region of
memory and a pointer to a structure is the address of its first byte. The compiler
maintains information about each structure type indicating the byte offset of
each field. It generates references to structure elements using these offsets as
displacements in memory referencing instructions.

### 3.9.3 Data Alignment

![20240906011405](https://s2.loli.net/2024/09/06/A3K91ZdaRwxM2E5.png)
![20240906011816](https://s2.loli.net/2024/09/06/VYlionXdecOHWkw.png)

## 3.10 combining Control and Data in Machine-Level Programs

### 3.10.1 Understaning Pointers

Pointers serve as a uniform way to generate references to elements within different data structures. Here we highlight some key principles of pointers and their mapping into machine code.  

* ***Every pointer has an associated type.*** This type indicates what kind of object
the pointer points to. Using the following pointer declarations as illustrations
![20240907030132](https://s2.loli.net/2024/09/07/GV63n9FXK7uqHmT.png)
* ***Every pointer has a value.*** This value is an address of some object of the
designated type. The special NULL (0) value indicates that the pointer does not point anywhere.
* ***Pointers are created with the ‘&’ operator.*** This operator can be applied to any
C expression that is categorized as an ***lvalue***, meaning an expression that can
appear on the left side of an assignment. Examples include variables and the
elements of structures, unions, and arrays. We have seen that the machinecode
realization of the ‘&’ operator often uses the `leaq` instruction to compute
the expression value, since this instruction is designed to compute the address
of a memory reference.
* ***Pointers are dereferenced with the ‘*’ operator.*** The result is a value having the
type associated with the pointer. Dereferencing is implemented by a memory reference, either storing to or retrieving from the specified address.
* ***Arrays and pointers are closely related.*** The name of an array can be referenced
(but not updated) as if it were a pointer variable. Array referencing (e.g.,
a[3]) has the exact same effect as pointer arithmetic and dereferencing (e.g.,
*(a+3)). Both array referencing and pointer arithmetic require scaling the
offsets by the object size.When we write an expression p+i for pointer p with
value p, the resulting address is computed as p + L . i, where L is the size of
the data type associated with p.
* ***Casting from one type of pointer to another changes its type but not its value.*** One effect of casting is to change any scaling of pointer arithmetic. So, for
example, if p is a pointer of type `char *` having value p, then the expression
(`int *`) p+7 computes p + 28, while (`int *`) (p+7) computes p + 7. (Recall
that casting has higher precedence than addition.)
* ***Pointers can also point to functions.*** This provides a powerful capability for
storing and passing references to code, which can be invoked in some other
part of the program. For example, if we have a function defined by the proto-type
![20240907032108](https://s2.loli.net/2024/09/07/7uKyh3o5svGOTmi.png)
![20240907032512](https://s2.loli.net/2024/09/07/wafHFTL1jscl6A2.png)

### 3.10.2 Using the GDB Debugger

![20240907164231](https://s2.loli.net/2024/09/07/IcgmEeSjikno8Ud.png)
![20240907164329](https://s2.loli.net/2024/09/07/pXsLYmZDQVByxqi.png)
![20240907163947](https://s2.loli.net/2024/09/07/wKilxt28XT9j4kU.png)

### 3.10.3 Out-of-Bounds Memory References and Buffer overflow

![20240907180648](https://s2.loli.net/2024/09/07/vYcy9aBmw8j5AP3.png)
![20240907180720](https://s2.loli.net/2024/09/07/NX3myeBhFZ6KL5O.png)
![20240907180753](https://s2.loli.net/2024/09/07/3Jw1iZXWLQp9TrS.png)

### 3.10.4 Thwarting Buffer Overflow Attacks

* Stack Randomization
* Stack Corruption Detection
* Limiting Executable Code Regions

Historically, the x86 architecture merged the read and execute
access controls into a single 1-bit flag, so that any page marked as readable
was also executable. The stack had to be kept both readable and writable, and
therefore the bytes on the stack were also executable. Various schemes were implemented
to be able to limit some pages to being readable but not executable,
but these generally introduced significant inefficiencies.  
More recently, AMDintroduced an NX (for “no-execute”) bit into the memory
protection for its 64-bit processors, separating the read and execute access
modes, and Intel followed suit. With this feature, the stack can be marked as being
readable and writable, but not executable, and the checking of whether a page
is executable is performed in hardware, with no penalty in efficiency
