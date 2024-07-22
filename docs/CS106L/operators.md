---
comments: true
---

# Operators

## operator overloading

当运算符 overload as member funcitons 时， 左侧的操作数应是调用对象；当overload as non-member funcitons 时，运算符左侧的操作数对应于运算符函数的第一个参数，运算符表达式右侧的操作数对应于运算符函数的第二个参数。  
友元函数是在类声明中声明的，但它不是成员函数，因此不能使用成员运算符来调用。
![20240708161630](https://s2.loli.net/2024/07/08/mo9ve3UPzxB8TbJ.png)
how does C++ know how to apply operators to user-defined classes?  
![20240707151410](https://s2.loli.net/2024/07/07/raGMkyW2zFnZ69H.png)
![20240707151443](https://s2.loli.net/2024/07/07/JjQrylUqOespkKR.png)

const object can only call const functions  
return type with const -> can't be assigned(changed) as lvalue  
for a const variable you have to do them(declare, initialize) simutaneously
![截屏2024-07-09 17.59.22](https://s2.loli.net/2024/07/09/CXDQNB2kjJ5pGtd.png)
![20240709182028](https://s2.loli.net/2024/07/09/UJCxSPjRZqY2yDt.png)
![20240709182851](https://s2.loli.net/2024/07/09/T7VGula6nxeEAX9.png)
![20240709183147](https://s2.loli.net/2024/07/09/6mkdDFiarxwltqX.png)

## canonical forms

![20240708165205](https://s2.loli.net/2024/07/08/RrKdEs8m3jqGTQC.png)
![20240708165619](https://s2.loli.net/2024/07/08/1OPQ4gouhJp5inX.png)

![20240708180210](https://s2.loli.net/2024/07/08/OuJ4VQATZYbslLi.png)
![20240708180237](https://s2.loli.net/2024/07/08/f3Uev2AdHknEPGS.png)
![20240708180255](https://s2.loli.net/2024/07/08/qzdLkMJ3EFAbQe8.png)
![20240708225446](https://s2.loli.net/2024/07/08/k9BCoydA37aX421.png)
![20240708225548](https://s2.loli.net/2024/07/08/BEvpdgfH5zkxlaT.png)

## POLA（principle of least astonishment

![20240709004752](https://s2.loli.net/2024/07/09/qK9aLFNiQt1Mdx2.png)
![20240709004814](https://s2.loli.net/2024/07/09/bmDNAhlkZsB6e53.png)
![20240709010159](https://s2.loli.net/2024/07/09/KuMowUPbSgVXpnB.png)
