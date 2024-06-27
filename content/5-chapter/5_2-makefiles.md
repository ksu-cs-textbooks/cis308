---
title: "Makefiles"
pre: "5.2. "
weight: 61
date: 2018-08-24T10:53:26-05:00
---

It now takes three lines to compile our program, which is a pain to
have to type every time we make a change. We can simplify
compilation by placing all of the compilation instructions in a
single file called a *Makefile* (with NO extension).

## Here is the format of a Makefile:

```text
compiler declaration
compiler flags declaration
executable name declaration
header list declaration

object list declaration

compiling/linking instruction
cleaning instruction (removing output files)
```

(There are many other options for creating Makefiles, but we will use the template above in this class.) Here is the Makefile for our [statistics program]({{% ref "5-chapter/5_1-headerFiles.md"  %}})

```text
//saved in a file name Makefile, with no extension
CC = gcc
CFLAGS = -g -Wall
EXE = nums
HEADERS = stats.h
CODE = stats.c prog.c

OBJECTS = $(CODE:.c=.o)

nums: $(OBJECTS) $(HEADERS)
    $(CC) $(CFLAGS) $(OBJECTS) –o $(EXE)

clean:
    rm -f *.o *.exe *.out
 ```

Now, let's go through the Makefile one line at a time:

```text
CC = gcc
```

This line declares the variable `CC`, and says that we're using the
gcc compiler. 

```text
CFLAGS = -g -Wall
```

This line declares the variable `CFLAGS` and states that we will use two compiler flags -- `-g` and `-Wall`. You don't have to include this line, but it can be useful. The `-g` option means that our executable is always built with debugging information, so that we can debug it in gdb. The `-Wall` option tells the compiler to display warnings. Often times these compiler warnings can give insight into why a program isn't working, as C will let you do many things that you probably don't intend to do (especially with pointers).

```text
EXE = nums
```

This line declares the variable `EXE` and states that we wish to name our executable "nums", instead of the default "a.out" or a.exe". We can replace "nums" with whatever we want to use as our executable name. Again, this line is optional.

```text
HEADERS = stats.h
```

This line declared the variable `HEADERS` and lists all the (user-created) header files used in the program.

```text
CODE = stats.c prog.c
```

This line declares the variable `CODE` and lists all the code files (.c files) used in the program.

```text
OBJECTS = $(CODE:.c=.o)
```

This declares the variable `OBJECTS` and instructions to create an object file (.o) for every .c file listed in the `CODE` variable. (An object file is a single file converted to machine code.) So, since we have the files `prog.c` and `stats.c`, will we get the object files `prog.o` and `stats.o`.

```text
nums: $(OBJECTS) $(HEADERS)
    $(CC) $(CFLAGS) $(OBJECTS) –o $(EXE)
```

This line describes how to compile our program. The`nums` at
the beginning is a name we're giving this compilation instruction –
we could have called it anything. When we put $(OBJECTS) on the top line (and similarly for other variables), this gets the value out of the `OBJECTS` variable. The top line, `$(OBJECTS) $(HEADERS)`, states that our program is dependent on all the header files and all the object files. This line says that to compile the program, all the object files must first be made. By listing the header files as a dependency as well, it ensures that if a change was made to a header file then the entire program will be rebuilt.

When we substitute the values of the variables, the second line
becomes:

```text
gcc -g -Wall prog.o stats.o –o nums
```

This line says to link together the two object files, and rename the
executable to `nums`. (That's the `–o nums` part). It also says to build the executable with debugging information (`g`) and to display compiler warnings (`-Wall`).

Next, we have:

```text
clean:
    rm -f *.o *.exe *.out
```
This line says that to clean our program, we want to delete the
object files (`*.o`), all executable files (`*.exe` and `*.out`). The `-f` option ensures that we will not see a warning if there are no files to remove that match one of the wildcards.

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
but now the executable is named `nums` instead of `a.exe`.

To remove all the output files, we type:

```text
make clean
```

This will remove all .o files and executable files.

## Makefile Rules
We could spend the rest of the semester talking about exactly how
Makefiles work and different intricacies and still not cover
everything. Makefiles are a very powerful tool – we've only
scratched the surface to be able to compile our program in a
specific way.

Here are some rules to follow as you write your own Makefiles:
- You should always define the variables `CC`, `HEADERS`, `CODE`, and
`OBJECTS`. The value of `HEADERS` should be a list of all .h files in your project, and the value of `CODE` should be a list of all .co files in your program. Your `OBJECTS` value should always be the same -- `$(CODE:.c=.o)` (create an object file for every .c file).
- The `CFLAGS` declaration is optional, but recommended
- The `EXE` declaration is optional -- if you leave it off (along with the `-o $EXE` in the compilation instruction), then your executable will be named `a.exe` (or `a.out`).
- There should be a tab character at the beginning of the
second line for the `nums: instruction` and the `clean:
instruction`. This MUST be a tab – spaces won't work.
- For the most part, your Makefiles will remain the same
from program to program. You'll just change the
`HEADERS` and `CODE` lists and change the name of the executable.

## Getting make

The `make` tool may have already be installed when you installed the `gcc` compiler. To test, open a terminal and type:

```text
make
```

If you see an error that says something about "No targets specified and no makefile found", then `make` is correctly installed. If you see an error that says something like: "The term make is not recognized...", then `make` is either not installed or the PATH variable does not include its location.

### Windows users

For Windows users who don't already have `make`, open an MSYS2 terminal and type:

```text
pacman -S make
```

Then, you will need to add the location of `make.exe` to your PATH environment variable. Look in both `C:\msys64\mingw64\bin` and `C:\msys64\usr\bin` -- copy the address of whichever location contains `make.exe`.

Click Start, type *Environment variables*, and select "Edit the system environment variables"). Click "Environment Variables..", then find Path under System variables and click "Edit...". Click "New", paste in the address you copied in the previous step, and click OK three times to dismiss each frame.

### Mac users

For Windows users who don't already have `make`, open the terminal and enter:

```text
xcode-select --install
```