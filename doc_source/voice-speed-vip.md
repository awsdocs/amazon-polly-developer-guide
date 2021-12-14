# Voice Speed<a name="voice-speed-vip"></a>

Because of the natural variation between voices, each available voice will speak the text at slightly different speeds\. For instance, with US English voices, Ivy and Joanna are slightly faster than Matthew when saying "Mary had a little lamb," and considerably faster than Joey\.

Since there is so much variation between voices, and the degree of that variation can depend on the text being spoken, no standard speed \(words per minute\) is available for Amazon Polly voices\. However, you can find how long it takes for your voice to say the selected text using SpeechMarks\. For more information on using speechmarks in Amazon Polly, see [Using Speech Marks ](using-speechmarks.md)

**To see approximately how long it takes to speak a text passage**

1. Open the AWS CLI\.

1. Run the following code, filling in as needed

   ```
        aws polly synthesize-speech \
             --language-code optional language code if needed
             --output-format json \
             --voice-id [name of desired voice] \
             --text '[desired text]' \
             --speech-mark-types='["viseme"]' \
             LengthOfText.txt
   ```

1. Open LengthOfText\.txt

If the text were "Mary had a little lamb," the last few lines returned by Amazon Polly would be:

```
     {"time":882,"type":"viseme","value":"t"}
     {"time":964,"type":"viseme","value":"a"}
     {"time":1082,"type":"viseme","value":"p"}
```

The last viseme, essentially the sound for the final letters in "lamb" starts 1082 milliseconds after the beginning of the speech\. While this is not exactly the length of the audio, it's close and can serve as the basis for comparison between voices\. 

## Changing Your Voice Speed<a name="voice-speed-change-vip"></a>

 For certain applications, you may find that you'd prefer the voice you like be slowed down, or speeded up\. If the speed of the voice is a concern, Amazon Polly provides the ability to modify this using SSML tags\.

For example:

Your organization is making an application that reads books to immigrant audiences\. The audience speaks English, but their fluency is limited\. In this case, you might consider slowing the rate of speech to give your audience a little more time for comprehension while the application is speaking\.

Amazon Polly helps you slow down the rate of speech using the SSML <prosody> tag, as in: 

```
<speak>
     In some cases, it might help your audience to <prosody rate="85%">slow 
     the speaking rate slightly to aid in comprehension.</prosody>
<speak>
```

or

```
<speak>
     In some cases, it might help your audience to <prosody rate="slow">slow 
     the speaking rate slightly to aid in comprehension.</prosody>
<speak>
```

Two speed options are available to you when using SSML with Amazon Polly:
+ Preset speeds: `x-slow`, `slow`, `medium`, `fast`, and `x-fast`\. In these cases, the speed of each option is approximate, depending on your preferred voice\. The `medium` option is the normal speed of the voice\.
+ n% of speech rate: any percentage of the speech rate, between 20% and 200% can be used\. In these cases, you can choose exactly the speed you want\. However, the actual speed of the voice is approximate, depending on the voice you've chosen\. 100% is considered to be the normal speed of the voice\.



Because the speed of each option is approximate and depends on the voice you choose, we recommend that you test your selected voice at various speeds to see what exactly meets your needs\. 

For more information on using the `prosody` tag to best effect, see [Controlling Volume, Speaking Rate, and Pitch ](supportedtags.md#prosody-tag)