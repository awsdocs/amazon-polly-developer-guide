# Storing Audio Files<a name="pollycast"></a>

When you publish content on your site, it's sent to Amazon Polly for synthesis\. By default, Amazon Polly stores new audio files on your web server\. You can also store the files on Amazon Simple Storage Service \(Amazon S3\) or on Amazon CloudFront, which is a global content delivery network \(CDN\)\. 

Users have the same listening experience regardless of where you store your audio files\. Only the broadcast location changes:: 

1. For audio files stored on the WordPress server, files are broadcast directly from the server\.

1. For files stored in an S3 bucket, files are broadcast from the bucket\. 

1. If you use CloudFront, the files are stored on Amazon S3 and are broadcast with CloudFront\. 

 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/polly/latest/dg/images/chart.png)

You can choose where to store your files when you install the Amazon Polly plugin\.  