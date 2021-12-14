# StartSpeechSynthesisTask<a name="API_StartSpeechSynthesisTask"></a>

Allows the creation of an asynchronous synthesis task, by starting a new `SpeechSynthesisTask`\. This operation requires all the standard information needed for speech synthesis, plus the name of an Amazon S3 bucket for the service to store the output of the synthesis task and two optional parameters \(`OutputS3KeyPrefix` and `SnsTopicArn`\)\. Once the synthesis task is created, this operation will return a `SpeechSynthesisTask` object, which will include an identifier of this task as well as the current status\. The `SpeechSynthesisTask` object is available for 72 hours after starting the asynchronous synthesis task\.

## Request Syntax<a name="API_StartSpeechSynthesisTask_RequestSyntax"></a>

```
POST /v1/synthesisTasks HTTP/1.1
Content-type: application/json

{
   "Engine": "string",
   "LanguageCode": "string",
   "LexiconNames": [ "string" ],
   "OutputFormat": "string",
   "OutputS3BucketName": "string",
   "OutputS3KeyPrefix": "string",
   "SampleRate": "string",
   "SnsTopicArn": "string",
   "SpeechMarkTypes": [ "string" ],
   "Text": "string",
   "TextType": "string",
   "VoiceId": "string"
}
```

## URI Request Parameters<a name="API_StartSpeechSynthesisTask_RequestParameters"></a>

The request does not use any URI parameters\.

