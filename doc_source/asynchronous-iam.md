# Setting Up the IAM Policy for Asynchronous Synthesis<a name="asynchronous-iam"></a>

In order to use the asynchronous synthesis functionality, you will need an IAM policy that allows the following: 
+ use of new Amazon Polly operations
+ writing to the output S3 bucket
+ publishing to the status SNS topic \[optional\] 

The following policy grants only the necessary permissions required for asynchronous synthesis and can be attached to the IAM user\. 

```
{
  "Version": "2012-10-17",
  "Statement": [
    {  
      "Effect": "Allow",
      "Action": [
        "polly:StartSpeechSynthesisTask",
        "polly:GetSpeechSynthesisTask",
        "polly:ListSpeechSynthesisTasks"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::bucket-name/*"
    },
    {
      "Effect": "Allow",
      "Action": "sns:Publish",
      "Resource": "arn:aws:sns:region:account:topic"
    }
  ]
}
```