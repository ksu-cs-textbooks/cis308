---
title: "Functions"
weight: 26
pre: "1.7. "
---

Functions in C are very similar to methods in other languages, except functions are not associated with any class. (They are like static methods in Java and C#.) They take a number of parameters, perform on operation on those parameters, and may or may not return a value.

## Function Prototypes
Some C compilers will complain if they see a call to a function before they’ve seen the function itself. To avoid this problem, it’s best to include a prototype for a function at the top of the file, and then to implement it someplace else in the file. 

A *prototype* lists the name, return type, and parameters for a function – but it does not implement the function. Here’s an example:

```c
int max(int num1, int num2);
```

We list the return type (`int`), the function name (`max`), and the parameters with their types (`int num1` and `int num2`). This is a prototype, so we don’t implement the function here. Instead, we end it with a semi-colon. (Note that this already looks very similar to other languages – the only difference is that C functions are not associated with classes, so they don't need a visibility modifier like `private` or `public`.)

Return types can be any valid type (like `char`, `int`, `double`, etc.). If the function does not return a value, its return type should be `void`.

In a prototype, you don’t have to list the names of the parameters – you just need to list the types. For example, this would also be a valid prototype for the `max` function:

```c
int max(int, int);
```

If you are writing a prototype for a function that takes no parameters, you can leave the parameter list blank, like this:

```c
int getNum();
```

However, a better way would be to put `void` in the parameter list, like this:

```c
int getNum(void);
```

When the compiler sees a blank parameter list in the prototype, it will allow ANY parameter list in the function implementation. However, if it sees `void` in the prototype’s parameter list, then the implementation must also have a `void` parameter list.

## Function Implementations
A function implementation starts off the same as a prototype. Instead of ending with a semi-colon, it includes the code for the function in brackets { }. 

Here’s the implementation of the `max` function:

```c
int max(int num1, int num2) 
{
	if (num1 >= num2) return num1;
	else return num2;
}
```

Like in other languages, if a C function has a non-void return type, it must include a *return statement* that returns a value of the designated type.

## Calling Functions
For now, all our programs are in one file, so calling functions is pretty easy. You just put the function name and include appropriate parameters, as if you were calling function from within the same class in Java or C#. 

Here’s a full example of a C program that uses the `max` function:

```c
#include <stdio.h>

//max function prototype
int max(int, int); 

int main() 
{
	int val1, val2, big;
	printf("Enter two ints, separated by spaces: ");
	scanf("%d %d", &val1, &val2);
	big = max(val1, val2);
	printf("The max is %d\n", big);

	//This indicates the program is ending normally
	return 0; 
}

//max function implementation
int max(int num1, int num2) 
{
	if (num1 >= num2) return num1;
	else return num2;
}
```