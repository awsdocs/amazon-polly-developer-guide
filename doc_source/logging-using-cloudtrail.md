# Logging Amazon Polly API Calls with AWS CloudTrail<a name="logging-using-cloudtrail"></a>

Amazon Polly is integrated with CloudTrail, a service that captures all of the Amazon Polly API calls and delivers the log files to an Amazon S3 bucket that you specify\. CloudTrail captures API calls from the Amazon Polly console or from your code to the Amazon Polly APIs\. Using the information collected by CloudTrail, you can determine the request that was made to Amazon Polly, the source IP address from which the request was made, who made the request, when it was made, and so on\. 

To learn more about CloudTrail, including how to configure and enable it, see the [AWS CloudTrail User Guide](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

## Amazon Polly Information in CloudTrail<a name="parrot-info-in-cloudtrail"></a>

When CloudTrail logging is enabled in your AWS account, API calls made to Amazon Polly actions are tracked in CloudTrail log files, where they are written with other AWS service records\. CloudTrail determines when to create and write to a new file based on a time period and file size\.

All Amazon Polly actions are logged by CloudTrail and are documented in the [Amazon Polly API Reference](API_Reference.md)\. The following actions are supported\.

+ [DeleteLexicon](API_DeleteLexicon.md)

+ [DescribeVoices](API_DescribeVoices.md)

+ [GetLexicon](API_GetLexicon.md)

+ [ListLexicons](API_ListLexicons.md)

+ [PutLexicon](API_PutLexicon.md)

+ [SynthesizeSpeech](API_SynthesizeSpeech.md)

Every log entry contains information about who generated the request\. The user identity information in the log entry helps you determine the following: 

+ Whether the request was made with root or IAM user credentials

+ Whether the request was made with temporary security credentials for a role or federated user

+ Whether the request was made by another AWS service

For more information, see the [CloudTrail userIdentity Element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

You can store your log files in your Amazon S3 bucket for as long as you want, but you can also define Amazon S3 lifecycle rules to archive or delete log files automatically\. By default, your log files are encrypted with Amazon S3 server\-side encryption \(SSE\)\.

If you want to be notified upon log file delivery, you can configure CloudTrail to publish Amazon SNS notifications when new log files are delivered\. For more information, see [Configuring Amazon SNS Notifications for CloudTrail](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)\.

You can also aggregate Amazon Polly log files from multiple AWS regions and multiple AWS accounts into a single Amazon S3 bucket\. 

For more information, see [Receiving CloudTrail Log Files from Multiple Regions](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html) and [Receiving CloudTrail Log Files from Multiple Accounts](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)\.

## Understanding Amazon Polly Log File Entries<a name="understanding-parrot-entries"></a>

CloudTrail log files can contain one or more log entries\. Each entry lists multiple JSON\-formatted events\. A log entry represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. Log entries are not an ordered stack trace of the public API calls, so they do not appear in any specific order\. 

Because of potential confidentiality issues, log entries do not contain the synthesized text\. Instead, this text is redacted in the log entry\.

The following example shows a CloudTrail log entry that demonstrates the `SynthesizeSpeech`\.

```
{
    "Records": [
        {
            "awsRegion": "us-east-2", 
            "eventID": "19bd70f7-5e60-4cdc-9825-936c552278ae", 
            "eventName": "SynthesizeSpeech", 
            "eventSource": "tts.amazonaws.com", 
            "eventTime": "2016-11-02T03:49:39Z", 
            "eventType": "AwsApiCall", 
            "eventVersion": "1.05", 
            "recipientAccountId": "123456789012", 
            "requestID": "414288c2-a1af-11e6-b17f-d7cfc06cb461", 
            "requestParameters": {
                "lexiconNames": [
                    "SampleLexicon"
                ], 
                "outputFormat": "mp3", 
                "sampleRate": "22050", 
                "text": "**********", 
                "textType": "text", 
                "voiceId": "Kendra"
            }, 
            "responseElements": {
                "contentType": "audio/mpeg", 
                "requestCharacters": 25
            }, 
            "sourceIPAddress": "1.2.3.4", 
            "userAgent": "Amazon CLI/Polly 1.10 API 2016-06-10",
            "userIdentity": {
                "accessKeyId": "EXAMPLE_KEY_ID", 
                "accountId": "123456789012", 
                "arn": "arn:aws:iam::123456789012:user/Alice", 
                "principalId": "EX_PRINCIPAL_ID", 
                "type": "IAMUser", 
                "userName": "Alice"
            }
        }

    ]
}
```

The `eventName` element identifies the action that occurred and may include date and version information, such as `"SynthesizeSpeech20161128"`, nevertheless it is still referring to the same public API\.