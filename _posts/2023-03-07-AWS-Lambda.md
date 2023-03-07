---
layout: post
title: AWS Lambda
category: [AWS]
---

# What is Lambda ?

AWS Lambda is an event-driven, serverless computing platform. It simply let's you run your code without deploying resources and apps. 

# How does Lambda work ?

Step 1 : Upload AWS supported code ( Java, Pythin, Go, C#)

Step 2 : AWS services will trigget the Lamba function

Step 3: Following are some examples of what lambda fuction can do

* Upload files in s3 bucket
* GET/POST HTTP requests
* add/modify DB tables
* Push notifications
* run a Website
* Email delivery

# What can trigger lambda ?

For Lambda function to execute, an event must occur. Events cane be anything happenign with resources within your aws account. 

e.g Did someone upload a file to S3 ? or  Did someone write a record to datbse ? or Event bridge to trigger lamba using cron. 