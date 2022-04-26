---
title: "Pointers"
pre: "3.1. "
weight: 40
date: 2018-08-24T10:53:26-05:00
---

Pointers in C are variables that store the memory address of some other variable or data. They have an associated type of what kind of value they reference.

Pointers are one of the most difficult concepts in the C language. However, mastering pointers allows you do have a deeper understanding of what actually happens when your program runs. Higher-level languages do not explicitly use pointers, but they do use pointers "behind the scenes". Learning pointers in C can also help you understand what's going on in Java/C#/etc. programs.

## Declaring

The type of a pointer variable is:

```c
type*
```

where *type* is the type of data this pointer will reference. For example:

```c
int* intPtr;
```

*intPtr* can hold the address of an int variable. Another:

```c
char* charPtr;
```

*charPtr* can hold the address of a char variable.

When you are declaring pointers, the * can go any where between the type and the variable name. For example, all of the following are acceptable:

```c
int* intPtr;
int * intPtr;
int*intPtr;
int *intPtr;
```

Variables in C are not automatically initialized – and this includes pointers. After declaring a pointer, it holds some garbage value that was left in that spot in memory.

## & Operator (Address-Of)
The & operator returns the memory address of a variable. For example, if we have:

```c
int x = 4;
```

And the *x* variable is stored at spot 1714 in memory (every variable is given a certain spot in memory, and these spots have an associated number), then if we do:

```c
&x
```

this will give us the 1714 spot.

The address-of operator isn't very useful unless we're using pointers. Since pointers are supposed to hold memory addresses, we can initialize them to be the address of some other variable.

So, suppose we have the following variable declarations:

```c
int x = 4; //x is given spot 1714 in memory
int *xPtr;
```

We can make the *xPtr* variable reference *x*:

```c
xPtr = &x; //Now xPtr "points to" x – it holds address 1714
```

Notice that when we DECLARE a pointer, we include the *. However, when we INITIALIZE the pointer, we don't include the *.

## * Operator (Dereferencing)
The * operator is an operator specifically for pointer variables. It returns the value of what is being pointed at. 

For example, if we have:

```c
int x = 4; //x is given spot 1714 in memory
int *xPtr;
xPtr = &x;
```

Then saying **xPtr* gets us the value pointed to by *xPtr*. *xPtr* holds memory address 1714, so if I say **xPtr*, then I get the value stored in spot 1714 – which is a 4. I can also use this operator to modify the value at that spot in memory. For example:

```c
*xPtr = 6;
```

Now the value at spot 1714 is a 6. The *x* variable is stored in spot 1714, so now *x* has the value 6.

## Example
The following example illustrates how pointers work:

```c
int i; //i gets a memory location, say 3245, and has some random value
int *ip; //ip has some random address
i = 36; //i has the value 36
*ip = 72; //Most likely, causes a segmentation fault
ip = & i; //ip references memory address 3245
*ip = 72; //Memory address 3245 has value 72 (so i = 72)
```

The reason ***ip = 72** will cause problems is that *ip* currently holds some random memory address, since it has not been initialized. When we say **ip*, we're trying to access the memory at that random spot. This is most likely not the program's memory, so we will get a segmentation fault when we try to change it. (The other possibility is that we could end up overwriting one of the other program variables.)
