হ্যাঁ, **একদম এভাবেই এক একটা করে আগাবো।** 👍

আমাদের flow হবে:

```text
M02 — NLP Foundation
        │
        ├── M02.01 → Complete
        ├── M02.02 → Complete
        ├── M02.03 → Complete
        ├── M02.04 → Complete
        │      ...
        └── M02.84 → Final Project
```

প্রতিটি lesson **আগেরটার ওপর ভিত্তি করে** তৈরি হবে। কোনো গুরুত্বপূর্ণ topic skip করব না।

### প্রতিটি Lesson-এ থাকবে

1. **Concept**
2. **Why it is important**
3. **Internal working**
4. **Detailed explanation**
5. **Python examples**
6. **NLP examples**
7. **Real-world use case**
8. **Common mistakes**
9. **Practice problems**
10. **Theory questions**
11. **Interview questions**
12. **Mini challenge**
13. **AI/NLP project connection**
14. **Completion checklist**

আর যেখানে দরকার সেখানে:

```text
Theory
   ↓
Simple Example
   ↓
Python Implementation
   ↓
NLP Implementation
   ↓
Real Project Use
   ↓
Practice
```

### তাহলে এখন শুরু

**M02.01 — What is NLP?**

এখানে আমরা একদম foundation থেকে শুরু করব—NLP কী, কেন দরকার, computer কীভাবে human language দেখে, NLP-এর major tasks, NLP-এর evolution, AI/ML-এর সাথে NLP-এর relationship এবং তোমার future AI Writing project-এর সাথে NLP-এর connection।

তুমি শুধু **“M02.01”** বললেই আমি পুরো lesson শুরু করে দেব।


---
# 🧠 M02.01 — What is NLP?

আজ থেকে **PHASE 2 → NLP Foundation** শুরু।
আমরা একদম zero থেকে শুরু করব, যাতে পরে **Machine Learning → Deep Learning → Transformer → BERT/GPT → LLM → AI Writing System** বুঝতে কোনো gap না থাকে।

---

# 1. NLP কী?

**NLP = Natural Language Processing**

NLP হলো **Computer Science + Artificial Intelligence + Linguistics**-এর একটি field, যেখানে computer-কে মানুষের ভাষা:

* পড়তে
* বুঝতে
* বিশ্লেষণ করতে
* classify করতে
* translate করতে
* generate করতে

শেখানো হয়।

সহজভাবে:

> **NLP হলো computer-এর মাধ্যমে human language নিয়ে কাজ করার প্রযুক্তি।**

উদাহরণ:

```text
Human:
"I love Python."

        ↓

       NLP

        ↓

Computer:
এই sentence-এর অর্থ/structure কী?
Sentiment কী?
কোন শব্দ noun?
কোন শব্দ verb?
```

---

# 2. Natural Language বলতে কী বোঝায়?

**Natural Language** হলো মানুষ স্বাভাবিকভাবে যে language ব্যবহার করে।

যেমন:

```text
English
Bangla
Arabic
Hindi
Chinese
Japanese
French
German
```

উদাহরণ:

```text
I am learning Python.
আমি Python শিখছি।
```

এগুলো Natural Language।

অন্যদিকে:

```python
print("Hello")
```

এটা **Programming Language**।

---

# 3. Human Language বনাম Programming Language

এটা খুব গুরুত্বপূর্ণ।

### Programming Language

Computer-এর জন্য তৈরি:

```python
if age >= 18:
    print("Adult")
```

এখানে rules খুব strict।

একটি ছোট syntax error হলেও program কাজ নাও করতে পারে।

### Human Language

মানুষ একই কথা বিভিন্নভাবে বলতে পারে:

```text
I love Python.

I really like Python.

Python is one of my favorite languages.

I enjoy programming in Python.
```

মানুষ context দেখে অর্থ বুঝতে পারে।

Computer-এর জন্য এটা অনেক কঠিন।

---

# 4. NLP কেন দরকার?

আমরা প্রতিদিন প্রচুর text তৈরি করি:

```text
Facebook posts
Emails
Messages
News
Books
Reviews
Comments
Documents
Web pages
Search queries
```

মানুষ এগুলো বুঝতে পারে।

কিন্তু computer মূলত numbers/processes নিয়ে কাজ করে।

তাই আমাদের দরকার:

```text
Human Language
       ↓
      NLP
       ↓
Machine Representation
       ↓
Processing
       ↓
Useful Result
```

---

# 5. Computer-এর কাছে Text কী?

ধরো:

```text
"I love Python."
```

মানুষ দেখে:

> আমি Python পছন্দ করি।

কিন্তু computer-এর জন্য শুরুতে এটা মূলত characters-এর sequence:

```text
I
l
o
v
e
P
y
t
h
o
n
.
```

তারপর NLP pipeline এটাকে বিভিন্ন representation-এ convert করতে পারে:

```text
Raw Text
   ↓
Characters
   ↓
Tokens
   ↓
Token IDs
   ↓
Vectors
   ↓
Model
```

এই concept পুরো Phase 2-তে বারবার আসবে।

---

# 6. NLP-এর Basic Mental Model

এটা ভালোভাবে মনে রাখো:

```text
              HUMAN LANGUAGE
                     │
                     ↓
                   TEXT
                     │
                     ↓
              NLP PROCESSING
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
       Analyze    Understand   Generate
          │          │          │
          ↓          ↓          ↓
      Sentiment    Meaning     Text
      POS          Context     Translation
      NER          Intent      Summary
      Topic        Semantics   Response
```

---

# 7. NLP-এর প্রধান কাজগুলো

NLP অনেকগুলো task নিয়ে গঠিত।

---

## 7.1 Text Classification

Text-কে category দেওয়া।

Example:

```text
"I love this phone."
```

→ Positive

```text
"This phone is terrible."
```

→ Negative

আরেকটি:

```text
"Messi scored two goals."
```

→ Sports

```text
"Python is a programming language."
```

→ Technology

---

# 7.2 Sentiment Analysis

Text-এর emotion/sentiment বের করা।

```text
"I really love this product."
```

→ Positive

```text
"I hate this product."
```

→ Negative

```text
"The product arrived today."
```

→ Neutral

---

# 7.3 Named Entity Recognition — NER

Text থেকে গুরুত্বপূর্ণ entity খুঁজে বের করা।

```text
"Atiar lives in Dhaka."
```

সম্ভাব্য output:

```text
Atiar     → PERSON
Dhaka     → LOCATION
```

আর:

```text
"Google released a new product."
```

```text
Google → ORGANIZATION
```

---

# 7.4 Part-of-Speech Tagging

প্রতিটি word-এর grammatical role বের করা।

Sentence:

```text
Python is powerful.
```

Conceptually:

```text
Python   → NOUN
is       → VERB
powerful → ADJECTIVE
```

---

# 7.5 Machine Translation

এক language থেকে অন্য language-এ translation।

```text
English
   ↓
NLP
   ↓
Bangla
```

Example:

```text
"I am learning NLP."
```

↓

```text
"আমি NLP শিখছি।"
```

---

# 7.6 Text Summarization

বড় document থেকে summary তৈরি করা।

```text
Long Document
      ↓
     NLP
      ↓
Short Summary
```

দুই ধরনের concept:

### Extractive

মূল text-এর গুরুত্বপূর্ণ অংশ নির্বাচন করে।

### Abstractive

নিজে নতুনভাবে summary generate করে।

---

# 7.7 Question Answering

User:

```text
What is Python?
```

System:

```text
Python is a high-level programming language...
```

---

# 7.8 Text Generation

Input:

```text
Write a paragraph about AI.
```

System:

```text
Artificial intelligence is...
```

এখানেই আমরা পরবর্তীতে **GPT/LLM** বুঝব।

---

# 7.9 Text Similarity

দুটি text কতটা similar তা বের করা।

```text
Text A:
"I love programming."

Text B:
"I enjoy coding."
```

শব্দ আলাদা হলেও meaning কাছাকাছি।

এখানে আমরা পরে:

* TF-IDF
* Cosine Similarity
* Word Embedding
* Sentence Embedding

শিখব।

---

# 7.10 Spam Detection

```text
"Congratulations! You won $1,000."
```

→ Spam

```text
"Can you send me the report?"
```

→ Not Spam

---

# 8. NLP-এর 5টি গুরুত্বপূর্ণ স্তর

NLP বুঝতে linguistic levels জানা খুব গুরুত্বপূর্ণ।

```text
Language
   │
   ├── Morphology
   ├── Syntax
   ├── Semantics
   ├── Pragmatics
   └── Discourse
```

এগুলো একে একে বুঝি।

---

# 9. Morphology

**Morphology** হলো word-এর internal structure নিয়ে study।

Example:

```text
unhappiness
```

এখানে:

```text
un + happy + ness
```

আর:

```text
play
playing
played
player
```

এগুলো word formation-এর সাথে সম্পর্কিত।

NLP-তে এটা গুরুত্বপূর্ণ কারণ:

```text
word
 ↓
root
 ↓
morphological information
```

---

# 10. Syntax

**Syntax** হলো sentence-এর grammatical structure।

Example:

```text
Atiar reads a book.
```

Structure:

```text
Atiar
  ↓
Subject

reads
  ↓
Verb

a book
  ↓
Object
```

NLP-তে syntax বুঝতে:

* POS tagging
* Parsing
* Dependency parsing

ব্যবহার হয়।

---

# 11. Semantics

**Semantics = Meaning**

Example:

```text
"The boy ate the apple."
```

এখানে কে কী করল?

```text
boy → eater
apple → thing being eaten
ate → action
```

এটা sentence-এর meaning।

---

# 12. Pragmatics

একটি sentence-এর meaning **context-এর ওপর** নির্ভর করতে পারে।

Example:

```text
"Can you open the window?"
```

Literally এটা capability সম্পর্কে question।

কিন্তু বাস্তবে speaker-এর উদ্দেশ্য:

> Please open the window.

এই context-based meaning বুঝতে pragmatics গুরুত্বপূর্ণ।

---

# 13. Discourse

একাধিক sentence কীভাবে একে অপরের সাথে সম্পর্কিত সেটা discourse analysis-এর বিষয়।

Example:

```text
Atiar bought a laptop.
He uses it every day.
```

এখানে:

```text
He → Atiar
it → laptop
```

আগের sentence-এর information ব্যবহার করে পরের sentence বুঝতে হচ্ছে।

---

# 14. NLP কেন কঠিন?

Human language-এর কিছু বড় সমস্যা আছে।

## Ambiguity

একটি sentence-এর multiple meaning হতে পারে।

Example:

```text
I saw the man with a telescope.
```

এর অর্থ হতে পারে:

1. আমি telescope ব্যবহার করে লোকটিকে দেখেছি।
2. আমি এমন একজন লোককে দেখেছি যার কাছে telescope ছিল।

Computer-এর জন্য ambiguity resolve করা কঠিন।

---

# 15. Word Ambiguity

একটি word-এর multiple meaning থাকতে পারে।

Example:

```text
bank
```

Meaning 1:

```text
financial institution
```

Meaning 2:

```text
river bank
```

Sentence:

```text
I went to the bank.
```

vs

```text
I sat near the river bank.
```

Context অনুযায়ী meaning পরিবর্তন হয়েছে।

---

# 16. Synonym

একই বা কাছাকাছি meaning-এর word:

```text
big
large
huge
```

আর:

```text
happy
joyful
glad
```

NLP-তে semantic similarity-এর সময় এগুলো গুরুত্বপূর্ণ।

---

# 17. Antonym

Opposite meaning:

```text
good ↔ bad

hot ↔ cold

fast ↔ slow
```

---

# 18. Polysemy

একটি word-এর related multiple meanings।

Example:

```text
head
```

```text
head of a person
head of a company
head of a department
```

---

# 19. Context কেন গুরুত্বপূর্ণ?

এই sentence দেখো:

```text
I went to the bank.
```

এখানে bank কোন অর্থে ব্যবহৃত হয়েছে?

Context ছাড়া নিশ্চিত হওয়া কঠিন।

কিন্তু:

```text
I deposited money at the bank.
```

→ financial bank

আর:

```text
I sat on the bank of the river.
```

→ river bank

এই **context understanding** modern NLP-এর সবচেয়ে গুরুত্বপূর্ণ ধারণাগুলোর একটি।

---

# 20. NLP-এর Evolution

NLP একদিনে তৈরি হয়নি।

একটি simplified timeline:

```text
Rule-Based NLP
      ↓
Statistical NLP
      ↓
Machine Learning NLP
      ↓
Deep Learning NLP
      ↓
Word Embeddings
      ↓
RNN / LSTM
      ↓
Attention
      ↓
Transformer
      ↓
BERT / GPT
      ↓
Large Language Models
```

আমরা Phase 2-তে এই evolution বুঝব।

---

# 21. Rule-Based NLP

প্রথম দিকের NLP systems অনেকটা manually written rules-এর ওপর নির্ভর করত।

Example:

```text
IF text contains "good"
THEN sentiment = positive
```

Problem:

```text
"This is not good."
```

এখানে `"good"` আছে কিন্তু sentiment negative।

আর:

```text
"Not bad."
```

এখানে `"bad"` আছে কিন্তু sentiment positive/neutral হতে পারে।

Rules যত বাড়বে system তত complex হবে।

---

# 22. Statistical NLP

পরবর্তীতে probability/statistics ব্যবহার করা শুরু হলো।

Concept:

```text
P(word | context)
```

যেমন:

```text
"I drink a cup of ___"
```

সম্ভাব্য:

```text
tea
coffee
water
```

এই ধরনের probabilistic language modeling পরে আরও advanced হয়েছে।

---

# 23. Machine Learning NLP

তারপর machine learning:

```text
Text
 ↓
Features
 ↓
ML Algorithm
 ↓
Prediction
```

যেমন:

```text
TF-IDF
   ↓
Logistic Regression
   ↓
Spam / Not Spam
```

---

# 24. Deep Learning NLP

তারপর neural networks:

```text
Text
 ↓
Embedding
 ↓
Neural Network
 ↓
Prediction
```

Models:

```text
RNN
LSTM
GRU
```

---

# 25. Transformer Era

বর্তমান modern NLP-এর সবচেয়ে গুরুত্বপূর্ণ architecture:

**Transformer**

Basic idea:

```text
Text
 ↓
Tokenization
 ↓
Embeddings
 ↓
Attention
 ↓
Transformer
 ↓
Output
```

Transformer-এর ওপর ভিত্তি করে তৈরি হয়েছে:

```text
BERT
GPT
T5
RoBERTa
LLaMA
সহ আরও অনেক model
```

Phase 2-এর শেষের দিকে আমরা Transformer-এর foundation বিস্তারিতভাবে শিখব।

---

# 26. NLP বনাম ML বনাম DL বনাম AI

এখানে confusion অনেকের হয়।

```text
Artificial Intelligence
│
├── Machine Learning
│   │
│   └── Deep Learning
│
└── NLP
```

তবে এগুলো strict nested boxes হিসেবে সবসময় ভাবা ঠিক নয়; NLP একটি application/research domain, যেখানে rule-based methods থেকে ML/DL পর্যন্ত অনেক approach ব্যবহৃত হয়।

সহজভাবে:

### AI

Machine-কে intelligent behavior করানোর বড় field।

### ML

Data থেকে pattern শেখানো।

### Deep Learning

Neural network-এর মাধ্যমে learning।

### NLP

Human language নিয়ে computational processing।

এরা একে অপরের সাথে overlap করে।

---

# 27. NLP + Machine Learning

Example:

```text
Reviews
   ↓
Preprocessing
   ↓
TF-IDF
   ↓
Machine Learning
   ↓
Sentiment
```

---

# 28. NLP + Deep Learning

```text
Text
 ↓
Tokenizer
 ↓
Embedding
 ↓
Neural Network
 ↓
Prediction
```

---

# 29. NLP + LLM

Modern system:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
Transformer
 ↓
Attention
 ↓
Next Token Prediction
 ↓
Generated Text
```

এখানেই আমাদের future AI Writing system-এর foundation।

---

# 30. NLP কোথায় ব্যবহার হয়?

বাস্তব জীবনে NLP everywhere।

### Search Engine

```text
"What is Python?"
```

→ relevant results

### Chatbot

```text
User
 ↓
NLP
 ↓
Response
```

### Email

```text
Spam detection
Smart reply
Email classification
```

### Social Media

```text
Sentiment
Toxicity
Topic detection
```

### Customer Service

```text
User complaint
 ↓
Intent detection
 ↓
Appropriate response
```

### Translation

```text
English → Bangla
Bangla → English
```

### Writing Assistant

```text
Text
 ↓
Grammar
 ↓
Style
 ↓
Clarity
 ↓
Rewrite
```

---

# 31. তোমার AI Writing Project-এর সাথে NLP

এটা তোমার জন্য সবচেয়ে গুরুত্বপূর্ণ অংশ।

তুমি ভবিষ্যতে একটি AI Writing Assistant তৈরি করতে চাইলে:

```text
User Text
     ↓
Text Preprocessing
     ↓
Sentence Segmentation
     ↓
Tokenization
     ↓
Linguistic Analysis
     ↓
Semantic Representation
     ↓
AI Model
     ↓
Rewrite / Improve
     ↓
Quality Analysis
     ↓
Final Text
```

এখানে Phase 2-এর প্রায় প্রতিটি topic কাজে আসবে।

---

# 32. Example — একটি Text বিশ্লেষণ

Input:

```text
"Python is a very powerful programming language."
```

NLP pipeline conceptually:

```text
Raw Text
   ↓
Sentence
   ↓
Tokens
```

```text
[
"Python",
"is",
"a",
"very",
"powerful",
"programming",
"language"
]
```

তারপর:

```text
POS
```

Conceptually:

```text
Python       → NOUN
is           → VERB
a            → DET
very         → ADV
powerful     → ADJ
programming  → NOUN/Modifier
language     → NOUN
```

তারপর:

```text
Embedding
```

শেষে model text-এর representation নিয়ে কাজ করতে পারে।

---

# 33. NLP Pipeline — Full Mental Model

এটা আজকের সবচেয়ে গুরুত্বপূর্ণ diagram:

```text
                 RAW TEXT
                    │
                    ↓
              TEXT CLEANING
                    │
                    ↓
              NORMALIZATION
                    │
                    ↓
              TOKENIZATION
                    │
                    ↓
         ┌──────────┴──────────┐
         ↓                     ↓
   Linguistic Analysis    Feature Extraction
         ↓                     ↓
   POS / NER / Syntax     BoW / TF-IDF
         │                     │
         └──────────┬──────────┘
                    ↓
              REPRESENTATION
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
     Classical ML        Embeddings
          │                   │
          └─────────┬─────────┘
                    ↓
               NLP MODEL
                    │
                    ↓
               PREDICTION
                    │
                    ↓
                EVALUATION
```

Modern NLP:

```text
Raw Text
   ↓
Tokenizer
   ↓
Token IDs
   ↓
Embedding
   ↓
Transformer
   ↓
Prediction / Generation
```

---

# 34. আজকের Important Terms

আজ এগুলো পরিষ্কারভাবে জানতে হবে:

| Term             | Meaning                                            |
| ---------------- | -------------------------------------------------- |
| NLP              | Natural Language Processing                        |
| Natural Language | Human language                                     |
| Text             | Written language data                              |
| Corpus           | Collection of texts                                |
| Vocabulary       | Unique words/tokens                                |
| Token            | Processed text unit                                |
| Morphology       | Word structure                                     |
| Syntax           | Sentence structure                                 |
| Semantics        | Meaning                                            |
| Pragmatics       | Contextual meaning                                 |
| Discourse        | Relationship across sentences                      |
| Classification   | Assigning category                                 |
| Sentiment        | Positive/negative/neutral feeling                  |
| NER              | Named Entity Recognition                           |
| POS              | Part of Speech                                     |
| Embedding        | Numeric representation                             |
| Language Model   | Model that learns language patterns                |
| Transformer      | Modern neural architecture for sequence/text tasks |

---

# 🧪 Practice — M02.01

## Practice 1

নিচের sentence-এর:

* characters
* words
* sentence
* vocabulary

identify করো:

```text
Python is easy to learn.
```

---

## Practice 2

নিচের কোনগুলো NLP task?

```text
1. Sentiment Analysis
2. Image Classification
3. Named Entity Recognition
4. Machine Translation
5. Text Summarization
6. Text Classification
```

---

## Practice 3

এই sentence-এ ambiguity কোথায়?

```text
I saw the man with a telescope.
```

দুটি possible meaning লেখো।

---

## Practice 4

নিচের sentence-এ identify করো:

```text
Atiar bought a laptop from Dhaka.
```

* Person
* Location
* Object

---

# 🧠 Theory Questions

নিজে উত্তর দেওয়ার চেষ্টা করবে:

### Q1.

NLP কী?

### Q2.

Natural Language এবং Programming Language-এর মধ্যে পার্থক্য কী?

### Q3.

NLP কেন challenging?

### Q4.

Morphology কী?

### Q5.

Syntax কী?

### Q6.

Semantics কী?

### Q7.

Pragmatics কী?

### Q8.

NLP এবং Machine Learning-এর relationship কী?

### Q9.

Traditional Rule-Based NLP-এর সমস্যা কী?

### Q10.

Transformer কেন modern NLP-তে গুরুত্বপূর্ণ?

---

# 🎯 Interview Questions

### Beginner

1. What is NLP?
2. What are the applications of NLP?
3. What is tokenization?
4. What is stemming?
5. What is lemmatization?
6. What is POS tagging?
7. What is NER?
8. What is sentiment analysis?

### Intermediate

9. Why is NLP difficult?
10. What is ambiguity in NLP?
11. What is semantic similarity?
12. What is a corpus?
13. What is a vocabulary?
14. What is an embedding?
15. What is a language model?

### Advanced Foundation

16. Why did NLP move from rule-based systems to statistical methods?
17. Why are contextual representations important?
18. Why were RNN/LSTM systems eventually complemented by Transformers?
19. What is the difference between traditional NLP features and embeddings?
20. What is the basic idea behind self-attention?

---

# 💻 Mini Python Practice

এখন library ছাড়াই basic text processing করো:

```python
text = "Python is easy to learn."

words = text.split()

print("Text:", text)
print("Words:", words)
print("Word count:", len(words))
print("Character count:", len(text))
```

তারপর:

```python
unique_words = set(words)

print("Vocabulary:", unique_words)
print("Vocabulary size:", len(unique_words))
```

এখানে তুমি ইতিমধ্যে NLP-এর কয়েকটি basic concept ব্যবহার করছ:

```text
Text
 ↓
Tokenization
 ↓
Vocabulary
 ↓
Statistics
```

---

# 🔥 Mini Challenge

এই text নিয়ে কাজ করো:

```python
text = """
Python is powerful.
Python is easy to learn.
NLP is interesting.
I am learning NLP with Python.
"""
```

তোমার program-এর কাজ:

```text
1. Sentence count
2. Word count
3. Unique word count
4. Most frequent word
5. Average word length
```

**এখনো NLTK/spaCy ব্যবহার করবে না।**
কারণ আমরা প্রথমে concept বুঝে তারপর library ব্যবহার করব।

---

# ✅ M02.01 Completion Checklist

আজকের lesson complete হবে যদি তুমি explain করতে পারো:

* [ ] NLP কী
* [ ] Natural Language কী
* [ ] NLP কেন প্রয়োজন
* [ ] NLP-এর major applications
* [ ] Text Classification
* [ ] Sentiment Analysis
* [ ] NER
* [ ] POS Tagging
* [ ] Machine Translation
* [ ] Summarization
* [ ] Question Answering
* [ ] Text Generation
* [ ] Text Similarity
* [ ] Morphology
* [ ] Syntax
* [ ] Semantics
* [ ] Pragmatics
* [ ] Discourse
* [ ] Ambiguity
* [ ] Context
* [ ] Rule-Based NLP
* [ ] Statistical NLP
* [ ] ML-based NLP
* [ ] Deep Learning NLP
* [ ] Transformer-এর basic idea
* [ ] NLP বনাম ML বনাম DL
* [ ] NLP pipeline

### ⭐ আজকের মূল takeaway

```text
NLP
=
Human Language
+
Linguistics
+
Computer Science
+
Machine Learning / Deep Learning
```

আর modern NLP-এর journey:

```text
Rules
 ↓
Statistics
 ↓
Machine Learning
 ↓
Deep Learning
 ↓
Embeddings
 ↓
RNN/LSTM
 ↓
Attention
 ↓
Transformer
 ↓
BERT/GPT
 ↓
LLM
```

**M02.01 এখানেই complete।**
পরের lesson হবে **M02.02 — Text & Language Fundamentals**, যেখানে আমরা **Character → Word → Token → Sentence → Paragraph → Document → Corpus → Vocabulary → Lexicon → Morphology → Syntax → Semantics → Pragmatics → Context** একদম গভীরভাবে শিখব।


---
# 🧠 M02.02 — Text & Language Fundamentals

আজ আমরা NLP-এর **সবচেয়ে basic কিন্তু সবচেয়ে গুরুত্বপূর্ণ foundation** শিখব।

M02.01-এ আমরা জেনেছি NLP কী। এখন বুঝব:

```text
Character
   ↓
Word
   ↓
Token
   ↓
Sentence
   ↓
Paragraph
   ↓
Document
   ↓
Corpus
   ↓
Vocabulary / Lexicon
```

এর পাশাপাশি:

```text
Morphology
Syntax
Semantics
Pragmatics
Context
Discourse
```

এই concepts পরিষ্কার না হলে পরে **Tokenization, Embedding, Transformer, BERT, GPT** বুঝতে সমস্যা হবে।

---

# 1. Text কী?

সহজভাবে, **Text হলো language-এর লিখিত representation**।

উদাহরণ:

```text
Python is a programming language.
```

এটি একটি text।

Text হতে পারে:

```text
Email
Message
Book
Article
Review
Comment
News
Social media post
Chat
Question
```

NLP-এর input হিসেবে আমরা সাধারণত text পাই।

```text
User
 ↓
"I want to learn NLP"
 ↓
NLP System
```

---

# 2. Character কী?

**Character** হলো text-এর সবচেয়ে ছোট মৌলিক unit-গুলোর একটি।

উদাহরণ:

```text
Python
```

Characters:

```text
P
y
t
h
o
n
```

অর্থাৎ:

```text
"Python"
```

এর length:

```python
text = "Python"

print(len(text))
```

Output:

```text
6
```

কারণ:

```text
P y t h o n
1 2 3 4 5 6
```

---

# 3. Character শুধু Letter নয়

Character বলতে শুধু alphabet বোঝায় না।

উদাহরণ:

```text
A
1
!
?
.
,
@
space
```

সবই character হিসেবে text representation-এর অংশ হতে পারে।

Example:

```text
"Hello!"
```

Characters:

```text
H
e
l
l
o
!
```

---

# 4. Space কি Character?

হ্যাঁ।

Python:

```python
text = "Hello World"

print(len(text))
```

Output:

```text
11
```

কারণ:

```text
Hello → 5
space → 1
World → 5

Total → 11
```

NLP preprocessing-এর সময় whitespace খুব গুরুত্বপূর্ণ।

---

# 5. Character-level NLP

আমরা যদি text-কে character দিয়ে process করি:

```text
"hello"
```

তাহলে:

```text
h
e
l
l
o
```

এটাকে বলা যায় **character-level representation**।

এটি কাজে লাগে:

* spelling correction
* typo handling
* noisy text
* OCR errors
* unknown words
* morphological analysis
* multilingual text
* character-level language modeling

---

# 6. Word কী?

একটি language-এর অর্থবহ lexical unit হলো সাধারণভাবে **word**।

Example:

```text
I love Python.
```

Words:

```text
I
love
Python
```

Python-এর মাধ্যমে:

```python
text = "I love Python."

words = text.split()

print(words)
```

Output:

```text
['I', 'love', 'Python.']
```

কিন্তু এখানে একটি গুরুত্বপূর্ণ সমস্যা আছে।

`Python.`-এর সাথে punctuation যুক্ত হয়েছে।

তাই:

```text
Python.
```

সবসময় একটি clean word হিসেবে ধরা ঠিক নয়।

এই সমস্যা আমরা পরে **Tokenization** lesson-এ বিস্তারিত করব।

---

# 7. Word এবং Character-এর Relationship

ধরো:

```text
Python
```

তাহলে:

```text
Character
   ↓
P
y
t
h
o
n

Word
   ↓
Python
```

অর্থাৎ:

```text
Multiple Characters
        ↓
       Word
```

---

# 8. Token কী?

এটা খুব গুরুত্বপূর্ণ।

**Token হলো NLP system যেভাবে text-কে processing unit-এ ভাগ করে।**

Token হতে পারে:

* word
* punctuation
* subword
* character
* special token

উদাহরণ:

```text
I love Python.
```

একটি tokenizer করতে পারে:

```text
["I", "love", "Python", "."]
```

এখানে:

```text
I       → token
love    → token
Python  → token
.       → token
```

---

# 9. Word ≠ Token সবসময়

এটা ভালোভাবে মনে রাখবে।

Traditional NLP-তে:

```text
Word ≈ Token
```

কিন্তু modern NLP/LLM-এ:

```text
Token ≠ necessarily Word
```

উদাহরণ:

```text
unhappiness
```

Subword tokenizer এটাকে এমনভাবে ভাগ করতে পারে:

```text
un
happi
ness
```

অথবা model-specific অন্য segmentation হতে পারে।

তাই:

> **Token হলো model-এর processing unit; এটি সবসময় একটি complete word নয়।**

---

# 10. Tokenization কেন দরকার?

Computer সরাসরি:

```text
"I love NLP."
```

এর semantic meaning process করে না।

প্রথমে text-কে processing units-এ ভাগ করা হয়:

```text
"I love NLP."
      ↓
Tokenization
      ↓
["I", "love", "NLP", "."]
```

তারপর:

```text
Tokens
 ↓
Token IDs
 ↓
Embeddings
 ↓
Model
```

এটাই modern NLP pipeline-এর foundation।

---

# 11. Sentence কী?

**Sentence হলো একটি grammatical/semantic unit যা সাধারণত একটি complete thought প্রকাশ করে।**

Example:

```text
I am learning NLP.
```

এটি একটি sentence।

দুটি sentence:

```text
I am learning NLP.
Python is interesting.
```

---

# 12. Sentence Boundary

Sentence কোথায় শেষ হয়েছে সেটা detect করা NLP-এর একটি গুরুত্বপূর্ণ task।

সাধারণত:

```text
.
?
!
```

sentence boundary নির্দেশ করতে পারে।

কিন্তু সবসময় নয়।

Example:

```text
Dr. Rahman lives in Dhaka.
```

এখানে:

```text
Dr.
```

এর `.` sentence ending নয়।

তাই শুধু:

```python
text.split(".")
```

দিয়ে sentence segmentation সবসময় সঠিক হবে না।

---

# 13. Paragraph কী?

এক বা একাধিক related sentence মিলে paragraph তৈরি করে।

Example:

```text
Python is a programming language.
It is easy to learn.
It is widely used in AI.
```

এটি একটি paragraph।

Structure:

```text
Paragraph
 ├── Sentence 1
 ├── Sentence 2
 └── Sentence 3
```

---

# 14. Document কী?

একটি complete text resource হলো document।

উদাহরণ:

```text
Article
```

একটি article-এর মধ্যে:

```text
Document
 ├── Paragraph
 │    ├── Sentence
 │    ├── Sentence
 │    └── Sentence
 │
 ├── Paragraph
 │    ├── Sentence
 │    └── Sentence
 │
 └── Paragraph
```

Document হতে পারে:

* PDF
* Article
* Book
* Email
* Report
* Research paper
* Web page

---

# 15. Corpus কী?

এটা খুব গুরুত্বপূর্ণ।

**Corpus = অনেকগুলো text/document-এর collection।**

একটি document:

```text
Document 1
```

আর অনেকগুলো document:

```text
Document 1
Document 2
Document 3
Document 4
...
Document N
```

সবগুলো মিলে:

```text
Corpus
```

---

# 16. Corpus-এর Example

ধরো তুমি sentiment analysis model বানাচ্ছ।

তোমার dataset:

```text
"I love this phone."
"This product is amazing."
"I hate this service."
"This is terrible."
```

এই collection-টাই একটি corpus হিসেবে কাজ করতে পারে।

Structure:

```text
Corpus
│
├── Document 1
├── Document 2
├── Document 3
└── Document 4
```

---

# 17. Corpus বনাম Dataset

দুটো related হলেও এক জিনিস নয়।

### Corpus

মূলত language/text collection।

```text
Many Texts
 ↓
Corpus
```

### Dataset

Machine learning-এর জন্য structured data।

Example:

```text
text                         label

"I love this"                positive
"I hate this"                negative
```

এটা ML dataset।

একটি NLP dataset-এর text অংশ একটি corpus-এর মতো কাজ করতে পারে।

---

# 18. Vocabulary কী?

**Vocabulary হলো কোনো corpus/document-এ ব্যবহৃত unique tokens/words-এর collection।**

Example:

```text
I love Python.
I love NLP.
```

Tokens:

```text
I
love
Python
I
love
NLP
```

Unique vocabulary:

```text
I
love
Python
NLP
```

Python:

```python
text = "I love Python. I love NLP."

words = text.replace(".", "").split()

vocabulary = set(words)

print(vocabulary)
```

---

# 19. Vocabulary Size

উপরের example-এ:

```text
I
love
Python
NLP
```

Total:

```text
4
```

অর্থাৎ:

```text
Vocabulary Size = 4
```

ML/NLP-তে vocabulary size অত্যন্ত গুরুত্বপূর্ণ।

কারণ বড় vocabulary মানে:

* বেশি memory
* বড় embedding matrix
* বেশি token IDs
* computational cost বৃদ্ধি

---

# 20. Vocabulary বনাম Word Frequency

এখানে পার্থক্য:

Text:

```text
I love Python.
I love Python.
I love NLP.
```

Word frequency:

```text
I       → 3
love    → 3
Python  → 2
NLP     → 1
```

কিন্তু vocabulary:

```text
I
love
Python
NLP
```

Vocabulary size:

```text
4
```

অর্থাৎ:

> **Frequency বলে কতবার এসেছে, vocabulary বলে কতগুলো unique word/token আছে।**

---

# 21. Lexicon কী?

**Lexicon** হলো language-এর words এবং তাদের linguistic information-এর collection।

একটি lexicon-এ থাকতে পারে:

```text
Word
Meaning
Part of Speech
Morphological information
Pronunciation
Other linguistic properties
```

উদাহরণ conceptually:

```text
run
 ├── Verb
 ├── Noun
 ├── meanings
 └── grammatical information
```

---

# 22. Vocabulary বনাম Lexicon

সহজভাবে:

### Vocabulary

```text
কোন কোন word/token আছে?
```

### Lexicon

```text
এই word সম্পর্কে linguistic information কী?
```

তাই:

```text
Vocabulary → list/collection of terms
Lexicon    → terms + linguistic information
```

---

# 23. Morphology কী?

**Morphology হলো word কীভাবে তৈরি হয় এবং word-এর internal structure কী—তার study।**

Example:

```text
unhappiness
```

ভাঙলে:

```text
un + happy + ness
```

এখানে:

```text
un    → prefix
happy → root/base
ness  → suffix
```

---

# 24. Morpheme কী?

**Morpheme হলো meaning বহনকারী smallest linguistic unit।**

Example:

```text
unhappy
```

ভাঙলে:

```text
un + happy
```

দুটিই meaning contribute করছে।

আর:

```text
cats
```

ভাঙলে:

```text
cat + s
```

এখানে:

```text
cat → animal
s   → plural
```

---

# 25. Free Morpheme

যে morpheme একা word হিসেবে থাকতে পারে।

Example:

```text
cat
book
happy
```

---

# 26. Bound Morpheme

যে morpheme একা সাধারণত word হিসেবে ব্যবহার করা যায় না।

Example:

```text
un-
-re
-s
-ed
-ness
```

যেমন:

```text
un + happy
```

`un` একা সাধারণ word নয়।

---

# 27. Prefix

Word-এর শুরুতে যুক্ত হয়।

```text
un + happy
re + write
```

Examples:

```text
unhappy
rewrite
```

---

# 28. Suffix

Word-এর শেষে যুক্ত হয়।

```text
happy + ness
teach + er
play + ing
```

Examples:

```text
happiness
teacher
playing
```

---

# 29. Stemming-এর সাথে Morphology-এর Connection

আগের lesson-এ আমরা stemming-এর কথা বলেছি।

ধরো:

```text
playing
played
plays
player
```

এগুলো related forms।

Morphology বুঝলে আমরা বুঝতে পারি word forms কীভাবে পরিবর্তিত হচ্ছে।

পরে:

```text
Stemming
Lemmatization
```

এগুলো বিস্তারিত করব।

---

# 30. Syntax কী?

**Syntax হলো sentence-এর structure এবং words-এর grammatical relationship-এর study।**

Example:

```text
Atiar reads a book.
```

Conceptually:

```text
Subject → Atiar
Verb    → reads
Object  → a book
```

---

# 31. Word Order

Syntax-এর কারণে word order গুরুত্বপূর্ণ।

```text
The cat chased the mouse.
```

এবং:

```text
The mouse chased the cat.
```

দুটো sentence-এর words একই।

কিন্তু meaning আলাদা।

কারণ:

```text
word relationship + structure
```

পরিবর্তন হয়েছে।

---

# 32. Syntax Tree — Basic Idea

Sentence:

```text
Atiar reads books.
```

Conceptually:

```text
Sentence
│
├── Noun Phrase
│      └── Atiar
│
└── Verb Phrase
       ├── reads
       └── books
```

এটাই পরে parsing বুঝতে সাহায্য করবে।

---

# 33. Semantics কী?

**Semantics হলো meaning-এর study।**

Example:

```text
The dog chased the cat.
```

Semantic interpretation:

```text
Agent  → dog
Action → chased
Object → cat
```

অর্থাৎ sentence কী meaning প্রকাশ করছে সেটা semantics-এর বিষয়।

---

# 34. Syntax বনাম Semantics

খুব গুরুত্বপূর্ণ difference:

### Syntax

```text
Sentence structure কী?
```

### Semantics

```text
Sentence-এর meaning কী?
```

Example:

```text
Colorless green ideas sleep furiously.
```

Grammar structure কিছুটা valid হতে পারে, কিন্তু semantic meaning অদ্ভুত।

এখানে দেখা যাচ্ছে:

```text
Syntax ≠ Semantics
```

---

# 35. Pragmatics কী?

Pragmatics হলো **context অনুযায়ী intended meaning** বোঝা।

Example:

```text
Can you open the door?
```

Literal meaning:

> তুমি কি দরজা খুলতে সক্ষম?

কিন্তু বাস্তব conversational meaning:

> দরজাটা খুলে দাও।

এটাই pragmatics।

---

# 36. Semantics বনাম Pragmatics

### Semantics

Sentence-এর literal/conventional meaning।

### Pragmatics

Context অনুযায়ী speaker কী বোঝাতে চেয়েছে।

```text
Sentence
   │
   ├── Literal Meaning → Semantics
   │
   └── Intended Meaning → Pragmatics
```

---

# 37. Context কী?

**Context হলো text-এর আশেপাশের information যা meaning বুঝতে সাহায্য করে।**

Example:

```text
I went to the bank.
```

`bank` কী?

Financial institution?

নাকি river bank?

Context দরকার।

```text
I deposited money at the bank.
```

→ financial bank

অন্যদিকে:

```text
I sat near the bank of the river.
```

→ river bank

---

# 38. Local Context

একটি word-এর কাছাকাছি words।

Example:

```text
machine learning model
```

`model`-এর local context:

```text
machine
learning
```

---

# 39. Sentence Context

পুরো sentence:

```text
The bank approved my loan.
```

এখানে bank-এর meaning বোঝা সহজ।

---

# 40. Document Context

একটি document-এর আগের/পরের অনেক sentence-ও context হতে পারে।

Example:

```text
Atiar bought a laptop yesterday.
He uses it every day.
```

এখানে:

```text
He → Atiar
it → laptop
```

এগুলো document context-এর মাধ্যমে বোঝা যায়।

---

# 41. Discourse কী?

একাধিক sentence কীভাবে একে অপরের সাথে connected—এটা discourse-এর বিষয়।

Example:

```text
Atiar bought a laptop.
He needed it for programming.
The device has 16GB RAM.
```

এখানে sentenceগুলোর মধ্যে relationship আছে।

```text
Sentence 1
    ↓
Sentence 2
    ↓
Sentence 3
```

---

# 42. Coreference

Discourse-এর একটি গুরুত্বপূর্ণ concept হলো **coreference**।

Example:

```text
Atiar bought a laptop.
He uses it every day.
```

এখানে:

```text
He → Atiar
it → laptop
```

এগুলো একই entity-কে refer করছে।

---

# 43. Anaphora

একটি pronoun বা expression আগের entity-কে refer করে।

```text
Atiar went home.
He was tired.
```

`He` → Atiar

এটা NLP-তে খুব গুরুত্বপূর্ণ problem।

---

# 44. Entity কী?

Entity হলো text-এর মধ্যে কোনো identifiable person/place/organization/object/concept।

Example:

```text
Google is based in California.
```

Potential entities:

```text
Google     → Organization
California → Location
```

NER lesson-এ পরে এগুলো গভীরভাবে করব।

---

# 45. Text Hierarchy

আজকের পুরো lesson-কে একটি hierarchy হিসেবে দেখো:

```text
Character
    ↓
Word / Subword
    ↓
Token
    ↓
Sentence
    ↓
Paragraph
    ↓
Document
    ↓
Corpus
```

আর language understanding-এর দিক থেকে:

```text
Morphology
    ↓
Syntax
    ↓
Semantics
    ↓
Pragmatics
    ↓
Discourse / Context
```

---

# 46. একটি Complete Example

এই text নাও:

```text
Atiar is learning NLP.
He enjoys working with text.
```

### Character

```text
A
t
i
a
r
...
```

### Words

```text
Atiar
is
learning
NLP
He
enjoys
working
with
text
```

### Tokens

Tokenizer অনুযায়ী:

```text
["Atiar", "is", "learning", "NLP", ".", "He", ...]
```

### Sentences

```text
Sentence 1:
Atiar is learning NLP.

Sentence 2:
He enjoys working with text.
```

### Paragraph

দুটি sentence একত্রে একটি paragraph হতে পারে।

### Document

একটি article/report হলে পুরো content document।

### Corpus

এ ধরনের হাজার document একত্রে:

```text
NLP Corpus
```

### Vocabulary

Unique tokens:

```text
Atiar
is
learning
NLP
He
enjoys
working
with
text
```

### Discourse

```text
He → Atiar
```

### Semantics

```text
Atiar
 ↓
learning
 ↓
NLP
```

### Context

দ্বিতীয় sentence-এর `He` প্রথম sentence-এর context থেকে বোঝা যায়।

---

# 47. NLP-তে এগুলো কেন এত গুরুত্বপূর্ণ?

কারণ modern NLP model-এর পুরো process এই concepts-এর ওপর দাঁড়ানো।

```text
Raw Text
   ↓
Characters
   ↓
Tokens
   ↓
Token IDs
   ↓
Vectors
   ↓
Context
   ↓
Semantic Representation
   ↓
Model
```

আর model-এর language understanding-এর জন্য:

```text
Word Structure
      ↓
Syntax
      ↓
Semantics
      ↓
Context
      ↓
Meaning
```

---

# 48. AI Writing System-এ এগুলোর ব্যবহার

তোমার future AI Writing Assistant-এর কথা ধরো।

Input:

```text
"Atiar is a very good developer. He writes clean code."
```

System-এর দরকার হতে পারে:

### Tokenization

```text
Atiar
is
a
very
good
developer
...
```

### Sentence segmentation

```text
Sentence 1
Sentence 2
```

### POS

```text
good → adjective
developer → noun
```

### NER

```text
Atiar → PERSON
```

### Coreference

```text
He → Atiar
```

### Semantics

```text
Atiar → developer
Atiar → writes code
```

### Context

দ্বিতীয় sentence-এর `He` প্রথম sentence থেকে বুঝতে হবে।

এগুলো ছাড়া advanced writing analysis system তৈরি করা কঠিন।

---

# 49. Important Difference Table

| Concept    | কী বোঝায়                              |
| ---------- | ------------------------------------- |
| Character  | Text-এর individual symbol             |
| Word       | Language-এর lexical unit              |
| Token      | NLP processing unit                   |
| Sentence   | Complete linguistic unit              |
| Paragraph  | Related sentences                     |
| Document   | Complete text resource                |
| Corpus     | Collection of documents/texts         |
| Vocabulary | Unique words/tokens                   |
| Lexicon    | Words + linguistic information        |
| Morphology | Word structure                        |
| Morpheme   | Meaningful smallest linguistic unit   |
| Syntax     | Sentence structure                    |
| Semantics  | Meaning                               |
| Pragmatics | Contextual/intended meaning           |
| Discourse  | Relationship across sentences         |
| Context    | Meaning বুঝতে surrounding information |

---

# 🧪 Practical Python

এখন আমরা basic text hierarchy নিজের হাতে দেখি।

```python
text = "Python is powerful. Python is easy to learn."

print("Text:")
print(text)

sentences = text.split(".")

print("\nSentences:")
for sentence in sentences:
    sentence = sentence.strip()

    if sentence:
        print(sentence)

words = text.replace(".", "").split()

print("\nWords:")
print(words)

vocabulary = set(words)

print("\nVocabulary:")
print(vocabulary)

print("\nVocabulary size:")
print(len(vocabulary))
```

---

# 🧪 Practice 1 — Character

```python
text = "NLP is amazing"
```

Find:

* total characters
* total spaces
* total letters

Hint:

```python
for char in text:
    print(char)
```

---

# 🧪 Practice 2 — Word Frequency

এই text:

```text
Python is easy.
Python is powerful.
I love Python.
```

Expected concept:

```text
Python → 3
is     → 2
easy   → 1
powerful → 1
I      → 1
love   → 1
```

নিজে Python দিয়ে বের করার চেষ্টা করো।

---

# 🧪 Practice 3 — Vocabulary

এই text:

```text
AI is powerful.
AI is useful.
Python is powerful.
```

বের করো:

```text
Total words
Unique words
Vocabulary size
```

---

# 🧪 Practice 4 — Sentence

এই text-এর sentence count বের করো:

```text
Python is easy to learn.
NLP is interesting.
Machine learning is powerful.
```

---

# 🧠 Theory Questions

নিজে উত্তর দেওয়ার চেষ্টা করবে:

### Q1.

Character কী?

### Q2.

Word এবং token-এর মধ্যে পার্থক্য কী?

### Q3.

Modern NLP-তে token সবসময় word হয় না কেন?

### Q4.

Corpus কী?

### Q5.

Vocabulary কী?

### Q6.

Vocabulary এবং lexicon-এর পার্থক্য কী?

### Q7.

Morphology কী?

### Q8.

Morpheme কী?

### Q9.

Syntax কী?

### Q10.

Semantics কী?

### Q11.

Syntax এবং semantics-এর difference কী?

### Q12.

Pragmatics কী?

### Q13.

Context NLP-তে কেন গুরুত্বপূর্ণ?

### Q14.

Discourse কী?

### Q15.

Coreference কী?

---

# 🎯 Interview Questions

### Beginner

1. What is a character in NLP?
2. What is a word?
3. What is a token?
4. What is a sentence?
5. What is a corpus?
6. What is vocabulary?

### Intermediate

7. What is the difference between a word and a token?
8. What is the difference between vocabulary and lexicon?
9. What is morphology?
10. What is syntax?
11. What is semantics?
12. What is pragmatics?
13. What is discourse?
14. What is context in NLP?

### Advanced Foundation

15. Why is context important for word meaning?
16. Why can the same word have multiple meanings?
17. Why isn't sentence splitting using `.` always reliable?
18. Why do modern NLP models use subword tokens?
19. What is coreference resolution?
20. How are syntax, semantics and pragmatics related?

---

# 🔥 Mini Challenge

এই paragraph:

```text
Python is a popular programming language.
It is widely used in artificial intelligence.
Many developers use Python for NLP.
```

তোমার program-কে নিচের information দিতে হবে:

```text
1. Character count
2. Sentence count
3. Word count
4. Unique word count
5. Vocabulary
6. Most frequent word
7. Average word length
```

**Restriction:** এখনো `NLTK`, `spaCy` ব্যবহার করবে না।

কারণ আমাদের লক্ষ্য হচ্ছে আগে **concept নিজে implement করা**, তারপর library দিয়ে professional implementation শেখা।

---

# ✅ M02.02 Completion Checklist

Lesson complete করার আগে নিশ্চিত হও:

* [ ] Character
* [ ] Character-level processing
* [ ] Word
* [ ] Token
* [ ] Word vs Token
* [ ] Sentence
* [ ] Sentence boundary
* [ ] Paragraph
* [ ] Document
* [ ] Corpus
* [ ] Corpus vs Dataset
* [ ] Vocabulary
* [ ] Vocabulary size
* [ ] Word frequency
* [ ] Lexicon
* [ ] Vocabulary vs Lexicon
* [ ] Morphology
* [ ] Morpheme
* [ ] Free morpheme
* [ ] Bound morpheme
* [ ] Prefix
* [ ] Suffix
* [ ] Syntax
* [ ] Syntax structure
* [ ] Semantics
* [ ] Syntax vs Semantics
* [ ] Pragmatics
* [ ] Semantics vs Pragmatics
* [ ] Context
* [ ] Local context
* [ ] Sentence context
* [ ] Document context
* [ ] Discourse
* [ ] Coreference
* [ ] Anaphora
* [ ] Entity
* [ ] NLP text hierarchy

---

## ⭐ আজকের সবচেয়ে গুরুত্বপূর্ণ Mental Model

```text
                 TEXT
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
    Structure            Meaning
        │                   │
        ↓                   ↓
Character               Semantics
Word                    Pragmatics
Token                   Context
Sentence                Discourse
Paragraph
Document
Corpus
```

আর পুরো NLP-এর foundation:

```text
Character
    ↓
Word / Subword
    ↓
Token
    ↓
Sentence
    ↓
Document
    ↓
Corpus
    ↓
Representation
    ↓
Model
    ↓
Understanding / Prediction / Generation
```

**M02.02 complete।**
পরবর্তী lesson: **M02.03 — NLP Pipeline**, যেখানে আমরা একটি raw text কীভাবে step-by-step **Cleaning → Normalization → Tokenization → Linguistic Processing → Feature Extraction → Representation → Model → Prediction → Evaluation**-এর মধ্য দিয়ে যায়, সেটা হাতে-কলমে একটি complete pipeline বানিয়ে শিখব।


---
# 🧠 M02.03 — NLP Pipeline

এখন আমরা NLP-এর একটি **complete end-to-end pipeline** বুঝব।

M02.01-এ শিখেছি **NLP কী**।  
M02.02-এ শিখেছি **Character → Word → Token → Sentence → Document → Corpus** এবং **Morphology → Syntax → Semantics → Pragmatics → Context**।

আজ এগুলোকে একসাথে নিয়ে দেখব:

```text
Raw Text
   ↓
Cleaning
   ↓
Normalization
   ↓
Sentence Segmentation
   ↓
Tokenization
   ↓
Stopword Handling
   ↓
Stemming / Lemmatization
   ↓
Linguistic Analysis
   ↓
Feature Extraction
   ↓
Numerical Representation
   ↓
NLP Model
   ↓
Prediction / Generation
   ↓
Evaluation
```

এটা Phase 2-এর **সবচেয়ে গুরুত্বপূর্ণ mental models**-এর একটি।

---

# 1. NLP Pipeline কী?

**NLP Pipeline** হলো raw human language-কে ধাপে ধাপে process করে machine-readable representation এবং শেষ পর্যন্ত useful output তৈরি করার workflow।

সহজভাবে:

```text
Human Text
    ↓
Process
    ↓
Understand / Analyze
    ↓
Result
```

Example:

```text
"I really love this product!"
```

System চাইলে:

```text
Raw Text
   ↓
Clean
   ↓
Tokenize
   ↓
Analyze
   ↓
Extract Features
   ↓
Model
   ↓
Positive Sentiment
```

---

# 2. কেন Pipeline দরকার?

একটি model-কে সরাসরি raw text দিলে সবসময় ভালো ফল পাওয়া যায় না।

ধরো:

```text
"   I LOVE this product!!! 😍   "
```

এখানে আছে:

- extra spaces
    
- uppercase
    
- punctuation
    
- emoji
    

আমাদের task অনুযায়ী এগুলো handle করতে হতে পারে।

তাই:

```text
Raw Text
   ↓
Preprocessing
   ↓
Representation
   ↓
Model
```

---

# 3. Complete NLP Pipeline

আমাদের pipeline:

```text
                    RAW TEXT
                       │
                       ↓
                  CLEANING
                       │
                       ↓
                 NORMALIZATION
                       │
                       ↓
              SENTENCE SEGMENTATION
                       │
                       ↓
                 TOKENIZATION
                       │
                       ↓
              STOPWORD HANDLING
                       │
                       ↓
            STEMMING / LEMMATIZATION
                       │
                       ↓
             LINGUISTIC ANALYSIS
                       │
                       ↓
              FEATURE EXTRACTION
                       │
                       ↓
             NUMERICAL REPRESENTATION
                       │
                       ↓
                   NLP MODEL
                       │
                       ↓
              PREDICTION / GENERATION
                       │
                       ↓
                  EVALUATION
```

তবে **সব NLP project-এ প্রতিটি ধাপ mandatory নয়**।

এটা খুব গুরুত্বপূর্ণ।

---

# 4. Stage 1 — Raw Text

সবকিছু শুরু হয় raw text থেকে।

Example:

```python
text = "   I LOVE Python!!! I am learning NLP.   "
```

এটাই আমাদের input।

Raw text হতে পারে:

```text
User input
Email
PDF
Web page
CSV
Database
Chat
Social media
News article
```

---

# 5. Stage 2 — Text Cleaning

এখানে unwanted content remove/handle করা হয়।

Example:

```text
"   I LOVE Python!!!   "
```

Cleaning:

```text
"I LOVE Python!!!"
```

Possible cleaning:

- extra spaces
    
- HTML tags
    
- unwanted URLs
    
- unwanted symbols
    
- duplicate content
    
- malformed text
    
- unnecessary characters
    

---

# 6. Basic Cleaning Example

```python
text = "   I LOVE Python!!!   "

text = text.strip()

print(text)
```

Output:

```text
I LOVE Python!!!
```

`strip()` শুরু এবং শেষের whitespace remove করে।

---

# 7. Multiple Spaces

Input:

```text
I    love     Python.
```

Normalize:

```text
I love Python.
```

Python:

```python
import re

text = "I    love     Python."

text = re.sub(r"\s+", " ", text)

print(text)
```

Output:

```text
I love Python.
```

---

# 8. HTML Cleaning

Web থেকে text সংগ্রহ করলে:

```html
<p>I love Python.</p>
```

আমাদের দরকার হতে পারে:

```text
I love Python.
```

HTML remove করার জন্য task অনুযায়ী HTML parser বা carefully designed rules ব্যবহার করা যায়।

**Important:** সবসময় শুধু regex দিয়ে complex HTML parse করা ভালো practice নয়।

---

# 9. URL Handling

Input:

```text
Visit https://example.com for more information.
```

Task অনুযায়ী:

```text
Visit [URL] for more information.
```

অথবা URL সম্পূর্ণ remove করা হতে পারে।

কিন্তু decisionটা **task-dependent**।

যেমন:

### Spam Detection

URL গুরুত্বপূর্ণ feature হতে পারে।

### Sentiment Analysis

URL হয়তো দরকার নেই।

তাই:

> Cleaning is task-dependent.

---

# 10. Emoji Handling

Input:

```text
I love this 😍
```

Sentiment analysis-এর ক্ষেত্রে:

```text
😍
```

খুব useful signal হতে পারে।

তাই emoji blindly remove করা উচিত নয়।

এটা NLP-এর একটি গুরুত্বপূর্ণ principle:

> **Preprocessing should preserve information that is useful for the task.**

---

# 11. Stage 3 — Normalization

Cleaning এবং normalization কাছাকাছি হলেও একই নয়।

### Cleaning

Unwanted/noisy information handle করা।

### Normalization

Text-কে consistent representation-এ আনা।

Example:

```text
HELLO
Hello
hello
```

Normalize:

```text
hello
hello
hello
```

---

# 12. Lowercasing

```python
text = "I LOVE Python"

text = text.lower()

print(text)
```

Output:

```text
i love python
```

কিন্তু এটাও সব task-এ করা উচিত নয়।

Example:

```text
Apple
apple
```

এখানে capitalization meaning/entity identification-এ useful হতে পারে।

NER-এর ক্ষেত্রে original capitalization গুরুত্বপূর্ণ হতে পারে।

---

# 13. Unicode Normalization

Multilingual NLP-তে Unicode খুব গুরুত্বপূর্ণ।

Example:

```text
Bangla
বাংলা
```

একই language-এর text হলেও internal representation-এর বিষয় থাকতে পারে।

Normalization techniques:

- Unicode normalization
    
- whitespace normalization
    
- punctuation normalization
    

এগুলো আমরা M02.14-এ আরও গভীরভাবে করব।

---

# 14. Stage 4 — Sentence Segmentation

Paragraph:

```text
Python is easy to learn. NLP is interesting. I love AI.
```

এটাকে sentence-এ ভাগ করতে হবে:

```text
Sentence 1:
Python is easy to learn.

Sentence 2:
NLP is interesting.

Sentence 3:
I love AI.
```

---

# 15. কেন Sentence Segmentation কঠিন?

শুধু:

```python
text.split(".")
```

সবসময় কাজ করবে না।

Example:

```text
Dr. Rahman lives in Dhaka.
```

এখানে:

```text
Dr.
```

এর `.` sentence ending নয়।

আর:

```text
I scored 3.5 GPA.
```

এখানেও প্রথম `.` sentence boundary নয়।

তাই sophisticated NLP tokenizer ব্যবহার করা হয়।

---

# 16. Stage 5 — Tokenization

Sentence:

```text
I love Python.
```

Tokenization:

```text
["I", "love", "Python", "."]
```

Token হতে পারে:

```text
Word
Subword
Punctuation
Special token
Character
```

---

# 17. Modern NLP Tokenization

Traditional:

```text
"playing"
```

→ one word/token

Modern subword tokenizer:

```text
playing
 ↓
play + ing
```

Actual split model/tokenizer-specific।

এই কারণে:

```text
Word ≠ Token
```

সবসময়।

---

# 18. Token IDs

Modern NLP model সাধারণত text directly process করে না।

Concept:

```text
"I love NLP"
      ↓
Tokenizer
      ↓
["I", "love", "NLP"]
      ↓
Token IDs
      ↓
[101, 2057, 17953, ...]
```

**Note:** actual IDs tokenizer/model অনুযায়ী আলাদা হবে।

---

# 19. Stage 6 — Stopword Handling

Stopwords হলো এমন common words যেগুলো কিছু NLP task-এ কম informative হতে পারে।

Examples:

```text
the
is
a
an
of
to
in
```

Example:

```text
"The cat is on the table."
```

কিছু classical NLP pipeline-এ stopwords remove করলে:

```text
"cat table"
```

হতে পারে।

---

# 20. Stopwords কি সবসময় remove করব?

**না।**

এটা অত্যন্ত গুরুত্বপূর্ণ।

Sentence:

```text
"This is not good."
```

`not` remove করলে:

```text
"This good."
```

Meaning পরিবর্তন হতে পারে।

Sentiment analysis-এ এটা disastrous হতে পারে।

Modern transformer-based models-এর ক্ষেত্রেও classical stopword-removal blindly apply করা সাধারণত ভালো ধারণা নয়।

---

# 21. Stage 7 — Stemming

Words:

```text
playing
played
plays
```

Stemming এগুলোকে approximate root-এ আনতে পারে:

```text
play
```

কিন্তু stemming কখনো incorrect output দিতে পারে।

---

# 22. Stage 8 — Lemmatization

Lemmatization linguistic information ব্যবহার করে base/lemma form বের করার চেষ্টা করে।

Example:

```text
running
ran
runs
```

→

```text
run
```

Stemming বনাম lemmatization আমরা M02.08 এবং M02.09-এ বিস্তারিত করব।

---

# 23. Stage 9 — Linguistic Analysis

এখন text-এর linguistic properties বের করতে পারি।

যেমন:

### POS

```text
Python → NOUN
is → VERB
powerful → ADJECTIVE
```

### NER

```text
Dhaka → LOCATION
Google → ORGANIZATION
```

### Dependency

```text
Subject
Verb
Object
Modifier
```

---

# 24. Example

Sentence:

```text
Atiar works at Google in Dhaka.
```

Possible analysis:

```text
Atiar → PERSON
works → VERB
Google → ORGANIZATION
Dhaka → LOCATION
```

Dependency structure conceptually:

```text
Atiar
   ↓
works
 /    \
Google Dhaka
```

---

# 25. Stage 10 — Feature Extraction

এখানে text-কে এমন features-এ convert করি যা model ব্যবহার করতে পারে।

Classical NLP:

```text
Text
 ↓
Features
```

Features হতে পারে:

- word frequency
    
- n-grams
    
- TF-IDF
    
- sentence length
    
- word length
    
- POS counts
    
- punctuation counts
    

---

# 26. Bag of Words

Example documents:

```text
I love Python.
I love NLP.
```

Vocabulary:

```text
I
love
Python
NLP
```

Document vectors:

```text
I love Python
[1, 1, 1, 0]

I love NLP
[1, 1, 0, 1]
```

এটাই Bag-of-Words-এর basic idea।

---

# 27. TF-IDF

TF-IDF text-এর মধ্যে কোন term relatively informative সেটা measure করতে সাহায্য করে।

Concept:

```text
TF-IDF = TF × IDF
```

এটা classical NLP-এর অত্যন্ত গুরুত্বপূর্ণ representation।

M02.17-এ পুরো mathematical calculation করব।

---

# 28. Stage 11 — Numerical Representation

Computer model numerical data নিয়ে কাজ করে।

তাই:

```text
Text
 ↓
Numerical Representation
```

Traditional:

```text
BoW
TF-IDF
```

Modern:

```text
Word Embedding
Sentence Embedding
Contextual Embedding
```

---

# 29. One-Hot Representation

Example vocabulary:

```text
["cat", "dog", "bird"]
```

Representation:

```text
cat  → [1,0,0]
dog  → [0,1,0]
bird → [0,0,1]
```

Problem:

```text
cat
dog
```

এর semantic similarity এখানে বোঝা যাচ্ছে না।

---

# 30. Dense Embedding

Modern representation:

```text
cat
 ↓
[0.21, -0.34, 0.72, ...]
```

এখানে semantic relationship encode করা যায়।

পরবর্তীতে আমরা শিখব:

- Word2Vec
    
- GloVe
    
- FastText
    
- Sentence embeddings
    
- contextual embeddings
    

---

# 31. Stage 12 — NLP Model

Representation পাওয়ার পরে model ব্যবহার করা যায়।

Classical ML:

```text
TF-IDF
 ↓
Logistic Regression
```

অথবা:

```text
TF-IDF
 ↓
Naive Bayes
```

Deep Learning:

```text
Embedding
 ↓
LSTM
```

Modern:

```text
Token IDs
 ↓
Transformer
```

---

# 32. Stage 13 — Prediction

Task অনুযায়ী output আলাদা হবে।

### Sentiment

```text
Positive
```

### Spam

```text
Spam
```

### Topic

```text
Technology
```

### NER

```text
Dhaka → LOCATION
```

### Generation

```text
Generated text
```

---

# 33. Stage 14 — Post-processing

Model output পাওয়ার পর সেটাকে usable format-এ convert করা হতে পারে।

Example:

Model:

```text
positive: 0.94
negative: 0.06
```

User-facing:

```text
Sentiment: Positive
Confidence: 94%
```

Generation-এর ক্ষেত্রে:

```text
Token IDs
 ↓
Decoded Tokens
 ↓
Text
```

---

# 34. Stage 15 — Evaluation

Model ভালো করছে কি না সেটা measure করতে হবে।

Classification:

```text
Accuracy
Precision
Recall
F1
```

Generation:

```text
BLEU
ROUGE
```

Language modeling:

```text
Perplexity
```

পরে এগুলো আলাদা lessons-এ বিস্তারিত করব।

---

# 35. Complete Classical NLP Pipeline

একটি sentiment classifier:

```text
Raw Text
   ↓
Cleaning
   ↓
Normalization
   ↓
Tokenization
   ↓
Stopword Handling
   ↓
Lemmatization
   ↓
TF-IDF
   ↓
Logistic Regression
   ↓
Prediction
   ↓
Evaluation
```

---

# 36. Complete Modern NLP Pipeline

Transformer-based system:

```text
Raw Text
   ↓
Tokenizer
   ↓
Token IDs
   ↓
Attention Mask
   ↓
Embeddings
   ↓
Transformer
   ↓
Contextual Representation
   ↓
Task Head / Generation
   ↓
Output
```

খেয়াল করো, modern transformer pipeline-এ classical preprocessing-এর অনেকগুলো ধাপ **অবশ্যই করতে হবে এমন নয়**।

---

# 37. Classical বনাম Modern NLP

|Classical NLP|Modern NLP|
|---|---|
|Manual preprocessing|Minimal task-specific preprocessing|
|BoW|Embeddings|
|TF-IDF|Contextual representations|
|Handcrafted features|Learned features|
|Naive Bayes|Transformer|
|SVM|BERT/GPT-like models|
|N-gram LM|Neural language model|
|More manual engineering|More learned representation|

তবে classical NLP এখনও useful।

বিশেষ করে:

- small datasets
    
- interpretable systems
    
- baseline models
    
- search
    
- feature analysis
    
- lightweight systems
    

---

# 38. একটি গুরুত্বপূর্ণ বিষয়: Pipeline Task অনুযায়ী পরিবর্তিত হয়

ধরো তিনটি task:

### Task A — Sentiment Analysis

```text
Text
 ↓
Tokenizer
 ↓
Model
 ↓
Sentiment
```

### Task B — Classical Text Classification

```text
Text
 ↓
Clean
 ↓
Tokenize
 ↓
TF-IDF
 ↓
ML Model
```

### Task C — Modern LLM

```text
Text
 ↓
Tokenizer
 ↓
Transformer
 ↓
Generation
```

তাই:

> **NLP pipeline একটি fixed checklist নয়; task এবং model অনুযায়ী pipeline পরিবর্তিত হয়।**

---

# 39. Data Pipeline বনাম Model Pipeline

এখানে একটি important distinction আছে।

### Data Pipeline

```text
Raw Data
 ↓
Cleaning
 ↓
Validation
 ↓
Preprocessing
 ↓
Dataset
```

### Model Pipeline

```text
Tokens
 ↓
Embeddings
 ↓
Model
 ↓
Prediction
```

Production system-এ দুটো combine হতে পারে:

```text
Data Pipeline
      ↓
Model Pipeline
      ↓
Output
```

---

# 40. Training Pipeline

Training-এর সময়:

```text
Raw Dataset
     ↓
Cleaning
     ↓
Preprocessing
     ↓
Tokenization
     ↓
Representation
     ↓
Train Model
     ↓
Validation
     ↓
Evaluation
     ↓
Saved Model
```

---

# 41. Inference Pipeline

User যখন নতুন text দেয়:

```text
User Text
   ↓
Same Preprocessing
   ↓
Same Tokenizer
   ↓
Same Representation
   ↓
Trained Model
   ↓
Prediction
```

### Important:

Training এবং inference-এর preprocessing mismatch হলে সমস্যা হতে পারে।

---

# 42. Example: Training/Inference Mismatch

Training:

```text
"I LOVE Python"
```

Preprocessed:

```text
"i love python"
```

Inference:

```text
"I LOVE Python"
```

কিন্তু inference-এ যদি preprocessing করা না হয়, representation mismatch হতে পারে—বিশেষত classical pipelines-এ।

তাই:

```text
Training preprocessing
=
Inference preprocessing
```

এই consistency খুব গুরুত্বপূর্ণ।

---

# 43. Data Leakage

Training-এর data থেকে এমন information validation/test-এ accidentally চলে গেলে সেটাকে **data leakage** বলা হয়।

Example:

```text
Entire Dataset
      ↓
Fit TF-IDF
      ↓
Split Train/Test
```

এভাবে করলে test-set vocabulary/statistics training process-এ ঢুকে যেতে পারে।

সঠিক approach সাধারণত:

```text
Dataset
   ↓
Train/Test Split
   ↓
Fit preprocessing on Train
   ↓
Transform Train
   ↓
Transform Test
```

এটা আমরা dataset engineering-এর সময় আরও গভীরভাবে করব।

---

# 44. AI Writing System-এর NLP Pipeline

এখন তোমার future project-এর দিকে আসি।

ধরো user লিখল:

```text
"Artificial intelligence is changing the way people work."
```

একটি writing assistant-এর conceptual pipeline:

```text
                USER TEXT
                    ↓
              Input Validation
                    ↓
              Text Processing
                    ↓
             Sentence Splitting
                    ↓
                Tokenization
                    ↓
           Linguistic Analysis
                    ↓
        ┌───────────┼───────────┐
        ↓           ↓           ↓
      Grammar     Style       Semantics
      Analysis    Analysis    Analysis
        │           │           │
        └───────────┼───────────┘
                    ↓
              AI Model / LLM
                    ↓
              Rewrite / Improve
                    ↓
              Quality Checks
                    ↓
              Final Response
```

এখানে আমাদের Phase 2-এর পরের topics একে একে যুক্ত হবে।

---

# 45. AI Writing Assistant-এর Example

Input:

```text
"AI is very good and it can do many things."
```

System analysis:

```text
Sentence Count → 1
Word Count → 10
POS → ...
Entities → AI
Semantic representation → ...
Style → generic
```

তারপর model একটি improved version দিতে পারে:

```text
"AI is a powerful technology capable of performing a wide range of tasks."
```

এখানে লক্ষ্য হবে **clarity, grammar, style এবং meaning preservation**।

---

# 46. AI Detector/Analyzer-এর ক্ষেত্রে

Text analysis system:

```text
Input Text
    ↓
Sentence Segmentation
    ↓
Tokenization
    ↓
Text Statistics
    ↓
Linguistic Features
    ↓
Embedding
    ↓
Classifier / Analyzer
    ↓
Score / Analysis
```

কিন্তু মনে রাখতে হবে, কোনো detector-এর score-কে absolute proof হিসেবে ধরা ঠিক নয়; statistical/ML detectors ভুল করতে পারে।

---

# 47. Pipeline-এর একটি Real Example

Input:

```text
"   I really LOVE Python!!!   "
```

### Step 1 — Raw

```text
"   I really LOVE Python!!!   "
```

### Step 2 — Cleaning

```text
"I really LOVE Python!!!"
```

### Step 3 — Normalization

Task অনুযায়ী:

```text
"i really love python!!!"
```

### Step 4 — Sentence Segmentation

```text
["i really love python!!!"]
```

### Step 5 — Tokenization

```text
["i", "really", "love", "python", "!", "!", "!"]
```

### Step 6 — Stopword handling

Task-dependent।

### Step 7 — Lemmatization

যদি applicable হয়:

```text
love → love
```

### Step 8 — Features

```text
word count
punctuation count
TF-IDF
...
```

### Step 9 — Representation

```text
Vector
```

### Step 10 — Model

```text
Classifier / Neural Network / Transformer
```

### Step 11 — Output

```text
Positive
```

---

# 48. Python দিয়ে Basic Pipeline

এখন library ছাড়াই ছোট pipeline:

```python
import re

text = "   I LOVE Python!!!   "

# 1. Cleaning
text = text.strip()

# 2. Normalization
text = text.lower()

# 3. Whitespace normalization
text = re.sub(r"\s+", " ", text)

# 4. Basic tokenization
tokens = text.split()

print("Clean text:", text)
print("Tokens:", tokens)
```

Output conceptually:

```text
Clean text: i love python!!!
Tokens: ['i', 'love', 'python!!!']
```

এখানে একটি সমস্যা দেখতে পাচ্ছ?

```text
python!!!
```

punctuation-এর সাথে যুক্ত।

এই সমস্যার proper solution আমরা **M02.05 — Tokenization**-এ বিস্তারিত শিখব।

---

# 49. Pipeline Design Principle

একটি ভালো NLP pipeline-এর কয়েকটি principle:

### 1. Consistency

Training এবং inference একই processing ব্যবহার করবে।

### 2. Reproducibility

একই input → একই preprocessing।

### 3. Modularity

প্রতিটি stage আলাদা component হতে পারে।

```text
clean_text()
tokenize()
extract_features()
predict()
```

### 4. Task Awareness

সব preprocessing সব task-এর জন্য নয়।

### 5. Information Preservation

Useful information accidentally remove করা যাবে না।

---

# 50. Pipeline-কে Code Architecture-এ ভাঙা

Future project-এ:

```text
nlp_project/
│
├── preprocessing/
│   ├── cleaner.py
│   ├── normalizer.py
│   └── tokenizer.py
│
├── features/
│   ├── tfidf.py
│   └── embeddings.py
│
├── models/
│   └── classifier.py
│
├── evaluation/
│   └── metrics.py
│
└── main.py
```

এটা M01-এ শেখা **modular Python architecture**-এর সাথেও directly connected।

---

# 51. NLP Pipeline-এর 3টি Major Layer

পুরো বিষয়টা আরও সহজে:

```text
                 NLP SYSTEM
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
   Preprocessing   Representation  Modeling
       │             │             │
       ↓             ↓             ↓
   Cleaning        TF-IDF         ML
   Tokenization    Embedding      DL
   Normalization   Vector         Transformer
```

তারপর:

```text
Model
 ↓
Prediction
 ↓
Evaluation
```

---

# 52. সবচেয়ে গুরুত্বপূর্ণ Difference

### Preprocessing

Text clean/prepare করা।

### Feature Extraction

Text থেকে measurable features বের করা।

### Representation

Text-কে numerical form-এ represent করা।

### Modeling

এই representation ব্যবহার করে prediction/generation করা।

এগুলো এক জিনিস নয়।

---

# 53. Classical Pipeline বনাম Transformer Pipeline

### Classical

```text
Raw Text
 ↓
Cleaning
 ↓
Tokenization
 ↓
Stopword
 ↓
Stemming/Lemma
 ↓
TF-IDF
 ↓
ML
```

### Transformer

```text
Raw Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embeddings
 ↓
Self-Attention
 ↓
Transformer
 ↓
Output
```

এই difference পরবর্তীতে BERT/GPT বুঝতে অনেক সাহায্য করবে।

---

# 🧪 Practical Exercise 1

এই text:

```python
text = """
Python is powerful.
Python is easy to learn.
NLP is interesting.
"""
```

তোমার pipeline:

```text
1. Clean
2. Normalize
3. Sentence split
4. Tokenize
5. Count words
6. Count unique words
```

---

# 🧪 Practical Exercise 2

Input:

```python
text = "   AI is AMAZING!!!   "
```

তৈরি করো:

```text
Raw Text
↓
Clean Text
↓
Normalized Text
↓
Tokens
```

---

# 🧪 Practical Exercise 3 — Mini Pipeline

একটি function তৈরি করো:

```python
def preprocess(text):
    pass
```

যেটা:

1. whitespace remove করবে
    
2. lowercase করবে
    
3. multiple spaces ঠিক করবে
    
4. tokens return করবে
    

Expected:

```python
text = "   I LOVE   NLP   "

print(preprocess(text))
```

Conceptually:

```text
['i', 'love', 'nlp']
```

---

# 🔥 Mini Challenge

একটি reusable pipeline তৈরি করো:

```python
def clean_text(text):
    pass


def normalize_text(text):
    pass


def tokenize_text(text):
    pass


def preprocess(text):
    pass
```

তারপর:

```python
text = """
   Python is AMAZING!!!
   I love learning NLP.
"""

tokens = preprocess(text)

print(tokens)
```

**এখনো NLTK/spaCy ব্যবহার করবে না।**

কারণ আমাদের প্রথমে pipeline-এর logic নিজের হাতে বুঝতে হবে।

---

# 🧠 Theory Questions

### Q1.

NLP pipeline কী?

### Q2.

NLP pipeline-এর প্রধান stages কী কী?

### Q3.

Cleaning এবং normalization-এর পার্থক্য কী?

### Q4.

Sentence segmentation কী?

### Q5.

Sentence segmentation শুধু `.` দিয়ে করা যায় না কেন?

### Q6.

Tokenization কী?

### Q7.

Stopwords সবসময় remove করা উচিত নয় কেন?

### Q8.

Stemming এবং lemmatization pipeline-এ কোথায় আসে?

### Q9.

Feature extraction কী?

### Q10.

Numerical representation কেন দরকার?

### Q11.

TF-IDF কীভাবে pipeline-এ কাজ করে?

### Q12.

Training এবং inference pipeline-এর consistency কেন গুরুত্বপূর্ণ?

### Q13.

Data leakage কী?

### Q14.

Classical NLP pipeline এবং Transformer pipeline-এর পার্থক্য কী?

### Q15.

কেন সব NLP task-এর pipeline একই হয় না?

---

# 🎯 Interview Questions

### Beginner

1. What is an NLP pipeline?
    
2. What are the major steps in an NLP pipeline?
    
3. What is text preprocessing?
    
4. What is tokenization?
    
5. What is normalization?
    

### Intermediate

6. Why is preprocessing task-dependent?
    
7. Why shouldn't stopwords always be removed?
    
8. What is feature extraction?
    
9. What is TF-IDF?
    
10. What is the difference between preprocessing and feature extraction?
    
11. Why is data leakage dangerous?
    
12. Why should training and inference preprocessing be consistent?
    

### Advanced

13. How does a Transformer-based NLP pipeline differ from a traditional NLP pipeline?
    
14. Why can aggressive preprocessing hurt modern NLP models?
    
15. Why is information preservation important in NLP preprocessing?
    
16. How would you design an NLP pipeline for a text classification system?
    
17. How would you design an NLP pipeline for an AI writing assistant?
    

---

# 🔥 AI Project Connection

তোমার future AI Writing Platform-এর জন্য আজকের concept:

```text
                    USER
                     │
                     ↓
                  TEXT
                     │
                     ↓
              INPUT VALIDATION
                     │
                     ↓
              PREPROCESSING
                     │
                     ↓
               TOKENIZATION
                     │
                     ↓
             NLP ANALYSIS
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
      Syntax      Semantics     Style
        │            │            │
        └────────────┼────────────┘
                     ↓
                AI MODEL
                     │
                     ↓
             GENERATED/EDITED
                     │
                     ↓
              POST PROCESSING
                     │
                     ↓
                FINAL TEXT
```

এই architecture-এর প্রতিটি component আমরা পরের lessons-এ ধীরে ধীরে build করব।

---

# ✅ M02.03 Completion Checklist

-  NLP Pipeline
    
-  Raw Text
    
-  Text Cleaning
    
-  Whitespace Cleaning
    
-  HTML Handling
    
-  URL Handling
    
-  Emoji Handling
    
-  Text Normalization
    
-  Lowercasing
    
-  Unicode normalization concept
    
-  Sentence Segmentation
    
-  Tokenization
    
-  Word vs Token
    
-  Token IDs
    
-  Stopword Handling
    
-  Stemming
    
-  Lemmatization
    
-  Linguistic Analysis
    
-  POS
    
-  NER
    
-  Dependency Analysis
    
-  Feature Extraction
    
-  Bag of Words
    
-  TF-IDF
    
-  Numerical Representation
    
-  One-Hot
    
-  Embeddings concept
    
-  NLP Model
    
-  Prediction
    
-  Post-processing
    
-  Evaluation
    
-  Training Pipeline
    
-  Inference Pipeline
    
-  Data Leakage
    
-  Classical NLP Pipeline
    
-  Modern Transformer Pipeline
    
-  Task-dependent preprocessing
    
-  Information preservation
    
-  Modular NLP architecture
    

---

# ⭐ আজকের সবচেয়ে গুরুত্বপূর্ণ Mental Model

তুমি এই তিনটা pipeline মনে রাখবে।

### Classical NLP

```text
TEXT
 ↓
CLEAN
 ↓
TOKENIZE
 ↓
NORMALIZE
 ↓
TF-IDF
 ↓
ML MODEL
 ↓
PREDICTION
```

### Neural NLP

```text
TEXT
 ↓
TOKENIZE
 ↓
EMBEDDING
 ↓
RNN/LSTM
 ↓
PREDICTION
```

### Modern NLP

```text
TEXT
 ↓
TOKENIZER
 ↓
TOKEN IDs
 ↓
EMBEDDINGS
 ↓
TRANSFORMER
 ↓
CONTEXTUAL REPRESENTATION
 ↓
PREDICTION / GENERATION
```

আর সবচেয়ে গুরুত্বপূর্ণ:

> **NLP pipeline মানে শুধু text cleaning নয়। Raw text থেকে final intelligent output পর্যন্ত পুরো journey-টাই NLP pipeline।**

**M02.03 complete.**

পরের lesson হবে **M02.04 — Text Preprocessing**, যেখানে আমরা cleaning-এর প্রতিটি অংশ—**lowercase, whitespace, punctuation, special characters, numbers, URLs, emails, HTML, emojis, contractions, repeated characters, noisy text এবং spelling normalization**—প্রতিটা হাতে-কলমে implement করব।

---
# M02.04 — Text Preprocessing 🔥

এখন আমরা NLP-এর সবচেয়ে গুরুত্বপূর্ণ foundation topic-গুলোর একটি শুরু করছি: **Text Preprocessing**।

AI writing assistant, text classifier, sentiment analysis, AI detector, chatbot—প্রায় সব NLP system-এই raw text সরাসরি model-এ না দিয়ে আগে কিছু preprocessing করা হয়।

আজকের lesson-এ আমরা শুধু `lowercase()` শেখার মধ্যে সীমাবদ্ধ থাকব না। **Real-world noisy text কীভাবে clean এবং normalize করতে হয়** সেটাও দেখব।

---

# 1. Text Preprocessing কী?

**Text Preprocessing** হলো raw text-কে এমনভাবে পরিবর্তন/পরিষ্কার করা যাতে পরবর্তী NLP processing বা model-এর জন্য text উপযোগী হয়।

ধরো input:

```text
"  HELLO!!! Visit https://example.com 😊
Email: TEST@GMAIL.COM <b>Welcome</b>!!!  "
```

Preprocessing-এর পরে আমরা পেতে পারি:

```text
"hello visit url email welcome"
```

তবে গুরুত্বপূর্ণ বিষয়:

> **সব text-এর জন্য একই preprocessing করা যাবে না।**

যেমন sentiment analysis-এ:

```text
"I LOVE this!!!"
```

এখানে `!!!` বা uppercase কখনো কখনো useful signal হতে পারে।

---

# 2. Complete Text Preprocessing Pipeline

আজ আমরা এই বিষয়গুলো শিখব:

```text
Raw Text
   ↓
Lowercasing
   ↓
Whitespace Cleaning
   ↓
HTML Cleaning
   ↓
URL Handling
   ↓
Email Handling
   ↓
Punctuation Handling
   ↓
Special Character Handling
   ↓
Number Handling
   ↓
Emoji Handling
   ↓
Contraction Handling
   ↓
Repeated Character Handling
   ↓
Noisy Text Cleaning
   ↓
Spelling Normalization
   ↓
Clean Text
```

---

# 3. Lowercasing

সব text lowercase করা।

### Example

```python
text = "Hello WORLD NLP"

print(text.lower())
```

Output:

```text
hello world nlp
```

### কেন?

এতে:

```text
Python
python
PYTHON
```

একই শব্দ হিসেবে treat করা যায়।

### Example

```python
words = ["Python", "python", "PYTHON"]

normalized = [word.lower() for word in words]

print(normalized)
```

Output:

```text
['python', 'python', 'python']
```

---

# 4. কিন্তু Lowercase সবসময় করা উচিত?

না।

ধরো:

```text
US
us
```

এগুলোর meaning আলাদা হতে পারে।

আর:

```text
Apple
apple
```

context অনুযায়ী আলাদা meaning হতে পারে।

তাই preprocessing সবসময় **task-dependent**।

---

# 5. Whitespace Cleaning

Raw text-এ অনেক extra space থাকতে পারে।

```python
text = "Hello     world    NLP"

print(text)
```

Output:

```text
Hello     world    NLP
```

আমরা চাই:

```text
Hello world NLP
```

### Solution

```python
text = "Hello     world    NLP"

cleaned = " ".join(text.split())

print(cleaned)
```

Output:

```text
Hello world NLP
```

---

# 6. Leading এবং Trailing Spaces

```python
text = "   Hello World   "

print(text.strip())
```

Output:

```text
Hello World
```

### Important methods

```python
text.strip()
text.lstrip()
text.rstrip()
```

---

# 7. Newline Cleaning

Example:

```python
text = """
Hello

World

NLP
"""
```

আমরা normalize করতে পারি:

```python
cleaned = " ".join(text.split())

print(cleaned)
```

Output:

```text
Hello World NLP
```

---

# 8. Punctuation

Punctuation:

```text
.
,
!
?
:
;
'
"
-
(
)
[
]
{
}
```

Example:

```python
text = "Hello, world!"

print(text)
```

যদি punctuation remove করতে চাই:

```python
import string

text = "Hello, world!"

cleaned = text.translate(
    str.maketrans("", "", string.punctuation)
)

print(cleaned)
```

Output:

```text
Hello world
```

---

# 9. সব punctuation remove করা কি ভালো?

সবসময় না।

Example:

```text
I am happy!
Are you okay?
```

`!` এবং `?` emotional/contextual information বহন করতে পারে।

আর:

```text
can't
don't
I'm
```

এখানে punctuation contraction-এর অংশ।

তাই blind removal dangerous।

---

# 10. Special Characters

Example:

```text
Hello @user #NLP $100 % test & AI
```

Special characters:

```text
@
#
$
%
&
*
```

কোনগুলো remove করব সেটা task অনুযায়ী নির্ধারণ করতে হবে।

যেমন social-media analysis-এ:

```text
#AI
@OpenAI
```

খুব গুরুত্বপূর্ণ হতে পারে।

---

# 11. URL Handling

Raw text:

```text
Visit https://example.com/article
```

URL সরাসরি remove করার পরিবর্তে placeholder ব্যবহার করা ভালো হতে পারে।

```text
Visit URL
```

Python:

```python
import re

text = "Visit https://example.com/article"

cleaned = re.sub(
    r'https?://\S+|www\.\S+',
    ' URL ',
    text
)

print(cleaned)
```

Output:

```text
Visit  URL
```

Whitespace normalize করলে:

```python
cleaned = " ".join(cleaned.split())

print(cleaned)
```

Output:

```text
Visit URL
```

---

# 12. কেন URL → URL?

কারণ URL-এর actual value অনেক সময় গুরুত্বপূর্ণ নয়।

যেমন:

```text
Visit https://abc.com
Visit https://xyz.com
```

দুটোতেই semantic information হতে পারে:

```text
Visit URL
```

এতে vocabulary size কমতে পারে।

---

# 13. Email Handling

Example:

```text
Contact me at test@gmail.com
```

Email replace করা যায়:

```text
Contact me at EMAIL
```

Python:

```python
import re

text = "Contact me at test@gmail.com"

cleaned = re.sub(
    r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b',
    ' EMAIL ',
    text
)

print(cleaned)
```

Output:

```text
Contact me at EMAIL
```

---

# 14. HTML Cleaning

Web data থেকে HTML আসতে পারে।

```html
<p>Hello <b>World</b></p>
```

আমরা চাই:

```text
Hello World
```

Simple regex:

```python
import re

text = "<p>Hello <b>World</b></p>"

cleaned = re.sub(r'<[^>]+>', ' ', text)

cleaned = " ".join(cleaned.split())

print(cleaned)
```

Output:

```text
Hello World
```

### Real project

Production-level HTML parsing-এর জন্য dedicated HTML parser ব্যবহার করা বেশি reliable।

---

# 15. Emoji Handling 😊

Example:

```text
I love this product 😊❤️
```

Emoji কখনো useful information বহন করে।

যেমন:

```text
😊 = positive
😢 = negative
🔥 = excitement
```

তাই emoji সবসময় remove করা উচিত নয়।

### Option 1 — Keep

```text
I love this product 😊
```

### Option 2 — Convert

```text
I love this product smiling_face
```

### Option 3 — Remove

```text
I love this product
```

Task অনুযায়ী choice করতে হবে।

---

# 16. Unicode Normalization

একই character বিভিন্ন Unicode representation-এ থাকতে পারে।

Python:

```python
import unicodedata

text = "café"

normalized = unicodedata.normalize("NFC", text)

print(normalized)
```

Common forms:

```text
NFC
NFD
NFKC
NFKD
```

NLP preprocessing-এ Unicode normalization বিশেষভাবে useful যখন বিভিন্ন source থেকে text আসে।

---

# 17. Numbers

Example:

```text
I bought 25 books.
```

Number রেখে দিতে পারি:

```text
I bought 25 books.
```

অথবা placeholder:

```text
I bought NUMBER books.
```

অথবা remove:

```text
I bought books.
```

কোনটি করব?

Task-এর উপর নির্ভর করে।

### Financial NLP

```text
$500
```

খুব important।

### General text classification

```text
25
```

হয়তো ততটা important নয়।

---

# 18. Number Replacement

```python
import re

text = "I have 25 books and 3 pens."

cleaned = re.sub(r'\d+', ' NUMBER ', text)

cleaned = " ".join(cleaned.split())

print(cleaned)
```

Output:

```text
I have NUMBER books and NUMBER pens.
```

---

# 19. Contractions

English text-এ:

```text
I'm
don't
can't
isn't
won't
you're
they're
```

এসবকে contractions বলে।

Example:

```text
I'm happy.
```

Expanded:

```text
I am happy.
```

আর:

```text
don't
```

→

```text
do not
```

---

# 20. Contraction কেন গুরুত্বপূর্ণ?

Tokenization-এর আগে:

```text
don't
```

এবং:

```text
do not
```

দুইভাবে tokenize হতে পারে।

Classical NLP system-এ contraction expansion useful হতে পারে।

কিন্তু modern transformer tokenizer অনেক ক্ষেত্রে contractions handle করতে পারে।

তাই আবারও:

> **Preprocessing depends on the model.**

---

# 21. Repeated Characters

Social media text:

```text
Sooooooo good!!!
```

বা:

```text
Hellooooooo
```

এগুলো noisy text।

আমরা normalize করতে পারি:

```text
Soo good
```

বা:

```text
So good
```

Simple regex:

```python
import re

text = "Sooooooo good"

cleaned = re.sub(r'(.)\1{2,}', r'\1\1', text)

print(cleaned)
```

Output:

```text
Soo good
```

আরও aggressive normalization করলে:

```text
So good
```

করা যায়।

কিন্তু মনে রাখবে:

```text
Nooooo!
```

এর emotional intensity আছে।

তাই sentiment analysis-এ repeated characters useful signal হতে পারে।

---

# 22. Noisy Text

Real-world data অনেক noisy।

Example:

```text
Hiiii!!!! I loooove this 😍😍😍
Visit: https://example.com
Email: abc@gmail.com
```

এখানে আছে:

```text
Repeated characters
Repeated emoji
Punctuation
URL
Email
Uppercase
Whitespace
```

এটাই real-world NLP।

---

# 23. Spelling Normalization

Social media:

```text
gr8
u
pls
thx
luv
```

এগুলো informal spelling।

Possible normalization:

```text
gr8 → great
u → you
pls → please
thx → thanks
luv → love
```

কিন্তু blindly replace করা যাবে না।

Example:

```text
US
```

কে:

```text
us
```

করলে meaning পরিবর্তন হতে পারে।

---

# 24. Case + Whitespace + URL + Email একসাথে

এখন একটি simple preprocessing function বানাই।

```python
import re

def preprocess_text(text):
    text = text.lower()

    text = re.sub(
        r'https?://\S+|www\.\S+',
        ' URL ',
        text
    )

    text = re.sub(
        r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b',
        ' EMAIL ',
        text
    )

    text = re.sub(r'<[^>]+>', ' ', text)

    text = re.sub(r'\d+', ' NUMBER ', text)

    text = " ".join(text.split())

    return text
```

Test:

```python
text = """
HELLO!!! Visit https://example.com
Contact TEST@gmail.com
I have 25 books.
"""

print(preprocess_text(text))
```

Output approximately:

```text
hello!!! visit URL contact EMAIL i have NUMBER books.
```

---

# 25. এবার Punctuation Add করি

```python
import re
import string

def preprocess_text(text):

    text = text.lower()

    # URL
    text = re.sub(
        r'https?://\S+|www\.\S+',
        ' URL ',
        text
    )

    # Email
    text = re.sub(
        r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b',
        ' EMAIL ',
        text
    )

    # HTML
    text = re.sub(
        r'<[^>]+>',
        ' ',
        text
    )

    # Numbers
    text = re.sub(
        r'\d+',
        ' NUMBER ',
        text
    )

    # Punctuation
    text = text.translate(
        str.maketrans("", "", string.punctuation)
    )

    # Whitespace
    text = " ".join(text.split())

    return text
```

Input:

```text
HELLO!!! Visit https://example.com
```

Output:

```text
hello visit URL
```

---

# 26. Important Problem: Processing Order

Preprocessing-এর **order matters**।

ধরো:

```text
https://example.com
```

আগে punctuation remove করলে:

```text
httpsexamplecom
```

হয়ে যেতে পারে।

তারপর URL detect করা কঠিন হবে।

তাই:

```text
URL detection
      ↓
Email detection
      ↓
HTML handling
      ↓
Other cleaning
```

এই order বেশি logical।

---

# 27. Preprocessing Function Modular করা

একটা huge function না বানিয়ে ছোট ছোট function বানানো better।

```python
def lowercase(text):
    return text.lower()


def normalize_whitespace(text):
    return " ".join(text.split())


def remove_html(text):
    import re
    return re.sub(r'<[^>]+>', ' ', text)


def replace_urls(text):
    import re
    return re.sub(
        r'https?://\S+|www\.\S+',
        ' URL ',
        text
    )
```

তারপর:

```python
def preprocess(text):

    text = lowercase(text)
    text = remove_html(text)
    text = replace_urls(text)
    text = normalize_whitespace(text)

    return text
```

এটি maintain করা সহজ।

---

# 28. Real NLP Architecture

আমাদের future AI writing platform-এ:

```text
User Input
    ↓
Text Validation
    ↓
HTML Handling
    ↓
URL Detection
    ↓
Email Detection
    ↓
Unicode Normalization
    ↓
Whitespace Normalization
    ↓
Case Normalization
    ↓
Noise Handling
    ↓
Tokenization
    ↓
Model
```

---

# 29. Preprocessing ≠ Tokenization

এগুলো আলাদা।

### Preprocessing

```text
"  HELLO!!!   WORLD  "
```

↓

```text
"hello!!! world"
```

### Tokenization

```text
"hello!!! world"
```

↓

```text
["hello", "!", "!", "!", "world"]
```

অর্থাৎ:

```text
Preprocessing
      ↓
Tokenization
```

---

# 30. Preprocessing ≠ Feature Extraction

আরেকটি গুরুত্বপূর্ণ distinction:

```text
Raw Text
   ↓
Preprocessing
   ↓
Clean Text
   ↓
Feature Extraction
   ↓
Features
```

Example:

```text
"I love this movie"
```

Feature হতে পারে:

```text
word_count = 4
positive_words = 1
sentence_length = 4
```

---

# 31. Preprocessing-এর Golden Rule

সবচেয়ে গুরুত্বপূর্ণ rule:

> **Don't preprocess blindly.**

কারণ:

```text
More cleaning ≠ Better NLP
```

বরং:

```text
Task
 +
Model
 +
Data
 ↓
Preprocessing Strategy
```

---

# 32. Classical NLP বনাম Modern NLP

### Classical ML

অনেক সময়:

```text
Lowercase
↓
Remove noise
↓
Tokenize
↓
Stopword handling
↓
Stemming/Lemmatization
↓
TF-IDF
↓
ML
```

### Modern Transformer

অনেক সময়:

```text
Raw Text
↓
Light Cleaning
↓
Tokenizer
↓
Subword Tokens
↓
Token IDs
↓
Transformer
```

এখানে অতিরিক্ত preprocessing information নষ্ট করতে পারে।

---

# 33. AI Writing Assistant-এর ক্ষেত্রে

আমাদের target system:

```text
User:
"I thiiink this is REALLY good!!!"
```

আমরা যদি detector/classifier বানাই, তাহলে:

```text
Original text
```

সংরক্ষণ করতে হবে।

তারপর:

```text
Normalized copy
```

বানানো যেতে পারে।

অর্থাৎ:

```text
Original
   │
   ├──→ Display
   │
   └──→ Processing Copy
             ↓
        Preprocessing
             ↓
        NLP Pipeline
```

**Original user text কখনো অপ্রয়োজনে destroy করা উচিত নয়।**

---

# 34. একটি Better Preprocessor

এবার একটু structured version:

```python
import re
import unicodedata


def normalize_unicode(text):
    return unicodedata.normalize("NFC", text)


def normalize_case(text):
    return text.lower()


def replace_urls(text):
    pattern = r'https?://\S+|www\.\S+'
    return re.sub(pattern, ' URL ', text)


def replace_emails(text):
    pattern = r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b'
    return re.sub(pattern, ' EMAIL ', text)


def remove_html(text):
    return re.sub(r'<[^>]+>', ' ', text)


def normalize_whitespace(text):
    return " ".join(text.split())


def preprocess(text):

    text = normalize_unicode(text)
    text = remove_html(text)
    text = replace_urls(text)
    text = replace_emails(text)
    text = normalize_case(text)
    text = normalize_whitespace(text)

    return text
```

Test:

```python
text = """
<HTML>
HELLO!!! Visit https://example.com
Contact user@gmail.com
</HTML>
"""

result = preprocess(text)

print(result)
```

Possible output:

```text
hello!!! visit URL contact EMAIL
```

---

# 35. কোন জিনিস Keep / Replace / Remove?

একটি useful decision table:

| Element        | Possible Action     |
| -------------- | ------------------- |
| Uppercase      | lowercase           |
| Extra spaces   | normalize           |
| URL            | replace with URL    |
| Email          | replace with EMAIL  |
| HTML           | remove              |
| Numbers        | keep/replace        |
| Emoji          | keep/replace/remove |
| Punctuation    | task-dependent      |
| Hashtag        | task-dependent      |
| Mention        | task-dependent      |
| Repeated chars | normalize           |
| Spelling       | normalize carefully |
| Unicode        | normalize           |

---

# 36. Practice Project 🔥

একটি function বানাও:

```python
def clean_text(text):
    ...
```

Input:

```python
text = """
  HELLOOOO!!! 😍😍

  Visit https://example.com

  Contact: TEST@gmail.com

  I have 25 books!!!

  <b>Python is GREAT</b>
"""
```

তোমার function-এর লক্ষ্য:

```text
hellooo visit URL contact EMAIL i have NUMBER books python is great
```

Emoji remove করা optional।

---

# 37. Practice Task 2

এই text:

```text
"   I   LOVE   Python!!!   "
```

Expected:

```text
i love python
```

---

# 38. Practice Task 3

Input:

```text
"Visit https://google.com and https://github.com"
```

Expected:

```text
Visit URL and URL
```

---

# 39. Practice Task 4

Input:

```text
"Email me at hello@gmail.com"
```

Expected:

```text
Email me at EMAIL
```

---

# 40. Practice Task 5 — Noisy Text

Input:

```text
"Hellooooooo!!!! This is soooo coooool 😍😍😍"
```

তোমাকে normalize করতে হবে:

```text
Helloo!! This is soo cool
```

এখানে তুমি decide করবে কতটা aggressive normalization করবে।

---

# 41. Theory Questions

নিজে answer করার চেষ্টা করো:

### Q1

Text preprocessing কী?

### Q2

Lowercasing কেন করা হয়?

### Q3

সব NLP task-এ lowercase করা উচিত কি?

### Q4

URL কেন `URL` placeholder করা যেতে পারে?

### Q5

Email কেন placeholder করা যায়?

### Q6

Emoji সবসময় remove করা উচিত কি?

### Q7

Punctuation remove করার সমস্যা কী?

### Q8

Contraction কী?

### Q9

Repeated characters কী?

### Q10

Unicode normalization কী?

### Q11

Preprocessing এবং tokenization-এর difference কী?

### Q12

Preprocessing এবং feature extraction-এর difference কী?

### Q13

কেন preprocessing order গুরুত্বপূর্ণ?

### Q14

Classical NLP এবং Transformer NLP preprocessing-এর মধ্যে difference কী?

### Q15

কেন original text সংরক্ষণ করা উচিত?

---

# 42. Interview Questions

### Beginner

* What is text preprocessing?
* Why is preprocessing important in NLP?
* What is normalization?
* Why do we lowercase text?
* How do you remove extra whitespace?

### Intermediate

* How do you handle URLs?
* How do you handle HTML?
* How do you handle emojis?
* What are contractions?
* How do you handle noisy social-media text?

### Advanced

* Should punctuation always be removed?
* When can lowercasing hurt NLP performance?
* Why can aggressive preprocessing reduce model performance?
* How does preprocessing differ between TF-IDF and Transformers?
* Why should preprocessing be task-dependent?
* Why is preprocessing order important?

---

# 43. M02.04 Completion Checklist

আজকের lesson complete হলে তুমি বুঝবে:

* [x] Text preprocessing
* [x] Lowercasing
* [x] Whitespace cleaning
* [x] Newline normalization
* [x] Punctuation
* [x] Special characters
* [x] Numbers
* [x] URL handling
* [x] Email handling
* [x] HTML cleaning
* [x] Emoji handling
* [x] Unicode normalization
* [x] Contractions
* [x] Repeated characters
* [x] Noisy text
* [x] Spelling normalization concept
* [x] Processing order
* [x] Modular preprocessing
* [x] Preprocessing vs tokenization
* [x] Preprocessing vs feature extraction
* [x] Classical vs modern preprocessing
* [x] AI writing assistant application

### 🧠 Final mental model

```text
                 RAW TEXT
                    │
                    ▼
          ┌──────────────────┐
          │ Text Preprocessing│
          └──────────────────┘
                    │
       ┌────────────┼────────────┐
       ▼            ▼            ▼
   Normalize      Clean       Replace
       │            │            │
   lowercase     HTML        URL → URL
   Unicode       noise       Email → EMAIL
   whitespace    unwanted    Number → NUMBER
       │            │            │
       └────────────┼────────────┘
                    ▼
              CLEAN TEXT
                    │
                    ▼
               TOKENIZATION
                    │
                    ▼
             NUMERICAL DATA
                    │
                    ▼
                 MODEL
```

**M02.04 complete.**
পরের lesson হবে **M02.05 — Tokenization Deep Dive**, যেখানে আমরা **word tokenization, sentence tokenization, character tokenization, subword tokenization, BPE, WordPiece, Unigram, token IDs, vocabulary এবং Transformer tokenizer** একদম foundation থেকে শিখব।


---
# M02.05 — Tokenization Deep Dive 🔥

আজকের lesson NLP-এর **core foundation**।
তুমি যদি ভবিষ্যতে **AI Writing Assistant, AI Detector, Text Classifier, LLM-based application** বানাতে চাও, তাহলে tokenization খুব ভালোভাবে বুঝতে হবে।

আজ আমরা শিখব:

```text
Tokenization
├── Word Tokenization
├── Sentence Tokenization
├── Character Tokenization
├── Subword Tokenization
├── Vocabulary
├── Token ID
├── Special Tokens
├── BPE
├── WordPiece
├── Unigram
├── Padding
├── Truncation
├── Attention Mask
├── Tokenizer vs Embedding
└── Transformer Tokenization
```

---

# 1. Tokenization কী?

**Tokenization** হলো text-কে ছোট ছোট অংশে ভাগ করার process।

এই ছোট অংশগুলোকে বলা হয় **tokens**।

Example:

```text
I love Python
```

Word tokenization:

```text
["I", "love", "Python"]
```

অর্থাৎ:

```text
Text
 ↓
Tokens
```

---

# 2. Token কী?

Token হলো NLP system-এর জন্য text-এর একটি processing unit।

Token হতে পারে:

```text
Word
Subword
Character
Symbol
Punctuation
Special token
```

Example:

```text
Hello, world!
```

Possible tokens:

```text
["Hello", ",", "world", "!"]
```

---

# 3. Token এবং Word কি একই?

**না।**

অনেক ক্ষেত্রে:

```text
1 word = 1 token
```

কিন্তু সবসময় নয়।

Modern NLP/LLM-এ একটি word অনেক token-এ বিভক্ত হতে পারে।

Example conceptual:

```text
unhappiness
```

হতে পারে:

```text
["un", "happiness"]
```

অথবা:

```text
["un", "happy", "ness"]
```

তাই:

```text
Word ≠ Token
```

এটি খুব গুরুত্বপূর্ণ।

---

# 4. কেন Tokenization দরকার?

Computer সরাসরি:

```text
"I love Python"
```

এর semantic meaning model-এর কাছে numerical form-এ দিতে হয়।

তাই:

```text
Text
 ↓
Tokens
 ↓
Token IDs
 ↓
Embeddings
 ↓
Model
```

---

# 5. Tokenization-এর Types

আমরা প্রধানত চার ধরনের tokenization দেখব:

```text
1. Sentence Tokenization
2. Word Tokenization
3. Character Tokenization
4. Subword Tokenization
```

---

# 6. Sentence Tokenization

একটি paragraph-কে sentence-এ ভাগ করা।

Input:

```text
I love Python. Python is easy. NLP is interesting.
```

Output:

```python
[
    "I love Python.",
    "Python is easy.",
    "NLP is interesting."
]
```

একে বলা হয়:

**Sentence Segmentation**

---

# 7. Simple Sentence Tokenization

Python:

```python
text = "I love Python. Python is easy. NLP is interesting."

sentences = text.split(".")

print(sentences)
```

Output:

```text
['I love Python', ' Python is easy', ' NLP is interesting', '']
```

Problem আছে।

শেষে empty string এসেছে।

---

# 8. Regex Sentence Tokenization

```python
import re

text = "I love Python. Python is easy! NLP is interesting?"

sentences = re.split(r'[.!?]+', text)

sentences = [s.strip() for s in sentences if s.strip()]

print(sentences)
```

Output:

```text
[
    "I love Python",
    "Python is easy",
    "NLP is interesting"
]
```

কিন্তু real-world sentence segmentation আরও কঠিন।

---

# 9. Sentence Boundary Problem

Example:

```text
Dr. Rahman lives in Dhaka.
```

এখানে:

```text
Dr.
```

এর `.` sentence ending নয়।

আর:

```text
I live in the U.S.A. I like Python.
```

এখানেও period সবসময় sentence boundary নয়।

তাই:

```text
sentence splitting ≠ simply split(".")
```

---

# 10. Word Tokenization

Sentence:

```text
I love Python.
```

Word tokenizer:

```text
["I", "love", "Python", "."]
```

অথবা কিছু tokenizer:

```text
["I", "love", "Python"]
```

এখানে punctuation handling tokenizer-এর উপর নির্ভর করে।

---

# 11. Python Basic Word Tokenization

```python
text = "I love Python"

tokens = text.split()

print(tokens)
```

Output:

```text
['I', 'love', 'Python']
```

কিন্তু:

```python
text = "Hello, world!"
print(text.split())
```

Output:

```text
['Hello,', 'world!']
```

এখানে punctuation word-এর সঙ্গে attached।

---

# 12. Regex Word Tokenization

```python
import re

text = "Hello, world!"

tokens = re.findall(r'\w+|[^\w\s]', text)

print(tokens)
```

Output:

```text
['Hello', ',', 'world', '!']
```

এখানে punctuation আলাদা token হয়েছে।

---

# 13. Character Tokenization

এখানে প্রতিটি character token।

Input:

```text
cat
```

Output:

```text
["c", "a", "t"]
```

Example:

```python
text = "cat"

tokens = list(text)

print(tokens)
```

Output:

```text
['c', 'a', 't']
```

---

# 14. Character Tokenization-এর সুবিধা

Unknown word problem কমে যায়।

ধরো model আগে:

```text
supercalifragilistic
```

শব্দটি দেখেনি।

Character tokenizer এটাকে ভাঙতে পারবে:

```text
s
u
p
e
r
...
```

তাই unseen word handle করা সহজ।

---

# 15. Character Tokenization-এর সমস্যা

Sequence অনেক বড় হয়ে যায়।

Example:

```text
I love natural language processing
```

word tokens:

```text
6–7 tokens
```

character tokens:

```text
30+ tokens
```

Longer sequence:

```text
More computation
More memory
More processing
```

---

# 16. Subword Tokenization 🔥

Modern NLP-এর সবচেয়ে গুরুত্বপূর্ণ conceptগুলোর একটি।

Subword হলো:

> পুরো word এবং character-এর মাঝামাঝি ছোট linguistic units।

Example:

```text
unhappiness
```

Possible:

```text
un + happy + ness
```

অথবা:

```text
un + happiness
```

---

# 17. কেন Subword দরকার?

ধরো vocabulary-তে আছে:

```text
play
playing
played
player
```

যদি প্রতিটি পুরো word আলাদাভাবে রাখি:

```text
play
playing
played
player
...
```

Vocabulary বড় হবে।

Subword approach:

```text
play
ing
ed
er
```

তাহলে নতুন word থেকেও model meaningful pieces পেতে পারে।

---

# 18. Subword-এর সবচেয়ে বড় সুবিধা

ধরো model vocabulary-তে আছে:

```text
happy
ness
```

কিন্তু:

```text
happiness
```

আগে দেখেনি।

Subword tokenizer:

```text
happy + ness
```

করতে পারে।

অর্থাৎ unknown word পুরোপুরি unknown না হয়ে তার অংশগুলো known হতে পারে।

---

# 19. Word vs Character vs Subword

| Type      | Example: `unhappy`              |
| --------- | ------------------------------- |
| Word      | `["unhappy"]`                   |
| Character | `["u","n","h","a","p","p","y"]` |
| Subword   | `["un","happy"]`                |

Modern LLM-গুলো সাধারণত **subword/byte-level tokenization family** ব্যবহার করে।

---

# 20. Vocabulary কী?

Tokenizer-এর known tokens-এর collection হলো vocabulary।

Example:

```python
vocab = {
    "I": 0,
    "love": 1,
    "Python": 2,
    "NLP": 3
}
```

এখানে:

```text
Vocabulary size = 4
```

---

# 21. Token ID

Model text-এর পরিবর্তে token ID ব্যবহার করে।

Vocabulary:

```python
vocab = {
    "I": 0,
    "love": 1,
    "Python": 2
}
```

Text:

```text
I love Python
```

Tokens:

```text
["I", "love", "Python"]
```

Token IDs:

```text
[0, 1, 2]
```

Pipeline:

```text
Text
 ↓
Tokens
 ↓
Token IDs
```

---

# 22. Token IDs কেন দরকার?

Neural network text-এর string নিয়ে directly mathematical operation করতে পারে না।

তাই:

```text
"love"
```

কে:

```text
1532
```

এর মতো ID দেওয়া হয়।

তারপর:

```text
1532
 ↓
Embedding Vector
```

---

# 23. Token ID ≠ Meaning

এটি খুব important।

ধরো:

```text
"cat" → 10
"dog" → 11
"love" → 12
```

এর অর্থ এই নয়:

```text
dog > cat
```

Token ID শুধু একটি **identifier**।

Meaning embedding layer-এ আসে।

---

# 24. Token ID → Embedding

ধরো:

```text
love → 1532
```

Embedding layer:

```text
1532
 ↓
[0.21, -0.43, 0.76, ...]
```

অর্থাৎ:

```text
Token
 ↓
ID
 ↓
Vector
```

---

# 25. Special Tokens

Modern tokenizer-এ special tokens থাকে।

Common examples:

```text
[PAD]
[UNK]
[BOS]
[EOS]
[CLS]
[SEP]
[MASK]
```

সব model একই special token ব্যবহার করে না।

---

# 26. `[PAD]`

Padding-এর জন্য।

ধরো:

```text
I love Python
```

3 tokens।

আর:

```text
I love NLP very much
```

5 tokens।

Batch processing করতে একই length দরকার হতে পারে।

তখন:

```text
I love Python [PAD] [PAD]
```

---

# 27. `[UNK]`

Unknown token।

যদি tokenizer কোনো input piece handle করতে না পারে:

```text
[UNK]
```

ব্যবহার করতে পারে।

Modern subword/byte-level tokenizers অনেক unknown-word problem কমিয়ে দিয়েছে।

---

# 28. `[BOS]`

**Beginning Of Sequence**

Sequence শুরু বোঝাতে ব্যবহৃত হতে পারে।

```text
[BOS] I love Python
```

---

# 29. `[EOS]`

**End Of Sequence**

```text
I love Python [EOS]
```

Sequence শেষ বোঝায়।

---

# 30. `[CLS]`

বিশেষ করে BERT-family model-এ classification-related representation-এর জন্য ব্যবহৃত হয়েছে।

Example:

```text
[CLS] I love Python [SEP]
```

---

# 31. `[SEP]`

Separator token।

একাধিক sequence আলাদা করতে ব্যবহার হতে পারে।

```text
[CLS] Sentence A [SEP] Sentence B [SEP]
```

---

# 32. `[MASK]`

Masked language modeling-এ:

```text
I love [MASK].
```

Model predict করতে পারে:

```text
Python
```

BERT-এর training concept বোঝার জন্য এটি গুরুত্বপূর্ণ।

---

# 33. Padding

ধরো:

```text
Sentence A:
I love Python

Sentence B:
I love natural language processing
```

Token lengths:

```text
3
5
```

Batch:

```text
[ I love Python PAD PAD ]
[ I love natural language processing ]
```

এতে একই sequence length হয়।

---

# 34. Attention Mask

Padding token model-এর actual content নয়।

তাই model-কে জানাতে হয় কোন token valid এবং কোনটি padding।

Example:

```text
Tokens:
[I, love, Python, PAD, PAD]

Mask:
[1, 1, 1, 0, 0]
```

সাধারণভাবে:

```text
1 = attend/use
0 = padding/ignore
```

---

# 35. Truncation

Input অনেক বড় হলে maximum length-এর মধ্যে কাটতে হয়।

Example:

```text
max_length = 5
```

Input:

```text
I love Python because Python is very powerful
```

Truncated:

```text
I love Python because Python
```

এটি **truncation**।

---

# 36. Padding + Truncation

Transformer input preparation-এ প্রায়ই:

```text
Tokenizer
   ↓
Truncation
   ↓
Padding
   ↓
Token IDs
   ↓
Attention Mask
```

ব্যবহার করা হয়।

---

# 37. BPE — Byte Pair Encoding 🔥

এখন modern tokenizer-এর গুরুত্বপূর্ণ algorithm।

**BPE = Byte Pair Encoding**

মূল idea:

> Frequently occurring symbol pairs merge করতে করতে vocabulary তৈরি করা।

ধরো training data:

```text
low
lower
lowest
```

Initial characters:

```text
l o w
l o w e r
l o w e s t
```

Frequent patterns দেখা গেলে:

```text
l + o → lo
lo + w → low
```

তারপর আরও frequent combinations merge হতে পারে।

---

# 38. BPE-এর Basic Idea

Start:

```text
Characters / bytes
```

↓

```text
Frequent pair identify
```

↓

```text
Merge pair
```

↓

```text
Update vocabulary
```

↓

```text
Repeat
```

শেষে:

```text
Subword vocabulary
```

---

# 39. BPE কেন useful?

এটি balance করে:

```text
Word-level
     ↕
Character-level
```

Word-level:

```text
Vocabulary huge
```

Character-level:

```text
Sequence huge
```

Subword:

```text
Reasonable vocabulary
+
Reasonable sequence length
```

---

# 40. WordPiece

WordPiece-ও subword tokenization method।

BERT-family models-এর সঙ্গে এটি খুব পরিচিত।

Conceptually:

```text
playing
```

হতে পারে:

```text
play + ##ing
```

এখানে `##` সাধারণত বোঝায় এটি word-এর continuation।

---

# 41. BPE vs WordPiece

দুটোই subword approach।

Conceptually difference:

```text
BPE
→ frequency-based merge strategy

WordPiece
→ vocabulary/subword selection based on model-oriented objective
```

Implementation details model/tokenizer অনুযায়ী পরিবর্তিত হতে পারে।

---

# 42. Unigram Tokenization

আরেকটি subword approach হলো **Unigram**।

এখানে tokenizer সম্ভাব্য subword pieces-এর vocabulary থেকে sequence-এর জন্য ভালো segmentation নির্বাচন করে।

এটি SentencePiece ecosystem-এ গুরুত্বপূর্ণ।

---

# 43. SentencePiece

SentencePiece একটি tokenizer framework/library approach যা raw text থেকে language-independent subword segmentation করতে পারে।

এটি whitespace-based word splitting-এর উপর পুরোপুরি নির্ভর করে না।

তাই multilingual NLP-তে এটি খুব useful।

---

# 44. Byte-Level Tokenization

কিছু modern tokenizer byte-level approach ব্যবহার করে।

এতে unusual characters, punctuation এবং বিভিন্ন Unicode text handle করার robustness বাড়তে পারে।

Conceptually:

```text
Raw Text
 ↓
Bytes
 ↓
Subword/merge process
 ↓
Tokens
```

---

# 45. Modern LLM Tokenization

একটি simplified view:

```text
User Text
    ↓
Tokenizer
    ↓
Subword / Byte Tokens
    ↓
Token IDs
    ↓
Embedding
    ↓
Transformer
```

এখানে আমরা যে tokenizer ব্যবহার করছি সেটি model architecture-এর সঙ্গে closely connected।

---

# 46. Hugging Face Tokenizer Example

বাস্তবে Transformer model ব্যবহার করার সময় tokenizer library ব্যবহার করব।

উদাহরণ:

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)

text = "I love Python."

tokens = tokenizer.tokenize(text)

print(tokens)
```

Possible output:

```text
['i', 'love', 'python', '.']
```

---

# 47. Token IDs দেখা

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)

text = "I love Python."

encoded = tokenizer(text)

print(encoded["input_ids"])
```

এখানে output হবে integer IDs।

---

# 48. Attention Mask দেখা

```python
encoded = tokenizer(
    "I love Python.",
    padding=True,
    truncation=True
)

print(encoded["input_ids"])
print(encoded["attention_mask"])
```

তুমি সাধারণত এরকম structure দেখতে পারো:

```text
input_ids:
[101, ..., 102]

attention_mask:
[1, ..., 1]
```

Special token IDs model-specific।

---

# 49. Tokens + IDs একসাথে

```python
tokens = tokenizer.tokenize("I love Python.")

ids = tokenizer.convert_tokens_to_ids(tokens)

print(tokens)
print(ids)
```

Pipeline:

```text
"I love Python."
       ↓
["i", "love", "python", "."]
       ↓
[1045, 2293, ...]
```

---

# 50. Decode

Token IDs থেকে আবার text তৈরি করা যায়।

```python
encoded = tokenizer("I love Python.")

decoded = tokenizer.decode(
    encoded["input_ids"]
)

print(decoded)
```

এটি tokenizer-এর inverse direction বোঝায়।

```text
Text
 ↓
Tokenize
 ↓
IDs
 ↓
Decode
 ↓
Text
```

---

# 51. Token Count

LLM application-এ token count খুব গুরুত্বপূর্ণ।

কারণ model-এর:

```text
Context Window
```

token দিয়ে measured হয়।

Example:

```text
Input
 ↓
Tokenizer
 ↓
1000 tokens
```

তাহলে model input length ≈ 1000 tokens।

---

# 52. Word Count ≠ Token Count

এটি অবশ্যই মনে রাখবে।

একটি sentence:

```text
100 words
```

মানে:

```text
100 tokens
```

হতেই হবে এমন নয়।

Subword tokenization-এর কারণে:

```text
100 words
→ 130 tokens
```

হতে পারে।

আবার অন্য text-এ ratio আলাদা হতে পারে।

---

# 53. কেন Token Count গুরুত্বপূর্ণ?

AI writing platform-এ:

```text
User Input
   ↓
Token Count
   ↓
Context Limit
   ↓
Model
```

এছাড়া:

* API usage
* inference cost
* batching
* latency
* maximum input length

এসবের সঙ্গে token count সম্পর্কিত।

---

# 54. Tokenization এবং Context Window

ধরো model-এর maximum:

```text
8192 tokens
```

তোমার input:

```text
10000 tokens
```

তাহলে পুরো input সরাসরি পাঠানো যাবে না।

সম্ভাব্য strategy:

```text
Truncate
অথবা
Chunk
অথবা
Summarize
অথবা
Long-context model
```

---

# 55. Tokenization vs Preprocessing

M02.04-এ আমরা preprocessing শিখেছি।

Difference:

### Preprocessing

```text
"  HELLO!!!   "
```

↓

```text
"hello!!!"
```

### Tokenization

```text
"hello!!!"
```

↓

```text
["hello", "!", "!", "!"]
```

অর্থাৎ:

```text
Preprocessing
     ↓
Tokenization
```

তবে modern Transformer pipeline-এ tokenizer নিজেই কিছু normalization/preprocessing করতে পারে।

---

# 56. Tokenizer ≠ Embedding

খুব important distinction।

### Tokenizer

```text
Text
 ↓
Token IDs
```

### Embedding

```text
Token IDs
 ↓
Vectors
```

Full pipeline:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding Layer
 ↓
Vectors
 ↓
Transformer
```

---

# 57. AI Writing Assistant-এ Tokenization

ধরো user লিখল:

```text
"I think this paragraph can be improved."
```

System:

```text
User Text
    ↓
Preprocessing
    ↓
Tokenizer
    ↓
Tokens
    ↓
Token IDs
    ↓
Embedding
    ↓
Transformer
    ↓
Contextual Representation
    ↓
Rewrite / Analysis
```

এটাই আমাদের future project-এর foundation।

---

# 58. AI Detector-এ Tokenization

একইভাবে:

```text
Input Text
    ↓
Preprocessing
    ↓
Tokenizer
    ↓
Token IDs
    ↓
Transformer / Classifier
    ↓
Features
    ↓
Prediction
```

---

# 59. Important: Tokenization Model-Specific

একটি text:

```text
"unbelievable"
```

Tokenizer A:

```text
["un", "believable"]
```

Tokenizer B:

```text
["un", "believ", "able"]
```

Tokenizer C:

```text
["u", "n", ...]
```

তাই:

> **Tokenization-এর একটাই universal output নেই।**

---

# 60. Tokenization-এর Common Mistakes

### Mistake 1

```python
text.split()
```

কে complete tokenizer মনে করা।

না।

---

### Mistake 2

প্রতিটি word = একটি token ভাবা।

না।

---

### Mistake 3

Token ID-কে semantic value মনে করা।

না।

---

### Mistake 4

সব punctuation remove করে তারপর tokenize করা।

সব task-এ ভালো নয়।

---

### Mistake 5

সব model-এর tokenizer একই মনে করা।

না।

---

# 61. Complete Mental Model 🔥

এটি মুখস্থ না করে বুঝবে:

```text
                 RAW TEXT
                    │
                    ▼
             PREPROCESSING
                    │
                    ▼
                TOKENIZER
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
      TOKENS                 VOCABULARY
        │                       │
        └───────────┬───────────┘
                    ▼
                TOKEN IDs
                    │
                    ▼
                EMBEDDING
                    │
                    ▼
            CONTEXTUAL VECTORS
                    │
                    ▼
               TRANSFORMER
                    │
                    ▼
             OUTPUT / PREDICTION
```

---

# 62. চারটি Tokenization মনে রাখো

```text
Sentence
   ↓
Word
   ↓
Character
   ↓
Subword
```

আর modern LLM-এর ক্ষেত্রে সবচেয়ে গুরুত্বপূর্ণ:

```text
Subword / Byte-level tokenization
```

---

# 63. Hands-on Practice 🔥

### Practice 1 — Word Tokenization

```python
text = "Python is easy to learn."

# তোমার code
```

Expected concept:

```text
["Python", "is", "easy", "to", "learn", "."]
```

---

### Practice 2 — Character Tokenization

```python
text = "NLP"
```

Expected:

```text
["N", "L", "P"]
```

---

### Practice 3 — Sentence Tokenization

Input:

```python
text = """
I love Python.
I am learning NLP.
NLP is interesting!
"""
```

Output:

```text
[
    "I love Python.",
    "I am learning NLP.",
    "NLP is interesting!"
]
```

---

### Practice 4 — Vocabulary

নিজে তৈরি করো:

```python
vocab = {
    "I": 0,
    "love": 1,
    "Python": 2
}
```

তারপর:

```text
"I love Python"
```

কে ID-তে convert করো।

Expected:

```text
[0, 1, 2]
```

---

### Practice 5 — Padding

ধরো:

```text
A = ["I", "love", "Python"]

B = ["I", "love", "NLP", "very", "much"]
```

A-কে B-এর length পর্যন্ত pad করো।

Expected:

```text
["I", "love", "Python", "[PAD]", "[PAD]"]
```

---

# 64. Mini Project — Simple Tokenizer

নিজে এই class বানানোর চেষ্টা করো:

```python
class SimpleTokenizer:

    def __init__(self):
        self.vocab = {}
        self.inverse_vocab = {}

    def build_vocab(self, texts):
        pass

    def tokenize(self, text):
        pass

    def encode(self, text):
        pass

    def decode(self, ids):
        pass
```

Target:

```text
Text
 ↓
Tokenize
 ↓
Vocabulary
 ↓
Encode
 ↓
Decode
```

এটি তোমার NLP foundation-এর জন্য খুব গুরুত্বপূর্ণ exercise।

---

# 65. Theory Questions

নিজে answer করার চেষ্টা করো:

1. Tokenization কী?
2. Token কী?
3. Word এবং token-এর difference কী?
4. Sentence tokenization কী?
5. Word tokenization কী?
6. Character tokenization কী?
7. Subword tokenization কী?
8. Subword কেন দরকার?
9. Vocabulary কী?
10. Token ID কী?
11. Token ID কি semantic meaning বহন করে?
12. `[PAD]` কী?
13. `[UNK]` কী?
14. `[BOS]` কী?
15. `[EOS]` কী?
16. `[CLS]` কী?
17. `[SEP]` কী?
18. `[MASK]` কী?
19. Padding কী?
20. Truncation কী?
21. Attention mask কী?
22. BPE কী?
23. WordPiece কী?
24. Unigram কী?
25. SentencePiece কী?
26. Tokenizer এবং embedding-এর difference কী?
27. Word count এবং token count কেন আলাদা?
28. Context window-এর সঙ্গে tokenization-এর সম্পর্ক কী?
29. কেন tokenizer model-specific?
30. Transformer model-এ tokenizer-এর role কী?

---

# 66. Interview Questions

### Beginner

* What is tokenization?
* What is a token?
* What is word tokenization?
* What is sentence tokenization?
* What is vocabulary?

### Intermediate

* What is subword tokenization?
* Why is subword tokenization useful?
* What is BPE?
* What is WordPiece?
* What is padding?
* What is truncation?
* What is attention mask?

### Advanced

* Why do modern LLMs use subword/byte-level tokenization?
* Why is word-level tokenization problematic for rare words?
* What is the difference between BPE and WordPiece?
* Why does token count matter for LLM applications?
* Why can two tokenizers produce different token counts?
* Why should tokenizer and model usually be paired?
* What happens from raw text to transformer input?

---

# 67. M02.05 Completion Checklist

```text
[x] Tokenization
[x] Token
[x] Word vs Token
[x] Sentence Tokenization
[x] Sentence Segmentation
[x] Word Tokenization
[x] Character Tokenization
[x] Subword Tokenization
[x] Vocabulary
[x] Token ID
[x] Special Tokens
[x] [PAD]
[x] [UNK]
[x] [BOS]
[x] [EOS]
[x] [CLS]
[x] [SEP]
[x] [MASK]
[x] Padding
[x] Truncation
[x] Attention Mask
[x] BPE
[x] WordPiece
[x] Unigram
[x] SentencePiece
[x] Byte-level Tokenization
[x] Token Count
[x] Context Window
[x] Tokenizer vs Embedding
[x] Classical vs Modern Tokenization
[x] Transformer Tokenization
[x] AI Writing Assistant application
[x] AI Detector application
```

## 🧠 সবচেয়ে গুরুত্বপূর্ণ ৩টা জিনিস

এগুলো অবশ্যই পরিষ্কার থাকতে হবে:

```text
1. Text
      ↓
   Tokenizer
      ↓
   Token IDs

2. Token IDs
      ↓
   Embedding
      ↓
   Vectors

3. Word ≠ Token
```

আর পুরো pipeline:

```text
RAW TEXT
   ↓
PREPROCESSING
   ↓
TOKENIZATION
   ↓
TOKEN IDs
   ↓
EMBEDDINGS
   ↓
TRANSFORMER
   ↓
OUTPUT
```

**M02.05 complete.**

পরের lesson: **M02.06 — Stopwords** — stopword কী, কেন ব্যবহার করা হয়, কখন remove করা উচিত/উচিত নয়, English stopwords, custom stopwords, NLP model-এর উপর effect, এবং AI writing system-এ stopword handling।

----
# M02.06 — Stopwords 🔥

আজ আমরা NLP-এর একটি খুব গুরুত্বপূর্ণ classical NLP concept শিখব: **Stopwords**।

তবে শুধু “stopword remove করা” শিখলে হবে না। আমরা বুঝব:

* Stopword কী
* কেন stopword বলা হয়
* Common English stopwords
* Stopword removal
* Stopword রাখা বনাম বাদ দেওয়া
* Meaning-এর উপর impact
* Negation problem
* Custom stopwords
* Domain-specific stopwords
* Stopwords এবং tokenization-এর relation
* TF-IDF-এর সঙ্গে relation
* Classical ML বনাম Transformer
* AI writing assistant-এ stopword handling

---

# 1. Stopword কী?

**Stopwords** হলো এমন common words যেগুলো একটি NLP task-এর জন্য অনেক সময় কম informative মনে করা হয়।

Example:

```text
I am learning Python
```

Possible stopwords:

```text
I
am
```

Content words:

```text
learning
Python
```

আরও common examples:

```text
the
a
an
is
am
are
was
were
to
of
in
on
for
and
or
but
```

---

# 2. কেন এগুলোকে Stopwords বলা হয়?

Classical NLP-এর সময় দেখা যায় কিছু word dataset-এ খুব বেশি frequency-তে থাকে।

যেমন:

```text
the
is
a
of
and
```

এগুলো অনেক sentence-এ থাকে।

কিন্তু অনেক classification task-এ এগুলো আলাদা করার power কম হতে পারে।

তাই computational efficiency এবং feature reduction-এর জন্য কিছু common words বাদ দেওয়া হতো।

---

# 3. Example

ধরো:

```text
The cat is sitting on the table.
```

Stopwords বাদ দিলে:

```text
cat sitting table
```

এখানে content words বেশি prominent হয়ে যায়।

---

# 4. Common English Stopwords

একটি ছোট list:

```python
stopwords = {
    "a",
    "an",
    "the",
    "is",
    "am",
    "are",
    "was",
    "were",
    "be",
    "been",
    "being",
    "and",
    "or",
    "but",
    "if",
    "in",
    "on",
    "at",
    "to",
    "of",
    "for",
    "with"
}
```

এটি শুধু example list।

বাস্তব library-এর stopword list অনেক বড় হতে পারে।

---

# 5. Python দিয়ে Stopword Removal

```python
text = "I am learning Python and NLP"

stopwords = {
    "i", "am", "and"
}

tokens = text.lower().split()

filtered_tokens = [
    word
    for word in tokens
    if word not in stopwords
]

print(filtered_tokens)
```

Output:

```text
['learning', 'python', 'nlp']
```

---

# 6. Sentence থেকে Stopwords Remove

```python
text = "Python is a very useful programming language"

stopwords = {
    "is", "a", "very"
}

tokens = text.lower().split()

filtered = [
    word for word in tokens
    if word not in stopwords
]

result = " ".join(filtered)

print(result)
```

Output:

```text
python useful programming language
```

---

# 7. কিন্তু Stopword Removal সবসময় ভালো নয় ❗

এটাই আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়।

ধরো:

```text
I do not like this movie.
```

যদি stopword removal করি এবং:

```text
do
not
```

বাদ দিই:

```text
I like this movie
```

Meaning সম্পূর্ণ পরিবর্তিত হয়ে গেল।

Original:

```text
I do not like this movie.
```

Meaning:

```text
Negative
```

After bad preprocessing:

```text
I like this movie.
```

Meaning:

```text
Positive
```

তাই:

> **Stopword removal can destroy important information.**

---

# 8. Negation Words খুব গুরুত্বপূর্ণ

বিশেষ করে:

```text
not
no
never
neither
nor
n't
```

এগুলো অনেক NLP task-এ গুরুত্বপূর্ণ।

Example:

```text
good
```

vs

```text
not good
```

দুটোর meaning আলাদা।

তাই sentiment analysis-এর মতো task-এ সাধারণত negation carefully handle করতে হয়।

---

# 9. আরেকটি Example

```text
This product is not useful.
```

Bad stopword removal:

```text
product useful
```

Meaning:

```text
Positive-ish
```

Original:

```text
product is not useful
```

Meaning:

```text
Negative
```

---

# 10. Stopwords Context-dependent

একটি word এক task-এ useless হতে পারে, অন্য task-এ useful।

Example:

```text
to
```

একটি সাধারণ classification task-এ কম useful হতে পারে।

কিন্তু linguistic analysis-এ:

```text
I want to go.
```

এখানে `to` grammatical information বহন করছে।

---

# 11. Search Engine-এর ক্ষেত্রে

পুরনো search systems-এ stopword removal ব্যবহার করা হতো:

```text
the
is
a
of
```

ইত্যাদি বাদ দিয়ে search efficiency বাড়ানোর জন্য।

কিন্তু modern search systems অনেক বেশি sophisticated।

তাই traditional stopword rules blindly apply করা ঠিক নয়।

---

# 12. Stopwords + Tokenization

আগে আমরা tokenization শিখেছি।

Pipeline:

```text
Raw Text
   ↓
Preprocessing
   ↓
Tokenization
   ↓
Stopword Handling
```

Example:

```text
"The cat is sleeping."
```

Tokens:

```python
["the", "cat", "is", "sleeping"]
```

তারপর stopword removal:

```python
["cat", "sleeping"]
```

---

# 13. Stopword Removal আগে নাকি পরে?

সাধারণ conceptual pipeline:

```text
Text
 ↓
Normalize
 ↓
Tokenize
 ↓
Stopword Handling
 ↓
Feature Extraction
```

কারণ stopword শনাক্ত করার জন্য সাধারণত token-level information দরকার।

---

# 14. Stopword List কী?

Stopword list হলো predefined words-এর collection।

Example:

```python
stopwords = {
    "the",
    "is",
    "a",
    "an",
    "of"
}
```

তারপর:

```python
if token not in stopwords:
```

ব্যবহার করা হয়।

---

# 15. Library দিয়ে Stopwords

NLP শেখার সময় **NLTK**-তে stopword corpus খুব পরিচিত।

Conceptual example:

```python
from nltk.corpus import stopwords

stop_words = set(
    stopwords.words("english")
)
```

তারপর:

```python
tokens = ["this", "is", "a", "test"]

filtered = [
    word
    for word in tokens
    if word not in stop_words
]

print(filtered)
```

---

# 16. Stopword List Install

NLTK ব্যবহার করলে stopword data আলাদাভাবে download করতে হতে পারে।

```python
import nltk

nltk.download("stopwords")
```

তারপর:

```python
from nltk.corpus import stopwords

stop_words = set(
    stopwords.words("english")
)

print(len(stop_words))
```

---

# 17. spaCy

spaCy-তেও token-এর stopword property আছে।

Conceptually:

```python
import spacy

nlp = spacy.load("en_core_web_sm")

doc = nlp("This is a simple sentence.")

for token in doc:
    print(token.text, token.is_stop)
```

Possible output:

```text
This True
is True
a True
simple False
sentence False
. False
```

---

# 18. Custom Stopwords

নিজের project-এর জন্য নিজের stopword list বানাতে পারো।

Example:

```python
stopwords = {
    "the",
    "is",
    "a",
    "this"
}
```

তারপর:

```python
stopwords.update({
    "example",
    "website"
})
```

---

# 19. Domain-specific Stopwords

এটি real-world NLP-তে খুব গুরুত্বপূর্ণ।

ধরো তুমি একটি **news classification system** বানাচ্ছ।

Dataset-এর প্রতিটি document-এ প্রায় সবসময়:

```text
news
report
according
said
```

থাকতে পারে।

তখন task-এর জন্য এগুলোর information value কম হতে পারে।

তুমি domain-specific stopword list তৈরি করতে পারো।

---

# 20. AI Writing Assistant-এর ক্ষেত্রে

আমাদের target system:

```text
User Text
   ↓
Preprocessing
   ↓
Tokenization
   ↓
NLP Analysis
```

এখানে সাধারণ stopword removal **সবসময় করা উচিত নয়**।

কারণ writing assistant-এ:

```text
grammar
syntax
style
tone
meaning
sentence structure
```

গুরুত্বপূর্ণ।

আর function words:

```text
is
are
the
to
of
not
```

sentence structure-এর গুরুত্বপূর্ণ অংশ।

---

# 21. AI Detector-এর ক্ষেত্রে

আরও গুরুত্বপূর্ণ।

ধরো detector text-এর linguistic patterns analyse করছে।

যদি তুমি সব common words remove করো:

```text
The student is writing a paragraph.
```

থেকে:

```text
student writing paragraph
```

তাহলে:

* sentence structure হারাবে
* function-word usage হারাবে
* grammatical patterns হারাবে
* original style signal হারাতে পারে

তাই AI writing analysis-এর মতো task-এ aggressive stopword removal অনেক সময় **খারাপ idea**।

---

# 22. TF-IDF-এর সঙ্গে Stopwords

Classical NLP-তে আমরা পরে **TF-IDF** শিখব।

TF-IDF-এর idea:

```text
TF = Term Frequency
IDF = Inverse Document Frequency
```

যে word প্রায় সব document-এ থাকে, তার IDF কম হয়।

Example:

```text
the
is
and
```

অনেক document-এ থাকলে:

```text
low IDF
```

তাই কিছু ক্ষেত্রে TF-IDF model নিজেই common words-কে relatively কম weight দেয়।

এ কারণে stopword removal সবসময় প্রয়োজন হয় না।

---

# 23. Stopword Removal-এর Benefits

কখনো useful হতে পারে:

### 1. Vocabulary reduction

```text
Large vocabulary
       ↓
Remove common words
       ↓
Smaller vocabulary
```

### 2. Feature reduction

কম features:

```text
Less memory
Less computation
```

### 3. Classical ML efficiency

বিশেষ করে:

```text
Bag of Words
TF-IDF
```

এর মতো sparse representation-এর ক্ষেত্রে feature count কমানো useful হতে পারে।

---

# 24. Stopword Removal-এর Problems

### Problem 1 — Meaning loss

```text
not good
```

→

```text
good
```

### Problem 2 — Grammar loss

```text
I am learning Python.
```

→

```text
learning Python
```

### Problem 3 — Sentence structure loss

```text
The boy is not happy.
```

→

```text
boy happy
```

### Problem 4 — Context loss

Function words অনেক সময় context-এর অংশ।

---

# 25. Stopwords Remove করার আগে প্রশ্ন করো

প্রথমে জিজ্ঞেস করবে:

```text
What is my task?
```

তারপর:

```text
Do these words contain useful information?
```

তারপর:

```text
Does my model need syntax/context?
```

তারপর সিদ্ধান্ত:

```text
Keep
Remove
or
Selective Removal
```

---

# 26. Three Strategies

Stopword handling-এর তিনটি strategy:

### Strategy 1 — Remove all

```text
the → removed
is → removed
a → removed
```

Simple কিন্তু risky।

---

### Strategy 2 — Keep all

কোনো stopword remove না করা।

Modern NLP/Transformer-এর ক্ষেত্রে এটি খুব common choice।

---

### Strategy 3 — Selective removal

কিছু stopword remove করো কিন্তু important words রাখো।

Example:

```python
stopwords = {
    "the",
    "a",
    "an",
    "is",
    "am",
    "are"
}

important = {
    "not",
    "never",
    "no"
}
```

তারপর:

```python
if token in important:
    keep
```

---

# 27. Negation-aware Stopword Removal

একটি basic implementation:

```python
stopwords = {
    "the",
    "a",
    "an",
    "is",
    "am",
    "are",
    "was",
    "were",
    "and",
    "or"
}

negations = {
    "not",
    "no",
    "never"
}

tokens = [
    "this",
    "is",
    "not",
    "good"
]

filtered = [
    token
    for token in tokens
    if token not in stopwords
    or token in negations
]

print(filtered)
```

Output:

```text
['this', 'not', 'good']
```

এখানে `not` সংরক্ষিত হয়েছে।

---

# 28. Stopword Removal Function

```python
def remove_stopwords(tokens, stopwords):
    return [
        token
        for token in tokens
        if token.lower() not in stopwords
    ]
```

Example:

```python
tokens = [
    "I",
    "am",
    "learning",
    "Python"
]

stopwords = {
    "i",
    "am"
}

result = remove_stopwords(
    tokens,
    stopwords
)

print(result)
```

Output:

```text
['learning', 'Python']
```

---

# 29. Better Version

Case normalization আগে করলে comparison reliable হয়।

```python
def remove_stopwords(tokens, stopwords):

    stopwords = {
        word.lower()
        for word in stopwords
    }

    return [
        token
        for token in tokens
        if token.lower() not in stopwords
    ]
```

---

# 30. Keep Negation

আরও useful:

```python
def remove_stopwords(tokens, stopwords, keep_words=None):

    stopwords = {
        word.lower()
        for word in stopwords
    }

    keep_words = {
        word.lower()
        for word in (keep_words or set())
    }

    result = []

    for token in tokens:

        word = token.lower()

        if word in keep_words:
            result.append(token)

        elif word not in stopwords:
            result.append(token)

    return result
```

Usage:

```python
stopwords = {
    "the",
    "is",
    "a",
    "an",
    "and"
}

keep_words = {
    "not",
    "never"
}

tokens = [
    "This",
    "is",
    "not",
    "a",
    "good",
    "product"
]

result = remove_stopwords(
    tokens,
    stopwords,
    keep_words
)

print(result)
```

Output:

```text
['This', 'not', 'good', 'product']
```

---

# 31. Stopwords এবং Lemmatization

ধরো:

```text
The cats are running.
```

Pipeline হতে পারে:

```text
Tokenization
 ↓
Stopword Handling
 ↓
Lemmatization
```

Result:

```text
cats → cat
running → run
```

Potential output:

```text
cat run
```

কিন্তু modern NLP-তে exact pipeline task/model অনুযায়ী পরিবর্তিত হতে পারে।

---

# 32. Stopwords এবং Stemming

Example:

```text
The players are playing football.
```

Stopword removal:

```text
players playing football
```

Stemming:

```text
player play football
```

Possible classical pipeline:

```text
Raw Text
 ↓
Tokenization
 ↓
Stopword Removal
 ↓
Stemming
 ↓
Features
```

---

# 33. Modern Transformer-এ Stopword Removal

এখানে খুব গুরুত্বপূর্ণ:

**Transformer model-এর আগে manually সব stopword remove করা সাধারণত দরকার হয় না।**

কারণ transformer:

```text
the
is
a
to
not
```

সহ পুরো sequence-এর context ব্যবহার করে।

Example:

```text
The cat is not happy.
```

Transformer-এর জন্য:

```text
The
cat
is
not
happy
```

সবগুলো token context তৈরি করতে সাহায্য করতে পারে।

---

# 34. কেন Function Words গুরুত্বপূর্ণ?

Function words:

```text
the
is
to
of
and
```

semantic content কম হলেও:

* syntax
* grammatical relationship
* sentence structure
* dependency
* style

বোঝাতে সাহায্য করতে পারে।

AI writing analysis-এ এগুলো বিশেষভাবে useful হতে পারে।

---

# 35. Stopword Frequency

ধরো dataset:

```text
1000 documents
```

`the` আছে:

```text
950 documents
```

তাহলে:

```text
document frequency = 950
```

অর্থাৎ খুব common।

অন্যদিকে:

```text
Python
```

আছে:

```text
100 documents
```

তাহলে `Python` comparatively more discriminative হতে পারে।

এটাই TF-IDF-এর intuition-এর সঙ্গে related।

---

# 36. Stopword Removal Decision Table

| Task                         | Stopword Removal  |
| ---------------------------- | ----------------- |
| Basic keyword extraction     | কখনো useful       |
| Simple TF-IDF classification | useful হতে পারে   |
| Search preprocessing         | task-dependent    |
| Sentiment analysis           | সতর্ক             |
| Negation analysis            | সাধারণত selective |
| Grammar analysis             | avoid             |
| POS tagging                  | avoid             |
| Dependency parsing           | avoid             |
| Text generation              | avoid             |
| Transformer classification   | সাধারণত avoid     |
| AI writing analysis          | সাধারণত avoid     |

---

# 37. একটি গুরুত্বপূর্ণ Rule

```text
Classical NLP
    ↓
Stopword removal may help
```

কিন্তু:

```text
Modern NLP / Transformer
    ↓
Usually preserve the original linguistic context
```

এটি absolute rule নয়, কিন্তু ভালো starting principle।

---

# 38. Stopword ≠ Useless Word

এটি অবশ্যই মনে রাখবে।

**Stopword মানে word-টি inherently useless নয়।**

বরং:

> নির্দিষ্ট NLP task-এর জন্য word-টির information value কম হতে পারে।

Example:

```text
not
```

এক task-এ critical।

অন্য task-এ less important হতে পারে।

---

# 39. Bangla NLP-এর ক্ষেত্রে

Bangla-তেও common function words আছে:

```text
এবং
কিন্তু
এই
সে
আমি
তুমি
হয়
হয়
এর
কে
তে
```

কিন্তু English stopword list Bangla text-এর জন্য ব্যবহার করা যাবে না।

Language-specific stopword list প্রয়োজন।

আর Bangla NLP-তে:

* inflection
* spelling variation
* Unicode
* tokenization
* যৌগিক শব্দ
* clitic-like forms

ইত্যাদি বিষয়ও consideration-এ আসে।

---

# 40. Stopword List নিজে বানানো

ধরো তোমার dataset:

```python
texts = [
    "Python is easy",
    "Python is powerful",
    "Python is popular"
]
```

Common words:

```text
Python
is
```

Task অনুযায়ী `is` stopword হতে পারে।

কিন্তু `Python` যদি classification-এর গুরুত্বপূর্ণ feature হয়, তাহলে অবশ্যই রাখতে হবে।

---

# 41. AI Writing Project-এ Best Practice

আমাদের future system-এর জন্য:

```text
Original Text
       ↓
 Preserve
       │
       ├──→ User Display
       │
       └──→ Analysis Pipeline
```

Analysis pipeline-এ:

```text
Original
 ↓
Light Normalization
 ↓
Tokenizer
 ↓
Features
```

এখানে defaultভাবে:

```text
❌ Remove every stopword
```

না করে:

```text
✅ Preserve linguistic context
```

করাই বেশি sensible।

---

# 42. Complete Pipeline

Classical:

```text
RAW TEXT
   ↓
CLEANING
   ↓
TOKENIZATION
   ↓
STOPWORD REMOVAL
   ↓
STEMMING / LEMMATIZATION
   ↓
TF-IDF
   ↓
ML MODEL
```

Modern:

```text
RAW TEXT
   ↓
LIGHT PREPROCESSING
   ↓
TOKENIZER
   ↓
TOKEN IDs
   ↓
EMBEDDINGS
   ↓
TRANSFORMER
   ↓
OUTPUT
```

---

# 43. Mini Practice 🔥

### Task 1

Input:

```python
text = "This is a simple NLP example"
```

Stopwords:

```python
{"this", "is", "a"}
```

Expected:

```text
simple NLP example
```

---

### Task 2

Input:

```text
I do not like this product.
```

এমন stopword filter বানাও যাতে:

```text
not
```

remove না হয়।

Expected concept:

```text
I not like product
```

---

### Task 3

এই sentence-এর stopwords identify করো:

```text
The boy is playing in the garden.
```

সম্ভাব্য:

```text
the
is
in
the
```

---

# 44. Mini Project

একটি function বানাও:

```python
def preprocess_tokens(
    tokens,
    stopwords,
    keep_words=None
):
    ...
```

যেটা:

1. lowercase comparison করবে
2. stopwords remove করবে
3. `not`, `never`, `no` preserve করবে
4. original token list modify করবে না
5. নতুন list return করবে

Example:

```python
tokens = [
    "The",
    "movie",
    "is",
    "not",
    "very",
    "good"
]
```

Expected:

```text
["movie", "not", "good"]
```

---

# 45. Theory Questions

নিজে answer করার চেষ্টা করো:

1. Stopword কী?
2. কেন stopword ব্যবহার করা হয়?
3. পাঁচটি English stopword-এর নাম বলো।
4. Stopword removal কী?
5. Stopword removal-এর সুবিধা কী?
6. Stopword removal-এর অসুবিধা কী?
7. `not` কেন গুরুত্বপূর্ণ?
8. Negation কী?
9. সব stopword কি সব task-এ একই?
10. Custom stopword কী?
11. Domain-specific stopword কী?
12. Stopword এবং tokenization-এর relationship কী?
13. Stopword removal এবং TF-IDF-এর relationship কী?
14. Transformer model-এ stopword removal কেন সাধারণত প্রয়োজন হয় না?
15. Function words কেন গুরুত্বপূর্ণ?
16. Word frequency এবং stopword-এর relation কী?
17. Bangla NLP-তে English stopword list কেন ব্যবহার করা যাবে না?
18. Stopword কি inherently useless?
19. AI writing assistant-এ stopword removal করা উচিত কি?
20. AI detector-এ stopword removal করলে কী ধরনের information loss হতে পারে?

---

# 46. Interview Questions

### Beginner

* What are stopwords?
* Why are stopwords removed?
* Give examples of stopwords.
* What is stopword removal?

### Intermediate

* What are the advantages of stopword removal?
* What are the disadvantages?
* How would you create a custom stopword list?
* Why should negation words sometimes be preserved?

### Advanced

* Should stopwords be removed before Transformer models?
* How can stopword removal affect sentiment analysis?
* Why can function words be useful for linguistic analysis?
* How does stopword removal interact with TF-IDF?
* Why is stopword removal task-dependent?
* Why might stopword removal be harmful for an AI writing analysis system?

---

# 47. M02.06 Completion Checklist

```text
[x] Stopword definition
[x] Common English stopwords
[x] Stopword list
[x] Stopword removal
[x] Python implementation
[x] NLTK concept
[x] spaCy concept
[x] Custom stopwords
[x] Domain-specific stopwords
[x] Stopword + Tokenization
[x] Stopword + TF-IDF
[x] Stopword + Stemming
[x] Stopword + Lemmatization
[x] Negation
[x] Negation-aware filtering
[x] Function words
[x] Vocabulary reduction
[x] Feature reduction
[x] Meaning loss
[x] Grammar loss
[x] Classical NLP
[x] Modern Transformer NLP
[x] Bangla NLP consideration
[x] AI Writing Assistant application
[x] AI Detector application
```

## 🧠 Final Mental Model

সবচেয়ে গুরুত্বপূর্ণভাবে এটা বুঝবে:

```text
              STOPWORD
                  │
       ┌──────────┴──────────┐
       ▼                     ▼
  Classical NLP        Modern NLP
       │                     │
       ▼                     ▼
May remove            Usually preserve
       │                     │
       ▼                     ▼
TF-IDF / BoW          Transformer
       │                     │
       ▼                     ▼
Feature reduction     Context preservation
```

আর সবচেয়ে গুরুত্বপূর্ণ rule:

> **Stopword = “always useless” নয়। Stopword = task-dependent low-information word.**

**M02.06 complete.**

পরের lesson হবে **M02.07 — Stemming**, যেখানে আমরা **stem কী, stemming কীভাবে কাজ করে, Porter Stemmer, Snowball Stemmer, Lancaster Stemmer, over-stemming, under-stemming, stemming বনাম lemmatization, এবং real NLP project-এ কখন stemming ব্যবহার করা উচিত**—সব foundation থেকে শিখব।


---
# M02.07 — Stemming 🔥

আজ আমরা NLP-এর আরেকটি গুরুত্বপূর্ণ **Text Normalization** technique শিখব: **Stemming**।

এখানে শুধু definition জানলেই হবে না। আমরা দেখব:

```text
Stemming
├── Stem কী?
├── Stemming কী?
├── কেন Stemming?
├── Root Word vs Stem
├── Rule-based Stemming
├── Porter Stemmer
├── Snowball Stemmer
├── Lancaster Stemmer
├── Over-stemming
├── Under-stemming
├── Stemming vs Lemmatization
├── Python Implementation
├── NLTK
├── কখন ব্যবহার করব
└── AI/NLP Project-এ ব্যবহার
```

---

# 1. Stem কী?

**Stem** হলো কোনো word-এর এমন একটি base-like form যেটি related word-গুলোর common অংশ হিসেবে ব্যবহৃত হয়।

Example:

```text
playing
played
plays
player
```

এগুলোর stem হতে পারে:

```text
play
```

আর:

```text
connected
connecting
connection
```

এগুলোর ক্ষেত্রে stemming algorithm কোনো common shortened form বের করতে পারে।

কিন্তু গুরুত্বপূর্ণ:

> **Stem সবসময় dictionary-এর valid English word হতে হবে না।**

---

# 2. Stemming কী?

**Stemming** হলো algorithm ব্যবহার করে word-এর suffix/prefix-এর মতো অংশ কেটে একটি reduced form বা stem তৈরি করার process।

Example:

```text
playing
   ↓
play
```

```text
played
   ↓
play
```

```text
studies
   ↓
studi
```

শেষের example খুব গুরুত্বপূর্ণ।

`studi` dictionary word নয়, কিন্তু একটি stemming algorithm এটাকে stem হিসেবে দিতে পারে।

---

# 3. কেন Stemming দরকার?

ধরো dataset-এ আছে:

```text
play
plays
played
playing
player
```

Machine যদি প্রতিটাকে আলাদা feature হিসেবে দেখে:

```text
play
plays
played
playing
player
```

তাহলে vocabulary বড় হবে।

Stemming করলে related forms reduce করা যায়:

```text
play
play
play
play
play
```

ফলে:

```text
Vocabulary reduction
+
Feature normalization
```

হতে পারে।

---

# 4. একটি সহজ Example

Input:

```text
The players are playing football.
```

Tokens:

```text
["The", "players", "are", "playing", "football"]
```

Stemming-এর পরে একটি algorithm দিতে পারে:

```text
["the", "player", "are", "play", "footbal"]
```

খেয়াল করো:

```text
players → player
playing → play
football → footbal
```

শেষেরটি দেখতে অদ্ভুত।

এটাই stemming-এর একটি limitation।

---

# 5. Stemming কি Word Meaning বুঝে?

সাধারণ stemming algorithm সাধারণত deep semantic understanding করে না।

এটি মূলত rules/pattern-এর ভিত্তিতে word কাটে।

Simplified example:

```text
playing
   ↓
remove "ing"
   ↓
play
```

অর্থাৎ:

```text
Stemming ≠ Understanding
```

---

# 6. Simple Custom Stemmer

শুধু concept বোঝার জন্য একটি খুব basic stemmer:

```python
def simple_stem(word):
    suffixes = [
        "ing",
        "ed",
        "ly",
        "es",
        "s"
    ]

    for suffix in suffixes:
        if word.endswith(suffix):
            return word[:-len(suffix)]

    return word
```

Test:

```python
words = [
    "playing",
    "played",
    "quickly",
    "cats"
]

for word in words:
    print(word, "→", simple_stem(word))
```

Possible output:

```text
playing → play
played → play
quickly → quick
cats → cat
```

---

# 7. কিন্তু Simple Stemmer-এর সমস্যা আছে

ধরো:

```text
analysis
```

আমাদের simple rule:

```text
"s" remove
```

করলে:

```text
analysi
```

হয়ে যেতে পারে।

আবার:

```text
business
```

→

```text
busines
```

হতে পারে।

তাই real NLP-তে sophisticated stemming algorithms ব্যবহার করা হয়।

---

# 8. Rule-Based Stemming

Traditional stemming algorithms সাধারণত predefined linguistic rules ব্যবহার করে।

Concept:

```text
Word
 ↓
Check suffix
 ↓
Apply rule
 ↓
Remove/reduce ending
 ↓
Stem
```

Example:

```text
playing
 ↓
"ing" detect
 ↓
remove
 ↓
play
```

---

# 9. Porter Stemmer 🔥

সবচেয়ে পরিচিত classical stemming algorithms-এর একটি হলো:

**Porter Stemmer**

এটি Martin Porter-এর stemming algorithm।

এটি English words-এর suffix নিয়ে বিভিন্ন rules প্রয়োগ করে।

Example:

```text
caresses
ponies
cats
running
```

এসবকে reduced forms-এ নিয়ে আসতে পারে।

---

# 10. NLTK দিয়ে Porter Stemmer

প্রথমে:

```python
from nltk.stem import PorterStemmer
```

তারপর:

```python
stemmer = PorterStemmer()
```

ব্যবহার:

```python
words = [
    "playing",
    "played",
    "plays",
    "cats",
    "studies"
]

for word in words:
    print(word, "→", stemmer.stem(word))
```

Output algorithm/version অনুযায়ী হবে, কিন্তু conceptually:

```text
playing → play
played → play
plays → play
cats → cat
studies → studi
```

---

# 11. `studi` কেন?

এটা নতুন learner-দের সবচেয়ে common confusion।

তুমি ভাবতে পারো:

```text
studies → study
```

কিন্তু Porter Stemmer necessarily dictionary-based linguistic reasoning করে না।

এটি rule apply করে:

```text
studies
   ↓
studi
```

তাই:

> **Stem ≠ Lemma**

এই difference খুব ভালোভাবে মনে রাখতে হবে।

---

# 12. Snowball Stemmer

**Snowball Stemmer** একটি improved/modernized stemming framework এবং এতে বিভিন্ন language-এর stemming algorithms পাওয়া যায়।

NLTK:

```python
from nltk.stem import SnowballStemmer
```

English:

```python
stemmer = SnowballStemmer("english")
```

Example:

```python
words = [
    "playing",
    "played",
    "plays",
    "studies",
    "running"
]

for word in words:
    print(word, "→", stemmer.stem(word))
```

---

# 13. Porter বনাম Snowball

সাধারণভাবে:

```text
Porter
 ↓
Classic English stemmer
```

আর:

```text
Snowball
 ↓
Stemming framework
 ↓
Multiple languages
```

Snowball-এর English stemmer Porter-এর তুলনায় revised/improved algorithm হিসেবে পরিচিত।

---

# 14. Lancaster Stemmer

আরেকটি algorithm:

**Lancaster Stemmer**

NLTK:

```python
from nltk.stem import LancasterStemmer

stemmer = LancasterStemmer()
```

Example:

```python
words = [
    "playing",
    "played",
    "player",
    "running"
]

for word in words:
    print(word, "→", stemmer.stem(word))
```

---

# 15. Lancaster বেশি Aggressive হতে পারে

ধরো:

```text
friendship
```

একটি aggressive stemmer এটাকে অনেক বেশি কাটতে পারে।

এতে related words একসঙ্গে চলে আসতে পারে, কিন্তু কখনো meaning-related distinction হারাতে পারে।

এটাকে আমরা বলব:

**Over-stemming**

---

# 16. Over-Stemming 🔥

যখন stemming algorithm **ভিন্ন অর্থের words-কে ভুলভাবে একই stem-এর কাছাকাছি নিয়ে আসে**, তখন তাকে over-stemming বলা হয়।

Conceptual example:

```text
university
universe
```

যদি কোনো algorithm অতিরিক্ত কাটে এবং কাছাকাছি stem তৈরি করে, তাহলে semantic distinction হারাতে পারে।

আরেকটি classic conceptual case:

```text
generously
generation
```

ভুল aggressive stemming related না হওয়া words-কে কাছাকাছি করতে পারে।

---

# 17. Under-Stemming

এর বিপরীত:

**Under-stemming**

যখন related words যথেষ্ট reduce হয় না।

Example:

```text
connect
connected
connection
```

যদি algorithm এগুলোকে:

```text
connect
connect
connecti
```

এর মতো আলাদা রাখে, তাহলে normalization পুরোপুরি সফল হয়নি।

অর্থাৎ:

```text
Over-stemming
→ Too much reduction

Under-stemming
→ Too little reduction
```

---

# 18. Stemming-এর Core Goal

মূল লক্ষ্য:

```text
Related word forms
       ↓
Common representation
```

যেমন:

```text
connect
connected
connecting
```

↓

```text
connect
```

এতে feature space compact হতে পারে।

---

# 19. Stemming vs Root Word

এখানে খুব গুরুত্বপূর্ণ distinction।

### Root

একটি linguistic/morphological concept।

### Stem

Inflectional/derivational processing-এর পরে পাওয়া base-like form।

Example:

```text
studies
```

Stemming:

```text
studi
```

কিন্তু linguistic root/base:

```text
study
```

তাই:

```text
Stem ≠ Root
```

সব ক্ষেত্রে exact linguistic root পাওয়া যায় না।

---

# 20. Stemming vs Lemmatization 🔥🔥

এটি অবশ্যই পরিষ্কার থাকতে হবে।

### Stemming

```text
playing
 ↓
play
```

rules দিয়ে word কাটে।

### Lemmatization

```text
playing
 ↓
play
```

কিন্তু lemmatization linguistic information ব্যবহার করে valid dictionary base form বা **lemma** বের করার চেষ্টা করে।

আর:

```text
studies
```

Stemming:

```text
studi
```

Lemmatization:

```text
study
```

---

# 21. Another Example

```text
better
```

Stemming সাধারণ suffix rules দিয়ে:

```text
better
```

রেখে দিতে পারে।

কিন্তু linguistic lemmatization জানলে:

```text
better → good
```

হতে পারে, যদি appropriate lexical/pos context available থাকে।

এখানে দেখা যাচ্ছে:

```text
Lemmatization
→ linguistic knowledge বেশি ব্যবহার করে
```

---

# 22. Stemming বনাম Lemmatization Table

| Feature    | Stemming         | Lemmatization            |
| ---------- | ---------------- | ------------------------ |
| Speed      | সাধারণত দ্রুত    | তুলনামূলক ধীর            |
| Approach   | Rule-based       | Linguistic/lexical       |
| Output     | Invalid হতে পারে | সাধারণত valid lemma      |
| `studies`  | `studi` হতে পারে | `study`                  |
| Context    | কম ব্যবহার       | বেশি ব্যবহার করতে পারে   |
| Complexity | কম               | বেশি                     |
| Accuracy   | কম হতে পারে      | সাধারণত বেশি             |
| Use        | Classical NLP    | Linguistic normalization |

---

# 23. POS এবং Lemmatization

Lemmatization অনেক সময় **Part-of-Speech (POS)** information ব্যবহার করে ভালো ফল দিতে পারে।

Example:

```text
better
```

Adjective হিসেবে:

```text
better → good
```

কিন্তু context অনুযায়ী word-এর grammatical role বদলাতে পারে।

তাই:

```text
Token
 +
POS
 +
Lexical knowledge
 ↓
Lemma
```

এটি stemming-এর থেকে বেশি sophisticated।

---

# 24. Stemming Pipeline

Classical NLP pipeline:

```text
Raw Text
   ↓
Cleaning
   ↓
Tokenization
   ↓
Stopword Handling
   ↓
Stemming
   ↓
Feature Extraction
   ↓
TF-IDF
   ↓
ML Model
```

---

# 25. Example Pipeline

Input:

```text
The players are playing football games.
```

### Step 1 — Tokenization

```text
[
"The",
"players",
"are",
"playing",
"football",
"games"
]
```

### Step 2 — Stopword removal

```text
[
"players",
"playing",
"football",
"games"
]
```

### Step 3 — Stemming

Possible:

```text
[
"player",
"play",
"footbal",
"game"
]
```

দেখো:

```text
football → footbal
```

এটি technically valid English word নয়।

এটাই stemming-এর limitation।

---

# 26. Stemming কখন Useful?

Stemming useful হতে পারে:

### Search

```text
connect
connected
connecting
```

search query matching-এর জন্য related forms একই দিকে নেওয়া useful হতে পারে।

### Classical Text Classification

যেমন:

```text
spam
topic classification
document classification
```

### Information Retrieval

Related word forms matching করতে।

### Simple Feature Engineering

Vocabulary size কমাতে।

---

# 27. Stemming কখন Avoid করা ভালো?

যদি exact linguistic form গুরুত্বপূর্ণ হয়:

```text
Grammar analysis
Text generation
Machine translation
High-quality rewriting
Linguistic analysis
```

তখন aggressive stemming সাধারণত ভালো choice নয়।

বিশেষ করে আমাদের AI writing assistant-এর ক্ষেত্রে।

---

# 28. AI Writing Assistant-এ Stemming

আমাদের system:

```text
User Text
   ↓
Preprocessing
   ↓
Tokenization
   ↓
Linguistic Analysis
   ↓
Model
   ↓
Rewrite
```

এখানে যদি আমরা:

```text
beautiful
```

কে aggressive stem করে:

```text
beauti
```

বানিয়ে ফেলি, তাহলে generation-এর জন্য original linguistic form হারিয়ে যায়।

তাই:

```text
AI Writing / Generation
→ সাধারণত original text/token context preserve করা উচিত
```

---

# 29. AI Detector / Text Analysis

যদি আমরা text classification বা feature analysis করি, তখন একটি separate feature pipeline থাকতে পারে:

```text
Original Text
      │
      ├──────────────→ Display
      │
      └──→ Analysis Copy
                ↓
             Tokenize
                ↓
        Optional Stemming
                ↓
          TF-IDF / Features
```

এখানে stemming **optional feature-engineering step** হতে পারে।

Original text destroy করার দরকার নেই।

---

# 30. Stemming + TF-IDF

ধরো dataset:

```text
playing
played
player
plays
```

Stemming করলে:

```text
play
play
player
play
```

তখন vocabulary size কমতে পারে।

TF-IDF-এর জন্য:

```text
Vocabulary
```

ছোট হতে পারে।

ফলে sparse feature matrix কিছু ক্ষেত্রে compact হতে পারে।

---

# 31. Stemming + Search

Query:

```text
connect
```

Document:

```text
connecting systems
```

যদি stemming উভয় জায়গায় প্রয়োগ করা হয়:

```text
connect
```

এবং:

```text
connect
```

তাহলে match পাওয়া সহজ হতে পারে।

---

# 32. Stemming সব Language-এ একই নয়

English-এর জন্য:

```text
Porter
Snowball
Lancaster
```

আছে।

কিন্তু Bangla-এর জন্য English stemmer ব্যবহার করা যাবে না।

কারণ:

```text
Language
 ↓
Morphology
 ↓
Inflection
 ↓
Stemming rules
```

language-specific।

---

# 33. Bangla NLP

Bangla text:

```text
আমি বইটি পড়ছি।
আমি বই পড়লাম।
আমি বইগুলো পড়েছি।
```

এখানে word forms-এর morphological structure English-এর মতো নয়।

তাই:

```text
English Porter Stemmer
```

Bangla-এর জন্য সরাসরি ব্যবহার করা ভুল।

Bangla NLP-তে language-specific morphological processing দরকার হতে পারে।

---

# 34. Stemming-এর Major Limitations

### 1. Invalid words

```text
studies → studi
```

### 2. Over-stemming

Unrelated words একই stem-এ যেতে পারে।

### 3. Under-stemming

Related words আলাদা থাকতে পারে।

### 4. Meaning ignore করতে পারে

Algorithm সাধারণত semantic understanding করে না।

### 5. Language dependent

এক language-এর rules অন্য language-এ কাজ নাও করতে পারে।

---

# 35. Porter Stemmer Hands-on

```python
from nltk.stem import PorterStemmer

stemmer = PorterStemmer()

words = [
    "connect",
    "connected",
    "connecting",
    "connection",
    "studies",
    "studying"
]

for word in words:
    print(f"{word:15} → {stemmer.stem(word)}")
```

এখানে লক্ষ্য করবে related forms অনেক ক্ষেত্রে একই বা কাছাকাছি stem-এ চলে আসে।

---

# 36. Compare Three Stemmers

```python
from nltk.stem import (
    PorterStemmer,
    SnowballStemmer,
    LancasterStemmer
)

porter = PorterStemmer()
snowball = SnowballStemmer("english")
lancaster = LancasterStemmer()

words = [
    "playing",
    "studies",
    "connection",
    "beautifully",
    "running"
]

for word in words:

    print("\nWord:", word)

    print(
        "Porter:",
        porter.stem(word)
    )

    print(
        "Snowball:",
        snowball.stem(word)
    )

    print(
        "Lancaster:",
        lancaster.stem(word)
    )
```

এটি চালালে তুমি দেখবে **একই word-এর জন্য algorithm ভেদে output আলাদা হতে পারে।**

---

# 37. কেন Output আলাদা?

কারণ:

```text
Porter
   ↓
Rules A

Snowball
   ↓
Rules B

Lancaster
   ↓
Rules C
```

অর্থাৎ:

```text
Same Input
     ↓
Different Algorithm
     ↓
Different Stem
```

তাই stemming algorithm নির্বাচনও একটি design decision।

---

# 38. Stemming Quality Evaluate করা

শুধু output দেখে সিদ্ধান্ত নেবে না।

Task অনুযায়ী evaluate করবে:

```text
Precision
Recall
F1
Search relevance
Classification accuracy
Vocabulary reduction
```

যদি stemming করার পরে:

```text
Accuracy ↓
```

তাহলে stemming বাদ দেওয়াই ভালো হতে পারে।

---

# 39. Modern NLP-তে Stemming

Modern Transformer models-এর ক্ষেত্রে সাধারণত manually:

```text
word
 ↓
stem
```

করার প্রয়োজন কম।

কারণ tokenizer নিজেই subword representation তৈরি করে।

Example:

```text
playing
```

tokenizer এটাকে কোনো subword sequence হিসেবে represent করতে পারে।

Model context-এর মধ্যে word form-টিও দেখতে পায়।

তাই:

```text
Transformer
→ aggressive stemming usually unnecessary
```

---

# 40. Classical বনাম Modern NLP

### Classical

```text
Text
 ↓
Tokenize
 ↓
Stopword Removal
 ↓
Stem
 ↓
TF-IDF
 ↓
ML
```

### Modern

```text
Text
 ↓
Light Preprocessing
 ↓
Tokenizer
 ↓
Subword Tokens
 ↓
Token IDs
 ↓
Embedding
 ↓
Transformer
```

---

# 41. Stemming এবং Subword Tokenization কি একই?

**না।**

Stemming:

```text
playing
 ↓
play
```

এটি linguistic normalization-এর একটি classical technique।

Subword tokenization:

```text
playing
 ↓
play + ing
```

এটি model-এর vocabulary representation-এর জন্য।

Difference:

```text
Stemming
→ word form reduce করে

Subword Tokenization
→ model input units তৈরি করে
```

---

# 42. একটি গুরুত্বপূর্ণ Comparison

```text
playing
```

### Stemming

```text
play
```

### Lemmatization

```text
play
```

### Subword Tokenization

```text
play + ing
```

### Character Tokenization

```text
p + l + a + y + i + n + g
```

এগুলো চারটি আলাদা concept।

---

# 43. AI Project-এর জন্য Decision

আমাদের future AI Writing Assistant-এর জন্য:

```text
Generation
→ ❌ aggressive stemming

Grammar analysis
→ ❌ stemming as primary representation

Semantic analysis
→ সাধারণত ❌

Classical TF-IDF classifier
→ ✅ stemming test করা যেতে পারে

Search
→ ✅ stemming useful হতে পারে

Traditional text classification
→ ✅ experiment করা যেতে পারে
```

---

# 44. Hands-on Exercise 🔥

### Exercise 1

এই words-এর Porter stem বের করো:

```python
words = [
    "running",
    "played",
    "studies",
    "easily",
    "cats",
    "connected"
]
```

---

### Exercise 2

Porter এবং Lancaster compare করো:

```python
words = [
    "relational",
    "conditional",
    "organization",
    "beautifully",
    "friendship"
]
```

Output table তৈরি করো:

```text
Word | Porter | Lancaster
```

---

# 45. Exercise 3 — নিজের Stemmer

একটি basic function:

```python
def simple_stem(word):
    ...
```

এমনভাবে তৈরি করো যাতে:

```text
playing → play
played → play
cats → cat
```

হয়।

তারপর দেখো কোন input-এ এটি ভুল result দেয়।

---

# 46. Exercise 4 — Full Pipeline

Input:

```text
"The players are playing different games."
```

Pipeline:

```text
Tokenization
    ↓
Stopword Removal
    ↓
Stemming
```

নিজে output বের করো।

---

# 47. Theory Questions

নিজে answer করার চেষ্টা করো:

1. Stemming কী?
2. Stem কী?
3. Stemming কেন ব্যবহার করা হয়?
4. Stem এবং root-এর difference কী?
5. Stem এবং lemma-এর difference কী?
6. Stemming কি semantic understanding করে?
7. Rule-based stemming কী?
8. Porter Stemmer কী?
9. Snowball Stemmer কী?
10. Lancaster Stemmer কী?
11. Over-stemming কী?
12. Under-stemming কী?
13. `studies → studi` কেন হতে পারে?
14. Stemming-এর তিনটি limitation বলো।
15. Stemming এবং lemmatization-এর difference কী?
16. Stemming এবং subword tokenization-এর difference কী?
17. Stemming এবং TF-IDF-এর relationship কী?
18. Search engine-এ stemming কেন useful হতে পারে?
19. Transformer model-এ stemming সাধারণত কেন প্রয়োজন হয় না?
20. AI writing system-এ aggressive stemming কেন risky?

---

# 48. Interview Questions

### Beginner

* What is stemming?
* What is a stem?
* Why do we use stemming?
* Give an example of stemming.

### Intermediate

* What is Porter Stemmer?
* What is Snowball Stemmer?
* What is Lancaster Stemmer?
* What is over-stemming?
* What is under-stemming?
* Why can a stemmer produce invalid words?

### Advanced

* Stemming vs lemmatization?
* Stemming vs subword tokenization?
* Why might stemming hurt NLP performance?
* When would you choose stemming over lemmatization?
* Should stemming be applied before a Transformer?
* Why is stemming useful for classical TF-IDF systems?
* How would you evaluate whether stemming improves a classifier?

---

# 49. M02.07 Completion Checklist

```text
[x] Stem
[x] Stemming
[x] Purpose of stemming
[x] Rule-based stemming
[x] Simple stemmer
[x] Porter Stemmer
[x] Snowball Stemmer
[x] Lancaster Stemmer
[x] Over-stemming
[x] Under-stemming
[x] Stem vs Root
[x] Stem vs Lemma
[x] Stemming vs Lemmatization
[x] Stemming vs Subword Tokenization
[x] Stemming + Stopwords
[x] Stemming + TF-IDF
[x] Stemming + Search
[x] Classical NLP
[x] Modern NLP
[x] Language-specific stemming
[x] Bangla NLP consideration
[x] AI Writing Assistant application
[x] AI Detector/Text Analysis application
[x] Python hands-on
```

# 🧠 Final Mental Model

এই চারটি একসাথে confuse করবে না:

```text
                    WORD
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
      STEMMING   LEMMATIZE   TOKENIZE
          │          │          │
          ▼          ▼          ▼
        play       play      play + ing
```

আর:

```text
Stemming
    ↓
Fast
    ↓
Rule-based
    ↓
May produce invalid words
```

অন্যদিকে:

```text
Lemmatization
    ↓
More linguistic knowledge
    ↓
Usually valid lemma
    ↓
More computationally expensive
```

### সবচেয়ে গুরুত্বপূর্ণ:

> **Stemming-এর লক্ষ্য word-এর “সঠিক root” বের করা নয়; related word forms-কে একটি reduced representation-এ আনা।**

**M02.07 complete.**

পরের lesson হবে **M02.08 — Lemmatization Deep Dive** — যেখানে আমরা **lemma, morphology, dictionary form, POS-aware lemmatization, WordNet Lemmatizer, spaCy lemmatization, stemming বনাম lemmatization-এর practical comparison এবং কখন কোনটি ব্যবহার করবে** বিস্তারিত শিখব।


---
# M02.08 — Lemmatization Deep Dive

M02.07-এ আমরা **Stemming** শিখেছি। এবার তার পরের গুরুত্বপূর্ণ topic **Lemmatization**। এটি NLP-এর foundation-এর একটি core concept, বিশেষ করে text analysis, search, classification এবং language understanding-এর জন্য।

---

# 1. Lemmatization কী?

**Lemmatization** হলো এমন একটি NLP technique যেখানে একটি word-এর বিভিন্ন grammatical form-কে তার **base/dictionary form**, অর্থাৎ **lemma**-তে রূপান্তর করা হয়।

উদাহরণ:

```text
running  → run
runs     → run
walked   → walk
walking  → walk
cars     → car
studies  → study
children → child
mice     → mouse
```

এখানে:

```text
running
   ↓
 Lemmatization
   ↓
  run
```

`run` হলো **lemma**।

---

# 2. Lemma কী?

**Lemma** হলো একটি word-এর canonical বা dictionary form।

উদাহরণ:

| Word     | Lemma |
| -------- | ----- |
| cars     | car   |
| books    | book  |
| running  | run   |
| runs     | run   |
| walked   | walk  |
| walking  | walk  |
| studies  | study |
| children | child |
| mice     | mouse |
| better   | good  |

তাই:

```text
Word forms
     ↓
Lemmatization
     ↓
Lemma
```

---

# 3. Lemmatization কেন প্রয়োজন?

ধরো আমাদের dataset-এ আছে:

```text
run
runs
running
ran
```

একটি সাধারণ keyword/counting system এগুলোকে চারটি আলাদা word হিসেবে দেখতে পারে।

কিন্তু semantic perspective থেকে এগুলো একই concept-এর সঙ্গে সম্পর্কিত।

```text
run
runs
running
ran
   ↓
 run
```

এর ফলে:

* vocabulary size কমানো যায়
* related words একত্র করা যায়
* search improve করা যায়
* text classification improve করতে পারে
* feature space reduce করা যায়
* linguistic analysis সহজ হয়

---

# 4. Lemmatization বনাম Stemming

এটি **খুব গুরুত্বপূর্ণ interview topic**।

### Stemming

Word-এর ending কেটে একটি stem তৈরি করে।

```text
studies → studi
```

সমস্যা:

```text
studi ❌
```

এটি dictionary word নয়।

### Lemmatization

Linguistic knowledge ব্যবহার করে valid base form বের করার চেষ্টা করে।

```text
studies → study
```

```text
study ✅
```

---

# 5. Side-by-side comparison

| Word     | Stemming | Lemmatization |
| -------- | -------- | ------------- |
| studies  | studi    | study         |
| studying | studi    | study         |
| running  | run      | run           |
| better   | better   | good*         |
| children | children | child         |
| mice     | mice     | mouse         |
| cars     | car      | car           |

`*` কিছু lemmatizer-এ `better → good` পেতে context/POS information প্রয়োজন।

---

# 6. Stemming কেন `studi` দেয়?

ধরো একটি basic suffix rule:

```text
ies → i
```

তাহলে:

```text
studies
   ↓
studi
```

Stemming সাধারণত জিজ্ঞেস করে:

> "কোন characters remove করলে একটা common stem পাওয়া যায়?"

Lemmatization জিজ্ঞেস করে:

> "এই word-এর linguistic base form কী?"

এটাই মূল পার্থক্য।

---

# 7. Lemmatization এবং Morphology

Lemmatization-এর সঙ্গে **Morphology**-এর খুব গভীর সম্পর্ক আছে।

উদাহরণ:

```text
walk
walking
walked
walks
```

এগুলো একই lexical concept-এর বিভিন্ন grammatical form।

Lemmatizer word-এর:

* prefix
* suffix
* inflection
* grammatical form
* POS
* dictionary relationship

ইত্যাদি বিবেচনা করতে পারে।

---

# 8. Inflection কী?

একটি word grammatical কারণে পরিবর্তিত হলে তাকে **inflection** বলা হয়।

উদাহরণ:

```text
walk → walks
walk → walked
walk → walking
```

এখানে মূল lexical meaning একই family-এর মধ্যে থাকে।

আর:

```text
child → children
```

এখানে form সম্পূর্ণ বদলে গেছে।

এ ধরনের irregular form handle করতে linguistic/dictionary knowledge গুরুত্বপূর্ণ।

---

# 9. Regular বনাম Irregular Words

### Regular

```text
cars → car
books → book
played → play
walking → walk
```

এগুলো তুলনামূলকভাবে সহজ।

### Irregular

```text
children → child
mice → mouse
went → go
better → good
feet → foot
```

এখানে শুধু suffix কাটলেই হবে না।

তাই Lemmatization-এর জন্য lexical/linguistic information গুরুত্বপূর্ণ।

---

# 10. POS কেন গুরুত্বপূর্ণ?

**POS = Part of Speech**

একই word-এর lemma বের করার ক্ষেত্রে wordটি:

* noun
* verb
* adjective
* adverb

কোন category-তে ব্যবহৃত হচ্ছে তা গুরুত্বপূর্ণ হতে পারে।

উদাহরণ:

```text
better
```

এটি context অনুযায়ী adjective/adverb হতে পারে।

Verb-এর ক্ষেত্রে:

```text
saw → see
```

কিন্তু noun context-এ `saw` হলো একটি tool।

অর্থাৎ:

```text
POS + Context
       ↓
Better Lemmatization
```

---

# 11. Example with POS

Sentence:

```text
I saw a bird.
```

এখানে:

```text
saw → see
```

কারণ `saw` এখানে verb।

কিন্তু:

```text
I bought a saw.
```

এখানে:

```text
saw → saw
```

কারণ এটি noun।

তাই শুধু word দেখে সবসময় সঠিক lemma বের করা যায় না।

---

# 12. Context-এর গুরুত্ব

Lemmatization-এর quality অনেক সময় context-এর ওপর নির্ভর করে।

উদাহরণ:

```text
The leaves are green.
```

এখানে:

```text
leaves → leaf
```

কিন্তু:

```text
He leaves the house.
```

এখানে:

```text
leaves → leave
```

একই surface word:

```text
leaves
```

কিন্তু context আলাদা হওয়ায় lemma আলাদা।

---

# 13. Python-এ Lemmatization

Python NLP ecosystem-এ কয়েকটি popular option আছে:

```text
NLTK
spaCy
WordNet
```

আমরা প্রথমে NLTK দেখব।

---

# 14. NLTK WordNet Lemmatizer

Install:

```bash
pip install nltk
```

তারপর:

```python
import nltk

nltk.download("wordnet")
```

তারপর:

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

words = [
    "cars",
    "running",
    "studies",
    "played"
]

for word in words:
    print(word, "→", lemmatizer.lemmatize(word))
```

সম্ভাব্য output:

```text
cars → car
running → running
studies → study
played → played
```

এখানে একটি গুরুত্বপূর্ণ বিষয় আছে।

---

# 15. কেন `running → running` হলো?

কারণ WordNet Lemmatizer defaultভাবে ধরে নেয় wordটি **noun**।

তাই:

```python
lemmatizer.lemmatize("running")
```

noun হিসেবে কাজ করছে।

যদি আমরা POS দিই:

```python
lemmatizer.lemmatize("running", pos="v")
```

তাহলে:

```text
running → run
```

---

# 16. POS-aware Lemmatization

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

print(lemmatizer.lemmatize("running", pos="v"))
print(lemmatizer.lemmatize("played", pos="v"))
print(lemmatizer.lemmatize("studies", pos="v"))
```

Output:

```text
run
play
study
```

---

# 17. Common WordNet POS

NLTK WordNet-এ:

```text
n → noun
v → verb
a → adjective
r → adverb
```

Example:

```python
lemmatizer.lemmatize("better", pos="a")
```

Output:

```text
good
```

আর:

```python
lemmatizer.lemmatize("running", pos="v")
```

Output:

```text
run
```

---

# 18. Important Example

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

words = [
    ("running", "v"),
    ("played", "v"),
    ("studies", "v"),
    ("cars", "n"),
    ("children", "n"),
    ("better", "a")
]

for word, pos in words:
    lemma = lemmatizer.lemmatize(word, pos=pos)
    print(f"{word} → {lemma}")
```

Output:

```text
running → run
played → play
studies → study
cars → car
children → child
better → good
```

---

# 19. Stemming + Lemmatization একসাথে

সাধারণত একই preprocessing pipeline-এ blindly দুটো করার প্রয়োজন নেই।

অর্থাৎ:

```text
Text
 ↓
Stemming
 ↓
Lemmatization
```

এটি সাধারণত unnecessary।

বরং task অনুযায়ী choose করো:

```text
Text
 ↓
Tokenization
 ↓
       ┌───────────────┐
       ↓               ↓
   Stemming       Lemmatization
       ↓               ↓
   Stem form       Lemma form
```

---

# 20. কখন Stemming ব্যবহার করব?

Stemming useful হতে পারে:

* simple search
* information retrieval
* keyword matching
* classical NLP
* কিছু text classification
* দ্রুত preprocessing

উদাহরণ:

```text
connect
connected
connecting
connection
```

search system-এ related terms ধরতে stemming সাহায্য করতে পারে।

---

# 21. কখন Lemmatization ব্যবহার করব?

Lemmatization useful হতে পারে:

* linguistic analysis
* text normalization
* semantic-oriented preprocessing
* classical NLP
* search
* classification
* feature engineering
* vocabulary normalization

যেখানে valid linguistic form গুরুত্বপূর্ণ, সেখানে Lemmatization বেশি উপযোগী।

---

# 22. Modern Transformer NLP-তে কী হবে?

এটি খুব গুরুত্বপূর্ণ।

Modern Transformer model সাধারণত:

```text
Text
 ↓
Tokenizer
 ↓
Subword Tokens
 ↓
Token IDs
 ↓
Embedding
 ↓
Transformer
```

এখানে manual stemming/lemmatization অনেক ক্ষেত্রে প্রয়োজন হয় না।

কারণ modern tokenizer এবং model নিজেই বিভিন্ন word form handle করতে পারে।

উদাহরণ conceptually:

```text
playing
   ↓
subword tokenizer
   ↓
play + ing
```

Actual tokenization model অনুযায়ী ভিন্ন হবে।

তাই:

> Transformer ব্যবহার করলে সব text আগে lemmatize করতেই হবে — ❌

---

# 23. Stemming vs Lemmatization vs Tokenization

তিনটিকে আলাদা রাখো।

### Tokenization

Text ভাঙে:

```text
"I am learning NLP"

↓

"I"
"am"
"learning"
"NLP"
```

### Stemming

Word-এর form কাটে:

```text
learning → learn
```

### Lemmatization

Word-এর linguistic base form বের করে:

```text
children → child
```

Mental model:

```text
              TEXT
                ↓
          TOKENIZATION
                ↓
             TOKENS
                ↓
        ┌───────┴────────┐
        ↓                ↓
    STEMMING       LEMMATIZATION
        ↓                ↓
      STEM             LEMMA
```

---

# 24. Stopwords-এর সঙ্গে Lemmatization

ধরো:

```text
The children are running in the garden.
```

যদি stopwords remove করি:

```text
children
running
garden
```

তারপর lemmatization:

```text
child
run
garden
```

Pipeline:

```text
Text
 ↓
Tokenization
 ↓
Stopword handling
 ↓
Lemmatization
 ↓
Normalized text
```

তবে modern NLP-তে stopword removal সবসময় করা উচিত নয়।

---

# 25. Lemmatization + TF-IDF

ধরো dataset:

```text
I am running
He runs
They ran
```

Without normalization:

```text
running
runs
ran
```

এগুলো আলাদা feature হতে পারে।

Lemmatization করলে conceptually:

```text
running → run
runs → run
ran → run
```

তাহলে:

```text
run
run
run
```

এবং TF-IDF feature space ছোট হতে পারে।

---

# 26. AI Writing Assistant-এ ব্যবহার

আমাদের target AI writing assistant-এর ক্ষেত্রে Lemmatization useful হতে পারে।

উদাহরণ:

User লিখল:

```text
The students were studying different subjects.
```

Lemmatized representation:

```text
the
student
be
study
different
subject
```

এটি ব্যবহার করে:

* word frequency analysis
* vocabulary analysis
* readability analysis
* repeated word detection
* linguistic statistics
* feature extraction

করা যেতে পারে।

---

# 27. AI Text Analyzer-এ ব্যবহার

ধরো:

```text
The models are generating different responses.
```

Lemmatization:

```text
the
model
be
generate
different
response
```

এর মাধ্যমে normalized lexical representation পাওয়া যায়।

এটি statistical analysis-এ useful।

তবে **AI-generated text শনাক্ত করার জন্য শুধু lemmatization যথেষ্ট নয়**।

---

# 28. একটি গুরুত্বপূর্ণ সতর্কতা

Lemmatization করলে original sentence হারিয়ে ফেলতে পারি।

Original:

```text
The children were running quickly.
```

Normalized:

```text
the child be run quickly
```

এটি grammatical sentence নয়।

তাই:

> Lemmatized text সাধারণত final output হিসেবে user-কে দেখানোর জন্য নয়।

এটি analysis-এর জন্য intermediate representation।

---

# 29. Original Text Preserve করা

আমাদের system-এ ideally:

```python
original_text = "The children were running quickly."

lemmatized_text = [
    "the",
    "child",
    "be",
    "run",
    "quickly"
]
```

Original text কখনো replace করা উচিত নয় যদি পরে generation/rewrite করতে হয়।

Architecture:

```text
Original Text
     │
     ├──────────────→ UI / Final Output
     │
     ↓
NLP Analysis
     ↓
Lemmatization
     ↓
Features
```

---

# 30. Simple Lemmatization Function

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()


def lemmatize_words(words):
    return [
        lemmatizer.lemmatize(word, pos="v")
        for word in words
    ]


words = [
    "running",
    "played",
    "studies"
]

print(lemmatize_words(words))
```

Output:

```text
['run', 'play', 'study']
```

---

# 31. Sentence Example

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

sentence = "The students are studying different subjects."

words = sentence.lower().split()

lemmas = [
    lemmatizer.lemmatize(word, pos="v")
    for word in words
]

print(lemmas)
```

এখানে একটি সমস্যা আছে:

```text
subjects.
```

এখানে punctuation attached আছে।

তাই production NLP pipeline-এ শুধু `.split()` যথেষ্ট নয়।

---

# 32. Proper NLP Pipeline

আমরা আগে M02.03-এ যে pipeline শিখেছি সেটার সঙ্গে মিলিয়ে:

```text
Raw Text
   ↓
Cleaning
   ↓
Sentence Segmentation
   ↓
Tokenization
   ↓
POS Tagging
   ↓
Lemmatization
   ↓
Normalized Representation
```

এখানে POS tagging গুরুত্বপূর্ণ, কারণ:

```text
Word + POS
     ↓
Better Lemma
```

---

# 33. Lemmatization-এর সুবিধা

### 1. Meaningful output

```text
studies → study
```

### 2. Vocabulary reduction

```text
run
runs
running
ran
```

একটি lexical representation-এ আনা যায়।

### 3. Linguistically informed

Stemming-এর চেয়ে linguistic knowledge বেশি ব্যবহার করে।

### 4. Search improvement

Related word forms normalize করা যায়।

### 5. Feature reduction

Classical ML-এ feature space কমাতে সাহায্য করতে পারে।

---

# 34. Lemmatization-এর অসুবিধা

### 1. তুলনামূলকভাবে slow

Stemming-এর চেয়ে বেশি processing প্রয়োজন হতে পারে।

### 2. POS দরকার হতে পারে

```text
saw
```

এর সঠিক lemma context/POS-এর ওপর নির্ভর করতে পারে।

### 3. Language-dependent

English-এর জন্য যে system ভালো কাজ করে, অন্য ভাষায় একইভাবে নাও করতে পারে।

### 4. Perfect নয়

সব word/context সবসময় সঠিকভাবে normalize হবে না।

---

# 35. Stemming বনাম Lemmatization — Final Table

| বিষয়               | Stemming            | Lemmatization                  |
| ------------------ | ------------------- | ------------------------------ |
| Method             | Rule-based          | Linguistic                     |
| Speed              | Faster              | তুলনামূলক slow                 |
| Dictionary         | সাধারণত প্রয়োজন নেই | সাধারণত lexical knowledge লাগে |
| Output             | Stem                | Lemma                          |
| Valid word         | নাও হতে পারে        | সাধারণত valid form             |
| POS                | সাধারণত দরকার নেই   | গুরুত্বপূর্ণ হতে পারে          |
| Accuracy           | কম                  | বেশি                           |
| Complexity         | কম                  | বেশি                           |
| Classical NLP      | Useful              | Useful                         |
| Modern Transformer | সাধারণত unnecessary | সাধারণত unnecessary            |

---

# 36. সবচেয়ে গুরুত্বপূর্ণ তিনটি Concept

এগুলো অবশ্যই মনে রাখবে:

### Stem

```text
playing → play
```

Rule-based shortened form।

### Lemma

```text
children → child
```

Dictionary/canonical form।

### Token

```text
"I love NLP"
```

এর token:

```text
I
love
NLP
```

---

# 37. Complete NLP Mental Model

এখন পর্যন্ত আমাদের শেখা topics:

```text
                 NLP
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
   Text Structure       Language
        │                   │
        ↓                   ↓
   Tokenization         Morphology
                            │
                  ┌─────────┴─────────┐
                  ↓                   ↓
              Stemming          Lemmatization
                  │                   │
                  ↓                   ↓
                Stem                Lemma
```

---

# 38. আমাদের AI Project-এর সঙ্গে Connection

Future AI writing platform-এর analysis pipeline হতে পারে:

```text
User Text
    ↓
Text Cleaning
    ↓
Sentence Segmentation
    ↓
Tokenization
    ↓
POS Tagging
    ↓
Lemmatization
    ↓
Feature Extraction
    ↓
Text Analysis
    ↓
AI Model
    ↓
Rewrite / Improvement
    ↓
Final Text
```

কিন্তু গুরুত্বপূর্ণ:

**Lemmatization হলো analysis/preprocessing-এর একটি অংশ; এটি নিজে AI writing model নয়।**

---

# 39. Practice Task — Beginner

এই words-গুলোর lemma বের করো:

```text
cars
books
running
played
studies
children
mice
feet
better
went
```

নিজে আগে চেষ্টা করবে।

Expected concept:

```text
cars      → car
books     → book
running   → run
played    → play
studies   → study
children  → child
mice      → mouse
feet      → foot
better    → good
went      → go
```

---

# 40. Practice Task — Intermediate

একটি function তৈরি করো:

```python
def lemmatize_sentence(sentence):
    ...
```

Input:

```text
"The children are running and playing games."
```

Function-এর কাজ হবে:

```text
sentence
   ↓
tokenization
   ↓
lemmatization
   ↓
list of lemmas
```

---

# 41. Practice Task — Advanced

এই sentence:

```text
"The students studied different subjects and were writing interesting answers."
```

একটি pipeline বানাও:

```text
Sentence
 ↓
Tokenization
 ↓
POS
 ↓
Lemmatization
 ↓
Frequency Count
```

তারপর বের করো:

```text
original tokens
unique tokens
lemmas
unique lemmas
```

এটি তোমার AI text analyzer-এর জন্য খুব ভালো practice।

---

# 42. Theory Questions

নিজেকে এই প্রশ্নগুলো করো:

1. Lemmatization কী?
2. Lemma কী?
3. Stemming কী?
4. Stem এবং lemma-এর পার্থক্য কী?
5. Lemmatization কেন Stemming-এর চেয়ে linguistic?
6. POS কেন Lemmatization-এর জন্য গুরুত্বপূর্ণ?
7. `children → child` কীভাবে সম্ভব?
8. `saw → see` এবং `saw → saw` কেন হতে পারে?
9. Inflection কী?
10. Regular ও irregular word কী?
11. Lemmatization কি original sentence replace করা উচিত?
12. Transformer model-এ manual Lemmatization সবসময় প্রয়োজন হয় কি?
13. Lemmatization-এর সুবিধা কী?
14. Lemmatization-এর limitation কী?
15. Stemming কখন ব্যবহার করবে?

---

# 43. Interview Questions

### Q1. What is lemmatization?

**Answer:**

> Lemmatization is an NLP technique that converts a word into its canonical dictionary form or lemma using linguistic information.

### Q2. Stemming vs Lemmatization?

```text
Stemming:
studies → studi

Lemmatization:
studies → study
```

### Q3. Why is POS important?

কারণ একই word বিভিন্ন grammatical role-এ ভিন্ন lemma দিতে পারে।

```text
saw → see   # verb
saw → saw   # noun
```

### Q4. Which is faster?

```text
Stemming
```

সাধারণত faster।

### Q5. Which is more linguistically accurate?

```text
Lemmatization
```

সাধারণত বেশি linguistically meaningful।

---

# 44. M02.08 Completion Checklist

নিজেকে check করো:

* [ ] Lemmatization বুঝি
* [ ] Lemma বুঝি
* [ ] Stem vs Lemma বুঝি
* [ ] Morphology বুঝি
* [ ] Inflection বুঝি
* [ ] Regular words বুঝি
* [ ] Irregular words বুঝি
* [ ] POS-এর ভূমিকা বুঝি
* [ ] Context-এর ভূমিকা বুঝি
* [ ] NLTK WordNet Lemmatizer বুঝি
* [ ] POS-aware lemmatization বুঝি
* [ ] Stemming vs Lemmatization পার্থক্য বুঝি
* [ ] Stopword-এর সঙ্গে relation বুঝি
* [ ] TF-IDF-এর সঙ্গে relation বুঝি
* [ ] Transformer-এর ক্ষেত্রে role বুঝি
* [ ] AI text analyzer-এ application বুঝি
* [ ] Python-এ basic implementation করতে পারি

---

## 🔑 আজকের Final Mental Model

```text
                 WORD
                   │
          ┌────────┴────────┐
          ↓                 ↓
      STEMMING        LEMMATIZATION
          ↓                 ↓
        STEM              LEMMA
          │                 │
          ↓                 ↓
   rule-based form    dictionary/base form
          │                 │
          ↓                 ↓
     playing → play    children → child
     studies → studi   running → run
```

আর সবচেয়ে গুরুত্বপূর্ণ:

```text
STEM ≠ LEMMA
```

**Stemming word-কে কাটে, Lemmatization word-এর linguistic base form খুঁজে।**

**M02.08 complete.** পরের lesson হবে **M02.09 — POS Tagging (Part-of-Speech Tagging) Deep Dive**, যেখানে আমরা noun, verb, adjective, adverb, pronoun, determiner ইত্যাদি এবং Python-এ POS tagging কীভাবে কাজ করে তা শিখব।

---
# M02.09 — POS Tagging (Part-of-Speech Tagging) Deep Dive

M02.08-এ আমরা **Lemmatization** শিখেছি। সেখানে দেখেছি যে একটি word-এর সঠিক lemma বের করার জন্য **POS information** অনেক গুরুত্বপূর্ণ।

আজ আমরা **POS Tagging** পুরোপুরি শিখব।

---

# 1. POS কী?

**POS = Part of Speech**

একটি sentence-এর প্রতিটি word কোন grammatical category-তে কাজ করছে, সেটিই তার **Part of Speech**।

উদাহরণ:

> The boy plays football.

এখানে:

```text
The       → Determiner
boy       → Noun
plays     → Verb
football  → Noun
```

অর্থাৎ:

```text
Word
 ↓
Grammatical Role
 ↓
POS Tag
```

---

# 2. POS Tagging কী?

**POS Tagging** হলো sentence-এর প্রতিটি token-কে তার grammatical category বা **part of speech** অনুযায়ী tag করা।

উদাহরণ:

```text
I love programming.
```

POS tagging:

```text
I           → Pronoun
love        → Verb
programming → Noun
```

আর একটি formal representation:

```text
I/PRP love/VBP programming/NN
```

---

# 3. POS Tagging কেন গুরুত্বপূর্ণ?

NLP system-এর জন্য শুধু word জানা যথেষ্ট নয়।

ধরো:

```text
book
```

এটি হতে পারে:

```text
Noun:
I read a book.

Verb:
I will book a hotel.
```

একই word, কিন্তু grammatical role আলাদা।

POS tagging করলে system বুঝতে পারে:

```text
book → Noun
```

অথবা:

```text
book → Verb
```

এটি পরবর্তীতে:

* Lemmatization
* Parsing
* Information extraction
* Named Entity Recognition
* Text analysis
* Machine translation
* Question answering
* Search
* Grammar analysis

ইত্যাদিতে কাজে লাগে।

---

# 4. Common POS Categories

সবচেয়ে গুরুত্বপূর্ণ categories:

```text
Noun
Pronoun
Verb
Adjective
Adverb
Preposition
Conjunction
Determiner
Interjection
Auxiliary
Modal
```

এখন একে একে দেখি।

---

# 5. Noun

**Noun** হলো person, place, thing, object, concept ইত্যাদির নাম।

উদাহরণ:

```text
Rahim
Dhaka
computer
book
student
AI
education
```

Sentence:

```text
The student uses a computer.
```

```text
student   → Noun
computer  → Noun
```

---

# 6. Proper Noun

নির্দিষ্ট ব্যক্তি, স্থান, প্রতিষ্ঠান ইত্যাদির নাম।

উদাহরণ:

```text
Rahim
Bangladesh
Dhaka
Google
Python
```

Example:

```text
Rahim lives in Dhaka.
```

```text
Rahim → Proper Noun
Dhaka → Proper Noun
```

---

# 7. Pronoun

Noun-এর পরিবর্তে ব্যবহৃত word।

উদাহরণ:

```text
I
you
he
she
it
we
they
this
that
who
```

Example:

```text
Rahim is a student.
He studies computer science.
```

```text
Rahim → Noun
He    → Pronoun
```

---

# 8. Verb

কাজ, ঘটনা বা state প্রকাশ করে।

উদাহরণ:

```text
run
eat
write
learn
play
study
sleep
```

Example:

```text
She writes code.
```

```text
writes → Verb
```

---

# 9. Auxiliary Verb

Main verb-কে সাহায্য করে।

উদাহরণ:

```text
am
is
are
was
were
have
has
had
do
does
did
```

Example:

```text
She is studying.
```

```text
is       → Auxiliary
studying → Verb
```

---

# 10. Modal Verb

Possibility, ability, permission, obligation ইত্যাদি প্রকাশ করে।

উদাহরণ:

```text
can
could
may
might
must
shall
should
will
would
```

Example:

```text
You should study.
```

```text
should → Modal
study  → Verb
```

---

# 11. Adjective

Noun বা pronoun-এর property/quality বর্ণনা করে।

উদাহরণ:

```text
good
beautiful
large
small
intelligent
fast
interesting
```

Example:

```text
He is an intelligent student.
```

```text
intelligent → Adjective
student     → Noun
```

---

# 12. Adverb

Verb, adjective বা অন্য adverb সম্পর্কে অতিরিক্ত information দেয়।

উদাহরণ:

```text
quickly
slowly
very
carefully
extremely
```

Example:

```text
He runs quickly.
```

```text
runs    → Verb
quickly → Adverb
```

---

# 13. Preposition

দুটি entity/word-এর relationship প্রকাশ করে।

উদাহরণ:

```text
in
on
at
from
to
with
by
for
under
over
```

Example:

```text
The book is on the table.
```

```text
on → Preposition
```

---

# 14. Conjunction

Word, phrase বা clause connect করে।

উদাহরণ:

```text
and
or
but
because
although
if
while
```

Example:

```text
I study Python and JavaScript.
```

```text
and → Conjunction
```

---

# 15. Determiner

Noun সম্পর্কে নির্দিষ্টতা, quantity ইত্যাদি নির্দেশ করে।

উদাহরণ:

```text
a
an
the
this
that
these
those
some
many
```

Example:

```text
The boy reads a book.
```

```text
The → Determiner
a   → Determiner
```

---

# 16. Interjection

হঠাৎ emotion বা reaction প্রকাশ করে।

উদাহরণ:

```text
Wow!
Oh!
Hey!
Oops!
```

Example:

```text
Wow! That is amazing.
```

```text
Wow → Interjection
```

---

# 17. একটি সম্পূর্ণ Sentence Analysis

Sentence:

> The intelligent student quickly writes Python code.

Possible POS:

```text
The         → Determiner
intelligent → Adjective
student     → Noun
quickly     → Adverb
writes      → Verb
Python      → Proper Noun
code        → Noun
```

Structure:

```text
The
 ↓
Determiner

intelligent
 ↓
Adjective

student
 ↓
Noun

quickly
 ↓
Adverb

writes
 ↓
Verb

Python
 ↓
Proper Noun

code
 ↓
Noun
```

---

# 18. POS Tagging-এর Input কী?

সাধারণত:

```text
Raw Text
```

থেকে শুরু করি।

তারপর:

```text
Text
 ↓
Tokenization
 ↓
Tokens
 ↓
POS Tagging
 ↓
POS Tagged Tokens
```

উদাহরণ:

```text
I love Python.
```

Tokenization:

```text
["I", "love", "Python", "."]
```

POS tagging:

```text
I       → Pronoun
love    → Verb
Python  → Proper Noun
.       → Punctuation
```

---

# 19. POS Tag কী?

POS category-এর জন্য একটি short label ব্যবহার করা হয়।

Penn Treebank-এর কিছু common tag:

| Tag | Meaning                               |
| --- | ------------------------------------- |
| NN  | Noun                                  |
| NNS | Plural noun                           |
| NNP | Proper noun                           |
| PRP | Personal pronoun                      |
| VB  | Verb                                  |
| VBD | Past tense verb                       |
| VBG | Gerund/present participle             |
| VBN | Past participle                       |
| VBP | Present verb                          |
| VBZ | 3rd person singular verb              |
| JJ  | Adjective                             |
| RB  | Adverb                                |
| DT  | Determiner                            |
| IN  | Preposition/subordinating conjunction |
| CC  | Coordinating conjunction              |
| MD  | Modal                                 |
| CD  | Cardinal number                       |
| UH  | Interjection                          |

---

# 20. POS Tag-এর Example

Sentence:

```text
The boy is playing football.
```

Penn Treebank style:

```text
The       → DT
boy       → NN
is        → VBZ
playing   → VBG
football  → NN
```

এখানে:

```text
DT   → Determiner
NN   → Noun
VBZ  → Verb
VBG  → Verb form
```

---

# 21. NLTK দিয়ে POS Tagging

Install:

```bash
pip install nltk
```

প্রয়োজনীয় resource download করতে হবে।

```python
import nltk

nltk.download("punkt")
nltk.download("averaged_perceptron_tagger")
```

তারপর:

```python
from nltk.tokenize import word_tokenize
from nltk import pos_tag

sentence = "The boy is playing football."

tokens = word_tokenize(sentence)

tags = pos_tag(tokens)

print(tags)
```

Output-এর মতো কিছু পাওয়া যাবে:

```text
[
    ('The', 'DT'),
    ('boy', 'NN'),
    ('is', 'VBZ'),
    ('playing', 'VBG'),
    ('football', 'NN'),
    ('.', '.')
]
```

---

# 22. POS Tag থেকে Meaning

ধরো:

```python
[
    ("The", "DT"),
    ("boy", "NN"),
    ("is", "VBZ"),
    ("playing", "VBG")
]
```

আমরা বুঝতে পারি:

```text
The      → Determiner
boy      → Noun
is       → Verb/Auxiliary
playing  → Verb
```

এখন NLP system linguistic structure সম্পর্কে information পায়।

---

# 23. POS + Lemmatization

এটি আমাদের জন্য সবচেয়ে গুরুত্বপূর্ণ connection।

M02.08-এ দেখেছি:

```text
running → run
```

কিন্তু POS জানা থাকলে আরও ভালোভাবে করা যায়।

```text
running + Verb
       ↓
      run
```

Python:

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

word = "running"

lemma = lemmatizer.lemmatize(word, pos="v")

print(lemma)
```

Output:

```text
run
```

---

# 24. POS Mapping Problem

NLTK POS tag এবং WordNet POS একই format ব্যবহার করে না।

যেমন:

```text
NN → noun
VB → verb
JJ → adjective
RB → adverb
```

তাই mapping function বানানো যায়।

```python
def get_wordnet_pos(tag):
    if tag.startswith("J"):
        return "a"
    elif tag.startswith("V"):
        return "v"
    elif tag.startswith("N"):
        return "n"
    elif tag.startswith("R"):
        return "r"
    return "n"
```

তারপর:

```python
from nltk import pos_tag
from nltk.tokenize import word_tokenize
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

sentence = "The children are running quickly."

tokens = word_tokenize(sentence)

pos_tags = pos_tag(tokens)

for word, tag in pos_tags:
    pos = get_wordnet_pos(tag)
    lemma = lemmatizer.lemmatize(word, pos=pos)

    print(word, tag, "→", lemma)
```

Conceptually output:

```text
The        DT  → The
children   NNS → child
are        VBP → be
running    VBG → run
quickly    RB  → quickly
```

এটি অনেক বেশি powerful pipeline।

---

# 25. POS Tagging কীভাবে কাজ করে?

একটি POS tagger বিভিন্ন ধরনের information ব্যবহার করতে পারে:

```text
Word
+
Previous words
+
Next words
+
Sentence context
+
Statistical patterns
```

তারপর prediction:

```text
Token
 ↓
Context
 ↓
POS Model
 ↓
POS Tag
```

---

# 26. পুরনো POS Tagging Approaches

POS tagging-এর historical evolution:

```text
Rule-Based
     ↓
Statistical
     ↓
Machine Learning
     ↓
Neural Networks
     ↓
Transformer-based Models
```

---

# 27. Rule-Based POS Tagging

আগের system-গুলো manually তৈরি rule ব্যবহার করত।

উদাহরণ conceptually:

```text
যদি word-এর শেষে "ly" থাকে
→ সম্ভবত Adverb
```

যেমন:

```text
quickly
slowly
carefully
```

কিন্তু এটি সবসময় সঠিক নয়।

কারণ English language-এ অনেক exception আছে।

---

# 28. Statistical POS Tagging

পরবর্তী সময়ে statistical model ব্যবহার করা হয়।

Model training data থেকে শেখে:

```text
word
+
context
→
POS
```

যেমন:

```text
book
```

কোন context-এ noun বেশি এবং কোন context-এ verb বেশি—তা model শিখতে পারে।

---

# 29. Machine Learning POS Tagging

Features হতে পারে:

```text
current word
previous word
next word
suffix
prefix
capitalization
word shape
```

তারপর classifier:

```text
Features
   ↓
ML Model
   ↓
POS
```

---

# 30. Neural POS Tagging

Deep learning-এর মাধ্যমে:

```text
Tokens
 ↓
Embeddings
 ↓
Neural Network
 ↓
POS Predictions
```

LSTM/GRU ইত্যাদি historically ব্যবহার করা হয়েছে।

---

# 31. Transformer POS Tagging

Modern NLP-তে Transformer architecture ব্যবহার করা যায়।

Conceptually:

```text
Text
 ↓
Tokenizer
 ↓
Token Embeddings
 ↓
Transformer
 ↓
Contextual Representation
 ↓
POS Classification
```

এখানে model context অনেক ভালোভাবে ব্যবহার করতে পারে।

---

# 32. Context কেন গুরুত্বপূর্ণ?

ধরো:

```text
I will book a hotel.
```

এখানে:

```text
book → Verb
```

কিন্তু:

```text
I read a book.
```

এখানে:

```text
book → Noun
```

শুধু word দেখে POS নির্ধারণ করা কঠিন।

Context দরকার।

```text
book
 ↓
sentence context
 ↓
POS
```

---

# 33. Another Example: `light`

```text
The light is bright.
```

```text
light → Noun
```

কিন্তু:

```text
This bag is light.
```

```text
light → Adjective
```

আর:

```text
Please light the candle.
```

```text
light → Verb
```

একই word:

```text
light
```

তিনটি POS হতে পারে।

এটাই contextual NLP-এর গুরুত্ব।

---

# 34. POS Tagging বনাম NER

দুটো এক নয়।

### POS

Word-এর grammatical category:

```text
Dhaka → Proper Noun
```

### NER

Entity-এর semantic category:

```text
Dhaka → LOCATION
```

অর্থাৎ:

```text
POS:
Dhaka → NNP

NER:
Dhaka → GPE/LOCATION
```

---

# 35. POS Tagging বনাম Lemmatization

এগুলোও আলাদা।

### POS Tagging

```text
running → Verb
```

### Lemmatization

```text
running → run
```

দুটো একসঙ্গে:

```text
running
   ↓
POS Tagging
   ↓
Verb
   ↓
Lemmatization
   ↓
run
```

---

# 36. POS Tagging বনাম Tokenization

### Tokenization

```text
I love NLP.
```

↓

```text
I
love
NLP
.
```

### POS Tagging

↓

```text
I    → Pronoun
love → Verb
NLP  → Noun
.    → Punctuation
```

অর্থাৎ:

```text
Tokenization = "কী কী token আছে?"

POS Tagging = "প্রতিটি token-এর grammatical role কী?"
```

---

# 37. AI Writing Assistant-এ POS

আমাদের AI writing assistant-এর ক্ষেত্রে POS খুব useful।

ধরো user লিখেছে:

```text
He quickly writes professional emails.
```

System বুঝতে পারে:

```text
He           → Pronoun
quickly      → Adverb
writes       → Verb
professional → Adjective
emails       → Noun
```

এখন linguistic structure analysis করা সম্ভব।

---

# 38. Grammar Analysis

POS tagging দিয়ে basic grammar patterns detect করা যায়।

যেমন:

```text
Determiner + Adjective + Noun
```

Example:

```text
the + intelligent + student
```

এটি একটি common noun phrase pattern।

আর:

```text
Pronoun + Verb + Adverb
```

যেমন:

```text
He + runs + quickly
```

---

# 39. Writing Style Analysis

POS distribution থেকেও writing style সম্পর্কে features তৈরি করা যায়।

উদাহরণ:

```text
Noun ratio
Verb ratio
Adjective ratio
Adverb ratio
Pronoun ratio
```

একটি document:

```text
Noun = 20%
Verb = 15%
Adjective = 10%
Adverb = 5%
Pronoun = 12%
```

এ ধরনের features statistical text analysis-এ ব্যবহার করা যায়।

---

# 40. AI Text Analysis

আমাদের future platform-এ:

```text
User Text
     ↓
Tokenization
     ↓
POS Tagging
     ↓
Lemmatization
     ↓
Feature Extraction
     ↓
Text Analysis
```

Features হতে পারে:

```text
POS distribution
Sentence length
Word frequency
Vocabulary diversity
Verb ratio
Noun ratio
Adjective ratio
Adverb ratio
```

এগুলো **শুধু একটি feature set**; এগুলো একা কোনো reliable AI detector তৈরি করে না।

---

# 41. POS Tagging-এর Limitations

POS tagging perfect নয়।

### Ambiguity

```text
book
light
run
```

context অনুযায়ী POS পরিবর্তন করতে পারে।

### Domain-specific text

```text
AI
API
Django
TensorFlow
GPT
```

এগুলো সাধারণ corpus-এর বাইরে হলে tagger ভুল করতে পারে।

### Informal text

```text
u
gonna
wanna
lol
```

এগুলোতে সমস্যা হতে পারে।

### Spelling mistakes

```text
I am lerning Python.
```

এখানে tagger ভুল করতে পারে।

---

# 42. Bangla NLP

Bangla POS tagging আরও challenging হতে পারে।

উদাহরণ:

```text
আমি বাংলায় লিখি।
```

Conceptually:

```text
আমি       → Pronoun
বাংলায়    → Noun/related category
লিখি      → Verb
```

Bangla-তে:

* morphology
* suffix
* inflection
* word order
* ambiguity
* tokenization

ইত্যাদি কারণে POS tagging-এর জন্য language-specific model/resource প্রয়োজন হতে পারে।

---

# 43. Complete NLP Connection

এখন আমাদের শেখা concepts:

```text
RAW TEXT
   ↓
TOKENIZATION
   ↓
TOKENS
   ↓
POS TAGGING
   ↓
GRAMMATICAL INFORMATION
   ↓
LEMMATIZATION
   ↓
NORMALIZED WORDS
   ↓
FEATURE EXTRACTION
   ↓
MODEL
```

---

# 44. একটি Full Example

Input:

```text
"The children are running quickly in the garden."
```

### Step 1 — Tokenization

```text
The
children
are
running
quickly
in
the
garden
```

### Step 2 — POS

```text
The       → Determiner
children  → Noun
are       → Verb
running   → Verb
quickly   → Adverb
in        → Preposition
the       → Determiner
garden    → Noun
```

### Step 3 — Lemmatization

```text
The       → the
children  → child
are       → be
running   → run
quickly   → quickly
in        → in
the       → the
garden    → garden
```

Final:

```text
the child be run quickly in the garden
```

এটি **analysis representation**, final natural-language output নয়।

---

# 45. Important Pipeline Order

একটি classical NLP pipeline-এ:

```text
Raw Text
   ↓
Cleaning
   ↓
Sentence Segmentation
   ↓
Tokenization
   ↓
POS Tagging
   ↓
Lemmatization
   ↓
Feature Extraction
```

এখানে POS → Lemmatization খুব common relationship।

তবে production NLP system-এ exact order **task ও library অনুযায়ী পরিবর্তিত হতে পারে**।

---

# 46. Practice — Beginner

নিচের sentence-এর POS নিজে বের করো:

```text
The smart student writes code quickly.
```

Expected concept:

```text
The       → Determiner
smart     → Adjective
student   → Noun
writes    → Verb
code      → Noun
quickly   → Adverb
```

---

# 47. Practice — Intermediate

এই sentence analyze করো:

```text
She is learning Python because she wants to become a developer.
```

তোমাকে বের করতে হবে:

```text
1. Tokens
2. POS
3. Lemmas
```

---

# 48. Practice — Advanced

এই sentence:

```text
The experienced developers are building powerful AI applications.
```

একটি Python program বানাও যা বের করবে:

```text
Word
POS Tag
Lemma
```

Expected structure:

```text
Word          POS       Lemma
--------------------------------
The           DT        the
experienced   JJ        experienced
developers    NNS       developer
are           VBP       be
building      VBG       build
powerful      JJ        powerful
AI            NNP       AI
applications  NNS       application
```

---

# 49. Theory Questions

নিজেকে প্রশ্ন করো:

1. POS কী?
2. POS Tagging কী?
3. Noun কী?
4. Verb কী?
5. Adjective কী?
6. Adverb কী?
7. Pronoun কী?
8. Determiner কী?
9. Preposition কী?
10. Conjunction কী?
11. Auxiliary verb কী?
12. Modal verb কী?
13. POS tag কী?
14. `NN`, `VB`, `JJ`, `RB` কী?
15. Context কেন POS tagging-এর জন্য গুরুত্বপূর্ণ?
16. `book` কীভাবে noun এবং verb দুটোই হতে পারে?
17. POS এবং NER-এর পার্থক্য কী?
18. POS এবং Lemmatization-এর সম্পর্ক কী?
19. POS tagging-এর limitations কী?
20. Modern Transformer POS tagging কীভাবে করতে পারে?

---

# 50. Interview Questions

### Q1. What is POS tagging?

> POS tagging is the process of assigning a grammatical category to each token in a sentence.

### Q2. Why is POS tagging important?

> It provides grammatical information that can support lemmatization, parsing, information extraction, text analysis, and other NLP tasks.

### Q3. Difference between POS tagging and tokenization?

```text
Tokenization → identifies tokens
POS tagging  → identifies grammatical roles
```

### Q4. Difference between POS tagging and NER?

```text
POS → grammatical category
NER → semantic entity category
```

### Q5. Why is context important?

কারণ একই word বিভিন্ন sentence-এ বিভিন্ন grammatical role নিতে পারে।

```text
book → noun
book → verb
```

---

# 51. M02.09 Completion Checklist

নিজেকে check করো:

* [ ] POS বুঝি
* [ ] POS Tagging বুঝি
* [ ] Noun বুঝি
* [ ] Proper Noun বুঝি
* [ ] Pronoun বুঝি
* [ ] Verb বুঝি
* [ ] Auxiliary Verb বুঝি
* [ ] Modal বুঝি
* [ ] Adjective বুঝি
* [ ] Adverb বুঝি
* [ ] Preposition বুঝি
* [ ] Conjunction বুঝি
* [ ] Determiner বুঝি
* [ ] Interjection বুঝি
* [ ] Penn Treebank tags সম্পর্কে জানি
* [ ] NLTK POS tagging করতে পারি
* [ ] POS + Lemmatization বুঝি
* [ ] Contextual POS বুঝি
* [ ] POS বনাম NER বুঝি
* [ ] POS বনাম Tokenization বুঝি
* [ ] POS বনাম Lemmatization বুঝি
* [ ] AI text analysis-এ POS-এর ব্যবহার বুঝি

---

# 🔑 আজকের সবচেয়ে গুরুত্বপূর্ণ Mental Model

```text
                 TEXT
                   ↓
              TOKENIZATION
                   ↓
                 TOKEN
                   ↓
              POS TAGGING
                   ↓
          Grammatical Role
                   ↓
            LEMMATIZATION
                   ↓
                 LEMMA
                   ↓
          FEATURE EXTRACTION
                   ↓
              NLP MODEL
```

আর তিনটি concept আলাদা করে মনে রাখবে:

```text
Tokenization
→ "এটা কোন কোন token?"

POS Tagging
→ "প্রতিটি token কী grammatical role পালন করছে?"

Lemmatization
→ "এই word-এর base/dictionary form কী?"
```

**M02.09 complete.**

পরবর্তী ধাপে **M02.10 — Named Entity Recognition (NER) Deep Dive** এ গেলে আমরা `Person`, `Organization`, `Location`, `Date`, `Money`, `Product` ইত্যাদি entity কীভাবে text থেকে শনাক্ত করা হয় এবং POS-এর সঙ্গে NER-এর পার্থক্য কী—সেটা শিখব।


---
# M02.10 — Named Entity Recognition (NER) Deep Dive

M02.09-এ আমরা **POS Tagging** শিখেছি। সেখানে system বুঝেছে একটি word **Noun, Verb, Adjective, Pronoun** ইত্যাদি।

এখন আমরা আরও এক ধাপ এগোবো:

> **NER আমাদের বলে text-এর মধ্যে কোন word/phrase একটি গুরুত্বপূর্ণ real-world entity এবং সেটি কী ধরনের entity।**

এটি NLP-এর অত্যন্ত গুরুত্বপূর্ণ foundation topic।

---

# 1. NER কী?

**NER = Named Entity Recognition**

NER হলো এমন একটি NLP task যেখানে text থেকে **named entities** শনাক্ত করা এবং তাদের category নির্ধারণ করা হয়।

উদাহরণ:

> **Md. Atiar Rahman lives in Dhaka and works with Python.**

NER conceptually:

```text
Md. Atiar Rahman → PERSON
Dhaka            → LOCATION
Python           → PRODUCT / TECHNOLOGY
```

অর্থাৎ:

```text
Text
 ↓
Entity Detection
 ↓
Entity Classification
```

---

# 2. Entity কী?

**Entity** বলতে text-এর মধ্যে এমন কোনো ব্যক্তি, জায়গা, প্রতিষ্ঠান, তারিখ, টাকা, product ইত্যাদিকে বোঝানো হয় যার real-world meaning বা identifiable reference আছে।

উদাহরণ:

```text
Rahim
Dhaka
Google
Bangladesh
2026
$500
Python
```

এগুলো context অনুযায়ী entity হতে পারে।

---

# 3. Named Entity কী?

সব noun named entity নয়।

উদাহরণ:

```text
student
city
company
country
```

এগুলো সাধারণ noun।

কিন্তু:

```text
Rahim
Dhaka
Google
Bangladesh
```

নির্দিষ্ট entity।

তাই:

```text
Noun
 ↓
Generic noun / Named entity
```

---

# 4. NER-এর মূল কাজ

NER সাধারণত দুইটি কাজ করে:

### Step 1 — Entity Detection

Text-এর কোন অংশ entity তা খুঁজে বের করা।

### Step 2 — Entity Classification

Entity কোন category-এর তা নির্ধারণ করা।

উদাহরণ:

```text
I live in Dhaka.
```

প্রথমে:

```text
Dhaka
```

খুঁজে বের করবে।

তারপর:

```text
Dhaka → LOCATION
```

---

# 5. Common NER Categories

সবচেয়ে common entity types:

| Entity       | Meaning                       |
| ------------ | ----------------------------- |
| PERSON       | ব্যক্তি                       |
| ORGANIZATION | প্রতিষ্ঠান                    |
| LOCATION     | স্থান                         |
| GPE          | দেশ/শহর/রাজনৈতিক এলাকা        |
| DATE         | তারিখ                         |
| TIME         | সময়                           |
| MONEY        | টাকা                          |
| PERCENT      | শতাংশ                         |
| PRODUCT      | পণ্য                          |
| EVENT        | ঘটনা                          |
| LAW          | আইন                           |
| LANGUAGE     | ভাষা                          |
| NORP         | জাতীয়তা/ধর্মীয়/রাজনৈতিক group |
| FACILITY     | স্থাপনা                       |

Library/model অনুযায়ী labels কিছুটা পরিবর্তিত হতে পারে।

---

# 6. PERSON

ব্যক্তির নাম।

উদাহরণ:

```text
Elon Musk
Albert Einstein
William Shakespeare
```

Sentence:

```text
Elon Musk founded SpaceX.
```

NER:

```text
Elon Musk → PERSON
SpaceX    → ORGANIZATION
```

---

# 7. ORGANIZATION

Company, university, government organization, institution ইত্যাদি।

উদাহরণ:

```text
Google
Microsoft
NASA
Green University
United Nations
```

Sentence:

```text
Google developed several AI technologies.
```

```text
Google → ORGANIZATION
```

---

# 8. LOCATION

ভৌগোলিক স্থান।

উদাহরণ:

```text
Dhaka
London
Asia
Pacific Ocean
```

তবে কিছু model `LOCATION` এবং `GPE` আলাদা করে।

---

# 9. GPE

**GPE = Geopolitical Entity**

দেশ, city, state ইত্যাদি political/geographical entity।

উদাহরণ:

```text
Bangladesh
Dhaka
United States
India
```

spaCy-এর common labels-এর মধ্যে `GPE` রয়েছে।

---

# 10. DATE

Date-related entity।

উদাহরণ:

```text
September 6, 2026
January 2025
Monday
tomorrow
```

Sentence:

```text
The meeting will be held on September 6, 2026.
```

```text
September 6, 2026 → DATE
```

---

# 11. TIME

সময়:

```text
10:30 AM
5 PM
midnight
noon
```

Example:

```text
The meeting starts at 10 AM.
```

```text
10 AM → TIME
```

---

# 12. MONEY

Financial value।

```text
$500
৳10,000
€200
5 million dollars
```

Example:

```text
The phone costs $500.
```

```text
$500 → MONEY
```

---

# 13. PERCENT

Percentage:

```text
50%
10 percent
99.5%
```

Example:

```text
The model achieved 95% accuracy.
```

```text
95% → PERCENT
```

---

# 14. PRODUCT

Specific product name।

উদাহরণ:

```text
iPhone 17
PlayStation
Windows
GPT
```

তবে exact label model/corpus অনুযায়ী পরিবর্তিত হতে পারে।

---

# 15. একটি Complete Example

Sentence:

> Microsoft announced a $10 billion investment in London on September 6, 2026.

NER:

```text
Microsoft           → ORGANIZATION
$10 billion         → MONEY
London              → GPE/LOCATION
September 6, 2026   → DATE
```

এটাই NER-এর মূল কাজ।

---

# 16. POS বনাম NER

এটি খুব গুরুত্বপূর্ণ।

ধরো:

> Rahim lives in Dhaka.

POS:

```text
Rahim  → Proper Noun
lives  → Verb
Dhaka  → Proper Noun
```

NER:

```text
Rahim → PERSON
Dhaka → GPE
```

অর্থাৎ:

```text
POS
↓
Grammatical category

NER
↓
Real-world entity category
```

---

# 17. আরেকটি Example

```text
Google is located in California.
```

POS:

```text
Google     → Proper Noun
is         → Verb
located    → Verb
California → Proper Noun
```

NER:

```text
Google     → ORGANIZATION
California → GPE/LOCATION
```

একটি entity একই সঙ্গে:

```text
POS = Proper Noun
NER = Organization
```

হতে পারে।

---

# 18. NER বনাম Lemmatization

Lemmatization:

```text
cars → car
running → run
children → child
```

NER:

```text
Dhaka → GPE
Google → ORGANIZATION
Rahim → PERSON
```

দুটোর উদ্দেশ্য সম্পূর্ণ আলাদা।

```text
Lemmatization
→ word normalization

NER
→ entity identification
```

---

# 19. NER বনাম Tokenization

Tokenization:

```text
Google develops AI.
```

↓

```text
Google
develops
AI
.
```

NER:

```text
Google → ORGANIZATION
AI     → potentially ORG/PRODUCT/technology depending on model/context
```

তাই:

```text
Tokenization
→ text ভাঙে

NER
→ entity খুঁজে এবং classify করে
```

---

# 20. NER কেন কঠিন?

একটি word-এর meaning context-এর ওপর নির্ভর করতে পারে।

উদাহরণ:

```text
Apple
```

এটি হতে পারে:

```text
Apple → ORGANIZATION
```

যদি:

> Apple released a new product.

কিন্তু:

> I ate an apple.

এখানে:

```text
apple → সাধারণ noun
```

---

# 21. Context-এর গুরুত্ব

NER context ব্যবহার করে।

```text
Washington
```

হতে পারে:

```text
Washington → PERSON
```

অথবা:

```text
Washington → LOCATION/GPE
```

Sentence:

> George Washington was the first U.S. president.

```text
George Washington → PERSON
```

কিন্তু:

> Washington is the capital of the state.

এখানে location interpretation হতে পারে।

---

# 22. Multi-Word Entity

একটি entity সবসময় একটি token নয়।

উদাহরণ:

```text
New York
```

এখানে:

```text
New → ?
York → ?
```

কিন্তু পুরো phrase:

```text
New York → GPE
```

একইভাবে:

```text
United States
Google DeepMind
Albert Einstein
```

এগুলো multi-token entity।

এটি NER-এর গুরুত্বপূর্ণ feature।

---

# 23. BIO Tagging

NER dataset-এ entity boundaries represent করার জন্য **BIO tagging** খুব গুরুত্বপূর্ণ।

BIO:

```text
B = Beginning
I = Inside
O = Outside
```

উদাহরণ:

> Barack Obama visited New York.

Tokens:

```text
Barack
Obama
visited
New
York
```

BIO:

```text
Barack   → B-PER
Obama    → I-PER
visited  → O
New      → B-GPE
York     → I-GPE
```

---

# 24. B কেন দরকার?

ধরো:

```text
New York University
```

তিনটি token।

BIO:

```text
New        → B-ORG
York       → I-ORG
University → I-ORG
```

এতে model বুঝতে পারে পুরো phrase-টি একটি entity।

---

# 25. B এবং I-এর পার্থক্য

```text
B-PER
```

মানে:

> একটি PERSON entity-এর শুরু।

```text
I-PER
```

মানে:

> সেই PERSON entity-এর ভিতরের অংশ।

```text
O
```

মানে:

> কোনো entity-এর অংশ নয়।

---

# 26. Example

Sentence:

> Elon Musk founded SpaceX in California.

BIO:

```text
Elon       → B-PER
Musk       → I-PER
founded    → O
SpaceX     → B-ORG
in         → O
California → B-GPE
```

---

# 27. NER-এর Historical Approaches

NER-এর development:

```text
Rule-Based
     ↓
Dictionary / Gazetteer
     ↓
Statistical Models
     ↓
Machine Learning
     ↓
Deep Learning
     ↓
Transformer Models
```

---

# 28. Rule-Based NER

Manually তৈরি rules ব্যবহার করা হয়।

উদাহরণ:

```text
যদি "Mr."-এর পরে একটি capitalized word আসে
→ সম্ভবত PERSON
```

যেমন:

```text
Mr. Rahim
```

কিন্তু সমস্যা:

* অনেক exception
* language dependent
* context বোঝা কঠিন
* maintenance কঠিন

---

# 29. Gazetteer / Dictionary Approach

একটি predefined entity list থাকে।

যেমন:

```text
Cities:
Dhaka
London
Paris
Tokyo
```

যদি text-এ পাওয়া যায়:

```text
I live in Dhaka.
```

তাহলে:

```text
Dhaka → LOCATION
```

এটি useful হলেও সীমাবদ্ধ।

কারণ নতুন entity dictionary-তে নাও থাকতে পারে।

---

# 30. Machine Learning NER

ML model features ব্যবহার করে শেখে:

```text
Current word
Previous word
Next word
Capitalization
Prefix
Suffix
POS
Context
```

তারপর:

```text
Features
 ↓
ML Model
 ↓
Entity Label
```

---

# 31. Deep Learning NER

Neural network-based approach:

```text
Tokens
 ↓
Embeddings
 ↓
BiLSTM / Neural Network
 ↓
Entity Classification
```

Historical systems-এ BiLSTM-CRF খুব জনপ্রিয় ছিল।

---

# 32. CRF কী?

**CRF = Conditional Random Field**

NER-এ sequence-এর labelগুলোর relationship model করতে CRF ব্যবহার করা হয়েছে।

যেমন:

```text
B-PER
I-PER
I-PER
```

এটি logical sequence।

কিন্তু:

```text
I-PER
B-ORG
```

এর মতো transition কিছু context-এ অস্বাভাবিক হতে পারে।

CRF sequence-level consistency improve করতে পারে।

---

# 33. Transformer-based NER

Modern approach:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Transformer
 ↓
Contextual Embeddings
 ↓
Token Classification
 ↓
NER Labels
```

উদাহরণ:

```text
Elon Musk visited Paris.
```

Model output:

```text
Elon Musk → PERSON
Paris     → LOCATION
```

---

# 34. NER সাধারণত Token Classification

Transformer-based NER-এ অনেক সময় প্রতিটি token-এর জন্য label predict করা হয়।

Conceptually:

```text
Token 1 → Label
Token 2 → Label
Token 3 → Label
...
```

যেমন:

```text
Elon      → B-PER
Musk      → I-PER
visited   → O
Paris     → B-LOC
```

---

# 35. Subword Tokenization-এর সমস্যা

Modern Transformer tokenizer অনেক সময় একটি word-কে কয়েকটি subword-এ ভাগ করে।

ধরো conceptually:

```text
Washington
     ↓
Wash + ington
```

NER label তখন token-level alignment করতে হয়।

অর্থাৎ:

```text
Original Word
      ↓
Subword Tokens
      ↓
NER Labels
```

Training pipeline-এ এটি গুরুত্বপূর্ণ technical problem।

---

# 36. NER + POS

আমরা এখন তিনটি layer বুঝতে পারি:

```text
Text
 ↓
Tokenization
 ↓
POS
 ↓
NER
 ↓
Lemmatization
```

উদাহরণ:

```text
Google released a new product in Dhaka.
```

Possible analysis:

```text
Google   → NNP → ORGANIZATION
released → VBD → Verb
a        → DT  → Determiner
new      → JJ  → Adjective
product  → NN  → Noun
in       → IN  → Preposition
Dhaka    → NNP → GPE
```

এটি অনেক rich linguistic representation।

---

# 37. NER + Lemmatization

NER এবং Lemmatization একসঙ্গে ব্যবহার করা যায়।

কিন্তু entity name-এর ক্ষেত্রে blindly lemmatization করা উচিত নয়।

উদাহরণ:

```text
Microsoft
```

এটি entity name।

একে সাধারণ linguistic normalization-এর মাধ্যমে পরিবর্তন করা উচিত নয়।

Architecture:

```text
Text
 ↓
Tokenization
 ↓
POS / NER
 ↓
Linguistic Analysis
```

Entity preservation গুরুত্বপূর্ণ।

---

# 38. AI Writing Assistant-এ NER

আমাদের future AI writing assistant-এর জন্য NER অত্যন্ত useful।

ধরো user লিখল:

> I visited Dhaka and attended a conference at Green University.

NER:

```text
Dhaka            → GPE
Green University → ORGANIZATION
```

এখন rewrite করার সময় system বুঝতে পারে এগুলো **important named entities**।

---

# 39. Entity Preservation

AI rewriting system-এ এটি খুব গুরুত্বপূর্ণ।

Original:

> Microsoft released Windows in 2025.

Rewrite করার সময়:

```text
Microsoft
Windows
2025
```

এর মতো entities ভুলভাবে পরিবর্তন করা উচিত নয়।

তাই:

```text
Original Text
 ↓
NER
 ↓
Entity Detection
 ↓
Entity Protection
 ↓
Rewrite Model
```

এটি production writing system-এর একটি গুরুত্বপূর্ণ design concept।

---

# 40. Information Extraction

NER হলো **Information Extraction** pipeline-এর foundation।

উদাহরণ:

> Elon Musk founded SpaceX in 2002.

NER:

```text
Elon Musk → PERSON
SpaceX → ORGANIZATION
2002 → DATE
```

তারপর relation extraction:

```text
Elon Musk
    ↓ founded
SpaceX
    ↓ in
2002
```

এভাবে structured information তৈরি করা যায়।

---

# 41. Knowledge Graph-এর সঙ্গে সম্পর্ক

NER:

```text
Elon Musk → PERSON
SpaceX → ORGANIZATION
```

Relation Extraction:

```text
Elon Musk → founded → SpaceX
```

Knowledge Graph:

```text
[Elon Musk]
      |
    founded
      |
   [SpaceX]
```

অর্থাৎ:

```text
NER
 ↓
Relation Extraction
 ↓
Knowledge Graph
```

---

# 42. Search System-এ NER

User search করল:

> hotels in Dhaka

NER:

```text
Dhaka → LOCATION
```

Search engine বুঝতে পারে:

```text
Query Entity:
LOCATION = Dhaka
```

এটি search relevance improve করতে পারে।

---

# 43. Document Analysis

একটি document থেকে extract করা যায়:

```text
People
Organizations
Locations
Dates
Money
Products
Events
```

তারপর structured JSON:

```python
{
    "people": ["Elon Musk"],
    "organizations": ["SpaceX"],
    "locations": ["California"],
    "dates": ["2002"]
}
```

এটি backend/API-তে খুব useful।

---

# 44. Python দিয়ে spaCy NER

spaCy NER-এর জন্য খুব জনপ্রিয় NLP library।

Install:

```bash
pip install spacy
```

English model install:

```bash
python -m spacy download en_core_web_sm
```

---

# 45. Basic spaCy NER

```python
import spacy

nlp = spacy.load("en_core_web_sm")

text = "Apple was founded by Steve Jobs in California."

doc = nlp(text)

for ent in doc.ents:
    print(ent.text, "→", ent.label_)
```

Possible output:

```text
Apple → ORG
Steve Jobs → PERSON
California → GPE
```

---

# 46. Entity Explanation

spaCy-তে label-এর meaning দেখতে:

```python
import spacy

nlp = spacy.load("en_core_web_sm")

print(spacy.explain("ORG"))
print(spacy.explain("PERSON"))
print(spacy.explain("GPE"))
```

Conceptually:

```text
ORG    → Organization
PERSON → People
GPE    → Geopolitical Entity
```

---

# 47. Complete Example

```python
import spacy

nlp = spacy.load("en_core_web_sm")

text = """
Microsoft announced a $10 billion investment
in London on September 6, 2026.
"""

doc = nlp(text)

for ent in doc.ents:
    print(
        f"Entity: {ent.text} | "
        f"Label: {ent.label_} | "
        f"Description: {spacy.explain(ent.label_)}"
    )
```

Possible entities:

```text
Microsoft → ORG
$10 billion → MONEY
London → GPE
September 6, 2026 → DATE
```

Exact output/model behavior can vary by model version.

---

# 48. NER থেকে JSON তৈরি

আমাদের backend-এর জন্য:

```python
entities = []

for ent in doc.ents:
    entities.append({
        "text": ent.text,
        "label": ent.label_
    })

print(entities)
```

Result conceptually:

```python
[
    {
        "text": "Microsoft",
        "label": "ORG"
    },
    {
        "text": "London",
        "label": "GPE"
    }
]
```

এটি পরে Django REST API থেকে return করা সম্ভব।

---

# 49. AI Writing Platform Architecture

আমাদের project-এ:

```text
                USER TEXT
                    │
                    ↓
               Tokenization
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
     POS TAGGING              NER
          │                   │
          ↓                   ↓
    Grammar Info         Entity Info
          │                   │
          └─────────┬─────────┘
                    ↓
              Lemmatization
                    ↓
             Feature Extraction
                    ↓
              Text Analysis
                    ↓
             Writing Model
                    ↓
              Improved Text
```

---

# 50. NER এবং AI Rewrite

ধরো:

```text
Original:
Google released Gemini in 2024.
```

NER:

```text
Google  → ORG
Gemini  → PRODUCT/ORG depending on model
2024    → DATE
```

Rewrite model-এর উচিত:

```text
Google
Gemini
2024
```

এর semantic identity preserve করা।

---

# 51. NER-এর Limitations

NER perfect নয়।

### Ambiguity

```text
Apple
Amazon
Jordan
Washington
```

একাধিক meaning থাকতে পারে।

### Unknown entities

নতুন company/product/model হলে pretrained model ভুল করতে পারে।

### Spelling errors

```text
Micosoft
```

এ ধরনের typo entity recognition কঠিন করে।

### Domain-specific language

Medical, legal, financial, scientific text-এর জন্য general NER model যথেষ্ট নাও হতে পারে।

### Multilingual text

English model দিয়ে Bangla text-এর ভালো NER আশা করা যায় না।

---

# 52. Custom NER

নিজের domain-এর জন্য custom NER model train করা যায়।

ধরো আমাদের AI platform-এর জন্য custom entity:

```text
AI_MODEL
WRITING_STYLE
FEATURE
TECHNOLOGY
FRAMEWORK
```

Input:

> We use Django with a Transformer model.

Custom NER:

```text
Django       → FRAMEWORK
Transformer  → AI_MODEL
```

এটি domain-specific NLP system তৈরিতে useful।

---

# 53. NER Training Data

Custom NER-এর জন্য annotated dataset প্রয়োজন।

উদাহরণ:

```text
Google released Gemini.
```

Labels:

```text
Google    → B-ORG
released  → O
Gemini    → B-PRODUCT
```

অনেক annotated example থেকে model pattern শিখবে।

---

# 54. NER Evaluation

NER-এর জন্য সাধারণ metrics:

```text
Precision
Recall
F1-score
```

### Precision

Model যে entities detect করেছে তার মধ্যে কতগুলো সঠিক?

### Recall

Actual entities-এর কতগুলো model detect করতে পেরেছে?

### F1

Precision এবং Recall-এর harmonic mean।

```text
F1 = 2 × Precision × Recall
           ───────────────
           Precision + Recall
```

---

# 55. Entity-level Evaluation

NER-এ শুধু token accuracy যথেষ্ট নাও হতে পারে।

উদাহরণ:

```text
New York University
```

পুরো entity boundary এবং label সঠিকভাবে detect করা গুরুত্বপূর্ণ।

তাই অনেক NER benchmark-এ **entity-level precision/recall/F1** বেশি meaningful।

---

# 56. আজ পর্যন্ত NLP Foundation

এখন আমাদের foundation অনেক শক্ত হয়েছে:

```text
M02.01
NLP Introduction
       ↓
M02.02
Text & Language Fundamentals
       ↓
M02.03
NLP Pipeline
       ↓
M02.04
Text Preprocessing
       ↓
M02.06
Stopwords
       ↓
M02.07
Stemming
       ↓
M02.08
Lemmatization
       ↓
M02.09
POS Tagging
       ↓
M02.10
NER
```

---

# 57. সব Concepts একসঙ্গে

একটি sentence:

> Elon Musk visited Dhaka and discussed AI.

আমাদের pipeline conceptually:

### Tokenization

```text
Elon
Musk
visited
Dhaka
and
discussed
AI
```

### POS

```text
Elon       → Proper Noun
Musk       → Proper Noun
visited    → Verb
Dhaka      → Proper Noun
and        → Conjunction
discussed  → Verb
AI         → Noun/Proper Noun depending on tagger
```

### NER

```text
Elon Musk → PERSON
Dhaka     → GPE
AI        → technology-related entity depending on model
```

### Lemmatization

```text
visited   → visit
discussed → discuss
```

এখন text সম্পর্কে আমাদের কাছে অনেক richer information আছে।

---

# 58. Final Mental Model

এটি ভালোভাবে মনে রাখবে:

```text
                     RAW TEXT
                         │
                         ↓
                    TOKENIZATION
                         │
                         ↓
                       TOKENS
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
            POS         NER      LEMMATIZATION
             ↓           ↓           ↓
        Grammar       Entities      Lemmas
             │           │           │
             └───────────┼───────────┘
                         ↓
                  FEATURE EXTRACTION
                         ↓
                    NLP MODEL
```

সবচেয়ে গুরুত্বপূর্ণ distinction:

```text
Tokenization
→ Text-এর অংশগুলো কী?

POS
→ Word-এর grammatical role কী?

NER
→ Word/phrase কোন real-world entity?

Lemmatization
→ Word-এর base/dictionary form কী?
```

---

# 59. Practice Tasks

### Beginner

এই sentence থেকে entities বের করো:

```text
"Rahim lives in Dhaka and works at Google."
```

Expected:

```text
Rahim  → PERSON
Dhaka  → LOCATION/GPE
Google → ORGANIZATION
```

### Intermediate

```text
"Microsoft invested $10 billion in OpenAI in 2025."
```

Find:

```text
PERSON
ORGANIZATION
MONEY
DATE
```

### Advanced

spaCy দিয়ে একটি program বানাও:

```text
Input:
"Elon Musk founded SpaceX in 2002."
```

Output format:

```text
Entity        Label
------------------------
Elon Musk     PERSON
SpaceX        ORG
2002          DATE
```

তারপর JSON format-এ save করো।

---

# 60. Theory Questions

নিজেকে এগুলো জিজ্ঞেস করো:

1. NER কী?
2. Named Entity কী?
3. NER-এর দুটি প্রধান কাজ কী?
4. PERSON কী?
5. ORGANIZATION কী?
6. LOCATION কী?
7. GPE কী?
8. DATE কী?
9. MONEY কী?
10. PERCENT কী?
11. POS এবং NER-এর পার্থক্য কী?
12. NER এবং Lemmatization-এর পার্থক্য কী?
13. Context NER-এর জন্য কেন গুরুত্বপূর্ণ?
14. Multi-word entity কী?
15. BIO tagging কী?
16. B-PER কী?
17. I-PER কী?
18. O কী?
19. Gazetteer কী?
20. CRF কী?
21. Transformer-based NER কীভাবে কাজ করে?
22. NER-এর limitations কী?
23. Custom NER কেন প্রয়োজন হতে পারে?
24. NER-এর জন্য Precision/Recall/F1 কেন গুরুত্বপূর্ণ?
25. AI writing assistant-এ NER কেন দরকার?

---

# 61. M02.10 Completion Checklist

* [ ] NER বুঝি
* [ ] Named Entity বুঝি
* [ ] Entity Detection বুঝি
* [ ] Entity Classification বুঝি
* [ ] PERSON বুঝি
* [ ] ORGANIZATION বুঝি
* [ ] LOCATION বুঝি
* [ ] GPE বুঝি
* [ ] DATE বুঝি
* [ ] TIME বুঝি
* [ ] MONEY বুঝি
* [ ] PERCENT বুঝি
* [ ] PRODUCT বুঝি
* [ ] Multi-word Entity বুঝি
* [ ] BIO Tagging বুঝি
* [ ] B/I/O বুঝি
* [ ] Rule-based NER বুঝি
* [ ] Gazetteer বুঝি
* [ ] ML NER বুঝি
* [ ] Deep Learning NER বুঝি
* [ ] Transformer NER বুঝি
* [ ] NER বনাম POS বুঝি
* [ ] NER বনাম Lemmatization বুঝি
* [ ] NER + AI Writing বুঝি
* [ ] Entity Preservation বুঝি
* [ ] Custom NER concept বুঝি
* [ ] NER evaluation বুঝি
* [ ] spaCy দিয়ে basic NER করতে পারি

## 🔑 আজকের মূল কথা

```text
POS → grammatical role
NER → real-world entity
Lemma → base word
Token → text-এর ছোট unit
```

উদাহরণ:

```text
"Elon Musk visited Dhaka."

Elon Musk
→ POS: Proper Noun
→ NER: PERSON

visited
→ POS: Verb
→ Lemma: visit

Dhaka
→ POS: Proper Noun
→ NER: GPE/LOCATION
```

**M02.10 complete.**
পরবর্তী lesson হবে **M02.11 — Chunking / Shallow Parsing (NP, VP, Phrase Structure) Deep Dive**। এখানে আমরা POS tag-এর ওপর ভিত্তি করে কীভাবে `Noun Phrase`, `Verb Phrase`, `Prepositional Phrase` ইত্যাদি group করা হয় এবং NER/POS-এর পর parsing-এর দিকে কীভাবে যাওয়া হয় তা শিখব।

---
# M02.11 — Chunking / Shallow Parsing Deep Dive

M02.10-এ আমরা **NER** শিখেছি। এখন আমরা POS-tagged words-কে কীভাবে **meaningful phrase/group** হিসেবে একত্র করা যায়, সেটা শিখব।

এই topic-এর মূল উদ্দেশ্য:

> **একটি sentence-এর কোন কোন word একসঙ্গে একটি phrase হিসেবে কাজ করছে তা শনাক্ত করা।**

---

# 1. Chunking কী?

**Chunking** বা **Shallow Parsing** হলো POS-tagged tokens থেকে meaningful groups বা **phrases** শনাক্ত করার process।

উদাহরণ:

> The smart student writes Python code.

POS:

```text
The         → DT
smart       → JJ
student     → NN
writes      → VBZ
Python      → NNP
code        → NN
```

Chunking করলে:

```text
[The smart student] → Noun Phrase
[writes]            → Verb
[Python code]       → Noun Phrase
```

অর্থাৎ:

```text
Tokens
   ↓
POS Tags
   ↓
Chunking
   ↓
Phrases
```

---

# 2. কেন Chunking দরকার?

শুধু individual word জানলে sentence-এর structure পুরোপুরি বোঝা যায় না।

উদাহরণ:

```text
The
smart
student
writes
Python
code
```

এগুলো আলাদা token।

কিন্তু আমরা বুঝতে চাই:

```text
"The smart student"
```

একটি group।

এবং:

```text
"Python code"
```

আরেকটি group।

তাই:

```text
Word-level
     ↓
Phrase-level
```

analysis দরকার।

---

# 3. Shallow Parsing কেন বলা হয়?

Chunking পুরো sentence-এর গভীর grammatical tree তৈরি করে না।

এটি শুধু গুরুত্বপূর্ণ phrase groups খুঁজে বের করে।

তাই:

```text
Chunking
=
Shallow Parsing
```

অন্যদিকে:

```text
Full Parsing
=
Deep Syntactic Analysis
```

---

# 4. Chunk কী?

একটি **chunk** হলো related tokens-এর একটি group।

উদাহরণ:

```text
The intelligent student
```

এটি একটি **Noun Phrase (NP)**।

```text
in Dhaka
```

এটি একটি **Prepositional Phrase (PP)**।

---

# 5. প্রধান Phrase Types

সবচেয়ে গুরুত্বপূর্ণ:

```text
NP → Noun Phrase
VP → Verb Phrase
PP → Prepositional Phrase
ADJP → Adjective Phrase
ADVP → Adverb Phrase
```

এখন এগুলো দেখি।

---

# 6. Noun Phrase — NP

**Noun Phrase** এমন phrase যার প্রধান element সাধারণত একটি noun বা pronoun।

উদাহরণ:

```text
the student
a smart student
the intelligent computer science student
Python programming
```

Sentence:

> The intelligent student is learning Python.

NP:

```text
[The intelligent student]
[Python]
```

---

# 7. NP Structure

একটি সাধারণ NP:

```text
Determiner + Adjective + Noun
```

উদাহরণ:

```text
the + intelligent + student
```

তাই:

```text
[The intelligent student]
```

একটি NP।

আর:

```text
a + beautiful + city
```

হলো:

```text
[a beautiful city]
```

---

# 8. Noun Phrase আরও Complex হতে পারে

উদাহরণ:

> The highly intelligent computer science student

এখানে পুরো phrase:

```text
[The highly intelligent computer science student]
```

একটি বড় noun phrase।

ভেতরে:

```text
The
 ↓
Determiner

highly
 ↓
Adverb

intelligent
 ↓
Adjective

computer science
 ↓
Noun modifier

student
 ↓
Noun
```

---

# 9. Verb Phrase — VP

Verb এবং তার associated elements মিলে **Verb Phrase** হতে পারে।

উদাহরণ:

```text
is running
has finished
will study
is learning Python
```

Sentence:

> The student is learning Python.

VP:

```text
[is learning Python]
```

---

# 10. Prepositional Phrase — PP

Preposition + তার object মিলে সাধারণত PP তৈরি হয়।

উদাহরণ:

```text
in Dhaka
on the table
with my friend
at the university
from Bangladesh
```

Sentence:

> The student lives in Dhaka.

PP:

```text
[in Dhaka]
```

---

# 11. Adjective Phrase — ADJP

Adjective কেন্দ্রিক phrase।

উদাহরণ:

```text
very smart
extremely intelligent
quite beautiful
```

Sentence:

> He is very intelligent.

ADJP:

```text
[very intelligent]
```

---

# 12. Adverb Phrase — ADVP

Adverb কেন্দ্রিক phrase।

উদাহরণ:

```text
very quickly
extremely carefully
quite slowly
```

Sentence:

> He works very quickly.

ADVP:

```text
[very quickly]
```

---

# 13. একটি Complete Example

Sentence:

> The intelligent student is learning Python in Dhaka.

POS:

```text
The         → DT
intelligent → JJ
student     → NN
is          → VBZ
learning    → VBG
Python      → NNP
in          → IN
Dhaka       → NNP
```

Chunks:

```text
[The intelligent student] → NP

[is learning Python]      → VP

[in Dhaka]                → PP
```

Structure:

```text
Sentence
   │
   ├── NP
   │    └── The intelligent student
   │
   ├── VP
   │    └── is learning Python
   │
   └── PP
        └── in Dhaka
```

---

# 14. Chunking বনাম POS Tagging

এটি খুব গুরুত্বপূর্ণ।

### POS Tagging

প্রতিটি token-এর grammatical category:

```text
The         → DT
intelligent → JJ
student     → NN
```

### Chunking

একাধিক token group করে:

```text
[The intelligent student] → NP
```

অর্থাৎ:

```text
POS
↓
Word-level information

Chunking
↓
Phrase-level information
```

---

# 15. Chunking বনাম NER

এগুলোও আলাদা।

Sentence:

> Steve Jobs founded Apple.

NER:

```text
Steve Jobs → PERSON
Apple      → ORGANIZATION
```

Chunking:

```text
[Steve Jobs] → NP
[Apple]      → NP
```

অর্থাৎ:

```text
Chunking → grammatical phrase
NER      → named entity
```

একই phrase একই সঙ্গে দুটো হতে পারে:

```text
Steve Jobs
↓
NP
+
PERSON
```

---

# 16. Chunking বনাম Lemmatization

Lemmatization:

```text
running → run
children → child
```

Chunking:

```text
[the children]
```

অর্থাৎ:

```text
Lemmatization
→ word normalization

Chunking
→ phrase grouping
```

---

# 17. Chunking কীভাবে কাজ করে?

সাধারণ pipeline:

```text
Raw Text
   ↓
Tokenization
   ↓
POS Tagging
   ↓
Chunking
   ↓
Phrase Groups
```

এখানে POS tagging অত্যন্ত গুরুত্বপূর্ণ।

কারণ chunking rules সাধারণত POS pattern-এর ওপর ভিত্তি করে তৈরি করা যায়।

---

# 18. Rule-Based Chunking

একটি simple rule:

```text
DT + JJ + NN
```

মানে:

```text
Determiner
+
Adjective
+
Noun
```

যেমন:

```text
The smart student
```

POS:

```text
DT JJ NN
```

তাই:

```text
[The smart student]
```

একটি NP।

---

# 19. Python NLTK Chunking

NLTK দিয়ে rule-based chunking করা যায়।

```python
import nltk

sentence = "The smart student writes Python code."

tokens = nltk.word_tokenize(sentence)
tags = nltk.pos_tag(tokens)

print(tags)
```

তারপর grammar:

```python
grammar = r"""
    NP: {<DT>?<JJ>*<NN.*>}
"""
```

এখানে:

```text
DT?  → optional determiner
JJ*  → zero or more adjectives
NN.* → noun-related tags
```

---

# 20. ChunkParser তৈরি করা

```python
import nltk

sentence = "The smart student writes Python code."

tokens = nltk.word_tokenize(sentence)
tags = nltk.pos_tag(tokens)

grammar = r"""
    NP: {<DT>?<JJ>*<NN.*>}
"""

parser = nltk.RegexpParser(grammar)

tree = parser.parse(tags)

print(tree)
```

Conceptually output:

```text
(S
  (NP The/DT smart/JJ student/NN)
  writes/VBZ
  (NP Python/NNP code/NN))
```

---

# 21. Tree Representation

NLTK chunking একটি tree structure তৈরি করতে পারে।

Conceptually:

```text
              S
           /     \
         NP       VP
       / | \     /  \
     The JJ NN  Verb NP
                ...
```

এখানে `S` = Sentence।

---

# 22. Chunk Grammar কী?

Chunk grammar হলো POS pattern-এর rule।

উদাহরণ:

```text
NP: {<DT>?<JJ>*<NN.*>}
```

মানে:

```text
NP
=
optional Determiner
+
zero or more Adjectives
+
Noun
```

---

# 23. আরও একটি Grammar

Noun phrase:

```python
grammar = r"""
    NP: {<DT>?<JJ>*<NN.*>}
"""
```

Prepositional phrase:

```python
grammar = r"""
    PP: {<IN><NP>}
"""
```

এখানে:

```text
IN → Preposition
NP → Noun Phrase
```

তাই:

```text
[in Dhaka]
```

একটি PP হতে পারে।

---

# 24. Multiple Chunk Rules

আমরা একাধিক rule দিতে পারি:

```python
grammar = r"""
    NP: {<DT>?<JJ>*<NN.*>}
    PP: {<IN><NP>}
"""
```

এখন:

```text
The smart student in Dhaka
```

থেকে conceptually:

```text
[The smart student] → NP
[in Dhaka]           → PP
```

---

# 25. Chunking-এর সীমাবদ্ধতা

Rule-based chunking powerful হলেও perfect নয়।

ধরো:

```text
The student who lives in Dhaka is learning Python.
```

এখানে sentence-এর structure complex।

Simple rule:

```text
DT + JJ* + NN
```

সব relationship বুঝতে পারবে না।

এখানে দরকার:

```text
Full Parsing
```

---

# 26. Chunking বনাম Full Parsing

### Chunking

```text
The smart student
```

→ NP

### Full Parsing

এর complete syntactic structure:

```text
                 S
               /   \
             NP     VP
            / \     / \
          Det N    V   NP
```

অর্থাৎ full parsing sentence-এর hierarchical grammatical structure বের করে।

---

# 27. Shallow Parsing কেন Useful?

Chunking:

* Full parsing-এর চেয়ে সহজ
* দ্রুত
* কম computational cost
* useful phrase-level information দেয়
* information extraction-এ useful
* classical NLP pipeline-এ useful

---

# 28. Information Extraction-এ Chunking

ধরো:

> The company developed a new AI model.

Chunks:

```text
[The company] → NP
[a new AI model] → NP
```

এখন system noun phrases extract করতে পারে।

এটি useful হতে পারে:

```text
Entity Extraction
Keyword Extraction
Information Extraction
Question Answering
Search
Document Analysis
```

---

# 29. AI Writing Assistant-এ Chunking

আমাদের project-এর জন্য Chunking useful হতে পারে।

Sentence:

> The intelligent student writes high-quality Python code.

Chunks:

```text
[The intelligent student] → NP
[high-quality Python code] → NP
```

এখন system phrase structure সম্পর্কে ধারণা পেতে পারে।

---

# 30. Rewrite System-এ Phrase Preservation

AI rewriting-এর সময় কিছু phrase preserve করা গুরুত্বপূর্ণ।

উদাহরণ:

```text
high-quality Python code
```

এটি একটি meaningful phrase।

যদি rewrite system word-by-word modification করে, phrase-এর meaning নষ্ট হতে পারে।

তাই:

```text
Sentence
 ↓
Chunking
 ↓
Phrase Detection
 ↓
Rewrite
```

একটি useful strategy হতে পারে।

---

# 31. Chunking + NER

এখন দুটো একসঙ্গে দেখো:

Sentence:

> Elon Musk founded SpaceX in California.

NER:

```text
Elon Musk → PERSON
SpaceX → ORG
California → GPE
```

Chunking:

```text
[Elon Musk] → NP
[SpaceX] → NP
[in California] → PP
```

Combined representation:

```text
[Elon Musk]
    NP + PERSON

[SpaceX]
    NP + ORGANIZATION

[in California]
    PP
    California → GPE
```

এটি অনেক richer representation।

---

# 32. Chunking + POS + NER

আমাদের NLP pipeline এখন:

```text
                 TEXT
                   ↓
              TOKENIZATION
                   ↓
                POS TAG
                   ↓
        ┌──────────┴──────────┐
        ↓                     ↓
     CHUNKING                 NER
        ↓                     ↓
     PHRASES               ENTITIES
        │                     │
        └──────────┬──────────┘
                   ↓
             LEMMATIZATION
                   ↓
            FEATURE EXTRACTION
```

---

# 33. Chunk Tags বনাম POS Tags

একটি token-এর POS tag:

```text
student → NN
```

কিন্তু chunk tag:

```text
student → B-NP / I-NP
```

এখানে:

```text
POS
→ token-এর grammatical category

Chunk
→ token কোন phrase-এর অংশ
```

---

# 34. BIO Chunking

NER-এর মতো chunking-এও BIO format ব্যবহার করা যায়।

Example:

> The smart student

```text
The       → B-NP
smart     → I-NP
student   → I-NP
```

এখানে:

```text
B-NP = NP-এর beginning
I-NP = NP-এর ভিতরে
```

আর phrase-এর বাইরে:

```text
O
```

---

# 35. Example

Sentence:

> The smart student writes Python code.

Chunk BIO:

```text
The       → B-NP
smart     → I-NP
student   → I-NP
writes    → O
Python    → B-NP
code      → I-NP
```

এটি phrase boundary representation।

---

# 36. NER BIO বনাম Chunk BIO

NER:

```text
B-PER
I-PER
O
B-ORG
```

Chunking:

```text
B-NP
I-NP
O
B-NP
```

Difference:

```text
NER → Entity type
Chunk → Phrase type
```

---

# 37. Head Word

Phrase-এর একটি গুরুত্বপূর্ণ concept হলো **head**।

উদাহরণ:

```text
The intelligent student
```

এখানে:

```text
student
```

হলো noun phrase-এর head।

কারণ পুরো phrase-এর মূল noun হলো `student`।

আর:

```text
very quickly
```

এখানে:

```text
quickly
```

adverb phrase-এর head।

---

# 38. Modifier

Phrase-এর অন্য wordগুলো head-কে modify করতে পারে।

```text
The intelligent student
```

এখানে:

```text
student → Head
intelligent → Modifier
The → Determiner
```

আর:

```text
very intelligent student
```

এখানে:

```text
student → Head
intelligent → Modifier
very → Modifier of adjective
```

---

# 39. একটি গুরুত্বপূর্ণ Concept

Sentence:

> The very intelligent student from Dhaka is learning Python.

Potential structure:

```text
[The very intelligent student from Dhaka]
```

NP-এর ভিতরে:

```text
The
very
intelligent
student
from Dhaka
```

আর:

```text
[from Dhaka]
```

একটি PP।

অর্থাৎ phrase-এর ভিতরে আবার phrase থাকতে পারে।

এটিই **nested structure**।

---

# 40. Chunking এবং Nested Phrases

Conceptually:

```text
NP
│
├── Determiner
├── Adjective Phrase
├── Noun
└── PP
      │
      └── NP
```

উদাহরণ:

```text
[The [very intelligent] student [from [Dhaka]]]
```

এটি দেখায় natural language hierarchical।

---

# 41. Chunking-এর Practical Use Cases

### 1. Information Extraction

```text
Noun phrases → important concepts
```

### 2. Search

```text
Phrase-level matching
```

### 3. Question Answering

```text
NP / VP extraction
```

### 4. Text Summarization

Important phrases identify করা।

### 5. Grammar Analysis

Sentence structure বোঝা।

### 6. Writing Analysis

Phrase complexity analysis।

---

# 42. AI Writing Platform-এ Feature Engineering

Chunking থেকে features তৈরি করা যায়:

```text
NP count
VP count
PP count
Average NP length
Average phrase length
Phrase density
```

Example:

```text
NP count = 12
VP count = 8
PP count = 6
Average NP length = 2.7
```

এগুলো text analysis-এর feature হতে পারে।

---

# 43. কিন্তু একটি সতর্কতা

শুধু chunking ব্যবহার করে:

> "এই text AI-generated"

এমন reliable conclusion দেওয়া যাবে না।

Chunking হলো linguistic structure-এর একটি মাত্র feature।

AI text analysis-এর জন্য আরও অনেক signal দরকার হতে পারে।

---

# 44. Chunking বনাম Modern Transformers

Modern Transformer models সাধারণত:

```text
Tokenizer
+
Contextual Embeddings
+
Attention
```

ব্যবহার করে।

তাই traditional rule-based chunking সবসময় model-এর জন্য প্রয়োজন হয় না।

তবুও chunking-এর concept গুরুত্বপূর্ণ কারণ এটি শেখায়:

```text
Word
 ↓
Phrase
 ↓
Sentence Structure
```

অর্থাৎ NLP-এর syntax foundation বোঝা যায়।

---

# 45. Complete NLP Evolution

এখন আমাদের learning progression:

```text
Raw Text
   ↓
Tokenization
   ↓
Stopwords
   ↓
Stemming
   ↓
Lemmatization
   ↓
POS Tagging
   ↓
NER
   ↓
Chunking
   ↓
Parsing
```

এখন আমরা **word-level থেকে phrase-level**-এ চলে এসেছি।

---

# 46. একটি Full Example

Sentence:

> The experienced developer from Bangladesh is building an advanced AI application.

### Tokenization

```text
The
experienced
developer
from
Bangladesh
is
building
an
advanced
AI
application
```

### POS

```text
The          → DT
experienced  → JJ
developer    → NN
from         → IN
Bangladesh   → NNP
is           → VBZ
building     → VBG
an           → DT
advanced     → JJ
AI           → NNP
application  → NN
```

### NER

```text
Bangladesh → GPE
AI → technology-related entity depending on model
```

### Chunking

```text
[The experienced developer] → NP

[from Bangladesh] → PP

[an advanced AI application] → NP
```

এখন আমরা sentence-এর অনেক বেশি structure বুঝতে পারছি।

---

# 47. Python Practice

এই codeটি নিজে run করো:

```python
import nltk

text = "The experienced developer from Bangladesh builds advanced AI applications."

tokens = nltk.word_tokenize(text)
tags = nltk.pos_tag(tokens)

grammar = r"""
    NP: {<DT>?<JJ>*<NN.*>}
    PP: {<IN><NP>}
"""

parser = nltk.RegexpParser(grammar)

tree = parser.parse(tags)

print(tree)
```

Expected concept:

```text
[The experienced developer]
[from Bangladesh]
[advanced AI applications]
```

Exact chunks model-এর POS output অনুযায়ী কিছুটা ভিন্ন হতে পারে।

---

# 48. Practice Task — Beginner

Sentence:

```text
The smart student reads a programming book.
```

Find:

```text
1. POS
2. NP
3. VP
```

সম্ভাব্য:

```text
NP:
The smart student

NP:
a programming book
```

---

# 49. Practice Task — Intermediate

Sentence:

```text
The young developer works at a software company in Dhaka.
```

Identify:

```text
NP
PP
```

সম্ভাব্য:

```text
[The young developer] → NP
[at a software company] → PP
[in Dhaka] → PP
```

---

# 50. Practice Task — Advanced

Sentence:

```text
The experienced Python developer from Bangladesh is building a powerful AI system for a large company.
```

তোমাকে বের করতে হবে:

```text
Tokens
POS
NP
PP
NER
```

Possible entities:

```text
Bangladesh → GPE
```

Possible phrases:

```text
[The experienced Python developer] → NP

[from Bangladesh] → PP

[a powerful AI system] → NP

[for a large company] → PP
```

---

# 51. Theory Questions

নিজেকে জিজ্ঞেস করো:

1. Chunking কী?
2. Shallow Parsing কী?
3. Chunk কেন দরকার?
4. NP কী?
5. VP কী?
6. PP কী?
7. ADJP কী?
8. ADVP কী?
9. Chunking এবং POS Tagging-এর পার্থক্য কী?
10. Chunking এবং NER-এর পার্থক্য কী?
11. Chunking এবং Full Parsing-এর পার্থক্য কী?
12. Chunk Grammar কী?
13. `DT + JJ + NN` কী বোঝায়?
14. BIO chunk tagging কী?
15. B-NP কী?
16. I-NP কী?
17. Head word কী?
18. Modifier কী?
19. Nested phrase কী?
20. Information Extraction-এ chunking কেন useful?
21. AI writing assistant-এ chunking কীভাবে ব্যবহার করা যায়?
22. Transformer যুগে traditional chunking কেন এখনও শেখা গুরুত্বপূর্ণ?

---

# 52. Interview Questions

### Q1. What is chunking?

> Chunking is the process of grouping POS-tagged tokens into meaningful phrases such as noun phrases and prepositional phrases.

### Q2. Chunking vs Parsing?

```text
Chunking → shallow phrase structure
Parsing   → complete syntactic structure
```

### Q3. Chunking vs NER?

```text
Chunking → grammatical phrase
NER      → named entity
```

### Q4. What is an NP?

> A noun phrase is a group of words centered around a noun or pronoun.

Example:

```text
the intelligent student
```

### Q5. Why is POS tagging important for chunking?

> Traditional chunking rules often use POS-tag patterns to identify phrase boundaries.

---

# 53. M02.11 Completion Checklist

* [ ] Chunking বুঝি
* [ ] Shallow Parsing বুঝি
* [ ] NP বুঝি
* [ ] VP বুঝি
* [ ] PP বুঝি
* [ ] ADJP বুঝি
* [ ] ADVP বুঝি
* [ ] POS → Chunking relationship বুঝি
* [ ] Rule-based chunking বুঝি
* [ ] Chunk Grammar বুঝি
* [ ] NLTK RegexpParser বুঝি
* [ ] BIO chunk tagging বুঝি
* [ ] B-NP / I-NP / O বুঝি
* [ ] Head word বুঝি
* [ ] Modifier বুঝি
* [ ] Nested phrase বুঝি
* [ ] Chunking বনাম POS বুঝি
* [ ] Chunking বনাম NER বুঝি
* [ ] Chunking বনাম Parsing বুঝি
* [ ] Information Extraction-এ ব্যবহার বুঝি
* [ ] AI Writing Assistant-এ ব্যবহার বুঝি
* [ ] Chunking থেকে features তৈরি বুঝি

---

# 🔑 আজকের Final Mental Model

```text
                 RAW TEXT
                     ↓
                TOKENIZATION
                     ↓
                 POS TAGGING
                     ↓
        ┌────────────┼────────────┐
        ↓            ↓            ↓
       POS        CHUNKING        NER
        ↓            ↓            ↓
    Word Role      Phrases      Entities
                     ↓
             NP / VP / PP
                     ↓
              Phrase Analysis
                     ↓
               NLP MODEL
```

সবচেয়ে গুরুত্বপূর্ণ:

```text
Tokenization
→ Word/token কী কী?

POS Tagging
→ প্রতিটি token-এর grammatical role কী?

Chunking
→ কোন কোন token একসঙ্গে একটি phrase?

NER
→ কোন word/phrase real-world entity?
```

**M02.11 complete.**


----
# M02.12 — Dependency Parsing Deep Dive

M02.11-এ আমরা **Chunking / Shallow Parsing** পর্যন্ত এসেছি। এখন NLP-এর আরও গুরুত্বপূর্ণ linguistic analysis topic:

> **Dependency Parsing**

এটি AI writing assistant, grammar analysis, sentence understanding, information extraction—সব ক্ষেত্রেই খুব গুরুত্বপূর্ণ।

---

# 1. Dependency Parsing কী?

**Dependency Parsing** হলো একটি sentence-এর প্রতিটি word-এর মধ্যে grammatical dependency/relation বের করা।

সহজভাবে:

> কোন word কোন word-এর উপর নির্ভর করছে এবং তাদের grammatical relationship কী—তা বের করাই Dependency Parsing।

Example:

```text
The smart student writes Python code.
```

এখানে:

```text
student → subject
writes  → main verb
code    → object
Python  → modifier of code
smart   → modifier of student
```

একটি simplified dependency structure:

```text
              writes
             /      \
        student      code
        /    \         |
      The   smart    Python
```

---

# 2. Dependency শব্দটির অর্থ কী?

Dependency = নির্ভরতা।

ধরো:

```text
Rahim reads books.
```

এখানে:

```text
reads
 ├── Rahim
 └── books
```

`Rahim` এবং `books` grammaticalভাবে `reads`-এর সাথে সম্পর্কিত।

তাই:

```text
Rahim → reads
books → reads
```

---

# 3. Dependency Parsing বনাম Chunking

M02.11-এ আমরা শিখেছি:

```text
Chunking
→ কোন কোন word মিলে একটি phrase তৈরি করছে
```

Dependency Parsing:

```text
কোন word কোন word-এর সাথে grammaticalভাবে related
```

Example:

```text
The intelligent student writes Python code.
```

### Chunking

```text
[The intelligent student] → NP
[writes Python code]      → VP
```

### Dependency

```text
student → subject of writes
writes  → root
code    → object of writes
Python  → modifier of code
intelligent → modifier of student
```

অর্থাৎ:

```text
Chunking
   ↓
Phrase structure

Dependency Parsing
   ↓
Word-to-word grammatical relationships
```

---

# 4. Dependency Tree

Dependency parsing সাধারণত একটি **tree** তৈরি করে।

Example:

```text
The student reads a book.
```

Simplified tree:

```text
             reads
            /     \
       student     book
        /           \
       The           a
```

এখানে `reads` হচ্ছে sentence-এর মূল verb।

এটিকে বলা হয়:

**Root**

---

# 5. Root কী?

Dependency tree-এর প্রধান word হলো:

> **Root**

সাধারণত একটি sentence-এর main verb root হয়।

Example:

```text
Rahim plays football.
```

```text
        plays
       /     \
    Rahim   football
```

এখানে:

```text
plays → ROOT
```

---

# 6. Head এবং Dependent

Dependency Parsing-এর সবচেয়ে গুরুত্বপূর্ণ দুইটি concept:

### Head

যে word-এর সাথে অন্য word grammatical relationship তৈরি করছে।

### Dependent

যে wordটি head-এর উপর grammaticalভাবে নির্ভর করছে।

Example:

```text
Rahim plays football.
```

এখানে:

```text
plays → Head
Rahim → Dependent
football → Dependent
```

অর্থাৎ:

```text
          plays
         /     \
     Rahim   football
```

---

# 7. Dependency Relation

প্রতিটি dependency-এর একটি grammatical relation থাকে।

Common relations:

| Relation   | Meaning                  |
| ---------- | ------------------------ |
| `nsubj`    | nominal subject          |
| `obj`      | object                   |
| `iobj`     | indirect object          |
| `det`      | determiner               |
| `amod`     | adjective modifier       |
| `advmod`   | adverb modifier          |
| `prep`     | preposition              |
| `pobj`     | object of preposition    |
| `compound` | compound                 |
| `aux`      | auxiliary                |
| `root`     | root                     |
| `conj`     | conjunction              |
| `cc`       | coordinating conjunction |
| `neg`      | negation                 |
| `punct`    | punctuation              |
| `nmod`     | noun modifier            |
| `obl`      | oblique nominal          |

---

# 8. `nsubj`

`nsubj` = nominal subject.

Example:

```text
Rahim plays football.
```

```text
Rahim → nsubj → plays
```

মানে:

```text
Rahim = subject
plays = main verb
```

---

# 9. `obj`

`obj` সাধারণত direct object বোঝায়।

```text
Rahim plays football.
```

```text
football → obj → plays
```

অর্থাৎ:

```text
Subject → Rahim
Verb    → plays
Object  → football
```

---

# 10. `det`

Determiner-এর dependency relation হলো `det`।

Example:

```text
The student reads a book.
```

```text
The → det → student
a   → det → book
```

Tree:

```text
       reads
      /     \
  student   book
    ↑         ↑
   The        a
```

---

# 11. `amod`

Adjectival modifier:

```text
The smart student reads.
```

এখানে:

```text
smart → amod → student
```

কারণ `smart` শব্দটি `student`-কে modify করছে।

---

# 12. `advmod`

Adverbial modifier:

```text
Rahim runs quickly.
```

```text
quickly → advmod → runs
```

কারণ `quickly` বলে দিচ্ছে কীভাবে `runs` হচ্ছে।

---

# 13. `aux`

Auxiliary verb:

```text
Rahim is reading.
```

এখানে:

```text
is → aux → reading
```

Main verb:

```text
reading
```

Auxiliary:

```text
is
```

---

# 14. `neg`

Negation:

```text
Rahim does not play football.
```

এখানে:

```text
not → neg → play
```

এটি AI writing analysis-এর জন্য খুব গুরুত্বপূর্ণ।

কারণ:

```text
I like this.
```

এবং:

```text
I do not like this.
```

একটি `not` পুরো sentence-এর meaning পরিবর্তন করে।

---

# 15. `conj`

Conjunction দ্বারা connected words:

```text
Rahim and Karim play football.
```

Dependency structure conceptually:

```text
        play
       /    \
    Rahim   Karim
             ↑
           conj
```

এবং:

```text
and → cc
```

---

# 16. Dependency বনাম POS

আমরা M02.09-এ POS Tagging শিখেছি।

POS বলে:

> একটি word কী ধরনের grammatical category?

Example:

```text
Rahim plays football.
```

```text
Rahim     → PROPN
plays     → VERB
football  → NOUN
```

Dependency বলে:

```text
Rahim     → subject
plays     → root
football  → object
```

অর্থাৎ:

```text
POS
↓
What type of word?

Dependency
↓
What grammatical relationship?
```

---

# 17. Dependency বনাম NER

NER:

```text
Rahim visited Dhaka.
```

বলবে:

```text
Rahim → PERSON
Dhaka → LOCATION
```

Dependency:

```text
Rahim → nsubj → visited
Dhaka → obj/obl-type relation depending on structure
```

তাই:

```text
NER
→ Who/where/what entity?

Dependency
→ What grammatical relationship?
```

---

# 18. Dependency বনাম Chunking

একটি sentence:

```text
The smart student writes Python code.
```

Chunking:

```text
[The smart student] → NP
[writes Python code] → VP
```

Dependency:

```text
student → nsubj → writes
smart → amod → student
The → det → student
code → obj → writes
Python → compound → code
```

তাই Dependency Parsing অনেক বেশি detailed grammatical information দেয়।

---

# 19. Dependency Parsing Pipeline

আমাদের NLP pipeline এখন আরও পরিষ্কার হচ্ছে:

```text
Raw Text
   ↓
Sentence Segmentation
   ↓
Tokenization
   ↓
POS Tagging
   ↓
Dependency Parsing
   ↓
Syntactic Relations
   ↓
Semantic Analysis
```

---

# 20. Dependency Parsing-এর দুই ধরনের Approach

Historically দুটি গুরুত্বপূর্ণ approach:

### 1. Transition-based Parsing

Parser step-by-step transition করে tree তৈরি করে।

Concept:

```text
SHIFT
REDUCE
LEFT-ARC
RIGHT-ARC
```

এটি দ্রুত parsing-এর জন্য জনপ্রিয় ছিল।

---

### 2. Graph-based Parsing

সম্ভাব্য dependency structure-এর মধ্যে সবচেয়ে ভালো tree নির্বাচন করে।

Concept:

```text
Words
 ↓
Possible Relations
 ↓
Scoring
 ↓
Best Dependency Tree
```

---

# 21. Modern Dependency Parsing

বর্তমানে neural network এবং Transformer-based methods ব্যাপকভাবে ব্যবহৃত হয়।

Concept:

```text
Text
 ↓
Tokenizer
 ↓
Embeddings
 ↓
Neural / Transformer Model
 ↓
Dependency Relations
 ↓
Dependency Tree
```

---

# 22. spaCy দিয়ে Dependency Parsing

প্রথমে:

```bash
pip install spacy
```

তারপর English model:

```bash
python -m spacy download en_core_web_sm
```

Python:

```python
import spacy

nlp = spacy.load("en_core_web_sm")

text = "The smart student writes Python code."

doc = nlp(text)

for token in doc:
    print(
        token.text,
        token.pos_,
        token.dep_,
        token.head.text
    )
```

Output conceptually এমন হতে পারে:

```text
The         DET     det       student
smart       ADJ     amod      student
student     NOUN    nsubj     writes
writes      VERB    ROOT      writes
Python      PROPN   compound  code
code        NOUN    obj       writes
.           PUNCT   punct     writes
```

---

# 23. এখানে কী হচ্ছে?

এই line:

```python
token.text
```

word দেয়।

```python
token.pos_
```

POS দেয়।

```python
token.dep_
```

dependency relation দেয়।

```python
token.head.text
```

তার head word দেয়।

অর্থাৎ:

```text
Token
 ↓
POS
 ↓
Dependency
 ↓
Head
```

---

# 24. Dependency Tree Visualize করা

spaCy-তে:

```python
from spacy import displacy

displacy.render(
    doc,
    style="dep",
    jupyter=True
)
```

এতে sentence-এর dependency tree visual form-এ দেখা যাবে।

---

# 25. একটি গুরুত্বপূর্ণ Example

Sentence:

```text
The beautiful girl quickly reads a book.
```

আমরা linguistic analysis করলে:

```text
The       → determiner
beautiful → adjective
girl      → subject
quickly   → adverb
reads     → root/main verb
a         → determiner
book      → object
```

Dependency concept:

```text
                    reads
                 /         \
              girl         book
             /    \          ↑
           The  beautiful    a
                    \
                  quickly
```

বাস্তব parser-এর exact tree relation sentence/model অনুযায়ী দেখা উচিত; উপরেরটি concept বোঝানোর simplified structure।

---

# 26. Dependency Parsing কেন গুরুত্বপূর্ণ?

AI writing system-এ এটি অনেক কাজে লাগে।

### Grammar Analysis

```text
Subject → Verb → Object
```

বুঝতে সাহায্য করে।

### Sentence Structure

```text
Who did what?
```

বোঝার foundation তৈরি করে।

### Information Extraction

Example:

```text
Google acquired YouTube.
```

Dependency structure থেকে:

```text
Subject → Google
Action  → acquired
Object  → YouTube
```

তাহলে structured information:

```json
{
    "subject": "Google",
    "action": "acquired",
    "object": "YouTube"
}
```

---

# 27. AI Writing Assistant-এ ব্যবহার

তোমার future AI writing platform-এ Dependency Parsing ব্যবহার করা যেতে পারে:

```text
User Text
    ↓
Tokenization
    ↓
POS
    ↓
NER
    ↓
Dependency Parsing
    ↓
Sentence Structure Analysis
    ↓
Writing Suggestions
```

উদাহরণ:

```text
"The students was studying."
```

Dependency/POS analysis-এর মাধ্যমে subject এবং verb relationship পাওয়া যায়।

তারপর grammar system বলতে পারে:

```text
students → plural
was → singular auxiliary
```

সম্ভাব্য correction:

```text
The students were studying.
```

---

# 28. Subject-Verb Relationship

Dependency parsing grammar system-এর foundation হতে পারে।

Example:

```text
The boy plays football.
```

```text
boy → nsubj → plays
```

এখানে:

```text
boy = singular
plays = singular verb
```

কিন্তু:

```text
The boys plays football.
```

এখানে:

```text
boys = plural
plays = singular
```

তাই grammar checker dependency + morphology + POS information ব্যবহার করতে পারে।

---

# 29. Long Sentence Analysis

একটি complex sentence:

```text
The student who lives in Dhaka studies computer science because he wants to become a software engineer.
```

এখানে অনেক relationship:

```text
student
   ↓
lives
   ↓
Dhaka

student
   ↓
studies
   ↓
science

wants
   ↓
become
   ↓
engineer
```

Dependency parsing sentence-এর grammatical structure বুঝতে সাহায্য করে।

---

# 30. Dependency Parsing এবং Coreference

এখানে একটি interesting problem:

```text
Rahim went to Dhaka because he got a job.
```

এখানে:

```text
he → Rahim
```

এটি **Coreference Resolution**।

Dependency Parsing এবং Coreference Resolution একই জিনিস নয়।

```text
Dependency
→ grammatical relationship

Coreference
→ কোন expression একই entity-কে refer করছে
```

এগুলো পরে একসাথে ব্যবহার করা যায়।

---

# 31. Dependency Parsing এবং Semantic Understanding

শুধু words জানলেই sentence-এর meaning সম্পূর্ণ বোঝা যায় না।

Example:

```text
Dog bites man.
```

এবং:

```text
Man bites dog.
```

একই words, কিন্তু dependency relationship আলাদা।

### Sentence 1

```text
Dog → subject
bites → root
man → object
```

### Sentence 2

```text
Man → subject
bites → root
dog → object
```

এটাই syntactic structure-এর গুরুত্ব।

---

# 32. Dependency Parsing-এর Limitations

Dependency parsing খুব powerful হলেও perfect নয়।

Problems:

### Ambiguity

একটি sentence-এর multiple interpretations থাকতে পারে।

### Long-distance dependency

```text
The book that I bought yesterday was expensive.
```

`book` এবং `was`-এর relationship সরাসরি পাশাপাশি নয়।

### Coordination

```text
Rahim and Karim went to school.
```

এ ধরনের structure complex হতে পারে।

### Domain-specific language

Medical, legal, scientific বা informal text-এ parser performance পরিবর্তিত হতে পারে।

### Model errors

Parser সবসময় 100% correct হবে না।

---

# 33. Dependency Parsing + Transformer

Modern AI architecture:

```text
Text
 ↓
Subword Tokenization
 ↓
Transformer
 ↓
Contextual Representation
 ↓
Dependency Prediction
 ↓
Dependency Tree
```

Transformer নিজে traditional dependency tree ব্যবহার করতেই হবে এমন নয়।

কিন্তু Transformer-based models dependency information **learn** করতে পারে এবং dependency parsing-এর জন্য fine-tuned model তৈরি করা যায়।

---

# 34. Classical NLP বনাম Modern NLP

### Classical

```text
Text
 ↓
Tokenization
 ↓
POS
 ↓
Dependency Parser
 ↓
Features
 ↓
ML Model
```

### Modern

```text
Text
 ↓
Subword Tokenization
 ↓
Transformer
 ↓
Contextual Representation
 ↓
Task-specific Head
 ↓
Dependency Relations
```

---

# 35. M02-এর Concepts এখন কোথায় দাঁড়িয়েছে?

আমাদের NLP linguistic pipeline:

```text
                    TEXT
                     ↓
               TOKENIZATION
                     ↓
                 STOPWORDS
                     ↓
                 STEMMING
                     ↓
              LEMMATIZATION
                     ↓
                 POS TAGGING
                     ↓
                    NER
                     ↓
                  CHUNKING
                     ↓
             DEPENDENCY PARSING
                     ↓
             SYNTACTIC ANALYSIS
```

তবে **সবগুলো sequentially mandatory নয়**।

বাস্তব NLP system-এ task অনুযায়ী pipeline পরিবর্তিত হয়।

---

# 36. খুব গুরুত্বপূর্ণ: সব preprocessing একসাথে করা যাবে না

ধরো modern AI writing assistant:

```text
Text
 ↓
Aggressive Stopword Removal ❌
 ↓
Aggressive Stemming ❌
 ↓
Transformer
```

এটি ভালো design নাও হতে পারে।

Modern writing analysis-এর ক্ষেত্রে সাধারণত:

```text
Original Text
 ↓
Appropriate Tokenization
 ↓
Linguistic Analysis
 ↓
Transformer / NLP Model
```

এবং original context preserve করা গুরুত্বপূর্ণ।

---

# 37. Practical Python Exercise

এই sentence ব্যবহার করো:

```python
text = """
The intelligent student carefully writes Python code
because he wants to become a software engineer.
"""
```

Task:

### Task 1

প্রতিটি token print করো।

### Task 2

প্রতিটি token-এর:

```text
text
POS
dependency
head
```

print করো।

### Task 3

শুধু:

```text
ROOT
nsubj
obj
amod
advmod
```

relations বের করো।

### Task 4

প্রতিটি dependency relation-এর count বের করো।

Expected concept:

```text
{
    "nsubj": ...,
    "obj": ...,
    "amod": ...,
    "advmod": ...
}
```

---

# 38. Mini Project

একটি simple **Sentence Structure Analyzer** বানাও।

Input:

```text
The smart student writes Python code.
```

Output:

```text
Sentence: The smart student writes Python code.

Root: writes

Subject: student

Object: code

Adjective modifiers:
smart → student

Determiners:
The → student

Compound:
Python → code
```

এটি তোমার future AI writing platform-এর একটি ছোট component হতে পারে।

---

# 39. Interview Questions

### Beginner

**Q1. What is Dependency Parsing?**

একটি sentence-এর words-এর grammatical dependency relationship বের করার process।

**Q2. What is a dependency tree?**

Words এবং তাদের grammatical relationships-এর tree structure।

**Q3. What is root?**

Dependency tree-এর প্রধান/root word।

**Q4. What is head?**

যে word-এর সাথে dependent word grammatical relationship তৈরি করে।

**Q5. What is dependent?**

যে word একটি head-এর উপর syntactically dependent।

---

### Intermediate

**Q6. Dependency Parsing vs Chunking?**

```text
Chunking
→ phrase-level structure

Dependency Parsing
→ word-to-word grammatical relationships
```

**Q7. What is `nsubj`?**

Nominal subject।

**Q8. What is `obj`?**

Direct object relation।

**Q9. What is `amod`?**

Adjectival modifier।

**Q10. Why is dependency parsing useful for grammar checking?**

কারণ subject, verb, object এবং modifier-এর grammatical relationships পাওয়া যায়।

---

### Advanced

**Q11. Transition-based vs graph-based parsing?**

```text
Transition-based
→ sequential actions দিয়ে tree তৈরি

Graph-based
→ possible dependency graph থেকে best tree নির্বাচন
```

**Q12. Can Transformers perform dependency parsing?**

হ্যাঁ। Transformer-based models dependency parsing task-এর জন্য fine-tune করা যায়।

**Q13. Is dependency parsing the same as semantic parsing?**

না।

```text
Dependency Parsing
→ syntactic relationships

Semantic Parsing
→ meaning/structured semantic representation
```

---

# 40. M02.12 Completion Checklist

নিজেকে পরীক্ষা করো:

* [ ] Dependency Parsing কী জানি
* [ ] Dependency Tree বুঝি
* [ ] Root বুঝি
* [ ] Head বুঝি
* [ ] Dependent বুঝি
* [ ] Dependency Relation বুঝি
* [ ] `nsubj` বুঝি
* [ ] `obj` বুঝি
* [ ] `det` বুঝি
* [ ] `amod` বুঝি
* [ ] `advmod` বুঝি
* [ ] `aux` বুঝি
* [ ] `neg` বুঝি
* [ ] `conj` বুঝি
* [ ] POS বনাম Dependency বুঝি
* [ ] NER বনাম Dependency বুঝি
* [ ] Chunking বনাম Dependency বুঝি
* [ ] Dependency Tree বুঝি
* [ ] spaCy Dependency Parsing করতে পারি
* [ ] `token.dep_` বুঝি
* [ ] `token.head` বুঝি
* [ ] Grammar analysis-এর connection বুঝি
* [ ] Information extraction-এর connection বুঝি
* [ ] AI writing assistant-এর connection বুঝি
* [ ] Classical বনাম modern parsing বুঝি

## Final Mental Model

```text
                    SENTENCE
                       │
                 TOKENIZATION
                       │
                    TOKENS
                       │
                   POS TAG
                       │
              ┌────────┴────────┐
              │                 │
           CHUNKING             NER
              │                 │
          PHRASES            ENTITIES
              │
              ▼
       DEPENDENCY PARSING
              │
              ▼
        DEPENDENCY TREE
              │
       ┌──────┼──────┐
       ▼      ▼      ▼
    SUBJECT  VERB  OBJECT
       │      │      │
       └──────┼──────┘
              ▼
       SENTENCE STRUCTURE
              │
              ▼
       NLP / AI ANALYSIS
```

**M02.12-এর মূল কথা:**

> **Chunking বলে “কোন কোন word মিলে phrase”, আর Dependency Parsing বলে “কোন word কোন word-এর সাথে কী grammatical relationship-এ আছে।”**

পরবর্তী lesson হবে **M02.13**, এবং আমরা NLP Foundation-এর sequence অনুযায়ী পরের topic-এ যাব—কোনো topic skip না করে।


---

# M02.13 — Constituency Parsing / Phrase Structure Parsing

M02.11-এ আমরা **Chunking**, আর M02.12-এ **Dependency Parsing** শিখেছি। এখন আমরা আরও গভীরভাবে sentence-এর **phrase structure** বুঝব।

> **Constituency Parsing** একটি sentence-কে বিভিন্ন nested phrase/constituent-এ ভাগ করে তার hierarchical structure তৈরি করে।

---

## 1. Constituency Parsing কী?

একটি sentence-এর কোন কোন word একসাথে একটি meaningful grammatical unit বা **constituent** তৈরি করছে—তা বের করাই Constituency Parsing।

Example:

```text
The smart student reads a book.
```

এটাকে আমরা এভাবে ভাগ করতে পারি:

```text
Sentence
├── Noun Phrase (NP)
│   ├── The
│   ├── smart
│   └── student
│
└── Verb Phrase (VP)
    ├── reads
    └── Noun Phrase (NP)
        ├── a
        └── book
```

অর্থাৎ:

```text
S
├── NP
│   ├── DT The
│   ├── JJ smart
│   └── NN student
│
└── VP
    ├── VB reads
    └── NP
        ├── DT a
        └── NN book
```

এটাই একটি **constituency tree**।

---

# 2. Constituent কী?

**Constituent** হলো sentence-এর এমন একটি group of words, যেটি sentence-এর একটি grammatical unit হিসেবে কাজ করে।

Example:

```text
The smart student
```

এটি একটি:

```text
NP = Noun Phrase
```

আর:

```text
reads a book
```

এটি:

```text
VP = Verb Phrase
```

---

# 3. Common Constituents

সবচেয়ে গুরুত্বপূর্ণ:

| Label | Full Form            | Example           |
| ----- | -------------------- | ----------------- |
| S     | Sentence             | পুরো sentence     |
| NP    | Noun Phrase          | the smart student |
| VP    | Verb Phrase          | reads a book      |
| PP    | Prepositional Phrase | in Dhaka          |
| ADJP  | Adjective Phrase     | very intelligent  |
| ADVP  | Adverb Phrase        | very quickly      |

---

# 4. NP — Noun Phrase

Noun Phrase-এর কেন্দ্র সাধারণত একটি noun।

Example:

```text
the smart student
```

Structure:

```text
NP
├── DT → the
├── JJ → smart
└── NN → student
```

আরও examples:

```text
a book
the beautiful girl
my new computer
a very intelligent student
```

---

# 5. VP — Verb Phrase

Verb Phrase-এর প্রধান অংশ verb।

Example:

```text
reads a book
```

```text
VP
├── VB → reads
└── NP
    ├── DT → a
    └── NN → book
```

আরেকটি:

```text
is learning Python
```

Conceptually:

```text
VP
├── AUX → is
├── VERB → learning
└── NP → Python
```

---

# 6. PP — Prepositional Phrase

Preposition + noun phrase মিলে PP তৈরি করতে পারে।

Example:

```text
in Dhaka
```

```text
PP
├── IN → in
└── NP
    └── PROPN → Dhaka
```

আর:

```text
on the table
```

```text
PP
├── on
└── NP
    ├── the
    └── table
```

---

# 7. Nested Constituents

Constituency Parsing-এর সবচেয়ে গুরুত্বপূর্ণ বিষয় হলো **nesting**।

Example:

```text
The intelligent student from Dhaka reads a Python book.
```

Structure:

```text
S
├── NP
│   ├── The
│   ├── intelligent
│   ├── student
│   └── PP
│       ├── from
│       └── NP
│           └── Dhaka
│
└── VP
    ├── reads
    └── NP
        ├── a
        ├── Python
        └── book
```

খেয়াল করো:

```text
NP
└── PP
    └── NP
```

অর্থাৎ একটি phrase-এর ভিতরে আরেকটি phrase থাকতে পারে।

---

# 8. Constituency Tree

একই sentence:

```text
The smart student reads a book.
```

Tree:

```text
                    S
                  /   \
                NP     VP
              / | \    / \
            DT JJ NN  V  NP
            |  |  |   |  / \
           The smart student reads DT NN
                              |  |
                              a book
```

এটি sentence-এর **hierarchical structure** দেখায়।

---

# 9. Constituency বনাম Dependency

এটি খুব গুরুত্বপূর্ণ।

### Constituency Parsing

Focus:

```text
Phrase structure
```

### Dependency Parsing

Focus:

```text
Word-to-word relationship
```

Example:

```text
The smart student reads a book.
```

### Constituency

```text
S
├── NP
│   └── The smart student
│
└── VP
    ├── reads
    └── NP
        └── a book
```

### Dependency

```text
             reads
            /     \
       student     book
       /    \       |
     The   smart    a
```

---

# 10. Chunking বনাম Constituency Parsing

এগুলোও এক নয়।

### Chunking

```text
The smart student
```

কে NP হিসেবে identify করতে পারে।

কিন্তু detailed nested structure সাধারণত দেয় না।

### Constituency Parsing

```text
S
├── NP
│   ├── DT
│   ├── JJ
│   └── NN
└── VP
    ├── V
    └── NP
```

অর্থাৎ:

```text
Chunking
→ shallow phrase detection

Constituency Parsing
→ complete hierarchical phrase structure
```

---

# 11. Grammar Rules

Constituency parsing grammar rules ব্যবহার করতে পারে।

উদাহরণ:

```text
S → NP VP
```

অর্থাৎ:

```text
Sentence = Noun Phrase + Verb Phrase
```

আর:

```text
NP → DT JJ NN
```

মানে:

```text
Noun Phrase = Determiner + Adjective + Noun
```

আর:

```text
VP → V NP
```

মানে:

```text
Verb Phrase = Verb + Noun Phrase
```

---

# 12. একটি সম্পূর্ণ Grammar

ধরো:

```text
S  → NP VP
NP → DT JJ NN
NP → DT NN
VP → V NP
```

Sentence:

```text
The smart student reads a book.
```

Parsing:

```text
S
├── NP
│   ├── DT The
│   ├── JJ smart
│   └── NN student
│
└── VP
    ├── V reads
    └── NP
        ├── DT a
        └── NN book
```

---

# 13. Context-Free Grammar — CFG

Constituency parsing-এর foundation-এর একটি গুরুত্বপূর্ণ concept হলো:

**Context-Free Grammar (CFG)**

CFG-এর rule:

```text
A → B C
```

এখানে `A` একটি constituent তৈরি করছে `B` এবং `C` থেকে।

Example:

```text
S → NP VP
```

---

# 14. CFG Components

একটি CFG সাধারণত চারটি component দিয়ে প্রকাশ করা হয়:

```text
G = (N, Σ, P, S)
```

যেখানে:

```text
N = Non-terminals
Σ = Terminals
P = Production Rules
S = Start Symbol
```

Example:

```text
N = {S, NP, VP}
```

```text
Σ = {The, student, reads, book}
```

Rules:

```text
S → NP VP
NP → DT NN
VP → V NP
```

Start symbol:

```text
S
```

---

# 15. Terminal বনাম Non-terminal

### Terminal

Actual words/tokens:

```text
The
student
reads
book
```

### Non-terminal

Grammar categories:

```text
S
NP
VP
PP
```

---

# 16. Parse Tree

Grammar rules ব্যবহার করে যে tree তৈরি হয় সেটাই **Parse Tree**।

Example:

```text
S
├── NP
│   ├── DT
│   │   └── The
│   └── NN
│       └── student
│
└── VP
    ├── V
    │   └── reads
    │
    └── NP
        ├── DT
        │   └── a
        └── NN
            └── book
```

---

# 17. Ambiguity

Natural language-এ একটি sentence-এর একাধিক possible parse থাকতে পারে।

Example:

```text
I saw the man with a telescope.
```

এখানে দুটি interpretation হতে পারে।

### Interpretation 1

আমি telescope ব্যবহার করে মানুষটিকে দেখেছি।

```text
I saw [the man] [with a telescope]
```

### Interpretation 2

আমি এমন মানুষটিকে দেখেছি যার কাছে telescope ছিল।

```text
I saw [the man [with a telescope]]
```

দুটি structure:

```text
Different Parse Trees
        ↓
Different Interpretations
```

এটাকে **syntactic ambiguity** বলা হয়।

---

# 18. Why Ambiguity Matters?

AI system-এর জন্য এটি খুব গুরুত্বপূর্ণ।

Example:

```text
I saw the man with a telescope.
```

System যদি ভুল attachment করে:

```text
with a telescope → man
```

তাহলে meaning একরকম হবে।

আর:

```text
with a telescope → saw
```

হলে অন্য interpretation হবে।

তাই sentence structure বোঝা language understanding-এর জন্য গুরুত্বপূর্ণ।

---

# 19. Constituency Parsing Algorithms

Classical parsing-এ বিভিন্ন algorithm ব্যবহৃত হয়েছে।

Important:

### CYK Algorithm

**Cocke–Younger–Kasami algorithm**

এটি CFG parsing-এর জন্য একটি classic dynamic programming algorithm।

---

### Earley Parser

General CFG parsing-এর জন্য ব্যবহৃত হয়।

---

### Chart Parsing

Already computed parsing results store করে efficiency বাড়ায়।

---

# 20. CYK Algorithm — Basic Idea

ধরো:

```text
The smart student
```

Parser ছোট অংশ থেকে শুরু করে বড় constituent তৈরি করে:

```text
Words
 ↓
Small constituents
 ↓
Larger constituents
 ↓
NP
 ↓
Sentence structure
```

Concept:

```text
Token
 ↓
2-word spans
 ↓
3-word spans
 ↓
larger spans
```

এটি Dynamic Programming ব্যবহার করে।

---

# 21. Modern Constituency Parsing

Modern NLP-তে neural network এবং Transformer-based models ব্যবহার করা হয়।

Concept:

```text
Text
 ↓
Tokenizer
 ↓
Transformer
 ↓
Contextual Representation
 ↓
Span Prediction
 ↓
Constituency Tree
```

এখানে model sentence-এর বিভিন্ন **span** analyse করতে পারে।

---

# 22. Span কী?

Sentence:

```text
The smart student reads Python.
```

এখানে:

```text
The smart student
```

একটি span।

Index concept:

```text
The        0
smart      1
student    2
reads      3
Python     4
```

তাহলে:

```text
[0:3]
```

conceptually:

```text
The smart student
```

এ ধরনের span analysis modern parsing-এ গুরুত্বপূর্ণ।

---

# 23. Python-এ Constituency Parsing

NLTK-তে আমরা CFG ব্যবহার করতে পারি।

```python
import nltk

grammar = nltk.CFG.fromstring("""
S -> NP VP
NP -> DT JJ NN
NP -> DT NN
VP -> V NP
DT -> "The" | "a"
JJ -> "smart"
NN -> "student" | "book"
V -> "reads"
""")

parser = nltk.ChartParser(grammar)

sentence = "The smart student reads a book".split()

for tree in parser.parse(sentence):
    print(tree)
```

এটি grammar অনুযায়ী possible parse tree তৈরি করবে।

---

# 24. Tree Pretty Print

```python
for tree in parser.parse(sentence):
    tree.pretty_print()
```

তাহলে tree-like output দেখতে পারবে।

---

# 25. `Tree` Structure

NLTK tree object:

```python
tree.label()
```

Root label পাওয়া যায়।

Example:

```python
print(tree.label())
```

Output:

```text
S
```

Children:

```python
print(tree[0])
```

এটি প্রথম constituent:

```text
NP
```

---

# 26. AI Writing Assistant-এ ব্যবহার

তোমার future AI writing platform-এ Constituency Parsing ব্যবহার করা যেতে পারে:

```text
User Text
    ↓
Sentence Segmentation
    ↓
Tokenization
    ↓
POS
    ↓
Constituency Parsing
    ↓
Phrase Structure
    ↓
Writing Analysis
```

---

# 27. Grammar Structure Analysis

Example:

```text
The students are learning Python.
```

System বুঝতে পারে:

```text
NP
└── The students

VP
├── are learning
└── Python
```

এতে sentence structure সম্পর্কে feature তৈরি করা যায়।

---

# 28. Sentence Complexity

Constituency tree ব্যবহার করে sentence complexity-এর কিছু measurable feature বের করা যায়।

যেমন:

```text
Tree depth
Number of constituents
Number of subordinate structures
Number of noun phrases
Number of verb phrases
```

উদাহরণ:

```text
Simple sentence
→ shallow tree

Complex sentence
→ deeper tree
```

এগুলো readability/style analysis-এ ব্যবহার করা যেতে পারে।

---

# 29. Writing Style Analysis

ধরো:

```text
The intelligent student who lives in Dhaka carefully writes Python code.
```

Tree structure থেকে system দেখতে পারে:

```text
NP
├── adjective
├── noun
└── relative clause

VP
├── adverb
├── verb
└── object
```

এর মাধ্যমে writing-style features তৈরি করা যায়।

---

# 30. Dependency + Constituency একসাথে

এখন দুটি parsing approach একসাথে দেখো।

```text
                Sentence
                   │
          ┌────────┴────────┐
          ↓                 ↓
    Constituency        Dependency
       Parsing             Parsing
          │                 │
          ↓                 ↓
   Phrase Structure    Word Relations
          │                 │
          ↓                 ↓
     NP / VP / PP       subject/object
```

একটি AI language system-এ দুটো information complementary হতে পারে।

---

# 31. M02-এর Linguistic Analysis এখন

এখন পর্যন্ত:

```text
Raw Text
   ↓
Tokenization
   ↓
Stopwords
   ↓
Stemming
   ↓
Lemmatization
   ↓
POS Tagging
   ↓
NER
   ↓
Chunking
   ↓
Dependency Parsing
   ↓
Constituency Parsing
```

এখানে আবার মনে রাখবে:

> এগুলো সবসময় এই exact order-এ বাস্তব project-এ চালাতে হবে না।

Task অনুযায়ী pipeline design হবে।

---

# 32. চারটি Concept একসাথে

এই চারটি খুব ভালোভাবে আলাদা করতে হবে:

```text
POS Tagging
→ Word-এর grammatical category

NER
→ Named entity

Chunking
→ Phrase group

Parsing
→ Full grammatical structure
```

আর Parsing দুইভাবে খুব গুরুত্বপূর্ণ:

```text
Constituency
→ Phrase-to-phrase hierarchy

Dependency
→ Word-to-word relationships
```

---

# 33. একটি Full Example

Sentence:

```text
The intelligent student from Dhaka writes Python code.
```

### Tokenization

```text
The
intelligent
student
from
Dhaka
writes
Python
code
```

### POS

```text
The          DET
intelligent  ADJ
student      NOUN
from         ADP
Dhaka        PROPN
writes       VERB
Python       PROPN
code         NOUN
```

### NER

```text
Dhaka → GPE/LOCATION
Python → depending on model/context, possibly PRODUCT/ORG/etc.; not necessarily an entity
```

### Chunking

```text
[The intelligent student] → NP
[from Dhaka]             → PP
[Python code]             → NP
```

### Dependency

```text
student → subject → writes
code → object → writes
intelligent → modifier → student
Dhaka → related to from/student structure
```

### Constituency

```text
S
├── NP
│   ├── The
│   ├── intelligent
│   ├── student
│   └── PP
│       ├── from
│       └── NP
│           └── Dhaka
│
└── VP
    ├── writes
    └── NP
        ├── Python
        └── code
```

এখন দেখতেই পাচ্ছো NLP-এর প্রতিটি layer কীভাবে আলাদা information দেয়।

---

# 34. Practice — Beginner

Sentence:

```text
The young boy plays football.
```

নিজে বের করো:

1. NP
2. VP
3. Determiner
4. Adjective
5. Noun
6. Verb
7. Object

Expected:

```text
NP → The young boy
VP → plays football
```

---

# 35. Practice — Intermediate

Sentence:

```text
The smart student reads a book in the library.
```

Find:

```text
NP
VP
PP
Nested NP
```

Expected concept:

```text
NP → The smart student

VP → reads a book in the library

NP → a book

PP → in the library

NP → the library
```

---

# 36. Practice — Advanced

Sentence:

```text
The intelligent student who lives in Dhaka carefully writes Python code because he wants to become a software engineer.
```

Find:

* Main NP
* Main VP
* Relative clause
* PP
* Object NP
* Subordinate clause
* Nested constituents
* Tree depth

এটি M02.13-এর জন্য খুব ভালো exercise।

---

# 37. Theory Questions

1. What is Constituency Parsing?
2. What is a constituent?
3. What is a parse tree?
4. What is a phrase structure?
5. What is NP?
6. What is VP?
7. What is PP?
8. What is CFG?
9. What are terminal and non-terminal symbols?
10. What is syntactic ambiguity?
11. What is a span?
12. What is CYK?
13. What is Chart Parsing?
14. Constituency Parsing vs Dependency Parsing?
15. Chunking vs Constituency Parsing?

---

# 38. Interview Questions

### Q1. What is Constituency Parsing?

Sentence-কে hierarchical grammatical constituents/phrases-এ ভাগ করে parse tree তৈরি করার process।

### Q2. What is NP?

Noun Phrase।

### Q3. What is VP?

Verb Phrase।

### Q4. Constituency vs Dependency?

```text
Constituency
→ phrase hierarchy

Dependency
→ word-to-word relationships
```

### Q5. What is syntactic ambiguity?

যখন একটি sentence-এর একাধিক valid syntactic structure বা interpretation থাকতে পারে।

### Q6. What is CFG?

Context-Free Grammar, যা production rules ব্যবহার করে language-এর syntactic structure define করে।

### Q7. Why is constituency parsing useful?

Sentence structure, phrase hierarchy, grammar analysis এবং linguistic feature extraction-এর জন্য।

---

# 39. M02.13 Completion Checklist

* [ ] Constituency Parsing বুঝি
* [ ] Constituent বুঝি
* [ ] Parse Tree বুঝি
* [ ] Phrase Structure বুঝি
* [ ] NP বুঝি
* [ ] VP বুঝি
* [ ] PP বুঝি
* [ ] ADJP বুঝি
* [ ] ADVP বুঝি
* [ ] Nested Constituents বুঝি
* [ ] Grammar Rules বুঝি
* [ ] CFG বুঝি
* [ ] Terminal বুঝি
* [ ] Non-terminal বুঝি
* [ ] Start Symbol বুঝি
* [ ] Syntactic Ambiguity বুঝি
* [ ] Span বুঝি
* [ ] CYK-এর basic idea বুঝি
* [ ] Chart Parsing-এর ধারণা বুঝি
* [ ] NLTK CFG ব্যবহার করতে পারি
* [ ] Parse Tree তৈরি করতে পারি
* [ ] Chunking vs Constituency বুঝি
* [ ] Dependency vs Constituency বুঝি
* [ ] AI writing analysis-এর connection বুঝি

---

## Final Mental Model

```text
                         SENTENCE
                            │
                            ▼
                  CONSTITUENCY PARSING
                            │
                            ▼
                      PARSE TREE
                            │
              ┌─────────────┴─────────────┐
              ▼                           ▼
             NP                           VP
       Noun Phrase                  Verb Phrase
              │                           │
       ┌──────┴──────┐              ┌─────┴─────┐
       ▼             ▼              ▼           ▼
   Determiner      Noun           Verb          NP
       │             │              │            │
      The         student         reads        a book
```

### সবচেয়ে গুরুত্বপূর্ণ পার্থক্য

```text
POS
 ↓
Word-এর grammatical category

Chunking
 ↓
Phrase-এর basic group

Dependency Parsing
 ↓
Word-to-word relationship

Constituency Parsing
 ↓
Complete phrase hierarchy
```

**M02.13-এর মূল লক্ষ্য:** তুমি যেন একটি sentence দেখে শুধু শব্দগুলোর POS না বলে, বরং **কোন words মিলে কোন phrase এবং সেই phrase-এর ভিতরে কী nested structure আছে—তা বুঝতে পারো।**

---
# M02.14 — Semantic Analysis & Word Meaning

M02.13-এ আমরা **Constituency Parsing** শিখেছি। এখন আমরা syntax থেকে এক ধাপ সামনে যাব:

> **Sentence-এর structure না শুধু, sentence-এর actual meaning কী—তা বোঝার foundation হলো Semantic Analysis।**

এটি তোমার future **AI Writing Assistant / Text Analyzer** project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 1. Semantics কী?

**Semantics** হলো language-এর **meaning** নিয়ে study।

Example:

```text
Rahim eats rice.
```

Syntax আমাদের বলতে পারে:

```text
Rahim → subject
eats  → verb
rice  → object
```

কিন্তু semantics জানতে চায়:

```text
কে কাজটি করছে?
কী কাজ করছে?
কী জিনিসের উপর কাজটি হচ্ছে?
Sentence-এর অর্থ কী?
```

অর্থাৎ:

```text
Syntax
→ Structure

Semantics
→ Meaning
```

---

# 2. Syntax বনাম Semantics

এটি খুব ভালোভাবে বুঝতে হবে।

### Syntax

```text
The boy eats rice.
```

Structure:

```text
NP + VP
```

### Semantics

```text
boy = entity
eats = action
rice = thing being consumed
```

তাই:

```text
Syntax
↓
How is the sentence structured?

Semantics
↓
What does the sentence mean?
```

---

# 3. Lexical Semantics

**Lexical Semantics** হলো individual word-এর meaning নিয়ে study।

Example:

```text
car
```

এর semantic concept:

```text
vehicle
transport
wheels
engine
```

আর:

```text
run
```

এর meaning context অনুযায়ী পরিবর্তিত হতে পারে।

```text
I run every morning.
```

→ physical activity

```text
The machine runs well.
```

→ operates

তাই শুধু dictionary meaning যথেষ্ট নয়।

---

# 4. Word Meaning Context-এর উপর নির্ভর করে

Example:

```text
I went to the bank.
```

`bank` হতে পারে:

```text
financial institution
```

আবার:

```text
I sat on the river bank.
```

এখানে:

```text
bank = riverside
```

একই word:

```text
bank
```

কিন্তু context অনুযায়ী meaning আলাদা।

এটিকে বলা যায় **context-dependent meaning**।

---

# 5. Polysemy

একটি word-এর related multiple meanings থাকলে তাকে **Polysemy** বলা হয়।

Example:

```text
head
```

```text
head of a person
head of a department
head of a company
```

Meaningগুলো related।

---

# 6. Homonymy

দুটি একই form-এর word-এর completely different meanings থাকতে পারে।

Example:

```text
bat
```

একটি:

```text
bat → animal
```

অন্যটি:

```text
bat → sports equipment
```

এখানে meanings unrelated।

---

# 7. Synonym

**Synonym** = কাছাকাছি অর্থের word।

Example:

```text
big
large
huge
```

অথবা:

```text
happy
joyful
cheerful
```

কিন্তু গুরুত্বপূর্ণ:

> Synonym সবসময় 100% interchangeable নয়।

Example:

```text
big mistake
```

স্বাভাবিক।

কিন্তু:

```text
large mistake
```

grammatically সম্ভব হলেও naturalness আলাদা হতে পারে।

এটি AI writing system-এর জন্য গুরুত্বপূর্ণ।

---

# 8. Antonym

Opposite meaning:

```text
hot ↔ cold
big ↔ small
fast ↔ slow
happy ↔ sad
```

Types:

### Gradable

```text
hot ↔ cold
```

মাঝখানে:

```text
warm
cool
```

থাকতে পারে।

### Complementary

```text
alive ↔ dead
```

### Relational

```text
buy ↔ sell
teacher ↔ student
```

---

# 9. Hypernym

একটি general category word।

Example:

```text
animal
```

এর নিচে:

```text
dog
cat
horse
```

তাহলে:

```text
animal = hypernym
```

---

# 10. Hyponym

Specific member/category:

```text
dog
```

হলো:

```text
animal-এর hyponym
```

Structure:

```text
animal
 ├── dog
 ├── cat
 └── horse
```

---

# 11. Meronymy

**Part-whole relationship**।

Example:

```text
car
 ├── wheel
 ├── engine
 ├── door
 └── window
```

এখানে:

```text
wheel → part of car
engine → part of car
```

এটি semantic relationship।

---

# 12. Holonym

যে whole-এর অংশ কোনো object:

```text
car
```

হলো:

```text
wheel-এর holonym
```

সহজভাবে:

```text
Meronym
→ part

Holonym
→ whole
```

---

# 13. Semantic Similarity

দুটি word বা sentence কতটা semantically similar তা measure করা।

Example:

```text
car
automobile
```

high similarity।

কিন্তু:

```text
car
banana
```

low similarity।

---

# 14. Word Embeddings

Modern NLP-তে word meaning represent করার জন্য **embeddings** অত্যন্ত গুরুত্বপূর্ণ।

ধরো:

```text
king
queen
man
woman
```

প্রতিটি word একটি vector হিসেবে represent হতে পারে:

```text
king  → [0.21, -0.45, 0.78, ...]
queen → [0.19, -0.41, 0.81, ...]
```

এই vector-এর মাধ্যমে semantic relationship capture করা যায়।

---

# 15. Traditional Representation

পুরনো NLP-তে:

```text
Word
 ↓
One-hot vector
```

Example vocabulary:

```text
["cat", "dog", "car"]
```

তাহলে:

```text
cat → [1, 0, 0]
dog → [0, 1, 0]
car → [0, 0, 1]
```

Problem:

```text
cat
dog
car
```

সব word equally unrelated হিসেবে দেখা যায়।

---

# 16. Dense Embeddings

Embedding:

```text
cat → [0.2, 0.8, 0.1, ...]
dog → [0.3, 0.7, 0.2, ...]
car → [0.9, 0.1, 0.8, ...]
```

এখানে:

```text
cat ↔ dog
```

semantic space-এ কাছাকাছি হতে পারে।

---

# 17. Word2Vec

একটি classic word embedding technique:

**Word2Vec**

এর দুটি popular approach:

```text
CBOW
Skip-gram
```

### CBOW

Context দেখে target word predict করে।

```text
The cat ___ on the mat.
```

Context:

```text
The cat ... on the mat
```

→ target:

```text
sits
```

---

# 18. Skip-gram

Target word থেকে context predict করার চেষ্টা করে।

```text
cat
 ↓
nearby words
```

Conceptually:

```text
Input → cat
Output → nearby context words
```

---

# 19. Contextual Embeddings

Word2Vec-এর limitation:

একটি word-এর সাধারণত একটি fixed vector থাকে।

কিন্তু:

```text
bank
```

এর meaning context অনুযায়ী পরিবর্তিত হয়।

Modern models:

```text
bank + financial context
```

এবং:

```text
bank + river context
```

ভিন্ন contextual representation তৈরি করতে পারে।

এটাই **contextual embeddings**।

---

# 20. Transformer-এর Connection

Modern NLP:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embeddings
 ↓
Transformer
 ↓
Contextual Representation
 ↓
Meaning / Task Output
```

Transformer প্রতিটি token-এর representation-কে surrounding context-এর সাথে সম্পর্কিত করে।

---

# 21. Sentence Semantics

শুধু individual word-এর meaning যথেষ্ট নয়।

Example:

```text
The dog chased the cat.
```

Semantic interpretation:

```text
Agent → dog
Action → chase
Target → cat
```

এখানে sentence-level meaning তৈরি হচ্ছে।

---

# 22. Semantic Roles

একটি action-এর সাথে বিভিন্ন participant থাকে।

Example:

```text
Rahim bought a laptop from Karim.
```

Semantic roles:

```text
Rahim  → Buyer
laptop → Thing bought
Karim  → Seller
```

আরেকটি:

```text
Rahim ate rice.
```

```text
Rahim → Agent
ate   → Action
rice  → Patient/Theme
```

---

# 23. Semantic Role Labeling — SRL

**Semantic Role Labeling (SRL)** হলো sentence-এর predicate/action-এর সাথে কোন entity কী role পালন করছে তা identify করা।

Example:

```text
Rahim bought a laptop from Karim.
```

Possible representation:

```text
Predicate = bought

ARG0 = Rahim
ARG1 = a laptop
ARG2 = Karim
```

Conceptually:

```text
Rahim
  ↓
Buyer

bought
  ↓
Action

laptop
  ↓
Thing bought

Karim
  ↓
Seller
```

---

# 24. Why SRL Important?

Information extraction-এর জন্য অত্যন্ত useful।

Sentence:

```text
Google acquired YouTube in 2006.
```

System বের করতে পারে:

```text
Acquirer → Google
Action   → acquired
Target   → YouTube
Time     → 2006
```

এভাবে unstructured text থেকে structured data তৈরি করা যায়।

---

# 25. Semantic Parsing

Semantic Parsing হলো natural language-কে একটি structured semantic representation-এ convert করা।

Example:

```text
Show me hotels in Dhaka.
```

Structured form:

```json
{
    "intent": "search_hotel",
    "location": "Dhaka"
}
```

এটি conversational AI এবং information retrieval-এ গুরুত্বপূর্ণ।

---

# 26. Intent

User কী করতে চায়—তা হলো **intent**।

Example:

```text
"Show me cheap hotels in Dhaka."
```

Intent:

```text
hotel_search
```

আর:

```text
"Book a hotel in Dhaka."
```

Intent:

```text
hotel_booking
```

Words কাছাকাছি হলেও intent আলাদা।

---

# 27. Entity বনাম Intent

Conversational NLP-তে:

```text
"Book a hotel in Dhaka tomorrow."
```

Entity:

```text
Dhaka → location
tomorrow → date
hotel → object/category
```

Intent:

```text
booking
```

অর্থাৎ:

```text
Intent
→ User কী করতে চায়?

Entity
→ কোন object/person/place নিয়ে কাজ?
```

---

# 28. Word Sense Disambiguation

একটি word-এর কোন meaning এখানে ব্যবহৃত হয়েছে তা determine করা।

Example:

```text
I deposited money in the bank.
```

এখানে:

```text
bank → financial institution
```

আর:

```text
The fisherman sat on the bank.
```

এখানে:

```text
bank → riverside
```

এটাই **Word Sense Disambiguation (WSD)**।

---

# 29. Semantic Similarity বনাম Semantic Relatedness

দুটো এক নয়।

### Similarity

দুটি object একই ধরনের।

```text
car ↔ automobile
```

### Relatedness

দুটি concept related কিন্তু same type নাও হতে পারে।

```text
doctor ↔ hospital
```

তারা related, কিন্তু synonym নয়।

---

# 30. Sentence Similarity

AI writing assistant-এ এটি খুব গুরুত্বপূর্ণ।

Example:

```text
Sentence A:
The student completed the assignment.

Sentence B:
The learner finished the task.
```

Words আলাদা হলেও meaning কাছাকাছি।

Traditional word matching:

```text
Low overlap
```

Semantic model:

```text
High semantic similarity
```

---

# 31. Paraphrase Detection

দুটি sentence-এর meaning একই বা প্রায় একই কিনা।

Example:

```text
A:
The company increased its revenue.

B:
The company's revenue grew.
```

Semantic similarity:

```text
High
```

এটি AI writing assistant-এ useful হতে পারে।

---

# 32. Contradiction Detection

Example:

```text
A:
The meeting is scheduled for Monday.

B:
The meeting is scheduled for Tuesday.
```

এগুলো semantically contradictory হতে পারে।

Modern NLP systems:

```text
Entailment
Contradiction
Neutral
```

এই ধরনের relationship classify করতে পারে।

---

# 33. Natural Language Inference — NLI

NLI:

> একটি sentence অন্য sentence-এর meaning support করে, contradict করে, নাকি neither—তা determine করা।

Example:

Premise:

```text
A man is running.
```

Hypothesis:

```text
A person is moving.
```

→ **Entailment**

---

Premise:

```text
A man is running.
```

Hypothesis:

```text
The man is sleeping.
```

→ **Contradiction**

---

Premise:

```text
A man is running.
```

Hypothesis:

```text
The man is wearing a blue shirt.
```

→ **Neutral**

---

# 34. AI Writing Assistant-এ Semantic Analysis

তোমার project-এ:

```text
User Text
    ↓
Tokenization
    ↓
POS
    ↓
NER
    ↓
Dependency
    ↓
Semantic Analysis
    ↓
Meaning Representation
    ↓
Writing Improvement
```

এটি ব্যবহার করে:

* sentence similarity
* paraphrase analysis
* semantic consistency
* contradiction detection
* meaning preservation
* information extraction
* contextual rewriting

করতে পারো।

---

# 35. Meaning Preservation — খুব গুরুত্বপূর্ণ

ধরো original:

```text
The company launched a new product.
```

Rewrite:

```text
The company introduced a new product.
```

Meaning প্রায় একই।

কিন্তু:

```text
The company canceled a new product.
```

Meaning completely পরিবর্তিত।

তাই AI rewriting system-এ শুধু grammar ঠিক করলেই হবে না।

```text
Grammar
+
Meaning
+
Context
+
Intent
```

preserve করতে হবে।

---

# 36. AI Humanization/Writing System-এর জন্য

একটি safe writing improvement system:

```text
Original Text
      ↓
Grammar Analysis
      ↓
Syntax Analysis
      ↓
Semantic Analysis
      ↓
Meaning Representation
      ↓
Rewrite / Improve
      ↓
Semantic Similarity Check
      ↓
Meaning Preservation
      ↓
Final Text
```

এখানে লক্ষ্য হওয়া উচিত **clarity, naturalness, readability এবং meaning preservation**—কোনো detector বা review system bypass করা নয়।

---

# 37. একটি Practical Semantic Analyzer

ধরো:

```text
text = "Rahim bought a laptop from Karim."
```

আমরা চাই:

```json
{
    "action": "buy",
    "buyer": "Rahim",
    "item": "laptop",
    "seller": "Karim"
}
```

এটাই raw text থেকে structured semantic information extraction-এর basic idea।

---

# 38. Python — Semantic Similarity Concept

Modern NLP libraries/models ব্যবহার করে sentence embeddings বের করা যায়।

Concept:

```python
sentence1 = "The student completed the task."
sentence2 = "The learner finished the assignment."
```

তারপর:

```text
Embedding(sentence1)
Embedding(sentence2)
        ↓
Similarity Score
```

উচ্চ score হলে sentences semanticভাবে কাছাকাছি হতে পারে।

---

# 39. Cosine Similarity

Embedding vector-এর similarity measure করার জন্য commonly ব্যবহৃত:

**Cosine Similarity**

Formula:

```text id="v6n2k8"
cos(θ) = (A · B) / (||A|| ||B||)
```

Conceptually:

```text
1
↑
Highly similar

0
↑
Unrelated

-1
↑
Opposite direction
```

বাস্তবে text embedding-এর interpretation model অনুযায়ী করতে হবে; শুধু score দেখে meaning সম্পর্কে অতিরিক্ত দাবি করা ঠিক নয়।

---

# 40. Semantic Analysis-এর Important Concepts

আজকের lesson থেকে:

```text
Semantics
Lexical Semantics
Polysemy
Homonymy
Synonym
Antonym
Hypernym
Hyponym
Meronym
Holonym
Semantic Similarity
Semantic Relatedness
Word Embedding
Contextual Embedding
Semantic Role
SRL
Semantic Parsing
Intent
Entity
WSD
Paraphrase
Contradiction
NLI
```

এগুলো M02-এর foundation-এর খুব গুরুত্বপূর্ণ অংশ।

---

# 41. পুরো NLP Analysis এখন

আমাদের progression:

```text
TEXT
 ↓
TOKENIZATION
 ↓
STOPWORDS
 ↓
STEMMING
 ↓
LEMMATIZATION
 ↓
POS TAGGING
 ↓
NER
 ↓
CHUNKING
 ↓
DEPENDENCY PARSING
 ↓
CONSTITUENCY PARSING
 ↓
SEMANTIC ANALYSIS
```

এখন আমরা:

```text
Syntax
```

থেকে:

```text
Semantics
```

এ চলে এসেছি।

---

# 42. Syntax → Semantics

একটি simple mental model:

```text
                  TEXT
                   │
                   ▼
              TOKENIZATION
                   │
                   ▼
              POS TAGGING
                   │
                   ▼
              SYNTACTIC
               ANALYSIS
                   │
          ┌────────┴────────┐
          ▼                 ▼
     Dependency       Constituency
          │                 │
          └────────┬────────┘
                   ▼
              SEMANTICS
                   │
          ┌────────┼─────────┐
          ▼        ▼         ▼
       Meaning    Roles    Similarity
          │        │         │
          └────────┼─────────┘
                   ▼
             NLP UNDERSTANDING
```

---

# 43. Practice — Beginner

নিচের sentence-এর semantic roles বের করো:

```text
Rahim opened the door.
```

Find:

```text
Agent
Action
Object/Patient
```

Expected:

```text
Agent → Rahim
Action → opened
Object → the door
```

---

# 44. Practice — Intermediate

```text
Karim bought a new computer from a local shop.
```

Find:

* Buyer
* Action
* Item
* Seller/source
* Adjective
* Main object

---

# 45. Practice — Advanced

দুটি sentence:

```text
A: The company released a new smartphone.
B: The company launched a new mobile phone.
```

তোমার কাজ:

1. Semantic similarity explain করো।
2. কোন words synonyms/near-synonyms?
3. Subject কী?
4. Action কী?
5. Object কী?
6. Meaning কি preserved?
7. Paraphrase হিসেবে consider করা যায় কি?

---

# 46. Theory Questions

1. What is Semantics?
2. What is Lexical Semantics?
3. What is Polysemy?
4. What is Homonymy?
5. What is Synonym?
6. What is Antonym?
7. What is Hypernym?
8. What is Hyponym?
9. What is Meronym?
10. What is Holonym?
11. What is Semantic Similarity?
12. What is Semantic Relatedness?
13. What is Word Embedding?
14. What is Contextual Embedding?
15. What is Semantic Role Labeling?
16. What is Semantic Parsing?
17. What is Word Sense Disambiguation?
18. What is Intent?
19. What is Paraphrase Detection?
20. What is Natural Language Inference?

---

# 47. Interview Questions

### Q1. Syntax এবং Semantics-এর difference কী?

```text
Syntax
→ sentence structure

Semantics
→ sentence meaning
```

### Q2. Polysemy কী?

একটি word-এর related multiple meanings থাকা।

### Q3. Word2Vec কী?

Word-এর distributed vector representation শেখানোর একটি classic neural embedding technique।

### Q4. Contextual embedding কী?

যে representation word-এর surrounding context অনুযায়ী পরিবর্তিত হয়।

### Q5. Semantic Role Labeling কী?

Predicate/action-এর সাথে sentence-এর বিভিন্ন entity কী semantic role পালন করছে তা identify করা।

### Q6. Semantic similarity কী?

দুটি text/concept-এর meaning কতটা কাছাকাছি তা measure করা।

### Q7. WSD কী?

Context ব্যবহার করে ambiguous word-এর সঠিক sense নির্বাচন করা।

### Q8. NLI কী?

একটি statement অন্য statement-কে entail, contradict বা neither করে কিনা determine করা।

---

# 48. M02.14 Completion Checklist

* [ ] Semantics বুঝি
* [ ] Lexical Semantics বুঝি
* [ ] Context-dependent meaning বুঝি
* [ ] Polysemy বুঝি
* [ ] Homonymy বুঝি
* [ ] Synonym বুঝি
* [ ] Antonym বুঝি
* [ ] Hypernym বুঝি
* [ ] Hyponym বুঝি
* [ ] Meronym বুঝি
* [ ] Holonym বুঝি
* [ ] Semantic Similarity বুঝি
* [ ] Semantic Relatedness বুঝি
* [ ] Word Embedding বুঝি
* [ ] Word2Vec বুঝি
* [ ] CBOW বুঝি
* [ ] Skip-gram বুঝি
* [ ] Contextual Embedding বুঝি
* [ ] Semantic Role বুঝি
* [ ] SRL বুঝি
* [ ] Semantic Parsing বুঝি
* [ ] Intent বুঝি
* [ ] Entity বনাম Intent বুঝি
* [ ] Word Sense Disambiguation বুঝি
* [ ] Paraphrase Detection বুঝি
* [ ] Contradiction বুঝি
* [ ] NLI বুঝি
* [ ] AI Writing Assistant-এর সাথে connection বুঝি
* [ ] Meaning Preservation বুঝি

---

## Final Mental Model

```text
                    NATURAL LANGUAGE
                           │
                           ▼
                      WORD MEANING
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
         Synonym        Polysemy      Context
             │             │             │
             └─────────────┼─────────────┘
                           ▼
                    WORD EMBEDDINGS
                           │
                           ▼
                CONTEXTUAL EMBEDDINGS
                           │
                           ▼
                   SENTENCE MEANING
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
             SRL         Intent      Similarity
              │            │            │
              └────────────┼────────────┘
                           ▼
                    SEMANTIC ANALYSIS
                           │
                           ▼
                  LANGUAGE UNDERSTANDING
```

### সবচেয়ে গুরুত্বপূর্ণ ৫টি distinction

```text
POS
→ Word-এর grammatical category

Dependency
→ Word-to-word grammatical relation

Constituency
→ Phrase hierarchy

Syntax
→ Sentence structure

Semantics
→ Sentence meaning
```

**M02.14 complete হলে তোমার NLP Foundation-এর linguistic understanding layer আরও শক্ত হলো।** পরের lesson **M02.15**-এ আমরা semantic analysis-এর পরের গুরুত্বপূর্ণ topic-এ যাব, এবং আগের মতোই কোনো topic skip করব না।


---
# M02.15 — Word Embeddings & Vector Semantics

M02.14-এ আমরা **Semantic Analysis & Word Meaning** শিখেছি। সেখানে আমরা Word Meaning, Semantic Similarity, Word2Vec, Contextual Embeddings ইত্যাদির introduction পেয়েছি।

এখন M02.15-এ এগুলোকে **deep level-এ** শিখব।

> **Word Embedding হলো word-এর meaning/semantic information-কে numerical vector হিসেবে represent করার পদ্ধতি।**

এটি NLP-এর সবচেয়ে গুরুত্বপূর্ণ foundation-এর একটি, কারণ modern NLP/LLM system-এর ভিতরে text ultimately numerical representation-এ যায়।

---

# 1. কেন Word-কে Vector বানাতে হবে?

Computer সরাসরি:

```text
cat
dog
car
beautiful
running
```

এর semantic meaning বুঝতে পারে না।

Machine Learning model numerical data নিয়ে কাজ করে।

তাই:

```text
Text
 ↓
Numerical Representation
 ↓
Machine Learning / Neural Network
```

প্রয়োজন।

---

# 2. One-Hot Encoding দিয়ে শুরু করি

ধরো vocabulary:

```text
["cat", "dog", "car", "apple"]
```

One-hot:

```text
cat    → [1, 0, 0, 0]
dog    → [0, 1, 0, 0]
car    → [0, 0, 1, 0]
apple  → [0, 0, 0, 1]
```

এখানে প্রতিটি word-এর জন্য আলাদা position।

---

# 3. One-Hot-এর সমস্যা

দেখো:

```text
cat → [1,0,0,0]
dog → [0,1,0,0]
car → [0,0,1,0]
```

Computer-এর কাছে:

```text
cat ↔ dog
```

এবং:

```text
cat ↔ car
```

এর distance একই হতে পারে।

কিন্তু human হিসেবে আমরা জানি:

```text
cat ≈ dog
```

কিন্তু:

```text
cat ≠ car
```

One-hot representation semantic relationship ভালোভাবে capture করে না।

---

# 4. Dense Vector

Word embedding এই সমস্যার সমাধান করার চেষ্টা করে।

ধরো:

```text
cat → [0.21, 0.78, 0.12, 0.44]
dog → [0.24, 0.75, 0.15, 0.42]
car → [0.81, 0.10, 0.65, 0.20]
```

এখানে:

```text
cat ↔ dog
```

এর vector কাছাকাছি হতে পারে।

---

# 5. Embedding Space

ধরো 2D space:

```text
        ↑
        │       cat
        │     dog
        │
        │
        │
        │                    car
        └────────────────────────→
```

Semanticভাবে কাছাকাছি words embedding space-এ কাছাকাছি অবস্থান করতে পারে।

বাস্তবে embedding সাধারণত:

```text
100+
300+
768+
1024+
1536+
```

বা আরও বেশি dimensions হতে পারে।

তখন visualize করা কঠিন।

---

# 6. Distributed Representation

Word embedding-এর একটি গুরুত্বপূর্ণ ধারণা:

> একটি word-এর meaning একটি মাত্র dimension-এ থাকে না; অনেক dimensions-এর combination-এ distributed থাকে।

Example:

```text
dog
↓
[0.12, 0.82, -0.31, 0.44, ...]
```

প্রতিটি dimension সরাসরি:

```text
"animal"
"pet"
"size"
```

এর মতো human-readable label নাও হতে পারে।

---

# 7. Distributional Hypothesis

Word embeddings-এর foundation-এর একটি গুরুত্বপূর্ণ idea:

> **Words that occur in similar contexts tend to have similar meanings.**

সহজভাবে:

```text
You shall know a word by the company it keeps.
```

Example:

```text
The cat drinks milk.
The dog drinks milk.
```

`cat` এবং `dog` একই ধরনের context-এ এসেছে।

তাই model শিখতে পারে:

```text
cat ≈ dog
```

---

# 8. Context কেন গুরুত্বপূর্ণ?

দেখো:

```text
The cat eats fish.
```

এবং:

```text
The dog eats fish.
```

দুই sentence-এর context similar।

আবার:

```text
The car needs fuel.
```

এখানে `car`-এর context আলাদা।

তাই model word-এর surrounding context থেকে semantic representation শেখে।

---

# 9. Static Word Embedding

Classic embedding models-এ একটি word-এর একটি fixed vector থাকে।

Example:

```text
bank
↓
[0.31, 0.62, -0.14, ...]
```

কিন্তু সমস্যা:

```text
I deposited money in the bank.
```

এবং:

```text
I sat beside the river bank.
```

এখানে `bank`-এর meaning আলাদা।

Static embedding দুটির জন্য একই বা প্রায় একই word representation ব্যবহার করতে পারে।

---

# 10. Contextual Embedding

Modern NLP এই সমস্যার সমাধান করেছে।

একটি word-এর representation তার context অনুযায়ী পরিবর্তিত হতে পারে।

```text
I deposited money in the bank.
                         ↓
                  financial context
```

অন্যদিকে:

```text
I sat beside the river bank.
                         ↓
                   river context
```

তাই:

```text
bank₁ ≠ bank₂
```

context অনুযায়ী representation আলাদা হতে পারে।

---

# 11. Word2Vec

Classic এবং অত্যন্ত গুরুত্বপূর্ণ embedding algorithm:

> **Word2Vec**

Word2Vec দুইটি প্রধান architecture ব্যবহার করে:

```text
CBOW
Skip-gram
```

---

# 12. CBOW

CBOW:

> **Continuous Bag of Words**

এটি surrounding context দেখে target word predict করতে শেখে।

Example:

```text
The cat drinks milk.
```

ধরো:

```text
The cat ___ milk.
```

Model predict করবে:

```text
drinks
```

Concept:

```text
Context Words
      ↓
   Neural Network
      ↓
 Target Word
```

---

# 13. CBOW Example

Sentence:

```text
The quick brown fox jumps.
```

Context:

```text
The
brown
fox
```

Target:

```text
quick
```

Conceptually:

```text
The
brown
fox
 ↓
CBOW
 ↓
quick
```

Training-এর মাধ্যমে model word relationships শিখতে থাকে।

---

# 14. Skip-gram

Skip-gram CBOW-এর বিপরীত direction-এর মতো।

এখানে:

```text
Target Word
     ↓
Context Words
```

Example:

```text
Input:
fox
```

Possible context:

```text
quick
brown
jumps
```

Concept:

```text
fox
 ↓
Neural Network
 ↓
quick
brown
jumps
```

---

# 15. CBOW vs Skip-gram

| Feature    | CBOW                | Skip-gram      |
| ---------- | ------------------- | -------------- |
| Input      | Context             | Target         |
| Output     | Target              | Context        |
| Training   | তুলনামূলক দ্রুত     | তুলনামূলক ধীর  |
| Rare words | তুলনামূলক কম সুবিধা | সাধারণত ভালো   |
| Main idea  | Context → Word      | Word → Context |

Mental model:

```text
CBOW:

context → WORD
```

```text
Skip-gram:

WORD → context
```

---

# 16. Word2Vec কী শেখে?

ধরো training corpus:

```text
king queen man woman
```

অনেক context দেখে model semantic এবং syntactic relationships capture করতে পারে।

Classic Word2Vec-এর famous ধরনের analogy:

```text
king - man + woman ≈ queen
```

এটি embedding space-এর relational structure বোঝানোর একটি classic illustration।

তবে সব model/domain-এ এই arithmetic perfectly কাজ করবে—এমন নয়।

---

# 17. Embedding Matrix

Neural network-এর ভিতরে embeddings সাধারণত একটি matrix হিসেবে থাকে।

ধরো:

```text
Vocabulary = 10,000 words
Embedding dimension = 300
```

তাহলে embedding matrix:

```text
10000 × 300
```

অর্থাৎ:

```text
10,000 words
     ×
300 numerical dimensions
```

---

# 18. Word ID

Model সাধারণত সরাসরি word string নেয় না।

প্রথমে:

```text
"cat"
```

কে একটি ID দেওয়া হয়:

```text
cat → 25
```

তারপর:

```text
25
 ↓
Embedding Layer
 ↓
[0.21, 0.78, 0.12, ...]
```

Pipeline:

```text
Word
 ↓
Token ID
 ↓
Embedding Lookup
 ↓
Vector
```

---

# 19. Embedding Layer

Neural network-এ:

```text
Embedding(vocab_size, embedding_dim)
```

ধরো:

```python id="4z8n7m"
from tensorflow.keras.layers import Embedding

embedding = Embedding(
    input_dim=10000,
    output_dim=300
)
```

এখানে:

```text
input_dim = vocabulary size
output_dim = vector dimension
```

---

# 20. Embedding Layer কী করে?

ধরো:

```text
cat → ID 25
```

Embedding matrix থেকে:

```text
row 25
```

নিয়ে:

```text
[0.21, 0.78, 0.12, ...]
```

return করে।

Concept:

```text
Token ID
   ↓
Embedding Matrix
   ↓
Vector
```

---

# 21. Embedding Initialization

Training-এর শুরুতে embeddings সাধারণত meaningful হয় না।

Conceptually:

```text
Before training:

cat → random vector
dog → random vector
car → random vector
```

Training-এর সাথে সাথে model weights update করে:

```text
After training:

cat → meaningful representation
dog → meaningful representation
car → meaningful representation
```

---

# 22. Training কীভাবে Embedding শেখায়?

ধরো:

```text
The cat drinks milk.
```

Model repeatedly context prediction করতে থাকে।

Prediction error হয়:

```text
Predicted ≠ Actual
```

তারপর:

```text
Loss
 ↓
Backpropagation
 ↓
Gradient
 ↓
Weight Update
 ↓
Embedding Update
```

বারবার training-এর মাধ্যমে useful representations তৈরি হয়।

---

# 23. Cosine Similarity

দুটি embedding কতটা similar তা measure করার জন্য খুব popular:

**Cosine Similarity**

Formula:

```text
cos(θ) = (A · B) / (||A|| ||B||)
```

যদি vectors-এর direction কাছাকাছি হয়:

```text
similarity → high
```

---

# 24. Example

ধরো:

```text
A = [1, 0]
B = [0.9, 0.1]
```

তারা কাছাকাছি direction-এ।

তাই:

```text
cosine similarity ≈ high
```

অন্যদিকে:

```text
A = [1, 0]
C = [-1, 0]
```

তারা opposite direction-এ।

তাই cosine similarity:

```text
≈ -1
```

---

# 25. Euclidean Distance

আরেকটি similarity/distance measure:

```text
distance(A, B)
```

Formula:

```text
√((a₁-b₁)² + (a₂-b₂)² + ...)
```

Embedding space-এ distance ব্যবহার করেও কাছাকাছি vectors খোঁজা যায়।

---

# 26. Cosine vs Euclidean

|                       | Cosine              | Euclidean       |
| --------------------- | ------------------- | --------------- |
| Focus                 | Direction           | Distance        |
| Common in embeddings  | খুব common          | common          |
| Magnitude sensitivity | কম                  | বেশি            |
| Typical use           | Semantic similarity | Vector distance |

---

# 27. Sentence Embedding

Word embedding:

```text
cat → vector
```

কিন্তু আমাদের দরকার পুরো sentence-এর representation:

```text
"The student is learning Python."
```

→ একটি vector।

এটাকে বলা হয়:

> **Sentence Embedding**

এটি sentence similarity, retrieval, clustering, semantic search ইত্যাদিতে ব্যবহার করা যায়।

---

# 28. Sentence Similarity

ধরো:

```text
A = "The student completed the assignment."

B = "The learner finished the task."
```

Words আলাদা হলেও semantic meaning কাছাকাছি।

Sentence embeddings:

```text
A → Vector A
B → Vector B
```

তারপর:

```text
Cosine Similarity(A, B)
```

ব্যবহার করে semantic similarity estimate করা যায়।

---

# 29. Document Embedding

একই ধারণা পুরো document-এর জন্য:

```text
Document
 ↓
Embedding
 ↓
Vector
```

তারপর:

```text
Document A
     ↕
Similarity
     ↕
Document B
```

এটি semantic search এবং document clustering-এ useful।

---

# 30. Word Embedding বনাম Sentence Embedding

```text
Word Embedding
→ একটি word-এর representation
```

```text
Sentence Embedding
→ পুরো sentence-এর representation
```

```text
Document Embedding
→ পুরো document-এর representation
```

---

# 31. Static বনাম Contextual Embedding

### Static

```text
Word
 ↓
One fixed vector
```

Examples:

```text
Word2Vec
GloVe
FastText
```

### Contextual

```text
Word + Context
 ↓
Context-dependent vector
```

Examples:

```text
ELMo
BERT-family models
Transformer-based encoders
```

---

# 32. GloVe

আরেকটি classic embedding method:

> **GloVe = Global Vectors for Word Representation**

এটি corpus-এর global word co-occurrence statistics ব্যবহার করে word vectors শেখে।

Concept:

```text
Corpus
 ↓
Word Co-occurrence Statistics
 ↓
GloVe Training
 ↓
Word Vectors
```

---

# 33. Word2Vec vs GloVe

|             | Word2Vec      | GloVe                     |
| ----------- | ------------- | ------------------------- |
| Main idea   | Predictive    | Count/co-occurrence based |
| Context     | Local context | Global co-occurrence      |
| Output      | Word vectors  | Word vectors              |
| Classic NLP | Yes           | Yes                       |

দুটিই classic static embedding methods।

---

# 34. FastText

**FastText** Word2Vec-এর মতো word representation তৈরি করলেও subword information ব্যবহার করে।

Example:

```text
playing
```

এর character/subword components ব্যবহার করা যেতে পারে।

Conceptually:

```text
playing
 ↓
play
lay
ayin
...
```

Actual decomposition model-এর configuration অনুযায়ী হয়।

---

# 35. FastText কেন Useful?

Subword representation-এর কারণে:

* rare words
* unknown words
* morphological variations
* misspellings-এর কিছু ক্ষেত্রে

ভালো representation পাওয়া যেতে পারে।

বিশেষ করে morphologically rich language-এর জন্য subword information গুরুত্বপূর্ণ হতে পারে।

---

# 36. Embedding এবং Morphology

আমরা আগে শিখেছি:

```text
play
playing
played
plays
```

এগুলো related word forms।

Subword-based representation:

```text
play
+ ing
+ ed
+ s
```

এর মতো shared information capture করতে পারে।

তাই morphology এবং embeddings-এর মধ্যে strong connection আছে।

---

# 37. Embedding এবং Semantic Search

ধরো user search করল:

```text
"how to learn Python"
```

আর database-এ আছে:

```text
"Python programming tutorial for beginners"
```

Exact keyword match হয়তো perfect result নাও দিতে পারে।

Embedding-based search:

```text
Query
 ↓
Embedding
 ↓
Vector Search
 ↓
Similar Documents
```

semantic similarity ব্যবহার করে relevant result পাওয়া যায়।

---

# 38. AI Writing Assistant-এ Embedding

তোমার project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

ধরো original:

```text
The company released a new product.
```

Rewrite:

```text
The company launched a new product.
```

দুটোর embedding:

```text
Original → Vector A
Rewrite  → Vector B
```

তারপর:

```text
Similarity(A, B)
```

দেখে meaning কতটা preserved হয়েছে তার একটি signal পাওয়া যেতে পারে।

**তবে similarity score একাই meaning preservation-এর perfect guarantee নয়।**

---

# 39. Rewrite Quality Pipeline

একটি AI writing improvement system-এ:

```text
Original Text
      ↓
Generate Rewrite
      ↓
Original Embedding
      ↓
Rewrite Embedding
      ↓
Semantic Similarity
      ↓
Meaning Preservation Check
```

এটি একটি useful component।

---

# 40. Embedding + AI Detector / Text Analyzer

Text analysis system-এ embeddings ব্যবহার করা যায়:

```text
Text
 ↓
Embedding
 ↓
Classifier
 ↓
Prediction
```

যেমন:

```text
human-written
AI-generated
other classification task
```

কিন্তু বাস্তবে detector তৈরি করতে শুধু embedding similarity যথেষ্ট নয়; supervised data, model architecture, calibration এবং rigorous evaluation দরকার।

---

# 41. Embedding + Classification

ধরো:

```text
"I love this product."
```

Embedding:

```text
[0.21, 0.44, ...]
```

তারপর classifier:

```text
        Embedding
            ↓
        Classifier
            ↓
       Positive
```

এভাবে sentiment classification করা যায়।

---

# 42. Embedding + Clustering

Label না থাকলেও similar documents group করা যায়।

```text
Documents
    ↓
Embeddings
    ↓
Clustering
    ↓
Groups
```

যেমন:

```text
Cluster 1 → Sports
Cluster 2 → Technology
Cluster 3 → Politics
Cluster 4 → Education
```

---

# 43. Embedding + Recommendation

User-এর text/profile embedding:

```text
User Vector
```

Content embedding:

```text
Article Vector
```

তারপর similarity:

```text
User ↔ Article
```

High similarity হলে recommendation করা যেতে পারে।

---

# 44. Embedding-এর Limitations

Embeddings powerful হলেও perfect নয়।

### Bias

Training corpus-এর bias embedding-এ চলে আসতে পারে।

### Polysemy

Static embedding একই word-এর multiple meanings ভালোভাবে আলাদা করতে পারে না।

### Context limitation

Classic embeddings context-independent।

### Domain mismatch

General corpus-এর embedding medical/legal/scientific domain-এ optimal নাও হতে পারে।

### Meaning ≠ Vector Distance

High similarity মানেই সবসময় identical meaning নয়।

---

# 45. Contextual Embedding কেন Revolution এনেছে?

Static:

```text
bank
 ↓
one vector
```

Contextual:

```text
financial bank
 ↓
vector₁
```

```text
river bank
 ↓
vector₂
```

এতে language-এর contextual meaning better capture করা যায়।

---

# 46. BERT-এর সাথে Connection

BERT:

> **Bidirectional Encoder Representations from Transformers**

High-level:

```text
Text
 ↓
Tokenization
 ↓
Token Embeddings
+
Position Information
 ↓
Transformer Encoder
 ↓
Contextual Representations
```

একটি token-এর representation surrounding context-এর information পায়।

---

# 47. Important Distinction

Embedding আর model এক জিনিস নয়।

```text
Embedding
→ representation
```

```text
Model
→ representation ব্যবহার করে task perform করতে পারে
```

Example:

```text
Text
 ↓
Embedding
 ↓
Classifier
 ↓
Prediction
```

---

# 48. Token Embedding বনাম Positional Information

Transformer শুধু token embedding জানলে sequence order-এর information হারাতে পারে।

Example:

```text
Dog bites man.
```

এবং:

```text
Man bites dog.
```

তাই Transformer architecture-এ token-এর সাথে position/order information যুক্ত করা গুরুত্বপূর্ণ।

Concept:

```text
Token Representation
+
Position Information
 ↓
Transformer
```

---

# 49. Modern NLP Representation

এখন পুরো flow:

```text
Raw Text
   ↓
Tokenizer
   ↓
Token IDs
   ↓
Embedding
   ↓
Positional Information
   ↓
Transformer
   ↓
Contextual Representation
   ↓
Task
```

Task হতে পারে:

```text
Classification
NER
Similarity
Question Answering
Generation
Summarization
```

---

# 50. তোমার AI Writing Platform-এর Perspective

Future architecture:

```text
                  USER TEXT
                      │
                      ▼
                  TOKENIZER
                      │
                      ▼
                  TOKEN IDs
                      │
                      ▼
                  EMBEDDINGS
                      │
                      ▼
                 TRANSFORMER
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
       Meaning      Style      Similarity
       Analysis     Analysis    Analysis
          │           │           │
          └───────────┼───────────┘
                      ▼
              Writing Improvement
                      │
                      ▼
                 Final Output
```

---

# 51. Hands-on — Simple Embedding Layer

TensorFlow/Keras:

```python
import tensorflow as tf

vocab_size = 10000
embedding_dim = 128

embedding = tf.keras.layers.Embedding(
    input_dim=vocab_size,
    output_dim=embedding_dim
)

token_ids = tf.constant([[10, 25, 100]])

vectors = embedding(token_ids)

print(vectors.shape)
```

Output:

```text
(1, 3, 128)
```

মানে:

```text
1 → batch size
3 → tokens
128 → embedding dimension
```

---

# 52. Shape বুঝো

যদি:

```text
input:
(batch_size, sequence_length)
```

তাহলে embedding output:

```text
(batch_size, sequence_length, embedding_dim)
```

Example:

```text
(4, 20)
```

থেকে:

```text
(4, 20, 128)
```

---

# 53. Mini Exercise

নিজে করো:

```python
vocab_size = 5000
embedding_dim = 64
```

Input:

```text
batch_size = 2
sequence_length = 10
```

Question:

**Embedding output shape কত হবে?**

উত্তর:

```text
(2, 10, 64)
```

---

# 54. Theory Practice

### Beginner

1. What is Word Embedding?
2. Why do we need embeddings?
3. What is one-hot encoding?
4. What is dense representation?
5. What is distributional hypothesis?
6. What is embedding dimension?
7. What is an embedding matrix?

### Intermediate

8. What is Word2Vec?
9. What is CBOW?
10. What is Skip-gram?
11. CBOW vs Skip-gram?
12. What is GloVe?
13. What is FastText?
14. What is cosine similarity?
15. What is sentence embedding?
16. What is document embedding?

### Advanced

17. Static vs contextual embeddings?
18. Why does Word2Vec struggle with polysemy?
19. How does FastText use subword information?
20. How are embeddings learned?
21. What is an embedding layer?
22. How are embeddings used in semantic search?
23. How can embeddings help paraphrase analysis?
24. How can embeddings help meaning preservation?
25. Why isn't embedding similarity a perfect semantic equivalence test?

---

# 55. Interview Questions

### Q1. What is Word Embedding?

Word-এর semantic এবং linguistic information numerical dense vector হিসেবে represent করার পদ্ধতি।

### Q2. Why is one-hot encoding insufficient for semantic representation?

কারণ one-hot representation সাধারণত words-এর semantic similarity encode করে না এবং vocabulary বড় হলে vector খুব sparse/high-dimensional হয়।

### Q3. Word2Vec-এর দুটি architecture কী?

```text
CBOW
Skip-gram
```

### Q4. CBOW কী করে?

Context words ব্যবহার করে target word predict করে।

### Q5. Skip-gram কী করে?

Target word ব্যবহার করে surrounding context words predict করতে শেখে।

### Q6. Static vs contextual embedding?

```text
Static
→ word-এর fixed representation

Contextual
→ surrounding context অনুযায়ী representation পরিবর্তিত হয়
```

### Q7. Word2Vec এবং GloVe-এর difference?

Word2Vec predictive training ব্যবহার করে; GloVe global word co-occurrence statistics ব্যবহার করে vector শেখে।

### Q8. Embedding কোথায় ব্যবহার করা হয়?

* Classification
* Similarity
* Semantic search
* Clustering
* Recommendation
* Information retrieval
* NLP model inputs
* Paraphrase analysis

---

# 56. M02.15 Completion Checklist

* [ ] Word Embedding
* [ ] One-hot encoding
* [ ] Dense representation
* [ ] Distributional Hypothesis
* [ ] Embedding Space
* [ ] Embedding Dimension
* [ ] Embedding Matrix
* [ ] Word ID
* [ ] Embedding Layer
* [ ] Word2Vec
* [ ] CBOW
* [ ] Skip-gram
* [ ] CBOW vs Skip-gram
* [ ] Static Embedding
* [ ] Contextual Embedding
* [ ] GloVe
* [ ] FastText
* [ ] Subword Representation
* [ ] Cosine Similarity
* [ ] Euclidean Distance
* [ ] Sentence Embedding
* [ ] Document Embedding
* [ ] Semantic Search
* [ ] Similarity Analysis
* [ ] Clustering
* [ ] Embedding + Classification
* [ ] Embedding + Recommendation
* [ ] Embedding + Paraphrase Analysis
* [ ] Meaning Preservation
* [ ] BERT-এর সাথে Embedding connection
* [ ] Transformer-এর সাথে Embedding connection
* [ ] TensorFlow Embedding Layer
* [ ] Embedding shape বুঝি

---

# Final Mental Model

```text
                     WORD
                       │
                       ▼
                    TOKEN ID
                       │
                       ▼
               EMBEDDING VECTOR
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
       Static Embedding    Contextual Embedding
             │                   │
      Word2Vec/GloVe       Transformer/BERT
             │                   │
             └─────────┬─────────┘
                       ▼
                VECTOR SPACE
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
      Similarity    Classification  Search
          │            │            │
          └────────────┼────────────┘
                       ▼
                 NLP APPLICATION
```

### সবচেয়ে গুরুত্বপূর্ণ progression

```text
Text
 ↓
Token
 ↓
Token ID
 ↓
Embedding
 ↓
Contextual Representation
 ↓
Meaning
 ↓
NLP Task
```

**M02.15-এর core idea:**

> Machine-এর কাছে word শুধু `"cat"` নয়; embedding-এর মাধ্যমে সেটি এমন একটি numerical representation হয়ে যায় যার মধ্যে language-এর semantic/linguistic patterns শেখা সম্ভব।


---
# M02.16 — Language Modeling (N-gram → Neural Language Model)

M02.15-এ আমরা **Word Embeddings & Vector Semantics** শেষ করেছি। এখন NLP-এর খুব গুরুত্বপূর্ণ একটি foundation topic হলো **Language Modeling**।

Language Model-এর মূল প্রশ্ন:

> **“একটি শব্দ/sequence-এর পরে কোন শব্দ আসার সম্ভাবনা কত?”**

এটি পরবর্তীতে **RNN, LSTM, Transformer, BERT, GPT এবং AI Writing Assistant** বোঝার foundation তৈরি করবে।

---

# 1. Language Model কী?

**Language Model (LM)** হলো এমন একটি model যা ভাষার sequence থেকে সম্ভাব্যতা শেখে।

ধরো:

```text
I am going to ...
```

Model predict করতে পারে:

```text
school
market
college
work
```

অর্থাৎ:

```text
Previous words
      ↓
Language Model
      ↓
Next-word probability
```

উদাহরণ:

```text
"I am going to"

school → 0.40
work   → 0.25
market → 0.15
play   → 0.05
...
```

সবচেয়ে বেশি probability-এর word হতে পারে:

```text
school
```

---

# 2. Probability দিয়ে Language Model

Language model মূলত probability ব্যবহার করে।

ধরো:

```text
I love machine learning
```

আমরা probability লিখতে পারি:

```text
P(I love machine learning)
```

Chain Rule অনুযায়ী:

```text
P(I, love, machine, learning)
```

=

```text
P(I)
× P(love | I)
× P(machine | I love)
× P(learning | I love machine)
```

অর্থাৎ:

```text
P(sentence)
=
P(word1)
× P(word2 | word1)
× P(word3 | previous words)
× ...
```

এটাই language modeling-এর mathematical foundation।

---

# 3. Conditional Probability

Language model-এর জন্য সবচেয়ে গুরুত্বপূর্ণ concept:

```text
P(next word | previous words)
```

যেমন:

```text
P(learning | machine)
```

অথবা:

```text
P(is | The student)
```

অর্থাৎ:

> আগের শব্দগুলো জানা থাকলে পরের শব্দটির probability কত?

---

# 4. Example

Sentence:

```text
The cat is sleeping
```

একটি simple model ভাবতে পারে:

```text
P(The)
P(cat | The)
P(is | The cat)
P(sleeping | The cat is)
```

তাহলে:

```text
P(The cat is sleeping)
=
P(The)
× P(cat | The)
× P(is | The cat)
× P(sleeping | The cat is)
```

---

# 5. কিন্তু সমস্যা কোথায়?

পুরো previous sentence ব্যবহার করলে সমস্যা হয়।

ধরো:

```text
The intelligent student from Bangladesh is learning Python
```

এখানে:

```text
P(Python | The intelligent student from Bangladesh is learning)
```

এ ধরনের সব possible sequence-এর probability শেখা খুব difficult।

কারণ vocabulary এবং sentence length অনেক বড়।

এখান থেকেই আসে:

# N-gram Language Model

---

# 6. N-gram কী?

**N-gram** হলো consecutive `N`টি token/word-এর sequence।

### Unigram

```text
N = 1
```

Example:

```text
I love NLP
```

Unigrams:

```text
I
love
NLP
```

---

### Bigram

```text
N = 2
```

```text
I love NLP
```

Bigrams:

```text
I love
love NLP
```

---

### Trigram

```text
N = 3
```

```text
I love NLP
```

Trigrams:

```text
I love NLP
```

---

### 4-gram

```text
I love learning NLP
```

4-gram:

```text
I love learning NLP
```

---

# 7. N-gram Visualization

```text
Sentence
   ↓
"I love learning NLP"

Unigram
   ↓
I
love
learning
NLP

Bigram
   ↓
I love
love learning
learning NLP

Trigram
   ↓
I love learning
love learning NLP
```

---

# 8. Bigram Language Model

Bigram model ধরে নেয়:

> পরের word predict করার জন্য শুধু আগের একটি word দরকার।

অর্থাৎ:

```text
P(wₙ | w₁, w₂, ..., wₙ₋₁)
```

এর পরিবর্তে:

```text
P(wₙ | wₙ₋₁)
```

Example:

```text
I love machine learning
```

Bigram approximation:

```text
P(I)
× P(love | I)
× P(machine | love)
× P(learning | machine)
```

---

# 9. Trigram Language Model

Trigram model আগের দুইটি word ব্যবহার করে।

```text
P(wₙ | wₙ₋₂, wₙ₋₁)
```

Example:

```text
I love machine learning
```

তাহলে:

```text
P(I)
× P(love | I)
× P(machine | I love)
× P(learning | love machine)
```

এটি Bigram-এর চেয়ে বেশি context ব্যবহার করে।

---

# 10. N-gram-এর Python Implementation

প্রথমে sentence:

```python
text = "I love machine learning"
```

Tokenization:

```python
tokens = text.split()

print(tokens)
```

Output:

```text
['I', 'love', 'machine', 'learning']
```

---

## Bigram তৈরি

```python
bigrams = []

for i in range(len(tokens) - 1):
    bigram = (tokens[i], tokens[i + 1])
    bigrams.append(bigram)

print(bigrams)
```

Output:

```text
[
    ('I', 'love'),
    ('love', 'machine'),
    ('machine', 'learning')
]
```

---

# 11. Trigram তৈরি

```python
trigrams = []

for i in range(len(tokens) - 2):
    trigram = (
        tokens[i],
        tokens[i + 1],
        tokens[i + 2]
    )

    trigrams.append(trigram)

print(trigrams)
```

Output:

```text
[
    ('I', 'love', 'machine'),
    ('love', 'machine', 'learning')
]
```

---

# 12. N-gram Function

Reusable function:

```python
def generate_ngrams(tokens, n):
    return [
        tuple(tokens[i:i+n])
        for i in range(len(tokens) - n + 1)
    ]


tokens = "I love machine learning".split()

print(generate_ngrams(tokens, 1))
print(generate_ngrams(tokens, 2))
print(generate_ngrams(tokens, 3))
```

Output:

```text
[('I',), ('love',), ('machine',), ('learning',)]

[('I', 'love'), ('love', 'machine'), ('machine', 'learning')]

[('I', 'love', 'machine'), ('love', 'machine', 'learning')]
```

---

# 13. Word Frequency

Language model-এর জন্য frequency খুব গুরুত্বপূর্ণ।

Example:

```text
I love NLP
I love Python
I love AI
```

Words:

```text
I     → 3
love  → 3
NLP   → 1
Python→ 1
AI    → 1
```

Python:

```python
from collections import Counter

text = """
I love NLP
I love Python
I love AI
"""

tokens = text.lower().split()

frequency = Counter(tokens)

print(frequency)
```

---

# 14. Bigram Frequency

```python
from collections import Counter

text = """
I love NLP
I love Python
I love AI
"""

tokens = text.lower().split()

bigrams = [
    tuple(tokens[i:i+2])
    for i in range(len(tokens) - 1)
]

frequency = Counter(bigrams)

print(frequency)
```

Conceptually:

```text
('i', 'love') → 3
('love', 'nlp') → 1
('love', 'python') → 1
('love', 'ai') → 1
```

---

# 15. Bigram Probability

ধরো dataset:

```text
I love NLP
I love Python
I love AI
```

আমরা জানতে চাই:

```text
P(love | I)
```

Formula:

```text
P(love | I)
=
Count(I, love)
----------------
Count(I)
```

এখানে:

```text
Count(I, love) = 3
Count(I) = 3
```

তাই:

```text
P(love | I) = 3/3 = 1
```

---

# 16. Python Bigram Probability

```python
from collections import Counter

text = """
I love NLP
I love Python
I love AI
"""

tokens = text.lower().split()

unigrams = Counter(tokens)

bigrams = Counter(
    tuple(tokens[i:i+2])
    for i in range(len(tokens) - 1)
)

word = "i"
next_word = "love"

probability = (
    bigrams[(word, next_word)]
    / unigrams[word]
)

print(probability)
```

Output:

```text
1.0
```

---

# 17. Sentence Probability

ধরো:

```text
I love NLP
```

Bigram model:

```text
P(I)
× P(love | I)
× P(NLP | love)
```

এভাবে একটি complete sentence-এর probability calculate করা যায়।

---

# 18. Start এবং End Tokens

Language modeling-এ sentence boundary গুরুত্বপূর্ণ।

Original:

```text
I love NLP
```

আমরা ব্যবহার করতে পারি:

```text
<BOS> I love NLP <EOS>
```

যেখানে:

```text
<BOS> = Beginning Of Sentence
<EOS> = End Of Sentence
```

তাহলে bigrams:

```text
<BOS> I
I love
love NLP
NLP <EOS>
```

এটি language model-কে sentence শুরু এবং শেষ বুঝতে সাহায্য করে।

---

# 19. Vocabulary

Language model-এর জন্য vocabulary দরকার।

Example:

```text
I love NLP
I love Python
```

Vocabulary:

```text
{
    I,
    love,
    NLP,
    Python
}
```

Vocabulary size:

```text
4
```

Modern NLP-তে vocabulary সাধারণত **subword tokens** দিয়ে তৈরি হয়।

---

# 20. Unknown Word — `<UNK>`

Training data-তে কোনো word না থাকলে:

```text
<UNK>
```

ব্যবহার করা হতে পারে।

Example:

```text
I love programming
```

যদি:

```text
programming
```

vocabulary-তে না থাকে:

```text
I love <UNK>
```

তবে modern Transformer tokenizer-এ সাধারণত subword tokenization-এর কারণে এই সমস্যা অনেক কমে যায়।

---

# 21. N-gram-এর প্রধান সমস্যা

এটি খুব গুরুত্বপূর্ণ।

### Problem 1 — Data Sparsity

অনেক sequence training data-তে একবারও দেখা যাবে না।

```text
I love artificial intelligence
```

যদি এই exact sequence training data-তে না থাকে:

```text
Count = 0
```

তাহলে probability:

```text
0
```

হয়ে যেতে পারে।

---

# 22. Problem 2 — Zero Probability

ধরো:

```text
P(machine | quantum) = 0
```

শুধু training data-তে দেখা যায়নি বলে।

কিন্তু বাস্তবে:

```text
quantum machine
```

valid phrase হতে পারে।

এই সমস্যা:

> **Zero Probability Problem**

---

# 23. Smoothing

Zero probability সমস্যা কমানোর জন্য **smoothing** ব্যবহার করা হয়।

Common techniques:

```text
Laplace Smoothing
Add-k Smoothing
Good-Turing Smoothing
Kneser-Ney Smoothing
```

Foundation হিসেবে এখন মনে রাখো:

```text
Raw N-gram
    ↓
Zero probability
    ↓
Smoothing
    ↓
Better probability estimation
```

---

# 24. Problem 3 — Limited Context

Bigram:

```text
I love
```

শুধু previous word দেখে।

Trigram:

```text
I love machine
```

শুধু previous 2 words দেখে।

কিন্তু language-এ অনেক সময় long-range context দরকার।

Example:

```text
The student who studied Python for several months
finally built an AI application.
```

শেষের অংশ বুঝতে অনেক আগের context দরকার হতে পারে।

N-gram-এর fixed window limitation আছে।

---

# 25. N-gram বনাম Neural Language Model

### N-gram

```text
Text
 ↓
Count words
 ↓
Count n-grams
 ↓
Probability
 ↓
Prediction
```

### Neural Language Model

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embeddings
 ↓
Neural Network
 ↓
Probability Distribution
 ↓
Next Token
```

---

# 26. Neural Language Model

এখানে আমরা M02.15-এর embedding concept ব্যবহার করতে পারি।

```text
Token
 ↓
Token ID
 ↓
Embedding Vector
 ↓
Neural Network
 ↓
Next-word prediction
```

ধরো:

```text
I love machine
```

Model predict করবে:

```text
learning → 0.62
translation → 0.08
vision → 0.05
...
```

---

# 27. RNN Language Model

পরবর্তী পর্যায়ে আমরা RNN/LSTM বিস্তারিত শিখব।

Basic idea:

```text
I
 ↓
RNN
 ↓
love
 ↓
RNN
 ↓
machine
 ↓
RNN
 ↓
learning
```

RNN previous information-এর একটি hidden state ধরে রাখে।

```text
Previous context
       ↓
     RNN
       ↓
Hidden State
       ↓
Next prediction
```

---

# 28. LSTM Language Model

RNN-এর long-term dependency সমস্যা কমানোর জন্য:

```text
LSTM
```

ব্যবহার করা হয়।

Concept:

```text
Input
 ↓
LSTM
 ↓
Hidden State
 ↓
Prediction
```

এটি পরে **M02-এর NLP Deep Learning অংশে** বিস্তারিত আসবে।

---

# 29. Transformer Language Model

Modern NLP-এর সবচেয়ে গুরুত্বপূর্ণ architecture:

```text
Transformer
```

Concept:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embeddings
 ↓
Transformer
 ↓
Contextual Representation
 ↓
Next Token / Task
```

GPT-type systems autoregressive language modeling ব্যবহার করে।

Conceptually:

```text
The
 ↓
The cat
 ↓
The cat is
 ↓
The cat is sleeping
```

প্রতিটি step-এ পরবর্তী token predict করা হয়।

---

# 30. Language Model Training

Training-এর basic concept:

```text
Input:
"I love machine"

Target:
"learning"
```

Model prediction:

```text
learning → 0.40
Python   → 0.20
AI       → 0.10
...
```

Target:

```text
learning
```

Model ভুল করলে:

```text
Loss
 ↓
Backpropagation
 ↓
Weights update
```

বারবার training-এর মাধ্যমে prediction improve হয়।

---

# 31. Next Token Prediction

Modern generative NLP-এর foundation:

```text
Input:
"I want to learn"

Prediction:
"Python"
```

তারপর:

```text
"I want to learn Python"
```

আবার predict:

```text
"for"
```

তারপর:

```text
"I want to learn Python for"
```

এভাবে:

```text
Token
 ↓
Predict next token
 ↓
Add token
 ↓
Predict next token
 ↓
Add token
 ↓
...
```

এটাই autoregressive generation-এর basic idea।

---

# 32. AI Writing Assistant-এর সাথে Connection

তোমার future AI writing platform-এর জন্য এই concept খুব গুরুত্বপূর্ণ।

User লিখল:

```text
Artificial intelligence is changing the way
```

Language model context দেখে সম্ভাব্য continuation দিতে পারে:

```text
people work.
```

অথবা rewriting system-এর ক্ষেত্রে:

```text
AI is transforming how people work.
```

তবে শুধু next-token prediction দিয়ে high-quality rewriting system তৈরি হয় না। সেখানে আরও দরকার:

```text
Language Model
+
Semantic Understanding
+
Context
+
Instruction Following
+
Generation
+
Quality Evaluation
```

---

# 33. Language Model-এর Evolution

এটি অবশ্যই মনে রাখবে:

```text
Statistical NLP
      ↓
N-gram Language Model
      ↓
Neural Language Model
      ↓
RNN
      ↓
LSTM / GRU
      ↓
Attention
      ↓
Transformer
      ↓
Large Language Model
```

---

# 34. N-gram vs RNN vs Transformer

| Model       | Context                 | Main Idea       |
| ----------- | ----------------------- | --------------- |
| Unigram     | 1 word                  | Word frequency  |
| Bigram      | 1 previous word         | Word pair       |
| Trigram     | 2 previous words        | 3-word sequence |
| N-gram      | Fixed N                 | Fixed context   |
| RNN         | Sequential              | Hidden state    |
| LSTM        | Long sequential context | Memory/gates    |
| Transformer | Large context           | Attention       |

---

# 35. Perplexity

Language Model evaluation-এর একটি গুরুত্বপূর্ণ metric:

> **Perplexity**

সহজভাবে:

> Model কতটা uncertain about the next token?

Lower perplexity সাধারণত better language modeling performance নির্দেশ করে, যখন একই evaluation setup ব্যবহার করা হয়।

Conceptually:

```text
Low Perplexity
      ↓
More confident / better prediction

High Perplexity
      ↓
More uncertainty / worse prediction
```

Mathematical form:

```text
PP(W) = P(W)^(-1/N)
```

অথবা সাধারণভাবে:

```text
PP = exp(Cross Entropy)
```

Perplexity পরে আমরা **Language Model Evaluation**-এ আরও গভীরভাবে করব।

---

# 36. খুব গুরুত্বপূর্ণ Difference

### Language Model

```text
What is likely next?
```

### Embedding

```text
What does this word/vector represent?
```

### POS

```text
What grammatical role does this word have?
```

### NER

```text
Is this a named entity?
```

### Dependency Parsing

```text
How are words grammatically connected?
```

### Semantic Analysis

```text
What does the text mean?
```

---

# 37. Complete NLP Flow এখন

আমরা যেসব topic শিখেছি সেগুলোকে একসাথে দেখো:

```text
RAW TEXT
   ↓
Tokenization
   ↓
Stopwords
   ↓
Stemming / Lemmatization
   ↓
POS Tagging
   ↓
NER
   ↓
Chunking
   ↓
Dependency Parsing
   ↓
Constituency Parsing
   ↓
Semantic Analysis
   ↓
Word Embeddings
   ↓
Language Modeling
   ↓
Neural Networks
   ↓
Transformers
   ↓
LLM
```

এখন আমরা ধীরে ধীরে **classical NLP → neural NLP → Transformer NLP**-এর দিকে যাচ্ছি।

---

# 38. Practice Task

### Task 1 — Unigram

এই sentence-এর unigram বের করো:

```text
Python is easy to learn
```

---

### Task 2 — Bigram

```text
Python is easy to learn
```

Bigram বের করো।

Expected pattern:

```text
Python is
is easy
easy to
to learn
```

---

### Task 3 — Trigram

```text
I am learning Python
```

Trigram বের করো।

---

### Task 4 — Frequency

```text
I love Python
I love AI
I love NLP
```

প্রতিটি word-এর frequency বের করো।

---

### Task 5 — Bigram Probability

এই text:

```text
I love NLP
I love Python
I love AI
```

Calculate:

```text
P(love | I)
```

---

### Task 6 — নিজের N-gram function

এমন function তৈরি করো:

```python
generate_ngrams(tokens, n)
```

যেটা:

```python
generate_ngrams(
    ["I", "love", "NLP"],
    2
)
```

return করবে:

```text
[
    ("I", "love"),
    ("love", "NLP")
]
```

---

# 39. Theory Questions

নিজে answer দেওয়ার চেষ্টা করবে:

1. What is a Language Model?
2. What is conditional probability?
3. What is an N-gram?
4. What is a unigram?
5. What is a bigram?
6. What is a trigram?
7. Bigram কীভাবে next word predict করে?
8. What is data sparsity?
9. What is zero probability problem?
10. What is smoothing?
11. Why do N-gram models have limited context?
12. What is a neural language model?
13. What is next-token prediction?
14. What is autoregressive generation?
15. What is perplexity?
16. N-gram vs RNN?
17. RNN vs LSTM?
18. LSTM vs Transformer?
19. Language Model এবং Word Embedding-এর difference কী?
20. GPT-type systems-এর সাথে language modeling-এর relationship কী?

---

# 40. Interview Questions

### Q1. What is an N-gram?

**Answer:**

An N-gram is a contiguous sequence of N tokens or words from a text.

Example:

```text
"I love NLP"
```

Bigram:

```text
I love
love NLP
```

---

### Q2. What is a bigram language model?

A bigram language model predicts the next word using only the immediately previous word:

```text
P(wᵢ | wᵢ₋₁)
```

---

### Q3. What is the major limitation of N-gram models?

Main limitations:

```text
Data sparsity
Limited context
Large memory requirements for large N
Zero probabilities
Poor handling of unseen sequences
```

---

### Q4. Why are Transformers better than traditional N-grams?

Traditional N-grams use a fixed-size context, while Transformers can model relationships across much larger contexts using **attention**.

---

# 41. AI Writing Platform-এর জন্য কী শিখলে?

তোমার target architecture ধীরে ধীরে এমন হবে:

```text
                    USER TEXT
                        ↓
                   Tokenization
                        ↓
                Linguistic Analysis
                        ↓
                 Semantic Analysis
                        ↓
                  Embeddings
                        ↓
                Language Model
                        ↓
                  Transformer
                        ↓
              Text Generation
                        ↓
              Rewrite / Improve
                        ↓
                  Final Text
```

তবে এখনই Transformer implementation-এ jump করব না।

আমাদের foundation sequence হবে:

```text
M02
 │
 ├── NLP Fundamentals
 │
 ├── Text Processing
 │
 ├── Linguistic Analysis
 │
 ├── Semantic Analysis
 │
 ├── Embeddings
 │
 ├── Language Modeling  ← আজ
 │
 ├── Neural NLP
 │
 ├── RNN
 │
 ├── LSTM / GRU
 │
 ├── Attention
 │
 └── Transformer
```

---

# ✅ M02.16 Completion Checklist

আজকের lesson শেষ হলে তুমি explain করতে পারবে:

* [x] Language Model
* [x] Conditional Probability
* [x] Chain Rule
* [x] Unigram
* [x] Bigram
* [x] Trigram
* [x] N-gram
* [x] N-gram generation
* [x] Word frequency
* [x] Bigram probability
* [x] Sentence probability
* [x] BOS / EOS
* [x] Vocabulary
* [x] `<UNK>`
* [x] Data sparsity
* [x] Zero probability
* [x] Smoothing
* [x] Limited context
* [x] Neural Language Model
* [x] Next-token prediction
* [x] Autoregressive generation
* [x] RNN Language Model concept
* [x] LSTM Language Model concept
* [x] Transformer Language Model concept
* [x] Perplexity
* [x] N-gram vs Neural LM
* [x] Language Model vs Embedding
* [x] AI Writing Assistant connection

### 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ mental model

```text
Text
 ↓
Tokens
 ↓
N-grams
 ↓
Probability
 ↓
Next-word prediction
 ↓
Neural Language Model
 ↓
RNN / LSTM
 ↓
Attention
 ↓
Transformer
 ↓
LLM
```

**M02.16 = Language Modeling Foundation complete.**


----
# M02.17 — RNN (Recurrent Neural Network) for NLP

M02.16-এ আমরা **Language Modeling** শিখেছি—বিশেষ করে N-gram, next-word prediction, probability এবং autoregressive generation।

এখন তার পরের গুরুত্বপূর্ণ step:

> **RNN কীভাবে sequence/text-এর previous information মনে রেখে next prediction করে?**

NLP-এর historical deep-learning evolution বুঝতে **RNN → LSTM → GRU → Attention → Transformer** খুব গুরুত্বপূর্ণ।

---

# 1. RNN কী?

**RNN = Recurrent Neural Network**

এটি এমন একটি neural network যা **sequential data** process করার জন্য তৈরি।

NLP-তে text হলো sequence:

```text
I → love → machine → learning
```

RNN একসাথে সব word না দেখে sequentially process করে:

```text
I
 ↓
RNN
 ↓
love
 ↓
RNN
 ↓
machine
 ↓
RNN
 ↓
learning
```

মূল idea:

> আগের step-এর information পরের step-এ পাঠানো হয়।

---

# 2. কেন RNN দরকার?

সাধারণ neural network:

```text
Input
 ↓
Neural Network
 ↓
Output
```

প্রতিটি input independent হতে পারে।

কিন্তু language-এ:

```text
I love machine learning
```

`learning` শব্দটি বুঝতে আগের words গুরুত্বপূর্ণ।

তাই দরকার:

```text
Previous information
        ↓
Current input
        ↓
      RNN
        ↓
New information
```

---

# 3. RNN-এর Core Idea

ধরো sequence:

```text
x₁ → x₂ → x₃ → x₄
```

RNN:

```text
x₁ → [RNN] → h₁
             ↓
x₂ → [RNN] → h₂
             ↓
x₃ → [RNN] → h₃
             ↓
x₄ → [RNN] → h₄
```

এখানে:

* `x` = input
* `h` = hidden state

Hidden state হলো RNN-এর **running memory/context representation**।

---

# 4. Hidden State

সবচেয়ে গুরুত্বপূর্ণ concept:

```text
Hidden State
```

এটি previous information বহন করে।

ধরো:

```text
I love machine learning
```

প্রথম:

```text
I
 ↓
RNN
 ↓
h₁
```

তারপর:

```text
love + h₁
      ↓
     RNN
      ↓
     h₂
```

তারপর:

```text
machine + h₂
         ↓
        RNN
         ↓
        h₃
```

তারপর:

```text
learning + h₃
           ↓
          RNN
           ↓
          h₄
```

অর্থাৎ:

```text
h₁ → h₂ → h₃ → h₄
```

context forward যাচ্ছে।

---

# 5. RNN Mathematical Formula

Basic RNN equation:

$$
h_t = f(W_xx_t + W_hh_{t-1} + b)
$$

এখানে:

* `x_t` = current input
* `h_{t-1}` = previous hidden state
* `h_t` = current hidden state
* `W_x` = input weights
* `W_h` = recurrent weights
* `b` = bias
* `f` = activation function

সহজভাবে:

```text
Current Input
     +
Previous Hidden State
     ↓
   RNN
     ↓
Current Hidden State
```

---

# 6. Output

RNN hidden state থেকে output তৈরি করতে পারে:

$$
y_t = g(W_yh_t + b_y)
$$

Flow:

```text
Input
 ↓
Hidden State
 ↓
Output
```

Language modeling:

```text
Previous words
      ↓
     RNN
      ↓
Probability distribution
      ↓
Next token
```

---

# 7. RNN দিয়ে Next Word Prediction

Input:

```text
I love
```

Model predict করবে:

```text
machine → 0.45
Python  → 0.20
NLP     → 0.10
AI      → 0.08
...
```

তারপর:

```text
I love machine
```

আবার prediction:

```text
learning → 0.60
vision   → 0.08
...
```

এভাবে:

```text
Input sequence
      ↓
RNN
      ↓
Next-token probabilities
      ↓
Selected token
      ↓
New sequence
```

---

# 8. RNN Unrolling

RNN-এর একটি cell বারবার ব্যবহার করা হয়।

Conceptually:

```text
           ┌──────────────┐
x₁ ───────→│              │──→ h₁
           │     RNN      │
           └──────────────┘
                    │
                    ↓
           ┌──────────────┐
x₂ ───────→│     RNN      │──→ h₂
           └──────────────┘
                    │
                    ↓
           ┌──────────────┐
x₃ ───────→│     RNN      │──→ h₃
           └──────────────┘
```

বাস্তবে একই RNN parameters বিভিন্ন timestep-এ reuse হয়।

এটাকে বলা হয়:

> **Parameter Sharing**

---

# 9. Sequence-to-One

একটি পুরো sequence থেকে একটি output।

Example:

```text
"This movie is excellent"
```

Output:

```text
Positive
```

Flow:

```text
This
 ↓
movie
 ↓
is
 ↓
excellent
 ↓
RNN
 ↓
Positive
```

ব্যবহার:

* Sentiment Analysis
* Text Classification
* Spam Detection
* Document Classification

---

# 10. Sequence-to-Sequence

Input sequence থেকে output sequence।

Example:

```text
English
   ↓
RNN
   ↓
French
```

Concept:

```text
I love you
     ↓
Je t'aime
```

ব্যবহার:

* Machine Translation
* Text Transformation
* Sequence Generation

---

# 11. Sequence-to-Sequence Architecture

Conceptually:

```text
Input Sequence
      ↓
   Encoder
      ↓
Context
      ↓
   Decoder
      ↓
Output Sequence
```

Example:

```text
"I love NLP"
     ↓
  Encoder
     ↓
  Context
     ↓
  Decoder
     ↓
"J'aime le NLP"
```

এটি পরবর্তীতে **Encoder-Decoder** architecture বোঝার foundation দেবে।

---

# 12. Many-to-One

```text
x₁
 ↓
x₂
 ↓
x₃
 ↓
RNN
 ↓
Output
```

Example:

```text
"I really like this movie"
              ↓
         Sentiment
              ↓
           Positive
```

---

# 13. One-to-Many

একটি input থেকে sequence output।

Example:

```text
Image
 ↓
RNN
 ↓
A
 ↓
beautiful
 ↓
sunset
```

Image captioning-এ historical architecture হিসেবে এই ধারণা ব্যবহার করা হয়েছে।

---

# 14. Many-to-Many

প্রতিটি input-এর জন্য output।

Example:

```text
John    → PERSON
lives   → O
in      → O
Dhaka   → LOCATION
```

এটি sequence labeling-এর মতো task-এ ব্যবহার করা যায়।

---

# 15. RNN Architecture Types

মনে রাখবে:

```text
One-to-One
One-to-Many
Many-to-One
Many-to-Many
```

NLP-তে সবচেয়ে গুরুত্বপূর্ণ:

```text
Many-to-One
Many-to-Many
Sequence-to-Sequence
```

---

# 16. RNN + Embedding

M02.15-এ আমরা embedding শিখেছি।

RNN সাধারণত raw word directly নেয় না।

Flow:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
Vectors
 ↓
RNN
 ↓
Output
```

Example:

```text
"I love NLP"
```

Token IDs:

```text
[10, 25, 73]
```

Embedding:

```text
10 → [0.21, 0.45, ...]
25 → [0.17, 0.72, ...]
73 → [0.33, 0.11, ...]
```

তারপর:

```text
Embedding vectors
       ↓
      RNN
       ↓
 Prediction
```

---

# 17. Keras-এ Simple RNN

TensorFlow/Keras দিয়ে:

```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Embedding(
        input_dim=10000,
        output_dim=128
    ),

    tf.keras.layers.SimpleRNN(128),

    tf.keras.layers.Dense(1, activation="sigmoid")
])

model.summary()
```

এখানে:

```text
Embedding
    ↓
SimpleRNN
    ↓
Dense
    ↓
Output
```

---

# 18. RNN-এর Input Shape

ধরো:

```python
batch_size = 32
sequence_length = 20
```

Input shape:

```text
(32, 20)
```

অর্থাৎ:

```text
32 sequences
×
20 tokens
```

Embedding-এর পরে:

```text
(32, 20, 128)
```

কারণ:

```text
(batch, sequence_length, embedding_dimension)
```

---

# 19. RNN Output

Keras:

```python
tf.keras.layers.SimpleRNN(128)
```

default-এ final hidden representation দিতে পারে:

```text
(batch_size, 128)
```

কিন্তু:

```python
tf.keras.layers.SimpleRNN(
    128,
    return_sequences=True
)
```

দিলে:

```text
(batch_size, sequence_length, 128)
```

অর্থাৎ প্রতিটি timestep-এর output পাওয়া যায়।

---

# 20. `return_sequences`

খুব গুরুত্বপূর্ণ।

### False

```python
SimpleRNN(128)
```

Output:

```text
(batch, 128)
```

শুধু শেষ timestep-এর representation।

### True

```python
SimpleRNN(
    128,
    return_sequences=True
)
```

Output:

```text
(batch, sequence_length, 128)
```

প্রতিটি timestep-এর representation।

---

# 21. Stacking RNN

একাধিক RNN layer ব্যবহার করা যায়।

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(10000, 128),

    tf.keras.layers.SimpleRNN(
        128,
        return_sequences=True
    ),

    tf.keras.layers.SimpleRNN(64),

    tf.keras.layers.Dense(1, activation="sigmoid")
])
```

Flow:

```text
Embedding
    ↓
RNN 128
    ↓
RNN 64
    ↓
Dense
    ↓
Output
```

---

# 22. RNN Training

ধরো:

```text
Input:
"I love"

Target:
"machine"
```

Model:

```text
"I love"
   ↓
 RNN
   ↓
Prediction
```

Prediction:

```text
machine → 0.30
Python  → 0.20
NLP     → 0.10
...
```

Target:

```text
machine
```

Loss calculate হবে।

```text
Prediction
     ↓
    Loss
     ↓
Backpropagation
     ↓
Weight Update
```

---

# 23. Backpropagation Through Time

RNN-এর training-এর বিশেষ algorithmic concept:

> **BPTT = Backpropagation Through Time**

Unrolled RNN:

```text
x₁ → h₁ → h₂ → h₃ → h₄
      ↑    ↑    ↑    ↑
```

Training-এর সময় error sequence-এর timestep-এর মধ্য দিয়ে backward যায়।

Concept:

```text
Forward:
x₁ → x₂ → x₃ → x₄

Backward:
x₄ → x₃ → x₂ → x₁
```

এটাই:

```text
Backpropagation
+
Time
=
BPTT
```

---

# 24. Vanishing Gradient Problem

RNN-এর সবচেয়ে গুরুত্বপূর্ণ limitation।

Long sequence:

```text
x₁ → x₂ → x₃ → ... → x₁₀₀
```

Gradient backward যাওয়ার সময় খুব ছোট হয়ে যেতে পারে।

```text
Gradient
 ↓
0.5
 ↓
0.2
 ↓
0.05
 ↓
0.001
 ↓
0.00001
```

ফলে early information-এর জন্য model properly learn করতে পারে না।

এটাকে বলে:

> **Vanishing Gradient**

---

# 25. Exploding Gradient Problem

উল্টোভাবে gradient অনেক বড় হয়ে যেতে পারে।

```text
0.5
 ↓
2
 ↓
10
 ↓
100
 ↓
1000
```

এটাকে বলে:

> **Exploding Gradient**

ফলে training unstable হতে পারে।

---

# 26. Gradient Clipping

Exploding gradient মোকাবিলায়:

```text
Gradient Clipping
```

ব্যবহার করা যায়।

Concept:

```text
Very Large Gradient
        ↓
Gradient Clipping
        ↓
Controlled Gradient
```

TensorFlow-তে optimizer-এ:

```python
optimizer = tf.keras.optimizers.Adam(
    clipnorm=1.0
)
```

---

# 27. Long-Term Dependency Problem

এটি খুব গুরুত্বপূর্ণ।

Sentence:

```text
The boy who lives in Dhaka and studies computer science
every day is learning Python.
```

শেষের:

```text
is
```

বোঝার জন্য অনেক আগের:

```text
boy
```

information দরকার হতে পারে।

কিন্তু standard RNN দীর্ঘ sequence-এ আগের information effectively preserve করতে struggle করতে পারে।

এটাই:

> **Long-Term Dependency Problem**

---

# 28. RNN-এর Limitations

মূল limitations:

### 1. Sequential computation

```text
x₁
 ↓
x₂
 ↓
x₃
 ↓
x₄
```

আগের step-এর উপর পরের step depend করে।

তাই highly parallel processing কঠিন।

---

### 2. Vanishing Gradient

Long sequence-এ old information হারিয়ে যেতে পারে।

---

### 3. Exploding Gradient

Gradient অনেক বড় হতে পারে।

---

### 4. Long-Term Dependency

অনেক দূরের context মনে রাখা কঠিন।

---

### 5. Slow Training

Sequence sequential হওয়ায় training parallelization সীমিত।

---

# 29. RNN → LSTM কেন এলো?

RNN-এর limitation:

```text
Short-term memory
       ↓
Long-term information difficult
```

তাই এসেছে:

> **LSTM = Long Short-Term Memory**

LSTM special gates ব্যবহার করে information:

```text
Forget
Input
Output
```

নিয়ন্ত্রণ করে।

Evolution:

```text
RNN
 ↓
LSTM / GRU
 ↓
Attention
 ↓
Transformer
```

পরবর্তী lessons-এ LSTM গভীরভাবে আসবে।

---

# 30. RNN বনাম N-gram

| Feature           | N-gram       | RNN                 |
| ----------------- | ------------ | ------------------- |
| Context           | Fixed        | Hidden state        |
| Learning          | Counts       | Neural learning     |
| Representation    | Sparse/count | Dense vectors       |
| Long context      | Poor         | Better, but limited |
| Training          | Simple       | More complex        |
| Embeddings        | Not required | Usually used        |
| Sequential memory | No           | Yes                 |

---

# 31. RNN বনাম LSTM

| RNN                            | LSTM                 |
| ------------------------------ | -------------------- |
| Simple architecture            | More complex         |
| Basic hidden state             | Hidden + cell state  |
| Long-term dependency weak      | Better               |
| Vanishing gradient সমস্যা বেশি | কমানোর জন্য designed |
| Faster/simple                  | More computation     |

---

# 32. RNN বনাম Transformer

এটি future-এর জন্য খুব গুরুত্বপূর্ণ:

| RNN                                | Transformer                     |
| ---------------------------------- | ------------------------------- |
| Sequential processing              | Highly parallelizable           |
| Hidden-state memory                | Attention                       |
| Long context difficult             | Long-range relationships better |
| Older NLP architecture             | Modern NLP foundation           |
| Training slower for long sequences | Better hardware parallelism     |

---

# 33. AI Writing Assistant-এর সাথে RNN

তোমার future AI writing project-এর historical architecture হতে পারে:

```text
User Text
    ↓
Tokenizer
    ↓
Embedding
    ↓
RNN / LSTM
    ↓
Language Representation
    ↓
Prediction / Generation
```

Classification:

```text
Text
 ↓
Embedding
 ↓
RNN
 ↓
Classifier
 ↓
AI / Human / Other class
```

তবে modern high-quality text generation-এর জন্য RNN-এর চেয়ে **Transformer architecture** বেশি গুরুত্বপূর্ণ।

---

# 34. RNN দিয়ে Text Classification

Example:

```text
"This product is amazing"
```

Pipeline:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
RNN
 ↓
Dense
 ↓
Sigmoid
 ↓
Positive
```

---

# 35. Simple Complete Keras Example

```python
import tensorflow as tf

vocab_size = 10000
sequence_length = 100

model = tf.keras.Sequential([
    tf.keras.layers.Embedding(
        input_dim=vocab_size,
        output_dim=128,
        input_length=sequence_length
    ),

    tf.keras.layers.SimpleRNN(128),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])

model.compile(
    optimizer="adam",
    loss="binary_crossentropy",
    metrics=["accuracy"]
)

model.summary()
```

Architecture:

```text
Token IDs
   ↓
Embedding
   ↓
128-dimensional vectors
   ↓
SimpleRNN(128)
   ↓
Dense(1)
   ↓
Sigmoid
   ↓
Binary Prediction
```

---

# 36. Text Generation-এর Basic Concept

ধরো initial text:

```text
"The future of AI"
```

RNN predict:

```text
is
```

Sequence:

```text
"The future of AI is"
```

আবার predict:

```text
bright
```

তারপর:

```text
"The future of AI is bright"
```

এভাবে:

```text
Context
 ↓
RNN
 ↓
Next-token probabilities
 ↓
Select token
 ↓
Append token
 ↓
Repeat
```

---

# 37. Sampling

সবসময় highest probability token নেওয়া বাধ্যতামূলক নয়।

ধরো:

```text
learning → 0.40
Python   → 0.30
AI       → 0.20
NLP      → 0.10
```

Model বিভিন্ন strategy ব্যবহার করতে পারে।

পরবর্তীতে আমরা শিখব:

```text
Greedy Decoding
Temperature
Top-K
Top-P
Beam Search
```

এগুলো text generation-এর জন্য গুরুত্বপূর্ণ।

---

# 38. Complete NLP Evolution

এখন পর্যন্ত:

```text
Text
 ↓
Tokenization
 ↓
Stopwords
 ↓
Stemming
 ↓
Lemmatization
 ↓
POS
 ↓
NER
 ↓
Chunking
 ↓
Dependency Parsing
 ↓
Constituency Parsing
 ↓
Semantic Analysis
 ↓
Word Embeddings
 ↓
Language Modeling
 ↓
RNN  ← আজ
 ↓
LSTM
 ↓
GRU
 ↓
Attention
 ↓
Transformer
 ↓
LLM
```

এখানে আমরা খুব গুরুত্বপূর্ণ transition point-এ আছি।

---

# 39. আজকের Core Mental Model

এটা মুখস্থ করার চেয়ে **বোঝা** বেশি গুরুত্বপূর্ণ:

```text
                SEQUENCE
                    ↓
               Token IDs
                    ↓
                Embedding
                    ↓
             ┌────────────┐
Previous ───→│    RNN     │←── Current Input
State        └────────────┘
                    ↓
             Hidden State
                    ↓
                 Output
                    ↓
             Next Prediction
```

আর training:

```text
Input
 ↓
Embedding
 ↓
RNN
 ↓
Prediction
 ↓
Loss
 ↓
BPTT
 ↓
Weight Update
```

---

# 40. Practice Tasks

### Task 1

Explain:

```text
What is hidden state?
```

নিজের ভাষায় ৫–১০ লাইনে লিখো।

### Task 2

এই sequence-এর RNN flow আঁকো:

```text
I love machine learning
```

### Task 3

Explain:

```text
Many-to-One
Many-to-Many
Sequence-to-Sequence
```

### Task 4

এই সমস্যাগুলো explain করো:

```text
Vanishing Gradient
Exploding Gradient
Long-Term Dependency
```

### Task 5

Keras-এ এমন model বানাও:

```text
Embedding
 ↓
SimpleRNN
 ↓
Dense
 ↓
Sigmoid
```

### Task 6

`return_sequences=True` এবং `False`-এর difference explain করো।

---

# 41. Theory Questions

1. What is RNN?
2. Why is RNN useful for NLP?
3. What is a sequence?
4. What is hidden state?
5. What is recurrent connection?
6. What is parameter sharing?
7. What is RNN unrolling?
8. What is sequence-to-one?
9. What is sequence-to-sequence?
10. What is many-to-one?
11. What is many-to-many?
12. What is BPTT?
13. What is vanishing gradient?
14. What is exploding gradient?
15. What is long-term dependency?
16. Why does RNN use hidden state?
17. Why is Embedding used before RNN?
18. What does `return_sequences=True` do?
19. Why was LSTM introduced?
20. Why did Transformer eventually replace RNNs for many modern NLP applications?

---

# 42. Interview Questions

### Q1. What is RNN?

RNN is a neural network architecture designed for sequential data that maintains a hidden state to carry information from previous time steps.

### Q2. What is hidden state?

Hidden state is an internal representation that carries information from previous sequence steps to the current step.

### Q3. What is BPTT?

**Backpropagation Through Time** is the training approach used to propagate errors backward across the unfolded timesteps of an RNN.

### Q4. Why does vanilla RNN struggle with long sequences?

Primarily because repeated multiplication through time can cause gradients to vanish or explode, making long-term dependencies difficult to learn.

### Q5. Why was LSTM introduced?

LSTM was designed to better preserve and control information over long sequences using gated memory mechanisms.

---

# ✅ M02.17 Completion Checklist

* [x] RNN definition
* [x] Sequence data
* [x] Recurrent concept
* [x] Hidden state
* [x] RNN equations
* [x] Output
* [x] RNN unrolling
* [x] Parameter sharing
* [x] Sequence-to-One
* [x] One-to-Many
* [x] Many-to-One
* [x] Many-to-Many
* [x] Sequence-to-Sequence
* [x] RNN + Embedding
* [x] Keras SimpleRNN
* [x] `return_sequences`
* [x] Stacked RNN
* [x] RNN training
* [x] BPTT
* [x] Vanishing Gradient
* [x] Exploding Gradient
* [x] Gradient Clipping
* [x] Long-Term Dependency
* [x] RNN limitations
* [x] RNN vs N-gram
* [x] RNN vs LSTM
* [x] RNN vs Transformer
* [x] RNN for text classification
* [x] RNN for language modeling
* [x] Basic text generation
* [x] AI writing assistant connection

### 🔥 Final Evolution

```text
N-gram
  ↓
Neural Language Model
  ↓
RNN
  ↓
LSTM / GRU
  ↓
Attention
  ↓
Transformer
  ↓
Large Language Model
```

**M02.17 = RNN Foundation complete.**


---
# M02.18 — LSTM (Long Short-Term Memory) Deep Dive

M02.17-এ আমরা **RNN** শিখেছি। RNN-এর সবচেয়ে বড় সমস্যা ছিল **long-term dependency**, **vanishing gradient**, এবং long sequence-এর information ধরে রাখতে না পারা।

এই সমস্যাগুলো মোকাবিলা করার জন্য তৈরি করা হয়:

> **LSTM = Long Short-Term Memory**

NLP-এর evolution:

```text
N-gram
   ↓
Neural Language Model
   ↓
RNN
   ↓
LSTM  ← আজ
   ↓
GRU
   ↓
Attention
   ↓
Transformer
   ↓
LLM
```

---

# 1. কেন LSTM দরকার?

ধরো:

```text
The student who studied Python for many months
and practiced every day finally built an AI application.
```

শেষে:

```text
built
```

এর subject বুঝতে অনেক আগের:

```text
student
```

information দরকার।

Vanilla RNN দীর্ঘ sequence-এ আগের information হারিয়ে ফেলতে পারে।

```text
RNN

old information
      ↓
      ↓
      ↓
   gradually lost
```

LSTM এই information selectively ধরে রাখতে পারে।

---

# 2. LSTM কী?

LSTM হলো RNN-এর একটি advanced variant।

এর মূল বৈশিষ্ট্য:

```text
LSTM
 ├── Cell State
 ├── Hidden State
 ├── Forget Gate
 ├── Input Gate
 └── Output Gate
```

সবচেয়ে গুরুত্বপূর্ণ:

> **LSTM শেখে কোন information ভুলতে হবে, কোন information রাখতে হবে এবং কোন information output হিসেবে দিতে হবে।**

---

# 3. LSTM-এর Core Idea

একটি LSTM cell-এর মধ্যে দুটি state থাকে:

```text
Cell State
Hidden State
```

Conceptually:

```text
                 Cell State
──────────────────────────────────────→
       ↑             ↑             ↑
       │             │             │
      Gate          Gate          Gate

xₜ ─────────────→ LSTM Cell ───────→ hₜ
                  ↑
                 hₜ₋₁
```

এখানে:

* `xₜ` = current input
* `hₜ₋₁` = previous hidden state
* `hₜ` = current hidden state
* `Cₜ₋₁` = previous cell state
* `Cₜ` = current cell state

---

# 4. Cell State

LSTM-এর সবচেয়ে গুরুত্বপূর্ণ অংশ:

> **Cell State**

এটি long-term information carry করার জন্য ব্যবহৃত হয়।

```text
Cₜ₋₁
 ↓
LSTM
 ↓
Cₜ
```

একটি highway-এর মতো ভাবতে পারো:

```text
Previous information
────────────────────────→
           ↑
       gates control
```

Gate decide করে:

```text
keep?
forget?
update?
```

---

# 5. Hidden State বনাম Cell State

এটা খুব ভালোভাবে বুঝতে হবে।

### Cell State

```text
Long-term memory
```

### Hidden State

```text
Current/output representation
```

সহজ mental model:

```text
Cell State
→ কী information দীর্ঘসময় ধরে রাখব?

Hidden State
→ এই মুহূর্তে কী information output করব?
```

---

# 6. LSTM-এর তিনটি প্রধান Gate

LSTM-এর তিনটি gate:

```text
1. Forget Gate
2. Input Gate
3. Output Gate
```

এগুলো information flow নিয়ন্ত্রণ করে।

```text
Previous Memory
      ↓
Forget Gate
      ↓
Input Gate
      ↓
Updated Memory
      ↓
Output Gate
      ↓
Hidden State
```

---

# 7. Forget Gate

প্রথম প্রশ্ন:

> পুরনো information-এর কতটুকু রাখা হবে?

Forget gate:

$$
f_t = \sigma(W_f[h_{t-1},x_t]+b_f)
$$

Sigmoid output:

```text
0 → forget
1 → keep
```

উদাহরণ:

```text
0.00 → almost completely forget
0.25 → mostly forget
0.50 → partially keep
0.90 → mostly keep
1.00 → keep
```

---

# 8. Forget Gate Example

ধরো sentence:

```text
Rahim lives in Dhaka.
He is a programmer.
```

পরের sentence-এ নতুন subject information এলে LSTM সিদ্ধান্ত নিতে পারে পুরনো information-এর কোন অংশ গুরুত্বপূর্ণ।

Conceptually:

```text
Old memory
     ↓
Forget Gate
     ↓
Important information → keep
Unimportant information → remove
```

---

# 9. Input Gate

এখন LSTM-এর দ্বিতীয় প্রশ্ন:

> নতুন information-এর কোন অংশ memory-তে যোগ করব?

Input gate:

$$
i_t = \sigma(W_i[h_{t-1},x_t]+b_i)
$$

এটি decide করে নতুন information-এর কতটুকু গ্রহণ করা হবে।

---

# 10. Candidate Memory

Input gate-এর পাশাপাশি candidate memory তৈরি হয়:

$$
\tilde{C}_t =
\tanh(W_c[h_{t-1},x_t]+b_c)
$$

এটি নতুন সম্ভাব্য information তৈরি করে।

তারপর:

```text
Candidate information
        ↓
Input Gate
        ↓
Selected information
```

---

# 11. Cell State Update

পুরনো memory এবং নতুন information combine হয়:

$$
C_t = f_t \odot C_{t-1}
+
i_t \odot \tilde{C}_t
$$

এখানে:

* `fₜ` = forget gate
* `Cₜ₋₁` = old memory
* `iₜ` = input gate
* `Ĉₜ` = candidate memory
* `⊙` = element-wise multiplication

সহজভাবে:

```text
Old Memory
   ↓
Forget
   ↓
Keep useful old information
        +
New Information
   ↓
Input Gate
   ↓
Add useful new information
        ↓
Updated Cell State
```

---

# 12. Output Gate

এখন তৃতীয় প্রশ্ন:

> Updated memory থেকে কোন information output হিসেবে দেওয়া হবে?

Output gate:

$$
o_t = \sigma(W_o[h_{t-1},x_t]+b_o)
$$

তারপর hidden state:

$$
h_t = o_t \odot \tanh(C_t)
$$

অর্থাৎ:

```text
Cell State
    ↓
Output Gate
    ↓
Hidden State
```

---

# 13. Complete LSTM Equations

একসাথে:

### Forget Gate

$$
f_t = \sigma(W_f[h_{t-1},x_t]+b_f)
$$

### Input Gate

$$
i_t = \sigma(W_i[h_{t-1},x_t]+b_i)
$$

### Candidate State

$$
\tilde C_t =
\tanh(W_c[h_{t-1},x_t]+b_c)
$$

### Cell State

$$
C_t =
f_t\odot C_{t-1}
+
i_t\odot\tilde C_t
$$

### Output Gate

$$
o_t = \sigma(W_o[h_{t-1},x_t]+b_o)
$$

### Hidden State

$$
h_t =
o_t\odot\tanh(C_t)
$$

এগুলো এখনই পুরোপুরি মুখস্থ করার প্রয়োজন নেই। **flow বুঝতে হবে।**

---

# 14. Sigmoid কেন?

Sigmoid:

$$
\sigma(x)=\frac{1}{1+e^{-x}}
$$

Output:

```text
0 → 1
```

তাই gate হিসেবে খুব useful।

```text
0 → Don't allow
1 → Allow
```

অর্থাৎ:

```text
Sigmoid
   ↓
Gate value
   ↓
How much information?
```

---

# 15. Tanh কেন?

`tanh` output দেয়:

```text
-1 → +1
```

এটি candidate information এবং cell-state transformation-এ ব্যবহৃত হয়।

Mental model:

```text
Sigmoid
→ control

Tanh
→ information representation
```

---

# 16. LSTM Cell Visual Model

```text
                 Cell State
      ─────────────────────────────────→

             ↓ Forget Gate
             ↓
        Old Memory
             ↓
        ┌───────────┐
xₜ ───→ │   LSTM    │
hₜ₋₁ ─→ │   Cell    │
        └───────────┘
             ↑
             │
        Input Gate
             │
       New Information
             ↓
        Updated Memory
             ↓
        Output Gate
             ↓
            hₜ
```

---

# 17. RNN বনাম LSTM

| Feature            | RNN              | LSTM           |
| ------------------ | ---------------- | -------------- |
| Hidden State       | ✅                | ✅              |
| Cell State         | ❌                | ✅              |
| Forget Gate        | ❌                | ✅              |
| Input Gate         | ❌                | ✅              |
| Output Gate        | ❌                | ✅              |
| Long-term memory   | Weak             | Better         |
| Vanishing gradient | More problematic | Better handled |
| Architecture       | Simple           | Complex        |
| Computation        | Lower            | Higher         |

---

# 18. RNN-এর মূল সমস্যা কীভাবে LSTM কমায়?

Vanilla RNN:

```text
hₜ = tanh(Wxₜ + Uhₜ₋₁)
```

Repeated transformations-এর কারণে gradient vanish/explode করতে পারে।

LSTM-এর cell state এবং gates information/gradient flow-এর জন্য একটি more controlled path তৈরি করে।

```text
RNN
Previous State
      ↓
   repeated
transformations
      ↓
information may fade
```

LSTM:

```text
Previous Cell State
        ↓
  controlled memory
        ↓
      Gates
        ↓
Updated Cell State
```

---

# 19. LSTM + Embedding

M02.15-এর embedding এবং M02.17-এর RNN concept combine করলে:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
LSTM
 ↓
Output
```

Example:

```text
"I love machine learning"
```

Token IDs:

```text
[10, 25, 80, 100]
```

Embedding:

```text
10 → vector
25 → vector
80 → vector
100 → vector
```

তারপর:

```text
Vectors
   ↓
 LSTM
   ↓
Representation
   ↓
Prediction
```

---

# 20. Keras LSTM

Simple model:

```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Embedding(
        input_dim=10000,
        output_dim=128
    ),

    tf.keras.layers.LSTM(128),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])

model.summary()
```

Flow:

```text
Token IDs
   ↓
Embedding
   ↓
128-dimensional vectors
   ↓
LSTM(128)
   ↓
Dense
   ↓
Sigmoid
```

---

# 21. `return_sequences`

RNN-এর মতো LSTM-এও:

```python
return_sequences=True
```

ব্যবহার করা যায়।

### False

```python
tf.keras.layers.LSTM(128)
```

Output:

```text
(batch_size, 128)
```

শুধু final output।

### True

```python
tf.keras.layers.LSTM(
    128,
    return_sequences=True
)
```

Output:

```text
(batch_size, sequence_length, 128)
```

প্রতিটি timestep-এর output।

---

# 22. Stacked LSTM

দুইটি LSTM layer:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(10000, 128),

    tf.keras.layers.LSTM(
        128,
        return_sequences=True
    ),

    tf.keras.layers.LSTM(64),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])
```

Flow:

```text
Embedding
    ↓
LSTM 128
    ↓
LSTM 64
    ↓
Dense
    ↓
Prediction
```

প্রথম LSTM-তে:

```text
return_sequences=True
```

কারণ দ্বিতীয় LSTM পুরো sequence output পাবে।

---

# 23. Bidirectional LSTM

সাধারণ LSTM:

```text
Past → Current
```

Bidirectional LSTM:

```text
Past → Current
Current ← Future
```

অর্থাৎ sequence দুই direction-এ process করা হয়।

Keras:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(10000, 128),

    tf.keras.layers.Bidirectional(
        tf.keras.layers.LSTM(128)
    ),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])
```

---

# 24. কেন Bidirectional LSTM?

ধরো:

```text
The bank is near the river.
```

`bank`-এর meaning বুঝতে surrounding context দরকার।

Bidirectional model:

```text
left context
    →
  bank
    ←
right context
```

দুই direction-এর context ব্যবহার করতে পারে।

---

# 25. Important Warning

Bidirectional LSTM সব task-এর জন্য appropriate নয়।

যেমন **real-time next-token generation**-এ future token available থাকে না।

কারণ:

```text
Current token
↓
Future token এখনো জানা নেই
```

তাই autoregressive generation-এর ক্ষেত্রে causal direction গুরুত্বপূর্ণ।

কিন্তু:

* classification
* sequence labeling
* offline text analysis

এর মতো task-এ bidirectional architecture useful হতে পারে।

---

# 26. LSTM for Sentiment Analysis

Input:

```text
"The movie was absolutely fantastic"
```

Pipeline:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
LSTM
 ↓
Dense
 ↓
Sigmoid
 ↓
Positive
```

---

# 27. LSTM for Text Classification

Example classes:

```text
Spam
Not Spam
```

Model:

```text
Text
 ↓
Embedding
 ↓
LSTM
 ↓
Dense
 ↓
Prediction
```

Multiple classes হলে:

```python
tf.keras.layers.Dense(
    num_classes,
    activation="softmax"
)
```

---

# 28. LSTM for Language Modeling

Input:

```text
I love machine
```

Target:

```text
learning
```

Flow:

```text
I
 ↓
Embedding
 ↓
LSTM
 ↓
love
 ↓
LSTM
 ↓
machine
 ↓
LSTM
 ↓
Softmax
 ↓
Next-token probabilities
```

Output:

```text
learning → 0.60
Python   → 0.10
AI       → 0.08
...
```

---

# 29. Softmax

Language model-এ vocabulary-এর প্রতিটি token-এর probability দরকার।

ধরো vocabulary:

```text
["AI", "Python", "NLP", "learning"]
```

Output logits:

```text
[1.2, 0.5, 2.1, 0.8]
```

Softmax এগুলোকে probability distribution-এ convert করে:

```text
AI        → 0.20
Python    → 0.10
NLP       → 0.50
learning  → 0.20
```

সব probability-এর sum:

```text
1.0
```

---

# 30. LSTM Language Model Architecture

```text
                 Vocabulary
                     ↑
                     │
                  Softmax
                     ↑
                 Dense Layer
                     ↑
                    LSTM
                     ↑
                 Embedding
                     ↑
                 Token IDs
                     ↑
                    Text
```

---

# 31. LSTM Text Generation

Initial prompt:

```text
"I love"
```

Model predicts:

```text
machine
```

নতুন sequence:

```text
"I love machine"
```

আবার:

```text
learning
```

তারপর:

```text
"I love machine learning"
```

Flow:

```text
Prompt
 ↓
Tokenizer
 ↓
Embedding
 ↓
LSTM
 ↓
Next-token probability
 ↓
Select token
 ↓
Append
 ↓
Repeat
```

---

# 32. Teacher Forcing

Sequence model training-এর একটি গুরুত্বপূর্ণ concept:

> **Teacher Forcing**

ধরো target sequence:

```text
I love machine learning
```

Training-এর সময়:

```text
Input:
I

Target:
love
```

পরের step:

```text
Input:
I love

Target:
machine
```

পরের:

```text
Input:
I love machine

Target:
learning
```

অর্থাৎ training-এর সময় ground-truth previous tokens ব্যবহার করা হয়।

---

# 33. Teacher Forcing কেন?

Training দ্রুত ও stable করতে সাহায্য করে।

Without teacher forcing:

```text
Model prediction
      ↓
Next input
      ↓
Model prediction
      ↓
Error may accumulate
```

Teacher forcing:

```text
Correct previous token
      ↓
LSTM
      ↓
Next prediction
```

---

# 34. Exposure Bias

Teacher forcing-এর একটি সমস্যা:

Training:

```text
Correct previous token
```

Inference:

```text
Model's own previous prediction
```

এই difference-এর কারণে generation-এর সময় error accumulate করতে পারে।

এটি:

> **Exposure Bias**

নামটি মনে রাখবে; পরে sequence generation-এ আরও বিস্তারিত হবে।

---

# 35. LSTM-এর Advantages

### 1. Long-term dependencies

RNN-এর তুলনায় better।

### 2. Controlled memory

Gates information control করে।

### 3. Vanishing gradient সমস্যা কমায়

পুরোপুরি eliminate করে না, তবে traditional RNN-এর তুলনায় better।

### 4. NLP sequence tasks

ব্যবহার করা হয়েছে:

* sentiment analysis
* sequence classification
* language modeling
* speech processing
* machine translation
* sequence labeling

---

# 36. LSTM-এর Limitations

LSTM perfect নয়।

### 1. Complex

RNN-এর তুলনায় architecture বড়।

### 2. Computationally expensive

একাধিক gate-এর calculation লাগে।

### 3. Sequential processing

```text
x₁ → x₂ → x₃ → x₄
```

তাই parallelization সীমিত।

### 4. Long sequences

Long context-এর ক্ষেত্রে এখনও limitations থাকতে পারে।

### 5. Transformer-এর উত্থান

Attention/Transformer অনেক NLP task-এ LSTM-এর তুলনায় বেশি scalable এবং effective হয়েছে।

---

# 37. LSTM বনাম GRU

পরবর্তী lesson-এ GRU বিস্তারিত আসবে, কিন্তু basic difference:

| LSTM             | GRU                  |
| ---------------- | -------------------- |
| Cell state আছে   | আলাদা cell state নেই |
| 3 main gates     | 2 main gates         |
| More complex     | Simpler              |
| More parameters  | Fewer parameters     |
| More computation | Less computation     |

Mental model:

```text
LSTM
→ More control

GRU
→ Simpler control
```

---

# 38. RNN → LSTM → GRU

Evolution:

```text
RNN
 │
 ├── Problem:
 │   Vanishing Gradient
 │   Long-Term Dependency
 │
 ↓
LSTM
 │
 ├── Cell State
 ├── Forget Gate
 ├── Input Gate
 └── Output Gate
 │
 ↓
GRU
 │
 ├── Update Gate
 └── Reset Gate
```

---

# 39. LSTM বনাম Transformer

এটি তোমার future AI project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

| LSTM                     | Transformer                 |
| ------------------------ | --------------------------- |
| Recurrent                | Attention-based             |
| Sequential               | Highly parallelizable       |
| Hidden + Cell State      | Attention representations   |
| Long context difficult   | Better long-range modeling  |
| Older architecture       | Modern NLP standard         |
| Slower on long sequences | Better hardware utilization |

Evolution:

```text
RNN
 ↓
LSTM
 ↓
Attention
 ↓
Transformer
```

---

# 40. AI Writing Assistant-এর Connection

তোমার AI writing assistant-এ LSTM historical/learning architecture হিসেবে খুব গুরুত্বপূর্ণ।

Example:

```text
User Text
    ↓
Tokenizer
    ↓
Embedding
    ↓
LSTM
    ↓
Context Representation
    ↓
Prediction
```

Classification:

```text
Text
 ↓
Embedding
 ↓
LSTM
 ↓
Classifier
 ↓
Prediction
```

Generation:

```text
Prompt
 ↓
Embedding
 ↓
LSTM
 ↓
Next Token
 ↓
Next Token
 ↓
Next Token
```

তবে modern high-quality writing systems সাধারণত Transformer/LLM architecture-এর দিকে যায়।

---

# 41. M02 পর্যন্ত Evolution

আমাদের পুরো journey এখন:

```text
                    NLP
                     │
        ┌────────────┴────────────┐
        ↓                         ↓
 Linguistic Analysis         Representation
        │                         │
        ↓                         ↓
 POS / NER / Parsing         Embeddings
        │                         │
        └────────────┬────────────┘
                     ↓
              Language Model
                     ↓
                    RNN
                     ↓
                   LSTM  ← TODAY
                     ↓
                    GRU
                     ↓
                 Attention
                     ↓
                Transformer
                     ↓
                   LLM
```

---

# 42. Practical Keras Architecture

Text classification-এর জন্য:

```python
import tensorflow as tf

vocab_size = 10000
embedding_dim = 128
sequence_length = 100

model = tf.keras.Sequential([
    tf.keras.layers.Embedding(
        vocab_size,
        embedding_dim
    ),

    tf.keras.layers.LSTM(128),

    tf.keras.layers.Dense(
        64,
        activation="relu"
    ),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])

model.compile(
    optimizer="adam",
    loss="binary_crossentropy",
    metrics=["accuracy"]
)

model.summary()
```

Architecture:

```text
Token IDs
   ↓
Embedding
   ↓
LSTM
   ↓
Dense
   ↓
Sigmoid
   ↓
Binary Classification
```

---

# 43. গুরুত্বপূর্ণ Shape

Input:

```text
(batch_size, sequence_length)
```

Embedding:

```text
(batch_size, sequence_length, embedding_dim)
```

LSTM:

```text
(batch_size, units)
```

যদি:

```python
return_sequences=True
```

তাহলে:

```text
(batch_size, sequence_length, units)
```

Example:

```text
Input:
(32, 100)

Embedding:
(32, 100, 128)

LSTM(64):
(32, 64)

LSTM(64, return_sequences=True):
(32, 100, 64)
```

এগুলো ভবিষ্যতে model debugging-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 44. Practice Task

### Task 1

Explain:

```text
RNN কেন long-term dependency-তে struggle করে?
```

### Task 2

Explain:

```text
Cell State
Hidden State
```

দুটোর difference নিজের ভাষায় লিখো।

### Task 3

এই তিনটি gate explain করো:

```text
Forget Gate
Input Gate
Output Gate
```

### Task 4

এই flow explain করো:

```text
Text
 ↓
Tokenizer
 ↓
Embedding
 ↓
LSTM
 ↓
Dense
 ↓
Prediction
```

### Task 5

Keras-এ এই architecture তৈরি করো:

```text
Embedding
 ↓
LSTM(128)
 ↓
Dense(64)
 ↓
Dense(1)
```

### Task 6

`return_sequences=True` কখন ব্যবহার করতে হবে—একটি example দাও।

---

# 45. Theory Questions

1. What is LSTM?
2. Why was LSTM introduced?
3. What is long-term dependency?
4. What is cell state?
5. What is hidden state?
6. What is forget gate?
7. What is input gate?
8. What is output gate?
9. Why is sigmoid used in gates?
10. Why is tanh used in LSTM?
11. What is candidate cell state?
12. How is cell state updated?
13. What is BPTT?
14. How does LSTM reduce vanishing-gradient problems?
15. What is `return_sequences`?
16. What is Bidirectional LSTM?
17. When should Bidirectional LSTM be avoided?
18. What is teacher forcing?
19. What is exposure bias?
20. LSTM vs RNN?
21. LSTM vs GRU?
22. LSTM vs Transformer?

---

# 46. Interview Questions

### Q1. Why is LSTM better than vanilla RNN?

LSTM introduces gated memory and a separate cell state that allow it to control information flow and better preserve long-term dependencies.

### Q2. What are the three gates in LSTM?

```text
Forget Gate
Input Gate
Output Gate
```

### Q3. What is the difference between cell state and hidden state?

**Cell state** carries longer-term information through the sequence, while **hidden state** represents the information exposed by the LSTM at the current timestep.

### Q4. Why is `return_sequences=True` needed when stacking LSTM layers?

Because the next LSTM layer needs the output from **every timestep**, rather than only the final timestep.

### Q5. Is LSTM completely free from vanishing gradients?

No. LSTM significantly helps mitigate the problem compared with vanilla RNNs, but it does not mathematically eliminate all optimization difficulties.

---

# ✅ M02.18 Completion Checklist

* [x] LSTM definition
* [x] Why LSTM was introduced
* [x] Long-term dependency
* [x] Cell State
* [x] Hidden State
* [x] Forget Gate
* [x] Input Gate
* [x] Candidate Memory
* [x] Cell State Update
* [x] Output Gate
* [x] LSTM equations
* [x] Sigmoid
* [x] Tanh
* [x] LSTM architecture
* [x] LSTM + Embedding
* [x] Keras LSTM
* [x] `return_sequences`
* [x] Stacked LSTM
* [x] Bidirectional LSTM
* [x] LSTM for classification
* [x] LSTM for language modeling
* [x] LSTM text generation
* [x] Softmax
* [x] Teacher Forcing
* [x] Exposure Bias
* [x] LSTM advantages
* [x] LSTM limitations
* [x] RNN vs LSTM
* [x] LSTM vs GRU
* [x] LSTM vs Transformer
* [x] AI Writing Assistant connection

## 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ mental model

```text
                 INPUT
                   ↓
             ┌───────────┐
Previous ───→│   LSTM    │
Hidden       │           │
State        │  Forget   │
             │   Input   │
             │  Output   │
             │   Gates   │
             └─────┬─────┘
                   ↓
             Cell State
                   ↓
             Hidden State
                   ↓
                Output
```

আর পুরো evolution:

```text
N-gram
  ↓
RNN
  ↓
LSTM  ← M02.18
  ↓
GRU
  ↓
Attention
  ↓
Transformer
  ↓
LLM
```

**M02.18 = LSTM Foundation complete.**

---
# M02.19 — GRU (Gated Recurrent Unit) Deep Dive

M02.18-এ আমরা **LSTM (Long Short-Term Memory)** শিখেছি। LSTM RNN-এর long-term dependency সমস্যা কমানোর জন্য **cell state + multiple gates** ব্যবহার করে।

এরপরের গুরুত্বপূর্ণ architecture হলো:

> **GRU = Gated Recurrent Unit**

GRU হলো LSTM-এর একটি **simplified gated recurrent architecture**।

আমাদের sequence:

```text
N-gram
   ↓
RNN
   ↓
LSTM
   ↓
GRU  ← M02.19
   ↓
Attention
   ↓
Transformer
   ↓
LLM
```

---

# 1. GRU কী?

**GRU (Gated Recurrent Unit)** হলো RNN-এর একটি উন্নত variant যা gating mechanism ব্যবহার করে sequence-এর গুরুত্বপূর্ণ information ধরে রাখে।

মূল লক্ষ্য:

```text
RNN
 ↓
Long-term dependency problem
 ↓
GRU
 ↓
Better information flow
```

GRU-এর সবচেয়ে বড় বৈশিষ্ট্য:

* Cell state আলাদা নেই
* Hidden state-ই memory হিসেবে কাজ করে
* LSTM-এর তুলনায় কম gate
* তুলনামূলকভাবে simpler architecture
* সাধারণত fewer parameters

---

# 2. কেন GRU তৈরি করা হলো?

LSTM ভালো কাজ করে, কিন্তু architecture তুলনামূলক complex:

```text
LSTM
 ├── Cell State
 ├── Hidden State
 ├── Forget Gate
 ├── Input Gate
 └── Output Gate
```

GRU architecture আরও simple:

```text
GRU
 ├── Hidden State
 ├── Update Gate
 └── Reset Gate
```

তাই মূল ধারণা:

> **LSTM-এর মতো memory control, কিন্তু simpler architecture।**

---

# 3. LSTM বনাম GRU — প্রথম পার্থক্য

### LSTM

```text
        Cell State
            ↓
          Gates
            ↓
       Hidden State
```

### GRU

```text
        Hidden State
            ↓
          Gates
            ↓
       New Hidden State
```

GRU-তে আলাদা `Cell State` নেই।

---

# 4. GRU-এর দুইটি প্রধান Gate

GRU-তে মূলত দুইটি gate থাকে:

```text
1. Update Gate
2. Reset Gate
```

---

# 5. Update Gate

Update gate decide করে:

> পুরনো information-এর কতটুকু রাখা হবে এবং নতুন information-এর কতটুকু গ্রহণ করা হবে?

Formula:

$$
z_t = \sigma(W_z[x_t,h_{t-1}] + b_z)
$$

এখানে:

* `zₜ` = update gate
* `xₜ` = current input
* `hₜ₋₁` = previous hidden state
* `σ` = sigmoid

Output:

```text
0 → কম update
1 → বেশি update
```

---

# 6. Update Gate-এর Intuition

ধরো:

```text
Previous information
        +
Current information
```

GRU decide করবে:

```text
পুরনো information রাখব?
নতুন information নেব?
```

Concept:

```text
Previous Hidden State
        ↓
   Update Gate
        ↓
How much old information?
        +
Current Input
        ↓
How much new information?
```

---

# 7. Reset Gate

Reset gate decide করে:

> নতুন candidate information তৈরি করার সময় previous information-এর কতটুকু ব্যবহার করব?

Formula:

$$
r_t = \sigma(W_r[x_t,h_{t-1}] + b_r)
$$

এখানে:

* `rₜ` = reset gate
* `xₜ` = current input
* `hₜ₋₁` = previous hidden state

---

# 8. Reset Gate-এর Intuition

যদি previous context খুব relevant না হয়:

```text
Reset Gate
     ↓
Forget more previous information
```

যদি relevant হয়:

```text
Reset Gate
     ↓
Keep more previous information
```

---

# 9. Candidate Hidden State

GRU নতুন candidate state তৈরি করে:

$$
\tilde{h}_t =
\tanh(W_h[x_t,r_t\odot h_{t-1}] + b_h)
$$

এখানে:

```text
Current Input
      +
Reset-filtered Previous State
      ↓
Candidate Hidden State
```

---

# 10. Final Hidden State

শেষে update gate ব্যবহার করে পুরনো এবং নতুন information combine করা হয়।

একটি প্রচলিত formulation:

$$
h_t =
(1-z_t)\odot h_{t-1}
+
z_t\odot\tilde h_t
$$

এখানে:

* `hₜ₋₁` = old hidden state
* `zₜ` = update gate
* `h̃ₜ` = candidate state
* `hₜ` = new hidden state

**নোট:** বিভিন্ন implementation/paper-এ gate convention উল্টোভাবে সংজ্ঞায়িত হতে পারে। তাই equation দেখে gate-এর semantic interpretation মিলিয়ে নিতে হবে।

---

# 11. Complete GRU Flow

```text
                    Current Input
                         ↓
                       xₜ
                         │
             ┌───────────┴───────────┐
             │                       │
             ↓                       ↓
       Update Gate              Reset Gate
             │                       │
             │                       ↓
             │              Previous Hidden
             │                    State
             │                       ↓
             │              Candidate State
             │                       │
             └──────────┬────────────┘
                        ↓
                New Hidden State
                        ↓
                       hₜ
```

---

# 12. GRU Mathematical Summary

### Update Gate

$$
z_t = \sigma(W_z[x_t,h_{t-1}] + b_z)
$$

### Reset Gate

$$
r_t = \sigma(W_r[x_t,h_{t-1}] + b_r)
$$

### Candidate State

$$
\tilde h_t =
\tanh(W_h[x_t,r_t\odot h_{t-1}] + b_h)
$$

### Final Hidden State

$$
h_t =
(1-z_t)\odot h_{t-1}
+
z_t\odot\tilde h_t
$$

এই চারটি equation GRU-এর mathematical foundation।

---

# 13. LSTM-এর তিন Gate বনাম GRU-এর দুই Gate

### LSTM

```text
Forget Gate
Input Gate
Output Gate
```

### GRU

```text
Update Gate
Reset Gate
```

তাই:

```text
LSTM → more components
GRU  → fewer components
```

---

# 14. GRU-তে Cell State কেন নেই?

LSTM-এ:

```text
Cell State
+
Hidden State
```

GRU-তে:

```text
Hidden State
```

একটাই state information carry করে।

এটি architecture-কে simpler করে।

```text
LSTM:

Cₜ → Memory
hₜ → Output

GRU:

hₜ → Memory + Output representation
```

---

# 15. GRU + Embedding

M02.15-এর Embedding concept-এর সাথে GRU combine করলে:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
GRU
 ↓
Output
```

Example:

```text
"I love machine learning"
```

Token IDs:

```text
[10, 25, 80, 100]
```

Embedding:

```text
10 → vector
25 → vector
80 → vector
100 → vector
```

তারপর:

```text
Embedding vectors
       ↓
      GRU
       ↓
Hidden representation
       ↓
Prediction
```

---

# 16. Keras GRU

TensorFlow/Keras-এ:

```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Embedding(
        input_dim=10000,
        output_dim=128
    ),

    tf.keras.layers.GRU(128),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])

model.summary()
```

Architecture:

```text
Token IDs
   ↓
Embedding
   ↓
GRU(128)
   ↓
Dense(1)
   ↓
Sigmoid
```

---

# 17. GRU Text Classification

ধরো:

```text
"This movie was excellent"
```

Task:

```text
Positive / Negative
```

Pipeline:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
GRU
 ↓
Dense
 ↓
Sigmoid
 ↓
Positive
```

Keras:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(10000, 128),

    tf.keras.layers.GRU(128),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])
```

---

# 18. Multi-Class Classification

ধরো:

```text
Sports
Technology
Politics
Business
```

তাহলে:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(10000, 128),

    tf.keras.layers.GRU(128),

    tf.keras.layers.Dense(
        64,
        activation="relu"
    ),

    tf.keras.layers.Dense(
        4,
        activation="softmax"
    )
])
```

Flow:

```text
Text
 ↓
Embedding
 ↓
GRU
 ↓
Dense
 ↓
Softmax
 ↓
4 Classes
```

---

# 19. `return_sequences`

LSTM-এর মতো GRU-তেও:

```python
return_sequences=True
```

ব্যবহার করা যায়।

### Default

```python
tf.keras.layers.GRU(128)
```

Output:

```text
(batch_size, 128)
```

### Sequence output

```python
tf.keras.layers.GRU(
    128,
    return_sequences=True
)
```

Output:

```text
(batch_size, sequence_length, 128)
```

---

# 20. Stacked GRU

একাধিক GRU layer:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(10000, 128),

    tf.keras.layers.GRU(
        128,
        return_sequences=True
    ),

    tf.keras.layers.GRU(64),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])
```

Flow:

```text
Embedding
    ↓
GRU 128
    ↓
GRU 64
    ↓
Dense
    ↓
Prediction
```

প্রথম GRU-তে:

```text
return_sequences=True
```

কারণ দ্বিতীয় GRU পুরো sequence পাবে।

---

# 21. Bidirectional GRU

GRU-কে bidirectional করা যায়:

```python
model = tf.keras.Sequential([
    tf.keras.layers.Embedding(10000, 128),

    tf.keras.layers.Bidirectional(
        tf.keras.layers.GRU(128)
    ),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])
```

Flow:

```text
             Sequence
                ↓
       ┌────────┴────────┐
       ↓                 ↓
Forward GRU       Backward GRU
       ↓                 ↓
       └────────┬────────┘
                ↓
          Combined Output
                ↓
              Dense
```

এটি offline text analysis/classification-এ useful হতে পারে।

---

# 22. GRU for Language Modeling

Language modeling:

```text
Input:
"I love machine"

Target:
"learning"
```

Architecture:

```text
Token IDs
    ↓
Embedding
    ↓
GRU
    ↓
Dense
    ↓
Softmax
    ↓
Vocabulary probabilities
```

Output:

```text
learning → 0.61
Python   → 0.11
NLP      → 0.08
AI       → 0.05
...
```

---

# 23. GRU Text Generation

Prompt:

```text
"I love"
```

GRU:

```text
"I love"
    ↓
GRU
    ↓
machine
```

তারপর:

```text
"I love machine"
    ↓
GRU
    ↓
learning
```

তারপর:

```text
"I love machine learning"
```

Flow:

```text
Prompt
 ↓
Tokenizer
 ↓
Embedding
 ↓
GRU
 ↓
Next-token probabilities
 ↓
Select token
 ↓
Append token
 ↓
Repeat
```

---

# 24. GRU vs RNN

| Feature              | RNN              | GRU            |
| -------------------- | ---------------- | -------------- |
| Hidden State         | ✅                | ✅              |
| Gating               | ❌                | ✅              |
| Reset Gate           | ❌                | ✅              |
| Update Gate          | ❌                | ✅              |
| Long-term dependency | Weak             | Better         |
| Architecture         | Simple           | Moderate       |
| Vanishing gradient   | More problematic | Better handled |

---

# 25. GRU vs LSTM

সবচেয়ে গুরুত্বপূর্ণ comparison:

| Feature          | LSTM                   | GRU          |
| ---------------- | ---------------------- | ------------ |
| Cell State       | ✅                      | ❌            |
| Hidden State     | ✅                      | ✅            |
| Forget Gate      | ✅                      | ❌            |
| Input Gate       | ✅                      | ❌            |
| Output Gate      | ✅                      | ❌            |
| Update Gate      | ❌                      | ✅            |
| Reset Gate       | ❌                      | ✅            |
| Parameters       | More                   | Fewer        |
| Architecture     | More complex           | Simpler      |
| Computation      | More                   | Usually less |
| Memory mechanism | Separate cell + hidden | Hidden state |

---

# 26. কোনটি ভালো — LSTM না GRU?

একটি universal answer নেই।

কিছু ক্ষেত্রে:

```text
GRU
→ simpler
→ fewer parameters
→ faster training/inference হতে পারে
```

অন্যদিকে:

```text
LSTM
→ more explicit memory control
→ কিছু task-এ ভালো performance দিতে পারে
```

Best approach:

> **Dataset + task + compute budget অনুযায়ী experiment করা।**

---

# 27. GRU বনাম Transformer

এটি future AI project-এর জন্য খুব গুরুত্বপূর্ণ।

### GRU

```text
Sequential
 ↓
Hidden State
 ↓
Next Step
```

### Transformer

```text
All Tokens
 ↓
Self-Attention
 ↓
Contextual Representation
```

Comparison:

| GRU                            | Transformer                     |
| ------------------------------ | ------------------------------- |
| Recurrent                      | Attention-based                 |
| Sequential processing          | Highly parallelizable           |
| Hidden state                   | Attention representations       |
| Long-range context সীমিত       | Long-range relationships better |
| Older architecture             | Modern NLP foundation           |
| Smaller/simple models-এ useful | Large-scale NLP-তে dominant     |

---

# 28. Why Transformer Became Important?

GRU/LSTM sequence sequentially process করে:

```text
x₁
 ↓
x₂
 ↓
x₃
 ↓
x₄
```

Transformer attention-এর মাধ্যমে sequence-এর tokenগুলোর মধ্যে direct relationships model করতে পারে।

Conceptually:

```text
Token 1 ─────┐
Token 2 ─────┼──→ Attention
Token 3 ─────┤
Token 4 ─────┘
```

ফলে:

```text
Parallel processing
+
Long-range dependency modeling
```

অনেক বড় NLP model-এর জন্য সুবিধাজনক হয়েছে।

---

# 29. GRU-এর Advantages

### 1. Simple architecture

LSTM-এর তুলনায় fewer components।

### 2. Fewer parameters

অনেক configuration-এ LSTM-এর চেয়ে parameter কম।

### 3. Faster

কিছু task/hardware setup-এ training/inference দ্রুত হতে পারে।

### 4. Better than vanilla RNN

Gating mechanism থাকার কারণে long-term information handling উন্নত।

### 5. Useful for sequence data

ব্যবহার করা যায়:

* Text classification
* Sentiment analysis
* Sequence labeling
* Language modeling
* Time-series data
* Speech-related sequence tasks

---

# 30. GRU-এর Limitations

### 1. Sequential computation

```text
x₁ → x₂ → x₃ → x₄
```

### 2. Very long context

Transformer-এর মতো flexible global context modeling নেই।

### 3. Large-scale NLP

Modern large language model-এর ক্ষেত্রে Transformer বেশি suitable।

### 4. Still recurrent

Long sequence processing-এর জন্য recurrence-এর limitations থাকে।

---

# 31. GRU Training

Training flow:

```text
Input Sequence
      ↓
Embedding
      ↓
GRU
      ↓
Prediction
      ↓
Loss
      ↓
Backpropagation Through Time
      ↓
Weight Update
```

অর্থাৎ M02.17-এর RNN-এর মতো GRU-ও BPTT ব্যবহার করে train করা যায়।

---

# 32. Vanishing Gradient-এর সাথে GRU

Vanilla RNN:

```text
Long Sequence
     ↓
Repeated transformations
     ↓
Gradient may shrink
     ↓
Old information difficult to learn
```

GRU:

```text
Long Sequence
     ↓
Gates
     ↓
Controlled information flow
     ↓
Better gradient/information propagation
```

তবে মনে রাখবে:

> GRU **vanishing gradient পুরোপুরি eliminate করে না**।

এটি সমস্যা **mitigate** করে।

---

# 33. GRU-এর Internal Mental Model

সব mathematical formula একসাথে না ভেবে এভাবে মনে রাখো:

```text
Current Input
      +
Previous Hidden State
      ↓
 ┌───────────────┐
 │      GRU      │
 │               │
 │ Update Gate   │
 │ Reset Gate    │
 │               │
 └───────┬───────┘
         ↓
 New Hidden State
```

আর:

```text
Update Gate
→ How much new information?

Reset Gate
→ How much previous information for candidate?
```

---

# 34. LSTM Mental Model বনাম GRU Mental Model

### LSTM

```text
Old Memory
    ↓
Forget Gate
    ↓
Input Gate
    ↓
New Cell State
    ↓
Output Gate
    ↓
Hidden State
```

### GRU

```text
Previous Hidden State
        ↓
 ┌───────────────┐
 │ Update Gate   │
 │ Reset Gate    │
 └───────┬───────┘
         ↓
 New Hidden State
```

---

# 35. AI Writing Assistant-এর সাথে Connection

তোমার future AI writing project-এর architecture evolution:

```text
User Text
    ↓
Tokenizer
    ↓
Embedding
    ↓
RNN
    ↓
LSTM / GRU
    ↓
Context Representation
    ↓
Prediction
```

যেমন text classification:

```text
Text
 ↓
Embedding
 ↓
GRU
 ↓
Classifier
 ↓
Writing Quality Category
```

বা historical text-generation architecture:

```text
Prompt
 ↓
Embedding
 ↓
GRU
 ↓
Next Token
 ↓
Next Token
 ↓
Next Token
```

কিন্তু modern AI writing/humanization system-এর জন্য আমরা পরে:

```text
GRU
 ↓
Attention
 ↓
Transformer
 ↓
LLM
```

দিকে যাব।

---

# 36. Practical Example — Sentiment Model

```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Embedding(
        input_dim=10000,
        output_dim=128
    ),

    tf.keras.layers.GRU(128),

    tf.keras.layers.Dense(
        64,
        activation="relu"
    ),

    tf.keras.layers.Dense(
        1,
        activation="sigmoid"
    )
])

model.compile(
    optimizer="adam",
    loss="binary_crossentropy",
    metrics=["accuracy"]
)

model.summary()
```

Complete flow:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
GRU(128)
 ↓
Dense(64)
 ↓
Sigmoid
 ↓
Positive / Negative
```

---

# 37. Important Tensor Shapes

ধরো:

```text
batch_size = 32
sequence_length = 100
embedding_dim = 128
gru_units = 64
```

Input:

```text
(32, 100)
```

Embedding:

```text
(32, 100, 128)
```

GRU:

```python
GRU(64)
```

Output:

```text
(32, 64)
```

আর:

```python
GRU(
    64,
    return_sequences=True
)
```

Output:

```text
(32, 100, 64)
```

এগুলো model debugging-এর সময় খুব গুরুত্বপূর্ণ।

---

# 38. Practice Task

### Task 1

নিজের ভাষায় explain করো:

> GRU কেন তৈরি করা হয়েছিল?

---

### Task 2

এই দুইটি gate explain করো:

```text
Update Gate
Reset Gate
```

---

### Task 3

LSTM ও GRU-এর architecture আঁকো।

---

### Task 4

এই architecture explain করো:

```text
Embedding
 ↓
GRU
 ↓
Dense
 ↓
Sigmoid
```

---

### Task 5

এই shapeগুলো explain করো:

```text
Input:
(32, 100)

Embedding:
(32, 100, 128)

GRU(64):
(32, 64)

GRU(64, return_sequences=True):
(32, 100, 64)
```

---

### Task 6

Keras-এ তৈরি করো:

```text
Embedding(10000, 128)
        ↓
GRU(128)
        ↓
Dense(64)
        ↓
Dense(1)
```

---

# 39. Theory Questions

1. What is GRU?
2. Why was GRU introduced?
3. What is an Update Gate?
4. What is a Reset Gate?
5. Why does GRU not have a separate Cell State?
6. What is Hidden State in GRU?
7. How is candidate hidden state calculated?
8. How is final hidden state calculated?
9. Why is sigmoid used in GRU gates?
10. Why is tanh used for candidate state?
11. GRU কীভাবে long-term dependency handle করে?
12. GRU কীভাবে vanishing gradient problem mitigate করে?
13. What is `return_sequences`?
14. What is Bidirectional GRU?
15. GRU vs RNN?
16. GRU vs LSTM?
17. GRU vs Transformer?
18. What are the advantages of GRU?
19. What are the limitations of GRU?
20. Can GRU completely solve vanishing gradient?

---

# 40. Interview Questions

### Q1. What is GRU?

GRU is a gated recurrent neural network architecture designed to better model sequential dependencies using update and reset gates.

### Q2. What are the gates in GRU?

```text
Update Gate
Reset Gate
```

### Q3. Does GRU have a separate cell state?

No. GRU uses a single hidden state that serves as its recurrent memory representation.

### Q4. GRU vs LSTM?

LSTM has separate cell and hidden states and three major gates, while GRU uses a single hidden state and two main gates, making GRU simpler and typically parameter-efficient.

### Q5. Is GRU always faster than LSTM?

Not necessarily in every environment. GRU often has fewer parameters and can be computationally cheaper, but actual speed depends on implementation, hardware, sequence length, and configuration.

### Q6. Why are Transformers preferred for modern large-scale NLP?

Transformers use attention and allow much more parallel computation across sequence positions, while recurrent architectures process sequence steps sequentially.

---

# 41. RNN → LSTM → GRU → Transformer

এখন evolution খুব ভালোভাবে বুঝে রাখো:

```text
                    RNN
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
       LSTM                   GRU
          │                     │
          └──────────┬──────────┘
                     ↓
                 Attention
                     ↓
                Transformer
                     ↓
                    LLM
```

আর সমস্যার evolution:

```text
RNN
 ↓
Vanishing Gradient
 ↓
Long-Term Dependency
 ↓
LSTM / GRU
 ↓
Better sequence memory
 ↓
Attention
 ↓
Global context
 ↓
Transformer
```

---

# 42. M02 NLP Foundation Progress

এখন পর্যন্ত আমাদের foundation:

```text
M02.01  NLP Introduction
M02.02  Text & Language Fundamentals
M02.03  NLP Pipeline
M02.04  Text Preprocessing
M02.05  [Completed]
M02.06  Stopwords
M02.07  Stemming
M02.08  Lemmatization
M02.09  POS Tagging
M02.10  NER
M02.11  Chunking
M02.12  Dependency Parsing
M02.13  Constituency Parsing
M02.14  Semantic Analysis
M02.15  Word Embeddings
M02.16  Language Modeling
M02.17  RNN
M02.18  LSTM
M02.19  GRU  ← TODAY
```

পরবর্তী evolution:

```text
M02.20
   ↓
Attention
   ↓
Self-Attention
   ↓
Transformer
```

---

# ✅ M02.19 Completion Checklist

* [x] GRU definition
* [x] Why GRU was introduced
* [x] GRU architecture
* [x] Hidden State
* [x] Update Gate
* [x] Reset Gate
* [x] Candidate Hidden State
* [x] Final Hidden State
* [x] GRU equations
* [x] Sigmoid
* [x] Tanh
* [x] GRU + Embedding
* [x] Keras GRU
* [x] `return_sequences`
* [x] Stacked GRU
* [x] Bidirectional GRU
* [x] GRU for classification
* [x] GRU for language modeling
* [x] GRU text generation
* [x] BPTT
* [x] Vanishing Gradient
* [x] GRU advantages
* [x] GRU limitations
* [x] RNN vs GRU
* [x] LSTM vs GRU
* [x] GRU vs Transformer
* [x] AI Writing Assistant connection

## 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ mental model

```text
                 CURRENT INPUT
                      ↓
                     xₜ
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
    UPDATE GATE              RESET GATE
          │                       │
          │               Previous Hidden
          │                    State
          │                       ↓
          │              Candidate State
          │                       │
          └──────────┬────────────┘
                     ↓
             NEW HIDDEN STATE
                     ↓
                    hₜ
```

**M02.19 = GRU Foundation complete.**

---
# M02.20 — Attention Mechanism Deep Dive

M02.19-এ আমরা **GRU** পর্যন্ত এসেছি। এখন NLP-এর সবচেয়ে গুরুত্বপূর্ণ turning point-এর একটিতে যাব:

> **Attention Mechanism**

এটি বুঝতে পারলে পরের **Self-Attention → Transformer → BERT/GPT → LLM** অনেক সহজ হয়ে যাবে।

আমাদের evolution:

```text id="n8k4pf"
RNN
 ↓
LSTM
 ↓
GRU
 ↓
Attention       ← M02.20
 ↓
Self-Attention
 ↓
Transformer
 ↓
BERT / GPT
 ↓
LLM
```

---

# 1. Attention কী?

সহজ ভাষায়:

> **Attention হলো input-এর কোন অংশ বর্তমানে বেশি গুরুত্বপূর্ণ, সেটার উপর বেশি focus করার mechanism।**

ধরো:

```text id="w6k9qp"
The student went to the bank to deposit money.
```

এখানে `bank` শব্দের অর্থ বুঝতে:

```text id="t7c2ps"
deposit
money
```

এই context বেশি গুরুত্বপূর্ণ।

Attention এই ধরনের relevant information-কে বেশি weight দিতে পারে।

---

# 2. RNN-এর সমস্যা

ধরো:

```text id="g0j5px"
The student who studied Python for several years
and worked on many projects finally became a
professional machine learning engineer.
```

শেষে:

```text id="4f6x3w"
engineer
```

বোঝার জন্য অনেক আগের information দরকার।

RNN:

```text id="0t2x1p"
x₁ → x₂ → x₃ → x₄ → ... → xₙ
                     ↓
                  hₙ
```

সব information final hidden state-এর মধ্যে compress করার চেষ্টা হয়।

এটি long sequence-এ difficult হতে পারে।

---

# 3. LSTM/GRU কী সমস্যা solve করেছিল?

LSTM:

```text id="g7d8f3"
Memory
+
Gates
```

GRU:

```text id="f1d9k2"
Hidden State
+
Gates
```

এগুলো RNN-এর তুলনায় long-term dependency handle করতে পারে।

কিন্তু sequence খুব বড় হলে এখনও সমস্যা থাকতে পারে।

---

# 4. Attention-এর মূল ধারণা

Attention বলছে:

> "শুধু একটা final hidden state-এর উপর নির্ভর করব না। প্রয়োজন অনুযায়ী পুরো input sequence থেকে relevant information খুঁজে নেব।"

আগের ধারণা:

```text id="qj7v1p"
Input Sequence
      ↓
     RNN
      ↓
Final Hidden State
      ↓
   Output
```

Attention:

```text id="q7z2as"
Input Sequence
      ↓
RNN Encoder
      ↓
All Hidden States
      ↓
Attention
      ↓
Relevant Context
      ↓
Output
```

---

# 5. Attention কেন দরকার?

Machine Translation-এর example:

```text id="2k9y9a"
English:
I love machine learning.

French:
J'aime l'apprentissage automatique.
```

Decoder যখন `apprentissage` generate করবে, তখন source sentence-এর কোন শব্দগুলো গুরুত্বপূর্ণ?

```text id="7w4e2d"
machine
learning
```

Attention এই relevant encoder states-এ বেশি focus করতে পারে।

---

# 6. Encoder-Decoder Architecture

Traditional sequence-to-sequence architecture:

```text id="gk7s5f"
Input
 ↓
Encoder
 ↓
Hidden Representations
 ↓
Attention
 ↓
Decoder
 ↓
Output
```

আরও বিস্তারিত:

```text id="2v8d3p"
Source Sentence
      ↓
   Encoder
      ↓
h₁ h₂ h₃ h₄ h₅
 \  |  |  |  /
    Attention
       ↓
 Context Vector
       ↓
    Decoder
       ↓
Target Sentence
```

---

# 7. Attention-এর Basic Idea

ধরো encoder hidden states:

```text id="x5m8p3"
h₁
h₂
h₃
h₄
```

Decoder-এর current state:

```text id="j7d9q2"
sₜ
```

Attention হিসাব করবে:

```text id="a5q8vz"
How relevant is:

h₁ to sₜ?
h₂ to sₜ?
h₃ to sₜ?
h₄ to sₜ?
```

তারপর:

```text id="m8k3qa"
h₁ → 0.10
h₂ → 0.15
h₃ → 0.65
h₄ → 0.10
```

এখানে:

```text id="f4c9s1"
h₃
```

সবচেয়ে important।

---

# 8. Attention Score

প্রথমে প্রতিটি input representation-এর relevance score বের করা হয়।

Conceptually:

```text id="4g6m2p"
Query
  ↓
Compare with
  ↓
Keys
  ↓
Attention Scores
```

Traditional encoder-decoder attention-এ score function বিভিন্নভাবে হতে পারে।

যেমন:

### Dot Product

$$
score(s_t,h_i)=s_t^T h_i
$$

### General

$$
score(s_t,h_i)=s_t^T W h_i
$$

### Additive / Bahdanau Attention

$$
score(s_t,h_i)
=
v^T\tanh(W_s s_t+W_h h_i)
$$

এখন formula মুখস্থ করার চেয়ে concept গুরুত্বপূর্ণ।

---

# 9. Attention Weights

Score পাওয়ার পর সাধারণত **softmax** ব্যবহার করে weights বানানো হয়।

ধরো scores:

```text id="8y6h1a"
[1.2, 2.8, 0.5, 1.0]
```

Softmax:

```text id="h5z0kq"
[0.12, 0.62, 0.08, 0.18]
```

সবগুলোর যোগফল:

```text id="j8q2m4"
1.0
```

এগুলো হলো attention weights।

---

# 10. Context Vector

এখন hidden states-কে attention weights দিয়ে weighted sum করা হয়:

$$
c_t = \sum_i \alpha_{t,i}h_i
$$

এখানে:

* `cₜ` = context vector
* `αₜᵢ` = attention weight
* `hᵢ` = encoder hidden state

Concept:

```text id="p3s7d1"
h₁ × 0.12
+
h₂ × 0.62
+
h₃ × 0.08
+
h₄ × 0.18
       ↓
Context Vector
```

---

# 11. Complete Attention Flow

```text id="r1v8z5"
Input Tokens
     ↓
   Encoder
     ↓
h₁ h₂ h₃ h₄
 \  |  |  /
  Attention Scores
       ↓
    Softmax
       ↓
Attention Weights
       ↓
Weighted Sum
       ↓
Context Vector
       ↓
   Decoder
       ↓
    Output
```

---

# 12. Query, Key, Value

Modern attention বুঝতে সবচেয়ে গুরুত্বপূর্ণ তিনটি concept:

```text id="qkv8e2"
Query
Key
Value
```

এগুলো পরে Transformer-এর core হয়ে যাবে।

সহজ analogy:

> তুমি library-তে কোনো information খুঁজছো।

```text
Query
→ আমি কী খুঁজছি?

Key
→ কোন information কোন category-র?

Value
→ আসল information কী?
```

---

# 13. Query

Query হলো:

> **বর্তমানে কী information প্রয়োজন?**

ধরো current token:

```text id="7p5c1n"
bank
```

তার context বুঝতে model relevant information খুঁজছে।

Current representation থেকে query তৈরি হতে পারে।

$$
Q=XW_Q
$$

---

# 14. Key

Key হলো:

> **কোন information-এর সাথে query match করছে?**

$$
K=XW_K
$$

প্রতিটি token-এর একটি key representation থাকে।

---

# 15. Value

Value হলো:

> **যে actual information আমরা aggregate করতে চাই।**

$$
V=XW_V
$$

অর্থাৎ:

```text id="g2m5r9"
Query
 ↓
What am I looking for?

Key
 ↓
Which tokens are relevant?

Value
 ↓
What information should I retrieve?
```

---

# 16. Attention-এর সবচেয়ে গুরুত্বপূর্ণ Formula

Scaled Dot-Product Attention:

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

এটি পরে Transformer-এর সবচেয়ে গুরুত্বপূর্ণ equationগুলোর একটি হবে।

Flow:

```text id="h8f3k2"
Q × Kᵀ
   ↓
Similarity Scores
   ↓
÷ √dₖ
   ↓
Softmax
   ↓
Attention Weights
   ↓
× V
   ↓
Output
```

---

# 17. `QKᵀ` কেন?

Query এবং Key-এর similarity measure করার জন্য।

ধরো:

```text id="p0q5d7"
Q = current token representation

K₁ = token 1 representation
K₂ = token 2 representation
K₃ = token 3 representation
```

তাহলে:

```text id="4z6n1c"
Q·K₁ → score
Q·K₂ → score
Q·K₃ → score
```

যে token বেশি relevant:

```text id="y2c8q4"
Higher score
```

---

# 18. `√dₖ` দিয়ে ভাগ কেন?

Dot product-এর magnitude খুব বড় হয়ে গেলে softmax অত্যন্ত sharp হতে পারে।

তাই:

$$
\frac{QK^T}{\sqrt{d_k}}
$$

দিয়ে scale করা হয়।

এতে training আরও stable হতে সাহায্য করে।

---

# 19. Softmax আবার কেন?

Softmax scores-কে normalized weights-এ convert করে।

Example:

```text id="v8s4j2"
Scores:
[2.0, 5.0, 1.0]
```

Softmax:

```text id="m4c1z8"
[0.05, 0.94, 0.02]
```

অর্থাৎ model দ্বিতীয় token-এ সবচেয়ে বেশি attention দিচ্ছে।

---

# 20. Attention-এর ছোট Numerical Example

ধরো:

```text id="7x3p9m"
Q = [1, 0]
```

Keys:

```text id="q8n2s4"
K₁ = [1, 0]
K₂ = [0, 1]
K₃ = [0.8, 0.2]
```

Dot product:

```text id="j4r7w1"
Q·K₁ = 1
Q·K₂ = 0
Q·K₃ = 0.8
```

তাই:

```text id="a2m8k5"
K₁ → বেশি relevant
K₃ → moderately relevant
K₂ → কম relevant
```

তারপর softmax normalized weights তৈরি করবে।

---

# 21. Self-Attention কী?

এখন আসল গুরুত্বপূর্ণ transition:

> **Self-Attention হলো এমন attention যেখানে Query, Key এবং Value একই sequence থেকে আসে।**

উদাহরণ:

```text id="k9p4x2"
The cat sat on the mat.
```

সব token একই sequence-এর অংশ।

```text id="s5v7d3"
Q ← sentence
K ← sentence
V ← sentence
```

তাই:

```text id="e8q2n6"
Self-Attention
```

এটি Transformer-এর foundation।

**Self-Attention-এর পূর্ণ mathematical ও implementation details M02-এর পরের dedicated lesson-এ আরও গভীরভাবে করব।**

---

# 22. Attention বনাম Self-Attention

### Traditional Encoder-Decoder Attention

```text id="v6m3r1"
Query
← Decoder

Key/Value
← Encoder
```

অর্থাৎ:

```text id="q0h5t8"
Decoder
   ↓
Attention
   ↓
Encoder outputs
```

### Self-Attention

```text id="n4x7p2"
Same sequence
      ↓
 ┌────┼────┐
 Q    K    V
 └────┼────┘
      ↓
Attention
```

---

# 23. কেন Attention এত গুরুত্বপূর্ণ?

Attention model-কে:

```text id="s7q2n9"
Relevant information
        ↓
Focus
        ↓
Better context
```

দিতে সাহায্য করে।

একটি sentence:

```text id="w3p6k1"
The animal didn't cross the street because it was tired.
```

`it` কোন entity-কে refer করছে?

```text id="f2r8m5"
animal
```

Attention-এর মতো mechanisms token relationships model করতে সাহায্য করে।

তবে **attention alone = full coreference solver নয়**; learned representations-এর মাধ্যমে context relationships capture করার একটি mechanism।

---

# 24. Attention Matrix

ধরো sentence:

```text id="2v9c4h"
I love NLP
```

৩টি token:

```text id="j8k1s6"
I
love
NLP
```

Self-attention-এ প্রতিটি token অন্য tokenগুলোর দিকে attention দিতে পারে।

Conceptual matrix:

```text id="r5w2n7"
          I    love   NLP

I        0.5   0.3   0.2
love     0.2   0.5   0.3
NLP      0.1   0.3   0.6
```

প্রতিটি row-এর sum:

```text id="t1m7q4"
1.0
```

এটি বোঝায় প্রতিটি token কোন tokens-এ কতটা attention দিচ্ছে।

---

# 25. Attention Matrix-এর Shape

যদি sequence length হয়:

```text
L = 100
```

তাহলে একটি attention matrix-এর shape:

```text id="k5s8p1"
(100, 100)
```

Batch থাকলে:

```text id="h2v6q9"
(batch_size, 100, 100)
```

Multiple heads থাকলে আরও একটি head dimension থাকে:

```text id="p4n8x3"
(batch_size, num_heads, sequence_length, sequence_length)
```

এই shape পরে Transformer-এ অত্যন্ত গুরুত্বপূর্ণ হবে।

---

# 26. Attention Complexity

Self-attention-এর একটি গুরুত্বপূর্ণ limitation হলো sequence length-এর সাথে attention matrix বড় হয়।

Sequence length:

```text id="c7m1r5"
n
```

তাহলে সাধারণ self-attention-এর pairwise interaction:

$$
O(n^2)
$$

অর্থাৎ:

```text id="d8q4k2"
Sequence × Sequence
```

এই কারণে খুব long context-এর ক্ষেত্রে memory/computation expensive হতে পারে।

---

# 27. RNN বনাম Attention

| RNN                          | Attention                       |
| ---------------------------- | ------------------------------- |
| Sequential processing        | Tokens can interact directly    |
| Hidden state carries context | Direct weighted context         |
| Long dependency difficult    | Long-range relationships easier |
| Harder to parallelize        | More parallelizable             |
| Recurrence                   | Weighted information retrieval  |

---

# 28. LSTM বনাম Attention

LSTM:

```text id="w7n2k9"
Token 1
 ↓
Token 2
 ↓
Token 3
 ↓
Token 4
```

Attention:

```text id="a9f3x6"
Token 1 ─────┐
Token 2 ─────┤
Token 3 ─────┼→ Attention
Token 4 ─────┤
```

Attention direct relationships model করতে পারে।

---

# 29. Attention + RNN

Attention প্রথমে RNN/LSTM-এর সাথে combine করা হয়েছিল।

Architecture:

```text id="s4m8q2"
Input
 ↓
LSTM Encoder
 ↓
h₁ h₂ h₃ h₄
 ↓
Attention
 ↓
Context
 ↓
LSTM Decoder
 ↓
Output
```

এটি classic sequence-to-sequence architecture-কে উন্নত করেছিল।

---

# 30. Bahdanau Attention

**Bahdanau Attention** হলো একটি গুরুত্বপূর্ণ early neural attention mechanism।

এটি সাধারণত:

> **Additive Attention**

হিসেবে পরিচিত।

মূল ধারণা:

```text id="r7x3m9"
Encoder Hidden State
        +
Decoder Hidden State
        ↓
Neural Network
        ↓
Attention Score
```

এটি sequence-to-sequence translation-এ attention-এর জনপ্রিয় early formulation।

---

# 31. Luong Attention

আরেকটি গুরুত্বপূর্ণ architecture:

> **Luong Attention**

এটি সাধারণত dot-product/general ধরনের scoring ব্যবহার করে।

Basic idea:

```text id="v2n6k8"
Query
 ↓
Compare
 ↓
Encoder Hidden States
 ↓
Attention Weights
 ↓
Context
```

---

# 32. Bahdanau বনাম Luong

| Bahdanau                    | Luong                         |
| --------------------------- | ----------------------------- |
| Additive attention          | Dot/general style             |
| Neural scoring network      | Similarity-based scoring      |
| Earlier attention work      | Later alternative formulation |
| More computation in scoring | Often simpler scoring         |

দুটিই Transformer-এর আগে attention evolution বুঝতে গুরুত্বপূর্ণ।

---

# 33. Attention-এর Training Flow

```text id="n8q3v5"
Input
 ↓
Encoder
 ↓
Hidden States
 ↓
Attention
 ↓
Context Vector
 ↓
Decoder
 ↓
Prediction
 ↓
Loss
 ↓
Backpropagation
 ↓
Update weights
```

Attention-এর weights manually fixed নয়।

Model training-এর মাধ্যমে শিখে কোন information বেশি useful।

---

# 34. Attention কি Human-like Attention?

না।

এখানে "attention" শব্দটি human consciousness বা human attention-এর exact equivalent নয়।

এটি mathematical mechanism:

```text id="e3r7m1"
Similarity
 ↓
Weights
 ↓
Weighted aggregation
```

তাই:

> **Attention ≠ human attention**

---

# 35. Attention Weight কি সবসময় Explanation?

এটাও গুরুত্বপূর্ণ।

কোন token-এ বেশি attention weight এসেছে মানেই model-এর complete reasoning বা explanation সেটি নয়।

অর্থাৎ:

```text id="x5m9q2"
Attention Weight
      ≠
Complete Explanation
```

এটি একটি useful diagnostic signal হতে পারে, কিন্তু model-এর internal reasoning-এর পূর্ণ ব্যাখ্যা নয়।

---

# 36. AI Writing Assistant-এর জন্য Attention

তোমার future AI writing platform-এর জন্য attention অত্যন্ত গুরুত্বপূর্ণ।

ধরো:

```text id="b6q2w8"
The student submitted the assignment
because he had finished it early.
```

Contextual relationship বুঝতে:

```text id="p7m4n1"
student
assignment
he
finished
```

এর মধ্যে সম্পর্ক গুরুত্বপূর্ণ।

Attention-based architectures এই ধরনের context relationships model করতে পারে।

---

# 37. Text Rewriting-এর Connection

একটি sentence:

```text id="z8r2k5"
The implementation was very effective because
the algorithm reduced unnecessary computation.
```

Rewriting model-এর জন্য relevant relationships:

```text id="q4m7s9"
implementation
effective
algorithm
reduced
computation
```

Attention-based model পুরো sequence-এর relevant information dynamically combine করতে পারে।

এটি modern text generation/rewrite systems-এর foundation-এর অংশ।

---

# 38. Attention + Semantic Similarity

আগে আমরা embeddings শিখেছি।

এখন:

```text id="j2x8p5"
Embeddings
   ↓
Vector Representations
   ↓
Attention
   ↓
Context-dependent representation
```

Static embedding:

```text id="d4n7q1"
bank
→ one fixed vector
```

Contextual model:

```text id="h5m2s8"
river bank
→ context-specific representation

bank account
→ different contextual representation
```

এই contextualization modern NLP-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 39. Attention থেকে Transformer

এখন পুরো transition:

```text id="m9x3k7"
RNN
 ↓
LSTM
 ↓
GRU
 ↓
Encoder-Decoder Attention
 ↓
Self-Attention
 ↓
Multi-Head Attention
 ↓
Transformer
```

Transformer-এর core idea:

> **Recurrence বাদ দিয়ে attention-based sequence modeling।**

---

# 40. Transformer-এর High-Level Architecture

এখন শুধু overview:

```text id="q7n4v2"
Input Tokens
     ↓
Embedding
     ↓
Positional Information
     ↓
Self-Attention
     ↓
Feed Forward Network
     ↓
Layer Normalization
     ↓
Transformer Block
     ↓
Output
```

পরবর্তী lessons-এ আমরা এগুলো একেকটি করে গভীরভাবে শিখব।

---

# 41. Practical PyTorch-style Attention

Basic scaled dot-product attention conceptually:

```python id="p8v2m6"
import torch
import math

Q = torch.randn(2, 4, 8)
K = torch.randn(2, 4, 8)
V = torch.randn(2, 4, 8)

scores = Q @ K.transpose(-2, -1)

scores = scores / math.sqrt(K.size(-1))

weights = torch.softmax(scores, dim=-1)

output = weights @ V

print(output.shape)
```

Expected:

```text id="x4k7q2"
torch.Size([2, 4, 8])
```

এখানে:

```text id="s3m9v5"
Q → Query
K → Key
V → Value
```

---

# 42. Code Flow

উপরের code:

```text id="y6p1r8"
Q
 ↓
QKᵀ
 ↓
Similarity Scores
 ↓
Scale
 ↓
Softmax
 ↓
Attention Weights
 ↓
× V
 ↓
Attention Output
```

এটাই modern attention-এর core mathematical flow।

---

# 43. Shape Analysis

ধরো:

```text id="n2w7k4"
Q = (batch, seq_len, d)
K = (batch, seq_len, d)
V = (batch, seq_len, d)
```

তাহলে:

```text id="r8m3x1"
Kᵀ
→ (batch, d, seq_len)
```

তাই:

```text id="c5q9v2"
Q @ Kᵀ
```

ফল:

```text id="h7n4p6"
(batch, seq_len, seq_len)
```

তারপর:

```text id="z1m8s3"
Attention weights
@
V
```

ফল:

```text id="q6v2k9"
(batch, seq_len, d)
```

এই shape calculation ভালোভাবে আয়ত্ত করা খুব গুরুত্বপূর্ণ।

---

# 44. Padding Mask-এর Introduction

বাস্তব dataset-এ sentence-এর length আলাদা হতে পারে।

যেমন:

```text id="u4r8p1"
I love NLP
```

এবং:

```text id="v7m2q5"
I love machine learning
```

Batch করার জন্য padding:

```text id="s8k3n6"
I love NLP <PAD>
I love machine learning
```

Model যেন `<PAD>`-এ attention না দেয়, তাই **attention mask** ব্যবহার করা হয়।

Concept:

```text id="j5q9x2"
Real Token → attend
PAD Token  → ignore
```

---

# 45. Causal Mask-এর Introduction

Text generation-এর সময় model future token দেখতে পারবে না।

Example:

```text id="w2n7m4"
I love machine learning
```

যদি model `machine` predict করে:

```text id="e8p3q1"
I love
```

থেকে future:

```text id="k6r9s2"
learning
```

দেখা যাবে না।

তাই:

> **Causal Mask**

ব্যবহার করা হয়।

Concept:

```text id="a4v7n8"
Past      → visible
Current   → visible
Future    → hidden
```

এটি GPT-style autoregressive Transformer-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 46. দুই ধরনের Mask

```text id="z3q8m5"
Attention Mask
      │
      ├── Padding Mask
      │
      └── Causal Mask
```

### Padding Mask

PAD token ignore করে।

### Causal Mask

Future token block করে।

---

# 47. আজকের সবচেয়ে গুরুত্বপূর্ণ Concepts

এই ১০টি অবশ্যই বুঝবে:

```text id="y8m3q6"
1. Attention
2. Attention Score
3. Attention Weight
4. Context Vector
5. Query
6. Key
7. Value
8. Scaled Dot-Product Attention
9. Self-Attention
10. Attention Mask
```

---

# 48. Complete Evolution Mental Model

```text id="f7q2m9"
                 NLP Sequence Modeling
                         │
                         ↓
                        RNN
                         │
                         ↓
                       LSTM
                         │
                         ↓
                        GRU
                         │
                         ↓
              Encoder-Decoder Attention
                         │
                         ↓
                   Self-Attention
                         │
                         ↓
                 Multi-Head Attention
                         │
                         ↓
                    Transformer
                         │
               ┌─────────┴─────────┐
               ↓                   ↓
             BERT                 GPT
               │                   │
               └─────────┬─────────┘
                         ↓
                        LLM
```

---

# 49. AI Writing Project-এর Final Direction

তোমার project-এর জন্য আমরা যে architecture বুঝতে যাচ্ছি:

```text id="c8p4n1"
                 USER TEXT
                     ↓
                 TOKENIZER
                     ↓
               TOKEN IDs
                     ↓
                EMBEDDING
                     ↓
              SELF-ATTENTION
                     ↓
             TRANSFORMER
                     ↓
          CONTEXTUAL REPRESENTATION
                     ↓
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
   CLASSIFY       ANALYZE       GENERATE
       ↓             ↓             ↓
   AI Analysis   Style/Meaning   Rewrite
```

এখনো আমরা production AI writing model তৈরি করছি না। প্রথমে foundation সম্পূর্ণ করব।

---

# 50. Practice Tasks

### Task 1

Explain:

> Attention কেন RNN/LSTM-এর জন্য useful?

---

### Task 2

এই তিনটি explain করো:

```text
Query
Key
Value
```

---

### Task 3

এই formula explain করো:

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

---

### Task 4

Difference:

```text
Attention
vs
Self-Attention
```

---

### Task 5

Explain:

```text
Padding Mask
vs
Causal Mask
```

---

### Task 6

এই shapeগুলো বের করো:

```text
Q = (32, 100, 128)
K = (32, 100, 128)
V = (32, 100, 128)
```

তাহলে:

```text
Q @ Kᵀ = ?
Attention Output = ?
```

---

### Task 7

PyTorch দিয়ে scaled dot-product attention implement করো।

---

# 51. Theory Questions

1. What is Attention?
2. Why was attention introduced?
3. What is an attention score?
4. What is an attention weight?
5. What is a context vector?
6. What is Query?
7. What is Key?
8. What is Value?
9. Why do we calculate `QKᵀ`?
10. Why divide by `√dₖ`?
11. Why use Softmax?
12. What is scaled dot-product attention?
13. What is self-attention?
14. Attention vs self-attention?
15. What is encoder-decoder attention?
16. What is Bahdanau attention?
17. What is Luong attention?
18. What is attention matrix?
19. What is attention masking?
20. Padding mask কী?
21. Causal mask কী?
22. Why is causal masking needed for autoregressive generation?
23. What is the complexity of standard self-attention?
24. How does attention help long-range dependencies?
25. Why did attention become important for Transformers?

---

# 52. Interview Questions

### Q1. What is Attention?

Attention is a mechanism that computes relevance between representations and uses normalized weights to combine information from relevant positions.

### Q2. What are Q, K, and V?

```text
Q → Query
K → Key
V → Value
```

Query represents what is being searched for, Keys represent what each position can be matched against, and Values contain the information that is aggregated.

### Q3. What is the formula for scaled dot-product attention?

$$
softmax\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

### Q4. Why is scaling needed?

To prevent large dot-product values from producing overly sharp softmax distributions and unstable gradients.

### Q5. What is self-attention?

Self-attention is attention where Q, K, and V are derived from the same sequence.

### Q6. Why is attention useful compared with a single RNN final hidden state?

It allows the model to dynamically access information from multiple sequence positions instead of relying solely on one compressed recurrent state.

### Q7. What is causal masking?

It prevents a position from attending to future positions, which is necessary for autoregressive next-token prediction.

### Q8. What is the computational complexity of standard self-attention?

For sequence length \(n\), the attention score matrix generally requires **O(n²)** pairwise interactions.

---

# ✅ M02.20 Completion Checklist

* [x] Attention definition
* [x] Motivation for Attention
* [x] RNN limitation
* [x] LSTM/GRU limitation
* [x] Encoder-Decoder architecture
* [x] Attention Score
* [x] Attention Weight
* [x] Context Vector
* [x] Softmax
* [x] Query
* [x] Key
* [x] Value
* [x] Scaled Dot-Product Attention
* [x] QKᵀ
* [x] Scaling
* [x] Self-Attention introduction
* [x] Attention Matrix
* [x] Attention complexity
* [x] Bahdanau Attention
* [x] Luong Attention
* [x] Attention + RNN/LSTM
* [x] Padding Mask
* [x] Causal Mask
* [x] Attention + Embedding
* [x] Attention + Semantic Representation
* [x] Attention + Text Generation
* [x] AI Writing Assistant connection
* [x] PyTorch implementation
* [x] Tensor shapes
* [x] Theory questions
* [x] Interview questions

## 🧠 Final Mental Model

```text id="k7m2q9"
                   INPUT
                     ↓
                 Embedding
                     ↓
              Q ──────────┐
              K ──────────┤
              V ──────────┤
                          ↓
                       QKᵀ
                          ↓
                    Scale √dₖ
                          ↓
                       Softmax
                          ↓
                  Attention Weights
                          ↓
                       × V
                          ↓
                  Context Output
```

সবচেয়ে গুরুত্বপূর্ণভাবে মনে রাখো:

```text id="r4n8x2"
Attention
    ↓
"Which information is relevant?"

Query
    ↓
"What am I looking for?"

Key
    ↓
"Which information matches?"

Value
    ↓
"What information should I retrieve?"
```

**M02.20 = Attention Foundation complete.**

----
# M02.21 — Self-Attention Deep Dive

M02.20-এ আমরা **Attention Mechanism** শিখেছি। এখন আমরা সেটার সবচেয়ে গুরুত্বপূর্ণ form:

> **Self-Attention**

এটি ভালোভাবে বুঝতে পারলে পরের **Multi-Head Attention → Transformer → BERT/GPT → LLM** অনেক সহজ হবে।

আমাদের progression:

```text
RNN
 ↓
LSTM
 ↓
GRU
 ↓
Attention
 ↓
SELF-ATTENTION        ← M02.21
 ↓
Multi-Head Attention
 ↓
Transformer
 ↓
BERT / GPT
 ↓
LLM
```

---

# 1. Self-Attention কী?

**Self-Attention** হলো এমন একটি mechanism যেখানে একটি sequence-এর প্রতিটি token অন্য tokenগুলোর সাথে relationship তৈরি করে এবং context অনুযায়ী information সংগ্রহ করে।

উদাহরণ:

```text
The cat sat on the mat.
```

`cat` token-এর representation তৈরি করার সময় model দেখতে পারে:

```text
The
cat
sat
on
the
mat
```

অর্থাৎ `cat` শুধু নিজের information নয়, sentence-এর অন্য relevant token থেকেও information নিতে পারে।

---

# 2. কেন Self-Attention দরকার?

ধরো:

```text
The animal didn't cross the street because it was tired.
```

এখানে:

```text
it
```

কোন entity-এর সাথে সম্পর্কিত?

সম্ভবত:

```text
animal
```

Self-attention model-কে sequence-এর বিভিন্ন position-এর মধ্যে direct interaction তৈরি করতে সাহায্য করে।

Concept:

```text
it ───────────────→ animal
```

এখানে tokens-এর মধ্যে relationship capture করা সম্ভব।

---

# 3. RNN বনাম Self-Attention

RNN:

```text
x₁ → x₂ → x₃ → x₄ → x₅
```

Information sequentially flow করে।

Self-Attention:

```text
x₁ ───┬──→ x₂
      ├──→ x₃
      ├──→ x₄
      └──→ x₅

x₂ ───┬──→ x₁
      ├──→ x₃
      ├──→ x₄
      └──→ x₅
```

প্রতিটি token অন্য position-এর দিকে attention দিতে পারে।

---

# 4. একটি গুরুত্বপূর্ণ Example

Sentence:

```text
The student reads a book.
```

Tokens:

```text
x₁ = The
x₂ = student
x₃ = reads
x₄ = a
x₅ = book
```

`reads` token-এর contextual representation তৈরি করতে model হয়তো বেশি attention দেবে:

```text
student
book
```

Conceptually:

```text
student ── 0.35 ──┐
reads   ── 0.20 ──┤
book    ── 0.40 ──┤ → new representation of "reads"
a       ── 0.05 ──┘
```

Actual weights model training-এর মাধ্যমে শেখে।

---

# 5. Self-Attention-এর Core

Self-attention-এ:

```text
Input X
  │
  ├──→ Q
  ├──→ K
  └──→ V
```

অর্থাৎ একই input থেকে:

```text
Query
Key
Value
```

তৈরি হয়।

এটাই "self"-এর মূল ধারণা।

---

# 6. Q, K, V কীভাবে তৈরি হয়?

ধরো input representation:

$$
X
$$

তাহলে:

$$
Q=XW_Q
$$

$$
K=XW_K
$$

$$
V=XW_V
$$

এখানে:

```text
X   → Input embeddings/representations
WQ  → Query projection matrix
WK  → Key projection matrix
WV  → Value projection matrix
```

এই matrices model training-এর সময় শেখে।

---

# 7. কেন তিনটি আলাদা Projection?

খুব গুরুত্বপূর্ণ প্রশ্ন।

যদি একই vector সব কাজের জন্য ব্যবহার করতাম, তাহলে model-এর flexibility কমে যেত।

তাই:

```text
X
│
├── WQ → Query representation
│
├── WK → Key representation
│
└── WV → Value representation
```

Model শিখতে পারে:

> কোন information খুঁজব?

> কোন information relevant?

> কোন information aggregate করব?

---

# 8. Self-Attention-এর Complete Formula

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

Self-attention-এর ক্ষেত্রে:

$$
Q=XW_Q
$$

$$
K=XW_K
$$

$$
V=XW_V
$$

তাই পুরো flow:

```text
X
│
├──→ Q
├──→ K
└──→ V
      │
      ↓
     QKᵀ
      ↓
   Scaling
      ↓
    Softmax
      ↓
Attention Weights
      ↓
      × V
      ↓
Self-Attention Output
```

---

# 9. Step 1 — Input Matrix

ধরো sentence:

```text
I love NLP
```

৩টি token:

```text
I
love
NLP
```

প্রতিটি token-এর embedding dimension:

```text
d_model = 4
```

তাহলে:

$$
X \in \mathbb{R}^{3\times4}
$$

অর্থাৎ:

```text
X =

[ x₁ ]
[ x₂ ]
[ x₃ ]
```

Shape:

```text
(3, 4)
```

---

# 10. Step 2 — Q, K, V তৈরি

ধরো:

```text
d_model = 4
d_k = 4
```

তাহলে:

```text
X      = (3, 4)

WQ     = (4, 4)
WK     = (4, 4)
WV     = (4, 4)
```

তাই:

```text
Q = X @ WQ
K = X @ WK
V = X @ WV
```

সবগুলোর shape:

```text
(3, 4)
```

---

# 11. Step 3 — QKᵀ

আমরা:

$$
QK^T
$$

calculate করি।

Shape:

```text
Q       = (3, 4)
Kᵀ      = (4, 3)

QKᵀ     = (3, 3)
```

তাহলে:

```text
Attention Scores

       I    love   NLP

I     [?]   [?]    [?]
love  [?]   [?]    [?]
NLP   [?]   [?]    [?]
```

এই matrix-এর প্রতিটি value দুই token-এর compatibility/similarity score নির্দেশ করে।

---

# 12. Attention Matrix কেন Square?

Sequence length:

```text
3
```

তাই:

$$
3\times3
$$

যদি:

```text
sequence length = 100
```

তাহলে:

```text
100 × 100
```

যদি:

```text
sequence length = 1000
```

তাহলে:

```text
1000 × 1000
```

এটাই self-attention-এর quadratic complexity-এর মূল কারণ।

---

# 13. Step 4 — Scaling

আমরা score matrix-কে:

$$
\sqrt{d_k}
$$

দিয়ে ভাগ করি।

$$
Scores =
\frac{QK^T}{\sqrt{d_k}}
$$

যদি:

```text
d_k = 64
```

তাহলে:

$$
\sqrt{64}=8
$$

অর্থাৎ:

```text
QKᵀ
 ↓
÷ 8
```

---

# 14. Step 5 — Softmax

তারপর প্রতিটি row-তে softmax:

$$
A=softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)
$$

ধরো একটি row:

```text
[2.0, 1.0, 0.5]
```

Softmax-এর পরে approximately:

```text
[0.63, 0.23, 0.14]
```

যোগফল:

```text
1.00
```

অর্থাৎ model information distribution তৈরি করেছে।

---

# 15. Step 6 — Multiply with V

শেষে:

$$
Output=AV
$$

যেখানে:

```text
A = Attention Weights
V = Value Matrix
```

Concept:

```text
Attention Weights
       ×
Value
       ↓
New Contextual Representation
```

---

# 16. Complete Mathematical Flow

```text
                 X
                 │
       ┌─────────┼─────────┐
       ↓         ↓         ↓
      XWQ       XWK       XWV
       ↓         ↓         ↓
       Q         K         V
       │         │
       └────┬────┘
            ↓
           QKᵀ
            ↓
        / √dₖ
            ↓
         Softmax
            ↓
      Attention Matrix
            │
            ×
            V
            ↓
    Self-Attention Output
```

---

# 17. একটি গুরুত্বপূর্ণ বিষয়: Attention Row

ধরো:

```text
Sentence:
The cat eats fish
```

`eats` row:

```text
The     0.10
cat     0.40
eats    0.15
fish    0.35
```

তাহলে `eats`-এর নতুন representation তৈরি হবে:

$$
0.10V_{The}
+
0.40V_{cat}
+
0.15V_{eats}
+
0.35V_{fish}
$$

অর্থাৎ:

> `eats` token তার representation তৈরির জন্য পুরো sentence থেকে information সংগ্রহ করছে।

এটাই self-attention-এর heart।

---

# 18. Contextual Representation

M02.15-এ আমরা static embeddings দেখেছি।

যেমন:

```text
bank → fixed vector
```

কিন্তু self-attention-এর পরে:

```text
river bank
     ↓
contextual representation

bank account
     ↓
different contextual representation
```

অর্থাৎ একই token-এর representation surrounding context দ্বারা প্রভাবিত হতে পারে।

এটি modern NLP-এর অন্যতম গুরুত্বপূর্ণ ধারণা।

---

# 19. Self-Attention vs Word Embedding

Embedding:

```text
Token ID
   ↓
Embedding Lookup
   ↓
Vector
```

Self-Attention:

```text
Token Vectors
     ↓
Context Interaction
     ↓
Contextual Vectors
```

তাই:

```text
Embedding
→ token representation

Self-Attention
→ context-aware representation
```

---

# 20. Self-Attention vs RNN

### RNN

```text
x₁
 ↓
h₁
 ↓
x₂
 ↓
h₂
 ↓
x₃
 ↓
h₃
```

### Self-Attention

```text
x₁ ─────┐
x₂ ─────┤
x₃ ─────┼→ Attention
x₄ ─────┤
x₅ ─────┘
```

Self-attention-এর একটি বড় সুবিধা হলো sequence positions-এর মধ্যে direct interactions।

---

# 21. Parallelization

RNN:

```text
x₁ → x₂ → x₃ → x₄
```

এক timestep-এর computation পরের timestep-এর সাথে dependency রাখে।

Training-এ এটি parallelization সীমিত করে।

Self-attention:

```text
x₁
x₂
x₃
x₄
 ↓
Matrix Operations
```

অনেক computation একসাথে করা যায়।

এই কারণেই modern GPU-based training-এ self-attention অত্যন্ত powerful।

---

# 22. কিন্তু Self-Attention-এর সমস্যা আছে

সবকিছু perfect নয়।

মূল সমস্যা:

$$
O(n^2)
$$

যেখানে:

```text
n = sequence length
```

কারণ:

```text
প্রতিটি token
      ↕
প্রতিটি token
```

এর মধ্যে interaction তৈরি হচ্ছে।

---

# 23. Example of Complexity

Sequence length:

```text
100
```

Attention matrix:

```text
100 × 100 = 10,000
```

Sequence:

```text
1,000
```

Matrix:

```text
1,000 × 1,000
= 1,000,000
```

Sequence:

```text
10,000
```

Matrix:

```text
10,000 × 10,000
= 100,000,000
```

তাই long-context NLP computationally expensive হতে পারে।

---

# 24. Causal Self-Attention

GPT-এর মতো autoregressive model-এ future token দেখা যাবে না।

Sentence:

```text
I love machine learning
```

Training-এর সময়:

```text
I
```

শুধু নিজের information দেখতে পারে।

```text
I love
```

এখানে `I` এবং `love` দেখা যায়।

```text
I love machine
```

এখানে:

```text
I
love
machine
```

দেখা যায়।

কিন্তু future:

```text
learning
```

দেখা যাবে না।

---

# 25. Causal Attention Matrix

Conceptually:

```text
        I   love   machine   learning

I       ✓    ✗       ✗          ✗

love    ✓    ✓       ✗          ✗

machine ✓    ✓       ✓          ✗

learning✓    ✓       ✓          ✓
```

এটাকে triangular pattern দিয়ে represent করা যায়।

---

# 26. Causal Mask

Mathematically:

```text
Future positions
→ blocked
```

Conceptual mask:

```text
0   -∞  -∞  -∞
0    0  -∞  -∞
0    0   0  -∞
0    0   0   0
```

Softmax-এর আগে blocked positions-এ `-∞` দেওয়া হলে:

```text
softmax(-∞) ≈ 0
```

তাই future token-এর attention weight:

```text
0
```

হয়ে যায়।

---

# 27. Padding Mask

ধরো:

```text
I love NLP <PAD>
I love machine learning
```

`<PAD>` যেন attention না পায়/না দেয়, তার জন্য padding mask ব্যবহার করা হয়।

দুই ধরনের mask মনে রাখো:

```text
Mask
│
├── Padding Mask
│
└── Causal Mask
```

---

# 28. Bidirectional Context

যদি causal restriction না থাকে, self-attention-এর একটি token sequence-এর আগের এবং পরের token দুদিকের information ব্যবহার করতে পারে।

যেমন BERT-style encoder:

```text
Previous ← Token → Future
```

এটি bidirectional contextual representation তৈরিতে সাহায্য করে।

অন্যদিকে GPT-style autoregressive attention:

```text
Past → Current
```

Future blocked।

---

# 29. BERT বনাম GPT — Attention Perspective

### BERT

সাধারণ encoder-style self-attention:

```text
Previous
   ↕
Current
   ↕
Future
```

### GPT

Causal self-attention:

```text
Past
 ↓
Current

Future → blocked
```

এটি খুব গুরুত্বপূর্ণ distinction।

---

# 30. Self-Attention-এর PyTorch Implementation

একটি basic implementation:

```python
import torch
import math


def self_attention(x, Wq, Wk, Wv):
    Q = x @ Wq
    K = x @ Wk
    V = x @ Wv

    scores = Q @ K.transpose(-2, -1)

    scores = scores / math.sqrt(K.size(-1))

    weights = torch.softmax(scores, dim=-1)

    output = weights @ V

    return output, weights
```

ব্যবহার:

```python
batch_size = 2
seq_len = 5
d_model = 8

x = torch.randn(batch_size, seq_len, d_model)

Wq = torch.randn(d_model, d_model)
Wk = torch.randn(d_model, d_model)
Wv = torch.randn(d_model, d_model)

output, weights = self_attention(
    x, Wq, Wk, Wv
)

print("Output:", output.shape)
print("Weights:", weights.shape)
```

Output:

```text
Output: torch.Size([2, 5, 8])
Weights: torch.Size([2, 5, 5])
```

---

# 31. Shape Analysis

Input:

```text
X = (B, L, D)
```

যেখানে:

```text
B = batch size
L = sequence length
D = embedding/model dimension
```

তারপর:

```text
Q = (B, L, D)
K = (B, L, D)
V = (B, L, D)
```

Transpose:

```text
Kᵀ = (B, D, L)
```

তাই:

```text
Q @ Kᵀ
```

ফল:

```text
(B, L, L)
```

তারপর:

```text
Attention @ V
```

ফল:

```text
(B, L, D)
```

---

# 32. সবচেয়ে গুরুত্বপূর্ণ Shape Formula

মনে রাখো:

```text
Input
(B, L, D)

Q, K, V
(B, L, D)

QKᵀ
(B, L, L)

Attention Output
(B, L, D)
```

এটি Transformer implementation-এর সময় বারবার লাগবে।

---

# 33. `nn.MultiheadAttention` বনাম Basic Self-Attention

PyTorch-এ ready-made implementation আছে:

```python
import torch
import torch.nn as nn

attention = nn.MultiheadAttention(
    embed_dim=128,
    num_heads=8,
    batch_first=True
)
```

এটি **multi-head attention**, যেটা আমরা পরের lesson-এ গভীরভাবে শিখব।

Basic self-attention বুঝতে আগে manual implementation জানা গুরুত্বপূর্ণ।

---

# 34. Self-Attention-এর তিনটি Important Components

```text
1. Projection
   X → Q,K,V

2. Similarity
   QKᵀ

3. Weighted Aggregation
   Softmax(QKᵀ/√dₖ) × V
```

---

# 35. Self-Attention কি শুধু Similarity?

পুরোপুরি না।

এখানে:

```text
QKᵀ
```

দিয়ে compatibility/relevance score পাওয়া যায়।

কিন্তু final output:

```text
Attention Weights × V
```

এর মাধ্যমে তৈরি হয়।

তাই:

```text
Score
+
Normalization
+
Value aggregation
=
Attention Output
```

---

# 36. Self-Attention কেন "Self"?

কারণ:

```text
Q ← X
K ← X
V ← X
```

সবগুলো একই sequence-এর representation থেকে আসে।

অন্যদিকে encoder-decoder cross-attention-এ:

```text
Q ← Decoder
K ← Encoder
V ← Encoder
```

এটি **cross-attention**।

---

# 37. Self-Attention vs Cross-Attention

| Self-Attention                        | Cross-Attention                                    |
| ------------------------------------- | -------------------------------------------------- |
| Q, K, V same sequence থেকে            | Q ও K/V আলাদা sequence থেকে                        |
| Sequence-এর internal relationships    | দুই representation-এর interaction                  |
| Transformer encoder/decoder-এ ব্যবহৃত | Encoder-decoder architecture-এ গুরুত্বপূর্ণ        |
| Contextualization                     | External/context source থেকে information retrieval |

---

# 38. AI Writing Assistant-এ Self-Attention

ধরো user লিখল:

```text
Although the implementation was complex,
the final system performed efficiently because
the algorithm reduced unnecessary operations.
```

একটি rewrite model-এর জন্য:

```text
implementation
complex
system
performed
efficiently
algorithm
reduced
operations
```

এর মধ্যে relationships গুরুত্বপূর্ণ।

Self-attention:

```text
প্রতিটি token
      ↓
Relevant tokens-এর information
      ↓
Contextual representation
      ↓
Generation / Classification
```

এর মাধ্যমে model sentence-level context ব্যবহার করতে পারে।

---

# 39. AI Detector-এর ক্ষেত্রে

ধরো model sentence analysis করছে:

```text
The system consistently demonstrates
high computational efficiency.
```

Self-attention contextual features তৈরি করতে পারে:

```text
The ↔ system
system ↔ demonstrates
demonstrates ↔ efficiency
high ↔ computational
```

তারপর contextual representation classification model-এ যেতে পারে:

```text
Contextual Representation
          ↓
Classifier
          ↓
Prediction
```

তবে মনে রাখবে:

> Self-attention নিজে AI detector নয়।

এটি representation-learning mechanism।

---

# 40. Self-Attention-এর Limitations

### 1. Quadratic complexity

$$
O(n^2)
$$

### 2. Memory consumption

Large sequence → large attention matrix।

### 3. Positional information নিজে থেকে নেই

Self-attention-এর basic form-এ:

```text
"I love you"
```

এবং token order বুঝতে আলাদা positional information প্রয়োজন।

এটি পরের Transformer lesson-এর গুরুত্বপূর্ণ বিষয়।

### 4. Long context expensive

Sequence বড় হলে computation দ্রুত বাড়ে।

---

# 41. Positional Information কেন দরকার?

ধরো:

```text
Dog bites man.
```

এবং:

```text
Man bites dog.
```

একই tokens আছে:

```text
dog
bites
man
```

কিন্তু order আলাদা।

Basic self-attention-কে token position সম্পর্কে information দিতে হয়।

তাই Transformer-এ:

```text
Token Embedding
+
Positional Information
```

ব্যবহার করা হয়।

**Positional Encoding/Positional Embedding আমরা Transformer-এর dedicated lesson-এ বিস্তারিত করব।**

---

# 42. Self-Attention এবং Sequence Order

এখানে একটি subtle concept:

Self-attention নিজে token-to-token interaction করতে পারে, কিন্তু vanilla self-attention-এর operation token order-এর প্রতি inherently sequential recurrence-এর মতো সচেতন নয়।

তাই:

```text
Token Embedding
+
Position Information
```

দেওয়া গুরুত্বপূর্ণ।

---

# 43. Full Modern NLP Flow

এখন পুরো architecture:

```text
Raw Text
   ↓
Tokenizer
   ↓
Token IDs
   ↓
Token Embeddings
   ↓
Positional Information
   ↓
Self-Attention
   ↓
Contextual Representations
   ↓
Feed Forward Network
   ↓
Transformer Block
   ↓
Multiple Transformer Blocks
   ↓
Task Head
```

---

# 44. Transformer-এর সাথে Connection

এখন পর্যন্ত:

```text
M02.15
Word Embeddings
      ↓
M02.16
Language Modeling
      ↓
M02.17
RNN
      ↓
M02.18
LSTM
      ↓
M02.19
GRU
      ↓
M02.20
Attention
      ↓
M02.21
Self-Attention
```

পরের গুরুত্বপূর্ণ step:

```text
M02.22
Multi-Head Attention
```

তারপর:

```text
M02.23
Positional Encoding / Positional Embedding

M02.24
Transformer Architecture
```

এরপর Transformer থেকে:

```text
Encoder
Decoder
BERT
GPT
LLM
```

---

# 45. আজকের Core Formula

এটি অবশ্যই বুঝবে:

$$
Q=XW_Q
$$

$$
K=XW_K
$$

$$
V=XW_V
$$

তারপর:

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

সবচেয়ে সহজভাবে:

```text
X
 ↓
Q K V
 ↓
QKᵀ
 ↓
Scale
 ↓
Softmax
 ↓
Attention Weights
 ↓
× V
 ↓
Contextual Output
```

---

# 46. Practice — Beginner

### Task 1

Explain:

```text
Why is Self-Attention called "Self"?
```

### Task 2

Explain:

```text
Q
K
V
```

### Task 3

Why do we calculate:

```text
Q @ Kᵀ
```

### Task 4

Why divide by:

```text
√dₖ
```

### Task 5

Why use:

```text
Softmax
```

---

# 47. Practice — Intermediate

ধরো:

```text
Batch = 16
Sequence Length = 50
Embedding Dimension = 128
```

Find:

```text
X shape
Q shape
K shape
V shape
QKᵀ shape
Attention output shape
```

---

# 48. Practice — Advanced

একটি sentence:

```text
The student who studied Python
built an AI application.
```

Explain:

1. `student` কোন tokenগুলোর information ব্যবহার করতে পারে?
2. `application` কোন tokenগুলোর দিকে attention দিতে পারে?
3. Self-attention কীভাবে long-range relationship capture করতে সাহায্য করে?
4. যদি causal mask দেওয়া হয়, কী পরিবর্তন হবে?

---

# 49. Theory Questions

1. What is Self-Attention?
2. Why is it called self-attention?
3. How are Q, K and V generated?
4. What are \(W_Q,W_K,W_V\)?
5. What is \(QK^T\)?
6. Why transpose K?
7. Why divide by \(\sqrt{d_k}\)?
8. Why use Softmax?
9. What is an attention matrix?
10. What is a contextual representation?
11. What is causal self-attention?
12. What is padding mask?
13. What is cross-attention?
14. Self-attention vs cross-attention?
15. Self-attention vs RNN?
16. Why can self-attention be parallelized efficiently?
17. What is the complexity of self-attention?
18. Why is self-attention expensive for long sequences?
19. Why is positional information required?
20. How is self-attention used in GPT?
21. How is self-attention used in BERT?
22. What is the role of self-attention in Transformer?
23. Is attention weight a complete explanation of model reasoning?
24. Can self-attention alone understand semantics perfectly?
25. Why are Q, K and V projected separately?

---

# 50. Interview Questions

### Q1. Explain Self-Attention in one sentence.

> Self-attention allows each token to dynamically aggregate information from other tokens in the same sequence based on learned relevance scores.

### Q2. What is the formula?

$$
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

### Q3. Why `Kᵀ`?

Because matrix multiplication must produce pairwise token scores:

```text
(B,L,D)
×
(B,D,L)
=
(B,L,L)
```

### Q4. What does `(L,L)` represent?

Each token position-এর attention score relative to every token position।

### Q5. Why is self-attention O(n²)?

কারণ sequence-এর প্রায় প্রতিটি position-এর সাথে প্রতিটি position-এর pairwise interaction হিসাব করা হয়।

### Q6. Self-attention কি positional information জানে?

Basic self-attention নিজে sequence order encode করে না; তাই Transformer architecture-এ positional information যোগ করা হয়।

### Q7. GPT এবং BERT-এর attention-এর বড় পার্থক্য কী?

GPT autoregressive **causal self-attention** ব্যবহার করে, যাতে future tokens hidden থাকে। BERT-style encoder সাধারণত bidirectional self-attention ব্যবহার করে।

---

# ✅ M02.21 Completion Checklist

* [x] Self-Attention definition
* [x] Motivation
* [x] RNN vs Self-Attention
* [x] Self-Attention architecture
* [x] Query
* [x] Key
* [x] Value
* [x] Q projection
* [x] K projection
* [x] V projection
* [x] \(QK^T\)
* [x] Scaling
* [x] Softmax
* [x] Attention weights
* [x] Weighted aggregation
* [x] Contextual representation
* [x] Attention matrix
* [x] Tensor shapes
* [x] Causal Self-Attention
* [x] Padding Mask
* [x] Cross-Attention introduction
* [x] Self vs Cross Attention
* [x] Parallelization
* [x] Quadratic complexity
* [x] Positional information motivation
* [x] BERT connection
* [x] GPT connection
* [x] Transformer connection
* [x] PyTorch implementation
* [x] AI Writing Assistant connection
* [x] AI Detector/analysis connection
* [x] Theory questions
* [x] Interview questions

## 🧠 Final Mental Model

```text
                    INPUT X
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
       XWQ          XWK          XWV
          ↓            ↓            ↓
          Q            K            V
           \           /
            \         /
              QKᵀ
                ↓
             ÷ √dₖ
                ↓
             Softmax
                ↓
        Attention Weights
                │
                ×
                V
                ↓
       CONTEXTUAL OUTPUT
```

আর এক লাইনে:

```text
Self-Attention =
"প্রতিটি token নিজের context বোঝার জন্য
sequence-এর অন্য relevant token থেকে information নেয়।"
```

**M02.21 = Self-Attention Foundation complete.**


----
# M02.22 — Multi-Head Attention Deep Dive

M02.20-এ আমরা **Attention**, আর M02.21-এ **Self-Attention** শিখেছি।

এখন Self-Attention-এর সবচেয়ে গুরুত্বপূর্ণ extension:

> **Multi-Head Attention (MHA)**

এটাই Transformer architecture-এর core components-এর একটি।

আমাদের progression:

```text
RNN
 ↓
LSTM
 ↓
GRU
 ↓
Attention
 ↓
Self-Attention
 ↓
Multi-Head Attention     ← M02.22
 ↓
Positional Encoding
 ↓
Transformer
 ↓
BERT / GPT
 ↓
LLM
```

---

# 1. Multi-Head Attention কী?

সহজভাবে:

> **Multi-Head Attention একই sequence-এর উপর একাধিক attention mechanism parallelভাবে চালায়, যাতে model বিভিন্ন ধরনের relationship একসাথে শিখতে পারে।**

Single attention:

```text
Input
 ↓
One Attention
 ↓
Output
```

Multi-head:

```text
             Input
               ↓
      ┌────────┼────────┐
      ↓        ↓        ↓
    Head 1   Head 2   Head 3   ... Head N
      ↓        ↓        ↓          ↓
      └────────┼────────┘
               ↓
           Concatenate
               ↓
        Linear Projection
               ↓
             Output
```

---

# 2. কেন Multiple Heads?

ধরো sentence:

```text
The student reads a book because he likes it.
```

একটি attention head হয়তো focus করতে পারে:

```text
he → student
```

আরেকটি:

```text
it → book
```

আরেকটি:

```text
reads → student
reads → book
```

আরেকটি head grammatical relationship-এর উপর বেশি useful pattern শিখতে পারে।

অর্থাৎ:

```text
Head 1 → relationship A
Head 2 → relationship B
Head 3 → relationship C
...
```

তবে গুরুত্বপূর্ণ:

> কোন head ঠিক কোন linguistic concept শিখবে, সেটা manually assign করা হয় না। Training-এর মাধ্যমে heads বিভিন্ন useful patterns শিখে।

---

# 3. Single Attention-এর সীমাবদ্ধতা

আমরা M02.21-এ দেখেছি:

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

একটি attention operation একটি learned projection space-এ relationships model করে।

কিন্তু language-এ একই sentence-এ অনেক ধরনের relationship থাকতে পারে।

যেমন:

```text
subject relationship
object relationship
semantic relationship
syntactic relationship
long-distance relationship
local relationship
```

একটি single attention representation-এর বদলে multiple learned subspaces ব্যবহার করা বেশি expressive হতে পারে।

---

# 4. "Head" বলতে কী বোঝায়?

একটি **attention head** হলো একটি আলাদা scaled dot-product attention computation।

যেমন:

```text
Head 1:
Q₁ K₁ V₁
   ↓
Attention₁

Head 2:
Q₂ K₂ V₂
   ↓
Attention₂

Head 3:
Q₃ K₃ V₃
   ↓
Attention₃
```

প্রতিটি head-এর আলাদা projection parameters থাকে।

---

# 5. Multi-Head Attention Formula

প্রথমে প্রতিটি head:

$$
head_i =
Attention(QW_i^Q,KW_i^K,VW_i^V)
$$

তারপর:

$$
MultiHead(Q,K,V)
=
Concat(head_1,\ldots,head_h)W^O
$$

এখানে:

```text
WᵢQ → Query projection
WᵢK → Key projection
WᵢV → Value projection
Wᴼ  → Output projection
```

---

# 6. Formula ভেঙে দেখি

ধরো 4টি heads:

```text
Head 1
Head 2
Head 3
Head 4
```

প্রতিটির জন্য:

$$
Q_i=QW_i^Q
$$

$$
K_i=KW_i^K
$$

$$
V_i=VW_i^V
$$

তারপর:

$$
head_i =
softmax
\left(
\frac{Q_iK_i^T}{\sqrt{d_k}}
\right)V_i
$$

সবশেষে:

```text
head₁
head₂
head₃
head₄
  ↓
Concatenate
  ↓
Linear Layer
  ↓
MHA Output
```

---

# 7. একটি গুরুত্বপূর্ণ বিষয়

Multi-head attention মানে:

❌ একই attention 8 বার copy করা নয়।

বরং:

```text
Different learned projections
+
Different attention patterns
```

ব্যবহার করা হয়।

---

# 8. Model Dimension

ধরো:

```text
d_model = 512
num_heads = 8
```

সাধারণ Transformer design-এ:

$$
d_k=d_v=\frac{d_{model}}{h}
$$

তাহলে:

$$
d_k=d_v=\frac{512}{8}=64
$$

অর্থাৎ:

```text
Model dimension = 512

8 heads
↓
Each head dimension = 64
```

---

# 9. কেন Dimension ভাগ করা হয়?

যদি প্রত্যেক head-এ পুরো 512 dimension ব্যবহার করতাম:

```text
8 heads × 512
```

তাহলে computation অনেক বেড়ে যেত।

তাই সাধারণভাবে:

```text
512
 ↓
8 heads
 ↓
64 each
```

এভাবে model একই total representation dimension-এর মধ্যে multiple attention subspaces ব্যবহার করে।

---

# 10. Example

ধরো:

```text
d_model = 128
num_heads = 8
```

তাহলে:

$$
d_{head}=128/8=16
$$

তাই:

```text
Head 1 → 16 dimensions
Head 2 → 16 dimensions
Head 3 → 16 dimensions
...
Head 8 → 16 dimensions
```

Concatenate:

$$
8\times16=128
$$

আবার original model dimension:

```text
128
```

---

# 11. Complete Architecture

```text
                    Input X
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
       Head 1        Head 2       Head N
          ↓            ↓            ↓
      Attention     Attention    Attention
          ↓            ↓            ↓
          └────────────┼────────────┘
                       ↓
                  Concatenate
                       ↓
                Output Projection
                       ↓
                    MHA Output
```

---

# 12. Step-by-Step Example

ধরো:

```text
Sequence length = 4
d_model = 8
num_heads = 2
```

তাহলে:

```text
X shape
=
(4, 8)
```

প্রতিটি head:

```text
d_head = 8 / 2 = 4
```

তাই:

```text
Head 1 → (4,4)
Head 2 → (4,4)
```

Concatenate:

```text
(4,4) + (4,4)
=
(4,8)
```

তারপর output projection:

```text
(4,8)
```

---

# 13. Batch Dimension সহ

বাস্তবে input সাধারণত:

```text
(B, L, D)
```

যেখানে:

```text
B = batch size
L = sequence length
D = model dimension
```

ধরো:

```text
B = 32
L = 100
D = 128
H = 8
```

তাহলে:

```text
Input:
(32, 100, 128)
```

প্রতিটি head dimension:

```text
128 / 8 = 16
```

Heads:

```text
(32, 100, 16)
```

Conceptually multiple heads:

```text
Head 1 → (32,100,16)
Head 2 → (32,100,16)
...
Head 8 → (32,100,16)
```

---

# 14. Attention Score Shape

প্রতিটি head:

```text
Q = (B,L,d_head)

K = (B,L,d_head)
```

তাই:

```text
QKᵀ
```

এর shape:

```text
(B,L,L)
```

৮ heads একসাথে করলে:

```text
(B,H,L,L)
```

অর্থাৎ:

```text
(32,8,100,100)
```

---

# 15. Multi-Head Attention-এর Typical Shapes

Input:

```text
(B,L,D)
```

Projection-এর পরে:

```text
(B,L,H,d_head)
```

তারপর attention computation-এর জন্য সাধারণত rearrange:

```text
(B,H,L,d_head)
```

Attention scores:

```text
(B,H,L,L)
```

Attention output:

```text
(B,H,L,d_head)
```

তারপর transpose/reshape:

```text
(B,L,H,d_head)
```

Concatenate:

```text
(B,L,D)
```

শেষে output projection:

```text
(B,L,D)
```

---

# 16. Shape Flow — খুব গুরুত্বপূর্ণ

```text
Input
(B,L,D)
   ↓
Q,K,V projections
   ↓
(B,L,H,d_head)
   ↓
Transpose
   ↓
(B,H,L,d_head)
   ↓
QKᵀ
   ↓
(B,H,L,L)
   ↓
Softmax
   ↓
Attention × V
   ↓
(B,H,L,d_head)
   ↓
Transpose + Reshape
   ↓
(B,L,D)
   ↓
Output Projection
   ↓
(B,L,D)
```

Transformer implementation-এর জন্য এই shape flow অবশ্যই বুঝবে।

---

# 17. Single Head বনাম Multi-Head

### Single Head

```text
X
 ↓
Q K V
 ↓
Attention
 ↓
Output
```

### Multi-Head

```text
X
 │
 ├── Q₁ K₁ V₁ → Attention₁ ──┐
 ├── Q₂ K₂ V₂ → Attention₂ ──┤
 ├── Q₃ K₃ V₃ → Attention₃ ──┤
 └── Q₄ K₄ V₄ → Attention₄ ──┘
                              ↓
                          Concatenate
                              ↓
                         Linear Layer
                              ↓
                            Output
```

---

# 18. কেন Multiple Representation Useful?

ধরো:

```text
The bank approved the loan
```

একটি head হয়তো capture করতে পারে:

```text
bank → approved
```

আরেকটি:

```text
approved → loan
```

আরেকটি:

```text
the → bank
```

আরেকটি longer relationship।

এগুলো illustrative examples—actual learned heads সবসময় এভাবেই interpretable হবে এমন নয়।

---

# 19. Attention Head কি নির্দিষ্ট কাজ করে?

এটি একটি common misconception।

আমরা বলতে পারি:

> Different heads can learn different patterns.

কিন্তু:

> Head 1 = subject detector
> Head 2 = object detector

এভাবে fixed rule থাকে না।

Training-এর পরে attention patterns inspect করলে কিছু heads linguistic patterns-এর সাথে সম্পর্কিত মনে হতে পারে, কিন্তু এটি guaranteed specialization নয়।

---

# 20. Concatenation কী?

ধরো:

```text
Head 1:
[1,2]

Head 2:
[3,4]

Head 3:
[5,6]
```

Concatenate:

```text
[1,2,3,4,5,6]
```

অর্থাৎ:

```text
head₁
head₂
head₃
 ↓
Concat
```

একটি বড় representation তৈরি হয়।

---

# 21. Output Projection

Concatenation-এর পরে:

$$
Concat(head_1,\ldots,head_h)W^O
$$

করা হয়।

অর্থাৎ:

```text
Concatenated Representation
          ↓
       Wᴼ Linear
          ↓
      Final MHA Output
```

Output projection-এর কাজ হলো বিভিন্ন heads-এর information combine করে একটি unified representation তৈরি করতে সাহায্য করা।

---

# 22. PyTorch Implementation — Manual

এখন concept practically দেখি।

```python
import torch
import torch.nn as nn
import math


class MultiHeadAttention(nn.Module):

    def __init__(self, d_model, num_heads):
        super().__init__()

        assert d_model % num_heads == 0

        self.d_model = d_model
        self.num_heads = num_heads
        self.head_dim = d_model // num_heads

        self.W_q = nn.Linear(d_model, d_model)
        self.W_k = nn.Linear(d_model, d_model)
        self.W_v = nn.Linear(d_model, d_model)

        self.W_o = nn.Linear(d_model, d_model)

    def forward(self, x):

        batch_size, seq_len, _ = x.shape

        Q = self.W_q(x)
        K = self.W_k(x)
        V = self.W_v(x)

        Q = Q.view(
            batch_size,
            seq_len,
            self.num_heads,
            self.head_dim
        )

        K = K.view(
            batch_size,
            seq_len,
            self.num_heads,
            self.head_dim
        )

        V = V.view(
            batch_size,
            seq_len,
            self.num_heads,
            self.head_dim
        )

        Q = Q.transpose(1, 2)
        K = K.transpose(1, 2)
        V = V.transpose(1, 2)

        scores = Q @ K.transpose(-2, -1)

        scores = scores / math.sqrt(self.head_dim)

        weights = torch.softmax(
            scores,
            dim=-1
        )

        output = weights @ V

        output = output.transpose(1, 2)

        output = output.contiguous().view(
            batch_size,
            seq_len,
            self.d_model
        )

        output = self.W_o(output)

        return output
```

---

# 23. Test করি

```python
d_model = 128
num_heads = 8

model = MultiHeadAttention(
    d_model,
    num_heads
)

x = torch.randn(
    32,
    100,
    128
)

output = model(x)

print(output.shape)
```

Output:

```text
torch.Size([32, 100, 128])
```

অর্থাৎ:

```text
Input:
(32,100,128)

Output:
(32,100,128)
```

Transformer block-এর জন্য এই shape preservation খুব গুরুত্বপূর্ণ।

---

# 24. PyTorch Built-in Version

PyTorch-এ built-in layer আছে:

```python
import torch.nn as nn

attention = nn.MultiheadAttention(
    embed_dim=128,
    num_heads=8,
    batch_first=True
)
```

Input:

```python
x = torch.randn(32, 100, 128)
```

Self-attention:

```python
output, weights = attention(
    x,
    x,
    x
)
```

এখানে:

```text
Query = x
Key   = x
Value = x
```

তাই এটি self-attention।

---

# 25. Cross-Attention হলে?

যদি:

```python
output, weights = attention(
    query,
    key,
    value
)
```

এবং:

```text
query ≠ key/value
```

হয়, তাহলে এটি cross-attention হতে পারে।

Example:

```text
Decoder → Query
Encoder → Key/Value
```

---

# 26. Self-Attention বনাম Multi-Head Self-Attention

Self-attention:

```text
X
 ↓
Q K V
 ↓
One attention
 ↓
Output
```

Multi-head self-attention:

```text
X
 ↓
Q₁K₁V₁ → Head 1
Q₂K₂V₂ → Head 2
Q₃K₃V₃ → Head 3
...
 ↓
Concatenate
 ↓
Projection
 ↓
Output
```

---

# 27. Multi-Head Attention-এর Advantage

### 1. Multiple representation subspaces

Different heads বিভিন্ন learned projections ব্যবহার করে।

### 2. Multiple relationships

একসাথে বিভিন্ন token relationship capture করা সম্ভব।

### 3. Rich contextual representation

একাধিক attention outputs combine হয়।

### 4. Parallel computation

Heads parallelভাবে compute করা যায়।

---

# 28. Limitation

### 1. Computational cost

Attention matrix এখনও:

$$
O(L^2)
$$

### 2. Memory

প্রতিটি head-এর attention weights store করতে হয়।

### 3. More parameters

Multiple projection matrices থাকে।

### 4. Long context problem

Sequence খুব বড় হলে attention cost বড় হয়।

---

# 29. Complexity

Single-head self-attention-এর dominant attention computation:

$$
O(L^2D)
$$

Multi-head attention-এ heads ভাগ করলেও মোট dimension \(D\) একই scale-এ থাকলে overall dominant complexity সাধারণত একই order:

$$
O(L^2D)
$$

অর্থাৎ multiple heads নেওয়ার কারণে sequence-length quadratic problem চলে যায় না।

---

# 30. Memory Complexity

Attention matrix:

$$
(B,H,L,L)
$$

তাই sequence length বাড়লে memory দ্রুত বাড়ে।

যেমন:

```text
L = 100
→ 100 × 100
```

কিন্তু:

```text
L = 1000
→ 1000 × 1000
```

প্রতি head-এর জন্য অনেক বেশি attention values তৈরি হয়।

---

# 31. Multi-Head Attention + Positional Information

এখন একটা গুরুত্বপূর্ণ সমস্যা:

Self-attention:

```text
Token relationships
```

capture করে।

কিন্তু sequence order-এর information basic form-এ আলাদা করে দরকার।

তাই:

```text
Token Embedding
       +
Positional Information
       ↓
Multi-Head Self-Attention
```

পরের lesson-এ আমরা **Positional Encoding / Positional Embedding** বিস্তারিত শিখব।

---

# 32. Transformer-এর একটি Core Block

এখন আমরা Transformer-এর structure একটু দেখতে পারি:

```text
Input
  ↓
Multi-Head Self-Attention
  ↓
Add & Norm
  ↓
Feed Forward Network
  ↓
Add & Norm
  ↓
Output
```

এখন:

```text
Add & Norm
Feed Forward
```

এগুলো শুধু overview হিসেবে জানো।

Dedicated Transformer lesson-এ গভীরভাবে করব।

---

# 33. Residual Connection-এর Introduction

Transformer-এ attention-এর output সরাসরি discard করা হয় না।

Input-এর সাথে output যোগ করা হয়:

$$
Y = X + Attention(X)
$$

তারপর normalization।

Concept:

```text
       ┌─────────────────────┐
       │                     ↓
X ─────┼→ Multi-Head Attention
       │          ↓
       │        Output
       │          ↓
       └──────── Add
                  ↓
             LayerNorm
```

এটাকে **residual connection** বলা হয়।

পরের Transformer lesson-এ এটি বিস্তারিত হবে।

---

# 34. Multi-Head Attention + AI Writing Assistant

তোমার future AI writing platform-এ:

```text
User Text
   ↓
Tokenizer
   ↓
Embeddings
   ↓
Positional Information
   ↓
Multi-Head Self-Attention
   ↓
Contextual Representation
   ↓
Transformer Layers
   ↓
Task
```

Task হতে পারে:

```text
Rewrite
Classification
Summarization
Grammar Analysis
Semantic Analysis
Text Generation
```

---

# 35. Example — Rewrite Model

Input:

```text
The system is very useful for
analyzing large amounts of text.
```

Multi-head attention-এর মাধ্যমে representation-এর বিভিন্ন aspects model করতে পারে:

```text
system ↔ analyzing
large ↔ amounts
amounts ↔ text
useful ↔ system
```

তারপর Transformer layers আরও contextual processing করবে।

শেষে:

```text
Contextual Representation
        ↓
Language Modeling Head
        ↓
Generated Text
```

---

# 36. M02-এর Evolution এখন অনেক পরিষ্কার

```text
M02.15
Word Embeddings
      ↓
M02.16
Language Modeling
      ↓
M02.17
RNN
      ↓
M02.18
LSTM
      ↓
M02.19
GRU
      ↓
M02.20
Attention
      ↓
M02.21
Self-Attention
      ↓
M02.22
Multi-Head Attention
```

এখন আমরা Transformer-এর একদম কাছে।

---

# 37. তিনটি জিনিস আলাদা করে মনে রাখো

### Self-Attention

```text
Same sequence
→ Q,K,V
→ attention
```

### Multi-Head Attention

```text
Multiple attention heads
→ parallel attention
→ concatenate
→ output projection
```

### Cross-Attention

```text
Q ← one sequence
K,V ← another sequence
```

---

# 38. Full Mental Model

```text
                     INPUT X
                        │
        ┌───────────────┼───────────────┐
        ↓               ↓               ↓
      Head 1           Head 2          Head N
        │               │               │
     Q₁K₁V₁          Q₂K₂V₂          QₙKₙVₙ
        │               │               │
        ↓               ↓               ↓
   Attention₁      Attention₂      Attentionₙ
        │               │               │
        └───────────────┼───────────────┘
                        ↓
                   Concatenate
                        ↓
                   Linear Wᴼ
                        ↓
                    MHA Output
```

---

# 39. সবচেয়ে গুরুত্বপূর্ণ Formula

### Per-head:

$$
head_i =
softmax
\left(
\frac{
(QW_i^Q)(KW_i^K)^T
}{
\sqrt{d_k}
}
\right)
(VW_i^V)
$$

### Multi-head:

$$
MultiHead(Q,K,V)
=
Concat(head_1,\ldots,head_h)W^O
$$

এগুলো বুঝে রাখলে Transformer implementation অনেক সহজ হবে।

---

# 40. Practice — Beginner

### Task 1

Multi-Head Attention কী?

### Task 2

কেন multiple heads ব্যবহার করা হয়?

### Task 3

একটি head কী?

### Task 4

`d_model = 512`, `num_heads = 8` হলে:

```text
d_head = ?
```

### Task 5

Single-head এবং multi-head attention-এর পার্থক্য লেখো।

---

# 41. Practice — Intermediate

ধরো:

```text
Batch = 16
Sequence Length = 100
d_model = 256
num_heads = 8
```

Calculate:

```text
d_head
Q shape
K shape
V shape
Attention score shape
Concatenated output shape
Final output shape
```

---

# 42. Practice — Advanced

Sentence:

```text
The student submitted the project
because he completed it yesterday.
```

Explain:

1. কোন ধরনের relationship একটি head capture করতে পারে?
2. Multiple heads কেন useful?
3. `he` এবং `student` relationship কীভাবে contextual attention-এর মাধ্যমে model করা যেতে পারে?
4. `it` এবং `project` relationship-এর ক্ষেত্রে কী হতে পারে?
5. Causal mask দিলে কী পরিবর্তন হবে?

---

# 43. Theory Questions

1. What is Multi-Head Attention?
2. What is an attention head?
3. Why do Transformers use multiple heads?
4. What is \(W_i^Q\)?
5. What is \(W_i^K\)?
6. What is \(W_i^V\)?
7. What is \(W^O\)?
8. Why are Q/K/V projections different for each head?
9. What is `d_model`?
10. What is `d_head`?
11. Why is `d_model` usually divisible by `num_heads`?
12. What happens after each head computes attention?
13. What is concatenation?
14. Why is output projection required?
15. What is the shape of attention weights?
16. Why is the attention matrix `(L,L)`?
17. What is the shape `(B,H,L,L)`?
18. Multi-head vs single-head attention?
19. Self-attention vs multi-head self-attention?
20. Multi-head attention vs cross-attention?
21. Does every head necessarily learn a specific linguistic role?
22. What is the complexity of multi-head self-attention?
23. Why doesn't multi-head attention solve the quadratic complexity problem?
24. Why is positional information needed?
25. What is residual connection?

---

# 44. Interview Questions

### Q1. Why do we need multiple heads?

> Multiple heads allow the model to learn and combine different attention patterns in different learned representation subspaces.

### Q2. If `d_model = 512` and `num_heads = 8`, what is head dimension?

$$
512/8=64
$$

### Q3. What is the output shape?

If:

```text
Input = (B,L,D)
```

then standard MHA with matching model dimension produces:

```text
(B,L,D)
```

### Q4. What is the attention-weight shape?

For:

```text
B = batch
H = heads
L = sequence length
```

the conceptual attention-weight tensor is:

```text
(B,H,L,L)
```

### Q5. Does each head perform the same attention?

No. Each head generally has its own learned Q/K/V projections and can learn different patterns.

### Q6. What happens after concatenating heads?

The concatenated representation is passed through an output projection \(W^O\).

### Q7. What is the biggest computational limitation?

Standard self-attention still has quadratic dependence on sequence length:

$$
O(L^2D)
$$

---

# 45. M02.22 Completion Checklist

* [x] Multi-Head Attention definition
* [x] Motivation
* [x] Attention Head
* [x] Single-head vs multi-head
* [x] Q/K/V projections
* [x] Per-head attention
* [x] Head dimension
* [x] `d_model`
* [x] `num_heads`
* [x] Dimension splitting
* [x] Attention score
* [x] Scaling
* [x] Softmax
* [x] Attention weights
* [x] Value aggregation
* [x] Concatenation
* [x] Output projection
* [x] \(W^Q,W^K,W^V,W^O\)
* [x] Tensor shapes
* [x] Batch/head/sequence dimensions
* [x] `(B,H,L,L)` attention shape
* [x] Self-attention connection
* [x] Cross-attention connection
* [x] Causal masking connection
* [x] Positional information motivation
* [x] Residual connection introduction
* [x] Computational complexity
* [x] PyTorch manual implementation
* [x] PyTorch built-in implementation
* [x] AI Writing Assistant connection
* [x] Theory questions
* [x] Interview questions

---

# 🧠 Final Mental Model

এক লাইনে:

```text
Multi-Head Attention
=
একই input-এর উপর
multiple learned attention mechanisms
চালিয়ে তাদের information combine করা।
```

আর architecture:

```text
                    X
                    │
          ┌─────────┼─────────┐
          ↓         ↓         ↓
        Head 1    Head 2    Head N
          ↓         ↓         ↓
      Attention Attention Attention
          ↓         ↓         ↓
          └─────────┼─────────┘
                    ↓
               Concatenate
                    ↓
                Linear Wᴼ
                    ↓
                  Output
```

এখন আমাদের Transformer-এর জন্য পরবর্তী অত্যন্ত গুরুত্বপূর্ণ foundation হলো:

**M02.23 — Positional Encoding & Positional Embedding Deep Dive**

এখানে আমরা শিখব **Transformer কীভাবে token-এর order/position বুঝে**, কেন শুধু self-attention যথেষ্ট নয়, **Sinusoidal Positional Encoding**, **Learned Positional Embedding**, formulas, shapes এবং PyTorch implementation।


---
# M02.23 — Positional Encoding & Positional Embedding Deep Dive

M02.22-এ আমরা **Multi-Head Attention** শিখেছি। এখন Transformer-এর একটি fundamental problem solve করব:

> **Transformer কীভাবে বুঝবে কোন token আগে, কোন token পরে?**

এটাই **Positional Information**-এর বিষয়।

আমাদের progression এখন:

```text
M02.19 → GRU
M02.20 → Attention
M02.21 → Self-Attention
M02.22 → Multi-Head Attention
M02.23 → Positional Encoding & Positional Embedding ← আজ
M02.24 → Transformer Architecture
```

---

# 1. মূল সমস্যা: Self-Attention কি Position জানে?

ধরো:

```text
I love NLP
```

Tokens:

```text
I      → position 0
love   → position 1
NLP    → position 2
```

Self-attention tokenগুলোর মধ্যে relationship তৈরি করতে পারে।

কিন্তু basic self-attention-এর কাছে আলাদাভাবে position information না দিলে:

```text
I love NLP
```

এবং

```text
NLP love I
```

এর token representations একই ধরনের set হিসেবে দেখা যেতে পারে, কারণ attention operation নিজে recurrence-এর মতো sequential order encode করে না।

তাই Transformer-এ position information দরকার।

---

# 2. RNN-এর ক্ষেত্রে সমস্যা ছিল না কেন?

RNN naturally sequence order follow করে:

```text
x₁
 ↓
h₁
 ↓
x₂
 ↓
h₂
 ↓
x₃
 ↓
h₃
```

তাই RNN জানে:

```text
x₁ → আগে
x₂ → পরে
x₃ → আরও পরে
```

কিন্তু Transformer:

```text
x₁
x₂
x₃
x₄
 ↓
Self-Attention
```

parallelভাবে process করতে পারে।

তাই আলাদাভাবে position দিতে হয়।

---

# 3. Positional Information কী?

সহজভাবে:

> **প্রতিটি token sequence-এর কোথায় অবস্থান করছে, সেই information model-কে দেওয়াই positional information।**

যেমন:

```text
The    → position 0
student → position 1
reads  → position 2
Python → position 3
```

---

# 4. Token Embedding বনাম Positional Information

আমরা আগে শিখেছি:

```text
Token
 ↓
Token ID
 ↓
Embedding
 ↓
Vector
```

এখন:

```text
Token Embedding
       +
Position Information
       ↓
Transformer Input
```

অর্থাৎ:

$$
X = E + P
$$

যেখানে:

```text
E = Token Embedding
P = Positional Representation
X = Transformer input
```

---

# 5. কেন যোগ করা হয়?

ধরো:

```text
Token Embedding:
E
```

এবং:

```text
Position Embedding:
P
```

তাহলে:

$$
X=E+P
$$

এর ফলে একই vector space-এর মধ্যে:

```text
What is the token?
+
Where is the token?
```

দুটো information থাকে।

---

# 6. Example

ধরো:

```text
word = "cat"
```

Token embedding:

```text
cat → [0.2, 0.7, 0.1, 0.5]
```

Position 2-এর positional vector:

```text
position 2
→ [0.1, 0.3, 0.4, 0.2]
```

যোগ করলে:

```text
[0.2, 0.7, 0.1, 0.5]
+
[0.1, 0.3, 0.4, 0.2]
-------------------
[0.3, 1.0, 0.5, 0.7]
```

Transformer এই combined representation ব্যবহার করবে।

---

# 7. দুই ধরনের Positional Representation

সবচেয়ে গুরুত্বপূর্ণ দুইটি approach:

```text
Positional Information
       │
       ├── Positional Encoding
       │
       └── Positional Embedding
```

### Positional Encoding

সাধারণত fixed mathematical function দিয়ে position representation তৈরি করা হয়।

Classic Transformer-এ:

> **Sinusoidal Positional Encoding**

ব্যবহার করা হয়েছিল।

### Positional Embedding

Position-এর জন্য trainable vectors রাখা হয়।

```text
position 0 → learned vector
position 1 → learned vector
position 2 → learned vector
...
```

---

# 8. Sinusoidal Positional Encoding

Original Transformer paper-এ sinusoidal encoding ব্যবহার করা হয়েছিল।

দুইটি formula:

$$
PE(pos,2i)
=
\sin
\left(
\frac{pos}{10000^{2i/d_{model}}}
\right)
$$

$$
PE(pos,2i+1)
=
\cos
\left(
\frac{pos}{10000^{2i/d_{model}}}
\right)
$$

এখানে:

```text
pos       = token position
i         = dimension index
d_model   = model dimension
```

---

# 9. Even এবং Odd Dimensions

Formula-টা সহজভাবে:

```text
Even dimension
→ sin

Odd dimension
→ cos
```

যেমন:

```text
dimension 0 → sin
dimension 1 → cos
dimension 2 → sin
dimension 3 → cos
dimension 4 → sin
dimension 5 → cos
```

---

# 10. কেন Sine এবং Cosine?

Sine/cosine functions-এর কিছু useful mathematical properties আছে:

* periodic structure
* different frequencies
* relative positional relationships encode করার সুযোগ
* fixed representation
* training-এর জন্য extra position parameters দরকার হয় না

তাই বিভিন্ন position-এর জন্য unique patterns তৈরি করা যায়।

---

# 11. Positional Encoding Matrix

ধরো:

```text
sequence length = 4
d_model = 6
```

তাহলে:

$$
PE \in \mathbb{R}^{4\times6}
$$

Conceptually:

```text
          dimensions
       0  1  2  3  4  5

pos 0  [•  •  •  •  •  •]
pos 1  [•  •  •  •  •  •]
pos 2  [•  •  •  •  •  •]
pos 3  [•  •  •  •  •  •]
```

প্রতিটি row একটি position-এর representation।

---

# 12. Position 0

যখন:

```text
pos = 0
```

তখন:

$$
\sin(0)=0
$$

এবং:

$$
\cos(0)=1
$$

তাই position 0-এর vector নির্দিষ্ট pattern পাবে।

---

# 13. Position 1

যখন:

```text
pos = 1
```

তখন sine/cosine values পরিবর্তিত হবে।

```text
position 0
→ pattern A

position 1
→ pattern B

position 2
→ pattern C
```

এভাবে প্রতিটি position আলাদা representation পায়।

---

# 14. Different Frequencies

Sinusoidal encoding-এর সবচেয়ে interesting বিষয়:

সব dimension একই frequency ব্যবহার করে না।

কিছু dimension দ্রুত পরিবর্তিত হয়:

```text
~~~~~~~
```

কিছু ধীরে:

```text
~    ~    ~
```

আরও কিছু আরও ধীরে:

```text
~         ~
```

তাই model বিভিন্ন scale-এর positional patterns পেতে পারে।

---

# 15. কেন Different Frequencies?

ধরো sentence length অনেক বড়।

যদি সব dimension একই periodic pattern ব্যবহার করত, position distinguish করা কঠিন হতে পারত।

Different frequencies:

```text
Fast frequency
+
Medium frequency
+
Slow frequency
+
Very slow frequency
```

combine করে richer positional signature তৈরি করে।

---

# 16. Positional Encoding-এর একটি Mental Model

```text
Position
   ↓
Mathematical Functions
   ↓
Sin/Cos Patterns
   ↓
Position Vector
   ↓
+
Token Embedding
   ↓
Transformer Input
```

---

# 17. Learned Positional Embedding

আরেকটি approach হলো position vectors trainable করা।

ধরো:

```text
max_length = 100
embedding_dim = 128
```

তাহলে একটি positional embedding matrix:

$$
P \in \mathbb{R}^{100\times128}
$$

থাকতে পারে।

```text
Position 0  → learned vector
Position 1  → learned vector
Position 2  → learned vector
...
Position 99 → learned vector
```

Training-এর সময় এগুলো update হয়।

---

# 18. Learned Positional Embedding কীভাবে কাজ করে?

ধরো:

```text
Token:
cat

Position:
5
```

Token embedding:

```text
E(cat)
```

Position embedding:

```text
P(5)
```

তারপর:

$$
X=E(cat)+P(5)
$$

---

# 19. Sinusoidal বনাম Learned

| Sinusoidal                     | Learned                                 |
| ------------------------------ | --------------------------------------- |
| Fixed                          | Trainable                               |
| Formula-based                  | Parameters শেখে                         |
| Extra position parameters নেই  | Extra parameters আছে                    |
| Original Transformer-এ ব্যবহৃত | অনেক Transformer architecture-এ ব্যবহৃত |
| নির্দিষ্ট mathematical pattern | Data থেকে pattern শেখে                  |

---

# 20. Positional Encoding বনাম Positional Embedding

Terminology নিয়ে confusion হয়।

Strictly speaking:

```text
Encoding
→ usually fixed/generated representation

Embedding
→ usually learned vector representation
```

তবে literature-এ অনেক সময় দুটো term loosely ব্যবহার করা হয়।

তাই context দেখে বুঝতে হবে কোন implementation-এর কথা বলা হচ্ছে।

---

# 21. PyTorch — Sinusoidal Positional Encoding

একটি basic implementation:

```python
import torch
import math


def positional_encoding(seq_len, d_model):

    pe = torch.zeros(seq_len, d_model)

    position = torch.arange(
        0,
        seq_len,
        dtype=torch.float
    ).unsqueeze(1)

    div_term = torch.exp(
        torch.arange(
            0,
            d_model,
            2
        ).float()
        * (-math.log(10000.0) / d_model)
    )

    pe[:, 0::2] = torch.sin(
        position * div_term
    )

    pe[:, 1::2] = torch.cos(
        position * div_term
    )

    return pe
```

---

# 22. Test

```python
pe = positional_encoding(
    seq_len=10,
    d_model=8
)

print(pe.shape)
```

Output:

```text
torch.Size([10, 8])
```

অর্থাৎ:

```text
10 positions
×
8 dimensions
```

---

# 23. Visualize করার ধারণা

তুমি চাইলে positional encoding-এর matrix heatmap হিসেবে visualize করতে পারো।

```text
Position
   ↑
   │
   │
   │
   └────────────→ Dimension
```

Different sine/cosine frequencies-এর কারণে বিভিন্ন pattern দেখা যাবে।

---

# 24. Token Embedding + Positional Encoding

ধরো:

```text
batch = 32
sequence = 100
d_model = 128
```

Token embeddings:

```text
(32,100,128)
```

Positional encoding:

```text
(100,128)
```

Broadcasting-এর মাধ্যমে:

```text
(32,100,128)
+
(100,128)
```

ফল:

```text
(32,100,128)
```

অর্থাৎ batch-এর প্রতিটি sequence-এর জন্য একই position encoding pattern ব্যবহার করা যেতে পারে।

---

# 25. Broadcasting এখানে কী করছে?

M01-এ Python/NumPy broadcasting-এর concept পড়েছিলে।

এখানে:

```text
Embedding
(32,100,128)

Position
(100,128)
```

Position tensor batch dimension-এ broadcast হতে পারে:

```text
(1,100,128)
```

তারপর:

```text
(32,100,128)
+
(1,100,128)
```

ফল:

```text
(32,100,128)
```

এটি Transformer implementation-এ গুরুত্বপূর্ণ tensor operation।

---

# 26. Learned Positional Embedding — PyTorch

PyTorch-এ:

```python
import torch
import torch.nn as nn


max_len = 100
d_model = 128

position_embedding = nn.Embedding(
    max_len,
    d_model
)
```

Position IDs:

```python
positions = torch.arange(100)

print(positions.shape)
```

Output:

```text
torch.Size([100])
```

তারপর:

```python
pos_vectors = position_embedding(
    positions
)

print(pos_vectors.shape)
```

Output:

```text
torch.Size([100, 128])
```

---

# 27. Token Embedding + Learned Position

```python
vocab_size = 10000
max_len = 100
d_model = 128

token_embedding = nn.Embedding(
    vocab_size,
    d_model
)

position_embedding = nn.Embedding(
    max_len,
    d_model
)
```

Input:

```python
tokens = torch.randint(
    0,
    vocab_size,
    (32, 100)
)
```

Position IDs:

```python
positions = torch.arange(
    100
).unsqueeze(0)
```

Shape:

```text
positions
→ (1,100)
```

Embedding:

```python
x = token_embedding(tokens)

p = position_embedding(positions)
```

Shapes:

```text
x → (32,100,128)
p → (1,100,128)
```

তারপর:

```python
x = x + p
```

Result:

```text
(32,100,128)
```

---

# 28. কেন Position Embedding Token-এর সাথে Add করা হয়?

কারণ Transformer layer-এর input-এর মধ্যে দুটো information দরকার:

```text
Semantic Information
+
Positional Information
```

অর্থাৎ:

```text
What?
+
Where?
```

---

# 29. একটি Important Question

### কেন concatenate করা হয় না?

Technically concatenate করাও possible architecture design হতে পারে, কিন্তু standard Transformer-এ সাধারণত embedding এবং positional representation **add** করা হয়।

কারণ:

```text
E → d_model
P → d_model

E + P → d_model
```

Model dimension একই থাকে।

যদি concatenate করি:

```text
E → d_model
P → d_model

E + P → 2 × d_model
```

তাহলে downstream architecture পরিবর্তন করতে হবে।

Addition dimension preserve করে।

---

# 30. Position কি Absolute?

Classic sinusoidal এবং learned positional embeddings সাধারণত **absolute position** represent করে।

যেমন:

```text
position 0
position 1
position 2
...
```

কিন্তু language understanding-এ relative distance-ও গুরুত্বপূর্ণ:

```text
token A
   ↓
3 positions later
   ↓
token B
```

এই concept থেকে পরে আসে:

> **Relative Positional Encoding**

---

# 31. Relative Position

ধরো:

```text
The student reads Python
```

`student` থেকে:

```text
reads → +1
Python → +2
```

এখানে absolute position:

```text
student = 1
reads = 2
Python = 3
```

কিন্তু relative position:

```text
student → reads = +1
student → Python = +2
```

কিছু architecture relative positional relationships explicitly model করে।

---

# 32. Rotary Positional Embedding — RoPE

Modern LLMs-এর context-এ একটি অত্যন্ত গুরুত্বপূর্ণ technique:

> **RoPE — Rotary Positional Embedding**

এটি traditional sinusoidal addition-এর মতো শুধু position vector add না করে Q/K representations-এর মধ্যে positional information incorporate করে rotation ব্যবহার করে।

High-level:

```text
Token Representation
       ↓
Q / K
       ↓
Position-dependent Rotation
       ↓
Attention
```

RoPE বিশেষভাবে modern decoder-only Transformer architectures-এ গুরুত্বপূর্ণ।

এটি আমরা Transformer/LLM অংশে dedicatedভাবে আরও গভীরভাবে করব।

---

# 33. ALiBi — Another Approach

আরেকটি positional technique:

> **ALiBi — Attention with Linear Biases**

এখানে positional information embedding-এর সাথে যোগ করার বদলে attention scores-এ position-dependent bias যোগ করা হয়।

Concept:

```text
QKᵀ
 ↓
Position-based Bias
 ↓
Softmax
 ↓
Attention
```

এটি দেখায় যে positional information দেওয়ার একাধিক design আছে।

---

# 34. Modern Positional Methods — Big Picture

```text
Positional Information
       │
       ├── Sinusoidal Encoding
       │
       ├── Learned Positional Embedding
       │
       ├── Relative Position Methods
       │
       ├── RoPE
       │
       └── ALiBi
```

আমাদের foundation-এর জন্য প্রথমে classic approaches ভালোভাবে বুঝতে হবে।

---

# 35. কেন GPT-তে Position দরকার?

GPT autoregressive model:

```text
I
 ↓
I love
 ↓
I love machine
 ↓
I love machine learning
```

Token order খুব গুরুত্বপূর্ণ।

```text
I love you
```

এবং:

```text
You love I
```

একই token set হলেও meaning আলাদা।

তাই GPT-style Transformer-এ positional information গুরুত্বপূর্ণ।

---

# 36. BERT-এ Position

BERT-ও Transformer architecture ব্যবহার করে।

তাই:

```text
Token Embedding
+
Position Information
```

দরকার হয়।

BERT-এর original architecture learned positional embeddings ব্যবহার করেছিল।

---

# 37. Attention + Position

M02.22:

```text
Multi-Head Self-Attention
```

কিন্তু basic self-attention জানে না token order।

তাই:

```text
Token Embedding
+
Positional Information
       ↓
Multi-Head Self-Attention
```

এটাই Transformer input-এর একটি fundamental pattern।

---

# 38. Complete Transformer Input

```text
Raw Text
   ↓
Tokenizer
   ↓
Token IDs
   ↓
Token Embedding
   ↓
+
Positional Information
   ↓
Transformer
   ↓
Multi-Head Attention
```

---

# 39. Important Tensor Shapes

ধরো:

```text
B = 32
L = 128
D = 512
```

Token embedding:

```text
(32,128,512)
```

Sinusoidal position encoding:

```text
(128,512)
```

Broadcast:

```text
(1,128,512)
```

Addition:

```text
(32,128,512)
+
(1,128,512)
```

Result:

```text
(32,128,512)
```

---

# 40. Maximum Sequence Length

Learned positional embedding-এ সাধারণত একটি maximum length থাকে।

যেমন:

```text
max_len = 512
```

তাহলে:

```text
position 0 → available
...
position 511 → available
```

কিন্তু:

```text
position 512
```

সরাসরি learned table-এ নাও থাকতে পারে।

তাই learned absolute position embeddings-এর ক্ষেত্রে context length limitation গুরুত্বপূর্ণ।

---

# 41. Sinusoidal-এর একটি সুবিধা

Sinusoidal encoding fixed mathematical function হওয়ায় theoretically training-এর সময় দেখা না হওয়া larger positions-এর encoding generate করা যায়।

তবে এর অর্থ এই নয় যে model unlimited context perfectly বুঝতে পারবে।

Actual model architecture, training distribution, attention cost এবং implementation limitations গুরুত্বপূর্ণ।

---

# 42. Positional Information ≠ Context

এগুলো আলাদা:

```text
Positional Information
→ token কোথায়?

Contextual Representation
→ surrounding tokens দেখে token-এর representation কীভাবে বদলাবে?
```

Self-attention:

```text
Context
```

তৈরি করতে সাহায্য করে।

Position encoding:

```text
Order
```

সম্পর্কে information দেয়।

দুটো একসাথে:

```text
Position
+
Context
```

Transformer-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 43. AI Writing Assistant-এর ক্ষেত্রে

তোমার future AI writing platform-এর জন্য position অত্যন্ত গুরুত্বপূর্ণ।

ধরো:

```text
The model improves writing quality.
```

Order:

```text
The
 ↓
model
 ↓
improves
 ↓
writing
 ↓
quality
```

যদি order হারিয়ে যায়:

```text
quality writing improves model The
```

তাহলে sentence structure/meaning dramatically পরিবর্তিত হয়।

তাই:

```text
Token Embedding
+
Position
+
Self-Attention
```

একসাথে language representation তৈরি করে।

---

# 44. Text Generation-এ Position

ধরো model generate করছে:

```text
The
```

তারপর:

```text
The student
```

তারপর:

```text
The student is
```

তারপর:

```text
The student is learning
```

প্রতিটি token-এর sequence position গুরুত্বপূর্ণ।

```text
The       → position 0
student   → position 1
is        → position 2
learning  → position 3
```

---

# 45. Self-Attention + Position — Full Flow

```text
                 TEXT
                   ↓
                Tokenizer
                   ↓
                Token IDs
                   ↓
             Token Embedding
                   │
                   +
                   │
         Positional Information
                   ↓
              Input X
                   ↓
        Multi-Head Self-Attention
                   ↓
            Contextual Output
```

---

# 46. Common Mistakes

### Mistake 1

> Positional encoding = token embedding

❌ ভুল।

```text
Token Embedding
→ token identity/semantic representation

Positional Encoding
→ position information
```

---

### Mistake 2

> Self-attention automatically understands word order.

❌ Basic self-attention-এর জন্য explicit positional mechanism দরকার।

---

### Mistake 3

> Positional encoding always learned.

❌ না।

Sinusoidal encoding fixed হতে পারে।

---

### Mistake 4

> Positional embedding always sinusoidal.

❌ না।

Learned positional embedding আলাদা approach।

---

### Mistake 5

> Position information alone gives semantics.

❌ না।

Position শুধু location/order information দেয়।

---

# 47. Practical Mini Implementation

একটি simple Transformer input:

```python
import torch
import torch.nn as nn


batch_size = 4
seq_len = 20
d_model = 64
vocab_size = 5000

token_embedding = nn.Embedding(
    vocab_size,
    d_model
)

position_embedding = nn.Embedding(
    seq_len,
    d_model
)

tokens = torch.randint(
    0,
    vocab_size,
    (batch_size, seq_len)
)

positions = torch.arange(
    seq_len
).unsqueeze(0)

token_vectors = token_embedding(tokens)

position_vectors = position_embedding(positions)

x = token_vectors + position_vectors

print("Token:", token_vectors.shape)
print("Position:", position_vectors.shape)
print("Input:", x.shape)
```

Expected:

```text
Token:    torch.Size([4, 20, 64])
Position: torch.Size([1, 20, 64])
Input:    torch.Size([4, 20, 64])
```

---

# 48. Transformer-এর আগে এখন কী কী জানা হলো?

আমাদের foundation:

```text
Embedding
    ↓
Language Modeling
    ↓
RNN
    ↓
LSTM
    ↓
GRU
    ↓
Attention
    ↓
Self-Attention
    ↓
Multi-Head Attention
    ↓
Positional Information
```

এখন আমরা Transformer architecture-এর জন্য প্রায় ready।

---

# 49. Next Step

পরবর্তী:

# **M02.24 — Transformer Architecture Deep Dive**

সেখানে আমরা একসাথে দেখব:

```text
Transformer
│
├── Input Embedding
├── Positional Encoding
├── Multi-Head Self-Attention
├── Residual Connection
├── Layer Normalization
├── Feed Forward Network
├── Encoder Block
├── Decoder Block
├── Masked Self-Attention
├── Cross-Attention
├── Add & Norm
├── Stacking Transformer Blocks
└── Full Transformer
```

তারপর ধাপে ধাপে:

```text
Transformer
 ↓
BERT
 ↓
GPT
 ↓
Decoder-only Transformer
 ↓
LLM Architecture
```

---

# 50. Theory Questions

1. What is positional information?
2. Why does Transformer need positional information?
3. Why doesn't basic self-attention inherently encode sequence order?
4. What is positional encoding?
5. What is positional embedding?
6. What is sinusoidal positional encoding?
7. Write the sinusoidal positional encoding equations.
8. Why are sine and cosine used?
9. Why are different frequencies used?
10. What is `d_model`?
11. What does `pos` represent?
12. What does `i` represent?
13. What is learned positional embedding?
14. Sinusoidal vs learned positional embedding?
15. Why are token embedding and positional representation added?
16. Why not concatenate them in the standard Transformer?
17. What is absolute positional encoding?
18. What is relative positional information?
19. What is RoPE?
20. What is ALiBi?
21. Why is positional information important for GPT?
22. Why is positional information important for BERT?
23. What is the shape of positional encoding?
24. How does broadcasting work when adding position encoding?
25. What happens if positional information is removed?

---

# 51. Interview Questions

### Q1. Why does Transformer need positional encoding?

> Because self-attention processes token relationships without the sequential recurrence of RNNs, so explicit positional information is needed to represent token order.

### Q2. What is the original Transformer positional encoding?

> Fixed sinusoidal positional encoding.

### Q3. Formula?

$$
PE(pos,2i)
=
\sin
\left(
\frac{pos}{10000^{2i/d_{model}}}
\right)
$$

$$
PE(pos,2i+1)
=
\cos
\left(
\frac{pos}{10000^{2i/d_{model}}}
\right)
$$

### Q4. Difference between positional encoding and positional embedding?

> Positional encoding commonly refers to a fixed/generated position representation, while positional embedding commonly refers to trainable position vectors. Terminology can vary across papers and implementations.

### Q5. Why add position to token embedding?

> Addition preserves the model dimension while combining token identity information with position information.

### Q6. What is RoPE?

> Rotary Positional Embedding incorporates positional information by applying position-dependent rotations to query/key representations.

### Q7. Does positional encoding provide semantic meaning?

> No. It provides positional/order information; semantic/contextual representations come from token representations and model computation such as attention.

---

# 52. Practice Tasks

### Beginner

Explain:

```text
Token Embedding
+
Positional Encoding
```

কেন দরকার?

---

### Intermediate

ধরো:

```text
batch = 16
sequence_length = 100
d_model = 256
```

Find:

```text
Token Embedding shape
Sinusoidal PE shape
Broadcasted PE shape
Final Transformer input shape
```

---

### Advanced

Sentence:

```text
The student reads a book.
```

Compare:

```text
The student reads a book.
```

and:

```text
A book reads the student.
```

ব্যাখ্যা করো কেন token set-এর similarity থাকলেও position/order information অত্যন্ত গুরুত্বপূর্ণ।

---

# 53. M02.23 Completion Checklist

* [x] Positional Information
* [x] Why Transformer needs position
* [x] RNN vs Transformer order handling
* [x] Token Embedding
* [x] Positional Encoding
* [x] Positional Embedding
* [x] Token + Position addition
* [x] Sinusoidal Encoding
* [x] Sine
* [x] Cosine
* [x] Even/Odd dimensions
* [x] Sinusoidal formula
* [x] Different frequencies
* [x] Position matrix
* [x] Learned Positional Embedding
* [x] Sinusoidal vs Learned
* [x] Tensor shapes
* [x] Broadcasting
* [x] Maximum sequence length
* [x] Absolute position
* [x] Relative position introduction
* [x] RoPE introduction
* [x] ALiBi introduction
* [x] GPT connection
* [x] BERT connection
* [x] AI Writing Assistant connection
* [x] PyTorch implementation
* [x] Common mistakes
* [x] Theory questions
* [x] Interview questions
* [x] Practice tasks

---

# 🧠 Final Mental Model

সবচেয়ে গুরুত্বপূর্ণ:

```text
TOKEN
  ↓
Token ID
  ↓
Token Embedding
  ↓
"What does this token represent?"
  +
Positional Information
  ↓
"Where is this token?"
  ↓
Transformer Input
  ↓
Multi-Head Self-Attention
  ↓
Contextual Representation
```

আর:

```text
RNN
→ sequence order naturally follows recurrence

Transformer
→ parallel attention
→ therefore explicit positional information is needed
```

এখন পর্যন্ত আমাদের evolution:

```text
Embedding
   ↓
RNN
   ↓
LSTM
   ↓
GRU
   ↓
Attention
   ↓
Self-Attention
   ↓
Multi-Head Attention
   ↓
Positional Encoding
   ↓
⭐ Transformer
```

**M02.23 — Positional Encoding & Positional Embedding complete.**


----
# M02.24 — Transformer Architecture Deep Dive

আজ আমরা **NLP Foundation-এর সবচেয়ে গুরুত্বপূর্ণ milestone**-এ ঢুকছি:

> **Transformer Architecture**

M02.20–M02.23 পর্যন্ত তুমি Attention → Self-Attention → Multi-Head Attention → Positional Encoding শিখেছ। এখন এগুলোকে একসাথে নিয়ে **একটি complete Transformer** কীভাবে কাজ করে সেটা বুঝব।

---

# 1. Transformer কী?

**Transformer** হলো একটি neural network architecture যা মূলত sequence/text processing-এর জন্য তৈরি করা হয়েছিল এবং যার মূল building block হলো **Attention**।

2017 সালে paper:

> **“Attention Is All You Need”**

Transformer-এর সবচেয়ে গুরুত্বপূর্ণ বৈশিষ্ট্য:

```text
RNN/LSTM:
Token 1 → Token 2 → Token 3 → Token 4
             sequential processing

Transformer:
Token 1 ─┐
Token 2 ─┼──→ Self-Attention
Token 3 ─┤
Token 4 ─┘
             parallel processing
```

অর্থাৎ Transformer sequential recurrence-এর পরিবর্তে **attention-based parallel processing** ব্যবহার করে।

---

# 2. কেন Transformer প্রয়োজন হলো?

Transformer বোঝার আগে RNN/LSTM-এর সমস্যা মনে করতে হবে।

### RNN

```text
x1 → h1 → x2 → h2 → x3 → h3 → x4 → h4
```

প্রতিটি timestep আগের hidden state-এর উপর নির্ভর করে।

ফলে:

* parallelization কঠিন
* long sequence ধীর
* long-term dependency সমস্যা
* দূরের token-এর relationship শেখা কঠিন

---

# 3. LSTM কিছু সমস্যা সমাধান করলেও...

LSTM:

```text
x1 → LSTM → x2 → LSTM → x3 → LSTM → x4
```

Vanishing gradient সমস্যা কমায়।

কিন্তু:

```text
Token 1
   ↓
Token 2
   ↓
Token 3
   ↓
...
Token 100
```

Sequence processing এখনো fundamentally sequential।

---

# 4. Transformer-এর মূল ধারণা

Transformer বলে:

> "প্রতিটি token-এর অন্য token-এর সাথে relationship সরাসরি attention-এর মাধ্যমে বের করি।"

উদাহরণ:

```text
The animal didn't cross the street because it was tired.
```

এখানে:

```text
it → animal
```

Self-attention `it` token-কে sentence-এর অন্য tokenগুলোর দিকে তাকিয়ে relevant information বের করতে পারে।

---

# 5. Original Transformer Architecture

Original Transformer ছিল:

```text
                 TRANSFORMER
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
       ENCODER               DECODER
          │                     │
     Understand input      Generate output
```

Complete architecture:

```text
                INPUT
                  │
           Token Embedding
                  │
        Positional Encoding
                  │
                  ▼
        ┌─────────────────┐
        │    ENCODER      │
        │                 │
        │ Self-Attention  │
        │       ↓         │
        │ Add & Norm      │
        │       ↓         │
        │      FFN        │
        │       ↓         │
        │ Add & Norm      │
        └────────┬────────┘
                 │
                 │ Encoder Output
                 ▼
        ┌─────────────────┐
        │    DECODER      │
        │                 │
        │ Masked          │
        │ Self-Attention  │
        │       ↓         │
        │ Add & Norm      │
        │       ↓         │
        │ Cross Attention │◄──── Encoder Output
        │       ↓         │
        │ Add & Norm      │
        │       ↓         │
        │      FFN        │
        │       ↓         │
        │ Add & Norm      │
        └────────┬────────┘
                 │
                 ▼
          Linear Projection
                 │
                 ▼
              Softmax
                 │
                 ▼
             Output
```

এটাই আজকের মূল lesson।

---

# 6. Transformer-এর প্রধান components

একটি Transformer-এ গুরুত্বপূর্ণ components:

```text
1. Tokenization
2. Token Embedding
3. Positional Encoding
4. Multi-Head Self-Attention
5. Add & Norm
6. Feed Forward Network
7. Encoder Stack
8. Masked Self-Attention
9. Cross-Attention
10. Decoder Stack
11. Linear Projection
12. Softmax
```

এগুলো একে একে বুঝি।

---

# 7. Step 1 — Tokenization

প্রথমে text token-এ convert হবে।

```text
"I love AI"
```

ধরা যাক:

```text
["I", "love", "AI"]
```

তারপর tokenizer token ID দেয়:

```text
I     → 101
love  → 2057
AI    → 993
```

অর্থাৎ:

```text
Text
 ↓
Tokens
 ↓
Token IDs
```

---

# 8. Step 2 — Token Embedding

Token IDs সরাসরি Transformer বুঝতে পারে না।

তাই embedding:

```text
101
 ↓
[0.12, 0.44, 0.81, ...]
```

ধরি:

```text
d_model = 512
```

তাহলে প্রতিটি token:

```text
Token ID
   ↓
512-dimensional vector
```

Input shape:

```text
(B, L)
```

Embedding-এর পরে:

```text
(B, L, d_model)
```

যেমন:

```text
Batch = 32
Sequence = 100
d_model = 512
```

তাহলে:

```text
(32, 100, 512)
```

---

# 9. Step 3 — Positional Encoding

Transformer-এর self-attention নিজে থেকে token position জানে না।

তাই:

```text
Token Embedding
       +
Positional Encoding
       ↓
Transformer Input
```

Formula:

$$
X = E + P
$$

যেখানে:

* `E` = Token Embedding
* `P` = Positional Encoding

তুমি M02.23-এ এটা বিস্তারিত শিখেছ।

---

# 10. Encoder কী?

Encoder-এর কাজ:

> **Input sentence-এর contextual representation তৈরি করা।**

উদাহরণ:

```text
Input:
I love machine learning.
```

Encoder প্রতিটি token-এর context-aware representation তৈরি করবে।

```text
I       → contextual vector
love    → contextual vector
machine → contextual vector
learning→ contextual vector
```

---

# 11. Encoder Block

একটি encoder block:

```text
Input
  │
  ▼
Multi-Head Self-Attention
  │
  ▼
Add & Norm
  │
  ▼
Feed Forward Network
  │
  ▼
Add & Norm
  │
  ▼
Output
```

একাধিক block stack করা হয়।

---

# 12. Multi-Head Self-Attention

Encoder-এর সবচেয়ে গুরুত্বপূর্ণ অংশ:

```text
X
↓
Q K V
↓
Multi-Head Attention
↓
Contextual Representation
```

Formula:

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

Multi-head:

$$
MultiHead(Q,K,V)
=
Concat(head_1,\dots,head_h)W^O
$$

এটা তুমি M02.22-এ বিস্তারিত শিখেছ।

---

# 13. Self-Attention এখানে কী করছে?

Sentence:

```text
The student reads a book.
```

Self-attention প্রতিটি token-এর relationship বের করবে।

Conceptually:

```text
student ─────→ reads
book    ─────→ reads
reads   ─────→ student
reads   ─────→ book
```

প্রতিটি token অন্য tokenগুলোর context ব্যবহার করে নিজের representation update করে।

---

# 14. Add & Norm

Attention-এর পরে আসে:

```text
Add & Norm
```

এখানে দুটি গুরুত্বপূর্ণ concept:

1. Residual Connection
2. Layer Normalization

---

# 15. Residual Connection

ধরি input:

```text
X
```

Attention output:

```text
Attention(X)
```

তারপর:

$$
Y = X + Attention(X)
$$

অর্থাৎ original input সরাসরি পরের layer-এ যায়।

```text
          ┌───────────────┐
          │               ↓
X ───────→ Attention ───→ +
│                         ↑
└─────────────────────────┘
```

এটা gradient flow সহজ করে।

---

# 16. কেন Residual Connection?

Deep neural network-এ অনেক layer থাকলে gradient সমস্যা হতে পারে।

Residual connection:

```text
Input ────────────────┐
                      ↓
Layer → Layer → Layer → +
```

Original information-এর একটি direct path থাকে।

ফলে:

* optimization সহজ
* gradient flow ভালো
* deep network train করা সহজ

---

# 17. Layer Normalization

Add-এর পরে:

```text
LayerNorm
```

Layer Normalization activation-এর distribution normalize করতে সাহায্য করে।

Conceptually:

```text
Input
 ↓
Normalize
 ↓
Stable representation
```

Transformer-এ সাধারণত:

```text
LayerNorm
```

ব্যবহার করা হয়।

---

# 18. LayerNorm vs BatchNorm

এটা interview-এর জন্য গুরুত্বপূর্ণ।

### Batch Normalization

মূলত batch dimension-এর উপর statistics ব্যবহার করে।

### Layer Normalization

একটি individual sample-এর feature dimension-এর উপর normalize করে।

Transformer-এর জন্য LayerNorm বেশি উপযোগী কারণ:

```text
Sequence length
Batch size
```

পরিবর্তন হলেও LayerNorm ভালোভাবে কাজ করে।

---

# 19. Feed Forward Network — FFN

Attention-এর পরে আসে:

```text
Position-wise Feed Forward Network
```

সাধারণত:

$$
FFN(x)=W_2 \sigma(W_1x+b_1)+b_2
$$

সহজভাবে:

```text
Input
 ↓
Linear
 ↓
Activation
 ↓
Linear
 ↓
Output
```

যেমন:

```text
512
 ↓
2048
 ↓
ReLU/GELU
 ↓
512
```

---

# 20. কেন FFN দরকার?

Attention মূলত token-to-token relationship তৈরি করে।

FFN প্রতিটি position-এর representation-এর উপর আরও nonlinear transformation করে।

অর্থাৎ:

```text
Attention
→ information mixing

FFN
→ feature transformation
```

এটা খুব গুরুত্বপূর্ণ mental model।

---

# 21. ReLU / GELU

Original Transformer-এ ReLU ব্যবহৃত হয়েছিল।

$$
ReLU(x)=max(0,x)
$$

Modern Transformer architectures-এ GELU খুব common।

Conceptually:

```text
ReLU:
negative → 0

GELU:
smooth nonlinear transformation
```

BERT-এর মতো architecture-এ GELU ব্যবহৃত হয়।

---

# 22. Complete Encoder Block

এখন সব একসাথে:

```text
Input X
   │
   ▼
Multi-Head Self-Attention
   │
   ▼
Residual Add
   │
   ▼
LayerNorm
   │
   ▼
Feed Forward Network
   │
   ▼
Residual Add
   │
   ▼
LayerNorm
   │
   ▼
Encoder Output
```

---

# 23. Multiple Encoder Layers

একটি encoder block-এর পরিবর্তে অনেক block stack করা হয়।

Original Transformer:

```text
Encoder Layer × 6
```

Conceptually:

```text
Input
 ↓
Encoder 1
 ↓
Encoder 2
 ↓
Encoder 3
 ↓
Encoder 4
 ↓
Encoder 5
 ↓
Encoder 6
 ↓
Encoder Output
```

প্রতিটি layer আরও sophisticated contextual representation তৈরি করে।

---

# 24. Decoder কী?

Decoder-এর কাজ:

> **Output sequence generate করা।**

Translation example:

```text
English:
I love Bangladesh.

        ↓ Encoder

Bangla:
আমি বাংলাদেশকে ভালোবাসি।
```

Decoder একে একে output generate করবে।

```text
আমি
 ↓
বাংলাদেশকে
 ↓
ভালোবাসি
 ↓
।
```

---

# 25. Decoder Block

Decoder block-এর তিনটি প্রধান অংশ:

```text
1. Masked Self-Attention
2. Cross-Attention
3. Feed Forward Network
```

Architecture:

```text
Input
  │
  ▼
Masked Self-Attention
  │
  ▼
Add & Norm
  │
  ▼
Cross-Attention
  │
  ▼
Add & Norm
  │
  ▼
FFN
  │
  ▼
Add & Norm
  │
  ▼
Output
```

---

# 26. Masked Self-Attention

এটা অত্যন্ত গুরুত্বপূর্ণ।

ধরি decoder generate করছে:

```text
I love
```

এখন `"love"` predict করার সময় model future token দেখতে পারবে না।

যেমন:

```text
I love machine learning
```

`love` position থেকে:

```text
I       ✓
love    ✓
machine ✗
learning✗
```

Future token hidden থাকবে।

---

# 27. Causal Mask

Causal attention matrix conceptually:

```text
       I love machine learning

I      ✓  ✗    ✗      ✗
love   ✓  ✓    ✗      ✗
machine✓  ✓    ✓      ✗
learning✓ ✓    ✓      ✓
```

অর্থাৎ:

> Current token শুধুমাত্র past + current token দেখতে পারে।

এটাই **causal self-attention**।

---

# 28. কেন Mask দরকার?

Language generation-এ আমরা চাই:

```text
P(next_token | previous_tokens)
```

যদি model future token দেখতে পায়:

```text
Input:
I love machine learning

Model জানে:
learning
```

তাহলে training cheating হয়ে যাবে।

তাই future information mask করা হয়।

---

# 29. Cross-Attention

Decoder-এর দ্বিতীয় attention:

```text
Cross-Attention
```

এখানে:

```text
Query
← Decoder

Key
← Encoder

Value
← Encoder
```

অর্থাৎ:

```text
Decoder
   │
   │ Query
   ▼
Cross Attention
   ▲
   │ Key + Value
Encoder
```

এটা encoder-এর output থেকে প্রয়োজনীয় information retrieve করে।

---

# 30. Self-Attention vs Cross-Attention

খুব গুরুত্বপূর্ণ:

| Attention       | Q             | K             | V             |
| --------------- | ------------- | ------------- | ------------- |
| Self-Attention  | same sequence | same sequence | same sequence |
| Cross-Attention | Decoder       | Encoder       | Encoder       |

Example:

```text
Self:
Decoder → Decoder

Cross:
Decoder → Encoder
```

---

# 31. Decoder FFN

Cross-attention-এর পরে:

```text
FFN
```

আবার:

```text
Linear
 ↓
Activation
 ↓
Linear
```

তারপর:

```text
Residual
 ↓
LayerNorm
```

---

# 32. Output Projection

Decoder-এর final representation:

```text
(B, L, d_model)
```

এটাকে vocabulary probability-তে convert করতে হয়।

তাই:

```text
Linear Layer
```

ব্যবহার করা হয়।

ধরি:

```text
d_model = 512
vocab_size = 30,000
```

তাহলে:

```text
512
 ↓
Linear
 ↓
30,000 logits
```

Shape:

```text
(B, L, 30000)
```

---

# 33. Softmax

Logits থেকে probability:

$$
P(token)=softmax(logits)
$$

উদাহরণ:

```text
hello     → 0.05
world     → 0.02
machine   → 0.10
learning  → 0.72
...
```

সব probability-এর sum:

```text
1.0
```

Model highest probability token নির্বাচন করতে পারে।

---

# 34. Autoregressive Generation

Decoder একসাথে পুরো sentence generate করে না।

ধাপে ধাপে:

```text
<START>
   ↓
I
   ↓
I love
   ↓
I love AI
   ↓
I love AI <END>
```

Concept:

$$
P(y_1,y_2,\dots,y_n)
=
\prod_t P(y_t|y_{<t},x)
$$

---

# 35. Teacher Forcing

Training-এর সময় decoder-কে actual previous token দেওয়া হয়।

Target:

```text
I love AI
```

Training:

```text
Input:
<START> → I → love → AI

Target:
I       → love → AI → <END>
```

এটাই **Teacher Forcing**।

---

# 36. Training vs Inference

### Training

Actual previous token:

```text
<START> → I → love → AI
```

### Inference

Model নিজের prediction ব্যবহার করে:

```text
<START>
 ↓
I
 ↓
love
 ↓
AI
 ↓
<END>
```

এখানে training এবং inference-এর difference থেকে **exposure bias** তৈরি হতে পারে।

---

# 37. Padding Mask

সব sentence একই length-এর নয়।

Example:

```text
"I love AI"

"I love machine learning"
```

Batch করতে padding:

```text
I love AI <PAD> <PAD>
I love machine learning
```

Model যেন `<PAD>` token-কে meaningful token হিসেবে না দেখে।

তাই:

```text
Padding Mask
```

ব্যবহার করা হয়।

---

# 38. দুই ধরনের গুরুত্বপূর্ণ mask

Transformer-এ এখন পর্যন্ত:

```text
1. Padding Mask
2. Causal Mask
```

### Padding Mask

```text
<PAD> → ignore
```

### Causal Mask

```text
Future → ignore
```

---

# 39. Encoder বনাম Decoder

| Feature               | Encoder    | Decoder |
| --------------------- | ---------- | ------- |
| Self-Attention        | Yes        | Yes     |
| Masked Self-Attention | No         | Yes     |
| Cross-Attention       | No         | Yes     |
| FFN                   | Yes        | Yes     |
| Generate text         | সাধারণত না | Yes     |
| Input understanding   | Strong     | Yes     |
| Autoregressive        | No         | Yes     |

---

# 40. Original Transformer Full Flow

এখন পুরো architecture:

```text
                    INPUT TEXT
                        │
                        ▼
                    Tokenizer
                        │
                        ▼
                    Token IDs
                        │
                        ▼
                  Token Embedding
                        │
                        +
                Positional Encoding
                        │
                        ▼
                ┌───────────────┐
                │    ENCODER    │
                │               │
                │ Self-Attention│
                │      ↓        │
                │ Add & Norm    │
                │      ↓        │
                │ FFN           │
                │      ↓        │
                │ Add & Norm    │
                └───────┬───────┘
                        │
                  Encoder Output
                        │
              ┌─────────┴─────────┐
              │                   │
              │                   │
              ▼                   │
          Decoder Input           │
              │                   │
              ▼                   │
      Masked Self-Attention       │
              │                   │
              ▼                   │
          Add & Norm              │
              │                   │
              ▼                   │
       Cross-Attention ◄──────────┘
              │
              ▼
          Add & Norm
              │
              ▼
             FFN
              │
              ▼
          Add & Norm
              │
              ▼
          Linear Layer
              │
              ▼
            Softmax
              │
              ▼
        Next Token
```

---

# 41. Transformer-এর তিনটি architecture family

এটা ভবিষ্যতের BERT/GPT বোঝার জন্য খুব গুরুত্বপূর্ণ।

## A. Encoder-only

```text
Input
 ↓
Encoder
 ↓
Representation
```

Example:

```text
BERT
```

ব্যবহার:

* classification
* sentiment analysis
* NER
* embeddings
* semantic understanding

---

# 42. Decoder-only

```text
Input
 ↓
Decoder
 ↓
Next Token
 ↓
Next Token
```

Example:

```text
GPT-family
```

ব্যবহার:

* text generation
* chat
* completion
* writing
* coding

তোমার AI writing assistant-এর জন্য এটা অত্যন্ত গুরুত্বপূর্ণ।

---

# 43. Encoder-Decoder

```text
Input
 ↓
Encoder
 ↓
Decoder
 ↓
Output
```

Example:

```text
T5
```

ব্যবহার:

* translation
* summarization
* text-to-text tasks

---

# 44. BERT vs GPT vs T5

| Model | Architecture    | Main idea   |
| ----- | --------------- | ----------- |
| BERT  | Encoder-only    | Understand  |
| GPT   | Decoder-only    | Generate    |
| T5    | Encoder-Decoder | Text → Text |

Mental model:

```text
BERT
→ "What does this text mean?"

GPT
→ "What comes next?"

T5
→ "Transform this text into another text."
```

---

# 45. Transformer কেন এত powerful?

কারণ:

### 1. Parallelization

RNN:

```text
x1 → x2 → x3 → x4
```

Transformer:

```text
x1 ─┐
x2 ─┤
x3 ─┼→ Attention
x4 ─┘
```

---

### 2. Long-range dependencies

Sentence:

```text
The student who studied for many hours passed the exam.
```

Transformer সরাসরি relevant tokens-এর relationship capture করতে পারে।

---

### 3. Scalable

Transformer architecture অনেক বড় করা যায়:

```text
More layers
+
More dimensions
+
More heads
+
More data
```

ফলে large language models তৈরি সম্ভব হয়েছে।

---

# 46. Transformer-এর Computational Complexity

Self-attention-এর বড় সমস্যা:

$$
O(L^2)
$$

যেখানে:

```text
L = sequence length
```

কারণ attention matrix:

```text
L × L
```

যেমন:

```text
L = 100

100 × 100
= 10,000
```

কিন্তু:

```text
L = 10,000

10,000 × 10,000
= 100,000,000
```

তাই long-context Transformer computationally expensive হতে পারে।

---

# 47. Transformer বনাম RNN

| Feature           | RNN           | Transformer                         |
| ----------------- | ------------- | ----------------------------------- |
| Sequential        | Yes           | No recurrence                       |
| Parallel training | Limited       | Excellent                           |
| Long dependency   | Difficult     | Better                              |
| Attention         | Optional      | Core                                |
| Training speed    | তুলনামূলক ধীর | Faster parallel training            |
| Long context      | Difficult     | Better but O(L²) standard attention |
| Modern LLM        | Rarely core   | Core                                |

---

# 48. Transformer বনাম LSTM

```text
LSTM:
Memory through recurrent state

Transformer:
Context through attention
```

LSTM:

```text
Previous state
      ↓
Current state
```

Transformer:

```text
All relevant tokens
       ↓
Attention
       ↓
Context
```

---

# 49. AI Writing Assistant-এর ক্ষেত্রে Transformer

তোমার future AI writing platform-এর architecture conceptually:

```text
User Text
   ↓
Tokenizer
   ↓
Token IDs
   ↓
Embedding
   +
Position
   ↓
Transformer
   ↓
Contextual Representation
   ↓
Task Head / Generation Head
   ↓
Generated Text
```

যেমন user লিখল:

```text
"This is a very good product and it works very well."
```

System বিভিন্ন task করতে পারে:

```text
Grammar correction
        ↓
Rewrite
        ↓
Tone transformation
        ↓
Clarity improvement
        ↓
Summarization
        ↓
Paraphrasing
```

এখানে Transformer foundation খুব গুরুত্বপূর্ণ।

---

# 50. AI Writing Model-এর দুই ধরনের কাজ

### Understanding

```text
Text
 ↓
Encoder
 ↓
Representation
 ↓
Classification / Analysis
```

### Generation

```text
Prompt
 ↓
Decoder-only Transformer
 ↓
Next token
 ↓
Next token
 ↓
Next token
```

---

# 51. একটি Transformer Block-এর mental model

এটা মুখস্থ রাখো:

```text
                INPUT
                  │
                  ▼
        Multi-Head Attention
                  │
                  ▼
             Residual
                  │
                  ▼
            LayerNorm
                  │
                  ▼
                FFN
                  │
                  ▼
             Residual
                  │
                  ▼
            LayerNorm
                  │
                  ▼
               OUTPUT
```

---

# 52. Encoder-Decoder mental model

```text
              TRANSFORMER

        ┌───────────────────┐
        │      ENCODER      │
        │                   │
Input → │ Self-Attention    │
        │       ↓           │
        │ FFN               │
        │       ↓           │
        │ Context           │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │      DECODER      │
        │                   │
        │ Masked Attention  │
        │       ↓           │
        │ Cross Attention   │
        │       ↓           │
        │ FFN               │
        │       ↓           │
        │ Output            │
        └─────────┬─────────┘
                  │
                  ▼
               Softmax
                  │
                  ▼
              Next Token
```

---

# 53. PyTorch — Simplified Transformer

এখন implementation দেখি।

```python
import torch
import torch.nn as nn


d_model = 128
nhead = 8

encoder_layer = nn.TransformerEncoderLayer(
    d_model=d_model,
    nhead=nhead,
    batch_first=True
)

encoder = nn.TransformerEncoder(
    encoder_layer,
    num_layers=6
)

x = torch.randn(32, 100, 128)

output = encoder(x)

print(output.shape)
```

Output:

```text
torch.Size([32, 100, 128])
```

অর্থাৎ:

```text
Input:
(B, L, D)

Output:
(B, L, D)
```

---

# 54. Transformer Decoder

```python
decoder_layer = nn.TransformerDecoderLayer(
    d_model=128,
    nhead=8,
    batch_first=True
)

decoder = nn.TransformerDecoder(
    decoder_layer,
    num_layers=6
)
```

এখানে decoder সাধারণত নেয়:

```text
tgt
memory
```

যেখানে:

```text
tgt
→ decoder-side input

memory
→ encoder output
```

---

# 55. Full PyTorch Transformer

PyTorch-এর built-in:

```python
transformer = nn.Transformer(
    d_model=128,
    nhead=8,
    num_encoder_layers=6,
    num_decoder_layers=6,
    batch_first=True
)
```

Conceptually:

```text
Input
 ↓
Encoder
 ↓
Memory
 ↓
Decoder
 ↓
Output
```

---

# 56. Important: Transformer নিজে Tokenizer নয়

অনেক beginner এখানে ভুল করে।

Transformer:

```text
Tokenizer ≠ Transformer
Embedding ≠ Transformer
Transformer ≠ LLM
```

বরং:

```text
Tokenizer
   ↓
Token IDs
   ↓
Embedding
   ↓
Positional Information
   ↓
Transformer
   ↓
Prediction
```

---

# 57. Transformer ≠ GPT

GPT হলো একটি **Transformer-based model family**।

সহজভাবে:

```text
Transformer
    ↓
Architecture

GPT
    ↓
Transformer architecture
+
Training objective
+
Large dataset
+
Large parameters
+
Training strategy
```

---

# 58. Transformer ≠ LLM

Transformer হলো architecture।

LLM হলো large-scale language model।

একটি LLM:

```text
Architecture
+
Dataset
+
Tokenizer
+
Training
+
Parameters
+
Optimization
+
Inference
```

এর architecture Transformer হতে পারে।

---

# 59. Parameter Count-এর Basic Idea

ধরি:

```text
d_model = 512
```

Self-attention-এ:

```text
WQ
WK
WV
WO
```

প্রতিটি roughly:

```text
512 × 512
```

অর্থাৎ attention-এর parameter অনেক।

FFN:

```text
512 → 2048 → 512
```

এখানেও অনেক parameters।

তাই:

```text
More layers
+
larger d_model
+
larger FFN
```

→ model অনেক বড় হয়ে যায়।

---

# 60. Dropout

Transformer-এ regularization-এর জন্য dropout ব্যবহার করা হতে পারে।

Conceptually:

```text
Neurons
 ↓
Randomly কিছু activation drop
 ↓
Overfitting কমাতে সাহায্য
```

Training:

```text
Dropout ON
```

Inference:

```text
Dropout OFF
```

---

# 61. Pre-Norm vs Post-Norm

এটা একটু advanced কিন্তু জানা দরকার।

Original Transformer-এর common formulation:

```text
Attention
 ↓
Add
 ↓
Norm
```

এটাকে broadly **Post-Norm** বলা হয়।

অনেক modern Transformer:

```text
Norm
 ↓
Attention
 ↓
Add
```

ব্যবহার করে।

এটা **Pre-Norm**।

Modern large models-এ Pre-Norm খুব common কারণ deep network training stability-এর সুবিধা দিতে পারে।

---

# 62. Complete Tensor Flow

ধরি:

```text
Batch = 32
Sequence length = 128
d_model = 512
heads = 8
```

Input token IDs:

```text
(32, 128)
```

Embedding:

```text
(32, 128, 512)
```

Q/K/V:

```text
(32, 128, 512)
```

Head split:

```text
(32, 8, 128, 64)
```

কারণ:

$$
512 / 8 = 64
$$

Attention scores:

```text
(32, 8, 128, 128)
```

Attention output:

```text
(32, 8, 128, 64)
```

Concatenate:

```text
(32, 128, 512)
```

FFN:

```text
512 → 2048 → 512
```

Output:

```text
(32, 128, 512)
```

---

# 63. এখন পুরো Transformer-এর এক লাইনের ধারণা

```text
Text
 ↓
Tokenization
 ↓
Embedding
 ↓
Position
 ↓
Attention
 ↓
Residual + Norm
 ↓
FFN
 ↓
Residual + Norm
 ↓
Repeat Layers
 ↓
Decoder / Task Head
 ↓
Linear
 ↓
Softmax
 ↓
Prediction
```

---

# 64. সবচেয়ে গুরুত্বপূর্ণ 10টি Concept

আজকের lesson থেকে অবশ্যই master করতে হবে:

```text
1. Transformer
2. Encoder
3. Decoder
4. Multi-Head Self-Attention
5. Residual Connection
6. LayerNorm
7. Feed Forward Network
8. Masked Self-Attention
9. Cross-Attention
10. Autoregressive Generation
```

---

# 65. Transformer শেখার Dependency Map

তুমি এখন পর্যন্ত:

```text
M02.17 RNN
      ↓
M02.18 LSTM
      ↓
M02.19 GRU
      ↓
M02.20 Attention
      ↓
M02.21 Self-Attention
      ↓
M02.22 Multi-Head Attention
      ↓
M02.23 Positional Encoding
      ↓
M02.24 Transformer Architecture
```

এটা খুব সুন্দর progression।

---

# 66. M02.24-এর পরে কী আসবে?

আমাদের NLP Foundation এখনো শেষ হয়নি।

পরের গুরুত্বপূর্ণ topics:

```text
M02.25 — Transformer Encoder Deep Dive
M02.26 — Transformer Decoder Deep Dive
M02.27 — Masking Deep Dive
M02.28 — BERT Architecture
M02.29 — GPT Architecture
M02.30 — T5 / Encoder-Decoder Models
M02.31 — Pretraining & Fine-tuning
M02.32 — Transfer Learning in NLP
M02.33 — Subword Tokenization
M02.34 — BPE
M02.35 — WordPiece
M02.36 — SentencePiece
M02.37 — Modern LLM Architecture
M02.38 — Prompt & Context
M02.39 — Text Generation
M02.40 — Decoding Strategies
...
```

অর্থাৎ **M02.24 শেষ করলেই Transformer chapter পুরো শেষ নয়**। Encoder, Decoder, BERT, GPT, tokenization, pretraining, fine-tuning—এগুলো আলাদাভাবে deep dive করব যাতে কোনো foundational topic skip না হয়।

---

# 🧠 Final Mental Model

সবশেষে এই diagram-টা মাথায় রাখো:

```text
                         TEXT
                          │
                          ▼
                     TOKENIZER
                          │
                          ▼
                      TOKEN IDs
                          │
                          ▼
                    EMBEDDING
                          │
                          +
                 POSITION INFORMATION
                          │
                          ▼
                  ┌──────────────┐
                  │   ENCODER    │
                  │              │
                  │ Self-Attn    │
                  │     ↓        │
                  │ Add + Norm   │
                  │     ↓        │
                  │ FFN          │
                  │     ↓        │
                  │ Add + Norm   │
                  └──────┬───────┘
                         │
                    CONTEXT
                         │
                         ▼
                  ┌──────────────┐
                  │   DECODER    │
                  │              │
                  │ Masked Attn  │
                  │     ↓        │
                  │ Cross-Attn ◄─┘
                  │     ↓        │
                  │ FFN          │
                  │     ↓        │
                  │ Add + Norm   │
                  └──────┬───────┘
                         │
                         ▼
                       LINEAR
                         │
                         ▼
                      SOFTMAX
                         │
                         ▼
                    NEXT TOKEN
```

### ⭐ One-line summary

> **Transformer = Positional Information + Multi-Head Attention + Residual Connections + LayerNorm + FFN + (Decoder হলে Masked Self-Attention + Cross-Attention) + Output Prediction**

**M02.24 — Complete ✅**


---
# M02.25 — Transformer Encoder Deep Dive

আজ আমরা **Transformer Encoder**-কে আলাদাভাবে গভীরভাবে শিখব।

M02.24-এ তুমি পুরো Transformer architecture দেখেছ। এখন focus হবে শুধু:

> **Encoder কীভাবে input text-কে contextual representation-এ convert করে?**

এটি বিশেষভাবে গুরুত্বপূর্ণ কারণ **BERT, RoBERTa, DistilBERT** ইত্যাদি encoder-based model বুঝতে এই lesson foundation তৈরি করবে।

---

# 1. Transformer Encoder কী?

Transformer Encoder হলো এমন একটি neural network stack যা input sequence-এর প্রতিটি token-এর জন্য **context-aware representation** তৈরি করে।

সহজভাবে:

```text
Input Text
    ↓
Token IDs
    ↓
Embedding
    ↓
Positional Information
    ↓
Transformer Encoder
    ↓
Contextual Representations
```

উদাহরণ:

```text
"The bank is near the river."
```

Encoder `"bank"` token-এর representation তৈরি করার সময়:

```text
bank
 ↓
The
is
near
the
river
```

সব relevant context ব্যবহার করতে পারে।

---

# 2. Encoder-এর মূল কাজ

Encoder সাধারণত:

```text
Understand / Represent Input
```

করে।

এটি নিজে সাধারণত autoregressive text generation-এর জন্য তৈরি নয়।

উদাহরণ:

```text
Input:
"Python is a programming language."

        ↓ Encoder

Contextual representations
        ↓
Classification / NER / Similarity / etc.
```

---

# 3. Encoder-এর Complete Architecture

একটি Encoder Layer:

```text
                 INPUT
                   │
                   ▼
          Multi-Head Self-Attention
                   │
                   ▼
              Residual Add
                   │
                   ▼
               LayerNorm
                   │
                   ▼
           Feed Forward Network
                   │
                   ▼
              Residual Add
                   │
                   ▼
               LayerNorm
                   │
                   ▼
                 OUTPUT
```

এমন অনেকগুলো layer stack করা হয়:

```text
Input
 ↓
Encoder Layer 1
 ↓
Encoder Layer 2
 ↓
Encoder Layer 3
 ↓
...
 ↓
Encoder Layer N
 ↓
Final Representation
```

---

# 4. Encoder Input

ধরি sentence:

```text
I love machine learning.
```

প্রথমে tokenizer:

```text
["I", "love", "machine", "learning", "."]
```

তারপর token IDs:

```text
[101, 2057, 3698, 4083, 1012]
```

এগুলো embedding layer-এ যায়।

---

# 5. Token Embedding

ধরি:

```text
d_model = 768
```

তাহলে প্রত্যেক token:

```text
Token ID
   ↓
768-dimensional vector
```

Input shape:

```text
(B, L)
```

Embedding-এর পরে:

```text
(B, L, 768)
```

ধরি:

```text
B = 16
L = 128
```

তাহলে:

```text
(16, 128, 768)
```

---

# 6. Positional Information

Self-attention token order সরাসরি জানে না।

তাই:

```text
Token Embedding
       +
Position Information
       ↓
Encoder Input
```

Classic Transformer-এ:

$$
X = E + P
$$

যেখানে:

* `E` = token embedding
* `P` = positional encoding

তুমি M02.23-এ positional encoding বিস্তারিত শিখেছ।

---

# 7. Encoder-এর সবচেয়ে গুরুত্বপূর্ণ অংশ

Encoder-এর core হলো:

```text
Multi-Head Self-Attention
```

এখানে:

```text
Q = XW_Q
K = XW_K
V = XW_V
```

তারপর:

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

Multiple heads ব্যবহার করা হয়।

---

# 8. Encoder-এ Self-Attention কেন?

ধরি:

```text
The animal crossed the street because it was tired.
```

এখানে:

```text
it
```

কাকে refer করছে?

সম্ভবত:

```text
animal
```

Self-attention token relationship তৈরি করে:

```text
it ─────────→ animal
```

অর্থাৎ encoder প্রতিটি token-এর representation-এ পুরো sentence-এর context ব্যবহার করতে পারে।

---

# 9. Encoder Bidirectional

এটা অত্যন্ত গুরুত্বপূর্ণ।

Encoder সাধারণত দুই দিকের context ব্যবহার করতে পারে:

```text
Previous tokens ← Current token → Future tokens
```

উদাহরণ:

```text
The bank is near the river.
```

`bank` বোঝার সময়:

```text
The
bank
is
near
the
river
```

দুই পাশের information ব্যবহার করা যায়।

---

# 10. Encoder-এ Causal Mask নেই

GPT-এর মতো decoder-only model-এ:

```text
Future tokens → hidden
```

কিন্তু standard encoder-এ:

```text
Past    → visible
Current → visible
Future  → visible
```

অর্থাৎ:

```text
       T1 T2 T3 T4

T1     ✓  ✓  ✓  ✓
T2     ✓  ✓  ✓  ✓
T3     ✓  ✓  ✓  ✓
T4     ✓  ✓  ✓  ✓
```

তবে padding tokens ignore করার জন্য **padding mask** ব্যবহার করা হতে পারে।

---

# 11. Encoder Self-Attention vs Decoder Self-Attention

| বিষয়               | Encoder | Decoder |
| ------------------ | ------- | ------- |
| Self-attention     | Yes     | Yes     |
| Future দেখতে পারে? | Yes     | No      |
| Causal mask        | No      | Yes     |
| Padding mask       | Yes     | Yes     |
| Cross-attention    | No      | Yes     |

সবচেয়ে গুরুত্বপূর্ণ:

```text
Encoder:
Full context

Decoder:
Past + current context
```

---

# 12. Multi-Head Attention

ধরি:

```text
d_model = 768
num_heads = 12
```

তাহলে:

$$
d_{head}=768/12=64
$$

প্রতিটি head:

```text
768
 ↓
64
```

প্রতিটি head আলাদা attention pattern শিখতে পারে।

Conceptually:

```text
                 Input
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
     Head 1      Head 2      Head 12
       ↓           ↓           ↓
    Attention   Attention   Attention
       └───────────┼───────────┘
                   ↓
               Concatenate
                   ↓
                Wᵒ Linear
                   ↓
                 Output
```

---

# 13. Different Heads কী শিখতে পারে?

এগুলো hard-coded নয়; training-এর মাধ্যমে patterns শেখে।

Conceptually কোনো head:

```text
subject → verb
```

অন্য head:

```text
pronoun → antecedent
```

অন্য head:

```text
adjective → noun
```

অন্য head:

```text
long-range dependency
```

শিখতে পারে।

তবে বাস্তবে প্রতিটি head-এর নির্দিষ্ট human-interpretable role থাকা বাধ্যতামূলক নয়।

---

# 14. Residual Connection

Attention-এর পরে:

$$
Y = X + Attention(X)
$$

Diagram:

```text
             ┌───────────────┐
             │               │
             ↓               │
Input → Self-Attention → Add
             │               ↑
             └───────────────┘
```

এখানে original input হারিয়ে যায় না।

---

# 15. LayerNorm

Residual addition-এর পরে:

```text
LayerNorm
```

ধরা যাক:

```text
X + Attention(X)
       ↓
   LayerNorm
```

LayerNorm representation-এর feature values stabilize করতে সাহায্য করে।

---

# 16. দ্বিতীয় Sub-Layer — FFN

এরপর:

```text
LayerNorm
   ↓
FFN
```

FFN সাধারণত:

$$
FFN(x)=W_2 \sigma(W_1x+b_1)+b_2
$$

যেমন BERT-like configuration:

```text
768
 ↓
3072
 ↓
GELU
 ↓
768
```

অর্থাৎ:

```text
d_model
 ↓
d_ff
 ↓
activation
 ↓
d_model
```

---

# 17. FFN-এর কাজ

Self-attention:

```text
Token-to-token information mixing
```

FFN:

```text
Feature transformation
```

তাই mental model:

```text
Self-Attention
→ "কার সাথে সম্পর্ক আছে?"

FFN
→ "এই information কীভাবে transform করব?"
```

---

# 18. দ্বিতীয় Residual Connection

FFN-এর পরে:

$$
Z = Y + FFN(Y)
$$

তারপর:

```text
LayerNorm
```

ফলে complete encoder layer:

```text
Input
 ↓
Self-Attention
 ↓
Residual
 ↓
LayerNorm
 ↓
FFN
 ↓
Residual
 ↓
LayerNorm
 ↓
Output
```

---

# 19. Encoder Layer Mathematical View

একটি simplified Post-Norm formulation:

$$
A = LayerNorm(X + MHA(X))
$$

তারপর:

$$
Y = LayerNorm(A + FFN(A))
$$

অর্থাৎ:

```text
X
 ↓
MHA(X)
 ↓
X + MHA(X)
 ↓
LayerNorm
 ↓
FFN
 ↓
+ previous representation
 ↓
LayerNorm
 ↓
Y
```

---

# 20. Pre-Norm Architecture

Modern Transformer implementation-এ Pre-Norm-ও খুব গুরুত্বপূর্ণ।

Pre-Norm:

$$
Y=X+MHA(LN(X))
$$

তারপর:

$$
Z=Y+FFN(LN(Y))
$$

Diagram:

```text
Input
 ↓
LayerNorm
 ↓
Self-Attention
 ↓
Residual Add
 ↓
LayerNorm
 ↓
FFN
 ↓
Residual Add
 ↓
Output
```

---

# 21. Post-Norm vs Pre-Norm

|                      | Post-Norm          | Pre-Norm                |
| -------------------- | ------------------ | ----------------------- |
| Norm কোথায়?          | Sub-layer-এর পরে   | Sub-layer-এর আগে        |
| Original Transformer | Yes                | No                      |
| Modern deep models   | Less common        | Very common             |
| Training stability   | কিছু ক্ষেত্রে কঠিন | Deep models-এ সুবিধাজনক |

Implementation অনুযায়ী architecture variant পরিবর্তিত হতে পারে।

---

# 22. Encoder Stack

একটি encoder layer যথেষ্ট নয়।

ধরি:

```text
N = 12
```

তাহলে:

```text
Input
 ↓
Encoder Layer 1
 ↓
Encoder Layer 2
 ↓
Encoder Layer 3
 ↓
...
 ↓
Encoder Layer 12
 ↓
Final Encoder Output
```

প্রতিটি layer:

```text
আগের representation
        ↓
আরও contextual representation
```

তৈরি করে।

---

# 23. Layer-by-Layer Representation

ধরি:

```text
"I love Python."
```

প্রথম layer:

```text
Token + basic context
```

মাঝের layers:

```text
Grammar + semantic relationships
```

উচ্চ layers:

```text
Task-relevant contextual features
```

এটা conceptual understanding; প্রতিটি layer-এর নির্দিষ্ট human-defined role থাকে না।

---

# 24. Encoder Output

ধরি:

```text
Batch = 32
Sequence = 128
Hidden size = 768
```

তাহলে final output:

```text
(32, 128, 768)
```

প্রতিটি token-এর জন্য:

```text
768-dimensional contextual vector
```

---

# 25. Contextual Representation

এটা খুব গুরুত্বপূর্ণ।

Static embedding:

```text
bank
 ↓
একটি fixed vector
```

Contextual representation:

```text
"The bank approved my loan."
             ↓
          bank vector A
```

আর:

```text
"The boat reached the river bank."
             ↓
          bank vector B
```

একই word:

```text
bank
```

কিন্তু context অনুযায়ী representation আলাদা হতে পারে।

---

# 26. Encoder-এর বড় শক্তি

Encoder:

```text
Word meaning
+
Sentence structure
+
Context
+
Relationships
```

একসাথে representation-এর মধ্যে capture করতে পারে।

এজন্য BERT-এর মতো model NLP-তে খুব powerful হয়েছে।

---

# 27. Encoder-এর পরে কী করা যায়?

Encoder output বিভিন্ন task-এ ব্যবহার করা যায়।

```text
Encoder
   │
   ├──→ Classification
   │
   ├──→ NER
   │
   ├──→ POS Tagging
   │
   ├──→ Semantic Similarity
   │
   ├──→ Question Answering
   │
   ├──→ Embeddings
   │
   └──→ Retrieval
```

---

# 28. Classification Example

Input:

```text
"This movie is excellent."
```

Encoder:

```text
Text
 ↓
Encoder
 ↓
Contextual representation
 ↓
Classification Head
 ↓
Positive
```

---

# 29. NER Example

Input:

```text
"Barack Obama visited Paris."
```

Encoder:

```text
Barack → contextual vector
Obama  → contextual vector
visited→ contextual vector
Paris  → contextual vector
```

তারপর token classification head:

```text
Barack → B-PER
Obama  → I-PER
Paris  → B-GPE
```

---

# 30. Sentence Embedding

পুরো sentence-এর representation বের করেও ব্যবহার করা যায়।

```text
Sentence
 ↓
Encoder
 ↓
Pooling
 ↓
Sentence Vector
```

তারপর:

```text
Sentence A
      ↓
   Vector A

Sentence B
      ↓
   Vector B

      ↓

Cosine Similarity
```

এটা semantic similarity-এর জন্য ব্যবহার করা যায়।

---

# 31. `[CLS]` Token

BERT-style encoder models-এ special token:

```text
[CLS]
```

ব্যবহার করা হয়।

Example:

```text
[CLS] I love machine learning [SEP]
```

Encoder output:

```text
[CLS] → vector
I     → vector
love  → vector
machine → vector
learning → vector
[SEP] → vector
```

অনেক classification setup-এ `[CLS]` representation ব্যবহার করা হয়।

---

# 32. `[SEP]` Token

`[SEP]` সাধারণত sequence boundary বা multiple sentence separation বোঝাতে BERT-style models-এ ব্যবহৃত হয়।

Example:

```text
[CLS] Sentence A [SEP] Sentence B [SEP]
```

এটা model-কে input structure বোঝাতে সাহায্য করে।

---

# 33. Attention Mask in Encoder

ধরি:

```text
Sentence A:
I love AI

Sentence B:
Python is powerful
```

Batch করার জন্য:

```text
I love AI <PAD> <PAD>
Python is powerful
```

Padding mask:

```text
I       → attend
love    → attend
AI      → attend
<PAD>   → ignore
<PAD>   → ignore
```

---

# 34. Encoder-এ Padding Mask কেন?

কারণ `<PAD>` semantic information বহন করে না।

যদি model padding-এর দিকে attention দেয়:

```text
Useful information
        +
Noise
```

তৈরি হতে পারে।

তাই mask দিয়ে padding ignore করা হয়।

---

# 35. Encoder বনাম Classical NLP

Classical pipeline:

```text
Text
 ↓
Tokenization
 ↓
Stopword Removal
 ↓
Stemming
 ↓
TF-IDF
 ↓
ML Model
```

Encoder-based NLP:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding
 ↓
Transformer Encoder
 ↓
Contextual Representation
 ↓
Task
```

Modern Transformer সাধারণত manually stemming/stopword removal-এর মতো aggressive preprocessing চায় না।

---

# 36. BERT কেন Encoder?

BERT:

```text
Bidirectional Encoder Representations
from Transformers
```

BERT মূলত:

```text
Transformer Encoder
```

ব্যবহার করে।

Architecture:

```text
Text
 ↓
BERT Tokenizer
 ↓
Embeddings
 ↓
Transformer Encoder × N
 ↓
Contextual Representations
 ↓
Task Head
```

---

# 37. BERT-এর "Bidirectional" মানে কী?

ধরি:

```text
The bank is near the river.
```

`bank` representation তৈরি করার সময় model:

```text
The
is
near
the
river
```

দুই দিকের context ব্যবহার করতে পারে।

এটাই BERT-এর bidirectional contextual understanding-এর মূল ধারণা।

---

# 38. Encoder-only Model vs Decoder-only Model

### Encoder

```text
Full context
 ↓
Understanding
```

### Decoder

```text
Previous context
 ↓
Next-token generation
```

Mental model:

```text
Encoder:
"What does this text mean?"

Decoder:
"What should come next?"
```

---

# 39. Encoder-এর Complexity

Self-attention:

$$
O(L^2D)
$$

যেখানে:

* `L` = sequence length
* `D` = hidden dimension

মূল সমস্যা:

```text
Sequence length ↑
        ↓
Attention matrix ↑
        ↓
Memory/Computation ↑
```

তাই long documents encoder-এর জন্যও expensive হতে পারে।

---

# 40. PyTorch Encoder from Scratch

এখন একটি simplified encoder layer:

```python
import torch
import torch.nn as nn


class TransformerEncoderBlock(nn.Module):

    def __init__(
        self,
        d_model=128,
        num_heads=8,
        d_ff=512,
        dropout=0.1
    ):
        super().__init__()

        self.attention = nn.MultiheadAttention(
            embed_dim=d_model,
            num_heads=num_heads,
            dropout=dropout,
            batch_first=True
        )

        self.norm1 = nn.LayerNorm(d_model)

        self.ffn = nn.Sequential(
            nn.Linear(d_model, d_ff),
            nn.GELU(),
            nn.Linear(d_ff, d_model)
        )

        self.norm2 = nn.LayerNorm(d_model)

        self.dropout = nn.Dropout(dropout)

    def forward(self, x, padding_mask=None):

        attention_output, _ = self.attention(
            x,
            x,
            x,
            key_padding_mask=padding_mask
        )

        x = self.norm1(
            x + self.dropout(attention_output)
        )

        ffn_output = self.ffn(x)

        x = self.norm2(
            x + self.dropout(ffn_output)
        )

        return x
```

এখানে:

```text
x
 ↓
Self-Attention
 ↓
Residual + LayerNorm
 ↓
FFN
 ↓
Residual + LayerNorm
 ↓
Output
```

---

# 41. Test করি

```python
x = torch.randn(
    32,
    100,
    128
)

encoder_block = TransformerEncoderBlock(
    d_model=128,
    num_heads=8,
    d_ff=512
)

output = encoder_block(x)

print(output.shape)
```

Output:

```text
torch.Size([32, 100, 128])
```

অর্থাৎ:

```text
Input:
(32, 100, 128)

Output:
(32, 100, 128)
```

---

# 42. Multiple Encoder Blocks

```python
class TransformerEncoder(nn.Module):

    def __init__(
        self,
        num_layers=6,
        d_model=128,
        num_heads=8,
        d_ff=512
    ):
        super().__init__()

        self.layers = nn.ModuleList([
            TransformerEncoderBlock(
                d_model=d_model,
                num_heads=num_heads,
                d_ff=d_ff
            )
            for _ in range(num_layers)
        ])

    def forward(self, x, padding_mask=None):

        for layer in self.layers:
            x = layer(
                x,
                padding_mask
            )

        return x
```

এখন:

```python
encoder = TransformerEncoder(
    num_layers=6,
    d_model=128,
    num_heads=8,
    d_ff=512
)

x = torch.randn(32, 100, 128)

output = encoder(x)

print(output.shape)
```

Output:

```text
(32, 100, 128)
```

---

# 43. Encoder Layer-এর Tensor Flow

ধরি:

```text
B = 32
L = 100
D = 128
H = 8
```

Input:

```text
(32, 100, 128)
```

Q/K/V:

```text
(32, 100, 128)
```

Head split:

```text
(32, 8, 100, 16)
```

কারণ:

$$
128/8=16
$$

Attention score:

```text
(32, 8, 100, 100)
```

Attention output:

```text
(32, 100, 128)
```

FFN:

```text
128 → 512 → 128
```

Final:

```text
(32, 100, 128)
```

---

# 44. Encoder-এর Complete Data Flow

```text
                  TEXT
                   │
                   ▼
                TOKENIZER
                   │
                   ▼
                TOKEN IDs
                   │
                   ▼
              TOKEN EMBEDDING
                   │
                   +
          POSITION INFORMATION
                   │
                   ▼
             ENCODER INPUT
                   │
                   ▼
       ┌────────────────────────┐
       │    ENCODER LAYER 1     │
       │                        │
       │ Multi-Head Self-Attn   │
       │          ↓             │
       │ Residual + LayerNorm   │
       │          ↓             │
       │ FFN                    │
       │          ↓             │
       │ Residual + LayerNorm   │
       └────────────┬───────────┘
                    ↓
       ┌────────────────────────┐
       │    ENCODER LAYER 2     │
       └────────────┬───────────┘
                    ↓
                   ...
                    ↓
       ┌────────────────────────┐
       │    ENCODER LAYER N     │
       └────────────┬───────────┘
                    ↓
          CONTEXTUAL OUTPUT
                    │
          ┌─────────┼──────────┐
          ↓         ↓          ↓
     Classification NER    Embedding
```

---

# 45. Encoder-এর প্রতিটি Component-এর কাজ

| Component      | কাজ                              |
| -------------- | -------------------------------- |
| Tokenizer      | Text → tokens                    |
| Embedding      | Token → vector                   |
| Position       | Position information             |
| Self-Attention | Token relationships              |
| Multi-Head     | Multiple attention patterns      |
| Residual       | Information/gradient path        |
| LayerNorm      | Stable representations           |
| FFN            | Nonlinear feature transformation |
| Stack          | Deep contextual processing       |
| Output         | Contextual representation        |

---

# 46. সবচেয়ে গুরুত্বপূর্ণ পার্থক্য

এগুলো confuse করবে না:

```text
Token Embedding
→ token-এর initial representation

Positional Encoding
→ position information

Self-Attention
→ contextual interaction

FFN
→ feature transformation

Encoder
→ পুরো processing stack
```

---

# 47. AI Writing Assistant-এ Encoder

তোমার AI writing platform-এ encoder ব্যবহার করা যেতে পারে:

```text
User Text
   ↓
Tokenizer
   ↓
Encoder
   ↓
Contextual Representation
   ↓
┌─────────────────┐
│ Grammar Analysis│
│ Tone Analysis   │
│ Classification  │
│ Similarity      │
│ Quality Score   │
└─────────────────┘
```

উদাহরণ:

```text
Original:
"This product is very good and useful."
```

Encoder representation ব্যবহার করে system বুঝতে পারে:

```text
Topic
Sentiment
Semantic meaning
Sentence structure
Tone
```

তারপর অন্য generation model rewrite করতে পারে।

---

# 48. Encoder + Decoder একসাথে

যদি তুমি একটি sequence-to-sequence writing system তৈরি করো:

```text
Input
 ↓
Encoder
 ↓
Context
 ↓
Decoder
 ↓
Generated Rewrite
```

যেমন:

```text
Input:
"Make this sentence more professional."

        ↓

Encoder
        ↓

Meaning / Context
        ↓

Decoder
        ↓

Professional rewrite
```

---

# 49. Encoder-only বনাম Encoder-Decoder

### Encoder-only

```text
Text
 ↓
Encoder
 ↓
Representation
 ↓
Task
```

### Encoder-Decoder

```text
Input Text
 ↓
Encoder
 ↓
Context
 ↓
Decoder
 ↓
Output Text
```

---

# 50. আজকের সবচেয়ে গুরুত্বপূর্ণ 12টি বিষয়

M02.25 complete করতে তোমার এগুলো master করতে হবে:

```text
1. Transformer Encoder
2. Encoder Layer
3. Self-Attention
4. Bidirectional Context
5. Padding Mask
6. Residual Connection
7. LayerNorm
8. Feed Forward Network
9. Pre-Norm
10. Post-Norm
11. Encoder Stack
12. Contextual Representation
```

---

# 51. Interview Questions

### Q1. Transformer Encoder কী?

**Answer:**

Transformer Encoder হলো stacked self-attention এবং feed-forward layers-এর architecture যা input sequence-এর contextual representations তৈরি করে।

---

### Q2. Encoder কি future token দেখতে পারে?

**Answer:**

Standard Transformer Encoder-এ causal masking থাকে না, তাই sequence-এর পুরো visible context ব্যবহার করতে পারে। Padding tokens অবশ্য mask করা হতে পারে।

---

### Q3. Encoder এবং Decoder-এর প্রধান পার্থক্য?

```text
Encoder:
Bidirectional/full-context self-attention

Decoder:
Causal self-attention + generation
```

---

### Q4. Encoder-এ Cross-Attention আছে?

**না।**

Cross-attention original encoder-decoder Transformer-এর decoder অংশে থাকে।

---

### Q5. Encoder-এর FFN-এর কাজ কী?

Attention-এর মাধ্যমে information mixing হওয়ার পরে প্রতিটি position-এর representation-এ nonlinear feature transformation করা।

---

### Q6. Residual connection কেন?

* gradient flow improve করতে
* deep network training সহজ করতে
* original information preserve করতে

---

### Q7. LayerNorm কেন?

Representation-এর training stability উন্নত করতে এবং activation scale normalize করতে।

---

### Q8. BERT কোন architecture ব্যবহার করে?

**Transformer Encoder-only architecture.**

---

# 52. Practice Tasks

### Beginner

একটি tensor তৈরি করো:

```python
x = torch.randn(4, 20, 128)
```

তারপর একটি encoder block-এর মাধ্যমে pass করো।

Expected:

```text
(4, 20, 128)
```

---

### Intermediate

তৈরি করো:

```text
6 Encoder Layers
```

Configuration:

```text
d_model = 256
heads = 8
d_ff = 1024
```

---

### Advanced

একটি mini text classification system বানাও:

```text
Text
 ↓
Embedding
 ↓
Positional Encoding
 ↓
Transformer Encoder
 ↓
Pooling
 ↓
Linear
 ↓
Class
```

---

# 53. Completion Checklist

নিজেকে প্রশ্ন করো:

```text
☐ Transformer Encoder কী?

☐ Encoder Layer কী?

☐ Self-Attention কীভাবে কাজ করে?

☐ Encoder কেন bidirectional?

☐ Encoder-এ causal mask কেন নেই?

☐ Padding Mask কী?

☐ Multi-Head Attention কী?

☐ Residual Connection কেন?

☐ LayerNorm কী?

☐ FFN কী?

☐ Pre-Norm কী?

☐ Post-Norm কী?

☐ Encoder Stack কী?

☐ Contextual Representation কী?

☐ BERT কেন Encoder-based?

☐ Encoder output কোথায় ব্যবহার করা যায়?
```

যদি এগুলোর প্রতিটির উত্তর নিজের ভাষায় দিতে পারো, তাহলে **M02.25 ভালোভাবে complete**।

---

# 🧠 Final Mental Model

সবচেয়ে গুরুত্বপূর্ণ diagram:

```text
                    INPUT TEXT
                         │
                         ▼
                    TOKENIZER
                         │
                         ▼
                     TOKEN IDs
                         │
                         ▼
                   EMBEDDING
                         │
                         +
                POSITION INFORMATION
                         │
                         ▼
                ┌──────────────────┐
                │ TRANSFORMER      │
                │ ENCODER LAYER    │
                │                  │
                │ Self-Attention   │
                │       ↓          │
                │ Residual         │
                │       ↓          │
                │ LayerNorm        │
                │       ↓          │
                │ FFN              │
                │       ↓          │
                │ Residual         │
                │       ↓          │
                │ LayerNorm        │
                └────────┬─────────┘
                         │
                    Repeat N times
                         │
                         ▼
              CONTEXTUAL REPRESENTATION
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
    Classification      NER       Sentence Embedding
          │              │              │
          ▼              ▼              ▼
        Result         Entities      Similarity
```

### ⭐ এক লাইনে মনে রাখো

> **Transformer Encoder = Full-context Self-Attention + Residual Connections + LayerNorm + FFN, repeated across multiple layers to produce contextual representations.**

**M02.25 — Complete ✅**

পরবর্তী ধাপ হবে **M02.26 — Transformer Decoder Deep Dive**, যেখানে আমরা causal attention, decoder input shifting, cross-attention, autoregressive generation এবং training বনাম inference আরও গভীরভাবে করব।


----
# M02.26 — Transformer Decoder Deep Dive

আজ আমরা **Transformer Decoder** একদম ভিতর থেকে শিখব।

M02.24-এ পুরো Transformer architecture এবং M02.25-এ Encoder বিস্তারিত দেখেছি। এখন focus:

> **Decoder কীভাবে previous tokens + encoder information ব্যবহার করে একে একে নতুন token generate করে?**

এটি খুব গুরুত্বপূর্ণ, কারণ **GPT-style text generation**, translation, summarization এবং অনেক generative NLP system বুঝতে Decoder-এর ধারণা পরিষ্কার থাকা দরকার।

---

# 1. Transformer Decoder কী?

Transformer Decoder হলো এমন একটি neural network stack যা input/context থেকে **output sequence generate** করতে পারে।

মূল ধারণা:

```text
Previous Tokens
      +
Context
      ↓
   Decoder
      ↓
 Next Token
```

উদাহরণ:

```text
<START>
   ↓
I
   ↓
I love
   ↓
I love AI
   ↓
I love AI <END>
```

Decoder সাধারণত **autoregressive generation** ব্যবহার করে।

---

# 2. Encoder বনাম Decoder

আগের lesson-এর মূল ধারণা:

```text
Encoder
→ Input বুঝে contextual representation তৈরি করে

Decoder
→ Context ব্যবহার করে output generate করে
```

একটি encoder-decoder Transformer:

```text
Input
 ↓
Encoder
 ↓
Context / Memory
 ↓
Decoder
 ↓
Output
```

---

# 3. Decoder-এর তিনটি প্রধান Sub-layer

একটি original Transformer Decoder Layer-এর মধ্যে থাকে:

```text
1. Masked Multi-Head Self-Attention
2. Cross-Attention
3. Feed Forward Network
```

এর সাথে:

```text
Residual Connection
+
LayerNorm
+
Dropout
```

থাকতে পারে।

Complete structure:

```text id="m8r3qd"
                 DECODER INPUT
                       │
                       ▼
              Masked Self-Attention
                       │
                       ▼
                  Add + Norm
                       │
                       ▼
                 Cross-Attention
                       ▲
                       │
                Encoder Output
                       │
                       ▼
                  Add + Norm
                       │
                       ▼
                      FFN
                       │
                       ▼
                  Add + Norm
                       │
                       ▼
                    OUTPUT
```

---

# 4. Decoder Input কী?

ধরি target sentence:

```text
I love AI.
```

Training-এর সময় decoder input সাধারণত shifted version:

```text
<START> I love AI
```

Target:

```text
I love AI <END>
```

অর্থাৎ:

```text id="4ckq3n"
Decoder Input:
<START> → I → love → AI

Target:
I       → love → AI → <END>
```

এটাকে **shifted-right target** বলা হয়।

---

# 5. কেন Shift করা হয়?

কারণ প্রতিটি position-এ model-এর কাজ:

> **পরের token predict করা।**

ধরি:

```text id="0x4n4k"
Input:  <START>
Target: I
```

তারপর:

```text id="9zrlj5"
Input:  <START> I
Target: love
```

তারপর:

```text id="2y04gi"
Input:  <START> I love
Target: AI
```

অর্থাৎ:

$$
P(y_t|y_1,\dots,y_{t-1},x)
$$

---

# 6. Decoder-এর প্রথম অংশ — Masked Self-Attention

Decoder-এর প্রথম attention হলো:

> **Masked Multi-Head Self-Attention**

এখানে decoder নিজের generated/target-side tokens-এর মধ্যে relationship তৈরি করে।

কিন্তু একটি গুরুত্বপূর্ণ restriction আছে:

> Future token দেখা যাবে না।

---

# 7. কেন Future Token দেখা যাবে না?

ধরি:

```text
I love machine learning
```

`machine` predict করার সময় model যেন:

```text
learning
```

আগে থেকেই দেখতে না পারে।

তাহলে training cheating হয়ে যাবে।

তাই:

```text id="cvp2si"
machine
   ↓
I       ✓
love    ✓
machine ✓
learning✗
```

---

# 8. Causal Mask

Attention matrix:

```text id="q2kz4a"
             I   love  machine  learning

I            ✓    ✗      ✗        ✗
love         ✓    ✓      ✗        ✗
machine      ✓    ✓      ✓        ✗
learning     ✓    ✓      ✓        ✓
```

এটাকে **causal mask** বলা হয়।

আরেকভাবে:

```text id="8y1y6r"
Allowed:
Past + Current

Blocked:
Future
```

---

# 9. Causal Mask-এর Mathematical Idea

Mask না থাকলে:

$$
Scores = \frac{QK^T}{\sqrt{d_k}}
$$

Mask থাকলে:

$$
Scores' = Scores + M
$$

যেখানে future positions-এর জন্য:

$$
M_{ij}=-\infty
$$

Conceptually:

```text id="x9d2q0"
Allowed:
0

Future:
-∞
```

Softmax করার পরে:

```text id="9qgn0v"
softmax(-∞) ≈ 0
```

তাই future token-এর attention weight zero হয়ে যায়।

---

# 10. Decoder Self-Attention-এর Q/K/V

Decoder self-attention-এ:

```text id="vq7u0g"
Q ← Decoder input
K ← Decoder input
V ← Decoder input
```

অর্থাৎ:

```text
Q = XWQ
K = XWK
V = XWV
```

কিন্তু causal mask apply করা হয়।

---

# 11. First Sub-layer

Complete:

```text id="vqg6t8"
Decoder Input
      │
      ▼
Q, K, V
      │
      ▼
Multi-Head Self-Attention
      │
      +
   Residual
      │
      ▼
  LayerNorm
```

---

# 12. Cross-Attention

এরপর আসে Decoder-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি:

> **Cross-Attention**

এখানে Decoder encoder-এর output-এর দিকে attention করে।

```text id="a0qj4y"
              Encoder
                 │
                 │ K + V
                 ▼
Decoder → Cross-Attention
   │
   │ Q
   ▼
Decoder Representation
```

---

# 13. Cross-Attention-এর Q/K/V

এটা খুব ভালোভাবে মনে রাখো:

```text id="5y5xqb"
Q = Decoder

K = Encoder

V = Encoder
```

অর্থাৎ:

$$
Q=X_{decoder}W_Q
$$

$$
K=X_{encoder}W_K
$$

$$
V=X_{encoder}W_V
$$

তারপর:

$$
Attention(Q,K,V)
$$

---

# 14. Self-Attention বনাম Cross-Attention

|          | Self-Attention      | Cross-Attention             |
| -------- | ------------------- | --------------------------- |
| Q        | Same sequence       | Decoder                     |
| K        | Same sequence       | Encoder                     |
| V        | Same sequence       | Encoder                     |
| উদ্দেশ্য | নিজের sequence বোঝা | Encoder context ব্যবহার করা |

সহজভাবে:

```text id="zq1p6f"
Self-Attention:
"আমার sequence-এর কোন token relevant?"

Cross-Attention:
"Encoder-এর কোন information আমার এখন দরকার?"
```

---

# 15. Translation Example

ধরি:

```text
English:
I love Bangladesh.
```

Encoder:

```text id="9fj5xj"
I
love
Bangladesh
```

contextual representation তৈরি করবে।

Decoder যখন:

```text
আমি
```

generate করতে যাচ্ছে, তখন cross-attention encoder output-এর relevant information ব্যবহার করবে।

পরবর্তী token:

```text
বাংলাদেশকে
```

generate করার সময় আবার encoder information access করতে পারে।

---

# 16. Cross-Attention কেন দরকার?

Encoder input sentence-এর representation তৈরি করে:

```text id="4u4v1n"
Input
 ↓
Encoder
 ↓
Meaning / Context
```

Decoder সেই representation থেকে information নেয়:

```text id="w3x5f7"
Encoder Context
       ↓
Cross-Attention
       ↓
Decoder
       ↓
Output
```

এটাই encoder-decoder architecture-এর core communication mechanism।

---

# 17. Cross-Attention-এর Attention Matrix

ধরি:

```text id="6t2n3a"
Encoder length = 5
Decoder length = 4
```

তাহলে cross-attention score shape:

```text id="z7j0mj"
(B, H, decoder_length, encoder_length)
```

অর্থাৎ:

```text id="9j8q4e"
(B, H, 4, 5)
```

কারণ:

```text
Q length = decoder length
K length = encoder length
```

---

# 18. Cross-Attention-এর Shape

ধরি:

```text
B = 32
H = 8
Ld = 20
Le = 50
d_head = 64
```

তাহলে:

```text id="q3y2b1"
Q:
(32, 8, 20, 64)

K:
(32, 8, 50, 64)

V:
(32, 8, 50, 64)
```

Scores:

```text id="2q2r44"
(32, 8, 20, 50)
```

Output:

```text id="5xj4x5"
(32, 8, 20, 64)
```

শেষে heads concatenate করলে:

```text id="8x7y9q"
(32, 20, 512)
```

---

# 19. Cross-Attention-এর Mental Model

```text id="5g1x7r"
               ENCODER
                  │
                  │
             Context Vectors
                  │
                  ▼
          ┌─────────────────┐
          │ Cross-Attention │
          └────────┬────────┘
                   ▲
                   │
                Query
                   │
                DECODER
```

---

# 20. দ্বিতীয় Residual + LayerNorm

Cross-attention-এর পরে:

```text id="l4j0br"
Cross-Attention
       ↓
Residual Add
       ↓
LayerNorm
```

Conceptually:

$$
Y = LayerNorm(X + CrossAttention(X, EncoderOutput))
$$

---

# 21. Third Sub-layer — FFN

তারপর:

```text id="8uw6tg"
FFN
```

একই ধরনের position-wise feed-forward network:

$$
FFN(x)=W_2\sigma(W_1x+b_1)+b_2
$$

উদাহরণ:

```text id="v6f0ha"
512
 ↓
2048
 ↓
GELU/ReLU
 ↓
512
```

---

# 22. Third Residual + LayerNorm

শেষে:

```text id="e3s0q5"
FFN
 ↓
Residual Add
 ↓
LayerNorm
 ↓
Decoder Output
```

---

# 23. Complete Decoder Layer

এখন পুরো একটি layer:

```text id="1w9k4b"
                 INPUT
                   │
                   ▼
       Masked Self-Attention
                   │
                   ▼
              Residual
                   │
                   ▼
              LayerNorm
                   │
                   ▼
          Cross-Attention
                   ▲
                   │
            Encoder Output
                   │
                   ▼
              Residual
                   │
                   ▼
              LayerNorm
                   │
                   ▼
                  FFN
                   │
                   ▼
              Residual
                   │
                   ▼
              LayerNorm
                   │
                   ▼
                OUTPUT
```

---

# 24. Decoder Stack

একটি decoder layer যথেষ্ট নয়।

Original Transformer-এ:

```text
Decoder Layer × 6
```

Conceptually:

```text id="g1x9cv"
Decoder Input
      ↓
Decoder Layer 1
      ↓
Decoder Layer 2
      ↓
Decoder Layer 3
      ↓
Decoder Layer 4
      ↓
Decoder Layer 5
      ↓
Decoder Layer 6
      ↓
Final Decoder Representation
```

---

# 25. Decoder Output

ধরি:

```text
Batch = 32
Sequence = 100
d_model = 512
```

Decoder output:

```text id="0qjy7v"
(32, 100, 512)
```

কিন্তু আমাদের দরকার:

```text
Vocabulary probabilities
```

তাই Linear layer ব্যবহার করি।

---

# 26. Output Projection

ধরি:

```text
vocab_size = 30,000
```

তাহলে:

```text id="6zj3aa"
512
 ↓
Linear
 ↓
30,000
```

Output:

```text
(B, L, vocab_size)
```

অর্থাৎ:

```text
(32, 100, 30000)
```

---

# 27. Softmax

Linear layer থেকে পাওয়া values হলো **logits**।

Softmax:

$$
P_i=\frac{e^{z_i}}{\sum_j e^{z_j}}
$$

ফলে:

```text id="7vjj2u"
token A → 0.02
token B → 0.05
token C → 0.71
token D → 0.01
...
```

সব probability-এর sum:

```text
1.0
```

---

# 28. Next Token Prediction

ধরি decoder input:

```text id="8j3k0s"
"I love"
```

Model output:

```text
AI      → 0.60
Python  → 0.15
coding  → 0.08
music   → 0.02
...
```

তাহলে model `"AI"` select করতে পারে।

Result:

```text id="7m6kpf"
I love AI
```

---

# 29. Autoregressive Generation

তারপর নতুন token আবার input-এর অংশ হয়।

```text id="1r9bq7"
<START>
   ↓
I
   ↓
I love
   ↓
I love AI
   ↓
I love AI very
   ↓
I love AI very much
   ↓
<END>
```

প্রতিটি step:

```text id="w2p4v8"
Previous tokens
      ↓
Decoder
      ↓
Probability distribution
      ↓
Next token
```

---

# 30. Greedy Decoding

সবচেয়ে simple strategy:

> Highest probability token নেওয়া।

উদাহরণ:

```text id="8n0zpw"
AI      → 0.70
Python  → 0.15
ML      → 0.10
```

নির্বাচন:

```text
AI
```

এটাকে **greedy decoding** বলা হয়।

---

# 31. Beam Search

Translation-এর মতো task-এ:

```text id="p3g1s7"
Top 1
Top 2
Top 3
...
```

একাধিক candidate sequence রাখা যায়।

এটাকে **beam search** বলা হয়।

এটা পরে M02-এর generation/decoding lesson-এ আরও বিস্তারিত করা যাবে।

---

# 32. Teacher Forcing

Training-এর সময়:

```text id="w4h3sp"
Actual previous token
       ↓
Decoder
       ↓
Predict next token
```

উদাহরণ:

```text
Input:
<START> I love

Target:
I love AI
```

Model parallelভাবে প্রতিটি position-এর next token predict করতে পারে, causal mask ব্যবহার করে।

---

# 33. Training-এর সময় কি একেক token করে process করতে হয়?

Inference-এর সময়:

```text
token 1
 ↓
token 2
 ↓
token 3
```

ধাপে ধাপে generation হয়।

কিন্তু training-এর সময় target sequence-এর অনেক positions **একসাথে** process করা যায়।

কারণ causal mask future leakage আটকায়।

এটা Transformer-এর বড় efficiency advantage।

---

# 34. Training vs Inference

### Training

```text id="v7d1qk"
<START> I love AI
      ↓
Decoder
      ↓
I love AI <END>
```

Actual target জানা থাকে।

### Inference

```text id="a2u9h8"
<START>
 ↓
Prediction
 ↓
Token 1
 ↓
Prediction
 ↓
Token 2
 ↓
...
```

নিজের generated token ব্যবহার করতে হয়।

---

# 35. Teacher Forcing বনাম Autoregressive Inference

```text id="5slq7b"
TRAINING:

Ground Truth
     ↓
Decoder
     ↓
Next Token


INFERENCE:

Model Prediction
     ↓
Decoder
     ↓
Next Token
     ↓
Prediction আবার input
```

---

# 36. Decoder Input Embedding

Decoder-এর নিজের token IDs-এর জন্যও embedding layer থাকে।

```text id="8r6qko"
Decoder Token IDs
        ↓
Token Embedding
        ↓
Positional Information
        ↓
Masked Self-Attention
```

তাই encoder এবং decoder-এর input representation আলাদা হতে পারে।

---

# 37. Decoder Positional Information

Decoder-ও token order জানতে হবে।

যেমন:

```text
I love AI
```

এবং:

```text
AI love I
```

একই tokens কিন্তু order আলাদা।

তাই decoder input-এ positional information দরকার।

---

# 38. Decoder-এর Full Input Flow

```text id="g4p9f1"
Target-side Tokens
       ↓
Token IDs
       ↓
Embedding
       ↓
Positional Information
       ↓
Masked Self-Attention
       ↓
Cross-Attention
       ↓
FFN
       ↓
Decoder Output
```

---

# 39. Encoder Output কোথায় যায়?

Encoder output:

```text id="9yl1ka"
Encoder
   ↓
Memory
```

তারপর decoder-এর প্রতিটি layer-এর cross-attention-এ:

```text id="e6g0zx"
Encoder Output
      ↓
K + V
```

ব্যবহার করা হয়।

---

# 40. Complete Encoder-Decoder Flow

এখন পুরো architecture:

```text id="i0v0pv"
                    INPUT
                      │
                      ▼
                 TOKENIZER
                      │
                      ▼
                 EMBEDDING
                      │
                      +
                  POSITION
                      │
                      ▼
              ┌───────────────┐
              │    ENCODER    │
              │               │
              │ Self-Attention│
              │ Add + Norm    │
              │ FFN           │
              │ Add + Norm    │
              └───────┬───────┘
                      │
                      ▼
                ENCODER OUTPUT
                      │
                      │ K,V
                      │
                      ▼
              ┌───────────────┐
              │    DECODER    │
              │               │
Target Input →│ Masked Self   │
              │ Attention     │
              │      ↓        │
              │ Add + Norm    │
              │      ↓        │
              │ Cross-Attn ◄──┘
              │      ↓
              │ Add + Norm
              │      ↓
              │ FFN
              │      ↓
              │ Add + Norm
              └───────┬───────┘
                      │
                      ▼
                   Linear
                      │
                      ▼
                   Softmax
                      │
                      ▼
                 Next Token
```

---

# 41. Encoder এবং Decoder-এর Q/K/V পুরোপুরি মনে রাখো

এটা interview-এর জন্য খুব গুরুত্বপূর্ণ।

### Encoder Self-Attention

```text
Q = Encoder
K = Encoder
V = Encoder
```

### Decoder Masked Self-Attention

```text
Q = Decoder
K = Decoder
V = Decoder
```

### Decoder Cross-Attention

```text
Q = Decoder

K = Encoder

V = Encoder
```

এক লাইনে:

```text id="4g9jpv"
Encoder Self:
E → E

Decoder Self:
D → D

Decoder Cross:
D → E
```

---

# 42. Decoder-এর তিনটি Attention Concept

```text id="4b7x9s"
Decoder
   │
   ├── Masked Self-Attention
   │       ↓
   │   Previous target tokens
   │
   ├── Cross-Attention
   │       ↓
   │   Encoder information
   │
   └── FFN
           ↓
      Feature transformation
```

---

# 43. Decoder-only Model-এ Cross-Attention থাকে?

**না।**

এটা অত্যন্ত গুরুত্বপূর্ণ।

GPT-style decoder-only architecture:

```text id="x8h5ko"
Token Embedding
      ↓
Positional Information
      ↓
Masked Self-Attention
      ↓
FFN
      ↓
Repeat
      ↓
Output
```

এখানে:

```text
Cross-Attention ❌
```

কারণ encoder নেই।

---

# 44. Original Transformer বনাম GPT

### Original Transformer

```text
Encoder
   ↓
Decoder
```

### GPT-style

```text
Decoder-only
```

### BERT-style

```text
Encoder-only
```

এই তিনটি distinction খুব গুরুত্বপূর্ণ।

---

# 45. Decoder-only Architecture

GPT-like model:

```text id="o9z2rq"
Input Tokens
     ↓
Embedding
     ↓
Position
     ↓
Masked Self-Attention
     ↓
FFN
     ↓
Repeat many layers
     ↓
LM Head
     ↓
Softmax
     ↓
Next Token
```

এখানে Encoder নেই।

---

# 46. AI Writing Assistant-এ Decoder

তোমার AI writing platform-এর generation অংশ conceptually:

```text id="l1v5zi"
User Prompt
     ↓
Tokenizer
     ↓
Token Embeddings
     ↓
Decoder Transformer
     ↓
Next Token Prediction
     ↓
Generated Text
```

যেমন:

```text
Prompt:
"Rewrite this sentence professionally:"
```

Model:

```text
"The product provides excellent..."
```

এরপর token-by-token generate করবে।

---

# 47. Rewrite System-এ Encoder-Decoder

আরেক ধরনের architecture:

```text id="3b4hkg"
Original Text
     ↓
Encoder
     ↓
Meaning Representation
     ↓
Decoder
     ↓
Rewritten Text
```

এটা sequence-to-sequence model-এর natural design।

---

# 48. Decoder-এর Computational Cost

Causal self-attention-এর জন্য training-এ sequence length `L` হলে standard attention-এর complexity roughly:

$$
O(L^2D)
$$

Inference-এ autoregressive generation-এর সময় প্রতিটি নতুন token-এর জন্য attention computation করতে হয়।

তবে practical implementations **KV cache** ব্যবহার করে repeated computation কমায়।

KV cache আমরা পরবর্তী generation/inference lesson-এ বিস্তারিত দেখব।

---

# 49. Decoder-এর Common Mistakes

### Mistake 1

```text
Decoder = শুধু output layer
```

❌ ভুল।

Decoder একটি **multi-layer neural architecture**।

---

### Mistake 2

```text
Decoder সব future token দেখতে পারে
```

❌ ভুল।

Training-এ causal mask future tokens block করে।

---

### Mistake 3

```text
Cross-Attention = Self-Attention
```

❌ ভুল।

```text
Self:
D → D

Cross:
D → E
```

---

### Mistake 4

```text
GPT = Original Encoder-Decoder Transformer
```

❌ ভুল।

GPT হলো **decoder-only Transformer family**।

---

# 50. PyTorch Decoder Layer

PyTorch-এ:

```python id="b1v7kq"
import torch
import torch.nn as nn


decoder_layer = nn.TransformerDecoderLayer(
    d_model=128,
    nhead=8,
    batch_first=True
)
```

Decoder তৈরি:

```python id="e3q5cw"
decoder = nn.TransformerDecoder(
    decoder_layer,
    num_layers=6
)
```

---

# 51. Decoder Input এবং Memory

```python id="8a6y1h"
target = torch.randn(32, 20, 128)

memory = torch.randn(32, 50, 128)

output = decoder(
    target,
    memory
)

print(output.shape)
```

Output:

```text
torch.Size([32, 20, 128])
```

এখানে:

```text id="g7j8z0"
target
→ Decoder input

memory
→ Encoder output
```

---

# 52. Causal Mask তৈরি

PyTorch-এ conceptual causal mask:

```python id="z8x1q0"
seq_len = 20

mask = torch.triu(
    torch.ones(seq_len, seq_len),
    diagonal=1
).bool()
```

এখানে upper triangular অংশ future positions represent করে।

Implementation details PyTorch version অনুযায়ী mask type/semantics কিছুটা ভিন্ন হতে পারে, তাই API documentation অনুযায়ী ব্যবহার করা উচিত।

---

# 53. Decoder Layer Simplified from Scratch

```python id="8j7p0s"
class SimpleDecoderBlock(nn.Module):

    def __init__(
        self,
        d_model=128,
        num_heads=8,
        d_ff=512
    ):
        super().__init__()

        self.self_attention = nn.MultiheadAttention(
            d_model,
            num_heads,
            batch_first=True
        )

        self.cross_attention = nn.MultiheadAttention(
            d_model,
            num_heads,
            batch_first=True
        )

        self.ffn = nn.Sequential(
            nn.Linear(d_model, d_ff),
            nn.GELU(),
            nn.Linear(d_ff, d_model)
        )

        self.norm1 = nn.LayerNorm(d_model)
        self.norm2 = nn.LayerNorm(d_model)
        self.norm3 = nn.LayerNorm(d_model)

    def forward(
        self,
        x,
        memory,
        causal_mask=None
    ):

        attn_output, _ = self.self_attention(
            x,
            x,
            x,
            attn_mask=causal_mask
        )

        x = self.norm1(
            x + attn_output
        )

        cross_output, _ = self.cross_attention(
            x,
            memory,
            memory
        )

        x = self.norm2(
            x + cross_output
        )

        ffn_output = self.ffn(x)

        x = self.norm3(
            x + ffn_output
        )

        return x
```

এখানে খুব পরিষ্কারভাবে:

```text id="x0m5v9"
Self-Attention:
x, x, x

Cross-Attention:
x, memory, memory

FFN:
x
```

---

# 54. Tensor Shape Example

ধরি:

```text
B = 16
Decoder length = 20
Encoder length = 50
D = 256
Heads = 8
```

Decoder input:

```text
(16, 20, 256)
```

Encoder output:

```text
(16, 50, 256)
```

Self-attention scores:

```text
(16, 8, 20, 20)
```

Cross-attention scores:

```text
(16, 8, 20, 50)
```

Final decoder output:

```text
(16, 20, 256)
```

---

# 55. Decoder Layer-এর Shape Flow

```text id="l0j8c5"
Decoder Input
(16,20,256)
      │
      ▼
Masked Self-Attention
(16,20,256)
      │
      ▼
Cross-Attention
      │
Encoder Memory:
(16,50,256)
      │
      ▼
(16,20,256)
      │
      ▼
FFN
      │
      ▼
(16,20,256)
```

---

# 56. Decoder → Vocabulary

শেষে:

```text id="4v7g8w"
(16, 20, 256)
       ↓
Linear
       ↓
(16, 20, 30000)
       ↓
Softmax
       ↓
Token probabilities
```

প্রতিটি position-এর জন্য:

```text
30,000 possible tokens
```

এর probability distribution পাওয়া যায়।

---

# 57. Loss Function

Language modeling-এর জন্য সাধারণত:

> **Cross-Entropy Loss**

ব্যবহার করা হয়।

ধরি actual target:

```text
AI
```

Model probability:

```text
AI      → 0.8
Python  → 0.1
ML      → 0.05
...
```

তাহলে loss কম হবে।

যদি:

```text
AI → 0.01
```

তাহলে loss বেশি হবে।

---

# 58. Training Objective

Decoder-এর মূল objective:

$$
\max P(y_t|y_{<t},x)
$$

অথবা পুরো sequence:

$$
P(y|x)
=
\prod_{t=1}^{T}
P(y_t|y_{<t},x)
$$

অর্থাৎ:

```text
Previous tokens
+
Input context
       ↓
Next-token probability
```

---

# 59. Decoder-এর Final Mental Model

এটা সবচেয়ে ভালোভাবে মনে রাখো:

```text id="o0y9pz"
                    ENCODER
                       │
                       │ Context
                       ▼
                 ┌──────────────┐
                 │    DECODER   │
                 │              │
Target Tokens →  │ Masked Self  │
                 │ Attention    │
                 │      ↓       │
                 │ Add + Norm   │
                 │      ↓       │
Encoder Context→ │ Cross-Attn   │
                 │      ↓       │
                 │ Add + Norm   │
                 │      ↓       │
                 │ FFN          │
                 │      ↓       │
                 │ Add + Norm   │
                 └──────┬───────┘
                        │
                        ▼
                     Linear
                        │
                        ▼
                     Softmax
                        │
                        ▼
                   Next Token
                        │
                        ▼
                 Feed back again
```

---

# 60. সবচেয়ে গুরুত্বপূর্ণ Q/K/V Summary

এটা **অবশ্যই মুখস্থ নয়—বুঝে রাখতে হবে**:

```text id="6m4zqk"
┌─────────────────────────────┐
│ Encoder Self-Attention      │
│ Q = Encoder                 │
│ K = Encoder                 │
│ V = Encoder                 │
└─────────────────────────────┘

┌─────────────────────────────┐
│ Decoder Self-Attention      │
│ Q = Decoder                 │
│ K = Decoder                 │
│ V = Decoder                 │
│ + Causal Mask               │
└─────────────────────────────┘

┌─────────────────────────────┐
│ Decoder Cross-Attention     │
│ Q = Decoder                 │
│ K = Encoder                 │
│ V = Encoder                 │
└─────────────────────────────┘
```

---

# 61. Encoder বনাম Decoder — Final Comparison

| Feature         | Encoder        | Decoder                        |
| --------------- | -------------- | ------------------------------ |
| Self-Attention  | Yes            | Yes                            |
| Causal Mask     | No             | Yes                            |
| Full context    | Yes            | No, causal self-attention      |
| Cross-Attention | No             | Original encoder-decoder-এ Yes |
| FFN             | Yes            | Yes                            |
| Residual        | Yes            | Yes                            |
| LayerNorm       | Yes            | Yes                            |
| Main purpose    | Representation | Generation                     |
| BERT            | Yes            | No                             |
| GPT             | No             | Decoder-only                   |
| T5              | Yes            | Yes                            |

---

# 62. M02.26-এর 15টি Must-Know Concept

```text
☐ Transformer Decoder
☐ Decoder Layer
☐ Decoder Input
☐ Shifted-Right Target
☐ Masked Self-Attention
☐ Causal Mask
☐ Cross-Attention
☐ Decoder Q/K/V
☐ Encoder K/V
☐ Residual Connection
☐ LayerNorm
☐ FFN
☐ Autoregressive Generation
☐ Teacher Forcing
☐ Output Projection + Softmax
```

---

# 63. Interview Questions

### Q1. Transformer Decoder কী?

Decoder হলো Transformer-এর generation-oriented অংশ, যা causal self-attention এবং original encoder-decoder architecture-এ cross-attention ব্যবহার করে output sequence তৈরি করে।

---

### Q2. Decoder-এ causal mask কেন?

Future tokens যেন prediction-এর সময় দেখা না যায়।

---

### Q3. Decoder self-attention-এর Q/K/V কী?

```text
Q = Decoder
K = Decoder
V = Decoder
```

---

### Q4. Cross-attention-এর Q/K/V কী?

```text
Q = Decoder
K = Encoder
V = Encoder
```

---

### Q5. GPT-তে cross-attention কেন নেই?

কারণ GPT-style architecture হলো **decoder-only**; সেখানে separate encoder নেই।

---

### Q6. Teacher forcing কী?

Training-এর সময় previous ground-truth token decoder input হিসেবে দেওয়া।

---

### Q7. Training এবং inference-এর difference?

```text
Training:
Ground-truth previous tokens

Inference:
Model-generated previous tokens
```

---

### Q8. Decoder কেন autoregressive?

কারণ output token সাধারণত previous output tokens-এর উপর conditional।

$$
P(y_t|y_{<t},x)
$$

---

# 64. Practice

### Beginner

একটি decoder layer তৈরি করো:

```text
d_model = 128
heads = 8
d_ff = 512
```

Input:

```text
(4, 20, 128)
```

Encoder memory:

```text
(4, 30, 128)
```

Expected output:

```text
(4, 20, 128)
```

---

### Intermediate

একটি causal mask তৈরি করো এবং verify করো:

```text
Future positions = blocked
Past/current = allowed
```

---

### Advanced

Mini encoder-decoder model বানাও:

```text
Input
 ↓
Embedding
 ↓
Encoder
 ↓
Memory
 ↓
Decoder
 ↓
Linear
 ↓
Softmax
```

---

# 65. M02.24 → M02.26 পুরো connection

এখন তোমার mental map:

```text id="7w6r6k"
M02.23
Positional Encoding
       ↓
M02.24
Transformer Architecture
       ↓
M02.25
Transformer Encoder
       ↓
M02.26
Transformer Decoder
       ↓
       ├── Masked Self-Attention
       ├── Cross-Attention
       ├── FFN
       ├── Causal Mask
       └── Autoregressive Generation
```

এর পর আমরা masking-কে আলাদা করে গভীরভাবে নেব, কারণ এটি Encoder/Decoder উভয়ের জন্য গুরুত্বপূর্ণ।

### পরবর্তী:

**M02.27 — Transformer Masking Deep Dive**

এখানে আমরা **Padding Mask, Causal Mask, Attention Mask, Encoder Mask, Decoder Mask, Cross-Attention Mask, mask tensor shapes এবং PyTorch-এ mask implementation** একসাথে গভীরভাবে শিখব।

**M02.26 — Complete ✅**


------
# M02.27 — Transformer Masking Deep Dive

আজ আমরা **Transformer Masking** একদম foundation থেকে deep level পর্যন্ত শিখব।

M02.24 → Transformer Architecture
M02.25 → Transformer Encoder
M02.26 → Transformer Decoder
আজ:

> **M02.27 → Masking**

Masking ভালোভাবে না বুঝলে **BERT, GPT, T5, attention, text generation, padding, causal language modeling**—কোনোটাই পুরোপুরি পরিষ্কার হবে না।

---

# 1. Mask কী?

Transformer-এ **mask** হলো এমন একটি mechanism যা বলে দেয়:

> **কোন token-এর দিকে attention করা যাবে এবং কোন token-এর দিকে attention করা যাবে না।**

সহজভাবে:

```text
Token A
  ↓
কোন token দেখতে পারবে?
  ↓
Mask সিদ্ধান্ত নেয়
```

উদাহরণ:

```text
I love AI <PAD>
```

এখানে `<PAD>` কোনো real information নয়।

তাই:

```text
I → PAD ❌
love → PAD ❌
AI → PAD ❌
```

---

# 2. Mask কেন প্রয়োজন?

Transformer-এ প্রধানত দুই ধরনের সমস্যা সমাধান করতে mask লাগে:

```text
1. Padding problem
2. Future-token problem
```

অর্থাৎ:

```text
Padding Mask
     +
Causal Mask
```

এগুলো সবচেয়ে গুরুত্বপূর্ণ।

---

# 3. প্রথমে Attention মনে করি

Scaled dot-product attention:

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

প্রথমে:

```text
QKᵀ
```

থেকে attention scores তৈরি হয়।

তারপর:

```text
Softmax
```

থেকে attention weights।

Mask এই score calculation-এর আগে/সময় unwanted positions block করতে পারে।

---

# 4. Mask কোথায় Apply হয়?

Conceptually:

```text id="n4v1gs"
QKᵀ
 ↓
Add Mask
 ↓
Softmax
 ↓
Attention Weights
 ↓
V
```

অর্থাৎ:

$$
Scores = \frac{QK^T}{\sqrt{d_k}}
$$

তারপর:

$$
MaskedScores = Scores + M
$$

তারপর:

$$
Attention = softmax(MaskedScores)V
$$

---

# 5. Mask-এর দুইটি Basic Value

সাধারণভাবে additive mask-এ:

```text
Allowed position
→ 0

Blocked position
→ -∞
```

তারপর:

$$
softmax(-\infty)\approx0
$$

তাই blocked token-এর attention weight প্রায় zero হয়ে যায়।

---

# 6. Example

ধরি attention scores:

```text
[2.0, 1.0, 3.0, 4.0]
```

কিন্তু শেষ token block করতে হবে।

Mask:

```text
[0, 0, 0, -∞]
```

যোগ করলে:

```text
[2.0, 1.0, 3.0, -∞]
```

Softmax:

```text
[~0.24, ~0.09, ~0.67, 0]
```

শেষ token:

```text
0
```

attention পাবে।

---

# 7. Padding কী?

Batch processing-এর জন্য সাধারণত sequence একই length করতে হয়।

ধরি:

```text
Sentence 1:
I love AI

Sentence 2:
I love machine learning
```

Length:

```text
3
4
```

Batch করতে:

```text
I love AI <PAD>
I love machine learning
```

`<PAD>` হলো padding token।

---

# 8. Padding Mask

Padding token-এর দিকে attention prevent করতে:

> **Padding Mask**

ব্যবহার করা হয়।

Example:

```text id="m7y8jg"
I       → valid
love    → valid
AI      → valid
<PAD>   → ignore
```

Mask:

```text id="m6g12m"
[False, False, False, True]
```

এখানে ধরলাম:

```text
True = ignore
False = valid
```

তবে framework/API অনুযায়ী boolean mask-এর semantics উল্টো হতে পারে—এটা implementation-এর সময় অবশ্যই check করতে হবে।

---

# 9. Padding Mask-এর উদ্দেশ্য

Padding Mask:

```text id="w4l2a9"
Real token
     ↓
Attention allowed

<PAD>
     ↓
Attention blocked
```

অর্থাৎ:

```text
Padding = meaningless
```

Model যেন padding থেকে information শেখার চেষ্টা না করে।

---

# 10. Padding Mask Matrix

ধরি:

```text id="n8j1se"
I love AI <PAD>
```

Attention matrix conceptually:

```text
             I   love  AI   PAD

I            ✓    ✓    ✓    ✗
love         ✓    ✓    ✓    ✗
AI           ✓    ✓    ✓    ✗
PAD          ✗    ✗    ✗    ✗
```

শেষ row-এর behaviour implementation এবং whether padded query outputs are later used can vary; the key requirement is that padded **key/value positions** should not contribute meaningful attention.

---

# 11. Padding Mask-এর সবচেয়ে গুরুত্বপূর্ণ বিষয়

অনেকে ভাবে:

> "Padding mask শুধু PAD row block করে।"

মূল উদ্দেশ্য হলো:

> **PAD positions যেন attention-এর Key/Value হিসেবে information contribute না করে।**

অর্থাৎ:

```text
Query → PAD Key
```

block করা অত্যন্ত গুরুত্বপূর্ণ।

---

# 12. Causal Mask কী?

এবার দ্বিতীয় গুরুত্বপূর্ণ mask।

**Causal Mask** future token block করে।

এটি বিশেষভাবে decoder এবং autoregressive language modeling-এ ব্যবহৃত হয়।

---

# 13. কেন Causal Mask দরকার?

ধরি:

```text
I love machine learning
```

Model `"machine"` predict করবে।

সে যেন `"learning"` দেখতে না পারে।

কারণ `"learning"` future token।

```text
machine → I ✓
machine → love ✓
machine → machine ✓
machine → learning ❌
```

---

# 14. Causal Mask Matrix

ধরি sequence:

```text
T1 T2 T3 T4
```

Causal attention:

```text
       T1 T2 T3 T4

T1     ✓  ✗  ✗  ✗
T2     ✓  ✓  ✗  ✗
T3     ✓  ✓  ✓  ✗
T4     ✓  ✓  ✓  ✓
```

অর্থাৎ:

```text
Past + Current → allowed
Future → blocked
```

---

# 15. Causal Mask Visualize

```text
        Key
        ↓
       1  2  3  4

Q 1    ✓  ✗  ✗  ✗
u 2    ✓  ✓  ✗  ✗
e 3    ✓  ✓  ✓  ✗
r 4    ✓  ✓  ✓  ✓
y
```

এটি একটি **lower-triangular attention pattern**।

---

# 16. Causal Mask কেন "Causal"?

কারণ model:

$$
P(x_t|x_1,x_2,\dots,x_{t-1})
$$

এর মতো autoregressive dependency অনুসরণ করে।

অর্থাৎ:

```text
Past
 ↓
Current
```

Future থেকে information নেওয়া যাবে না।

---

# 17. Causal Mask তৈরি

PyTorch-এ একটি সাধারণ triangular mask:

```python
import torch

seq_len = 5

mask = torch.triu(
    torch.ones(seq_len, seq_len),
    diagonal=1
).bool()

print(mask)
```

Conceptually:

```text
False True  True  True  True
False False True  True  True
False False False True  True
False False False False True
False False False False False
```

এখানে:

```text
True
→ future position
```

ধরা হয়েছে।

---

# 18. Additive Causal Mask

আরেকভাবে:

```python
mask = torch.triu(
    torch.ones(seq_len, seq_len),
    diagonal=1
)

mask = mask.masked_fill(
    mask == 1,
    float("-inf")
)

mask = mask.masked_fill(
    mask == 0,
    0.0
)
```

তাহলে conceptually:

```text
0     -∞    -∞    -∞
0      0    -∞    -∞
0      0     0    -∞
0      0     0     0
```

---

# 19. Padding Mask বনাম Causal Mask

এটা অবশ্যই পরিষ্কার থাকতে হবে।

| বিষয়                | Padding Mask              | Causal Mask                |
| ------------------- | ------------------------- | -------------------------- |
| কী block করে?       | PAD token                 | Future token               |
| কেন?                | Fake padding              | Future information leakage |
| Encoder             | সাধারণত Yes               | No                         |
| Decoder             | Yes                       | Yes                        |
| GPT                 | সাধারণত padding থাকলে Yes | Yes                        |
| BERT                | Yes, padding থাকলে        | No                         |
| Translation Decoder | Yes                       | Yes                        |

---

# 20. Encoder Mask

Standard Transformer Encoder:

```text
Full context
```

তাই:

```text
Causal Mask ❌
Padding Mask ✅
```

Conceptually:

```text id="x8f2cs"
The student reads a book.

The      → সব valid tokens
student  → সব valid tokens
reads    → সব valid tokens
a        → সব valid tokens
book     → সব valid tokens
```

---

# 21. Encoder Attention

Encoder-এ:

```text
       T1 T2 T3 T4

T1     ✓  ✓  ✓  ✓
T2     ✓  ✓  ✓  ✓
T3     ✓  ✓  ✓  ✓
T4     ✓  ✓  ✓  ✓
```

যদি padding থাকে:

```text
       T1 T2 T3 PAD

T1     ✓  ✓  ✓  ✗
T2     ✓  ✓  ✓  ✗
T3     ✓  ✓  ✓  ✗
```

---

# 22. Decoder Mask

Decoder-এ সাধারণত দুটো mask গুরুত্বপূর্ণ:

```text
1. Causal Mask
2. Padding Mask
```

কারণ decoder:

```text
Future token দেখতে পারবে না
```

এবং:

```text
PAD token ignore করতে হবে
```

---

# 23. Decoder Self-Attention

ধরি:

```text
I love AI <PAD>
```

Causal + Padding দুটোই দরকার হতে পারে।

Conceptually:

```text
          I  love  AI  PAD

I         ✓   ✗    ✗   ✗
love      ✓   ✓    ✗   ✗
AI        ✓   ✓    ✓   ✗
PAD       ?   ?    ?   ✗
```

মূল লক্ষ্য:

```text
Future → blocked
PAD → ignored
```

Padded query row-এর exact treatment implementation-specific হতে পারে, এবং padded outputs সাধারণত downstream loss/pooling-এও ignore করা হয়।

---

# 24. Decoder Cross-Attention-এ কী Mask লাগে?

Cross-attention:

```text
Q = Decoder
K = Encoder
V = Encoder
```

এখানে সাধারণত:

```text
Encoder Padding Mask
```

দরকার হতে পারে।

কারণ decoder যেন encoder-এর padded positions attend না করে।

---

# 25. Cross-Attention Matrix

ধরি:

```text
Encoder:
I love AI <PAD>

Decoder:
আমি love করি
```

Encoder length:

```text
4
```

Decoder length:

```text
3
```

Cross-attention matrix:

```text
              Encoder

              I love AI PAD

Decoder 1     ✓  ✓   ✓  ✗
Decoder 2     ✓  ✓   ✓  ✗
Decoder 3     ✓  ✓   ✓  ✗
```

এখানে:

```text
PAD → blocked
```

---

# 26. Cross-Attention-এ Causal Mask?

সাধারণ encoder-decoder Transformer cross-attention-এ decoder-to-encoder attention-এর জন্য **causal mask সাধারণত ব্যবহার করা হয় না**।

কারণ encoder input-এর পুরো sequence available।

```text
Decoder Query
      ↓
Encoder Keys/Values
      ↓
All valid encoder positions
```

শুধু padding বা অন্য task-specific constraints mask করা হতে পারে।

---

# 27. Three Important Attention Situations

এখন খুব পরিষ্কার:

### Encoder Self-Attention

```text
Q = Encoder
K = Encoder
V = Encoder

Padding Mask → Yes
Causal Mask  → No
```

### Decoder Self-Attention

```text
Q = Decoder
K = Decoder
V = Decoder

Padding Mask → Yes, if needed
Causal Mask  → Yes
```

### Decoder Cross-Attention

```text
Q = Decoder
K = Encoder
V = Encoder

Encoder Padding Mask → Yes, if needed
Causal Mask          → Normally No
```

---

# 28. Combined Mask

কখনও একাধিক constraint একসাথে লাগতে পারে।

যেমন decoder:

```text
Causal constraint
+
Padding constraint
```

তখন combined mask:

```text
Final Mask
=
Causal Mask
+
Padding Mask
```

ধারণাগতভাবে।

বাস্তব implementation-এ boolean mask, additive mask, key padding mask ইত্যাদি আলাদাভাবে API-তে দেওয়া হতে পারে।

---

# 29. Attention Mask vs Padding Mask

এখানে terminology একটু confusing।

Framework অনুযায়ী:

```text
attention_mask
key_padding_mask
causal_mask
```

ভিন্ন অর্থ হতে পারে।

তাই:

> **"attention mask" শব্দটি universal এক অর্থে ব্যবহার হয় না।**

এটা গুরুত্বপূর্ণ।

---

# 30. PyTorch-এর ক্ষেত্রে

PyTorch-এর `MultiheadAttention`-এ গুরুত্বপূর্ণ arguments:

```python
nn.MultiheadAttention(
    embed_dim,
    num_heads,
    batch_first=True
)
```

Forward:

```python
output, weights = attention(
    query,
    key,
    value,
    attn_mask=...,
    key_padding_mask=...
)
```

Conceptually:

```text
attn_mask
→ attention relationship constraint

key_padding_mask
→ কোন key positions padding
```

Exact shape and semantics version/API documentation অনুযায়ী verify করা উচিত।

---

# 31. Padding Mask Example — PyTorch

ধরি:

```python
tokens = torch.tensor([
    [10, 20, 30, 0],
    [40, 50, 60, 70]
])
```

এখানে:

```text
0 = PAD
```

Mask:

```python
padding_mask = tokens == 0
```

Output:

```text
[
 [False, False, False, True],
 [False, False, False, False]
]
```

এখানে:

```text
True → padding
```

---

# 32. Causal Mask — PyTorch

```python
seq_len = 4

causal_mask = torch.triu(
    torch.ones(
        seq_len,
        seq_len,
        dtype=torch.bool
    ),
    diagonal=1
)

print(causal_mask)
```

Conceptually:

```text
False True  True  True
False False True  True
False False False True
False False False False
```

---

# 33. Multi-Head Attention-এর সঙ্গে Mask

ধরি:

```text
B = 2
H = 8
L = 100
D = 512
```

Attention scores:

```text
(B, H, L, L)
```

অর্থাৎ:

```text
(2, 8, 100, 100)
```

Mask এমনভাবে broadcast/expand হতে পারে যাতে blocked positions সব heads-এর জন্য apply হয়।

---

# 34. Mask Shape কেন গুরুত্বপূর্ণ?

ধরি:

```text
Attention score:
(2, 8, 100, 100)
```

Mask যদি:

```text
(100, 100)
```

হয়, তাহলে framework broadcasting ব্যবহার করে সেটি multiple batch/head-এর জন্য apply করতে পারে।

অন্যদিকে padding mask:

```text
(2, 100)
```

হতে পারে।

তারপর framework appropriate dimensions-এ ব্যবহার করে।

---

# 35. Important Shape Patterns

সাধারণ ধারণা:

```text
Self-attention score:

(B, H, L, L)
```

Causal mask:

```text
(L, L)
```

Padding mask:

```text
(B, L)
```

Cross-attention score:

```text
(B, H, L_decoder, L_encoder)
```

Encoder padding:

```text
(B, L_encoder)
```

---

# 36. Mask Broadcasting

ধরি:

```text
Attention:

(B,H,L,L)
```

Causal mask:

```text
(L,L)
```

Conceptually:

```text
          (L,L)
            ↓
     Broadcast across
       B and H
            ↓
       (B,H,L,L)
```

এজন্য একই causal pattern সব batch এবং heads-এ ব্যবহার করা যায়।

---

# 37. Why Padding Mask is Different

Padding প্রতিটি sample-এর জন্য আলাদা হতে পারে।

Example:

```text
Sample 1:
I love AI <PAD>

Sample 2:
I love machine learning
```

Mask:

```text
Sample 1:
[False False False True]

Sample 2:
[False False False False]
```

তাই padding mask সাধারণত batch-dependent।

---

# 38. Masking + Softmax

এটা খুব গুরুত্বপূর্ণ।

ধরি scores:

```text
[2.0, 1.0, 3.0, 4.0]
```

Future block:

```text
[2.0, 1.0, 3.0, -∞]
```

Softmax:

```text
[0.24, 0.09, 0.67, 0.00]
```

তাই:

```text
Blocked token
→ 0 attention
```

---

# 39. Masking Before Softmax কেন?

যদি softmax-এর পরে mask করি:

```text
Scores
 ↓
Softmax
 ↓
Mask
```

তাহলে weights-এর normalization নষ্ট হতে পারে।

তাই standard additive masking-এর ধারণা:

```text
Scores
 ↓
Mask
 ↓
Softmax
 ↓
Normalized attention
```

---

# 40. Masking-এর Mathematical Flow

$$
S = \frac{QK^T}{\sqrt{d_k}}
$$

তারপর:

$$
S' = S + M
$$

তারপর:

$$
A = softmax(S')
$$

তারপর:

$$
Output = AV
$$

Complete:

```text id="e7e9cj"
Q,K
 ↓
QKᵀ
 ↓
Scale
 ↓
Mask
 ↓
Softmax
 ↓
Attention Weights
 ↓
× V
 ↓
Output
```

---

# 41. BERT-এ Masking

BERT encoder-only architecture।

সাধারণ attention:

```text
Full bidirectional context
```

তাই:

```text
Causal Mask ❌
Padding Mask ✅
```

কিন্তু BERT-এর pretraining-এ আরেকটি আলাদা concept আছে:

> **Masked Language Modeling (MLM)**

এটা attention mask-এর সঙ্গে গুলিয়ে ফেলবে না।

---

# 42. Attention Mask বনাম Masked Language Modeling

খুব গুরুত্বপূর্ণ distinction:

### Attention Mask

```text
কোন token-এর দিকে attention করা যাবে?
```

### MLM

```text
কোন token input-এর মধ্যে hide/corrupt করা হবে?
```

উদাহরণ:

```text
I love [MASK].
```

এখানে `[MASK]` হলো MLM training objective-এর অংশ।

এটা causal attention mask-এর মতো একই জিনিস নয়।

---

# 43. GPT-তে Masking

GPT-style decoder-only model:

```text
Causal Self-Attention
```

ব্যবহার করে।

```text
T1 → T1
T2 → T1,T2
T3 → T1,T2,T3
T4 → T1,T2,T3,T4
```

অর্থাৎ:

```text
Future token → blocked
```

এটাই GPT-এর autoregressive nature-এর foundation।

---

# 44. BERT vs GPT Masking

|                         | BERT      | GPT                          |
| ----------------------- | --------- | ---------------------------- |
| Architecture            | Encoder   | Decoder-only                 |
| Causal mask             | ❌         | ✅                            |
| Full context            | ✅         | ❌                            |
| Padding mask            | সাধারণত ✅ | প্রয়োজন হলে ✅                |
| Main training objective | MLM-style | Causal next-token prediction |

---

# 45. T5 / Encoder-Decoder Masking

T5-like architecture:

```text
Encoder
+
Decoder
```

Encoder:

```text
Padding mask
```

Decoder self-attention:

```text
Causal mask
+
Padding mask if needed
```

Decoder cross-attention:

```text
Encoder padding mask
```

---

# 46. Masking-এর Real Architecture

```text id="f5t6xm"
                    TRANSFORMER
                        │
          ┌─────────────┴─────────────┐
          │                           │
       ENCODER                     DECODER
          │                           │
   Self-Attention              Self-Attention
          │                           │
   Padding Mask                 Causal Mask
                                      +
                                Padding Mask
                                      │
                                      ▼
                                Cross-Attention
                                      │
                               Encoder Padding
                                    Mask
```

---

# 47. Masking এবং Long Context

Sequence length বাড়লে:

```text
L ↑
 ↓
Attention matrix L×L ↑
 ↓
Mask matrix-ও L×L
```

উদাহরণ:

```text
L = 1,000
→ 1,000 × 1,000

L = 10,000
→ 10,000 × 10,000
```

তাই long-context models-এর ক্ষেত্রে attention/masking efficiently implement করা গুরুত্বপূর্ণ।

---

# 48. Efficient Causal Attention

Modern systems সাধারণত naive Python loops ব্যবহার করে না।

বরং optimized GPU kernels / fused attention implementations ব্যবহার করতে পারে।

যেমন conceptually:

```text
Naive Attention
      ↓
Memory heavy

Optimized Attention
      ↓
Better memory efficiency
      ↓
Faster training/inference
```

**FlashAttention**-এর মতো techniques attention computation ও memory access optimize করে।

এটা আমরা পরে advanced Transformer/LLM section-এ আরও বিস্তারিত করতে পারি।

---

# 49. KV Cache এবং Mask

Autoregressive inference-এ:

```text
Token 1
 ↓
Token 2
 ↓
Token 3
 ↓
Token 4
```

প্রতিবার আগের সব K/V আবার calculate না করে:

```text
K cache
V cache
```

রাখা যায়।

Causal nature তখনও বজায় থাকে।

Conceptually:

```text
Previous K,V
     ↓
Cache
     ↓
New Query
     ↓
Attention
     ↓
Next Token
```

KV cache আমরা generation optimization-এর অংশ হিসেবে পরে আরও বিস্তারিত দেখব।

---

# 50. Masking-এর Common Mistake

### Mistake 1

```text
Padding Mask = Causal Mask
```

❌ ভুল।

```text
Padding Mask
→ PAD block

Causal Mask
→ Future block
```

---

### Mistake 2

```text
BERT-এ causal mask থাকে
```

❌ Standard BERT encoder-এ causal mask থাকে না।

---

### Mistake 3

```text
GPT future token দেখতে পারে
```

❌ Causal mask future token block করে।

---

### Mistake 4

```text
[MASK] token = Attention Mask
```

❌ দুটি আলাদা concept।

---

# 51. Masking-এর সবচেয়ে গুরুত্বপূর্ণ Mental Model

```text id="dy4hjj"
                 ATTENTION
                     │
             ┌───────┴────────┐
             │                │
             ▼                ▼
        What is valid?    What is forbidden?
             │                │
             ▼                ▼
          MASKING         MASKING
             │
      ┌──────┴───────────┐
      │                  │
      ▼                  ▼
Padding Mask         Causal Mask
      │                  │
      ▼                  ▼
Ignore PAD          Ignore Future
```

---

# 52. Complete Masking Flow

```text id="jz9w5p"
                Q, K, V
                   │
                   ▼
              QKᵀ / √d
                   │
                   ▼
              ┌─────────┐
              │  MASK   │
              └────┬────┘
                   │
          ┌────────┴─────────┐
          │                  │
          ▼                  ▼
    Padding Mask        Causal Mask
          │                  │
          ▼                  ▼
      Ignore PAD        Ignore Future
          │                  │
          └────────┬─────────┘
                   ▼
                Softmax
                   │
                   ▼
           Attention Weights
                   │
                   ▼
                   × V
                   │
                   ▼
                Output
```

---

# 53. Mini PyTorch Example

```python
import torch
import torch.nn as nn

batch_size = 2
seq_len = 5
d_model = 128
num_heads = 8

attention = nn.MultiheadAttention(
    embed_dim=d_model,
    num_heads=num_heads,
    batch_first=True
)

x = torch.randn(
    batch_size,
    seq_len,
    d_model
)

# Causal mask
causal_mask = torch.triu(
    torch.ones(
        seq_len,
        seq_len,
        dtype=torch.bool
    ),
    diagonal=1
)

# Padding mask
# Example: last token of first sample is PAD
padding_mask = torch.tensor([
    [False, False, False, False, True],
    [False, False, False, False, False]
])

output, weights = attention(
    x,
    x,
    x,
    attn_mask=causal_mask,
    key_padding_mask=padding_mask
)

print(output.shape)
```

Expected:

```text
torch.Size([2, 5, 128])
```

এখানে:

```text
attn_mask
→ causal constraint

key_padding_mask
→ PAD constraint
```

---

# 54. Encoder Example

Encoder-এর ক্ষেত্রে:

```python
output, weights = attention(
    x,
    x,
    x,
    key_padding_mask=padding_mask
)
```

এখানে:

```text
Causal mask নেই
```

কারণ encoder full context দেখতে পারে।

---

# 55. Decoder Self-Attention Example

```python
output, weights = attention(
    x,
    x,
    x,
    attn_mask=causal_mask,
    key_padding_mask=padding_mask
)
```

এখানে:

```text
Causal
+
Padding
```

দুটো constraint আছে।

---

# 56. Cross-Attention Example

ধরি:

```python
decoder_x = torch.randn(2, 5, 128)
encoder_x = torch.randn(2, 8, 128)
```

Cross-attention:

```python
output, weights = attention(
    decoder_x,
    encoder_x,
    encoder_x,
    key_padding_mask=encoder_padding_mask
)
```

এখানে:

```text
Q = decoder_x

K = encoder_x

V = encoder_x
```

---

# 57. Mask-এর Shape Summary

### Self-Attention

```text
Q:
(B, H, Lq, D)

K:
(B, H, Lk, D)

Scores:
(B, H, Lq, Lk)
```

যদি self-attention:

```text
Lq = Lk = L
```

তাই:

```text
(B,H,L,L)
```

---

### Causal Mask

```text
(L,L)
```

---

### Padding Mask

```text
(B,L)
```

---

### Cross-Attention

```text
Scores:

(B,H,L_decoder,L_encoder)
```

---

# 58. Exam Question

### প্রশ্ন:

Decoder self-attention-এ কোন দুই ধরনের mask ব্যবহার করা হতে পারে?

### উত্তর:

```text
1. Causal Mask
2. Padding Mask
```

---

### প্রশ্ন:

Encoder self-attention-এ causal mask কেন ব্যবহার করা হয় না?

**উত্তর:**

কারণ standard encoder bidirectional/full-context representation তৈরি করে এবং future tokens block করার প্রয়োজন নেই।

---

### প্রশ্ন:

Cross-attention-এ causal mask সাধারণত কেন লাগে না?

**উত্তর:**

কারণ decoder encoder-এর সম্পূর্ণ input representation থেকে information নিতে পারে। তবে encoder padding positions ignore করার জন্য padding mask প্রয়োজন হতে পারে।

---

# 59. Interview Question — Very Important

### Q: Attention Mask কী?

**Answer:**

Attention Mask হলো এমন mechanism যা attention calculation-এর সময় নির্দিষ্ট token positions-কে allowed বা blocked হিসেবে নির্ধারণ করে।

---

### Q: Padding Mask কী?

**Answer:**

Padding Mask padded token positions-কে attention-এর Key/Value হিসেবে ignore করতে সাহায্য করে।

---

### Q: Causal Mask কী?

**Answer:**

Causal Mask future tokens-এর দিকে attention block করে, যাতে autoregressive model শুধুমাত্র previous/current context ব্যবহার করে next token predict করতে পারে।

---

### Q: BERT-এ causal mask কেন নেই?

**Answer:**

BERT encoder bidirectional contextual representation শেখে এবং input-এর উভয় দিকের context ব্যবহার করতে পারে।

---

### Q: GPT-তে causal mask কেন?

**Answer:**

GPT autoregressive next-token prediction করে। Future token দেখা গেলে training-এর সময় information leakage হবে।

---

# 60. M02.27 — Practice

## Beginner

এই sentence:

```text
I love AI <PAD>
```

এর padding mask তৈরি করো।

Expected concept:

```text
False False False True
```

---

## Intermediate

এই sequence:

```text
I love machine learning
```

এর causal mask matrix তৈরি করো।

Expected:

```text
✓ ✗ ✗ ✗
✓ ✓ ✗ ✗
✓ ✓ ✓ ✗
✓ ✓ ✓ ✓
```

---

## Advanced

একটি decoder self-attention তৈরি করো যেখানে:

```text
d_model = 128
heads = 8
```

এবং:

```text
Causal Mask
+
Padding Mask
```

দুটো apply করবে।

---

# 61. Challenge

নিজে একটি mini Transformer masking pipeline তৈরি করো:

```text
Token IDs
   ↓
Padding Detection
   ↓
Padding Mask
   ↓
Causal Mask
   ↓
Self-Attention
   ↓
Masked Attention
   ↓
Output
```

তারপর verify করো:

```text
☐ PAD token ignored
☐ Future token ignored
☐ Past token visible
☐ Current token visible
```

---

# 62. M02.27 Completion Checklist

```text
☐ Mask কী?

☐ Attention-এর কোথায় mask apply হয়?

☐ Padding কী?

☐ Padding Mask কী?

☐ Causal Mask কী?

☐ Padding Mask বনাম Causal Mask

☐ Encoder Masking

☐ Decoder Self-Attention Masking

☐ Cross-Attention Masking

☐ Attention Mask বনাম Padding Mask

☐ Q/K/V-এর সাথে mask-এর সম্পর্ক

☐ Mask + Softmax

☐ -∞ masking

☐ Causal Matrix

☐ Padding Matrix

☐ Combined Mask

☐ Mask Tensor Shapes

☐ PyTorch mask implementation

☐ BERT masking

☐ GPT masking

☐ T5 masking
```

---

# 🧠 Final Master Mental Model

এই diagram-টা অবশ্যই বুঝে রাখো:

```text
                         TRANSFORMER
                              │
             ┌────────────────┼────────────────┐
             │                │                │
             ▼                ▼                ▼
          ENCODER       DECODER SELF       CROSS
        SELF-ATTENTION   ATTENTION       ATTENTION
             │                │                │
             │                │                │
       Padding Mask      Causal Mask    Encoder Padding
             │                +                Mask
             │          Padding Mask            │
             │                │                │
             ▼                ▼                ▼
        Full Context      Past + Current    Encoder Context
```

আর attention-এর ভিতরে:

```text
QKᵀ
 ↓
Scale
 ↓
MASK
 ↓
Softmax
 ↓
Attention Weights
 ↓
× V
 ↓
Output
```

সবশেষে **এক লাইনে**:

> **Padding Mask বলে “কোন PAD token ignore করব”, আর Causal Mask বলে “কোন future token দেখতে পারব না।”**

### M02 Progress

```text
M02.23 → Positional Encoding              ✅
M02.24 → Transformer Architecture         ✅
M02.25 → Transformer Encoder              ✅
M02.26 → Transformer Decoder              ✅
M02.27 → Transformer Masking              ✅
```

**পরবর্তী: M02.28 — BERT Architecture Deep Dive**

সেখানে আমরা **BERT-এর input representation, `[CLS]`, `[SEP]`, token/type/position embeddings, bidirectional attention, MLM, pretraining, fine-tuning, BERT encoder layers এবং BERT-এর real NLP applications** একদম foundation থেকে শিখব।


---
# M02.28 — BERT Architecture Deep Dive

আজ আমরা **BERT** একদম foundation থেকে deep level পর্যন্ত শিখব।

আগের lessons-এর সাথে connection:

```text
M02.20 → Attention
M02.21 → Self-Attention
M02.22 → Multi-Head Attention
M02.23 → Positional Encoding
M02.24 → Transformer
M02.25 → Encoder
M02.26 → Decoder
M02.27 → Masking
             ↓
M02.28 → BERT
```

BERT বুঝতে পারলে তুমি **Transformer Encoder, contextual embedding, NER, classification, semantic similarity, text understanding** অনেক বেশি পরিষ্কারভাবে বুঝতে পারবে।

---

# 1. BERT কী?

**BERT = Bidirectional Encoder Representations from Transformers**

BERT হলো একটি **Transformer Encoder-based language representation model**।

মূল idea:

> একটি token-এর representation তৈরি করার সময় তার **left context এবং right context—দুই দিকের context** ব্যবহার করা।

উদাহরণ:

```text
The bank is near the river.
```

এখানে `bank` বুঝতে model দেখতে পারে:

```text
left:
The

right:
is near the river
```

তাই `bank`-এর contextual meaning ভালোভাবে বোঝা যায়।

---

# 2. BERT কেন গুরুত্বপূর্ণ?

BERT আসার আগে NLP-তে অনেক model ছিল:

```text
Bag of Words
TF-IDF
Word2Vec
GloVe
RNN
LSTM
```

এগুলোর limitations ছিল।

BERT Transformer-এর self-attention ব্যবহার করে প্রতিটি token-এর জন্য contextual representation তৈরি করে।

---

# 3. BERT-এর Core Idea

BERT:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Token + Segment + Position Embeddings
 ↓
Transformer Encoder
 ↓
Contextual Representations
 ↓
NLP Task
```

---

# 4. BERT Architecture

BERT হলো:

```text
Encoder-only Transformer
```

অর্থাৎ:

```text
BERT
 ↓
Transformer Encoder
 ↓
Self-Attention
 ↓
FFN
 ↓
Contextual Representation
```

BERT-এর মধ্যে GPT-style decoder নেই।

---

# 5. BERT vs Original Transformer

Original Transformer:

```text
Encoder
+
Decoder
```

BERT:

```text
Encoder only
```

GPT:

```text
Decoder only
```

T5-style:

```text
Encoder
+
Decoder
```

---

# 6. BERT-এর High-Level Architecture

```text
                    INPUT TEXT
                        │
                        ▼
                    TOKENIZER
                        │
                        ▼
                    TOKEN IDs
                        │
             ┌──────────┼──────────┐
             ▼          ▼          ▼
          Token      Segment     Position
        Embedding   Embedding   Embedding
             │          │          │
             └──────────┼──────────┘
                        ▼
                    ADD TOGETHER
                        │
                        ▼
                Transformer Encoder
                        │
             ┌──────────┴──────────┐
             │                     │
        Self-Attention             │
             ↓                     │
        Add + LayerNorm             │
             ↓                     │
             FFN                    │
             ↓                     │
        Add + LayerNorm             │
             │                     │
             └──── Repeat N times ─┘
                        │
                        ▼
             Contextual Representations
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
      [CLS] output     Token       Sentence
      Classification   NER         Embedding
```

---

# 7. BERT Input Representation

BERT-এর একটি খুব গুরুত্বপূর্ণ বিষয় হলো input representation।

BERT input representation সাধারণভাবে:

$$
E = E_{token} + E_{segment} + E_{position}
$$

অর্থাৎ:

```text
Input Embedding
=
Token Embedding
+
Segment Embedding
+
Position Embedding
```

---

# 8. Token Embedding

প্রথমে text tokenize হয়।

Example:

```text
I love AI
```

ধারণাগতভাবে:

```text
I
love
AI
```

প্রতিটি token-এর একটি ID থাকে:

```text
I     → 101
love  → 2023
AI    → 993
```

তারপর embedding lookup:

```text
101 → vector
2023 → vector
993 → vector
```

---

# 9. Position Embedding

Self-attention নিজে sequence order বুঝতে পারে না।

তাই BERT position information ব্যবহার করে।

ধরি:

```text
I love AI
```

positions:

```text
I     → 0
love  → 1
AI    → 2
```

প্রতিটি position-এর জন্য learned vector থাকে।

```text
Position 0 → vector
Position 1 → vector
Position 2 → vector
```

---

# 10. Segment Embedding

BERT-এর original design-এ দুইটি sentence একসাথে input দেওয়া যেতে পারে।

Example:

```text
Sentence A:
I love AI.

Sentence B:
AI is powerful.
```

BERT segment IDs দিতে পারে:

```text
I       → Segment A
love    → Segment A
AI      → Segment A

AI      → Segment B
is      → Segment B
powerful→ Segment B
```

Conceptually:

```text
Segment A → 0
Segment B → 1
```

এটাকে **token type embedding**-ও বলা হয়।

---

# 11. Special Tokens

BERT input-এ কিছু special token গুরুত্বপূর্ণ।

সবচেয়ে গুরুত্বপূর্ণ:

```text
[CLS]
[SEP]
[PAD]
[MASK]
[UNK]
```

---

# 12. `[CLS]`

`[CLS]` = classification token।

Single-sentence input:

```text
[CLS] I love AI [SEP]
```

`[CLS]` সাধারণত পুরো sequence-এর aggregated representation হিসেবে downstream classification task-এ ব্যবহার করা হয়।

Conceptually:

```text
[CLS]
 ↓
Whole sentence representation
 ↓
Classifier
```

---

# 13. `[SEP]`

`[SEP]` = separator token।

Single sentence:

```text
[CLS] I love AI [SEP]
```

Two sentences:

```text
[CLS] I love AI [SEP] AI is useful [SEP]
```

এটি sentence boundary indicate করে।

---

# 14. `[PAD]`

Batch processing-এর জন্য sequence একই length করার দরকার হলে:

```text
[PAD]
```

ব্যবহার করা হয়।

Example:

```text
[CLS] I love AI [SEP] [PAD] [PAD]
```

Padding positions attention mask দিয়ে ignore করা হয়।

এখানে M02.27-এর masking directly connected।

---

# 15. `[MASK]`

Masked Language Modeling-এর জন্য:

```text
I love [MASK].
```

Model-এর task:

```text
[MASK] → AI
```

এখানে `[MASK]` **training objective-এর অংশ**।

এটা M02.27-এর attention mask-এর থেকে আলাদা concept।

---

# 16. `[UNK]`

`[UNK]` = unknown token।

Tokenizer কোনো token/character sequence vocabulary-এর বাইরে গেলে কিছু tokenization setups-এ `[UNK]` ব্যবহার হতে পারে।

---

# 17. Complete BERT Input

Two-sentence example:

```text
Sentence A:
I love AI.

Sentence B:
AI is useful.
```

BERT-style input:

```text
[CLS]
I
love
AI
.
[SEP]
AI
is
useful
.
[SEP]
```

Segment:

```text
0 0 0 0 0 0
1 1 1 1 1
```

Position:

```text
0 1 2 3 4 5 6 7 8 9
```

---

# 18. Input Embedding Formula

প্রতিটি position-এর জন্য:

$$
E_i =
TokenEmbedding_i
+
SegmentEmbedding_i
+
PositionEmbedding_i
$$

Example:

```text
Token vector
     +
Segment vector
     +
Position vector
     ↓
Final input vector
```

---

# 19. BERT-এর Transformer Encoder

Input embeddings Transformer Encoder-এর মধ্যে যায়।

একটি encoder layer:

```text
Input
 ↓
Multi-Head Self-Attention
 ↓
Residual Connection
 ↓
LayerNorm
 ↓
Feed Forward Network
 ↓
Residual Connection
 ↓
LayerNorm
 ↓
Output
```

এটা আমরা M02.25-তে বিস্তারিত দেখেছি।

---

# 20. BERT Self-Attention

BERT-এর self-attention:

```text
Q = XWQ
K = XWK
V = XWV
```

তারপর:

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

BERT standard encoder attention-এ future-token causal restriction নেই।

---

# 21. BERT Bidirectional কেন?

ধরি:

```text
The animal didn't cross the road because it was tired.
```

`it` কোন entity-কে refer করছে বুঝতে left এবং right context দরকার হতে পারে।

BERT token representation তৈরির সময় sequence-এর উভয় দিকের context ব্যবহার করে।

```text
Left Context
     ↓
   TOKEN
     ↑
Right Context
```

---

# 22. BERT-এর "Bidirectional" মানে কী?

এটা **দুইটি আলাদা LSTM একসাথে চালানো** নয়।

বরং Transformer self-attention-এর মাধ্যমে একটি token sequence-এর অন্য valid tokens-এর দিকে attention করতে পারে।

তাই:

```text
BERT
→ Bidirectional contextual attention
```

---

# 23. GPT বনাম BERT

এটা খুব গুরুত্বপূর্ণ।

### BERT

```text
The [MASK] is blue.
```

Model context:

```text
left + right
```

### GPT

```text
The car is
```

পরবর্তী token predict করবে:

```text
blue
```

GPT future দেখতে পারে না।

---

# 24. BERT vs GPT

| Feature         | BERT                   | GPT                   |
| --------------- | ---------------------- | --------------------- |
| Architecture    | Encoder-only           | Decoder-only          |
| Attention       | Bidirectional          | Causal                |
| Future tokens   | Visible                | Blocked               |
| Main objective  | MLM-style              | Next-token prediction |
| Best suited     | Understanding          | Generation            |
| NER             | Excellent use case     | Possible              |
| Classification  | Excellent              | Possible              |
| Text generation | Not its primary design | Strong                |

---

# 25. BERT Pretraining

BERT-এর original pretraining setup-এ দুটি গুরুত্বপূর্ণ objective ছিল:

```text
1. Masked Language Modeling (MLM)
2. Next Sentence Prediction (NSP)
```

তবে modern BERT-family training recipes-এ সবসময় original NSP ব্যবহার করা হয় না।

---

# 26. Masked Language Modeling

এটাই BERT-এর সবচেয়ে গুরুত্বপূর্ণ concept।

Sentence:

```text
The cat is sleeping.
```

কিছু token mask/corrupt করা হয়:

```text
The cat is [MASK].
```

Model predict করবে:

```text
sleeping
```

---

# 27. MLM কেন দরকার?

Model যেন context থেকে missing word predict করতে শেখে।

```text
The cat is [MASK]
```

Model:

```text
sleeping
```

এভাবে language structure শেখে।

---

# 28. Original BERT MLM-এর Important Detail

Original BERT training-এ selected tokens-এর মধ্যে:

* বেশিরভাগ `[MASK]` দিয়ে replace করা হতো
* কিছু random token দিয়ে replace করা হতো
* কিছু unchanged রাখা হতো

অর্থাৎ training corruption পুরোপুরি শুধু `[MASK]` token বসানো ছিল না।

এই design-এর উদ্দেশ্য ছিল pretraining-এর সাথে downstream input mismatch কিছুটা কমানো।

---

# 29. MLM Loss

Suppose selected masked positions:

```text
t1
t2
t3
```

প্রতিটি position-এর জন্য vocabulary probability:

```text
P(token | context)
```

Cross-entropy loss ব্যবহার করে model train করা হয়।

Conceptually:

$$
Loss
=
-\sum \log P(x_i|context)
$$

শুধু selected prediction positions-এর উপর objective apply করা হয়।

---

# 30. BERT Vocabulary

BERT original implementation সাধারণত **WordPiece** subword tokenization ব্যবহার করে।

এটা খুব গুরুত্বপূর্ণ।

Example:

```text
playing
```

Conceptually tokenizer এটাকে subword pieces-এ ভাঙতে পারে।

Actual tokenization vocabulary-এর ওপর নির্ভর করে।

---

# 31. WordPiece কেন?

ধরি vocabulary-তে:

```text
play
playing
played
player
```

সব শব্দ রাখলে vocabulary বড় হয়ে যাবে।

Subword tokenization:

```text
play
##ing
```

এর মতো pieces ব্যবহার করতে পারে।

এতে:

```text
Unknown word
 ↓
Smaller subword pieces
```

handle করা সহজ হয়।

---

# 32. BERT Tokenization Pipeline

```text
Raw Text
 ↓
Basic normalization/tokenization
 ↓
WordPiece Tokenization
 ↓
Special Tokens
 ↓
Token IDs
 ↓
Segment IDs
 ↓
Attention Mask
 ↓
BERT
```

---

# 33. Attention Mask in BERT

ধরি:

```text
[CLS] I love AI [SEP] [PAD] [PAD]
```

Attention mask:

```text
1 1 1 1 1 1 0 0
```

Conceptually:

```text
1 → valid
0 → padding
```

এখানে মনে রাখবে:

> Model/framework অনুযায়ী internal boolean representation আলাদা হতে পারে।

---

# 34. BERT Output

BERT পুরো sequence-এর জন্য contextual representation দেয়।

যদি:

```text
sequence length = 10
hidden size = 768
```

তাহলে output:

```text
(10, 768)
```

Batch থাকলে:

```text
(batch_size, sequence_length, hidden_size)
```

যেমন:

```text
(32, 128, 768)
```

---

# 35. `[CLS]` Output

যদি:

```text
output.shape
=
(32, 128, 768)
```

তাহলে:

```python
cls_output = output[:, 0, :]
```

Shape:

```text
(32, 768)
```

এটা classification head-এ দেওয়া যেতে পারে।

---

# 36. Sequence Classification

Example:

```text
"This movie is excellent."
```

Task:

```text
Positive / Negative
```

Architecture:

```text
Text
 ↓
BERT
 ↓
[CLS] representation
 ↓
Linear Layer
 ↓
Softmax
 ↓
Class
```

---

# 37. Classification Formula

ধরি BERT `[CLS]` vector:

$$
h_{CLS}\in R^{768}
$$

Classifier:

$$
z = Wh_{CLS}+b
$$

তারপর:

$$
P = softmax(z)
$$

---

# 38. NER with BERT

NER-এর ক্ষেত্রে শুধু `[CLS]` ব্যবহার না করে প্রতিটি token representation ব্যবহার করা যায়।

Example:

```text
John lives in London.
```

BERT:

```text
John    → vector
lives   → vector
in      → vector
London  → vector
```

তারপর:

```text
Linear Classifier
 ↓
PER / O / O / LOC
```

---

# 39. BERT for NER

Architecture:

```text
Input
 ↓
BERT
 ↓
Token Representations
 ↓
Linear Layer
 ↓
NER Labels
```

Example:

```text
John     → B-PER
lives    → O
in       → O
London   → B-LOC
```

---

# 40. BERT for Question Answering

Question:

```text
Who is the president?
```

Context:

```text
The president is John.
```

BERT input:

```text
[CLS] Question [SEP] Context [SEP]
```

Model context-এর answer span identify করতে পারে।

Typical extractive QA formulation-এ:

```text
Start position
+
End position
```

predict করা হয়।

---

# 41. BERT for Sentence Similarity

দুটি sentence:

```text
A: I love programming.
B: I enjoy coding.
```

BERT representations ব্যবহার করে semantic relationship estimate করা যায়।

তবে modern sentence-embedding retrieval systems-এর জন্য vanilla BERT `[CLS]` representation সবসময় best choice নয়; Sentence-BERT-এর মতো models এই task-এর জন্য specifically designed।

---

# 42. BERT for Semantic Search

Query:

```text
How to learn Python?
```

Documents:

```text
Python programming tutorial
JavaScript tutorial
Database tutorial
```

BERT-family encoder representations semantic matching-এ ব্যবহার করা যায়।

Modern retrieval architecture-এ often:

```text
Encoder
 ↓
Embedding
 ↓
Vector Search
```

---

# 43. Fine-Tuning

BERT-এর সবচেয়ে শক্তিশালী concept:

> **Pretrain once → Fine-tune for many tasks**

প্রথমে:

```text
Large Text Corpus
 ↓
Pretraining
 ↓
BERT
```

তারপর:

```text
BERT
 ↓
Task-specific head
 ↓
Fine-tuning
```

---

# 44. Fine-Tuning Example

Pretrained BERT:

```text
BERT
```

Sentiment:

```text
BERT + Classification Head
```

NER:

```text
BERT + Token Classification Head
```

QA:

```text
BERT + QA Head
```

---

# 45. Transfer Learning

এটাই মূল concept:

```text
General Language Knowledge
          ↓
       BERT
          ↓
Task-specific learning
```

একে **Transfer Learning** বলা হয়।

---

# 46. Feature Extraction vs Fine-Tuning

দুইভাবে pretrained BERT ব্যবহার করা যায়।

### Feature Extraction

```text
BERT parameters
→ Frozen

Task head
→ Train
```

### Fine-Tuning

```text
BERT parameters
→ Update

Task head
→ Update
```

Fine-tuning সাধারণত task-specific adaptation-এর জন্য বেশি flexible।

---

# 47. BERT Base বনাম Large

Original BERT-এর বহুল পরিচিত configurations:

### BERT Base

```text
Layers = 12
Hidden Size = 768
Attention Heads = 12
Parameters ≈ 110M
```

### BERT Large

```text
Layers = 24
Hidden Size = 1024
Attention Heads = 16
Parameters ≈ 340M
```

এগুলো original BERT configurations-এর standard reference।

---

# 48. BERT Base Shape

ধরি:

```text
Batch = 16
Sequence = 128
Hidden = 768
```

Input:

```text
(16, 128, 768)
```

প্রতিটি encoder layer:

```text
(16, 128, 768)
```

Output:

```text
(16, 128, 768)
```

---

# 49. BERT Attention Shape

BERT Base:

```text
hidden_size = 768
heads = 12
```

তাই:

$$
d_{head} = \frac{768}{12}=64
$$

Attention representation:

```text
(B, 12, L, 64)
```

Attention scores:

```text
(B, 12, L, L)
```

---

# 50. BERT Encoder Layer

একটি BERT encoder layer:

```text
Input
 │
 ▼
Multi-Head Self-Attention
 │
 ▼
Add & LayerNorm
 │
 ▼
Feed Forward Network
 │
 ▼
Add & LayerNorm
 │
 ▼
Output
```

তারপর:

```text
Output
 ↓
Next Encoder Layer
```

BERT Base-এ:

```text
12 layers
```

---

# 51. Feed Forward Network

BERT Base:

```text
Hidden = 768
Intermediate = 3072
```

Conceptually:

```text
768
 ↓
3072
 ↓
768
```

Formula:

$$
FFN(x)=GELU(xW_1+b_1)W_2+b_2
$$

BERT original architecture uses GELU-style activation.

---

# 52. Why Hidden Representation Changes Layer by Layer?

একটি token:

```text
"bank"
```

প্রথম layer:

```text
basic contextual information
```

পরের layer:

```text
syntactic information
```

আরও গভীরে:

```text
semantic/task-relevant information
```

তবে layer-by-layer interpretation এত সরল নয়; বাস্তবে representations distributed এবং multiple types of information একসাথে encode করে।

---

# 53. BERT Contextual Embedding

Word2Vec:

```text
bank
 ↓
একটি fixed vector
```

BERT:

```text
bank in river context
 ↓
context-specific vector

bank in finance context
 ↓
different contextual vector
```

এটাই বিশাল পার্থক্য।

---

# 54. Static vs Contextual

### Word2Vec

```text
bank
→ Vector A
```

সব context-এ একই vector।

### BERT

```text
bank + river
→ Vector A

bank + money
→ Vector B
```

অর্থাৎ:

```text
Meaning depends on context
```

---

# 55. BERT vs Word2Vec

| Feature        | Word2Vec                     | BERT                     |
| -------------- | ---------------------------- | ------------------------ |
| Representation | Static                       | Contextual               |
| Architecture   | Shallow embedding model      | Transformer Encoder      |
| Context        | Limited/fixed representation | Full sequence context    |
| Subword        | No                           | WordPiece                |
| Pretraining    | Word prediction              | MLM-style + original NSP |
| Fine-tuning    | Not typical                  | Yes                      |

---

# 56. BERT vs LSTM

### LSTM

```text
Token 1
 ↓
Token 2
 ↓
Token 3
 ↓
Token 4
```

Sequential computation।

### BERT

```text
Token 1 ─┐
Token 2 ─┼→ Self-Attention
Token 3 ─┤
Token 4 ─┘
```

Training-এর সময় অনেক computation parallelize করা যায়।

---

# 57. BERT-এর Limitation

BERT powerful হলেও:

### 1. Generation-এর জন্য natural fit নয়

BERT:

```text
Understanding
```

GPT-style:

```text
Generation
```

### 2. Attention complexity

Standard self-attention:

$$
O(L^2)
$$

Sequence length বাড়লে cost দ্রুত বাড়ে।

### 3. Pretraining expensive

Large corpus + GPU resources দরকার।

### 4. Domain mismatch

General BERT medical/legal/financial domain-এর terminology সবসময় optimalভাবে represent নাও করতে পারে।

---

# 58. Domain-Specific BERT

Different domains-এর জন্য BERT-family models train/fine-tune করা যায়।

Examples:

```text
Medical
Legal
Scientific
Finance
```

Concept:

```text
General BERT
 ↓
Domain Corpus
 ↓
Domain Adaptation
 ↓
Domain-specific Model
```

---

# 59. BERT in AI Writing Platform

তোমার future AI writing platform-এর ক্ষেত্রে BERT-type encoder useful হতে পারে:

```text
User Text
   ↓
Tokenizer
   ↓
BERT Encoder
   ↓
Contextual Representation
   │
   ├── Grammar Analysis
   ├── Style Classification
   ├── Sentence Classification
   ├── Semantic Similarity
   ├── NER
   └── Text Quality Analysis
```

কিন্তু **high-quality text generation/rewrite-এর জন্য BERT alone যথেষ্ট নয়**, কারণ এটি মূলত encoder-based understanding model।

Generation-এর জন্য decoder/seq2seq/LLM architecture বেশি উপযুক্ত।

---

# 60. AI Writing Assistant Example

Input:

```text
This is very good and amazing product.
```

BERT-style encoder:

```text
Token representations
        ↓
Semantic analysis
        ↓
Style/quality classifier
```

Possible output:

```text
Repetition detected
```

তারপর একটি generative model rewrite করতে পারে:

```text
This is an excellent product.
```

অর্থাৎ architecture হতে পারে:

```text
BERT-like Encoder
       +
Generative LLM
```

---

# 61. BERT Pipeline — Full

```text
                    RAW TEXT
                        │
                        ▼
                    TOKENIZER
                        │
                        ▼
                  WORDPIECE TOKENS
                        │
                        ▼
                   TOKEN IDs
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
      Token Emb.    Segment Emb.   Position Emb.
          │             │             │
          └─────────────┼─────────────┘
                        ▼
                    ADDITION
                        │
                        ▼
                TRANSFORMER ENCODER
                        │
              ┌─────────┴─────────┐
              ▼                   ▼
        Self-Attention           FFN
              │                   │
              └─────────┬─────────┘
                        ▼
                 Encoder Layer
                        │
                     Repeat
                        │
                        ▼
              Contextual Embeddings
                        │
        ┌───────────────┼──────────────┐
        ▼               ▼              ▼
      [CLS]          Token Output    Pooling
        │               │              │
        ▼               ▼              ▼
 Classification        NER       Similarity/etc.
```

---

# 62. Hugging Face দিয়ে BERT ব্যবহার

Industry-তে সাধারণত Hugging Face Transformers-এর মতো library ব্যবহার করা হয়।

Install:

```bash
pip install transformers torch
```

---

# 63. BERT Tokenizer

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)

text = "I love AI."

tokens = tokenizer.tokenize(text)

print(tokens)
```

Output vocabulary/version অনুযায়ী হতে পারে:

```text
['i', 'love', 'ai', '.']
```

---

# 64. Token IDs

```python
encoded = tokenizer(
    "I love AI.",
    return_tensors="pt"
)

print(encoded)
```

তুমি সাধারণত পাবে:

```text
input_ids
token_type_ids
attention_mask
```

---

# 65. তিনটি গুরুত্বপূর্ণ Tensor

BERT input:

```text
input_ids
token_type_ids
attention_mask
```

### `input_ids`

```text
Token → ID
```

### `token_type_ids`

```text
Sentence A / B
```

### `attention_mask`

```text
Real token / Padding
```

---

# 66. BERT Model

```python
from transformers import AutoModel

model = AutoModel.from_pretrained(
    "bert-base-uncased"
)

outputs = model(**encoded)

print(outputs.last_hidden_state.shape)
```

যদি:

```text
batch = 1
length = 6
hidden = 768
```

তাহলে:

```text
torch.Size([1, 6, 768])
```

---

# 67. `[CLS]` Vector

```python
cls_vector = outputs.last_hidden_state[:, 0, :]

print(cls_vector.shape)
```

Output:

```text
torch.Size([1, 768])
```

---

# 68. Token Representation

ধরি:

```python
token_vectors = outputs.last_hidden_state
```

Shape:

```text
(B, L, 768)
```

প্রতিটি token-এর contextual representation আছে।

---

# 69. BERT Classification Architecture

```python
import torch.nn as nn
from transformers import AutoModel


class BertClassifier(nn.Module):

    def __init__(self, num_classes):
        super().__init__()

        self.bert = AutoModel.from_pretrained(
            "bert-base-uncased"
        )

        self.classifier = nn.Linear(
            768,
            num_classes
        )

    def forward(
        self,
        input_ids,
        attention_mask,
        token_type_ids=None
    ):

        outputs = self.bert(
            input_ids=input_ids,
            attention_mask=attention_mask,
            token_type_ids=token_type_ids
        )

        cls = outputs.last_hidden_state[:, 0, :]

        logits = self.classifier(cls)

        return logits
```

---

# 70. Model Flow

```text
Text
 ↓
Tokenizer
 ↓
input_ids
token_type_ids
attention_mask
 ↓
BERT
 ↓
last_hidden_state
 ↓
[CLS]
 ↓
Linear
 ↓
Logits
 ↓
Softmax
 ↓
Class
```

---

# 71. M02.28-এর সবচেয়ে গুরুত্বপূর্ণ 10টি Concept

এগুলো অবশ্যই mastery করতে হবে:

```text
1. BERT = Bidirectional Encoder Representations from Transformers

2. BERT = Encoder-only Transformer

3. BERT uses bidirectional self-attention

4. Token + Segment + Position Embeddings

5. [CLS] = sequence-level classification representation

6. [SEP] = sentence separator

7. [PAD] = padding

8. [MASK] = MLM training token

9. MLM = BERT's core original pretraining objective

10. BERT is primarily an understanding/representation model
```

---

# 72. BERT বনাম আমাদের আগের Lessons

```text
M02.15
Word Embedding
       ↓
M02.20
Attention
       ↓
M02.21
Self-Attention
       ↓
M02.22
Multi-Head Attention
       ↓
M02.23
Position
       ↓
M02.24
Transformer
       ↓
M02.25
Encoder
       ↓
M02.27
Masking
       ↓
M02.28
BERT
```

অর্থাৎ তুমি এখন পর্যন্ত যেসব concept শিখেছো, **BERT সেগুলোর একটি practical combination**।

---

# 73. Interview Questions

### Q1. What is BERT?

BERT is a Transformer Encoder-based language representation model that learns bidirectional contextual representations.

### Q2. What does BERT stand for?

**Bidirectional Encoder Representations from Transformers.**

### Q3. Is BERT encoder or decoder?

```text
Encoder
```

### Q4. Does BERT use causal masking?

Standard BERT encoder self-attention-এ **causal masking ব্যবহার করা হয় না**।

### Q5. What is MLM?

Masked Language Modeling—input-এর কিছু token hide/corrupt করে তাদের original token predict করতে model train করা।

### Q6. What is `[CLS]`?

Sequence-level representation হিসেবে classification-type tasks-এ ব্যবহৃত special token।

### Q7. What is `[SEP]`?

Sentence/segment boundary indicate করার special token।

### Q8. Why does BERT need position information?

Self-attention নিজে sequence order encode করে না, তাই position information প্রয়োজন।

### Q9. BERT কি text generate করতে পারে?

Vanilla BERT autoregressive GPT-style text generation-এর জন্য designed নয়।

### Q10. BERT এবং GPT-এর প্রধান পার্থক্য কী?

```text
BERT → Encoder-only + Bidirectional
GPT  → Decoder-only + Causal
```

---

# 74. Practice Tasks

### Beginner

এই text-এর BERT-style input তৈরি করো:

```text
I love Python.
```

তোমার structure:

```text
[CLS]
I
love
Python
.
[SEP]
```

---

### Intermediate

এই দুই sentence-এর input structure তৈরি করো:

```text
I love Python.

Python is powerful.
```

Include:

```text
[CLS]
[SEP]
Segment IDs
Position IDs
Attention Mask
```

---

### Advanced

Hugging Face দিয়ে:

```text
bert-base-uncased
```

load করে:

1. Tokenize
2. Input IDs বের করো
3. Attention mask বের করো
4. BERT output বের করো
5. `[CLS]` vector বের করো
6. প্রতিটি token-এর vector shape দেখো

---

# 75. Final Completion Checklist

```text
☑ BERT definition
☑ BERT full form
☑ Encoder-only architecture
☑ Bidirectional self-attention
☑ BERT input representation
☑ Token embedding
☑ Position embedding
☑ Segment embedding
☑ [CLS]
☑ [SEP]
☑ [PAD]
☑ [MASK]
☑ [UNK]
☑ WordPiece
☑ Attention mask
☑ Transformer Encoder
☑ Multi-head self-attention
☑ Feed Forward Network
☑ LayerNorm
☑ Residual connection
☑ MLM
☑ Original NSP concept
☑ MLM loss
☑ Contextual embedding
☑ Static vs contextual embedding
☑ BERT vs Word2Vec
☑ BERT vs LSTM
☑ BERT vs GPT
☑ BERT Base
☑ BERT Large
☑ Fine-tuning
☑ Transfer learning
☑ Classification
☑ NER
☑ Question Answering
☑ Semantic similarity
☑ Hugging Face implementation
☑ AI writing system application
```

---

# 🧠 Final Mental Model

সবচেয়ে গুরুত্বপূর্ণ diagram:

```text
                       BERT
                        │
                 Encoder-only
                        │
                        ▼
                    Tokenizer
                        │
                        ▼
                 WordPiece Tokens
                        │
                        ▼
                    Token IDs
                        │
        ┌───────────────┼────────────────┐
        ▼               ▼                ▼
   Token Embedding  Segment Embedding  Position
                                         Embedding
        │               │                │
        └───────────────┼────────────────┘
                        ▼
                    Input Vector
                        │
                        ▼
             ┌─────────────────────┐
             │ Transformer Encoder │
             │                     │
             │ Multi-Head          │
             │ Self-Attention      │
             │        ↓            │
             │ Add + Norm          │
             │        ↓            │
             │ FFN                 │
             │        ↓            │
             │ Add + Norm          │
             └──────────┬──────────┘
                        │
                  Repeat N times
                        │
                        ▼
             Contextual Representations
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
       [CLS]          Tokens       Sentence
          │             │          Embedding
          ▼             ▼
   Classification       NER
```

### সবচেয়ে গুরুত্বপূর্ণ distinction:

```text
Word2Vec
→ Word meaning

BERT
→ Contextual word meaning

GPT
→ Next-token generation
```

আর তোমার AI writing platform-এর perspective থেকে:

```text
                 USER TEXT
                     │
                     ▼
                  BERT
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       Meaning     Grammar    Style
       Analysis    Features   Analysis
          │          │          │
          └──────────┼──────────┘
                     ▼
              Writing Analysis
                     │
                     ▼
              Generative Model
                     │
                     ▼
               Improved Text
```

**M02.28 সম্পূর্ণ।**
পরবর্তী lesson হবে **M02.29 — GPT Architecture Deep Dive**, যেখানে BERT-এর বিপরীতে **Decoder-only Transformer, causal language modeling, next-token prediction, GPT input/output flow, causal attention, generation এবং GPT-style architecture** বিস্তারিত শিখব।

---------
# M02.29 — GPT Architecture Deep Dive

আজ আমরা **GPT Architecture** একদম foundation থেকে deep level পর্যন্ত শিখব।

আগের lessons-এর সাথে connection:

```text
M02.20 → Attention
M02.21 → Self-Attention
M02.22 → Multi-Head Attention
M02.23 → Positional Information
M02.24 → Transformer
M02.25 → Encoder
M02.26 → Decoder
M02.27 → Masking
M02.28 → BERT
             ↓
M02.29 → GPT Architecture
```

BERT এবং GPT-এর পার্থক্য বুঝতে এই lesson খুব গুরুত্বপূর্ণ।

---

# 1. GPT কী?

**GPT = Generative Pre-trained Transformer**

GPT হলো একটি **decoder-only Transformer architecture** যা autoregressive language modeling ব্যবহার করে।

সহজভাবে:

```text
GPT
 ↓
Transformer Decoder-style architecture
 ↓
Causal Self-Attention
 ↓
Next Token Prediction
 ↓
Text Generation
```

---

# 2. GPT-এর তিনটি শব্দ

GPT নামের তিনটি অংশের meaning:

### G — Generative

Text generate করতে পারে।

```text
Input:
I love

Output:
AI
```

### P — Pre-trained

আগে বিশাল text corpus-এর উপর train করা হয়।

```text
Large Text
 ↓
Pretraining
 ↓
Language Model
```

### T — Transformer

Transformer architecture ব্যবহার করে।

---

# 3. GPT = Decoder-Only

এটা খুব গুরুত্বপূর্ণ।

Original Transformer:

```text
Encoder + Decoder
```

BERT:

```text
Encoder-only
```

GPT:

```text
Decoder-only
```

অর্থাৎ:

```text
BERT → Encoder
GPT  → Decoder-style Transformer
```

---

# 4. GPT-এর Core Objective

GPT-এর মূল training objective:

> **Given previous tokens, predict the next token.**

Example:

```text
The cat is
```

Model predict করবে:

```text
sleeping
```

তারপর:

```text
The cat is sleeping
```

পরবর্তী token:

```text
.
```

---

# 5. Autoregressive Language Modeling

GPT autoregressive।

Formula:

$$
P(x_t|x_1,x_2,\dots,x_{t-1})
$$

অর্থাৎ current token predict করার সময় previous tokens ব্যবহার করা হয়।

পুরো sequence:

$$
P(x_1,x_2,\dots,x_T)
=
\prod_{t=1}^{T}
P(x_t|x_{<t})
$$

এটাই GPT-এর foundation।

---

# 6. GPT কেন Future Token দেখতে পারে না?

কারণ future token দেখা গেলে training leakage হবে।

ধরি:

```text
I love machine learning
```

`machine` predict করার সময় model যদি `learning` দেখতে পারে:

```text
machine → learning
```

তাহলে prediction সহজ হয়ে যাবে এবং genuine next-token modeling হবে না।

তাই:

```text
Future → Block
```

এজন্য **causal mask** ব্যবহার করা হয়।

---

# 7. GPT Causal Attention

ধরি:

```text
I love AI
```

Attention pattern:

```text id="gptcausal"
        I   love   AI

I       ✓    ✗     ✗
love    ✓    ✓     ✗
AI      ✓    ✓     ✓
```

অর্থাৎ:

```text
Token 1 → নিজেরটা
Token 2 → Token 1 + নিজেরটা
Token 3 → Token 1 + Token 2 + নিজেরটা
```

Future:

```text
❌
```

---

# 8. GPT Architecture — High Level

```text id="gptarch1"
                    INPUT TEXT
                        │
                        ▼
                    TOKENIZER
                        │
                        ▼
                    TOKEN IDs
                        │
                        ▼
                  TOKEN EMBEDDING
                        │
                        +
                POSITION INFORMATION
                        │
                        ▼
              TRANSFORMER BLOCK
                        │
              ┌─────────┴─────────┐
              │                   │
              ▼                   ▼
       Causal Self-Attention      │
              │                   │
              ▼                   │
         Add + Norm               │
              │                   │
              ▼                   │
             FFN                  │
              │                   │
              ▼                   │
         Add + Norm               │
              │                   │
              └─────────┬─────────┘
                        │
                  Repeat N times
                        │
                        ▼
                  Final LayerNorm
                        │
                        ▼
               Linear LM Head
                        │
                        ▼
                 Vocabulary Logits
                        │
                        ▼
                    Softmax
                        │
                        ▼
                Next Token
```

---

# 9. GPT Input

ধরি user লিখল:

```text
I want to learn
```

Tokenizer এটাকে token pieces-এ ভাগ করবে।

Conceptually:

```text
I
want
to
learn
```

তারপর:

```text
Token
 ↓
Token ID
```

---

# 10. Token Embedding

প্রতিটি token ID একটি vector-এ convert হয়।

ধরি:

```text
vocab_size = 50,000
embedding_dim = 768
```

Embedding matrix:

$$
E \in R^{50000\times768}
$$

যদি token ID হয়:

```text
1205
```

তাহলে:

```text
1205
 ↓
Embedding Lookup
 ↓
768-dimensional vector
```

---

# 11. Position Information

GPT-কে token order বুঝতে position information দরকার।

Conceptually:

```text
Token Embedding
      +
Position Information
      ↓
Transformer Input
```

Classic Transformer/GPT-family implementations বিভিন্ন positional mechanism ব্যবহার করতে পারে। আধুনিক GPT-style models-এ learned absolute position-এর পাশাপাশি RoPE-এর মতো relative/rotary mechanisms-ও বহুল ব্যবহৃত।

---

# 12. GPT Transformer Block

একটি GPT block:

```text
Input
 ↓
LayerNorm
 ↓
Causal Multi-Head Self-Attention
 ↓
Residual Connection
 ↓
LayerNorm
 ↓
Feed Forward Network
 ↓
Residual Connection
 ↓
Output
```

Modern GPT-style models সাধারণত **Pre-Norm** architecture ব্যবহার করে।

---

# 13. Pre-Norm কেন?

GPT-style modern architecture-এ:

```text
x
 ↓
LayerNorm
 ↓
Attention
 ↓
+
x
```

তারপর:

```text
x
 ↓
LayerNorm
 ↓
FFN
 ↓
+
previous
```

এতে deep Transformer training আরও stable হতে পারে।

---

# 14. GPT Attention

GPT-এর self-attention:

$$
Q=XW_Q
$$

$$
K=XW_K
$$

$$
V=XW_V
$$

তারপর:

$$
Scores=
\frac{QK^T}{\sqrt{d_k}}
$$

তারপর causal mask:

$$
Scores'=Scores+Mask
$$

তারপর:

$$
A=softmax(Scores')
$$

তারপর:

$$
Output=AV
$$

---

# 15. GPT-এর Attention Flow

```text id="gptflow2"
Input
 ↓
Q K V
 ↓
QKᵀ
 ↓
Scale
 ↓
Causal Mask
 ↓
Softmax
 ↓
Attention Weights
 ↓
× V
 ↓
Attention Output
 ↓
Residual
```

---

# 16. Multi-Head Attention

GPT একাধিক attention head ব্যবহার করে।

ধরি:

```text
d_model = 768
heads = 12
```

তাহলে:

$$
d_{head} = 768/12 = 64
$$

প্রতিটি head:

```text
Q
K
V
 ↓
Attention
```

তারপর:

```text
Head 1
Head 2
...
Head 12
 ↓
Concatenate
 ↓
Output Projection
```

---

# 17. GPT Feed Forward Network

Attention-এর পরে FFN আসে।

Conceptually:

```text
Hidden
 ↓
Expand
 ↓
Activation
 ↓
Project back
```

উদাহরণ:

```text
768
 ↓
3072
 ↓
GELU
 ↓
768
```

Modern GPT variants often use gated MLP variants such as SwiGLU rather than the original simple GELU FFN; architecture depends on the model generation.

---

# 18. GPT Residual Connection

ধরি attention output:

```text
Attention(x)
```

Residual:

$$
x' = x + Attention(x)
$$

তারপর FFN:

$$
y=x'+FFN(x')
$$

এতে information এবং gradient flow সহজ হয়।

---

# 19. GPT Block Mathematical View

একটি simplified Pre-Norm block:

$$
x' = x + Attention(LN(x))
$$

তারপর:

$$
x'' = x' + FFN(LN(x'))
$$

এটাই modern GPT-style block-এর core pattern।

---

# 20. GPT-এর Layer Stack

একটি block-এর পর আরেকটি block:

```text
Input
 ↓
Block 1
 ↓
Block 2
 ↓
Block 3
 ↓
...
 ↓
Block N
 ↓
Final LayerNorm
```

যত বেশি layer:

```text
Deep representation
```

তবে শুধু layer বাড়ালেই performance বাড়ে না; width, data, optimization, compute এবং architecture-ও গুরুত্বপূর্ণ।

---

# 21. Final LayerNorm

সব Transformer blocks-এর পর:

```text
Final LayerNorm
```

ব্যবহার করা হয়।

```text
Block N
 ↓
LayerNorm
 ↓
LM Head
```

---

# 22. LM Head কী?

LM = **Language Model**

Final hidden representation vocabulary-এর probability-তে convert করতে একটি linear projection ব্যবহার করা হয়।

ধরি:

```text
Hidden size = 768
Vocabulary = 50,000
```

LM head:

```text
768
 ↓
50,000 logits
```

Shape:

```text
(B, L, 50,000)
```

---

# 23. Logits কী?

Logits হলো softmax-এর আগের raw scores।

Example:

```text
AI      → 4.2
Python  → 2.1
Django  → 0.8
car     → -1.2
```

তারপর:

```text
Logits
 ↓
Softmax
 ↓
Probabilities
```

---

# 24. Softmax

Softmax:

$$
P_i =
\frac{e^{z_i}}
{\sum_j e^{z_j}}
$$

Output:

```text
AI      → 0.70
Python  → 0.15
Django  → 0.08
car     → 0.01
...
```

সব probability-এর sum:

$$
\sum_i P_i=1
$$

---

# 25. Next Token Prediction

Input:

```text
I love
```

Model output:

```text
AI → 0.50
Python → 0.20
coding → 0.10
...
```

ধরি selected token:

```text
AI
```

এখন sequence:

```text
I love AI
```

আবার model চালানো হয়।

Next token:

```text
is
```

তারপর:

```text
I love AI is
```

এভাবে চলতে থাকে।

---

# 26. Autoregressive Generation

```text id="autoregressive"
Prompt
  ↓
GPT
  ↓
Next Token
  ↓
Append
  ↓
GPT
  ↓
Next Token
  ↓
Append
  ↓
Repeat
```

Example:

```text
I
 ↓
I love
 ↓
I love AI
 ↓
I love AI because
 ↓
I love AI because it
 ↓
...
```

---

# 27. Training vs Generation

এখানে একটি গুরুত্বপূর্ণ difference আছে।

## Training

অনেক token একসাথে parallelভাবে process করা যায়।

```text
Input:
I love AI

Targets:
love AI <END>
```

Causal mask future leakage prevent করে।

## Generation

Inference-time-এ token-by-token generation হয়:

```text
Token 1
 ↓
Token 2
 ↓
Token 3
 ↓
Token 4
```

---

# 28. Teacher Forcing

Training-এ target sequence-এর known previous tokens model input হিসেবে ব্যবহার করা যায়।

Example:

```text
Input:
I love AI

Target:
love AI .
```

Training-এর সময় model-এর প্রতিটি position-এর correct previous context available থাকে।

এতে training efficient হয়।

---

# 29. GPT Loss

GPT সাধারণত **cross-entropy loss** ব্যবহার করে।

ধরি target token:

```text
AI
```

Model predicted:

```text
AI → 0.7
```

Loss:

$$
Loss=-\log(0.7)
$$

Probability যত ভালো target-এর দিকে যায়:

```text
Loss ↓
```

---

# 30. GPT Training Objective

সব token position-এর next-token prediction loss combine করা হয়:

$$
L
=
-\sum_{t=1}^{T}
\log P(x_t|x_{<t})
$$

Practical implementation-এ token-level losses সাধারণত mean/sum reduction এবং padding handling অনুযায়ী aggregate করা হয়।

---

# 31. Example Training

Text:

```text
I love AI
```

Training pairs conceptually:

```text
Input       Target

I           love
I love      AI
I love AI   <EOS>
```

কিন্তু efficient implementation-এ sequence-এর সব positions একসাথে process করা হয়।

---

# 32. Why GPT Can Generate Long Text?

কারণ প্রতিটি generated token পরবর্তী prediction-এর context হয়ে যায়।

```text
Prompt
 ↓
Token 1
 ↓
Token 1 + Token 2
 ↓
Token 1 + Token 2 + Token 3
 ↓
...
```

এটাই autoregressive generation।

---

# 33. GPT-এর Context Window

GPT model একটি নির্দিষ্ট maximum context length support করে।

ধরি:

```text
context_length = 4096
```

তাহলে model একই attention computation-এ সীমিত সংখ্যক tokens process করতে পারে।

Modern models অনেক larger context window support করতে পারে, কিন্তু architecture/model অনুযায়ী limit আলাদা।

---

# 34. Context Window কেন গুরুত্বপূর্ণ?

তোমার AI writing platform-এ:

```text
User Document
 ↓
Tokenize
 ↓
Context Window
```

যদি document খুব বড় হয়:

```text
Document > Context Window
```

তাহলে chunking, sliding windows, retrieval, summarization বা long-context architecture-এর মতো techniques দরকার হতে পারে।

---

# 35. GPT-এর Tokenization

GPT-family models historically বিভিন্ন subword tokenization approach ব্যবহার করেছে।

Classic GPT-2:

```text
Byte-level BPE
```

অন্যান্য modern model-এর tokenizer architecture/model generation অনুযায়ী ভিন্ন হতে পারে।

Core idea:

```text
Rare word
 ↓
Subword pieces
 ↓
Token IDs
```

---

# 36. BERT Tokenizer vs GPT Tokenizer

BERT:

```text
WordPiece
```

Classic GPT-2:

```text
Byte-level BPE
```

তাই:

```text
BERT tokenization
≠
GPT tokenization
```

---

# 37. GPT vs BERT — Fundamental Difference

এটা interview এবং practical NLP—দুই জায়গাতেই অত্যন্ত গুরুত্বপূর্ণ।

```text id="bertgpt"
                 BERT
                  │
          Encoder-only
                  │
       Bidirectional Attention
                  │
          Understanding
```

versus:

```text id="gptgpt"
                  GPT
                   │
            Decoder-only
                   │
           Causal Attention
                   │
             Generation
```

---

# 38. Attention Pattern Comparison

### BERT

```text
       T1 T2 T3 T4

T1     ✓  ✓  ✓  ✓
T2     ✓  ✓  ✓  ✓
T3     ✓  ✓  ✓  ✓
T4     ✓  ✓  ✓  ✓
```

### GPT

```text
       T1 T2 T3 T4

T1     ✓  ✗  ✗  ✗
T2     ✓  ✓  ✗  ✗
T3     ✓  ✓  ✓  ✗
T4     ✓  ✓  ✓  ✓
```

---

# 39. GPT vs Original Transformer Decoder

একটি subtle point:

Original Transformer decoder:

```text
Masked Self-Attention
+
Cross-Attention
+
FFN
```

GPT-style decoder-only model:

```text
Causal Self-Attention
+
FFN
```

**Cross-attention নেই**, কারণ আলাদা encoder নেই।

---

# 40. GPT Block vs Original Decoder Block

### Original Decoder

```text
Masked Self-Attention
 ↓
Cross-Attention
 ↓
FFN
```

### GPT

```text
Causal Self-Attention
 ↓
FFN
```

এই difference খুব গুরুত্বপূর্ণ।

---

# 41. GPT Input → Output

```text id="gptfull"
                PROMPT
                  │
                  ▼
               TOKENIZER
                  │
                  ▼
               TOKEN IDs
                  │
                  ▼
              EMBEDDINGS
                  │
                  +
             POSITION INFO
                  │
                  ▼
        ┌─────────────────────┐
        │   GPT BLOCK 1       │
        │ Causal Self-Attn    │
        │ FFN                 │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │   GPT BLOCK 2       │
        └──────────┬──────────┘
                   │
                  ...
                   │
                   ▼
        ┌─────────────────────┐
        │   GPT BLOCK N       │
        └──────────┬──────────┘
                   │
                   ▼
              Final LayerNorm
                   │
                   ▼
                 LM Head
                   │
                   ▼
                Logits
                   │
                   ▼
               Softmax
                   │
                   ▼
             Next Token
```

---

# 42. Generation Strategies

Next token probability থেকে token নির্বাচন করার অনেক strategy আছে।

### Greedy Decoding

সবচেয়ে বেশি probability:

```text
argmax(P)
```

নির্বাচন।

Example:

```text
AI → 0.70
Python → 0.20
ML → 0.10
```

Output:

```text
AI
```

---

# 43. Temperature

Temperature probability distribution-এর sharpness পরিবর্তন করে।

$$
P_i =
softmax(z_i/T)
$$

### Low temperature

```text
T ↓
 ↓
More deterministic
```

### High temperature

```text
T ↑
 ↓
More diverse/random
```

খুব high temperature হলে output incoherent হতে পারে।

---

# 44. Top-k Sampling

ধরি:

```text
k = 3
```

শুধু top 3 candidate রাখবে।

```text
AI       0.40
Python   0.25
ML       0.15
car      0.01
...
```

শুধু:

```text
AI
Python
ML
```

থেকে sample।

---

# 45. Top-p / Nucleus Sampling

এখানে fixed number `k` নয়।

Cumulative probability threshold:

```text
p = 0.90
```

পর্যন্ত candidates রাখা হয়।

এতে candidate count context অনুযায়ী পরিবর্তিত হয়।

---

# 46. Greedy vs Sampling

```text
Greedy
→ Highest probability

Temperature
→ Distribution control

Top-k
→ Fixed candidate pool

Top-p
→ Probability-mass candidate pool
```

Generation/decoding strategies আমরা পরে dedicated lesson-এ আরও গভীরভাবে করব।

---

# 47. KV Cache

Generation-এর সময় GPT-এর একটি গুরুত্বপূর্ণ optimization হলো **KV Cache**।

ধরি previous tokens:

```text
T1 T2 T3
```

তাদের K/V বারবার calculate না করে cache করা যায়।

```text
Past K,V
 ↓
Cache
 ↓
New Query
 ↓
Attention
 ↓
Next Token
```

এতে autoregressive inference অনেক efficient হতে পারে।

---

# 48. GPT-এর Computational Complexity

Standard self-attention-এর sequence-length complexity:

$$
O(L^2)
$$

কারণ attention matrix:

$$
L\times L
$$

যদি:

```text
L = 1000
```

তাহলে:

```text
1,000,000
```

attention pair।

তাই long-context generation computationally expensive।

---

# 49. Parameter Count

GPT model-এর parameters প্রধানত আসে:

```text
Embedding
+
Attention projections
+
FFN/MLP
+
LayerNorm
+
LM Head
```

Large GPT-style models-এ MLP/FFN অংশ parameter count-এর বড় অংশ হতে পারে।

---

# 50. Weight Tying

কিছু language model input token embedding এবং output LM head-এর weight share করতে পারে।

Conceptually:

```text
Input Embedding
      ↑
      │
 Shared Weights
      │
      ↓
Output LM Head
```

এতে parameter count কমতে পারে এবং representation sharing হতে পারে।

সব architecture-এ এটি বাধ্যতামূলক নয়।

---

# 51. GPT-Style AI Writing Platform

তোমার AI writing platform-এর জন্য GPT-style architecture সবচেয়ে গুরুত্বপূর্ণ কারণ এটি generation করতে পারে।

Potential flow:

```text id="awriting"
User Input
    │
    ▼
Tokenizer
    │
    ▼
Token IDs
    │
    ▼
GPT / Decoder-only LLM
    │
    ▼
Next Token Prediction
    │
    ▼
Autoregressive Generation
    │
    ▼
Generated Text
```

---

# 52. Humanization / Writing Improvement Architecture

একটি safe writing-improvement system:

```text
                USER TEXT
                    │
                    ▼
              Text Analysis
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
       Grammar    Style     Meaning
       Analysis   Analysis   Analysis
          │         │         │
          └─────────┼─────────┘
                    ▼
              Rewrite Prompt
                    │
                    ▼
             GPT-style Model
                    │
                    ▼
              Candidate Text
                    │
                    ▼
             Quality Evaluation
                    │
                    ▼
              Improved Text
```

এখানে লক্ষ্য হওয়া উচিত **clarity, fluency, tone, readability ও meaning preservation**—কোনো external detector বা safeguard bypass করা নয়।

---

# 53. BERT + GPT একসাথে ব্যবহার

একটি advanced system-এ:

```text
BERT-style Encoder
        │
        ▼
Understanding
        │
        ▼
GPT-style Generator
        │
        ▼
Generation
```

কিন্তু বাস্তবে modern LLM systems অনেক সময় একটি decoder-only model দিয়েই analysis + generation দুটো কাজ করতে পারে।

---

# 54. GPT Model Training Pipeline

```text
Large Text Corpus
       │
       ▼
Data Cleaning
       │
       ▼
Tokenizer
       │
       ▼
Token IDs
       │
       ▼
Training Sequences
       │
       ▼
GPT Model
       │
       ▼
Next Token Prediction
       │
       ▼
Cross Entropy Loss
       │
       ▼
Backpropagation
       │
       ▼
Optimizer
       │
       ▼
Weight Update
       │
       └──────→ Repeat
```

---

# 55. Pretraining → Fine-Tuning

GPT-এর ক্ষেত্রে সাধারণ pipeline:

```text
Large General Corpus
        ↓
Pretraining
        ↓
Base Language Model
        ↓
Fine-tuning / Instruction Tuning
        ↓
Task / Behavior Adaptation
```

Modern assistant models-এ এর পর preference/alignment training-এর বিভিন্ন techniques থাকতে পারে।

---

# 56. Base Model vs Instruction Model

### Base Model

মূলত:

```text
Next-token prediction
```

### Instruction-tuned Model

User instruction follow করার জন্য additional training করা হয়।

Example:

```text
User:
Explain Python loops.

Model:
Detailed explanation...
```

---

# 57. GPT-এর Important Components

এক নজরে:

```text id="gptelements"
GPT
│
├── Tokenizer
├── Token Embedding
├── Position Information
├── Transformer Blocks
│   ├── LayerNorm
│   ├── Causal Self-Attention
│   ├── Residual
│   ├── LayerNorm
│   ├── MLP/FFN
│   └── Residual
│
├── Final LayerNorm
├── LM Head
├── Softmax
└── Autoregressive Decoder
```

---

# 58. PyTorch Mini GPT Block

Foundation বোঝার জন্য একটি simplified implementation:

```python id="pygpt1"
import torch
import torch.nn as nn


class GPTBlock(nn.Module):

    def __init__(
        self,
        d_model=128,
        num_heads=8,
        d_ff=512,
        dropout=0.1
    ):
        super().__init__()

        self.norm1 = nn.LayerNorm(d_model)

        self.attention = nn.MultiheadAttention(
            embed_dim=d_model,
            num_heads=num_heads,
            dropout=dropout,
            batch_first=True
        )

        self.norm2 = nn.LayerNorm(d_model)

        self.ffn = nn.Sequential(
            nn.Linear(d_model, d_ff),
            nn.GELU(),
            nn.Linear(d_ff, d_model)
        )

        self.dropout = nn.Dropout(dropout)

    def forward(self, x):

        seq_len = x.size(1)

        causal_mask = torch.triu(
            torch.ones(
                seq_len,
                seq_len,
                device=x.device,
                dtype=torch.bool
            ),
            diagonal=1
        )

        attn_input = self.norm1(x)

        attn_output, _ = self.attention(
            attn_input,
            attn_input,
            attn_input,
            attn_mask=causal_mask
        )

        x = x + self.dropout(attn_output)

        ffn_input = self.norm2(x)

        ffn_output = self.ffn(ffn_input)

        x = x + self.dropout(ffn_output)

        return x
```

---

# 59. Simple GPT Model

```python id="pygpt2"
class SimpleGPT(nn.Module):

    def __init__(
        self,
        vocab_size,
        max_seq_len,
        d_model=128,
        num_heads=8,
        d_ff=512,
        num_layers=4
    ):
        super().__init__()

        self.token_embedding = nn.Embedding(
            vocab_size,
            d_model
        )

        self.position_embedding = nn.Embedding(
            max_seq_len,
            d_model
        )

        self.blocks = nn.ModuleList([
            GPTBlock(
                d_model=d_model,
                num_heads=num_heads,
                d_ff=d_ff
            )
            for _ in range(num_layers)
        ])

        self.norm = nn.LayerNorm(d_model)

        self.lm_head = nn.Linear(
            d_model,
            vocab_size
        )

    def forward(self, input_ids):

        batch_size, seq_len = input_ids.shape

        positions = torch.arange(
            seq_len,
            device=input_ids.device
        )

        token_embeddings = self.token_embedding(
            input_ids
        )

        position_embeddings = self.position_embedding(
            positions
        )

        x = token_embeddings + position_embeddings

        for block in self.blocks:
            x = block(x)

        x = self.norm(x)

        logits = self.lm_head(x)

        return logits
```

---

# 60. Tensor Shapes

ধরি:

```text
B = 4
L = 128
D = 128
V = 10,000
```

Input:

```text
(B,L)
=
(4,128)
```

Token embedding:

```text
(4,128,128)
```

Transformer blocks:

```text
(4,128,128)
```

Final LM head:

```text
(4,128,10000)
```

অর্থাৎ প্রতিটি position-এর জন্য পুরো vocabulary-এর logits।

---

# 61. Training Target Shift

ধরি:

```text
Input:
I love AI
```

Conceptually:

```text
Input:
I      love      AI

Target:
love   AI        <EOS>
```

Model প্রতিটি position-এ next token predict করে।

---

# 62. PyTorch Loss

ধরি:

```python id="pyloss"
logits = model(input_ids)
```

Shape:

```text
(B, L, V)
```

Target:

```text
(B, L)
```

Cross entropy:

```python id="loss1"
loss_fn = nn.CrossEntropyLoss()

loss = loss_fn(
    logits.reshape(-1, logits.size(-1)),
    targets.reshape(-1)
)
```

Conceptually:

```text
(B,L,V)
 ↓
(B×L,V)

(B,L)
 ↓
(B×L)
```

তারপর cross-entropy।

---

# 63. GPT Generation Pseudocode

```python id="gengpt"
tokens = prompt_tokens

for _ in range(max_new_tokens):

    logits = model(tokens)

    next_token_logits = logits[:, -1, :]

    next_token = sample(
        next_token_logits
    )

    tokens = torch.cat(
        [tokens, next_token],
        dim=1
    )
```

এটাই basic autoregressive generation।

বাস্তবে context limit, KV cache, batching, sampling, stopping criteria ইত্যাদি handle করতে হয়।

---

# 64. GPT-এর Complete Mental Model

```text id="mastergpt"
                         GPT
                          │
                 Decoder-only Model
                          │
                          ▼
                       Tokenizer
                          │
                          ▼
                       Token IDs
                          │
                          ▼
                   Token Embedding
                          +
                  Position Information
                          │
                          ▼
              ┌──────────────────────┐
              │    GPT Block         │
              │                      │
              │  LayerNorm           │
              │      ↓               │
              │  Causal MHA          │
              │      ↓               │
              │  Residual            │
              │      ↓               │
              │  LayerNorm           │
              │      ↓               │
              │  MLP / FFN           │
              │      ↓               │
              │  Residual            │
              └──────────┬───────────┘
                         │
                    Repeat N times
                         │
                         ▼
                  Final LayerNorm
                         │
                         ▼
                      LM Head
                         │
                         ▼
                       Logits
                         │
                         ▼
                      Softmax
                         │
                         ▼
                    Next Token
                         │
                         ▼
                     Append
                         │
                         └──────→ Repeat
```

---

# 65. BERT বনাম GPT — Final Comparison

| Feature          | BERT          | GPT                   |
| ---------------- | ------------- | --------------------- |
| Architecture     | Encoder-only  | Decoder-only          |
| Attention        | Bidirectional | Causal                |
| Future tokens    | Visible       | Blocked               |
| Main objective   | MLM-style     | Next-token prediction |
| Primary strength | Understanding | Generation            |
| `[CLS]`          | Commonly used | Not standard          |
| Cross-attention  | No            | No                    |
| NER              | Excellent     | Possible              |
| Classification   | Excellent     | Possible              |
| Text generation  | Not primary   | Core capability       |
| Autoregressive   | No            | Yes                   |

---

# 66. Interview Questions

### Q1. What is GPT?

GPT is a generative pretrained Transformer based on a decoder-only Transformer architecture.

### Q2. Why is GPT called decoder-only?

কারণ GPT-style architecture-এ separate Transformer encoder নেই এবং causal self-attention-based decoder blocks ব্যবহার করা হয়।

### Q3. Why does GPT use causal masking?

Future tokens block করার জন্য, যাতে model শুধু previous/current context ব্যবহার করে next token predict করে।

### Q4. What is autoregressive generation?

প্রতিটি generated token পরবর্তী token prediction-এর context হিসেবে ব্যবহার করার generation process।

### Q5. GPT কি BERT-এর মতো bidirectional?

Standard GPT causal attention ব্যবহার করে, তাই একই position থেকে future tokens visible নয়।

### Q6. GPT decoder-এ cross-attention আছে?

Standard decoder-only GPT-তে **না**। Cross-attention-এর জন্য আলাদা encoder representation দরকার।

### Q7. GPT কী predict করে?

পরবর্তী token-এর probability distribution।

### Q8. Logits কী?

Vocabulary-এর প্রতিটি token-এর জন্য softmax-এর আগের raw scores।

### Q9. Temperature কী করে?

Sampling distribution-এর sharpness/diversity নিয়ন্ত্রণ করে।

### Q10. KV cache কেন?

Autoregressive generation-এ previous keys এবং values পুনরায় compute করার প্রয়োজন কমিয়ে inference efficiency বাড়াতে।

---

# 67. Practice

## Beginner

নিজে লিখে explain করো:

```text
GPT
 ↓
Tokenizer
 ↓
Embedding
 ↓
Causal Self-Attention
 ↓
FFN
 ↓
LM Head
 ↓
Next Token
```

প্রতিটি step-এর কাজ লিখবে।

---

## Intermediate

এই sentence:

```text
I love machine learning
```

এর জন্য causal attention matrix তৈরি করো।

---

## Advanced

PyTorch-এ:

```text
vocab_size = 5000
d_model = 128
heads = 8
layers = 4
```

দিয়ে ছোট GPT model তৈরি করো।

তারপর:

```text
Input:
I love

Target:
AI
```

next-token training করো।

---

# 68. M02.29 Completion Checklist

```text
☑ GPT definition
☑ GPT full form
☑ Generative
☑ Pre-trained
☑ Transformer
☑ Decoder-only architecture
☑ Autoregressive modeling
☑ Next-token prediction
☑ Causal masking
☑ Tokenization
☑ Token embedding
☑ Position information
☑ Self-attention
☑ Multi-head attention
☑ Q/K/V
☑ Scaling
☑ Causal mask
☑ Softmax
☑ Residual connection
☑ LayerNorm
☑ Pre-Norm
☑ FFN / MLP
☑ Transformer block
☑ Layer stacking
☑ Final LayerNorm
☑ LM Head
☑ Logits
☑ Cross-entropy
☑ Teacher forcing
☑ Training vs inference
☑ Autoregressive generation
☑ Greedy decoding
☑ Temperature
☑ Top-k
☑ Top-p
☑ Context window
☑ KV Cache
☑ BERT vs GPT
☑ Original Decoder vs GPT
☑ GPT training pipeline
☑ GPT generation pipeline
☑ PyTorch implementation
☑ AI writing application
```

---

# 🧠 Final Concept

তুমি এখন এই difference-টা মাথায় স্থায়ীভাবে বসিয়ে ফেলো:

```text
                  TRANSFORMER
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
       BERT           T5           GPT
          │            │            │
      Encoder       Encoder +     Decoder
        Only         Decoder        Only
          │            │            │
   Bidirectional    Seq2Seq       Causal
     Attention      Attention     Attention
          │            │            │
   Understanding   Translation   Generation
                   / Seq2Seq
```

আর GPT-এর সবচেয়ে গুরুত্বপূর্ণ flow:

```text
Prompt
  ↓
Tokenizer
  ↓
Token IDs
  ↓
Embedding + Position
  ↓
Causal Self-Attention
  ↓
FFN
  ↓
Repeat N Layers
  ↓
LM Head
  ↓
Logits
  ↓
Softmax
  ↓
Next Token
  ↓
Append Token
  ↓
Repeat
```

**M02.29 সম্পূর্ণ।**

পরবর্তী logical lesson হবে **M02.30 — GPT Training Deep Dive**, যেখানে আমরা শুধু architecture নয়, **dataset তৈরি → tokenization → sequence creation → labels → causal masking → forward pass → cross-entropy loss → backpropagation → optimizer → checkpoint → validation → overfitting → training loop** একদম practicalভাবে শিখব।

---
# M02.30 — GPT Training Deep Dive

আজ আমরা GPT architecture-এর পরের সবচেয়ে গুরুত্বপূর্ণ অংশ শিখব: **কীভাবে একটি GPT-style language model train করা হয়**।

আগের lesson-এ তুমি শিখেছ:

```text
M02.29
GPT Architecture
      ↓
M02.30
GPT Training
```

এই lesson শেষে তুমি বুঝতে পারবে:

```text
Raw Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Training Sequences
 ↓
Input / Target
 ↓
Causal Mask
 ↓
Forward Pass
 ↓
Logits
 ↓
Cross Entropy Loss
 ↓
Backpropagation
 ↓
Optimizer
 ↓
Weight Update
 ↓
Validation
 ↓
Checkpoint
```

---

# 1. GPT Training-এর মূল উদ্দেশ্য

GPT-এর মূল objective খুব simple:

> **Previous tokens দেখে next token predict করা।**

Example:

```text
Input:
I love

Target:
AI
```

Model প্রথমে হয়তো predict করবে:

```text
AI       → 0.20
Python   → 0.15
coding   → 0.10
music    → 0.05
...
```

Target যদি `AI` হয়, তাহলে model-এর ভুল বেশি।

Training-এর লক্ষ্য:

```text
Prediction
    ↓
Compare with target
    ↓
Loss
    ↓
Backpropagation
    ↓
Weights update
    ↓
Better prediction
```

---

# 2. GPT Training Pipeline

সম্পূর্ণ pipeline:

```text
                RAW TEXT
                    │
                    ▼
              DATA CLEANING
                    │
                    ▼
                TOKENIZER
                    │
                    ▼
                TOKEN IDs
                    │
                    ▼
            TRAINING SEQUENCES
                    │
                    ▼
             INPUT / TARGET
                    │
                    ▼
              GPT MODEL
                    │
                    ▼
              CAUSAL MASK
                    │
                    ▼
                LOGITS
                    │
                    ▼
           CROSS-ENTROPY LOSS
                    │
                    ▼
            BACKPROPAGATION
                    │
                    ▼
               OPTIMIZER
                    │
                    ▼
              WEIGHT UPDATE
                    │
                    └───────→ Repeat
```

---

# 3. Training Data কী?

GPT train করার জন্য text data প্রয়োজন।

Example:

```text
Python is a programming language.
Python is easy to learn.
Machine learning uses data.
Deep learning uses neural networks.
```

এগুলো হলো raw text।

একটি বড় dataset হতে পারে:

```text
Books
Articles
Web documents
Code
Documentation
Conversations
News
Educational text
```

তবে production-scale training-এর ক্ষেত্রে data licensing, privacy, quality, filtering এবং safety অত্যন্ত গুরুত্বপূর্ণ।

---

# 4. Raw Text থেকে Token

ধরি:

```text
I love machine learning.
```

Tokenizer এটাকে token pieces-এ convert করবে।

Conceptually:

```text
I
love
machine
learning
.
```

তারপর:

```text
Token
 ↓
Token ID
```

Example:

```text
I          → 45
love       → 892
machine    → 2311
learning   → 982
.          → 13
```

Actual IDs tokenizer-এর উপর নির্ভর করে।

---

# 5. Tokenizer Training-এর গুরুত্বপূর্ণ অংশ

GPT model token directly বুঝে না।

Model receives:

```text
Token IDs
```

তারপর:

```text
Token IDs
 ↓
Embedding
 ↓
Vectors
```

তাই:

```text
TEXT
 ↓
TOKENIZER
 ↓
TOKEN IDs
 ↓
MODEL
```

---

# 6. Training Sequence তৈরি

ধরি token IDs:

```text
[10, 20, 30, 40, 50, 60]
```

এখানে:

```text
10 = I
20 = love
30 = machine
40 = learning
50 = with
60 = Python
```

যদি sequence length `4` হয়:

```text
[10,20,30,40]
```

এরপর next tokens predict করা হবে।

---

# 7. Input এবং Target

সবচেয়ে গুরুত্বপূর্ণ concept।

Text:

```text
I love machine learning
```

Token:

```text
I       love      machine      learning
```

Training:

```text
Input:

I       love      machine

Target:

love    machine   learning
```

অর্থাৎ:

```text
Input[t] → Target[t]
```

---

# 8. Shifted Target

আরেকটি representation:

```text
Input:
I love machine learning

Target:
love machine learning <EOS>
```

এখানে target এক position shifted।

এটাই **next-token prediction**।

---

# 9. Multiple Positions একসাথে

GPT-এর বড় সুবিধা হলো training-এর সময় sequence-এর সব positions parallelভাবে process করা যায়।

ধরি:

```text
Input:
I love machine learning
```

Model simultaneously predict করবে:

```text
I      → love
love   → machine
machine → learning
learning → <EOS>
```

কিন্তু causal mask নিশ্চিত করবে:

```text
I
```

`machine` বা `learning` দেখতে পারবে না।

---

# 10. Causal Mask

আগের lesson-এর concept এখানে সরাসরি ব্যবহার হবে।

```text
             I   love   machine   learning

I            ✓    ✗       ✗         ✗
love         ✓    ✓       ✗         ✗
machine      ✓    ✓       ✓         ✗
learning     ✓    ✓       ✓         ✓
```

এতে:

```text
Future tokens
     ↓
Blocked
```

---

# 11. কেন Mask দরকার?

Mask ছাড়া:

```text
I → love machine learning
```

সব future information দেখা সম্ভব।

তাহলে model cheating করতে পারে।

Mask সহ:

```text
I
 ↓
Only I

love
 ↓
I + love

machine
 ↓
I + love + machine
```

এটাই genuine autoregressive learning।

---

# 12. Sequence Length

ধরি:

```text
SEQ_LEN = 8
```

তাহলে training sample:

```text
Token 1
Token 2
Token 3
...
Token 8
```

Model প্রতি position-এর next token predict করে।

Large-scale training-এ sequence length খুব গুরুত্বপূর্ণ কারণ standard self-attention-এর computational cost sequence length-এর সাথে quadraticভাবে বাড়ে।

---

# 13. Batch

একটি sequence দিয়ে training করা inefficient।

তাই multiple sequences একসাথে:

```text
Batch = 4
```

Example:

```text
Sequence 1
Sequence 2
Sequence 3
Sequence 4
```

Input shape:

```text
(B, L)
```

যদি:

```text
B = 4
L = 128
```

তাহলে:

```text
(4,128)
```

---

# 14. Embedding

Input:

```text
(B,L)
```

Embedding-এর পরে:

```text
(B,L,D)
```

যদি:

```text
B = 4
L = 128
D = 256
```

তাহলে:

```text
(4,128,256)
```

---

# 15. Transformer Blocks

তারপর:

```text
Embedding
 ↓
GPT Block 1
 ↓
GPT Block 2
 ↓
GPT Block 3
 ↓
...
 ↓
GPT Block N
```

Shape সাধারণত একই থাকে:

```text
(B,L,D)
```

---

# 16. LM Head

শেষে:

```text
(B,L,D)
```

থেকে:

```text
(B,L,V)
```

যেখানে:

* `B` = batch size
* `L` = sequence length
* `D` = hidden dimension
* `V` = vocabulary size

Example:

```text
B = 4
L = 128
D = 256
V = 10,000
```

Output:

```text
(4,128,10000)
```

---

# 17. Logits

প্রতিটি position-এর জন্য vocabulary-এর প্রতিটি token-এর score থাকে।

Example:

```text
Position = "I love"

AI       → 2.4
Python   → 1.9
machine  → 1.2
football → 0.3
...
```

এগুলো:

```text
Logits
```

---

# 18. Softmax

Logits:

```text
[2.4, 1.9, 1.2, 0.3]
```

Softmax:

```text
[0.45, 0.27, 0.13, 0.05, ...]
```

এগুলো probability distribution।

তবে PyTorch training-এ সাধারণত **raw logits সরাসরি `CrossEntropyLoss`-এ দেওয়া হয়**; আগে manually softmax করার প্রয়োজন নেই।

---

# 19. Cross-Entropy Loss

Target token-এর probability যত কম:

```text
Loss ↑
```

Target token-এর probability যত বেশি:

```text
Loss ↓
```

Formula:

$$
L=-\log P(y_{true})
$$

Example:

```text
Target = AI
```

যদি:

```text
P(AI)=0.9
```

তাহলে:

$$
L=-\log(0.9)
$$

খুব ছোট loss।

কিন্তু:

```text
P(AI)=0.01
```

হলে:

$$
L=-\log(0.01)
$$

বড় loss।

---

# 20. Cross-Entropy কেন ব্যবহার করা হয়?

কারণ GPT classification-এর মতো vocabulary থেকে একটি target token predict করছে।

ধরি:

```text
Vocabulary = 50,000
```

প্রতিটি position-এর জন্য:

```text
50,000 possible tokens
```

এর মধ্যে correct token-এর probability maximize করতে হবে।

---

# 21. Training Example

Text:

```text
I love AI
```

ধরি:

```text
I    = 10
love = 20
AI   = 30
```

Input:

```text
[10,20]
```

Target:

```text
[20,30]
```

Model:

```text
10 → predicts 20
20 → predicts 30
```

Loss:

```text
Loss1 + Loss2
```

তারপর average/sum reduction।

---

# 22. Forward Pass

Forward pass:

```text
Input IDs
    ↓
Embedding
    ↓
Position Information
    ↓
Transformer Blocks
    ↓
Final LayerNorm
    ↓
LM Head
    ↓
Logits
```

এখানে model-এর parameters এখনও update হয়নি।

---

# 23. Loss Calculation

```text
Logits
   +
Target
   ↓
Cross Entropy
   ↓
Loss
```

Example:

```python
loss = loss_fn(
    logits.reshape(-1, vocab_size),
    targets.reshape(-1)
)
```

---

# 24. Backpropagation

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

ধরি:

```text
Loss = 3.2
```

Model জানতে চায়:

> কোন parameters-এর কারণে এই error হয়েছে?

Backpropagation gradient calculate করে।

```text
Loss
 ↓
Gradients
 ↓
Model Parameters
```

---

# 25. Gradient

Gradient বলে:

> Parameter সামান্য পরিবর্তন করলে loss কোন দিকে এবং কতটা পরিবর্তিত হবে?

Mathematically:

$$
\frac{\partial L}{\partial w}
$$

যেখানে:

* `L` = loss
* `w` = weight

---

# 26. Optimizer

Gradient পাওয়ার পর optimizer weights update করে।

Popular optimizers:

```text
SGD
Adam
AdamW
```

GPT/Transformer training-এ **AdamW** একটি খুব গুরুত্বপূর্ণ optimizer।

---

# 27. Weight Update

Simplified:

$$
w_{new}=w_{old}-\eta\nabla_wL
$$

যেখানে:

* `w` = weight
* `η` = learning rate
* `∇L` = gradient

---

# 28. Learning Rate

Learning rate ঠিক করে:

> কত বড় step নিয়ে weights update হবে।

### খুব বড়:

```text
Learning Rate ↑
 ↓
Training unstable হতে পারে
```

### খুব ছোট:

```text
Learning Rate ↓
 ↓
Training খুব slow হতে পারে
```

---

# 29. Complete Training Step

একটি training step:

```text
Input Batch
    ↓
Forward Pass
    ↓
Logits
    ↓
Loss
    ↓
Backward Pass
    ↓
Gradients
    ↓
Optimizer Step
    ↓
Updated Weights
```

PyTorch:

```python
optimizer.zero_grad()

logits = model(input_ids)

loss = loss_fn(
    logits.reshape(-1, vocab_size),
    targets.reshape(-1)
)

loss.backward()

optimizer.step()
```

---

# 30. কেন `zero_grad()`?

PyTorch সাধারণত gradients accumulate করে।

তাই next batch-এর আগে:

```python
optimizer.zero_grad()
```

দিয়ে previous gradients clear করা হয়।

---

# 31. Training Loop

একটি basic loop:

```python
for epoch in range(num_epochs):

    model.train()

    for input_ids, targets in train_loader:

        optimizer.zero_grad()

        logits = model(input_ids)

        loss = loss_fn(
            logits.reshape(-1, vocab_size),
            targets.reshape(-1)
        )

        loss.backward()

        optimizer.step()

    print(
        "Epoch:",
        epoch,
        "Loss:",
        loss.item()
    )
```

এটাই GPT training-এর fundamental loop।

---

# 32. Epoch কী?

একবার পুরো training dataset-এর উপর model train করা:

```text
1 Epoch
```

Example:

```text
Dataset = 1,000,000 samples
```

একবার সব samples process:

```text
1 epoch
```

---

# 33. Batch vs Epoch

ধরি:

```text
Dataset = 10,000 samples
Batch size = 100
```

তাহলে:

$$
10000/100=100
$$

অর্থাৎ:

```text
100 steps ≈ 1 epoch
```

---

# 34. Iteration / Step

এক batch process:

```text
1 training step
```

যেমন:

```text
Batch 1 → Step 1
Batch 2 → Step 2
Batch 3 → Step 3
...
```

---

# 35. Training Loss

Training চলাকালীন:

```text
Epoch 1 → Loss 5.2
Epoch 2 → Loss 4.4
Epoch 3 → Loss 3.8
Epoch 4 → Loss 3.2
```

Generally:

```text
Loss ↓
```

মানে model training data-এর next-token prediction ভালো শিখছে।

কিন্তু শুধু training loss কমলেই model ভালো generalize করবে—এমন নয়।

---

# 36. Validation Dataset

Dataset সাধারণত ভাগ করা হয়:

```text
Dataset
 ├── Train
 ├── Validation
 └── Test
```

Training:

```text
Train → weights update
```

Validation:

```text
Validation → monitor performance
```

Test:

```text
Test → final evaluation
```

---

# 37. Validation Loss

Training:

```text
Train Loss ↓
```

কিন্তু:

```text
Validation Loss ↓
```

হওয়াটাও গুরুত্বপূর্ণ।

Example:

```text
Epoch 1
Train = 4.5
Val   = 4.7

Epoch 5
Train = 2.0
Val   = 2.2

Epoch 10
Train = 1.2
Val   = 3.0
```

এখানে overfitting-এর signal দেখা যাচ্ছে।

---

# 38. Overfitting

Model training data খুব ভালোভাবে memorize করে কিন্তু unseen data-তে performance খারাপ হয়।

```text
Training
   ↓
Very good

Validation
   ↓
Poor
```

এটাই overfitting।

---

# 39. GPT Training-এ Overfitting

Possible causes:

```text
Small dataset
Too many training epochs
Poor data diversity
Insufficient regularization
Data duplication
```

Large language model pretraining-এ data quality, deduplication, mixture design, training duration এবং scale গুরুত্বপূর্ণ।

---

# 40. Dropout

Transformer block-এ dropout ব্যবহার করা যেতে পারে।

```text
Training:
Dropout ON

Evaluation:
Dropout OFF
```

PyTorch:

```python
model.train()
```

Training mode।

```python
model.eval()
```

Evaluation mode।

---

# 41. `torch.no_grad()`

Validation-এর সময় gradients দরকার নেই।

```python
model.eval()

with torch.no_grad():

    logits = model(input_ids)

    loss = loss_fn(
        logits.reshape(-1, vocab_size),
        targets.reshape(-1)
    )
```

এতে memory এবং computation save হয়।

---

# 42. Checkpoint

Training-এর সময় model save করা হয়।

```text
Checkpoint
```

সাধারণত save করা হয়:

```text
Model weights
Optimizer state
Scheduler state
Epoch
Step
Training metadata
```

Example:

```python
torch.save(
    {
        "model_state_dict": model.state_dict(),
        "optimizer_state_dict": optimizer.state_dict(),
        "epoch": epoch,
    },
    "checkpoint.pt"
)
```

---

# 43. কেন Checkpoint দরকার?

ধরি training:

```text
Epoch 1
Epoch 2
Epoch 3
Epoch 4
```

Epoch 4-এ PC crash করল।

Checkpoint না থাকলে:

```text
Training আবার শুরু
```

Checkpoint থাকলে:

```text
Checkpoint
 ↓
Resume training
```

---

# 44. Gradient Clipping

Deep neural network training-এ কখনও gradients খুব বড় হতে পারে।

এটাকে:

```text
Exploding Gradient
```

বলা হয়।

Gradient clipping:

```python
torch.nn.utils.clip_grad_norm_(
    model.parameters(),
    max_norm=1.0
)
```

তারপর:

```python
optimizer.step()
```

---

# 45. Learning Rate Scheduler

Training-এর সময় learning rate পরিবর্তন করা যায়।

Conceptually:

```text
Start
 ↓
Higher LR
 ↓
Gradually decrease
 ↓
Fine adjustment
```

Popular schedules:

```text
Linear decay
Cosine decay
Warmup + decay
```

Transformer training-এ **warmup** বিশেষভাবে গুরুত্বপূর্ণ হতে পারে।

---

# 46. Warmup

Training শুরুতেই learning rate ধীরে ধীরে বাড়ানো:

```text
Step 1
LR = small

Step 100
LR = medium

Step 1000
LR = target LR
```

তারপর decay করা হতে পারে।

```text
Warmup
   ↓
Peak LR
   ↓
Decay
```

---

# 47. AdamW

GPT-style training-এ AdamW গুরুত্বপূর্ণ।

Conceptually:

```python
optimizer = torch.optim.AdamW(
    model.parameters(),
    lr=3e-4,
    weight_decay=0.01
)
```

এখানে:

```text
lr
→ learning rate

weight_decay
→ regularization
```

Exact hyperparameters model size, dataset এবং training setup-এর উপর নির্ভর করে।

---

# 48. Mixed Precision

Modern GPU training-এ:

```text
FP32
```

এর পাশাপাশি:

```text
FP16
BF16
```

ব্যবহার করা যায়।

এতে:

```text
Memory ↓
Speed ↑
```

হতে পারে।

বিশেষ করে modern GPU-তে BF16 training অনেক ক্ষেত্রে সুবিধাজনক।

---

# 49. Gradient Accumulation

GPU memory কম হলে বড় effective batch simulate করা যায়।

ধরি:

```text
Actual batch = 4
Accumulation steps = 8
```

Effective batch approximately:

```text
4 × 8 = 32
```

Concept:

```text
Batch 1 → gradient
Batch 2 → accumulate
Batch 3 → accumulate
...
Batch 8 → optimizer step
```

---

# 50. Distributed Training

Large GPT model একটি GPU-তে fit নাও করতে পারে।

তখন:

```text
GPU 1
GPU 2
GPU 3
GPU 4
```

একসাথে training করা যায়।

Large-scale training-এ বিভিন্ন parallelism strategy ব্যবহৃত হয়:

```text
Data Parallelism
Tensor Parallelism
Pipeline Parallelism
```

এগুলো পরে advanced stage-এ বিস্তারিত শেখা হবে।

---

# 51. Data Quality

GPT training-এ শুধু dataset size গুরুত্বপূর্ণ নয়।

Quality খুব গুরুত্বপূর্ণ।

Bad data:

```text
Spam
Duplicates
Broken text
Low-quality content
Incorrect encoding
Malformed documents
```

এগুলো model quality খারাপ করতে পারে।

---

# 52. Data Cleaning Pipeline

```text
Raw Data
   ↓
Deduplication
   ↓
Quality Filtering
   ↓
Language Filtering
   ↓
Safety Filtering
   ↓
Normalization
   ↓
Tokenization
   ↓
Training Dataset
```

---

# 53. Data Leakage

Training এবং validation/test data overlap করলে evaluation misleading হতে পারে।

Example:

```text
Train:
"I love machine learning."

Validation:
"I love machine learning."
```

তাহলে validation performance artificially high হতে পারে।

তাই dataset split এবং deduplication গুরুত্বপূর্ণ।

---

# 54. Padding

সব sequence একই length না হলে padding দরকার হতে পারে।

Example:

```text
"I love AI"

"I love machine learning"
```

Padding:

```text
I love AI <PAD> <PAD>

I love machine learning
```

তারপর padding positions attention/loss থেকে appropriately mask করা হয়।

---

# 55. Padding Loss Mask

ধরি:

```text
Target:
love machine <PAD>
```

`<PAD>` position-এর জন্য loss calculate করা উচিত নয়।

PyTorch:

```python
loss_fn = nn.CrossEntropyLoss(
    ignore_index=pad_token_id
)
```

এতে padding token loss calculation থেকে বাদ দেওয়া যায়।

---

# 56. GPT Training-এ Attention Mask বনাম Loss Mask

দুটো আলাদা concept।

### Attention Mask

Model কোন token দেখতে পারবে?

```text
Future
 ↓
Blocked
```

### Loss Mask

কোন position-এর prediction-এর জন্য loss calculate হবে?

```text
PAD
 ↓
Ignored
```

Important:

```text
Attention masking
≠
Loss masking
```

---

# 57. Training Data Packing

অনেক ছোট document থাকলে padding-এর কারণে computation waste হতে পারে।

একাধিক text sequence carefully concatenate/pack করে full-length training sequences তৈরি করা যায়।

Concept:

```text
Doc A
+
Doc B
+
Doc C
 ↓
Long Training Sequence
```

তবে document boundary এবং special/end-of-document tokens সঠিকভাবে handle করতে হয়।

---

# 58. GPT Pretraining বনাম Fine-Tuning

### Pretraining

```text
Huge General Dataset
 ↓
Next Token Prediction
 ↓
Base Model
```

### Fine-tuning

```text
Task-specific Dataset
 ↓
Base Model
 ↓
Specialized Model
```

---

# 59. Instruction Tuning

Base GPT model next-token prediction জানে।

কিন্তু user instruction follow করার behavior improve করতে instruction-response datasets দিয়ে additional training করা যায়।

Example:

```text
Instruction:
Explain recursion.

Response:
Recursion is...
```

Training:

```text
Instruction + Response
        ↓
Model adaptation
```

---

# 60. Supervised Fine-Tuning

SFT = **Supervised Fine-Tuning**

Dataset:

```text
Prompt
Response
```

Example:

```text
Prompt:
Explain Python list.

Response:
A Python list is...
```

Model response generation pattern শেখে।

---

# 61. Pretraining vs SFT

```text
PRETRAINING
Large diverse text
 ↓
General language knowledge
```

```text
SFT
Instruction-response data
 ↓
Instruction following
```

---

# 62. GPT Training from Scratch — Practical Architecture

```text
                    DATA
                     │
                     ▼
                  TOKENIZER
                     │
                     ▼
                TOKEN IDs
                     │
                     ▼
              DATASET / DATALOADER
                     │
                     ▼
                  GPT MODEL
                     │
                     ▼
             CAUSAL SELF-ATTENTION
                     │
                     ▼
                   FFN
                     │
                     ▼
                LOGITS
                     │
                     ▼
                 LOSS
                     │
                     ▼
              BACKPROPAGATION
                     │
                     ▼
                ADAMW
                     │
                     ▼
             UPDATED WEIGHTS
                     │
                     ▼
                VALIDATION
                     │
                     ▼
                CHECKPOINT
```

---

# 63. Complete PyTorch Mini Training Example

একটি ছোট educational example:

```python
import torch
import torch.nn as nn
import torch.optim as optim


vocab_size = 1000

model = SimpleGPT(
    vocab_size=vocab_size,
    max_seq_len=128,
    d_model=128,
    num_heads=8,
    d_ff=512,
    num_layers=4
)

loss_fn = nn.CrossEntropyLoss()

optimizer = optim.AdamW(
    model.parameters(),
    lr=3e-4,
    weight_decay=0.01
)


for epoch in range(5):

    model.train()

    for input_ids, targets in train_loader:

        optimizer.zero_grad()

        logits = model(input_ids)

        loss = loss_fn(
            logits.reshape(-1, vocab_size),
            targets.reshape(-1)
        )

        loss.backward()

        torch.nn.utils.clip_grad_norm_(
            model.parameters(),
            max_norm=1.0
        )

        optimizer.step()

    print(
        f"Epoch {epoch + 1}, "
        f"Loss: {loss.item():.4f}"
    )
```

এখানে `SimpleGPT` হলো আগের lesson-এর educational model।

---

# 64. Validation Loop

```python
model.eval()

total_loss = 0

with torch.no_grad():

    for input_ids, targets in val_loader:

        logits = model(input_ids)

        loss = loss_fn(
            logits.reshape(-1, vocab_size),
            targets.reshape(-1)
        )

        total_loss += loss.item()

avg_loss = total_loss / len(val_loader)

print("Validation Loss:", avg_loss)
```

---

# 65. Perplexity

Language model evaluation-এর গুরুত্বপূর্ণ metric:

**Perplexity (PPL)**

$$
PPL=e^{Loss}
$$

যদি:

```text
Loss = 2
```

তাহলে:

$$
PPL=e^2
$$

অর্থাৎ প্রায়:

```text
7.39
```

সাধারণভাবে lower perplexity better predictive performance-এর signal, কিন্তু model quality বিচার করতে শুধু PPL যথেষ্ট নয়।

---

# 66. Perplexity কী বোঝায়?

সহজভাবে:

> Model next token prediction-এ কতটা uncertain?

Lower:

```text
Uncertainty ↓
```

Higher:

```text
Uncertainty ↑
```

তবে tokenizer, dataset এবং evaluation setup বদলালে perplexity সরাসরি comparable নাও হতে পারে।

---

# 67. Training-এর Complete Mathematical Flow

Input:

$$
X
$$

Embedding:

$$
E(X)
$$

Transformer:

$$
H = Transformer(E(X))
$$

LM Head:

$$
Z = HW_{LM}
$$

Softmax conceptually:

$$
P=softmax(Z)
$$

Loss:

$$
L=-\sum_t \log P(x_t|x_{<t})
$$

Gradient:

$$
\nabla_\theta L
$$

Update:

$$
\theta_{new}
=
Optimizer(\theta,\nabla_\theta L)
$$

---

# 68. One Training Step — Mental Model

এটা সবচেয়ে গুরুত্বপূর্ণ:

```text
                INPUT
                  │
                  ▼
              GPT MODEL
                  │
                  ▼
                LOGITS
                  │
                  │
             + TARGET
                  │
                  ▼
              LOSS
                  │
                  ▼
            BACKPROPAGATION
                  │
                  ▼
              GRADIENTS
                  │
                  ▼
               ADAMW
                  │
                  ▼
             NEW WEIGHTS
```

তারপর:

```text
NEW WEIGHTS
    ↓
Next Batch
```

আবার repeat।

---

# 69. Training vs Inference

### Training

```text
Input
 ↓
GPT
 ↓
Loss
 ↓
Backward
 ↓
Update
```

### Inference

```text
Input
 ↓
GPT
 ↓
Logits
 ↓
Sampling
 ↓
Next Token
```

Inference-এ:

```text
❌ backward
❌ optimizer update
```

---

# 70. Training vs Generation

Training:

```text
"I love AI"

Predict:
love
AI
<EOS>
```

এক sequence-এর সব positions parallelভাবে train করা যায়।

Generation:

```text
"I"
 ↓
"I love"
 ↓
"I love AI"
 ↓
"I love AI because"
```

এখানে autoregressive loop চলে।

---

# 71. কেন Training Faster Than Generation?

Training:

```text
Many positions
 ↓
Parallel
```

Generation:

```text
Token
 ↓
Token
 ↓
Token
 ↓
Token
```

Sequential dependency থাকার কারণে generation inherently autoregressive।

KV caching generation-কে significantly more efficient করতে পারে।

---

# 72. AI Writing Platform-এর ক্ষেত্রে

তোমার future AI writing assistant-এর জন্য এই knowledge খুব গুরুত্বপূর্ণ।

Potential architecture:

```text
USER TEXT
    │
    ▼
TOKENIZER
    │
    ▼
GPT / LLM
    │
    ├── Analyze
    │
    ├── Rewrite
    │
    ├── Summarize
    │
    └── Generate
```

কিন্তু নিজের GPT from scratch train করার আগে সাধারণত:

```text
Pretrained LLM
      ↓
Fine-tuning / Adaptation
      ↓
Your Writing Task
```

approach অনেক বেশি practical।

---

# 73. From-Scratch GPT vs Fine-Tuning

### From Scratch

```text
Random weights
 ↓
Huge dataset
 ↓
Huge compute
 ↓
Pretraining
```

Cost:

```text
Very high
```

### Fine-Tuning

```text
Pretrained model
 ↓
Your dataset
 ↓
Fine-tuning
```

Cost:

```text
Much lower
```

Learning purpose-এ ছোট GPT from scratch বানানো excellent।

Production system-এর জন্য pretrained/open models বা APIs সাধারণত বেশি practical।

---

# 74. তোমার Learning Project-এর জন্য Recommended Path

তোমার ক্ষেত্রে:

```text
Step 1
Small GPT from scratch
```

তারপর:

```text
Step 2
Tokenizer বুঝবে
```

তারপর:

```text
Step 3
Pretrained Transformer
```

তারপর:

```text
Step 4
Fine-tuning
```

তারপর:

```text
Step 5
Instruction tuning
```

তারপর:

```text
Step 6
AI Writing Assistant
```

---

# 75. Common Training Mistakes

### Mistake 1

Target shift ভুল করা।

```text
Input ≠ Target
```

### Mistake 2

Causal mask না দেওয়া।

```text
Future leakage
```

### Mistake 3

Padding loss ignore না করা।

### Mistake 4

Validation না করা।

### Mistake 5

Learning rate খুব high করা।

### Mistake 6

Gradient clipping দরকার হলেও ব্যবহার না করা।

### Mistake 7

Train/eval mode ভুল করা।

```python
model.train()
model.eval()
```

### Mistake 8

Checkpoint না রাখা।

---

# 76. Debugging Checklist

Training শুরু করার আগে:

```text
☑ Tokenizer works
☑ Token IDs valid
☑ Vocabulary size correct
☑ Input shape correct
☑ Target shape correct
☑ Target shifted correctly
☑ Causal mask correct
☑ Padding handled
☑ Logits shape correct
☑ Loss shape correct
☑ Loss decreases
☑ Validation works
☑ Checkpoint works
```

---

# 77. Most Important Tensor Shapes

ধরি:

```text
B = 8
L = 128
D = 256
V = 10000
```

### Input

```text
(B,L)
=
(8,128)
```

### Embedding

```text
(B,L,D)
=
(8,128,256)
```

### Transformer output

```text
(8,128,256)
```

### LM Head

```text
(8,128,10000)
```

### Target

```text
(8,128)
```

### Flatten for loss

```text
Logits:
(1024,10000)

Target:
(1024)
```

কারণ:

$$
8\times128=1024
$$

---

# 78. Full GPT Training Mental Model

```text
                         TEXT DATA
                             │
                             ▼
                       DATA CLEANING
                             │
                             ▼
                         TOKENIZER
                             │
                             ▼
                         TOKEN IDs
                             │
                             ▼
                    TRAINING SEQUENCES
                             │
                             ▼
                       INPUT / TARGET
                             │
                             ▼
                         EMBEDDING
                             │
                             ▼
                    POSITION INFORMATION
                             │
                             ▼
                  ┌─────────────────────┐
                  │      GPT BLOCK      │
                  │                     │
                  │    LayerNorm        │
                  │        ↓            │
                  │ Causal Self-Attn    │
                  │        ↓            │
                  │    Residual         │
                  │        ↓            │
                  │    LayerNorm        │
                  │        ↓            │
                  │     MLP/FFN         │
                  │        ↓            │
                  │    Residual         │
                  └─────────┬───────────┘
                            │
                       Repeat N times
                            │
                            ▼
                       Final LayerNorm
                            │
                            ▼
                          LM Head
                            │
                            ▼
                          Logits
                            │
                     +      │
                     │      ▼
                     │    TARGET
                     │      │
                     └──────┤
                            ▼
                     Cross Entropy
                            │
                            ▼
                     Backpropagation
                            │
                            ▼
                         Gradients
                            │
                            ▼
                          AdamW
                            │
                            ▼
                      Updated Weights
                            │
                            ▼
                        Next Batch
```

---

# 79. Interview Questions

### Q1. What is GPT training objective?

Next-token prediction using autoregressive language modeling.

### Q2. Why do we shift target tokens?

কারণ model-এর input-এর প্রতিটি position থেকে পরবর্তী token predict করতে হয়।

### Q3. Why is causal masking required?

Future-token information leakage prevent করার জন্য।

### Q4. What is cross-entropy loss?

Predicted probability distribution এবং true target token-এর মধ্যে classification loss।

### Q5. What does backpropagation do?

Loss-এর respect-এ model parameters-এর gradients calculate করে।

### Q6. What does optimizer do?

Gradients ব্যবহার করে model parameters update করে।

### Q7. Why AdamW?

Adaptive optimization এবং decoupled weight decay-এর কারণে Transformer training-এ widely used।

### Q8. What is validation loss?

Unseen validation data-তে model-এর language-modeling loss।

### Q9. What is overfitting?

Training data-তে performance ভালো হলেও unseen data-তে performance খারাপ হওয়া।

### Q10. What is perplexity?

Language-model uncertainty/predictive performance-এর একটি metric, সাধারণত exponentiated average negative log-likelihood হিসেবে প্রকাশ করা হয়।

### Q11. Training এবং inference-এর প্রধান পার্থক্য?

Training-এ loss + backpropagation + parameter update থাকে; inference-এ সাধারণত parameter update থাকে না।

### Q12. Why is generation slower than training?

Generation autoregressive এবং token-by-token sequential dependency-এর কারণে।

---

# 80. Practice Tasks

## Beginner

নিজে explain করো:

```text
Token
 ↓
Embedding
 ↓
GPT
 ↓
Logits
 ↓
Loss
 ↓
Backpropagation
 ↓
Optimizer
```

---

## Intermediate

নিজে তৈরি করো:

```text
Text:
I love Python programming
```

তারপর:

```text
Input
Target
```

তৈরি করো।

---

## Advanced

PyTorch-এ:

```text
vocab_size = 1000
seq_len = 32
d_model = 128
heads = 8
layers = 4
```

দিয়ে mini GPT train করো।

---

## Expert Practice

নিজে implement করো:

```text
1. Dataset
2. Token IDs
3. Input/target shifting
4. Causal mask
5. GPT model
6. Cross entropy
7. AdamW
8. Training loop
9. Validation loop
10. Checkpoint
11. Text generation
```

---

# 81. M02.30 Completion Checklist

```text
☑ GPT training objective
☑ Raw text
☑ Tokenization
☑ Token IDs
☑ Training sequence
☑ Sequence length
☑ Batch
☑ Input/target
☑ Target shifting
☑ Next-token prediction
☑ Causal masking
☑ Padding
☑ Attention mask
☑ Loss mask
☑ Embedding
☑ Transformer blocks
☑ LM Head
☑ Logits
☑ Softmax concept
☑ Cross-Entropy
☑ Forward pass
☑ Backpropagation
☑ Gradient
☑ Optimizer
☑ AdamW
☑ Learning rate
☑ Warmup
☑ Scheduler
☑ Gradient clipping
☑ Epoch
☑ Step
☑ Training loop
☑ Validation
☑ Validation loss
☑ Overfitting
☑ Dropout
☑ Checkpoint
☑ Mixed precision
☑ Gradient accumulation
☑ Data quality
☑ Data leakage
☑ Data packing
☑ Perplexity
☑ Pretraining
☑ Fine-tuning
☑ Instruction tuning
☑ Training vs inference
☑ Training vs generation
☑ PyTorch implementation
☑ Tensor shapes
☑ AI writing platform connection
```

---

## 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ ১০টি বিষয়

```text
1. GPT = Next Token Prediction
2. Input → Target shifted by one token
3. Causal Mask → Future tokens blocked
4. Embedding → Token IDs → vectors
5. Transformer → contextual representation
6. LM Head → vocabulary logits
7. Cross-Entropy → prediction error
8. Backpropagation → gradients
9. AdamW → weight update
10. Repeat → model learns
```

Final mental model:

```text
              GPT TRAINING

                  TEXT
                   ↓
                TOKENIZE
                   ↓
                TOKEN IDs
                   ↓
              INPUT/TARGET
                   ↓
                GPT MODEL
                   ↓
             CAUSAL ATTENTION
                   ↓
                 LOGITS
                   ↓
              CROSS-ENTROPY
                   ↓
                  LOSS
                   ↓
            BACKPROPAGATION
                   ↓
               GRADIENTS
                   ↓
                 ADAMW
                   ↓
             UPDATE WEIGHTS
                   ↓
                NEXT BATCH
                   ↓
                 REPEAT
```

**M02.30 complete.**


---
# M02.31 — GPT Text Generation & Decoding Deep Dive

M02.30-এ আমরা শিখেছি **GPT কীভাবে train হয়**। এখন খুব গুরুত্বপূর্ণ next step:

> **Trained GPT কীভাবে নতুন text generate করে?**

এখানে আমরা শুধু `generate()` function ব্যবহার করব না—ভেতরে **token-by-token generation, logits, temperature, greedy decoding, top-k, top-p, repetition penalty, EOS, context window, KV cache**—সব বুঝব।

---

# 1. Text Generation কী?

GPT training-এ:

```text
Previous Tokens
      ↓
Predict Next Token
```

Generation-এ একই process repeatedly চালানো হয়।

Example:

```text
Prompt:
I love

Step 1:
I love → Python

Step 2:
I love Python → because

Step 3:
I love Python because → it

Step 4:
I love Python because it → is
```

অর্থাৎ:

```text
Prompt
  ↓
Predict next token
  ↓
Append token
  ↓
Predict next token
  ↓
Append token
  ↓
Repeat
```

---

# 2. GPT Generation-এর মূল Formula

GPT model:

$$
P(x_t|x_1,x_2,\dots,x_{t-1})
$$

অর্থাৎ বর্তমান token-এর probability নির্ভর করে আগের tokenগুলোর উপর।

সম্পূর্ণ sequence:

$$
P(x_1,x_2,\dots,x_T)
=
\prod_{t=1}^{T}
P(x_t|x_{<t})
$$

এটাই autoregressive generation-এর mathematical foundation।

---

# 3. Training বনাম Generation

### Training

```text
Input
 ↓
Model
 ↓
Logits
 ↓
Loss
 ↓
Backpropagation
 ↓
Weight Update
```

### Generation

```text
Prompt
 ↓
Model
 ↓
Logits
 ↓
Decode/Sample
 ↓
Next Token
 ↓
Append
 ↓
Repeat
```

Generation-এ:

```text
❌ Loss optimization
❌ Backpropagation
❌ Weight update
```

---

# 4. Generation-এর প্রথম Step

ধরি:

```text
Prompt:
I love
```

Tokenizer:

```text
I     → 10
love  → 25
```

Input:

```python
input_ids = [10, 25]
```

Model:

```text
[10,25]
   ↓
GPT
   ↓
Logits
```

Output:

```text
Vocabulary
   ↓
Probability distribution
```

---

# 5. Logits কী?

ধরি vocabulary:

```text
Python
AI
music
football
programming
...
```

Model logits:

```text
Python       4.5
AI           3.7
music        1.2
football     0.8
programming  4.0
```

Logits হলো raw scores।

তারপর probability:

```text
Python       0.40
programming  0.30
AI           0.20
music        0.06
football     0.04
```

---

# 6. Next Token নির্বাচন

এখন প্রশ্ন:

> কোন token নেওয়া হবে?

এখানেই **decoding strategy** আসে।

Popular strategies:

```text
1. Greedy Decoding
2. Random Sampling
3. Temperature
4. Top-K Sampling
5. Top-P / Nucleus Sampling
6. Repetition Penalty
7. Beam Search
```

---

# 7. Greedy Decoding

সবচেয়ে সহজ strategy।

যে token-এর probability সবচেয়ে বেশি:

```text
Take argmax
```

Example:

```text
Python       0.40
programming  0.30
AI           0.20
music        0.06
football     0.04
```

Choose:

```text
Python
```

কারণ:

$$
Python = \arg\max P(token)
$$

---

# 8. Greedy Generation

```python
next_token = torch.argmax(
    logits[:, -1, :],
    dim=-1
)
```

তারপর:

```python
tokens = torch.cat(
    [tokens, next_token.unsqueeze(1)],
    dim=1
)
```

Repeat।

---

# 9. Greedy-এর সমস্যা

ধরি:

```text
Python = 0.35
AI = 0.34
coding = 0.20
...
```

Greedy সবসময়:

```text
Python
```

নেবে।

কিন্তু অনেক সময় slightly lower-probability token sequence overall অনেক better হতে পারে।

তাই generation-এর জন্য sampling গুরুত্বপূর্ণ।

---

# 10. Random Sampling

Probability distribution থেকে randomভাবে token নির্বাচন করা যায়।

Example:

```text
Python       0.40
AI           0.30
coding       0.20
music        0.10
```

Sampling করলে:

```text
Python → 40%
AI → 30%
coding → 20%
music → 10%
```

একবার:

```text
Python
```

আসতে পারে।

অন্যবার:

```text
AI
```

আসতে পারে।

---

# 11. Sampling-এর সুবিধা

এতে generation:

```text
Less deterministic
More diverse
```

হতে পারে।

Creative writing-এ sampling useful।

---

# 12. Temperature

Temperature controls:

> Probability distribution কতটা sharp বা flat হবে।

Formula:

$$
P_i =
softmax
\left(
\frac{z_i}{T}
\right)
$$

যেখানে:

* `z` = logits
* `T` = temperature

---

# 13. Temperature = 1

```text
T = 1
```

Original logits distribution-এর মতো থাকে।

---

# 14. Temperature < 1

Example:

```text
T = 0.5
```

Distribution বেশি sharp হবে।

```text
Most likely token
      ↑
More dominant
```

Result:

```text
More predictable
Less diverse
```

---

# 15. Temperature > 1

Example:

```text
T = 1.5
```

Distribution flatter হবে।

```text
Less likely tokens
      ↑
More probability
```

Result:

```text
More diverse
More random
```

কিন্তু খুব বেশি temperature হলে output incoherent হতে পারে।

---

# 16. Temperature Example

Original:

```text
Python       0.50
AI           0.30
coding       0.15
music        0.05
```

Low temperature:

```text
Python       ↑↑
AI           ↓
coding       ↓
music        ↓
```

High temperature:

```text
Python       ↓
AI           ↑
coding       ↑
music        ↑
```

---

# 17. PyTorch Temperature

```python
logits = logits / temperature

probs = torch.softmax(
    logits,
    dim=-1
)
```

তারপর:

```python
next_token = torch.multinomial(
    probs,
    num_samples=1
)
```

---

# 18. Top-K Sampling

Vocabulary অনেক বড় হতে পারে।

ধরি:

```text
Vocabulary = 50,000
```

আমরা সব token থেকে sample না করে শুধু top `K` token রাখি।

যদি:

```text
K = 5
```

তাহলে:

```text
Top 5 tokens
      ↓
Sampling
```

---

# 19. Top-K Example

ধরি:

```text
Python       0.35
AI           0.25
coding       0.18
program      0.10
model        0.06
music        0.03
football     0.02
...
```

`top_k = 5`

তাহলে:

```text
Python
AI
coding
program
model
```

এই পাঁচটির মধ্যেই sampling হবে।

---

# 20. Top-K কেন ব্যবহার করব?

Very unlikely tokens বাদ দিতে।

```text
Vocabulary
   ↓
Top K
   ↓
Reasonable candidates
   ↓
Sampling
```

এতে:

```text
Randomness ↓
Quality ↑
```

সাধারণত, যদিও exact behavior task/model-এর উপর নির্ভর করে।

---

# 21. Top-K Code

```python
k = 50

values, indices = torch.topk(
    logits,
    k
)
```

তারপর অন্য logits:

```python
-∞
```

করে দেওয়া যায়।

```python
filtered_logits = torch.full_like(
    logits,
    float("-inf")
)

filtered_logits.scatter_(
    1,
    indices,
    values
)
```

তারপর:

```python
probs = torch.softmax(
    filtered_logits,
    dim=-1
)
```

---

# 22. Top-P / Nucleus Sampling

Top-K fixed number token রাখে।

Top-P probability mass অনুযায়ী token রাখে।

Example:

```text
Python      0.40
AI          0.25
coding      0.15
program     0.10
music       0.05
football    0.03
other       0.02
```

ধরি:

```text
top_p = 0.80
```

Cumulative:

```text
Python               0.40
Python + AI          0.65
+ coding             0.80
```

তাই:

```text
Python
AI
coding
```

candidate হবে।

---

# 23. Top-K vs Top-P

### Top-K

```text
Always K tokens
```

Example:

```text
K = 50
```

### Top-P

```text
Dynamic number of tokens
```

Example:

```text
P = 0.9
```

কখনও:

```text
10 tokens
```

কখনও:

```text
100 tokens
```

দরকার হতে পারে।

---

# 24. Top-P Code

Conceptually:

```python
sorted_logits, sorted_indices = torch.sort(
    logits,
    descending=True
)

sorted_probs = torch.softmax(
    sorted_logits,
    dim=-1
)

cumulative_probs = torch.cumsum(
    sorted_probs,
    dim=-1
)
```

তারপর cumulative probability threshold-এর বাইরে token remove করা হয়।

---

# 25. Top-K + Top-P

Modern text generation-এ দুটো একসাথে ব্যবহার করা যেতে পারে:

```text
Logits
 ↓
Temperature
 ↓
Top-K
 ↓
Top-P
 ↓
Sampling
 ↓
Next Token
```

তবে exact ordering/implementation library ও generation setup-এর উপর নির্ভর করতে পারে।

---

# 26. Repetition Problem

GPT কখনও একই শব্দ বারবার generate করতে পারে।

Example:

```text
AI is useful because AI is useful because AI is useful...
```

এটাকে repetition বলা হয়।

---

# 27. Repetition Penalty

Already generated token-এর probability কমানো যায়।

Concept:

```text
Token already used
       ↓
Penalty
       ↓
Probability ↓
```

এতে repetition কমানোর চেষ্টা করা হয়।

তবে খুব aggressive penalty দিলে text unnatural হতে পারে।

---

# 28. Frequency Penalty বনাম Repetition Penalty

Conceptually:

### Frequency penalty

একটি token যত বেশি এসেছে:

```text
More occurrences
      ↓
More penalty
```

### Repetition penalty

Previously generated tokens-এর logits/probability modify করে repetition discourage করা হয়।

Different libraries different implementations ব্যবহার করতে পারে।

---

# 29. EOS Token

Generation কখন stop করবে?

এজন্য:

```text
<EOS>
```

অথবা model-specific end-of-sequence token থাকে।

Example:

```text
I love Python <EOS>
```

Model `<EOS>` generate করলে:

```text
STOP
```

---

# 30. Maximum New Tokens

EOS না এলেও maximum length সেট করা যায়।

```python
max_new_tokens = 100
```

মানে:

```text
At most 100 new tokens
```

---

# 31. Context Window

GPT একবারে সীমিত সংখ্যক tokens process করতে পারে।

ধরি:

```text
Context Window = 4096
```

তাহলে input + generated context-এর effective token budget এই limit-এর মধ্যে থাকতে হবে।

Modern models-এর context window অনেক বড় হতে পারে, কিন্তু model-specific।

---

# 32. Long Generation

ধরি:

```text
Prompt = 3000 tokens
```

এবং:

```text
max context = 4096
```

তাহলে generation-এর জন্য available room সীমিত।

Concept:

```text
Context Window
┌─────────────────────────────┐
│ Prompt + Generated Tokens   │
└─────────────────────────────┘
```

---

# 33. Sliding Window Concept

Long text handle করার জন্য context-এর পুরোনো অংশ বাদ দিয়ে নতুন অংশ রাখা যেতে পারে।

```text
Old Context
    ↓
Drop
    ↓
Recent Context
    +
New Token
```

এটা model architecture/serving strategy অনুযায়ী ভিন্নভাবে implement করা হয়।

---

# 34. KV Cache

Generation-এর সবচেয়ে গুরুত্বপূর্ণ optimization-এর একটি:

**KV Cache**

আগে আমরা self-attention শিখেছি:

```text
Q
K
V
```

প্রতিটি generation step-এ পুরোনো tokens-এর K/V আবার calculate না করে cache করা যায়।

---

# 35. Without KV Cache

ধরি:

```text
Step 1:
Token 1

Step 2:
Token 1 + Token 2

Step 3:
Token 1 + Token 2 + Token 3
```

প্রতিবার পুরো sequence process করলে repeated computation হয়।

---

# 36. With KV Cache

পুরোনো:

```text
K₁,V₁
K₂,V₂
K₃,V₃
```

cache-এ থাকে।

নতুন token এলে:

```text
New Q
+
Cached K/V
```

ব্যবহার করা হয়।

---

# 37. KV Cache Mental Model

```text
                Previous Tokens
                      │
                      ▼
                  K / V Cache
                      │
                      │
New Token ────────────┤
   │                  │
   ▼                  ▼
   Q            Cached K/V
   │                  │
   └────────┬─────────┘
            ▼
        Attention
            │
            ▼
       Next Token
```

---

# 38. কেন KV Cache গুরুত্বপূর্ণ?

Generation:

```text
Without cache
→ repeated computation

With cache
→ reuse previous K/V
```

তাই autoregressive decoding অনেক বেশি efficient হয়।

Tradeoff:

```text
Speed ↑
Memory usage ↑
```

---

# 39. Greedy Generation Code

Educational implementation:

```python
def generate_greedy(
    model,
    tokens,
    max_new_tokens
):

    model.eval()

    for _ in range(max_new_tokens):

        with torch.no_grad():

            logits = model(tokens)

        next_token = torch.argmax(
            logits[:, -1, :],
            dim=-1,
            keepdim=True
        )

        tokens = torch.cat(
            [tokens, next_token],
            dim=1
        )

    return tokens
```

---

# 40. Sampling Generation

```python
def generate_sample(
    model,
    tokens,
    max_new_tokens,
    temperature=1.0
):

    model.eval()

    for _ in range(max_new_tokens):

        with torch.no_grad():

            logits = model(tokens)

        logits = logits[:, -1, :]

        logits = logits / temperature

        probs = torch.softmax(
            logits,
            dim=-1
        )

        next_token = torch.multinomial(
            probs,
            num_samples=1
        )

        tokens = torch.cat(
            [tokens, next_token],
            dim=1
        )

    return tokens
```

---

# 41. Production Generation Pipeline

একটি practical conceptual pipeline:

```text
Prompt
  ↓
Tokenizer
  ↓
Input IDs
  ↓
GPT
  ↓
Last-token logits
  ↓
Temperature
  ↓
Top-K / Top-P
  ↓
Sampling
  ↓
Next Token
  ↓
EOS?
 ├── YES → STOP
 └── NO
      ↓
   Append
      ↓
   GPT again
```

---

# 42. Beam Search

Beam search অন্য ধরনের decoding strategy।

একটি sequence রাখার পরিবর্তে:

```text
1 candidate
```

এর বদলে:

```text
K candidates
```

রাখে।

Example:

```text
Beam = 3

Candidate 1
Candidate 2
Candidate 3
```

প্রতিটি step-এ best candidates expand করা হয়।

---

# 43. Beam Search কোথায় বেশি useful?

Beam search historically:

```text
Machine Translation
Text Summarization
Seq2Seq generation
```

এর মতো tasks-এ খুব গুরুত্বপূর্ণ ছিল।

Open-ended GPT-style creative generation-এ সাধারণত sampling-based decoding বেশি common, কারণ beam search অনেক সময় output-কে overly deterministic বা generic করতে পারে।

---

# 44. Greedy vs Sampling vs Beam Search

| Method      |   Diversity | Deterministic | Main Idea                    |
| ----------- | ----------: | ------------: | ---------------------------- |
| Greedy      |         Low |           Yes | Highest probability          |
| Sampling    |        High |            No | Probability-based            |
| Top-K       | Medium/High |            No | Sample from K                |
| Top-P       | Medium/High |            No | Sample from probability mass |
| Beam Search |  Low/Medium |       Usually | Keep best sequences          |

---

# 45. Temperature + Top-P

একটি common conceptual configuration:

```text
temperature = 0.7
top_p = 0.9
```

এর মানে:

```text
Temperature
→ distribution control

Top-P
→ candidate filtering
```

Exact best settings সব model/task-এর জন্য একই নয়।

---

# 46. Deterministic Generation

যদি:

```text
temperature = 0
```

ব্যবহার করা হয়, many generation APIs effectively greedy/argmax-like behavior দেয়।

তবে exact implementation framework-specific হতে পারে।

Production code-এ সাধারণত explicit greedy mode ব্যবহার করা clearer:

```python
next_token = torch.argmax(...)
```

---

# 47. Random Seed

Sampling reproducible করতে seed set করা যায়।

```python
torch.manual_seed(42)
```

তারপর একই model/input/settings-এ randomness অনেক ক্ষেত্রে reproducible হবে।

Distributed/GPU environment-এ exact reproducibility আরও complicated হতে পারে।

---

# 48. Generation Quality

শুধু:

```text
Probability ↑
```

হলেই human-quality output নিশ্চিত নয়।

Generation quality depend করতে পারে:

```text
Model quality
Training data
Prompt
Context
Temperature
Top-P
Top-K
Repetition control
Context length
Decoding strategy
```

---

# 49. AI Writing Assistant-এ Generation

তোমার future writing platform-এ user input:

```text
"I want to improve this paragraph."
```

System:

```text
User Text
 ↓
Prompt Builder
 ↓
LLM
 ↓
Generation
 ↓
Post-processing
 ↓
Result
```

Different writing modes:

```text
Improve clarity
Improve grammar
Change tone
Make concise
Make professional
Rewrite for readability
```

এখানে goal হওয়া উচিত **writing quality and meaning preservation**, detection bypass নয়।

---

# 50. Rewrite Generation

Example:

```text
Input:
The system is very useful because it helps users
to manage their information easily.
```

Possible improved output:

```text
The system helps users manage their information
more efficiently.
```

Generation-এর সময় model:

```text
Token 1
 ↓
Token 2
 ↓
Token 3
 ↓
...
```

generate করে।

---

# 51. Meaning Preservation

Writing assistant-এ শুধু fluent text যথেষ্ট নয়।

Need:

```text
Original Meaning
       ↓
Preserved
       ↓
Improved Wording
```

তাই system architecture-এ একটি semantic checking layer রাখা যেতে পারে:

```text
Original
   │
   ├──→ Rewrite Model
   │
   └──→ Semantic Representation
              │
              ▼
        Meaning Check
              │
              ▼
         Final Output
```

---

# 52. Generation + Evaluation

Production writing system-এ:

```text
Generated Text
      ↓
Grammar Check
      ↓
Semantic Similarity
      ↓
Quality Check
      ↓
Safety Check
      ↓
Final Text
```

একটি single score-এর উপর নির্ভর না করে multiple signals ব্যবহার করা ভালো।

---

# 53. Generation Failure Cases

### Repetition

```text
AI AI AI AI...
```

### Hallucination

Model confident-sounding কিন্তু unsupported information generate করতে পারে।

### Incoherence

Sentence-to-sentence logical consistency কমে যেতে পারে।

### Context drift

Long generation-এ original instruction থেকে দূরে যেতে পারে।

### Meaning drift

Rewrite করতে গিয়ে original meaning পরিবর্তন হতে পারে।

---

# 54. Generation Debugging

যদি output খারাপ হয়:

```text
Check:
```

```text
☑ Tokenizer
☑ Input IDs
☑ Context length
☑ Model.eval()
☑ Temperature
☑ Top-K
☑ Top-P
☑ EOS
☑ Repetition control
☑ Prompt
☑ Model quality
```

---

# 55. Important Tensor Shape

ধরি:

```text
B = 1
L = 50
V = 10,000
```

Model output:

```text
(B,L,V)
=
(1,50,10000)
```

Generation-এর জন্য আমরা শুধু শেষ position নিই:

```python
logits[:, -1, :]
```

Shape:

```text
(1,10000)
```

তারপর:

```text
10000 vocabulary tokens
```

এর মধ্যে next token select করি।

---

# 56. কেন শুধু শেষ Position?

কারণ generation-এর current step-এ আমাদের দরকার:

$$
P(x_{t+1}|x_{\leq t})
$$

তাই শেষ input position-এর logits next token distribution দেয়।

```text
Prompt
 ↓
GPT
 ↓
Last position
 ↓
Next token probability
```

---

# 57. Complete Generation Algorithm

```text
1. Take prompt
2. Tokenize prompt
3. Convert to token IDs
4. Feed IDs into GPT
5. Get logits
6. Select last-position logits
7. Apply temperature
8. Apply Top-K/Top-P if desired
9. Convert to probabilities
10. Select/sample next token
11. Append token
12. Check EOS
13. Check max length
14. Repeat
15. Decode token IDs → text
```

---

# 58. Final Generation Pseudocode

```python
tokens = tokenize(prompt)

for step in range(max_new_tokens):

    logits = model(tokens)

    logits = logits[:, -1, :]

    logits = logits / temperature

    logits = apply_top_k(logits)

    logits = apply_top_p(logits)

    probs = softmax(logits)

    next_token = sample(probs)

    tokens = append(
        tokens,
        next_token
    )

    if next_token == EOS:
        break

text = decode(tokens)
```

এটাই GPT generation-এর core algorithm।

---

# 59. সবচেয়ে গুরুত্বপূর্ণ Concept Map

```text
                 GPT GENERATION
                       │
                       ▼
                    PROMPT
                       │
                       ▼
                   TOKENIZER
                       │
                       ▼
                   TOKEN IDs
                       │
                       ▼
                      GPT
                       │
                       ▼
                     LOGITS
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
        Temperature   Top-K     Top-P
             │         │         │
             └─────────┼─────────┘
                       ▼
                    Sampling
                       │
                       ▼
                  NEXT TOKEN
                       │
                       ▼
                    Append
                       │
                       ▼
                    EOS?
                   /     \
                 Yes      No
                  │        │
                STOP       └──→ GPT
```

---

# 60. M02.31 Completion Checklist

```text
☑ Text generation
☑ Autoregressive generation
☑ Conditional probability
☑ Sequence probability
☑ Logits
☑ Softmax
☑ Next-token prediction
☑ Greedy decoding
☑ Random sampling
☑ Temperature
☑ Top-K
☑ Top-P / Nucleus Sampling
☑ Repetition problem
☑ Repetition penalty
☑ Frequency penalty
☑ EOS token
☑ Max new tokens
☑ Context window
☑ Long-context issue
☑ Sliding-window concept
☑ KV Cache
☑ Beam Search
☑ Greedy vs Sampling
☑ Deterministic generation
☑ Random seed
☑ Generation quality
☑ Hallucination
☑ Meaning drift
☑ Generation debugging
☑ Tensor shapes
☑ PyTorch implementation
☑ AI Writing Assistant connection
```

---

## 🧠 আজকের ৮টি বিষয় অবশ্যই মনে রাখবে

```text
1. GPT generates one token at a time.

2. Last-position logits give the next-token distribution.

3. Greedy = highest probability token.

4. Sampling = probability distribution থেকে token নির্বাচন।

5. Temperature controls randomness/sharpness.

6. Top-K keeps a fixed number of candidate tokens.

7. Top-P keeps enough tokens to cover a probability mass.

8. KV Cache avoids recomputing old K/V during generation.
```

### Final Mental Model

```text
TRAINED GPT
    │
    ▼
  PROMPT
    │
    ▼
TOKENIZER
    │
    ▼
TOKEN IDs
    │
    ▼
   GPT
    │
    ▼
 LOGITS
    │
    ▼
DECODING
    │
    ├── Greedy
    ├── Temperature
    ├── Top-K
    ├── Top-P
    └── Sampling
    │
    ▼
NEXT TOKEN
    │
    ▼
APPEND
    │
    ▼
REPEAT
    │
    ▼
   EOS
    │
    ▼
FINAL TEXT
```

**M02.31 complete.**


---
# M02.32 — BERT vs GPT vs T5 + Transformer Family Deep Dive

M02.29–M02.31 পর্যন্ত তুমি GPT-এর **architecture → training → generation** শিখেছ।

এখন next important step হলো Transformer-based model family-গুলোকে গভীরভাবে বোঝা:

```text
Transformer
   │
   ├── Encoder-only
   │      └── BERT
   │
   ├── Decoder-only
   │      └── GPT
   │
   └── Encoder-Decoder
          └── T5
```

এই lesson-এর লক্ষ্য হলো শুধু “BERT encoder, GPT decoder” মুখস্থ করা নয়—**কোন architecture কোন problem-এর জন্য, কীভাবে input/output process করে, কীভাবে train হয় এবং তোমার AI writing platform-এ কখন কোনটা ব্যবহার করবে** সেটা বোঝা।

---

# 1. Transformer Family

Original Transformer architecture:

```text
                 Transformer
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
       Encoder     Decoder    Encoder-Decoder
          ↓           ↓           ↓
        BERT         GPT          T5
```

তিনটি major architecture:

| Architecture    | Example | Main Strength                 |
| --------------- | ------- | ----------------------------- |
| Encoder-only    | BERT    | Understanding                 |
| Decoder-only    | GPT     | Generation                    |
| Encoder-Decoder | T5      | Input → Output transformation |

---

# 2. Encoder-only Model

Encoder model পুরো input sequence একসাথে দেখতে পারে।

Example:

```text
The student reads a book.
```

Encoder:

```text
The       ↔ student
 ↕           ↕
reads     ↔ book
```

প্রতিটি token context-এর অন্য token-গুলোর information ব্যবহার করতে পারে।

এটাকে সাধারণভাবে:

```text
Bidirectional Attention
```

বলা হয়।

---

# 3. BERT

BERT:

**Bidirectional Encoder Representations from Transformers**

BERT হলো:

```text
Encoder-only Transformer
```

Architecture:

```text
Text
 ↓
Tokenizer
 ↓
Token Embeddings
 +
Position Embeddings
 +
Token-Type Embeddings
 ↓
Transformer Encoder
 ↓
Contextual Representations
```

---

# 4. BERT কী জন্য ভালো?

BERT-style models understanding tasks-এর জন্য খুব effective।

যেমন:

```text
Classification
NER
Sentiment Analysis
Question Answering
Semantic Similarity
Information Extraction
Embedding / Retrieval
```

Example:

```text
Input:
"The movie was excellent."

Output:
Positive
```

---

# 5. BERT Bidirectional কেন?

ধরি:

```text
The bank is near the river.
```

`bank` শব্দের meaning বুঝতে model দুই দিকের context দেখতে পারে:

```text
The bank
    ↑
near the river
```

তাই context-rich representation তৈরি হয়।

---

# 6. BERT-এর Masked Language Modeling

BERT-এর famous pretraining objective:

**MLM — Masked Language Modeling**

Example:

```text
The cat is [MASK] on the mat.
```

Model predict করবে:

```text
sitting
```

অর্থাৎ:

```text
Input:
The cat is [MASK] on the mat.

Target:
sitting
```

---

# 7. BERT কেন GPT-এর মতো Next Token Prediction করে না?

কারণ BERT-এর goal মূলত:

```text
Understand context
```

GPT-এর goal:

```text
Generate next token
```

BERT:

```text
The cat is [MASK] on the mat.
            ↑
       Predict missing token
```

GPT:

```text
The cat is
          ↓
Predict next token
```

---

# 8. GPT

GPT:

**Generative Pre-trained Transformer**

GPT হলো:

```text
Decoder-only Transformer
```

Architecture:

```text
Prompt
 ↓
Tokenization
 ↓
Embedding
 ↓
Causal Self-Attention
 ↓
Transformer Blocks
 ↓
LM Head
 ↓
Next Token
```

---

# 9. GPT-এর Attention

GPT causal attention ব্যবহার করে।

```text
             I   love   AI

I            ✓    ✗     ✗
love         ✓    ✓     ✗
AI           ✓    ✓     ✓
```

Future token দেখতে পারে না।

---

# 10. GPT কেন Causal?

কারণ GPT:

$$
P(x_t|x_{<t})
$$

predict করে।

অর্থাৎ:

```text
Previous tokens
       ↓
Next token
```

---

# 11. GPT-এর Main Use Cases

```text
Text Generation
Conversation
Code Generation
Summarization
Rewriting
Question Answering
Translation
Creative Writing
Instruction Following
```

তোমার AI writing assistant-এর জন্য GPT-style architecture খুব গুরুত্বপূর্ণ।

---

# 12. T5

T5:

**Text-To-Text Transfer Transformer**

T5 হলো:

```text
Encoder + Decoder
```

Architecture:

```text
Input Text
    ↓
Encoder
    ↓
Context
    ↓
Decoder
    ↓
Output Text
```

T5-এর philosophy:

> প্রায় সব NLP task-কে text-to-text problem হিসেবে দেখা।

---

# 13. T5 Example

Task:

```text
Translate English to French
```

Input:

```text
translate English to French:
I love Python.
```

Output:

```text
J'aime Python.
```

---

# 14. T5 Summarization

Input:

```text
summarize:
Artificial intelligence is...
```

Output:

```text
AI is...
```

---

# 15. T5 Classification

Input:

```text
sentiment:
The movie was amazing.
```

Output:

```text
positive
```

অর্থাৎ classification-ও text generation-এর মাধ্যমে করা যায়।

---

# 16. BERT vs GPT vs T5

এটা খুব ভালোভাবে বুঝতে হবে।

| Feature               | BERT                | GPT                   | T5                                     |
| --------------------- | ------------------- | --------------------- | -------------------------------------- |
| Architecture          | Encoder-only        | Decoder-only          | Encoder-Decoder                        |
| Attention             | Bidirectional       | Causal                | Encoder bidirectional + decoder causal |
| Main objective        | MLM                 | Next-token prediction | Text-to-text                           |
| Generation            | Limited/not primary | Excellent             | Excellent                              |
| Understanding         | Excellent           | Excellent             | Excellent                              |
| Classification        | Excellent           | Possible              | Possible                               |
| NER                   | Excellent           | Possible              | Possible                               |
| Translation           | Not primary         | Possible              | Excellent                              |
| Summarization         | Possible            | Excellent             | Excellent                              |
| Open-ended generation | Not primary         | Excellent             | Good                                   |

---

# 17. Simple Mental Model

```text
BERT
"What does this text mean?"

GPT
"What comes next?"

T5
"Transform this text into another text."
```

---

# 18. Architecture Comparison

### BERT

```text
Input
 ↓
Embedding
 ↓
Encoder
 ↓
Encoder
 ↓
Encoder
 ↓
Representation
```

### GPT

```text
Input
 ↓
Embedding
 ↓
Decoder Block
 ↓
Decoder Block
 ↓
Decoder Block
 ↓
Next Token
```

### T5

```text
Input
 ↓
Encoder
 ↓
Context
 ↓
Decoder
 ↓
Output
```

---

# 19. BERT Attention vs GPT Attention

### BERT

```text
Token 1 ↔ Token 2 ↔ Token 3 ↔ Token 4
```

সবদিকে context access করতে পারে।

### GPT

```text
Token 1 → Token 2 → Token 3 → Token 4
```

Future information blocked।

---

# 20. T5 Attention

T5-এর ক্ষেত্রে:

### Encoder self-attention

```text
Full input context
```

### Decoder self-attention

```text
Causal
```

### Decoder cross-attention

```text
Decoder
   ↓
Encoder representation
```

---

# 21. T5 Q/K/V

Encoder self-attention:

```text
Q = Encoder
K = Encoder
V = Encoder
```

Decoder self-attention:

```text
Q = Decoder
K = Decoder
V = Decoder
```

Cross-attention:

```text
Q = Decoder
K = Encoder
V = Encoder
```

---

# 22. BERT Input Representation

BERT-style input traditionally combines:

```text
Token Embedding
+
Segment/Token-Type Embedding
+
Position Embedding
```

Conceptually:

$$
X = E_{token}+E_{segment}+E_{position}
$$

Example:

```text
[CLS] I love AI [SEP]
```

---

# 23. `[CLS]`

`[CLS]` = classification token।

Example:

```text
[CLS] The movie is excellent [SEP]
```

BERT-style classification-এর ক্ষেত্রে `[CLS]` representation ব্যবহার করা যেতে পারে।

---

# 24. `[SEP]`

`[SEP]` sequence boundary indicate করতে ব্যবহৃত হয়।

Example:

```text
[CLS] Sentence A [SEP] Sentence B [SEP]
```

---

# 25. `[MASK]`

MLM training-এর জন্য:

```text
I love [MASK].
```

Model missing token predict করবে।

---

# 26. GPT Special Tokens

GPT-family tokenizer/model অনুযায়ী special tokens ভিন্ন হতে পারে।

Conceptually থাকতে পারে:

```text
<BOS>
<EOS>
<PAD>
```

সব GPT model-এ একই special token naming বা behavior থাকবে—এমন নয়।

---

# 27. BERT Training

Simplified:

```text
Large Text
 ↓
Randomly mask tokens
 ↓
BERT
 ↓
Predict masked tokens
 ↓
Loss
 ↓
Backpropagation
 ↓
Weight Update
```

---

# 28. GPT Training

```text
Text
 ↓
Tokenize
 ↓
Input / Target Shift
 ↓
GPT
 ↓
Next Token Prediction
 ↓
Cross Entropy
 ↓
Backpropagation
 ↓
Weight Update
```

---

# 29. T5 Training

T5 denoising/text-to-text objective ব্যবহার করে।

Conceptually:

```text
Original:
The cat is sitting on the mat.

Corrupted input:
The cat <extra_id_0> on the mat.

Target:
<extra_id_0> is sitting
```

T5-এর exact pretraining details model/version অনুযায়ী আলাদা হতে পারে, কিন্তু মূল idea হলো corrupted text থেকে missing/spanned content reconstruct করা।

---

# 30. BERT vs GPT Training Objective

### BERT

```text
Masked Token
      ↓
Predict
```

### GPT

```text
Previous Tokens
      ↓
Next Token
```

---

# 31. BERT কেন Future দেখতে পারে?

কারণ BERT-এর goal next-token generation নয়।

তাই:

```text
I love [MASK] because it is useful.
```

`[MASK]` predict করার সময়:

```text
I love
+
because it is useful
```

দুই পাশের context ব্যবহার করতে পারে।

---

# 32. GPT কেন Future দেখতে পারে না?

GPT-এর training objective:

$$
P(x_t|x_{<t})
$$

তাই future token visible হলে training leakage হবে।

তাই:

```text
Future
 ↓
Masked
```

---

# 33. T5 কেন Encoder + Decoder ব্যবহার করে?

Input এবং output আলাদা sequence।

Example:

```text
Input:
Translate this sentence.

Output:
Translated sentence.
```

Encoder:

```text
Understand input
```

Decoder:

```text
Generate output
```

---

# 34. AI Writing Assistant-এ BERT

BERT-style encoder ব্যবহার করা যেতে পারে:

```text
User Text
 ↓
BERT Encoder
 ↓
Text Representation
```

তারপর:

```text
      Representation
            │
      ┌─────┼─────┐
      ↓     ↓     ↓
   Quality  Tone  Classification
```

---

# 35. AI Writing Assistant-এ GPT

GPT-style model:

```text
User Text
 ↓
Prompt
 ↓
GPT
 ↓
Rewrite
```

Example:

```text
Rewrite this sentence to make it clearer:

"The system is good because it can help people."
```

Output:

```text
"The system is useful because it helps people work more efficiently."
```

---

# 36. AI Writing Assistant-এ T5

T5-style:

```text
Input:
rewrite: The system is good.

Output:
The system is effective.
```

অর্থাৎ text transformation-এর জন্য natural fit।

---

# 37. কোনটা ব্যবহার করবে?

তোমার AI writing platform-এর জন্য:

### Generation

```text
GPT / decoder-only
```

### Text analysis

```text
BERT / encoder-only
```

### Text transformation

```text
T5 / encoder-decoder
```

তবে modern production systems-এ একটি architecture-ই সব কাজ করতে পারে; architecture choice task, model quality, latency, cost এবং available models-এর উপর নির্ভর করে।

---

# 38. Hybrid Architecture

একটি advanced writing platform:

```text
                USER TEXT
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
      BERT-like            GPT-like
      Analyzer             Generator
          ↓                   ↓
      Analysis             Rewrite
          │                   │
          └─────────┬─────────┘
                    ↓
             Quality Check
                    ↓
              Final Output
```

এটি একটি useful conceptual architecture।

---

# 39. Semantic Similarity

BERT-like encoder ব্যবহার করে:

```text
Original
   ↓
Embedding
```

এবং:

```text
Rewrite
   ↓
Embedding
```

তারপর:

```text
Cosine Similarity
```

দিয়ে semantic similarity estimate করা যায়।

Example:

```text
Original:
I like programming.

Rewrite:
I enjoy coding.
```

Semantic similarity high হতে পারে।

কিন্তু similarity score-কে absolute proof হিসেবে ধরা যাবে না।

---

# 40. Rewrite Quality Pipeline

তোমার project-এর জন্য:

```text
Original Text
      │
      ├──────────────┐
      ↓              ↓
   Generator      Analyzer
      ↓              ↓
   Rewrite       Embedding
      │              │
      └──────┬───────┘
             ↓
      Meaning Check
             ↓
       Quality Score
             ↓
       Final Rewrite
```

---

# 41. Important Difference: Representation vs Generation

BERT:

```text
Text
 ↓
Representation
```

GPT:

```text
Text
 ↓
Representation
 ↓
Next Token
 ↓
Text
```

T5:

```text
Input Text
 ↓
Representation
 ↓
Output Text
```

---

# 42. Parameter Sharing

Transformer family-তে একই layer-এর parameters sequence positions-এর মধ্যে shared থাকে।

তবে:

```text
BERT parameters
≠
GPT parameters
≠
T5 parameters
```

Architecture একই family-এর হলেও trained weights আলাদা।

---

# 43. Pretraining → Fine-Tuning

BERT:

```text
Pretraining
 ↓
Fine-tuning
 ↓
NER
```

GPT:

```text
Pretraining
 ↓
Instruction tuning
 ↓
Generation
```

T5:

```text
Pretraining
 ↓
Fine-tuning
 ↓
Specific text-to-text task
```

---

# 44. Transfer Learning

এখানে একটি গুরুত্বপূর্ণ ML concept:

**Transfer Learning**

একটি model আগে বড় dataset-এ general knowledge শেখে।

তারপর:

```text
Pretrained Model
       ↓
Task-specific Training
       ↓
Specialized Model
```

এতে scratch থেকে train করার প্রয়োজন কমে।

---

# 45. Encoder-only vs Decoder-only vs Encoder-Decoder

```text
                  TRANSFORMER
                      │
      ┌───────────────┼────────────────┐
      ↓               ↓                ↓
   ENCODER         DECODER       ENCODER-DECODER
      │               │                │
      ↓               ↓                ↓
    BERT             GPT              T5
      │               │                │
 Understand         Generate        Transform
```

এই diagram অবশ্যই মনে রাখবে।

---

# 46. Sequence-to-Sequence

T5-এর মতো model-এ:

```text
Input Sequence
      ↓
Encoder
      ↓
Context
      ↓
Decoder
      ↓
Output Sequence
```

একে:

```text
Seq2Seq
```

বলা হয়।

---

# 47. GPT কি Seq2Seq?

GPT technically classic encoder-decoder Seq2Seq architecture নয়।

এটি:

```text
Decoder-only
```

তবে causal language modeling-এর মাধ্যমে prompt থেকে continuation generate করে।

---

# 48. BERT কি Generative Model?

Standard BERT architecture generation-এর জন্য designed নয়।

BERT-এর strength:

```text
Understanding
Representation
Classification
Token-level analysis
```

---

# 49. T5 কি শুধু Translation Model?

না।

T5 text-to-text framework ব্যবহার করে:

```text
Translation
Summarization
Question Answering
Classification
Paraphrasing
```

সহ বিভিন্ন task handle করতে পারে।

---

# 50. AI Writing Platform-এর জন্য Practical Architecture

তোমার target project ধরে একটি practical design:

```text
                  USER
                   │
                   ▼
              Django API
                   │
                   ▼
             AI Service
                   │
        ┌──────────┼──────────┐
        ↓          ↓          ↓
     Analyzer   Generator   Embedding
        │          │          │
      BERT       GPT/T5      Encoder
        │          │          │
        └──────────┼──────────┘
                   ↓
              Quality Layer
                   ↓
              Final Response
```

---

# 51. Django Backend-এর সাথে Connection

তোমার backend architecture হতে পারে:

```text
React
  │
  ▼
Django REST API
  │
  ▼
AI Service
  │
  ├── Analyzer Model
  ├── Generator Model
  └── Embedding Model
```

API:

```text
POST /api/analyze/
POST /api/rewrite/
POST /api/summarize/
POST /api/semantic-check/
```

---

# 52. Model Selection Decision Tree

```text
Need text understanding?
        │
        ▼
   Encoder model
      BERT-like


Need open-ended generation?
        │
        ▼
   Decoder model
      GPT-like


Need input → transformed output?
        │
        ▼
 Encoder-Decoder
    T5-like
```

---

# 53. Hugging Face Concept

বাস্তবে pretrained models ব্যবহার করতে:

```python
from transformers import AutoTokenizer
from transformers import AutoModel
```

BERT-like:

```python
tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)

model = AutoModel.from_pretrained(
    "bert-base-uncased"
)
```

এখানে model identifier শুধু example; production project-এ task, language, license, size এবং performance অনুযায়ী model নির্বাচন করতে হবে।

---

# 54. GPT-style Model Loading

Causal language model-এর জন্য সাধারণ pattern:

```python
from transformers import AutoTokenizer
from transformers import AutoModelForCausalLM

tokenizer = AutoTokenizer.from_pretrained(
    "MODEL_NAME"
)

model = AutoModelForCausalLM.from_pretrained(
    "MODEL_NAME"
)
```

---

# 55. T5-style Model Loading

```python
from transformers import AutoTokenizer
from transformers import AutoModelForSeq2SeqLM

tokenizer = AutoTokenizer.from_pretrained(
    "MODEL_NAME"
)

model = AutoModelForSeq2SeqLM.from_pretrained(
    "MODEL_NAME"
)
```

---

# 56. Model Class Difference

খুব গুরুত্বপূর্ণ:

```text
BERT
→ AutoModel / AutoModelForSequenceClassification
```

```text
GPT
→ AutoModelForCausalLM
```

```text
T5
→ AutoModelForSeq2SeqLM
```

Task অনুযায়ী head/model class পরিবর্তিত হতে পারে।

---

# 57. Generation API

GPT/T5-like generative model-এ সাধারণ pattern:

```python
outputs = model.generate(
    input_ids,
    max_new_tokens=100
)
```

তারপর:

```python
text = tokenizer.decode(
    outputs[0],
    skip_special_tokens=True
)
```

---

# 58. BERT Embedding Example

```python
import torch

inputs = tokenizer(
    "I love Python",
    return_tensors="pt"
)

with torch.no_grad():

    outputs = model(
        **inputs
    )

hidden_states = outputs.last_hidden_state

print(hidden_states.shape)
```

Conceptually:

```text
(B, L, D)
```

---

# 59. BERT Classification Architecture

```text
Text
 ↓
Tokenizer
 ↓
BERT
 ↓
[CLS] Representation
 ↓
Linear Layer
 ↓
Class
```

Example:

```text
Positive
Negative
Neutral
```

---

# 60. GPT Generation Architecture

```text
Prompt
 ↓
Tokenizer
 ↓
GPT
 ↓
Logits
 ↓
Decoding
 ↓
Generated Text
```

---

# 61. T5 Transformation Architecture

```text
Input
 ↓
Tokenizer
 ↓
Encoder
 ↓
Context
 ↓
Decoder
 ↓
Output IDs
 ↓
Decode
 ↓
Output Text
```

---

# 62. Interview Questions

### Q1. What is BERT?

BERT হলো Transformer encoder-only architecture-based pretrained language model।

### Q2. What is GPT?

GPT হলো decoder-only autoregressive Transformer language model।

### Q3. What is T5?

T5 হলো encoder-decoder Transformer এবং text-to-text framework।

### Q4. Why is BERT bidirectional?

কারণ encoder self-attention input-এর দুই পাশের context ব্যবহার করতে পারে।

### Q5. Why does GPT use causal masking?

Future token information leakage prevent করার জন্য।

### Q6. What is MLM?

Masked Language Modeling—masked token predict করা।

### Q7. What is GPT's main pretraining objective?

Next-token prediction।

### Q8. What is T5's main idea?

Different NLP tasks-কে text-to-text transformation হিসেবে model করা।

### Q9. Which is best for generation?

GPT-style decoder-only models are naturally designed for autoregressive generation।

### Q10. Which is useful for NER?

BERT-style encoder models are a natural fit for token classification/NER।

---

# 63. সবচেয়ে গুরুত্বপূর্ণ Comparison

```text
                 BERT
                  │
          "Understand text"
                  │
                  ▼
           Encoder-only


                  GPT
                  │
          "Generate text"
                  │
                  ▼
           Decoder-only


                  T5
                  │
       "Transform text"
                  │
                  ▼
         Encoder-Decoder
```

---

# 64. M02.32 Completion Checklist

```text
☑ Transformer family
☑ Encoder-only
☑ Decoder-only
☑ Encoder-decoder
☑ BERT
☑ GPT
☑ T5
☑ BERT bidirectional attention
☑ GPT causal attention
☑ T5 encoder attention
☑ T5 decoder attention
☑ T5 cross-attention
☑ BERT MLM
☑ GPT next-token prediction
☑ T5 text-to-text objective
☑ [CLS]
☑ [SEP]
☑ [MASK]
☑ GPT special-token concept
☑ BERT input representation
☑ Token embeddings
☑ Position embeddings
☑ Segment/token-type embeddings
☑ Classification
☑ NER
☑ Generation
☑ Translation
☑ Summarization
☑ Paraphrasing
☑ Semantic representation
☑ Seq2Seq
☑ Transfer learning
☑ Pretraining
☑ Fine-tuning
☑ Encoder vs decoder
☑ BERT vs GPT
☑ GPT vs T5
☑ BERT vs T5
☑ Hugging Face model classes
☑ AI Writing Assistant architecture
☑ Model selection
```

---

# 🧠 Final Mental Model

```text
                         TRANSFORMER
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
          ▼                   ▼                   ▼
      ENCODER-ONLY       DECODER-ONLY      ENCODER-DECODER
          │                   │                   │
          ▼                   ▼                   ▼
        BERT                 GPT                 T5
          │                   │                   │
          ▼                   ▼                   ▼
     Understand            Generate           Transform
       Context               Text               Text
          │                   │                   │
          ▼                   ▼                   ▼
 Classification        Next Token          Input → Output
 NER                   Prediction          Translation
 Embedding              Chat               Summarization
 Similarity             Writing            Paraphrasing
```

### তোমার AI Writing Project-এর জন্য:

```text
              USER TEXT
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
     BERT-like   GPT-like  T5-like
        │         │         │
     Analyze    Generate   Transform
        │         │         │
        └─────────┼─────────┘
                  ↓
          Quality / Meaning
               Check
                  ↓
             Final Text
```

**M02.32 complete.**

---
# M02.33 — Subword Tokenization Deep Dive

M02.32-এ আমরা **BERT vs GPT vs T5 এবং Transformer family** শিখেছি।

এখন আমরা এমন একটি topic-এ যাচ্ছি যেটা **modern NLP এবং LLM-এর foundation-এর অন্যতম গুরুত্বপূর্ণ অংশ**:

> **Subword Tokenization**

GPT, BERT, T5 এবং modern LLM কীভাবে words-কে tokens-এ ভাঙে—এটা ভালোভাবে না বুঝলে LLM-এর ভিতরের অনেক বিষয় বোঝা কঠিন হবে।

---

# 1. Tokenization কী?

Tokenization হলো text-কে ছোট ছোট অংশে ভেঙে token তৈরি করা।

Example:

```text
I love Python
```

Word-level tokenization:

```text
I
love
Python
```

কিন্তু modern LLM সাধারণত শুধু পুরো word ব্যবহার করে না।

বরং:

```text
I
love
Python
```

এর পাশাপাশি word-এর অংশও token হতে পারে।

এটাই:

```text
Subword Tokenization
```

---

# 2. কেন Subword Tokenization দরকার?

ধরি vocabulary-তে আছে:

```text
play
playing
played
player
```

যদি প্রতিটি word আলাদা token হয়:

```text
play
playing
played
player
```

তাহলে vocabulary বড় হবে।

কিন্তু subword approach:

```text
play
ing
ed
er
```

ব্যবহার করে অনেক নতুন word represent করা সম্ভব।

---

# 3. Unknown Word Problem

Word-level tokenizer-এর বড় সমস্যা:

```text
Vocabulary
↓
Known words
```

ধরি model-এর vocabulary:

```text
cat
dog
computer
Python
```

এখন input:

```text
"unbelievability"
```

যদি পুরো word vocabulary-তে না থাকে:

```text
UNKNOWN
```

Problem।

Subword tokenizer করতে পারে:

```text
un
believ
ability
```

Conceptually।

তাই unknown word handle করা সহজ হয়।

---

# 4. Character vs Word vs Subword

তিনটি approach:

```text
Character-level
      ↓
c a t


Word-level
      ↓
cat


Subword-level
      ↓
cat
```

আর:

```text
playing
```

হতে পারে:

```text
Character:
p l a y i n g

Word:
playing

Subword:
play + ing
```

Actual segmentation tokenizer অনুযায়ী আলাদা হতে পারে।

---

# 5. Vocabulary Size

ধরি:

### Character vocabulary

```text
~100 characters
```

### Word vocabulary

```text
500,000+ words
```

### Subword vocabulary

```text
10,000–100,000 tokens
```

এগুলো শুধু illustrative ranges; actual tokenizer/model অনুযায়ী vocabulary size অনেক ভিন্ন হতে পারে।

Subword method সাধারণত একটি useful middle ground:

```text
Small vocabulary
+
Ability to represent unseen words
```

---

# 6. Subword-এর মূল Idea

ধরি words:

```text
play
playing
played
player
playful
```

Common part:

```text
play
```

তাহলে tokenizer:

```text
play
+
ing
+
ed
+
er
+
ful
```

এর মতো reusable pieces তৈরি করতে পারে।

---

# 7. Morphology-এর সাথে সম্পর্ক

আগে M02.02-এ আমরা morphology শিখেছি।

Example:

```text
unhappy
```

Morphologically:

```text
un + happy
```

Subword tokenizer কখনও এরকম meaningful linguistic pieces তৈরি করতে পারে।

কিন্তু গুরুত্বপূর্ণ:

> **Subword token সবসময় linguistic morpheme নয়।**

Tokenizer frequency/statistical patterns-এর ভিত্তিতে এমন pieces বানাতে পারে যেগুলো মানুষের কাছে natural morpheme নাও হতে পারে।

---

# 8. Subword Token ≠ Morpheme

Example:

```text
unhappiness
```

Morpheme:

```text
un + happy + ness
```

কিন্তু tokenizer segmentation হতে পারে অন্যরকম:

```text
un
happi
ness
```

অথবা অন্য segmentation।

তাই:

```text
Morpheme
≠
Subword Token
```

এটা খুব গুরুত্বপূর্ণ।

---

# 9. Major Subword Algorithms

Modern NLP-তে গুরুত্বপূর্ণ algorithms:

```text
1. BPE
2. WordPiece
3. Unigram Language Model
4. SentencePiece framework
```

আর model-specific tokenizer implementation এগুলোর variant/combination ব্যবহার করতে পারে।

---

# 10. BPE

BPE:

**Byte Pair Encoding**

মূল ধারণা:

> Frequent symbol pairs repeatedly merge করে vocabulary তৈরি করা।

ধরি:

```text
low
lower
lowest
```

Character-level শুরু:

```text
l o w
l o w e r
l o w e s t
```

Frequent pair:

```text
l + o
```

merge:

```text
lo
```

তারপর:

```text
lo + w
```

→

```text
low
```

---

# 11. BPE-এর Basic Process

Conceptually:

```text
Characters
    ↓
Find frequent pair
    ↓
Merge pair
    ↓
Update vocabulary
    ↓
Find next frequent pair
    ↓
Merge
    ↓
Repeat
```

---

# 12. Simple BPE Example

Corpus:

```text
low
lower
lowest
```

Start:

```text
l o w
l o w e r
l o w e s t
```

Frequent:

```text
l o
```

Merge:

```text
lo
```

তারপর:

```text
lo w
lo w e r
lo w e s t
```

`lo + w` frequent হলে:

```text
low
```

এরপর:

```text
low er
low est
```

এভাবে vocabulary তৈরি হতে পারে।

---

# 13. BPE-এর Important Idea

BPE:

```text
Small units
    ↓
Repeated merging
    ↓
Frequent subwords
```

তাই:

```text
Character
 ↓
Subword
 ↓
Word
```

এর মাঝামাঝি representation পাওয়া যায়।

---

# 14. GPT-2 এবং BPE

GPT-2 historically **byte-level BPE** ব্যবহার করেছে।

এখানে একটি গুরুত্বপূর্ণ idea:

```text
Text
 ↓
Bytes
 ↓
BPE merges
 ↓
Token IDs
```

Byte-level approach-এর কারণে অনেক ধরনের text এবং unseen character sequence handle করা যায়।

Modern GPT-family model-গুলোর tokenizer implementation একই হবে—এমন নয়।

---

# 15. Byte-Level BPE

Normal character vocabulary:

```text
A-Z
a-z
0-9
...
```

এর বদলে byte representation ব্যবহার করা যায়।

Concept:

```text
Text
 ↓
UTF-8 bytes
 ↓
BPE
 ↓
Tokens
```

এতে arbitrary text sequence represent করা সহজ হয়।

---

# 16. WordPiece

WordPiece হলো আরেকটি subword tokenization algorithm।

এটি বিশেষভাবে BERT-family models-এর সাথে associated।

Concept:

```text
Word
 ↓
Candidate subwords
 ↓
Best segmentation
 ↓
Tokens
```

Example conceptual:

```text
playing
```

হতে পারে:

```text
play
##ing
```

এখানে `##` convention বোঝায় যে subwordটি word-এর continuation।

সব tokenizer একই notation ব্যবহার করে না।

---

# 17. WordPiece-এর Important Point

WordPiece vocabulary:

```text
play
playing
##ing
##ed
##er
```

এর মতো subword units রাখতে পারে।

Unknown word:

```text
unbelievable
```

কে পুরো word হিসেবে না পেলে pieces-এ ভাঙতে পারে।

---

# 18. BPE vs WordPiece

| Feature               | BPE                   | WordPiece                  |
| --------------------- | --------------------- | -------------------------- |
| Main idea             | Frequent pair merging | Subword selection/learning |
| Famous association    | GPT-2                 | BERT                       |
| Character/subword     | Yes                   | Yes                        |
| Unknown word handling | Good                  | Good                       |
| Vocabulary            | Subword units         | Subword units              |

Implementation details model-specific।

---

# 19. SentencePiece

SentencePiece হলো একটি **tokenization framework/library**, শুধুমাত্র একটি single segmentation algorithm নয়।

এটি raw text directly process করতে পারে।

Concept:

```text
Raw Text
 ↓
SentencePiece
 ↓
Subword Tokens
```

এতে আগে manually whitespace tokenize করার প্রয়োজন নেই।

---

# 20. SentencePiece কেন গুরুত্বপূর্ণ?

Traditional word tokenization:

```text
Text
 ↓
Whitespace
 ↓
Words
 ↓
Subword
```

SentencePiece:

```text
Raw Text
 ↓
Tokenizer
 ↓
Subwords
```

এতে whitespace-সহ text sequence directly model করা যায়।

---

# 21. SentencePiece Algorithms

SentencePiece framework-এর মধ্যে বিভিন্ন model থাকতে পারে, যেমন:

```text
BPE
Unigram
```

তাই:

```text
SentencePiece
≠ BPE
```

বরং:

```text
SentencePiece
 ├── BPE
 └── Unigram
```

conceptually।

---

# 22. Unigram Language Model

আরেকটি approach:

**Unigram Language Model**

এখানে শুরুতে অনেক candidate subwords থাকে।

তারপর statistical probability-এর ভিত্তিতে vocabulary reduce করা হয়।

Conceptually:

```text
Large Candidate Vocabulary
          ↓
Probability Estimation
          ↓
Remove Less Useful Pieces
          ↓
Final Vocabulary
```

---

# 23. Unigram Tokenization

একটি word:

```text
unbelievable
```

এর বিভিন্ন segmentation হতে পারে:

```text
un + believe + able
```

অথবা:

```text
un + believable
```

Tokenizer probability অনুযায়ী best segmentation নির্বাচন করতে পারে।

---

# 24. BPE vs Unigram

### BPE

```text
Start small
 ↓
Merge
 ↓
Merge
 ↓
Merge
```

### Unigram

```text
Start larger
 ↓
Remove less useful pieces
 ↓
Final vocabulary
```

এটা conceptual difference; actual implementations আরও nuanced।

---

# 25. Special Tokens

Modern tokenizers-এ special tokens থাকতে পারে:

```text
[PAD]
[UNK]
[CLS]
[SEP]
[MASK]
<BOS>
<EOS>
```

সব model-এ সব token থাকবে না।

---

# 26. `[UNK]`

`UNK` = Unknown token।

যদি tokenizer কোনো input represent করতে না পারে:

```text
Input
 ↓
[UNK]
```

তবে byte-level বা sufficiently capable subword tokenizers unknown-token problem অনেকটা কমিয়ে দিতে পারে।

---

# 27. `[PAD]`

Padding token:

```text
[PAD]
```

Different length sequence একই batch shape-এ আনার জন্য ব্যবহৃত হতে পারে।

Example:

```text
I love AI

I love machine learning
```

Padding:

```text
I love AI [PAD] [PAD]

I love machine learning
```

---

# 28. `[CLS]`, `[SEP]`, `[MASK]`

BERT-style tokenizer-এ:

```text
[CLS]
```

sequence শুরুতে।

```text
[SEP]
```

sequence boundary।

```text
[MASK]
```

MLM training-এর জন্য।

Example:

```text
[CLS] I love AI [SEP]
```

---

# 29. GPT Special Tokens

GPT-family models-এ special tokens model অনুযায়ী আলাদা হতে পারে।

Conceptually:

```text
<BOS>
<EOS>
```

Generation stopping-এর জন্য EOS-type token ব্যবহার হতে পারে।

কিছু GPT-style models-এর tokenizer-এ padding behavior-ও আলাদা হতে পারে।

---

# 30. Token IDs

Tokenizer শুধু tokens তৈরি করে না।

এগুলোকে integer ID-তে convert করে।

Example:

```text
I       → 40
love    → 812
Python  → 9231
```

Final:

```text
[40, 812, 9231]
```

---

# 31. Tokenizer Vocabulary

Tokenizer-এর একটি vocabulary থাকে:

```text
Token → ID
```

Example:

```text
"the" → 10
"ing" → 25
"Python" → 900
```

এই mapping:

```text
Tokenizer Vocabulary
```

এর অংশ।

---

# 32. Token ID থেকে Embedding

আগের lesson-এ embedding শিখেছ।

Flow:

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding Lookup
 ↓
Vectors
 ↓
Transformer
```

Example:

```text
"Python"
 ↓
9231
 ↓
[0.21, 0.55, ...]
```

---

# 33. Tokenization বনাম Embedding

এ দুটো confuse করা যাবে না।

### Tokenization

```text
Text
 ↓
Token IDs
```

### Embedding

```text
Token IDs
 ↓
Vectors
```

অর্থাৎ:

```text
Tokenizer
→ discrete representation

Embedding
→ dense numerical representation
```

---

# 34. Tokenization Example

ধরি input:

```text
"playing"
```

Possible subword tokens:

```text
play
ing
```

IDs:

```text
[1254, 321]
```

Embedding:

```text
[1254]
 ↓
vector

[321]
 ↓
vector
```

---

# 35. কেন Subword LLM-এর জন্য Ideal?

কারণ এটি balance করে:

```text
Character-level
    │
    │ Small vocabulary
    │ Long sequences
    ↓
Subword
    │
    │ Balance
    ↓
Word-level
    │ Large vocabulary
    │ Unknown-word problem
```

Subword:

```text
Vocabulary manageable
+
Rare words representable
```

---

# 36. Rare Words

ধরি vocabulary-তে:

```text
computer
```

আছে।

কিন্তু:

```text
computationalization
```

নেই।

Subword tokenizer:

```text
computer
ation
ization
```

এর মতো pieces ব্যবহার করতে পারে।

Actual segmentation tokenizer-dependent।

---

# 37. Morphologically Rich Languages

যেসব language-এ word-এর অনেক morphological variation আছে, subword tokenization বিশেষভাবে useful হতে পারে।

Example concept:

```text
Root
+
Prefix
+
Suffix
+
Inflection
```

এর ফলে word vocabulary explode না করেও অনেক forms represent করা যায়।

---

# 38. Bangla NLP

Bangla-তে tokenization আরও interesting কারণ:

```text
Unicode
যুক্তাক্ষর
কার
বিভিন্ন word forms
```

ইত্যাদি বিষয় রয়েছে।

তাই English tokenizer blindly Bangla-এর জন্য ideal হবে—এমন নয়।

Bangla-focused model-এর tokenizer language-specific data দিয়ে trained হওয়া গুরুত্বপূর্ণ।

---

# 39. Unicode

Computer text ultimately Unicode characters/code points দিয়ে represent হয়।

Example:

```text
A
আ
ক
```

প্রতিটির Unicode representation আছে।

Tokenizer এই text কে model-specific token units-এ convert করে।

---

# 40. Character ≠ Byte ≠ Token

এগুলো খুব ভালোভাবে আলাদা করতে হবে।

```text
Character
↓
Unicode representation

Byte
↓
Encoded binary unit

Token
↓
Tokenizer-defined text unit
```

একটি token:

```text
একটি character
```

হতে পারে।

আবার:

```text
একাধিক character
```

হতে পারে।

আবার byte-level tokenizer হলে underlying byte sequence-এর সাথে token-এর relation থাকতে পারে।

---

# 41. Token Count বনাম Word Count

একটি sentence:

```text
I love programming.
```

Word count:

```text
3
```

Token count হতে পারে:

```text
3
4
5
```

ইত্যাদি—tokenizer-এর উপর নির্ভর করে।

তাই:

> **1 word ≠ 1 token**

---

# 42. কেন Token Count গুরুত্বপূর্ণ?

কারণ LLM systems-এ token count-এর সাথে অনেক কিছু সম্পর্কিত:

```text
Context length
Inference cost
Training compute
Memory usage
Latency
API usage
```

---

# 43. Context Window-এর সাথে সম্পর্ক

ধরি model context:

```text
4096 tokens
```

এটা:

```text
4096 words
```

নয়।

বরং:

```text
4096 tokenizer tokens
```

---

# 44. Tokenization এবং Context Window

ধরি:

```text
Text A = 1000 words
```

এটা হয়তো:

```text
1300 tokens
```

হতে পারে।

আবার অন্য text:

```text
1000 words
```

হয়তো:

```text
2000 tokens
```

হতে পারে।

Language এবং tokenizer-এর উপর depend করে।

---

# 45. Tokenization Efficiency

ভালো tokenizer-এর একটি লক্ষ্য:

```text
Meaningful text
 ↓
Reasonable token count
```

Token count খুব বেশি হলে:

```text
Sequence length ↑
 ↓
Computation ↑
```

বিশেষ করে standard attention-এর quadratic sequence-length cost-এর কারণে।

---

# 46. Tokenization-এর একটি বড় Trade-off

```text
Small vocabulary
      ↓
More tokens per word
      ↓
Longer sequences
```

অন্যদিকে:

```text
Large vocabulary
      ↓
Fewer tokens
      ↓
More vocabulary parameters / complexity
```

তাই vocabulary design একটি important engineering decision।

---

# 47. Tokenizer Training

Tokenizer নিজেও train করা হয়।

Conceptually:

```text
Large Text Corpus
      ↓
Tokenizer Training
      ↓
Vocabulary
      ↓
Merge Rules / Token Probabilities
      ↓
Saved Tokenizer
```

তারপর model training:

```text
Text
 ↓
Trained Tokenizer
 ↓
Token IDs
 ↓
Model
```

---

# 48. Important: Tokenizer এবং Model একসাথে কাজ করে

Tokenizer vocabulary:

```text
ID 100 → "hello"
```

Model-এর embedding matrix-এ:

```text
row 100
```

এই token-এর vector থাকবে।

তাই tokenizer বদলে দিলে model-এর token-ID mapping আর model weights-এর সাথে compatible নাও থাকতে পারে।

---

# 49. Embedding Matrix-এর সাথে সম্পর্ক

ধরি:

```text
vocab_size = 50,000
d_model = 768
```

Embedding matrix:

```text
(50,000, 768)
```

Token ID:

```text
100
```

মানে embedding matrix-এর:

```text
row 100
```

retrieve করা হবে।

---

# 50. Tokenizer পরিবর্তন করলে কী হয়?

ধরি পুরোনো:

```text
Python → 500
```

নতুন tokenizer:

```text
Python → 820
```

কিন্তু model-এর embedding row 500 যদি Python-এর জন্য trained থাকে, নতুন mapping সরাসরি ব্যবহার করলে সমস্যা হবে।

তাই pretrained model-এর সাথে matching tokenizer ব্যবহার করতে হয়।

---

# 51. Hugging Face Tokenizer

Modern NLP-তে commonly:

```python
from transformers import AutoTokenizer
```

Example:

```python
tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)
```

তারপর:

```python
text = "I love Python."

tokens = tokenizer.tokenize(text)

print(tokens)
```

Output model-specific হতে পারে।

---

# 52. Token IDs বের করা

```python
inputs = tokenizer(
    "I love Python.",
    return_tensors="pt"
)

print(inputs["input_ids"])
```

Output:

```text
tensor([
    [101, ..., 102]
])
```

Exact IDs/tokenization model-specific।

---

# 53. Tokenizer-এর Full Output

```python
inputs = tokenizer(
    "I love Python.",
    return_tensors="pt"
)
```

এতে সাধারণত থাকতে পারে:

```text
input_ids
attention_mask
```

এবং model/tokenizer অনুযায়ী additional fields থাকতে পারে।

---

# 54. Attention Mask

Example:

```text
Tokens:
I love Python [PAD]
```

Attention mask:

```text
1 1 1 0
```

Meaning:

```text
1 → valid token
0 → padding
```

এটি model-specific API convention-এর অংশ হতে পারে।

---

# 55. Decode

Token IDs → text:

```python
text = tokenizer.decode(
    input_ids[0]
)

print(text)
```

অর্থাৎ:

```text
Text
 ↓
Encode
 ↓
Token IDs

Token IDs
 ↓
Decode
 ↓
Text
```

---

# 56. Encode → Decode

```python
text = "I love Python."

encoded = tokenizer.encode(text)

decoded = tokenizer.decode(encoded)

print(decoded)
```

Concept:

```text
"I love Python."
       ↓
[IDs]
       ↓
"I love Python."
```

তবে special-token handling এবং normalization-এর কারণে decoded string সবসময় byte-for-byte identical নাও হতে পারে।

---

# 57. Tokenizer-এর Important Operations

```text
tokenize()
encode()
decode()
batch_encode_plus() / tokenizer(...)
convert_tokens_to_ids()
convert_ids_to_tokens()
```

Modern Hugging Face usage-এ সাধারণত:

```python
tokenizer(...)
```

interface-ই বেশি ব্যবহৃত হয়।

---

# 58. Tokenizer Debugging

কোন model কীভাবে text tokenize করছে দেখতে:

```python
tokens = tokenizer.tokenize(
    "unbelievable"
)

print(tokens)
```

তারপর:

```python
ids = tokenizer.convert_tokens_to_ids(
    tokens
)

print(ids)
```

---

# 59. Subword Visualization

Conceptually:

```text
"unbelievable"

       ↓

["un", "believable"]

       ↓

[1012, 5821]
```

Actual result tokenizer-specific।

এভাবে tokenizer-এর behavior বুঝতে পারবে।

---

# 60. BPE Training-এর Simplified Python Example

Educational version:

```python
from collections import Counter


words = [
    "low",
    "lower",
    "lowest",
    "low"
]

pairs = Counter()

for word in words:

    symbols = list(word)

    for i in range(len(symbols) - 1):

        pair = (
            symbols[i],
            symbols[i + 1]
        )

        pairs[pair] += 1


print(pairs.most_common())
```

এখানে আমরা frequent character pairs খুঁজছি।

Production BPE tokenizer অবশ্যই এর চেয়ে অনেক sophisticated।

---

# 61. Simple BPE Merge Function

Educational:

```python
def merge_pair(tokens, pair):

    result = []

    i = 0

    while i < len(tokens):

        if (
            i < len(tokens) - 1
            and (tokens[i], tokens[i + 1]) == pair
        ):
            result.append(
                tokens[i] + tokens[i + 1]
            )
            i += 2

        else:
            result.append(tokens[i])
            i += 1

    return result
```

Example:

```python
tokens = ["l", "o", "w"]

tokens = merge_pair(
    tokens,
    ("l", "o")
)

print(tokens)
```

Output:

```text
['lo', 'w']
```

---

# 62. BPE-এর Educational Flow

```text
["l","o","w"]
       ↓
Find ("l","o")
       ↓
Merge
       ↓
["lo","w"]
       ↓
Find ("lo","w")
       ↓
Merge
       ↓
["low"]
```

এভাবেই frequent patterns vocabulary-তে উঠতে পারে।

---

# 63. BPE vs Stemming

খুব গুরুত্বপূর্ণ comparison।

### Stemming

```text
playing
 ↓
play
```

Goal:

```text
linguistic normalization
```

### BPE

```text
playing
 ↓
play + ing
```

Goal:

```text
efficient token representation
```

---

# 64. BPE vs Lemmatization

Lemmatization:

```text
better
 ↓
good
```

বা:

```text
running
 ↓
run
```

Subword tokenization:

```text
running
 ↓
run + ning
```

Actual tokenizer output may differ।

তাই:

```text
Lemmatization
≠
Subword Tokenization
```

---

# 65. Subword Tokenization vs Word Tokenization

```text
Word Tokenization

playing
 ↓
["playing"]
```

```text
Subword Tokenization

playing
 ↓
["play", "ing"]
```

Subword approach rare/unseen words-এর ক্ষেত্রে বেশি flexible।

---

# 66. Subword Tokenization vs Character Tokenization

### Character

```text
internationalization
 ↓
i n t e r n a t i o n ...
```

অনেক tokens।

### Subword

```text
international + ization
```

কম tokens হতে পারে।

---

# 67. LLM-এর Complete Token Pipeline

এখন আগের সব lesson connect করো:

```text
                  RAW TEXT
                      │
                      ▼
                  TOKENIZER
                      │
          ┌───────────┴───────────┐
          │                       │
       Subword                 Special
       Tokens                   Tokens
          │                       │
          └───────────┬───────────┘
                      ▼
                   Token IDs
                      │
                      ▼
                  Embedding
                      │
                      ▼
              Position Information
                      │
                      ▼
               Transformer
                      │
                      ▼
                    Logits
                      │
                      ▼
                 Generation
```

---

# 68. AI Writing Assistant-এর ক্ষেত্রে

User লিখল:

```text
"Please improve this paragraph."
```

System:

```text
User Text
   ↓
Tokenizer
   ↓
Subword Tokens
   ↓
Token IDs
   ↓
Embedding
   ↓
Transformer
   ↓
Logits
   ↓
Decoder
   ↓
Generated Tokens
   ↓
Tokenizer Decode
   ↓
Final Text
```

---

# 69. Original Text বনাম Generated Text

Input:

```text
Improve this sentence.
```

Tokenizer:

```text
Tokens
 ↓
IDs
```

Model:

```text
IDs
 ↓
Transformer
```

Generation:

```text
Next token
 ↓
Next token
 ↓
Next token
```

শেষে:

```text
Token IDs
 ↓
Decode
 ↓
Human-readable text
```

---

# 70. Tokenizer কেন Project-এর জন্য Important?

তোমার AI writing platform-এ tokenization directly affect করবে:

```text
Input limit
Output limit
Inference cost
Memory
Latency
Context window
Prompt size
Training data preparation
Fine-tuning
```

তাই tokenizer শুধু preprocessing tool নয়।

এটা পুরো LLM system-এর fundamental component।

---

# 71. Tokenizer-এর Common Mistakes

### Mistake 1

ভাবা:

```text
1 word = 1 token
```

❌ ভুল।

### Mistake 2

ভাবা:

```text
Subword = Morpheme
```

❌ সবসময় নয়।

### Mistake 3

Tokenizer এবং model আলাদা করে arbitraryভাবে change করা।

❌ pretrained model-এর ক্ষেত্রে সমস্যা হতে পারে।

### Mistake 4

Token count-কে word count ভাবা।

❌ ভুল।

### Mistake 5

English tokenizer দিয়ে সব language equally ভালো handle হবে ভাবা।

❌ ভুল।

---

# 72. Interview Questions

### Q1. What is subword tokenization?

Text-এর words-কে reusable smaller units/subwords-এ ভেঙে token তৈরি করার technique।

### Q2. Why do modern LLMs use subword tokenization?

Vocabulary size manageable রাখা এবং rare/unseen words efficiently represent করার জন্য।

### Q3. What is BPE?

Byte Pair Encoding—frequent symbol/subword pairs merge করে vocabulary তৈরি করার algorithm।

### Q4. What is WordPiece?

Subword tokenization algorithm, notably associated with BERT-family models।

### Q5. What is SentencePiece?

Raw text-এর উপর subword tokenization করার framework, যা BPE বা Unigram-এর মতো algorithms ব্যবহার করতে পারে।

### Q6. Is a subword the same as a morpheme?

না।

### Q7. What is `[UNK]`?

Unknown token।

### Q8. What is `[PAD]`?

Sequence padding-এর জন্য ব্যবহৃত token।

### Q9. What is the difference between tokenizer and embedding?

Tokenizer text → token IDs করে; embedding token IDs → dense vectors করে।

### Q10. Why does token count matter?

Context length, memory, computation, latency এবং cost-এর সঙ্গে token count directly related।

---

# 73. Theory Questions

নিজে answer করার চেষ্টা করো:

1. Why can't we use only word-level tokenization?
2. Why is character-level tokenization inefficient for LLMs?
3. How does BPE work?
4. BPE এবং WordPiece-এর conceptual difference কী?
5. SentencePiece কী?
6. Why is tokenizer-model compatibility important?
7. Token এবং word-এর difference কী?
8. Token এবং morpheme-এর difference কী?
9. Why does tokenization affect context length?
10. Why can two languages produce different token counts for similar-length text?

---

# 74. Practical Exercises

## Beginner

এই words-এর সম্ভাব্য subword decomposition manually লেখো:

```text
playing
unhappy
developer
programming
internationalization
```

---

## Intermediate

Hugging Face tokenizer ব্যবহার করে:

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)

text = "I am learning natural language processing."

tokens = tokenizer.tokenize(text)

print(tokens)
```

তারপর:

```python
ids = tokenizer.convert_tokens_to_ids(
    tokens
)

print(ids)
```

---

## Advanced

নিজে calculate করো:

```text
Number of words
Number of tokens
Token/word ratio
```

একটি paragraph-এর জন্য।

Formula:

$$
Token\ Ratio =
\frac{Number\ of\ Tokens}
{Number\ of\ Words}
$$

---

# 75. M02.33 Completion Checklist

```text
☑ Tokenization
☑ Word-level tokenization
☑ Character-level tokenization
☑ Subword tokenization
☑ Unknown-word problem
☑ Vocabulary size
☑ Subword concept
☑ Morphology connection
☑ Subword ≠ Morpheme
☑ BPE
☑ BPE merge process
☑ Byte-level BPE
☑ GPT-2 tokenizer concept
☑ WordPiece
☑ ## continuation concept
☑ SentencePiece
☑ SentencePiece vs BPE
☑ Unigram Language Model
☑ Special tokens
☑ [UNK]
☑ [PAD]
☑ [CLS]
☑ [SEP]
☑ [MASK]
☑ BOS/EOS concept
☑ Token IDs
☑ Vocabulary
☑ Tokenizer vocabulary
☑ Tokenizer-model compatibility
☑ Character vs byte vs token
☑ Word count vs token count
☑ Context window relation
☑ Tokenization efficiency
☑ Tokenizer training
☑ Embedding connection
☑ Attention mask connection
☑ BPE vs stemming
☑ BPE vs lemmatization
☑ Word vs subword
☑ Character vs subword
☑ Hugging Face tokenizer
☑ Encode
☑ Decode
☑ Tokenize
☑ Token ID conversion
☑ BPE educational implementation
☑ AI Writing Assistant connection
☑ Practical exercises
☑ Interview questions
```

---

# 🧠 Final Mental Model

সবচেয়ে গুরুত্বপূর্ণ diagram:

```text
                       TEXT
                        │
                        ▼
                    TOKENIZER
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
      Character       Subword        Word
       Token           Token         Token
          │             │             │
          └─────────────┼─────────────┘
                        ▼
                    TOKEN IDs
                        │
                        ▼
                    EMBEDDING
                        │
                        ▼
              POSITION INFORMATION
                        │
                        ▼
                  TRANSFORMER
                        │
                        ▼
                     LOGITS
                        │
                        ▼
                  NEXT TOKEN
                        │
                        ▼
                   TOKEN IDs
                        │
                        ▼
                     DECODE
                        │
                        ▼
                       TEXT
```

আর subword algorithms:

```text
              SUBWORD TOKENIZATION
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
         BPE       WordPiece     Unigram
          │            │            │
        GPT-2         BERT      SentencePiece
       association   association    often
```

**M02.33 complete.**

---
# M02.34 — Tokenization Deep Dive: BPE, WordPiece & SentencePiece From Scratch

M02.33-এ আমরা **Subword Tokenization**-এর foundation শিখেছি। এবার M02.34-এ আমরা tokenization-কে আরও গভীরে নিয়ে যাব।

এখানে মূল লক্ষ্য:

```text
Subword Tokenization
        ↓
BPE কীভাবে শেখে?
        ↓
WordPiece কীভাবে কাজ করে?
        ↓
Unigram কীভাবে কাজ করে?
        ↓
SentencePiece কীভাবে কাজ করে?
        ↓
Tokenizer কীভাবে train + save + load হয়?
        ↓
LLM-এর সাথে tokenizer কীভাবে কাজ করে?
```

---

# 1. প্রথমে পুরো ধারণাটা

একটি LLM সরাসরি এই text দেখে না:

```text
I love programming.
```

বরং:

```text
I love programming.
        ↓
Tokenizer
        ↓
Subword Tokens
        ↓
Token IDs
        ↓
Embeddings
        ↓
Transformer
```

অর্থাৎ:

> **Tokenizer হলো Text এবং Neural Network-এর মধ্যে bridge।**

---

# 2. Tokenizer-এর তিনটি প্রধান কাজ

Tokenizer-এর কাজকে তিন ভাগে দেখতে পারো:

```text
Text
 ↓
Segmentation
 ↓
Vocabulary Lookup
 ↓
Token IDs
```

উদাহরণ:

```text
"playing"
```

হতে পারে:

```text
["play", "ing"]
```

তারপর:

```text
["play", "ing"]
       ↓
[1254, 321]
```

---

# 3. Tokenizer Training বনাম Tokenization

এ দুটো আলাদা।

### Tokenizer Training

নতুন tokenizer বানানো:

```text
Large Corpus
     ↓
Tokenizer Training
     ↓
Vocabulary + Rules
```

### Tokenization

আগে trained tokenizer ব্যবহার করা:

```text
New Text
   ↓
Trained Tokenizer
   ↓
Tokens
   ↓
IDs
```

---

# 4. BPE আবার শুরু থেকে

BPE-এর মূল ধারণা:

> Frequent adjacent symbol/subword pair বারবার merge করা।

ধরি corpus:

```text
low
lower
lowest
```

শুরুতে:

```text
l o w
l o w e r
l o w e s t
```

---

# 5. Pair Frequency

এখন adjacent pairs count করি:

```text
l o
o w
w e
e r
e s
s t
```

ধরি:

```text
(l, o) = 3
(o, w) = 3
(w, e) = 2
```

সবচেয়ে frequent:

```text
l + o
```

তাই merge:

```text
lo
```

---

# 6. দ্বিতীয় Merge

এখন:

```text
lo w
lo w e r
lo w e s t
```

`lo + w` frequent হলে:

```text
low
```

তাহলে:

```text
low
low e r
low e s t
```

---

# 7. আরও Merge

পরবর্তী frequent pair:

```text
e + r
```

→

```text
er
```

আর:

```text
e + s
```

→

```text
es
```

ইত্যাদি।

এভাবে vocabulary gradually তৈরি হয়।

---

# 8. BPE-এর Mental Model

```text
Characters
    ↓
Frequent Pair
    ↓
Merge
    ↓
New Subword
    ↓
Frequent Pair
    ↓
Merge
    ↓
Larger Subword
```

অর্থাৎ:

```text
small units
     ↓
learned units
     ↓
larger units
```

---

# 9. BPE Vocabulary

শেষে tokenizer-এর vocabulary-এর মধ্যে থাকতে পারে:

```text
l
o
w
low
er
est
```

নতুন word:

```text
lowest
```

tokenize হতে পারে:

```text
low + est
```

---

# 10. BPE-এর গুরুত্বপূর্ণ বিষয়

BPE শুধু:

```text
"common words"
```

শেখে না।

এটি:

```text
common subword patterns
```

শেখে।

তাই:

```text
program
programming
programmer
programmed
```

এর মধ্যে common patterns reuse করা সম্ভব।

---

# 11. BPE-এর Advantages

```text
☑ Vocabulary manageable
☑ Rare words handle করতে পারে
☑ Unknown word problem কম
☑ Morphological patterns capture করতে পারে
☑ LLM-এর জন্য efficient
```

---

# 12. BPE-এর Limitations

```text
☑ Linguistic meaning guarantee করে না
☑ Token boundary সবসময় intuitive নয়
☑ Language অনুযায়ী efficiency ভিন্ন
☑ Token count বেশি হতে পারে
```

---

# 13. WordPiece

এবার WordPiece।

WordPiece BERT-family tokenizer-এর সাথে strongly associated।

Concept:

```text
Text
 ↓
Candidate subwords
 ↓
Best segmentation
 ↓
Token IDs
```

---

# 14. WordPiece Example

ধরি:

```text
playing
```

সম্ভাব্য:

```text
play + ##ing
```

এখানে:

```text
play
```

একটি starting token।

আর:

```text
##ing
```

বোঝায় এটি word-এর continuation।

---

# 15. `##` কেন?

BERT-style WordPiece notation-এ:

```text
play
```

word-এর beginning।

কিন্তু:

```text
##ing
```

word-এর মাঝখান/শেষের continuation।

Example:

```text
playing
 ↓
play
##ing
```

এটা tokenizer notation; সব tokenizer `##` ব্যবহার করে না।

---

# 16. WordPiece Unknown Problem

যদি tokenizer কোনো word-কে available subwords দিয়ে represent করতে না পারে:

```text
[UNK]
```

আসতে পারে।

BERT-এর WordPiece vocabulary-তে `[UNK]` গুরুত্বপূর্ণ।

---

# 17. WordPiece বনাম BPE

দুটোই subword tokenization।

কিন্তু তাদের learning objective/selection process একই নয়।

Simplified:

```text
BPE
↓
Frequent pair merge
```

WordPiece:

```text
Candidate vocabulary
↓
Likelihood-oriented selection
↓
Useful subwords
```

Exact algorithm implementation আরও nuanced।

---

# 18. Unigram Language Model

এবার Unigram।

এখানে BPE-এর বিপরীত ধরনের intuition পাওয়া যায়।

BPE:

```text
Small
 ↓
Merge
 ↓
Large
```

Unigram:

```text
Large candidate vocabulary
 ↓
Remove less useful pieces
 ↓
Final vocabulary
```

---

# 19. Unigram Example

ধরি candidate vocabulary:

```text
u
un
b
be
bel
believe
able
ability
...
```

Tokenizer probability estimate করতে পারে।

তারপর কম useful tokens বাদ দিতে পারে।

---

# 20. Unigram Segmentation

ধরি:

```text
unbelievable
```

সম্ভাব্য:

```text
un + believable
```

অথবা:

```text
un + believe + able
```

অথবা অন্য segmentation।

Unigram model probability-based segmentation ব্যবহার করতে পারে।

---

# 21. BPE বনাম Unigram

```text
BPE:

characters
    ↓
merge
    ↓
merge
    ↓
merge
```

```text
Unigram:

many candidates
    ↓
estimate usefulness
    ↓
remove
    ↓
final vocabulary
```

---

# 22. SentencePiece

SentencePiece হলো খুব গুরুত্বপূর্ণ concept।

এটি একটি **general subword tokenization framework**।

এটি raw text সরাসরি process করতে পারে।

```text
Raw Text
   ↓
SentencePiece
   ↓
Subword Tokens
```

---

# 23. SentencePiece কেন তৈরি করা হয়েছিল?

Traditional tokenization অনেক সময় whitespace-এর উপর নির্ভর করে:

```text
"I love NLP"
      ↓
["I", "love", "NLP"]
```

তারপর subword।

SentencePiece raw text থেকে directly কাজ করতে পারে।

এতে language-specific whitespace assumptions কমে।

---

# 24. SentencePiece এবং Languages

SentencePiece-এর বড় সুবিধা হলো এটি language-agnosticভাবে raw text process করতে পারে।

তাই এটি এমন language-এর ক্ষেত্রেও useful যেখানে whitespace word boundary সবসময় English-এর মতো straightforward নয়।

---

# 25. SentencePiece-এর ভিতরে কী Algorithm?

SentencePiece নিজে একটি single tokenization algorithm নয়।

এটি ব্যবহার করতে পারে:

```text
SentencePiece
   │
   ├── BPE
   │
   └── Unigram
```

তাই:

```text
SentencePiece ≠ BPE
```

বরং:

```text
SentencePiece
→ framework
```

---

# 26. Whitespace-এর Representation

SentencePiece-style tokenization-এ whitespace-কে special marker দিয়ে represent করা হতে পারে।

প্রচলিত representation:

```text
▁
```

Example conceptual:

```text
"I love AI"
```

হতে পারে:

```text
▁I
▁love
▁AI
```

এটি tokenizer-এর internal representation বোঝাতে সাহায্য করে।

---

# 27. কেন Whitespace Marker দরকার?

কারণ tokenizer raw text থেকে কাজ করলে জানতে হবে:

```text
কোথায় নতুন word শুরু হয়েছে?
```

তাই whitespace information token sequence-এর মধ্যে encode করা হতে পারে।

---

# 28. SentencePiece Example

Input:

```text
I love Python
```

Conceptually:

```text
▁I
▁love
▁Python
```

তারপর এগুলো vocabulary IDs-তে convert হয়।

---

# 29. Tokenizer Vocabulary কী?

Tokenizer-এর vocabulary হলো:

```text
Token → Integer ID
```

mapping।

Example:

```text
"hello" → 100
"world" → 205
"ing" → 301
```

Actual IDs arbitrary এবং model-specific।

---

# 30. Vocabulary তৈরি হয় কীভাবে?

Tokenizer training-এর মাধ্যমে:

```text
Large Corpus
     ↓
Statistics
     ↓
Subword Learning
     ↓
Vocabulary
     ↓
Tokenizer Model
```

---

# 31. Vocabulary Size

ধরি:

```text
vocab_size = 30,000
```

মানে tokenizer-এর vocabulary-তে প্রায় 30k token entries থাকতে পারে।

Special tokens-সহ exact count tokenizer configuration-এর উপর নির্ভর করে।

---

# 32. Vocabulary বড় হলে?

Advantages:

```text
More words/subwords represented directly
Potentially fewer tokens
```

কিন্তু:

```text
Embedding matrix বড়
Model input/output vocabulary বড়
Memory ↑
```

---

# 33. Vocabulary ছোট হলে?

Advantages:

```text
Smaller vocabulary
Smaller embedding/output matrix
```

কিন্তু:

```text
More splitting
More tokens
Longer sequences
```

---

# 34. Tokenizer Design Trade-off

```text
             Vocabulary
                 │
       ┌─────────┴─────────┐
       ↓                   ↓
    Smaller              Larger
       │                   │
More subwords        Fewer tokens
       │                   │
Longer sequence      Larger vocab
       │                   │
Attention cost       More parameters
```

এটা LLM engineering-এর important concept।

---

# 35. Tokenizer Training Corpus

ভালো tokenizer train করতে representative corpus দরকার।

যদি target language:

```text
English
```

হয়:

```text
English corpus
```

প্রচুর থাকা দরকার।

Bangla model হলে:

```text
Bangla corpus
```

ভালোভাবে represent করা দরকার।

---

# 36. Domain-specific Tokenizer

ধরি তুমি medical LLM বানাচ্ছো।

General tokenizer:

```text
medical terminology
```

কে অনেক pieces-এ ভাগ করতে পারে।

Domain corpus দিয়ে tokenizer training করলে:

```text
medical terms
```

আরও efficient tokenization পেতে পারে।

---

# 37. Code Tokenization

Code-এর ক্ষেত্রেও tokenizer গুরুত্বপূর্ণ।

Example:

```python
def calculate_total(price, tax):
    return price + tax
```

এখানে tokens হতে পারে:

```text
def
calculate
_
total
(
price
,
tax
)
:
return
...
```

Actual tokenizer অনুযায়ী segmentation ভিন্ন হতে পারে।

---

# 38. Programming Language Tokenization বনাম LLM Tokenization

Compiler tokenizer:

```text
keyword
identifier
operator
literal
```

এগুলো language grammar-এর ভিত্তিতে tokenize করে।

LLM tokenizer:

```text
subword/byte/token units
```

ব্যবহার করে।

তাই:

```text
Compiler Tokenizer
≠
LLM Tokenizer
```

---

# 39. Tokenizer এবং Context Window

ধরি:

```text
Context = 4096 tokens
```

Input:

```text
3000 words
```

এটা automatically 3000 tokens হবে না।

হতে পারে:

```text
3500 tokens
```

অথবা:

```text
5000 tokens
```

language/tokenizer-এর উপর নির্ভর করে।

---

# 40. Token Budget

LLM application-এ অনেক সময়:

```text
Input Tokens
+
Output Tokens
=
Total Token Usage
```

ধরা হয়।

উদাহরণ:

```text
Input = 1000 tokens
Output = 500 tokens

Total ≈ 1500 tokens
```

API/provider-এর accounting rules model-specific হতে পারে।

---

# 41. AI Writing Platform-এ Token Budget

ধরি user একটি বড় document পাঠালো।

```text
Document
 ↓
Tokenizer
 ↓
50,000 tokens
```

কিন্তু model-এর context:

```text
32,000 tokens
```

তাহলে পুরো document একসাথে process করা যাবে না।

---

# 42. তখন কী করবে?

Chunking:

```text
Document
 ↓
Chunk 1
Chunk 2
Chunk 3
Chunk 4
 ↓
Process
 ↓
Combine
```

এখানে tokenizer knowledge খুব গুরুত্বপূর্ণ।

---

# 43. Token-based Chunking

Character-based:

```text
5000 characters
```

Word-based:

```text
1000 words
```

Token-based:

```text
1000 tokens
```

LLM systems-এ token-based chunking অনেক সময় বেশি predictable।

---

# 44. Overflow

Tokenizer ব্যবহার করে model input-এর maximum length control করা যায়।

Hugging Face example:

```python
inputs = tokenizer(
    text,
    truncation=True,
    max_length=512
)
```

এখানে text 512-token limit-এর মধ্যে truncate করা হতে পারে।

---

# 45. Padding

Batch processing-এ:

```text
I love AI
I love natural language processing
```

length আলাদা।

Padding:

```text
I love AI [PAD] [PAD]

I love natural language processing
```

তারপর:

```text
attention_mask
```

padding positions ignore করতে সাহায্য করে।

---

# 46. Truncation + Padding

একসাথে:

```python
inputs = tokenizer(
    texts,
    padding=True,
    truncation=True,
    max_length=512,
    return_tensors="pt"
)
```

Output সাধারণত:

```text
input_ids
attention_mask
```

সহ model-specific fields থাকতে পারে।

---

# 47. Batch Tokenization

একটি text:

```python
tokenizer(
    "I love Python."
)
```

অনেকগুলো:

```python
tokenizer(
    [
        "I love Python.",
        "I love NLP."
    ],
    padding=True,
    return_tensors="pt"
)
```

এতে batch processing করা যায়।

---

# 48. Attention Mask-এর সাথে Tokenizer

Example:

```text
Tokens:

I
love
AI
[PAD]
[PAD]
```

Mask:

```text
1
1
1
0
0
```

Model বুঝতে পারে:

```text
1 → actual input
0 → padding
```

---

# 49. Token Type IDs

BERT-style models-এ token type/segment IDs থাকতে পারে।

Example:

```text
Sentence A
+
Sentence B
```

Conceptually:

```text
A → 0
A → 0
A → 0

B → 1
B → 1
```

সব modern Transformer model token type IDs ব্যবহার করে না।

---

# 50. Offset Mapping

Advanced tokenizer feature:

```text
offset_mapping
```

এটি token-এর original text-এর character span জানাতে পারে।

Example:

```text
"Hello world"
```

Conceptually:

```text
Hello → (0,5)
world → (6,11)
```

এটি NER, highlighting, text span mapping-এর জন্য useful।

---

# 51. কেন Offset Mapping গুরুত্বপূর্ণ?

ধরি model detect করল:

```text
Microsoft
```

NER result token-level।

UI-তে user-এর original text-এ highlight করতে হবে:

```text
Microsoft announced...
^^^^^^^^^
```

Token → character position mapping দরকার।

---

# 52. AI Writing Platform-এ Offset Mapping

তোমার system:

```text
User Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Analyzer
 ↓
Detected span
 ↓
Offset Mapping
 ↓
Frontend Highlight
```

এটা খুব practical।

---

# 53. Special Token Handling

Tokenizer কখনও automatically special tokens add করতে পারে।

Example BERT:

```text
[CLS] sentence [SEP]
```

Code:

```python
inputs = tokenizer(
    "I love NLP."
)
```

Tokenizer configuration অনুযায়ী special tokens automatically add হতে পারে।

---

# 54. `add_special_tokens`

Control করা যায়:

```python
tokenizer(
    text,
    add_special_tokens=True
)
```

অথবা:

```python
tokenizer(
    text,
    add_special_tokens=False
)
```

কোন setting ব্যবহার করবে তা model-এর expected input format-এর উপর নির্ভর করবে।

---

# 55. Encoding Pipeline

Complete:

```text
Raw Text
   ↓
Normalization
   ↓
Pre-tokenization / segmentation
   ↓
Subword Model
   ↓
Special Token Handling
   ↓
Token IDs
   ↓
Attention Mask
   ↓
Tensor
```

---

# 56. Decoding Pipeline

Reverse direction:

```text
Token IDs
   ↓
Tokens
   ↓
Post-processing
   ↓
Text
```

Code:

```python
text = tokenizer.decode(
    ids,
    skip_special_tokens=True
)
```

---

# 57. Encode-Decode Example

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)

text = "I love natural language processing."

encoded = tokenizer(
    text
)

print(encoded["input_ids"])

decoded = tokenizer.decode(
    encoded["input_ids"],
    skip_special_tokens=True
)

print(decoded)
```

Conceptually:

```text
Text
 ↓
IDs
 ↓
Text
```

---

# 58. Tokenizer Files

একটি trained tokenizer save করলে একাধিক configuration/model file থাকতে পারে।

Common examples include:

```text
tokenizer.json
tokenizer_config.json
special_tokens_map.json
vocab.txt
merges.txt
spiece.model
```

কোন files থাকবে তা tokenizer type-এর উপর নির্ভর করে।

---

# 59. BERT Tokenizer Files

Traditional BERT WordPiece tokenizer-এ:

```text
vocab.txt
```

খুব গুরুত্বপূর্ণ।

এতে token vocabulary থাকে।

---

# 60. BPE Tokenizer Files

BPE implementation-এ থাকতে পারে:

```text
vocab.json
merges.txt
```

বিশেষ করে GPT-2-style tokenizer ecosystem-এ এই ধরনের files historically common।

---

# 61. SentencePiece Files

SentencePiece model-এর জন্য:

```text
spiece.model
```

এর মতো model file থাকতে পারে।

---

# 62. Tokenizer Save/Load

Hugging Face:

```python
tokenizer.save_pretrained(
    "./my_tokenizer"
)
```

তারপর:

```python
tokenizer = AutoTokenizer.from_pretrained(
    "./my_tokenizer"
)
```

এভাবে tokenizer reuse করা যায়।

---

# 63. Tokenizer + Model Versioning

Production system-এ:

```text
Model Version
+
Tokenizer Version
```

compatible রাখতে হবে।

যেমন:

```text
Model v1
Tokenizer v1
```

এবং:

```text
Model v2
Tokenizer v2
```

arbitrary mixing করা উচিত নয়।

---

# 64. কেন Compatibility গুরুত্বপূর্ণ?

Model embedding matrix:

```text
ID 100 → specific learned vector
```

যদি tokenizer বদলে:

```text
ID 100 → completely different token
```

হয়ে যায়, তাহলে model-এর learned meaning নষ্ট হবে।

---

# 65. Tokenizer Drift

Production application-এ tokenizer change করলে:

```text
Old requests
New requests
```

এর tokenization behavior আলাদা হতে পারে।

তাই tokenizer update:

```text
Model deployment
```

এর সাথে carefully manage করতে হয়।

---

# 66. Tokenizer-এর Efficiency Measure

একটি useful metric:

$$
Tokens\ Per\ Word =
\frac{Number\ of\ Tokens}
{Number\ of\ Words}
$$

Example:

```text
100 words
120 tokens
```

তাহলে:

$$
1.2
$$

tokens per word।

এটা tokenizer efficiency বোঝার একটি rough measure, কিন্তু একমাত্র metric নয়।

---

# 67. Language-wise Efficiency

ধরি:

```text
English:
100 words → 120 tokens
```

Bangla:

```text
100 words → 250 tokens
```

এটা হতে পারে tokenizer-এর vocabulary/corpus suitability-এর difference-এর কারণে।

তাই multilingual model design-এ tokenizer quality গুরুত্বপূর্ণ।

---

# 68. Fertility

NLP tokenizer evaluation-এ একটি related concept:

**Fertility**

একটি word গড়ে কত tokens-এ split হচ্ছে।

Example:

```text
programming
 ↓
program + ming
```

fertility:

```text
2
```

Dataset level-এ average fertility measure করা যায়।

---

# 69. Tokenization Quality

শুধু কম tokens হলেই tokenizer ভালো—এটা ঠিক নয়।

Consider:

```text
Token Count
+
Coverage
+
Language Support
+
Rare Word Handling
+
Vocabulary Size
+
Downstream Performance
```

সব একসাথে দেখতে হয়।

---

# 70. Tokenizer Security

AI application-এ tokenizer security-ও relevant।

বিশেষ করে:

```text
Unicode
homoglyphs
zero-width characters
unusual whitespace
```

ইত্যাদি input behavior model analysis-কে affect করতে পারে।

তাই production text pipeline-এ normalization carefully design করতে হয়।

---

# 71. Unicode Normalization

একই visual text বিভিন্ন Unicode representation-এ থাকতে পারে।

তাই:

```text
Raw Unicode
 ↓
Normalization
 ↓
Tokenizer
```

কিছু systems-এ useful।

তবে normalization blindly করলে original text-এর meaningful distinctions নষ্ট হতে পারে।

---

# 72. Tokenization এবং Prompt Injection

Tokenizer নিজে prompt injection solve করে না।

Security architecture:

```text
Input
 ↓
Validation
 ↓
Prompt construction
 ↓
Model
```

Tokenizer শুধু text representation করে।

তাই:

```text
Tokenizer
≠
Security Layer
```

---

# 73. AI Writing Assistant-এর Complete Flow

এখন পুরো M02-এর অনেকগুলো topic connect করো:

```text
USER TEXT
   ↓
Normalization
   ↓
Sentence Segmentation
   ↓
SUBWORD TOKENIZER
   ↓
Token IDs
   ↓
Attention Mask
   ↓
Embeddings
   ↓
Positional Information
   ↓
Transformer
   ↓
Contextual Representation
   ↓
Generation / Analysis
```

---

# 74. Rewrite System

```text
Original Text
      ↓
Tokenizer
      ↓
GPT-style Model
      ↓
Generated Token IDs
      ↓
Decode
      ↓
Rewritten Text
```

---

# 75. Analyzer System

```text
Text
 ↓
Tokenizer
 ↓
BERT-style Encoder
 ↓
Contextual Embeddings
 ↓
Classifier / NER / Similarity
 ↓
Analysis
```

---

# 76. Text Transformation System

```text
Input Text
 ↓
T5-style Encoder
 ↓
Context
 ↓
Decoder
 ↓
Output Tokens
 ↓
Decode
 ↓
Transformed Text
```

---

# 77. BPE From Scratch — Mini Implementation

Educational version:

```python
from collections import Counter


corpus = [
    "low",
    "lower",
    "lowest",
    "low"
]


def get_pairs(tokens):
    pairs = Counter()

    for token_list in tokens:

        for i in range(len(token_list) - 1):

            pair = (
                token_list[i],
                token_list[i + 1]
            )

            pairs[pair] += 1

    return pairs
```

---

# 78. Initialize Characters

```python
tokens = [
    list(word)
    for word in corpus
]

print(tokens)
```

Conceptually:

```text
[
 ['l','o','w'],
 ['l','o','w','e','r'],
 ['l','o','w','e','s','t'],
 ['l','o','w']
]
```

---

# 79. Find Most Frequent Pair

```python
pairs = get_pairs(tokens)

best_pair = pairs.most_common(1)[0][0]

print(best_pair)
```

Potential:

```text
('l', 'o')
```

---

# 80. Merge Pair

```python
def merge_pair(tokens, pair):

    merged = []

    i = 0

    while i < len(tokens):

        if (
            i < len(tokens) - 1
            and (tokens[i], tokens[i + 1]) == pair
        ):
            merged.append(
                tokens[i] + tokens[i + 1]
            )
            i += 2

        else:
            merged.append(
                tokens[i]
            )
            i += 1

    return merged
```

---

# 81. Apply Merge

```python
tokens = [
    merge_pair(word, best_pair)
    for word in tokens
]

print(tokens)
```

এখন:

```text
['l','o','w']
```

হয়ে যেতে পারে:

```text
['lo','w']
```

---

# 82. Repeat

BPE algorithm conceptually:

```python
for _ in range(num_merges):

    pairs = get_pairs(tokens)

    best_pair = pairs.most_common(1)[0][0]

    tokens = [
        merge_pair(word, best_pair)
        for word in tokens
    ]
```

এটি শুধুমাত্র educational demonstration।

Production tokenizer implementation-এর জন্য optimized libraries ব্যবহার করবে।

---

# 83. Real-world Tokenizer

Production:

```python
from transformers import AutoTokenizer
```

তারপর:

```python
tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)
```

এটাই practical approach।

---

# 84. Tokenizer Inspect

```python
text = "I am learning programming."

tokens = tokenizer.tokenize(text)

for token in tokens:
    print(token)
```

এতে model কীভাবে text ভাঙছে সেটা সরাসরি দেখতে পারবে।

---

# 85. Token IDs Inspect

```python
ids = tokenizer.convert_tokens_to_ids(
    tokens
)

for token, token_id in zip(tokens, ids):
    print(token, token_id)
```

Output conceptually:

```text
I          1045
am         2572
learning   ...
program    ...
##ming     ...
```

Exact values model-specific।

---

# 86. Token → ID → Embedding

```text
"program"
    ↓
Token
    ↓
1250
    ↓
Embedding Matrix
    ↓
Vector
```

এখানে:

```text
Tokenizer
```

শুধু ID দেয়।

Vector তৈরি করে:

```text
Embedding Layer
```

---

# 87. One Critical Difference

```text
Tokenizer:
"programming"
↓
["program", "##ming"]
```

এটা representation।

কিন্তু:

```text
Embedding:
"program"
↓
[0.23, -0.51, ...]
```

এটা learned numerical representation।

---

# 88. M02.34 Interview Questions

### 1. What is BPE?

Frequent adjacent symbol/subword pairs merge করে vocabulary শেখার subword tokenization method।

### 2. What is WordPiece?

Subword tokenization method associated with BERT-family models, which learns/selects useful subword units based on a likelihood-oriented objective.

### 3. What is SentencePiece?

Raw text-এর উপর subword tokenization করার framework, যা BPE বা Unigram-এর মতো algorithms ব্যবহার করতে পারে।

### 4. BPE vs Unigram?

BPE iterative merge-based; Unigram starts with candidate pieces and removes less useful pieces based on probabilistic modeling.

### 5. Is SentencePiece an algorithm?

Strictly speaking, SentencePiece হলো framework/toolkit; এটি BPE বা Unigram model ব্যবহার করতে পারে।

### 6. Why do LLMs use subword tokenization?

Vocabulary manageable রাখা এবং rare/unseen words represent করার জন্য।

### 7. What is tokenizer vocabulary?

Token-to-ID mapping-এর collection।

### 8. What is `[UNK]`?

Unknown token।

### 9. Why does tokenizer affect context length?

কারণ model context tokens দিয়ে measure করে, words দিয়ে নয়।

### 10. Why must tokenizer and model be compatible?

কারণ token IDs model-এর learned embedding/output vocabulary-এর সাথে directly connected।

---

# 89. Advanced Theory Questions

নিজে answer করার চেষ্টা করো:

1. BPE কীভাবে vocabulary তৈরি করে?
2. কেন BPE frequent pair merge করে?
3. BPE এবং WordPiece-এর main conceptual difference কী?
4. SentencePiece কেন useful?
5. SentencePiece এবং BPE-এর relationship কী?
6. Unigram কীভাবে vocabulary তৈরি করে?
7. Tokenizer vocabulary বড়/ছোট হলে কী trade-off হয়?
8. Token count কেন inference cost affect করে?
9. Tokenizer কীভাবে context window-এর সাথে সম্পর্কিত?
10. Offset mapping কেন NER/highlighting-এর জন্য useful?
11. Tokenizer এবং embedding layer-এর relationship কী?
12. কেন arbitrary tokenizer দিয়ে pretrained model চালানো যায় না?
13. multilingual tokenizer-এর efficiency কেন language অনুযায়ী পরিবর্তিত হয়?
14. token এবং morpheme-এর difference কী?
15. tokenizer training এবং tokenization-এর difference কী?

---

# 90. Practical Task

একটি paragraph নাও:

```text
Artificial intelligence is changing the way people work, learn, and communicate.
```

তার জন্য বের করো:

```text
1. Words
2. Tokens
3. Token IDs
4. Token/word ratio
5. Special tokens
6. Attention mask
```

তারপর:

```text
Tokenizer
   ↓
IDs
   ↓
Decode
```

করো এবং original-এর সাথে compare করো।

---

# 91. M02.34 Completion Checklist

```text
☑ BPE from scratch concept
☑ Pair frequency
☑ BPE merge
☑ BPE vocabulary
☑ BPE advantages
☑ BPE limitations
☑ WordPiece
☑ ## continuation
☑ WordPiece unknown token
☑ BPE vs WordPiece
☑ Unigram Language Model
☑ Unigram segmentation
☑ BPE vs Unigram
☑ SentencePiece
☑ SentencePiece vs BPE
☑ SentencePiece BPE
☑ SentencePiece Unigram
☑ Whitespace marker
☑ Vocabulary
☑ Vocabulary size
☑ Vocabulary trade-off
☑ Tokenizer training
☑ Tokenization
☑ Tokenizer corpus
☑ Domain tokenizer
☑ Code tokenization
☑ Context window
☑ Token budget
☑ Token-based chunking
☑ Padding
☑ Truncation
☑ Batch tokenization
☑ Attention mask
☑ Token type IDs
☑ Offset mapping
☑ Special tokens
☑ Encode
☑ Decode
☑ Tokenizer files
☑ vocab.txt
☑ vocab.json
☑ merges.txt
☑ spiece.model
☑ Save/load tokenizer
☑ Model-tokenizer compatibility
☑ Tokenization efficiency
☑ Fertility
☑ Unicode considerations
☑ AI Writing Assistant connection
☑ BPE implementation
☑ Hugging Face tokenizer
☑ Interview questions
☑ Theory questions
☑ Practical task
```

---

# 🧠 Final Mental Model

এখন পুরো tokenizer system-টা এভাবে মনে রাখো:

```text
                         RAW TEXT
                            │
                            ▼
                       NORMALIZATION
                            │
                            ▼
                     SUBWORD TOKENIZER
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
             BPE        WordPiece       Unigram
             │              │              │
             └──────────────┼──────────────┘
                            ▼
                         TOKENS
                            │
                            ▼
                         TOKEN IDs
                            │
                 ┌──────────┴──────────┐
                 ▼                     ▼
           Attention Mask        Token Type IDs
                 │
                 └──────────┬──────────┘
                            ▼
                       EMBEDDING
                            │
                            ▼
                  POSITION INFORMATION
                            │
                            ▼
                       TRANSFORMER
                            │
                            ▼
                          LOGITS
                            │
                            ▼
                      GENERATED IDs
                            │
                            ▼
                         DECODE
                            │
                            ▼
                       FINAL TEXT
```

### সবচেয়ে গুরুত্বপূর্ণ ৫টি line:

```text
BPE       → Merge frequent pairs
WordPiece → BERT-associated subword method
Unigram   → Probability-based vocabulary/segmentation
SentencePiece → Raw-text subword framework
Tokenizer → Text ↔ Token IDs
```

**M02.34 complete.**

----
# M02.35 — Subword Tokenization Implementation with Hugging Face

M02.34-এ আমরা BPE, WordPiece, Unigram, SentencePiece, vocabulary, token IDs, padding, truncation, offset mapping ইত্যাদি শিখেছি।

এখন M02.35-এ আমরা এগুলো **বাস্তবে code দিয়ে ব্যবহার** করব।

আজকের লক্ষ্য:

```text
Text
 ↓
Tokenizer Load
 ↓
Tokenize
 ↓
Token IDs
 ↓
Attention Mask
 ↓
Special Tokens
 ↓
Padding / Truncation
 ↓
Batch Encoding
 ↓
Decode
 ↓
Offset Mapping
 ↓
Transformer Input
```

---

# 1. Hugging Face কী?

Hugging Face হলো NLP/ML ecosystem-এর একটি গুরুত্বপূর্ণ platform/library ecosystem।

বিশেষ করে:

```text
Transformers
Tokenizers
Datasets
Accelerate
```

ইত্যাদি tools দিয়ে pretrained NLP/LLM models নিয়ে কাজ করা যায়।

আমাদের আজকের মূল focus:

```python
from transformers import AutoTokenizer
```

---

# 2. AutoTokenizer

`AutoTokenizer` model-এর configuration দেখে উপযুক্ত tokenizer automatically load করতে পারে।

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "bert-base-uncased"
)
```

এখন:

```text
tokenizer
```

হলো trained tokenizer object।

---

# 3. প্রথম Text Tokenization

```python
text = "I love learning NLP."

tokens = tokenizer.tokenize(text)

print(tokens)
```

Conceptually output হতে পারে:

```text
['i', 'love', 'learning', 'nl', '##p', '.']
```

**Exact output tokenizer/model version-এর উপর নির্ভর করতে পারে।**

---

# 4. `tokenize()` কী করে?

```python
tokenizer.tokenize(text)
```

শুধু text-কে token pieces-এ ভাগ করে।

এটি এখনো:

```text
Token → ID
```

করেনি।

---

# 5. Tokens থেকে IDs

```python
ids = tokenizer.convert_tokens_to_ids(
    tokens
)

print(ids)
```

Conceptually:

```text
Tokens
 ↓
['i', 'love', 'learning']
 ↓
IDs
 ↓
[1045, 2293, ...]
```

Exact IDs model-specific।

---

# 6. Text → IDs একসাথে

আরও সহজ:

```python
encoded = tokenizer.encode(
    text
)

print(encoded)
```

এটি সাধারণত special tokens-সহ encoded IDs return করতে পারে।

---

# 7. `encode()` বনাম `tokenize()`

| Method                    | কাজ           |
| ------------------------- | ------------- |
| `tokenize()`              | Text → Tokens |
| `convert_tokens_to_ids()` | Tokens → IDs  |
| `encode()`                | Text → IDs    |
| `decode()`                | IDs → Text    |

Mental model:

```text
Text
 ↓
tokenize()
 ↓
Tokens
 ↓
convert_tokens_to_ids()
 ↓
IDs
```

অথবা:

```text
Text
 ↓
encode()
 ↓
IDs
```

---

# 8. Recommended API — `tokenizer()`

Modern Hugging Face code-এ সাধারণত:

```python
inputs = tokenizer(
    text
)
```

ব্যবহার করবে।

Example:

```python
inputs = tokenizer(
    "I love NLP."
)

print(inputs)
```

Output-এ সাধারণত থাকতে পারে:

```text
input_ids
attention_mask
```

Model অনুযায়ী আরও fields থাকতে পারে।

---

# 9. `input_ids`

এটাই model-এর primary token representation।

Example:

```text
"I love NLP"
```

↓

```text
[101, 1045, 2293, ..., 102]
```

এগুলো integer token IDs।

---

# 10. `attention_mask`

Example:

```text
input_ids:

[101, 1045, 2293, 102]

attention_mask:

[1, 1, 1, 1]
```

এখানে:

```text
1 → actual token
0 → padding
```

---

# 11. Special Tokens

BERT-style tokenizer-এ:

```text
[CLS]
[SEP]
```

এর মতো special tokens থাকতে পারে।

Conceptually:

```text
Original:

I love NLP.

Tokenized:

[CLS] I love NLP . [SEP]
```

---

# 12. Special Token IDs

দেখতে পারো:

```python
print(tokenizer.cls_token)
print(tokenizer.sep_token)

print(tokenizer.cls_token_id)
print(tokenizer.sep_token_id)
```

---

# 13. সব Special Tokens

```python
print(tokenizer.special_tokens_map)
```

এতে model-এর configured special tokens সম্পর্কে ধারণা পাওয়া যাবে।

---

# 14. Special Tokens ছাড়া

```python
tokens = tokenizer(
    text,
    add_special_tokens=False
)

print(tokens)
```

এখন `[CLS]`, `[SEP]` automatically যোগ নাও হতে পারে।

---

# 15. কেন Special Tokens দরকার?

Model architecture অনুযায়ী special tokens বিভিন্ন কাজ করতে পারে।

BERT:

```text
[CLS] → sequence-level representation
[SEP] → sequence boundary
[MASK] → masked language modeling
[PAD] → padding
```

তবে exact use model-specific।

---

# 16. Decode

IDs থেকে text:

```python
encoded = tokenizer(
    text
)

decoded = tokenizer.decode(
    encoded["input_ids"]
)

print(decoded)
```

---

# 17. `skip_special_tokens`

যদি special tokens output-এ না চাই:

```python
decoded = tokenizer.decode(
    encoded["input_ids"],
    skip_special_tokens=True
)

print(decoded)
```

---

# 18. Full Round Trip

```python
text = "I love learning NLP."

encoded = tokenizer(text)

ids = encoded["input_ids"]

decoded = tokenizer.decode(
    ids,
    skip_special_tokens=True
)

print("Original:", text)
print("IDs:", ids)
print("Decoded:", decoded)
```

Mental model:

```text
Original Text
     ↓
Tokenizer
     ↓
IDs
     ↓
Tokenizer
     ↓
Decoded Text
```

---

# 19. Batch Tokenization

একসাথে multiple text:

```python
texts = [
    "I love Python.",
    "I love NLP.",
    "Transformers are powerful."
]

encoded = tokenizer(
    texts
)

print(encoded)
```

এটা batch processing-এর foundation।

---

# 20. Padding কেন দরকার?

ধরি:

```text
Sentence 1 → 4 tokens
Sentence 2 → 7 tokens
Sentence 3 → 5 tokens
```

একটি tensor তৈরি করতে same sequence length দরকার হতে পারে।

তাই:

```text
4 → 7
5 → 7
7 → 7
```

padding করা হয়।

---

# 21. Dynamic Padding

```python
encoded = tokenizer(
    texts,
    padding=True
)
```

এতে batch-এর longest sequence অনুযায়ী padding হতে পারে।

Conceptually:

```text
[1,2,3,4,0,0]
[1,2,3,4,5,6]
[1,2,3,4,5,0]
```

---

# 22. `padding="max_length"`

```python
encoded = tokenizer(
    texts,
    padding="max_length",
    max_length=20
)
```

সব sequence:

```text
20 tokens
```

length-এর হবে।

---

# 23. Dynamic vs Fixed Padding

### Dynamic

```python
padding=True
```

Batch-এর longest sequence পর্যন্ত pad।

### Fixed

```python
padding="max_length"
max_length=512
```

সব sequence 512 পর্যন্ত।

---

# 24. Truncation

Text অনেক বড় হলে:

```python
encoded = tokenizer(
    text,
    truncation=True,
    max_length=128
)
```

এতে 128-token limit-এর বাইরে অংশ truncate হতে পারে।

---

# 25. Padding + Truncation

Production NLP code-এ common pattern:

```python
encoded = tokenizer(
    texts,
    padding=True,
    truncation=True,
    max_length=512
)
```

---

# 26. PyTorch Tensor

PyTorch ব্যবহার করলে:

```python
encoded = tokenizer(
    texts,
    padding=True,
    truncation=True,
    return_tensors="pt"
)
```

এখন output PyTorch tensors হিসেবে আসবে।

---

# 27. Tensor Shape

ধরি:

```text
batch_size = 3
max_length = 10
```

তাহলে:

```python
encoded["input_ids"].shape
```

হতে পারে:

```text
torch.Size([3, 10])
```

অর্থাৎ:

```text
(B, L)
```

---

# 28. Transformer Input Flow

```text
Text
 ↓
Tokenizer
 ↓
input_ids
 ↓
Embedding
 ↓
(B, L, D)
 ↓
Transformer
```

Tokenizer-এর output সাধারণত:

```text
(B, L)
```

Embedding-এর output:

```text
(B, L, D)
```

---

# 29. Attention Mask Shape

সাধারণভাবে:

```text
attention_mask
```

এর shape:

```text
(B, L)
```

থাকতে পারে।

Example:

```text
input_ids:
[101, 2009, 2003, 102, 0, 0]

attention_mask:
[1,   1,    1,   1,   0, 0]
```

---

# 30. Token-to-ID Mapping

দেখতে পারো:

```python
tokens = tokenizer.tokenize(
    "I love NLP."
)

ids = tokenizer.convert_tokens_to_ids(
    tokens
)

for token, token_id in zip(tokens, ids):
    print(token, "→", token_id)
```

এটা tokenizer debugging-এর জন্য খুব useful।

---

# 31. ID-to-Token

Reverse:

```python
tokens = tokenizer.convert_ids_to_tokens(
    ids
)

print(tokens)
```

অর্থাৎ:

```text
IDs
 ↓
Tokens
```

---

# 32. ID-to-Text

```python
text = tokenizer.decode(
    ids
)

print(text)
```

এখানে tokenizer tokens reconstruct করে text বানায়।

---

# 33. Vocabulary Size

```python
print(tokenizer.vocab_size)
```

ধরি:

```text
30522
```

BERT-base-uncased-এর ক্ষেত্রে এটি commonly 30,522।

---

# 34. Vocabulary Inspect

```python
vocab = tokenizer.get_vocab()

print(len(vocab))
```

এখানে token → ID mapping পাওয়া যায়।

---

# 35. Specific Token-এর ID

```python
print(
    tokenizer.convert_tokens_to_ids("python")
)
```

---

# 36. Specific ID-এর Token

```python
token_id = 18750

print(
    tokenizer.convert_ids_to_tokens(
        token_id
    )
)
```

---

# 37. Offset Mapping

Advanced feature:

```python
encoded = tokenizer(
    text,
    return_offsets_mapping=True
)

print(
    encoded["offset_mapping"]
)
```

এটি token-এর original text-এর character span সম্পর্কে information দিতে পারে।

---

# 38. Offset Example

Text:

```text
"Hello world"
```

Conceptually:

```text
Hello → (0, 5)
world → (6, 11)
```

Special tokens-এর offset behavior tokenizer-specific হতে পারে।

---

# 39. Offset Mapping কেন দরকার?

ধরি model বললো:

```text
"Microsoft"
```

একটি entity।

Frontend-এ highlight করতে চাই:

```text
Microsoft announced a new product.
^^^^^^^^^
```

তখন:

```text
Token
 ↓
Offset
 ↓
Original Character Span
```

দরকার।

---

# 40. NER + Tokenizer

Complete pipeline:

```text
Text
 ↓
Tokenizer
 ↓
Subword Tokens
 ↓
Model
 ↓
Token Classification
 ↓
Entity Labels
 ↓
Offset Mapping
 ↓
Original Text Highlight
```

---

# 41. Word-Level Mapping Problem

ধরি:

```text
playing
```

tokenizer করে:

```text
play
##ing
```

NER model-এর prediction token-level হতে পারে।

কিন্তু user-এর text-এ:

```text
playing
```

একটি word।

তাই:

```text
Subword
 ↓
Word
```

alignment দরকার।

---

# 42. `is_split_into_words`

যদি আগে থেকেই words split করা থাকে:

```python
words = [
    "I",
    "love",
    "programming"
]

encoded = tokenizer(
    words,
    is_split_into_words=True
)
```

এটি token-to-word alignment tasks-এ useful হতে পারে।

---

# 43. Word IDs

Fast tokenizer হলে:

```python
word_ids = encoded.word_ids()

print(word_ids)
```

Conceptually:

```text
I          → 0
love       → 1
program    → 2
##ming     → 2
```

অর্থাৎ:

```text
program
##ming
```

দুটো একই original word-এর অংশ।

---

# 44. NER Alignment

ধরি word labels:

```text
programming → O
```

Subword:

```text
program
##ming
```

দুই token-এর label mapping করতে হবে।

এখানে:

```text
word_ids()
```

খুব useful।

---

# 45. Fast Tokenizer

Hugging Face-এর fast tokenizers সাধারণত Rust-based `tokenizers` library ব্যবহার করে এবং অনেক preprocessing/alignment operation দ্রুত করতে পারে।

Check:

```python
print(tokenizer.is_fast)
```

Output:

```text
True
```

হতে পারে।

---

# 46. Why Fast Tokenizer?

Benefits:

```text
☑ Faster tokenization
☑ Offset mapping
☑ Word alignment
☑ Batch processing
```

বিশেষ করে production NLP pipeline-এ useful।

---

# 47. Tokenizer Configuration

দেখতে পারো:

```python
print(tokenizer)
```

এবং:

```python
print(
    tokenizer.name_or_path
)
```

---

# 48. Model-এর সাথে Tokenizer

সবচেয়ে গুরুত্বপূর্ণ rule:

```text
Pretrained Model
        +
Compatible Tokenizer
```

Example:

```python
from transformers import (
    AutoTokenizer,
    AutoModel
)

name = "bert-base-uncased"

tokenizer = AutoTokenizer.from_pretrained(name)

model = AutoModel.from_pretrained(name)
```

এখানে একই model family-এর compatible tokenizer ব্যবহার করা হচ্ছে।

---

# 49. Model Input

```python
inputs = tokenizer(
    "I love NLP.",
    return_tensors="pt"
)

outputs = model(**inputs)
```

এখানে:

```text
**inputs
```

এর মাধ্যমে:

```text
input_ids
attention_mask
```

ইত্যাদি model-এর expected arguments হিসেবে যায়।

---

# 50. Output Shape

BERT-style encoder-এর output সাধারণত:

```text
last_hidden_state
```

এর shape:

```text
(B, L, H)
```

যেখানে:

```text
B = batch size
L = sequence length
H = hidden size
```

BERT-base-এ hidden size commonly:

```text
768
```

---

# 51. Tokenizer → Model

Complete:

```text
"I love NLP."
      ↓
Tokenizer
      ↓
input_ids
      ↓
attention_mask
      ↓
BERT
      ↓
Hidden States
```

এটাই M02-এর অনেকগুলো topic একসাথে connect করছে।

---

# 52. GPT-style Model-এর ক্ষেত্রেও একই Concept

GPT-style model:

```text
Prompt
 ↓
Tokenizer
 ↓
input_ids
 ↓
Embedding
 ↓
Positional Information
 ↓
Causal Transformer
 ↓
Logits
 ↓
Next Token
```

Difference হলো model architecture এবং tokenizer configuration।

---

# 53. GPT Tokenizer Example

Genericভাবে:

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained(
    "gpt2"
)

text = "I love programming."

tokens = tokenizer.tokenize(text)

print(tokens)
```

GPT-2 tokenizer-এর tokenization BERT WordPiece-এর মতো নয়।

এখানে historically GPT-2-style byte-level BPE ব্যবহৃত হয়।

---

# 54. BERT vs GPT Tokenizer

Simplified:

```text
BERT
 ↓
WordPiece-style tokenization
```

```text
GPT-2
 ↓
Byte-level BPE
```

Modern model families-এর tokenizer implementation ভিন্ন হতে পারে, তাই model documentation/configuration follow করা উচিত।

---

# 55. Tokenizer Training বনাম Pretrained Tokenizer

তুমি সাধারণত দুইভাবে কাজ করতে পারো।

### Option 1

Pretrained tokenizer:

```python
AutoTokenizer.from_pretrained(...)
```

### Option 2

নিজের tokenizer train:

```text
Custom Corpus
 ↓
Tokenizer Training
 ↓
Vocabulary
 ↓
Tokenizer
```

---

# 56. কখন নিজের Tokenizer দরকার?

যদি তুমি:

```text
☑ নতুন language model
☑ domain-specific model
☑ specialized corpus
☑ unusual vocabulary
```

train করো, custom tokenizer বিবেচনা করতে পারো।

কিন্তু pretrained model fine-tuning-এর সময় সাধারণত model-এর original tokenizer ব্যবহার করাই সঠিক।

---

# 57. AI Writing Platform-এ Tokenizer Service

Django backend-এর architecture:

```text
React
  ↓
Django API
  ↓
Text Service
  ↓
Tokenizer
  ↓
Model
  ↓
Generation / Analysis
  ↓
Tokenizer Decode
  ↓
Response
```

---

# 58. Long Document Processing

ধরি user দিয়েছে:

```text
100-page document
```

Tokenizer:

```text
100 pages
 ↓
80,000 tokens
```

Model:

```text
Context limit = 32,000 tokens
```

তখন:

```text
80k tokens
 ↓
Chunking
 ↓
Chunk 1
Chunk 2
Chunk 3
...
 ↓
Process separately
 ↓
Combine
```

---

# 59. Token-based Chunking Example

```python
encoded = tokenizer(
    text,
    add_special_tokens=False
)

input_ids = encoded["input_ids"]

chunk_size = 512

chunks = [
    input_ids[i:i + chunk_size]
    for i in range(
        0,
        len(input_ids),
        chunk_size
    )
]
```

এটি basic educational implementation।

Production system-এ overlap, sentence boundaries, special tokens ইত্যাদি carefully handle করতে হবে।

---

# 60. Chunk Overlap

ধরি:

```text
Chunk 1:
tokens 0–500

Chunk 2:
tokens 450–950
```

Overlap:

```text
450–500
```

কেন?

Context continuity রাখার জন্য।

```text
Chunk 1
────────────
       ↘ overlap
          ────────────
          Chunk 2
```

---

# 61. Tokenizer Statistics

একটি document-এর জন্য:

```python
encoded = tokenizer(
    text,
    add_special_tokens=False
)

token_count = len(
    encoded["input_ids"]
)

print(token_count)
```

এটা AI application-এ খুব useful।

---

# 62. Token Counter Feature

তুমি frontend-এ দেখাতে পারো:

```text
Words: 1,250
Characters: 7,420
Tokens: 1,680
```

এখানে token count tokenizer-এর মাধ্যমে calculate করা যায়।

---

# 63. Cost Estimation

API-based model হলে token count-এর ভিত্তিতে usage/cost estimate করা যায়।

Conceptually:

$$
Cost =
InputTokens \times InputRate
+
OutputTokens \times OutputRate
$$

Actual pricing provider/model-specific।

---

# 64. Tokenizer Cache

Production application-এ tokenizer বারবার load করা উচিত নয়।

Bad:

```python
def process(text):

    tokenizer = AutoTokenizer.from_pretrained(
        "model"
    )

    return tokenizer(text)
```

প্রতিবার load করলে unnecessary overhead হবে।

Better architecture:

```text
Application Start
       ↓
Load Tokenizer Once
       ↓
Reuse
```

---

# 65. Django Service Pattern

Conceptually:

```python
class NLPService:

    def __init__(self):
        self.tokenizer = AutoTokenizer.from_pretrained(
            "bert-base-uncased"
        )

    def tokenize(self, text):
        return self.tokenizer(
            text,
            return_tensors="pt"
        )
```

তারপর application lifecycle অনুযায়ী service reuse করতে পারো।

---

# 66. Tokenizer Error Handling

Possible issues:

```text
☑ Model not found
☑ Wrong tokenizer
☑ Invalid input
☑ Sequence too long
☑ Missing padding token
☑ Tensor shape mismatch
☑ CPU/GPU mismatch
```

Production application-এ এগুলো handle করতে হবে।

---

# 67. Padding Token Issue

কিছু decoder-only model-এর ক্ষেত্রে:

```text
pad_token
```

preconfigured নাও থাকতে পারে।

কখনো model-specificভাবে:

```python
tokenizer.pad_token = tokenizer.eos_token
```

এর মতো configuration দেখা যায়।

**এটি universal rule নয়।** Model documentation অনুযায়ী করতে হবে।

---

# 68. Common Mistake #1

ভুল:

```text
BERT tokenizer
+
GPT model
```

শুধু model চলবে মনে করা।

সবসময়:

```text
Compatible tokenizer
+
Compatible model
```

ব্যবহার করবে।

---

# 69. Common Mistake #2

সব text lowercase করা।

BERT uncased model:

```text
"I Love NLP"
```

lowercase behavior রাখতে পারে।

কিন্তু অন্য model-এর tokenizer-এর জন্য manually lowercase করা ঠিক নাও হতে পারে।

**Tokenizer/model-এর own preprocessing follow করো।**

---

# 70. Common Mistake #3

Blindly truncate করা।

```python
truncation=True
```

দিয়ে long document-এর গুরুত্বপূর্ণ অংশ হারিয়ে যেতে পারে।

AI writing platform-এ better:

```text
Long Document
 ↓
Smart Chunking
 ↓
Process
 ↓
Merge
```

---

# 71. Common Mistake #4

Token ≠ Word

Example:

```text
unbelievable
```

হতে পারে:

```text
un
believ
able
```

তাই:

```python
len(text.split())
```

এবং:

```python
len(tokenizer.encode(text))
```

এক জিনিস নয়।

---

# 72. Practical Exercise 1

এই text ব্যবহার করো:

```text
Artificial intelligence is transforming modern education.
```

Calculate:

```text
1. Tokens
2. Token IDs
3. Token count
4. Vocabulary IDs
5. Decoded text
```

---

# 73. Practical Exercise 2

৩টি text:

```python
texts = [
    "I love Python.",
    "I am learning NLP.",
    "Transformers are powerful."
]
```

করো:

```text
☑ Batch tokenization
☑ Padding
☑ Truncation
☑ PyTorch tensors
☑ input_ids shape
☑ attention_mask shape
```

---

# 74. Practical Exercise 3

একটি text-এর জন্য:

```python
return_offsets_mapping=True
```

ব্যবহার করো।

তারপর:

```text
token
start
end
```

print করো।

---

# 75. Practical Exercise 4

এই word-এর tokenization compare করো:

```text
playing
played
programming
unbelievable
internationalization
```

দেখো:

```text
BERT tokenizer
vs
GPT-2 tokenizer
```

কীভাবে আলাদা segmentation হয়।

---

# 76. Practical Exercise 5 — Token Counter

একটি function বানাও:

```python
def count_tokens(text):
    ...
```

যা return করবে:

```text
{
    "characters": ...,
    "words": ...,
    "tokens": ...
}
```

এটা তোমার future AI writing platform-এর একটি real feature হতে পারে।

---

# 77. Interview Questions

### Q1. `tokenize()` কী return করে?

Token/subword strings।

### Q2. `encode()` কী করে?

Text-কে token IDs-এ encode করে।

### Q3. `decode()` কী করে?

Token IDs থেকে text reconstruct করে।

### Q4. `input_ids` কী?

Model-এর input token IDs।

### Q5. `attention_mask` কী?

কোন positions valid input এবং কোনগুলো padding—তা indicate করতে ব্যবহৃত হয়।

### Q6. Padding কেন?

Batch-এর sequences একই length করার জন্য।

### Q7. Truncation কেন?

Maximum sequence length সীমার মধ্যে রাখতে।

### Q8. Offset mapping কী?

Token এবং original text-এর character positions-এর alignment information।

### Q9. Fast tokenizer কী?

High-performance tokenizer implementation, যা tokenization-এর পাশাপাশি alignment-related features দিতে পারে।

### Q10. Tokenizer এবং model compatible হওয়া কেন দরকার?

Model-এর vocabulary এবং token IDs learned parameters-এর সাথে aligned থাকতে হয়।

---

# 78. Advanced Interview Questions

1. BPE tokenizer কীভাবে vocabulary তৈরি করে?
2. WordPiece এবং BPE-এর difference কী?
3. SentencePiece কী?
4. Tokenizer vocabulary size model parameter count-কে কীভাবে affect করে?
5. Tokenization context window-কে কীভাবে affect করে?
6. Padding এবং truncation-এর difference কী?
7. `attention_mask` কেন দরকার?
8. `offset_mapping` NER-এ কেন গুরুত্বপূর্ণ?
9. Word-level labels-কে subword-level labels-এ কীভাবে map করবে?
10. `word_ids()` কী কাজে আসে?
11. Fast tokenizer কেন production-এ useful?
12. কেন tokenizer বদলালে pretrained model-এর performance নষ্ট হতে পারে?
13. Tokenizer এবং embedding layer-এর relationship কী?
14. Long-document processing-এ token-based chunking কেন useful?
15. Token count এবং word count কেন আলাদা?

---

# 79. Complete Tokenizer Architecture

এখন M02.34 + M02.35 একসাথে:

```text
                    RAW TEXT
                       │
                       ▼
                 NORMALIZATION
                       │
                       ▼
                PRE-TOKENIZATION
                       │
                       ▼
              SUBWORD TOKENIZER
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
         BPE       WordPiece      Unigram
          │            │            │
          └────────────┼────────────┘
                       ▼
                     TOKENS
                       │
                       ▼
                   TOKEN IDs
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
      Attention Mask       Special Tokens
             │
             ▼
          Tensor
             │
             ▼
        Transformer
             │
             ▼
       Hidden States / Logits
             │
             ▼
        Generated IDs
             │
             ▼
           Decode
             │
             ▼
         FINAL TEXT
```

---

# 80. AI Writing Assistant-এর জন্য গুরুত্বপূর্ণ

তোমার future platform-এর একটি request:

```text
POST /api/rewrite/
```

এলে backend:

```text
Request
 ↓
Validate Text
 ↓
Count Tokens
 ↓
Check Context Limit
 ↓
Chunk if Necessary
 ↓
Tokenizer
 ↓
Model
 ↓
Generated Token IDs
 ↓
Decode
 ↓
Quality / Meaning Checks
 ↓
Response
```

এখন তুমি বুঝতে পারছো কেন **Tokenizer শুধু ছোট একটা preprocessing step নয়**—LLM application architecture-এর core component।

---

# 81. M02.35 Completion Checklist

```text
☑ Hugging Face tokenizer
☑ AutoTokenizer
☑ from_pretrained()
☑ tokenize()
☑ convert_tokens_to_ids()
☑ encode()
☑ tokenizer()
☑ input_ids
☑ attention_mask
☑ Special tokens
☑ CLS
☑ SEP
☑ PAD
☑ MASK
☑ decode()
☑ skip_special_tokens
☑ Batch tokenization
☑ Dynamic padding
☑ Fixed padding
☑ Truncation
☑ PyTorch tensors
☑ Tensor shapes
☑ Vocabulary size
☑ Token ↔ ID
☑ ID ↔ Token
☑ Offset mapping
☑ Word alignment
☑ word_ids()
☑ is_split_into_words
☑ Fast tokenizer
☑ Model + tokenizer compatibility
☑ BERT tokenizer
☑ GPT-2 tokenizer
☑ Token counting
☑ Long document chunking
☑ Chunk overlap
☑ Token budget
☑ Tokenizer caching
☑ Production architecture
☑ AI writing platform connection
☑ Practical exercises
☑ Interview questions
```

## 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ ৭টি জিনিস

```text
1. tokenize()
   Text → Tokens

2. encode()
   Text → Token IDs

3. decode()
   Token IDs → Text

4. input_ids
   Model-এর token representation

5. attention_mask
   Valid token বনাম padding

6. offset_mapping
   Token → Original text position

7. Compatible Tokenizer + Model
   সবসময় একসাথে রাখতে হবে
```

**M02.35 complete.**


---
ঠিক আছে। তাহলে **M02.36 = Dense Representation**।
এটি M02.15-এর Word Embeddings এবং M02.34–35-এর Tokenization-এর সঙ্গে খুব গুরুত্বপূর্ণভাবে connected। আজ আমরা **dense representation কী, কেন দরকার, কীভাবে তৈরি হয়, sparse বনাম dense, embeddings, dimensions, similarity এবং Transformer-এ এর ভূমিকা** গভীরভাবে শিখব।

# M02.36 — Dense Representation

---

## 1. Dense Representation কী?

কম্পিউটার সরাসরি মানুষের ভাষার meaning বুঝতে পারে না। তাই text-কে numerical representation-এ convert করতে হয়।

**Dense Representation** হলো এমন একটি numerical representation যেখানে একটি object/token-কে তুলনামূলকভাবে **ছোট সংখ্যক continuous numerical values** দিয়ে represent করা হয় এবং সাধারণত vector-এর বেশিরভাগ element-ই non-zero।

উদাহরণ:

```text
cat
 ↓
[0.21, 0.73, -0.14, 0.56, 0.91]
```

এখানে:

```text
5-dimensional vector
```

এটাই dense vector।

---

# 2. কেন Dense Representation দরকার?

ধরি vocabulary:

```text
["cat", "dog", "car", "apple", "book"]
```

একটি traditional One-Hot representation:

```text
cat   → [1,0,0,0,0]
dog   → [0,1,0,0,0]
car   → [0,0,1,0,0]
```

এখানে সমস্যা:

```text
cat এবং dog
```

দুটো semanticভাবে related হলেও vector দেখে:

```text
[1,0,0,0,0]
[0,1,0,0,0]
```

তাদের similarity বোঝা যায় না।

Dense representation এই সমস্যা অনেকটা সমাধান করে।

```text
cat → [0.81, 0.32, 0.71, ...]
dog → [0.79, 0.35, 0.69, ...]
```

দুটো vector কাছাকাছি হতে পারে।

---

# 3. Sparse vs Dense

এটি খুব গুরুত্বপূর্ণ।

### Sparse Representation

```text
[0, 0, 0, 1, 0, 0, 0, 0, 0, 0]
```

বেশিরভাগ value:

```text
0
```

### Dense Representation

```text
[0.21, -0.54, 0.83, 0.17, -0.32]
```

বেশিরভাগ value non-zero।

---

# 4. One-Hot কেন Sparse?

ধরি vocabulary:

```text
100,000 words
```

One-hot representation:

```text
cat
```

হবে:

```text
[0,0,0,0,....,1,....,0]
```

Vector dimension:

```text
100,000
```

কিন্তু মাত্র একটি value:

```text
1
```

বাকি:

```text
99,999 → 0
```

তাই এটি sparse।

---

# 5. Dense Representation-এর Dimension

Dense vector:

```text
cat
 ↓
[0.12, 0.85, -0.44, 0.31]
```

dimension:

```text
4
```

আরেকটি:

```text
cat
 ↓
[0.12, 0.85, -0.44, 0.31, 0.72, ...]
```

dimension:

```text
100
```

অথবা:

```text
300
768
1024
1536
4096
```

ইত্যাদি হতে পারে।

Dimension model/embedding design-এর উপর নির্ভর করে।

---

# 6. Dense Vector কী Represent করে?

একটি গুরুত্বপূর্ণ বিষয়:

**Vector-এর প্রতিটি dimension সাধারণত সরাসরি একটি মানুষের বোঝার মতো feature নয়।**

যেমন:

```text
[0.21, 0.73, -0.12, 0.44]
```

এর অর্থ এমন নয়:

```text
dimension 1 = animal
dimension 2 = color
dimension 3 = size
dimension 4 = age
```

বাস্তব learned embeddings-এ information distributed থাকে।

একে বলা হয়:

**Distributed Representation**

---

# 7. Distributed Representation

একটি concept একটি মাত্র dimension-এ থাকে না।

বরং:

```text
Meaning
 ↓
Multiple dimensions
 ↓
Vector
```

উদাহরণ:

```text
dog
 ↓
[0.82, 0.31, -0.17, 0.66, ...]
```

এই পুরো vector-এর pattern-এ information distributed থাকতে পারে।

---

# 8. Dense Representation এবং Embedding

NLP-তে:

```text
Dense Representation
```

এবং:

```text
Embedding
```

অনেক ক্ষেত্রে closely related concepts।

সহজভাবে:

> Embedding হলো learned dense numerical representation।

Example:

```text
word
 ↓
embedding
 ↓
dense vector
```

---

# 9. Embedding Matrix

ধরি:

```text
vocab_size = 10,000
embedding_dim = 300
```

তাহলে embedding matrix:

```text
(10000, 300)
```

অর্থাৎ:

```text
10,000 tokens
×
300-dimensional vector
```

---

# 10. Embedding Lookup

ধরি:

```text
Token ID = 25
```

Embedding matrix:

```text
E
```

থেকে row 25 নেওয়া হলো:

```text
E[25]
```

এটি একটি dense vector।

```text
Token ID
   ↓
Embedding Matrix
   ↓
Vector
```

---

# 11. Python Example

NumPy দিয়ে:

```python
import numpy as np

vocab_size = 5
embedding_dim = 4

embedding_matrix = np.random.randn(
    vocab_size,
    embedding_dim
)

token_id = 2

vector = embedding_matrix[token_id]

print(vector)
```

Possible output:

```text
[ 0.31 -0.72  0.45  0.91]
```

---

# 12. Shape বুঝো

```python
print(embedding_matrix.shape)
```

Output:

```text
(5, 4)
```

মানে:

```text
5 tokens
4 dimensions
```

---

# 13. PyTorch Embedding

```python
import torch
import torch.nn as nn

embedding = nn.Embedding(
    num_embeddings=10000,
    embedding_dim=128
)
```

এখানে:

```text
10000 → vocabulary size
128   → embedding dimension
```

---

# 14. Token IDs

```python
token_ids = torch.tensor([
    [10, 25, 100]
])
```

Shape:

```text
(1, 3)
```

মানে:

```text
batch = 1
sequence length = 3
```

---

# 15. Embedding Lookup

```python
vectors = embedding(token_ids)

print(vectors.shape)
```

Output:

```text
torch.Size([1, 3, 128])
```

অর্থাৎ:

```text
(B, L)
 ↓
(B, L, D)
```

---

# 16. Dense Representation Pipeline

```text
Text
 ↓
Tokenizer
 ↓
Token IDs
 ↓
Embedding Lookup
 ↓
Dense Vectors
 ↓
Transformer
```

Example:

```text
"I love NLP"
```

↓

```text
[10, 25, 100]
```

↓

```text
[
 [0.2, 0.7, ...],
 [0.4, 0.1, ...],
 [0.8, 0.3, ...]
]
```

---

# 17. Dense Representation বনাম Tokenization

এ দুটোকে কখনো এক মনে করবে না।

### Tokenization

```text
Text
 ↓
Tokens
```

### Dense Representation

```text
Token IDs
 ↓
Dense vectors
```

Complete:

```text
Text
 ↓
Tokenizer
 ↓
Tokens
 ↓
Token IDs
 ↓
Embedding
 ↓
Dense Representation
```

---

# 18. Dense Representation বনাম One-Hot

| বিষয়              | One-Hot              | Dense                       |
| ----------------- | -------------------- | --------------------------- |
| Dimension         | খুব বড় হতে পারে      | তুলনামূলক ছোট               |
| Values            | mostly 0             | mostly non-zero             |
| Semantic relation | সরাসরি encode করে না | learned relation থাকতে পারে |
| Memory            | বেশি                 | কম                          |
| Learned           | সাধারণত না           | সাধারণত হ্যাঁ               |
| NLP Deep Learning | সীমিত                | অত্যন্ত গুরুত্বপূর্ণ        |

---

# 19. Dense Representation কীভাবে শেখে?

Embedding randomly initialize হতে পারে:

```text
cat
 ↓
[0.12, -0.44, 0.82]
```

Training-এর সময়:

```text
Prediction
 ↓
Loss
 ↓
Backpropagation
 ↓
Gradient
 ↓
Embedding Update
```

ফলে:

```text
Before:

cat → [0.12, -0.44, 0.82]

After:

cat → [0.71, 0.33, 0.59]
```

Embedding values training-এর মাধ্যমে learned হয়।

---

# 20. Word2Vec এবং Dense Representation

Word2Vec একটি classic example।

দুইটি প্রধান approach:

```text
CBOW
Skip-gram
```

### CBOW

```text
Context
 ↓
Target Word
```

### Skip-gram

```text
Target Word
 ↓
Context Words
```

Training শেষে word vectors পাওয়া যায়।

---

# 21. Similar Words

ধরি learned embeddings:

```text
cat
dog
tiger
car
bus
```

Embedding space-এ:

```text
cat ─── dog ─── tiger


car ─── bus
```

একই semantic neighborhood-এর vectors কাছাকাছি হতে পারে।

---

# 22. Cosine Similarity

দুই vector-এর similarity measure করতে cosine similarity ব্যবহার করা যায়:

$$
\cos(\theta)=
\frac{A\cdot B}
{\|A\|\|B\|}
$$

Example:

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([2, 4, 6])

similarity = np.dot(a, b) / (
    np.linalg.norm(a) *
    np.linalg.norm(b)
)

print(similarity)
```

Output:

```text
1.0
```

কারণ vector দুটো একই direction-এ।

---

# 23. Dense Representation-এর একটি গুরুত্বপূর্ণ বৈশিষ্ট্য

Dense vector-এর numerical values নিজেরা সবসময় human-interpretable নয়।

তুমি সাধারণত বলবে না:

```text
0.72 = intelligence
0.31 = formality
```

বরং:

```text
Vector pattern
 ↓
Learned representation
 ↓
Semantic/task information
```

---

# 24. Static Dense Representation

Classic embeddings:

```text
Word2Vec
GloVe
FastText
```

এগুলো সাধারণত static embedding।

একটি word-এর একটি মূল vector থাকে।

যেমন:

```text
bank
 ↓
একটি vector
```

কিন্তু সমস্যা:

```text
I went to the bank.

The river bank was beautiful.
```

দুই `bank`-এর meaning আলাদা।

Static embedding একই/প্রায় একই representation দিতে পারে।

---

# 25. Contextual Dense Representation

Modern Transformer models এই সমস্যা অনেক ভালোভাবে handle করে।

```text
I went to the bank.
```

এবং:

```text
The river bank was beautiful.
```

এখানে `bank`-এর contextual representation আলাদা হতে পারে।

```text
bank
 ↓
Context
 ↓
Contextual Vector
```

---

# 26. Static বনাম Contextual

```text
Static:

word
 ↓
one vector
```

```text
Contextual:

word + context
 ↓
context-dependent vector
```

এটি modern NLP-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 27. Transformer-এ Dense Representation

Transformer input:

```text
Token IDs
 ↓
Token Embeddings
 ↓
Positional Information
 ↓
Transformer
```

ধরি:

```text
input_ids shape:

(B, L)
```

Embedding:

```text
(B, L, D)
```

এখন প্রতিটি token একটি dense vector।

---

# 28. Transformer-এর ভিতরে Representation আরও পরিবর্তিত হয়

এখানে একটি গুরুত্বপূর্ণ distinction আছে।

Input embedding:

```text
Token
 ↓
Embedding
```

তারপর Transformer layers:

```text
Embedding
 ↓
Self-Attention
 ↓
FFN
 ↓
Layer 2
 ↓
...
 ↓
Final Hidden Representation
```

অর্থাৎ final representation শুধু original embedding নয়।

---

# 29. Hidden Representation

ধরি:

```text
"I love NLP"
```

Token embedding:

```text
I     → vector
love  → vector
NLP   → vector
```

Transformer-এর পরে:

```text
I     → contextual vector
love  → contextual vector
NLP   → contextual vector
```

এগুলোকে contextual hidden representations বলা যায়।

---

# 30. Dense Representation-এর স্তর

একটি modern NLP system-এ:

```text
                 TEXT
                  ↓
              TOKENIZER
                  ↓
              TOKEN IDs
                  ↓
          INPUT EMBEDDINGS
                  ↓
        POSITION INFORMATION
                  ↓
         TRANSFORMER LAYERS
                  ↓
       CONTEXTUAL REPRESENTATION
                  ↓
              TASK HEAD
```

---

# 31. Sentence Dense Representation

শুধু word নয়, পুরো sentence-কেও vector হিসেবে represent করা যায়।

Example:

```text
"I love Python."
```

↓

```text
[0.21, 0.73, -0.11, ...]
```

ধরি:

```text
384-dimensional vector
```

এটাকে sentence embedding বলা যেতে পারে।

---

# 32. Similar Sentence Detection

ধরি:

```text
A:
"I love programming."

B:
"I enjoy coding."
```

দুই sentence-এর dense embeddings:

```text
A → vector A
B → vector B
```

তারপর:

```text
Cosine Similarity
```

ব্যবহার করে semantic similarity estimate করা যায়।

---

# 33. AI Writing Assistant-এ ব্যবহার

তোমার future AI writing platform-এ dense representation অত্যন্ত গুরুত্বপূর্ণ।

ধরি user লিখলো:

```text
"Artificial intelligence is changing education."
```

System-এর rewritten version:

```text
"AI is transforming the education sector."
```

দুটো sentence-এর embeddings বের করে similarity compare করা যায়।

```text
Original
   ↓
Embedding
   ↓
Vector A

Rewrite
   ↓
Embedding
   ↓
Vector B

Vector A ↔ Vector B
   ↓
Semantic Similarity
```

এটি **meaning preservation-এর একটি signal**, কিন্তু একে একমাত্র correctness metric হিসেবে ব্যবহার করা উচিত নয়।

---

# 34. Rewrite Quality Pipeline

Conceptually:

```text
Original Text
      ↓
Embedding
      │
      │
      ▼
Rewrite Model
      ↓
Rewritten Text
      ↓
Embedding
      ↓
Similarity
      ↓
Quality Checks
```

Possible checks:

```text
Semantic similarity
Grammar
Fluency
Length
Entity preservation
Factual consistency
```

---

# 35. NER + Dense Representation

ধরি:

```text
"Microsoft opened an office in London."
```

NER:

```text
Microsoft → ORG
London → GPE
```

Dense representations:

```text
Microsoft → vector
opened    → vector
office    → vector
London    → vector
```

Transformer এগুলোকে context-aware representation-এ convert করতে পারে।

---

# 36. Search System

Dense representation semantic search-এর foundation।

Traditional search:

```text
keyword matching
```

Dense search:

```text
Query
 ↓
Embedding
 ↓
Vector

Documents
 ↓
Embeddings
 ↓
Vectors

Similarity Search
 ↓
Relevant Documents
```

---

# 37. Example

Query:

```text
"How can I learn artificial intelligence?"
```

Document:

```text
"Beginner's guide to machine learning and AI."
```

Exact words পুরোপুরি একই নয়।

কিন্তু dense embeddings semantic similarity ধরতে পারে।

---

# 38. Vector Database Connection

Large-scale semantic search-এ:

```text
Text
 ↓
Embedding Model
 ↓
Vector
 ↓
Vector Database
```

Common vector database concepts:

```text
Embedding
Index
Similarity Search
Nearest Neighbor
Metadata
```

এগুলো পরবর্তী advanced NLP/LLM topics-এ আরও বিস্তারিত আসবে।

---

# 39. Dense Representation-এর Advantages

### 1. Compact

One-hot-এর তুলনায় ছোট dimension হতে পারে।

### 2. Semantic information

Training-এর মাধ্যমে relationships capture করতে পারে।

### 3. Similarity

Vector similarity calculate করা যায়।

### 4. Machine Learning friendly

Neural networks dense vectors নিয়ে efficiently কাজ করতে পারে।

### 5. Generalization

Similar concepts-এর representations কাছাকাছি হতে পারে।

---

# 40. Limitations

Dense representation perfect নয়।

### 1. Meaning automatically guaranteed নয়

```text
similar vector
≠
always same meaning
```

### 2. Bias

Training data-এর bias embedding-এ থাকতে পারে।

### 3. Context dependency

Static embedding context handle করতে দুর্বল।

### 4. Dimension trade-off

খুব ছোট dimension হলে information loss হতে পারে।

### 5. Domain mismatch

General-domain embedding medical/legal/technical domain-এ সবসময় optimal নাও হতে পারে।

---

# 41. Dimension Trade-off

ধরি:

```text
embedding_dim = 16
```

Representation compact।

কিন্তু capacity কম হতে পারে।

আর:

```text
embedding_dim = 4096
```

অনেক বেশি information represent করার capacity থাকতে পারে, কিন্তু:

```text
Memory ↑
Computation ↑
Storage ↑
```

হয়।

তাই dimension একটি design trade-off।

---

# 42. Memory Calculation

ধরি:

```text
vocab_size = 50,000
embedding_dim = 768
```

Parameters:

$$
50,000 \times 768
$$

```text
= 38,400,000 parameters
```

যদি FP32 ব্যবহার করা হয়:

```text
প্রতি parameter ≈ 4 bytes
```

তাহলে প্রায়:

```text
153.6 MB
```

শুধু embedding matrix-এর জন্য।

---

# 43. PyTorch Practical

```python
import torch
import torch.nn as nn

vocab_size = 10000
embedding_dim = 128

embedding = nn.Embedding(
    vocab_size,
    embedding_dim
)

input_ids = torch.tensor([
    [10, 25, 100, 500]
])

output = embedding(input_ids)

print("Input shape:", input_ids.shape)
print("Output shape:", output.shape)
```

Expected:

```text
Input shape: torch.Size([1, 4])
Output shape: torch.Size([1, 4, 128])
```

---

# 44. একটি Token-এর Vector

```python
single_token = torch.tensor([25])

vector = embedding(
    single_token
)

print(vector.shape)
```

Shape:

```text
(1, 128)
```

---

# 45. Similarity Practice

```python
import torch
import torch.nn.functional as F

a = torch.tensor([
    [0.2, 0.7, 0.4]
])

b = torch.tensor([
    [0.3, 0.6, 0.5]
])

similarity = F.cosine_similarity(
    a,
    b
)

print(similarity)
```

---

# 46. Dense Representation থেকে Transformer

এখন পুরো architecture:

```text
                    TEXT
                     ↓
                 TOKENIZER
                     ↓
                 TOKEN IDs
                     ↓
              Embedding Layer
                     ↓
             Dense Representation
                     ↓
          Positional Information
                     ↓
          Multi-Head Self-Attention
                     ↓
                    FFN
                     ↓
             Transformer Layers
                     ↓
          Contextual Representation
                     ↓
             Prediction / Task
```

---

# 47. M02-এর Previous Topics-এর সাথে Connection

এখন পর্যন্ত আমরা:

```text
M02.03 → NLP Pipeline
M02.15 → Word Embeddings
M02.16 → Language Modeling
M02.20 → Attention
M02.21 → Self-Attention
M02.22 → Multi-Head Attention
M02.23 → Positional Encoding
M02.24 → Transformer
M02.29 → GPT
M02.34 → BPE / WordPiece / SentencePiece
M02.35 → Hugging Face Tokenizer
M02.36 → Dense Representation
```

সবগুলো এখন একসাথে connect হচ্ছে।

---

# 48. Complete Mental Model

সবচেয়ে গুরুত্বপূর্ণ flow:

```text
                    RAW TEXT
                       ↓
                   TOKENIZER
                       ↓
                  SUBWORDS
                       ↓
                  TOKEN IDs
                       ↓
               EMBEDDING LOOKUP
                       ↓
              DENSE REPRESENTATION
                       ↓
             POSITION INFORMATION
                       ↓
            MULTI-HEAD ATTENTION
                       ↓
                      FFN
                       ↓
               TRANSFORMER BLOCK
                       ↓
             CONTEXTUAL DENSE
               REPRESENTATION
                       ↓
                TASK / LM HEAD
                       ↓
              LOGITS / PREDICTION
```

---

# 49. Dense Representation বনাম Contextual Representation

এখানে distinction মনে রাখবে:

### Dense Representation

```text
Numerical vector
```

### Embedding

```text
Learned dense representation
```

### Contextual Representation

```text
Dense representation
+
Context
```

অর্থাৎ:

```text
Embedding
   ↓
Transformer
   ↓
Contextual Representation
```

---

# 50. Interview Questions

### Basic

1. Dense representation কী?
2. Sparse এবং dense representation-এর difference কী?
3. One-hot কেন sparse?
4. Dense vector কী?
5. Embedding কী?
6. Embedding dimension কী?
7. Distributed representation কী?
8. Embedding matrix কী?
9. Embedding lookup কী?
10. Dense representation কেন NLP-তে দরকার?

### Intermediate

11. One-hot representation-এর limitation কী?
12. Dense vector semantic similarity কীভাবে represent করতে পারে?
13. Word2Vec কীভাবে dense representation তৈরি করে?
14. Static এবং contextual embedding-এর difference কী?
15. Sentence embedding কী?
16. Cosine similarity কী?
17. Embedding dimension বাড়ালে কী হয়?
18. Dense representation-এর limitations কী?
19. Transformer-এর আগে এবং পরে representation-এর difference কী?
20. Token ID এবং dense vector-এর difference কী?

### Advanced

21. কেন embedding-এর individual dimensions সাধারণত interpretable নয়?
22. Embedding matrix-এর memory requirement কীভাবে calculate করবে?
23. Contextual representation কীভাবে তৈরি হয়?
24. Dense embeddings semantic search-এ কীভাবে ব্যবহৃত হয়?
25. Sentence similarity এবং lexical similarity-এর difference কী?
26. Domain-specific embedding কেন প্রয়োজন হতে পারে?
27. Dense representation-এ bias কীভাবে আসতে পারে?
28. কেন cosine similarity semantic equivalence-এর perfect measure নয়?
29. Embedding এবং hidden state-এর difference কী?
30. Token embedding এবং positional embedding কীভাবে combine হয়?

---

# 51. Practice Tasks

### Beginner

```text
Task 1:
5টি word-এর জন্য manually dense vectors তৈরি করো।

Task 2:
One-hot এবং dense representation-এর shape compare করো।

Task 3:
PyTorch nn.Embedding দিয়ে 1000-token vocabulary তৈরি করো।
```

### Intermediate

```text
Task 4:
10টি token-এর embedding তৈরি করো।

Task 5:
দুইটি embedding-এর cosine similarity calculate করো।

Task 6:
(B, L) → (B, L, D) shape transformation verify করো।
```

### Advanced

```text
Task 7:
একটি sentence-এর token embeddings বের করো।

Task 8:
একটি document-এর sentence embeddings তৈরি করে similarity compare করো।

Task 9:
Original এবং rewritten sentence-এর embedding similarity calculate করো।

Task 10:
একটি simple semantic-search system তৈরি করো।
```

---

# 52. M02.36 Completion Checklist

```text
☑ Dense Representation
☑ Sparse Representation
☑ Dense vs Sparse
☑ One-Hot limitation
☑ Dense Vector
☑ Vector Dimension
☑ Distributed Representation
☑ Embedding
☑ Embedding Matrix
☑ Embedding Lookup
☑ Token ID → Vector
☑ Word2Vec
☑ CBOW
☑ Skip-gram
☑ Static Embedding
☑ Contextual Representation
☑ Sentence Embedding
☑ Cosine Similarity
☑ Semantic Similarity
☑ Transformer Representation
☑ Hidden Representation
☑ Memory Calculation
☑ Dimension Trade-off
☑ Semantic Search
☑ Vector Database concept
☑ AI Writing Assistant application
☑ Meaning Preservation application
☑ PyTorch implementation
☑ Interview Questions
☑ Practice Tasks
```

## 🧠 এক লাইনের Memory Trick

```text
Tokenization:
Text → Token IDs

Dense Representation:
Token IDs → Dense Vectors

Transformer:
Dense Vectors → Contextual Dense Vectors
```

আর পুরোটা:

```text
TEXT
 ↓
TOKENIZER
 ↓
TOKEN IDs
 ↓
DENSE REPRESENTATION
 ↓
POSITION
 ↓
TRANSFORMER
 ↓
CONTEXTUAL REPRESENTATION
 ↓
PREDICTION / GENERATION
```

**M02.36 — Dense Representation complete.**


----------
