## The Fastest Way To Replace All Occurrences Of A String In JavaScript

[ECMAScript 2021](https://catalins.tech/javascript-es2021-you-need-to-see-these-ecmascript-2021-features) will introduce a new String method, called `replaceAll`. As you can infer from the name, this method allows you to replace all the occurrences of a String in one go.

Let's see the new method in action. With the code snippet below, you replace the word "*boring*" with the word "*powerful*".

```
const myStr = "JavaScript is a boring programming language. JavaScript is the most boring!";

const newStr = myStr.replaceAll("boring", "powerful");

console.log(newStr);
```

Run the above code to see what happens! However, it's important **to note** that the method `String.prototype.replaceAll()` does not modify the string on which it's called. The method returns a new String.

Before it, you would need to use RegEx or other workarounds, which would take longer. Therefore, the new method `replaceAll` is a great addition. 

If you want to read more about the new [ECMAScript 2021 Features](https://catalins.tech/javascript-es2021-you-need-to-see-these-ecmascript-2021-features), I recommend reading the [JavaScript ES2021](https://catalins.tech/javascript-es2021-you-need-to-see-these-ecmascript-2021-features) article.