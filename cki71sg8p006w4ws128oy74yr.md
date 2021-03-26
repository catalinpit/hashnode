## AWS CloudWatch vs AWS CloudTrail - What Is The Difference?

%%[mailerlite]

<hr/>

It can be very easy to confuse the two services; especially when you are under pressure in the certification exams.

The aim of the article is therefore to eliminate the confusion between the two services. After reading the article, it should be clear what each service does and what is the difference between them. 

Without further ado, let's jump straight in!

# AWS CloudWatch
AWS CloudWatch is a monitoring service. That means it allows you to monitor the performance of your AWS resources and applications.

**Where would you use AWS CloudWatch?**
* **To analyze logs** - CloudWatch is useful in exploring and analyzing logs. Why would you do that? By analyzing your logs, you might find issues which can be addressed to improve the performance of your applications. Besides that, when a resource/application fails, you can determine what happened and why by looking at the logs.
* **To monitor your applications** - For instance, you could monitor EC2 metrics such as CPU utilization, memory used, status check, network throughput and more. It gives you insights about your application so you can act accordingly. One example would be adding another EC2 instance if the previous one is at maximum capacity.
* **To optimize your resources** - With CloudWatch, you can specify what happens when a specific threshold is met or not. For example, terminate an EC2 instance if a condition is met. Or create additional instances to support more traffic.

Moreover, AWS CloudWatch is made up of multiple monitoring tools such as:
* **Events** - You can trigger an action based on an event. For instance, we could create an event that sends an email to the administrator when a resource fails. You specify how and when to trigger an action. Then you define what action to trigger. Thus, CloudWatch events are very useful.
* **Alarms** - With alarms, you need to define a threshold, a condition, and what to trigger. The most popular scenario is an alarm for billing. That is, trigger an alarm if the estimated charges are greater than the threshold set.
* **Logs** - CloudWatch logs allows you to store the log files for various sources such as EC2 instances, CloudTrail and many more. You can then use these logs to detect issues, find leaks, patterns and so on.

Finally, AWS CloudWatch is an excellent service which you can use to monitor the performance and metrics of your resources an applications that run in AWS. It helps you to improve and scale your applications. It also enables you to stay within a budget, and thus not having unwanted costs. Consider CloudWatch as a person that watches your applications to make sure they work correctly, and at the best prices.

# AWS CloudTrail
Consider AWS CloudTrail as a detective that watches over your AWS account and environment. It shows you:
* what action was taken
* who did it
* when the action was taken
* where the action was taken

For instance, let's say your S3 bucket was deleted by mistake. You can use AWS CloudTrail to see who deleted the bucket, when, and where (e.g. API Call or from the AWS Management console).

Thus, the primary use case for AWS CloudTrail is to monitor the activity in your AWS environment. Additionally, CloudTrail is compliance support due to providing a history of activity in your AWS environment. That means it is easier to ensure compliance with regulatory standards and internal policies.

# The difference between CloudWatch and CloudTrail
AWS CloudWatch monitors your AWS resources and applications, whereas CloudTrail monitors the activity in your AWS environment. For instance, with CloudWatch, you can scale your applications, whereas, with CloudTrail, you can see who did what to your applications.

They are not mutually exclusive, and you can set CloudTrail to send events to a CloudWatch log, for instance.

Finally, remember:
* CloudWatch **monitors performance**, whereas CloudTrail **monitors actions** in your AWS environment.
* One (CloudWatch) focuses on performance, whereas the other (CloudTrail) focuses on auditing.

# Conclusion
The two services, CloudWatch and CloudTrail, can be used together. After this article, it should be clearer what is the difference between them. Also, you should know when to use one over the other.

# Sources
* FreecodeCamp's AWS Certified Solutions Architect - Associate 2020
* ACloudGuru AWS Certified Solutions Architect Associate
* AWS Documentation
