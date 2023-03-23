---
layout: post
title: Terraform Block
category: [Terraform]
---

# IMPORTANT NOTE 
Only constant values can be used within terraform block. Arguments may not refer to named objects like resources, input variables and may not use    terraform language built-in functions. 

- Here is the code where you define terraform and provider block

```terraform
terraform {
# Required version
required_version = "~> 1.4.2"

# Required proivders
required_providers {
    aws = {
        source = "hashicorp/aws"
        version = "4.59.0"
    }
}

# provider block
provider "aws" {
    region   = "eu-west-1"
    profile  = "profilename"
}
# Remote backend for storing Terraform State in s3 bucket - if not defined it will be stoted locally
backend "s3" {
    bucket = "mybucket"
    key    = "path/to/my/key"
    region = "eu-west-1"
}
}
```

## Required providers  
- Inside required_providers block "aws" is an argument with map list
- Name of the provider can be anything "aws1"
- Terraform configurations will refer to custom name "aws1" outside required_provider block