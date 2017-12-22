# Launching Polly\-batch\-processor<a name="launching-polly-batch"></a>

AWS Batch and Amazon Polly are not available in all AWS Regions\. You can use the Polly\-batch\-processor application only in AWS Regions where both services are available\. For more information on valid Regions, see [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html#pol_region)\.

To use the Polly\-batch\-processor application, you need a virtual private cloud \(VPC\) with at least one public subnet and one private subnet\. To set up these resources, you use two AWS CloudFormation templates:

+ `PollyBatchNetwork` creates the VPC resources, including subnets, a NAT gateway, and an Internet gateway\. It also provides the VPC ID and subnets as output parameters\.

+ `PollyBatchMaster` sets up the remaining AWS resources necessary for the application\.

These templates also provide the name of the S3 bucket where the original documents that you want to convert are stored and the audio files are created\.

**To launch the AWS CloudFormation templates**

1. Sign in to the AWS Management Console and open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation/](https://console.aws.amazon.com/cloudformation/)\.

1. Choose the AWS Region\.

1. Choose **Create Stack**\.

1. For **Choose a Template**, choose **Specify an Amazon S3 template URL**, and type `https://s3.amazonaws.com/aws-bigdata-blog/artifacts/PollyBatch/cfn/network.yaml`\.

1. Choose **Next**\.

1. For **Stack Name**, type `PollyBatchNetwork`\.

1. Choose **Next**, and then choose **Next** again\.

1. Choose **Create**, and then wait for stack creation to complete\.

1. Choose **Create Stack**\.

1. For **Choose a Template**, choose **Specify an Amazon S3 template URL**, and type `https://s3.amazonaws.com/aws-bigdata-blog/artifacts/PollyBatch/cfn/master.yaml`\.

1. For **Stack Name**, type `PollyBatchMaster`\.

1. For **Mandatory Parameters**, specify an email address that can receive notifications when a new audio file has been created\.

1. For **VPC**, choose a VPC\.

1. Choose the private subnet where you want to run the AWS Batch resources\.

1. Choose **Next**, and then choose **Next** again\.

1. Choose **Create**\.

1. When Amazon SNS sends an email to the address that you provided, follow the directions to confirm the subscription to the topic named **PollyTopic**\.

## Next Step<a name="polly-batch-next-step-3"></a>

[Converting a Text File to Audio](converting-text-file-to-audio.md)