---
title: "Remote Access"
pre: "0."
weight: 15
pre: "0.6 "
date: 2018-08-24T10:53:26-05:00
---

In the case that you are unable (or uninterested) to install some of the C tools on your own machine (such as `gcc`, `gdb`, or `make`), you can install the *Remote - SSH extension* in VS Code. This will allow you to remotely connect to the CS Linux server, which already has all the C tools installed. You will be able to use VS Code to edit files that are stored on your CS department U: drive the same way that you would edit local files.

## Getting the Remote - SSH extension
In VS Code, find the *extensions* icon on the left hand side (it looks like four squares with one corner pulled away). Search for *remote* and find *Remote - SSH* (the current version is v0.90.1, but install the latest version if you see a newer version number). Click *Install*.

You should now see the *remote explorer* icon on the left bar in VS code, like this:

![remote explorer](/images/remoteExplorer.png)

## K-State VPN

If you are off-campus, you will need to connect to the VPN used by K-State (GlobalProtect) before you can make a remote connection. If you already have GlobalProtect installed, connect to it. If you don't, go [here](https://www.k-state.edu/it/cybersecurity/vpn/) for installation links.

If you are on-campus (and on a K-State network connection), you do not need to connect to a VPN.

## Connecting to CS Linux

To connect to CS Linux, click the remote explorer icon here:

![remote explorer](/images/remoteExplorer.png)

If this is your first time making a remote connection, you will see this page:

![ssh targets](/images/sshTargets.png)

When you hover over *SSH Targets*, you should see a plus (+) icon that says "Add New" (as shown above). Click it. You will see a prompt that says: *Enter SSH Connection Command". Type:

```text
ssh eID@cslinux.cs.ksu.edu
```

where `eID` is your eID. Press Enter to connect. 

It may ask you to set up an SSH client, if one isn't already installed. If so, go [here](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client) for SSH client installation information.

If an SSH client is already installed, it will ask you to select an SSh configuration file. Select one from the menu. At this point, you should see `cslinux.cs.ksu.edu` under *SSH Targets*. Hover over the `cslinux.cs.ksu.edu` name and select *Connect to Host in New Window*:

![ssh connect](/images/connect.png)

Select "Linux" as the platform:

![Linux](/images/linux.png)

Click *Continue* when prompted, and then enter your CS password (NOT your eID password) to login. You should see:

![logged in](/images/loggedin.png)

Click *Open Folder*, and navigate to a folder on your department U: drive. If you are prompted to log in again, do so. You should see the folder on the left side and a Linux terminal in the same directory on the bottom. You can also open files in that directory the same way you might with local files. For example, I might see:

![display](/images/displayLinux.png)

From there, you can use `gcc`, `gdb`, or `make` to compile, debug, or build your projects.

Once you are done with your connection, close the connection by going to *File->Close Remote Connection* (you might need to scroll down in the menu).

The next time you click *Remote Explorer" to connect to CS Linux, you should see `cslinux.cs.ksu.edu` already listed under `SSH targets`.