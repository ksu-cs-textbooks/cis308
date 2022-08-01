---
title: "Compiling and Running"
pre: "0."
weight: 11
pre: "0.2. "
date: 2018-08-24T10:53:26-05:00
---

After you have installed VS Code along with `gcc`, you can write C programs in the VS Code editor and then use the integrated terminal to compile and run.

## Hello, World! in VS Code

Here is a Hello, World! program written in C using VS Code. It is saved to the file `hello.c` (note that `.c` is the extension for C programs):

![Hello C](/images/helloC.png)

## Find code in terminal

To compile and run a C program, make sure the integrated terminal appears below the code in VS Code (as shown above). If it doesn't, select "Terminal->New Terminal". This will open a new terminal in your current directory. 

### List directory contents

In the integrated terminal, type:

```text
ls
```

This should list the contents of the current directory, which hopefully includes your `hello.c` file. If you get an error that `ls` is unrecognized (which it might be, depending on what kind of terminal you are using), try:

```text
dir
```

instead.

### Change directory

If you do not see your code file displayed after typing `ls` or `dir`, then you are likely not in the folder that contains your code. If your code is contained within a subfolder of the current directory path displayed in the terminal, do:

```text
cd {dir-name}
```

where `dir-name` is the name of a subfolder within the terminal's current directory. (Make sure to leave off the `{` and `}` when substiting a directory name.) This will change the terminal's current directory to be: `dir-name`.

Alternatively, you may need to back out to the parent folder of the current directory. If you do:

```text
cd ..
```

Then the terminal's current directory will update to be its parent folder.

## Compile and run

Once you have found the directory with your code (which was most likely the original terminal directory without having to make any changes), you are ready to compile your code. To compile our `hello.c` program, we type:

```text
gcc hello.c
```

(replacing `hello.c` with the name of our C program file). If there were no errors, it will generate an executable file. If you type:

```text
ls
```

(or `dir`), you should see either `a.out` or `a.exe` -- this is the executable file for your program.

To run your executable, type either:

```text
./a.out
```

or:

```text
./a.exe
```

Depending on the name of your executable file. You should see your program running in the terminal.

Here is an example of compiling and running our Hello, World! program in the VS Code terminal:

![C compile run](/images/compileRunHello.png)
