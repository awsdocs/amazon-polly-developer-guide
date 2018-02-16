# Storing Audio Files<a name="pollycast"></a>

When you publish content on your site, it's sent to Amazon Polly for synthesis\. By default, new audio files are stored on your web server\. You can also store the files using Amazon S3 or Amazon CloudFront\. 

The way your WordPress users listen to the audio content on your website depends on where the content is stored: 

1. For audio files stored on the WordPress server, files are broadcast directly from the server\.

1. For files stored in an Amazon S3 bucket, files are broadcast from the S3 bucket\. 

1. If you use Amazon CloudFront \(CDN\), the files are stored on Amazon S3 and are broadcast with Amazon CloudFront\. 

 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/polly/latest/dg/images/chart.png)

Your users have the same listening experience regardless of how you store your audio files\. 

## Positioning the HTML Player<a name="pollycast-html"></a>

When you install the Amazon Polly plugin, it displays an HTML player on your WordPress website\.

 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/polly/latest/dg/images/htmlplayer.png)

You can use the **Player position** option when configuring the plugin on the **Amazon Polly Settings** page to display the player above or below your text, or not display it at all\. For more information about setting configuration options, see [Installing and Configuring the Plugin](plugin-install.md#wp-install)\.

## Podcasting with Amazon Pollycast<a name="pollycast-podcast"></a>

To let users listen to your audio content using standard podcast applications, set up Pollycast feeds\. RSS 2\.0\-compliant Pollycast feeds provide the necessary XML data for aggregation by popular podcast mobile applications and podcast directories, such as iTunes\. The Amazon Polly plugin automatically adds Amazon Pollycast endpoints to all WordPress archive URLs\. This lets you syndicate both site\-wide or targeted podcasts\. 

You can also add Amazon Pollycast endpoints manually by adding `/amazon-pollycast/` to the URL for a page in a podcasting application\. For example:

```
example.com/amazon-pollycast/
example.com/category/news/amazon-pollycast/
example.com/author/john/amazon-pollcast/
```