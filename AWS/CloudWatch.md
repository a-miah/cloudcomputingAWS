# Monitoring with CloudWatch

![Alt text](https://github.com/a-miah/cloudcomputingAWS/blob/main/images/Monitoring.JPG "Monitoring")

-	Response time depending on network/traffic
-	How often - use logs – hourly/daily/weekly etc
-	Status code is 200
-	CPU utilisation  => 50% (if above then email needs to be sent)
-	Package loss – missing user requests
-	Simple Queue Service (SQS) – no request is missed
-	Simple Notification Service (SNS)
-	AutoScale on demand and notification from cloudwatch
-	Load Balance

## Create Alarm
-	Select EC2 instance > Actions > Monitor and troubleshoot > Manage cloudwatch alarms
-	Add alarm – name it 
-	Alarm notification – enter a name to create an SNS topic to send notification when alarm is triggered 
-	Specify alarm thresholds – criteria for alarm to trigger
-	Select create 

> When you create a CloudWatch alarm, you can add this SNS topic to send an email notification when the alarm changes state.


## Create SNS Topic (SNS - Simple Notification Service)
-	Go to SNS – Simple Notification Service > Topics
-	Enter the name of the topic created in the alarm step 
-	Publish message – the message you want to send to the person being notified
-	Create subscription – the way and person you want to be notified

Amazon SNS Topics - https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/US_SetupSNS.html

## CloudWatch Services

![Alt text](https://github.com/a-miah/cloudcomputingAWS/blob/main/images/CloudWatch-services.JPG "CloudWatch Services")


### Automated and Manual monitoring 

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring_automated_manual.html