# Managing Lexicons Using the Amazon Polly Console<a name="managing-lexicons-console"></a>

You can use the Amazon Polly console to upload, download, apply, filter, and delete lexicons\. The following procedures demonstrate each of these processes\. 

## Uploading Lexicons Using the Console<a name="managing-lexicons-console-upload"></a>

To use a pronunciation lexicon, you must first upload it\. There are two locations on the console from which you can upload a lexicon, the **Text\-to\-Speech** tab and the **Lexicons** tab\.

The following processes describe how to add lexicons that you can use to customize how words and phrases uncommon to the chosen language are pronounced\. <a name="upload-lexicon-lexicons-tab"></a>

**To add a lexicon from the Lexicons tab**

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Choose the **Lexicons** tab\.

1. Choose **Upload lexicon**\.

1. Provide a name for the lexicon and then use **Choose a lexicon file** to find the lexicon to upload\. You can only upload PLS files with \.pls or \.xml extensions\.

1. Choose **Upload lexicon**\. If a lexicon by the same name \(whether a \.pls or \.xml file\) already exists, uploading the lexicon overwrites the existing lexicon\.<a name="upload-lexicon-tts-tab"></a>

**To add a lexicon from the Text\-to\-Speech tab**

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Choose the **Text\-to\-Speech** tab\.

1. Expand **Additional settings**, turn on **Customize pronunciation,** and then choose **Upload lexicon**\.

1. Provide a name for the lexicon and then use **Choose a lexicon file** to find the lexicon to upload\. You can only use PLS files with \.pls or \.xml extensions\. 

1. Choose **Upload lexicon**\. If a lexicon with the same name \(whether a \.pls or \.xml file\) already exists, uploading the lexicon overwrites the existing lexicon\.

## Applying Lexicons Using the Console \(Synthesize Speech\)<a name="managing-lexicons-console-synthesize-speech"></a>

The following procedure demonstrates how to apply a lexicon to your input text by applying the `W3c.pls` lexicon to substitute "World Wide Web Consortium" for "W3C"\. If you apply multiple lexicons to your text they are applied in a top\-down order with the first match taking precedence over later matches\. A lexicon is applied to the text only if the language specified in the lexicon is the same as the language chosen\.

You can apply a lexicon to plain text or SSML input\.

**Example – Applying the W3C\.pls Lexicon**  
To create the lexicon you'll need for this exercise, see [Using the PutLexicon Operation](gs-put-lexicon.md)\. Use a plain text editor to create the W3C\.pls lexicon shown at the top of the topic\. Remember where you save this file\.  

**To apply the W3C\.pls lexicon to your input**

In this example we introduce a lexicon to substitute "World Wide Web Consortium" for "W3C"\. Compare the results of this exercise with that of [Using SSML \(Console\)](ssml-to-speech-console.md) for both US English and another language\.

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Do one of the following:
   + Turn off **SSML** and then type or paste this text into the text input box\.

     ```
     He was caught up in the game. 
     In the middle of the 10/3/2014 W3C meeting 
     he shouted, "Score!" quite loudly.
     ```
   + Turn on **SSML** and then type or paste this text into the text input box\.

     ```
     <speak>He wasn't paying attention.<break time="1s"/>
     In the middle of the 10/3/2014 W3C meeting 
     he shouted, "Score!" quite loudly.</speak>
     ```

1. From the **Language** list, choose **English, US**, then choose the voice you want to use for this text\.

1. Expand **Additional settings** and turn on **Customize pronunciation\.**

1. From the list of lexicons, choose `W3C (English, US)`\.

   If the `W3C (English, US)` lexicon is not listed, choose **Upload lexicon** and upload it, then choose it from the list\. To create this lexicon, see [Using the PutLexicon Operation](gs-put-lexicon.md)\.

1. To listen to the speech immediately, choose **Listen**\.

1. To save the speech to a file,

   1. Choose **Download**\.

   1. To change to a different file format, turn on **Speech file format settings**, choose the file format you want, and then choose **Download**\.
Repeat the previous steps, but choose a different language and notice the difference in the output\.

## Filtering the Lexicon List Using the Console<a name="managing-lexicons-console-filter"></a>

The following procedure describes how to filter the lexicons list so that only lexicons of a chosen language are displayed\.<a name="filter-and-choose-lexicons"></a>

**To filter the lexicons listed by language**

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Choose the **Lexicons** tab\.

1. Choose **Any language**\.

1. From the list of languages, choose the language you want to filter on\.

   The list displays only the lexicons for the chosen language\.

## Downloading Lexicons Using the Console<a name="managing-lexicons-console-download"></a>

The following process describes how to download one or more lexicons\. You can add, remove, or modify lexicon entries in the file and then upload it again to keep your lexicon up\-to\-date\. <a name="download-lexicon"></a>

**To download one or more lexicons**

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Choose the **Lexicons** tab\.

1. Choose the lexicon or lexicons you want to download\.

   1. To download a single lexicon, choose its name from the list\.

   1. To download multiple lexicons as a single compressed archive file, select the check box next to each entry in the list that you want to download\.

1. Choose **Download**\.

1. Open the folder where you want to download the lexicon\.

1. Choose **Save**\.

## Deleting a Lexicon Using the Console<a name="managing-lexicons-console-delete"></a><a name="delete-lexicon"></a>

**To delete a lexicon**

The following process describes how to delete a lexicon\. After deleting the lexicon, you must add it back before you can use it again\. You can delete one or more lexicons at the same time by selecting the check boxes next to individual lexicons\.

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Choose the **Lexicons** tab\.

1. Choose one or more lexicons that you want to delete from the list\.

1. Choose **Delete**\.

1. Enter confirmation text and then choose **Delete** to remove the lexicon from the Region or **Cancel** to keep it\.