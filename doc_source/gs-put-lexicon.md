# Using the PutLexicon Operation<a name="gs-put-lexicon"></a>

With Amazon Polly, you can use [PutLexicon](API_PutLexicon.md) to store pronunciation lexicons in a specific AWS Region for your account\. Then, you can specify one or more of these stored lexicons in your [SynthesizeSpeech](API_SynthesizeSpeech.md) request that you want to apply before the service starts synthesizing the text\. For more information, see [Managing Lexicons](managing-lexicons.md)\.

This section provides example lexicons and step\-by\-step instructions for storing and testing them\.

**Note**  
These lexicons must conform to the Pronunciation Lexicon Specification \(PLS\) W3C recommendation\. For more information, see [Pronunciation Lexicon Specification \(PLS\) Version 1\.0](https://www.w3.org/TR/pronunciation-lexicon/#S4.7) on the W3C website\.

## Example 1: Lexicon with One Lexeme<a name="gs-put-lexicon-example-1"></a>

Consider the following W3C PLS\-compliant lexicon\. 

```
<?xml version="1.0" encoding="UTF-8"?>
<lexicon version="1.0" 
      xmlns="http://www.w3.org/2005/01/pronunciation-lexicon"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
      xsi:schemaLocation="http://www.w3.org/2005/01/pronunciation-lexicon 
        http://www.w3.org/TR/2007/CR-pronunciation-lexicon-20071212/pls.xsd"
      alphabet="ipa" 
      xml:lang="en-US">
  <lexeme>
    <grapheme>W3C</grapheme>
    <alias>World Wide Web Consortium</alias>
  </lexeme>
</lexicon>
```

Note the following:

+ The two attributes specified in the `<lexicon>` element:

  + The `xml:lang` attribute specifies the language code, `en-US`, to which the lexicon applies\. Amazon Polly can use this example lexicon if the voice you specify in the `SynthesizeSpeech` call has the same language code \(en\-US\)\. 
**Note**  
You can use the `DescribeVoices` operation to find the language code associated with a voice\.

     

  + The `alphabet` attribute specifies `IPA`, which means that the International Phonetic Alphabet \(IPA\) alphabet is used for pronunciations\. IPA is one of the alphabets for writing pronunciations\. Amazon Polly also supports the Extended Speech Assessment Methods Phonetic Alphabet \(X\-SAMPA\)\.

     

+ The `<lexeme>` element describes the mapping between `<grapheme>` \(that is, a textual representation of the word\) and `<alias>`\. 

To test this lexicon, do the following:

1. Save the lexicon as `example.pls`\.

1. Run the `put-lexicon` AWS CLI command to store the lexicon \(with the name `w3c`\), in the us\-east\-2 region\.

   ```
   aws polly put-lexicon \
   --name w3c \
   --content file://example.pls
   ```

1. Run the `synthesize-speech` command to synthesize sample text to an audio stream \(`speech.mp3`\), and specify the optional `lexicon-name` parameter\. 

   ```
   aws polly synthesize-speech \
   --text 'W3C is a Consortium' \
   --voice-id Joanna \
   --output-format mp3 \
   --lexicon-names="w3c" \
   speech.mp3
   ```

1. Play the resulting `speech.mp3`, and notice that the word W3C in the text is replaced by World Wide Web Consortium\.

The preceding example lexicon uses an alias\. The IPA alphabet mentioned in the lexicon is not used\. The following lexicon specifies a phonetic pronunciation using the `<phoneme>` element with the IPA alphabet\.

```
<?xml version="1.0" encoding="UTF-8"?>
<lexicon version="1.0" 
      xmlns="http://www.w3.org/2005/01/pronunciation-lexicon"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
      xsi:schemaLocation="http://www.w3.org/2005/01/pronunciation-lexicon 
        http://www.w3.org/TR/2007/CR-pronunciation-lexicon-20071212/pls.xsd"
      alphabet="ipa" 
      xml:lang="en-US">
  <lexeme>
    <grapheme>pecan</grapheme>
    <phoneme>pɪˈkɑːn</phoneme>
  </lexeme>
</lexicon>
```

Follow the same steps to test this lexicon\. Make sure you specify input text that has word "pecan" \(for example, "Pecan pie is delicious"\)\.

## Example 2: Lexicon with Multiple Lexemes<a name="gs-put-lexicon-example-2"></a>

In this example, the lexeme that you specify in the lexicon applies exclusively to the input text for the synthesis\. Consider the following lexicon: 

```
<?xml version="1.0" encoding="UTF-8"?>
<lexicon version="1.0"
      xmlns="http://www.w3.org/2005/01/pronunciation-lexicon"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.w3.org/2005/01/pronunciation-lexicon
        http://www.w3.org/TR/2007/CR-pronunciation-lexicon-20071212/pls.xsd"
      alphabet="ipa" xml:lang="en-US">

  <lexeme> 
    <grapheme>W3C</grapheme>
    <alias>World Wide Web Consortium</alias>
  </lexeme>
  <lexeme> 
    <grapheme>W3C</grapheme>
    <alias>WWW Consortium</alias>
  </lexeme>
  <lexeme> 
    <grapheme>Consortium</grapheme>
    <alias>Community</alias>
  </lexeme>
</lexicon>
```

The lexicon specifies three lexemes, two of which define an alias for the grapheme W3C as follows:

+ The first `<lexeme`> element defines an alias \(World Wide Web Consortium\)\.

+ The second `<lexeme>` defines an alternative alias \(WWW Consortium\)\. 

Amazon Polly uses the first replacement for any given grapheme in a lexicon\.

The third `<lexeme>` defines a replacement \(Community\) for the word Consortium\.

First, let's test this lexicon\. Suppose you want to synthesize the following sample text to an audio file \(`speech.mp3`\), and you specify the lexicon in a call to `SynthesizeSpeech`\.

```
The W3C is a Consortium
```

`SynthesizeSpeech` first applies the lexicon as follows: 

+ As per the first lexeme, the word W3C is revised as World Wide Web Consortium\. The revised text appears as follows:

  ```
  The World Wide Web Consortium is a Consortium
  ```

+ The alias defined in the third lexeme applies only to the word Consortium that was part of the original text, resulting in the following text:

  ```
  The World Wide Web Consortium is a Community.
  ```

You can test this using the AWS CLI as follows:

1. Save the lexicon as `example.pls`\.

1. Run the `put-lexicon` command to store the lexicon with name w3c in the us\-east\-2 region\.

   ```
   aws polly put-lexicon \
   --name w3c \
   --content file://example.pls
   ```

1. Run the `list-lexicons` command to verify that the w3c lexicon is in the list of lexicons returned\.

   ```
   aws polly list-lexicons
   ```

1. Run the `synthesize-speech` command to synthesize sample text to an audio file \(`speech.mp3`\), and specify the optional `lexicon-name` parameter\. 

   ```
   aws polly synthesize-speech \
   --text 'W3C is a Consortium' \
   --voice-id Joanna \
   --output-format mp3 \
   --lexicon-names="w3c" \
   speech.mp3
   ```

1. Play the resulting `speech.mp3` file to verify that the synthesized speech reflects the text changes\.

## Example 3: Specifying Multiple Lexicons<a name="gs-put-lexicon-example-3"></a>

In a call to `SynthesizeSpeech`, you can specify multiple lexicons\. In this case, the first lexicon specified \(in order from left to right\) overrides any preceding lexicons\.

Consider the following two lexicons\. Note that each lexicon describes different aliases for the same grapheme W3C\. 

+ Lexicon 1: `w3c.pls`

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <lexicon version="1.0" 
        xmlns="http://www.w3.org/2005/01/pronunciation-lexicon"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
        xsi:schemaLocation="http://www.w3.org/2005/01/pronunciation-lexicon 
          http://www.w3.org/TR/2007/CR-pronunciation-lexicon-20071212/pls.xsd"
        alphabet="ipa" xml:lang="en-US">
    <lexeme>
      <grapheme>W3C</grapheme>
      <alias>World Wide Web Consortium</alias>
    </lexeme>
  </lexicon>
  ```

+ Lexicon 2: `w3cAlternate.pls`

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <lexicon version="1.0"
        xmlns="http://www.w3.org/2005/01/pronunciation-lexicon"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.w3.org/2005/01/pronunciation-lexicon
          http://www.w3.org/TR/2007/CR-pronunciation-lexicon-20071212/pls.xsd"
        alphabet="ipa" xml:lang="en-US">
  
    <lexeme> 
      <grapheme>W3C</grapheme>
      <alias>WWW Consortium</alias>
    </lexeme>
  </lexicon>
  ```

Suppose you store these lexicons as `w3c` and `w3cAlternate` respectively\. If you specify lexicons in order \(`w3c` followed by `w3cAlternate`\) in a `SynthesizeSpeech` call, the alias for W3C defined in the first lexicon has precedence over the second\. To test the lexicons, do the following:

1. Save the lexicons locally in files called `w3c.pls` and `w3cAlternate.pls`\.

1. Upload these lexicons using the `put-lexicon` AWS CLI command\.

   + Upload the `w3c.pls` lexicon and store it as `w3c`\.

     ```
     aws polly put-lexicon \
     --name w3c \
     --content file://w3c.pls
     ```

   + Upload the` w3cAlternate.pls` lexicon on the service as `w3cAlternate`\.

     ```
     aws polly put-lexicon \
     --name w3cAlternate \
     --content file://w3cAlternate.pls
     ```

1. Run the `synthesize-speech` command to synthesize sample text to an audio stream \(`speech.mp3`\), and specify both lexicons using the `lexicon-name` parameter\. 

   ```
   aws polly synthesize-speech \
   --text 'PLS is a W3C recommendation' \
   --voice-id Joanna \
   --output-format mp3 \
   --lexicon-names '["w3c","w3cAlternative"]' \
   speech.mp3
   ```

1. Test the resulting `speech.mp3`\. It should read as follows:

   ```
   PLS is a World Wide Web Consortium recommendation
   ```

## Additional Code Samples for the PutLexicon API<a name="gs-put-lexicon-example-4"></a>

+ Java Sample: [PutLexicon](PutLexiconSample.md)

+ Python \(Boto3\) Sample: [PutLexicon](PutLexiconSamplePython.md)