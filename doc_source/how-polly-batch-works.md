# How Polly\-batch\-processor Works<a name="how-polly-batch-works"></a>

The Polly\-batch\-processor application uses AWS Batch to asynchronously, and concurrently, break a document into small chunks that can be easily passed through Amazon Polly\.By using AWS Batch in conjunction with Amazon Simple Storage Service \(Amazon S3\), Amazon Elastic Compute Cloud \(Amazon EC2\), and AWS Lambda, Polly\-batch\-processor enables you to quickly create an MP3 file and avoid potential throttling issues\.

This is how the Polly\-batch\-processor application works: 

1. Upload your document to an S3 bucket\. After you've uploaded the document, you can optionally apply S3 object tags to add metadata, such as the title and the author's name\. You can also change the voice that Amazon Polly uses or specify that you don't want to consolidate the MP3 chunks\.

1. A Lambda function passes in the S3 bucket name and object key as input parameters for a new AWS Batch job in the AWS Batch queue\.

1. AWS Batch downloads the document from the S3 bucket, and Polly\-batch\-processor breaks it into paragraph\-sized chunks\. It detects paragraph boundaries by searching for two line feed characters \(\(\\n\\n, which is the equivalent of two presses of the Enter key\)\. If a paragraph is too large, the application splits the paragraph into sentences separated by the dot \(‘\.’\) character\. 
**Note**  
If a sentence contains an abbreviation \(for example, St\. Paul\), Polly\-batch\-processor might split it after the period\. In that case, the intonation of the resulting speech will be incorrect\. 

1. AWS Batch processes each text chunk in parallel,calling the Amazon Polly `SynthesizeSpeech` API for each chunk, and returning an MP3 file for each\. , The number of chunks processed in parallel depends on the number of virtual CPUs \(vCPUs\) configured in the AWS Batch job definition\. By default, AWS Batch combines the files into a single MP3 file, and uploads it to the S3 bucket where the original document is stored\. If you don't want save all of the audio files in a single MP3 file, you can direct the application upload each chunk to the S3 bucket individually\. To do this, apply an S3 object tag with the name `consolidated` and the value `false`\. 

1. AWS Batch publishes a message to an Amazon Simple Notification Service \(Amazon SNS\) topic that includes the URL of the MP3 file or that of the list of files if you chose not to consolidate the audio files\.

1. Amazon SNS then sends you an email message that contains the URL of the MP3 file or list of files\.

## Next Step<a name="polly-batch-next-step-2"></a>

[Polly\-batch\-processor Resources](polly-batch-processor-resources.md)