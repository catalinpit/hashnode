# AWS Virtual Private Cloud (VPC) - Let's Learn About It

AWS Virtual Private Cloud (VPC) is another essential AWS service. Also, it is something you need to know if you want to pursue the certifications. 

When we build a cloud infrastructure, we want control over the security, of the traffic between our services and much more. In simpler words, AWS VPC provides us with more control over our network. 

##  AWS Virtual Private Cloud use cases

There are a few use cases for having your private networking environment. Some of the are:

* **Hosting websites** => You can host a basic web application (e.g. a blog) in your virtual private cloud. The benefits of doing so are that you get additional layers of privacy and security.
* **Extend your network into the cloud** => You can move your IT resources into the cloud seamlessly. That is, you do not have to change how the users access your applications. Connect your VPC to your network.
* **Multi-tier web applications** => Improve the security of your web application by enforcing restrictions between the different parts of your application. In simple words, that means to provide internet access to your web servers, while restricting public access to your database.

However, there are other use cases such as disaster recovery, connecting cloud applications to your datacenter, and so on.

## What is AWS Virtual Private Cloud

AWS Virtual Private Cloud allows us to define our virtual private network, which we can isolate from all the other networks on AWS. However, let us also have a look at the official AWS definition. AWS VPC allows you to "provision a logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define".

You might ask "why would I create my private cloud?". The reason for creating your private cloud is to have full control of your virtual networking environment. Having your private network, you can control the IP address range, create your subnets, configure the route tables and network gateways.

## AWS Networking Core Components

A bit of networking knowledge would help us a lot with AWS. However, we can learn along while learning about AWS. There are a handful of components and services that makes up your virtual private cloud. Those are:

* Route tables
* Internet Gateways
* NAT (Network Address Translation)
* Security Groups
* VPC peering
* DNS
* Elastic IP Addresses
* ClassicLink (deprecated service - it allows us to connect EC2-Classic instances privately to a VPC)
* Public subnets
* Private subnets

I know the above list looks a bit daunting, but do not worry. We take it one by one, and the concepts are going to make sense.

## Default AWS VPC

By default, your account has a default virtual private cloud in each of the AWS regions. That means, you do not have to create a new one from scratch, and you can immediately deploy EC2 instances in your default VPC. Moreover, you can use other services such as Elastic Load Balancing and Amazon RDS in the default VPC.

Therefore, should you use a default VPC or a custom VPC? It depends on your needs. If you want to launch a blog or a simple website, you can make use of the default virtual private network. If you want a more complex cloud architecture, with specific requirements, you can create your custom AWS virtual private cloud.

However, how do you know if a default VPC is enough? Where can you see what it consists of? Amazon AWS configures the following for your default VPN:

* The size of the IPv4 CIDR block is `/16`, which means it provides up to 65,536 IPv4 addresses.
* It creates a default subnet in each Availability Zone of size `/20`, which means it provides up to 4,096 addresses per subnet (AWS reserves some of them for their use).
* Creates a default network access control list (ACL).
* Creates an internet gateway and it connects it to the default VPC. The reason for doing so is to allow your instances to access the internet.
* It creates a default security group.
* It associates the default DHCP options set for your AWS account with the default VPC.

Note that it automatically associates the security group and network ACL with the default VPC. Also, when you create a VPC, it automatically has a main route table.

#### 0.0.0.0/0

0.0.0.0/0 represents all the possible IP addresses, which means we are allowing access from anywhere on the internet.

When you specify 0.0.0.0/0 in the Internet Gateway, you allow internet access. Besides, if we define 0.0.0.0/0 in the security groups inbound rules, we grant public internet access to our resources.

