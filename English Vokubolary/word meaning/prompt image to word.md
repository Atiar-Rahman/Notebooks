
# final prompt
হ্যাঁ—তোমার উদ্দেশ্য যদি **একদম 0 level থেকে vocabulary শেখা** হয়, তাহলে prompt-টা আরও strict করা ভালো। বিশেষ করে **description-এ ব্যবহৃত কোনো meaningful English word বাদ যাবে না**। তবে `a, an, the, is, am, are, in, on`-এর মতো grammar/function words-ও চাইলে শেখার জন্য আলাদা section-এ দেওয়া যাবে।

তুমি এই updated prompt-টা ব্যবহার করতে পারো:

```text
আমি তোমাকে একটি image দেব। ছবিটি খুব মনোযোগ দিয়ে পর্যবেক্ষণ করে English-এ একটি natural, detailed description লিখবে। আমার মূল উদ্দেশ্য হলো এই description ব্যবহার করে একদম 0 level থেকে English vocabulary শেখা।

IMPORTANT RULE:
Description-এ যে যে English word ব্যবহার করবে, কোনো meaningful word বাদ দেবে না। আমি যেহেতু একদম শুরু থেকে vocabulary শিখছি, তাই প্রতিটি শব্দের বাংলা meaning জানতে চাই।

### 1. Image Description

প্রথমে ছবিটির একটি natural এবং detailed English description লিখবে।

Description-এ ছবিতে স্পষ্টভাবে দেখা যায় এমন বিষয়গুলো উল্লেখ করবে, যেমন:
- মানুষ
- পোশাক
- শরীরের অবস্থান
- কাজ/action
- গাছপালা
- প্রাণী
- বস্তু
- জায়গা
- পরিবেশ
- রং
- আকার
- অবস্থান
- আলো
- আকাশ
- আবহাওয়া
- background
- foreground
- texture
- অন্যান্য গুরুত্বপূর্ণ visual details

Description-এ beginner-friendly English ব্যবহার করবে, কিন্তু vocabulary শেখানোর জন্য useful এবং slightly advanced শব্দও ব্যবহার করবে।

কোনো কিছু ছবিতে নিশ্চিতভাবে দেখা না গেলে সেটিকে fact হিসেবে বলবে না। প্রয়োজনে:
"It appears that..."
"It seems that..."
"It may be..."
এই ধরনের expression ব্যবহার করবে।

---

### 2. COMPLETE VOCABULARY BREAKDOWN

এটাই সবচেয়ে গুরুত্বপূর্ণ অংশ।

Description-এ ব্যবহৃত প্রতিটি English word/phrase vocabulary list-এ include করবে।

কোনো meaningful word skip করবে না।

একই word description-এ একাধিকবার থাকলে vocabulary list-এ একবারই দেবে।

শুধু খুব basic grammar words যেমন punctuation বা repeated articles বাদ দেওয়া যেতে পারে। কিন্তু আমি যেহেতু 0 level থেকে শুরু করছি, তাই useful ছোট শব্দও বাদ দেবে না।

যেমন:
beautiful
green
tree
person
walk
through
large
water
surface
behind
near
under
bright
slowly
etc.

প্রতিটি vocabulary-এর জন্য অবশ্যই দেবে:

1. English Word/Phrase
2. বাংলা Meaning
3. Part of Speech
4. Very Simple English Meaning
5. Pronunciation (বাংলা অক্ষরে সহজ pronunciation)
6. Example Sentence
7. Example Sentence-এর বাংলা Meaning

Output format:

| English Word/Phrase | বাংলা অর্থ | Part of Speech | Pronunciation | Very Simple English Meaning | Example Sentence | Example-এর বাংলা অর্থ |
|---|---|---|---|---|---|---|

---

### 3. WORD-BY-WORD DESCRIPTION BREAKDOWN

Description-টি sentence অনুযায়ী ভেঙে দেবে।

প্রতিটি sentence-এর নিচে সেই sentence-এর প্রতিটি important word-এর বাংলা meaning দেবে।

Example:

English:
"The woman is walking through the green tea garden."

Word breakdown:
- woman = নারী / মহিলা
- walking = হাঁটছে
- through = মধ্য দিয়ে
- green = সবুজ
- tea = চা
- garden = বাগান

বাংলা অর্থ:
"মহিলাটি সবুজ চা-বাগানের মধ্য দিয়ে হাঁটছেন।"

এভাবে description-এর প্রতিটি sentence explain করবে।

---

### 4. BASIC WORDS

আমি 0 level থেকে শুরু করছি, তাই description-এর মধ্যে থাকা basic vocabulary-ও আলাদা করে শেখাবে।

যেমন:

- woman = মহিলা
- man = পুরুষ
- tree = গাছ
- sky = আকাশ
- green = সবুজ
- walk = হাঁটা
- water = পানি
- big = বড়
- small = ছোট
- near = কাছে
- behind = পেছনে
- above = উপরে

অতিরিক্ত basic word হলেও বাদ দেবে না যদি সেটি description বুঝতে সাহায্য করে।

---

### 5. ADVANCED / USEFUL VOCABULARY

Description-এর মধ্যে থাকা তুলনামূলক কঠিন বা useful vocabulary আলাদা section-এ আবার দেখাবে।

যেমন:

- lush = ঘন সবুজ
- verdant = সবুজে ভরা
- picturesque = ছবির মতো সুন্দর
- tranquil = শান্ত ও প্রশান্ত
- abundant = প্রচুর
- foliage = গাছের পাতা
- expansive = বিস্তৃত

প্রতিটির বাংলা meaning এবং example sentence দেবে।

---

### 6. USEFUL PHRASES

Description-এ ব্যবহৃত useful phrases আলাদা করে দেবে।

যেমন:

- surrounded by = দ্বারা ঘেরা
- covered with = দিয়ে আবৃত
- in the foreground = ছবির সামনের অংশে
- in the background = ছবির পেছনের অংশে
- can be seen = দেখা যায়
- appears to be = মনে হচ্ছে / বলে মনে হয়
- walking through = মধ্য দিয়ে হাঁটা

প্রতিটির বাংলা meaning এবং একটি example sentence দেবে।

---

### 7. USEFUL SENTENCE PATTERNS

শেষে 5–10টি sentence pattern দেবে, যেগুলো আমি ভবিষ্যতে অন্য ছবি describe করতে ব্যবহার করতে পারি।

প্রতিটির সঙ্গে:
- English pattern
- বাংলা meaning
- একটি example

দেবে।

---

### IMPORTANT RULES

1. কোনো meaningful vocabulary skip করবে না।
2. Description-এর vocabulary এবং vocabulary list-এর মধ্যে মিল থাকতে হবে।
3. একই word বারবার থাকলে vocabulary list-এ একবার রাখবে।
4. কোনো word-এর বাংলা meaning ভুল বা অতিরিক্ত complicated করবে না।
5. Beginner-friendly বাংলা ব্যবহার করবে।
6. কঠিন vocabulary-এর pronunciation বাংলা অক্ষরে দেবে।
7. Noun-এর সঙ্গে article বা plural form থাকলে মূল word-টিও দেখাবে।
   Example: "trees" → tree = গাছ
8. Verb-এর ক্ষেত্রে base form দেখাবে।
   Example: "walking" → walk = হাঁটা
9. Adjective-এর মূল form দেখাবে।
10. কোনো word-এর একাধিক গুরুত্বপূর্ণ meaning থাকলে context অনুযায়ী relevant meaning দেবে।
11. Description খুব ছোট করবে না। ছবিতে যত meaningful visual information আছে, সেগুলো naturalভাবে describe করবে।
12. কিন্তু ছবিতে নেই এমন কোনো বিষয় invent করবে না।
13. আমার লক্ষ্য হলো English vocabulary একদম 0 level থেকে শেখা, তাই explanation সহজ রাখবে।
14. English word-এর সঙ্গে বাংলা pronunciation অবশ্যই দেবে।
15. Vocabulary শেখানোর সময় শুধু কঠিন word নয়—easy + medium + advanced সব useful word include করবে।

### FINAL OUTPUT FORMAT

## 1. Image Description
[Detailed English description]

## 2. Complete Vocabulary List
[Every meaningful word used in the description]

## 3. Sentence-by-Sentence Word Breakdown
[প্রতিটি sentence-এর word-by-word explanation]

## 4. Basic Vocabulary
[সব beginner-level useful words]

## 5. Advanced & Useful Vocabulary
[সব important harder words]

## 6. Useful Phrases
[Important phrases + বাংলা meaning]

## 7. Useful Sentence Patterns
[5–10 patterns + examples]

আমাকে এমনভাবে শেখাবে যেন আমি একদম 0 থেকে English vocabulary শুরু করেছি। কোনো meaningful vocabulary ইচ্ছাকৃতভাবে বাদ দেবে না।
```


