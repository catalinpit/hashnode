## How To Delete All Local Git Branches In One Go

Sometimes, you might want to delete all your local branches from a project. Doing it one by one might be very tedious when you have lots of branches.

Thus, with the command below, you can delete all your local branches except `main`:

```
git branch | grep -v "main" | xargs git branch -D
```

Of course, you can replace the `main` branch with any other branch. 

---

Additionally, you might be interested in [Git Aliases](https://catalins.tech/git-aliases-what-are-they-and-how-to-use-them). The aliases will improve your experience significantly, and it is going to save you time as well.
