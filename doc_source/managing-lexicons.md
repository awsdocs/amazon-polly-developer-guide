# Managing Lexicons<a name="managing-lexicons"></a>

Pronunciation lexicons enable you to customize the pronunciation of words\. Amazon Polly provides API operations that you can use to store lexicons in an AWS region\. Those lexicons are then specific to that particular region\. You can use one or more of the lexicons from that region when synthesizing the text by using the `SynthesizeSpeech` operation\. This applies the specified lexicon to the input text before the synthesis begins\. For more information, see [SynthesizeSpeech](API_SynthesizeSpeech.md)\.

**Note**  
These lexicons must conform with the Pronunciation Lexicon Specification \(PLS\) W3C recommendation\. For more information, see [Pronunciation Lexicon Specification \(PLS\) Version 1\.0](https://www.w3.org/TR/pronunciation-lexicon/) on the W3C website\. 

The following are examples of ways to use lexicons with speech synthesis engines:

+ Common words are sometimes stylized with numbers taking the place of letters, as with "g3t sm4rt" \(get smart\)\. Humans can read these words correctly\. However, a Text\-to\-Speech \(TTS\) engine reads the text literally, pronouncing the name exactly as it is spelled\. This is where you can leverage lexicons to customize the synthesized speech by using Amazon Polly\. In this example, you can specify an alias \(get smart\) for the word "g3t sm4rt" in the lexicon\. 

+ Your text might include an acronym, such as W3C\. You can use a lexicon to define an alias for the word W3C so that it is read in the full, expanded form \(World Wide Web Consortium\)\.

Lexicons give you additional control over how Amazon Polly pronounces words uncommon to the selected language\. For example, you can specify the pronunciation using a phonetic alphabet\. For more information, see [Pronunciation Lexicon Specification \(PLS\) Version 1\.0](https://www.w3.org/TR/pronunciation-lexicon/) on the W3C website\.


+ [Applying Multiple Lexicons](lexicons-applying.md)
+ [Managing Lexicons Using the Amazon Polly Console](managing-lexicons-console.md)
+ [Managing Lexicons Using the AWS CLI](managing-lexicons-cli.md)