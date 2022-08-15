---
title: "User Input"
weight: 23
pre: "1.4. "
---

User input in C is, in short, a pain. There are three major input functions:
`getchar()`, `scanf(...)`, and `scanf_s(...)`. To use any of these functions, you must include the `stdio.h` library.

## `getchar()`

The `getchar()` function takes no arguments and returns the very next character in the standard input stream. If there are no more characters in the input stream, it returns the constant `EOF`. 

Here's an example that reads a student's letter grade and then prints it back to the console.

```c
char grade;
printf("Enter your grade: ");
grade = getchar();
printf("Your grade is %c\n", grade);
```

## `scanf(...)`

The `scanf(...)` function allows us to read formatted input, like ints and
doubles. 

The first argument to `scanf` is the format string, which specifies the kind of data you expect to read. To specify the data types you expect, use the same control string characters you used for printf -- %d, %f, %lf, %c, and %s. If you want to read an int, the first argument to scanf should be "%d". If you want to read two ints, put "%d %d".

The next arguments to `scanf` are the corresponding variables that you want to store the input in. We won't go into details now, but `scanf` needs the memory address of these variables so it can modify their value. To get the address of a variable, put a & in front of the variable name.

Here's a simple example that prompts the user for an integer, and then reads in the value:

```c
int num;
printf("Enter a number: ");
scanf("%d", &num); 
//%d: we're reading in an integer
//&num: we're storing that integer in the num variable
```

Here's an example that reads in an integer and a double:

```c
int num1;
double num2;
printf("Enter an int and a double: ");
scanf("%d %lf", &num1, &num2);
```

The first number typed will get stored in `num1`, and the second number will get stored in `num2`. Our format string specified that these numbers should be separated by a space, but they can be separated by any amount of whitespace (multiple spaces, tabs, or newlines).

Suppose that the user is entering a fraction, like 9/5. Here's how we could read in that information:

```c
int numerator, denominator;
printf("Enter a fraction (like 9/5): ");
scanf("%d/%d", &numerator, &denominator);
```

By putting the "/" in the format string, we specify that we expect the input to have a / there, but we don't wish to store it in a variable.

`scanf` returns the number of variables that were correctly read in. If an error occurred during input, it returns the constant `EOF`.

Here is an (incomplete) list of subtleties when using `scanf`:
- In most cases, `scanf` skips whitespace. However, if you type a space (or tab or newline) where `scanf` expects a character,
it will read the whitespace into your `char` variable.
- If you use `scanf` to read a single character, then the user will type an input character and then hit return. `scanf` will read the input character, but
the newline will remain in the input buffer. This can cause problems if you
call `scanf` a second time – the newline character will then be read, and not
any new input. To fix this problem, add a call to `getchar()` after reading
a char to read the extra newline character.
- If `scanf` reads input that it does not expect (for example, if it sees a
character but is supposed to be reading an int), it will not discard the bad
input. The bad input will still be in the input buffer if you
call `scanf` again. To fix this, call `getchar()` until you reach `EOF`. This
will clear the input buffer.


In the next chapter, we will see that `scanf` can be very dangerous to use when reading strings from user input. In short, if the user enters a string that is longer than expected, `scanf` can accidentally overwrite other parts of memory. This can even be exploited using a *buffer overflow attack* by tricking `scanf` into reading in program instructions.