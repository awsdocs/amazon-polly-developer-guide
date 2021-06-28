# Step 1: Set Up an AWS Account and Create a User<a name="setting-up"></a>

Before you use Amazon Polly for the first time, complete the following tasks:

1. [Step 1\.1: Sign up for AWS](#setting-up-signup)

1. [Step 1\.2: Create an IAM User](#setting-up-iam)

## Step 1\.1: Sign up for AWS<a name="setting-up-signup"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including Amazon Polly\. You are charged only for the services that you use\.

With Amazon Polly, you pay only for the resources you use\. If you are a new AWS customer, you can get started with Amazon Polly for free\. For more information, see [AWS Free Usage Tier](https://aws.amazon.com/free/)\.

If you already have an AWS account, skip to the next step\. If you don't have an AWS account, perform the steps in the following procedure to create one\.

**To create an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

Note your AWS account ID because you'll need it for the next step\.

## Step 1\.2: Create an IAM User<a name="setting-up-iam"></a>

Services in AWS, such as Amazon Polly, require that you provide credentials when you access them so that the service can determine whether you have permissions to access the resources owned by that service\. The console requires your password\. You can create access keys for your AWS account to access the AWS CLI or API\. However, we don't recommend that you access AWS using the credentials for your AWS account\. Instead, we recommend that you use AWS Identity and Access Management \(IAM\)\. Create an IAM user, add the user to an IAM group with administrative permissions, and then grant administrative permissions to the IAM user that you created\. You can then access AWS using a special URL and that IAM user's credentials\.

If you signed up for AWS, but you haven't created an IAM user for yourself, you can create one using the IAM console\.

The exercises in this guide assume that you have a user \(`adminuser`\) with administrator privileges\. Follow the procedure to create `adminuser` in your account\.





**To create an administrator user and sign in to the console**

1. Create an administrator user called `adminuser` in your AWS account\. For instructions, see [Creating Your First IAM User and Administrators Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

1. A user can sign in to the AWS Management Console using a special URL\. For more information, [How Users Sign In to Your Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_how-users-sign-in.html) in the *IAM User Guide*\.

**Important**  
The Getting Started exercises use the adminuser credentials\. For added security, when building and testing production application we recommend you create a service\-specific administrator user who has permissions for only the Amazon Polly actions\. For an example policy that grants Amazon Polly specific permissions, see [Example 1: Allow All Amazon Polly Actions](security_iam_id-based-policy-examples.md#example-managed-policy-service-admin)\. 

For more information about IAM, see the following:
+ [AWS Identity and Access Management \(IAM\)](https://aws.amazon.com/iam/)
+ [Getting started](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html)
+ [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)

## Next Step<a name="setting-up-next-step-2"></a>

[Step 2: Getting Started \(Console\)](getting-started-console.md)