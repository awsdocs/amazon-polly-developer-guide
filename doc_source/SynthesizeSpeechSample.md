# SynthesizeSpeech<a name="SynthesizeSpeechSample"></a>

The following Java code sample show how to use Java\-based applications to synthesize speech from for inputed text\. 

For more information, see the reference for [http://docs.aws.amazon.com/polly/latest/dg/API_SynthesizeSpeech.html](http://docs.aws.amazon.com/polly/latest/dg/API_SynthesizeSpeech.html) API\. 

```
package com.amazonaws.polly.samples;
 
import com.amazonaws.services.polly.AmazonPolly;
import com.amazonaws.services.polly.AmazonPollyClientBuilder;
import com.amazonaws.services.polly.model.OutputFormat;
import com.amazonaws.services.polly.model.SynthesizeSpeechRequest;
import com.amazonaws.services.polly.model.SynthesizeSpeechResult;
import com.amazonaws.services.polly.model.VoiceId;
 
import java.io.File;
import java.io.FileOutputStream;
import java.io.InputStream;
 
public class SynthesizeSpeechSample {
    AmazonPolly client = AmazonPollyClientBuilder.defaultClient();
 
    public void synthesizeSpeech() {
        String outputFileName = "/tmp/speech.mp3";
 
        SynthesizeSpeechRequest synthesizeSpeechRequest = new SynthesizeSpeechRequest()
                .withOutputFormat(OutputFormat.Mp3)
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