## How To Disable Comments On Hashnode

The Hashnode platform gave bloggers the ability to make custom CSS settings. As a result, we can customize the look of our blog, but we can also disable elements.

You might, or might not prefer to have comments enabled on your blog. There are many reasons why you might choose to have them or not. But if you would rather not have them, then in this article you learn how to do it.

Therefore, let us see how we can do it. 

# 1. Inspect the element
The first step is to inspect the element for the comments. To do so, right-click anywhere in the comments. For example, you can right-click on an individual comment. Figure 1 illustrates that.

> ![Screenshot 2020-10-05 at 10.03.09.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1601882204038/mYH3GJsGt.png)
Figure 1

P.S: The image might look confusing because I cropped the commenter's details. 

# 2. Find the element class
The next step is to find the class for the comments that start with `blog-`, and finishes with `-wrapper`. The reason is that the classes beginning with `.blog-*` are unique and represent only one element. Also, the `-wrapper` class means that the element wraps all the other elements related to the comments. 

Figure 2 illustrates the wrapper class for the comments. You can see that the wrapper element contains other elements. Thus, that is where its name comes from; because it wraps all other elements.

> ![Screenshot 2020-10-05 at 10.04.00.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1601882234913/Rd20qJTV4.png)
Figure 2

If you cannot see it in the image properly, the wrapper class is `blog-comments-section-wrap`. In the third step, we are going to write custom CSS that hides the class. 

# 3. Write the custom CSS
Now that we know what element we need to hide, we have to add some custom CSS settings. In CSS, we have a useful property called `display` that allows us to specify the display behaviour. 

> ![Screenshot 2020-10-05 at 10.07.12.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1601882250809/0520mR5yz.png)
Figure 3

Now go to your blog dashboard > Appearance > Add Custom CSS > Articles. Once you are there, add the following CSS snippet to the editor:

```css
.blog-comments-section-wrapper {
    display: none;
}
```

Click the button saying "Save Styles", and then press the "Publish" button. After doing so, your articles no longer have a comment section. Well done!

# 4. No more comments
At this point, you should not see the comment section on your blog anymore. If you followed all the steps, your blog should look like figure 4.

> ![Screenshot 2020-10-05 at 10.04.41.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1601882171756/R2LCIK27U.png)
Figure 4

If you want to enable the comment section in the future, you have to remove the custom CSS settings from the third step.

# Conclusion
In the future, there might be other ways to do it as well. However, for now, using `display: none` is the only way to disable comments.

> By the way, I have a YouTube channel now. If you enjoy my articles, you are most likely going to enjoy my videos too. [Check my channel here](https://www.youtube.com/c/catalinpit?sub_confirmation=1)!