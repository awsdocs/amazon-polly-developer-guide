# Polly\-batch\-processor Components<a name="polly-batch-processor-components"></a>

Launching the AWS CloudFormation template,creates the following AWS resources:

+ A number of Lambda functions, including: 

  + `PollyBookSplitterFunction`, submits a new AWS Batch job for each new document whe it is uploaded to Amazon S3\. 

  + `CodeBuildTriggerFunction`, which triggers building a Docker image that the AWS Batch job uses to synthesize a chunk of text into speech with Amazon Polly\. AWS CloudFormation calls this function as a custom resource\.

  + `AWSBatchComputeEnvFunction`, which creates the AWS Batch compute environment as an AWS CloudFormation custom resource, and deletes it when it's no longer needed\.

  + `AWSBatchJobQueueFunction`, which creates the AWS Batch job queue as an AWS CloudFormation custom resource, and deletes it when it's no longer needed\.

  + `WSBatchJobDefinitionFunction`, which registers the AWS Batch job definition as an AWS CloudFormation custom resource, and later deregisters it\.

+ AWS Identity and Access Management IAM\) service roles for AWS CodeBuild and AWS Batch\.

+ IAM roles and a security group for the EC2 instances used by AWS Batch\.

+ An S3 bucket configured as an Amazon S3 website, which stores the document that you want to convert to an audio file, the audio file, and a manifest file\.

+ An Amazon Elastic Container Registry \(Amazon ECR\) repository, named polly\_document\_processor, that stores the Docker image run by the AWS Batch jobs\.

+ An AWS CodeBuild project that builds the Docker image used by AWS Batch to generate the audio file\. The AWS CodeBuild project pushes the built Docker image to the Amazon ECR repository named polly\_document\_processor\.

+ A custom AWS CloudFormation resource that triggers building the AWS CodeBuild project\.

+ An AWS Batch compute environment that launches the EC2 resources needed to run the AWS Batch jobs\.

+ An AWS Batch job queue where the `PollyBookSplitterFunction` Lambda function submits jobs\.

+ An AWS Batch job definition that specifies the Docker image and other parameters that are used to execute the AWS Batch job\.