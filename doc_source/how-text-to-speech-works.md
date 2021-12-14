# How Amazon Polly Works<a name="how-text-to-speech-works"></a>

Amazon Polly converts input text into life\-like speech\. You call one of the speech synthesis methods, provide the text that you want to synthesize, choose one of the Neural Text\-to\-Speech \(NTTS\) or Standard Text\-to\-Speech \(TTS\) voices, and specify an audio output format\. Amazon Polly then synthesizes the provided text into a high\-quality speech audio stream\.


+  **Input text** – Provide the text that you want to synthesize, and Amazon Polly returns an audio stream\. You can provide the input as plain text or in Speech Synthesis Markup Language \(SSML\) format\. With SSML you can control various aspects of speech, such as pronunciation, volume, pitch, and speech rate\. For more information, see [Generating Speech from SSML Documents](ssml.md)\.

   
+ **Available voices** – Amazon Polly provides a portfolio of languages and a variety of voices, including a bilingual voice \(for both English and Hindi\)\. For most languages you can choose from several voices, both male and female\. When launching a speech synthesis task, you specify the voice ID, and then Amazon Polly uses this voice to convert the text to speech\. Amazon Polly is not a translation service—the synthesized speech is in the same language as the text\. However, if the text is in a different language than designated for the voice, numbers represented as digits \(for example, *53*, not *fifty\-three*\) are synthesized in the language of the voice and not the text\. For more information, see [Voices in Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/voices-in-polly.html)\. 

   
+ **Output format** – Amazon Polly can deliver the synthesized speech in multiple formats\. You can select the audio format that suits your needs\. For example, you might request the speech in the MP3 or Ogg Vorbis format for consumption by web and mobile applications\. Or, you might request the PCM output format for consumption by AWS IoT devices and telephony solutions\.

  

## What's Next?<a name="how-it-works-what-next"></a>

If you are new to Amazon Polly, we recommend that you to read the following topics in order:
+ [Getting Started with Amazon Polly](getting-started.md)
+  [Example Applications](examples-for-using-polly.md) 
+  [Quotas in Amazon Polly](limits.md) 



