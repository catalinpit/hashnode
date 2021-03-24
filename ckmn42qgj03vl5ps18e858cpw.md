## KeystoneJS & GraphQL API Crash Course

> Article written for PullRequest and published on [their blog originally](https://www.pullrequest.com/blog/keystonejs-and-graphql-crash-course-book-headless-cms/).

# Video version
%[https://www.youtube.com/watch?v=SfYNg6vQH4I&list=PL4tJdkBbj_XXJgwJsoF9lIsbsZzP_qI9T&index=29]

KeystoneJS is a headless content management system (CMS) and a GraphQL API for NodeJS. A CMS like KeystoneJS allows us to create and store content. Then, it provides access to the content through an API.

In this tutorial, you'll build a simple book inventory to store the books you are reading!

# 1. Install Keystone
The [documentation](https://www.keystonejs.com/quick-start/) does a great job explaining how to get started with KeystoneJS. Therefore, I am not going to reinvent the wheel.

You can initialize a Keystone application using either `npm` or `yarn`.  Choose whatever suits you from the two:

```
npm init keystone-app my-app

yarn create keystone-app my-app
```

After running the commands, you will be prompted to answer five questions. The purpose of those questions is to configure a default project for you. They are as follows:

1. **What is your project name?** - Choose whatever name you want for your project.
2. **Select a database type** - Here, you can choose between 3 options:
    * MongoDB (we will use Mongo for this tutorial)
    * PostgreSQL
    * Prisma
3. **Where is your database located?** - We will use the local MongoDB from our machine. Thus, the URL is `mongodb://localhost/db_name`. (Replace `db_name` with whatever name you want for your database)
4. **Test database connection?** - You can choose between `Yes/No`. I always choose `Yes` because I want to test the DB connection before proceeding further.
5. **Select a starter project** - Here, you can select pre-configured projects. You can choose between 4 options:
    * Starter (Users + Authentication) - *Simple starting point with users and basic authentication*
    * Blank - *A completely blank project. Provides an AdminUI and GraphQL App ready for to you configure*
    * Todo - *A very simple Todo app with a static front-end written in good old HTML,
   CSS and JavaScript*
    * Nuxt - *A simple app using the NuxtJS front-end framework*

We will choose the `blank` option for this course as we want to start from scratch. You will build and learn everything.

Now you need to wait a few minutes for yarn to install the project dependencies.

# 2. Open the project
After the dependencies are installed, you should see the following output:

> ![Screenshot 2021-03-15 at 13.44.12.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615808663640/Bl2dtvXkn.png)

Now, let's open the project and start hacking around:
- `cd my-app` (replace `my-app` with your project name)
- open the project in your favourite code editor

**Note**: You can start the application by running `yarn dev`, but there is not much to see. Let's add some stuff and run it after!

# 3. Some Keystone basics
There is some basic stuff you need to know about KeystoneJS before moving further. Let's start by talking about lists.

**Lists** - Lists are a way of representing data. If you worked with Node.js and MongoDB, you could associate lists with models. For instance, in this application, we have a list for users. That is a model for the user. The list specifies what you store about each user, where the fields come into play.

**Fields** - The lists are made of fields. A field represents a piece of information about the user (in our example). For instance, in the "user" list, you might add fields such as the:
* first name
* last name
* email

...and so on!

It's easier to understand if you see an example. Thus, below you can see a possible representation of the `User` list.

```
const { Text, Password } = require('@keystonejs/fields');

module.exports = {
    fields: {
        firstName: {
            type: Text,
            isRequired: true
        },
        lastName: {
            type: Text,
            isRequired: true
        },
        username: {
            type: Text,
            isRequired: true 
        },
        password: {
            type: Password,
            isRequired: true
        }
    }
}
```

Now that we cleared the basics, we can move further and build the application!


The `User` list has the following fields for the user:
* first name
* last name
* username
* password

# 4. Create the folder structure
First of all, you need to set up the folder structure of your application.

Start by creating a new folder `schemas` in the root folder of the project. This is the folder for our lists. Alternatively, you can name it `lists`,  `models` or whatever you think it's more descriptive.

In the newly-created folder (`schemas`), create a new file called `User.js`.

Your project structure should look as follows:
> ![Screenshot 2021-03-15 at 17.41.15.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615822896496/fbH2BwvTU.png)

# 5. Create the User list (model)
Now that you have the project structure in place, let's create the `User` list. Open the file `schemas > User.js` and write the code below:

```
const { Text, Password } = require('@keystonejs/fields');

module.exports = {
    fields: {
        firstName: {
            type: Text,
            isRequired: true
        },
        lastName: {
            type: Text,
            isRequired: true
        },
        username: {
            type: Text,
            isRequired: true 
        },
        password: {
            type: Password,
            isRequired: true
        }
    }
}
```

In this application, you only store the first name, last name, username and password about users. It's important to note that you imported the fields `Text` and `Password` from `'@keystonejs/fields'`. 

For this article, we'll keep it simple and only use these fields. You could expand it to store more information, though.

### Use the User list
Even though you created the list, you cannot use it yet. Head back to `index.js` and add the following code anywhere at the top of the file:

```
const UserSchema = require('./schemas/User');
```

With this line, you imported the `User` list into the `index.js` file to use it. Now, add the following line of code after the `keystone` constant:

```
keystone.createList('User', UserSchema);
```

The above line of code creates a `User` list with the schema you created and specified. After writing the above lines in `index.js`, the file should look as follows:

```js
const { Keystone } = require('@keystonejs/keystone');
const { GraphQLApp } = require('@keystonejs/app-graphql');
const { AdminUIApp } = require('@keystonejs/app-admin-ui');
const { MongooseAdapter: Adapter } = require('@keystonejs/adapter-mongoose');
const UserSchema = require('./schemas/User');
const PROJECT_NAME = 'my-app';
const adapterConfig = { mongoUri: 'mongodb://localhost/my-app' };

const keystone = new Keystone({
  adapter: new Adapter(adapterConfig),
});

keystone.createList('User', UserSchema);

module.exports = {
  keystone,
  apps: [new GraphQLApp(), new AdminUIApp({ name: PROJECT_NAME, enableDefaultRoute: true })],
};
```

Save all the files, and run `yarn dev` in the terminal to start the application. Once the application started, head to `http://localhost:3000/admin` to see what you've done!

Now you should see the Users and the fields you specified! You should have the same view as the images below:

> ![Screenshot 2021-03-15 at 17.36.21.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615822620694/IvW9aVasH.png)
> ![Screenshot 2021-03-15 at 17.37.49.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615822680825/RvRD4ldKO.png)

Well done! Now you are ready.

# 6. Create the Book list (model)
The next step is to create a Book model. So people using the application can keep track of the books they are reading!

Create a new file, `Book.js`, in the `schemas` folder. Once you created the file, write the following code (or modify it as you wish):

```
const { Text } = require('@keystonejs/fields');

module.exports = {
    fields: {
        name: {
            type: Text,
            isRequired: true
        },
        author: {
            type: Text,
            isRequired: true
        },
        genre: {
            type: Text,
            isRequired: true
        },
        description: {
            type: Text,
            isRequired: true
        },
        edition: {
            type: Text,
            isRequired: true
        }
    }
}
```

This step is similar to how you created the `User` list.

**Note**: There are many more fields, which you can see here - [in the documentation](https://www.keystonejs.com/keystonejs/fields/). However, for this tutorial/course, we keep it simple by using the Text field. I did not use other fields because they need to be installed separately via `npm`/`yarn`. As an exercise, change some of the fields to different types!

Moving further, you need to include the new schema and use it in the `index.js` file. As with the `User` list, open `index.js` and write the following code:

```
const BookSchema = require('./schemas/Book');
keystone.createList('Book', BookSchema);
```

Now, your `index.js` file should look as follows:

```
// [...code removed for simplicity purposes...]
const UserSchema = require('./schemas/User');
const BookSchema = require('./schemas/Book');
const PROJECT_NAME = 'my-app';
const adapterConfig = { mongoUri: 'mongodb://localhost/my-app' };

const keystone = new Keystone({
  adapter: new Adapter(adapterConfig),
});

keystone.createList('User', UserSchema);
keystone.createList('Book', BookSchema);

// [...code removed for simplicity purposes...]
```

At this point, we have the `User` and `Book` list in place. The next step is to create the relationship between them.

# 7. Create the relationship User - Books
So far, you created the User and Book models. However, there is no relationship between the two. How can a user add a book? Thus, in this section, you will create the relationship!

What will the relationship look like?
- a user can have many books
- and a book can have my readers

Thus, we have a many-to-many relationship.

### Modify User.js
The first step is to import the `Relationship` field, as shown in the code below:

```js
const { Text, Password, Relationship } = require('@keystonejs/fields');
```

Now, you need to add a new field, which is of a `Relationship` type. Write the following code in `User.js`, after the `password` field:

```js
books: {
    type: Relationship,
    ref: 'Book.readers',
    many: true
}
```

The `User.js` file is almost the same, except for the two additions. Let's take each field one by one and see what they mean:
* `type: Relationship` - like the type for the `username` field is "text", we have "relationship" for this field.
* `ref: 'Book.readers'` - this field indicates that the `books` field relates to the `readers` field in the `Book` list.
* `many: true` - each user can read many books, and each book can have many readers (many-to-many relationship).

That's all you have to do for the `User` list.

### Modify Book.js
Now you need to do something similar to the `Book` list. Head over to the file `Book.js`, and import the `Relationship` field.

```js
const { Text, Relationship } = require('@keystonejs/fields');
```

After that, add the following code after the `edition` field:

```js
readers: {
    type: Relationship,
    ref: 'User.books',
    many: true
}
```

It's similar to what you did for the `User` list with only one difference - `ref: 'User.books'`.

### Relationship created
Well done! You created the relationship between *Readers* and *Books*. You can test the relationship by adding readers and books and link them.

As an example, I created a reader and a book to show it to you. See the images below:

> ![ss1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615827827673/nbo_VRQvj.png)
> ![ss2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1615827834929/BFszff-Dy.png)

Up to this point, you have the basic functionalities up and running. If you want to exercise, you can do the following steps:
1. Create a `Review` model
2. Create the relationship between the models (e.g. a book can have multiple reviews, each author can leave multiple reviews, and so on) 
3. Test it

Let's move onto the next section!

# Admin field
Before moving onto authorization and authentication, you need to add a new field to the `User` list. The new field is called `isAdmin`, and it's used to give a user admin privileges.

Go to the `schemas` folder and open `User.js`. At the top of the file, import the `Checkbox` field, like in the code below:

```
const { Text, Password, Relationship, Checkbox } = require('@keystonejs/fields');
```

After that, add the following field anywhere you want in the file:

```
isAdmin: {
    type: Checkbox,
    defaultValue: false
}
```

Now, when you create a new user, you have the possibility to make that user an admin. Before moving on, I advise you to create:
1. an **admin** user
2. a normal user

Otherwise, you won't be able to access and test the application!

# Authentication & Authorization
Before proceeding further, read this article on [Authentication versus Authorization](https://www.okta.com/identity-101/authentication-vs-authorization/#:~:text=Authentication%20and%20authorization%20might%20sound,permission%20to%20access%20a%20resource) from Okta, if you are not familiar with the terms.

Now that you know the difference between the two terms let's proceed further. You have a working application, but there is one flaw. The flaw is that everyone can access and modify data. You do not want that, right?

Thus, in this section, we restrict access to the admin panel and accessing & modifying resources.

### Check permissions
The first step is to open your `index.js` file and write the following code after the Keystone constant (`const keystone.....`):

```js
const isAdmin = ({ authentication: { item: user } }) => !!user && !!user.isAdmin;
const isLoggedIn = ({ authentication: { item: user } }) => !!user;

const isOwner = ({ authentication: { item: user } }) => {
  if (!user) {
    return false;
  }

  return { id: user.id }
}

const isAdminOrOwner = auth => {
  const admin = access.isAdmin(auth);
  const owner = access.isOwner(auth);

  return admin ? admin : owner;
}

const access = { isAdmin, isOwner, isLoggedIn, isAdminOrOwner };
```

That's a lot of code! Thus, let's break it down:
* `isAdmin` checks if a user is an admin (duh) and it grants/rejects access to the admin panel based on that
* `isLoggedIn` simply checks if the user is authenticated
* `isOwner` checks if the user is the owner of the resource or not. For instance, you might want to restrict users from deleting resources NOT created by them
* `isAdminOrOwner` checks if the user is an admin or an owner and returns the value.

In the last line, we add the functionalities on the `access` object so we can access them as `access.isAdmin`, for example.

### Modify Lists
Let's put those methods to use. Go into your `index.js` file and find the following code:

```js
keystone.createList('User', UserSchema);
keystone.createList('Book', BookSchema);
```

What you are going to do, is to provide an object instead of the schema. Modify the above two lines, into the following code:

```js
keystone.createList('User', {
  fields: UserSchema.fields,
  access: {
    read: access.isAdminOrOwner,
    create: access.isAdmin,
    update: access.isAdmin,
    delete: access.isAdmin,
    auth: true
  }
});

keystone.createList('Book', {
  fields: BookSchema.fields,
  access: {
    read: true,
    create: access.isLoggedIn,
    update: access.isAdminOrOwner,
    delete: access.isAdminOrOwner,
    auth: true
  }
});
```

Like I said, instead of providing the schema directly, you provide an object now. For the `fields`, you provide the fields from the schemas you created at the beginning of the article. Basically, the two are equivalent:

```js
keystone.createList('User', UserSchema);

// or

keystone.createList('User', { fields: UserSchema.fields});
```

What's new is the `access` object which allows tighter control of the resources. The code is rather intuitive, and for each CRUD operation, you specify the access. 

For instance, **only the admin can create/read/update/delete other users**. Additionally, the users can only see their accounts, but not other people's accounts! On the other hand, you **allow everyone to read your book reviews** (`read: true`). The user has to be logged in to create a book review. Regarding updating and deleting books, one has to be the admin or the owner.

### Create authStrategy
To be able to allow or restrict access, you have to install the `auth-password` package. You can do so by running either one of:

```
npm install @keystonejs/auth-password

// or

yarn add @keystonejs/auth-password
```

After the package is installed successfully, add the following line at the top of your `index.js` file:

```js
const { PasswordAuthStrategy } = require('@keystonejs/auth-password')
```

Now you are ready to configure the authentication. Write the following code before the `module.exports` line:

```js
const authStrategy = keystone.createAuthStrategy({
  type: PasswordAuthStrategy,
  list: 'User',
  config: {
    identityField: 'username',
    secretField: 'password'
  }
})
```

Here you create an `authStrategy` constant, where you specify the type, the list it should use (`User` in this case), and the fields used to log in. In this application, users login using their `username` and `password`.

Observe the final two lines in the code below - `authStrategy` and `isAccessAllowed: isLoggedIn`. You pass the `authStrategy` and restrict access to the admin panel if the users are not logged in.

```js
module.exports = {
  keystone,
  apps: [
    new GraphQLApp(), 
    new AdminUIApp({ 
      name: PROJECT_NAME, 
      enableDefaultRoute: true, 
      authStrategy, 
      isAccessAllowed: isLoggedIn 
    })],
};
```

Save everything, and run the application - `yarn dev`. Well done! You set up authorization and authentication in your application! Now the admin has full power, whereas other users are pretty limited to creating books and managing their books.

`isAccessAllowed: isLoggedIn` allows everyone to access the **admin page** as long as they are logged in. If you want to allow only admins, change the line to:

```
isAccessAllowed: isAdmin
```

#### Caveat for isAdmin field
Before implementing authentication and authorization, you added the `isAdmin` field to users. However, there is one problem - everyone can make themselves admin. Luckily, there is a way to restrict that.

Open the `User.js` file, and modify the field as follows:

```js
isAdmin: {
    type: Checkbox,
    defaultValue: false,
    access: ({ authentication: { item: user } }) => {
        return user.isAdmin
     }
 }
```

After making this change, only the admins can make other users an admin. It's a great way to prevent everyone from making themselves an admin.

**P.S**: The way you set the access field is similar to how you did it in the `index.js` file for the **User** and **Book** lists.

# Conclusion
In this tutorial, you learnt the basics of KeystoneJS. From here, you can add more features to make a complex application.

Some ideas:
* add a front-end
* allow people to comment on books
* create profiles for each user