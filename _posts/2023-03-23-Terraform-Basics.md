---
layout: post
title: Terraform Basics
category: [Terraform]
---

# Table of Contents
<!-- TOC -->

- [Table of Contents](#table-of-contents)
- [Terraform Configuration Syntax](#terraform-configuration-syntax)
- [Arguments, Attributes and Meta-Arguments](#arguments-attributes-and-meta-arguments)
    - [Arguments](#arguments)
    - [Attributes](#attributes)
    - [Meta-arguments](#meta-arguments)
- [Terraform Top-Level Blocks](#terraform-top-level-blocks)
- [Fundamental Blocks](#fundamental-blocks)
    - [Terraform block](#terraform-block)
    - [Provider Block](#provider-block)
    - [Resource Block](#resource-block)
- [Terraform State File](#terraform-state-file)
- [Terraform Dependency Lock File](#terraform-dependency-lock-file)
- [Terraform Desired & Current States](#terraform-desired--current-states)
- [Terraform Variables](#terraform-variables)
    - [Input Variables](#input-variables)
    - [Output Variables](#output-variables)
    - [Local Variables](#local-variables)

<!-- /TOC -->

- Terraform uses HCL - Hashicorp Language
- Code in Terraform langugae is stored in plain text files with .tf file extension.
- There is also a JSON-based variant of the language that is name with .tf.json  file extension.
- All the files containing terraform code is known as **Terraform Configuration Files** or **Terraform Manifests**


# Terraform Configuration Syntax
- Terraform language consist of mainly 4 parts

1. Blocks 
    - Block is a container for the content like resources, providers, configs etc. 
      
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

# Terraform State File
- Terraform state file is creted after issuing terraform apply" and once infrastructed is cretaed on cloud.
- It stores state about your managed infrastructe and configureation
- This state is used by Terraform to map real world resources to your configuration (.tf files), keep track of metadata and to improve performance for large infrastructure
- This state is stored by default in a local file named "terraform.tfstate", but it can also be stored remotely for team environment. 
- if you delete state file by mistake, Terraform will assume it hasn't created any state and will try to create it again and you will end up with duplicate resources
- you can try using terraform.tfstate.backup file to simplify recovery. 
- Best place to store tfstate will be on a s3 bucket with version control enabled. 

# Terraform Dependency Lock File
- Every terraform project has external dependencies on code that does not exist within the project itself.
- These dependencies rely on terraform providers and modules that may exist outside of the code base. 
- There are two dependency types
    - Terraform providers - These are the plugins that required to work with external systems such as AWS. e.g required provider version, required terraform version
    - Terraform modules   - These are reusabe groups of terraform code hosted on terraform registry. 
 
# Terraform Desired & Current States
- Desired state is Terraform configuration file ( or tf files)
- Current State is deployed real world resources. 
- Terraform stat keeps track of current state config and gets updated when desired state configs are deployed. 

# Terraform Variables
- There are three type of variables used in terraform

## Input Variables 
- Serves as parameters for a terraform module, allowing aspects for module to be customized without altering the module's own source code and allowing modules to be shared between different configurations. 
- There are multiple ways to pass variale values
    - Basics
    - When prompted during terraform plan or apply
    - Override default variable using cli argument -var
    - Overrise default variable values using env variables (TF_var_aa)
    - Provide input variables using terraform.tfvars files
    - Provide input variables using <any-name>.tfvars file with CLI argument -var-file
    - Provide input variables using auto.tfvars files
    - List and Map
    - Implement custom validation rules in variables
    - Protect Sensitive input variables

## Output Variables
- Output variables are like return values of a terraform module and have severa uses
- A root module can use output to print values in the CLI output after running terraform apply. 
- A chils module can use outputs to expose a subset of its resource attrivute to a parent module
- when using remote state, root module outputs can be accesses by other configurations via terraform_remote_state data source

## Local Variables