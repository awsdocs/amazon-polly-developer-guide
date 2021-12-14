# SynthesisTask<a name="API_SynthesisTask"></a>

SynthesisTask object that provides information about a speech synthesis task\.

## Contents<a name="API_SynthesisTask_Contents"></a>

 ** CreationTime **   <a name="polly-Type-SynthesisTask-CreationTime"></a>
Timestamp for the time the synthesis task was started\.  
Type: Timestamp  
Required: No

 ** Engine **   <a name="polly-Type-SynthesisTask-Engine"></a>
Specifies the engine \(`standard` or `neural`\) for Amazon Polly to use when processing input text for speech synthesis\. Using a voice that is not supported for the engine selected will result in an error\.  
Type: String  
Valid Values:` standard | neural`   
Required: No

 ** LanguageCode **   <a name="polly-Type-SynthesisTask-LanguageCode"></a>
Optional language code for a synthesis task\. This is only necessary if using a bilingual voice, such as Aditi, which can be used for either Indian English \(en\-IN\) or Hindi \(hi\-IN\)\.   
If a bilingual voice is used and no language code is specified, Amazon Polly uses the default language of the bilingual voice\. The default language for any voice is the one returned by the [DescribeVoices](https://docs.aws.amazon.com/polly/latest/dg/API_DescribeVoices.html) operation for the `LanguageCode` parameter\. For example, if no language code is specified, Aditi will use Indian English rather than Hindi\.  
Type: String  
Valid Values:` arb | cmn-CN | cy-GB | da-DK | de-DE | en-AU | en-GB | en-GB-WLS | en-IN | en-US | es-ES | es-MX | es-US | fr-CA | fr-FR | is-IS | it-IT | ja-JP | hi-IN | ko-KR | nb-NO | nl-NL | pl-PL | pt-BR | pt-PT | ro-RO | ru-RU | sv-SE | tr-TR | en-NZ | en-ZA`   
Required: No

 ** LexiconNames **   <a name="polly-Type-SynthesisTask-LexiconNames"></a>
List of one or more pronunciation lexicon names you want the service to apply during synthesis\. Lexicons are applied only if the language of the lexicon is the same as the language of the voice\.   
Type: Array of strings  
Array Members: Maximum number of 5 items\.  
Pattern: `[0-9A-Za-z]{1,20}`   
Required: No

 ** OutputFormat **   <a name="polly-Type-SynthesisTask-OutputFormat"></a>
The format in which the returned output will be encoded\. For audio stream, this will be mp3, ogg\_vorbis, or pcm\. For speech marks, this will be json\.   
Type: String  
Valid Values:` json | mp3 | ogg_vorbis | pcm`   
Required: No

 ** OutputUri **   <a name="polly-Type-SynthesisTask-OutputUri"></a>
Pathway for the output speech file\.  
Type: String  
Required: No

 ** RequestCharacters **   <a name="polly-Type-SynthesisTask-RequestCharacters"></a>
Number of billable characters synthesized\.  
Type: Integer  
Required: No

 ** SampleRate **   <a name="polly-Type-SynthesisTask-SampleRate"></a>
The audio frequency specified in Hz\.  
The valid values for mp3 and ogg\_vorbis are "8000", "16000", "22050", and "24000"\. The default value for standard voices is "22050"\. The default value for neural voices is "24000"\.  
Valid values for pcm are "8000" and "16000" The default value is "16000"\.   
Type: String  
Required: No

 ** SnsTopicArn **   <a name="polly-Type-SynthesisTask-SnsTopicArn"></a>
ARN for the SNS topic optionally used for providing status notification for a speech synthesis task\.  
Type: String  
Pattern: `^arn:aws(-(cn|iso(-b)?|us-gov))?:sns:[a-z0-9_-]{1,50}:\d{12}:[a-zA-Z0-9_-]{1,256}$`   
Required: No

 ** SpeechMarkTypes **   <a name="polly-Type-SynthesisTask-SpeechMarkTypes"></a>
The type of speech marks returned for the input text\.  
Type: Array of strings  
Array Members: Maximum number of 4 items\.  
Valid Values:` sentence | ssml | viseme | word`   
Required: No

 ** TaskId **   <a name="polly-Type-SynthesisTask-TaskId"></a>
The Amazon Polly generated identifier for a speech synthesis task\.  
Type: String  
Pattern: `^[a-zA-Z0-9_-]{1,100}$`   
Required: No

 ** TaskStatus **   <a name="polly-Type-SynthesisTask-TaskStatus"></a>
Current status of the individual speech synthesis task\.  
Type: String  
Valid Values:` scheduled | inProgress | completed | failed`   
Required: No

 ** TaskStatusReason **   <a name="polly-Type-SynthesisTask-TaskStatusReason"></a>
Reason for the current status of a specific speech synthesis task, including errors if the task has failed\.  
Type: String  
Required: No

 ** TextType **   <a name="polly-Type-SynthesisTask-TextType"></a>
Specifies whether the input text is plain text or SSML\. The default value is plain text\.   
Type: String  
Valid Values:` ssml | text`   
Required: No

 ** VoiceId **   <a name="polly-Type-SynthesisTask-VoiceId"></a>
Voice ID to use for the synthesis\.   
Type: String  
Valid Values:` Aditi | Amy | Astrid | Bianca | Brian | Camila | Carla | Carmen | Celine | Chantal | Conchita | Cristiano | Dora | Emma | Enrique | Ewa | Filiz | Gabrielle | Geraint | Giorgio | Gwyneth | Hans | Ines | Ivy | Jacek | Jan | Joanna | Joey | Justin | Karl | Kendra | Kevin | Kimberly | Lea | Liv | Lotte | Lucia | Lupe | Mads | Maja | Marlene | Mathieu | Matthew | Maxim | Mia | Miguel | Mizuki | Naja | Nicole | Olivia | Penelope | Raveena | Ricardo | Ruben | Russell | Salli | Seoyeon | Takumi | Tatyana | Vicki | Vitoria | Zeina | Zhiyu | Aria | Ayanda`   
Required: No

## See Also<a name="API_SynthesisTask_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/SynthesisTask) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/SynthesisTask) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/polly-2016-06-10/SynthesisTask) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/polly-2016-06-10/SynthesisTask) 