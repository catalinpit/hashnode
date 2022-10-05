## Create Custom API Endpoints in Nuxt

Did you know you can create custom API endpoints in Nuxt.js? That means you do not have to spin a standalone server. Instead, you can do it straight in your Nuxt application!

In this article, you will see how to do it. You will create a simple Express server with an endpoint that allows you to get data from the database.

Therefore, let's see how to set up a custom API server!

---

## `serverMiddleware` Property

Nuxt.js has a property called `serverMiddleware` that allows you to create additional API routes inside your application.

How does it work? Nuxt.js creates an instance of `connect`, which is a middleware layer for Node.js. Thanks to the `connect` instance, you can create a custom API with different endpoints.

The `serverMiddleware` property is handy when you want to have the API in the same place as your Nuxt application. It is also a helpful feature when you want to build a proof of concept or when you have a small API.

---

## How to create the API

The first step is to create a new folder inside the root directory of the project. Create the new folder as follows:

```
mkdir api
```

Inside the folder, create a new file `courseAPI.js`. The `courseAPI.js` file is where you will build the Express server.

**Scenario** - For this example, let's pretend you have a database storing web development courses. Thus, you will build an endpoint that allows you to retrieve all the courses from the database.

Open the file `courseAPI.js` and write the following code:

```js
const express = require('express');
const { GraphQLClient } = require('graphql-request');

const app = express();
app.use(express.json());

const client = new GraphQLClient(
    process.env.ENDPOINT
);

app.get('/getCourses', async (req, res) => {
    const allCourses = `
    {
        courses {
          id
          name
          description
          url
          vote
          authors {
            name
          }
        }
    }
  `;

  const { courses } = await client.request(allCourses);

  res.json({ courses })
});

module.exports = app
```

There are multiple things happening in the above code. You:
* import the packages needed to build the API server - `Express` and `graphql-request`
* create a new Express instance and use the `express.json()` middleware
* create a new GraphQLClient instance passing a fictive endpoint
* build the `/getCourses` endpoint
* make a request using the newly-created GraphQLClient while passing the `allCourses` query
* return the courses from the database
* export the app

Now you have a simple Express server inside Nuxt. The next step is to register the `serverMiddleware`. Go to the `nuxt.config.js` file and add the following property:

```js
export default {
  serverMiddleware: ['~/server-middleware/courseAPI.js']
}
```

Now, if you start the application and go to the `/getCourses` route, you should see all the courses from the database.

**Note**: If you want to add a specific path or a prefix such as `/api`, you need to use the Object form and specify the path. The code snippet below illustrates the Object form with a specific path.

```js
export default {
  serverMiddleware: [
    { path: '/api', handler: '~/server-middleware/courseAPI.js' }
  ]
}
```

In this tutorial, you will see the first option, without the Object form. However, feel free to use the option that suits your needs. 

---

## How to use the API endpoint

Now that you have the custom API endpoint, you can start using it. The code below illustrates one way of fetching the data.

The component below fetches the courses from the database and renders them on the page. It is very basic, and its purpose is to simply illustrate how to use the custom endpoint. In real life, you would present the data in a better way.

```js
<template>
    <div>
        {{ courses }}
    </div>
</template>

<script>
export default {
    data() {
        return {
            courses: []
        }
    },
    async fetch() {
        this.courses = await fetch('http://localhost:65064/getCourses').then(res => res.json());
    }
}
</script>
```

It's important to note that you would not hardcode the URL in a real-world application. Also, when you use the `fetch` hook, you need to pass the absolute URL. So doing something such as `fetch('/getCourses')` would give you an error.

---

## Conclusion

In this article, you built a simple Express server inside Nuxt. However, you can build upon it and create a more complex API.

But the question would be - is this the right approach? Do you want to have the API inside Nuxt? Especially if it is a complex API.

There are some points to think about, such as:
* scaling the API
* having a single point of failure