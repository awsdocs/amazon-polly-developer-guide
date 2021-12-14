# Customizing Your WordPress Page<a name="CustomizingWordPress"></a>

You can use several options for customizing your WordPress content to make it work more effectively with the Amazon Polly WordPress plugin:
+ [Adjust the plugin settings to fine tune the audio files](#adjustsettings)
+ [Use SSML in your content to modify how it will be spoken](#SSML-wordpress-options)
+ [Use Audio Only and Word Only tags in your content](#WP-audiowordonly)

## Adjust the plugin settings to fine tune the audio files<a name="adjustsettings"></a>

The **AWS for WordPress** plugin settings have three options that can help you customize the sound of your WordPress text for the audio file:
+  Voice name: The voice name and language selected enables you to select the gender of the Amazon Polly voice\. Specific voices are available for each language, and you have several options within each gender in many languages\. For more information, see [Voices in Amazon Polly](voicelist.md)\.
+  Automated breaths: If enabled, Amazon Polly will automatically insert breathing sounds into your content at appropriate locations\. Setting this option will only enable you to use automated breaths and not manually set them\. For more information, see [automated breathing](https://docs.aws.amazon.com/polly/latest/dg/supportedtags.html#breath-tag)\.
+ Audio speed: This option enables you to alter the speed of delivery of the audio version of your content, ranging from 20% to 200% of the default speed of the voice\.

## Use SSML in your content to modify how it will be spoken<a name="SSML-wordpress-options"></a>

Amazon Polly itself supports multiple SSML tags that enable you to control many aspects of how Amazon Polly generates speech from the text you provide\. \(For more information about SSML and Amazon Polly, see [Supported SSML Tags](supportedtags.md)\. A few of these tags are echoed in the plug\-in settings when configuring your plug\-in\. Currently, however, only the <break> tag is available for direct use in the **AWS for WordPress** plugin\. 

The <break> tag enables you to add a pause into the spoken version of your text\. You can adjust the length of this pause to meet your particular needs\. The default length of the pause is equivalent to the pause following a comma\. For more information on the <break> tag, see [Supported SSML Tags](supportedtags.md)\.

To use SSML tags to enhance your WordPress text, the Enable SSML support option must be selected in Amazon Polly Settings on the **WordPress Admin** page\. The **Store audio in Amazon S3 option** must also be selected because audio files with SSML tags need to be stored in an S3 bucket\.

## Use Audio Only and Word Only tags in your content<a name="WP-audiowordonly"></a>

Sometimes you want to add something to your audio podcast but don't want it to display in the browser\. Or you want something to show in the browser but not include it in the audio file\. This can be done with the `Audio Only` and `Word Only` tags, which you place in the WordPress content to control which part of the text will be displayed or spoken\.

**To convert text to audio but not display it in the browser**

1. Isolate the selected text on your WordPress page by placing an empty line above and below it\.

1. On the line above the selected text, insert the following tag:

   `-AMAZONPOLLY-ONLYAUDIO-START-`

1. On the line following the text, insert the following tag:

   `-AMAZONPOLLY-ONLYAUDIO-END-`

You can use the same procedure to show text in the browser without including it in the audio file by using the tags `-AMAZONPOLLY-ONLYWORD-START-` and `-AMAZONPOLLY-ONLYWORD-END-` in the same manner\.

For example:

```
     Initial text of your blog displayed in the browser and heard in the audio file.]
     -AMAZONPOLLY-ONLYAUDIO-START-
     [This part will not be displayed in the browser but will be heard in the audio file.]
     -AMAZONPOLLY-ONLYAUDIO-END-
     [Subsequent text of your blog displayed in the browser and heard in the audio file.]
```

and

```
     [Initial text of your blog displayed in the browser and heard in the audio file.]
     -AMAZONPOLLY-ONLYWORD-START-
     This part will be displayed in the browser but will not be heard in the audio file.]
     -AMAZONPOLLY-ONLYWORD-END-
     Subsequent text of your blog displayed in the browser and heard in the audio file.
```

## Adding Translated Text to Your Post<a name="WP-translate"></a>

The **AWS for WordPress** plugin uses Amazon Translate to create translated versions of your post in one or more other languages\. In addition to English, four languages are available for this service: Spanish, French, German, and Portuguese\. The languages to be used and the voices for those languages can be configured on the **Settings** page under Amazon Translate configuration\.

**To translate your WordPress post into other languages**

1. On the **Add New Post** page, create and publish your new WordPress post\.

1. On the same page, ensure that the **Enable Amazon Polly option** is chosen\.

1. To see the approximate cost of creating audio files in the original languages plus any additionally selected languages, choose **How much will this cost to convert?** Choose **OK** to return to the **Add New Post** page\.

1. Choose **Translate**



**To set the languages into which you translate your post**

1. On the **Settings** page, under **Amazon Translate configuration**, choose the language of your post from the **Source language** drop\-down list\. 

1. Under **Target languages**, choose the languages into which you want to translate your post\.

1. From the **Voice** dropdown list, choose the voice you want to use for each language selected\.

1. Enter a label for the language choice\.

1. Choose **Save Changes**\.