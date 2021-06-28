# Speech Mark Types<a name="using-speechmarks1"></a>

You request speech marks using the [SpeechMarkTypes](https://docs.aws.amazon.com/polly/latest/dg/API_StartSpeechSynthesisTask.html#polly-StartSpeechSynthesisTask-request-SpeechMarkTypes) option for either the [SynthesizeSpeech](https://docs.aws.amazon.com/polly/latest/dg/API_SynthesizeSpeech.html) or [StartSpeechSynthesisTask](https://docs.aws.amazon.com/polly/latest/dg/API_StartSpeechSynthesisTask.html) commands\. You specify the metadata elements that you want to return from your input text\. You can request as many as four types of metadata but you must specify at least one per request\. No audio output is generated with the request\.

In the AWS CLI, for example:

```
--speech-mark-types='["sentence", "word", "viseme", "ssml"]'
```

Amazon Polly generates speech marks using the following elements:
+  **sentence** – Indicates a sentence element in the input text\. 
+  **word** – Indicates a word element in the text\. 
+  **viseme** – Describes the face and mouth movements corresponding to each phoneme being spoken\. For more information, see [Visemes and Amazon Polly](viseme.md)\. 
+  **ssml** – Describes a <mark> element from the SSML input text\. For more information, see [Generating Speech from SSML Documents](ssml.md)\.