However, I want to thank [Andrew Brown](https://www.youtube.com/watch?v=Ia-UEYYR44s&amp;t=127s) for this piece of information!

## Let's create a VPC
The first step is to log into AWS and go to the VPC service. Once you are there, click on the option saying `Your VPCs`, as shown in figure 1. We are not using the wizard because the point of the article is to learn how to create a VPC manually. 

> ![Screenshot 2020-08-28 at 11.35.35.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1598603751951/XyJRmIn5r.png)
Figure 1

Afterwards, you are taken to another page where you can see all your VPC. You might have no VPC available, or the default one. However, click on the button saying `Create VPC`.

> ![Screenshot 2020-08-28 at 11.36.39.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1598603835165/sns45H_Tx.png)
Figure 2

Once you click the button, you are going to see another webpage where you have to fill some information. Once you are here, you need to choose a name for your VPC (e.g. `CatalinsVPC`), an IPv4 CIDR Block, and the Tenancy. The `tenancy` is about how we launch EC2 instances within the VPC, and it has two values: 
* **Default** => It means shared hardware (e.g. used by multiple people).
* **Dedicated** => Hardware only used by yourself.

> ![Screenshot 2020-08-28 at 11.38.49.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1598603970030/jLgRhSeEk.png)
Figure 3

After you fill all the information, click the `Create` button, and your VPC will be created. The newly created VPC comes with a main route table and a main network ACL. Therefore, you have a new VPC. Well done!

## VPC Peering

> ![AWS VPC Peering (Source: AWS DOCS)](https://docs.aws.amazon.com/vpc/latest/peering/images/peering-intro-diagram.png)
Figure 4

If you wonder how can you connect two AWS Virtual Private Clouds, the answer is VPC peering. With VPC peering, we can connect two Virtual Private Clouds over a direct network route. It routes the traffic between them by using private IP addresses such as IPv4 or IPv6.

Moreover, you can connect VPCs from different AWS accounts or regions, and the instances communicate like they are in the same network. If the VPCs are in different regions, the connection is called inter-region VPC peering connection.

For instance, you could think of two AWS Virtual Private Clouds as two cities. Thus, the VPC peering acts as a road connecting these two cities.

> ![AWS VPC Peering Creation (Source: AWS docs)](https://media.amazonwebservices.com/blog/2018/ivpc_create_2.png)
Figure 5

Figure 5 shows how to create a peering between two Virtual Private Clouds.

To sum up, VPC peering allows you to connect two private clouds irrespective of the accounts and regions they are in. One important thing to note is that there is no transitive peering. That means the peering must take place directly between two VPCs. For example, we cannot go from VPC A to VPC C through VPC B. VPC A and VPC C needs to have a direct connection between them.

### Route Tables

Route tables allow you to determine where to direct your network traffic. In other words, route tables are just lists of IP ranges (CIDR blocks) that the traffic can come from or leave from.

Route Tables also have Subnet associations, which means that each subnet in our AWS VPC must be associated with a route table. You can only associate one subnet with one route table at the time, but you can associate multiple subnets with the same route table. In other words, the route table determines the traffic that can enter and leave the associated subnet.

For more information on this subject, check the <a href="https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html">AWS documentation</a>. They have more information than we need at the moment, but it is always good to go in-depth and understand a concept properly.

## Internet Gateway

The name of this concept is, more or less, describing its purpose. Internet Gateway allows your VPC to communicate with the internet. It is important to note that if your VPC does not have an Internet Gateway, it cannot communicate with the internet. You can attach one VPC to only one Internet Gateway, and vice-versa. 

Let us now talk about the two purposes of this service:

* it provides a target in your Virtual Private Cloud route tables for internet-routable traffic
* it does network address translation for instances with public IPv4 addresses

To make a subnet public, associate it with a route table and connect it to an IGW. If you only have a subnet associated with a route table, but not connected to an IG, then your subnet is private.

Therefore, Internet Gateway allows communication between a VPC and the internet.

## AWS Direct Connect

For different reasons, some companies use a hybrid cloud. That means they are using AWS as a cloud provider, but they also have their on-premise services. Then, the question becomes, how do we connect the on-premise services to AWS?

They are connected through an Ethernet cable, which in turn, connects the company's router and the AWS Direct Connect Router. Doing so, you create a virtual interface, bypassing the internet service provider, and you can access public AWS services such as S3 or VPC.

There are two types of connections:
* **Dedicated** => It is a physical ethernet port dedicated to a customer. It has a capacity of 1 Gbps and 10 Gbps.
* **Hosted** => You can add or remove capacity on-demand, and the capacities are: 50 Mbps, 500 Mbps, 10 Gbps.

Let us now look at the main components of AWS Direct Connect:

* **Connections** => It creates a network connection between on-premises services and an AWS region. You need to create a connection in an AWS Direct Connect location.
* **Virtual Interfaces** => It creates a virtual interface, which allows your on-premise services to access AWS public services such as S3, for instance.

> ![Screenshot 2020-08-28 at 10.14.48.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1598598921183/AEd1beMft.png)
Figure 6

Figure 6 shows the web page when you create a connection. You have to choose a name, a location (e.g. London), a port speed (1Gbps or 10Gbps), and the service provider. Alternatively, you can use the `Connection Wizard`, where you can choose between `Maximum Resiliency`, `High Resiliency`, or `Development and Test`. Choosing any of the three options will configure the connection automatically for you.

This service is excellent for high-traffic networks because it increases the bandwidth throughput and helps reduce network costs. Also, it is perfect for a hybrid environment where you want to connect a data centre directly to the AWS, without using the public internet.

## AWS VPC Endpoints

AWS Virtual Private Cloud Endpoints gives you the possibility to connect your VPC to various AWS services and other VPC endpoint services. Everything is done in a private network - Amazon network. As a result, there is no need for an internet gateway, VPN Connection, AWS Direct Connect connection and other services.

There are two types of VPC endpoints:

* **Interface endpoints** => This type of endpoints use AWS PrivateLink, which enables you to access different services privately by using private IP addresses. When you use an interface endpoint for a supported service, this is the entry point for the traffic trying to access that specific service.
* **Gateway endpoints** => You specify these gateways in your route table as a target for a route. In simple words, you specify what AWS services the instances from a specific subnet can access. For example, the instances in subnet four can access S3 and DynamoDB through a particular gateway endpoint. The only two services that it supports are Amazon AWS S3 and DynamoDB. You can create a gateway endpoint by specifying a VPC where the endpoint resides, and the service to which you want to create the connection.

These VPC endpoints allow instances from a VPC to communicate with various AWS services without adding bandwidth constraints and availability risks on your network traffic.

## Bastion Hosts
In AWS, we can use Bastion Hosts to access instances on a private network. How is that possible? The Bastions are in a public subnet, which is connected to the other private subnets from your account. How do we protect the Bastions? We enforce strict security groups, to make sure only specific IPs can log into the instances. 

For instance, we can ssh (log into) our Bastion Host, and from there we can access other private instances. The other private instances are not accessible from outside, other than through the Bastions. 

## VPC Flow Logs
Like with any other service, we have logs to capture various information which we might inspect later. You can use this service with CloudWatch or S3 to store your logs, in case you need them to analyse them.

What this service does is to allow you to record information about the network traffic to and from your VPC. For instance, you can monitor the traffic that reaches your instances. You can create flow logs for your VPC, Subnet or Network Interface. Thus, let us see the format of a flow log:

`<version> <account-id> <interface-id> <srcaddr> <dstaddr> <srcport> <dstport> <protocol> <packets> <bytes> <start> <end> <action> <log-status>`

* `version` represents the VPC Flow Logs version. By default, it is 2.
* `account-id` is the account's id of the owner. For instance, the account-id can be my account id.
* `interface-it` represents the ID of the interface for which the traffic is recorded.
* `srcaddr` stands for "source address", and `dstaddr` stands for "destination address". They help us identify problematic IPs.
* `srcport` is the an abbreviation for "source port", and `dstport` stands for "destination port". They help us identify the problematic ports.
* `action` tells us whether the security groups and network ACLs accept or not the traffic.

The above fields are the important ones. However, for a description of all the fields, feel free to read the [VPC Flow Logs documentation](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html).

#### How to create a VPC Flow Log
The first step is to go to your VPC, right-click on the specific VPC, and click on "Create flow log". Figure 7 shows how the web page should look like when you access all your VPCs.

> ![Screenshot 2020-08-27 at 11.43.49.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1598518931434/XqQqTNO-o.png)
Figure 7

Once you click on "Create flog log", you are taken on the screen from figure 8. The `Filter` option allows us to select the traffic we want to log - accepted, rejected or all traffic. Going further, `Maximum aggregation interval` gives us the option to choose the interval of time when to capture the packet, and store them. Afterwards, we can select the `Destination` where to store the logs. You can store them in CloudWacth, or S3. In this example (figure 8), I chose to keep them in an S3 bucket. Lastly, in `S3 bucket ARN*` we need to add the name of the bucket, which in this example is `arn:aws:s3:::catalins-bucket`. 

After that, the logs are available in the specified bucket.

> ![Screenshot 2020-08-27 at 12.07.30.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1598519277516/McR9xgEeP.png)
Figure 8

When it comes to the "Log record format", we. can use the "AWS default format" or a "Custom format". In figure 8, you can see that it is using the "AWS default format" because it did not make sense to change it. Of course, there are cases when you might need a custom format. Thus, feel free to use it if you have to.

If you create a flow log, and then you add more instances in your subnet, it creates a log file object for each network interface. It is important to note that collecting log data does not affect your network throughput. It collects the data outside your network traffic.

## AWS PrivateLink
AWS PivateLink allows us to connect our AWS services without exposing them to the public internet. In simpler words, all the traffic happens within the AWS network.

It does not require VPC peering, an Internet Gateway, NAT, or route tables. However, it requires an NLB (network load balancer) and an ENI (Elastic Network Interface). 

Therefore, AWS PrivateLink allows you to secure your traffic by keeping it within the AWS network. It also helps you to simplify the network management, because you do not have to deal with firewall rules, path definitions, or route tables. Lastly, it accelerates the migration of on-premise applications to AWS.

## Conclusion

In this article you learnt about:
* AWS Virtual Private Cloud use cases
* What is AWS Virtual Private Cloud
* AWS Networking Core Components
* Default AWS VPC
* VPC Peering
* Route Tables
* Internet Gateway
* AWS Direct Connect
* Bastion Hosts
* AWS VPC Endpoints
* VPC Flow Logs
* AWS PrivateLink

This article has a lot of information, so make sure you take your time to understand it. In the future, I plan to create labs on YouTube for each AWS article to make it easier to understand and use the concepts. 
 
> Learn AWS from scratch and become a cloud engineer with the [AWS Certified Cloud Practitioner course](https://academy.zerotomastery.io/a/aff_1f8vmvjz/external?affcode=441520_zj_tadya).