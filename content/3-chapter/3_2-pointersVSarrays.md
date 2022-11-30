---
title: "Pointers vs. Arrays"
pre: "3.2. "
weight: 41
date: 2018-08-24T10:53:26-05:00
---
Arrays and pointers have a lot in common. When we do:

```c
int nums[10];
```

Then we get a spot in memory that looks like this:

![new array](/images/emptyArray.png)

But what is *nums*? It is actually a constant pointer to the first spot in the array, `nums[0]`. So really, the picture looks like this:

![nums array](/images/numsArray.png)

So, `&nums[0]` (the address of the first element in the array) is the same thing as `nums`.

## Pointer Notation
Because pointers and arrays are essentially the same thing (except array addresses cannot be
changed), we can also access elements in an array by treating it as a pointer. In the above
example, `nums` is a pointer to the first spot in the array. Space for arrays is reserved
contiguously, so the second element in the array is physically next to the first element. This
means that I can say:

```text
nums+1
```

to get the memory address of the second element in the array.

Note: an integer uses 4 bytes of space. However, you don’t say `nums+4` to move to the next
integer. This is because pointers have a particular type associated with them – like an int – and
the compiler will automatically move over the space of an int when you say `+1`.

Suppose now that you want to initialize the value at index 4 in the `nums` array to 7. You could
say:

```c
nums[4] = 7;
```

However, you could do the same thing by treating *nums* as a pointer. You can get the address of
the array element at index 4 by saying:

```c
nums+4
```

This is a pointer, so if we want to change the contents of that location to 7, we need to
dereference it:

```c
*(nums+4) = 7;
```

## Example
Recall that an array is a constant pointer to a block of reserved memory. This means that we can
change the values stored in the array, but we can’t change the array itself (make it reference
another piece of memory). Consider the following statements – which are legal?

```c
int a[10]; 		//OK – a points to a block of 10 ints in memory
a++; 			//NO – The address of an array can’t change
int *xp = a;	//OK – Now xp also points to the beginning of the array
a = xp; 		//NO – The address of an array can’t change
int b[5]; 		//OK – b points to a block of 5 ints in memory
int *bp = b;	//OK – Now b also points to the beginning of the array
xp++; 			//OK – Now xp points to the second element in the array
*xp = 14; 		//OK – The second element in the array is set to 14 (a[1] = 14)
```