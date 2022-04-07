---
title: "Arrays"
weight: 30
pre: "2.1. "
---

Arrays in C are, for the most part, the same as arrays in Java or C#. Here are the key differences:

- Arrays in C must be of a **constant size** (not a variable size from user input, for example)
- Arrays in C **do not have an associated length field** that keep track of the number of slots in the array (you must keep track of this information yourself)


## Declaring

Here is the format for declaring an array:

```c
type name[size];
```

Here, *type* is the type of elements you want to store in the array (like int), *name* is the name of the array, and *size* is how many slots you want to reserve. **Note that *size* MUST be a constant.** 

Here is an example:

```c
int nums[10];
```

However, the following will not compile because the size is given by a variable:

```c
//this code will not compile as size is not constant
int size = 10;
int nums[size];
```

## Initializing

Unlike Java, arrays in C are not initialized to any value. Instead, each slot in the array holds some random garbage value that is leftover in that spot in memory. 

Here is how you could initialize all the values in the *nums* array to 0:

```c
int i;
for (i = 0; i < 10; i++) {
	nums[i] = 0;
}
```

Notice that the first index in the array is 0, and the last index is *size-1*. Also, recall that arrays do not have a length field – we must remember that we reserved 10 spaces for *nums*.

## Arrays and Functions

Arrays can be passed to functions just like any other variable. Because arrays don't have a length field, you will almost always want to pass the size of the array and the array itself. Here's an example:

```c
#include <stdio.h>

//function prototype – takes an array of ints and its size
void print(int[], int);

int main() 
{
	int nums[10];
	int i;
	for (i = 0; i < 10; i++) 
	{
		nums[i] = i;
	}

	print(nums, 10);

	return 0;
}

void print(int arr[], int size) 
{
	int i;
	for (i = 0; i < size; i++) 
	{
		printf("%d\n", arr[i]);
	}
}
```

## Multi-Dimensional Arrays
You can create multi-dimensional arrays in C by specifying extra dimensions at the time of declaration. For example, this declares a 5x10 array of characters:

```c
char array[5][10];
```

The first dimension is the row and the second dimension is the column. To access an array element, specify the desired row and column number. For example:

```c
//sets element at row 2, column 3 to 'A'
array[2][3] = 'A'; 
```

## Be Careful!
If you access an array element in Java or C# with an index that is either negative or too big, you will get some kind of array index exception. Those languages will even tell you in what file and on what line the error occurred.
C is not as friendly about this mistake. If you access an element with a bad index, such as:

```c
int nums[10];
nums[10] = 0; //10 is past the bounds of the array
```

Then one of two things will happen:

1) C will allow you to modify the memory that is just past the end of your array (where spot 10 would be if there were that many spots). This memory might belong to one of your other variables!
2) Your program will crash with a segmentation fault (seg fault). You will see this error quite a bit when you get started in C – it means that you tried to access memory that isn't yours. Unfortunately, the error message does not give you any information about where the problem occurred – you will have to find it yourself.