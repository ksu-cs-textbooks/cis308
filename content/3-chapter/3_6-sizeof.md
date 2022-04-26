---
title: "sizeof"
pre: "3.6. "
weight: 45
date: 2018-08-24T10:53:26-05:00
---

The *sizeof* function in C returns the number of bytes needed to store a specified type. It is
needed for dynamic memory allocation because we need to know how many bytes we want to
allocate.

Here is the prototype:

```c
int sizeof(type);
```

where *type* is a defined type in C, like *char* or *int**. Here are a few examples:

```c
sizeof(int) 	//evaluates to 4
sizeof(char) 	//evaluates to 1
sizeof(double) 	//evaluates to 8
sizeof(int*) 	//evaluates to 4
sizeof(char*) 	//evaluates to 4
```