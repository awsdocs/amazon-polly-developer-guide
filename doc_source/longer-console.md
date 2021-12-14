# Creating Long Audio Files \(Console\)<a name="longer-console"></a>

You can use the Amazon Polly console to create long speeches using asynchronous synthesis with the same functionality as you can use with the AWS CLI\. This is done using the **Text\-to\-Speech** tab much like any other synthesis\. 

The other asynchronous synthesis functionality is also available via the console\. The **S3 synthesis tasks** tab reflects the `ListSpeechSynthesisTasks` functionality, displaying all tasks saved to the S3 bucket and enabling you to filter them if you want\. Clicking on a specific single task shows its details, reflecting `GetSpeechSynthesisTask` functionality\.

**To synthesize a large text using the Amazon Polly Console**

1. Sign in to the AWS Management Console and open the Amazon Polly console at [https://console\.aws\.amazon\.com/polly/](https://console.aws.amazon.com/polly/)\.

1. Choose the **Text\-to\-Speech** tab\. 

1. With **SSML** on or off, type or past your text into the input box\.

1. Choose the language, region, and voice for your text\. 

1. Choose **Save to S3**\. 
**Note**  
Both the **Download** and **Listen** options are greyed out if the text length is above the limits for the real\-time `SynthesizeSpeech` operation\.

1. The console opens a form so that you can choose where to store the output file\.

   1. Fill in the name of the destination Amazon S3 bucket\.

   1. Optionally, fill in the prefix key of the output\.
**Note**  
The output S3 bucket must be writable\.

   1. If you want to be notified when the synthesis task is complete, provide an optional SNS topic identifier\.
**Note**  
The SNS must be open for publication by the current console user to use this option\. For more information, see [Amazon Simple Notification Service \(SNS\)](https://aws.amazon.com/sns/)

   1. Choose **Save to S3**\. 

**To retrieve information on your speech synthesis tasks**

1. In the console, choose the **S3 Synthesis Tasks** tab\.

1. The tasks are displayed in date order\. To filter the tasks, by status, choose **All statuses** and then choose the status to use\.

1. To view the details of a specific task, choose the linked **Task ID**\.