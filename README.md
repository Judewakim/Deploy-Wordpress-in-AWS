<h1>Deploy-Wordpress-in-AWS</h1>
<p align="center">
<img src="https://i.imgur.com/vHDg7sM.png" height="25%" width="25%" alt="AWS Logo"/>
</p>
<b>This lab is on how to deploy a Wordpress website in Amazon Web Services using a Windows computer. This lab utilize EC2, RDS, VPC, Route 53, and ASG. Programs such as Putty and AWS CLI are used.</b>
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
<h4>Create Security Groups</h4>
-Application Load Balancer Security<br>
-SSH Security<br>
-Webserver Security<br>
-Database Security<br>
-EFS Security<br>
<br>
<p align="center">
<img src="https://i.imgur.com/tl72KKY.jpg" height="85%" width="85%" alt="RDS Architecture"/>
</p>
<h4>Create RDS in Private Data Subnets</h4>
-Create Database Subnet Group<br>
-Create RDS
<p align="center">
<img src="https://i.imgur.com/KeKEB4G.png" height="85%" width="85%" alt="EFS Architecture"/>
</p>
<h4>Create EFS</h4>
-Place Mount Targets in each Private Data Subnet 
<h4>Create Key Pair in EC2</h4>
-Download Private Key to your computer
<h4>Download Putty</h4>
<h4>Launch EC2 instance for Wordpress Setup</h4>
<h4>SSH into Setup Server using Putty</h4>
-input hostname into Putty configuration<br>
-Connnection->Auth->Private Key File for Authentication
<h4>Use "install_wordpress_putty" file to install Wordpress using Putty</h4>
-Before fourth command, update EFS mount information<br>
-Update 'DB_NAME', 'DB_USER', 'DB_PASSWORD', 'DB_HOST' in PHP nano text editor<br>
-Enter Wordpress login information
<p align="center">
<img src="https://i.imgur.com/O6D87h6.png" height="85%" width="85%" alt="EFS Architecture"/>
</p>
<h4>Create Application Load Balancer</h4>
-Route to both EC2 instance in Private App Subnets 
<h4></h4>
