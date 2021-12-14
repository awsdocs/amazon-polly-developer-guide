# Installing and Configuring Amazon Polly for Windows \(SAPI\)<a name="install-voice-plugin2"></a>

To install and configure the Amazon Polly for Windows \(SAPI\) plugin, you need an AWS account\. If you don't have an account, see [Step 1\.1: Sign up for AWS](setting-up.md#setting-up-signup)\. 

**Topics**
+ [Create an IAM User for the AWS Client](#voice-create-iam)
+ [Install the AWS CLI for Windows](#voice-install-cli)
+ [Create a Profile for the AWS Client](#voice-create-profile)
+ [Install the Amazon Polly for Windows Plugin](#voice-verify)

## Create an IAM User for the AWS Client<a name="voice-create-iam"></a>

Before connecting the AWS client to your AWS account, you need to create an Identity and Access Management \(IAM\) user for the client, then attach a permissions policy to that user\. An *IAM user* is a person or application in an AWS account that can make API calls to AWS products\. 

The AWS client uses the Amazon Polly service, so it needs the `AmazonPollyReadOnlyAccess` permissions policy \.

**To create an IAM user**

1. Sign in to the AWS Management Console and open the [IAM console ](https://console.aws.amazon.com/iam/)\. 

1. Choose **Users**\. 

1. Choose **Add User**\. 

1. For **User Name**, enter `polly-windows-user`\. 

1. For **Access Type**, choose **Programmatic access**, then choose **Next: Permissions**\. 

1. Choose **Attach existing policies directly**

1. In the search box, enter `polly`\.

1. Choose **AmazonPollyReadOnlyAccess**\.

1. Choose **Next: Tags**\. 

1. Choose **Next: Review**\. 

1. Choose **Create User**\. 

1. Record the access key ID and secret access key\. You need them to configure the AWS client\. 
**Important**  
 This is the only time you can access these keys, so be sure to record them\.

## Install the AWS CLI for Windows<a name="voice-install-cli"></a>

The AWS Command Line Interface \(AWS CLI\) is an open source tool that enables you to interact with AWS services using commands from the Windows command prompt\. To install the AWS CLI, see [Installing the AWS CLI on Windows](https://docs.aws.amazon.com/cli/latest/userguide/install-windows.html) in the *AWS Command Line Interface User's Guide*\.

## Create a Profile for the AWS Client<a name="voice-create-profile"></a>

The Amazon Polly for Windows plugin requires an AWS profile called `polly-windows`\. This profile ensures that the Amazon Polly engine use the correct account\. 

**To create the `polly-windows` profile for the AWS client**

1. In Windows, open a command prompt\. 

1.  At the command prompt, run the `aws configure --profile polly-windows` command\. 

1.  When prompted for the **AWS Access Key ID** and **AWS Secret Access Key**, enter the values that you saved when you created the IAM user\. 

1.  For **Default region**, enter the name of the desired AWS Region in lower\-case letters\.
**Note**  
Not all Amazon Polly voices and features are available in all AWS Regions\. For more information, see [Feature and Region Compatibility](NTTS-main.md#ntts-regions)\.

1.  For **Default output format**, press **Enter**\. 

1.  At the command prompt, verify the profile by running the `aws --profile polly-windows polly describe-voices` command\. If you have successfully created the profile, the AWS CLI displays a list the available Amazon Polly names\. 

## Install the Amazon Polly for Windows Plugin<a name="voice-verify"></a>

Install the Amazon Polly for Windows plugin by downloading it from Amazon Simple Storage Service \(Amazon S3\) and running the installer\. After you install the plugin, you can use Amazon Polly voices in all Windows application that use the SAPI API\. 

**Note**  
If you are planning to use a neural voice in your SAPI application, ensure that your client is configured for an AWS Region that supports NTTS before installing the Amazon Polly for Windows plugin\. For more information, see [Feature and Region Compatibility](NTTS-main.md#ntts-regions)\. 

**To install the Amazon Polly for Windows plugin**

1. In Windows, download the [plugin\.](samples/AmazonPollyForWindowsSetup.zip) 

1. Unzip the folder\.

1. Run `AmazonPollyForWindowsSetup.exe`\.

1. In the **Control Panel**, search for `speech settings`\.

1. Under **Text\-to\-speech**, for **Voice**, choose an Amazon Polly voice\. 

1. Choose **Preview Voice**\.