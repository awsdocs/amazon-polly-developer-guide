# Using the ListLexicons Operations<a name="gs-list-lexicons"></a>

Amazon Polly provides the [ListLexicons](API_ListLexicons.md) API operation that you can use to get the list of pronunciation lexicons in your account in a specific AWS Region\. The following AWS CLI call lists the lexicons in your account in the us\-east\-2 region\.

```
aws polly list-lexicons
```

The following is an example response, showing two lexicons named `w3c` and `tomato`\. For each lexicon, the response returns metadata such as the language code to which the lexicon applies, the number of lexemes defined in the lexicon, the size in bytes, and so on\. The language code describes a language and locale to which the lexemes defined in the lexicon apply\. 

```
{
    "Lexicons": [
        {
            "Attributes": {
                "LanguageCode": "en-US",
                "LastModified": 1474222543.989,
                "Alphabet": "ipa",
                "LexemesCount": 1,
                "LexiconArn": "arn:aws:polly:aws-region:account-id:lexicon/w3c",
                "Size": 495
            },
            "Name": "w3c"
        },
        {
            "Attributes": {
                "LanguageCode": "en-US",
                "LastModified": 1473099290.858,
                "Alphabet": "ipa",
                "LexemesCount": 1,
                "LexiconArn": "arn:aws:polly:aws-region:account-id:lexicon/tomato",
                "Size": 645
            },
            "Name": "tomato"
        }
    ]
}
```

## Additional Code Samples for the ListLexicon API<a name="gs-list-lexicon-example-4"></a>

+ Java Sample: [ListLexicons](ListLexiconsSample.md)

+ Python \(Boto3\) Sample: [ListLexicon](ListLexiconSamplePython.md)