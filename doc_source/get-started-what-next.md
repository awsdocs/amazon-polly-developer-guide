# What's Next?<a name="get-started-what-next"></a>

This guide provides additional examples, some of which are Python code examples that use AWS SDK for Python \(Boto\) to make API calls to Amazon Polly\. We recommend you to set up Python and test the example code provided in the following section\. For additional examples, see [Example Applications](examples-for-using-polly.md)\.

## Set Up Python and Test an Example<a name="get-started-setup-python"></a>

To test the Python example code, you need the AWS SDK for Python \(Boto\)\. For instruction, see [AWS SDK for Python \(Boto3\)](https://aws.amazon.com/sdk-for-python/)\.

**To test Example Python Code**

The following Python code example does the following:

+ Uses the AWS SDK for Python \(Boto\) to send a `SynthesizeSpeech` request to Amazon Polly \(by providing simple text as input\)\. 

+ Accesses the resulting audio stream in the response and saves the audio to a file on your local disk \(`speech.mp3`\)\.

+ Plays the audio file with the default audio player for your local system\.

Save the code to a file \(example\.py\) and run it\.

```
"""Getting Started Example for Python 2.7+/3.3+"""
from boto3 import Session
from botocore.exceptions import BotoCoreError, ClientError
from contextlib import closing
import os
import sys
import subprocess
from tempfile import gettempdir

# Create a client using the credentials and region defined in the [adminuser]
# section of the AWS credentials file (~/.aws/credentials).
session = Session(profile_name="adminuser")
polly = session.client("polly")

try:
    # Request speech synthesis
    response = polly.synthesize_speech(Text="Hello world!", OutputFormat="mp3",
                                        VoiceId="Joanna")
except (BotoCoreError, ClientError) as error:
    # The service returned an error, exit gracefully
    print(error)
    sys.exit(-1)

# Access the audio stream from the response
if "AudioStream" in response:
    # Note: Closing the stream is important as the service throttles on the
    # number of parallel connections. Here we are using contextlib.closing to
    # ensure the close method of the stream object will be called automatically
    # at the end of the with statement's scope.
    with closing(response["AudioStream"]) as stream:
        output = os.path.join(gettempdir(), "speech.mp3")

        try:
            # Open a file for writing the output as a binary stream
            with open(output, "wb") as file:
                file.write(stream.read())
        except IOError as error:
            # Could not write to file, exit gracefully
            print(error)
            sys.exit(-1)

else:
    # The response didn't contain audio data, exit gracefully
    print("Could not stream audio")
    sys.exit(-1)

# Play the audio using the platform's default player
if sys.platform == "win32":
    os.startfile(output)
else:
    # the following works on Mac and Linux. (Darwin = mac, xdg-open = linux).
    opener = "open" if sys.platform == "darwin" else "xdg-open"
    subprocess.call([opener, output])
```

For additional examples including an example application, see [Example Applications](examples-for-using-polly.md)\.