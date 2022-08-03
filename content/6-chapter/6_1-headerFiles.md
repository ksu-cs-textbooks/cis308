---
title: "Header Files"
pre: "6.1. "
weight: 70
date: 2018-08-24T10:53:26-05:00
---

Our first step in writing a program with multiple files is to just
divide related functions into different .c files. However, suppose
we're in our main function and we call a function from a different
file? This is just like calling a C library function without using any
include statements. The compiler will not know where to find the
outside function.

To solve this within the C libraries, function prototypes are placed
in header files (.h files). The functions themselves are
implemented in corresponding .c files. If I want to use a C library
function, I include the appropriate header file so that the compiler
knows about the function.

This is what we will do with our C programs. First, we will have a
"main file" that contains the main function and any other function
we do not want to reuse. This code will stay in a .c file as we've
done before. Then, we will divide other functions among several
.c files (functions that are related in some way are usually put in
the same file). For each of these .c files, we will make a corresponding .h file
with the same name that contains the prototypes of each
function. Finally, we will include these header files from our main
file.

## One-File Program
To see how this works, consider the example below, which is in
the file `prog.c`:

```c
#include <stdio.h>
#include <stdlib.h>

//later, we will move these three prototypes into stats.h
int min(int*, int);
int max(int*, int);
double avg(int*, int);

//main function will stay here
int main() {
    int* nums;
    int i, length;

    printf("Enter size of array: ");
    scanf("%d", &length);

    nums = malloc(length*sizeof(int));
    for (i = 0; i < length; i++) {
        printf("Enter a number: ");
        scanf("%d", nums+i);
    }

    printf("The min is: %d\n", min(nums, length));
    printf("The max is: %d\n", max(nums, length));
    printf("The average is: %.2lf\n", avg(nums, length));

    return 0;
}

//later, we will move these three functions into stats.c
int min(int *vals, int size) {
    int min = vals[0];
    int i;
    for (i = 1; i < size; i++) {
        if (vals[i] < min) {
            min = vals[i];
        }
    }

    return min;
}

int max(int *vals, int size) {
    int max = vals[0];
    int i;
    for (i = 1; i < size; i++) {
        if (vals[i] > max) {
            max = vals[i];
        }
    }

    return max;
}

double avg(int *vals, int size) {
    int sum = 0;
    int i;
    for (i = 0; i < size; i++) {
        sum += vals[i];
    }

    return sum/(double)size;
}
```

## Multiple Files Program
Suppose we want to be able to reuse our `min`, `max`, and `avg`
functions. We would create a new file, `stats.h`, with the
`min`, `max`, and `avg` prototypes:

```c
// stats.h
#ifndef STATS_H
#define STATS_H

int min(int*, int);
int max(int*, int);
double avg(int*, int);
#endif
```

(Notice the `ifndef` statement, and defining the constant
`STATS_H`. This is standard when writing header files to keep the
same code from being included twice. Just surround your .h file
with a similar statement – changing the `STATS_H` constant to
match your header file's name.)

Next, we would create the new file `stats.c` with the implementations of
the `min`, `max`, and `avg` functions:

```c
//stats.c

//We must include the corresponding header file
#include "stats.h"

int min(int *vals, int size) {
    int min = vals[0];
    int i;
    for (i = 1; i < size; i++) {
        if (vals[i] < min) {
            min = vals[i];
        }
    }

    return min;
}

int max(int *vals, int size) {
    int max = vals[0];
    int i;
    for (i = 1; i < size; i++) {
        if (vals[i] > max) {
            max = vals[i];
        }
    }

    return max;
}

double avg(int *vals, int size) {
    int sum = 0;
    int i;
    for (i = 0; i < size; i++) {
        sum += vals[i];
    }

    return sum/(double)size;
}
```

Finally, we can rewrite our main file, `prog.c`:

```c
//prog.c
#include <stdio.h>
#include <stdlib.h>

//include our header file
//use "" since it is in the current directory
#include "stats.h"

int main() {
    int* nums;
    int i, length;

    printf("Enter size of array: ");
    scanf("%d", &length);

    nums = malloc(length*sizeof(int));
    for (i = 0; i < length; i++) {
        printf("Enter a number: ");
        scanf("%d", nums+i);
    }

    printf("The min is: %d\n", min(nums, length));
    printf("The max is: %d\n", max(nums, length));
    printf("The average is: %.2lf\n", avg(nums, length));

    return 0;
}
```

Header files can also contain definitions of types needed for the
corresponding .c file, like structs, unions, and enums.

## Compiling with Multiple Files
The way we would compile the original statistics program (in the file `prog.c`) is:

```text
gcc prog.c
```

Now that our program is in two files, we might try:

```text
gcc prog.c stats.c
```

or

```text
gcc stats.c
gcc prog.c
```

...but in fact neither of these statements will get our program to
compile. The trouble is that the C compiler first compiles each .c
file, and then tries to link each of the files together into a single
executable. If we don't tell the compiler how the files are related,
it won't be able to properly link them.

To compile our new program, we must first compile each file
separately:

```text
gcc –c stats.c
gcc –c prog.c
```

The –c option forces the compiler to stop after compiling the file,
before trying to link the files or create an executable. These two
instructions will create the object files `stats.o` and `prog.o`,
respectively. 

Now, we need to link these two compiled files into
an executable:

```text
gcc stats.o prog.o
```

This line will create the executable `a.out`, which we can now run
as usual.