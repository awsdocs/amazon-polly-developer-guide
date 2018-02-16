# Common Questions<a name="faq-developer"></a>

This topic provides answers to questions that are commonly asked about Amazon Polly\.


+ [General Questions](#faqs-general)
+ [Content Rendering](#faqs-render)
+ [Voices](#faqs-voices)
+ [Data Security and Confidentiality](#faqs-security)

## General Questions<a name="faqs-general"></a>

**Q: Can I save the synthesized speech?**

You can save the output of the synthesis for use on your own system\. You can also call Amazon Polly, and then encrypt the file with any encryption key and store it in Amazon Simple Storage Service \(Amazon S3\) or any other secure storage\. The Amazon Polly `SynthesizeSpeech` call is stateless and is not associated with a customer identity\. You can't retrieve it from Amazon Polly later\.

## Content Rendering<a name="faqs-render"></a>

**Q: Some of my text coming out with the stress on the wrong syllable when it is spoken by Amazon Polly\. I've even tried using an acute accent \(U\+0301\) to mark the stress but it is still on the wrong syllable\. How can I fix this?**

Amazon Polly doesn't currently recognize an acute accent \(U\+0301\) as indicating syllable stress in a word\. However, there are two ways you can change the stress in a word\. You can use an IPA phone and ssml tags to alter the pronunciation of the word\. For more information, see [SSML Tags in Amazon Polly](supported-ssml.md)\. In some languages, you can also use an apostrophe immediately after the syllable to indicate a change in stress\. For instance, in Russian, the words страны́ and стра́ны have different stresses \(marked here with an acute accent\)\. However, because of the identical spelling, Amazon Polly will pronounce them both with the stress on the final syllable, according to standard language usage\. You can use an apostrophe to mark the alternatively stressed syllable, as in стран'ы, and the Amazon Polly will stress the correct syllable\. 

 **Q: When I use bullet points in my text, Amazon Polly doesn't render them correctly\. It says "minus" every time it encounters one\. What do I do?** 

If you use "\-" \(a hyphen\) as a substitute for a bullet point, in some languages,Amazon Polly renders it as a minus sign\. If you want to use hyphens as substitutes for a bullet point, you can do so with a lexicon entry\. For more information, see [Managing Lexicons](managing-lexicons.md)\. 

**Q: I use the "/" \(forward slash\) symbol frequently in my text, especially when saying "and/or" and "yes/no\." How does Amazon Polly render this?**

In English, Amazon Polly renders "and/or" in speech as "and or\." Currently, this rule isn't available in other languages\. In languages other than English, Amazon Polly renders "yes/no" as "yes slash no\." If you want to change this behavior, you can use a lexicon entry\. For more information, see [Managing Lexicons](managing-lexicons.md)\. 

**Q: When I use text from an existing source in order to synthesize speach using the AWS CLI on a Linux machine, some UTF\-8 characters do not seem work with Amazon Polly, even though the same characters seem to work properly using the Console\. What is happening?**

This is based in how the Unix Shell handles Unicode and isn't a Amazon Polly\-specific problem\. Two options are available: you can find the problem characters and replace them in the input text, or you can u tilize an alternate means of accessing Amazon Polly that does not experience this issue, such as the PHP interface\. This is a known issue that we are working to address and only a few uncommon unicode characters have this issue\. 

**Q: When I try to synthesize text from a source containing International Phonetic Alphabet \(IPA\) symbols, Amazon Polly doesn't recognize them and even tries to pronounce some of them\. How do I fix this?**

Amazon Polly does not recognize IPA symbols unless SSML \(Speech Synthesis Markup Language\) is used to delineate it\. However, since small sections of IPA symbols usually indicate a pronunciation guide for a reader, in many cases, this section can be safely removed from the input text by simple deletion\. You can also use a lexicon to change the way this is rendered by Amazon Polly\. For more information, see [Using SSML](ssml.md) and [Managing Lexicons](managing-lexicons.md)\.

## Voices<a name="faqs-voices"></a>

**Q: How can I listen to a voice to see if I want to use it?**

You can listen to any voice supported by Amazon Polly by synthesizing a short text through the Amazon Polly console or by using the `synthesize-speech` API with the AWS CLI\. You can select any supported voice in the console and listen to the voice by running a sample text\. For more information, see [Exercise 1: Synthesizing Speech Quick Start \(Console\)](getting-started-console.md#quick-start-text-to-speech)\. In the AWS CLI, you can use the `voice-id` of the voice you want to hear when you run the `synthesize-speech` API\. For more information, see [Step 3\.2: Getting Started Exercise Using the AWS CLI](get-started-cli-exercise.md)\.

**Q: How long will the voices be available? If I choose a voice for my application now, will it still be available in five years?**

To ensure continuous support for customers, we don't plan to retire any voices\. This applies to both currently available and future voices\. 

## Data Security and Confidentiality<a name="faqs-security"></a>

**Q: Can I choose to mask certain data fields so that they are not stored?\(For instance, if I convert text with some sensitive data, but don't want it stored on the AWS systems, can I mask it?**

 No\. Amazon Polly doesn’t currently support this functionality\.

**Q: The text I want to use with Amazon Polly is confidential\. How is my data protected?**

All text submissions are protected by Secure Sockets Layer \(SSL\) while in transit, and are stored using RSA encryption\. We keep the service logs and text separate, so that the content can't be linked with the customer ID\. As a result, Amazon Polly does not associate text submissions with customer identity\. 

**Q: How long is data retained?**

Amazon Polly retains data for 14 days\. After that, it's automatically deleted from our system\. 

**Q: Can I request that data be wiped earlier?**

Yes, you can request that by contacting [AWS Support](https://aws.amazon.com/contact-us/?nc2=h_l2_su)\. 