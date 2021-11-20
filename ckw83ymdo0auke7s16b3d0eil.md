## How to Push Empty Git Commits

Git does not allow commits without messages. Also, to push a new commit to the remote repository, you need to make changes to your project.

The question is - how do you push a commit without making any changes? You can do it with the following command:

```javascript
git commit --allow-empty -m "Empty commit"
```

It's like pushing a normal commit, except that you add the `--allow-empty` flag.

### Why would you do it?

Sometimes, you might need to trigger a build without making changes to your project. On top of that, you might not have access to trigger the build manually.

Your only way to trigger the build is through Git. By pushing an empty commit, you can trigger your build without making any changes to the project.

### Git Aliases

You could shorten the command with [Git Aliases](https://catalins.tech/git-aliases-what-are-they-and-how-to-use-them), which allows you to create shortcuts for frequently used Git commands.

Instead of writing `git commit --allow-empty -m "Empty commit"` each time you want to push an empty commit, you could have a shortcut such as `git ec "Empty commit"`.

You can set a new Git alias by running the following command in your terminal:

```javascript
git config --global alias.ec 'commit --allow-empty -m'
```

For in-depth information about Git aliases, I recommend you to check my other article that talks about [what Git aliases are and how to use them](https://catalins.tech/git-aliases-what-are-they-and-how-to-use-them).