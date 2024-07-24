
# DET-32 & IP-73: Automatically Revert and Receive Notifications About Changes to AWS VPC Security Groups

## Best Practice
Receive Notification when Security Group Configuration changes are made. Example Includes creating, deleting, modifying SG changes. Controls to ensure that no Security Groups allow ingress from 0.0.0.0/0 to port 22 and 3389

## Description
Ensure there is CloudWatch alarm created and configured in the AWS account to fire each time a security groups configuration change is made. This CloudWatch alarm must be triggered every time an AWS API call is performed to update security groups. This script monitors and manages security group (SG) ingress rule changes in AWS. It uses AWS CloudWatch to detect changes, a Lambda function to evaluate and revert unauthorized changes, and sends email notifications about the actions taken.

## Control Type
Control Type : Detection & Infrastructure Protection


## Architecture
![Architecture Diagram](./images/architecture-diagram.png)

1. **New ingress rule**: A new ingress rule is added to a security group.
2. **CloudWatch event**: A CloudWatch event monitors changes in the security group and detects the new ingress rule, triggering a designated Lambda function.
3. **Lambda function evaluation**: The Lambda function evaluates the event to determine if it is monitoring the security group and reverts the new SG changes if necessary.
4. **Email notification**: The Lambda function sends an email notification detailing the change, the person who made it, and confirmation that the change was reverted.

## Installation
1. Clone the repository:
   ```sh
   git clone git@gitlab.com:toyotaconnectedindia/secops/aws-security-improvement-program/aws-security-group-automation.git
   ```
2. Navigate to the project directory:
   ```sh
   cd <project_directory>
   ```
3. Set up the required AWS resources (CloudWatch, Lambda function, etc.):
   ```sh
   # Log in to AWS tcin infosec account
   # Use the code to deploy as a template in order to create a cloud formation stackset inside it in ap-south-1 region
   # Add stacks to stackset by selecting multiple OU ids and target accounts to deploy
   # Add the sns topic as 'tcin-cloud-security@toyotaconnected.co.in'
   # Review and enable it
   ```
