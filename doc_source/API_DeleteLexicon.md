# DeleteLexicon<a name="API_DeleteLexicon"></a>

Deletes the specified pronunciation lexicon stored in an AWS Region\. A lexicon which has been deleted is not available for speech synthesis, nor is it possible to retrieve it using either the `GetLexicon` or `ListLexicon` APIs\.

For more information, see [Managing Lexicons](https://docs.aws.amazon.com/polly/latest/dg/managing-lexicons.html)\.

## Request Syntax<a name="API_DeleteLexicon_RequestSyntax"></a>

```
DELETE /v1/lexicons/LexiconName HTTP/1.1
```

## URI Request Parameters<a name="API_DeleteLexicon_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [ LexiconName ](#API_DeleteLexicon_RequestSyntax) **   <a name="polly-DeleteLexicon-request-Name"></a>
The name of the lexicon to delete\. Must be an existing lexicon in the region\.  
Pattern: `[0-9A-Za-z]{1,20}`   
Required: Yes

## Request Body<a name="API_DeleteLexicon_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_DeleteLexicon_ResponseSyntax"></a>

```
HTTP/1.1 200
```

## Response Elements<a name="API_DeleteLexicon_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response with an empty HTTP body\.

## Errors<a name="API_DeleteLexicon_Errors"></a>

 ** LexiconNotFoundException **   
Amazon Polly can't find the specified lexicon\. This could be caused by a lexicon that is missing, its name is misspelled or specifying a lexicon that is in a different region\.  
Verify that the lexicon exists, is in the region \(see [ ListLexicons ](API_ListLexicons.md)\) and that you spelled its name is spelled correctly\. Then try again\.  
HTTP Status Code: 404

 ** ServiceFailureException **   
An unknown condition has caused a service failure\.  
HTTP Status Code: 500

## See Also<a name="API_DeleteLexicon_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/polly-2016-06-10/DeleteLexicon) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/polly-2016-06-10/DeleteLexicon) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/DeleteLexicon) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/DeleteLexicon) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/polly-2016-06-10/DeleteLexicon) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/polly-2016-06-10/DeleteLexicon) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/polly-2016-06-10/DeleteLexicon) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/polly-2016-06-10/DeleteLexicon) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/polly-2016-06-10/DeleteLexicon) 