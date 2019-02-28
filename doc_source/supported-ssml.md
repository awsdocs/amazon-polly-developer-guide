# SSML Tags Supported by Amazon Polly<a name="supported-ssml"></a>

Using SSML\-enhanced input text gives you additional control over how Amazon Polly generates speech from the text you provide\.

For example, you can include a long pause within your text, or change the speech rate or pitch\. Amazon Polly provides this type of control with a subset of the SSML markup tags that are defined by [Speech Synthesis Markup Language \(SSML\) Version 1\.1, W3C Recommendation](https://www.w3.org/TR/2010/REC-speech-synthesis11-20100907/)\.

## Supported SSML Tags<a name="supportedtags"></a>

Amazon Polly supports the following SSML tags:


|  Action  |  SSML Tag  | 
| --- | --- | 
|  [Adding a Pause](#break-tag)  |  <break>  | 
|  [Emphasizing Words ](#emphasis-tag)  | <emphasis> | 
|  [Specifying Another Language for Specific Words ](#lang-tag)  | <lang> | 
|  [Placing a Custom Tag in Your Text ](#custom-tag)  | <mark> | 
|  [Adding a Pause Between Paragraphs ](#p-tag)  |  <p>  | 
|  [Using Phonetic Pronunciation ](#phoneme-tag)  |  <phoneme>  | 
|  [Controlling Volume, Speaking Rate, and Pitch ](#prosody-tag)  |  <prosody>  | 
|  [Setting a Maximum Duration for Synthesized Speech](#maxduration-tag)  |  <prosody amazon:max\-duration>  | 
|  [Adding a Pause Between Sentences ](#s-tag)  |  <s>  | 
|  [Controlling How Special Types of Words Are Spoken ](#say-as-tag)  |  <say\-as>  | 
|  [Identifying SSML\-Enhanced Text ](#speak-tag)  |  <speak>  | 
|  [Pronouncing Acronyms and Abbreviations ](#sub-tag)  |  <sub>  | 
|  [Improving Pronunciation by Specifying Parts of Speech ](#w-tag)  |  <w>  | 
|  [Adding the Sound of Breathing ](#breath-tag)  |  <amazon:auto\-breaths>  | 
|  [Adding Dynamic Range Compression ](#drc-tag)  |  <amazon:effect name="drc">  | 
|  [Speaking Softly ](#phonation-tag)  |  <amazon:effect phonation="soft">  | 
|  [Controlling Timbre ](#vocaltractlength-tag)  |  <amazon:effect vocal\-tract\-length>  | 
|  [Whispering ](#whispered-tag)  |  <amazon: effect name="whispered">  | 

Unsupported SSML tags in input text generate errors\. 

### Identifying SSML\-Enhanced Text<a name="speak-tag"></a>

*<speak>*

The `<speak>` tag is the root element of all Amazon Polly SSML text\. All SSML\-enhanced text must be enclosed within a pair of <speak> tags\.

```
<speak>Mary had a little lamb.</speak>
```

### Adding a Pause<a name="break-tag"></a>

*<break>*

To add a pause to your text, use the <break> tag\. You can set a pause based on strength \(equivalent to the pause after a comma, a sentence, or a paragraph\), or you can set it to a specific length of time in seconds or milliseconds\. If you don't specify an attribute to determine the pause length, Amazon Polly uses the default, which is `<break strength="medium">`, which adds a pause the length of a pause after a comma\.

`strength` attribute values:
+ `none`: No pause\. Use `none` to remove a normally occurring pause, such as after a period\.
+ `x-weak`: Has the same strength as `none`, no pause\.
+ `weak`: Sets a pause of the same duration as the pause after a comma\.
+ `medium`: Has the same strength as `weak`\.
+ `strong`: Sets a pause of the same duration as the pause after a sentence\. 
+ `x-strong`: Sets a pause of the same duration as the pause after a paragraph\. 

`time` attribute values:
+ `[number]s`: The duration of the pause, in seconds\. The maximum duration is `10s`\.
+ `[number]ms`: The duration of the pause, in milliseconds\. The maximum duration is `10000ms`\.

For example:

```
<speak>
     Mary had a little lamb <break time="3s"/>Whose fleece was white as snow.
</speak>
```

If you don't use an attribute with the `break` tag, the result varies depending on text:
+ If there is no other punctuation next to the `break` tag, it creates a `<break strength="medium">` \(comma\-length pause\)\.
+ If the tag is next to a comma, it upgrades the tag to a `<break strength="strong">` \(sentence\-length pause\)\.
+ If the tag is next to a period, it upgrades the tag to `<break strength="x-strong">` \(paragraph\-length pause\)\.

### Emphasizing Words<a name="emphasis-tag"></a>

*<emphasis>*

To emphasize words, use the <emphasis> tag\. Emphasizing words changes the speaking rate and volume\. More emphasis makes Amazon Polly speak the text louder and slower\. Less emphasis makes it speak quieter and faster\. To specify the degree of emphasis, use the `level` attribute\.

`level` attribute values:
+ `Strong`: Increases the volume and slows the speaking rate so that the speech is louder and slower\.
+ `Moderate`: Increases the volume and slows the speaking rate, but less than `strong`\. `Moderate` is the default\. 
+ `Reduced`: Decreases the volume and speeds up the speaking rate\. Speech is softer and faster\.

**Note**  
The normal speaking rate and volume for a voice falls between the `moderate` and `reduced` levels\.

For example:

```
<speak>
     I already told you I <emphasis level="strong">really like</emphasis> that person.
</speak>
```

### Specifying Another Language for Specific Words<a name="lang-tag"></a>

*<lang>*

Specify another language for a specific word, phrase, or sentence with the <lang> tag\. Foreign language words and phrases are generally spoken better when they are enclosed within a pair of `<lang>` tags\. To specify the language, use the `xml:lang` attribute\. For a complete list of available languages, see [Languages Supported by Amazon Polly](SupportedLanguage.md)\.

 Unless you apply the `<lang>` tag, all of the words in the input text are spoken in the language of the voice specified in the `voice-id`\. If you apply the `<lang>` tag, the words are spoken in that language\. 

For example, if the `voice-id` is Joanna \(who speaks US English\), Amazon Polly speaks the following in the Joanna voice without a French accent:

```
<speak>
     Je ne parle pas français.
</speak>
```

If you use the Joanna voice with the `<lang>` tag, Amazon Polly speaks the sentence in the Joanna voice in American\-accented French:

```
<speak>
     <lang xml:lang="fr-FR">Je ne parle pas français.</lang>.
</speak>
```

Because Joanna is not a native French voice, pronunciation is based on her native language, US English\. For example, although perfect French pronunciation features an uvual trill /R/ in the word *français*, Joanna's US English voice pronounces this phoneme as the corresponding sound /r/\. 

If you use the `voice-id` of Giorgio, who speaks Italian, with the following text, Amazon Polly speaks the sentence in Giorgio's voice with an Italian pronunciation: 

```
<speak>
     Mi piace Bruce Springsteen.
</speak>
```

If you use the same voice with the following `<lang>` tag, Amazon Polly pronounces Bruce Springsteen in Italian\-accented English: 

```
<speak>
     Mi piace <lang xml:lang="en-US">Bruce Springsteen.</lang>
</speak>
```

This tag can also be used as a substitute for the optional [DefaultLangCode](API_StartSpeechSynthesisTask.html#polly-StartSpeechSynthesisTask-request-DefaultLangCode) option when synthesizing speech\. However, doing so requires that you format your text using SSML\.

### Placing a Custom Tag in Your Text<a name="custom-tag"></a>

*<mark>*

To put a custom tag within the text, use the <mark> tag\. Amazon Polly takes no action on the tag, but returns the location of the tag in the SSML metadata\. This tag can be anything you want to call out, as long as it maintains the following format:

```
<mark name="tag_name"/>
```

 For example, suppose that the tag name is "animal" and the input text is:

```
<speak>
     Mary had a little <mark name="animal"/>lamb.
</speak>
```

Amazon Polly might return the following SSML metadata: 

```
{"time":767,"type":"ssml","start":25,"end":46,"value":"animal"}
```

### Adding a Pause Between Paragraphs<a name="p-tag"></a>

*<p>*

To add a pause between paragraphs in your text, use the <p> tag\. Using this tag provides a longer pause than native speakers usually place at commas or the end of a sentence\. Use the <p> tag to enclose the paragraph:

```
<speak>
     <p>This is the first paragraph. There should be a pause after this text is spoken.</p> 
     <p>This is the second paragraph.</p> 
</speak>
```

This is equivalent to specifying a pause using <break strength="x\-strong"/>\.

### Using Phonetic Pronunciation<a name="phoneme-tag"></a>

*<phoneme>*

To make Amazon Polly use phonetic pronunciation for specific text, use the <phoneme> tag\. 

Two attributes are required with the `<phoneme>` tag\. They indicate the phonetic alphabet Amazon Polly uses and the phonetic symbols of the corrected pronunciation: 
+ `alphabet` 
  +  `ipa`— Indicates that the International Phonetic Alphabet \(IPA\) will be used\. 
  +  `x-sampa`— Indicates that the Extended Speech Assessment Methods Phonetic Alphabet \(X\-SAMPA\) will be used\.
+ `ph` 
  + Specifies the phonetic symbols for pronunciation\. For more information, see [Phoneme and Viseme Tables for Supported Languages](ref-phoneme-tables-shell.md)

With the `<phoneme>` tag, Amazon Polly uses the pronunciation specified by the `ph` attribute instead of the standard pronunciation associated by default with the language used by the selected voice\.

For instance, the word "pecan" can be pronounced two ways\. In the following example, “pecan” is assigned a different pronunciation in each line\. Amazon Polly pronounces pecan as specified in the `ph` attributes, instead of using the default pronunciation:

```
<speak>
     You say, <phoneme alphabet="ipa" ph="pɪˈkɑːn">pecan</phoneme>. 
     I say, <phoneme alphabet="ipa" ph="ˈpi.kæn">pecan</phoneme>.
</speak>
```

### Controlling Volume, Speaking Rate, and Pitch<a name="prosody-tag"></a>

*<prosody>*

To control the volume, rate, or pitch of your selected voice, use the `prosody` tag\.

Volume, speech rate, and pitch are dependent on the specific voice selected\. In addition to differences between voices for different languages, there are differences between individual voices speaking the same language\. Because of this, while attributes are similar across all languages, there are clear variations from language to language and no absolute value is available\. 

The `prosody` tag has three attributes, each of which has several available values to set the attribute\. Each attribute uses the same syntax:

```
<prosody attribute="value"></prosody>
```
+ `volume`
  + `default`: Resets volume to the default level for the current voice\.
  + `silent`, `x-soft`, `soft`, `medium`, `loud`, `x-loud`: Sets the volume to a predefined value for the current voice\. 
  + `+ndB`, `-ndB`: Changes volume relative to the current level\. A value of `+0dB` means no change, `+6dB` means approximately twice the current volume, and `-6dB` means approximately half the current volume\.

  For example, you could set the volume for a passage as follows:

  ```
  <speak>
       Sometimes it can sometimes be useful to <prosody volume="loud">increase the volume 
       for a specific speech.</prosody>                     
  </speak>
  ```

  Or you could set it this way:

  ```
  <speak>
       And sometimes a lower volume <prosody volume="-6dB">is a more effective way of 
       interacting with your audience.</prosody>  
  </speak>
  ```
+ `rate`
  +  `x-slow`, `slow`, `medium`, `fast`,`x-fast`\. Sets the pitch to a predefined value for the selected voice\.
  + `n%`: A non\-negative percentage change in the speaking rate\. For example, a value of 100% means no change in speaking rate, a value of 200% means a speaking rate twice the default rate, and a value of 50% means a speaking rate of half the default rate\. This value has a range of 20\-200%\.

  For example, you could set the speech rate for a passage as follows:

  ```
  <speak>
       For dramatic purposes, you might wish to <prosody rate="slow">speed up the speaking 
       rate of your text.</prosody>                     
  </speak>
  ```

  Or you could set it this way:

  ```
  <speak>
       Although in some cases, it might help your audience to <prosody rate="85%">slow 
       the speaking rate slightly to aid in comprehension.</prosody>  
  </speak>
  ```
+ `pitch`
  + `default`: Resets pitch to the default level for the current voice\.
  + `x-low`, `low`, `medium`, `high`, `x-high`: Sets the pitch to a predefined value for the current voice\. 
  + `+n%` or `-n%`: Adjusts pitch by a relative percentage\. For example, a value of `+0%` means no baseline pitch change, `+5%` gives a little higher baseline pitch, and `-5%` results in a little lower baseline pitch\.

  For example, you could set the pitch for a passage as follows:

  ```
  <speak>
       Do you like sythesized speech <prosody pitch="high">with a pitch that is higher 
       than normal?</prosody>                     
  </speak>
  ```

  Or you could set it this way:

  ```
  <speak>
       Or do you prefer your speech <prosody pitch="-10%">with a somewhat lower pitch?</prosody>  
  </speak>
  ```

The <prosody> tag must contain at least one attribute, but can include more within the same tag\. 

```
<speak>
     Each morning when I wake up, <prosody volume="loud" rate="x-slow">I speak  
     quite slowly and deliberately until I have my coffee.</prosody>
</speak>
```

It can also be combined with nested tags, as follows:

```
<speak>
     <prosody rate="85%">Sometimes combining attributes <prosody pitch="-10%">can 
     change the impression your audience has of a voice</prosody> as well.</prosody>                  
</speak>
```

### Setting a Maximum Duration for Synthesized Speech<a name="maxduration-tag"></a>

*<prosody amazon:max\-duration>*

To control how long you want a speech to take when it is synthesized, use the `<prosody>` tag with the `amazon:max-duration` attribute\.

The duration of synthesized speech varies slightly, depending on the voice you select\. This can make it difficult to match synthesized speech with visuals or other activities that require precise timing\. This issue is magnified for translation applications because the time it takes to say particular phrases can vary widely with different languages\.

The `<prosody amazon:max-duration>` tag matches synthesized speech to the amount of time you want it to take \(the duration\)\. 

This tag uses the following syntax:

```
<prosody amazon:max-duration="time duration">
```

With the `<prosody amazon:max-duration>` tag, you can specify duration in either seconds or milliseconds:
+ `ns`: the maximum duration in seconds
+ `nms`: the maximum duration in milliseconds

For example, the following spoken text has a maximum duration of 2 seconds: 

```
<speak>
     <prosody amazon:max-duration="2s">
          Human speech is a powerful way to communicate. 
     </prosody>
</speak>
```

Text placed within the tag, it doesn't exceed the specified duration\. If the chosen voice or language would normally take longer than that duration, Amazon Polly speeds up the speech so that it fits into the specified duration\. 

If the specified duration is longer than it takes to read the text at a normal rate, Amazon Polly reads the speech normally\. It doesn't slow down the speech or add silence, so the resulting audio is shorter than requested\. 

**Note**  
Amazon Polly increases the speed no more than 5 times the normal rate\. If text is spoken faster than this, it usually doesn't make sense\. If a speech cannot fit within your specfied duration even when speeded up to the maxium, the audio will be speeded up but will last longer than the specified duration\.

You can include a single sentence or multiple sentences within a `<prosody amazon:max-duration>` tag, and you can use multiple `<prosody amazon:max-duration>` tags within your text\.

For example:

```
<speak>
     <prosody amazon:max-duration="2400ms">
        Human speech is a powerful way to communicate.
     </prosody>
     <break strength="strong"/>
     <prosody amazon:max-duration="5100ms">
        Even a simple ‘Hello’ can convey a lot of information depending on the pitch, intonation, and tempo.
     </prosody>
     <break strength="strong"/>
     <prosody amazon:max-duration="8900ms">
        We naturally understand this information, which is why speech is ideal for creating applications where 
        a screen isn’t practical or possible, or simply isn’t convenient.
     </prosody>
</speak>
```

```
```

Using the `<prosody amazon:max-duration>` tag can increase latency when Amazon Polly is returns synthesized speech\. The degree of latency depends on the passage and its length\. We recommend using text comprised of relatively short text passages\. 

**Limitations**

There are limitations both in how you use `<prosody amazon:max-duration>` tag and in how it works with other SSML tags:
+ The text inside a `<prosody amazon:max-duration>` tag can't be longer than 1500 characters\. 
+ You can't nest `<prosody amazon:max-duration>` tags\. If you put one `<prosody amazon:max-duration>` tag inside another, Amazon Polly ignores the inner tag\.

  For example, in the following, the `<prosody amazon:max-duration="5s">` tag is ignored:

  ```
  <speak>
       <prosody amazon:max-duration="16s">
            Human speech is a powerful way to communicate.
          
            <prosody amazon:max-duration="5s">
                 Even a simple ‘Hello’ can convey a lot of information depending on the pitch, intonation, and tempo.
            </prosody>
  
            We naturally understand this information, which is why speech is ideal for creating applications where a screen isn’t practical or possible, or simply isn’t convenient.
       </prosody>
  </speak>
  ```
+ You can't use the `<prosody>` tags with the `rate` attribute within a `<prosody amazon:max-duration>` tag\. This is because both affect the speed at which text is spoken\. 

  In the following example, Amazon Polly ignores the `<prosody rate="2">` tag:

  ```
  <speak>
       <prosody amazon:max-duration="7500ms">
            Human speech is a powerful way to communicate.
        
            <prosody rate="2">
                 Even a simple ‘Hello’ can convey a lot of information depending on the pitch, intonation, and tempo.
            </prosody>
       </prosody>
  </speak>
  ```

**Pauses and `max-duration` **

When using `max-duration` tag, you can still insert pauses within your text\. However, Amazon Polly includes the length of the pause when calculating the maximum duration for speech\. Additionally, Amazon Polly preserves the short pauses that occur where commas and periods are placed within a passage and includes in the maximum duration\.

For example, in the following block, the 600 millisecond break and the breaks caused by the commas and periods occur within the 8\-second speech:

```
<speak>
     <prosody amazon:max-duration="8s">
          Human speech is a powerful way to communicate.
          <break time="600ms"/>
          Even a simple ‘Hello’ can convey a lot of information depending on the pitch, intonation, and tempo.
     </prosody>
</speak>
```

### Adding a Pause Between Sentences<a name="s-tag"></a>

*&lt;s>*

To add a pause between lines or sentences in your text, use the `<s>` tag\. Using this tag has the same effect as:
+ Ending a sentence with a period \(\.\)
+ Specifying a pause with `<break strength="strong"/>`

Unlike the `<break>` tag, the `<s>` tag encloses the sentence\. This is useful for synthesizing speech that is organized in lines, rather than sentence, such as poetry\.

In the following example, the `<s>` tag creates a short pause after both the first and second sentences\. The final sentence has no `<s>` tag, but it is also followed by a short pause because it ends with a period\.

```
<speak>
     <s>Mary had a little lamb</s> 
     <s>Whose fleece was white as snow</s> 
     And everywhere that Mary went, the lamb was sure to go.
</speak>
```

### Controlling How Special Types of Words Are Spoken<a name="say-as-tag"></a>

*<say\-as>*

Use the `<say-as>` tag with the `interpret-as` attribute to tell Amazon Polly how to say certain characters, words, and numbers\. This enables you to provide additional context to eliminate any ambiguity on how Amazon Polly should render the text\.

The `say-as` tag uses one attribute, <interpret\-as>, which uses a number of possible available values\. Each uses the same syntax:

```
<say-as interpret-as="value">[text to be interpreted]</say-as>
```

The following values are available with `interpret-as`:
+ `character` or `spell-out`: Spells out each letter of the text, as in a\-b\-c\.
+ `cardinal` or `number`: Interprets the numerical text as a cardinal number, as in 1,234\.
+ `ordinal`: Interprets the numerical text as an ordinal number, as in 1,234th\. 
+ `digits`: Spells out each digit individually, as in 1\-2\-3\-4\. 
+ `fraction`: Interprets the numerical text as a fraction\. This works for both common fractions such as 3/20, and mixed fractions, such as 2 ½\. See below for more information\.
+ `unit`: Interprets a numerical text as a measurement\. The value should be either a number or a fraction followed by a unit with no space in between as in `1/2inch`, or by just a unit, as in `1meter`\.
+ `date`: Interprets the text as a date\. The format of the date must be specified with the format attribute\. See below for more information\.
+ `time`: Interprets the numerical text as duration, in minutes and seconds, as in `1'21"`\. 
+ `address`: Interprets the text as part of a street address\. 
+ `expletive`: "Beeps out" the content included within the tag\. 
+ `telephone`: Interprets the numerical text as a 7\-digit or 10\-digit telephone number, as in `2025551212`\. You can also use this value for handle telephone extensions, as in `2025551212x345`\. See below for more information\.
**Note**  
Currently the `telephone` option is only available for English language voices\. 

**Fractions**

Amazon Polly interprets values within the `say-as` tag that have the `interpret-as="fraction"` attribute as common fractions\. The following is the syntax for fractions:
+ *Fraction*

  Syntax: *cardinal number*/*cardinal number*, such as 2/9\.

  For example: `<say-as interpret-as="fraction">2/9</say-as>` is pronounced "two ninths\."
+ *Non\-negative Mixed Number*

  Syntax: *cardinal number*\+*cardinal number*/*cardinal number*, such as 3\+1/2\. 

  For example, `<say-as interpret-as="fraction">3+1/2</say-as>` is pronounced "three and a half\."
**Note**  
There must be a `+` between the "3" and the "1/2"\. Amazon Polly doesn't support a mixed number without the `+`, such as "3 1/2"\.

**Dates**

When `interpret-as` is set to `date`, you also need to indicate the format of the date\. 

This uses the following syntax:

```
<say-as interpret-as="date" format="format">[date]</say-as>
```

For example:

```
<speak>
     I was born on <say-as interpret-as="date" format="dmy">12-31-1900</say-as>.
</speak>
```

The following formats can be used with the `date` attribute\.
+ `mdy`: Month\-day\-year\.
+ `dmy`: Day\-month\-year\.
+ `ymd`: Year\-month\-day\.
+ `md`: Month\-day\.
+ `dm`: Day\-month\.
+ `ym`: Year\-month\.
+ `my`: Month\-year\.
+ `d`: Day\.
+ `m`: Month\.
+ `y`: Year\.
+ `yyyymmdd`: Year\-month\-day\. If you use this format, you can make Amazon Polly skip parts of the date using question marks\. 

  For example, Amazon Polly renders the following as "September 22nd":

  ```
  <say-as interpret-as="date">????0922</say-as>
  ```

   `Format` is not needed\.

**Telephone**

Amazon Polly attempts to interpret the text you provide correctly based on the text’s formatting even without the `<say-as>` tag\. For example, if your text includes "202\-555\-1212," Amazon Polly interprets it as a 10\-digit telephone number and says each digit individually, with a brief pause for each dash\. In this case, you don't need to use `<say-as interpret-as="telephone">`\. However, if you provide the text “2025551212” and want Amazon Polly to say it as a phone number, you would specify `<say-as interpret-as="telephone">`\.

The logic for interpreting each element is language\-specific\. For example, US and UK English differ in how phone numbers are pronounced \(in UK English, sequences of the same digit are grouped together, as in "double five" or "triple four"\)\. To see the difference, test the following example with a US voice and with a UK voice: 

```
<speak>
     Richard's number is <say-as interpret-as="telephone">2122241555</say-as>
</speak>
```

### Pronouncing Acronyms and Abbreviations<a name="sub-tag"></a>

*<sub>*

Use the `<sub>` tag with the `alias` attribute to substitute a different word \(or pronunciation\) for selected text such as an acronym or abbreviation\.

This uses the syntax:

```
<sub alias="new word">abbreviation</sub>
```

 In the following example, the name "Mercury" is substituted for the element's chemical symbol to make the audio content clearer\.

```
<speak>
     My favorite chemical element is <sub alias="Mercury">Hg</sub>, because it looks so shiny. 
</speak>
```

### Improving Pronunciation by Specifying Parts of Speech<a name="w-tag"></a>

*<w>*

You can use the <w> tag to customize the pronunciation of words by specifying the word’s part of speech or alternate meaning\. This is done using the `role` attribute\.

This tag uses the following syntax: 

```
<w role="attribute">text</w>
```

The following values can be used for the `role` attribute:

To specify the part of speech:
+ `amazon:VB`: interprets the word as a verb \(present simple\)\.
+ `amazon:VBD`: interprets the word as past tense or as a past participle\.

For example, depending on its part of speech, the US English pronunciation of the word "read" varies based on the tag:

```
<speak>
     The word <say-as interpret-as="characters">read</say-as> may be interpreted 
     as either the present simple form <w role="amazon:VB">read</w>, or the past 
     participle form <w role="amazon:VBD">read</w>.
</speak>
```

To specify an alternate meaning:
+ `amazon:SENSE_1`: uses the non\-default sense of the word when present\. For example, the noun "bass" is pronounced differently depending on its meaning\. The default meaning is the lowest part of the musical range\. The alternate meaning is a species of freshwater fish, also called "bass" but pronounced differently\. Using `<w role="amazon:SENSE_1">bass</w>` renders the non\-default pronunciation \(freshwater fish\) for the audio text\.

  This difference can be heard if you synthesize the following:

  ```
  <speak>
      Depending on your meaning, the word <say-as interpret-as="characters">bass</say-as> 
      may be interpreted as either a musical element: read, or as its alternative meaning, 
      a fresh waterfish <w role="amazon:SENSE_1">bass</w>.
  </speak>
  ```

**Note**  
 Some languages may have a different selection of supported parts of speech\. 

### Adding the Sound of Breathing<a name="breath-tag"></a>

*<amazon:breath> and <amazon:auto\-breaths>*

Natural\-sounding speech includes both correctly spoken words and breathing sounds\. By adding breathing sounds to synthesized speech, you can make it sound more natural\. The `<amazon:breath>` and `<amazon:auto-breaths>` tags provide breaths\. You have the following options: 
+  Manual mode: you set the location, length, and volume of a breath sound within the text
+  Automated mode: Amazon Polly automatically inserts breathing sounds into the speech output
+  Mixed mode: both you and Amazon Polly add breathing sounds 

**Manual Mode**  
In manual mode, you place the `<amazon:breath/>` tag in the input text where you want to locate a breath\. You can customize the length and volume of breaths with the `duration` and `volume` attributes, respectively: 
+ `duration`: Controls the length of the breath\. Valid values are: `default`, `x-short`, `short`, `medium`, `long`, `x-long`\. The default value is `medium`\. 
+ `volume`: Controls how loud breathing sounds\. Valid values are: `default`, `x-soft`, `soft`, `medium`, `loud`, `x-loud`\. The default value is `medium`\. 

**Note**  
The exact length and volume of each attribute value is dependent on the specific Amazon Polly voice used\.

To set a breath sound using the defaults, use `<amazon:breath/>` without attributes\. 

For example, to use attributes to set the duration and volume for a breath to medium, you would set the attributes as follows: 

```
<speak>
     Sometimes you want to insert only <amazon:breath duration="medium" volume="x-loud"/>a single breath.
</speak>
```

To use the defaults, you would just use the tag:

```
<speak>
     Sometimes you need <amazon:breath/>to insert one or more average breathes <amazon:breath/> so that the 
     text sounds correct.
</speak>
```

You can add individual breathing sounds within a passage, as follows: 

```
<speak>
     <amazon:breath duration="long" volume="x-loud"/> <prosody rate="120%"> <prosody volume="loud"> 
     Wow! <amazon:breath duration="long" volume="loud"/> </prosody> That was quite fast <amazon:breath 
     duration="medium" volume="x-loud"/>. I almost beat my personal best time on this track. </prosody>
</speak>
```

**Automated Mode**  
In automated mode, you use the `<amazon:auto-breaths>` tag to tell Amazon Polly to automatically create breathing noises at appropriate intervals\. You can set the frequency of the intervals, their volume, and their duration\. Place the `</amazon:auto-breaths>` tag at the beginning of the text that you want to apply automated breathing to and the close the tag at the end\. 

**Note**  
Unlike the manual mode tag, `<amazon:breath/>`, the `<amazon:auto-breaths>` tag requires a closing tag \(`</amazon:auto-breaths>`\)\. 

You can use the following optional attributes with the `<amazon:auto-breaths>` tag: 
+ `volume`: Controls how loud the breathing sounds\. Valid values are: `default`, `x-soft`, `soft`, `medium`, `loud`, `x-loud`\. The default value is `medium`\.
+ `frequency`: Controls how often breathing sounds occur in the text\. Valid values are: `default`, `x-low`, `low`, `medium`, `high`, `x-high`\. The default value is `medium`\.
+ `duration`: Controls the length of the breath\. Valid values are: `default`, `x-short`, `short`, `medium`, `long`, `x-long`\. The default value is `medium`\. 

By default, the frequency of breathing sounds depends on the input text\. However, breathing sounds often occur after commas and periods\. 

The following examples show how to use the `<amazon:auto-breaths>` tag\. To decide which options to use for your content, copy the applicable examples to the Amazon Polly console and listen to the differences\. 
+  Using automated mode without optional parameters\. 

  ```
  <speak>
       <amazon:auto-breaths>Amazon Polly is a service that turns text into lifelike speech, 
       allowing you to create applications that talk and build entirely new categories of speech-
       enabled products. Amazon Polly is a text-to-speech service that uses advanced deep learning 
       technologies to synthesize speech that sounds like a human voice. With dozens of lifelike 
       voices across a variety of languages, you can select the ideal voice and build speech-
       enabled applications that work in many different countries.</amazon:auto-breaths>
  </speak>
  ```
+  Using automated mode with volume control\. The unspecified parameters \(`duration` and `frequency`\) are set to the default values \(`medium`\)\. 

  ```
  <speak>
       <amazon:auto-breaths volume="x-soft">Amazon Polly is a service that turns text into lifelike 
       speech, allowing you to create applications that talk and build entirely new categories of 
       speech-enabled products. Amazon Polly is a text-to-speech service, that uses advanced deep 
       learning technologies to synthesize speech that sounds like a human voice. With dozens of 
       lifelike voices across a variety of languages, you can select the ideal voice and build speech-
       enabled applications that work in many different countries.</amazon:auto-breaths>
  </speak>
  ```
+  Using automated mode with frequency control\. The unspecified parameters \(`duration` and `volume`\) are set to the default values \(`medium`\)\.

  ```
  <speak>
       <amazon:auto-breaths frequency="x-low">Amazon Polly is a service that turns text into lifelike 
       speech, allowing you to create applications that talk and build entirely new categories of 
       speech-enabled products. Amazon Polly is a text-to-speech service, that uses advanced deep 
       learning technologies to synthesize speech that sounds like a human voice. With dozens of 
       lifelike voices across a variety of languages, you can select the ideal voice and build speech-
       enabled applications that work in many different countries.</amazon:auto-breaths>
  </speak>
  ```
+  Using automated mode with multiple parameters\. For the unspecified `Duration` parameter, Amazon Polly uses the default value \(`medium`\)\.

  ```
  <speak>
       <amazon:auto-breaths volume="x-loud" frequency="x-low">Amazon Polly is a service that turns 
       text into lifelike speech, allowing you to create applications that talk and build entirely new 
       categories of speech-enabled products. Amazon Polly is a text-to-speech service, that uses 
       advanced deep learning technologies to synthesize speech that sounds like a human voice. With 
       dozens of lifelike voices across a variety of languages, you can select the ideal voice and build 
       speech-enabled applications that work in many different countries.</amazon:auto-breaths>
  </speak>
  ```

#### Adding Dynamic Range Compression<a name="drc-tag"></a>

*<amazon:effect name="drc">*

Depending on the text, language, and voice used in an audio file, the sounds range from soft to loud\. Environmental sounds, such as the sound of a moving vehicle, can often mask the softer sounds, which makes the audio track difficult to hear clearly\. To enhance the volume of certain sounds in your audio file, use the dynamic range compression \(`drc`\) tag\.

The `drc` tag sets a midrange "loudness" threshold for your audio, and increases the volume \(the gain\) of the sounds around that threshold\. It applies the greatest gain increase closest to the threshold, and the gain increase is lessened farther away from the threshold\. 

![\[Dynamic range compression increases the volume of the sounds around a certain threshold.\]](http://docs.aws.amazon.com/polly/latest/dg/images/drc-on.png)

This makes the middle\-range sounds easier to hear in a noisy environment, which makes the entire audio file clearer\.

The `drc` tag is a Boolean parameter \(it's either present or it isn't\)\. It uses the syntax: `<amazon:effect name="drc">` and is closed with `</amazon:effect>`\.

You can use the `drc` tag with any voice or language supported by Amazon Polly\. You can apply it to an entire section of the recording, or for only a few words\. For example:

```
<speak>
     Some audio is difficult to hear in a moving vehicle, but <amazon:effect name="drc"> this audio 
     is less difficult to hear in a moving vehicle.</amazon:effect>
</speak>
```

**Note**  
When you use "`drc`" in the `amazon:effect `syntax, it is case\-sensitive\. 

**Using `drc` with the `prosody volume` Tag**  
As the following graphic shows, the `prosody volume` tag evenly increases the volume of an entire audio file from the original level \(dotted line\) to an adjusted level \(solid line\)\. To further increase the volume of certain parts of the file, use the `drc` tag with the `prosody volume` tag\. Combining tags doesn't affect the settings of the `prosody volume` tag\. 

![\[Using the prosody volume tag increases the volume across the entire audio file.\]](http://docs.aws.amazon.com/polly/latest/dg/images/prosodyloud.png)

When you use the `drc` and `prosody volume` tags together, Amazon Polly applies the `drc` tag first, increasing the middle\-range sounds \(those near the threshold\)\. It then applies the `prosody volume` tag and further increases the volume of the entire audio track evenly\.

![\[Using the drc tag with a prosody volume tag increases the volume of the middle-range sounds in addition to the volume of the entire audio track.\]](http://docs.aws.amazon.com/polly/latest/dg/images/prosody+drc.png)

To use the tags together, nest one inside the other\. For example:

```
<speak>
     <prosody volume="loud">This text needs to be understandable and loud. <amazon:effect name="drc">
     This text also needs to be more understandable in a moving car.</amazon:effect></prosody> 
</speak>
```

In this text, the `prosody volume` tag increases the volume of the entire passage to "loud\." The `drc` tag enhances the volume of the middle\-range values in the second sentence\.

**Note**  
When using the `drc` and `prosody volume` tags together, use standard XML practices for nesting tags\.

#### Speaking Softly<a name="phonation-tag"></a>

*<amazon:effect phonation="soft">*

To specify that input text should be spoken in a softer\-than\-normal voice, use the <amazon:effect phonation="soft"> tag\.

This uses the syntax:

```
<amazon:effect phonation="soft">text</amazon:effect>
```

For example, you might use this tag with the Matthew voice as follows:

```
<speak>
     This is Matthew speaking in my normal voice. <amazon:effect phonation="soft">This 
     is Matthew speaking in my softer voice.</amazon:effect>
</speak>
```

#### Controlling Timbre<a name="vocaltractlength-tag"></a>

*<amazon:effect vocal\-tract\-length>*

Timbre is the tonal quality of a voice that helps you tell the difference between voices, even when they have the same pitch and loudness\. One of the most important physiological features that contributes to speech timbre is the length of the vocal tract\. The vocal tract is a cavity of air that spans from the top of the vocal folds up to the edge of the lips\. 

To control the timbre of output speech in Amazon Polly, use the `vocal-tract-length` tag\. This tag has the effect of changing the length of the speaker’s vocal tract, which sounds like a change in the speaker’s size\. When you increase the `vocal-tract-length`, the speaker sounds physically bigger\. When you decrease it, the speaker sounds smaller\. You can use this tag with any of the voices in the Amazon Polly Text\-to\-Speech portfolio\. 

To change timbre, use the following values: 
+ `+n%` or `-n%`: Adjusts the vocal tract length by a relative percentage change in the current voice\. For example, \+4% or \-2%\. Valid values range from \+100% to \-50%\. Values outside this range are clipped\. For example, \+111% sounds like \+100% and \-60% sounds like \-50%\.
+ `n%`: Changes the vocal tract length to an absolute percentage of the tract length of the current voice\. For example, 110% or 75%\. An absolute value of 110% is equivalent to a relative value of \+10%\. An absolute value of 100% is the same as the default value for the current voice\.

The following example shows how to change the vocal tract length to change timbre:

```
<speak>
     This is my original voice, without any modifications. <amazon:effect vocal-tract-length="+15%"> 
     Now, imagine that I am much bigger. </amazon:effect> <amazon:effect vocal-tract-length="-15%"> 
     Or, perhaps you prefer my voice when I'm very small. </amazon:effect> You can also control the 
     timbre of my voice by making minor adjustments. <amazon:effect vocal-tract-length="+10%"> 
     For example, by making me sound just a little bigger. </amazon:effect><amazon:effect 
     vocal-tract-length="-10%"> Or, making me sound only somewhat smaller. </amazon:effect> 
</speak>
```

**Combining Multiple Tags**

You can combine the `vocal-tract-length` tag with any other SSML tag that is supported by Amazon Polly\. Because timbre \(vocal tract length\) and pitch are closely connected, you might get the best results by using both the `vocal-tract-length` and the `<prosody pitch>` tags\. To produce the most realistic voice, we recommend that you use different percentages of change for the two tags\. Experiment with various combinations to get the results you want\. 

The following example shows how to combine tags\.

```
<speak> 
     The pitch and timbre of a person's voice are connected in human speech.
     <amazon:effect vocal-tract-length="-15%"> If you are going to reduce the vocal tract length, 
     </amazon:effect><amazon:effect vocal-tract-length="-15%"> <prosody pitch="+20%"> you 
     might consider increasing the pitch, too. </prosody></amazon:effect>  
     <amazon:effect vocal-tract-length="+15%"> If you choose to lengthen the vocal tract, 
     </amazon:effect> <amazon:effect vocal-tract-length="+15%"> <prosody pitch="-10%"> 
     you might also want to lower the pitch. </prosody></amazon:effect>
</speak>
```

#### Whispering<a name="whispered-tag"></a>

*<amazon:effect name="whispered">*

This tag indicates that the input text should be spoken in a whispered voice rather than as normal speech\. This can be used with any of the voices in the Amazon Polly Text\-to\-Speech portfolio\.

This uses the following syntax:

```
<amazon:effect name=”whispered”>text</amazon:effect>
```

For example:

```
<speak>
     <amazon:effect name="whispered">If you make any noise, </amazon:effect> 
     she said, <amazon:effect name="whispered">they will hear us.</amazon:effect>
</speak>
```

In this case, the synthesized speech spoken by the character is whispered, but the phrase "she said" is spoken in the normal synthesized speech of the selected Amazon Polly voice\.

You can enhance the "whispered" effect by slowing down the prosody rate by up to 10%, depending on the effect you want\. 

For example:

```
<speak>
     When any voice is made to whisper, <amazon:effect name="whispered">
     <prosody rate="-10%">the sound is slower and quieter than normal speech
     </prosody></amazon:effect>
</speak>
```

When generating speech marks for a whispered voice, the audio stream must also include the whispered voice to ensure that the speech marks match the audio stream\.