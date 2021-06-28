# Applying Multiple Lexicons<a name="lexicons-applying"></a>

You can apply up to five lexicons to your text\. If the same grapheme appears in more than one lexicon that you apply to your text, the order in which they are applied can make a difference in the resulting speech\. For example, given the following text, "Hello, my name is Bob\." and two lexemes in different lexicons that both use the grapheme `Bob`\.

**LexA**

```
<lexeme>
   <grapheme>Bob</grapheme>
   <alias>Robert</alias>
</lexeme>
```

**LexB**

```
<lexeme>
   <grapheme>Bob</grapheme>
   <alias>Bobby</alias>
</lexeme>
```

If the lexicons are listed in the order LexA and then LexB, the synthesized speech will be "Hello, my name is Robert\." If they are listed in the order LexB and then LexA, the synthesized speech is "Hello, my name is Bobby\."

**Example – Applying LexA Before LexB**  

```
aws polly synthesize-speech \
--lexicon-names LexA LexB \
--output-format mp3 \
--text 'Hello, my name is Bob' \
--voice-id Justin \
bobAB.mp3
```
**Speech output:** "Hello, my name is Robert\."

**Example – Applying LexB before LexA**  

```
aws polly synthesize-speech \
--lexicon-names LexB LexA \
--output-format mp3 \
--text 'Hello, my name is Bob' \
--voice-id Justin \
bobBA.mp3
```
**Speech output:** "Hello, my name is Bobby\."

For information about applying lexicons using the Amazon Polly console, see [Applying Lexicons Using the Console \(Synthesize Speech\)](managing-lexicons-console.md#managing-lexicons-console-synthesize-speech)\.