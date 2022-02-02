# Configure the AWS Provider
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

# creating S3 bucket using Terraform
resource "aws_s3_bucket" "b" {
  bucket = "my-tf-test-bucket"
  acl    = "private"

  tags = {
    Name        = "My bucket"
    Environment = "Dev"
  }
}

# Creating Ec2 using Terraform(Linux Machine)

resource "aws_instance" "app_server" {
  ami           = "ami-08e4e35cccc6189f4"
  instance_type = "t2.micro"

  tags = {
    Name = "Example"
  }
}

# Creating S3 bucket using variables
variable s3-bucket-name {
type = string
}

variable s3-ver {
type = bool
default = false
}

variable s3-acl {
type = string
default = "private"
}

# Varaible file for s3

resource "aws_s3_bucket" "s3bktn" {
  bucket = "var.s3-bucket-name"
  acl    = var.s3-acl

  versioning {
      enabled = var.s3-ver
  }

  tags = {
    Name        = "My bucket"
    Environment = "Dev"
  }
}

# Creating Ec2 using variables

resource "aws_instance" "app_server" {
  ami           = var.ec2ami
  instance_type = var.inst-type

  tags = {
    Name = "Example"
  }
}

# Varaible file for Ec2

variable "ec2ami"{

type = string
default = "ami-08e4e35cccc6189f4"

}
variable "inst-type"{

type = string
default = "t2.micro"
description = "Instance type"

}

