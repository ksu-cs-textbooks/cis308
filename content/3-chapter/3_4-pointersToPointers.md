---
title: "Pointers to Pointers"
pre: "3.4. "
weight: 43
date: 2018-08-24T10:53:26-05:00
---

Just like a variable can be a pointer, we can also declare pointers to pointers. (We can take it
even further than that, but it starts to get pretty confusing!) You can denote the "level" of the
pointer by how many *’s you use in the declaration.

Here's an example of using pointers to pointers:

```c
int i; 		//declares the int i
int *ip; 	//declares the int pointer ip
int **ipp; 	//declares a pointer to a pointer to an int, ipp
i = 36; 	//gives i the value 36
ip = &i; 	//now ip points to i
*ip = 72; 	//dereferences ip to get i, and sets it to 72 (now i=72)
ipp = &ip; 	//ipp points to ip, which points to i
**ipp = 24; //dereferences ipp to get ip, then dereferences again to get i,
			//and sets it to 24 (now i = 24)
```