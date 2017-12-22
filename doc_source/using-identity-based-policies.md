# Using Identity\-Based Policies \(IAM Policies\) for Amazon Polly<a name="using-identity-based-policies"></a>

This topic provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\) and thereby grant permissions to perform operations on Amazon Polly resources\.

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available to manage access to your Amazon Polly resources\. For more information, see [Overview of Managing Access Permissions to Your Amazon Polly Resources](access-control-overview.md)\. 


+ [Permissions Required to Use the Amazon Polly Console](#console-permissions)
+ [AWS Managed \(Predefined\) Policies for Amazon Polly](#access-policy-aws-managed-policies)
+ [Customer Managed Policy Examples](#access-policy-customer-managed-examples)

The following shows an example of a permissions policy\.

```
{
   "Version": "2012-10-17",
   "Statement": [{
      "Sid": "AllowGet-Delete-ListActions",
      "Effect": "Allow",
      "Action": [
         "polly:GetLexicon",
         "polly:DeleteLexicon",
         "polly:ListLexicons"],
      "Resource": "*"
      }
   ],
    "Statement": [{
      "Sid": "NoOverrideMyLexicons",
      "Effect": "Deny",
      "Action": [
         "polly:PutLexicon"],
      "Resource": "arn:aws:polly:us-east-2:123456789012:lexicon/my*"
      }
   ]
}
```

The policy has two statements:

+ The first statement grants permission for three Polly actions \(`polly:GetLexicon`, `polly:DeleteLexicon`, and `polly:ListLexicons` on any lexicon\. Use of the wildcard character \(\*\) as the resource grants universal permissions for these actions across all regions and lexicons owned by this account\.

+ The second statement explicitly denies permission for one Polly action \(`polly:PutLexicon`\)\. The ARN shown as the resource specifically applies this permission all lexicons that begin with the letters "my" that are in the region `us-east-2`\. 

For a table showing all of the Amazon Polly API operations and the resources that they apply to, see [Amazon Polly API Permissions: Actions, Permissions, and Resources Reference](api-permissions-reference.md)\. 

## Permissions Required to Use the Amazon Polly Console<a name="console-permissions"></a>

For a user to work with the Amazon Polly console, that user must have a minimum set of permissions that allows users to describe the Amazon Polly resources in their AWS account\.

If you create an IAM policy that is more restrictive than the minimum required permissions, the console won't function as intended for users with that IAM policy\.

You don't need to allow minimum console permissions for users that are making calls only to the AWS CLI or the Amazon Polly API\. 

To use the Amazon Polly console, you need to grant permissions to all the Amazon Polly APIs\. There are no additional permissions needed\. The following permissions policy is all that is needed to use the Amazon Polly console\.

```
}
"Version": "2012-10-17",
   "Statement": [{
      "Sid": "Console-AllowAllPollyActions",
      "Effect": "Allow",
      "Action": [
         "polly:*"],
      "Resource": "*"
      }
   ]
}
```

## AWS Managed \(Predefined\) Policies for Amazon Polly<a name="access-policy-aws-managed-policies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These AWS managed policies grant necessary permissions for common use cases so that you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\. 

The following AWS managed policies, which you can attach to users in your account, are specific to Amazon Polly:

+ **AmazonPollyReadOnlyAccess** – Grants read only access to resources, allows listing lexicons, fetching lexicons, listing available voices and synthesizing speech \(including, applying lexicons to the synthesized speech\)\. 

+ **AmazonPollyFullAccess** – Grants full access to resources and all the supported operations\.

**Note**  
You can review these permissions policies by signing in to the IAM console and searching for specific policies there\.

You can also create your own custom IAM policies to allow permissions for Amazon Polly actions and resources\. You can attach these custom policies to the IAM users or groups that require those permissions\. 

## Customer Managed Policy Examples<a name="access-policy-customer-managed-examples"></a>

In this section, you can find example user policies that grant permissions for various Amazon Polly actions\. These policies work when you are using AWS SDKs or the AWS CLI\. When you are using the console, you need to grant permissions to all the Amazon Polly APIs\. This is discussed in [Permissions Required to Use the Amazon Polly Console](#console-permissions)\.

**Note**  
All examples use the us\-east\-2 region and contain fictitious account IDs\.


+ [Example 1: Allow All Amazon Polly Actions](#example-managed-policy-service-admin)
+ [Example 2: Allow All Polly Actions Except DeleteLexicon](#example-managed-policy-full-permissions-no-delete)
+ [Example 3: Allow DeleteLexicon](#example-managed-policy-delete-all-regions)
+ [Example 4: Allow Delete Lexicon in a Specified Region](#example-managed-policy-delete-one-region)
+ [Example 5: Allow DeleteLexicon for Specified Lexicon](#example-managed-policy-delete-specific-lexicon)

### Example 1: Allow All Amazon Polly Actions<a name="example-managed-policy-service-admin"></a>

After you sign up \(see [Step 1\.1: Sign up for AWS](setting-up.md#setting-up-signup)\) you create an administrator user to manage your account, including creating users and managing their permissions\. 

You might choose to create a user who has permissions for all Amazon Polly actions \(think of this user as a service\-specific administrator\) for working with Amazon Polly\. You can attach the following permissions policy to this user\. 

```
{
   "Version": "2012-10-17",
   "Statement": [{
      "Sid": "AllowAllPollyActions",
      "Effect": "Allow",
      "Action": [
         "polly:*"],
      "Resource": "*"
      }
   ]
}
```

### Example 2: Allow All Polly Actions Except DeleteLexicon<a name="example-managed-policy-full-permissions-no-delete"></a>

The following permissions policy grants the user permissions to perform all actions except `DeleteLexicon`, with the permissions for delete explicitly denied in all regions\. 

```
{
   "Version": "2012-10-17",
   "Statement": [{
      "Sid": "AllowAllActions-DenyDelete",
      "Effect": "Allow",
      "Action": [
         "polly:DescribeVoices",
         "polly:GetLexicon",
         "polly:PutLexicon",
         "polly:SynthesizeSpeech",
         "polly:ListLexicons"],
      "Resource": "*"
      }
      {
      "Sid": "DenyDeleteLexicon",
      "Effect": "Deny",
      "Action": [
         "polly:DeleteLexicon"],
      "Resource": "*"
      }
   ]
}
```

### Example 3: Allow DeleteLexicon<a name="example-managed-policy-delete-all-regions"></a>

The following permissions policy grants the user permissions to delete any lexicon that you own regardless of the project or region in which it is located\. 

```
{
  "Version": "2012-10-17",
  "Statement": [{
      "Sid": "AllowDeleteLexicon",
      "Effect": "Allow",
      "Action": [
         "polly:DeleteLexicon"],
      "Resource": "*"
      }
   ]
}
```

### Example 4: Allow Delete Lexicon in a Specified Region<a name="example-managed-policy-delete-one-region"></a>

The following permissions policy grants the user permissions to delete any lexicon in any project that you own that is located in a single region \(in this case, us\-east\-2\)\. 

```
{
  "Version": "2012-10-17",
  "Statement": [{
      "Sid": "AllowDeleteSpecifiedRegion",
      "Effect": "Allow",
      "Action": [
         "polly:DeleteLexicon"],
      "Resource": "arn:aws:polly:us-east-2:123456789012:lexicon/*"
      }
   ]
}
```

### Example 5: Allow DeleteLexicon for Specified Lexicon<a name="example-managed-policy-delete-specific-lexicon"></a>

The following permissions policy grants the user permissions to delete a specific lexicon that you own \(in this case, myLexicon\) in a specific region \(in this case, us\-east\-2\)\. 

```
{
  "Version": "2012-10-17",
  "Statement": [{
      "Sid": "AllowDeleteForSpecifiedLexicon",
      "Effect": "Allow",
      "Action": [
         "polly:DeleteLexicon"],
      "Resource": "arn:aws:polly:us-east-2:123456789012:lexicon/myLexicon"
      }
   ]
}
```