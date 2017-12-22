# Step 2: Getting Started Using the Console<a name="getting-started-console"></a>

The Amazon Polly console is the easiest way to get started testing and using Amazon Polly's speech synthesizing\. The Amazon Polly console supports synthesizing speech from either plain text or SSML input\.


+ [Exercise 1: Synthesizing Speech Quick Start \(Console\)](#quick-start-text-to-speech)
+ [Exercise 2: Synthesizing Speech \(Plain Text Input\)](#plain-text-to-speech-console)
+ [Next Step](#gs-console-next-step)

## Exercise 1: Synthesizing Speech Quick Start \(Console\)<a name="quick-start-text-to-speech"></a>

The Quick Start walks you through the fastest way to test the Amazon Polly speech synthesis for speech quality\. When you select the **Text\-to\-Speech** tab, the text field for entering your text is pre\-loaded with example text so you can quickly try out Amazon Polly\.

**To quickly test Amazon Polly**

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Choose the **Text\-to\-Speech** tab\.

1. \(Optional\) Choose **SSML**\.

1. Choose a language and region, then choose a voice\.

1. Choose **Listen to speech**\.

For more in\-depth testing, see the following topics:

+ [Exercise 2: Synthesizing Speech \(Plain Text Input\)](#plain-text-to-speech-console)

+ [Using SSML with the Amazon Polly Console](ssml-to-speech-console.md#ssml-console-exercise)

+ [Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech)

## Exercise 2: Synthesizing Speech \(Plain Text Input\)<a name="plain-text-to-speech-console"></a>

The following procedure synthesizes speech using plain text input\. Note how "W3C" and the date "10/3" \(October 3rd\) are synthesized\.

**To synthesize speech using plain text input**

1. After logging on to the Amazon Polly console, choose **Get started**, and then choose the **Text\-to\-Speech** tab\. 

1. Choose the **Plain text** tab\.

1. Type or paste this text into the input box\.

   ```
   He was caught up in the game. 
   In the middle of the 10/3/2014 W3C meeting
   he shouted, "Score!" quite loudly.
   ```

1. For **Choose a language and region**, choose **English US**, then choose the voice you want to use for this text\.

1. To listen to the speech immediately, choose **Listen to speech**\.

1. To save the speech to a file, do one of the following:

   1. Choose **Save speech to MP3**\.

   1. To change to a different file format, choose **Change file format**, choose the file format you want, and then choose **Change**\.

For more in\-depth examples, see the following topics:

+ [Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech)

+ [Using SSML with the Amazon Polly Console](ssml-to-speech-console.md#ssml-console-exercise)

## Next Step<a name="gs-console-next-step"></a>

[Step 3: Getting Started Using the AWS CLI](getting-started-cli.md)