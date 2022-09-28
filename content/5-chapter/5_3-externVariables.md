---
title: "Extern Variables"
pre: "5.3. "
weight: 62
date: 2018-08-24T10:53:26-05:00
---

Sometimes when our program is in multiple files, we still want to
define variables that are visible to each file. Here's how to do this:

1) Declare the global variable in a .h file. This can either
be done in a .h file with some of your function
prototypes, or in a special file, globals.h, that
contains the declarations of all global variables. If you
do use a special globals header file, it does not need a
corresponding .c file.
2) Include the .h file wherever you want to use the
variable
3) When you want to use the variable, declare:

```text
extern type name;
```

where `type` is the type of the global variable, and
`name` is its name. The `extern` keyword tells the
compiler not to create a new variable, but instead to
find the variable name declared in another file.

As an example, suppose we want to make the array size a global
variable in our for our earlier [statistics program]({{<ref "5-chapter/5_1-headerFiles.md" >}}). Here's
what we'd do:

```c
//start of stats.h
#ifndef STATS_H
#define STATS_H

//define array size
int size;

//functions no longer need array lengths
int min(int*);
int max(int*);
double avg(int*);

#endif
//end of stats.h

////////////////////////////

//start of stats.c

//We must include the corresponding header file
#include "stats.h"

//say we're going to use the size variable
extern int size;

int min(int *vals) {
    int min = vals[0];
    int i;
    for (i = 1; i < size; i++) {
        if (vals[i] < min) {
            min = vals[i];
        }
    }

    return min;
}

int max(int *vals) {
    int max = vals[0];
    int i;
    for (i = 1; i < size; i++) {
        if (vals[i] > max) {
            max = vals[i];
        }
    }

    return max;
}

double avg(int *vals) {
    int sum = 0;
    int i;
    for (i = 0; i < size; i++) {
        sum += vals[i];
    }

    return sum/(double)size;
}
//end of stats.c

/////////////////////////

//start of prog.c
#include <stdio.h>
#include <stdlib.h>

//include our header file
//use "" since it is in the current directory
#include "stats.h"

//declare that we're using the size variable
extern int size;

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

    printf("The min is: %d\n", min(nums));
    printf("The max is: %d\n", max(nums));
    printf("The average is: %.2lf\n", avg(nums));

    return 0;
}

//end of prog.c
```

Notice that we declare the variable in a header file. When we want
to use the `size` variable, we first include that header file. Then,
we declare `size` as an extern variable.