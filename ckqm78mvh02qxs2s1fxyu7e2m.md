## GitHub Copilot - Will Artificial Intelligence Replace Developers?

> %[https://www.youtube.com/watch?v=uwfhDNxR_Zw]

Will AI replace developers?

Will you lose your job because of AI?

These two are some of the questions I have seen online for a long time. However, they intensified even more after GitHub released the Copilot.

Thus, in this article, you will see an overview of GitHub Copilot and my thoughts about it.

# What is GitHub Copilot?

According to GitHub, their Copilot application is an artificial intelligence pair programmer that "helps you write code faster and with less work".

GitHub Copilot is a Visual Studio Code extension that generates code based on either a `docstring`, `comment` or `function name`. For instance, you could add the following comment, and the Copilot will generate the appropriate piece of code:

```js
// find all images and add a black border
```

In simpler words, you can write comments to describe the functionality you want, and the extension generates the appropriate code for you. 

The video shows an example I created earlier. It's important to remember that I created just a simple example, but it can do more complex stuff!

%[https://www.youtube.com/watch?v=edSZh-tpTIk]

I would say it's scary and fascinating at the same time! I am highly impressed with it. So, the question is...

# Will Artificial Intelligence Replace Developers?

Even though applications like the Copilot are helpful and super powerful, I still believe we are far from being replaced by them.

After playing with the GitHub Copilot for a while, you can see that it's pretty limited and does not always come up with a reasonable solution. 

Applications like the Copilot does not create a fully-fledged application for you. For example, you cannot provide a comment such as `// build an e-commerce app` and expect the Copilot to do it for you. It cannot even create an extremely basic Express server for you.

Thus, **for complex scenarios**, these AI applications are not very useful. However, for smaller tasks and boilerplate code, they are extremely useful. Take the piece of code below as an example:

```js
function getDaysBetweenTwoDates(start, end) {
    const startDate = new Date(start);
    const endDate = new Date(end);

    const diff = endDate - startDate;

    return Math.ceil(diff / (1000 * 60 * 60 * 24));
}
```

The GitHub Copilot generated the full code. I only provided the function header - `function getDaysBetweenTwoDates(start, end) {` - and the extension did the rest. As you can see, it's super useful for such tasks.

The article only scratches the surface, but there are other things to take into consideration, such as:
* How accurate is the code?
* How secure is the code?
* Will the generated code work?
* Will people blindly use code written by Codepilot without understanding it?

And many more.

# Conclusion

In my opinion, I do not think any AI application will replace developers soon. I rather see these applications as an extra tool that helps us write code quicker. I see them as time-saving tools.

I am curious to see what do you think? Feel free to leave your thoughts in the comments below!

> I will create some videos/live streams about GitHub Copilot. Make sure you are subscribed to my YouTube channel. [Subscribe here](https://catalins.tech/youtube).

