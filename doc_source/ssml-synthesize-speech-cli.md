# Using SSML with the AWS CLI<a name="ssml-synthesize-speech-cli"></a>

The following topics demonstrate how to use SSML input with the AWS CLI for Amazon Polly\.

## Example 1: Passing SSML Through the Synthesize\-Speech Command<a name="example-ssml-synthesize-speech-cli"></a>

In the following `synthesize-speech` command, you specify a simple SSML string with only the required opening and closing `<speak></speak>` tags and the quotation marks that surround them\. \(Optionally, you can specify the full document header too\)\. Because plain text is the default, the command also specifies the `--text-type` parameter to indicate that the input text is SSML\. The only required elements for an SSML string are the input text \(targeted by the generated speech\), `output-format`, and `voice-id`\.

**Important**  
Although you do not use quotation marks around the input text in the Amazon Polly Console, they are required when using the AWS CLI or other code, both for plain text and SSML\. It is also important that the quotation marks around the entire input text and the quotation marks within the text are differentiated\.   
For example, you can use single quote marks \('\) surrounding the entire input text, and standard quotation marks \("\) in any interior tags or use the reverse\. \(When using the AWS CLI, both options will work for Unix, Linux, and macOS\. Standard quotations marks for the input text and single quote marks for interior tags are required when using a Windows command prompt\.\)   
 Thus you can use either   

```
--text '<speak>Hello <break time="300ms"/> World</speak>'
```
or  

```
--text "<speak>Hello <break time='300ms'/> World</speak>"
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

Play the resulting `speech.mp3` file to verify the synthesized speech\.

## Example 2: Synthesizing a Full SSML Document<a name="example-ssml-synthesize-document"></a>

In this example you save SSML content to a file and specify the file name in the `synthesize-speech` command\. This example uses the following SSML\.

```
<?xml version="1.0"?>
<speak version="1.1" 
       xmlns="http://www.w3.org/2001/10/synthesis"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
       xsi:schemaLocation="http://www.w3.org/2001/10/synthesis http://www.w3.org/TR/speech-synthesis11/synthesis.xsd"
       xml:lang="en-US">Hello World</speak>
```

Note that the `xml:lang` attribute specifies `en-US` \(US English\) as the language of the input text\. For information about how the language of the input text and the language of the voice selected affect the `SynthesizeSpeech` operation, see [Using the xml:lang Attribute](#example-ssml-foreign-language-words)\. 

**To test the SSML**

1. Save the SSML to a file \(`example.xml`\)\.

1. Run the following `synthesize-speech` command from the path where the XML file is stored and specify the SSML as input\. Note that because this points to a file rather than containing the actual input text, no quotation marks are needed\.

   The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

   ```
   aws polly synthesize-speech \
   --text-type ssml \
   --text file://example.xml \
   --output-format mp3 \
   --voice-id Joanna \
   speech.mp3
   ```

1. Play the `speech.mp3` file to verify the synthesized speech\.

## Example 3: Using Common SSML Tags<a name="example-common-ssml-tags"></a>

This section explains how to use some common SSML tags to achieve specific results\. For more examples, see [Speech Synthesis Markup Language \(SSML\) Version 1\.1](https://www.w3.org/TR/2010/REC-speech-synthesis11-20100907/)\.

You can use the `synthesize-speech` command to test the examples in this section\.

### Using the <break> Element<a name="ssml-break-element"></a>

The following SSML `synthesize-speech` command uses the `<break>` element to add a 300 millisecond delay between the words "Hello" and "World" in the resulting speech\.

```
<speak>
     Hello <break time="300ms"/> World.
</speak>
```

The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly synthesize-speech \
--text-type ssml \
--text '<speak>Hello <break time="300ms"/> World</speak>' \
--output-format mp3 \
--voice-id Joanna \
speech.mp3
```

Play the resulting `speech.mp3` file to verify the synthesized speech\.

### Using the <prosody> Element<a name="ssml-prosody-element"></a>

This element enables you to control pitch, speaking rate, and volume of speech\. 

+ The following SSML uses the `<prosody>` element to control volume:

  ```
  <speak>
       <prosody volume="+20dB">Hello world</prosody>
  </speak>
  ```

  The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

  ```
  aws polly synthesize-speech \
  --text-type ssml \
  --text '<speak><prosody volume="+20dB">Hello world</prosody></speak>' \
  --output-format mp3 \
  --voice-id Joanna \
  speech.mp3
  ```

+ The following SSML uses the `<prosody>` element to control pitch:

  ```
  <speak>
       <prosody pitch="x-high">Hello world.</prosody>
  </speak>
  ```

  The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

  ```
  aws polly synthesize-speech \
  --text-type ssml \
  --text '<speak><prosody pitch="x-high">Hello world</prosody></speak>' \
  --output-format mp3 \
  --voice-id Joanna \
  speech.mp3
  ```

+ The following SSML uses the `<prosody>` element to specify the speech rate:

  ```
  <speak>
       <prosody rate="x-fast">Hello world.</prosody>
  </speak>
  ```

  The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

  ```
  aws polly synthesize-speech \
  --text-type ssml \
  --text '<speak><prosody rate="x-fast">Hello world</prosody></speak>' \
  --output-format mp3 \
  --voice-id Joanna \
  speech.mp3
  ```

+ You can specify multiple attributes in a `<prosody>` element, as shown in the following example:

  ```
  <speak>
       <prosody volume="x-loud" pitch="x-high" rate="x-fast">Hello world.</prosody>
  </speak>
  ```

  The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

  ```
  aws polly synthesize-speech \
  --text-type ssml \
  --text '<speak><prosody volume="x-loud" pitch="x-high" rate="x-fast">Hello world</prosody></speak>' \
  --output-format mp3 \
  --voice-id Joanna \
  speech.mp3
  ```

Play the resulting `speech.mp3` file to verify the synthesized speech\.

### Using a whispered voice<a name="whispered-element"></a>

The following synthesize\-speech command uses the ` <amazon:effect name="whispered">` element to say the words "little lamb" in a whispered voice in the resulting speech: 

```
<speak>
     Mary has a <amazon:effect name="whispered">little lamb.</amazon:effect>
</speak>
```

This effect can be enhanced by slowing the whispered speech slightly using the <prosody> element\.

The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly synthesize-speech \
--text-type ssml \
--text '<speak> Mary has a <prosody rate="-10%"><amazon:effect name="whispered"> \
little lamb.</amazon:effect></prosody></speak>' \
--output-format mp3 \
--voice-id Joanna \
speech.mp3
```

Play the resulting `speech.mp3` file to verify the synthesized speech\. 

### Using the <emphasis> Element<a name="ssml-emphasis-element"></a>

This element enables you to specify the stress or prominence to apply when speaking a specified word or phrase\.

```
<speak>
     <emphasis level="strong">Hello</emphasis> world how are you?
</speak>
```

The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly synthesize-speech \
--text-type ssml \
--text '<speak><emphasis level="strong">Hello</emphasis> world how are you?</speak>' \
--output-format mp3 \
--voice-id Joanna \
speech.mp3
```

Play the resulting `speech.mp3` file to verify the synthesized speech\.

## Example 4: Controlling the Way Words are Said<a name="example-ssml-control-pronunciation"></a>

This example explains some of the common SSML tags you can use to control the way Amazon Polly says certain words, either by interpreting the words in a particular way or by how they're pronounced\. 

### Using the <say\-as> Element<a name="ssml-say-as-element"></a>

The <say\-as> element enables you to provide information about the type of text contained within the element\. 

For instance, in the following SSML, `<say-as>` indicates that the text 4/6 should be interpreted in a specific way, the attribute `interpret-as="date" format="dm"` indicates it should be said as a date value with the format month/day\. 

```
<speak>
     Today is <say-as interpret-as="date" format="md" >4/6</say-as>
</speak>
```

This element can also be used to say fractions, telephone numbers, measurement units, and more\.

The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\) and use full quotation marks \("\) around the input text with single quotes \('\) for interior tags\.

```
aws polly synthesize-speech \
--text-type ssml \
--text '<speak>Today is <say-as interpret-as="date" format="md" >4/6</say-as></speak>' \
--output-format mp3 \
--voice-id Joanna \
speech.mp3
```

 The resulting speech says "Today is June 4th"\. The `<say-as>` tag describes how the text should be interpreted by providing additional context via the `interpret-as` attribute\.

Play the resulting `speech.mp3` file to verify the synthesized speech\.

For more information on this element, see [<say\-as>](supported-ssml.md#say-as-tag)\.

### Using the xml:lang Attribute<a name="example-ssml-foreign-language-words"></a>

You can improve pronunciation of words that are foreign to the input text language by specifying the target language using the `xml:lang` attribute\. This forces the TTS engine to apply different pronunciation rules for the words that are specific to the target language\. The examples below show different combinations of languages for the input text and the voices you can specify in the `synthesize-speech` call\. You can test these examples using the `synthesize-speech` command to verify the results\.

For a complete list of which languages are available, see [Languages Supported by Amazon Polly](SupportedLanguage.md)\.

In this example, the chosen voice is a US English voice\. Amazon Polly assumes the input text is in the same language as the selected voice\. To achieve a Spanish pronunciation of specific words, you need to mark the targeted words as Spanish\. 

```
aws polly synthesize-speech \
--text-type ssml \
--text '<speak>That restaurant is terrific. <lang xml:lang="es-ES">Mucho gusto.</lang></speak>' \
--output-format mp3 \
--voice-id Joanna \
speech.mp3
```

Because the language of the input text is specified, Amazon Polly maps the resulting Spanish phonemes to English phonemes of the smallest acoustic distance\. As a result, Salli reads the text as a US native speaker who knows the correct Spanish pronunciation, but in a US English accent\.

**Note**  
This practice is limited to pairs of languages available in the Amazon Polly language portfolio\. Some language pairs work better than others because of the phonological structure of the languages\.

Play the resulting `speech.mp3` file to listen to the synthesized speech\.