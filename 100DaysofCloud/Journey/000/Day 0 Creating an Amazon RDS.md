![SQL Server DB Diagram](https://raw.githubusercontent.com/RightHandCloud77/AWS-Cloud-Journey/2ba2a20fad368a985896d5d33105f159ef798d73/Notes/Architecture%20Diagrams/%23DBS03-AWS100.png)

Create DB Instance (MS SQL Server)

## Introduction

I chose to do this project today after studying & going over some RDS Practice Questions for the Cloud Practitioner Course. I created a similar database on the CloudQuest Game using MariaDB engine. So I figured I'd start Day 0 Here! 🚀

## Prerequisite

Amazon RDS: is a service that lets you run relational databases in the cloud 📊

## Use Case

![Simplified PrizePicks Cloud Model](https://raw.githubusercontent.com/RightHandCloud77/AWS-Cloud-Journey/2ba2a20fad368a985896d5d33105f159ef798d73/Notes/Architecture%20Diagrams/%23DBS03-AWS100.png)

- I want most of my examples on this 100 day journey to be sport based... There aren't too many guys breaking this stuff down to where sport lovers like myself can understand!

- With the uproar in sports betting in the past couple years, I'm going to use PrizePicks as an example. PrizePicks obviously maintains a boatload of sports data (stats, game scores, team performance). This data changes by the second each day. The PrizePicks app needs a reliable and scalable database solution to store and manage the large volume of game data generated during the sporting event 🏀🏈⚾⚽🏆

## Cloud Research

- Justin Baker gives a great perspective on Adding Real-Time Data into applications. He also gives specific companies that thrive in "real-time" services. Going up the technology ladder in the PrizePicks reference, the stats are disseminated from servers that are designed to seamlessly distribute data to bettors end devices. Go up one or two more rungs and I'm sure you'll find a Relational Database thats storing this game data daily. Link below (about a 5 min read) 🧠

https://hackernoon.com/adding-realtime-data-streaming-to-your-app-b9b6ec034afd

## Trial and Error

- After getting my cloud RDS provisioned, I thought I would be able to connect to it using the endpoint address located in the connectivity & security tab. I had to navigate https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToMicrosoftSQLServerInstance.html to determine how to establish a database connection using the credentials that I assigned while creating the DB. Maybe there is a way to access via a webportal but as of now my steps are in the "☁️ Cloud Outcome" section below.

- After about an hour of  trying to connect using the SSMS (SQL Server Management Studio) and looking over the subnets. I verified that I had the proper gateway set up to allow incoming traffic, and still couldn't connect.🤔 

![This is the error that I kept getting](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%2016.png?raw=true)

- After about another 15 mins of shooting and missing, I decided to check the security groups. And realized my public IP wasn't added on the list to allow traffic into the private subnet that housed the DB, only "all traffic from within the VPC (Virtual Private Cloud)💡

## Tutorial

- Here is my version of setting up a basic RDS via AWS. Initially, I did not configure any settings (monitoring, backups, scaling) outside of the default except for allowing the RDS to have an endpoint connection to be able to connect from my desktop.

### Step 1 — Log in to your AWS account & navigate to the search bar & find "RDS" It may be in your recent tab on the home screen dashboard.

![Step 1](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%201.png?raw=true)

### Step 2 — Get started by clicking Create Database

![Step 2](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%202.png?raw=true)

### Step 3 — Choose "Standard create", easy create may be used for other projects that require a quick setup after becoming familiar with RDS and what you may need to change.

![Step 3](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%203.png?raw=true)

### Step 4 - Choose the database engine that meets the needs of you or your client. This project required Mircrosoft SQL Server.

![Step 4](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%204.png?raw=true)

#### Each Engine will show a quick description and how they correlate with AWS.

![DB Engine Description](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%204%20Explanation.png?raw=true) 

### Step 5 - Choose your template.

![Step 5](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%205.png?raw=true) 

### Step 6 - Type a name for your database instance.

![Step 6](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%206.png?raw=true)

### Step 7 - Give the instance login credentials. (WRITE THEM DOWN!)

![Step 7](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%207.png?raw=true)

### Step 8 - Choose a DB instance. (This is where you choose the size and power of the DB)

![Step 8](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%208.png?raw=true)

### Step 9 - Configure the storage for your DB. (For Future Reference: As you scale vertically/horizontally the instance will remain available as the process finishes)

![Step 9](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%209.png?raw=true)

### Step 10 - If you want to connect to your RDS from outside the cloud, enable Public access

![Step 10](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%2010.png?raw=true)

### Step 11 - Finally, create your database.

![Step 11](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%2011.png?raw=true)

### Step 12 - It takes about 15-20 minutes for your database to become available. Be patient! Go sweat some of your parlays or something 🤑

![Step 12](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%2012.png?raw=true)

### Step 13 - Open the connectivity & Security tab after clicking on your database. Review under Publically accessible, ensure it says "Yes" Then navigate to the VPC Security Groups.

![Step 13](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%2013.png?raw=true)

### Step 14 - Navigate to "Inbound Rules" and Add Rule. Enable All Traffic under "Type" and My IP under "Source" it will  automatically populate your public IP given by your ISP. Save Changes.

![Step 14](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Untitled%20design.png?raw=true)

### Step 15 - Download Engine based SQL Management Server, for this project I used SQL Server Management studio by Microsoft being this is a Microsoft SQL Server. Here is the link: https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms

### Step 16 - Copy the endpoint address located on your DB instance dashboard from earlier. Choose Server Type. Paste that address into the Server name:

![Step 16](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%2013.png?raw=true)

![Step 16a](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/Step%2015.png?raw=true)

#### Copy your admin credentials that you created and wrote down when provisioning the database.

### Step 17 - If your credentials were correct, you should be granted access to the database.

![Step 17](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23DBS-AWS100/GOT%20IN%20DB!.png?raw=true)

## ☁️ Cloud Outcome

- Prizepicks is obviously run on a more sophisticated cloud model than this (Example of a sports betting app cloud below). However, at a simplified core, their data is used to make odds, show bettors previous game statistics, and send out "deals" to end users via a powerful EC2 Instance. With that being said, the data(stats) have to be stored in a relational database that can be housed in a way that relates to other pieces of data, that provides high availability as well as low latency. Which goes back to Justin Baker's article about data streaming 📲

### In the intimidating diagram below, focus on #3 and #7. For the sake of your sanity & mine, we'll keep it at those two for now 😂

# 3: Amazon Managed Streaming for Apache Kafka is used to build real-time streaming data pipelines between services, applications, and data layers.

# 7: The Amazon RDS (Similar to what I set up in this project) stores platform data and historical transactions while providing resiliency, redundancy, & quick failover.

![Sports Betting Cloud Model from AWS](https://docs.aws.amazon.com/images/architecture-diagrams/latest/sports-betting-architecture/images/2-deployment-of-player-related-components-outside-of-aws.png)

- Configuring an RDS Instance to pair with an EC2 was my first official project done outside of Amazon CloudQuest. Without any guide to immediately tell me where I went wrong definitely prolonged the process on the backend, but thats where I was able to learn about some of the default security group settings of the Database. Specifically, if you don't "allow" the public address to connect to the DB instance from outside of the VPC, it won't connect!



## Next Steps

- This project gave me a couple ideas for my next stage. 

- Keeping it down to the basics to prevent from getting ahead of myself, I want to explore setting up a scalable EC2 instance from scratch that has a couple different functionalities. Maybe look into the cloud structure of some of these sport analytics, or betting apps 👨🏾‍🔧

- Or exploring into a security project (Due to getting caught up on the "Security Group" portion of this project), maybe setting up a secure cloud to hold some of the said instances above with multiple security practices inside 🔒
