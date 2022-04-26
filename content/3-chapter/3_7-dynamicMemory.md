---
title: "Dynamic Memory"
pre: "3.7. "
weight: 46
date: 2018-08-24T10:53:26-05:00
---

Currently, we can only declare arrays to be of a constant size (like 10). This is not always
convenient – sometimes we want to make the size based on some user input. If we want to
allocate a dynamic amount of space, we need to use C's dynamic memory functions. Each of
these functions is in **<stdlib.h>**.

## malloc
This function allocates a contiguous block of memory with the specifies size (number of bytes).
It returns a void pointer to the block of memory. (This pointer will be automatically cast to the
correct type when you store it.) 

Here is the prototype:

```c
void* malloc(int numBytes);
```

For example, we could allocate an array like this:

```c
int nums1[5];
```

Or we could do the same thing using *malloc*. If we use *malloc*, we need to specify the
number of bytes to reserve. We want 5 ints, and each int takes up **sizeof(int)** bytes. So,
the total needed is **5*sizeof(int)**:

```c
//The result of malloc is automatically cast to an int*
int* nums2 = malloc(5*sizeof(int));
```

Now, we can treat *nums2* just like an array. For instance, if we wanted to initialize all elements
in *nums2* to 0:

```c
int i;
for (i = 0; i < 5; i++) {
	nums2[i] = 0; 	//The compiler converts this to *(nums2+i) = 0
}
```

Allocating arrays with malloc has several key difference from standard array allocation:
- *malloc* can handle a variable for the desired size; a standard array cannot
- The result of *malloc* is a pointer; the result of a standard array allocation is a constant pointer
- *malloc* memory is allocated on the heap. If there is not enough space to do the allocation, *malloc* will return NULL. An array is allocated on the program stack – if there is not enough space, the program simply won't compile.

## calloc
The *calloc* function is very similar to *malloc*. The only difference is that when arrays are
allocated using *calloc*, all elements are automatically initialized to 0. 

Here is the prototype:

```c
void* calloc(int numElems, int sizePerElem);
```

The prototype of *calloc* is also a little different than the one for *malloc*. It takes two
arguments – the number of elements you want in the array, and the number of bytes needed for
each elements. Like *malloc*, *calloc* returns a void pointer to the contiguous block of
memory it allocated. This pointer will be automatically cast to the appropriate type when you
store it.

Here's how to create an array of 10 ints, all initialized to 0:

```c
int* nums = calloc(10, sizeof(int));
```

Now you can use *nums* just like an array. For example:

```c
nums[0] = 4;
```

Like *malloc*, *calloc* will return NULL if there is not enough space to do the allocation. In
both cases, it's a good idea to check if the pointer is NULL before you use it. 

For example:

```c
int* nums = calloc(10, sizeof(int));
if (nums == NULL) {
	printf("Not enough space.\n");
}
else {
	//Use nums as usual
}
```

## realloc
The *realloc* function allows you to easily expand and shrink the space allocated for an array.

Here is the prototype:

```c
void* realloc(void* origPtr, int newSize);
```

This function takes your original pointer and the desired new size in bytes. It looks for a
contiguous block of memory with the desired size. If it can find one, it copies the contents of the
old array into the new block of memory. Then it releases the space needed for the old array, and
returns a void pointer to the new block of memory.

The *realloc* function doesn't always behave as you intend. Here are the possible return
values of *realloc*:
- NULL (if not enough space is found)
- The original pointer (if there is enough space at that location)
- A new pointer to a different spot in memory

Suppose we allocate the nums array like this:

```c
int* nums = malloc(10*sizeof(int));
```

Now we decide that we want *nums* to hold 15 elements instead of 10. Here's what we might
try:

```c
nums = realloc(nums, 15*sizeof(int));
```

Suppose that *realloc* could not find enough space to grant the request – so it returns NULL.
This means that we assign NULL to our original *nums* pointer. Now *nums* does not reference
the original array – in fact, nothing does. The original array is stuck in memory with no way to
get at it – this is called a memory leak.

To fix this problem, assign a temporary pointer to the result of *realloc*. Then, if it's not
NULL, reassign the original pointer. This keeps you from losing your array:

```c
int *temp = realloc(nums, 15*sizeof(int));
if (temp != NULL) {
	nums = temp;
}
```

## free
In Java and C#, any memory that you're no longer using will be cleaned up by the garbage collector. C
has no garbage collector, so you are in charge of releasing memory that you're done with. If you
never release any allocated memory, you will eventually run out of space.

The C function that releases dynamic memory is called *free*. Here is the prototype:

```c
void free(void* pointer);
```

Note that even though *free* takes a void pointer, it can take any type of pointer that has been
dynamically allocated. 

Here's an example of using *free*:

```c
int* nums = malloc(10*sizeof(int));
int i;
for (i = 0; i < 10; i++) {
	nums[i] = i;
}

//done using nums
free(nums);
```