## Node.js + Express Tutorial for 2021 – Getting Started with the JavaScript Web Server Framework

> Article written for PullRequest and published originally on their blog - [Node.js + Express Tutorial 2021](https://www.pullrequest.com/blog/nodejs-express-tutorial-for-2021/)

Node.js with Express is a popular combo used by a lot of applications worldwide. This tutorial helps you get started with Node.js and Express by building a simple web server.

Your server will serve up an HTML page, which will be accessible by other people. By the end of the article, you will have basic knowledge about:
* Node.js
* Express
* npm
* creating Express routes
* serving HTML
* setting up static assets in Express

Pro tip: do not copy the code from the tutorial. Write the code yourself to learn better.
Without further ado, let's jump straight in!

---

# Create and initialise the project
The first step in the tutorial is to create an empty folder for the project. You can create one in the usual way, or you can do it from the terminal as follows:

```
mkdir express-server
cd express-server
```

Now that you have an empty project, it's time to initialise it by running the following command:

```
npm init -y
```

The above command creates the `package.json` file and initialises it with the default values. If you want to fill the fields manually, remove the `-y` flag and follow the instructions.

---

# Add Express
You have an initialised Node.js project, but there is no track of Express so far. Thus, that takes you to the next step - adding Express to the project. In Node.js, you install packages by running `npm install packageName`. 

Thus, to add the latest stable version of Express, run the following command:

```
npm install express
```

Now that Express is installed, your `package.json` file should look as follows:

```js
{
  "name": "express-server",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

You can see that Express was installed successfully because it's listed under the "dependencies". Now let's move onto the next step - creating the server.

---

# Create Express server
Before proceeding further, you need to create the JavaScript file for the web server. You can do so by running the following command in your terminal:

```
touch index.js
```

Open the file, and start by writing the following lines:

```js
const express = require('express');
const app = express();
```

What are these two lines doing?
1. With the first line, you import Express in your project so you can use it. Each time you add a package to your project, you need to import it where you want to use it.
2. In the second line, you call the `express` function, which creates a new application, and then assigns the result to the `app` constant.

#### Creating routes and listening on a specific port
In the simplest terms, a route represents an endpoint which people can access. A route is associated with an HTTP verb (e.g. GET, POST and so on), and it takes a URL path. It also takes a function which is called when the endpoint is accessed.

Write the following code in your file:

```js
app.get('/', (req, res) => {
    res.send({ message: 'Hello WWW!' });
});
```

Let's dissect the above code:
1. It's associated with an HTTP verb - in this case, it's the GET verb.
2. It takes a URL path - in this case, it's the homepage (`/`)
3. It takes a function which will be called when you access the endpoint

Therefore, when a person makes a `GET` request to your homepage - `localhost:3333`, the arrow function is called and will display "Hello WWW!".

The last step for the server to work is to set up a "listener". You need to set a specific port for the application. Write the following code at the end of your JavaScript file.

```js
app.listen(3333, () => {
    console.log('Application listening on port 3333!');
});
```

You need to call the method `listen` to be able to start the server. Also, you can replace the port number (3333) with whatever number you want!

#### Access the app in the browser
To start the application, run `node index.js` in the terminal. Mind you, `index.js` is the name I chose for this tutorial. However, you can name it `app.js` or whatever you want!

Now that the server is running, you can access it in your browser. Go to `http://localhost:3333/`, and you should see the following message:

> ![Screenshot 2021-01-27 at 14.11.25.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611749619127/RYtcqP8VW.png)

Well done for setting up a Node.js + Express web server! In the next section, you will set up the static assets such as JavaScript, CSS, HTML, images, etc.

# Static assets
The application does not like too nice at the moment. Would not be nicer with a bit of structure and styling? But where should you add them? 

In this section, you will see how to set up and serve static assets such as HTML, CSS, JavaScript and images.

#### Import the path module
The first step you have to make is to import the "path" module into your application. You do not have to install anything, because "path" comes by default with Node.

At the top of your file, write the following line:

```js
const path = require('path');
```

But why do you need this module? The "path" module allows us to generate absolute paths, which you need to serve static assets. Add the following line of code (before defining the routes) in your application:

```js
app.use(express.static(path.join(__dirname, 'public')))
```

`path.join` takes two arguments:
1. The current working directory (cwd)
2. The second directory, the one we want to join with the cwd.

As an exercise, try printing out to the console `path.join(__dirname, 'public')` to see what you get.

Your server should look like this so far:

```js
const path = require('path');
const express = require('express');
const app = express();

app.use(express.static(path.join(__dirname, 'public')))

app.get('/', (req, res) => {
    res.send({ message: 'Hello WWW!' });
});

app.listen(3333, () => {
    console.log('Application listening on port 3333!');
});
```


#### Create public and add assets
The next step is to create the "public" folder and add some assets. You can create an empty folder and change to it by running the following commands:

```
mkdir public
cd public
```

Now, let's create some empty files where you will add the HTML, CSS and JavaScript. Run the following lines in your terminal:

```
touch app.js
touch index.html
touch styles.css
```

We'll keep `app.js` super simple - only showing an alert to make sure it works. Thus, open `app.js` and add the following line:

```js
alert('it works');
```

Similarly, we'll keep `styles.css` simple as well. To make sure it works, let's set the background colour to blue. You can do that by adding the following code in `styles.css`:

```css
html {
    background-color: blue;
}
```

Lastly, you need to write the HTML so you can display it on your homepage. Open the file `index.html` and add the following HTML code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="/app.js"></script>
    <link rel="stylesheet" href="/styles.css">
    <title>My server</title>
</head>
<body>
    <h1>My server</h1>
    <p>Server built with Node.js and Express</p>
</body>
</html>
```

After writing the above code, there is one more step left! See the next section.

### Serve the HTML file
You are almost done. All that's left is to serve the HTML code. To do that, you have to go to your `index.js` file, which has your server code. Open the file and write the following code:

```js
app.get('/', (req, res) => {
    res.sendFile(`${__dirname}/public/index.html`);
});
```

If it's not your first time using Node.js and Express, you might ask what's up with the method `sendFile`, and why aren't you using the `render` method. Since you are not using any engine (e.g. Pug, EJS, and so on), you cannot use the `render` method. Thus, you send back an HTML file when people access your homepage. 

The final version of your server code should look as follows:

```js
const path = require('path');
const express = require('express');
const app = express();

app.use(express.static(path.join(__dirname, 'public')))

app.get('/', (req, res) => {
    res.sendFile(`${__dirname}/public/index.html`);
});

app.listen(3333, () => {
    console.log('Application listening on port 3333!');
});
```

Now, if you go to `http://localhost:3333`, you should see a webpage with a blue background. Of course, after you close the annoying pop-up.

> ![Screenshot 2021-02-01 at 17.57.22.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612195055791/CiCI_XpoF.png)

The above image shows what you should see on your screen!

---

# Conclusion
Congratulations on making it to the end of the article. By now, you should have a simple web application.

In this article, you learned:
* about Node.js
* about Express and how to use it to create a small web application
* how to create routes
* how to set up static assets in a Node.js + Express application
* how to serve a simple HTML file in Express

If you enjoyed the article, and if you want a part 2 where you add a database such as Mongo or Postgres, let me know in the comments!