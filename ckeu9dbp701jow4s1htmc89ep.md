## JavaScript ES2020 - The Features You Should Know

ES2020 or ECMAScript 2020 brings exciting features to JavaScript. In this article, I want to talk about my favourite features from ES2020. That means the article does not cover all the additions. Thus, let us see my favourite new additions:

* Dynamic Import
* Nullish Coalescing Operator
* Optional Chaining Operator
* Private Class Variables
* Promise.allSettled

For more information and all the additions, have a look at the official [ECMAScript Language Specification](https://tc39.es/ecma262/2020/). Additionally, you can have a look at the <a href="https://github.com/tc39/proposals/blob/master/finished-proposals.md">finished proposals</a>.

# Dynamic Imports
One of the additions is that we can import dependencies dynamically with async/await. That means we do not have to import everything before, and we can import the dependencies only when we need them. As a result, the performance of the application improves by loading the modules at runtime.

How does it improve performance? With the conventional module system, we import the modules statically at the beginning of the program. Whether we need them now or later, we have to import them first. Also, all the code from an imported module is evaluated at the load time. Thus, it slows down the application unnecessarily. Why? Because it downloads the imported modules and evaluates the code of each module before executing your code.

Let us see an example.

```js
if (calculations) {
    const calculator = await import('./calculator.js');
    const result = calculator.add(num1, num2);

    console.log(result);
}
```

In the above code snippet, you can see that we only import the calculator module when we want to perform calculations. As a result, we do not slow down the application unnecessarily by loading all the code before the runtime. Therefore, Dynamic imports is a handy addition.

# Nullish Coalescing Operator
"The nullish coalescing operator (??) is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand." [Source: MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator")

Basically, the Nullish Coalescing Operator allows us to check if a value is null or undefined, and provide a fallback value if that is the case. Let us see an example:

```js
let score = 0;
let pass = score ?? 60;

console.log(pass);
```

In the above code snippet, the value of `pass` is 0. The reason is that the `??` operator does not coerce zero to a falsy value. The variable `pass` only gets 60 assigned if the variable `score` is `undefined` or `null`.

However, what is the difference between double pipes "||" and this operator? When using the double pipes "||", it always returns a truthy value which might lead to some unexpected results. When using the nullish coalescing operator, we can be more strict and thus only allow the default when the value is null or undefined.

For instance, let us say we have the following code:

```js
let score = 0;
let pass = score || 60;

console.log(pass);
```

In the above example, the value 0 is treated as a falsy value when using `||`. In the above code snippet, the value of `pass` is 60, which is not what we want. Therefore, the double question mark allows us to check if a variable is nullish, which means if a variable is either undefined or null.

# Optional Chaining Operator
"Shorter and simpler expressions when accessing chained properties when the possibility exists that a reference may be missing." [Source: MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

Using the Optional Chaining Operator, we can access deeply nested properties from an object. If the property exists, the operator returns its value. If the property does not exist, the operator returns undefined.

```js
const person = {
 name: "Catalin Pit",
 employer: {
  name: "Catalins Tech",
 }
};

console.log(person?.employer?.name);
```

The above code snippet illustrates an example of accessing deeply nested object properties. However, we can use it on arrays, and function calls as well. Below, in the code snippet, you can see that we check if the array exists, and if it does, we access the third value. Also, you can see checking if a function from an API exists, and if it does, it calls it.

```js
const allowedValues = [1, 5, 10, 13, 90, 111];
console.log(allowedValues?.[2]);

// functional call
const response = myAPI.getData?.();
```

In conclusion, the optional chaining operator is handy, and it also helps us make the code more readable and shorter. 

# Promise.AllSettled 
The new method, Promise.allSettled() waits for all promises to be settled. That is, it takes an array of Promises, and it only returns when the promises are settled, either rejected or resolved.

When this function returns, we can loop over each Promise and see whether it was fulfilled or rejected, and why. Let us see an example of this function in action.

```js
const promise1 = Promise.resolve(5);
const promise2 = Promise.reject("Reject promise");
const promises = [promise1, promise2];

Promise.allSettled(promises)
    .then(results => console.log(`Here are are your promises results`, results))
    .catch(err => console.log(`Catch ${err}`));
```

The above code returns an array of objects, and each object represents a Promise. The object has a status and a value if the Promise is fulfilled, or status and a reason if the Promise is rejected. Therefore, `Promise.AllSettled` is useful when you want to complete all the promises, irrelevant whether they are rejected or fulfilled. 


# Private Class Variables
From now on, we can create private variables in classes in JavaScript as well. All you need to do to make a private variable is to add the hash symbol in front of the variable. For instance, `#firstName` is a private variable which cannot be accessed outside a class.

Trying to call the variable outside of the class, results in a SyntaxError.

```js
class Person {
  #firstName = "Catalin";
  getFirstName() 
  { 
      console.log(this.#firstName) 
   }
}

const person1 = new Person();
person1.getFirstName() // "Catalin"

console.log(person1.firstName); // Returns "undefined"
console.log(person1.#firstName); // Returns "Uncaught SyntaxError: Private field '#firstName' must be declared in an enclosing class"
```

In the code above, you can see a private class variable in action. Trying to access the variable `firstName` outside the class, we get an error. Therefore, the addition is handy when we do not want to expose data outside a class.

# Conclusion
The additions from the article are not the only ones. There are more, and I encourage you to have a look at the official [ECMAScript Language Specification](https://tc39.es/ecma262/2020/) to see all of them. Also, I encourage you to play with the features to get a taste of them.

To conclude, in this article you learnt about:
* Dynamic Imports
* Nullish Coalescing Operator
* Optional Chaining Operator
* Promise.allSettled
* Private Class Variables

> If you enjoyed the article, consider sharing it so more people can benefit from it! Also, feel free to @ me on Twitter with your opinion.