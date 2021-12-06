# AMI – Amazon Machine Image

## AMI Diagram

![Alt text](relative/path/to/img.jpg?raw=true "AMI Diagram")

The AMI saves a snapshot of an instance with all the required dependencies installed therefore when you later return you don't have to reset another instance as it saves it in memory

![Alt text](relative/path/to/img.jpg?raw=true "AMI Location")

- Need an EC2 instance running
- ami-id – location of the AMI

Given an AMI we need to know a few things before we load up an instance

- AWS keys 
- Security rules - things which are to be shown on the browser and hidden (such as databases)
- Type of instance – family t2-micro
- Elastic bandwith storage – EBS 8gb
-	Tags - same naming convention - eng99-attaik-ami
-	Operating systems

## Creating AMI Instance
- Select the instance you want to create an image for
- Actions > Images and templates > Create Image
- Launch the AMI and review (similar to setting up EC2 instance)