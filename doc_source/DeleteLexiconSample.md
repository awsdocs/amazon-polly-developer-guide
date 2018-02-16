# DeleteLexicon<a name="DeleteLexiconSample"></a>

The following Java code sample show how to use Java\-based applications to delete a specific lexicon stored in an AWS region\. A lexicon which has been deleted is not available for speech synthesis, nor can it be retrieved using either the `GetLexicon` or `ListLexicon` APIs\.

For more information on this operation, see the reference for the [http://docs.aws.amazon.com/polly/latest/dg/API_DeleteLexicon.html](http://docs.aws.amazon.com/polly/latest/dg/API_DeleteLexicon.html) API\. 

```
package com.amazonaws.polly.samples;
 
import com.amazonaws.services.polly.AmazonPolly;
import com.amazonaws.services.polly.AmazonPollyClientBuilder;
import com.amazonaws.services.polly.model.DeleteLexiconRequest;
 
public class DeleteLexiconSample {
    private String LEXICON_NAME = "SampleLexicon";
 
    AmazonPolly client = AmazonPollyClientBuilder.defaultClient();
 
    public void deleteLexicon() {
        DeleteLexiconRequest deleteLexiconRequest = new DeleteLexiconRequest().withName(LEXICON_NAME);
 
        try {
            client.deleteLexicon(deleteLexiconRequest);
        } catch (Exception e) {
            System.err.println("Exception caught: " + e);
        }
    }
}
```