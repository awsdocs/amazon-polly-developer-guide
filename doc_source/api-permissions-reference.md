# Amazon Polly API Permissions: Actions, Permissions, and Resources Reference<a name="api-permissions-reference"></a>

When you are setting up [Access Control](authentication-and-access-control.md#access-control) and writing a permissions policy that you can attach to an IAM identity \(identity\-based policies\), you can use the following table as a reference\. The table lists each Amazon Polly API operation, the corresponding actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

You can use AWS\-wide condition keys in your Amazon Polly policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `polly` prefix followed by the API operation name \(for example, `polly:GetLexicon`\)\.

If you see an expand arrow \(**↗**\) in the upper\-right corner of the table, you can open the table in a new window\. To close the window, choose the close button \(**X**\) in the lower\-right corner\.


**Amazon Polly API and Required Permissions for Actions**  

| Amazon Polly API Operations | Required Permissions \(API Actions\) | Resources | 
| --- | --- | --- | 
|  [DeleteLexicon](API_DeleteLexicon.md)  |  `polly:DeleteLexicon`  |  `arn:aws:polly:region:account-id:lexicon/LexiconName`  | 
|  [DescribeVoices](API_DescribeVoices.md)  |  `polly:DescribeVoices`  |  `*`  | 
|  [GetLexicon](API_GetLexicon.md)  |  polly:GetLexicon  |  `arn:aws:polly:region:account-id:lexicon/LexiconName`  | 
|  [ListLexicons](API_ListLexicons.md)  |  `polly:ListLexicons`  |  `arn:aws:polly:region:account-id:lexicon/*`  | 
|  [PutLexicon](API_PutLexicon.md)  |  `polly:PutLexicon`  |  `*`  | 
|  [SynthesizeSpeech](API_SynthesizeSpeech.md)  |  `polly:SynthesizeSpeech`  |  `*`  | 

Amazon Polly supports Identity\-based policies for actions at the resource\-level\. Therefore, the `Resource` value is indicated by the ARN\. For example: `arn:aws:polly:us-east-2:account-id:lexicon/*` as the `Resource` value specifies permissions on all owned lexicons within the `us-east-2`region\.

Because Amazon Polly doesn't support permissions for actions at the resource\-level, most policies specify a wildcard character \(\*\) as the `Resource` value\. However, if it is necessary to limit permissions to a specific region this wildcard character is replaced with the appropriate ARN: `arn:aws:polly:region:account-id:lexicon/*. ` 