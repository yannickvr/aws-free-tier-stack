# The AWS free tier stack
Everything you need to get started safely on the AWS free tier

The AWS Free Tier Stack is a CloudFormation stack that contains everything a new user of AWS needs to safely start using AWS. It contains tools and configuration that helps you in managing budgets and basic security configuration.

All configuration done by this stack should easily fit in the free tier itself. This means that for example, the SNS topic we use does not use encryption, because that would require use of a KMS key. Also, the stack should be a one-click install: no packaging and building lambda functions please.

## Installation

*note: this stack must be installed in the `us-east-1` region.

- Log in to your AWS account
- [Click this link *while pressing CTRL* to install the stack](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?templateURL=https://aws-free-tier-stack.s3.eu-west-1.amazonaws.com/stack.yml&stackName=aws-free-tier-stack)
- Update the daily budget amount.
- Update the email address(ses, comma separated)
- Acknowledge the required access capabilities
- Press `Create Stack`
- ***You will get an email on the email address(ses) entered. Make sure to accept the subscription, or alerts will not be sent!***

## Features

- SNS Topic with a list of email subscribers that get alarms and notifications
- AWS Budgets
    - Sends alarms when a pre-set daily, weekly or monthly budget is passed.
        - Currently just a daily amount configured
- Root User Alarms
    -  Send a notice every 24 hours if root user..
        - does not have MFA configured
        - access keys are set
    - (MVP) Send a notice whenever the root user is used
        - This is already in the code as Eventbridge Event and forwarded to SNS
            - Looking into sending this to the lambda and creating a readable event
- CloudTrail
    - Creates a CloudTrail-trail
    - (Planned) Monitors if there are more than 1 trails in (any) region


## FAQ

### Why is this called the "aws free tier" stack? I dont see anything to do with the free tier
Because this stack aims to solve some issues that people have that rely on the free tier, and are new users to AWS. It monitors some basic security features and sets up some basic cost monitoring. On online platforms there are many first time users who's accounts are compromised or accidentally run something that they can't afford. This stack should help reduce the blast radius.

### Why are you using CloudFormation and not CDK, Terraform or something else?
Because CloudFormation has the best new-user experience. Just click the link and follow the wizard. As this stack is created for new users, this is the best solution

### Why does the stack need to be deployed in US-EAST-1?
Some services, like IAM, only publish their events in US-EAST-1. As we want to monitor these services, we need to deploy resources in that region.

### I've got some ideas, can I help?
Yes! Feel free to open an issue or a PR
