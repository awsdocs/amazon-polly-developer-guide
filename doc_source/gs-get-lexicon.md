# Using the GetLexicon Operation<a name="gs-get-lexicon"></a>

Amazon Polly provides the [GetLexicon](API_GetLexicon.md) API operation to retrieve the content of a pronunciation lexicon you stored in your account in a specific region\. 

The following `get-lexicon` AWS CLI command retrieves the content of the `example` lexicon\.

```
aws polly get-lexicon \
--name example
```

If you don't already have a lexicon stored in your account, you can use the `PutLexicon` operation to store one\. For more information, see [Using the PutLexicon Operation](gs-put-lexicon.md)\.

The following is a sample response\. In addition to the lexicon content, the response returns the metadata, such as the language code to which the lexicon applies, number of lexemes defined in the lexicon, the Amazon Resource Name \(ARN\) of the resource, and the size of the lexicon in bytes\. The `LastModified` value is a Unix timestamp\.

```
{
    "Lexicon": {
        "Content": "lexicon content in plain text PLS format",
        "Name": "example"
    },
    "LexiconAttributes": {
        "LanguageCode": "en-US",
        "LastModified": 1474222543.989,
        "Alphabet": "ipa",
        "LexemesCount": 1,
        "LexiconArn": "arn:aws:polly:us-east-2:account-id:lexicon/example",
        "Size": 495
    }
}
```

## Additional Code Samples for the GetLexicon API<a name="gs-get-lexicon-example-4"></a>

+ Java Sample: [GetLexicon](GetLexiconSample.md)

+ Python \(Boto3\) Sample: [GetLexicon](GetLexiconSamplePython.md)