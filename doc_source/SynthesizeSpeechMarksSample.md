# Speech Marks<a name="SynthesizeSpeechMarksSample"></a>

The following code sample shows how to use Java\-based applications to synthesize speech marks for inputed text\. This functionality uses the SynthesizeSpeech API\.

For more information on this functionality, see [Speech Marks ](speechmarks.md)\.

For more information on the API, see the reference for [http://docs.aws.amazon.com/polly/latest/dg/API_SynthesizeSpeech.html](http://docs.aws.amazon.com/polly/latest/dg/API_SynthesizeSpeech.html) API\. 

```
package com.amazonaws.polly.samples;
 
import com.amazonaws.services.polly.AmazonPolly;
import com.amazonaws.services.polly.AmazonPollyClientBuilder;
import com.amazonaws.services.polly.model.OutputFormat;
import com.amazonaws.services.polly.model.SpeechMarkType;
import com.amazonaws.services.polly.model.SynthesizeSpeechRequest;
import com.amazonaws.services.polly.model.SynthesizeSpeechResult;
import com.amazonaws.services.polly.model.VoiceId;
 
import java.io.File;
import java.io.FileOutputStream;
import java.io.InputStream;
 
public class SynthesizeSpeechMarksSample {
    AmazonPolly client = AmazonPollyClientBuilder.defaultClient();
 
    public void synthesizeSpeechMarks() {
        String outputFileName = "/tmp/speechMarks.json";
 
        SynthesizeSpeechRequest synthesizeSpeechRequest = new SynthesizeSpeechRequest()
                .withOutputFormat(OutputFormat.Json)
                .withSpeechMarkTypes(SpeechMarkType.Viseme, SpeechMarkType.Word)
                .withVoiceId(VoiceId.Joanna)
                .withText("This is a sample text to be synthesized.");
 
        try (FileOutputStream outputStream = new FileOutputStream(new File(outputFileName))) {
            SynthesizeSpeechResult synthesizeSpeechResult = client.synthesizeSpeech(synthesizeSpeechRequest);
            byte[] buffer = new byte[2 * 1024];
            int readBytes;
 
            try (InputStream in = synthesizeSpeechResult.getAudioStream()){
                while ((readBytes = in.read(buffer)) > 0) {
                    outputStream.write(buffer, 0, readBytes);
                }
            }
        } catch (Exception e) {
            System.err.println("Exception caught: " + e);
        }
    }
}
```