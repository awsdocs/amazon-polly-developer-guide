# Speech Mark Types<a name="using-speechmarks1"></a>

You request speech marks in the AWS CLI using the `speech-mark-types` option for the `synthesize-speech` command\. You specify the metadata elements that you want to return from your input text\. You can request as many as four types of metada but you must specify at least one per request\. No audio output is generated with the request\.

```
--speech-mark-types='["sentence", "word", "viseme", "ssml"]'
```

Amazon Polly generates speech marks using the following elements:

+  **sentence** – Indicates a sentence element in the input text\. 

+  **word** – Indicates a word element in the text\. 

+  **viseme** – Describes the face and mouth movements corresponding to each phoneme being spoken\. For more information, see [Visemes and Amazon Polly](viseme.md)\. 

+  **ssml** – Describes a <mark> element from the SSML input text\. For more information, see [Using SSML](ssml.md)\.