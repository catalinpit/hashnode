## Parameter And Argument - What Is The Difference Between Them?

Many developers, use the words "parameter" and "argument" interchangeably. However, their meanings are not the same. In this article, I aim to explain the subtle difference between these two terms.

Therefore, let us clarify what each of these terms means.

<h2>Parameters</h2>

The parameters refer to the variables that are in the method/function header. These variables, which we call parameters, receive a value when we call the function or the method. We can think of them as placeholders. In other words, they tell us what values we need to pass to the function/method.

However, an example helps us understand this term better.&nbsp;

```js
function sayHello(name) {
    console.log(`Hello ${name}`);
}
```

In the above function, the "name" variable is the parameter. The "name" parameter gets assigned a value when we call the function <code>sayHello</code>.

<h2>Arguments</h2>

The term "arguments" refers to the actual value we pass to the function when we call it. When we call the function <code>sayHello</code> with the value "Catalin Pit", the value is the argument.

```js
sayHello('Catalin Pit');
```

In the above example, "Catalin Pit" is the argument. In other words, the parameters are the placeholders for where the arguments (values) go.

<h2>Conclusion</h2>

I hope you understand now what is the difference between these two terms.

To sum up, the parameters are in the method/function definition, and I like to think of them as placeholders for the actual values we pass when calling the method/function. On the other hand, arguments are the actual values that we pass when we call the function/method.

