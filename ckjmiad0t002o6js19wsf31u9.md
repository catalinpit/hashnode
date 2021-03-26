## How To Use TypeScript In A Node.js and Express Project

In this tutorial, you will learn how to use Typescript in a Node.js and Express project. The purpose of the tutorial is to show how to create a project with the mentioned technologies. Its purpose is not to debate whether you should add TypeScript or not.

Before going further, the prerequisites are:
* Basic knowledge in Typescript, Node.js and Express
* Having a Node version from v12 upwards, including Node 12.

# 1. Set up the project
The first step is to create a directory for the project and initialise it. Run the following commands to create an empty directory called `typescript-nodejs`, and change the current directory to it:

```
mkdir typescript-nodejs
cd typescript-nodejs
```

Now that you are in the `typescript-nodejs` directory, you have to initialise the Node project. To do so, run the following command:

```
npm init -y
```

Using the `-y` flag in the above command generates the `package.json` file with the default values. Instead of adding information like the name and description of the project ourselves, npm initialises the file with default values.

The project is initialised, and thus you can move to the next section - adding the project dependencies.

# 2. Add dependencies
The next step is to add the project dependencies. Those are the Express framework and Typescript. Add these dependencies by running the following commands:

```
npm install express
npm install typescript ts-node @types/node @types/express --save-dev
```

Why save everything Typescript-related as `devDependencies`? Even though you write the code using Typescript, the code gets compiled back to vanilla JavaScript. Typescript is not needed per se to run the application. Thus, since Typescript is used only by developers, it's saved as a dev dependency.

Moving forward, your `package.json` should look as follows after installing all the dependencies:

```js
{
  "name": "typescript-nodejs",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "@types/express": "^4.17.9",
    "@types/node": "^14.14.20",
    "ts-node": "^9.1.1",
    "typescript": "^4.1.3"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

# 3. Configure TypeScript
So far, you only installed Typescript, but you cannot use it yet. The reason is that you need to configure it. You need to create a file called `tsconfig.json`, which indicates that the directory is the root of a TypeScript or JavaScript project.

```
npx tsc --init
```

Running the above command creates the `tsconfig.json` file where we can customise the Typescript configuration. The newly created file contains lots of code, most of which is commented out. However, there are some settings you need to know about:

* **target** -> using this option, you can specify wich ECMAScript version to use in your project. For instance, if you set the `target` to ES5 and then you use arrow functions, the code is compiled to an equivalent ES5 function. The available versions are 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', or 'ESNEXT'.
* **module** -> with this option, you can specify which module manager to use in the generated JavaScript code. You can choose between the following values 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. The most common module manager and the default one is `commonjs`.
* **outDir** -> with this option, we can specify where to output the vanilla JavaScript code.
* **rootDir** -> the option specifies where are the TypeScript files located.
* **strict** -> the option is enabled by default, and it enabes strict type-checking options.
* **esModuleInterop** -> this option is true by default, and it enables interoperability between CommonJS and ES modules. How does it do it? It does it by creating namespace objects for all imports.

For in-depth information about all the options available, I recommend checking the [TypeScript TSConfig Reference](https://www.staging-typescript.org/tsconfig).

# 4. Create Express server
With TypeScript configured, it's time to create the Express web server. First of all, create the file `index.ts` (attention to the file extension) by running `touch index.ts`.

After creating the file, write the following code inside:

```
import express from 'express';

const app = express();

app.get('/', (req, res) => {
    res.send('Well done!');
})

app.listen(3000, () => {
    console.log('The application is listening on port 3000!');
})
```

Now you have a simple web server that shows "Well done!" when you access `localhost:3000`. The server is super simple, and without taking advantage of TypeScript. However, the purpose of this tutorial is to make the technologies work together and create a boilerplate. From here, you can build any application you want.

Whenever you make changes and want to run the application, you need to compile TypeScript to vanilla JavaScript. To do that, you need to run:

```
npx tsc --project ./
```

The command `tsc` compiles TypeScript to JavaScript. The flag `--project` specifies from where to pick the TS files. Lastly, `./` specifies the root of the project.

If you go into the `build` folder, you should see the compiled JavaScript code. That is, the code compiled from the TypeScript code you wrote.

However, we can simplify the process a little bit, and you will see how in the next section.

# 5. Create scripts
It can be tedious to write `npx tsc --project ./` each time you want to compile your code. As a result, we can add a script in `package.json` to make the process easier. 

Add the following line of code in `package.json` under `scripts`:

```
"build": "tsc --project ./"
```

Now you can run `npm run build` to compile your code. This way, it's simpler and quicker.

# Conclusion
In this tutorial, you learnt how to create a TypeScript + Node.js + Express boilerplate. This is just the tip of the iceberg, so you can build any application you want from here.
