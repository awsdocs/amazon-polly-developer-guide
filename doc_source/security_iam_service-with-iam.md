# How Amazon Polly Works with IAM<a name="security_iam_service-with-iam"></a>

Before you use IAM to manage access to Amazon Polly, you should understand what IAM features are available to use with Amazon Polly\. To get a high\-level view of how Amazon Polly and other AWS services work with IAM, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide*\.

**Topics**
+ [Amazon Polly Identity\-Based Policies](#security_iam_service-with-iam-id-based-policies)
+ [Amazon Polly IAM Roles](#security_iam_service-with-iam-roles)

## Amazon Polly Identity\-Based Policies<a name="security_iam_service-with-iam-id-based-policies"></a>

With IAM identity\-based policies, you can specify allowed or denied actions and resources as well as the conditions under which actions are allowed or denied\. Amazon Polly supports specific actions, resources, and condition keys\. To learn about all of the elements that you use in a JSON policy, see [IAM JSON Policy Elements Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) in the *IAM User Guide*\.

### Actions<a name="security_iam_service-with-iam-id-based-policies-actions"></a>

Administrators can use AWS JSON policies to specify who has access to what\. That is, which **principal** can perform **actions** on what **resources**, and under what **conditions**\.

The `Action` element of a JSON policy describes the actions that you can use to allow or deny access in a policy\. Policy actions usually have the same name as the associated AWS API operation\. There are some exceptions, such as *permission\-only actions* that don't have a matching API operation\. There are also some operations that require multiple actions in a policy\. These additional actions are called *dependent actions*\.

Include actions in a policy to grant permissions to perform the associated operation\.

Policy actions in Amazon Polly use the following prefix before the action: `polly:`\. For example, to grant someone permission to delete a Amazon Polly lexicon with the Amazon Polly `DeleteLexicon` API operation, you include the `polly:DeletedLexicon` action in their policy\. Policy statements must include either an `Action` or `NotAction` element\. Amazon Polly defines its own set of actions that describe tasks that you can perform with this service\.

To specify multiple actions in a single statement, separate them with commas as follows:

```
"Action": [
      "polly:action1",
      "polly:action2"]
```

You can specify multiple actions using wildcards \(\*\)\. For example, to specify all actions that begin with the word `Get`, include the following action:

```
"Action": "polly:Get*"
```



To see a list of Amazon Polly actions, see [Actions Defined by Amazon Polly](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awskeymanagementservice.html#awskeymanagementservice-actions-as-permissions) in the *IAM User Guide*\.

### Resources<a name="security_iam_service-with-iam-id-based-policies-resources"></a>

Amazon Polly does not support specifying resource ARNs in a policy\.

### Condition Keys<a name="security_iam_service-with-iam-id-based-policies-conditionkeys"></a>

Amazon Polly does not provide any service\-specific condition keys, but it does support using some global condition keys\. To see all AWS global condition keys, see [AWS Global Condition Context Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html) in the *IAM User Guide*\.

### Examples<a name="security_iam_service-with-iam-id-based-policies-examples"></a>

To view examples of Amazon Polly identity\-based policies, see [Amazon Polly Identity\-Based Policy Examples ](security_iam_id-based-policy-examples.md)\.

## Amazon Polly IAM Roles<a name="security_iam_service-with-iam-roles"></a>

You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in account A can create a role to grant cross\-account permissions to another AWS account \(for example, account B\) or an AWS service as follows:

1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in account A\.

1. Account A administrator attaches a trust policy to the role identifying account B as the principal who can assume the role\. 

1. Account B administrator can then delegate permissions to assume the role to any users in account B\. Doing this allows users in account B to create or access resources in account A\. The principal in the trust policy can also be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

For more information about using IAM to delegate permissions, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\.

The following is an example policy that grants permissions to put and get lexicons as well as to list those lexicons currently available\.

Amazon Polly supports Identity\-based policies for actions at the resource\-level\. In some cases, the resource can be limited by an ARN\. This is true for the `SynthesizeSpeech`, `StartSpeechSynthesisTask`, `PutLexicon`, `GetLexicon`, and `DeleteLexicon` operations\. In these cases, the `Resource` value is indicated by the ARN\. For example: `arn:aws:polly:us-east-2:account-id:lexicon/*` as the `Resource` value specifies permissions on all owned lexicons within the `us-east-2` Region\.

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

However, not all operations use ARNs\. This is the case with the `DescribeVoices`, `ListLexicons`, `GetSpeechSynthesisTasks`, and `ListSpeechSynthesisTasks` operations\.

For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 