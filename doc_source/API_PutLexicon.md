# PutLexicon<a name="API_PutLexicon"></a>

Stores a pronunciation lexicon in an AWS Region\. If a lexicon with the same name already exists in the region, it is overwritten by the new lexicon\. Lexicon operations have eventual consistency, therefore, it might take some time before the lexicon is available to the SynthesizeSpeech operation\.

For more information, see [Managing Lexicons](https://docs.aws.amazon.com/polly/latest/dg/managing-lexicons.html)\.

## Request Syntax<a name="API_PutLexicon_RequestSyntax"></a>

```
PUT /v1/lexicons/LexiconName HTTP/1.1
Content-type: application/json

{
   "Content": "string"
}
```

## URI Request Parameters<a name="API_PutLexicon_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [LexiconName](#API_PutLexicon_RequestSyntax) **   <a name="polly-PutLexicon-request-Name"></a>
Name of the lexicon\. The name must follow the regular express format \[0\-9A\-Za\-z\]\{1,20\}\. That is, the name is a case\-sensitive alphanumeric string up to 20 characters long\.   
Length Constraints: Maximum length of 20\.  
Pattern: `[0-9A-Za-z]{1,20}`   
Required: Yes

## Request Body<a name="API_PutLexicon_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [Content](#API_PutLexicon_RequestSyntax) **   <a name="polly-PutLexicon-request-Content"></a>
Content of the PLS lexicon as string data\.  
Type: String  
Length Constraints: Maximum length of 2000000\.  
Required: Yes

## Response Syntax<a name="API_PutLexicon_ResponseSyntax"></a>

```
HTTP/1.1 200
```

## Response Elements<a name="API_PutLexicon_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_PutLexicon_Errors"></a>

 **InvalidLexiconException**   
Amazon Polly can't find the specified lexicon\. Verify that the lexicon's name is spelled correctly, and then try again\.  
HTTP Status Code: 400

 **LexiconSizeExceededException**   
The maximum size of the specified lexicon would be exceeded by this operation\.  
HTTP Status Code: 400

 **MaxLexemeLengthExceededException**   
The maximum size of the lexeme would be exceeded by this operation\.  
HTTP Status Code: 400

 **MaxLexiconsNumberExceededException**   
The maximum number of lexicons would be exceeded by this operation\.  
HTTP Status Code: 400

 **ServiceFailureException**   
An unknown condition has caused a service failure\.  
HTTP Status Code: 500

 **UnsupportedPlsAlphabetException**   
The alphabet specified by the lexicon is not a supported alphabet\. Valid values are `x-sampa` and `ipa`\.  
HTTP Status Code: 400

 **UnsupportedPlsLanguageException**   
The language specified in the lexicon is unsupported\. For a list of supported languages, see [Lexicon Attributes](https://docs.aws.amazon.com/polly/latest/dg/API_LexiconAttributes.html)\.  
HTTP Status Code: 400

## See Also<a name="API_PutLexicon_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/polly-2016-06-10/PutLexicon) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/polly-2016-06-10/PutLexicon) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/PutLexicon) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/PutLexicon) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/polly-2016-06-10/PutLexicon) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/polly-2016-06-10/PutLexicon) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/polly-2016-06-10/PutLexicon) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/polly-2016-06-10/PutLexicon) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/polly-2016-06-10/PutLexicon) 