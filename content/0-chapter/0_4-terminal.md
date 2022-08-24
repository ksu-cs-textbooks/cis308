---
title: "Terminal commands"
pre: "0."
weight: 13
pre: "0.4 "
date: 2018-08-24T10:53:26-05:00
---

A side goal of this class is for students to become more comfortable with using the terminal. With practice, you will find that you are faster at navigating folders, creating files/folders, compiling/running programs, using tools stuch as git, etc. using the terminal than you are using a GUI. Familiarity with a terminal is especially useful in system administration and web development.

## Summary of common terminal commands

Here is a summary table of the most common terminal commands for this course:

| Command | Description |
| ----------- | ----------- |
| dir | Lists the current directory contents (only available in Windows) |
| ls | Lists the current directory contents (not available in Windows command prompt) |
| cd dirName | Changes the current directory in the terminal to be `dirName`. (Note: dirName must be a subfolder of the current directory.) |
| mkdir dirName | Makes a new, empty directory called `dirName` |
| ni fileName | Creates a new, empty file called `fileName`. We can do `ni prog.c` to create a new C program called `prog.c` (only available in Windows) |
| touch fileName | Creates a new, empty file called fileName. We can do `touch prog.c` to create a new C program called `prog.c` (only available in Mac/Linux/Unix) |
| cd .. | Updates the current directory in the terminal to be its parent directory. For example, if the current directory is `C:\Users\Julie`, then `cd ..` makes the current directory be `C:\Users` |
| del fileName | Deletes the file called `fileName`, which must be in the current directory (only available in Windows) |
| rm fileName | Deletes the file called `fileName`, which must be in the current directory (only available in Mac/Linux/Unix) |

## Other terminal tips

When you are typing a directory name or file name in the terminal, you can type a few letters and hit *Tab* -- the terminal will attempt to autocomplete the rest of the name.

To recall a command you recently typed in the terminal, you can use the up or down arrows. This saves you from typing the same commands over and over.