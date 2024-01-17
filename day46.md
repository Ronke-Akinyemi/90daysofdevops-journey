---
title: "Set up CloudWatch Alarms and SNS topic in AWS"
datePublished: Tue Dec 12 2023 15:37:34 GMT+0000 (Coordinated Universal Time)
cuid: clq2iarbr000608jz8astal9b
slug: set-up-cloudwatch-alarms-and-sns-topic-in-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702389589493/68c4b2fc-7ae4-4b61-b4a0-4a9060d49f20.png
tags: aws, cloudwatch, 90daysofdevops

---

## What is Amazon CloudWatch?

Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real-time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications. Read more about CloudWatch from the official documentation [here](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html).

## What is Amazon SNS?

Amazon Simple Notification Service is a notification service provided as part of Amazon Web Services since 2010. It provides a low-cost infrastructure for the mass delivery of messages, predominantly to mobile users.

Read more about it [here](https://docs.aws.amazon.com/sns/latest/dg/welcome.html).

## Task :

* Create a CloudWatch alarm that monitors your billing and sends an email to you when it reaches $2. (You can keep it for your future use)
    
* Delete your billing Alarm that you created now. (Now you also know how to delete as well. )
    

To create a billing alarm using the Cloudwatch Console: Open the CloudWatch Console

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702386404642/33a9dd6f-5830-4ea6-8679-325d4edecf32.png align="center")

On the left-hand side, choose "Alarms" and then choose "Billing".

Click on the "Create Alarm" button.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702386612409/d4350ec4-6c2f-4217-9c05-6a321728df00.png align="center")

Under Metrics, select "EstimatedCharges" for the Metric name.

Define the conditions for your alarm. For example, I set the threshold to be "**Greater than $2**" for a "**Period**" of 6 hours.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702386953919/aa8f767d-da32-4142-9730-c48ea7a477a5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702387329124/9bb2db71-4176-4d73-9ba2-623554126cf7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702387833031/03c084ae-72e8-429c-b2f7-8d29762b2996.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702387923114/c0cd1996-3fcf-4093-9d3a-87323ff622ac.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702387953347/a4ba82d2-b889-413f-88f5-cac09528e8bd.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702388323842/cacc376c-8861-4520-8a4d-7fb5cf957ef1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702388428166/08072f65-885f-40d1-b29b-f74ba70f7211.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702388502219/ce1bc950-d134-4706-9fb4-bb7a784f3f5a.png align="center")

### Deleting a billing alarm

Go to the CloudWatch Console, navigate to Alarms and choose "Alarms". Find and select the alarm you want to delete. Click on the "Actions" button and choose "Delete." Confirm the deletion when prompted.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702388704590/2b6450a0-0b10-4283-8412-037f6354c044.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702388735518/82d50e53-66bf-4410-aaac-600dd82391b6.png align="center")

You can check out the [official documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/monitor_estimated_charges_with_cloudwatch.html).
