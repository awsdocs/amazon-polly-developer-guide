# Neural TTS<a name="NTTS-main"></a>

Amazon Polly has a *Neural TTS \(NTTS\)* system that can produce even higher quality voices than its standard voices\. The NTTS system produces the most natural and human\-like text\-to\-speech voices possible\. 

Standard TTS voices use concatenative synthesis\. This method strings together \(concatenates\) the phonemes of recorded speech, producing very natural\-sounding synthesized speech\. However, the inevitable variations in speech and the techniques used to segment the waveforms limits the quality of speech\. 

The Amazon Polly Neural TTS system doesn't use standard concatenative synthesis to produce speech\. It has two parts: 
+ A neural network that converts a sequence of phonemes—the most basic units of language—into a sequence of *spectrograms*, which are snapshots of the energy levels in different frequency bands
+ A vocoder, which converts the spectrograms into a continuous audio signal\.

The first component of the neural TTS system is a sequence\-to\-sequence model\. This model doesn’t create its results solely from the corresponding input but also considers how the sequence of the elements of the input work together\. The model chooses the spectrograms that it outputs so that their frequency bands emphasize acoustic features that the human brain uses when processing speech\. 

The output of this model then passes to a neural vocoder\. This converts the spectrograms into speech waveforms\. When trained on the large data sets used to build general\-purpose concatenative\-synthesis systems, this sequence\-to\-sequence approach will yield higher\-quality, more natural\-sounding voices\. 

The Aria \(New Zealand English\), Ayanda \(South African English\), Gabrielle \(Canadian French\), Kevin \(US English\), and Olivia \(Australian English\) voices are only supported by Amazon Polly when using NTTS\. All other voices have a counterpart created using the standard TTS method\. When using an NTTS\-only voice, the TTS engine parameter must be set to `neural`, whether using the console or API\.

**Topics**
+ [Feature and Region Compatibility](#ntts-regions)
+ [The Voice Engine](#ntts-engine)
+ [Neural Voices](ntts-voices-main.md)
+ [NTTS Newscaster Speaking Style](ntts-speakingstyles.md)

## Feature and Region Compatibility<a name="ntts-regions"></a>

Neural voices aren't available in all AWS Regions, nor do they support all Amazon Polly features\. 

Neural voices are supported in the following Regions: 
+ US East \(N\. Virginia\): us\-east\-1
+ US West \(Oregon\): us\-west\-2
+ Africa \(Cape Town\): af\-south\-1
+ Asia Pacific \(Tokyo\): ap\-northeast\-1
+ Asia Pacific \(Seoul\): ap\-northeast\-2
+ Asia Pacific \(Singapore\): ap\-southeast\-1
+ Asia Pacific \(Sydney\): ap\-southeast\-2
+ Canada \(Central\): ca\-central\-1
+ Europe \(Frankfurt\): eu\-central\-1
+ Europe \(Ireland\): eu\-west\-1
+ Europe \(London\): eu\-west\-2
+ AWS GovCloud \(US\-West\): us\-gov\-west\-1

Endpoints and protocols for these Regions are identical to those used for standard voices\. For more information, see [Amazon Polly endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/pol.html)\.

The following features are supported for neural voices:
+ Real\-time and asynchronous speech synthesis operations\.
+ Newscaster speaking style\. For more information about the speaking styles, see [NTTS Newscaster Speaking Style](ntts-speakingstyles.md)\.
+ All speechmarks\. 
+ Many \(but not all\) of the SSML tags that are supported by Amazon Polly\. For more information about NTTS\-supported SSML tags, see [Supported SSML Tags](supportedtags.md)\.

 As with standard voices, you can choose from various sampling rates to optimize the bandwidth and audio quality for your application\. Valid sampling rates for standard and neural voices are 8 kHz, 16 kHz, 22 kHz, or 24 kHz\. The default for standard voices is 22 kHz\. The default for neural voices is 24 kHz\. Amazon Polly supports MP3, OGG \(Vorbis\), and raw PCM audio stream formats\.

## The Voice Engine<a name="ntts-engine"></a>

Amazon Polly enables you to use either neural or standard voice with the `engine` property\. It has two possible values: **Standard** or **Neural**, indicating whether to use a standard or neural voice\. **Standard** is the default value\. 

**Important**  
If you are not in one of the regions where NTTS is supported, only the standard voice engine will be displayed in the console\. If the neural engine is not displayed, check your region\. For more information on the regions where NTTS can be used, see [Feature and Region Compatibility](#ntts-regions)\.

When using an NTTS\-only voice, the TTS engine parameter must be set to `neural`, whether using the console or API\.

### Choosing the Voice Engine \(Console\)<a name="choosing-engine-console"></a>

**To choose a voice engine \(console\)**

1. Open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. On the Text\-to\-Speech page, for **Engine**, choose **Standard** or **Neural**\.   
![\[The Engine option on the console Text-to-Speech page. Note that the Neural option is only displayed in Regions where the neural engine is supported.\]](http://docs.aws.amazon.com/polly/latest/dg/images/engine-console.png)

   If you choose **Neural**, only neural voices are available and standard\-only voices are disabled\. 

### Choosing the Voice Engine \(CLI\)<a name="choosing-engine-cli"></a>

**To choose a voice engine \(CLI\)**

The `engine` parameter is optional, with two possible values: `standard` or `Neural`\. Use this property when creating a `SynthesisSynthesisTask` operation\. 

For example, you can use the following code to run the `start-speech-synthesis-task` AWS CLI command in the US West\-2 \(Oregon\) region 

The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly start-speech-synthesis-task \
  --engine neural
  --region us-west-2 \
  --endpoint-url "https://polly.us-west-1.amazonaws.com/" \
  --output-format mp3 \
  --output-s3-bucket-name your-bucket-name \
  --output-s3-key-prefix optional/prefix/path/file \
  --voice-id Joanna \
  --text file://text_file.txt
```

This will result in a response that looks similar to this: 

```
"SynthesisTask": 
{
     "CreationTime": [..],
     "Engine": "neural",
     "OutputFormat": "mp3",
     "OutputUri": "https://s3.us-west-1.amazonaws.com/your-bucket-name/optional/prefix/path/file.<task_id>.mp3",
     "TextType": "text",
     "RequestCharacters": [..],
     "TaskStatus": "scheduled",
     "TaskId": [task_id],
     "VoiceId": "Joanna"
 }
```