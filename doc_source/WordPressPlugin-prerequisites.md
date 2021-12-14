# Installation Prerequisites<a name="WordPressPlugin-prerequisites"></a>

To use the AWS for WordPress plugin, you need an AWS account, an AWS Identity and Access Management \(IAM\) user, and a WordPress website\.

**Topics**
+ [Creating an AWS Account](#WordPressPlugin-prerequisites-AWS)
+ [Creating an IAM User](#WordPressPlugin-prerequisites-IAM-user)
+ [Creating a WordPress Website](#WordPressPlugin-prerequisites-WordPress)

## Creating an AWS Account<a name="WordPressPlugin-prerequisites-AWS"></a>

If you have an AWS account already, you can skip this section\. Otherwise, create one\.<a name="setting-up-sign-up-for-aws-procedure"></a>

**To create an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

## Creating an IAM User<a name="WordPressPlugin-prerequisites-IAM-user"></a>

To use the AWS for WordPress plugin, you must create an *IAM user* for the plugin\. An IAM user is a person or application under an AWS account that has permission to make API calls to AWS services\.

**Note**  
If you don't use [WordPress\.com](https://wordpress.com/) and instead have a self\-hosted WordPress website on Amazon EC2, you can use an IAM role instead of an IAM user\. For more information, see [IAM Roles for Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html) in the *Amazon EC2 User Guide*\.

The following procedure contains the steps to create an IAM *policy*, and then attach it to the IAM user\. An IAM policy is a document that defines the permissions that apply to the user\.

**To create an IAM user**

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Policies**\. Then choose **Create policy**\.

1. Choose **JSON**\.

1. Delete everything in the policy text box, and then paste or enter the following JSON policy into the text box:

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": "acm:DeleteCertificate",
               "Resource": "*",
               "Condition": {
                   "StringEquals": {
                       "aws:RequestedRegion": "us-east-1"
                   }
               }
           }
       ]
   }
   ```

1. Choose **Review policy**\.

1. On the **Review policy** page, do the following:

   1. For **Name**, enter **AWSForWordPressDeleteCert**\.

   1. Choose **Create policy**\.

1. In the navigation pane, choose **Users**\. Then choose **Add user**\.

1. On the **Set user details** page, do the following:

   1. For **User name**, enter **AWSForWordPressPlugin**\.

   1. For **Access type**, choose **Programmatic access**\.

   1. Choose **Next: Permissions**\.

1. On the **Set permissions** page, do the following:

   1. Choose **Attach existing policies directly**\.

   1. In the search box, enter **WordPress**, and then select the check boxes next to **AWSForWordPressPolicy** and **AWSForWordPressDeleteCert**\. Make sure to select the check boxes for both WordPress policies\.
**Note**  
The *AWSForWordPressPolicy* is an AWS managed policy that gives the user permission to use all the features included in the AWS for WordPress plugin\. When new features are added to the plugin, AWS will update this policy to include the permissions necessary to use the new features\.

   1. Choose **Next: Tags**\.

1. Choose **Next: Review**\.

1. Choose **Create user**\.

1. Choose **Download \.csv** to save the user's credentials \(access key ID and secret access key\) to your computer\. You need them to configure the AWS for WordPress plugin\.
**Important**  
This is the only time that you can save the user's secret access key, so make sure to save it now\.

## Creating a WordPress Website<a name="WordPressPlugin-prerequisites-WordPress"></a>

If you have a WordPress website already, you can skip ahead to [Installing and Configuring the Plugin](WordPressPlugin-install.md)\.

If you don't have a WordPress website, you can create one using [WordPress\.com](https://wordpress.com/)\. To use the AWS for WordPress plugin, you need a WordPress\.com Business or eCommerce plan\.

You can also install the WordPress software on your own web server, using Amazon Lightsail, Amazon EC2, or another web hosting platform\. Hosting your own WordPress website involves more steps than using WordPress\.com, and requires the ability to configure and manage a web server, a load balancer, DNS records, and web server certificates\.

Regardless of how you set up your WordPress website, you need the following before you can use the AWS for WordPress plugin:
+ Your website must have its own *domain name*\. A domain name, also known as a *web address* or a *URL \(uniform resource locator\)*, is the address that visitors use to go to your website\. For example, Amazon's domain name is *amazon\.com*\. In this topic, we use *example\.com* as a generic example domain name, but you need a custom domain name for your website\.
+ Your website must work using HTTPS\. This is a security best practice, and the plugin assumes that your website works using HTTPS\. To check, go to your website's address using HTTPS \(for example, ***https**://example\.com*\) and make sure that your website displays correctly\.

When your website has a domain name and works using HTTPS, proceed to the following section\.