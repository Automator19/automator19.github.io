---
layout: post
title: Amazon S3 Permissions overview
category: [AWS]
---

# What is S3 Access Policy ?

* Amazon s3 access policy describes who has access to what and what level of permissions.
* Access policy attached to S3 resource (buckets and objects) which is called **bucket policy** 
* Access policy attached to an AWS user is called **user policy**

# S3 access configuration options

There are 3 different s3 access configurations options avaialble within amzon S3.

## Bucket Policy

A bucket policy is used by the bucket owner to grant permissions to the bucket and pbject inside the bucket. 
You can create a bucket policy [AWS Policy Generator](http://awspolicygen.s3.amazonaws.com/policygen.html)

This policy is set on the bucket under permissions --> bucket policy

For example policy below allows access to pdf files stored in the bucket
```
{
  "Id": "Policy1678106477411",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1678106470336",
      "Action": "s3:*",
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::my-aws-bucket-2023-03-06/*.pdf",
      "Principal": "*"
    }
  ]
}
```

## User Policy

You can create a user policy and configure json to create a customised access policy.
IAM Policy then can be attached to IAM user as requiered. Example below show user policy to grant access to specific folder. 
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1678107240224",
      "Action": [
        "s3:ListBucket"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::my-aws-bucket-2023-03-06",
      "Condition": {
        "StringNotLike": {
          "s3:prefix": "development"
        }
      }
    }
  ]
}
```

screenshot below show polict attached to the IAM user

![policy_attached_to_IAM_user](/assets/images/policy_attached_to_IAM_user.JPG)

## S3 Access Control List

### Object ACLs

ACLs are defined explicirtly in the objet ACL. This provides a specific and granular way to maintain permission to s3 bucket objects. 
You can set this permisions by going to the object, select permissions and edit ACLs.

### Bucket ACLs

ACLs can alsoe be defined explicitly at bucket level. For example if you just need to give read access to everyone for public access to the bucket. 

