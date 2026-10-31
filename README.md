
# Rafi needs to build a custom AWS VPC (not the default one) with a public subnet for an Nginx web server hosting the static landing page, reachable by anyone on the internet via an Internet Gateway, public IP, and a security rule allowing HTTP/HTTPS.

# Create the ShopBondhu VPC

## Goal

Create an Amazon Virtual Private Cloud (VPC) with these settings:

This file contains instructions. No AWS resources have been created by generating this file.

## Task 1: Create the VPC

1. Sign in to  AWS account and select intended AWS Region.
2. Search VPC
3. In Virtual Private Cloud Menu, Select Your VPCs
4. Click Create PVC
5. In VPC setting Name Tag shopbondhu-vpc
6. IPv4 CIDR 10.0.0.0/16 
(10.0.0.0/16 represents a block of IPv4 addresses where the first 16 bits are locked as the network prefix, leaving 16 bits for individual devices (hosts))
7. Create VPC Click and shopbondhu-vpc created

[PVC](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/12ddadbec3eb82803d39028ad14a14b1f3a5793a/screenshots/01-vpc.png)

## Task 2: Create the subnets

In Virtual Private Cloud Menu Select Subnets and click
Select VPC ID 
Create Two Subnet one is Public and another is private

Public Subnet
1. Subnet Name shopbondhu-public-subnet
2. Select Availability Zone
3. IPv4 subnet CIDR block 10.0.0.0/28

Private Subnet
1. Subnet Name shopbondhu-private-subnet
2. Select Availability Zone
3. IPv4 subnet CIDR block 10.0.0.16/28
4. Create Subnet

[Public Subnet ](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/12ddadbec3eb82803d39028ad14a14b1f3a5793a/screenshots/02-subnets_Pub.png)

[Private Subnet](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/12ddadbec3eb82803d39028ad14a14b1f3a5793a/screenshots/02-subnets_PVT.png)

## Task 3: Internet Gateway

In Virtual Private Cloud Menu Select Internet Gateways

1. Click Create internet gateway
2. Name Tag shopbondhu-igw
3. Create internet gateway
4. Select Actions tab into internet gateways then select Attach to VPC
5. Select shopbondhu-vpc,then create

[Internet Gateway](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/12ddadbec3eb82803d39028ad14a14b1f3a5793a/screenshots/03-igw-attached.png)

## Task 4: NAT Gateway

In Virtual Private Cloud Menu Select NAT Gateways

1. Click Create NAT Gateways
2. Name shopbondhu-nat
3. Availability mode Regional-new 
4. Select shopbondhu-vpc
5. Connectivity Type Public
6. Create NAT gateway 

[NAT Gateways](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/12ddadbec3eb82803d39028ad14a14b1f3a5793a/screenshots/04-nat-gateway.png)

## Task 5: Route tables

In Virtual Private Cloud Menu Select Route tables

Create Two Route tables has been create. 
One for Public Subnet (shopbondhu-public-subnet)
Another for Private Subnet (shopbondhu-private-subnet)

## Public Route

1. Click Create route table
2. Name shopbondhu-public-rt
3. Select shopbondhu-vpc
4. Create route table

[Public route](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/05-public-rt.png)

5. Click Edit routes
6. Add route
7. Select Destination 0.0.0.0/0 (In routing tables, a default route (0.0.0.0/0) forwards traffic to any destination that doesn't have a more specific route.)
8. Target select internet Gateway for Drop down
9. Then route associated with Internet Gateway(shopbondhu-igw)
10. Save Changes 


## Subnet associations with public route
In public route 
1. Select Subnet associations tab
2. Click Edit subnet Associations
3. Public route association with public subnet(shopbondhu-public-subnet)
4. Save associations



## Private Route

1. Click Create route table
2. Name shopbondhu-private-rt
3. Select shopbondhu-vpc
4. Create route table

[Private Route](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/06-private-rt.png)

5. Click Edit routes
6. Add route
7. Select Destination 0.0.0.0/0 (In routing tables, a default route (0.0.0.0/0) forwards traffic to any destination that doesn't have a more specific route.)
8. Target select Nat Gateway for Drop down
9. Then route associated with NAT Gateway(shopbondhu-nat)
10. Save Changes 

## Subnet associations with private route
In private route 
1. Select Subnet associations tab
2. Click Edit subnet Associations
3. private route association with private subnet(shopbondhu-private-subnet)
4. Save associations

## Task 6: Launch the EC2 instances

# Instance menu: go to Launch instance
1. Name and tags server name shopbondhu-web
2. Application and OS Images section select Ubuntu OS
3. Instance Type select t3.micro

[Launch instance_01](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/07-ec2-instances_01.png)
[Launch instance_02](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/07-ec2-instances_02.png)



# Key pair(login)
4. Create new Key pair. then click
5. Key pair name shopbondhu-web-public
6. Key pair type select RSA
7. Private key file formate select .pem
8. Create key pair

 [Key pair](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/07-ec2-instances_02.png)

# Network Setting
1. Click Edit
2. VPC-required; in drop-down select shopbondhu-vpc
3. Subnet drop-down select shopbondhu-public-subnet
4. Auto -assign public drop-down select Enable
5. Name Security group ShopbondhuSG
6. Click Launch Instance
7. Connect to server
8. In Connect to Linux instance, go to  SSH client for server connection details 


 [Network Setting](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/07-ec2-instances_03.png

# Connect to Ubuntu server with Git Bash

1. Create a aws folder
2. Paste download .pem file within aws folder
3. Open folder open with git bash
4. Run those command 
   chmod 400 "shopbondhu-web-public.pem"
   ssh -i "shopbondhu-web-public.pem" ubuntu@13.210.117.22
5. Now connect to 13.210.117.22 with git base
6. Run sudo apt update
7. Run sudo apt upgrade

## Task 7: Install and configure Nginx (web server)
1. sudo apt install nginx -y
2. sudo systemctl status nginx

 ## Security group
1. Go to AWS Instance shopbondhu-web ,then Connect
2. Select Security Tab
3. Click Security groups
4. In inbound rules click Edit inbound rules
5. Add rule click 
6. Type section select HTTP and Source Type section select anywhere-IPv4
7. Create route
[Security group](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/08-security-groups.png)

## Nginx Port Access
1. In Browser hit http://13.210.117.22,Welcome to nginx message will be appears

[Nginx Status](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/09-nginx-status.png)

[Nginx Broswer](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/10-website-browser.png)

## Task 8: Deploy the frontend
1. git clone https://github.com/sumaya-shemo/shopbondhu.git
2. cd shopbondhu
3. npm i
4. npm run dev
5. In Browser hit http://localhost:3001 shopbondhu website will be appears

[Shopbondhu website](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/10-website-browser_01.png)  

## History of Linux Command
[History](https://github.com/sumaya-shemo/shopbondhu-aws-assignment/blob/8aca5cd58b1760cbc919dc1634aaea00ffb645b0/screenshots/History.png)

