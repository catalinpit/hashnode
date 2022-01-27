## Install a Specific Version of a Node.JS Package

Usually, you install the latest version of a package when you want to use it. But there are circumstances when you might need to install a specific package version. 

One example would be when the latest changes in a package are not compatible with your code.

This article shows you how to install a specific package version to avoid such situations. You will learn to do it using both `yarn` and `npm`.

## Using npm

With npm, you install a package as follows:

```
npm install package_name

// or

npm i package_name
```

**Note**: `npm i` is the shortcut for `npm install`.

The above commands install the latest version of the specified package. 

But what if you want to install a specific version? The syntax for installing a particular package version is as follows:

```
npm install package_name@version_number
```

When running the above command, npm installs the version specified after the "@" symbol.

### Package versions

If you want to see all the versions of a package, you can do it with the following command:

```
npm view package_name versions
```

That will list all the versions from the first to the last one.

## Using yarn

With yarn, you can accomplish the same thing as follows:

```
yarn add package_name@version
```

The idea is the same, but the syntax differs.