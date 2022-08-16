---
title: "Strings"
weight: 31
pre: "2.2. "
---

We saw before that there is no string type in C. This is true – but you can simulate a string by using an array of characters that is terminated with a special end-of-string character, '\0'.

## String Variables
A *string constant* can be declared as follows:

```c
char str[] = "Hello";
```

After this line, str references the following characters in memory:

| 0 | 1 | 2 | 3 | 4 | 5  |
|---|---|---|---|---|----|
| H | e | l | l | o | \0 |


We could have created the same string like this:

```c
char str[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

Arrays (and strings) are constant memory addresses. We can change values in strings and arrays, but we can't change the memory address. So, we can do things like this:

```c
str[0] = 'h'; //OK
```

But we can't change the memory address (the entire string):

```c
str = "hi"; //Compiler error!
```

Later in this section, you will see a function called `strcpy` that copies the characters from one string to another.

## String Variables
If you want to be able to modify a string, you need to fill it like a normal array. For example:

```c
char str[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

(You can create and fill an array like this.) Now we can modify the characters in `str`:

```c
str[0] = 'h';
```

## String Input and Output
Strings can be inputted and outputted just like any other variable. To print a string, use `printf` with the `%s` control string character. To get a string as input, use `scanf` (again with the `%s` control string character). 

Here's an example:

```c
char name[10];
printf("Enter your name: "); //Suppose you enter "Fred"
scanf("%s", name);
printf("Hello, %s!\n", name); //Will print "Hello, Fred!"
```

Notice that when you use `scanf` to read in a string, you do not need to put an & in front of the string variable name. This is because a string is an array of characters, and arrays are already memory addresses. (We'll learn more about this in the section on Pointers.)

The trouble with using `scanf` to input strings is that the function doesn't check the size of the array when it is reading input. So, if you typed the name "George Washington" in the above example (which needs 18 characters of space), `scanf` wouldn't stop writing once it reached the end of the array. Instead, it would try to write past the end of the array. This would
cause some of your variables to be overwritten, or a segmentation fault. In the worst case, it could be exploited by a hacker with a *buffer overflow attack*, where the hacker knowingly inserted program instructions beyond the bounds of the input buffer.

A better choice for reading in strings is the `fgets` function. Here's the prototype:

```c
char[] fgets(char s[], int size, FILE *stream);
```

You pass `fgets` the string buffer (`s`), the size of the buffer (`size`), and the stream you're reading from (use `stdin` to read as regular user input). It returns the string it read, or `NULL` if it was unable to read anything. 

It will stop reading user input when either:
- It has read `size-1` characters (it needs the last spot for a '\0')
- It has reached the end of the input
- It has reached a newline

Here is same example using `fgets`:

```c
char name[10];
printf("Enter your name: "); //Suppose you enter "Fred"
fgets(name, 10, stdin);
printf("Hello, %s", name); //Will print "Hello, Fred"
```

NOTE: if `fgets` reaches a newline character before reading `size-1` characters, it WILL store the newline as its last character (just before the `\0`). If the user enters "Fred" in the example above, the `name` array will hold: `{'F', 'r', 'e', 'd', '\n', '\0', (garbage), (garbage), (garbage), (garbage)}`.

If you want to remove that `\n` character, you will need to overwrite the `\n` to hold the end-of-string character instead (`\0`). We will see a convenient trick for doing this in the `strcspn` section below.

## Conversions
It is sometimes necessary to convert between strings, ints, and doubles. Here is a list of conversion functions:
- `atoi`: converts from a string to an int
- `atof`: converts from a string to a double
- `itoa`: converts from an int to a string
- `ftoa`: converts from a double to a string

To use any of these functions, you need to add:

```text
#include <stdlib.h>
```

To the top of the file.

Here is an example of using the conversion functions:

```c
char buff[10];
int num;
double d;

printf("Enter an integer: ");
fgets(buff, 10, stdin); //Suppose you enter "47"
num = atoi(buff); //num = 47

printf("Enter a real number: ");
fgets(buff, 10, stdin); //Suppose you enter "4.75"

d = atof(buff); //d = 4.75
itoa(num, buff, 10); //buff = "47"
itof(d, buff, 10); //buff = "4.75"
```

## String Functions
Below is a list of common string functions. To use any of these, you need to add:

```text
#include <string.h>
```

To to the top of the file.

### strcat
```c
char[] strcat(char str1[], char str2[]);
```

This function copies the characters in `str2` onto the end of `str1`. It returns the newly concatenated string (although `str1` also references the concatenated string).

For example:

```c
char str1[20];
char str2[20];
printf("Enter two words: "); //Suppose you entered "hi hello"
scanf("%s %s", str1, str2);
strcat(str1, str2); 		//str1 = "hihello", str2 = "hello"
```

### strcmp
```c
int strcmp(char str1[], char str2[]);
```

This function compares `str1` and `str2` to see which string comes alphabetically before the other. It returns:
- A number less than 0, if `str1` comes alphabetically before `str2`
- 0, if `str1` equals `str2`
- A number greater than 0, if `str1` comes alphabetically after `str2`

For example:

```c
char str1[20];
char str2[20];
printf("Enter two words: "); //Suppose you entered "hi hello"
scanf("%s %s", str1, str2);

if (strcmp(str1, str2) < 0) {
	printf("%s comes first\n", str1);
}
else if (strcmp(str1, str2) > 0) {
	printf("%s comes first\n", str2);
}
else {
	printf("The strings are equal\n");
}
```
The code above would print "hello comes first".

### strcpy
```c
char[] strcpy(char str1[], char str2[]);
```

This function copies the characters in `str2` into `str1`, overwriting anything that was already in `str1`. It returns the newly copied string (although `str1` also references the copied string).

For example:

```c
char src[20];
char dest[20];

printf("Enter a word: ");
scanf("%s", src); 			//Suppose you entered "hello"

strcpy(dest, src); 			//Now dest also holds "hello"

src[0] = 'B'; 				//Now src is "Bello", and dest is "hello"
```

### strcspn
```c
int strcspn(char str1[], char str2[]);
```

This function returns the number of characters that appear in `str1` before reaching ANY character from `str2`. (If the first character in `str1` also appears in `str2`, then `strcspn` returns 0.)

For example:

```c
char str[20];
int index;

printf("Enter a word: ");//Suppose you entered "hello"
scanf("%s", str);

index = strcpsn(str, "la"); //index is 2
//2 characters appear in str before finding any character from "la"
```

`strcspn` is especially handy for removing the trailing `\n` that gets added to strings when using `fgets`. As we saw earlier in this section, if we do:

```c
char name[10];
printf("Enter your name: ");
fgets(name, 10, stdin);
```

And enter "Fred", then the `name` array will hold `{'F', 'r', 'e', 'd', '\n', '\0', (garbage), (garbage), (garbage), (garbage)}`. We can use `strcspn` to find the index of `\n` and then replace it with a `\0`:

```c
name[strcspn(name, "\n")] = '\0';
```

When `strcspn` gives us the number of characters read before reaching a `\n`, that IS the index of `\n`. In the same line, we can replace that position to be the end-of-string marker, which effectively deletes the newline from the end of the string.

### strlen
```c
int strlen(char str[]);
```

This function returns the number of characters in `str`.

For example:

```c
char str[20];
printf("Enter a word: ");		//Suppose you entered "hello"
scanf("%s", str);

printf("%d\n", strlen(str)); 	//prints 5
```

### strtok
```c
char[] strtok(char str[], char delim[]);
```

This function returns the first token found in `str` before the occurrence of any character in `delim`. (After the first call to `strtok`, pass `NULL` as `str`. This will tell it to continue looking for tokens in the original string.)

For example:

```c
char buff[200];
char *token; //We'll learn about this notation in "Pointers"

printf("Enter names, separated by commas: ");
//Suppose you entered "Fred,James,Jane,Lynn"
scanf("%s", buff);

token = strtok(buff, ",");
while (token != NULL) 
{
	printf("%s\n", token);
	token = strtok(NULL, ",");
}
```

The code above will print:
```
Fred
James
Jane
Lynn
```

### strncpy
```c
char[] strncpy(char str1[], char str2[], int n);
```

This function copies the first `n` characters from `str2` to `str1`, overwriting anything that was already in `str1`. It returns the newly copied string (although `str1` also references the copied string).

### strncmp
```c
int strncmp(char str1[], char str2[], int n);
```

This function compares the first `n` characters in `str1` and `str2` to see which length-n prefix comes first alphabetically. It returns:
- A number less than 0, if the first `n` characters in `str1` come alphabetically before the first `n` characters in `str2`
- 0, if the first `n` characters in `str1` equal the first `n` characters in `str2`
- A number greater than 0, if the first `n` characters in `str1` come alphabetically after the first `n` characters in `str2`

### strrchr
```c
char[] strrchr(char str[], char c);
```

This function finds the LAST occurrence of `c` in `str`. It returns the suffix of `str` that begins with the last occurrence of `c`.

### strspn
```c
int strspn(char str1[], char str2[]);
```

This function returns the number of characters read in `str1` before reaching a character that is NOT in `str2`.

### strstr
```c
char[] strstr(char str1[], char str2[]);
```

This function determines whether `str2` is a substring of `str1`. If `str2` is not a substring of `str1`, it returns `NULL`. If `str2` is a substring of `str1`, it returns the suffix of `str1` beginning with the `str2` substring.

## Be Careful!
It's very easy to make a mistake when using strings. Strings are arrays, so you will get in trouble if you try to access memory beyond the end of the array. 

For example:

```c
char buff[5];
printf("Enter a word: ");
//Suppose you enter "Hello"
scanf("%s", buff);
```

`scanf` will copy the characters 'H', 'e', 'l', 'l', 'o' into the array. However, it will then try to add the end-of-string character, '\0', into the 6th spot in the array. This is past the end of the array, so your program will either crash with a segmentation fault, or you will overwrite the
value of some other variable. A lot of the string functions involve writing to strings, and none of them will handle an out-of-bounds error gracefully. 

When you use the following functions, **MAKE SURE you have enough memory allocated**:
- `scanf`
- `strcpy`
- `strcat`
- `strncpy`