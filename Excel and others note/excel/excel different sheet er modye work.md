অবশ্যই। আপনার screenshot অনুযায়ী আপনি **LibreOffice Calc** ব্যবহার করছেন, তাই আমি **৩টি Sheet একসাথে ব্যবহার করে Excel/Calc-এর practical full tutorial** ৬টি lesson-এ ভাগ করে দিচ্ছি।

আমরা একটি ছোট **Sales Management Project** বানাব:

- **Sheet1 = Products** → Product, Price, Stock
    
- **Sheet2 = Sales** → Product, Quantity, Price, Total
    
- **Sheet3 = Report** → Total Sales, Average, Highest/Lowest, Product-wise summary
    

> **নোট:** নিচের formula-গুলো LibreOffice Calc অনুযায়ী। Calc-এ function-এর argument আলাদা করতে সাধারণত `;` ব্যবহার হয়। Excel-এর কিছু version-এ `,` লাগে।

---

# 📘 Lesson 1 — 3 Sheet তৈরি ও এক Sheet থেকে অন্য Sheet-এ Data আনা

### Sheet1: `Products`

এভাবে data দিন:

|A|B|C|
|---|--:|--:|
|Product|Price|Stock|
|Laptop|40000|10|
|Samsung|20000|15|
|Apple|400000|5|
|Keyboard|2000|30|
|Mouse|1000|50|

---

### Sheet2: `Sales`

এভাবে লিখুন:

|A|B|C|D|
|---|--:|--:|--:|
|Product|Quantity|Price|Total|
|Laptop|2|||
|Samsung|3|||
|Apple|1|||
|Keyboard|5|||

### Sheet1 থেকে Price আনা

Sales-এর `C2`:

```text
=Sheet1.B2
```

তাহলে Laptop-এর price আসবে `40000`।

C2 নিচে drag করলে:

```text
=Sheet1.B3
=Sheet1.B4
=Sheet1.B5
```

হবে।

### অন্য Sheet-এর cell reference-এর basic rule

```text
=Sheet1.A2
=Sheet1.B2
=Sheet2.C5
=Sheet3.D10
```

যদি Sheet-এর নামের মধ্যে space থাকে, যেমন `Product Data`, তাহলে:

```text
='Product Data'.B2
```

---

# 📘 Lesson 2 — Basic Calculation + 3 Sheet-এর মধ্যে Calculation

এখন Sales sheet-এ Total বের করব।

`D2`:

```text
=B2*C2
```

অর্থাৎ:

**Quantity × Price = Total**

Laptop:

```text
2 × 40000 = 80000
```

তারপর D2 নিচে drag করুন।

---

## SUM

Sales-এর মোট বিক্রি:

```text
=SUM(D2:D5)
```

ধরুন result:

```text
80000 + 60000 + 400000 + 10000
= 550000
```

---

## Sheet1-এর পুরো price column যোগ

```text
=SUM(Sheet1.B2:B6)
```

---

## 2টা Sheet একসাথে

```text
=SUM(Sheet1.B2:B6;Sheet2.D2:D5)
```

এখানে Sheet1-এর price এবং Sheet2-এর total—দুটো range একসাথে যোগ হচ্ছে।

---

## 3টা Sheet একসাথে

```text
=SUM(Sheet1.B2:B6;Sheet2.D2:D5;Sheet3.B2:B10)
```

এটাই আপনার আগের প্রশ্নের মূল concept:

**একাধিক Sheet-এর data এক formula-তে ব্যবহার করা যায়।**

---

# 📘 Lesson 3 — SUM, AVERAGE, MAX, MIN, COUNT, IF

এগুলো Excel/Calc-এর সবচেয়ে গুরুত্বপূর্ণ functions।

## 1. SUM

```text
=SUM(D2:D5)
```

মোট যোগফল।

---

## 2. AVERAGE

```text
=AVERAGE(D2:D5)
```

গড় বের করবে।

---

## 3. MAX

```text
=MAX(D2:D5)
```

সবচেয়ে বড় value।

---

## 4. MIN

```text
=MIN(D2:D5)
```

সবচেয়ে ছোট value।

---

## 5. COUNT

```text
=COUNT(D2:D5)
```

কতগুলো numeric data আছে সেটা গুনবে।

---

## 6. COUNTA

```text
=COUNTA(A2:A10)
```

