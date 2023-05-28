# vault-aws-cloudformation

NOTE: This repository is not being actively maintained. Contact your HashiCorp representative or community leader for the latest on installing Vault on AWS.

## Introduction

This repository contains code for building Amazon Machine Images (AMI) and a generic Cloudformation template. The AMI and template can be used to spin up a production-ready Vault cluster.

## What does it build?

The Cloudformation templates published by this pipeline stand up the following configuration:

- VPC with 3 public and 3 private subnets
- Operating system for Vault and Consul is Centos 7
- Operating system for the Bastion host is AWS Linux (latest)
- 3 Vault servers and 5 Consul servers distributed across the private subnets
- A bastion host for connecting to the other servers, which are not directly accessible from the Internet
- A real SSL certificate tied to your FQDN, managed by Amazon Certificate Manager
- Automatic unsealing of Vault using AWS Key Management Service to store the unseal key
- The Vault cluster will be ready in 10-15 minutes. The cluster comes up in an uninitialized state. The API listens on port 8200 and is accessible from the Internet.

## Instructions for use

* Build AMIs for Vault and Consul using the included Packer templates. 
* Edit the cloudformation/aws_vault_cf.yml file and insert your new values for the AMIs.
* OPTIONAL: Have a domain (or subdomain) that you own in AWS Route 53 management. This allows you to automate the creation of DNS records that point at your Vault cluster. It also allows you to automatically validate the SSL certificate.
* Use the AWS Cloudformation UI to upload your aws_vault_cf.yml file, fill in all the necessary values and create a new stack. Make sure and verify the DNS record that you used for the Vault cluster in Route 53 (or by creating a DNS TXT record in your own DNS provider).
* After about 15 minutes your Vault cluster will be ready for initial setup. You can use 1 and 1 for the initial key shares and recovery shares. Save the initial root token and recovery key in a safe place.
* Log onto your Vault cluster using the root token and configure Vault. 
# AWS
