---
title: "Printing"
weight: 22
pre: "1.3. "
---

## *printf* Function

As you've seen, the *printf* function is used to display output in C. For example, to display a string of text:

```c
printf("Hello\n");
```

Note that you always need to specify the newline character (\n). There is
no *println* equivalent in C.

## Printing Variables

Printing variables works a bit differently. First, you specify the kind of variable that's going to be printed (called a control string). Then, outside the string, you give the corresponding variable name.

Here are the different control strings:

| Type | Control String |
|-----|----------------|
| int | %d |
| double | %lf |
| float | %f |
| char | %c |
| char* (string) | %s (see String section) |

It's easiest to see an example to figure out how printing works. Here's how to print the value of an integer to the screen:

	int num = 4;
	printf("The value of num is %d\n", num);

Notice that where we want to print a variable, we put the control string
(*%d* for int). After we've listed the entire string, we put the corresponding variable names as the next arguments to *printf*. The above example will print:

 	"The value of num is 4" 

to the screen.

We can also print several variables at once:

```c
char letter = 'A';
int val = (int) letter;
printf("The ASCII value of %c is %d\n", letter, val);
```

This prints:

	"The ASCII value of A is 65"

to the screen. Notice that the *%c* corresponds to the *letter* argument, and the *%d* corresponds to the *val* argument.

## Formatting

The *printf* function also allows you some control over formatting your output. For example, if you want a value to take up exactly 6 spaces (padded with space characters on the left, if necessary), put a 6 between the % and the control string character. 

For example:

```c
int num = 4;
printf("The value of num is %6d\n", num);
```

This will print:

	"The value of num is 4" 

to the screen (note the padding on the left of the 4).

You can also only display a certain number of digits for decimal numbers. For
example, put a .2 in between the % and the control string character to only display two decimal places. 

For example:

```c
double val = 3.14159;
printf("Pi is %.2lf\n", val);
```

This will display:

 	"Pi is 3.14" 

You can specify both the width of the output (for example, six spaces) and the number of decimals to display by doing something like this:

```c
double val = 3.14159;
printf("Pi is %6.2lf\n", val);
```
