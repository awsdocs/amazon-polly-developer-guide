# Using SSML with the Amazon Polly Console<a name="ssml-to-speech-console"></a>

Amazon Polly supports version 1\.1 SSML as defined by the W3C\. This section covers how to use SSML input for speech synthesis in the Amazon Polly console\.

## Using SSML with the Amazon Polly Console<a name="ssml-console-exercise"></a>

The following procedure synthesizes speech using SSML input\. Except for steps 3 and 4 below, the steps in this example are identical to those in [Exercise 2: Synthesizing Speech \(Plain Text Input\)](getting-started-console.md#plain-text-to-speech-console)\.

**To synthesize speech using the Amazon Polly console \(SSML input\)**

In this example we introduce SSML tagging to substitute "World Wide Web Consortium" for "W3C"\. Compare the results of this exercise with that of [Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech) for both US English and another language\.

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. If needed, choose the **Text\-to\-Speech** tab\. 

1. Choose the **SSML** tab\.

1. Type or paste the following text in the text box: 

   ```
   <speak>
        He was caught up in the game.<break time="1s"/> 
        In the middle of the 10/3/2014 <sub alias="World Wide Web Consortium">W3C</sub> meeting 
        he shouted, "Score!" quite loudly. When his boss stared at him, he repeated 
        <amazon:effect name="whispered">"Score"</amazon:effect> in a whisper.
   </speak>
   ```

   The SSML tags inform Amazon Polly that the text should be rendered in a specified way\.

   + `<break time="1s"/>` instructs Amazon Polly to pause 1 second between the initial two sentences\.

   + `<sub alias="World Wide Web Consortium">W3C</sub>` instructs Amazon Polly to substitute "World Wide Web Consortium" for the acronym "W3C"\.

   + `<amazon:effect name="whispered">Score</amazon:effect>` instructs Amazon Polly to say the second "Score" in a whispered voice\.

   For more information on SSML with examples, see [Supported SSML Tags](supported-ssml.md#supportedtags)

1. For **Choose a language and region**, choose **English US**, then choose the voice you want\.

1. To listen to the speech immediately, choose **Listen to speech**\.

1. To save the speech file, choose **Download \[format\]** if the format is the one you want\. Otherwise choose **Change file format**, choose the format you want, and then choose **Change**\. Choose **Download \[format\]**\. 

 **Related Console Examples** 

+ [Exercise 2: Synthesizing Speech \(Plain Text Input\)](getting-started-console.md#plain-text-to-speech-console)

+ [Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech)

**Note**  
When entering the input text in the AWS CLI, quotation marks are used around the input text to differentiate it from the surrounding code\. Because the Amazon Polly console does not show you the code, quotation marks are not used around the input text in the console\.

## Next Step<a name="ssml-console-next-step"></a>

[Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech)