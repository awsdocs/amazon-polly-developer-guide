# SynthesizeSpeech<a name="API_SynthesizeSpeech"></a>

Synthesizes UTF\-8 input, plain text or SSML, to a stream of bytes\. SSML input must be valid, well\-formed SSML\. Some alphabets might not be available with all the voices \(for example, Cyrillic might not be read at all by English voices\) unless phoneme mapping is used\. For more information, see [How it Works](http://docs.aws.amazon.com/polly/latest/dg/how-text-to-speech-works.html)\.

## Request Syntax<a name="API_SynthesizeSpeech_RequestSyntax"></a>

```
POST /v1/speech HTTP/1.1
Content-type: application/json

{
   "LexiconNames": [ "string" ],
   "OutputFormat": "string",
   "SampleRate": "string",
   "SpeechMarkTypes": [ "string" ],
   "Text": "string",
   "TextType": "string",
   "VoiceId": "string"
}
```

## URI Request Parameters<a name="API_SynthesizeSpeech_RequestParameters"></a>

The request does not use any URI parameters\.

## Request Body<a name="API_SynthesizeSpeech_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** LexiconNames **   
List of one or more pronunciation lexicon names you want the service to apply during synthesis\. Lexicons are applied only if the language of the lexicon is the same as the language of the voice\. For information about storing lexicons, see [PutLexicon](http://docs.aws.amazon.com/polly/latest/dg/API_PutLexicon.html)\.  
Type: Array of strings  
Array Members: Maximum number of 5 items\.  
Pattern: `[0-9A-Za-z]{1,20}`   
Required: No

 ** OutputFormat **   
 The format in which the returned output will be encoded\. For audio stream, this will be mp3, ogg\_vorbis, or pcm\. For speech marks, this will be json\.   
Type: String  
Valid Values:` json | mp3 | ogg_vorbis | pcm`   
Required: Yes

 ** SampleRate **   
 The audio frequency specified in Hz\.   
The valid values for `mp3` and `ogg_vorbis` are "8000", "16000", and "22050"\. The default value is "22050"\.   
 Valid values for `pcm` are "8000" and "16000" The default value is "16000"\.   
Type: String  
Required: No

 ** SpeechMarkTypes **   
The type of speech marks returned for the input text\.  
Type: Array of strings  
Array Members: Maximum number of 4 items\.  
Valid Values:` sentence | ssml | viseme | word`   
Required: No

 ** Text **   
 Input text to synthesize\. If you specify `ssml` as the `TextType`, follow the SSML format for the input text\.   
Type: String  
Required: Yes

 ** TextType **   
 Specifies whether the input text is plain text or SSML\. The default value is plain text\. For more information, see [Using SSML](http://docs.aws.amazon.com/polly/latest/dg/ssml.html)\.  
Type: String  
Valid Values:` ssml | text`   
Required: No

 ** VoiceId **   
 Voice ID to use for the synthesis\. You can get a list of available voice IDs by calling the [DescribeVoices](http://docs.aws.amazon.com/polly/latest/dg/API_DescribeVoices.html) operation\.   
Type: String  
Valid Values:` Geraint | Gwyneth | Mads | Naja | Hans | Marlene | Nicole | Russell | Amy | Brian | Emma | Raveena | Ivy | Joanna | Joey | Justin | Kendra | Kimberly | Matthew | Salli | Conchita | Enrique | Miguel | Penelope | Chantal | Celine | Mathieu | Dora | Karl | Carla | Giorgio | Mizuki | Liv | Lotte | Ruben | Ewa | Jacek | Jan | Maja | Ricardo | Vitoria | Cristiano | Ines | Carmen | Maxim | Tatyana | Astrid | Filiz | Vicki | Takumi | Seoyeon | Aditi`   
Required: Yes

## Response Syntax<a name="API_SynthesizeSpeech_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-Type: ContentType
x-amzn-RequestCharacters: RequestCharacters

AudioStream
```

## Response Elements<a name="API_SynthesizeSpeech_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The response returns the following HTTP headers\.

 ** ContentType **   
 Specifies the type audio stream\. This should reflect the `OutputFormat` parameter in your request\.   

+  If you request `mp3` as the `OutputFormat`, the `ContentType` returned is audio/mpeg\. 

+  If you request `ogg_vorbis` as the `OutputFormat`, the `ContentType` returned is audio/ogg\. 

+  If you request `pcm` as the `OutputFormat`, the `ContentType` returned is audio/pcm in a signed 16\-bit, 1 channel \(mono\), little\-endian format\. 

+ If you request `json` as the `OutputFormat`, the `ContentType` returned is audio/json\.
 

 ** RequestCharacters **   
Number of characters synthesized\.

The response returns the following as the HTTP body\.

 ** AudioStream **   
 Stream containing the synthesized speech\. 

## Errors<a name="API_SynthesizeSpeech_Errors"></a>

 **InvalidSampleRateException**   
The specified sample rate is not valid\.  
HTTP Status Code: 400

 **InvalidSsmlException**   
The SSML you provided is invalid\. Verify the SSML syntax, spelling of tags and values, and then try again\.  
HTTP Status Code: 400

 **LexiconNotFoundException**   
Amazon Polly can't find the specified lexicon\. This could be caused by a lexicon that is missing, its name is misspelled or specifying a lexicon that is in a different region\.  
Verify that the lexicon exists, is in the region \(see [ListLexicons](API_ListLexicons.md)\) and that you spelled its name is spelled correctly\. Then try again\.  
HTTP Status Code: 404

 **MarksNotSupportedForFormatException**   
Speech marks are not supported for the `OutputFormat` selected\. Speech marks are only available for content in `json` format\.  
HTTP Status Code: 400

 **ServiceFailureException**   
An unknown condition has caused a service failure\.  
HTTP Status Code: 500

 **SsmlMarksNotSupportedForTextTypeException**   
SSML speech marks are not supported for plain text\-type input\.  
HTTP Status Code: 400

 **TextLengthExceededException**   
The value of the "Text" parameter is longer than the accepted limits\. The limit for input text is a maximum of 3000 characters total, of which no more than 1500 can be billed characters\. SSML tags are not counted as billed characters\.  
HTTP Status Code: 400

## See Also<a name="API_SynthesizeSpeech_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/polly-2016-06-10/SynthesizeSpeech) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/polly-2016-06-10/SynthesizeSpeech) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/SynthesizeSpeech) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/SynthesizeSpeech) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/polly-2016-06-10/SynthesizeSpeech) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/polly-2016-06-10/SynthesizeSpeech) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/polly-2016-06-10/SynthesizeSpeech) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/polly-2016-06-10/SynthesizeSpeech) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/polly-2016-06-10/SynthesizeSpeech) 