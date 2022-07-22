---
title: "Syntax Mistakes"
pre: "7.5. "
weight: 84
date: 2018-08-24T10:53:26-05:00
---

## Incorrect syntax



```c
//WRONG for pointer-to-function
int *pfi(); 
```

and	this	would	declare	a	function	returning	a	pointer	to int.	With	the	explicit	parentheses,	
however, `int (*pfi)()` first tells	us	that `pfi` is	a	pointer,	and	that	what	it's	a	pointer	to	
is	a	function,	and	what	that	function	returns	is	an int.