খালি নয় এমন cell গুনবে।

---

# IF Function

ধরুন Sales-এর D column-এ Total আছে।

E2-তে:

```text
=IF(D2>=50000;"High";"Low")
```

যদি Total 50,000 বা বেশি হয়:

**High**

নাহলে:

**Low**

---

### আরেকটি example

```text
=IF(C2>30000;"Expensive";"Normal")
```

---

# 📘 Lesson 4 — SUMIF, COUNTIF, Lookup এবং 3 Sheet Connection

এটা খুব গুরুত্বপূর্ণ lesson।

## SUMIF

ধরুন Sheet2-তে:

|A|D|
|---|--:|
|Laptop|80000|
|Samsung|60000|
|Laptop|40000|
|Apple|400000|

Laptop-এর মোট sales বের করতে:

```text
=SUMIF(A2:A5;"Laptop";D2:D5)
```

Result:

```text
120000
```

---

## COUNTIF

Laptop কতবার বিক্রি হয়েছে:

```text
=COUNTIF(A2:A5;"Laptop")
```

---

# Lookup

এখন আমরা চাই:

**Sales sheet-এ Product লিখলেই Sheet1 থেকে Price automatically আসবে।**

এটার জন্য lookup ব্যবহার করা যায়।

LibreOffice Calc-এ:

```text
=VLOOKUP(A2;Sheet1.A2:C6;2;0)
```

এখানে:

- `A2` = কোন product খুঁজব
    
- `Sheet1.A2:C6` = কোথায় খুঁজব
    
- `2` = Price কোন column-এ
    
- `0` = exact match
    

তাহলে Sales-এর A2-তে `Laptop` থাকলে C2-তে automatically `40000` আসবে।

এরপর:

```text
D2=B2*C2
```

এভাবে Product + Quantity দিলেই Price ও Total automatic করা যায়।

---

# 📘 Lesson 5 — Sheet3-তে Automatic Report তৈরি

এখন আসল কাজ।

### Sheet3: `Report`

এভাবে বানান:

|A|B|
|---|--:|
|Total Sales||
|Average Sales||
|Highest Sale||
|Lowest Sale||
|Number of Sales||

### B1

```text
=SUM(Sheet2.D2:D100)
```

### B2

```text
=AVERAGE(Sheet2.D2:D100)
```

### B3

```text
=MAX(Sheet2.D2:D100)
```

### B4

```text
=MIN(Sheet2.D2:D100)
```

### B5

```text
=COUNT(Sheet2.D2:D100)
```

এখন Sheet2-তে নতুন sales যোগ করলে Report-এর calculation automatically update হবে।

---

## Product-wise Report

Sheet3-তে:

|A|B|
|---|--:|
|Laptop||
|Samsung||
|Apple||
|Keyboard||
|Mouse||

B2:

```text
=SUMIF(Sheet2.A:A;A2;Sheet2.D:D)
```

তারপর নিচে drag করুন।

এখন Sheet3 নিজে নিজে দেখাবে:

**Laptop-এর total sales**  
**Samsung-এর total sales**  
**Apple-এর total sales**  
ইত্যাদি।

---

# 📘 Lesson 6 — Sorting, Filter, Formatting, Chart এবং Final Project

এখন spreadsheet-টাকে professional করব।

## 1. Sort

Sales data select করুন → **Data → Sort**

যেমন Total:

**Largest → Smallest**

তাহলে সবচেয়ে বেশি sales উপরে আসবে।

---

## 2. Filter

Header select করে:

**Data → AutoFilter**

তারপর Product অনুযায়ী শুধু:

```text
Laptop
```

দেখাতে পারবেন।

---

## 3. Currency/Number Format

Price/Total select করে currency বা number format দিতে পারবেন।

যেমন:

```text
40000
```

কে দেখানো যেতে পারে:

```text
40,000
```

---

## 4. Conditional Formatting

ধরুন Total > 50,000 হলে cell highlight করতে চান।

**Format → Conditional → Condition**

তারপর:

```text
Cell value > 50000
```

দিতে পারেন।

---

## 5. Chart

Sheet3-এর product-wise sales table select করুন।

তারপর:

**Insert → Chart**

এখান থেকে:

- Column Chart
    
- Bar Chart
    
- Pie Chart
    
- Line Chart
    

ব্যবহার করতে পারবেন।

