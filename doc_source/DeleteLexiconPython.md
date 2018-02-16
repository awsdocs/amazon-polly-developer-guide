# DeleteLexicon<a name="DeleteLexiconPython"></a>

The following Python code example uses the AWS SDK for Python \(Boto\) to delete a lexicon in the region specified in your local AWS configuration\. The example deletes only the specified lexicon\. It asks you to confirm that you want to proceed before actually deleting the lexicon\.

The following code example uses default credentials stored in the AWS SDK configuration file\. For information about creating the configuration file, see [Step 3\.1: Set Up the AWS Command Line Interface \(AWS CLI\)](setup-aws-cli.md)\. 

```
from argparse import ArgumentParser
from sys import version_info

from boto3 import Session
from botocore.exceptions import BotoCoreError, ClientError


# Define and parse the command line arguments
cli = ArgumentParser(description="DeleteLexicon example")
cli.add_argument("name", type=str, metavar="LEXICON_NAME")
arguments = cli.parse_args()

# Create a client using the credentials and region defined in the adminuser
# section of the AWS credentials and configuration files
session = Session(profile_name="adminuser")
polly = session.client("polly")

# Request confirmation
prompt = input if version_info >= (3, 0) else raw_input
proceed = prompt((u"This will delete the \"{0}\" lexicon,"
                  " do you want to proceed? [y,n]: ").format(arguments.name))

if proceed in ("y", "Y"):
    print(u"Deleting {0}...".format(arguments.name))

    try:
        # Request deletion of a lexicon by name
        response = polly.delete_lexicon(Name=arguments.name)
    except (BotoCoreError, ClientError) as error:
        # The service returned an error, exit gracefully
        cli.error(error)

    print("Done.")
else:
    print("Cancelled.")
```