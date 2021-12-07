# Virtual Private Clouds - VPCs

![Alt text](https://github.com/a-miah/cloudcomputingAWS/blob/main/images/VPC-diagram.JPG "VPC Diagram")

- VPCs are an area within the cloud which only you have access to and can decide who enters etc 
- Subnets – rooms within the VPC with certain access to each part



## What is CIDR block


- CIDR, which stands for Classless Inter-Domain Routing, is an IP addressing scheme that improves the allocation of IP addresses.
- CIDR is based on variable-length subnet masking (VLSM). This allows it to define prefixes of arbitrary lengths making it much more efficient than the old system. CIDR IP addresses are composed of two sets of numbers. The network address is written as a prefix, like you would see a normal IP address (e.g. 192.255.255.255). The second part is the suffix which indicates how many bits are in the entire address (e.g. /12). Putting it together, a CIDR IP address would look like the following:
- `192.255.255.255/12`

## What is an IPv4 and IPv6

- There are two revisions of the IP protocol that are widely implemented on systems today:
- IPv4 and IPv6 are CIDR classes. IPv4 is current standard, but as demand is exceeding amount, IPv6 will be implemented. IPv6 addresses may contain up to 128 bits instead of the 32-bit maximum of IPv4.

## What is a route table (RT)

- A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed. To put it simply, a route table tells network packets which way they need to go to get to their destination.

## What is an Internet Gateway (IG)

- A computer that sits between different networks or applications. The gateway converts information, data or other communications from one protocol or format to another. A router may perform some of the functions of a gateway. An Internet gateway can transfer communications between an enterprise network and the Internet.

## VPC and Subnets Range

- VPC & Subnet Range: A virtual private cloud (VPC) is a secure, isolated private cloud hosted within a public cloud. VPC customers can run code, store data, host websites, and do anything else they could do in an ordinary private cloud, but the private cloud is hosted remotely by a public cloud provider. (Not all private clouds are hosted in this fashion.) VPCs combine the scalability and convenience of public cloud computing with the data isolation of private cloud computing.
- A subnet, or subnetwork, is a segmented piece of a larger network. More specifically, subnets are a logical partition of an IP network into multiple, smaller network segments.

https://www.cloudflare.com/en-gb/learning/cloud/what-is-a-virtual-private-cloud/

## What is NACLs

- A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. You might set up network ACLs with rules similar to your security groups in order to add an additional layer of security to your VPC.

## What is the diff between stateless and stateful (NACLs vs Security Groups)

- Security groups are stateful, acts as the firewall for an EC2 instance.
- NACL's are stateless and act as the firewall to the VPC subnets.
- Security rules only allow rules and do not deny whereas NACLs can allow and deny rules therefore can prevent certain IP addresses from accessing the subnets.

## Create a Diagram for your VPC


https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html


# Steps to create a VPC:

Connecting an internet based app to the database without giving direct access to the db.

1.	Create a VPC
2.	Create an Internet Gateway (IG)
    - Attach the IG with our VPC
3.	Create a public subnet for our app
4.	Create a Route Table (RT) with routes/rules
    - Edit routes to allow IG and VPC
    - Associate our RT to our public subnet
5.	Create a Security Group (SG) now or create when we launch the app
    - Port 22 from my IP
    - Port 3000
  	- Port 80 HTTP
  	- HTTPS – SSL


## Steps: 


Create VPC:
1.	Go to VPC services > VPC Dashboard
2.	VPCs > Create VPC
3.	Name it – eng99_attaik_vpc
4.	IPv4 CIDR – 10.0.0.0/16 (no IPv6 cidr block)
5.	Add tags (name – eng99_attaik_vpc)
6.	Click create VPC

Create Internet Gateways:

7.	Create IG
8.	Name and tag it - eng99_attaik_IG

Attach to VPC:

9.	Attach to VPC either from green banner or banner > attach to VPC
10.	Select from list the one you created 

Subnets:

11.	Select VPC from dropdown list
12.	Subnet settings – name it 
13.	Select Availability Zone – Ireland (eu-west-1a)
14.	Select an IPv4 CIDR block – 10.0.2.0/24 (different to one created above – slightly)
15.	Create subnet

Create Route Table:

16.	Name it and select your VPC from the dropdown 
17.	Create RT
18.	Actions > Edit routes
19.	Search for your IG
20.	Save changes
21.	Actions > Edit subnet associations > Select the subnet you created above

Go to AMI’s:

22.	Launch your app ami
23.	T2 micro
24.	Network- select the VPC you created
25.	Subnet – select the subnet you created
26.	Enable IP
27.	Storage > Tags

Create new Security Groups: (eng99_attaik_SG)

28.	SSH – port 22 – my IP 
29.	HTTP – port 80 – 0.0.0.0
30.	Custom TCP – port 3000 – anywhere – 0.0.0.0
31.	Review and launch > eng99|rsa

Connect Instance 

32.	SSH in bash and launch app using np start


### Creating private subnet for same VPC:

1.	Select VPC from dropdown list
2.	Subnet settings – name it (eng99_attaik_vpc_subnet_db)
3.	Select Availability Zone – Ireland (eu-west-1a)
4.	Select an IPv4 CIDR block – 10.0.1.0/24 (different to one created above – slightly)
5.	Create subnet

**Subnet automatically connects to the route table and sets it to private therefore no need to create another one**


6.	Go to ami select ami and launch
7.	Select vpc
8.	Private subnet
9.	Enable auto assign IP
10.	No storage
11.	Tags – eng99-attaik_vpc_db
12.	SG – add public to SSH for db
13.	Custom TCP – 27017 – 10.0.2.0/24

Public - 10.0.2.0/24

Private - 10.0.1.0/24

14.	Launch eng99|rsa
15.	Go into bashrc and update DB_HOST with private db vpc subnet IP from networking tab
16.	Exit out and connect to app instance to double check db_host is done 
17.	Npm install and npm start



# Creating NACL

Making sure DB is not exposed to the internet 

1.	VPC > Create NACL
2.	Name and select your VPC
3.	Create NACL
4.	Go to NACL > edit inbound rules
5.	Add new rule
6.	Type – all traffic, source – app public subnet 
7.	Save changes
8.	Change outbound rules
9.	Type – all traffic, source – app public subnet 
10.	Go to db subnet and edit nacl
11.	Select nacl you made and save changes 
