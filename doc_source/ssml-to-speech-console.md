# Using SSML \(Console\)<a name="ssml-to-speech-console"></a>

With SSML tags, you can customize and control aspects of speech such as pronunciation, volume, and speech rate\. In the AWS Management Console, the SSML\-enhanced text that you want to convert to audio is entered on the SSML tab of the Text\-to\-Speech page\. Although text entered in plain text relies on default settings for the language and voice you've chosen, text enhanced with SSML tells Amazon Polly not only what you want to say, but how you want to say it\. Except for the added SSML tags, Amazon Polly synthesizes SSML\-enhanced text in the same way as it synthesizes plain text\. See [Exercise 2: Synthesizing Speech with Plain Text Input \(Console\)](getting-started-console.md#plain-text-to-speech-console) for more information\. 

When using SSML, you enclose the entire text in a `<speak>` tag to let Amazon Polly know that you're using SSML\. For example: 

```
<speak>Hi! My name is Joanna. I will read any text you type here.</speak>
```

You then use specific SSML tags on the text inside the `<speak>` tags to customize the way you want the text to sound\. You can add a pause, change the pace of the speech, lower or raise the volume of the voice, or add many other customizations so that the text sounds right for you\. For a full list of the SSML tags that you can use, see [Supported SSML Tags](supportedtags.md)\. 

In the following example, you use an SSML tag to tell Amazon Polly to substitute "World Wide Web Consortium" for "W3C" when it speaks a short paragraph\. You also use tags to introduce a pause and whisper a word\. Compare the results of this exercise with that of [Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech) \.

For more information on SSML, with examples, see [Supported SSML Tags](supportedtags.md)\.

**To synthesize speech from SSML\-enhanced text \(console\)**



1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. If it isn't already displayed, choose the **Text\-to\-Speech** tab\. 

1. Turn on **SSML**\.

1. Type or paste the following text in the text box: 

   ```
   <speak>
        He was caught up in the game.<break time="1s"/> In the middle of the 
        10/3/2014 <sub alias="World Wide Web Consortium">W3C</sub> meeting, 
        he shouted, "Nice job!" quite loudly. When his boss stared at him, he repeated 
        <amazon:effect name="whispered">"Nice job,"</amazon:effect> in a 
        whisper.
   </speak>
   ```

   The SSML tags tell Amazon Polly how to render the text:
   + `<break time="1s"/>` tells Amazon Polly to pause 1 second between the first two sentences\.
   + `<sub alias="World Wide Web Consortium">W3C</sub>` tells Amazon Polly to substitute World Wide Web Consortium for the acronym W3C\.
   + `<amazon:effect name="whispered">Nice job</amazon:effect>` tells Amazon Polly to whisper the second instance of "Nice job\." \.
**Note**  
When you use the AWS CLI, you enclose the input text in quotation marks to differentiate it from the surrounding code\. The Amazon Polly console doesn't show you code, so you don't enclose input text in quotation marks when you use it\.

1. For **Language**, choose **English, US**, then choose a voice\.

1. To listen to the speech, choose **Listen**\.

1. To save the speech file, choose **Download**\. If you want to save it in a different format, expand **Additional settings**, turn on **Speech file format settings** and choose the format that you want, then choose **Download**\. 