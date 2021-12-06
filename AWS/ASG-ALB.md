# Auto Scaling Group and Application Load Balancing 

![Alt text](relative/path/to/img.jpg?raw=true "Autoscaling and Load Balancing Diagram")

**Scaling out** – creating more copies of the same server and if one gets damaged or more traffic then you then move it to the replica instances whilst the other one gets updated (24 mins in recording)

**Scaling up** – increasing facility 

**Highly available** – making it available in different AWS servers in different locations/regions to ensure if one location goes down such as Ireland it is available in London etc (multi-availability zones deployment – Multi AZs)


- We need to make it highly available and highly scalable 
- The service we need: Autoscaling Group and Load Balancers

Paying for the instances when the traffic increases and then reducing when traffic is down thus saving money

-	Need to create a launch template for our Autoscaling group
-	Create Auto scaling group
-	ALB – Application Load Balancer
-	Attach to VPC – 3 subnets in 3 different AZs
-	Security Group  (SG) for app
-	All EC2 have Nginx installed 
-	Regions EU and AZs in Europe
-	Disaster Recovery (DR) plan


# Create a Launch Template
1.	Create launch template
2.	Template name - eng99_attaik_ASG_lt (or similar)
3.	Tick autoscaling guidance box
4.	Select Ubuntu Server 18.04 LTS (ends in 5b5)
5.	Instance type – t2 micro
6.	Select key pair – eng99
7.	Network settings – Virtual Private Cloud (VPC)
8.	Find your security group you previously created
9.	Keep storage same
10.	Advanced details – fill in user data box with commands from app provision to install the packages you require

![Alt text](relative/path/to/img.jpg?raw=true "Launch template advanced detail")

# Create Auto Scaling Group
11.	After creating launch instance 
12.	Go to Auto Scaling Groups from E2 instance dashboard
13.	Create autoscaling group with name (eng99-attaik-ASG-app-ami)
14.	Find the template you created
15.	Keep VPC same
16.	Select availability zones 1a, 1b, 1c
17.	Next
18.	Attach to a new load balancer > Application load balancer
19.	Internet facing selected
20.	Keep AV Zones the same 
21.	Create a target group for listeners and routing
22.	Select monitoring – enable group metric for CloudWatch
23.	Enter group size with min, max and desired 
24.	Target tracking scaling policy
25.	Add notifications
26.	Add tags > eng99_attaik_asg_appami
27.	Review and create

(NOTE: for the app ami had to go in terminal and manually run npm install/start from ssh)

## ASG and ALB Review 

![Alt text](relative/path/to/img.jpg?raw=true "Review Diagram")