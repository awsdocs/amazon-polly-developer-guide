# SSML Tags in Amazon Polly<a name="supported-ssml"></a>

Using SSML\-enhanced input text enables you to exert additional control over how Amazon Polly generates speech from the text you provide\.

For example, you can include a long pause within your text, or alter it in another way such as changing the speech rate or pitch\. Amazon Polly provides this type of control and more using a subset of the SSML markup tags as defined by [Speech Synthesis Markup Language \(SSML\) Version 1\.1, W3C Recommendation](https://www.w3.org/TR/2010/REC-speech-synthesis11-20100907/)

## Supported SSML Tags<a name="supportedtags"></a>

Amazon Polly supports the following SSML:

**root**

+ [<speak>](#speak-tag)

**standard tags**

+ [<break>](#break-tag)

+ [<emphasis>](#emphasis-tag)

+ [<lang>](#lang-tag)

+ [<mark>](#custom-tag)

+ [<p>](#p-tag)

+ [<phoneme>](#phoneme-tag)

+ [<prosody>](#prosody-tag)

+ [<s>](#s-tag)

+ [<say\-as>](#say-as-tag)

+ [<sub>](#sub-tag)

+ [<w>](#w-tag)

**Amazon Polly\-specific tags**

+ [<amazon:effect name="drc">](#drc-tag)

+ [<amazon:effect phonation="soft">](#phonation-tag)

+ [<amazon:effect vocal\-tract\-length>](#vocaltractlength-tag)

+ [<amazon:effect name="whispered">](#whispered-tag)

Note that any SSML tags in your input text that are unsupported are automatically ignored when Amazon Polly processes it\. 

## <speak><a name="speak-tag"></a>

 The `<speak>` tag is the root element of all Amazon Polly SSML text\. All SSML\-enhanced text to be spoken must be included within this tag\.

```
<speak>Mary had a little lamb.</speak>
```

## <break><a name="break-tag"></a>

This tag indicates a pause in the speech\. The length of the pause can be set with either a `strength` or `time` attribute\. If no attribute is used with a `break` tag, the default `<break strength="medium">` is used\.

The following values can be used with the `strength` attribute:

+ `none`: No pause occurs\. This can be used to remove a pause that would normally occur \(such as after a period\)\.

+ `x-weak`: Same as `none`\.

+ `weak`: Treats adjacent words as if they are separated by a single comma\.

+ `medium`: Same as `weak`\.

+ `strong`: Treats adjacent words as if they are separated by a sentence break \(equivalent to the `<s>` tag\)\. 

+ `x-strong`: Treats adjacent words as if they are separated by a paragraphy break \(equivalent to the ` <p>` tag\)\. 

The following values can be used with the `time` attribute:

+ `s`: Duration of the pause in seconds\. A pause may be up to `10s` in duration\.

+ `ms`: Duration of the pause in milliseconds\. A pause may be up to `10000ms`\.

For example:

```
<speak>
     Mary had a little lamb <break time="3s"/>Whose fleece was white as snow.
</speak>
```

## <emphasis><a name="emphasis-tag"></a>

This tag emphasizes the tagged words or phrases\. Emphasizing text changes the rate and volume of the speech\. More emphasis means the text is spoken louder and slower\. Less emphasis is quieter and faster\. The `level` attribute indicates the degree of emphasis that you want to place on the text\.

Three `level` options are available:

+ `Strong`: Increases the volume and slows down speaking rate so the speech is louder and slower\.

+ `Moderate`: Increases the volume and slows down the speaking rate, but less so than when set to `strong`\. This is the default and is used if no level is provided\.

+ `Reduced`: Decrease the volume and speed up the speaking rate\. The speech is softer and faster\.

**Note**  
The normal speaking rate and volume for a given voice will fall between the `moderate` and `reduced` levels\.

For example:

```
<speak>
     I already told you I <emphasis level="strong">really like</emphasis> that person.
</speak>
```

## <lang><a name="lang-tag"></a>

This tag indicates the language of a specific word or phrase\. Foreign language words and phrases are generally rendered better audibly when they are enclosed in inside a `<lang>` tag\. The language in which you want to render the pronunciation must be specified using the `xml:lang` attribute\. 

For a complete list of which languages are available, see [Languages Supported by Amazon Polly](SupportedLanguage.md)\.

The actual language in which the word or phrase is rendered is the language of the `voice-id` used, and not the language of the `<lang>` tag\. The tag serves only to set the pronunciation of the text, when it is different from the language of the `voice-id`\.

For example:

When the `voice-id` is Joanna \(American English\), run the following:

```
<speak>
     Je ne parle pas français.
</speak>
```

Amazon Polly will say this in the Joanna voice without attempting to use a French accent\. 

When the same voice is used with the following `<lang>` tab:

```
<speak>
     <lang xml:lang="fr-FR">Je ne parle pas français.</lang>.
</speak>
```

Amazon Polly will pronounce this in the Joanna voice using American\-accented French\.

However, because Joanna is not a native French voice, pronunciation is based on the language the voice speaks natively\. For example, while a perfect French pronunciation would feature an uvual trill /R/ in the word adore, Joanna's American English voice will pronounce it as this phoneme as the corresponding sound /r/\. 

In another, when the `voice-id` of Giorgio \(Italian\) is used with the following text: 

```
<speak>
     Mi piace Bruce Springsteen.
</speak>
```

Amazon Polly will say this in the Giorgio voice with no attempt to use a non\-Italian pronunciation\.

When the same voice is used with the following `<lang>` tab:

```
<speak>
     Mi piace <lang xml:lang="en-US">Bruce Springsteen.</lang>
</speak>
```

Amazon Polly will pronounce this in the Giorgio voice using Italian\-accented English\.

## <mark><a name="custom-tag"></a>

This tag provides the user with the ability to place a custom tag within the text\. No action is taken on the tag by Amazon Polly, but when SSML metadata is returned, the position of this tag will also be returned\.

This tag may be anything designated by the user with the following format:

```
<mark name="tag_name"/>
```

 For example, if the tag name is "animal" and the input text is:

```
<speak>
     Mary had a little <mark name="animal"/>lamb.
</speak>
```

the following SSML metadata might be returned by Amazon Polly

```
{"time":767,"type":"ssml","start":25,"end":46,"value":"animal"}
```

## <p><a name="p-tag"></a>

This tag indicates a paragraph in the text\. This is equivalent to specifying a pause with `<break strength="x-strong"/>`\. As with the `<s>` tag, this tag needs to enclose the sentence in question\.

```
<speak>
     <p>This is the first paragraph. There should be a pause after this text is spoken.</p> 
     <p>This is the second paragraph.</p> 
</speak>
```

## <phoneme><a name="phoneme-tag"></a>

This tag provides a phonetic pronunciation \(the phonemes\) for the indicated text\. 

Two attributes are required with the `phoneme` tag: 

+ `alphabet`

  +  `ipa`  — Indicates the phoneme uses The International Phonetic Alphabet \(IPA\) system\. 

  +  `x-sampa`  — Indicates the phoneme uses The Extended Speech Assessment Methods Phonetic Alphabet \(X\-SAMPA\) system\.

+ `ph`

  + Indicates the phonetic symbols to be used for pronunciation\. Amazon Polly supports standard IPA and X\-SAMPA phonetic symbols\. For more information see [Phonetic Tables Used by Amazon Polly](phonemetables.md)

When using the `phoneme` tag, Amazon Polly uses the pronunciation provided in the `ph` attribute rather than the one associated by default with the text contained within the tags\. However, you should still provide human\-readable text within the tags\. 

For instance, the word "pecan" can be pronounced two different ways\. In the following example, the word “pecan” is assigned a different custom pronunciation in each line\. Amazon Polly thus uses the pronunciation provided in the `ph` attributes instead of the default pronunciation:

```
<speak>
     You say, <phoneme alphabet="ipa" ph="pɪˈkɑːn">pecan</phoneme>. 
     I say, <phoneme alphabet="ipa" ph="ˈpi.kæn">pecan</phoneme>.
</speak>
```

**Note**  
In some cases phonetic symbols may include single or double quotes, which conflict with the quote marks used to mark the strings being spoken\. Use a backslash in these cases to mark the symbol so it doesn’t conflict with the string marker\.  
For example, when you use the IPA symbol for primary stress \(a single quote mark\), you would mark it as **\\'**\. The X\-SAMPA symbol for an open mid\-central unrounded r\-colored vowel \(**3'**\) is marked as **3\\'**\. The single or double quote string marker is not changed\.

## <prosody><a name="prosody-tag"></a>

The `prosody` tag enables you to control the volume, rate, and pitch of the delivery of the text\.

The following values can be used for the `volume` attribute, to modify the volume of the speech:

+ `default`: Resets volume to default for current voice\. 

+ `silent`, `x-soft`, `soft`, `medium`, `loud`, `x-loud`: Sets the volume to a predefined value for current voice\. 

+ `+ndB`, `-ndB`: Changes the volume relative to the current volume level\. A value of "\+0dB" means no change of volume, "\+6dB" means approximately twice the current amplitude, "\-6dB" means approximately half the current amplitude\. 

The following values can be used for the `rate` attribute, to modify the rate of speech:

+  `x-slow`, `slow`, `medium`, `fast`, `x-fast`: Sets the rate of speech to a predefined value for the current voice\. 

The following values can be used for the `pitch` attribute, to modify the pitch of the voice:

+ `default`: Resets pitch to the default pitch for the current voice\.

+ `x-low`, `low`, `medium`, `high`, `x-high`: Sets the pitch to a predefined value for the current voice\.

+ `+n%` or `-n%`: Adjusts pitch by a relative percentage change in the current pitch level of the current voice\. For example, `+4%`, or `-2%`\.

For example, prosody for a passage could be set in the following ways:

```
<speak>
     Prosody can be used to change the way words sound. The following words are 
     <prosody volume="x-loud"> quite a bit louder than the rest of this passage. 
     </prosody> Each morning when I wake up, <prosody rate="x-slow">I speak  
     quite slowly and deliberately until I have my coffee.</prosody> I can also  
     change the pitch of my voice using prosody. Do you like <prosody pitch="+5%"> 
     speech with a pitch that is higher,</prosody> or <prosody pitch="-10%"> 
     is a lower pitch preferable?</prosody>
</speak>
```

## <s><a name="s-tag"></a>

This tag indicates a sentence in the text\. This is equivalent to:

+ Ending a sentence with a period \(\.\)\.

+ Specifying a pause with `<break strength="strong"/>`\.

Unlike the `<break strength="strong"/>` tag, this tag needs to enclose the sentence in question\.

In this example, the `<s>` tag creates a short pause after both the first and second sentences\. The final sentence has no `<s>` tag but also has a short pause after it because it contains a period\.

```
<speak>
     <s>Mary had a little lamb</s> 
     <s>Whose fleece was white as snow</s> 
     And everywhere that Mary went, the lamb was sure to go.
</speak>
```

## <say\-as><a name="say-as-tag"></a>

This tag indicates how the input text should be interpreted\. This enables you provide additional context to eliminate any ambiguity on how Amazon Polly should render the text\.

When using the `say-as` tag, you need to indicate how Amazon Polly should interpret the text with the `interpret-as` attribute\. 

The following values are available with the `interpret-as` attribute:

+ `character` or `spell-out`: spells out each letter, as in a\-b\-c\.

+ `cardinal` or `number`: pronounces the value as a cardinal number, as in 1,234\.

+ `ordinal`: pronounces the value as an ordinal number, as in 1,234th\. 

+ `digits`: pronounces each digit of the number individually, as in 1\-2\-3\-4\. 

+ `fraction`: pronounces the value as a fraction\. This works for both common fractions such as 3/20, and mixed fractions, such as 2 1/2 \(see below\)\.

+ `unit`: interprets a value as a measurement\. The value should be followed by either a number or a fraction followed by a unit \(with no space in between\), or by just a unit, as in `1meter`\.

+ `date`: interprets the value as a date\. The format of the date must be specified with the format attribute \(see below\)\.

+ `time`: interprets the value as duration in minutes and seconds, as in `1'21"`\. 

+ `address`: interprets the value as part of a street address\. 

+ `expletive`: "bleeps" out the content included within the tag\. 

+ `telephone`: interprets the value as a 7\-digit or 10\-digit telephone, as in `2025551212` This can also handle telephone extensions, as in `2025551212x345`\.

The Amazon Polly service attempts to interpret the text you provide correctly based on the text’s formatting even without the `<say-as>` tag\. For example, if your text includes “202\-555\-1212”, Amazon Polly will interpret it as a 10\-digit telephone number and say each individual digit individually, with a brief pause for each dash\. It isn't necessary to use ` <say-as interpret-as="telephone">` in this case\. However, if you provide the text “2025551212” and want Amazon Polly to say it as a phone number, you need to use `<say-as interpret-as="telephone">`\.

The logic underlying the interpretation of each element is language\-specific\. For example, US and UK English differ in how phone numbers are pronounced \(in UK English, sequences of the same digit are grouped together, e\.g\. "double five" or "triple four"\)\. You can test the following example with a US voice and with a UK voice to demonstrate the difference: 

```
<speak>
     Richard's number is <say-as interpret-as="telephone">2122241555</say-as>
</speak>
```

**Fractions**

Amazon Polly will interpret values within the `say-as` having the `interpret-as="fraction"` attribute as common fractions\. The following is the syntax for fractions:

+ *Fraction*

  Syntax: *cardinal number*/*cardinal number* such as 2/9\.

  For example: `<say-as interpret-as="fraction">2/9</say-as>` is pronounced "two ninths"\.

+ *Non\-negative Mixed Number*

  Syntax: *cardinal number*\+*cardinal number*/*cardinal number* such as 3 1/2\. 

  For example: `<say-as interpret-as="fraction">3+1/2</say-as>` is pronounced "three and a half"\.

**Dates**

The following values can be used when `interpret-as` is set to `date` to indicate the format of the date:

+ `mdy`: month\-day\-year\.

+ `dmy`: day\-month\-year\.

+ `ymd`: year\-month\-day\.

+ `md`: month\-day\.

+ `dm`: day\-month\.

+ `ym`: year\-month\.

+ `my`: month\-year\.

+ `d`: day\.

+ `m`: month\.

+ `y`: year\.

+ `yyyymmdd`: year\-month\-day\. If this format is used, you can include question marks for portions of the date to leave out\. For instance, `<say-as interpret-as="date">????0922</say-as>` would be "September 22nd\."

## <sub><a name="sub-tag"></a>

This tag substitutes the pronunciation inside the `alias` attribute for the pronunciation of the text enclosed in the tag\. A common use for this tag is to provide expanded pronunciation for acronyms and abbreviations\.

```
<speak>
     My favorite chemical element is <sub alias="mercury">Hg</sub>, it looks cool. 
</speak>
```

## <w><a name="w-tag"></a>

Similar to `<say-as>`, this tag customizes word pronunciation by specifying the word’s part of speech\. The attribute `role` is included with the tag to specify the part of speech indicated\.

The following values can be used for the `role` attribute:

+ `amazon:VB`: interprets the word as a verb \(present simple\)\.

+ `amazon:VBD`: interprets the word as past tense or as a past participle\.

+ `amazon:SENSE_1`: uses the non\-default sense of the word when present\. For example, the default meaning of "bass" is that of the low note in a chord or the lowest part of the musical range\. This is pronounced differently than the alternate sense a freshwater fish, also called a "bass" but pronounced differently\. Using `<w role="amazon:SENSE_1">bass</w>` renders the non\-default pronunciation \(freshwater fish\) for the audio text\.

Depending how you intend to use it, the American English pronunciation of the word "read," depending on how it's being used: 

```
<speak>
     The present simple form of the word is pronounced <w role="amazon:VB">read</w>, 
where the past tense or past participle is pronounced <w role="amazon:VBD">read</w>.
</speak>
```

## <amazon:effect name="drc"><a name="drc-tag"></a>

Depending on the text, language, and voice used in an audio file, the sounds range from soft to loud\. Environmental sounds, such as the sound of a moving vehicle, can often mask the softer sounds, which makes the audio track difficult to hear clearly\. To enhance the volume of certain sounds in your audio file, use the dynamic range compression \(`drc`\) tag\.

The `drc` tag sets a mid\-range "loudness" threshold for your audio, and increases the volume \(the gain\) of the sounds around that threshold\. It applies the greatest gain increase closest to the threshold, and the gain increase is lessened farther away from the threshold\. 

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
When you use "`drc`" in the amazon:effect syntax, it is case\-sensitive\. 

**Using `drc` with the `prosody volume` tag**  
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

## <amazon:effect phonation="soft"><a name="phonation-tag"></a>

This tag indicates that the input text should be spoken in a softer than normal voice rather than as normal speech\. This can be used with any of the voices in the Amazon Polly Text\-to\-Speech portfolio\. It uses the syntax: `<amazon:effect phonation=”soft”>` and is closed with `</amazon:effect>`\.

For example, when using the Matthew voice:

```
<speak>
     This is Matthew speaking in my normal voice. <amazon:effect phonation="soft">This 
     is Matthew speaking in my softer voice.</amazon:effect>
</speak>
```

In this case, the first portion of the synthesized speech is spoken with a normal voice, whereas the portion using the `phonation` tag is spoken more softly\.

## <amazon:effect vocal\-tract\-length><a name="vocaltractlength-tag"></a>

Timbre is the tonal quality of a voice that helps you tell the difference between voices, even when they have the same pitch and loudness\. One of the most important physiological features which contribute towards speech timbre is the length of the vocal tract, a cavity of air which spans from the top of the vocal folds up to the edge of the lips\. 

To control the timbre of output speech in Amazon Polly, use the `vocal-tract-length` tag\. This tag has the effect of changing the length of the speaker’s vocal tract, which sounds like a change in the speaker’s size\. When you increase the `vocal-tract-length`, the speaker sounds physically bigger\. When you decrease it, the speaker sounds smaller\. You can use this tag with any of the voices in the Amazon Polly Text\-to\-Speech portfolio\. 

To change timbre, use the following values: 

+ `+n%` or `-n%`: Adjusts the vocal tract length by a relative percentage change in the current voice\. For example, \+4% or \-2%\. Valid values range from \+100% to \-50%\. Values outside this range areclipped\. For example, \+111% sounds like \+100% and \-60% sounds like \-50%\.

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

You can combine the `vocal-tract-length` tag with any other SSML tag that is supported by Amazon Polly\. Because timbre \(vocal tract length\) and pitch are closely connected, you might get the best results by using both the `vocal-tract-length` and the `<prosody pitch>` tags``\. To produce the most realistic voice, you will likely use different percentages of change for the two tags\. Experiment with various combinations to get the results you want\. 

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

## <amazon:effect name="whispered"><a name="whispered-tag"></a>

This tag indicates that the input text should be spoken in a whispered voice rather than as normal speech\. This can be used with any of the voices in the Amazon Polly Text\-to\-Speech portfolio\. It uses the syntax: `<amazon:effect name=”whispered”>` and is closed with `</amazon:effect>`\.

For example:

```
<speak>
     <amazon:effect name="whispered">If you make any noise, </amazon:effect> 
     she said, <amazon:effect name="whispered">they will hear us.</amazon:effect>
</speak>
```

In this case, the synthesized speech spoken by the character will be whispered, whereas the phrase "she said" will be in the normal synthesized speech of the selected Amazon Polly voice\.

You can enhance the "whispered" effect by slowing down the prosody rate by up to 10%, depending on the effect you desire\. 

For example:

```
<speak>
     When any voice is made to whisper, <amazon:effect name="whispered">
     <prosody rate="-10%">the sound is slower and quieter than normal speech
     </prosody></amazon:effect>
</speak>
```

When generating speech marks for a whispered voice, the audio stream must also include the whispered voice to ensure that the speech marks match the audio stream\.