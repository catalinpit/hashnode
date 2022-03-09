## How to Store a Javascript Array in localStorage

The `localStorage` enables you to store data in the browser. The data stored is in the form of key/value pairs and it does not expire when you close the browser.

It's also important to note that the `localStorage` only stores strings. That brings us to the theme of this article - how do you store arrays?

## JSON Methods

There are two JSON methods that can help us "store arrays" in `localStorage`:
* `stringify()` - It helps us convert the array into a string
* `parse()` - It allows us to parse the string and construct a JavaScript array

Why "stringifying" and "parsing" the data? 

Before you save the array in the `localStorage`, you need to convert it to a string since it can only store strings.

When you retrieve the array from the `localStorage`, you will get a string, so you need to convert it to an array if you want to manipulate it.

## Solution

Let's say we have an array containing links to some blogs we own.

```javascript
const myBlogs = ["https://catalins.tech", "https://exampleblog.com"];
```

We can stringify the array as follows:

```javascript
JSON.stringify(myBlogs)
```

The array becomes a string and you can save it into your browser's local storage.

### Save Array In localStorage

You can save the array by using the `setItem` method.

```javascript
const myBlogs = ["https://catalins.tech", "https://exampleblog.com"];
localStorage.setItem('links', JSON.stringify(myBlogs));
```

The `setItem` method takes two parameters:
* key - the "links" is the key
* value - the array of blogs is the value

As an exercise, run the two lines of code in your browser's console. After running the code, go to the "Applications" tab and click on "Local Storage".

You should see the array of links, as shown in the image below.

![Local Storage Example with JavaScript](https://cdn.hashnode.com/res/hashnode/image/upload/v1646837796356/qzJaaHk0Y.png)

### Get Array From localStorage

If you want to retrieve the array from the local storage, you can use the `getItem` method. The method takes only one parameter, the "key", and returns the "value" in a string format.

The last line of code retrieves the array from the local storage and converts it from a string to an array.

```javascript
const myBlogs = ["https://catalins.tech", "https://exampleblog.com"];
localStorage.setItem('links', JSON.stringify(myBlogs));

const storedBlogs = JSON.parse(localStorage.getItem('links'));
```

The above code snippet illustrates the complete solution. It shows how to save and retrieve an array from the local storage.