# Step 3\.2: Getting Started Exercise Using the AWS CLI<a name="get-started-cli-exercise"></a>

Now you can test the speech synthesis offered by Amazon Polly\. In this exercise, you call the `SynthesizeSpeech` operation by passing in sample text\. You can save the resulting audio as a file and verify its content\. 

If you specified one of the Amazon Polly supported regions when you configured the AWS CLI, you can omit the following line from the AWS CLI code examples\. If you specified a region not supported by Amazon Polly in your AWS CLI configuration \(for example, if you're an existing AWS customer using other services in regions that don't support Amazon Polly\), you must include the following line: 

```
--region polly-supported-aws-region
```

1. Run the `synthesize-speech` AWS CLI command to synthesize sample text to an audio file \(`hello.mp3`\)\. 

   The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

   ```
   aws polly synthesize-speech \
       --output-format mp3 \
       --voice-id Joanna \
       --text 'Hello, my name is Joanna. I learned about the W3C on 10/3 of last year.' \
       hello.mp3
   ```

   In the call to `synthesize-speech`, you provide sample text for the synthesis, the voice to use \(by providing a voice ID, explained in the following step 3\), and the output format\. The command saves the resulting audio to the `hello.mp3` file\. 

   In addition to the MP3 file, the above operation produces the following output to the console\.

   ```
   {
           "ContentType": "audio/mpeg", 
           "RequestCharacters": "71"
   }
   ```

1. Play the resulting `hello.mp3` file to verify the synthesized speech\.

1. You can get the list of available voices by using the `DescribeVoices` operation\. Run the following `describe-voices` AWS CLI command\.

   ```
   aws polly describe-voices
   ```

   In response, Amazon Polly returns the list of all available voices\. For each voice the response provides the following metadata: voice ID, language code, language name, and the gender of the voice\. The following is a sample response:

   ```
   {
       "Voices": [
           {
               "Gender": "Female",
               "Name": "Salli",
               "LanguageName": "US English",
               "Id": "Salli",
               "LanguageCode": "en-US"
           },
           {
               "Gender": "Female",
               "Name": "Joanna",
               "LanguageName": "US English",
               "Id": "Kendra",
               "LanguageCode": "en-US"
           }
       ]
   }
   ```

   Optionally, you can specify the language code to find the available voices for a specific language\. Amazon Polly supports dozens of voices\. The following example lists all the voices for Brazilian Portuguese\.

   ```
   aws polly describe-voices \
       --language-code pt-BR
   ```

   For a list of language codes, see [DescribeVoices](API_DescribeVoices.md)\. These language codes are W3C language identification tags \(*ISO 639 code for the language name*\-*ISO 3166 country code*\)\. For example, en\-US \(US English\), en\-GB \(British English\), and es\-ES \(Spanish\), etc\. 

   You can also use the `help` option in the AWS CLI to get the list of language codes:

   ```
   aws polly describe-voices help
   ```