তাহলে Sheet3-তে আপনার **Sales Dashboard-এর মতো report** তৈরি হবে।

---

# 🎯 Final Project Structure

শেষে আপনার workbook এমন হবে:

### 🟦 Sheet1 — Products

```text
Product | Price | Stock
Laptop  | 40000 | 10
Samsung | 20000 | 15
Apple   | 400000| 5
Keyboard| 2000  | 30
Mouse   | 1000  | 50
```

### 🟩 Sheet2 — Sales

```text
Product | Quantity | Price | Total
Laptop  | 2        | 40000 | 80000
Samsung | 3        | 20000 | 60000
Apple   | 1        | 400000| 400000
```

Price → **Sheet1 থেকে automatic**

Total → **Quantity × Price**

### 🟨 Sheet3 — Report

```text
Total Sales       550000
Average Sales     137500
Highest Sale      400000
Lowest Sale       10000
Number of Sales   4
```

এর নিচে:

```text
Product | Total Sales
Laptop  | ...
Samsung | ...
Apple   | ...
```

এবং শেষে **Chart**।

---

## 🧠 এই ৬ Lesson-এ যে জিনিসগুলো শিখবেন

|Lesson|বিষয়|
|---|---|
|1|Sheet reference, data transfer|
|2|+, -, ×, ÷, SUM, multiple sheets|
|3|AVERAGE, MAX, MIN, COUNT, IF|
|4|SUMIF, COUNTIF, VLOOKUP|
|5|Automatic Report + 3-sheet calculation|
|6|Sort, Filter, Formatting, Conditional Formatting, Chart|

এরপর advanced level-এ গেলে **XLOOKUP, INDEX/MATCH, SUMIFS, COUNTIFS, IFERROR, Date/Time, Text functions, Data Validation, Pivot Table এবং Dashboard** শেখা যাবে।

-------
এটা খুব গুরুত্বপূর্ণ একটা বিষয়। `Sheet2.A:A` এবং `Sheet2.D:D` হলো **পুরো Column reference**।

ধরুন আপনার **Sheet2** এমন:

| A       | B        | C      | D      |
| ------- | -------- | ------ | ------ |
| Product | Quantity | Price  | Total  |
| Laptop  | 2        | 40000  | 80000  |
| Samsung | 3        | 20000  | 60000  |
| Laptop  | 1        | 40000  | 40000  |
| Apple   | 1        | 400000 | 400000 |

তাহলে:

### `Sheet2.A:A` মানে কী?

```text
Sheet2.A:A
```

মানে **Sheet2-এর পুরো A column**।

অর্থাৎ:

```text
Product
Laptop
Samsung
Laptop
Apple
...
```

### `Sheet2.D:D` মানে কী?

```text
Sheet2.D:D
```

মানে **Sheet2-এর পুরো D column**।

অর্থাৎ:

```text
Total
80000
60000
40000
400000
...
```

---

### তাহলে পুরো formula:

```text
=SUMIF(Sheet2.A:A;A2;Sheet2.D:D)
```

এটার অর্থ হলো:

> **Sheet2-এর A column-এর মধ্যে A2-এর নাম খুঁজবে, আর যেসব row-তে নাম মিলে যাবে, সেই row-এর D column-এর numbers যোগ করবে।**

ধরুন **Sheet3-এর A2 = Laptop**।

তাহলে formula:

```text
=SUMIF(Sheet2.A:A;A2;Sheet2.D:D)
```

এভাবে কাজ করবে:

```text
Sheet2 A column       Sheet2 D column
-------------------------------------
Laptop                80000    ← যোগ
Samsung               60000
Laptop                40000    ← যোগ
Apple                 400000
```

Result:

```text
80000 + 40000 = 120000
```

### সহজভাবে মনে রাখুন

```text
SUMIF(
    কোথায় খুঁজবে ;
    কী খুঁজবে ;
    কোন column-এর number যোগ করবে
)
```

তাই:

```text
=SUMIF(Sheet2.A:A;A2;Sheet2.D:D)
```

মানে:

**A column-এ খুঁজবে → A2-এর নাম অনুযায়ী → D column-এর amount যোগ করবে।**

আর `A:A`, `D:D` **আপনি নিজে টাইপ না করেও mouse দিয়ে column select করে তৈরি করতে পারেন**। চাইলে আমি পরের ধাপে **mouse দিয়ে কীভাবে এই formula বানাবেন, একদম click-by-click** দেখাতে পারি।

