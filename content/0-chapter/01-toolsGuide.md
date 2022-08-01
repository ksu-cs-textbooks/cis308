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

If you have no errors, it will generate an executable named either `a.exe` or `a.out`. Run your program as follows, depending on the name of your executable:

```text
./a.out
```

Or:

```text
./a.exe
```

You should now see "Hello, World!" in your terminal.

## Working with git in assignments

This class will use GitHub links to create initial repositories for both labs and programming projects, similarly to what you have done in CIS 300 and 301. 

1. When you get a new assignment, first click the assignment link -- this will create an initial GitHub repository. 

2. After opening your GitHub repository, click the green "Code" button and click the copy icon next to the URL name. This will copy the URL of your GitHub repository:

![Clone repo](/images/gitHubRepo.png)

3. Next, create a new, empty folder on your computer that you will use for your assignment. Open that folder in VS Code by either:

- Right-clicking on the folder name and selecting "Open with Code"
- Opening VS Code, and selecting "File->Open Folder" and selecting your new folder

4. Open the Terminal within VS Code by selecting "Terminal->New Terminal". This should open a terminal in your new folder, like this:

![Open terminal](/images/vsCodeTerminal.png)

5. Clone your GitHub repository by typing in the terminal:

```text
git clone {repository-url}
```

Where `{repository-url}` is the URL you copied from your GitHub repository (leave off the `{` and `}` when you insert your URL). For example, I might type:

![git clone](/images/gitClone.png)

6. Add any the necessary programming files to your project. You can add a file in VS Code by clicking your project name under "Explorer", and then clicking the icon labeled "New File". Type the name of your new file and hit Enter to save it:

![add file](/images/vsCodeAddFile.png)

7. Write the code for your project. As you go, save it and test it with the `gcc` compiler. If it builds, run the resulting executable (either `a.exe` or `a.out`). Here is an example of compiling and running a Hello, World! program:

![compile run](/images/compileRunHello.png)

Note that GitHub might have created an extra folder within your new folder, as it did here. You can test this by typing:

```text
ls
```

in the terminal, which will list the contents of the current directory (Windows users might need to use `dir` instead, depending on which terminal they are using). If you see an extra folder, type:

```text
cd {folder-name}
```

where `{folder-name}` is the name of the contained folder. If you type `ls` or `dir` again, you should see your code. Now, you can compile and run as usual.

8. Once you are ready to commit your changes, type the following in the integrated terminal:

```text
git add *
```

This will add all changes to the current commit. Then type:

```text
git commit -m "descriptive message"
```

to create a local commit, where "descriptive message" is replaced with a message describing your changes (you DO need to include the quotations). Finally, push your local commit to the current branch:

```text
git push
```

If you go to your GitHub repository URL, you should see the latest changes.