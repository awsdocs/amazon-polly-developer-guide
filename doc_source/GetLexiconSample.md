# GetLexicon<a name="GetLexiconSample"></a>

The following Java code sample show how to use Java\-based applications to produce the content of a specific pronunciation lexicon stored in a AWS Region\. 

For more information on this operation, see the reference for the [http://docs.aws.amazon.com/polly/latest/dg/API_GetLexicon.html](http://docs.aws.amazon.com/polly/latest/dg/API_GetLexicon.html) API\. 

```
package com.amazonaws.polly.samples;
 
import com.amazonaws.services.polly.AmazonPolly;
import com.amazonaws.services.polly.AmazonPollyClientBuilder;
import com.amazonaws.services.polly.model.GetLexiconRequest;
import com.amazonaws.services.polly.model.GetLexiconResult;
 
public class GetLexiconSample {
    private String LEXICON_NAME = "SampleLexicon";
 
    AmazonPolly client = AmazonPollyClientBuilder.defaultClient();
 
    public void getLexicon() {
        GetLexiconRequest getLexiconRequest = new GetLexiconRequest().withName(LEXICON_NAME);
 
        try {
            GetLexiconResult getLexiconResult = client.getLexicon(getLexiconRequest);
            System.out.println("Lexicon: " + getLexiconResult.getLexicon());
        } catch (Exception e) {
            System.err.println("Exception caught: " + e);
        }
    }
}
```