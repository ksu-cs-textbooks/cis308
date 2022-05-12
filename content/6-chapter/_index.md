+++
title = "Multiple Files"
date = 2018-08-24T10:53:05-05:00
weight = 7
chapter = true
pre = "<b>6. </b>"
+++

### Chapter 6

# Multiple Files

<div align="left">
Up to this point, all of our programs have been written within a
single file. There is nothing wrong with this – a C program is just
a bunch of functions, and it's fine to group those functions within a
single file. However, as your programs get bigger, it's nice to
physically separate functions into different files. This makes it
easier to find certain pieces of your program.
</div>
<div align="left">
Separating functions also promotes reuse. Right now, if we
wanted to reuse a function we’d written in another program, we would
have to copy it from our old program to our new one. With
multiple files, we can separate the functions we want reused and
just link to that file when we want to use them (this is like
separating the C library functions and including them when we
want to use them).
</div>
