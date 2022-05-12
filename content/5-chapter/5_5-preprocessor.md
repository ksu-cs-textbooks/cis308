---
title: "Preprocessor Directives"
pre: "5.5. "
weight: 64
date: 2018-08-24T10:53:26-05:00
---
The C pre-processor is a special program that runs before the C
compiler. It processes every line that begins with a #, such as a
#include statement. The pre-processor may add, remove, or
change your code when handling the # statements.

## #include
We’ve been using the #include statement since our first
program in order to get access to C's library functions (like
printf in stdio.h). When the pre-processor sees a
#include statement, it replaces the #include line with the
contents of the included file. For example, when the pre-processor
sees:

```c
#include <stdio.h>
```

then it replaces that line with the contents of the `stdio.h` file (which includes definitions for `printf`,
`scanf`, `fprintf`, etc.). Then, when the compiler sees a call to
`printf`, it knows what you mean because `printf` is defined in
your file.

Including a file like:

```c
#include <stdio.h>
```

tells the pre-processor to look for `stdio.h` in the standard
include directory (which is where all the library files live). If
instead you say:

```c
#include "stdio.h"
```

the pre-processor will first look for `stdio.h` in the current
directory. If it can't find the file, it will hen look in the standard
include directory.

## #define
The `#define` statement tells the pre-processor to find all
occurrences of one value in your code, and to replace them with
another value. This can be used in two ways: to define constants
and to define macros (simplified functions).

### Constants
A constant in C is defined like this:

```c
#define name value
```

Here, `name` is the name we are giving the constant, and value is
the value we would like it to have. Here is an example:

```c
#define PI 3.14159
```

Now, we can use `PI` in our code when we want the value
3.14159. For example:

```c
int radius = 10;
double area = PI * radius * radius;
```

When the pre-processor sees a `#define` constant, it replaces all
occurrences of the constant's name with it's specified value. So
by the time the pre-processor gets done with it, the above code
looks like:

```c
int radius = 10;
double area = 3.14159 * radius * radius;
```

### Macros
A macro is simplified function that includes a name and a list of
arguments. They are defined using the `#define` statement, just
like constants. For example:

```c
#define SUM(a, b) a+b
```

When the preprocessor sees a call to the macro, it will replace the
macro call with the macro formula. For example, if we do:

```c
int x = 3;
int y = 4;
int result = SUM(x, y);
```

Then the pre-processor will change the last line to be:

```c
//Uses x as a and y as b in the macro formula
int result = x + y; 
```

Just like other pre-processor directives, the compiler never sees the
macro itself. It only sees the final result, after the pre-processor
has replaced the macro call with the macro formula.

As another example, let's try to write a macro that computes the
difference of two squares:

```c
//This is not right!
#define DIFF_SQUARE(a, b) a*a – b*b 
```

This macro may look right (and this is how we would write a
diffSquare function), but it has some problems. For example:

```c
int x = 4;
int y = 3;
int c = 2;
int d = 1;
int result = DIFF_SQUARE(x-c, y-d);
```

The pre-processor will replace the call to `DIFF_SQUARE` with the
macro value. It will use `x-c` as the value for `a`, and `y-d` as
the value for `b`. Here's what the last line will become:

```c
int result = x-c*x-c – y-d*y-d;
```

However, what we WANT is:

```c
int result = (x-c)*(x-c) – (y-d)*(y-d);
```

To get this substitution, we need to add parentheses to the original
macro:

```c
#define DIFF_SQUARE(a, b) (a)*(a) – (b)*(b)
```

Here is a macro that returns the minimum of two numbers:

```c
#define MIN(a, b) a < b ? a : b
```

This uses the ternary conditional operator. It means: if `a` is less
then `b`, then `a` is the minimum. Otherwise, `b` is the minimum.

Here is a macro that eats all input left in the input buffer. This can
be VERY useful as any unexpected input will stay in the input
buffer. It reads one character at a time until it runs out of input.

```c
#define FLUSH() while (getchar() != '\n')
```

## #ifdef, #ifndef
There is also a pre-processor if-statement that checks to see
whether or not a constant has been defined. Here's the format:

```c
#ifdef (pre-processor constant)
code
#endif
```

The code inside this `#ifdef/#endif` block will only be
compiled if the pre-processor constant was defined. For example:

```c
#define SIZE 10

//(elsewhere)
#ifdef SIZE
int nums[SIZE];
#endif
```

In this example, we only include the `int nums[SIZE];` line
in our program if the `SIZE` constant has already been defined.

There is a similar construct called `#ifndef`, which evaluates to
true if a constant has NOT been defined. For example:

```c
#ifndef SIZE
printf("Define SIZE!\n");
#endif
```
The `printf` statement will only be part of the program if the
`SIZE` constant has not been defined. The `#ifndef` statement
will be very useful when we start to break our programs into
several files – it will help ensure that we don't end up including the
same information twice when we link our files together.