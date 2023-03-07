---
layout: post
title: Connect Lambda function to VPC
category: [AWS]
---

- AWS Lamba is a public service which runs within a region. Therefore it can not connect to resources hosted within VPC. 

- In some cases you will need to connect your function to VPC to access private resurces ( like database server) during execution. 

# What do you need to setup Lamba access to VPC ?

- Lambda function needs to be configured with below
    * Private subbet ID
    * Security Group ID 

- Lambda function's execution role must have following permissions:
    * ec2:CreateNetworkInterface
    * ec2:DescribeNetworkInterfaces
    * ec2:DeleteNetworkInterface 
    * All above permissions are included in AWSLambdaVPCAccessExecutionRole managed policy. 


- Lambda uses above information to setup an Elastic Network Interface (ENI), using avaiable IP from your private subnet. 
- Note that Lambda will loose internet connectivity as soon as ENI is setup. You will need NAT Gateway for internet access 

# How does it look like in a diagram ?

![Diagram](/assets/images/connect-lambda-to-vpc.JPG)


# How do you connect Lambda function to VPC ?

## Create a Test VPC

## Create a Private Subnet

## Create a Public Subnet

## Create a "Hellow World" Lambda function

## Go to configuration and VPC , Setup VPC, Subnet and Security Group. 
