# Python Example \(HTML5 Client and Python Server\)<a name="examples-python"></a>

This example application consists of the following:

+ An HTTP 1\.1 server using the HTTP chunked transfer coding \(see [Chunked Transfer Coding](https://tools.ietf.org/html/rfc2616#section-3.6.1)\)

+ A simple HTML5 user interface that interacts with the HTTP 1\.1 server \(shown below\):

     
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/polly/latest/dg/images/app1-10.png)

The goal of this example is to show how to use Amazon Polly to stream speech from a browser\-based HTML5 application\. Consuming the audio stream produced by Amazon Polly as the text gets synthesized is the recommended approach for use cases where responsiveness is an important factor \(for example, dialog systems, screen readers, etc\.\)\.

To run this example application you need the following:

+ Web browser compliant with the HTML5 and EcmaScript5 standards \(for example, Chrome 23\.0 or higher, Firefox 21\.0 or higher, Internet Explorer 9\.0, or higher\)

+ Python version greater than 3\.0

**To test the application**

1. Save the server code as `server.py`\. For the code, see [Python Example: Python Server Code \(server\.py\)](example-Python-server-code.md)\.

1. Save the HTML5 client code as `index.html`\. For the code, see [Python Example: HTML5 User Interface \(index\.html\)](example-html-app.md)\.

1. Run the following command from the path where you saved server\.py to start the application \(on some systems you might need to use `python3` instead of `python` when running the command\)\.

   ```
   $ python  server.py
   ```

   After the application starts, a URL appears on the terminal\. 

1. Open the URL shown in the terminal in a web browser\. 

   You can pass the address and port for the application server to use as a parameter to `server.py`\. For more information, run `python server.py -h`\.

1. To listen to speech, choose a voice from the list, type some text, and then choose **Read**\. The speech starts playing as soon as Amazon Polly transfers the first usable chunk of audio data\.

1. To stop the Python server when you're finished testing the application, press Ctrl\+C in the terminal where the server is running\.

**Note**  
The server creates a Boto3 client using the AWS SDK for Python \(Boto\)\. The client uses the credentials stored in the AWS config file on your computer to sign and authenticate the requests to Amazon Polly\. For more information on how to create the AWS config file and store credentials, see [Configuring the AWS Command Line Interface](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) in the *AWS Command Line Interface User Guide*\.