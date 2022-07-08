## Git Aliases - What Are They And How To Use Them?

Being a developer, we work a lot with Git. We tend to write the same commands countless times in a day. Thus, repeating the same long Git commands over and over can become a tedious task.

As a result, in this article, you are going to see how to set up Git aliases for any Git command you want. The aliases are going to improve your experience significantly, and it is going to save you time as well. 

## What are Git Aliases
Git Aliases are shorter commands that map to longer commands. In simpler words, they act as a shortcut. For instance, instead of typing `git commit -m "message here"` every time you want to commit some changes, you can use an alias such as `git cm "message"`.  

At first glance, it might not seem like a significant improvement, but once you repeat the same command a dozen times, you can see the benefit. Also, it saves you a lot of time when you are pushing changes and use various commands.

Therefore, let us see how to set up the Git aliases. 

## How to setup aliases
To set up an alias for a command, you need to run a one-line configuration in the terminal. All the commands start with `git config --global alias.`, and you add the alias and Git command after the dot. For example, to create an alias for `git status`, we can run the following command in the terminal `git config --global alias.st status`.

The template for adding aliases is as follows `git config --global alias.[insertYourShortcut] [gitCommand]`. Below, you can see the Git aliases I am using for guidance: 

```
git config --global alias.c checkout
git config --global alias.st status
git config --global alias.cm 'checkout master'
git config --global alias.b branch
git config --global alias.c checkout
git config --global alias.cmm 'commit -m'
git config --global alias.p pull
git config --global alias.cb 'checkout -b'
git config --global alias.sc 'switch -c'
```

However, you can modify in any way you like it. Besides that, you can also add new, more complex commands.

## How to run the commands

You run the commands the way you run any other Git command. For instance, if you want to checkout master, you run `git cm` instead of `git checkout master`. 

I would suggest using descriptive aliases for your commands. Otherwise, you can get confused. For example, looking at `git.st` or `git.cm`, you can understand easier what their purpose is. On the other side, using something like `git cm` for `git rebase <base>`, it can confuse you.

## Caveat

To easily display your git aliases run the following command in your terminal `git config --global alias.alias "! git config --get-regexp ^alias\. | sed -e s/^alias\.// -e s/\ /\ =\ /"`.

Now you can use `git alias` to list all the aliases you have created.

## Conclusion
In conclusion, you will appreciate the aliases after using them. They help you to save time, to make fewer mistakes, and they speed up the development. 

If you have other aliases, you can reply in the comments. I am curious to see them!
