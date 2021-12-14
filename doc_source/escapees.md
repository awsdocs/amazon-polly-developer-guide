# Reserved Characters in SSML<a name="escapees"></a>

There are five predefined characters that can't normally be used within an SSML statement\. These entities are reserved by the language specification\. These characters are


| Name |       Character       |       Escape code       | 
| --- | --- | --- | 
| quotation mark \(double quotation mark\) | " | &quot; | 
| ampersand | & | &amp; | 
| apostrophe or single quotation mark | ' | &apos; | 
| less than sign | < | &lt; | 
| greater than sign | > | &gt; | 

Because SSML uses these characters as part of its code, to use these symbols in SSML, you must *escape* the character when you use it\. You use the escape code instead of the actual character so it displays properly while still creating a valid SSML document\. For example, the following sentence

```
We're using the lawyer at Peabody & Chambers, attorneys-at-law.
```

would be rendered in SSML as 

```
<speak>
We&apos;re using the lawyer at Peabody &amp; Chambers, attorneys-at-law.
</speak>
```

In this case, the special characters for the apostrophe and ampersand are escaped so the SSML document remains valid\.

For the **&**, **<**, and **>** symbols, escape codes are always necessary when you use SSML\. Additionallty, when you use the apostrophe/single quotation mark \(**'**\) as an apostrophe, you must also use the escape code\.

However, when you use the double quotation mark \(**"**\), or the apostrophe/single quotation mark \(**'**\) as a quotation mark, then whether or not you use the escape code is dependent on context\.

Double quotation marks 
+ Must be escaped when in a attribute value delimited by double quotes\. For example, in the following AWS CLI code 

  ```
  --text "Pete &quot;Maverick&quot; Mitchell"
  ```
+ Do not need to be escaped when in textual context\. For example, in the following

  ```
  He said, "Turn right at the corner."
  ```
+ Do not need to be escaped when in a attribute value delimited by single quotes\. For example, in the following AWS CLI code 

  ```
  --text 'Pete "Maverick" Mitchell'
  ```

Single quotation marks 
+ Must be escaped when used as an apostrophe\. For example, in the following 

  ```
  We&apos;ve got to leave quickly.
  ```
+ Do not need to be escaped when in textual context\. For example, in the following

  ```
  "And then I said, 'Don't quote me.'"
  ```
+ Do not need to be escaped when in a code attribute delimited by double quotes\. For example, in the following AWS CLI code 

  ```
  --text "Pete 'Maverick' Mitchell"
  ```