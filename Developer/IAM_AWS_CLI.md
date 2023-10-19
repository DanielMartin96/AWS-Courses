# IAM & AWS CLI
## Users, Groups, Policies

### Users & Groups
- IAM = Identity and Access Management, **global** service
- **Root account** created by default, shouldn't be used or shared
- **Users** are people within your organisation and can be grouped
- **Groups** only contain users, not other groups
- Users don't have to belong to a group and users can belong to multiple groups

### Policies
- **Users or Groups** can be assigned JSON documents called policies
- These policies define the **permissions** of the users
- In AWS you apply the **least privilege principle:** don't give more permissions than a user needs

## IAM Policies

### IAM Policies Structure
- **Version:** policy language version, always include "2012-10-17"
- **Id:** an indentifier for the policy (optional)
- **Statement:** one or more individual statements (required)
  Statements consist of
- **Sid:** an identifier for the statement (optional)
- **Effect:** whether the statement allows or denies access (Allow, Deny)
- **Principal:** account/user/role to which this policy is applied to
- **Action:** list of actions this policy allows or denies
- **Resource:** list of resources to which the actions applied to
- **Condition:** conditions for when this policy is in effect (optional)

## MFA Overview 

### Password Policy
- Strong passwords = higher security in your account
In AWS, you can setup a password policy:
- Set a minimum password length
- Require specific character types
- Allow all IAM users to change their own passwords
- Require users to change their password after some time (password expiration)
- Prevent password re-use

### Multi Factor Authentication - MFA
- Users have access to your account and can possibly change configurations or delete resources in your AWS account
- **You want to protect your Root Accounts and IAM users**
- MFA = password *you know* + security device *you own*
- If a password is stolen or hacked, the account is not compromised

### MFA devices options in AWS
- Virtual MFA device
- Universal 2nd Factor (U2F) Security Key
- Hardware Key Fob MFA Device
- Hardware Key Fob MFA Device for AWS GovCloud (US)

## AWS Access Keys, CLI and SDK

### How can users access AWS?
- AWS Management Console (protected by password + MFA)
- AWS Command Line Interface (protected by access keys)
- AWS Software Development Kit (protected by access keys)
- Access Keys are generated through the AWS Console
- Users manage their own access keys
- **Access Keys are secret, just like a password. Don't share them**
- Access Key ID ~= username
- Secret Access Key ~= password

## IAM Roles for AWS Services
- Some AWS service will need to perform actions on your behalf
- To do so, we will assign **permissions** to AWS services with **IAM Roles**
- EC2 Instance Roles
- Lambda Function Roles
- Roles for CloudFormation

## IAM Security Tools

### IAM Credentials Report (account-level)
- A report that lists all your account's users and the status of their various credentials 

### IAM Access Adviser (user-level)
- shows the service permissions granted to a user when those services were last accessed

## IAM Best Practices 
- Don't use root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions to groups
- Create a **strong password policy**
- Use and enforce the use of **Multi Factor Authentication (MFA)**
- Create and use **Roles** for giving permissions to AWS services
- Use Access Keys for Programmatic Access (CLI/SDK)
- Audit permissions of your account using IAM Credentials Report & IAM Access Adviser
- **Never share IAM users & Access Keys**

## Shared Responsibility for IAM

### AWS
- Infrastructure (global network security)
- Configuration and vulnerability analysis
- Compliance validation

### You
- Users, Groups, Roles, Policies management and monitoring
- Enable MFA on all accounts
- Rotate all your keys often
- Use IAM tools to apply appropriate permissions
- Analyse access patterns & review permissions

## Summary
- **Users:** mapped to a physical user, has a password for AWS Console
- **Groups:** contains users only
- **Policies:** JSON document that outlines permissions for users or groups
- **Roles:** for EC2 instances or AWS services
- **Security:** MFA + Password Policy
- **AWS CLI:** manage your AWS services using the command-line
- **AWS SDK:** manage your AWS services using a programming langauge
- **Audit:** IAM Credentials Reports & IAM Access Adviser
- **Access Keys:** access AWS using the CLI or SDK
