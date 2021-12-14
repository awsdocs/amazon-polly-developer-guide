# GetSpeechSynthesisTask<a name="API_GetSpeechSynthesisTask"></a>

Retrieves a specific SpeechSynthesisTask object based on its TaskID\. This object contains information about the given speech synthesis task, including the status of the task, and a link to the S3 bucket containing the output of the task\.

## Request Syntax<a name="API_GetSpeechSynthesisTask_RequestSyntax"></a>

```
GET /v1/synthesisTasks/TaskId HTTP/1.1
```

## URI Request Parameters<a name="API_GetSpeechSynthesisTask_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [ TaskId ](#API_GetSpeechSynthesisTask_RequestSyntax) **   <a name="polly-GetSpeechSynthesisTask-request-TaskId"></a>
The Amazon Polly generated identifier for a speech synthesis task\.  
Pattern: `^[a-zA-Z0-9_-]{1,100}$`   
Required: Yes

## Request Body<a name="API_GetSpeechSynthesisTask_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetSpeechSynthesisTask_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "SynthesisTask": { 
      "CreationTime": number,
      "Engine": "string",
      "LanguageCode": "string",
      "LexiconNames": [ "string" ],
      "OutputFormat": "string",
      "OutputUri": "string",
      "RequestCharacters": number,
      "SampleRate": "string",
      "SnsTopicArn": "string",
      "SpeechMarkTypes": [ "string" ],
      "TaskId": "string",
      "TaskStatus": "string",
      "TaskStatusReason": "string",
      "TextType": "string",
      "VoiceId": "string"
   }
}
```

## Response Elements<a name="API_GetSpeechSynthesisTask_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ SynthesisTask ](#API_GetSpeechSynthesisTask_ResponseSyntax) **   <a name="polly-GetSpeechSynthesisTask-response-SynthesisTask"></a>
SynthesisTask object that provides information from the requested task, including output format, creation time, task status, and so on\.  
Type: [ SynthesisTask ](API_SynthesisTask.md) object

## Errors<a name="API_GetSpeechSynthesisTask_Errors"></a>

 ** InvalidTaskIdException **   
The provided Task ID is not valid\. Please provide a valid Task ID and try again\.  
HTTP Status Code: 400

 ** ServiceFailureException **   
An unknown condition has caused a service failure\.  
HTTP Status Code: 500

 ** SynthesisTaskNotFoundException **   
The Speech Synthesis task with requested Task ID cannot be found\.  
HTTP Status Code: 400

## See Also<a name="API_GetSpeechSynthesisTask_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/polly-2016-06-10/GetSpeechSynthesisTask) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/polly-2016-06-10/GetSpeechSynthesisTask) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/GetSpeechSynthesisTask) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/GetSpeechSynthesisTask) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/polly-2016-06-10/GetSpeechSynthesisTask) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/polly-2016-06-10/GetSpeechSynthesisTask) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/polly-2016-06-10/GetSpeechSynthesisTask) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/polly-2016-06-10/GetSpeechSynthesisTask) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/polly-2016-06-10/GetSpeechSynthesisTask) 