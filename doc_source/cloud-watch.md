# Integrating CloudWatch with Amazon Polly<a name="cloud-watch"></a>

When you interact with Amazon Polly, it sends the following metrics and dimensions to CloudWatch every minute\. You can use the following procedures to view the metrics for Amazon Polly\.

You can monitor Amazon Polly using CloudWatch, which collects and processes raw data from Amazon Polly into readable, near real\-time metrics\. These statistics are recorded for a period of two weeks, so that you can access `historical information` and gain a better perspective on how your web application or service is performing\. By default, Amazon Polly metric data is sent to CloudWatch in 1 minute intervals\. For more information, see [What Is Amazon CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html) in the Amazon *CloudWatch User Guide*\.

## Getting CloudWatch Metrics \(Console\)<a name="cloud-watch-metrics-console"></a>

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Metrics**\.

1. In the ** CloudWatch Metrics by Category** pane, under the metrics category for Amazon Polly, select a metrics category, and then in the upper pane, scroll down to view the full list of metrics\.

## Getting CloudWatch Metrics \(CLI\)<a name="cloud-watch-metrics-cli"></a>

The following code display available metrics for Amazon Polly\.

```
aws cloudwatch list-metrics --namespace "AWS/Polly"
```

The preceding command returns a list of Amazon Polly metrics similar to the following\. The `MetricName` element identifies what the metric is\.

```
{
    "Metrics": [
        {
            "Namespace": "AWS/Polly", 
            "Dimensions": [
                {
                    "Name": "Operation", 
                    "Value": "SynthesizeSpeech"
                }
            ], 
            "MetricName": "ResponseLatency"
        }, 
        {
            "Namespace": "AWS/Polly", 
            "Dimensions": [
                {
                    "Name": "Operation", 
                    "Value": "SynthesizeSpeech"
                }
            ], 
            "MetricName": "RequestCharacters"
        }
```

For more information, see [GetMetricStatistics](http://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_GetMetricStatistics.html) in the *Amazon CloudWatch API Reference*\.

## Amazon Polly Metrics<a name="polly-metrics"></a>

Amazon Polly produces the following metrics for each request\. These metrics are aggregated and in one minute intervals sent to CloudWatch where they are available\.


| Metric | Description | 
| --- | --- | 
|  `RequestCharacters` |  The number of characters in the request\. This is billable characters only and does not include SSML tags\. Valid Dimension: Operation Valid Statistics: Minimum, Maximum, Average, SampleCount, Sum Unit: Count  | 
|  `ResponseLatency` |  The latency between when the request was made and the start of the streaming response\. Valid Dimensions: Operation Valid Statistics: Minimum, Maximum, Average, SampleCount Unit: milliseconds  | 
|  `2XXCount` |  HTTP 200 level code returned upon a successful response\. Valid Dimensions: Operation Valid Statistics: Average, SampleCount, Sum Unit: Count  | 
|  `4XXCount` |  HTTP 400 level error code returned upon an error\. For each successful response, a zero \(0\) is emitted\. Valid Dimensions: Operation Valid Statistics: Average, SampleCount, Sum Unit: Count  | 
|  `5XXCount` |  HTTP 500 level error code returned upon an error\. For each successful response, a zero \(0\) is emitted\. Valid Dimensions: Operation Valid Statistics: Average, SampleCount, Sum Unit: Count  | 

## Dimensions for Amazon Polly Metrics<a name="polly-metricdimensions"></a>

Amazon Polly metrics use the AWS/Polly namespace and provide metrics for the following dimension:


| Dimension | Description | 
| --- | --- | 
|  `Operation`  |  Metrics are grouped by the API method they refer to\. Possible values are `SynthesizeSpeech`, `PutLexicon`, `DescribeVoices`, etc\.  | 