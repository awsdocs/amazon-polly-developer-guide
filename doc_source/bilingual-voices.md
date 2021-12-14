# Bilingual Voices<a name="bilingual-voices"></a>

Amazon Polly has two ways of producing bilingual voices: 
+ [Accented bilingual voices](#accented-bilingual)
+ [Fully bilingual voices](#true-bilingual)

## Accented bilingual voices<a name="accented-bilingual"></a>

Accented bilingual voices can be created using any Amazon Polly voice, but only when using SSML tags\. 

Normally, all words in the input text are spoken in the default language of the voice specified you're using\. 

For example, if you're using the voice of Joanna \(who speaks US English\), Amazon Polly speaks the following in the Joanna voice without a French accent: 

```
<speak>
     Why didn't she just say, 'Je ne parle pas français?'
</speak>
```

In this case, the words *Je ne parle pas français* are spoken as they would be if they were English\. 

However, if you use the Joanna voice with the <lang> tag, Amazon Polly speaks the sentence in the Joanna voice in American\-accented French: 

```
<speak>
     Why didn't she just say, <lang xml:lang="fr-FR">'Je ne parle pas français?'</lang>.
</speak>
```

Because Joanna is not a native French voice, pronunciation is based on her native language, US English\. For instance, although perfect French pronunciation features an uvual trill /R/ in the word *français*, Joanna's US English voice pronounces this phoneme as the corresponding sound /r/\. 

If you use the voice of Giorgio, who speaks Italian, with the following text, Amazon Polly speaks the sentence in Giorgio's voice with an Italian pronunciation: 

```
<speak>
     Mi piace Bruce Springsteen.
</speak>
```

## Fully bilingual voices<a name="true-bilingual"></a>

A fully bilingual voice like Aditi \(Indian English and Hindi\) can speak two languages fluently\. This gives you the ability to use words and phrases from both languages in a single text using the same voice\. 

Currently, Aditi is the only fully bilingual voice available\. 

**Using a Bilingual Voice \(Aditi\) **

Aditi speaks both Indian English \(en\-IN\) and Hindi \(hi\-IN\) fluently\. You can synthesize speech in both English and Hindi, and the voice can switch between the two languages even within the same sentence\.

Hindi can be used in two different forms: 
+ Devanagari: "उसने कहाँ, खेल तोह अब शुरू होगा"
+ Romanagari \(using the Latin alphabet\): "Usne kahan, khel toh ab shuru hoga"

Additionally, it's possible to mix English and Hindi of either or both forms within a single sentence:
+ Devanagari \+ English: "This is the song कभी कभी अदिति"
+ Romanagari \+ English: "This is the song from the movie Jaane Tu Ya Jaane Na\." 
+ Devanagari \+ Romanagari \+ English: "This is the song कभी कभी अदिति from the movie Jaane Tu Ya Jaane Na\." 

Because Aditi is a bilingual voice, text in all of these cases will be read correctly, as Amazon Polly can differentiate between the languages and scripts\. 

Amazon Polly also supports numbers, dates, times, and currency expansion in both English \(Arabic numerals\) and Hindi \(Devanagari numerals\)\. By default, Arabic numerals are read in Indian English\. To make Amazon Polly read them in Hindi, you must use the `hi-IN` language code parameter\.