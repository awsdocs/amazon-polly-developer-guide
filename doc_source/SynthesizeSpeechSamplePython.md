# SynthesizeSpeech<a name="SynthesizeSpeechSamplePython"></a>

The following Python code example uses the AWS SDK for Python \(Boto\) synthesize speech with shorter texts for near real\-time processing\. For more information, see the reference for the [ SynthesizeSpeech ](API_SynthesizeSpeech.md) operation\. 

This example uses a short string of plain text\. You can use SSML text for more control over the output\. For more information, see [Generating Speech from SSML Documents](ssml.md)\.

```
import boto3

polly_client = boto3.Session(
                aws_access_key_id=,                     
    aws_secret_access_key=,
    region_name='us-west-2').client('polly')

response = polly_client.synthesize_speech(VoiceId='Joanna',
                OutputFormat='mp3', 
                Text = 'This is a sample text to be synthesized.',
                Engine = 'neural')

file = open('speech.mp3', 'wb')
file.write(response['AudioStream'].read())
file.close()
```