## How To Use TailwindCSS With Node.js, Express And Pug

In this article, you will learn how to use TailwindCSS with Node.js, Express and Pug. The purpose of this tutorial is to teach you how to create a Node.js application with TailwindCSS, Express and Pug.

Pre-requisites:
* Basic terminal knowledge.
* Knowing how to use a code editor.
* Basic npm/npx/yarn knowledge.
* Pug and Express.js knowledge.

# Project configuration
The first step is to create and configure our application. Run the following commands to create an empty directory `nodejs-tailwind`, and change the current directory to it:

```
mkdir nodejs-tailwind
cd nodejs-tailwind
```

Now that we are in the `nodejs-tailwind` directory, we have to initialize our Node project. To do so, we need to run the following command:

```
npm init
```

For each Node.js project, we need a file called `package.json`. Its purpose is to store metadata about the project (e.g. name, description, version, author, etc.), and to manage the project dependencies and scripts. We could create the file manually, but that would be tedious. 

Thus, the purpose of `npm init` is to create the `package.json` file. Once you run the command, you get an interactive prompt where you can add information about your project. Or, if you are happy with the suggested information, you can press enter until the end. If you do not add any information, your file should look like this:

```
{
  "name": "nodejs-tailwind",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

Now we need to create the `index.js`, which stores our basic server. You can create the file by running:

```
touch index.js
```

#### Create basic server
There are various Node.js frameworks to create a server. However, for this tutorial, we use Express because it is a mature, well-known web framework. We install Express in your project as follows:

```
npm install express
```

If you go to `package.json`, you can see "express" listed under dependencies. That means we are ready to build the server and test it in the browser. 


```
const express = require('express');

const app = express();

app.get('/', (req, res) => {
    res.send('It works');
})

const server = app.listen(3000, () => {
    console.log(`The application started on port ${server.address().port}`);
});
```

Now make sure the server works. You can check it by running `node index.js` in your terminal, and then visiting `localhost:3000`. If you did everything correctly, you should see a page that says "It works".

# Add Pug
Before adding TailwindCSS to our project, we should install Pug. Pug is a template engine for Node, which has a simplified syntax and it compiles to HTML. It makes it easier to write HTML code, and cleaner too.

The first step is to install Pug in our project. We can install it by running the command below:

```
npm install pug
```

Once Pug is installed, we need to create a new directory to store the pug files. You can create a new directory, and a pug file, as follows:

```
mkdir views

