# Running EC2 instance for app

![Alt text](https://github.com/a-miah/cloudcomputingAWS/blob/main/images/EC2.JPG "EC2 Instance")

## What is an EC2 Instance

An Amazon EC2 instance is a virtual server in Amazon's Elastic Compute Cloud (EC2) for running applications on the Amazon Web Services (AWS) infrastructure. It is a web service that provides secure, resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.

## Running EC2 Instance for app

- Launch instance from EC2 dashboard
- Choose Ubuntu 18.04LTS on AWS (which box we are using)
- select size of VM (storage size)
- Configure instance (autoassign public IP - enable - to ensure it works in browser and not just terminal)
- Add tags - Name: devops_attaik_app 
- security group to secure it (who can access it) - type: SSH, Port range: 22, Source: My IP
- To allow to launch on browser - type: HTTP, Port: 80, Source: anywhere
- Review and launch - select eng99|rsm key and tick box

Then open bash terminal and do below commands:

- `cd .ssh` in git bash
- `chmod 400 eng99.pem` - giving permission
- connect with instance created and go to SSH Client
- Copy the EC2 instance from AWS
- `sudo apt-get update -y`
- `sudo apt-get upgrade -y`
-	`git pull` <github URL>
-	`sudo chmod +x environment/provision.sh` (filepath to provision folder) - this will install nginx and other required packages
-	`sudo environment/provision.sh`
-	`sudo apt install npm`
-	Go into app location
- `npm install`
- might need to seed first 
-	`npm start` and app will be ready

# 2-tier architecture deployment 

![Alt text](https://github.com/a-miah/cloudcomputingAWS/blob/main/images/2-tier-architecture-deployment.JPG "db EC2 Instance")

## Creating the db istance
- Create EC2 Linux Ubuntu 180.04LTS
- t2-micro
- default storage 
- tags eng99_attaik_db
- SG allow 27017 only from your app IP
> Note EC2 IP changes every time we stop and start 
- allow ssh port 22 from your IP only (secure)
- eng99_attaik_db_sg
- ssh into your db ec2 instance 
- install required mongodb
- status active
- change mongod.conf file ip to 0.0.0.0
- cat mongod.conf
- restart, enable, status
- head back to our app instance
- create env var DB_HOST="mongodb://db-ip:27017/posts"
- source it
- cd app
- node seeds/seed.js (if needed)
- npm start


DB_HOST="mongodb://3.250.226.137:27017/posts  #IP (3.250.226.137) is the public ip from ec2 db instance 


### EC2 Instance Documentation

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html