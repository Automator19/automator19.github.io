---
layout: post
title: Terraform Language Basics
category: [Terraform]
---

- Terraform uses HCL - Hashicorp Language
- Code in Terraform langugae is stored in plain text files with .tf file extension.
- There is also a JSON-based variant of the language that is name with .tf.json  file extension.
- All the files containing terraform code is known as **Terraform Configuration Files** or **Terraform Manifests**


# Terraform Configuration Syntax
- Terraform language consist of mainly 4 parts

1. Blocks 
    - Block is a container for the content like 
        - Terraform Settings block
        - Provider Block
        - Resource Block
        - Input Variable Block
        - Output variable block
        - Local values block
        - data sources block
        - modules block

2. Arguments
    - Argument assisngs a value to a particular name
    - As per code below **Identifier** before the equal sign the **Argument Name** and **Expresssion** after equal sign is **Argument Value**
3. Identifiers
4. Comments

example
```terraform

# Template
<BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>"   {
  # Block body
  <IDENTIFIER> or <ARGUMENT NAME> = <EXPRESSION> or <ARGUMENT VALUE> 
}

# AWS Example
resource "aws_instance" "ec2demo" { # BLOCK
  ami           = "ami-04d29b6f966df1537" 
  instance_type = var.instance_type 
}
```

- Single line comments with # or //
- Milti line comments are defined with 
```terraform
    /* 
    you comments goes here
    */
```

# Arguments, Attributes and Meta-Arguments

## Arguments
- is used to configure a particular resource. Arguments can be required or optional, as specified by the provider. 
- if required argument ( or expression) value not provided, terraform will give an error.

## Attributes
- are values exposed by existing resource. Reference to resource attribute are defined in format below
  resource_type.resource_name. attribute_name
- Attribute value are proivded by underlying cloud provider or API when arguments are infrastructure object's config which is provided to cloud provider or API. 

## Meta-arguments
- Changes a resource's behaviour, example **count or for_each** meta-arguments will deploy multiple resources. 
- Meta arguments are function of terraform itself and not resource or provider specific. 
- Detailed info on meta arguments are here - https://developer.hashicorp.com/terraform/language/meta-arguments/lifecycle

# Terraform Top-Level Blocks
- Terraform language uses a limited number of top-level-block types, which are blocks that can appear outsire of anyother block in a TF configuration file. 
- Most terraform's features are implemented as top-level blocks. 
- What are terrafomr top level blocks ?
    - Terraform Settings block
    - Provider Block
    - Resource Block
    - Input Variable Block
    - Output variable block
    - Local values block
    - data sources block
    - modules block

- You can catagorise blocks in three catagories
    - Fundamental Blocks
        - Terraform Settings Block
        - Providers Block
        - Resource Block
    - Variables Blocks
        - Input variables block
        - Output values block
        - Local values block
    - Calling/Referencing Blocks
        - Data sources block
        - Modules block



# Fundamental Blocks
## Terraform block
    - Required Terraform version
    - List required providers
    - Terraform backend
    - IMPORTANT NOTE - Only constant values can be used within terraform block. Arguments may not refer to named objects like resources, input variables and may not use    terraform language built-in functions. 

## Provider Block
     - Terraform relies on provider bloack to interact with remote systems
     - Declare providers for Terraform to install providers and user them
     - Provider configs belong to Root Module

## Resource Block
    - Each resource block describes one or more infrastructure objects
    - Resource Syntax - How to declare resources ?
    - Resource Behavior - How Terraform handles resources declarations?
    - provisioners - We can configure resources post-creation actions