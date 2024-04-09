![Amazon EC2](https://qph.cf2.quoracdn.net/main-qimg-845942cf034f83d1949b61ba59794e8a)

![Intro Diagram](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Architecture%20Diagrams/COM03-AWS100.png?raw=true)

# Beyond the Stadium: The Cloud's Influence on the Future of Sports

## Introduction

Building upon insights gained from my previous project documented on GitHub (https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/100DaysofCloud/Journey/000/Day%200%20Creating%20an%20Amazon%20RDS.md), where I outlined the "Next Steps," In this article, we explore the impact of cloud computing on the future of sports, focusing on the role of Amazon EC2 instances in powering sports data analytics websites and applications.

## Prerequisite 👣

Alright, so think of EC2 as that all-around teammate who's always got your back on the field or court. Great players adapt their game depending on the situation. EC2 instances adjust their performance and capabilities to meet the demand, whether it's the 4th Quarter of the Super Bowl or a small training session. 🏁

EC2 is like that versatile player who can handle different positions and playstyles. On the subject of this project, EC2 keeps our sports apps and websites running smoothly, no matter how intense things get. The ultimate point guard or quarterback, communicating with the team, bench, coaches & fans all at the same time! 🌟

[What is an EC2 Instance?](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)

## Use Case 🌎 

A basic example of ESPN.com "Accelerated Computing" EC2. This is one of the 4 types of EC2 Instances, designed with hardware accelerators/co-processors to perform functions more efficiently than is possible in software on normal computers. Ideal for graphics apps, game streaming, and app streaming.

![Diagram](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Architecture%20Diagrams/COM03-AWS100.png?raw=true)

If we're looking at this diagram from the inside out. You have the EC2 running the webserver of ESPN.com putting out tons of information to sports fans around the world. Stats, live streams, on-demand video all touch this instance in some way or fashion via the many other instances that AWS has to offer 🛜 We are able to access this data from the internet by going through the internet gateway that's setup on the VPC into the public subnet. ESPN is currently managed and updated by it's developers constantly remoting in from the backend terminals via SSH 🖥️

## Cloud Research 📖

- Initially, I found the diagram I created to be too simplistic to capture the power and efficiency required for such a task. I thought a couple years back to watching Steph Curry shoot a 3 on a Wednesday night ESPN feature realizing they added a feature where the 3PT Line glows whenever a player attempts a three. After understanding a bit more about EC2, I started researching how in the world is this possible during a live stream. 

- I came across almost the perfect example from an AWS promotional e-book, but the short, seller based infograph provided me the simplicity I needed to understand the concept perfectly. Although it used the NFL's Next-Gen Stats model (powered by AWS), I understood it took along a similar format.

![Next Gen Stats](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/Open%20How+AWS+is+changing+the+game.jpg?raw=true)

Notice how the EC2 is at the nucleus of the is model, similar to the architecture diagram at in the introduction. The EC2 is created to both recieve and transmit data to be manipulated at lightning speeds. From the time a shot goes up or a QB cocks back to launch a bomb down field, the EC2 is able to receive data at about a half-second, and the same time it took to receive, it sends out to other instances (The machine learning instance 🧠) that work their magic and provide on screen graphics (The 3 point line glowing after a shot is taken) to viewers. 
 
 - This also translates to the video production teams. As they had their first [cloud-based live game](https://www.sportsvideo.org/2023/01/24/espn-dmed-pull-off-first-end-to-end-cloud-based-live-production-in-u-s-with-a-10-college-hoops-game/) production in Jan 2023, involving feeds from onsite cameras and microphones, video switching, slow motion replay, and on screen graphics. Imagine the guys working for ESPN running an entire broadcast of the NBA Finals from home! 😶‍🌫️


## Trial and Error

- I didn't have many issues provisioning the EC2 and being able to reach it from the web. Although, I did run into some trouble configuring the site via the putty SSH connection. The goal of the project was to start a Linux based webserver on and EC2 instance and remote in via SSH from my home network and change the site around, as the ESPN developers would when they need to update something. This involved putty commands to configure the Linux webserver that I simply did not know. As these were speed bumps in the project, these were a google search away, the links to all my "how to" guides are under my struggles: 

![Putty Problems](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/Trial%20and%20Error/Screenshot%202024-04-05%20220952.png?raw=true)

This is me finally using my private key to SSH into the backend of the EC2, all to be staring at this screen for 5 mins figuring out what to do next.

[How to SSH into EC2 from Windows](https://stackoverflow.com/questions/5264945/ssh-to-ec2-linux-instance-from-windows)

After my brain fart, I realized it was time to get in my "devops" mode and install the webserver on the Instance.

![websever](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/Trial%20and%20Error/Screenshot%202024-04-05%20221119.png?raw=true)

[How to install Apache Webserver on linux-based EC2](https://httpd.apache.org/docs/2.4/install.html)

Once I got the server installed successfully, it was time to change the site around to my liking. The project required changing of the websites interface, which is found in the "index" section of website codes. Youtube University came through here 📺

![Finding Index](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/Trial%20and%20Error/Screenshot%202024-04-05%20225922.png?raw=true)

[How to configure/personalize webserver settings in an EC2 Instance](https://www.youtube.com/watch?v=5wFUE61nBBE&t=1s)



## Tutorial 📋

This Step-by-Step is based around setting up the EC2 instance, and showing how I was successfully able to set the website up. By no means am I a website dev, therefore, the process that I had to go through personalizing the base configuration of the website is in the Trial & Error section.

### Step 1 - Find EC2 in Dashboard

![EC2](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/02.png?raw=true)

### Step 2 - Launch the instance setup

![Launch](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/02.png?raw=true)

### Step 3 - Enter the name of your EC2 Server

![Name](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/03.png?raw=true)

- This is essential in finding a specific instance in a more complex cloud environment where you may be running many instances at once.

### Step 4 - Chose your AMI (Amazon Machine Image)

![AMI](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/04.png?raw=true)

- Your AMI is basically the OS that will be running on the EC2. There are many images to choose from. I'm sure there are some you are already familiar with.



### Step 5 - Chose Instance Type

![Instance Type](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/05.png?raw=true)

- Here is where you choose how powerful and versatile you need your instance to be. This depends on your overall goals of what the instance is being created for in the first place. The more powerful & versatile, the more expensive. These instances at default are set to run on demand, meaning you only pay for what you use. If you have data going to it for 2 seconds every hour, you're only being charged at that rate.

### Step 6 - Create a Key Pair

![Pair Login](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/06.png?raw=true)

- This will be your "key" to get into your instance, when trying to SSH in to make backend changes

![key pair format](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/06a.png?raw=true)

- Your key pair type and format basically chooses the type of key that you will need to enter, which affects the way you remote into the instance.



Open SSH is used login into a Linux system from Windows

### Step 7 - Download your key! Remember where you saved it!

![Key](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/07.png?raw=true)
Save this key to use in the tutorial links I attached in the Trial & Error Section.



### Step 8 - Create your security group
Who do you want in? Who do you not want in? Remember, this is a public webserver where we want out fans, subscribers, or customers to access. But we also want our web developers to have access to make changes as need.

![Security Groups](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/08.png?raw=true)

- Allow SSH (for the devs)
- Allow HTTP & HTTPS (for customers, and secure transactions/connections)



### Step 9 - Review Summary

- Here you get a quick review of all of your Instances setttings, from the image to the storage & more.

![Summary](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/09.png?raw=true)

### Step 10 - Double Check Security Groups

- Double check security groups to ensure proper inbound traffic is allowed and blocked. Edit if you forgot an inbound rule.

![Inbound Rules](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/11.png?raw=true)


### Step 11 - Copy your Public IP

- This is what you will paste into your web browser. In more complete websites, DNS will translate this to an actual domain name rather than an IP.

![Public IP](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/13.png?raw=true)

### Step 12 - Paste the IP into your web browswer

- Whatever the web browser is configured on the EC2 to show, will appear. This is the default Header on the Apache webserver that I installed on the EC2 instance.

![Default Webpage](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/14.png?raw=true)


### Step 13 - Post Development changes

- after adjusting the internal code of the "Index" section of the server, your website is now personalized! The more moving parts that your website has, the more complex your code will be.

![Jersey Site](https://github.com/RightHandCloud77/AWS-Cloud-Journey/blob/main/Notes/Project%20Screenshots/%23COM3-AWS100/15.png?raw=true)
You can see the public IP that I copied in Step 11 now shows my lackluster e-commerce site for selling jerseys & other fan merchandise. Fanatics.com better watch out 💰


## ☁️ Cloud Outcome


Further investigation into EC2 provided me a better understanding of cloud computing. I absolutely underestimated the power of an EC2 even after studying the capabilities. Applying real-world business concepts to the capabilities of EC2 instances provided me with a new perspective. In a world that is changing from hardware to virtual, EC2s are essential & constantly evolving to meet more and more consumer demand. The possibilities are endless.

Through trial and error, I provisioned an EC2 instance, configured to host a website, and made necessary adjustments using SSH from my IP. However, I am curious about how these instances are created at a faster pace and on a larger scale to meet the demands of powerhouse companies worldwide. As always, I learned the importance of troubleshooting and utilizing online resources to overcome challenges during the setup process.

## Next Steps

After this project, I'm a little curious on how AWS processes DNS request in real time. Or maybe the scaling capabilities of an EC2 Instance. I also plan to explore the scaling capabilities of EC2 instances and study which companies are leveraging cloud technologies to enhance customer/fan experiences and business infrastructure.


