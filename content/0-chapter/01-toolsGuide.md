---
title: "Tools Guide"
pre: "0."
weight: 10
pre: "0.1. "
date: 2018-08-24T10:53:26-05:00
---

## GitHub account

First, you will need to create a GitHub account [here](https://github.com/). If you already have one, you can use your existing account.

Your GitHub account will need to be set up to use two-factor authentication (a new requirement). When logged into your GitHub account (link above), click your icon in the upper-left corner (it will say "Signed in as...(your account name)"). Select "Settings" and then "Account security". Scroll down until you find "Two-factor authentication". If it is disabled, then enable it. I use an SMS number, but you are welcome to use an authenticator app instead (I'm not familiar with that process, though).

## VS Code

In CIS 308, we will edit our C programs using VS Code with C/C++ extensions. You likely already have Visual Studio (2019 or 2022) installed on your computer from CIS 300 and/or 400 -- however, we will not be using Visual Studio in CIS 308. While it does have a C++ compiler, it behaves differently than more widely accepted C compilers (versions of gcc and clang). Finally, this class has a secondary goal of exposing students to a variety of Unix/Linux tools -- something that cannot be done as easily in Visual Studio.

You can download VS Code [here](https://code.visualstudio.com/download):

![VS Code download](/images/vsCodeDownload.png)

Install VS Code. When you see the prompt below, I recommend adding the "Open with code" action for both files and directories:

![Open with code](/images/addAction.png)

### C/C++ extensions

If you are prompted to install C/C++, do so. If you are not, launch VS Code and select "Extensions" from the left-hand toolbar. From there, you can find and install "C/C++" (this will add syntax highlighting to our C programs).

We ONLY need C/C++, not the whole extension pack.

### VS Code integrated terminal

We will be using the integrated terminal within VS Code, so that we can have the editor and the terminal (for compiling and running) within the same frame. If you do not see the Terminal at the bottom of VS code, select Terminal->New Terminal.

Windows users will want to select *powershell* as their terminal type, and Mac users will want to select the Mac terminal.

## Get the compiler

VS code does not contain a C compiler (even with the C/C++ extensions) -- we will need to install one.

### Windows Users

I recommend using either MSYS2 or WSL. (I prefer WSL, but on some systems it requires a BIOS edit before it will work.) You can download MSYS2 [here](https://www.msys2.org/). Follow the installation instructions. 

Then, launch an MSYS2 shell (click Start, type MSYS2, and run the app). In the resulting shell, type:

```text
pacman -S base-devel gcc
```

When prompted, say Y. You should now have both `gcc` and `make` installed.

In order to use these commands from the command prompt, you will need to add C:\msys64\mingw64\bin to your Path (click Start, type *Environment variables*, and select "Edit the system environment variables"). Click "Environment Variables..", then find Path under System variables and click "Edit...". Click "New", paste in *C:\msys64\mingw64\bin*, and click OK three times to dismiss each frame.

Open VS Code with an integrated terminal. Try typing:

```text
gcc
```

and then:

```text
make
```

You should see an error that no input files were provided (and not that the term is unrecognized).

### Mac users

After installing VS Code with C/C++, follow this [user guide](https://code.visualstudio.com/docs/cpp/config-clang-mac) to get gcc and make.

Open VS Code with an integrated terminal, and type:

```text
gcc --version
```

If you get an error that `gcc` is unrecognized, run the command:

```text
xcode-select --install
```

If you try `gcc --version` again, it should give you a version number.

## Hello, World in C

Create a new file in VS Code, and save it as *hello.c*. Type the following code:

```c
#include <stdio.h>

int main() {
    printf("Hello, world!\n");

    return 0;
}
```

Within the integrated terminal, type:

```text
gcc hello.c
```

If you have no errors, it will generate the executable `a.out`. Run your program as follows:

```text
./a.out
```

You should now see "Hello, World!" in your terminal.