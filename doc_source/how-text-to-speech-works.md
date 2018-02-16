# Amazon Polly: How It Works<a name="how-text-to-speech-works"></a>

Amazon Polly converts input text into life\-like speech\. You just need to call the `SynthesizeSpeech` method, provide the text you wish to synthesize, select one of the available Text\-to\-Speech \(TTS\) voices, and specify an audio output format\. Amazon Polly then synthesizes the provided text into a high\-quality speech audio stream\.

+  **Input text** – Provide the text you want to synthesize, and Amazon Polly returns an audio stream\. You can provide the input as plain text or in Speech Synthesis Markup Language \(SSML\) format\. With SSML you can control various aspects of speech such as pronunciation, volume, pitch, and speech rate\. For more information, see [Using SSML](ssml.md)\.

   

+ **Available voices** – Amazon Polly provides a portfolio of multiple languages and a variety of voices\. For most languages you can select from several different voices, including both male and female\. You only need to specify the voice name when calling the `SynthesizeSpeech` operation, and then the service uses this voice to convert the text to speech\. Amazon Polly is not a translation service—the synthesized speech is in the language of the text\. Numbers using digits \(for example, *53*, not *fifty\-three*\) are synthesized in the language of the voice\.

   

+ **Output format** – Amazon Polly can deliver the synthesized speech in multiple formats\. You can select the audio format that suits your needs\. For example, you might request the speech in the MP3 or Ogg Vorbis format to consume in web and mobile applications\. Or, you might request the PCM output format for AWS IoT devices and telephony solutions\.

## What's Next?<a name="how-it-works-what-next"></a>

If you are new to Amazon Polly, we recommend that you to read the following topics in order:

+ [Getting Started with Amazon Polly](getting-started.md)

+  [Example Applications](examples-for-using-polly.md) 

+  [Limits in Amazon Polly](limits.md) 