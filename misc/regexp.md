## Regular Expression

যখন w3school এর টিউটোরিয়ালে প্রথম Regular Expression দেখলাম, মনে করছিলাম কি খুব ই সহজ জিনিস!

```javascript
var patt = /w3schools/i;
```
পুরো পেইজ পড়লাম। না বেশ সহজ। 

কিন্তু আমার ধারনা ভুল প্রমাণিত হতে বেশি সময় লাগল না।

একটা প্রবলেম সলুশান করছিলাম। USA ফোন নাম্বার validate  করতে হবে। আর তখনই আমি নিচের কোড এর সম্মুখীন হইলাম। 
```javascript
var number = /1?\s?\(?[\d]{3}\)?-?\s?[\d]{3}-?\s?[\d]{4}/;
```
একটু ভয় পেয়ে গেলাম। ভয় পাব না কেন বলেন? এইরকম উল্টা-পাল্টা কিছু character দেখলে নতুন যে কেঊ ঘাবড়ে যাইতে পারে। 

নেট এ সার্চ কিছু বই ডাউনলোড করলাম। আরও বেশি ভয় পাইলাম।
অবশেষে Eloquent JavaScript বইটা পাইলাম, এটা পড়লাম। Regular Expression পুরো  chapter পড়লাম, এরপর একটু সহজ মনে হইতেছে। 

যাই হোক, লেখা শুরু করি।

প্রথমেই সংজ্ঞাঃ

উইকিপিডিয়ার থেকে,
>  A regular expression is a sequence of characters that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. "find and replace"-like operations.

সহজভাবে বললে,
> Regular Expression হল একটি object যা কিছু কিছু ধারাবাহিক characters  এর মাধ্যমে বর্ননা করা হয়।

Regular Expression দ্বারা একটি সার্চ প্যাটার্ন বানানো হয়। অর্থাৎ আমরা যে শব্দ অথবা বাক্যের জন্য সার্চ করব তাতে কতগুলো বর্ণ থাকবে, কি কি বর্ণ থাকবে, বাক্যে কত গুলো স্পেস থাকবে নাম্বার থাকবে কি না ইত্যাদি।

এর মধ্যে থাকতে পারেঃ
* Email
* Phone number
* Postal Code
* Date
* Time etc.

Sky is the limit.

আপনি যে কাজে ব্যবহার করেন।

## কিভাবে লিখতে হয়?
আগেই বলেছি *Regular Expression* হল  *object* । *Regular Expression* কে  **RegExp()** *constructor* দ্বারা define করা হয়। 
 
```javascript
var regexp = new RegExp("abc");
```

এর একটা সর্টকাট আছে। *string* কে যেমন  `''`/`""` (quotation mark) দিয়ে বোঝানো হয়, তেমনি *Regular Expression* কে এক জোড়া forward slash `/` এর মধ্যে specify করা হয়। 
```javascript
var regexp = /abc/i;
```

কোনটা সহজ? নিশ্চিতভাবে দ্বিতীয়টা। তাই এটি বেশি ব্যবহার করা হয়। কিন্তু এই পদ্ধতিতে কিছু সমস্যা আছে।
আমরা যে প্যাটার্ন match করতে চাই তা কে এক জোড়া forward slash `/` এর মধ্যে রাখতে হয়। উমম, যদি আমরা forward slash `/` ই match করতে চাই, তাহলে?

```javascript
var regexp = ///; // ????
```
সমস্যা!!! 

কিন্তু সমাধান খুবই সহজ। *string* বেলায় আমরা কি করি, যখন single qoute`""` এর মধ্যে  single quote `''` এসে পরে? 

```javascript
var str = 'I don't know Regular Expression'; // error
```
একটা escape character ব্যবহার করি। backslash `\`.

```javascript
var str = 'I don\'t know Regular Expression'; // this looks okay
```
 
*Regular Expression* এর ক্ষেত্রেও ***escape character to rescue***

```js
var regexp = /\//; // perfect 
```

কিছু character যেমন `+`  `?` , *Regular Expression* এ এগুলোর বিশেষ অর্থ আছে(যা আমরা পরে জানব),  এগুলো লেখার আগেও backslash `\` ব্যবহার করতে হয়। 

```javascript
var regexp = /abc\+/;
```

## Regular Expression Patterns



#### Literal Characters

 **Alphanumeric characters:** [a-zA-Z0-9]
 
 **nonalphabetic characters:**  

Character | Matches
:----------: | -------
\0 | The NUL character (\u0000)
\t | Tab (\u0009)
\n | Newline (\u000A)
\v | Vertical tab (\u000B)
\f | Form feed (\u000C)
\r | Carriage return (\u000D)

এই characters গুলো JavaScript regular-expression syntax সরাসরি সাপোর্ট করে। সরাসরি match  করে, `\` ছাড়া।

    ^ $ . * + ? = ! : | \ / ( ) [ ] { }
    
এই চিহ্ন গুলোর *Regular Expression Patterns* এ বিশেষ ব্যবহার আছে। তাই এগুলো ব্যবহার করতে হলে `\` আগে যোগ করে ব্যবহার করতে হয়।


### Character class

আলাদা আলাদা Literal Characters  কে square brackets `[]` মধ্যে আবদ্ধ করে একটি Character class বানানো যায়। `[]` যে সকল characters থাকবে শুধু মাত্র সেগুলো দিয়ে জন্যে সার্চ করা হবে, অর্ডার কোন ব্যাপার না, character গুলো থাকলেই হলো। যেমনঃ 

```javascript
console.log(/[abc]/.test("abcde"));
// → true
```
```javascript
console.log(/[abc]/.test("aebdc"));
// → true
```