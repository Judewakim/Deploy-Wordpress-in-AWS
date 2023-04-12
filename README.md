<h1>Deploy-Wordpress-in-AWS</h1>
<p align="center">
<img src="https://i.imgur.com/vHDg7sM.png" height="25%" width="25%" alt="AWS Logo"/>
</p>
<b>This lab is on how to deploy a Wordpress website in Amazon Web Services. This lab utilize EC2, RDS, VPC, Route 53, and ASG. Programs such as Putty and AWS CLI are used.</b>
<h2>Overview</h2>
<br>
<p align="center">
<img src="https://i.imgur.com/6Y1wHG0.jpg" height="85%" width="85%" alt="Reference Architecture"/>
</p>
<br>
In this lab you will build a three-tiered network <b>VPC</b> using this reference architecture. The first tier, a public subnet, will hold the <b>NAT Gateway, Application Load Balancer, and Bastion Host</b>. The second tier, a private subnet, will hold the <b>EC2 instances</b>. The third tier, antoher private subnet, will hold the <b>RDS database</b>. These three tiers will be duplicated amongst two availablity zones for high fault tolerance and availability. Also, an <b>Internet Gateway and Public Route Table</b> will be used to give the VPC access to the Internet.

<h2>Steps</h2>
<h4>Create a VPC</h4>
-Enable DNS Hostnames
<h4>Create Internet Gateway</h4>
-Attach IG to VPC
<h4>Create Public Subnets in both availability zones</h4>
-Enable Auto Assign IP for both subnets
<h4>Create Public Route Table</h4>
-Add route to Internet from IG<br>
-Associate to Public Subnets
<h4>Create four Private Subnets</h4>
-Two App Subnets and Two Data Subnets
<br>
<br>
<p align="center">
<img src="https://i.imgur.com/KKjpbGH.jpg" height="85%" width="85%" alt="NAT Gateway Architecture"/>
</p>
<h4>Create NAT Gateways in Public Subnets of each availability zone</h4>
<h4>Create Route Private Route Tables for each gateway</h4>
-Connect Private Route Tables to NAT Gateways<br>
-Connect each Route Table to Private Subnets
<br>
<br>
<p align="center">
<img src="https://i.imgur.com/DKIzjt6.jpg" height="85%" width="85%" alt="Security Group Architecture"/>
</p>
<br>

<br>
<p align="center">
<img src="https://i.imgur.com/tl72KKY.jpg" height="85%" width="85%" alt="RDS Architecture"/>
</p>
<br>

