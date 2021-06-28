# SynthesizeSpeech<a name="API_SynthesizeSpeech"></a>

Synthesizes UTF\-8 input, plain text or SSML, to a stream of bytes\. SSML input must be valid, well\-formed SSML\. Some alphabets might not be available with all the voices \(for example, Cyrillic might not be read at all by English voices\) unless phoneme mapping is used\. For more information, see [How it Works](https://docs.aws.amazon.com/polly/latest/dg/how-text-to-speech-works.html)\.

## Request Syntax<a name="API_SynthesizeSpeech_RequestSyntax"></a>

```
POST /v1/speech HTTP/1.1
Content-type: application/json

{
   "Engine": "string",
   "LanguageCode": "string",
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

 ** [Engine](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-Engine"></a>
Specifies the engine \(`standard` or `neural`\) for Amazon Polly to use when processing input text for speech synthesis\. For information on Amazon Polly voices and which voices are available in standard\-only, NTTS\-only, and both standard and NTTS formats, see [Available Voices](https://docs.aws.amazon.com/polly/latest/dg/voicelist.html)\.  
 **NTTS\-only voices**   
When using NTTS\-only voices such as Kevin \(en\-US\), this parameter is required and must be set to `neural`\. If the engine is not specified, or is set to `standard`, this will result in an error\.   
Type: String  
Valid Values: `standard` \| `neural`   
Required: Yes  
 **Standard voices**   
For standard voices, this is not required; the engine parameter defaults to `standard`\. If the engine is not specified, or is set to `standard` and an NTTS\-only voice is selected, this will result in an error\.   
Type: String  
Valid Values:` standard | neural`   
Required: No

 ** [LanguageCode](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-LanguageCode"></a>
Optional language code for the Synthesize Speech request\. This is only necessary if using a bilingual voice, such as Aditi, which can be used for either Indian English \(en\-IN\) or Hindi \(hi\-IN\)\.   
If a bilingual voice is used and no language code is specified, Amazon Polly uses the default language of the bilingual voice\. The default language for any voice is the one returned by the [DescribeVoices](https://docs.aws.amazon.com/polly/latest/dg/API_DescribeVoices.html) operation for the `LanguageCode` parameter\. For example, if no language code is specified, Aditi will use Indian English rather than Hindi\.  
Type: String  
Valid Values:` ar-SA | arb | cmn-CN | cy-GB | da-DK | de-DE | en-AU | en-CA | en-GB | en-GB-WLS | en-IN | en-NZ | en-US | es-ES | es-MX | es-US | fr-CA | fr-FR | hi-IN | is-IS | it-IT | ja-JP | ko-KR | nb-NO | nl-NL | pl-PL | pt-BR | pt-PT | ro-RO | ru-RU | sv-SE | tr-TR`   
Required: No

 ** [LexiconNames](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-LexiconNames"></a>
List of one or more pronunciation lexicon names you want the service to apply during synthesis\. Lexicons are applied only if the language of the lexicon is the same as the language of the voice\. For information about storing lexicons, see [PutLexicon](https://docs.aws.amazon.com/polly/latest/dg/API_PutLexicon.html)\.  
Type: Array of strings  
Array Members: Maximum number of 5 items\.  
Length Constraints: Maximum length of 20\.  
Pattern: `[0-9A-Za-z]{1,20}`   
Required: No

 ** [OutputFormat](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-OutputFormat"></a>
 The format in which the returned output will be encoded\. For audio stream, this will be mp3, ogg\_vorbis, or pcm\. For speech marks, this will be json\.   
When pcm is used, the content returned is audio/pcm in a signed 16\-bit, 1 channel \(mono\), little\-endian format\.   
Type: String  
Valid Values:` json | mp3 | ogg_vorbis | pcm | pcm_u8`   
Required: Yes

 ** [SampleRate](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-SampleRate"></a>
The audio frequency specified in Hz\.  
The valid values for mp3 and ogg\_vorbis are "8000", "16000", "22050", and "24000"\. The default value for standard voices is "22050"\. The default value for neural voices is "24000"\.  
Valid values for pcm are "8000" and "16000" The default value is "16000"\.   
Type: String  
Length Constraints: Maximum length of 5\.  
Pattern: `^\d{4,5}$`   
Required: No

 ** [SpeechMarkTypes](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-SpeechMarkTypes"></a>
The type of speech marks returned for the input text\.  
Type: Array of strings  
Array Members: Maximum number of 4 items\.  
Valid Values:` sentence | ssml | viseme | word`   
Required: No

 ** [Text](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-Text"></a>
 Input text to synthesize\. If you specify `ssml` as the `TextType`, follow the SSML format for the input text\.   
Type: String  
Length Constraints: Maximum length of 2000000\.  
Required: Yes

 ** [TextType](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-TextType"></a>
 Specifies whether the input text is plain text or SSML\. The default value is plain text\. For more information, see [Using SSML](https://docs.aws.amazon.com/polly/latest/dg/ssml.html)\.  
Type: String  
Valid Values:` ssml | text`   
Required: No

 ** [VoiceId](#API_SynthesizeSpeech_RequestSyntax) **   <a name="polly-SynthesizeSpeech-request-VoiceId"></a>
 Voice ID to use for the synthesis\. You can get a list of available voice IDs by calling the [DescribeVoices](https://docs.aws.amazon.com/polly/latest/dg/API_DescribeVoices.html) operation\.   
Type: String  
Valid Values:` Aditi | Amy | Astrid | Bianca | Brian | Camila | Carla | Carmen | Celine | Chantal | Conchita | Cristiano | Dora | Emma | Enrique | Ewa | Filiz | Gabrielle | Geraint | Giorgio | Gwyneth | Hans | Ines | Ivy | Jacek | Jan | Joanna | Joey | Justin | Karl | Kendra | Kevin | Kimberly | Lea | Liv | Lotte | Lucia | Lupe | Mads | Maja | Marlene | Mathieu | Matthew | Maxim | Mia | Miguel | Mizuki | Naja | Nicole | Olivia | Penelope | Raveena | Ricardo | Ruben | Russell | Salli | Seoyeon | Takumi | Tatyana | Vicki | Vitoria | VSD | Zhiyu | Abbey | Alicia | Aria | Awhina | Becca | Candela | Charlie | Charlotte | Chloe | Colonel | Ella | Evelyn | Fernanda | Giulia | Hawkeye | Ira | Jay | John | Mariana | Mayor | Nina | Robin | Sara | Silke | TestingBrandVoice | Yumiko | Zeina`   
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

 ** [ContentType](#API_SynthesizeSpeech_ResponseSyntax) **   <a name="polly-SynthesizeSpeech-response-ContentType"></a>
 Specifies the type audio stream\. This should reflect the `OutputFormat` parameter in your request\.   
+  If you request `mp3` as the `OutputFormat`, the `ContentType` returned is audio/mpeg\. 
+  If you request `ogg_vorbis` as the `OutputFormat`, the `ContentType` returned is audio/ogg\. 
+  If you request `pcm` as the `OutputFormat`, the `ContentType` returned is audio/pcm in a signed 16\-bit, 1 channel \(mono\), little\-endian format\. 
+ If you request `json` as the `OutputFormat`, the `ContentType` returned is audio/json\.
 

 ** [RequestCharacters](#API_SynthesizeSpeech_ResponseSyntax) **   <a name="polly-SynthesizeSpeech-response-RequestCharacters"></a>
Number of characters synthesized\.

The response returns the following as the HTTP body\.

 ** [AudioStream](#API_SynthesizeSpeech_ResponseSyntax) **   <a name="polly-SynthesizeSpeech-response-AudioStream"></a>
 Stream containing the synthesized speech\. 

## Errors<a name="API_SynthesizeSpeech_Errors"></a>

 **EngineNotSupportedException**   
This engine is not compatible with the voice that you have designated\. Choose a new voice that is compatible with the engine or change the engine and restart the operation\.  
HTTP Status Code: 400

 **InvalidSampleRateException**   
The specified sample rate is not valid\.  
HTTP Status Code: 400

 **InvalidSsmlException**   
The SSML you provided is invalid\. Verify the SSML syntax, spelling of tags and values, and then try again\.  
HTTP Status Code: 400

 **LanguageNotSupportedException**   
The language specified is not currently supported by Amazon Polly in this capacity\.  
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
The value of the "Text" parameter is longer than the accepted limits\. For the `SynthesizeSpeech` API, the limit for input text is a maximum of 6000 characters total, of which no more than 3000 can be billed characters\. For the `StartSpeechSynthesisTask` API, the maximum is 200,000 characters, of which no more than 100,000 can be billed characters\. SSML tags are not counted as billed characters\.  
HTTP Status Code: 400

## See Also<a name="API_SynthesizeSpeech_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/polly-2016-06-10/SynthesizeSpeech) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/polly-2016-06-10/SynthesizeSpeech) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/SynthesizeSpeech) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/SynthesizeSpeech) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/polly-2016-06-10/SynthesizeSpeech) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/polly-2016-06-10/SynthesizeSpeech) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/polly-2016-06-10/SynthesizeSpeech) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/polly-2016-06-10/SynthesizeSpeech) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/polly-2016-06-10/SynthesizeSpeech) 