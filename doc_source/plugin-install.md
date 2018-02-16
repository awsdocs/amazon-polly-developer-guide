# Installing the Plugin<a name="plugin-install"></a>

Setting up the Amazon Polly plugin for WordPress requires that you have an active AWS account in addition to your working WordPress installation\. If you don't have an account, see [Step 1\.1: Sign up for AWS](setting-up.md#setting-up-signup)\. When you have an AWS account, follow these steps to finish setting up the plugin: 

1. [Create a Permissions Policy](#wp-permissions)

1. [Create an IAM User for the Plugin](#wp-account)

1. [Installing and Configuring the Plugin](#wp-install)

## Create a Permissions Policy<a name="wp-permissions"></a>

In the [AWS Management Console](https://console.aws.amazon.com/), create an IAM permissions policy called *PollyForWordPressPolicy* using the following code:

```
{
    "Version": "2012-10-17",
    "Statement": [use
        {
            "Sid": “Permissions1”,
            "Effect": "Allow",
            "Action": [
                "polly:SynthesizeSpeech",
                "s3:HeadBucket",
                "polly:DescribeVoices"
            ],
           "Resource": "*"
        },
        {
            "Sid": "Permissions2”,
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket",
                "s3:GetBucketAcl",
                "s3:GetBucketPolicy",
                "s3:PutObject”,
                                "s3:DeleteObject”,
                "s3:CreateBucket",
                "s3:PutObjectAcl"
            ],
            "Resource": "arn:aws:s3:::audio_for_wordpress*"
        }
    ]
}
```

For more information on creating a permissions policy, see [Creating Customer\-Managed Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_managed-policies.html)\.

## Create an IAM User for the Plugin<a name="wp-account"></a>

To connect the plugin to your AWS account, you need to create an AWS Identity and Access Management \(IAM\) user, then attach the permissions policy to that user\. If you deployed WordPress on Amazon EC2, you can skip this step and use the IAM role instead of an individual IAM user\. For more information, see: [IAM Roles for Amazon EC2](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html) in the *Amazon EC2 User Guide*\. 

**To create an IAM user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/) and choose **Users**\. 

1. Choose **Add User**\.

1. For **User Name**, type **WordPress**\. 

1. For **Access Type**, choose **Programmatic access**, then choose **Next: Permissions**\.

1. Choose **Attach existing policies direction**\. Choose your newly created policy \(*PollyForWordPressPolicy*\) from the list, then choose **Next: Review**\.

1. Choose **Create User**\.

1. Copy the **Access key ID** and **Secret access key**\. You need them to configure the plugin\.
**Important**  
This is the only time you can access these keys, so be sure to record them\.

## Installing and Configuring the Plugin<a name="wp-install"></a>

**To install and configure the plugin**

1. Download the Amazon Polly plugin for WordPress from the [Amazon Polly plugin GitHub site](https://github.com/awslabs/amazon-polly-wordpress-plugin)\. 

1. On the **WordPress Admin** page, choose **Add New Plugin**, then install and activate the plugin\. 

1. On the **WordPress Admin** page, choose **Settings**, then for **Amazon Polly Settings**, configure the plugin: 

   + **AWS access key and AWS secret key**—AWS credentials, which allow the plugin to use Amazon Polly and Amazon Simple Storage Service \(Amazon S3\)\. If you are hosting your WordPress site on Amazon Elastic Compute Cloud \(Amazon EC2\), you can use AWS Identity and Access Management \(IAM\) roles instead of credentials\. In that case, leave these two fields blank\.

   + **Sample rate**—The sample rate of the audio files that will be generated, in Hz\. Higher sampling rates mean higher quality audio\.

   + **Voice name**—The Amazon Polly voice to use to create the audio file\.

   + **Player position**—Where to position the audio player on the website\. You can put it before or after the post, or not use it at all\. If you want to make your files available as podcasts, using Amazon Pollycast, choose to not display the audio player\. 

   + **New post default**—Specifies whether Amazon Polly is automatically enabled for all new posts\. Choose this option if you want Amazon Polly to use the configuration settings to create an audio file for each new post\.

   + **Autoplay**—Specifies whether the audio player automatically starts playing the audio when a user visits an individual post on the website\. 

   + **Store audio in Amazon S3**—If you want to store audio files in an S3 bucket instead of on the server, choose this option\. Amazon Polly creates the bucket for you\. For more information and pricing, see [Amazon S3](https://aws.amazon.com/s3)\.

   + **Amazon CloudFront \(CDN\) domain name**—If you want to broadcast your audio files with Amazon CloudFront, provide the name of your CloudFront domain, which the plugin will use for streaming audio\. You must first create the domain in Amazon CloudFront\. 

   + **ITunes category**—The category for your podcast\. Choosing a category makes it easier for podcast users to find your podcast in the podcast catalog\.

   + **ITunes explicit**—Specifies whether to enable Amazon Pollycast podcasting\. 

   + **Bulk update all posts**—If you want to convert all posts to use the new plugin settings, choose this option\. 

1. Choose **Save Changes**