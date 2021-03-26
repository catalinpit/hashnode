## Optional Chaining In JavaScript - What Is It And How To Use It?

# What Is Optional Chaining in JavaScript

According to the MDN docs, optional chaining is "*shorter and simpler expressions when accessing chained properties when the possibility exists that a reference may be missing*". In simpler words, optional chaining allows us to access chained properties, such as object properties.

Let us illustrate optional chaining with an example:

```js
const person = {
 name: "Catalin Pit",
 socialMedia: {
  twitter: "@catalinmpit",
  instagram: "@catalinmpit",
  linkedin: "@catalinmpit",
 },
 experience: "Junior",
 employed: true
};
```

In the example, you can see a person object with different properties such as name, social media accounts, experience, and a boolean field `employed`. Let's say we want to access the `instagram` property. We would have to check if the:
* person object exists
* `socialMedia` field exists
* `instagram` field is present

We would have to do three checks, and the if statement would like like this:

```js
if (person && person.socialMedia && person.socialMedia.instagram) {
 console.log(person.socialMedia.instagram);
}
```

We can agree that there is quite a lot of code for a simple check. However, we can shorten it by using the optional chaining feature.

# Optional Chaining
The optional chaining feature is similar to the `.` chaining operator. The only difference is that it returns the value of `undefined` if the reference is `null` or `undefined`. That is if the object property does not exist. Similarly, if a function does not exist, it returns `undefined`. However, if you are looking for extra information, I recommend you read the MDN docs explanation [here (click-me)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining).

Coming back to our previous example, let's see how can we shorten the if statement. First of all, we refactor the if statement to look as follows:

```js
if (person?.socialMedia?.twitter) {
 console.log(person.socialMedia.twitter); // outputs @catalinmpit
}
```

It is still three lines of code, but it is easier to write it and read it. Still, we can make it shorter. Would you believe me if I would say we can shorten it to one line? Here is the one-liner:

```js
console.log(person?.socialMedia?.twitter)
```

Ta-da! Instead of three lines of code, we only have one, and that is without sacrificing the code readability.

# More Examples
We can use optional chaining for arrays, and functional calls. Thus, I want to illustrate some more examples of can you use this operator.

Let us start with the **arrays**.

```js
const examScores = [90, 100, 84, 78, 65, 79, 56];
console.log(examScores?.[3]);
```

We check if the array `examScores` exists, and if it does, we output the fourth array element.

In the same vein, we can use it for **function** calls as follows:

```js
const response = myAPI.getData?.();
```

Optional chaining is very useful when working with APIs, where a method might not be available for various reasons. We can check if the method exists, and proceed with our code based on whether it exists or not.

# Conclusion
I find this feature extremely useful, and I like that it shortens your code without sacrificing the code readability. Let us see the takeaway points from this article:

* Optional chaining allows us to check the properties of an object
* Especially useful when the properties might be missing
* It returns `undefined` if a property/function does not exist, instead of throwing an error
* It shortens the code without sacrificing readability

> If you enjoyed the article, consider sharing it so more people can benefit from it! Also, feel free to @me on Twitter with your opinions.

<hr/>

_[Daily](https://r.daily.dev/get?r=devto) delivers the best programming news every new tab. We will rank hundreds of qualified sources for you so that you can hack the future._

[![Daily Poster](https://dev-to-uploads.s3.amazonaws.com/i/b996k4sm4efhietrzups.png)](https://r.daily.dev/get?r=devto)