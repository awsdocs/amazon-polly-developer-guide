# Step 2: Getting Started \(Console\)<a name="getting-started-console"></a>

The Amazon Polly console is the easiest way to get started testing and using Amazon Polly's speech synthesizing\. The Amazon Polly console supports synthesizing speech from either plain text or SSML input\.

**Topics**
+ [Exercise 1: Synthesizing Speech Quick Start \(Console\)](#quick-start-text-to-speech)
+ [Exercise 2: Synthesizing Speech with Plain Text Input \(Console\)](#plain-text-to-speech-console)
+ [Next Step](#gs-console-next-step)

## Exercise 1: Synthesizing Speech Quick Start \(Console\)<a name="quick-start-text-to-speech"></a>

The Quick Start walks you through the fastest way to test the Amazon Polly speech synthesis for speech quality\. When you select the **Text\-to\-Speech** tab, the text field for entering your text is pre\-loaded with example text so you can quickly try out Amazon Polly\.

**To quickly test Amazon Polly \(Console\)**

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Choose the **Text\-to\-Speech** tab\.

1. Turn off **SSML**\. 

1. Under **Engine**, choose `Standard` or `Neural`\. 

1. Choose a language and AWS Region, then choose a voice\. If you choose `Neural` for **Engine**, only the languages and voices that support NTTS are available\. All Standard voices are disabled\.

1. Choose **Listen**\.

For more in\-depth testing, see the following topics:
+ [Exercise 2: Synthesizing Speech with Plain Text Input \(Console\)](#plain-text-to-speech-console)
+ [Using SSML \(Console\)](ssml-to-speech-console.md)
+ [Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech)

## Exercise 2: Synthesizing Speech with Plain Text Input \(Console\)<a name="plain-text-to-speech-console"></a>

The following procedure synthesizes speech using plain text input\. Note how "W3C" and the date "10/3" \(October 3rd\) are synthesized\.

**To synthesize speech using plain text input \(console\)**

1. After logging on to the Amazon Polly console, choose **Try Amazon Polly**, and then choose the **Text\-to\-Speech** tab\. 

1. Turn off **SSML**\.

1. Type or paste this text into the input box\.

   ```
   He was caught up in the game. 
   In the middle of the 10/3/2014 W3C meeting
   he shouted, "Score!" quite loudly.
   ```

1. For **Engine**, choose `Standard` or `Neural`\. 

1. Choose a language and AWS Region, then choose a voice\. If you choose `Neural` for **Engine**, only the languages and voices that support NTTS are available\. All Standard voices are disabled\.

1. To listen to the speech immediately, choose **Listen**\.

1. To save the speech to a file, do one of the following:

   1. Choose **Download**\.

   1. To change to a different file format, expand **Additional settings**, turn on **Speech file format settings**, choose the file format that you want, and then choose **Download**\.

For more in\-depth examples, see the following topics:
+ [Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech)
+ [Using SSML \(Console\)](ssml-to-speech-console.md)

## Next Step<a name="gs-console-next-step"></a>

[Step 3: Getting Started \(AWS CLI\)](getting-started-cli.md)