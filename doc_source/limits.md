# Limits in Amazon Polly<a name="limits"></a>

The following are limits to be aware of when using Amazon Polly\.

## Supported Regions<a name="limits-regions"></a>

For a list of AWS Regions where Amazon Polly is available, see [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html#pol_region) in the *Amazon Web Services General Reference*\.

## Throttling<a name="limits-throttle"></a>

+ Throttle rate per account: 100 transactions \(requests\) per second \(tps\) with a burst limit of 120 tps\.

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

Note the following limits related to using the SynthesizeSpeech API operation:

+ The size of the input text can be up to 1500 billed characters \(3000 total characters\)\. SSML tags are not counted as billed characters\.

+ You can specify up to five lexicons to apply to the input text\.

+ The output audio stream \(synthesis\) is limited to 5 minutes, after which, any remaining speech is cut off\.

For more information, see [SynthesizeSpeech](API_SynthesizeSpeech.md)\. 

**Note**  
Some limitations of the `SynthesizeSpeech` API operation can be bypassed using AWS Batch or other services\.  For more information on AWS Batch, see [What Is AWS Batch?](http://docs.aws.amazon.com/batch/latest/userguide/what-is-batch.html)

## Speech Synthesis Markup Language \(SSML\)<a name="limits-ssml"></a>

Note the following limits related to using SSML:

+ The `<audio>`, `<lexicon>`, `<lookup>`, and `<voice>` tags are not supported\.

+ `<break>` elements can specify a maximum duration of 10 seconds each\.

+ The `<prosody>` tag doesn't support values for the rate attribute lower than \-80%\.

 For more information, see [Using SSML](ssml.md)\.