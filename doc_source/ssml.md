# Using SSML<a name="ssml"></a>

Amazon Polly generates speech from both plain text input and Speech Synthesis Markup Language \(SSML\) documents that conform to SSML version 1\.1\. Using SSML tags, you can customize and control aspects of speech such as pronunciation, volume, and speech rate\. 

Amazon Polly supports SSML 1\.1 as defined in the following W3C recommendation:

+ [Speech Synthesis Markup Language \(SSML\) Version 1\.1, W3C Recommendation 7 September 2010](https://www.w3.org/TR/2010/REC-speech-synthesis11-20100907/)

Some of the elements in the SSML W3C recommendation are not supported\. For more information, see [Limits in Amazon Polly](limits.md)\.

This section provides simple examples of SSML that can be used to generate and control speech output\. The examples also provide the `synthesize-speech` AWS CLI command to test these examples\. 


+ [Using SSML with the Amazon Polly Console](ssml-to-speech-console.md)
+ [Using SSML with the AWS CLI](ssml-synthesize-speech-cli.md)
+ [SSML Tags in Amazon Polly](supported-ssml.md)