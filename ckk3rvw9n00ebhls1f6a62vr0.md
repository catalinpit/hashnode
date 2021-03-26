## JavaScript ES2021 - You Need To See These ES12 Features

It's important to start the article by mentioning that ES2021 or ES12 is in stage 4 of the process. That means it's not released yet. The plan is to release ES12 in June 2021. Despite that, we can have a look at the features it's going to bring.

What's new in ES12?
* String.prototype.replaceAll()
* Promise.any
* WeakRef
* `&&=`, `||=` and `??=`
* Numeric separators

# Numeric Separators
Working with large numbers can quickly become confusing. For instance, consider the number "92145723". You have to pay close attention to see that it's 92 million and something.

With the new addition from ES2021, you can re-write the same number as follows "92_145_723". That is, you use underscores to improve the readability. You can see it's already better, and easier to understand the number. Now, you can clearly see it's 92 million and something.

Therefore, the numeric separator feature is simply for improving readability. It does not affect the performance of your application negatively or positively.

```js
// previous syntax before ES12
const number = 92145723;

// new syntax coming with ES12
const number = 92_145_723;
```

# String.prototype.replaceAll()
The new method `replaceAll` does not bring groundbreaking changes, but it's a small, nice addition. As the name implies, using the method, you can replace all the occurrences from a String.

It's always easier with an example, so let's see the method in action:

```js
// replacing all occurrences of x with a
// jxvxscript becomes javascript
'jxvxscript'.replaceAll('x', 'a');
```

Before `replaceAll`, you would have to use RegEx to replace all the character/word occurrences. Thus, it's a welcome addition that allows you to replace text easier and quicker.

# Logical Assignment Operators
With the new logical assignment operators - `&&=`, `||=` and `??=` - you can assign a value to a variable based on a logical operation. That is, it combines the logical operators with the assignment expression. 

Think of them as similar to the `+=`, `-=`, `*=` and `/=` operators. Do not worry; it will make more sense once you see some examples for each operator.

### And and equals (&&=)
The `and and equals` operator performs the assignment only when the left operand is truthy. Let's see an example:

```js
let first = 10;
let second = 15;

first &&= second;
```

The equivalent of the above expression is `first && (first = second)`. If it's hard to grasp the operator, think of it as follows:

```js
let first = 10;
let second = 15;

if (first) {
    first = second;
}
```

The above code shows how you do the same thing before ES2021. Let's go more in-depth and see what `first &&= second` means:
* if `first` is truthy, then the variable `second` is assigned to `first`.
* otherwise, if `first` is falsy (false, 0, -0, 0n, "", null, undefined and NaN), then it does not do anything - `second` is not assigned to `first`.

### Or or equals (||=)
On the opposite spectrum of `&&=`, the logical OR performs the assignment only when the left operand is falsy. As usual, let's see an example:

```js
let first = null;
let second = 15;

first ||= second; // first is 15 now
```

The equivalent of the above expression is `first || (first = second)`. This means that the variable `first` gets assigned `second` only when `first` is a falsy value. If the variable `first` is truthy, the assignment is not performed.

After running the code, the variable `first` will be assigned the number "15". If you replace `let first = null` with `let first = 10`, then the assignment does not happen. The variable `first` remains "10".

The equivalent code with an "if statement" is as follows:

```js
let first = null;
let second = 15;

if (!first) {
    first = second;
}
```

### Question question equals (??=)
Similarly to the [Nullish Coalescing Operator](https://catalins.tech/nullish-coalescing-operator-in-javascript-what-is-it-and-how-to-use-it), an assignment is performed only when the left operand is `nullish` or `undefined`.

```js
let first = null;
let second = 15;

first ??= second;
```

`first ?? (first = second)` is the equivalent of the above expression. The variable `first` gets assigned the variable `second` only if `first` is "null" or "undefined". In this example, `first` is 15. If we replace `let first = null` with `let first = 20`, the assignment does not happen. The variable `first` stays "20".

The equivalent code with an "if statement" is as follows:

```js
let first = null;
let second = 15;

if (first == null || first == undefined) {
    first = second;
}
```

With this operator, it's important to note that it does not check for other falsy values. It only checks for `null` and `undefined`, like the Nullish Coalescing Operator. With that being said, whenever you struggle with these operators, look at the alternative code with an "if statement". After you use them for a while, you will get used to them.

# Promise.any
We have a new Promise method - `Promise.any()`. The new method takes multiple promises and resolves once any of the promises is resolved. Promise.any() takes whichever promise resolves first. Hence its name - any.

```js
try {
    const firstPromiseResolved = Promise.any(promisesArray);

    // do more work with the first promise resolved
catch(e) {
   // catch the error
}
```

On the other side, if no promise resolves, Promise.any() throws an `AggregateError` exception. It also tells the reason for the rejection if all the promises are rejected. That's all it is about Promise.any; feel free to play with it!

# WeakRef
WeakRef is the shorthand for Weak References, and its primary use is to hold a weak reference to another object. That means it does not prevent the garbage collector from collecting the object. The Weak Reference is useful when we do not want to keep the object in the memory forever.

But why do we need the WeakRef in the first place? In JavaScript, the object is not collected by the garbage collector as long as a reference to that object exists. Thus, it keeps the object in the memory, which leaves you with less memory. The WeakRef implementation allows you to avoid that.

You can create a Weak Reference by using `new WeakRef`, and you can read a reference by calling the `deref()` method. A simple example would be:

```js
const largeObject = new WeakRef({
     name: "CacheMechanism",
     type: "Cache",
     implementation: "WeakRef"
});

largeObject.deref();
largeObject.deref().name;
largeObject.deref().type;
largeObject.deref().implementation;
```

Mind you; the example is just for illustrative purposes showing how to access and read weak references.

Be careful when using them. Even though the WeakRef can be useful in some cases, the TC39 Proposal advises to avoid it if possible. You can read [here](https://github.com/tc39/proposal-weakrefs#a-note-of-caution) why you should avoid it if possible.

# Conclusion
In this article, you learnt about the new features coming to JavaScript with ES12. For more information, keep an eye on the [ECMAScript finished proposals](https://github.com/tc39/proposals/blob/master/finished-proposals.md).