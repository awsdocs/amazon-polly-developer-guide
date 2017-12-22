# Overview of Managing Access Permissions to Your Amazon Polly Resources<a name="access-control-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\), and some services \(such as AWS Lambda\) also support attaching permissions policies to resources\. 

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific actions that you want to allow on those resources\.


+ [Amazon Polly Resources and Operations](#access-control-resources)
+ [Understanding Resource Ownership](#access-control-resource-ownership)
+ [Managing Access to Resources](#manage-access-overview)
+ [Specifying Policy Elements: Actions, Effects, and Principals](#specify-policy-elements)
+ [Specifying Conditions in a Policy](#specifying-conditions-overview)

## Amazon Polly Resources and Operations<a name="access-control-resources"></a>

In Amazon Polly, the primary resource is *a lexicon*\. In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource that the policy applies to\.

These resources and subresources have unique Amazon Resource Names \(ARNs\) associated with them, as shown in the following table\. 


****  

| Resource Type | ARN Format | 
| --- | --- | 
| Lexicon | arn:aws:polly:region:account\-id:lexicon/LexiconName | 

Amazon Polly provides a set of operations to work with Amazon Polly resources\. For a list of available operations, see Amazon Polly [Amazon Polly API Reference](API_Reference.md)\.

## Understanding Resource Ownership<a name="access-control-resource-ownership"></a>

The AWS account owns the resources that are created in the account, regardless of who created the resources\. Specifically, the resource owner is the AWS account of the [principal entity](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html) \(that is, the root account, an IAM user, or an IAM role\) that authenticates the resource creation request\. The following examples illustrate how this works:

+ If you use the root account credentials of your AWS account to create a lexicon, your AWS account is the owner of the resource \(in Amazon Polly, the resource is a lexicon\)\.

+ If you create an IAM user in your AWS account and grant permissions to create a lexicon to that user, the user can create a lexicon\. However, your AWS account, to which the user belongs, owns the lexicon resource\.

+ If you create an IAM role in your AWS account with permissions to create a lexicon, anyone who can assume the role can create a lexicon\. Your AWS account, to which the user belongs, owns the lexicon resource\. 

## Managing Access to Resources<a name="manage-access-overview"></a>

A *permissions policy* describes who has access to what\. The following section explains the available options for creating permissions policies\.

**Note**  
This section discusses using IAM in the context of Amazon Polly\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](http://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies attached to an IAM identity are referred to as *identity\-based* policies \(IAM polices\) and policies attached to a resource are referred to as *resource\-based* policies\. Amazon Polly supports identity\-based policies\. 


+ [Identity\-Based Policies \(IAM Policies\)](#manage-access-iam-policies)
+ [Resource\-Based Policies](#manage-access-resource-policies)

### Identity\-Based Policies \(IAM Policies\)<a name="manage-access-iam-policies"></a>

You can attach policies to IAM identities\. For example, you can do the following:

+ **Attach a permissions policy to a user or a group in your account** – To grant a user permissions to create a Amazon Polly resource, such as a lexicon, you can attach a permissions policy to a user or group that the user belongs to\.

+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in account A can create a role to grant cross\-account permissions to another AWS account \(for example, account B\) or an AWS service as follows:

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in account A\.

  1. Account A administrator attaches a trust policy to the role identifying account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in account B\. Doing this allows users in account B to create or access resources in account A\. The principal in the trust policy can also be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

  For more information about using IAM to delegate permissions, see [Access Management](http://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\.

The following is an example policy that grants permissions to put and get lexicons as well as to list those lexicons currently available\.

Amazon Polly supports Identity\-based policies for actions at the resource\-level\. Therefore, the `Resource` value is indicated by the ARN\. For example: `arn:aws:polly:us-east-2:account-id:lexicon/*` as the `Resource` value specifies permissions on all owned lexicons within the `us-east-2` region\.

```
{
   "Version": "2012-10-17",
   "Statement": [{
      "Sid": "AllowPut-Get-ListActions",
      "Effect": "Allow",
      "Action": [
         "polly:PutLexicon",
         "polly:GetLexicon",
         "polly:ListLexicons"],
      "Resource": "arn:aws:polly:us-east-2:account-id:lexicon/*"
      }
   ]
}
```

For more information about using identity\-based policies with Amazon Polly, see [Using Identity\-Based Policies \(IAM Policies\) for Amazon Polly](using-identity-based-policies.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](http://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-Based Policies<a name="manage-access-resource-policies"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. Amazon Polly doesn't support resource\-based policies\.

## Specifying Policy Elements: Actions, Effects, and Principals<a name="specify-policy-elements"></a>

For each Amazon Polly resource, the service defines a set of API operations\. To grant permissions for these API operations, Amazon Polly defines a set of actions that you can specify in a policy\. Some API operations can require permissions for more than one action in order to perform the API operation\. For more information about resources and API operations, see [Amazon Polly Resources and Operations](#access-control-resources) and [Amazon Polly API Reference](API_Reference.md)\.

The following are the most basic policy elements:

+ **Resource** – You use an Amazon Resource Name \(ARN\) to identify the resource that the Identity\-based policy applies to\. For more information, see [Amazon Polly Resources and Operations](#access-control-resources)\.

+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, you can use `polly:PutLexicon` to add a lexicon to the region\.

+ **Effect** – You specify the effect, either allow or deny, when the user requests the specific action\. If you don't explicitly grant access to \(allow\) a resource, access is implicitly denied\. You can also explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.

+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. For resource\-based policies, you specify the user, account, service, or other entity that you want to receive permissions \(applies to resource\-based policies only\)\. Amazon Polly doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table showing all of the Amazon Polly API operations and the resources that they apply to, see [Amazon Polly API Permissions: Actions, Permissions, and Resources Reference](api-permissions-reference.md)\.

## Specifying Conditions in a Policy<a name="specifying-conditions-overview"></a>

When you grant permissions, you can use the access policy language to specify the conditions when a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to Amazon Polly\. However, there are AWS\-wide condition keys that you can use as appropriate\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\.