# Monitoring with CloudWatch
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


## Create SNS Topic (SNS - Simple Notification Service)
-	Go to SNS – Simple Notification Service > Topics
-	Enter the name of the topic created in the alarm step 
-	Publish message – the message you want to send to the person being notified
-	Create subscription – the way and person you want to be notified
