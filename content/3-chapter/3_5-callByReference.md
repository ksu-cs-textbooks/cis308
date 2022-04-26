---
title: "Call by Reference"
pre: "3.5. "
weight: 44
date: 2018-08-24T10:53:26-05:00
---

C functions are naturally call-by-value, which means that we don’t pass variables themselves –
we pass their value. So, if we modify one of the parameters in our function, it does not modify
the original variable passed to the function. Consider the following example:

```c
//This example doesn’t work!
void swap(int a, int b) {
	int temp = a;
	a = b;
	b = temp;
}

//assume the test code below is in another function
int x = 3;
int y = 4;
swap(x, y);
```

This code fragment is supposed to swap the values in *x* and *y*, so that **x = 4** and **y = 3**.
However, when we call *swap*, only the VALUES 3 and 4 are passed – not *x* and *y* themselves.
The values 3 and 4 get bound to the function parameters *a* and *b*. By the end of the function, we
do have that **a = 4** and **b = 3**. However, *x* and *y* don’t change because they are completely
different from *a* and *b*.
If we do want to change *x* and *y*, we need to pass in the address of *x* and the address of *y*. Then,
we can update the values at those memory locations. Here is our revised *swap* function:

```c
//Take two memory addresses (pointers)
void swap(int *a, int *b) {
	int temp = *a; 	//Store the value pointed to by a
	*a = *b; 		//Update the contents of a to be the contents of b
	*b = temp; 		//Update the contents of a to be temp
}
```

Now, when we call *swap*, we will need to pass the memory address of the variables we want to
swap. This means we need to use the & operator:

```c
int x = 3;
int y = 4;
swap(&x, &y);
```