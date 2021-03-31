## Getting Started With Open-Source: How To Contribute

<div class="no-border">[![cover (1).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1617198357271/uoNdlXnwM.png)](https://codelounge.dev)</div>

---

Video version

%[https://www.youtube.com/watch?v=8e1Mnkdgi4Y&list=PL4tJdkBbj_XXJgwJsoF9lIsbsZzP_qI9T&index=29]

---

Contributing to open-source projects is a great way to improve your programming skills and contribute to the community. Also, it's important to note that contributing to open-source projects is not all about coding. You can contribute in other ways. For example:
* organise code
* write or improve the documentation
* design stuff
* review code

Before going further, I advise you to read the code of conduct and the contribution guidelines. Please read them carefully before you start contributing because it explains what is expected from you. It also describes the workflow required to make contributions. The Open-Source guide has a great article on this subject - [Your Code of Conduct](https://opensource.guide/code-of-conduct/).

Are you ready to make your first contributions? Let's do it!

# 1. Find a project
Finding a project to contribute to is a difficult task. I advise you to start small and pick a small project at first. Why? Things move faster in a small project, and it's more likely to get your first contribution. But if you feel adventurous, you can start with a bigger project!

Moving further, there are a handful of useful websites which you can use to find projects and issues suited for beginners. Here is a non-exhaustive list:
* goodfirstissues.com - This website is great because it only contains issues that are suited for first time contributors; that is, for beginners. You can filter projects by programming language and repository.
* [goodfirstissue.dev](https://goodfirstissue.dev) - More or less, the same thing as the above website. Good First Issue curates easy pickings from popular open-source projects and helps you make your first contribution to open-source.
* up-for-grabs.net - This website is a list of projects which have curated tasks specifically for new contributors.
* github.com/explore - This is the explore page from Github itself. You can find lots of projects, but you have to search for issues suited for beginners manually.

These websites should be more than enough to find a project. If not, you pick a tool that you use daily and contribute to that if it's open-source.

# 2. Basic Git workflow
This article assumes basic knowledge of Git. The Git workflow you will be using is as follows:

1. Fork the repository to your GitHub account.
2. Clone the project on your machine.
3. Create a branch before making changes.
4. Make your changes.
5. Commit and push your changes.
6. Open a pull request.

The above workflow is the most basic one, and it's enough to contribute to open source projects. It's important to note that there are other variants, as well. However, you will use this one in the tutorial.

# 3. Fork the project
Let's assume you found the perfect project to contribute. I will use the [OSS-Contribution](https://github.com/catalinpit/OSS-Contribution) repository I created a while ago for this tutorial.

> ![Screenshot 2021-03-18 at 19.48.38.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1616089776958/Ex7jwqAVN.png)
Figure 1

Go to the repository page, and click on the `Fork` button, as shown in figure 1 above! 

**Why fork it first and not clone it directly?** When you fork a project, you make a copy of it in your account. As a result, you can work on it without affecting the original repository. Forking creates a separate copy, whereas cloning downloads the project on your machine. Also, you cannot make changes to the repository if you only clone it. Only authorised people can make changes. By forking the project, you can make changes and submit pull requests.

After the forking is complete, it will redirect you to your copy of the project. Now it's time to move onto the next step.

# 4. Clone the project
Now clone the project from your account. Go to the repository page to find the link.

> ![fs.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1616090573604/vGqYf2tA8.png)
Figure 2

To find the forked repository URL, click on the green button saying `Code` and copy the URL as shown in figure 2.

After copying the link, go to your terminal and run the following command *(replace the URL with yours)*:

```
git clone https://github.com/catalinstech/OSS-Contribution.git
```

Wait for the repository to download and then open it in your favourite code editor.

# 5. Create a branch
Before making any changes to the codebase, it's important to create a new branch. Branches allow people to work on the project without getting into conflict with each other. Also, each branch is independent of others, so your branch's changes are not visible in another branch (unless they are merged).

In the simplest words, your branch holds the changes you make to the project. Also, read the branch naming convention of each project. All projects specify how you should name your branches. Some examples are:
* `your_name/issue_fix` - E.g. catalinpit/add-name-768
* `issue_number-issue` - E.g. ET182-Fix-broken-navbar

Moving on, you can create a new branch and switch to it as follows:

```
git branch <your_branch_name>
git checkout <your_branch_name>
```

Alternatively, you can do the same thing in one command as follows:

```
git checkout -b <your_branch_name>
```

Now that you created a new branch, you are ready to make changes! Move onto the next section.

# 6. Make changes
> ![download.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1616133977788/IX_7lmFcR.png)
Figure 3

The next step is to make changes in the repository. I cannot advise you about making changes because it depends on each repository.

However, using my Github example repository, I added a new Twitter account in the `README` file. Now you need to commit and push your changes, which you will do in the next step.

# 7. Publish your changes
The first step is to add all your changes to the staging area. Basically, the `add` command includes your updates from a particular file in the next commit. It specifies what "to send to Github", in the simplest terms ever. 

Run either of the following commands:

```
git add . 

// or

git add README.md (your file name might differ)
```

`git add .` adds all your changes to the staging area. For instance, if you made changes in 10 files, it adds all those files. On the other hand, you can handpick changes by specifying the file name, as in the second version above. It only includes the files you specify.

#### Commit your changes
You included the updates in the staging area, but now you have to commit them as well. Committing files means saving your updates to the local repository. Think of it as saving a Word document after making changes.

```
git commit -m "Added my name to the README"
```

You can see the `git commit` command in action above. The `-m' flag stands for "message", and it allows you to summarise your changes. That means you should describe what you did in the project. Try to make the commit messages as concise and descriptive as possible. At the same time, it does not mean you should write a novel.

#### Push your changes
The last step is to "push" the changes to the remote repository. Until you "push" your changes, they are only available in your local repository. That is, nobody can see them except yourself.

To push your changes, run the following command:

```
git push -u origin <your-branch-name>
```

You are almost done now! The next and last step is to create a Pull Request, which you'll see in the next chapter.

# 8. Open a pull request
> ![download (1).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1616136305402/eYHDgIyNp.png)
Figure 4

Suppose you followed all the steps from the seventh step - `7. Publish your changes` - you should get a link in your terminal to open a pull request. Figure 4 (above) illustrates what you should see in your terminal. 

If you do not get the same output for some reason, you can go to the `repository URL > Pull requests tab > click on the Compare & pull request`. See figure 5 below.

> ![Screenshot 2021-03-19 at 09.15.12.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1616138181397/u8Xpx96Hx.png)
Figure 5

Whatever option you choose, a new window should open where you can create the pull request. Figure 6 illustrates that!

**Be careful, though!** Before submitting the pull request, make sure you read the contribution guidelines. At the minimum, add a descriptive title and description!

> ![Screenshot 2021-03-19 at 08.46.35.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1616136411248/6yLfMlEdB.png)
Figure 6

Click on the green button saying `Create pull request`, and you are done! All you have to do is to wait for PR comments. Well done!

#### Why do you need a PR?
By opening a pull request, other people can see the changes you've made to the codebase. Additionally, it allows other members to do a code review, which in turn might help you improve your skills and code. Thus, you can get valuable feedback!

Also, some changes might not be approved for various reasons, such as:
* poor code quality
* inefficient implementation
... and many others.

By creating pull requests, you protect the codebase from unwanted additions. Without pull requests, everyone can merge whatever they want to the `main` branch. Thus, the code quality will suffer.

In conclusion, pull requests helps and allows developers to:
* maintain a high-quality codebase
* avoid introducing *(too many)* bugs *(because it can happen with PRs as well)*
* get feedback on the code
* improve their skills and code

# Conclusion
Well done for learning the most basic Git workflow you can use to make OSS contributions. Also, well done for making your first open-source contribution if you followed the article!