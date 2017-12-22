# LexiconAttributes<a name="API_LexiconAttributes"></a>

Contains metadata describing the lexicon such as the number of lexemes, language code, and so on\. For more information, see [Managing Lexicons](http://docs.aws.amazon.com/polly/latest/dg/managing-lexicons.html)\.

## Contents<a name="API_LexiconAttributes_Contents"></a>

 **Alphabet**   
Phonetic alphabet used in the lexicon\. Valid values are `ipa` and `x-sampa`\.  
Type: String  
Required: No

 **LanguageCode**   
Language code that the lexicon applies to\. A lexicon with a language code such as "en" would be applied to all English languages \(en\-GB, en\-US, en\-AUS, en\-WLS, and so on\.  
Type: String  
Valid Values:` cy-GB | da-DK | de-DE | en-AU | en-GB | en-GB-WLS | en-IN | en-US | es-ES | es-US | fr-CA | fr-FR | is-IS | it-IT | ko-KR | ja-JP | nb-NO | nl-NL | pl-PL | pt-BR | pt-PT | ro-RO | ru-RU | sv-SE | tr-TR`   
Required: No

 **LastModified**   
Date lexicon was last modified \(a timestamp value\)\.  
Type: Timestamp  
Required: No

 **LexemesCount**   
Number of lexemes in the lexicon\.  
Type: Integer  
Required: No

 **LexiconArn**   
Amazon Resource Name \(ARN\) of the lexicon\.  
Type: String  
Required: No

 **Size**   
Total size of the lexicon, in characters\.  
Type: Integer  
Required: No

## See Also<a name="API_LexiconAttributes_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/LexiconAttributes) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/LexiconAttributes) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/polly-2016-06-10/LexiconAttributes) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/polly-2016-06-10/LexiconAttributes) 