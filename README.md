# Kepler RHEL Demo

This repository contains the necessary files to deploy a demo of Kepler
on RHEL 9.

## Prerequisites

- An AWS Account
- You are logged in with the `aws` CLI
- You have a key pair in the region you are deploying to

# Instructions

Deploy the VMs, passing the name of your keypair and the region you want to
deploy to as extra vars.

```bash
 ansible-playbook -vv --extra-vars "setup_ec2_aws_region=eu-west-1" --extra-vars "setup_ec2_aws_key_name=dave-kepler-demo"  deploy-ec2.yml
```

> Note: Ensure your AWS region is set correctly in the `inventory.aws_ec2.yml` file.

Deploy Kepler to the VMs, passing the private key for your AWS keypair
as the `--private-key` argument.

```bash
 ansible-playbook -i inventory.aws_ec2.yml -u ec2-user --private-key ~/.ssh/dave-kepler-demo.pem kepler.yml
```

And then finally deploy some workloads to be monitored:

```bash
 ansible-playbook -i inventory.aws_ec2.yml -u ec2-user --private-key ~/.ssh/dave-kepler-demo.pem workloads.yml
```
