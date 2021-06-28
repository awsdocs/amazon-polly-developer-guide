# Generating Speech from SSML Documents<a name="ssml"></a>

You can use Amazon Polly to generate speech from either plain text or from documents marked up with Speech Synthesis Markup Language \(SSML\)\. Using SSML\-enhanced text gives you additional control over how Amazon Polly generates speech from the text you provide\.

For example, you can include a long pause within your text, or change the speech rate or pitch\. Other options include:
+ emphasizing specific words or phrases
+ using phonetic pronunciation
+ including breathing sounds
+ whispering
+ using the Newscaster speaking style\.

For complete details on the SSML tags supported by Amazon Polly and how to use them, see [Supported SSML Tags](supportedtags.md)

When using SSML, there are several reserved characters that require special treatment\. This is because SSML uses these characters as part of its code\. In order to use them, you use a specific entity to *escape* them\. For more information, see [Reserved Characters in SSML](escapees.md)

Amazon Polly provides these types of control with a subset of the SSML markup tags that are defined by [Speech Synthesis Markup Language \(SSML\) Version 1\.1, W3C Recommendation](https://www.w3.org/TR/2010/REC-speech-synthesis11-20100907/)\.

You can use SSML within the Amazon Polly console or by using the AWS CLI\. The following topics show you how you can use SSML to generate speech and control the output so that it precisely fits your needs\. 

**Topics**
+ [Reserved Characters in SSML](escapees.md)
+ [Using SSML \(Console\)](ssml-to-speech-console.md)
+ [Using SSML \(AWS CLI\)](ssml-synthesize-speech-cli.md)
+ [Supported SSML Tags](supportedtags.md)