## Request Body<a name="API_StartSpeechSynthesisTask_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [ Engine ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-Engine"></a>
Specifies the engine \(`standard` or `neural`\) for Amazon Polly to use when processing input text for speech synthesis\. Using a voice that is not supported for the engine selected will result in an error\.  
Type: String  
Valid Values:` standard | neural`   
Required: No

 ** [ LanguageCode ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-LanguageCode"></a>
Optional language code for the Speech Synthesis request\. This is only necessary if using a bilingual voice, such as Aditi, which can be used for either Indian English \(en\-IN\) or Hindi \(hi\-IN\)\.   
If a bilingual voice is used and no language code is specified, Amazon Polly uses the default language of the bilingual voice\. The default language for any voice is the one returned by the [DescribeVoices](https://docs.aws.amazon.com/polly/latest/dg/API_DescribeVoices.html) operation for the `LanguageCode` parameter\. For example, if no language code is specified, Aditi will use Indian English rather than Hindi\.  
Type: String  
Valid Values:` arb | cmn-CN | cy-GB | da-DK | de-DE | en-AU | en-GB | en-GB-WLS | en-IN | en-US | es-ES | es-MX | es-US | fr-CA | fr-FR | is-IS | it-IT | ja-JP | hi-IN | ko-KR | nb-NO | nl-NL | pl-PL | pt-BR | pt-PT | ro-RO | ru-RU | sv-SE | tr-TR | en-NZ | en-ZA`   
Required: No

 ** [ LexiconNames ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-LexiconNames"></a>
List of one or more pronunciation lexicon names you want the service to apply during synthesis\. Lexicons are applied only if the language of the lexicon is the same as the language of the voice\.   
Type: Array of strings  
Array Members: Maximum number of 5 items\.  
Pattern: `[0-9A-Za-z]{1,20}`   
Required: No

 ** [ OutputFormat ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-OutputFormat"></a>
The format in which the returned output will be encoded\. For audio stream, this will be mp3, ogg\_vorbis, or pcm\. For speech marks, this will be json\.   
Type: String  
Valid Values:` json | mp3 | ogg_vorbis | pcm`   
Required: Yes

 ** [ OutputS3BucketName ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-OutputS3BucketName"></a>
Amazon S3 bucket name to which the output file will be saved\.  
Type: String  
Pattern: `^[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9]$`   
Required: Yes

 ** [ OutputS3KeyPrefix ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-OutputS3KeyPrefix"></a>
The Amazon S3 key prefix for the output speech file\.  
Type: String  
Pattern: `^[0-9a-zA-Z\/\!\-_\.\*\'\(\):;\$@=+\,\?&]{0,800}$`   
Required: No

 ** [ SampleRate ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-SampleRate"></a>
The audio frequency specified in Hz\.  
The valid values for mp3 and ogg\_vorbis are "8000", "16000", "22050", and "24000"\. The default value for standard voices is "22050"\. The default value for neural voices is "24000"\.  
Valid values for pcm are "8000" and "16000" The default value is "16000"\.   
Type: String  
Required: No

 ** [ SnsTopicArn ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-SnsTopicArn"></a>
ARN for the SNS topic optionally used for providing status notification for a speech synthesis task\.  
Type: String  
Pattern: `^arn:aws(-(cn|iso(-b)?|us-gov))?:sns:[a-z0-9_-]{1,50}:\d{12}:[a-zA-Z0-9_-]{1,256}$`   
Required: No

 ** [ SpeechMarkTypes ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-SpeechMarkTypes"></a>
The type of speech marks returned for the input text\.  
Type: Array of strings  
Array Members: Maximum number of 4 items\.  
Valid Values:` sentence | ssml | viseme | word`   
Required: No

 ** [ Text ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-Text"></a>
The input text to synthesize\. If you specify ssml as the TextType, follow the SSML format for the input text\.   
Type: String  
Required: Yes

 ** [ TextType ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-TextType"></a>
Specifies whether the input text is plain text or SSML\. The default value is plain text\.   
Type: String  
Valid Values:` ssml | text`   
Required: No

 ** [ VoiceId ](#API_StartSpeechSynthesisTask_RequestSyntax) **   <a name="polly-StartSpeechSynthesisTask-request-VoiceId"></a>
Voice ID to use for the synthesis\.   
Type: String  
Valid Values:` Aditi | Amy | Astrid | Bianca | Brian | Camila | Carla | Carmen | Celine | Chantal | Conchita | Cristiano | Dora | Emma | Enrique | Ewa | Filiz | Gabrielle | Geraint | Giorgio | Gwyneth | Hans | Ines | Ivy | Jacek | Jan | Joanna | Joey | Justin | Karl | Kendra | Kevin | Kimberly | Lea | Liv | Lotte | Lucia | Lupe | Mads | Maja | Marlene | Mathieu | Matthew | Maxim | Mia | Miguel | Mizuki | Naja | Nicole | Olivia | Penelope | Raveena | Ricardo | Ruben | Russell | Salli | Seoyeon | Takumi | Tatyana | Vicki | Vitoria | Zeina | Zhiyu | Aria | Ayanda`   
Required: Yes

## Response Syntax<a name="API_StartSpeechSynthesisTask_ResponseSyntax"></a>

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

## Response Elements<a name="API_StartSpeechSynthesisTask_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [ SynthesisTask ](#API_StartSpeechSynthesisTask_ResponseSyntax) **   <a name="polly-StartSpeechSynthesisTask-response-SynthesisTask"></a>
SynthesisTask object that provides information and attributes about a newly submitted speech synthesis task\.  
Type: [ SynthesisTask ](API_SynthesisTask.md) object

## Errors<a name="API_StartSpeechSynthesisTask_Errors"></a>

 ** EngineNotSupportedException **   
This engine is not compatible with the voice that you have designated\. Choose a new voice that is compatible with the engine or change the engine and restart the operation\.  
HTTP Status Code: 400

 ** InvalidS3BucketException **   
The provided Amazon S3 bucket name is invalid\. Please check your input with S3 bucket naming requirements and try again\.  
HTTP Status Code: 400

 ** InvalidS3KeyException **   
The provided Amazon S3 key prefix is invalid\. Please provide a valid S3 object key name\.  
HTTP Status Code: 400

 ** InvalidSampleRateException **   
The specified sample rate is not valid\.  
HTTP Status Code: 400

 ** InvalidSnsTopicArnException **   
The provided SNS topic ARN is invalid\. Please provide a valid SNS topic ARN and try again\.  
HTTP Status Code: 400

 ** InvalidSsmlException **   
The SSML you provided is invalid\. Verify the SSML syntax, spelling of tags and values, and then try again\.  
HTTP Status Code: 400

 ** LanguageNotSupportedException **   
The language specified is not currently supported by Amazon Polly in this capacity\.  
HTTP Status Code: 400

 ** LexiconNotFoundException **   
Amazon Polly can't find the specified lexicon\. This could be caused by a lexicon that is missing, its name is misspelled or specifying a lexicon that is in a different region\.  
Verify that the lexicon exists, is in the region \(see [ ListLexicons ](API_ListLexicons.md)\) and that you spelled its name is spelled correctly\. Then try again\.  
HTTP Status Code: 404

 ** MarksNotSupportedForFormatException **   
Speech marks are not supported for the `OutputFormat` selected\. Speech marks are only available for content in `json` format\.  
HTTP Status Code: 400

 ** ServiceFailureException **   
An unknown condition has caused a service failure\.  
HTTP Status Code: 500

 ** SsmlMarksNotSupportedForTextTypeException **   
SSML speech marks are not supported for plain text\-type input\.  
HTTP Status Code: 400

 ** TextLengthExceededException **   
The value of the "Text" parameter is longer than the accepted limits\. For the `SynthesizeSpeech` API, the limit for input text is a maximum of 6000 characters total, of which no more than 3000 can be billed characters\. For the `StartSpeechSynthesisTask` API, the maximum is 200,000 characters, of which no more than 100,000 can be billed characters\. SSML tags are not counted as billed characters\.  
HTTP Status Code: 400

## See Also<a name="API_StartSpeechSynthesisTask_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/polly-2016-06-10/StartSpeechSynthesisTask) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/polly-2016-06-10/StartSpeechSynthesisTask) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/StartSpeechSynthesisTask) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/StartSpeechSynthesisTask) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/polly-2016-06-10/StartSpeechSynthesisTask) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/polly-2016-06-10/StartSpeechSynthesisTask) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/polly-2016-06-10/StartSpeechSynthesisTask) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/polly-2016-06-10/StartSpeechSynthesisTask) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/polly-2016-06-10/StartSpeechSynthesisTask) 