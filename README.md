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
-In User Data section, paste "create_ALB" file as text with updated mount information<br>
-Route to both EC2 instance in Private App Subnets<br>
-Create Target Group<br>
-Create ALB<br>
-Access website using DNS name on ALB and update URL in admin settings of Wordpress
<h4>Register Domain Name using Route 53</h4>
-Payment may be required
<h4>Create DNS Domain Name Record</h4>
-Access the website using the domain name<br>
-Update Domain Name settings in Wordpress admin settings
<h4>Register SSL certificate</h4>
-Create record in Route 53
<p align="center">
<img src="https://i.imgur.com/PCits2k.png" height="85%" width="85%" alt="Bastion Host Architecture"/>
</p>
<h4>Create Bastion Host in Public Subnet</h4>
-Add SSH security group
<h4>Download paegant.exe from Putty download page</h4>
-Add Private Key Pair<br>
-Allow agent forwarding in Putty configuration<br>
<h4>Create HTTPS Listener for ALB</h4>
-Redirect traffic to HTTPS<br>
-SSH into Private Data Subnet Webserver EC2 instance through public IP of Bastion Host instance to modify wp-config file using "HTTPS_Listner_ALB" file<br>
-To access PHP nano text editor wp-config file type "sudo su" "nano /var/www/html/wp-config.php"
<p align="center">
<img src="https://i.imgur.com/gsXtY61.png" height="85%" width="85%" alt="ASG Architecture"/>
</p>
<h4>Create Auto Scaling Group</h4>
-Terminate EC2 Webservers<br>
-Create Launch Template<br>
-Include "create_ASG" file in User Data section<br>
-Create ASG
<h4>Clean Up Everything to Avoid Charges</h4>

<br>
<h2>Resources Used</h2>
- <b>YouTube:</b> https://www.youtube.com/watch?v=MHsI8hJmggI&list=PLqBeiU46hx1H--SNfTrohTOWeqkK-M2Y0&index=1&ab_channel=JoshMadakor-Tech%2CEducation%2CCareer 

- <b>YouTube Channel:</b> [TechWithLucy](https://www.youtube.com/watch?v=5RVT3BN9Iws&t=193s&ab_channel=TechWithLucy) <br>
- <b>AOSNote Course:</b> [Deploy a WordPress Website on AWS](https://www.aosnote.com/offers/xFzqby9z/checkout)
