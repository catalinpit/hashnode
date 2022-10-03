## A Beginner's Guide To The File System Module In Node.js

%[https://www.youtube.com/watch?v=QkwHP4d01xA]

The file system module, or simply `fs`, allows you to **access** and **interact** with the **file system on your machine**.

Using the `fs` module, you can perform actions such as:
* creating files and directories
* modifying files and directories
* deleting files and directories
* reading the content of files and directories

This article teaches you the most common and useful `fs` methods. So, without further ado, let's see what those methods are.

---

## How to use `fs`

The file system module is a core Node.js module. That means that you do not have to install it. The only thing you have to do is to import the `fs` module into your file. 
 
Thus, add the following line at the top of your file:

```js
const fs = require('fs');
```

Now you can call any method from the file system module by using the prefix `fs`. 

Alternatively, you can import only the methods you want from the `fs` API as follows:

```js
const { writeFile, readFile } = require('fs');
```

However, in this tutorial, you will see the first option used - importing the whole `fs` module.

### Caveat

For this tutorial, you also need to import the `path` module. It is another core Node.js module, and it allows you to work with file and directory paths.

Add the following line in your file, after the import of the `fs` module: 

```js
const path = require('path');
```

The `path` module is **not mandatory** to work with the file system module. However, it helps!

---

# Sync vs Async

It's important to note that by default, all the `fs` methods are asynchronous. However, you can use the synchronous version by adding `Sync` at the end of the method.

For instance, a method such as `writeFile` becomes `writeFileSync`. Synchronous methods complete the code synchronously, and thus they block the main thread. Blocking the main thread in Node.js is considered bad practice.

As a result, this tutorial uses the asynchronous methods from the file system module.

---

## Write to a file

The first thing you learn is how to write to a file. To write to a file from your Node.js application, you use the method `writeFile`.

The method `writeFile` takes the following arguments at a minimum:
* the name of the file
* the content
* a callback

If the specified file already exists, it replaces the old content with the content you provide as an argument. If the specified file does not exist, it creates a new file.

After importing the `fs` and `path` modules, write the following code in your application:

```js
fs.writeFile('content.txt', 'This is my first file!', (err) => {
    if (err) {
        throw err;
    };

    process.stdout.write('File created successfully!');
});
```

The above code creates a new file called `content.txt` and adds the text `This is my first file!` as the content. The callback function throws the error if there is any. Otherwise, it outputs to the console that the file creation succeeded.

Assuming you named your file `fsPractice.js`, go to the terminal and run the command `node fsPractice.js`. After you run the command, you should see the new file with the specified content.

There are other variants of "writeFile" such as:
* fs.writeFileSync - writes to the file synchronously
* fsPromises.writeFile - uses the promise based API to write to a file

> Check [this gist](https://gist.github.com/catalinpit/571ba06c06214b5c8744036c6500af92) to see how your application should look up to this point.

---

## Read from a file

Before you read from a file, you need to create and store the path to the file. Here is where the `path` module comes in handy.

With the `join` method from the `path` module, you can create the file path as follows:

```js
const filePath = path.join(process.cwd(), 'content.txt');
```

The first argument, `process.cwd()`, returns the current working directory. Now that you have the file path, you can read the content of the file.

Write the following code in your file:

```js
fs.readFile(filePath, (error, content) => {
  if (error) throw error;

  process.stdout.write(content);
});
```

The `readFile` method takes two arguments at the minimum:
* the path of the file
* a callback

If there is an error, it throws an error. Otherwise, it outputs the file content in the terminal.

If you go to the terminal and run the command `node fsPractice.js`, you should see the file content in your terminal.

There are other variants of "readFile" such as:
* fs.readFileSync - writes to the file synchronously
* fsPromises.readFile - uses the promise based API to write to a file

> Check [this gist](https://gist.github.com/catalinpit/badc2a539a44412892a0e05a9575d54d) to see how your application should look up to this point.

---

## Read a directory's content

Displaying the files inside a directory is quite similar to reading the content of a file. 
But, instead of passing the file path, you pass the current working directory *(you can pass any other directory)*.

After that, you pass a callback function to handle the response. Write the following code in your file:

```js
fs.readdir(process.cwd(), (error, files) => {
  if (error) throw error;

  console.log(files);
});
```

Up to this point, you only used `process.stdout.write` to output stuff to the terminal. However, you can simply use `console.log`, like in the above code snippet.

If you run the application, you should get an array with all the files in your directory.

> Check [this gist](https://gist.github.com/catalinpit/f82c4e6ae3acd5d97efdecb0bc67979e) to see how your application should look up to this point.

---

## Delete a file

The file system module has a method that allows you to delete files. However, it's important to note that it only works for files and not for directories.

When you call the `unlink` method with the file path as an argument, it deletes the file. Add the following code snippet to your file:

```js
fs.unlink(filePath, (error) => {
  if (error) throw error;

  console.log('File deleted!')
});
```

If you rerun the code, your file should be deleted!

> Check [this gist](https://gist.github.com/catalinpit/b1201434218c400f77e042109bfce99e) to see how your application should look up to this point.

---

## Create a directory

You can create a directory asynchronously by using the `mkdir` method. Write the following piece of code in your file:

```js
fs.mkdir(`${process.cwd()}/myFolder/secondFolder`, { recursive: true }, (err) => {
  if (err) throw err;

  console.log('Folder created successfully!');
});
```

Let's take it step by step. First, you want to create a new folder inside the current working directory. As mentioned previously, you can get the current working directory with the `cwd()` method from the `process` object.

After that, you pass the folder or folders you want to create. However, it does not mean you have to create the new folder/s in the current working directory. You can create them anywhere.

Now, the second parameter is the recursive option. If you do not set it to true you cannot create multiple folders. The above code would give an error if you set the `recursive` option to false. **Try out to see!**

However, if you want to create only one folder, you do not need to set the `recursive` option to true.

The following code would work just fine!

```
fs.mkdir(`${process.cwd()}/myFolder`, (err) => {
  if (err) throw err;

  console.log('Folder created successfully!');
});
```

Thus, I want to emphasize the use of `recursive`. When you want to create folders inside folders, you need to set it to true. It will create all the folders, even if they do not exist. 

On the other hand, if you want to create **only one** folder, you can leave it to false.

> Check [this gist](https://gist.github.com/catalinpit/09bad802541102c0cce2a2e4c3985066) to see how your application should look up to this point.

---

## Delete a directory

The logic to delete a directory is similar to creating one. If you look at the code you wrote to create a directory and the one below, you will see similarities.

Thus, write the following code in your file:

```js
fs.rmdir(`${process.cwd()}/myFolder/`, { recursive: true }, (err) => {
  if (err) throw err;

  console.log('Folder/s deleted successfully!');
});
```

You use the `rmdir` method from the file system module, and you pass the following arguments:
* the directory you want to delete
* the recursive property
* a callback

If you set the `recursive` property to true, it deletes the folder and its contents. It's important to note that **you need to set it to true** if the folder has content inside. Otherwise, you get an error.

The code snippet below only works if the folder is empty:

```js
fs.rmdir(`${process.cwd()}/myFolder/`, (err) => {
  if (err) throw err;

  console.log('Folder/s deleted successfully!');
});
```

If you have other files and/or folders inside `myFolder`, you get an error if you do not pass `{ recursive: true }`.

It's important to know when to use the `recursive` option and when not to avoid issues.

> Check [this gist](https://gist.github.com/catalinpit/a8cb6aca75cef8d6ac5043eae9ba22ce) to see how your application should look up to this point.

---

## Rename

Using the `fs` module, you can rename both directories and files. The code snippet below shows how you can do it with the `rename` method.

```js
// renaming a directory
fs.rename(`${process.cwd()}/myFolder/secondFolder`, `${process.cwd()}/myFolder/newFolder`, (err) => {
  if (err) throw err;

  console.log('Directory renamed!')
});

// renaming a file
fs.rename(`${process.cwd()}/content.txt`, `${process.cwd()}/newFile.txt`, (err) => {
  if (err) throw err;

  console.log('File renamed!')
});
```

You can see that the `rename` method takes three arguments:
1. the first argument is the existing folder/file
2. the second argument is the new name
3. a callback

Thus, to rename a file or directory, you need to pass the current file/directory's name and the new name. After you run the application, the name of the directory/file should be updated.

It's important **to note** that if the new path already exists *(e.g. the new name for the file/folder)*, it will be overwritten. Therefore, be sure you do not overwrite existing files/folders by mistake.

> Check [this gist](https://gist.github.com/catalinpit/5c3e7c6ae39d09996ff67175a719122e) to see how your application should look up to this point.

---

## Add content to file

With the file system module, you can also add new content to an existing file. The method `appendFile` allows you to do that.

If you compare the two methods `writeFile` and `appendFile`, you can see that they are similar. You pass the **file path**, the **content** and a **callback**.

```js
fs.appendFile(filePath, '\nNew data to be added!', (err) => {
  if (err) throw err;

  console.log('New content added!');
});
```

The code snippet above illustrates how you can add new content to an existing file. If you run the application and open your file, you should see the new content inside.

> Check [this gist](https://gist.github.com/catalinpit/7c8d40db53dea9e6831f9ee89d92475c) to see how your application should look up to this point.

---

## Conclusion

If you are reading this, it means that now you can:
* create files and directories
* modify files and directories
* delete files and directories
* read the content of files and directories

Well done! However, the file system module is more complex, and I encourage you to check the [official documentation](https://nodejs.org/docs/latest-v16.x/api/fs.html). In the official documentation, you can see all the methods.