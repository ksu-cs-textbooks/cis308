---
title: "Returning Pointers from Functions"
pre: "3.9. "
weight: 48
date: 2018-08-24T10:53:26-05:00
---

We can also return pointers from functions, via
pointer arguments rather than as the formal return value. To explain this, let's first step back and
consider the case of returning a simple type, such as int, from a function via a pointer argument. 

If we write the function:

```c
f(int *ip) {
    *ip = 5;
}
```

And then call it like this:

```c
int i;
f(&i);
```

then `f` will "return" the value 5 by writing it to the location specified by the pointer passed by the
caller; in this case, to the caller's variable `i`. A function might "return" values in this way if it had
multiple things to return, since a function can only have one formal return value (that is, it can only
return one value via the return statement.) The important thing to notice is that for the function to
return a value of type int, it used a parameter of type pointer-to-int.

Now,	suppose	that	a	function	wants	to	return	a pointer in	this	way.	The	corresponding	parameter	will	
then	have	to	be	a	pointer	to	a	pointer.	For	example,	here	is	a	little	function	which	tries	to	allocate	
memory	for	a	string	of	length `n`,	and	which	returns	zero	(`false`)	if	it	fails	and	1	(nonzero,	or	`true`)	
if	it	succeeds,	returning	the	actual	pointer	to	the	allocated	memory	via	a	pointer:

```c
#include <stdlib.h>
int allocstr(int len, char **retptr) {
     //+1 for the \0 character
    char *p = malloc(len + 1);
    if(p == NULL) {
        return 0;
    }

    *retptr = p;
    return 1;
}
```

The caller can then do something like:

```c
char *string = "Hello, world!";
char *copystr;
if(allocstr(strlen(string), &copystr)) {
    strcpy(copystr, string);
}
else {
    printf(stderr, "out of memory\n");
}
```

(This is a crude example; the `allocstr` function is not terribly useful. It would have been just about as
easy for the caller to call `malloc` directly. A different, and more useful, approach to writing a *wrapper*
function around `malloc` is exemplified by the `chkmalloc` function we've seen before.)

One side point about pointers to pointers and memory allocation: although the `void*` type, as returned
by `malloc`, is a *generic pointer*, suitable for assigning to or from pointers of any type, the hypothetical
type `void**` is NOT a *generic pointer to pointer.* Our `allocstr` example can only be used for allocating
pointers to ``char`. 

It would not be possible to use a function which returned generic pointers indirectly
via a `void** pointer, because when you tried to use it, for example by declaring and calling:

```c
double *dptr;
if(!hypotheticalwrapperfunc(100, sizeof(double), &dptr)) {
    printf(stderr, "out of memory\n");
}
```

you would not be passing a `void**`, but rather a `double**`.