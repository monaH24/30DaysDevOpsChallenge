## Project Overview:
This project is is an alert system designed to provide real-time NBA games updates via SMS and Email.
Features:

## Prerequisites:
AWS account<br/>
SportsData.io account<br/>
Basic understanding of Cloud computing<br/>
Familiarity with API fundamentals<br/>
Python programming knowledge

## Technologies:
AWS Cloud <br/>
SNS (Sending notifications)<br/>
Lambda (to execute code for handling API requests and responses)<br/>
EventBridge (to create schedule events)<br/>
NBA Game API<br/>
Python


## Steps:

## 1.Create an SNS Topic
Open AWS Management Console<br/>
Open SNS<br/>
Select Create Topic<br/>
Name the topic and select Standard for the topic type

## 2.Add Subscriptions to the SNS Topic
After creating the topic click on the topic from the topics page<br/>
From the subscriptions tab Select create subscription<br/>
Add an Email or a Phone Number for SMS <br/>
Click Create Subscription<br/>
Confirm the email

## 3.Create an SNS Publish Policy
Select IAM service in the AWS Management Console<br/>
from Policies select Create Policy<br/>
Click JSON and paste the JSON policy<br/>

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "sns:Publish",
            "Resource": "arn:aws:sns:REGION:ACCOUNT_ID:gd_topic"
        }
    ]
}
```

Replace REGION and ACCOUNT_ID with your AWS region and account ID<br/>
Enter a name for the policy <br/>
Click Create Policy

## 4.Create an IAM Role for Lambda
From the same IAM Service as before<br/>
Select Roles and create one<br/>
For policies add the policy created in the previous step and AWSLambdaBasicExecutionRole<br/>
Click Next<br/>
Enter a name for the role<br/>
Click Create Role

## 5.Deploy Lambda Function
Search Lambda service and click create Function<br/>
Select Author from Scratch<br/>
Enter a function name<br/>
Choose programming language (python for this project)<br/>
Assign the IAM role created earlier<br/>
For the Function Code section:<br/>
Copy the content of the src/gd_notifications.py file from the repository<br/>
Under the Environment Variables section, add the following:<br/>
NBA_API_KEY: your NBA API key<br/>
SNS_TOPIC_ARN: the ARN of the SNS topic created earlier<br/>
Click Create Function

## 6.Setup Automation with EventBridge
Open Eventbridge service and select create Role from Roles<br/>
Select Event Source: Schedule<br/>
Set the Cron schedule for when you want updates<br/>
Under Targets, select the Lambda function created earlier and save the rule.

## 7.Test the System
In the Lambda function create a test event to simulate execution<br/>
Check Email or Phone to verify that SMS notifications are sent to the subscribed users<br/>
