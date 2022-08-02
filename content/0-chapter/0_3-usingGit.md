---
title: "Using git"
pre: "0."
weight: 12
pre: "0.3 "
date: 2018-08-24T10:53:26-05:00
---

This class will use GitHub links to create initial repositories for both labs and programming projects, similarly to what you have done in CIS 300 and 301. 

## GitHub account

First, you will need to create a GitHub account [here](https://github.com/). If you already have one, you can use your existing account.

## Clone the repository
When you get a new assignment, first click the assignment link -- this will create an initial GitHub repository. 

After opening your GitHub repository, click the green "Code" button and click the copy icon next to the URL name. This will copy the URL of your GitHub repository:

![Clone repo](/images/gitHubRepo.png)

Next, create a new, empty folder on your computer that you will use for your assignment. Open that folder in VS Code by either:

- Right-clicking on the folder name and selecting "Open with Code"
- Opening VS Code, and selecting "File->Open Folder" and selecting your new folder

Open the Terminal within VS Code by selecting "Terminal->New Terminal". This should open a terminal in your new folder, like this:

![Open terminal](/images/vsCodeTerminal.png)

Clone your GitHub repository to your new, empty folder (which should be the current directory in VS Code) by typing in the terminal:

```text
git clone {repository-url} ./
```

Where `{repository-url}` is the URL you copied from your GitHub repository (leave off the `{` and `}` when you insert your URL). The `/.` tells git to clone the repository to the current directory.

## Add code and test

Add the necessary programming files to your project. You can add a file in VS Code by clicking your project name under "Explorer", and then clicking the icon labeled "New File". Type the name of your new file and hit Enter to save it:

![add file](/images/vsCodeAddFile.png)

Write the code for your project. As you go, save it and test it with the `gcc` compiler. If it builds, run the resulting executable (either `a.exe` or `a.out`). Here is an example of compiling and running a Hello, World! program:

![compile run](/images/compileRunHello.png)

## Commit and push

Once you are ready to commit your changes, type the following in the integrated terminal:

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