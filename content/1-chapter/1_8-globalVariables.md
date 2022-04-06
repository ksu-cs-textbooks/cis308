---
title: "Global Variables"
weight: 27
pre: "1.8. "
---

All the variables we’ve seen so far have been *local variables* – variables that are defined within a function. These variables are only visible within that function. 

Consider this function:

```c
int count(void) 
{
	int sum = 0;
	sum++;
	return sum;
}
```

Each time we call *count*, the *sum* variable is set back to 0, and the return value is 1. *sum* does not retain its value across function calls. 

If we did want this function to keep track of how many times it had been called, we could store *sum* as a *global variable*. Global variables are declared outside any function, and are visible to any function in the same file:

```c
int sum = 0;
int count(void) 
{
	sum++;
	return sum;
}
```

Now, *sum* does not get set back to 0 each time the function is called.

Global variables should be declared at the top of the file, near the function
prototypes (but before any function implementation). If a global variable is
declared in the middle of a file, some compilers will not allow you to refer to that variable in any function that comes before its declaration.