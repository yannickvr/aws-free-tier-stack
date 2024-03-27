# aws-free-tier-stack
Everything you need to get started safely on the AWS free tier

The AWS Free Tier Stack is a CloudFormation stack that contains everything a new user of AWS needs to safely start using AWS. It contains tools and configuration that helps you in managing budgets and basic security configuration.

All configuration done by this stack should easily fit in the free tier itself. This means that for example, the SNS topic we use does not use encryption, because that would require use of a KMS key. Also, the stack should be a one-click install: no packaging and building lambda functions please.

## Installation

- Download `stack.yml`
- Log in to your AWS account, and open the CloudFormation service in your region (e.g. https://eu-west-1.console.aws.amazon.com/cloudformation)
- Create Stack
    - With new resources
    - Upload a template file
    - Select the downloaded template
    - Follow the wizard.
- ***You will get an email on the email address(ses) entered. Make sure to accept the subscription, or alerts will not be sent!***

## Contents

These services are configured.

### SNS Topic

- SNS Topic with a list of email subscribers that get alarms and notifications

### AWS Budgets

- Sends alarms when a pre-set daily, weekly or monthly budget is passed.
    - Currently just a daily amount configured

### Root User Alarms

- Send a notice every 24 hours if root user..
    - does not have MFA configured
    - access keys are set
- (In Progress) Send a notice whenever the root user is used
    - This is already in the code as Eventbridge Event, but also requires CloudTrail to be configured

### (TBD) CloudTrail

- Creates a CloudTrail-trail
- Monitors if there are more than 1 trails in (any) region
