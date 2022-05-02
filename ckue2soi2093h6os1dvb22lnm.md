## Mac Terminal Commands I Use Everyday

The Mac terminal is a command-line interface (CLI) that allows users to interact with the operating system through text commands.

Using the terminal, users can accomplish the same tasks as when they use the standard graphical user interface (GUI) and even more. One example would be creating a directory from the terminal with one command.

![MacOS Terminal Example](https://cdn.hashnode.com/res/hashnode/image/upload/v1633436252555/A-huLOyD7.png)

When it comes to developers, the terminal it's even more important because they spend a good chunk of time each day using it. Developers use the terminal for tasks such as:
* creating new projects
* running and testing the applications
* inspecting files

**Thus, the terminal is an essential tool in any developer's toolbelt, and knowing how to use it is very beneficial.** In this article, you will see the main terminal commands you will most likely use daily as a developer.

---

## List the contents - ls

One of the most common and important commands is the `list` command or `ls` in short. The `ls` command allows you to view the content of a directory.

When you run the `ls` command, it shows you all the files and directories in the current directory. For instance, if you are in the *Downloads* directory, it shows you all the files and directories inside it.

Figure 1 shows an example of running the `list` command in the terminal.

![Screenshot of ls command on Mac](https://cdn.hashnode.com/res/hashnode/image/upload/v1633368983715/KnBw4FNq6.png)*Figure 1*

The `ls` command is the terminal alternative for opening the "Finder" on your machine and browsing the content of a specific folder.

## Change directories - cd

Another terminal command developers use a lot is the `cd` command, which is the shorthand for "**change directory**". 

The `cd` command allows you to navigate between directories on your machine. For instance, if you are in the *Desktop* folder and want to go to the *Work* folder, you can run the following command:

```
cd Work
```

The above command takes you from one folder (*Desktop*) to another one (*Work*). 

> Note: It only works if the *Work* folder is inside *Desktop*. Otherwise, you need to provide the full path. 

But, you can do more stuff using the `cd` command. Here are the things you can do:
* `cd ..` - With this command, you can go back one folder. For instance, if you are in the *Desktop/Work* folder, running `cd ..` will take you to the *Desktop* folder. In other words, it takes you one level above the current working directory.
* `cd -` - It takes you to the directory you've been browsing before using the `cd` command.
* `cd` - Using this command, without specifying any folder, takes you to the Home folder.

![Screenshot illustrating the use of cd command in the macOS terminal](https://cdn.hashnode.com/res/hashnode/image/upload/v1633369048773/_2yI_iBJj.png)*Figure 2*

Figure 2 illustrates how the command can be used to change directories from the terminal. The `cd` command is the terminal alternative for clicking on a folder to open it.

## Create a file - touch

At this point, you know how to list the content of directories and how to change directories. But how do you create new files inside those directories?

The `touch` command allows you to create new files from the terminal on Mac! When you use the command, you need to specify the name of the file and press enter. After that, it creates a new file in the current working directory with the name you specified.

Let's say you are in the *Desktop* folder. If you run the command `touch taxes.txt`, it creates a new, empty file in the *Desktop* folder with the name *taxes.txt*.

![Screenshot illustrating the touch command on macOS terminal](https://cdn.hashnode.com/res/hashnode/image/upload/v1633369100980/F4AHncmRj.png)*Figure 3*

Figure 3, above, shows the newly created file. 

## Create a directory - mkdir

Besides creating new files, you also need to create new folders from time to time. The terminal enables you to do that as well!

The command `mkdir` is the shorthand for **make directory**, and it allows you to create new, empty directories. Similar to the `touch` command, you need to provide the folder's name as an argument.

```
mkdir Projects
```

The above command creates a new directory with the name "Projects". The `mkdir` command creates the new folder in the current working directory. For instance, if you are in the *Desktop* directory, that's where it makes the *Projects* directory.

![Screenshot illustrating how to create a directory in the terminal on macOS](https://cdn.hashnode.com/res/hashnode/image/upload/v1633410669537/3lmwuLr_F.png)*Figure 4*

The `mkdir` command is the terminal alternative of right-clicking and choosing "New Folder" using the mouse.

## Remove a file - rm

You can also remove files from the terminal using the `rm` command, which is the short form for **remove**.

Running the following command removes a file from your machine:

```
rm myFile.txt
```

Thus, you can quickly delete files from your machine using the terminal.

![Screenshot illustrating the rm command on macOS terminal](https://cdn.hashnode.com/res/hashnode/image/upload/v1633410785982/l7chRy3RU.png)*Figure 5*

Figure 5 shows the `rm` command in action. After deleting the file, I ran the `ls` command to show you that the file was removed.

## Remove a directory - rm -r

Removing a directory is similar to removing a single file. You can remove a directory and its content with the `rm -r` command.

The `-r` stands for recursively, and it tells the system to remove the files and other sub-directories inside the specified directory. If you have a folder *School Work* with other files/directories inside it and run `rm School Work`, you get an error saying that the directory is not empty.

To remove the *School Work* directory and all of its content, you need to run the following command:

```
rm -r School Work
```

Figure 6 shows the command `rm -r` in action, and you can see that I ran it twice. Once before deleting the directory to show that it exists and after deleting it to show that the command worked.

![Screenshot illustrating the rm -r command on macOS terminal](https://cdn.hashnode.com/res/hashnode/image/upload/v1633413155230/XpUahKtrn.png)*Figure 6*

## Get the current directory - pwd

`pwd` stands for "**Print Working Directory**" and prints the full path to the current working directory.

![Screenshot illustrating the pwd command on macOS terminal](https://cdn.hashnode.com/res/hashnode/image/upload/v1633410923914/dRcSPsfVB6.png)*Figure 7*

In figure 7, you can see that I ran the command in the "Desktop" directory. The command returned the full path to the "Desktop" directory.

## Display the content of a file - cat

The `cat` command is a complex and powerful command, which allows you to:
* display the content of a file
* create a new file with content inside
* concatenate multiple files and display their content

When you run the command `cat fileName`, it outputs the content of that file to the terminal. Figure 8 illustrates an example of running the `cat` command.

![Screenshot illustrating the cat command on macOS terminal](https://cdn.hashnode.com/res/hashnode/image/upload/v1633412215222/YYSJ111ux.png)*Figure 8*

Alternatively, you can display the content of multiple files by specifying all the files whose content you want to see. See the example below:

```
cat file1 file2 file3
```

The above command concatenates "file1", "file2", "file3" and prints their content to the terminal.

Thus, the `cat` command is helpful when you want to display the content of a file in the terminal rather than opening it in a text editor.

---

## Conclusion

As you can see, the terminal is extremely powerful. Using the terminal, you can do everything you can do with the GUI and more!

Also, it's important to note that it will take a while until you get familiar with the commands. The more you use them, the more familiar you become with them. Take your time and practice.

Lastly, after becoming familiar with these basic commands, challenge yourself and deep dive into more complex commands.

---

## Frequently Asked Questions (FAQ)

Let's answer some common questions you might have. If you have additional questions, leave them in the reply, and I will add them here.

### What is the current working directory?

In this article, you saw the term "*current working directory*" quite a few times. The "*current working directory*" refers to the directory you are executing commands from.

For instance, if you are in the "Desktop" directory, that's your "*current working directory*".

### Do I need to install the terminal myself?

No, you do not need to install the terminal yourself. The terminal comes pre-installed on macOS.

### How do I open the terminal on my Mac?

There are two ways to open the terminal. 

The first way of opening the terminal is to go to the **Launchpad** and then search for the **Terminal**.

The second way is to open the **Finder**, go to **Utilities**, and click on the **Terminal**.

### Do I need to know how to use the terminal?

Whether you are programming as a hobby or working as a software developer, you will have to use the terminal sooner or later.

So, we can say that you need to know how to use the terminal. You should learn the basics, at least.

### Do Mac terminal commands work on Linux?

The terminal commands on MacOS work on Linux as well because they are both UNIX-based. Thus, learning how to use the terminal on Mac means you can also use the terminal on Linux.

### Do Mac terminal commands work on Windows?

Some commands work on both systems, but not all of them. The commands that work on both systems are limited.

If you want to see the MacOS terminal commands and their Windows alternatives, check [this resource](https://enexdi.sciencesconf.org/data/pages/windows_vs_mac_commands_1.pdf).

By the way, check this article to learn how to [supercharge your Mac terminal with oh-my-zsh and iTerm2](https://catalins.tech/improve-mac-terminal).
