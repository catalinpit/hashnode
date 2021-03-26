## How To Setup A Budget On AWS

Unfortunately, it is very easy to over-spend money in AWS, and you do not want that. Your costs can quickly spiral to thousands of dollars. 

Therefore, the first step I advise people to do after creating an AWS account is to set up a budget. By setting up a budget, you make sure you are not over-spending money. 

As a result, in this article, I am going to show you how to set a budget on AWS.

# Login to your account
The first step is to log into your account. Once you are logged in, click on your name and a list should appear. Figure 1 illustrates an example from my account.

> ![AWS Account List](https://dev-to-uploads.s3.amazonaws.com/i/a1nenvv5lthdhsi69io2.png)
*Figure 1*

Once you can see the list, click on `My Billing Dashboard`, which takes you to another page.

# Billing & Cost Management Page
At this point, you should be on the Billing & Cost Management page. Figure 2 illustrates the top of the page. The image is cropped to show only the important information. 

> ![Billing & Cost Management Page](https://dev-to-uploads.s3.amazonaws.com/i/h8uxhh654rvt4hrqzdbf.png)
*Figure 2*

On the left side of the page, you should see an option called `Budgets`. Click on that option, and you will be taken to a new page again. 

The new page is called `AWS Budgets` and you should see a blue button on the right-hand side saying "Create budget". Click the button to create a new budget. 

# Create a budget
After you click the "Create budget" button, you are prompted to choose between different types of budgets. You can see the different types of budgets in figure 3.

> ![Types of budgets](https://dev-to-uploads.s3.amazonaws.com/i/jtz1vpe2cbb6f3kr9mi4.png)
*Figure 3*

For this article, we are creating a `cost budget`, because we want to stay under a specific sum and receive alerts when particular thresholds are met. Therefore, select the first option, and click the button saying "Set your budget".

#### Set up the budget
After you click the button, you are taken to another web page where you can set the:

* name of your budget
* period (e.g. monthly, quarterly)
* budget effective dates (recurring or expiring)
* start month
* budget amount

> ![Setup your budget](https://dev-to-uploads.s3.amazonaws.com/i/38yrg1gjmzh5ab3hbkvq.png)
*Figure 4*

Figure 4 illustrates an example from my account. I want to make sure I do not spend more than ten dollars. You are free to use any sum, though. If you do not want to pay anything, add 0.01 dollars. You cannot add a zero, so we use the lowest amount, which is 0.01.

#### Configure the alerts
Once you filled all the fields, click on the button saying "Configure alerts". You are going to see a new page, like in Figure 5. 


> ![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/sr4j0mpeicchonacak9g.png)
*Figure 5*

You can choose to receive alerts based on actual costs or forecasted costs. For this article, I left the alerts for the actual costs. 

Also, you can choose an alert threshold, so you get an email when the threshold is met. In this case, I decided the alert threshold to be one hundred. As a result, I will get an email when my costs are higher than ten dollars. 

The last steps are to enter an email address where you get the budget alerts and to confirm your budget. Once you do that, you have a budget set up. 

# Conclusion
Congratulations! You just set up a budget alarm for your account. It is essential to create one, so you do not end up over-spending money. 

Feel free to change the settings to fit your needs and budget. If you want a smaller/bigger budget, adjust it accordingly. However, if you plan on getting familiar with AWS, I would follow the examples from this article.

If you followed all the steps from the article, your "budgets" page should look like the one in figure 6.

> ![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/lkdmbl8jnekukqcwindm.png)
Figure 6