# Creating Longer Audio Files<a name="creating-longer-audio-files"></a>

Currently, you can't convert large documents, such as books or reports, to audio with Amazon Polly\. That's because Amazon Polly has two limitations that present challenges for large text\-to\-speech applications:

+ The maximum size of input text for the `SynthesizeSpeech` API is 1,500 billed characters\.

+ The maximum number of concurrent requests to the `SynthesizeSpeech` API per second is 80, with a burst limit of 100\.

To create audio files for large documents, use the Polly\-batch\-process application\. This application overcomes the challenge of processing a text document that exceeds the maximum number of characters supported by Amazon Polly\. Polly\-batch\-processor takes a large text document and breaks it into chunks, and then uses Amazon Polly to generate an audio file for each chunk\. Polly\-batch\-processor generates each sentence asynchronously and concurrently, reducing the time to create the audio file and overcoming any potential throttling issues\. After processing the complete text file, it consolidates the chunks into a single large MP3 file\. If you prefer to listen to the chunks \(small\) files individually, you can do so\. You can also use Polly\-batch\-processor to create audio files for documents containing multiple short phrases that are less than 1500 characters long, such as movie titles\. 

## Next Step<a name="polly-batch-next-step-1"></a>

[How Polly\-batch\-processor Works](how-polly-batch-works.md)