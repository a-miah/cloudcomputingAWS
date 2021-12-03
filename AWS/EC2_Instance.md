# Running EC2 instance for app

*Insert Image*

## Running EC2 Instance for app

- Choose Ubuntu 18.04LTS on AWS
- select size of VM
- security group to secure it
- `cd .ssh` in git bash
- `chmod 400 eng99.pem` - giving permission
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