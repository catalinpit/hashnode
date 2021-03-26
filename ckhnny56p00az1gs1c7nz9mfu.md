## How To Integrate Mailerlite Newsletter With Hashnode

Hashnode has a built-in newsletter service, which does the job well and saves you money/time. However, you might want to use a custom one. In my case, I use Mailerlite for a while, and I am happy with it.

Therefore, I want to show you how you can integrate Mailerlite with Hashnode. That is, how can you embed your sign-up form into your blog.

# Getting the embed code from Mailerlite
I want to mention that I am not showing how to create a sign-up form. The purpose of this article is only to show how to integrate an existing one with Hashnode.

The **first step** is to log into your Mailerlite account, and go to the **Forms** tab. Once you are on the page with all the forms, click on the **Embedded forms** options. This is the category of the form we are going to use.

Lastly, click on the **Get embed code** button for the form you want to use.

> ![sdgsdg.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605023390726/CJSNfvbUn.png)
Figure 1 

Figure 1 illustrates all the steps explained above.

After that, you'll be taken to another page. On the new page, you have to scroll until to the bottom, where you should see a section "**Embed form into your website**".

The last thing you have to do in the MailerLite application is to copy all the code from the "**HTML Code**" tab.

> ![Screenshot 2020-11-10 at 17.38.58.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605622990332/lhZV1Q-xA.png)
Figure 2

Figure 2 illustrates what you should see on your page. The code has been cut from the image.

# Create the widget in Hashnode
The last step you have to do is to create and use the widget on Hashnode. Go to your blog dashboard, and then click on the "**Widgets**" tab. Once you are there, click on the button saying "**Add new Widget**". 

Figure 3 illustrates what you should see in your blog dashboard.

> ![Screenshot 2020-11-17 at 16.33.44.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605718370321/8aw4ee0mD.png)
Figure 3

After clicking on the "**Add new Widget**" button, you are taken to another page. On this page, you need to add the code you copied from the Mailerlite dashboard. Your code should replace the text *<your_code>* from figure 4 below.

Now that you added the code, you need to name your widget. In figure 4, you can see a dummy name I chose for my widget - *newsletter_mailerlite*. However, you can name it as you please, as long as there is not another widget with the same name.

Click on the button saying "*Create*", and you are ready to use your widget.

> ![Screenshot 2020-11-17 at 16.34.16.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605718475897/M2IGqz0rq.png)
Figure 4

# How to use the widget on your blog
Figure 5 illustrates how you can use the widget on your blog. Add the name of your widget between the square brackets.

**Mention**: The `<hr/>` tag is not necessary.

> ![Screenshot 2020-11-17 at 16.34.37.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605718927510/mtFcnekXx.png)
Figure 5

At the time of writing the article, you can use widgets in your articles and pages. However, this might be subject to change.

# Conclusion
The article taught you how to integrate Mailerlite with Hashnode. Except for the part with the Mailerlite, you would use the same steps to integrate other providers and services.

To recap:
1. Log into your Mailerlite account.
2. Go to the "**Forms**" tab.
3. Click on the "**Embedded forms**".
4. Choose the form you want to embed.
5. Click on "**Get embed code**".
6. Scroll to the bottom of the page, and click on "**HTML code**".
7. Go to your blog dashboard.
8. Click on "**Widgets**".
9. Click on the button saying "**Add new Widget**".
10. Paste your code.
11. Name your widget.
12. Save your widget.
13. Start using it.