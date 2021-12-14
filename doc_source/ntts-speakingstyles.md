# NTTS Newscaster Speaking Style<a name="ntts-speakingstyles"></a>

People use different speaking styles, depending on context\. Casual conversation, for example, sounds very different from a TV or radio newscast\. Because of the way standard voices are made, they can't produce different speaking styles\. However, neural voices can\. They can be trained for a specific speaking style, with the variations and emphasis on certain parts of speech inherent in that style\.

In addition to the default neural voices, Amazon Polly provides a newscaster speaking style that uses the neural system to generate speech in the style of a TV or radio newscaster\. The Newscaster style is available with the Matthew and Joanna voices in US English \(en\-US\), the Lupe voice in US Spanish \(es\-US\), and the Amy voice in British English \(en\-GB\)\.

To use the Newscaster style, first choose the neural engine and then use the syntax described in the following steps in your input text\.

**Note**  
To use any neural speaking style, you must use one of the AWS Regions that support neural voices\. This option is not available in all Regions\. For more information, see [Feature and Region Compatibility](NTTS-main.md#ntts-regions)\. 

**To apply the Newscaster style \(console\)**

1. Open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Make sure that you are using an AWS Region where neural voices are supported\.

1. On the Text\-to\-Speech page, for **Engine**, choose **Neural**\. 

1. Choose the language and voice you want to use\.

   Only Matthew and Joanna for US English \(en\-US\), Lupe for US Spanish \(es\-US\), and Amy for British English \(en\-GB\) are available in the newscaster voice\.

1. Turn on **SSML**\.

1. Add input text to your text\-to\-speech request using the Newscaster style SSML syntax\.

   ```
   <amazon:domain name="news">text</amazon:domain>
   ```

   For example, you might use the newscaster tag as follows: 

   ```
   <speak> 
   <amazon:domain name="news"> 
   From the Tuesday, April 16th, 1912 edition of The Guardian newspaper: 
   
   The maiden voyage of the White Star liner Titanic, the largest ship ever launched 
   ended in disaster. 
   
   The Titanic started her trip from Southampton for New York on Wednesday. Late on 
   Sunday night she struck an iceberg off the Grand Banks of Newfoundland. By 
   wireless telegraphy she sent out signals of distress, and several liners were 
   near enough to catch and respond to the call.
   </amazon:domain> 
   </speak>
   ```

1. Choose **Listen**\.



**To apply the Newscaster style \(CLI\)**

1. In your API request, include the engine parameter with the `neural` value:

   ```
     --engine neural
   ```

1. Add input text to your API request using the Newscaster style SSML syntax\.

   ```
   <amazon:domain name="news">text</amazon:domain>
   ```

   For example, you might use the newscaster tag as follows: 

   ```
   <speak> 
   <amazon:domain name="news"> 
   From the Tuesday, April 16th, 1912 edition of The Guardian newspaper: 
   
   The maiden voyage of the White Star liner Titanic, the largest ship ever launched 
   ended in disaster. 
   
   The Titanic started her trip from Southampton for New York on Wednesday. Late on 
   Sunday night she struck an iceberg off the Grand Banks of Newfoundland. By 
   wireless telegraphy she sent out signals of distress, and several liners were 
   near enough to catch and respond to the call.
   </amazon:domain> 
   </speak>
   ```



For more information about SSML, see [Supported SSML Tags](supportedtags.md)\.