touch views/index.pug
```

After creating the `index.pug` file, add the following content to your file:

```
doctype html
html(lang="en")
  head
    meta(charset="utf-8")
    meta(http-equiv="X-UA-Compatible", content="IE=edge")
    meta(name="viewport", content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0")
    title Node.js with TailwindCSS, Express and Pug
    link(href="./styles/style.css", rel="stylesheet")
  body
    h1 Hello world!
    p My starter template
```

The tutorial assumes Pug knowledge. However, if you wish to see the same code in HTML format, you can use the [Pug to HTML converter](https://pughtml.com/). It's a useful tool if you want to convert your code between Pug and HTML, or vice versa.


#### Configure views and static files
Before we can start coding, we have to set up views and static files. The first step is to import the `path` module, which comes with Node.js by default. The `path` module allows us to work with directories and file paths, which we need when we serve static assets such as images, for instance.

```
const path = require('path');
```

Thus, import the path module, as in the line above. Now, let's see what the code below does.

```
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'pug');
app.use(express.static(path.join(__dirname, 'public')))
```

With the first line, `app.set('views', path.join(__dirname, 'views'));`, we tell Node.js what the source of our templates is. Now, Node.js knows where to look for our pug templates. 

Going further, the second line - `app.set('view engine', 'pug');` - tells Node.js what engine to use. In our case, it is Pug. 

The last step is to specify the directory from where to serve static assets such as JavaScript, CSS, images, and so on. The last line, `app.use(express.static(path.join(__dirname, 'public')))`, tells Node.js that we store the static assets in a directory named `public`.

#### Update index.js
We need to update our server to serve the pug file we created previously. To do that, change `res.send('It works');` to `res.render('index');` in the app.get function. Your "get" route should look like the one below: 

```
app.get('/', (req, res) => {
    res.render('index');
});
```

Run the server to make sure the changes did not break our application. Going to localhost:3000, you should see:

> Hello world!

> My starter template

# Add TailwindCSS
The step of the tutorial is to add Tailwind to our project and configure it. Let's start by adding TailwindCSS and PostCSS to our project:

```
npm install tailwindcss postcss autoprefixer postcss-cli
```

Why do we need to add PostCSS and Autoprefixer as well? First of all, PostCSS allows us to "convert modern CSS into something most browsers can understand, determining the polyfills you need based on your targeted browsers or runtime environments". But why do we need it for Tailwind? The reason is that TailwindCSS is a PostCSS plugin. As a result, we need a tool to translate the modern CSS into something the browsers can understand.

Secondly, autoprefixer is a PostCSS plugin as well. Autoprefixer adds vendor prefixes to CSS rules using the values from [Can I Use](https://caniuse.com/). In other words, it makes sure the application looks the same in all browser. 

Let's move further, and generate the tailwind.config.js file. The purpose of this file is to allow you to customize your TailwindCSS installation. It is a configuration file where you can add additional information such as plugins, themes, margins, paddings and everything you require and Tailwind does not have. 

```
npx tailwindcss init
```

By running the above command, it automatically creates the tailwind.config.js file. If you want to add customizations, I recommend checking the [TailwindCSS Configuration page](https://tailwindcss.com/docs/configuration).

That is all it takes to add TailwindCSS to your Node.js project!

#### PostCSS
What is left, is to set up the `postcss.config.js` file, which stores the configuration for PostCSS. First of all, we have to create the file, which we can do as follows:

```
touch postcss.config.js
```

Once the file is created, add the following configuration to it: 

```
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer'),
  ]
}
```

The `postcss.config.js` file specifies what PostCSS plugin our project uses. In our case, it is TailwindCSS and Autoprefixer.

#### Create the necessary files
After adding and configuring all the packages, we need to create the files for our CSS. For this tutorial, I chose to create the folder `styles` inside the "public" folder. Lastly, the `tailwind.css` file holds the Tailwind CSS, whereas the `style.css` file contains the final CSS that is used by our application.

```
mkdir public
mkdir public/styles
touch public/styles/tailwind.css
touch public/styles/style.css
```

You can create the directory and the two files, by running the above commands. `mkdir` creates a new directory, whereas `touch` creates an empty file. Also, add the following code in `tailwind.css`:

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

The above code injects base, components, and utilities styles from TailwindCSS into our CSS. These directives become actual CSS at run time. After you run the command from the next section - `" tailwind:css"` - check the file `style.css` to see the generated code.

#### Package.json 
The last thing we have to do is to add the following line in our project's `package.json`:

```
"tailwind:css": "postcss public/styles/tailwind.css -o public/styles/style.css"
```

With the above command, we build the CSS and add it to the `styles.css` file, which is used by our application. If you add CSS to your application, make sure to run `npm run tailwind:css` each time, so the changes apply. After doing so, start your application, and you should see the changes.

# Conclusion
At this point, you should have a complete Node.js application with Express, Pug and TailwindCSS. If you want to check the project, here is the [GitHub link to the project](). Feel free to use it as a starter for your project.

To recap, we learnt how to:
* add Express, Pug and TailwindCSS to a Node.js project.
* set up Pug as the view engine in the application.
* set up the folder for our assets.
* create a basic Node server.

<hr />

> Originally published on [daily.dev](https://daily.dev/posts/how-to-use-tailwindcss-with-node-js-express-and-pug)