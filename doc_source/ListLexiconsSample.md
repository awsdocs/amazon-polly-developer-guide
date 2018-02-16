# ListLexicons<a name="ListLexiconsSample"></a>

The following Java code sample shows how to use Java\-based applications to produce a list of pronunciation lexicons stored in a AWS Region\. 

For more information on this operation, see the reference for the [http://docs.aws.amazon.com/polly/latest/dg/API_ListLexicons.html](http://docs.aws.amazon.com/polly/latest/dg/API_ListLexicons.html) API\. 

```
package com.amazonaws.polly.samples;
 
import com.amazonaws.services.polly.AmazonPolly;
import com.amazonaws.services.polly.AmazonPollyClientBuilder;
import com.amazonaws.services.polly.model.LexiconAttributes;
import com.amazonaws.services.polly.model.LexiconDescription;
import com.amazonaws.services.polly.model.ListLexiconsRequest;
import com.amazonaws.services.polly.model.ListLexiconsResult;
 
public class ListLexiconsSample {
    AmazonPolly client = AmazonPollyClientBuilder.defaultClient();
 
    public void listLexicons() {
        ListLexiconsRequest listLexiconsRequest = new ListLexiconsRequest();
 
        try {
            String nextToken;
            do {
                ListLexiconsResult listLexiconsResult = client.listLexicons(listLexiconsRequest);
                nextToken = listLexiconsResult.getNextToken();
                listLexiconsRequest.setNextToken(nextToken);
 
                for (LexiconDescription lexiconDescription : listLexiconsResult.getLexicons()) {
                    LexiconAttributes attributes = lexiconDescription.getAttributes();
                    System.out.println("Name: " + lexiconDescription.getName()
                            + ", Alphabet: " + attributes.getAlphabet()
                            + ", LanguageCode: " + attributes.getLanguageCode()
                            + ", LastModified: " + attributes.getLastModified()
                            + ", LexemesCount: " + attributes.getLexemesCount()
                            + ", LexiconArn: " + attributes.getLexiconArn()
                            + ", Size: " + attributes.getSize());
                }
            } while (nextToken != null);
        } catch (Exception e) {
            System.err.println("Exception caught: " + e);
        }
    }
}
```