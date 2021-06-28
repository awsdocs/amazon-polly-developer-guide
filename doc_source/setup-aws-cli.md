# Step 3\.1: Set Up the AWS Command Line Interface \(AWS CLI\)<a name="setup-aws-cli"></a>

Follow the steps to download and configure the AWS CLI\.

**Important**  
You don't need the AWS CLI to perform the steps in this exercise\. However, some of the exercises in this guide use the AWS CLI\. You can skip this step and go to [Step 3\.2: Getting Started Exercise Using the AWS CLI](get-started-cli-exercise.md), and then set up the AWS CLI later when you need it\.

**To set up the AWS CLI**

1. Download and configure the AWS CLI\. For instructions, see the following topics in the *AWS Command Line Interface User Guide*: 
   + [Getting Set Up with the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html)
   + [Configuring the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)

1. Add a named profile for the administrator user in the AWS CLI config file\. You use this profile when running the AWS CLI commands\. For more information about named profiles, see [Named Profiles](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html) in the *AWS Command Line Interface User Guide*\.

   ```
   [profile adminuser]
       aws_access_key_id = adminuser access key ID
       aws_secret_access_key = adminuser secret access key
       region = aws-region
   ```

   For a list of available AWS Regions and those supported by Amazon Polly, see [Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html) in the *Amazon Web Services General Reference*\.
**Note**  
If you're using the Region supported by Amazon Polly that you specified when you configured the AWS CLI, omit the following line from the AWS CLI code examples\.   

   ```
   --region aws-region
   ```

1. Verify the setup by typing the following help command at the command prompt\. 

   ```
   aws help
   ```

   A list of valid AWS commands should appear in the AWS CLI window\.

**To enable Amazon Polly in the AWS CLI \(optional\)**

If you have previously downloaded and configured the AWS CLI, Amazon Polly might not be available unless you reconfigure the AWS CLI\. This procedure checks to see if this is necessary and provides instructions if Amazon Polly is not automatically available\.

1. Verify the availability of Amazon Polly by typing the following help command at the AWS CLI command prompt\.

   ```
   aws polly help
   ```

   If a description of Amazon Polly and a list of valid commands appears in the AWS CLI window, Amazon Polly is available in the AWS CLI and can be used immediately\. In this case, you can skip the rest of this procedure\. If this is not displayed, continue with Step 2\.

1. Use one of the two following options to enable Amazon Polly:

   1. Uninstall and reinstall the AWS CLI\.

      For instructions, see [Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) in the *AWS Command Line Interface User Guide*\.

      

      or

   1. Download the file [service\-2\.json\.](https://github.com/boto/botocore/blob/develop/botocore/data/polly/2016-06-10/service-2.json)

      At the command prompt, run the following command\. 

      ```
      aws configure add-model --service-model file://service-2.json --service-name polly
      ```

1. Reverify the availability of Amazon Polly\.

   ```
   aws polly help
   ```

   The description of Amazon Polly should be visible\.

## Next Step<a name="setting-up-next-step-3"></a>

[Step 3\.2: Getting Started Exercise Using the AWS CLI](get-started-cli-exercise.md)