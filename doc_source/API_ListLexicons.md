# ListLexicons<a name="API_ListLexicons"></a>

Returns a list of pronunciation lexicons stored in an AWS Region\. For more information, see [Managing Lexicons](https://docs.aws.amazon.com/polly/latest/dg/managing-lexicons.html)\.

## Request Syntax<a name="API_ListLexicons_RequestSyntax"></a>

```
GET /v1/lexicons?NextToken=NextToken HTTP/1.1
```

## URI Request Parameters<a name="API_ListLexicons_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [NextToken](#API_ListLexicons_RequestSyntax) **   <a name="polly-ListLexicons-request-NextToken"></a>
An opaque pagination token returned from previous `ListLexicons` operation\. If present, indicates where to continue the list of lexicons\.  
Length Constraints: Minimum length of 0\. Maximum length of 4096\.

## Request Body<a name="API_ListLexicons_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_ListLexicons_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "Lexicons": [ 
      { 
         "Attributes": { 
            "Alphabet": "string",
            "LanguageCode": "string",
            "LastModified": number,
            "LexemesCount": number,
            "LexiconArn": "string",
            "Size": number
         },
         "Name": "string"
      }
   ],
   "NextToken": "string"
}
```

## Response Elements<a name="API_ListLexicons_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [Lexicons](#API_ListLexicons_ResponseSyntax) **   <a name="polly-ListLexicons-response-Lexicons"></a>
A list of lexicon names and attributes\.  
Type: Array of [LexiconDescription](API_LexiconDescription.md) objects

 ** [NextToken](#API_ListLexicons_ResponseSyntax) **   <a name="polly-ListLexicons-response-NextToken"></a>
The pagination token to use in the next request to continue the listing of lexicons\. `NextToken` is returned only if the response is truncated\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 4096\.

## Errors<a name="API_ListLexicons_Errors"></a>

 **InvalidNextTokenException**   
The NextToken is invalid\. Verify that it's spelled correctly, and then try again\.  
HTTP Status Code: 400

 **ServiceFailureException**   
An unknown condition has caused a service failure\.  
HTTP Status Code: 500

## See Also<a name="API_ListLexicons_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/polly-2016-06-10/ListLexicons) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/polly-2016-06-10/ListLexicons) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/polly-2016-06-10/ListLexicons) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/polly-2016-06-10/ListLexicons) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/polly-2016-06-10/ListLexicons) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/polly-2016-06-10/ListLexicons) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/polly-2016-06-10/ListLexicons) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/polly-2016-06-10/ListLexicons) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/polly-2016-06-10/ListLexicons) 