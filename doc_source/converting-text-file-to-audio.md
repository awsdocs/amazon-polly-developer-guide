# Converting a Text File to Audio<a name="converting-text-file-to-audio"></a>

To convert a text file to audio, copy it to Polly\-batch\-processor's S3 bucket\. The Lambda function begins processing the file immediately\.

**To prepare a document for the conversion**

1. Encode it in `UTF-8` format\.

1. Save it in text format \(with the `.txt` extension\)\.

**To upload a file to the S3 bucket**

+ In the AWS CLI, type the following command\.
**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

  ```
  aws s3api put-object
     --bucket bucket-name 
     --key books/filename.txt 
     --body filename.txt 
     --tagging "voiceid=voice&author=Firstname%20Lastname&title=The%20Content%20Title"
  ```

  To change default settings or provide more information, you can add the following optional Amazon S3 object tags:

  + To prevent the application from consolidating the audio files into a single MP3 file, upload the document with the S3 object tag name `consolidated` and value `false`: 

    ```
    --tagging "consolidated=false"
    ```

    You can combine this command with other S3 object tags, such as `voiceid`, `author`, and `title`\.

  + To use a voice other than the default voice for your language \(for English, the default voice is Joanna\), apply the `voiceid` tag and specify another voice\.

  + To make it easier to manage your audio files, add S3 `Author` and `Title` tags\. 

  The application sends you an email with the URL for the consolidated file or the list of files\.

For example, to convert the text of Oscar Wilde's story "The Happy Prince" to an audio file, type the following command in the AWS CLI\. It uploads the document, tagged with the author's name and the title of the story, and uses the Brian voice\.

```
aws s3api put-object 
  --bucket bucket-name    
  --key books/the-happy-prince.txt 
  --body the-happy-prince.txt 
  --tagging "voiceid=Brian&author=Oscar%20Wilde&title=The%20Happy%20Prince"
```

## Next Step<a name="polly-batch-next-step-4"></a>

[Cleaning Up](cleaning-up.md)