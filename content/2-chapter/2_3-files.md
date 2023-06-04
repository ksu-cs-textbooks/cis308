---
title: "Files"
pre: "2.3. "
weight: 32
date: 2018-08-24T10:53:26-05:00
---

This section contains information on opening a file, reading from a file, and writing to a file. I only cover how to interact with text files – it is also possible to read from and write to binary files.

Whenever you are doing file I/O, you need to add:

```text
#include <stdio.h>
```

## Opening a File
Before we can interact with a file, we need to open it. The `fopen` function lets us open files for different kinds of input and output. Here's the prototype:

```c
FILE* fopen(char filename[], char mode[])
```

The `FILE*` return type means that the function is returning the address of a `FILE` object. We'll learn more about pointers in the next section. If the file could not be opened, fopen returns `NULL`.

Here, `filename` is a string representation of the filename, such as "data.txt". `fopen` searches the current directory for the file if no absolute path is given. The string `mode` specifies what type of operations you want to do on the file. 

Here are the different options for the mode:

| Mode | Description |
| -----|-------------|
| "r" | Open for reading (file must exist) |
| "w" | Open for writing (overwrites old data) |
| "a" | Open for appending (creates file if necessary) |
| "r+" | Open for reading and writing (file must exist) |
| "w+" | Open for reading and writing (overwrites old data) |
| "a+" | Open for reading and appending (opens at end of file) |

For example, we can open the file "data.txt" for reading, and print an error if we were unsuccessful:

```c
FILE *fp = fopen("data.txt", "r");
if (fp == NULL) {
  printf("Error opening file\n");
}
```

After we are done reading from a file or writing to a file, we must close the file with the `fclose` function. Here's the prototype:

```c
int fclose(FILE* fp)
```

To close data.txt, we'd do:

```c
fclose(fp);
```

## Reading from a File
There are two major functions for reading from a file – `fscanf` and `fgets`. `fgets` works exactly like we've seen before, except now we specify a `FILE*` instead of `stdin`. `fscanf` works exactly like `scanf`, except we first specify the `FILE*`. We'll start with `fscanf`:

```c
int fscanf(FILE *stream, char str[], variable addresses...)
```

`fscanf`, like `scanf`, returns the number of variables that were correctly read in. If it was unable to read any more input, the `EOF` constant is returned. Thus we can compare the return value of `fscanf` to `EOF` to see if we've reached the end of the file.

Suppose the file data.txt looks like this (a bunch of names and ages, each on separate lines):

```text
Bob 20
Jill 15
Tony 17
Lisa 22
```

We want to read this file, and print something like "Bob is 20 years old" to the console for each person in the file. Here's how:

```c
FILE *fp = fopen("data.txt", "r");
char name[20];
int age;
if (fp != NULL) {
  while (fscanf(fp, "%s %d", name, &age) != EOF) {
    printf("%s is %d years old\n", name, age);
  }
  fclose(fp);
}
```

Now, lets try to do the same thing with the `fgets` function. Here's the prototype:

```c
char[] fgets(char s[], int size, FILE *stream)
```

`fgets` reads a string from a specified file into the `s` array. The `size` parameter specifies the size of the string – it will not write past the end of the array. It returns a reference to the string that was read. If no string was read (specifying an error or the end of file), `NULL` is returned.
`fgets` will attempt to read `size-1` characters _unless it reaches a newline or the end of the file_.

Here's the same example repeated with `fgets`:

```c
FILE *fp = fopen("data.txt", "r");
char name[20];
char buf[30];
int age;
if (fp != NULL) {
  while (fgets(buf, 30, fp) != NULL) {
    //parse the current line
    char *token = strtok(buf, " ");
    strcpy(name, token);

    //get the age
    token = strtok(buf, " ");
    age = atoi(token);
    printf("%s is %d years old\n", name, age);
  }
  fclose(fp);
}
```

As we saw when using `fgets` to read from `stdin`, it WILL store the newline character at the end of each string when reading from a file (assuming there is still room in the array). You may want to use `strcspn` to overwrite the `\n` with a `\0`.

Reading files with `fscanf` is usually simpler (since it doesn't involve parsing lines), but it is more error-prone than `fgets`.

## Writing to a File
The primary function for writing to a file is `fprintf`. This function works exactly like `printf`, but the first argument is now a `FILE*`. Here's the prototype:

```c
int fprintf(FILE* fp, char str[], variables to print...)
```

Here is an example that will ask the user to input 10 numbers. Each number will be written on a separate line to the file out.txt:

```c
FILE *fp = fopen("out.txt", "w");
if (fp != NULL) {
  int num, i;
  for (i = 0; i < 10; i++) {
    printf("Type a number: ");
    scanf("%d", num);
    fprintf(fp, "%d\n", num);
  }
  fclose(fp);
}
```