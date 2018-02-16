# Using the DeleteLexicon Operation<a name="gs-delete-lexicon"></a>

Amazon Polly provides the [DeleteLexicon](API_DeleteLexicon.md) API operation to delete a pronunciation lexicon from a specific AWS Region in your account\. The following AWS CLI deletes the specified lexicon\. 

The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly delete-lexicon \
--name example
```

## Additional Code Samples for the DeleteLexicon API<a name="gs-delete-lexicon-example-4"></a>

+ Java Sample: [DeleteLexicon](DeleteLexiconSample.md)

+ Python \(Boto3\) Sample: [DeleteLexicon](DeleteLexiconPython.md)