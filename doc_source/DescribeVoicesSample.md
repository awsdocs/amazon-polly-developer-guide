# DescribeVoices<a name="DescribeVoicesSample"></a>

The following Java code sample show how to use Java\-based applications to produce a list of the voices that are available for use when requesting speech synthesis\. You can optionally specify a language code to filter the available voices\. For example, if you specify en\-US, the operation returns a list of all available US English voices\.

For more information on this operation, see the reference for the [http://docs.aws.amazon.com/polly/latest/dg/API_DescribeVoices.html](http://docs.aws.amazon.com/polly/latest/dg/API_DescribeVoices.html) API\. 

```
package com.amazonaws.polly.samples;
 
import com.amazonaws.services.polly.AmazonPolly;
import com.amazonaws.services.polly.AmazonPollyClientBuilder;
import com.amazonaws.services.polly.model.DescribeVoicesRequest;
import com.amazonaws.services.polly.model.DescribeVoicesResult;
 
public class DescribeVoicesSample {
    AmazonPolly client = AmazonPollyClientBuilder.defaultClient();
 
    public void describeVoices() {
        DescribeVoicesRequest allVoicesRequest = new DescribeVoicesRequest();
        DescribeVoicesRequest enUsVoicesRequest = new DescribeVoicesRequest().withLanguageCode("en-US");
 
        try {
            String nextToken;
            do {
                DescribeVoicesResult allVoicesResult = client.describeVoices(allVoicesRequest);
                nextToken = allVoicesResult.getNextToken();
                allVoicesRequest.setNextToken(nextToken);
 
                System.out.println("All voices: " + allVoicesResult.getVoices());
            } while (nextToken != null);
 
            do {
                DescribeVoicesResult enUsVoicesResult = client.describeVoices(enUsVoicesRequest);
                nextToken = enUsVoicesResult.getNextToken();
                enUsVoicesRequest.setNextToken(nextToken);
 
                System.out.println("en-US voices: " + enUsVoicesResult.getVoices());
            } while (nextToken != null);
        } catch (Exception e) {
            System.err.println("Exception caught: " + e);
        }
    }
}
```