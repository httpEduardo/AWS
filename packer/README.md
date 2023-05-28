# Packer for Vault on AWS Cloudformation

This directory containers packer templates and related scripts for building Vault on AWS. You'll need an S3 Bucket for your install artifcacts (See the --help for install-vault.sh and install-consul.sh for more info.)

Some post launch config needs to be done to make the Vault cluster functional. These steps include setting up Consul ACLs and configuring auto-unseal with AWS KMS. We handle these through UserData scripts.

Note that we disable DEBUG logging which is the default for AWS Cloud Init. DEBUG leaks secrets into the log files.

The packer templates and install_files were copied from here. The scripts were adapted to update our config to support consul 1.4.4.  Once issue #3 is addressed we can go back to using these standard HashiCorp packer templates for Vault and Consul

https://github.com/hashicorp/sm-terraform-aws-vault/
https://github.com/hashicorp/sm-terraform-aws-vault/issues/3
