# Using SSML \(AWS CLI\)<a name="ssml-synthesize-speech-cli"></a>

You can use the AWS CLI to synthesize SSML input text\. The following examples show how to perform common tasks using the AWS CLI\. 

**Topics**
+ [Using SSML With the Synthesize\-Speech Command](#example-ssml-synthesize-speech-cli)
+ [Synthesizing an SSML\-enhanced Document](#example-ssml-synthesize-document)
+ [Using SSML for Common Amazon Polly Tasks](#example-common-ssml-tags)

## Using SSML With the Synthesize\-Speech Command<a name="example-ssml-synthesize-speech-cli"></a>

This example shows how to use the `synthesize-speech` command with an SSML string\. When you use the `synthesize-speech` command, you typically provide the following:
+ The input text \(required\) 
+ Opening and closing tags \(required\)
+ The output format
+ A voice 

In this example, you specify a simple text string in quotation marks along with the required opening and closing `<speak></speak>` tags\. 

**Important**  
Although you don't use quotation marks around input text in the Amazon Polly console, you must use them in use the AWS CLI It's also important that you differentiate between the quotation marks around input text and quotations required for individual tags\.  
For example, you can use standard quotation marks \("\) to enclose the input text, and single quotation marks \('\) for interior tags, or vice versa\. Either option works for Unix, Linux, and macOS\. However, with Windows you must enclose the input text in standard quotations marks and use single quotation marks for the tags\.   
For all operating systems, you can use standard quotation marks \("\) to enclose the input text, and single quotation marks \('\) for interior tags\)\. For example:  

```
--text "<speak>Hello <break time='300ms'/> World</speak>"
```
  
For Unix, Linux, and macOS, you can also use the reverse, with single quotation marks \('\) enclosing the input text and standard quotation marks \("\) for interior tags:  

```
--text '<speak>Hello <break time="300ms"/> World</speak>'
```


The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly synthesize-speech \
--text-type ssml \
--text '<speak>Hello world</speak>' \
--output-format mp3 \
--voice-id Joanna \
speech.mp3
```

To hear the synthesized speech, play the resulting `speech.mp3` file using any audio player\.

## Synthesizing an SSML\-enhanced Document<a name="example-ssml-synthesize-document"></a>

For longer input text, you may find it easier to save your SSML content to a file and simply specify the file name in the `synthesize-speech` command\. For example you could save the following to a file called `example.xml`:

```
<?xml version="1.0"?>
<speak version="1.1" 
       xmlns="http://www.w3.org/2001/10/synthesis"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xsi:schemaLocation="http://www.w3.org/2001/10/synthesis http://www.w3.org/TR/speech-synthesis11/synthesis.xsd"
       xml:lang="en-US">Hello World</speak>
```

The `xml:lang` attribute specifies `en-US` \(US English\) as the language of the input text\. For information about how the language of the input text and the language of the chosen voice affect the `SynthesizeSpeech` operation, see [Improving the Pronunciation of Foreign Words](#example-ssml-foreign-language-words)\. 

**To run an SSML\-enhanced file**

1. Save the SSML to a file \(for example, `example.xml`\)\.

1. Run the following `synthesize-speech` command from the path where the XML file is stored and specify the SSML file as input by substituting `file:\\example.xml` for the input text\. Because this command points to a file instead of containing the actual input text, you don't use quotation marks\.
**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws polly synthesize-speech \
   --text-type ssml \
   --text file://example.xml \
   --output-format mp3 \
   --voice-id Joanna \
   speech.mp3
   ```

1. To hear the synthesized speech, play the resulting `speech.mp3` file using any audio player\.

## Using SSML for Common Amazon Polly Tasks<a name="example-common-ssml-tags"></a>

The following examples show how to use SSML tags to complete common Amazon Polly tasks\. For more SSML tags, see [Supported SSML Tags](supportedtags.md)\. 

To test the following examples, use the following `synthesize-speech` command with the appropriate SSML\-enhanced text:

The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly synthesize-speech \
--text-type ssml \
--text '<speak>Hello <break time="300ms"/> World</speak>' \
--output-format mp3 \
--voice-id Joanna \
speech.mp3
```



### Adding a Pause<a name="ssml-break-element"></a>

To add a pause between words, use the <break> element\. The following SSML `synthesize-speech`command uses the `<break>` element to add a 300\-millisecond delay between the words "Hello" and "World\." 

```
<speak>
     Hello <break time="300ms"/> World.
</speak>
```



### Controlling Volume, Pitch, and Speed<a name="ssml-prosody-element"></a>

To control pitch, speaking rate, and speech volume, use the <prosody> element\. 
+ The following synthesize\-speech command uses the `<prosody>` element to control volume:

  ```
  <speak>
       <prosody volume="+20dB">Hello world</prosody>
  </speak>
  ```
+ The following `synthesize-speech` command uses the `<prosody>` element to control pitch:

  ```
  <speak>
       <prosody pitch="x-high">Hello world.</prosody>
  </speak>
  ```
+ The following `synthesize-speech` command uses the `<prosody>` element to specify the speech rate \(speaking speed\):

  ```
  <speak>
       <prosody rate="x-fast">Hello world.</prosody>
  </speak>
  ```
+ You can specify multiple attributes in a `<prosody>` element, as shown in the following examples:

  ```
  <speak>
       <prosody volume="x-loud" pitch="x-high" rate="x-fast">Hello world.</prosody>
  </speak>
  ```

### Whispering<a name="whispered-element"></a>

To whisper words, use the `<amazon:effect name="whispered">` element\. In the following example, the ` <amazon:effect name="whispered">` element tells Amazon Polly to whisper "little lamb": 

```
<speak>
     Mary has a <amazon:effect name="whispered">little lamb.</amazon:effect>
</speak>
```

To enhance this effect, use the <prosody> element to slightly slow down the whispered speech\.

### Emphasizing Words<a name="ssml-emphasis-element"></a>

To stress a word or phrase, use the <emphasis> element\.

```
<speak>
     <emphasis level="strong">Hello</emphasis> world how are you?
</speak>
```

### Specifying How to Say Certain Words<a name="ssml-say-as-element"></a>

To provide information about the type of text to be spoken, use the <say\-as> element\. 

For instance, in the following SSML, `<say-as>` indicates that the text 4/6 should be interpreted as a date\. The attribute `interpret-as="date" format="dm"` indicates that it should be spoken as a date with the format month/day\. 

You can also use the <say\-as> element to tell Amazon Polly to say numbers as fractions, telephone numbers, measurement units, and more\.



```
<speak>
     Today is <say-as interpret-as="date" format="md" >4/6</say-as>
</speak>
```

The resulting speech is "Today is June 4th\." The `<say-as>` tag describes how the text should be interpreted by providing additional context with the `interpret-as` attribute\.

To verify the accuracy of the synthesized speech, play the resulting `speech.mp3` file\.

For more information on this element, see [Controlling How Special Types of Words Are Spoken ](supportedtags.md#say-as-tag)\.

### Improving the Pronunciation of Foreign Words<a name="example-ssml-foreign-language-words"></a>

Amazon Polly assumes that the input text is in the same language as the language spoken by the voice you choose\. To improve the pronunciation of foreign words within input text, in the `synthesize-speech` call\. Specify the target language with the `xml:lang` attribute\. This tells Amazon Polly to apply different pronunciation rules for the foreign words that you tag\. 

The following examples show how to use different combinations of languages in the input text, and how to specify voices and the pronunciation of foreign words\. For a complete list of available languages, see [Languages Supported by Amazon Polly](SupportedLanguage.md)\.

In the following example, the voice \(Joanna\) is a US English voice\. By default, Amazon Polly assumes that the input text is in the same language as the voice \(in this case, US English\)\. When you use the `xml:lang` tag, Amazon Polly interprets the text as Spanish and the text is spoken as the selected voice would pronounce Spanish words, according to the pronunciation rules of the foreign language\. Without this tag, the text is spoken using the pronunciation rules of the selected voice\. 

```
<speak>
     That restaurant is terrific. <lang xml:lang="es-ES">Mucho gusto.</lang>
</speak>
```

Because the language of the input text is English, Amazon Polly maps the Spanish phonemes to the closest English phonemes\. As a result, Joanna speaks the text as a native US speaker who pronounces the works correctly in Spanish, but with a US English accent\.

**Note**  
Some languages are more similar than others, and so some language combinations work better than others\. 

