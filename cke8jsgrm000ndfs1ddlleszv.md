## Nullish Coalescing Operator (??) In JavaScript

# What Is Nullish Coalescing Operator in JavaScript

The Nullish Coalescing Operator allows us to check if a value is `null` or `undefined`, and provide a fallback value if that is the case. 

However, let us have a look what [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) docs say as well. According to MDN, the nullish coalescing is "*a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand.*".

This type of operator is handy when we want falsy values like 0 (zero) or empty strings ('' or "") to be valid values.  

Before proceeding further, let us remind ourselves what are the falsy values. In JavaScript, the following values are always falsy:
* NaN
* 0
* empty string - "" or ''
* null
* undefined
* false

Now let us illustrate the nullish coalescing operator with an example:

```js
let score = 0;
let pass = 0 ?? 60;
```
What do you think the value of pass is? It is 0, because the `??` operator does not coerce falsy values. Therefore, the nullish coalescing operator only returns the right-hand side operand, if the left-side operand is `null` or `undefined`. 

In the above example, it would return 60 if we would have had `undefined` or `null` instead of the number 0.

Let us actually replace 0 with undefined/null would return 60.

```js
let pass = null ?? 60;
let pass = undefined ?? 60;
```

In this case it makes sense to return the right-hand side value, because `undefined`/`null` means that the variable was not assigned a value.

# The usual way - the OR operator
In the usual way, we would use the `||` operator to check the value of the `pass` variable. However, there is a problem with the operator. 

What if there are some falsy values like `0` or `''`? The operator does not return the correct value. Let us illustrate it with an example:

```js
let pass = 0 || 60;
```

In the above case, the `||` operator returns "60" because "0" is evaluated as a falsy value. In addition, `||` is a boolean logical operator, which is why it coerced "0" to a falsy value, and returned the number "60".

So how can we solve the problem? We can solve the problem with the help of the nullish coalescing operator. By replacing `||` with `??` we get the correct value, which is "0" in this case.

# The Nullish Coalescing and Optional Chaining Operators
These two operators work very well together. If you remember from our previous post about the [Optional Chaining operator](https://catalins.tech/optional-chaining-in-javascript-what-is-it-and-how-to-use-it), we use it to access chained object properties easier. For in-depth information about this operator, feel free to read the article.

Why do they work well together? The reason why they work well together is that they both treat `undefined`, and `null` as valid values. Therefore, it makes it handy when we access properties that are one of the two values - `undefined` or `null`.

```js
const person = {
  name: "Catalin Pit",
};

console.log(person.name?.toLowerCase() ?? "No name defined"); // outputs "catalin pit"
console.log(person.employer?.toLowerCase() ?? "No employer defined"); // outputs "No employer defined"
```

Therefore, these two operators are convenient both on their own and when used together.

# Conclusion
The Nullish Coalescing Operator is handy when you want to use falsy values as a default. Or simply when you treat the falsy values as valid ones. Therefore, let us see the key points from the article:

* The Nullish Coalescing Operator returns the right-hand side value when the left-side one is `undefined` or `null`.
* Using the OR (`||`) operator, you can run into troubles with falsy values like 0 and empty strings. 
* `||` is a logical boolean operator, and it coerces values. Thus, it does not return falsy values. 

> If you enjoyed the article, consider sharing it so more people can benefit from it! Also, feel free to @me on Twitter with your opinions.