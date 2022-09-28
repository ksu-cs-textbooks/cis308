---
title: "Makefiles"
pre: "5.2. "
weight: 61
date: 2018-08-24T10:53:26-05:00
---

It now takes three lines to compile our program, which is a pain to
have to type every time we make a change. We can simplify
compilation by placing all of the compilation instructions in a
single file called a *Makefile*.

## Here is the format of a Makefile:

```text
compiler declaration
object list declaration
compiling/linking instruction
cleaning instruction (removing output files)
```

Here is the Makefile for our [statistics program]({{<ref "5-chapter/5_1-headerFiles.md" >}})

```text
//saved in a file name Makefile, with no extension
CC = gcc
OBJECTS = prog.o stats.o

nums: $(OBJECTS)
    $(CC) $(OBJECTS) –o nums

clean:
    rm *.o num
 ```

Now, let's go through the Makefile one line at a time:

```text
CC = gcc
```

This line declares the variable `CC`, and says that we're using the
gcc compiler. 

```text
OBJECTS = prog.o stats.o
```

This declares the variable `OBJECTS`, which contains a list of all
object files for the program. (An object file is a single file
converted to machine code.) We have a .o file for every .c file in
our program. So, since we have the files `prog.c` and `stats.c`,
will we get the object files `prog.o` and `stats.o`.

```text
nums: $(OBJECTS)
    $(CC) $(OBJECTS) –o nums
```

This line describes how to compile our program. The`nums` at
the beginning is a name we're giving this compilation instruction –
we could have called it anything. For our program to compile, all
the .o files must be generated. The `$(OBJECTS)` on the top line
gets the value out of the `OBJECTS` variable. This line says that to
compile the program, all the object files must be made.

When we substitute the values of the variables, the next line
becomes:

```text
gcc prog.o stats.o –o nums
```

This line says to link together the two object files, and rename the
executable to `nums`. (That's the `–o nums` part).

Next, we have:

```text
clean:
    rm *.o nums
```
This line says that to clean our program, we want to delete the
object files (*.o) and the executable (`nums`).

## Using a Makefile
Now that we have a Makefile, we want to use it to compile our
program. To compile a program with a Makefile, type:

```text
make
```

This will generate all the object files, link them together, and
create the executable called `nums`.

To run our program, we do:

```text
./nums
```

This is the same as what we've done before to run our program,
but now the executable is named `nums` instead of `a.out`.

To remove all the output files, we type:

```text
make clean
```

This will remove all the .o files and the executable `nums`.

## Makefile Rules
We could spend the rest of the semester talking about exactly how
Makefiles work and different intricacies and still not cover
everything. Makefiles are a very powerful tool – we've only
scratched the surface to be able to compile our program in a
specific way.

Here are some rules to follow as you write your own Makefiles:
- You should always define the variables `CC` and
`OBJECTS`. The value of `OBJECTS` should include a .o
file for every .c file in your program.
- You can rename your executable (`-o nums`) to be
whatever you want.
- There should be a tab character at the beginning of the
second line for the `nums: instruction` and the `clean:
instruction`. This MUST be a tab – spaces won't work.
- For the most part, your Makefiles will remain the same
from program to program. You'll just change the
`OBJECTS` list and change the name of the executable.