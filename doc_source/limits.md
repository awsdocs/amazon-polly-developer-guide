# Quotas in Amazon Polly<a name="limits"></a>

The following are limits to be aware of when using Amazon Polly\.

## Supported Regions<a name="limits-regions"></a>

For a list of AWS Regions where Amazon Polly is available, see [Amazon Polly Endpoints and Quotas](https://docs.aws.amazon.com/general/latest/gr/pol.html) in the *Amazon Web Services General Reference*\.

Neural voices aren't available in all AWS Regions\. For the Regions that support neural voices, see [Feature and Region Compatibility](NTTS-main.md#ntts-regions) for neural TTS\.

## Throttling<a name="limits-throttle"></a>
+ Throttle rate per account: 100 transactions \(requests or operations\) per second \(tps\) with a burst limit of 120 tps\.

  Concurrent connections per account: 90 
+ Throttle rate per operation:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/polly/latest/dg/limits.html)

## Pronunciation Lexicons<a name="limits-lexicons"></a>
+ You can store up to 100 lexicons per account\.
+ Lexicon names can be an alphanumeric string up to 20 characters long\.
+ Each lexicon can be up to 4,000 characters in size\. \(Note that the size of the lexicon affects the latency of the SynthesizeSpeech operation\.\)
+ You can specify up to 100 characters for each <phoneme> or <alias> replacement in a lexicon\.

For information about using lexicons, see [Managing Lexicons](managing-lexicons.md)\. 

## SynthesizeSpeech API Operation<a name="limits-synthesizespeech"></a>

Note the following limits related to using the `SynthesizeSpeech` API operation:
+ The size of the input text can be up to 3000 billed characters \(6000 total characters\)\. SSML tags are not counted as billed characters\.
+ You can specify up to five lexicons to apply to the input text\.
+ The output audio stream \(synthesis\) is limited to 10 minutes\. After this is reached, any remaining speech is cut off\.

For more information, see [ SynthesizeSpeech ](API_SynthesizeSpeech.md)\. 

**Note**  
Some limitations of the `SynthesizeSpeech` API operation can be bypassed using the `StartSythensizeSpeechTask` API operation\. For more information, see [Creating Long Audio Files](asynchronous.md)\. 

## SpeechSynthesisTask API Operations<a name="limits-long"></a>

Note the following limit relating to using the `StartSpeechSynthesisTask`, `GetSpeechSynthesisTask`, and `ListSpeechSynthesisTasks` API operations:
+ The size of the input text can be up to 100,000 billed characters \(200,000 total characters\)\. SSML tags are not counted as billed characters\.
+ You can specify up to five lexicons to apply to the input text\.

## Speech Synthesis Markup Language \(SSML\)<a name="limits-ssml"></a>

Note the following limits related to using SSML:
+ The `<audio>`, `<lexicon>`, `<lookup>`, and `<voice>` tags are not supported\.
+ `<break>` elements can specify a maximum duration of 10 seconds each\.
+ The `<prosody>` tag doesn't support values for the rate attribute lower than \-80%\.

 For more information, see [Generating Speech from SSML Documents](ssml.md)\.