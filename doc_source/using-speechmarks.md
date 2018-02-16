# Using Speech Marks<a name="using-speechmarks"></a>

## Requesting Speech Marks<a name="requestingspeechmarks"></a>

To request speech marks for input text, use the `synthesize-speech` command\. Besides the input text, the following elements are required to return this metadata: 

+ `output-format`

  Amazon Polly supports only the JSON format when returning speech marks\. 

  ```
  --output-format json
  ```

  If you use an unsupported output format, Amazon Polly throws an exception\.

+ `voice-id`

  To ensure that the metadata matches the associated audio stream, specify the same voice that is used to generate the synthesized speech audio stream\. The available voices don't have identical speech rates\. If you use a voice other than the one used to generate the speech, the metadata will not match the audio stream\.

  ```
  --voice-id Joanna
  ```

+ `speech-mark-types`

  Specify the type or types of speech marks you want\. You can request any or all of the speech mark types, but must specify at least one type\.

  ```
  --speech-mark-types='["sentence", "word", "viseme", "ssml"]'
  ```

+ `text-type`

  Plain text is the default input text for Amazon Polly, so you must use `text-type ssml` if you want to return SSML speech marks\.

+ `outfile`

  Specify the output file to which the metadata is written\.

  ```
  MaryLamb.txt 
  ```

 

The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly synthesize-speech \
  --output-format json \
  --voice-id Voice ID \
  --text 'Input text' \
  --speech-mark-types='["sentence", "word", "viseme"]' \
  outfile
```

## Speech Mark Output<a name="output"></a>

Amazon Polly returns speech mark objects in a line\-delimited JSON stream\. A speech mark object contains the following fields:

+  **time** – the timestamp in milliseconds from the beginning of the corresponding audio stream

+  **type** – the type of speech mark \(sentence, word, viseme, or ssml\)\.

+  **start** – the offset in bytes of the start of the object in the input text \(not including viseme marks\)

+  **end** – the offset in bytes of the object's end in the input text \(not including viseme marks\)

+  **value** – this varies depending on the type of speech mark

  +  **SSML**: <mark> SSML tag

  +  **viseme**: the viseme name

  +  **word** or **sentence**: a substring of the input text, as delimited by the start and end fields

For example, Amazon Polly generates the following `word` speech mark object from the text "Mary had a little lamb":

```
{"time":373,"type":"word","start":5,"end":8,"value":"had"}
```

The described word \("had"\) begins 373 milliseconds after the audio stream begins, and starts at byte 5 and ends at byte 8 of the input text\. 

**Note**  
This metadata is for the `Joanna` voice\-id\. If you use another voice with the same input text, the metadata might differ\.

 