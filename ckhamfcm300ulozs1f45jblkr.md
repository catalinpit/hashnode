## How To Use Multiple Node Versions With NVM On MacOS

Different projects use different Node versions. That means you might have to switch your Node versions depending on the project. As you might image, installing and uninstalling Node version is time-consuming.

Thankfully, we have the Node Version Manager that allows us to switch between different Node versions easily. Thus, in this article, you will learn how to install it and use it on macOS.

The article illustrates you two ways of installing the Node Version Manager. With Homebrew and with the `cURL` command.

# Using the cURL command
One of the simplest ways to install NVM is to run the following cURL command in your terminal:

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.36.0/install.sh | bash
```

What does the command actually do?
1. It downloads the nvm script from GitHub and then it runs it.
2. After that, it also clones the nvm repository to `/Users/yourMacUsername/.nvm`.
3. Lastly, it adds a script to your profile file (~/.bash_profile, or ~/.zshrc, or ~/.profile, or ~/.bashrc) to enable you to use the nvm command in your terminal.

All you have to do now is to restart your terminal, and you can use the Node Version Manager. Alternatively, if you do not want to restart your terminal after running the `cURL` command, run `source ~/.nvm/nvm.sh` in your terminal. Afterwards, you can run the nvm commands straightaway.

# Using Homebrew
Another method is to install the Node Version Manager with Homebrew. Run the below command in your terminal:

```
brew install nvm
```

After the installation finishes, open your profile file (~/.bash_profile, or ~/.zshrc, or ~/.profile, or ~/.bashrc), and add the following lines to it at the end:

```
export NVM_DIR=~/.nvm
source $(brew --prefix nvm)/nvm.sh
```

By adding the above lines to your profile page, you can run the nvm command in your terminal. If you don't add the above lines, you will get an error when you run nvm commands in the terminal. Going further, you need to restart your terminal to use the nvm commands in the terminal.

# NVM commands
Now that you have NVM installed let's see some of the most useful commands. 

#### nvm ls-remote
First of all, we can run `nvm ls-remote` to find all the Node versions available for download. Caution: by running this command, you'll get a lot of versions. 

Thus, it might take a while until it finishes.

#### nvm install <node_version>
After running the command `nvm ls-remote`, we can install the version we want by running the following command:

```
nvm install <node_version>
```

For instance, if you want to install Node version 14, you need to run `nvm install 14`. It installs the latest Node 14 version. However, if you're going to install a particular version, you can specify it as follows - 13.10.1.

Tip: You can install the latest LTS version of Node by running `nvm install --lts`.

#### nvm ls
`nvm ls` lists all the Node versions installed on your machine. Don't confuse `nvm ls` with `nvm ls-remote`. The former one lists the ones installed on your machine, whereas the 'ls-remote' lists all the Node versions available for download.

#### nvm use
After installing the Node version you want, you can use it by running the following command:

```
nvm use <node_version>
```

By running this command, nvm switches the Node version to the one you specified.

Tip: To use the latest LTS version of Node by running `nvm use --lts`.

# Conclusion
The Node Version Manager is a handy tool to switch between Node versions. To recap, in this article, you learnt how to:
* install nvm using two different methods
* use nvm to install and use various Node versions

For more commands, information, troubleshooting, and anything else, check the [official nvm repository](https://github.com/nvm-sh/nvm) on GitHub.

<hr/>
_[daily.dev](https://api.daily.dev/get?r=catalins.tech) delivers the best programming news every new tab. We will rank hundreds of qualified sources for you so that you can hack the future._
[![Daily Poster](https://dev-to-uploads.s3.amazonaws.com/i/b996k4sm4efhietrzups.png)](https://api.daily.dev/get?r=devto)