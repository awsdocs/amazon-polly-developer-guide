# Chinese, Mandarin \(cmn\-CN\)<a name="ph-table-mandarin"></a>

The following table lists the Pinyin and International Phonetic Alphabet \(IPA\) phonemes for the Mandarin Chinese voice that is supported by Amazon Polly\. Pinyin is the international standard for Standard Chinese romanization\. IPA and X\-SAMPA are not commonly used but are available for English support\. The IPA and X\-SAMPA symbols in the table are for reference only and should not be used for Chinese transcription\. Pinyin examples and the corresponding visemes are also shown\.

To make Amazon Polly use phonetic pronunciation win Pinyin, use the `phoneme alphabet="x-amazon-phonetic standard used"` tag\.

The following examples show this with each standard\.

Pinyin:

```
<speak>
     你说 <phoneme alphabet="x-amazon-pinyin" ph="bo2">薄</phoneme>。 
     我说 <phoneme alphabet="x-amazon-pinyin" ph="bao2">薄</phoneme>。
</speak>
```

IPA:

```
<speak>
     你说 <phoneme alphabet="ipa" ph="pɪˈkɑːn">pecan</phoneme>。 
     我说 <phoneme alphabet="ipa" ph="ˈpi.kæn">pecan</phoneme>。
</speak>
```

X\-SAMPA:

```
<speak>
     你说 <phoneme alphabet='x-sampa' ph='pI"kA:n'>pecan</phoneme>。 
     我说 <phoneme alphabet='x-sampa' ph='"pi.k{n'>pecan</phoneme>。
</speak>
```

**Note**  
Amazon Polly accepts Mandarin Chinese input encoded in UTF\-8 only\. The GB 18030 encoding standard is not currently supported by Amazon Polly\. 


**Phoneme/Viseme Table**  

|  Pinyin  |  IPA  |  X\-SAMPA  |  Description  |  Pinyin Example  |  Viseme  | 
| --- | --- | --- | --- | --- | --- | 
|  **Consonants**  | 
|  f  |  f   |  f  |  voiceless labiodental fricative   |  发, **f**a1  |  f   | 
|  h  |  h   |  h  |  voiceless glottal fricative   |  和, **h**e2  |  k   | 
|  g  |  k   |  k  |  voiceless velar plosive   |  古, **g**u3   |  k   | 
|  k  |  kʰ   |  k\_h  |  aspirated voiceless velar plosive   |  苦, **k**u3   |  k   | 
|  l  |  l   |  l  |  alveolar lateral approximant   |  拉, **l**a1  |  t   | 
|  m  |  m   |  m  |  bilabial nasal   |  骂, **m**a4   |  p   | 
|  n  |  n   |  n  |  alveolar nasal   |  那, **n**a4   |  t   | 
|  ng  |  ŋ   |  N  |  velar nasal   |  正, zhe**ng**4   |  k   | 
|  b  |  p   |  p  |  voiceless bilabial plosive   |  爸, **b**a4  |  p   | 
|  p  |  pʰ   |  p\_h  |  aspirated voiceless bilabial plosive   |  怕, **p**a4   |  p   | 
| s |  s   |  s  |  voiceless alveolar fricative   |  四, **s**i4   |  s   | 
|  x  |  ɕ   |  s\\  |  voiceless alveolo\-palatal fricative   |  西, **x**i1   |  J   | 
|  sh  |  ʂ   |  s`  |  voiceless retroflex fricative   |  是, **sh**i4   |  S   | 
|  d  |  t   |  t  |  voiceless alveolar plosive   |  打, **d**a3   |  t   | 
|  t  |  tʰ   |  t\_h  |  aspirated voiceless alveolar plosive   |  他, **t**a1   |  t   | 
|  zh  |  ʈ͡ʂ   |  t`s`   |  voiceless retroflex affricate   |  之, **zh**i1   |  S   | 
|  ch  |  ʈ͡ʂʰ   |  t`s`\_h  |  aspirated voiceless retroflex affricate   |  吃, **ch**i1   |  S   | 
|  s  |  t͡s   |  ts  |  voiceless alveolar affricate   |  字, **z**i4   |  s   | 
|  j  |  t͡ɕ   |  ts\\  |  voiceless alveolo\-palatal affricate   |  鸡, **j**i1   |  J   | 
|  q  |  t͡ɕʰ   |  ts\\\_h  |  aspirated voiceless alveolo\-palatal affricate   |  七, **q**i1   |  J   | 
|  c  |  t͡sʰ   |  ts\_h  |  aspirated voiceless alveolar affricate   |  次, **c**i4   |  s   | 
|  w  |  w   |  w  |  labio\-velar approximant   |  我, **w**o3   |  u   | 
|  r  |  ʐ   |  z`  |  voiced retroflex fricative   |  日, **r**i4   |  S   | 
|  **"er" and "r" colored syllables**  | 
|  er  |  ɚ   |  @`   |  r\-coloured mid central vowel  |  二, **er**4   |  @   | 
|  \-r  |     |    |  r\-colored syllable   |  馅儿, xian**r**4   |  @   | 
|  **Vowels**  | 
|  e  |  ɤ   |  7  |  close\-mid back unrounded vowel   |  恶, **e**4  |  e   | 
|  e  |  ə   |  @  |  mid central vowel   |  恩, **e**n1  |  @   | 
|  a  |  a   |  a  |  open front unrounded vowel   |  安, **a**n1  |  a   | 
|  ai  |  aɪ   |  aI   |  diphthong   |  爱, **ai**4  |  a   | 
|  ao  |  aʊ   |  aU  |  diphthong   |  奥, **ao**4  |  a   | 
|  ei  |  eɪ   |  e  |  diphthong   |  诶, **ei**4  |  e   | 
|  e  |  ɛ   |  E  |  open\-mid front unrounded vowel   |  姐, ji**e**3  |  E   | 
|  i  |  i   |  i  |  close front unrounded vowel   |  鸡, j**i**1  |  i   | 
|  ou  |  oʊ   |  oU  |  diphthong   |  欧, **ou**1  |  o   | 
|  o  |  ɔ   |  O  |  open\-mid back rounded vowel   |  哦, **o**4  |  o   | 
|  u  |  u   |  u  |  close back rounded vowel   |  主, zh**u**3  |  u   | 
|  yu  |  y   |  y  |  close front rounded vowel   | 于, yu2 |  u   | 
|  **Tone marks and Additional Symbols**  | 
|  1  |     |  |  high level tone  |  淤, yu1   |  | 
|  2  |     |  |  rising tone  |  鱼, yu2   |  | 
|  3  |     |  |  low \(falling\-rising\) tone  |  语, yu3   |  | 
|  4  |     |  |  falling tone  |  育, yu4   |  | 
|  0  |     |  |  neutral tone  |  的, de0   |  | 
|  \-  |  \.  |  \.  |  syllable boundary  |  语音 yu3\-yin1  |     | 