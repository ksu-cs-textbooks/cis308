---
title: "Functions and Function Pointers"
pre: "7.2. "
weight: 81
date: 2018-08-24T10:53:26-05:00
---

Since a function pointer is a valid type, we can pass function pointers as arguments to functions and can also return them from functions.

## Passing Function Pointers to Functions

Recall that the syntax for declaring a function ponter is:

```c
return_type (*ptr_name) (args);
```

Where `ptr_name` is the new variable name for a function pointer that returns something of type `return_type` and that takes the argument types described in `args`. We can similarly accept a function pointer as an argument to a function using the same syntax.

For example, consider the following program:

```c
#include <stdio.h>

int plus(int a, int b) {
    return a + b;
}

int minus(int a, int b) {
    return a - b;
}

int times(int a, int b) {
    return a * b;
}

int divide(int a, int b) {
    return a / b;
}

//op is a function pointer to a function that takes two integer arguments
//and returns an integer result
int doOperation(int (*op)(int, int), int x, int y) {

    //calls the function pointed to by op and returns the result
    return op(x, y);
}

int main() {
    int num1 = 3;
    int num2 = 4;

    printf("Added result: %d\n", doOperation(plus, num1, num2));
    printf("Multiplied result: %d\n", doOperation(times, num1, num2));

    return 0;
}
```

The code above will print:

```text
Added result: 7
Multiplied result: 12
```

The above example might seem unnecessarily complicated, as we could have directly called `plus` and `times` from `main` and bypassed the `doOperation` function altogether. However, using function pointers as arguments can be very powerful -- for example, the `stdlib` library defines a `qsort` function that accepts a comparator function pointer as an argument. This way, we can use the same sorting function to sort in a variety of ways -- ascending order, descending order, by length, etc. -- by passing in a different comparator function pointer. We will demonstrate this process in lab.

## Typedef and Function Pointers

Listing the type of function pointers can be tedious and error-prone. It can be much easier to use `typedef` once to create a new (more simply named) type representing a particular kind of function pointer, and then use the new type name after that. For example, in our math operations program above, we can first create a new type name for our function pointer type:

```c
typedef int (*function) (int, int);
```

This creates a new type called `function` that represents a function pointer to a function that returns an int and takes two int arguments. We can then use the type `function` in our `doOperation` method instead of writing out the argument `int (*op)(int, int)`. Here is the new `doOperation` function:

```c
int doOperation(function op, int x, int y) {

    //calls the function pointed to by op and returns the result
    return op(x, y);
}
```

Note that the type name `function` can be anything -- this is just the new type name we happened to pick when using `typedef`.

## Returning Function Pointers from Functions

Returning function pointers from functions is exactly the same idea as returning any other other type from a function. Ideally, we would first use `typedef` to create a new type name for the desired type of function pointer. For example, we could add a new function to our operations example above that returns a pointer to the correct operation function based on a char argument:

```c
function getOperation(char c) {
    if (c == '+') {
        return plus;
    }
    else if (c == '-') {
        return minus;
    }
    else if (c == '*') {
        return times;
    }
    else {
        //will return 'divide' if a non-operation char argument
        //is passed

        return divide;
    }
}
```

Then, we could use our `getOperation` function to get the correct operation based on user input:

```c
char op;
int num1, num2;

printf("Enter number op number (no spaces, like 3+2): ");
scanf("%d%c%d", &num1, &op, &num2);

function opResult = getOperation(op);
printf("Result: %d\n", opResult(num1, num2));
```

By saving the correct operation function in `opResult`, we could then call `opResult` (which would call either `plus`, `minus`, `times`, or `divide` based on the value of `op`) to get the result of the operation.