----
না, `A:A` লিখলে **কোনো row number দিতে হয় না**। এটা পুরো A column বোঝায়।

### তিনভাবে লিখতে পারেন:

**1. পুরো column:**

```text
Sheet2.A:A
```

মানে A1 থেকে A-এর শেষ row পর্যন্ত।

**2. নির্দিষ্ট row range:**

```text
Sheet2.A2:A100
```

মানে শুধু A2 থেকে A100।

**3. নির্দিষ্ট কয়েকটি row:**

```text
Sheet2.A2:A6
```

মানে শুধু A2, A3, A4, A5, A6।

তাই আপনার formula:

```text
=SUMIF(Sheet2.A:A;A2;Sheet2.D:D)
```

এখানে **row number না দেওয়ার কারণ হলো আপনি পুরো column-টা search করতে চাচ্ছেন।**

আর যদি আপনার data শুধু row 2 থেকে 100 পর্যন্ত হয়, তাহলে এভাবে লিখতে পারেন:

```text
=SUMIF(Sheet2.A2:A100;A2;Sheet2.D2:D100)
```

**Practicalভাবে:** ছোট data হলে `A2:A100` ব্যবহার করা ভালো; data কতদূর যাবে জানা না থাকলে `A:A` ব্যবহার করা সহজ।

---
হ্যাঁ, **একদম ঠিক।** ✅

LibreOffice Calc-এ:

```text
A:A
```

মানে **পুরো A column**—অর্থাৎ A1 থেকে নিচের শেষ পর্যন্ত।

একইভাবে:

```text
B:B
```

= পুরো B column

```text
D:D
```

= পুরো D column

আর:

```text
A2:A100
```

= শুধু **A2 থেকে A100** পর্যন্ত।

তাই:

```text
=SUMIF(Sheet2.A:A;A2;Sheet2.D:D)
```

এখানে **Sheet2-এর পুরো A column-এ** A2-এর value খুঁজবে এবং **Sheet2-এর পুরো D column থেকে** matching row-এর value যোগ করবে। ✔️


---
হ্যাঁ, **Excel আর Google Sheets অনেকটাই একই**, বিশেষ করে basic থেকে intermediate কাজের ক্ষেত্রে। তবে ১০০% একই নয়।

আপনি যেগুলো এখন শিখছেন—**Sheet reference, SUM, SUMIF, IF, AVERAGE, COUNT, VLOOKUP**—এসব দুটোতেই করা যায়।

### মূল পার্থক্য

| বিষয়                    | Excel          | Google Sheets |
| ----------------------- | -------------- | ------------- |
| Multiple Sheets         | ✅              | ✅             |
| `SUM()`                 | ✅              | ✅             |
| `SUMIF()`               | ✅              | ✅             |
| `IF()`                  | ✅              | ✅             |
| `AVERAGE()`             | ✅              | ✅             |
| `COUNT()`               | ✅              | ✅             |
| `VLOOKUP()`             | ✅              | ✅             |
| `XLOOKUP()`             | ✅              | ✅             |
| Chart                   | ✅              | ✅             |
| Filter                  | ✅              | ✅             |
| Pivot Table             | ✅              | ✅             |
| Online collaboration    | সীমিত/OneDrive | ⭐ খুব সহজ     |
| Advanced Excel features | ⭐ বেশি         | তুলনামূলক কম  |

### তবে একটা গুরুত্বপূর্ণ পার্থক্য

আপনি এখন **LibreOffice Calc**-এ যে formula ব্যবহার করছেন:

```text
=SUM(Sheet1.B2:B6)
```

Google Sheets/Excel-এ সাধারণত reference হবে:

```text
=SUM(Sheet1!B2:B6)
```

অর্থাৎ **LibreOffice Calc-এ `.`**, আর Excel/Google Sheets-এ সাধারণত **`!`**।

আর পুরো column:

**Excel/Google Sheets:**

```text
Sheet2!A:A
Sheet2!D:D
```

তাই আপনি যদি **Excel বা Google Sheets শেখার জন্য tutorial করেন**, আমি পরের lessonগুলো **Excel + Google Sheets-এর common formula** দিয়ে শেখাতে পারি—তাহলে দুটোতেই একইভাবে কাজ করতে পারবেন।

---
