## How To Use Async/Await in JavaScript

The purpose of this article is to teach you how to work with promises by using async/await. Why would you want to use async/await, though? The most significant benefit is that it makes the code more readable and cleaner by removing the promise chains.

Therefore, let us see what async/await is and how to use it.

# The usual promise
Let's see an example of a promise in JavaScript:

```js
fetch("https://api.app/v1/users/cp"); // dummy URL
.then(response => response.json());
.then(console.log);
```

Probably it looks familiar to you. Now, let's see the same code re-written with async/await.

```js
async function getData() {
    const response = await fetch("https://api.app/v1/users/cp/avatar"); // dummy URL
    const data = response.json();

    console.log(data);
}
```

Which one do you prefer? In my opinion, it is clearer to understand what happens in the code when using async/await.

# What async/await is
Async/Await is built on top of promises, and it allows us to write asynchronous code better. It is a new way of writing asynchronous code, besides promises and callbacks.

The power of Async/Await is that it makes the code look more organised and cleaner. It makes it look more "synchronous" too.

There are two particular keywords:
1. `async`
2. `await`

We use the keyword `async` at the beginning of the function. When using the `async` keyword, it means the function always returns a promise. Also, if we want to use the keyword `await` inside a function, that function must always start with the keyword `async`. The code below returns a promise when we call the greeting function. The promise object contains a state (fulfilled or rejected) and a result (in this case is a string).

```js
async function greeting(name) {
    return `Hello, ${name}!`;
}
```

Secondly, we can use the keyword `await` to wait until a promise fulfils and return the result.

```js
async function greeting(name) {
    return greet = await Promise.resolve(`Hello, ${name}!`);
}

greeting("Catalin").then(console.log); // Returns "Hello, Catalin!"
```

The above example might not be useful, but imagine when you make an API call - see the example above, in the first section of the article.

# Other benefits
### Better error handling
First of all, we can handle the synchronous code and asynchronous code in the same construct. Secondly, if there is an error in resolving the promise, the control jumps to the catch block to handle the error.

You can even wrap multiple promises in the same try block, and the code catches the errors from all promises, not only from one. It also tells you where the error occurred, in which promise.

```js
async function getUserInfo() {
    try {
        const response = await fetch("https://api.app/v1/users/cp/avatar"); // dummy URL
        const data = response.json();

        console.log(data);
    } catch (err) {
        console.log(err);
    }
}
```

In the above code snippet, the code jumps to the `catch` block if there is an error.

### Better code
Async/await allows us to write clear and better code. It makes it easier and quicker to understand what happens in the code because it looks more like synchronous code.

Even in short code snippets such as the ones from "The usual promise" section, we can see how clean the code looks.

### Conditionals
Another benefit of using async/await is that it makes it easier and cleaner to work with conditionals. The code snippets below are basic, and they do not handle errors. Their sole purpose is to show the difference between Promises and async/await when using conditionals.

```js
const getUserInformation = () => {
    return getUser()
    .then(user => {
      if (user.profile) {
        return getUserProfile(user.id)
        .then(userProfile) {
          console.log(userProfile);
          return userProfile;
        }
      } else {
        console.log(user);
        return user;
      }
    });
};
```

The above snippet illustrates using conditionals in a Promise. Even though the code is not complex, it is difficult to read it. Now imagine how complex the code would be if we would have more if statements, and more requests.

Below, you can see the code re-written using async/await. Does not it look better? It is easier to read the code and understand what happens.

```js
const getUserInformation = async () => {
  const user = await getUser();

  if (user.profile) {
    const userProfile = await getUserProfile(user.id);

    console.log(userProfile);
    return userProfile;
  } else {
    console.log(user);
    return user;
  }
};
```
Therefore, you can improve your code by converting promises to async/await. You can see that they improve code readability by a significant margin.

# Conclusion
In conclusion, let us recap what you learnt:
* Adding async to your method header, you always return a promise. Besides that, it allows you to use the await keyword. Therefore you can wait until a promise is resolved.
* Makes the code more explicit, easier to understand, and more concise.
* Using the await keyword, you block the code from executing until the promise is resolved or rejected.
* When the promise cannot settle, it generates an exception.
