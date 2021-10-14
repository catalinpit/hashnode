## Check if an Array of Objects Contains a Value in JavaScript

Having duplicate data in your application is not desired. Imagine you have an array with people, and you have the same person multiple times. Thus, in this article, you will see how to check if an array of objects contains an object with a specific value.

Let's take the following phone book as an example:

```js
const people = [
  { name: 'Alan Turing', number: '040-123456', id: 1 },
  { name: 'Ada Lovelace', number: '39-44-5323523', id: 2 },
  { name: 'Barbara Liskov', number: '12-43-234345', id: 3 },
  { name: 'Mary Poppendieck', number: '39-23-6423122', id: 4 }
]
```

The question is - how do you prevent users from adding a person that already exists?

The answer is `Array.prototype.some()`. You can use the method "some" to check if the person is already there.

## some() method

The `some()` method checks if at least one element in the array passes a condition defined by you. If it finds at least one element matching the condition, it returns true. Otherwise, it returns false.

It's important to note that it returns `true` as soon as it finds an element that passes the condition. For example, if the first element matches the condition, it stops searching and returns `true`.

Also, `some()` does not mutate (change) the array.

## Solution

Let's start solving the problem. 

The first step is to create an object that is a duplicate of an existing object from the array.

```js
const newPerson = {
    name: 'Ada Lovelace',
    number: '39-44-5323523',
};
```

The next step is to use the method `some()` to find whether the new person is already in the array or not. Since it's a simple check, we use an arrow function.


```js
const newPerson = {
    name: 'Ada Lovelace',
    number: '39-44-5323523',
};

const duplicate = people.some(person => person.name === newPerson.name);
```

Lastly, it shows the appropriate message based on whether the new person already exists or not.

Below you can see the complete code.

```js
const newPerson = {
    name: 'Ada Lovelace',
    number: '39-44-5323523',
};

const duplicate = people.some(person => person.name === newPerson.name);

if (duplicate) {
    console.log(`you already added ${newName}!`)
} else {
    console.log(`${newName} was added to the array`);
}
```

## Conclusion

It's important to note that there are other ways to accomplish the same task. After all, that's programming!

One way would be to loop manually over all the objects from the array and check if the object exists.

Another way would be to use the method `Array.prototype.find()`, which returns the object if it exists, or `undefined` otherwise.

Anyways, I am curious - how would you solve this task?