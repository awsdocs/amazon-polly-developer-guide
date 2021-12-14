# Installing and Configuring the Plugin<a name="WordPressPlugin-install"></a>

Before you install the plugin, make sure to complete the [prerequisites](WordPressPlugin-prerequisites.md)\.

**To install the plugin**

1. Log in to the admin dashboard for your WordPress website, also known as **WP Admin**\.

1. Choose **Plugins**\.

1. Choose **Add New**\.

1. In the search box, enter **AWS for WordPress**\.

1. Find the **AWS for WordPress** plugin\. Choose **Install Now**, and then choose **Activate**\.

## Configuring the Plugin<a name="wp-install"></a>

Once you've installed the **AWS for WordPress** plugin, configure it to enable podcasting, alternative storage locations, and other options\. 

**Note**  
In the following procedure, command and field names might differ slightly from the names used in WordPress\. 

**To configure the plugin**

1. On the **WordPress Admin** page, choose **Settings**\. 

1. Configure the plugin using the following options: 
   + ****AWS access key and AWS secret key****—These AWS credentials allow the plugin to use Amazon Polly and Amazon Simple Storage Service \(Amazon S3\)\. Type the AWS access and secret keys that you created earlier\. If you are hosting your WordPress site on Amazon EC2, you can use an IAM role instead of credentials\. In that case, leave these two fields blank\.
   + ****Sample rate****—The sample rate for the audio files that will be generated, in Hz\. Higher sampling rates produce higher\-quality audio\.
   + ****Voice name****—The Amazon Polly voice to use in the audio file\. 
**Note**  
Remember that the choice of voice is determined by the language you're using\. For a complete set of available voices, see [Available Voices](voicelist.md#availablevoice-list)
   + ****Player position****—Where to position the audio player on the website\. You can put it before or after the post, or not use it at all\. If you want to make your files available as podcasts by using Amazon Pollycast, don't display the audio player\. 
   + ****New post default****—Specifies whether Amazon Polly should automatically create an audio file for all new posts\. Choose this option if you want Amazon Polly to create an audio file for each new post\.
   + ****Autoplay****—Specifies whether the audio player automatically starts playing the audio for a post when a visitor visits it\. 
   + ****Store audio in Amazon S3****—If you want to store audio files in an S3 bucket instead of on your web server, choose this option\. Amazon Polly creates the bucket for you\. For more information and pricing, see [Amazon S3](https://aws.amazon.com/s3)\.
   + ****Amazon CloudFront** **\(CDN\) domain name****—If you want to broadcast your audio files with Amazon CloudFront, provide the name of your CloudFront domain\. The plugin uses the domain to stream audio\. If you don't already have a domain, create one in Amazon CloudFront\. 
   + ****ITunes category****—The category for your podcast\. Choosing a category makes it easier for podcast users to find your podcast in the podcast catalog\.
   + ****ITunes explicit****—Specifies whether to enable Amazon Pollycast podcasting with the ITunes explicit setting\.\. 
   + ****Bulk update all posts****—If you want to convert all your previous WordPress posts to use the **AWS for WordPress** plugin, choose this option\. 

1. Choose **Save Changes**\.