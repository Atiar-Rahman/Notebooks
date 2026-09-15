# 📊 Excel Mastery — Class 1

## Excel Interface + Workbook, Worksheet, Row, Column, Cell & Range

আজকের class-এর লক্ষ্য হলো **Excel-এর basic structure একদম পরিষ্কার করা**। এগুলো ভালোভাবে না বুঝলে পরের formula, PivotTable, Power Query—সবকিছুতেই confusion হবে।

---

## 1️⃣ Excel কী?

**Microsoft Excel** হলো spreadsheet software, যেটা দিয়ে আমরা:

- Data store করতে পারি
    
- হিসাব করতে পারি
    
- Data clean করতে পারি
    
- Data analyze করতে পারি
    
- Chart বানাতে পারি
    
- Report/Dashboard তৈরি করতে পারি
    

Data Analyst হিসেবে Excel-এর মূল কাজ হবে:

> **Data → Clean → Calculate → Analyze → Visualize → Report**

---

# 2️⃣ Workbook কী?

তুমি যখন Excel খুলে একটি file তৈরি করো এবং সেটি save করো:

```text
sales.xlsx
```

পুরো `sales.xlsx` file-টিই হলো **Workbook**।

সহজভাবে:

> **Workbook = পুরো Excel file**

একটি workbook-এর মধ্যে অনেকগুলো worksheet থাকতে পারে।

উদাহরণ:

```text
📁 Sales.xlsx
   ├── Sales Data
   ├── Customers
   ├── Products
   └── Summary
```

### মনে রাখবে

**Workbook → File**

---

# 3️⃣ Worksheet কী?

Workbook-এর ভিতরের প্রতিটি আলাদা sheet হলো **Worksheet**।

উদাহরণ:

```text
Sales.xlsx
│
├── Sheet1 → Sales Data
├── Sheet2 → Customers
└── Sheet3 → Products
```

এখানে:

- `Sales.xlsx` = Workbook
    
- `Sales Data` = Worksheet
    
- `Customers` = Worksheet
    
- `Products` = Worksheet
    

### সহজ analogy

একটা **খাতা** চিন্তা করো।

```text
খাতা = Workbook

পৃষ্ঠা ১ = Worksheet
পৃষ্ঠা ২ = Worksheet
পৃষ্ঠা ৩ = Worksheet
```

---

# 4️⃣ Row কী?

Excel-এর **horizontal line** হলো Row।

Row সাধারণত number দিয়ে identify করা হয়:

```text
1
2
3
4
5
...
```

যেমন:

```text
        A       B       C
      ─────────────────────
1     Rahim   Dhaka    IT
2     Karim   Khulna   HR
3     Hasan   Dhaka    Sales
```

এখানে:

```text
Row 1
Row 2
Row 3
```

### মনে রাখার trick:

**Row = Number**

---

# 5️⃣ Column কী?

Excel-এর **vertical line** হলো Column।

Column সাধারণত letter দিয়ে identify করা হয়:

```text
A
B
C
D
E
...
```

উদাহরণ:

```text
       A          B          C
       ↓          ↓          ↓
1    Rahim      Dhaka       IT
2    Karim      Khulna      HR
3    Hasan      Dhaka       Sales
```

এখানে:

- A = Name
    
- B = City
    
- C = Department
    

### মনে রাখার trick:

**Column = Letter**

---

# 6️⃣ Cell কী?

এটাই সবচেয়ে important।

**একটি Row এবং একটি Column যেখানে intersect করে, সেই জায়গাটিকে Cell বলে।**

উদাহরণ:

```text
       A        B        C
    ┌────────┬────────┬────────┐
1   │ Rahim  │ Dhaka  │ IT     │
    ├────────┼────────┼────────┤
2   │ Karim  │ Khulna │ HR     │
    ├────────┼────────┼────────┤
3   │ Hasan  │ Dhaka  │ Sales  │
    └────────┴────────┴────────┘
```

`Rahim` আছে:

```text
Column A
Row 1
```

তাই cell address:

```text
A1
```

`Dhaka` প্রথম row-তে:

```text
B1
```

`Sales`:

```text
C3
```

---

# 7️⃣ Cell Address কী?

প্রতিটি cell-এর একটি unique address থাকে।

Format:

```text
Column + Row
```

উদাহরণ:

```text
A1
B5
C10
D25
```

### A5 মানে কী?

```text
Column = A
Row = 5
```

অর্থাৎ:

> Column A-এর 5 নম্বর row-এর cell।

---

# 8️⃣ Active Cell কী?

তুমি Excel-এ কোনো cell-এ click করলে যে cell select হয়, সেটি হলো **Active Cell**।

যেমন তুমি `B3`-এ click করেছো:

```text
       A       B       C
1
2
3             🟦
4
```

তাহলে:

```text
Active Cell = B3
```

Formula বা data টাইপ করলে সেটা সাধারণত active cell-এ যাবে।

---

# 9️⃣ Cell Range কী?

একাধিক cell-এর group হলো **Range**।

ধরো:

```text
A1
A2
A3
A4
A5
```

এগুলো একসাথে:

```text
A1:A5
```

এটাই একটি range।

### `A1:C3`

এর অর্থ:

```text
       A       B       C
1     [ ]     [ ]     [ ]
2     [ ]     [ ]     [ ]
3     [ ]     [ ]     [ ]
```

অর্থাৎ মোট:

```text
3 columns × 3 rows
= 9 cells
```

---

# 🔟 Range লেখার নিয়ম

### Vertical range

```text
A1:A10
```

A1 থেকে A10।

### Horizontal range

```text
A1:F1
```

A1 থেকে F1।

### Rectangle range

```text
A1:C5
```

A থেকে C এবং row 1 থেকে 5।

মোট:

```text
3 × 5 = 15 cells
```

---

# 1️⃣1️⃣ Data কীভাবে রাখব?

ধরো আমরা employee data রাখছি।

|ID|Name|Department|Salary|
|--:|---|---|--:|
|101|Rahim|IT|30000|
|102|Karim|HR|28000|
|103|Hasan|IT|35000|
|104|Nila|Sales|32000|

Excel-এ:

```text
       A       B          C             D
1     ID      Name     Department     Salary
2     101     Rahim       IT          30000
3     102     Karim       HR          28000
4     103     Hasan       IT          35000
5     104     Nila        Sales       32000
```

এখানে:

```text
A1 = ID
B1 = Name
C1 = Department
D1 = Salary
```

আর:

```text
A2 = 101
B2 = Rahim
C2 = IT
D2 = 30000
```

---

# 1️⃣2️⃣ Header কী?

Dataset-এর প্রথম row-তে যে column names থাকে, সেগুলোকে সাধারণত **Header** বলা হয়।

উপরের dataset-এ:

```text
ID
Name
Department
Salary
```

এগুলো হলো headers।

Data analysis-এর সময় **clear header থাকা খুব গুরুত্বপূর্ণ**।

❌ Bad:

```text
Column1
Column2
Column3
```

✅ Good:

```text
Employee_ID
Employee_Name
Department
Salary
```

---

# 1️⃣3️⃣ Excel-এর Formula Bar

যখন কোনো cell select করবে, উপরে **Formula Bar**-এ সেই cell-এর content দেখতে পারবে।

ধরো:

```text
D2 = 30000
```

D2 select করলে formula bar-এ:

```text
30000
```

দেখাবে।

পরবর্তীতে formula লিখলে এখানেও formula দেখতে পারবে।

যেমন:

```excel
=D2*12
```

---

# 1️⃣4️⃣ Name Box

Formula bar-এর বাম পাশে সাধারণত **Name Box** থাকে।

যদি তুমি `C25` select করো, Name Box-এ:

```text
C25
```

দেখাবে।

এটার আরেকটা useful কাজ আছে।

তুমি Name Box-এ:

```text
A1:D100
```

লিখে Enter দিলে পুরো range select হয়ে যাবে।

এটা বড় dataset-এর সময় খুব useful।
 
---

# 1️⃣5️⃣ Sheet Rename

Default:

```text
Sheet1
Sheet2
Sheet3
```

এভাবে না রেখে meaningful নাম দাও:

```text
Sales_Data
Customers
Products
Summary
```

উদাহরণ:

```text
Workbook: ECommerce.xlsx

Sheets:
├── Sales_Data
├── Customers
├── Products
└── Dashboard
```

এটা professional habit।

---

# 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ ৮টি শব্দ

এগুলো মুখস্থ না করে **বুঝে ফেলো**:

|Term|Meaning|
|---|---|
|Workbook|পুরো Excel file|
|Worksheet|Workbook-এর একটি sheet|
|Row|Horizontal, number|
|Column|Vertical, letter|
|Cell|Row + Column intersection|
|Cell Address|যেমন A1, B5|
|Range|একাধিক cell-এর group|
|Header|Column-এর নাম|

---

# ⚠️ Beginner Mistakes

### ❌ Mistake 1

Row এবং Column গুলিয়ে ফেলা।

মনে রাখবে:

> **Row → Number**  
> **Column → Letter**

---

### ❌ Mistake 2

`A1`-কে Range মনে করা।

`A1` = একটি cell।

```text
A1:A10
```

= Range।

---

### ❌ Mistake 3

Dataset-এর মাঝখানে blank row রাখা।

যেমন:

```text
ID   Name   Salary
1    Rahim  30000
2    Karim  35000

3    Hasan  40000
```

Data analysis-এর সময় unnecessary blank row সমস্যা তৈরি করতে পারে।

---

### ❌ Mistake 4

একই column-এ different types of data রাখা।

যেমন Salary column:

```text
30000
35000
"thirty thousand"
40000
```

এটা bad data practice।

---

# 📝 Class 1 Assignment

Excel খুলে একটি নতুন workbook তৈরি করো।

### Step 1

Workbook-এর নাম দাও:

```text
Excel_Mastery.xlsx
```

### Step 2

প্রথম sheet-এর নাম:

```text
Employees
```

### Step 3

এই data manually enter করো:

|Employee_ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Rahim|IT|Dhaka|30000|
|102|Karim|HR|Khulna|28000|
|103|Hasan|IT|Dhaka|35000|
|104|Nila|Sales|Chittagong|32000|
|105|Rafi|Finance|Dhaka|40000|

### Step 4 — এই প্রশ্নগুলোর উত্তর দাও

**Q1.** `Hasan` কোন cell-এ আছে? =>B4

**Q2.** `35000` কোন cell-এ আছে? => E4

**Q3.** `Department` কোন cell-এ আছে? =>C1

**Q4.** পুরো Salary column-এর range কী? => E1:E6

**Q5.** পুরো dataset-এর range কী? => A1:E6

**Q6.** `A2:E6`-এ মোট কয়টি cell আছে?=> 20

**Q7.** `C4`-এ কী data আছে? => IT

**Q8.** Workbook এবং Worksheet-এর পার্থক্য কী? =>WORKBOOK FULL FILE AND WORKSHEET ONLY SHEET

---

### 🎯 Next Class

**Class 2: Data Entry + Formatting + Number/Text/Date data types + Row/Column width + Merge + Freeze Panes + professional dataset formatting**

আগে **Class 1 assignment-এর ৮টা answer আমাকে দাও**। আমি check করে তারপর Class 2 শুরু করব।



----

# 📊 Excel Mastery — Class 2

## Data Entry + Formatting + Data Types + Freeze Panes

আজকের class-এর মূল লক্ষ্য হলো **Excel-এ data professionalভাবে enter এবং format করা**।

Data Analyst হিসেবে একটা গুরুত্বপূর্ণ rule:

> **Formatting সুন্দর করার জন্য নয় শুধু—data যেন Excel সহজে বুঝতে পারে, সেটাও নিশ্চিত করতে হবে।**

---

# 1️⃣ Data Entry কী?

Excel cell-এর মধ্যে data লেখা হলো **Data Entry**।

যেমন:

|Employee_ID|Name|Department|Salary|
|--:|---|---|--:|
|101|Rahim|IT|30000|
|102|Karim|HR|28000|

এখানে:

```text
A2 → 101
B2 → Rahim
C2 → IT
D2 → 30000
```

---

# 2️⃣ Excel-এর প্রধান Data Types

আজকে ৪টি type ভালোভাবে বুঝবে:

### ① Text

যেমন:

```text
Rahim
Dhaka
IT
Laptop
```

Excel এগুলোকে সাধারণত text হিসেবে ধরে।

---

### ② Number

যেমন:

```text
100
250
30000
99.5
```

Number দিয়ে calculation করা যায়।

```excel
=30000+5000
```

Result:

```text
35000
```

---

### ③ Date

যেমন:

```text
13/09/2026
```

Date Excel-এর কাছে বিশেষ ধরনের numeric value হিসেবে internally handled হয়।

তাই date নিয়ে calculation করা সম্ভব।

যেমন:

```excel
=A2+7
```

Date-এর সাথে 7 দিন যোগ হবে।

---

### ④ Time

যেমন:

```text
09:30 AM
05:45 PM
```

Time দিয়েও calculation করা যায়।

---

# 3️⃣ সবচেয়ে গুরুত্বপূর্ণ: Number বনাম Text

ধরো Salary:

```text
30000
```

এটা যদি **Number** হয়:

```excel
=SUM(A1:A5)
```

কাজ করবে।

কিন্তু যদি number-এর মতো দেখতে হলেও Excel সেটাকে **Text** হিসেবে ধরে, তাহলে calculation-এ সমস্যা হতে পারে।

### Example

❌ Text:

```text
'30000
```

এখানে শুরুতে `'` থাকায় Excel এটাকে text হিসেবে treat করতে পারে।

✅ Number:

```text
30000
```

---

# 4️⃣ ID কেন Number না Text হতে পারে?

ধরো Employee ID:

```text
001
002
003
```

যদি এগুলো সাধারণ number হিসেবে রাখো:

```text
1
2
3
```

leading zero হারিয়ে যেতে পারে।

যদি ID-এর leading zero গুরুত্বপূর্ণ হয়, তাহলে **Text** হিসেবে রাখা ভালো।

এটা Data Analyst হিসেবে খুব গুরুত্বপূর্ণ data-type decision।

---

# 5️⃣ Data Entry Shortcut

### নতুন cell-এ যেতে

```text
Enter
```

সাধারণত নিচের cell-এ যাবে।

### পাশের cell-এ যেতে

```text
Tab
```

---

# 6️⃣ Copy & Paste

ধরো B2-তে:

```text
Rahim
```

Copy:

```text
Ctrl + C
```

Paste:

```text
Ctrl + V
```

---

# 7️⃣ Fill Handle

এটা Excel-এর খুব useful feature।

ধরো:

```text
A1 = 1
A2 = 2
```

দুটো cell select করে নিচে drag করলে Excel pattern বুঝে:

```text
1
2
3
4
5
6
```

তৈরি করতে পারে।

এটাকে **AutoFill** বলা হয়।

---

# 8️⃣ Formatting কী?

Data-এর appearance পরিবর্তন করাকে Formatting বলা হয়।

যেমন:

- Font
    
- Font size
    
- Bold
    
- Alignment
    
- Number format
    
- Border
    
- Fill
    
- Decimal places
    

---

# 9️⃣ Header Formatting

আমাদের dataset:

|Employee_ID|Name|Department|City|Salary|
|---|---|---|---|--:|
|101|Rahim|IT|Dhaka|30000|
|102|Karim|HR|Khulna|28000|

Header আলাদা করে দেখাতে পারো:

```text
Employee_ID
Name
Department
City
Salary
```

### Bold

Header select করে:

```text
Ctrl + B
```

---

# 🔟 Alignment

Text সাধারণত left aligned এবং number সাধারণত right aligned দেখা যায়।

উদাহরণ:

```text
Rahim          30000
Karim          28000
```

প্রয়োজনে:

- Left
    
- Center
    
- Right
    

alignment ব্যবহার করতে পারো।

### Shortcut

Center:

```text
Alt → H → A → C
```

তবে shortcut মুখস্থ করার দরকার নেই। Ribbon দিয়েও করা যায়।

---

# 1️⃣1️⃣ Column Width

কখনো data পুরোটা দেখা যায় না।

যেমন:

```text
Employee_Name
```

কিন্তু column ছোট হওয়ায়:

```text
Employee_N...
```

দেখাচ্ছে।

Column boundary-তে double-click করলে **AutoFit** হতে পারে।

এতে content অনুযায়ী column width adjust হবে।

---

# 1️⃣2️⃣ Row Height

একইভাবে row-এর height পরিবর্তন করা যায়।

যদি row ছোট হয়:

```text
Row 1
```

তার height বাড়ানো যায়।

---

# 1️⃣3️⃣ Wrap Text

ধরো cell-এর মধ্যে বড় text:

```text
Senior Backend Developer
```

Column ছোট।

Wrap Text দিলে একই cell-এর text একাধিক line-এ দেখা যাবে।

```text
Senior Backend
Developer
```

**Important:** Wrap Text data পরিবর্তন করে না, শুধু display পরিবর্তন করে।

---

# 1️⃣4️⃣ Merge Cells

ধরো:

```text
A1:E1
```

এগুলো merge করে মাঝখানে লিখতে পারো:

```text
EMPLOYEE REPORT
```

এটা title-এর জন্য ব্যবহার করা যায়।

### কিন্তু ⚠️ Data Table-এর মধ্যে Merge Avoid করো

যেমন:

```text
Employee_ID | Name | Salary
```

এই ধরনের dataset-এর মাঝখানে merge করলে sorting, filtering, Power Query ইত্যাদিতে সমস্যা হতে পারে।

### Rule:

> **Title → Merge করা যেতে পারে**  
> **Raw dataset → Merge Avoid**

---

# 1️⃣5️⃣ Number Formatting

ধরো:

```text
30000
```

তুমি এটাকে দেখাতে পারো:

```text
30,000
```

অথবা currency হিসেবে:

```text
৳30,000
```

কিন্তু এখানে একটা গুরুত্বপূর্ণ বিষয়:

**Number format পরিবর্তন করলে underlying value পরিবর্তন হয় না।**

`30000` একই থাকে।

শুধু display পরিবর্তিত হয়।

---

# 1️⃣6️⃣ Decimal Places

ধরো:

```text
95.67891
```

তুমি display করতে পারো:

```text
95.68
```

কিন্তু underlying value এখনও `95.67891` থাকতে পারে।

এটা Data Analysis-এ খুব important।
 
---

# 1️⃣7️⃣ Percentage

ধরো:

```text
0.75
```

Percentage format দিলে:

```text
75%
```

হতে পারে।

আর:

```text
0.25 → 25%
0.50 → 50%
1.00 → 100%
```

### Common mistake ⚠️

যদি তুমি cell-এ সরাসরি:

```text
75
```

লিখে Percentage format দাও, সেটা `7500%` হিসেবে দেখা যেতে পারে।

কারণ:

```text
75 = 7500%
```

Percentage-এর জন্য:

```text
0.75 = 75%
```

---

# 1️⃣8️⃣ Date Formatting

একই date বিভিন্নভাবে display করা যায়।

Underlying date একই হলেও display হতে পারে:

```text
13/09/2026
09/13/2026
13-Sep-2026
September 13, 2026
```

কোন format ব্যবহার করবে সেটা project-এর requirement অনুযায়ী।

---

# 1️⃣9️⃣ Freeze Panes ⭐

Data Analyst-এর জন্য **খুব useful**।

ধরো তোমার dataset-এ 10,000 rows আছে।

উপরে:

```text
Employee_ID | Name | Department | Salary
```

তারপর অনেক নিচে scroll করলে header আর দেখা যাচ্ছে না।

এটা খুব inconvenient।

### Freeze Top Row

তাহলে তুমি নিচে scroll করলেও:

```text
Employee_ID | Name | Department | Salary
```

উপরে visible থাকবে।

Excel-এ:

**View → Freeze Panes → Freeze Top Row**

---

# 2️⃣0️⃣ Freeze First Column

যদি অনেকগুলো column থাকে এবং horizontally scroll করতে হয়, প্রথম column freeze করা যায়।

যেমন:

```text
Employee_ID
```

সবসময় visible থাকবে।

---

# 2️⃣1️⃣ Freeze Multiple Rows/Columns

এখানে একটু advanced concept।

ধরো তুমি চাও:

```text
Row 1
Row 2
```

freeze থাকবে।

তাহলে **Row 3 select** করে:

**View → Freeze Panes → Freeze Panes**

কারণ Excel নির্বাচিত cell-এর **উপরের rows** এবং **বামের columns** freeze করতে পারে।

---

# 2️⃣2️⃣ Hide / Unhide

কোনো column hide করা যায়।

যেমন:

```text
A = ID
B = Name
C = Email
D = Salary
```

Email column আপাতত দরকার নেই।

Column C hide করতে পারো।

পরে আবার **Unhide** করা যায়।

⚠️ মনে রাখবে:

> Hide করা মানে delete করা নয়।

Data এখনও workbook-এ থাকে।

---

# 2️⃣3️⃣ Professional Dataset Structure

Data Analyst হিসেবে raw data ideally এমন রাখবে:

```text
A              B          C            D        E
Employee_ID    Name       Department   City     Salary
101            Rahim      IT           Dhaka    30000
102            Karim      HR           Khulna   28000
103            Hasan      IT           Dhaka    35000
104            Nila       Sales        Chittagong 32000
```

### Avoid:

```text
❌ Blank rows in the middle
❌ Merged cells inside data
❌ Multiple headers
❌ Random formatting
❌ Mixed data types
❌ Empty column names
```

---

# 🧠 আজকের সবচেয়ে গুরুত্বপূর্ণ concepts

|Concept|মনে রাখবে|
|---|---|
|Text|Rahim, Dhaka|
|Number|100, 50000|
|Date|13/09/2026|
|Time|10:30 AM|
|Formatting|Data-এর appearance|
|AutoFit|Content অনুযায়ী size|
|Wrap Text|Long text multiple lines|
|Merge|Cells combine করা|
|Freeze Panes|Scroll করলেও header visible|
|Number Format|Value-এর display পরিবর্তন|
|Hide|Temporarily data লুকানো|

---

# 📝 Class 2 Assignment

Excel-এ এই dataset তৈরি করো:

|Employee_ID|Name|Department|City|Joining_Date|Salary|
|--:|---|---|---|---|--:|
|101|Rahim|IT|Dhaka|10/01/2024|30000|
|102|Karim|HR|Khulna|15/02/2024|28000|
|103|Hasan|IT|Dhaka|20/03/2024|35000|
|104|Nila|Sales|Chittagong|12/04/2024|32000|
|105|Rafi|Finance|Dhaka|25/05/2024|40000|

তারপর:

### Task 1

Header-গুলো **Bold** করো।

### Task 2

সব column **AutoFit** করো।

### Task 3

Salary-কে comma format-এ দেখাও:

```text
30,000
28,000
35,000
```

### Task 4

Joining_Date-কে এই format-এ দেখাও:

```text
10-Jan-2024
15-Feb-2024
```

### Task 5

Top row **Freeze** করো।

### Task 6

Department column-এর width এমন করো যাতে পুরো `Department` দেখা যায়।

### Task 7

Dataset-এর মধ্যে কোনো cell **Merge করবে না**।

---

## 🧪 Mini Quiz

নিজে answer দাও:

**1. Workbook এবং Worksheet-এর মধ্যে পার্থক্য কী?**

**2. `B7` কী?**

A. Row  
B. Column  
C. Cell  
D. Range

**3. `A1:D10`-এ মোট কতটি cell?**

**4. `30000` এবং `'30000`-এর মধ্যে পার্থক্য কী হতে পারে?**

**5. Freeze Panes কেন ব্যবহার করি?**

**6. Dataset-এর মাঝখানে Merge Cells করা কেন avoid করা উচিত?**

**7. `0.25` Percentage format করলে কত দেখাবে?**

**8. Hide করা column কি delete হয়ে যায়?**

তুমি **1–8-এর answer পাঠাও**। আমি check করে ভুলগুলো explain করব, তারপর **Class 3: Basic Formulas & Operators** শুরু করব।


----

# 📊 Excel Mastery — Class 3

## Basic Formulas & Operators

আজকের class থেকে আমরা Excel-এ **calculation** শুরু করব। এই class খুব গুরুত্বপূর্ণ, কারণ পরের `IF`, `SUMIFS`, `XLOOKUP`, PivotTable—সবকিছুর ভিত্তি হলো formula।

---

# 1️⃣ Formula কী?

Excel-এ কোনো calculation বা operation করার instruction হলো **Formula**।

Formula সাধারণত `=` দিয়ে শুরু হয়।

উদাহরণ:

```excel
=10+20
```

Result:

```text
30
```

### গুরুত্বপূর্ণ

❌ এটা formula নয়:

```text
10+20
```

✅ Formula:

```excel
=10+20
```

---

# 2️⃣ Arithmetic Operators

Excel-এর basic mathematical operators:

|Operator|কাজ|Example|Result|
|---|---|---|--:|
|`+`|যোগ|`=10+5`|15|
|`-`|বিয়োগ|`=10-5`|5|
|`*`|গুণ|`=10*5`|50|
|`/`|ভাগ|`=10/5`|2|
|`^`|Power|`=2^3`|8|
|`%`|Percentage|`=50*10%`|5|

⚠️ Excel-এ multiplication-এর জন্য `×` নয়, `*` ব্যবহার করতে হবে।

---

# 3️⃣ Cell Reference দিয়ে Calculation

এটাই বাস্তবে বেশি ব্যবহার করবে।

ধরো:

|A|B|C|
|---|--:|--:|
|Product|Price|Quantity|
|Laptop|50000|2|

এখন `D2`-তে Total Price বের করতে চাই।

Formula:

```excel
=B2*C2
```

Result:

```text
100000
```

এখানে:

```text
B2 = 50000
C2 = 2
```

তাই:

```text
50000 × 2 = 100000
```

---

# 4️⃣ Cell Reference কেন ব্যবহার করব?

তুমি চাইলে লিখতে পারো:

```excel
=50000*2
```

কিন্তু এটা ভালো practice নয়।

বরং:

```excel
=B2*C2
```

কারণ পরে Price বা Quantity পরিবর্তন করলে formula automatically নতুন result দেবে।

যেমন:

```text
Price = 50000
Quantity = 2
Total = 100000
```

Quantity পরিবর্তন করে `3` করলে:

```text
Total = 150000
```

Formula নতুন করে লিখতে হবে না।

---

# 5️⃣ Addition

ধরো:

|A|B|
|---|--:|
|Product A|100|
|Product B|200|

Total:

```excel
=B2+B3
```

Result:

```text
300
```

তবে অনেকগুলো value থাকলে `SUM()` ব্যবহার করা better—সেটা পরের class-এ বিস্তারিত করব।

---

# 6️⃣ Subtraction

ধরো:

```text
Original Price = 50000
Discount = 5000
```

Formula:

```excel
=B2-B3
```

Result:

```text
45000
```

---

# 7️⃣ Multiplication

ধরো:

|Product|Price|Quantity|
|---|--:|--:|
|Laptop|50000|2|

Formula:

```excel
=B2*C2
```

Result:

```text
100000
```

Sales data-তে এই ধরনের formula খুব common।

---

# 8️⃣ Division

ধরো:

```text
Total Sales = 100000
Orders = 20
```

Average order value:

```excel
=B2/B3
```

Result:

```text
5000
```

---

# 9️⃣ Power Operator `^`

Excel-এ:

```excel
=2^3
```

মানে:

```text
2 × 2 × 2
```

Result:

```text
8
```

আর:

```excel
=5^2
```

Result:

```text
25
```

Data Analytics-এ এটা basic হলেও mathematical calculations-এ কাজে লাগে।

---

# 🔟 Percentage

ধরো:

```text
Price = 1000
Discount = 10%
```

Discount amount:

```excel
=1000*10%
```

Result:

```text
100
```

Final price:

```excel
=1000-(1000*10%)
```

Result:

```text
900
```

আর cell reference দিয়ে:

|A|B|
|---|--:|
|Price|1000|
|Discount|10%|

Formula:

```excel
=B2*B3
```

Discount amount:

```text
100
```

Final price:

```excel
=B2-(B2*B3)
```

Result:

```text
900
```

---

#  1️⃣1️⃣ Parentheses `()`

Excel-এ calculation order খুব গুরুত্বপূর্ণ।

ধরো:

```excel
=10+20*2
```

Excel আগে multiplication করবে:

```text
20 × 2 = 40

10 + 40 = 50
```

Result:

```text
50
```

কিন্তু:

```excel
=(10+20)*2
```

প্রথমে:

```text
10 + 20 = 30
```

তারপর:

```text
30 × 2 = 60
```

Result:

```text
60
```

### Rule

Parentheses ব্যবহার করলে calculation-এর priority তুমি control করতে পারো।

---

# 1️⃣2️⃣ Order of Operations

সহজভাবে মনে রাখো:

```text
()
↓
^
↓
* /
↓
+ -
```

অর্থাৎ:

1. Parentheses
    
2. Power
    
3. Multiplication / Division
    
4. Addition / Subtraction
    

---

# 1️⃣3️⃣ Formula Copy করা ⭐

এটা আজকের সবচেয়ে গুরুত্বপূর্ণ practical concept।

Dataset:

|Product|Price|Qty|Total|
|---|--:|--:|--:|
|Laptop|50000|2|?|
|Mouse|1000|5|?|
|Keyboard|2000|3|?|

D2-তে লিখবে:

```excel
=B2*C2
```

Result:

```text
100000
```

তারপর D2-এর নিচের দিকে **Fill Handle drag** করলে Excel automatically formula adjust করবে:

```excel
=B2*C2
=B3*C3
=B4*C4
```

Result:

|Product|Price|Qty|Total|
|---|--:|--:|--:|
|Laptop|50000|2|100000|
|Mouse|1000|5|5000|
|Keyboard|2000|3|6000|

এটাই Excel-এর **relative cell reference**-এর basic behavior।

---

# 1️⃣4️⃣ Relative Reference

ধরো D2:

```excel
=B2*C2
```

যখন এক row নিচে copy করবে:

```excel
=B3*C3
```

আরেক row:

```excel
=B4*C4
```

অর্থাৎ reference automatically পরিবর্তন হয়।

এটাই **Relative Reference**।

---

# 1️⃣5️⃣ Absolute Reference — Intro

এখন ধরো আমাদের একটা fixed tax rate আছে:

|A|B|
|---|--:|
|Price|1000|
|Tax Rate|15%|

ধরো Tax Rate রাখা হয়েছে:

```text
B1 = 15%
```

আর নিচে অনেক product আছে।

তুমি চাইবে প্রত্যেক product-এর জন্য একই `B1` ব্যবহার করতে।

এখানে `$` ব্যবহার করা হয়।

```excel
=B2*$B$1
```

`$B$1` মানে:

> Column B এবং Row 1—দুটোকেই fixed রাখো।

এটাকে **Absolute Reference** বলে।

এটা আমরা পরের advanced formula classes-এ আরও গভীরভাবে practice করব।

---

# 1️⃣6️⃣ Mixed Reference — Intro

আরও দুই ধরনের reference আছে:

```text
$B$1 → Column + Row fixed
B$1 → Row fixed
$B1 → Column fixed
```

এগুলোকে **Mixed Reference** বলা হয়।

এখন শুধু conceptটা মনে রাখো। পরে dedicated practice করব।

---

# 1️⃣7️⃣ Formula vs Function

এই দুটো গুলিয়ে ফেলবে না।

### Formula

তুমি নিজে operation তৈরি করছো:

```excel
=B2*C2
```

### Function

Excel-এর built-in calculation:

```excel
=SUM(B2:B10)
```

অর্থাৎ:

> **Function হলো Excel-এর predefined formula/tool।**

পরের class থেকে আমরা Functions শুরু করব।

---

# ⚠️ Common Beginner Mistakes

### Mistake 1 — `=` ভুলে যাওয়া

❌

```text
B2*C2
```

✅

```excel
=B2*C2
```

---

### Mistake 2 — Multiplication-এর জন্য `x`

❌

```excel
=B2xC2
```

✅

```excel
=B2*C2
```

---

### Mistake 3 — Division-এর জন্য `÷`

❌

```excel
=B2÷C2
```

✅

```excel
=B2/C2
```

---

### Mistake 4 — Text দিয়ে calculation

যদি:

```text
B2 = "50000"
```

text হিসেবে stored থাকে, তাহলে কিছু calculation-এ সমস্যা হতে পারে।

তাই data type ঠিক রাখা গুরুত্বপূর্ণ।

---

### Mistake 5 — Formula copy করার সময় reference না বোঝা

```excel
=B2*C2
```

copy করলে:

```excel
=B3*C3
```

হবে।

এটা ভুল নয়—এটাই Relative Reference-এর behavior।

---

# 🧪 Practical Exercise

Excel-এ নিচের table তৈরি করো:

|Product|Price|Quantity|Total|
|---|--:|--:|--:|
|Laptop|50000|2|?|
|Mouse|1000|5|?|
|Keyboard|2000|3|?|
|Monitor|15000|2|?|
|Headphone|3000|4|?|

### Task 1

`D2`-তে Total বের করো।

```text
Price × Quantity
```

### Task 2

D2 formula-টা D6 পর্যন্ত copy করো।

### Task 3

নতুন column তৈরি করো:

```text
Discount
```

প্রতিটি product-এর জন্য `10%` discount ধরে Discount Amount বের করো।

### Task 4

আরেকটি column:

```text
Final Price
```

Formula:

```text
Total - Discount Amount
```

---

# 🧠 Mini Quiz

**1. Excel formula সাধারণত কোন symbol দিয়ে শুরু হয়?**

A. `+`  
B. `=`  
C. `#`  
D. `$`

**2. `=B2*C2` কী করছে?**

A. যোগ  
B. বিয়োগ  
C. গুণ  
D. ভাগ

**3. `=100/5` এর result কত?**

**4. `=2^4` এর result কত?**

**5. `=10+20*2` এর result কত?**

**6. `(10+20)*2` এর result কত?**

**7. `=B2*C2` নিচে copy করলে কেন `=B3*C3` হয়?**

**8. `$B$1` কী ধরনের reference?**

**9. Formula এবং Function-এর মধ্যে মূল পার্থক্য কী?**

---

### 🎯 পরের Class

**Class 4 — SUM, AVERAGE, COUNT, COUNTA, MIN, MAX + practical Sales Dataset**

এই class-এ আমরা শুধু function মুখস্থ করব না—**কোন situation-এ কোন function ব্যবহার করতে হবে**, সেটা real data দিয়ে শিখব।


----
# 📊 Excel Mastery — Class 4

## SUM, AVERAGE, COUNT, COUNTA, MIN, MAX

Class 3-এ আমরা basic formula শিখেছি। আজ থেকে Excel-এর **Functions** শেখা শুরু করব।

---

# 1️⃣ Function কী?

Function হলো Excel-এর built-in calculation tool।

যেমন:

```excel
=SUM(B2:B6)
```

এখানে `SUM()` হলো function।

### Formula বনাম Function

|বিষয়|Example|
|---|---|
|Formula|`=B2+B3+B4+B5+B6`|
|Function|`=SUM(B2:B6)`|

দুটোতেই একই result পাওয়া যায়, কিন্তু Function অনেক সহজ।

---

# 2️⃣ SUM()

**SUM = সব সংখ্যাকে যোগ করা**

ধরো:

|A|B|
|---|--:|
|Product|Sales|
|Laptop|50000|
|Mouse|1000|
|Keyboard|2000|
|Monitor|15000|
|Headphone|3000|

মোট Sales বের করতে:

```excel
=SUM(B2:B6)
```

Result:

```text
71000
```

### আলাদা cell যোগ করতেও পারো

```excel
=SUM(B2,B4,B6)
```

এটি B2 + B4 + B6 যোগ করবে।

### কখন SUM ব্যবহার করব?

যখন তোমার দরকার:

- Total Sales
    
- Total Salary
    
- Total Quantity
    
- Total Expense
    
- Total Marks
    
- Total Revenue
    

---

# 3️⃣ AVERAGE()

**AVERAGE = গড়**

ধরো Marks:

|Student|Marks|
|---|--:|
|A|80|
|B|70|
|C|90|
|D|60|
|E|100|

Average:

```excel
=AVERAGE(B2:B6)
```

Result:

```text
80
```

কারণ:

```text
(80 + 70 + 90 + 60 + 100) / 5
= 400 / 5
= 80
```

### Real-world example

Employee salary-এর average:

```excel
=AVERAGE(F2:F20)
```

এতে F2 থেকে F20 পর্যন্ত salary-এর average পাওয়া যাবে।

---

# 4️⃣ COUNT()

এটা খুব গুরুত্বপূর্ণ।

**COUNT = কতগুলো numerical value আছে সেটা count করে।**

Example:

|A|B|
|---|--:|
|Name|Marks|
|Rahim|80|
|Karim|70|
|Hasan|90|
|Jony|60|

Formula:

```excel
=COUNT(B2:B5)
```

Result:

```text
4
```

কারণ B2:B5-এ 4টি number আছে।

### ⚠️ COUNT Text count করে না

ধরো:

|A|B|
|---|--:|
|Name|Marks|
|Rahim|80|
|Karim|70|
|Hasan|Absent|
|Jony|60|

```excel
=COUNT(B2:B5)
```

Result:

```text
3
```

কারণ `Absent` একটি text।

---

# 5️⃣ COUNTA()

**COUNTA = খালি নয় এমন cell count করে।**

Example:

|Name|
|---|
|Rahim|
|Karim|
|Hasan|
|Jony|

```excel
=COUNTA(A2:A5)
```

Result:

```text
4
```

এখানে text হলেও count হবে।

### COUNT বনাম COUNTA

|Function|কী count করে?|
|---|---|
|COUNT|শুধু numbers|
|COUNTA|যেকোনো non-empty cell|

Example:

|A|
|---|
|100|
|200|
|Rahim|
|300|
|Absent|

```excel
=COUNT(A1:A5)
```

Result:

**3**

কারণ 100, 200, 300 → তিনটি number।

আর:

```excel
=COUNTA(A1:A5)
```

Result:

**5**

কারণ কোনো cell-ই empty নয়।

---

# 6️⃣ MIN()

**MIN = সবচেয়ে ছোট number**

Example:

|Student|Marks|
|---|--:|
|A|80|
|B|70|
|C|90|
|D|60|
|E|100|

```excel
=MIN(B2:B6)
```

Result:

```text
60
```

### কোথায় ব্যবহার হবে?

- Lowest marks
    
- Lowest salary
    
- Minimum price
    
- Minimum temperature
    
- Minimum sales
    

---

# 7️⃣ MAX()

**MAX = সবচেয়ে বড় number**

উপরের dataset:

```excel
=MAX(B2:B6)
```

Result:

```text
100
```

### কোথায় ব্যবহার হবে?

- Highest marks
    
- Highest salary
    
- Maximum sales
    
- Highest price
    

---

# 8️⃣ ছয়টি Function একসাথে

একটা Sales dataset ধরি:

|Product|Sales|
|---|--:|
|Laptop|50000|
|Mouse|1000|
|Keyboard|2000|
|Monitor|15000|
|Headphone|3000|

### Total

```excel
=SUM(B2:B6)
```

➡️ `71000`

### Average

```excel
=AVERAGE(B2:B6)
```

➡️ `14200`

### Number of sales entries

```excel
=COUNT(B2:B6)
```

➡️ `5`

### Non-empty cells

```excel
=COUNTA(B2:B6)
```

➡️ `5`

### Lowest sale

```excel
=MIN(B2:B6)
```

➡️ `1000`

### Highest sale

```excel
=MAX(B2:B6)
```

➡️ `50000`

---

# 🧠 সহজে মনে রাখার Trick

```text
SUM     → মোট
AVERAGE → গড়
COUNT   → কতগুলো Number
COUNTA  → কতগুলো Non-empty
MIN     → সবচেয়ে ছোট
MAX     → সবচেয়ে বড়
```

---

# 9️⃣ COUNT আর COUNTA নিয়ে Beginner Mistake

ধরো:

|Employee|Salary|
|---|--:|
|Rahim|30000|
|Karim|35000|
|Hasan|40000|
|Jony||
|Sakib|45000|

### Salary count:

```excel
=COUNT(B2:B6)
```

Result:

**4**

কারণ একজনের salary blank।

কিন্তু Employee count:

```excel
=COUNTA(A2:A6)
```

Result:

**5**

কারণ পাঁচজন employee-এর নাম আছে।

👉 তাই employee/customer/product-এর সংখ্যা বের করতে অনেক সময় `COUNTA()` useful।

---

# 🔟 Practical Excel Task

Excel-এ নিচের dataset তৈরি করো:

|Employee|Department|Salary|Sales|
|---|---|--:|--:|
|Rahim|IT|30000|50000|
|Karim|HR|35000|40000|
|Hasan|IT|40000|60000|
|Jony|Sales|28000|35000|
|Sakib|IT|45000|70000|
|Rafi|HR|32000|45000|

তারপর বের করো:

### Task 1

Total Salary

```excel
=SUM(C2:C7)
```

### Task 2

Average Salary

```excel
=AVERAGE(C2:C7)
```

### Task 3

Highest Salary

```excel
=MAX(C2:C7)
```

### Task 4

Lowest Salary

```excel
=MIN(C2:C7)
```

### Task 5

Total Sales

```excel
=SUM(D2:D7)
```

### Task 6

Average Sales

```excel
=AVERAGE(D2:D7)
```

### Task 7

Number of Employees

```excel
=COUNTA(A2:A7)
```

### Task 8

Number of Salary values

```excel
=COUNT(C2:C7)
```

---

# 📝 Class 4 Quiz

নিজে answer করার চেষ্টা করো।

**1. Total বের করার জন্য কোন function?**

A. COUNT  
B. SUM  
C. MAX  
D. MIN

**2. Average salary বের করতে কোনটা সঠিক?**

A. `=SUM(C2:C10)`  
B. `=COUNT(C2:C10)`  
C. `=AVERAGE(C2:C10)`  
D. `=MAX(C2:C10)`

**3. Highest value বের করতে?**

A. MIN  
B. MAX  
C. COUNT  
D. SUM

**4. Lowest value বের করতে?**

A. MIN  
B. MAX  
C. COUNTA  
D. AVERAGE

**5. শুধু numerical cells count করবে কোনটা?**

A. COUNTA  
B. COUNT  
C. SUM  
D. AVERAGE

**6. Non-empty cells count করবে কোনটা?**

A. COUNT  
B. COUNTA  
C. MIN  
D. MAX

**7. যদি A1:A5 হয় `10, 20, Rahim, 30, blank`, তাহলে `COUNT(A1:A5)` কত?**

A. 2  
B. 3  
C. 4  
D. 5

**8. একই range-এর জন্য `COUNTA(A1:A5)` কত হবে?**

A. 2  
B. 3  
C. 4  
D. 5

### 🎯 আজকের মূল লক্ষ্য

আজ শুধু এই ৬টা function ভালোভাবে আয়ত্ত করো:

**`SUM → AVERAGE → COUNT → COUNTA → MIN → MAX`**

পরের **Class 5**-এ আমরা **IF, IF-ELSE type logic, AND, OR, NOT** শিখব—এগুলো Excel-এ decision making-এর foundation।

---
# 📊 Excel Mastery — Class 5

## IF, AND, OR, NOT — Excel-এর Logic & Decision Making

Class 4-এ আমরা `SUM`, `AVERAGE`, `COUNT`, `COUNTA`, `MIN`, `MAX` শিখেছি।

আজ থেকে Excel-এ **decision নেওয়া** শিখব।

যেমন:

> Marks 40 বা তার বেশি হলে **Pass**, না হলে **Fail**।

এ ধরনের কাজের জন্য সবচেয়ে গুরুত্বপূর্ণ function হলো **IF()**।

---

# 1️⃣ IF() কী?

`IF()` কোনো condition সত্য নাকি মিথ্যা সেটা পরীক্ষা করে।

### Syntax

```excel
=IF(condition, value_if_true, value_if_false)
```

সহজভাবে:

```text
যদি condition সত্য হয় → এটা দেখাও
না হলে → ওটা দেখাও
```

---

# 2️⃣ Basic IF Example

ধরো:

|Student|Marks|
|---|--:|
|Rahim|80|
|Karim|35|
|Hasan|55|
|Jony|20|

আমাদের rule:

```text
Marks >= 40 → Pass
Marks < 40  → Fail
```

C2 cell-এ:

```excel
=IF(B2>=40,"Pass","Fail")
```

Result:

|Student|Marks|Result|
|---|--:|---|
|Rahim|80|Pass|
|Karim|35|Fail|
|Hasan|55|Pass|
|Jony|20|Fail|

---

# 3️⃣ IF Formula ভেঙে বুঝি

```excel
=IF(B2>=40,"Pass","Fail")
```

এখানে:

|অংশ|অর্থ|
|---|---|
|`IF`|condition check করবে|
|`B2>=40`|Marks 40 বা বেশি কিনা|
|`"Pass"`|condition TRUE হলে|
|`"Fail"`|condition FALSE হলে|

---

# 4️⃣ Comparison Operators

IF শেখার জন্য এগুলো খুব গুরুত্বপূর্ণ।

|Operator|Meaning|Example|
|---|---|---|
|`=`|সমান|`A1=10`|
|`>`|বড়|`A1>10`|
|`<`|ছোট|`A1<10`|
|`>=`|বড় অথবা সমান|`A1>=10`|
|`<=`|ছোট অথবা সমান|`A1<=10`|
|`<>`|সমান নয়|`A1<>10`|

### Example

```excel
=B2>50
```

যদি B2 = 70 হয় → TRUE

যদি B2 = 40 হয় → FALSE

---

# 5️⃣ Salary দিয়ে IF

ধরো:

|Employee|Salary|
|---|--:|
|Rahim|50000|
|Karim|30000|
|Hasan|70000|

Rule:

```text
Salary >= 50000 → High
Salary < 50000 → Normal
```

Formula:

```excel
=IF(B2>=50000,"High","Normal")
```

---

# 6️⃣ IF দিয়ে Discount

ধরো:

|Product|Price|
|---|--:|
|Laptop|80000|
|Mouse|1000|
|Monitor|20000|

Rule:

```text
Price >= 50000 → Discount
Price < 50000 → No Discount
```

Formula:

```excel
=IF(B2>=50000,"Discount","No Discount")
```

---

# 7️⃣ Text Condition

IF শুধু number নিয়ে কাজ করে না।

ধরো:

|Employee|Department|
|---|---|
|Rahim|IT|
|Karim|HR|
|Hasan|IT|

যদি IT department হয়:

```text
Technical
```

অন্যথায়:

```text
Non-Technical
```

Formula:

```excel
=IF(B2="IT","Technical","Non-Technical")
```

⚠️ Text comparison-এ `"IT"` এর মতো quotation mark ব্যবহার করতে হয়।

---

# 8️⃣ AND()

এখন একটু advanced logic।

`AND()` তখন TRUE হবে যখন **সব condition TRUE** হবে।

Example:

```excel
=AND(B2>=40,C2>=40)
```

যদি:

```text
B2 = 60
C2 = 70
```

তাহলে:

```text
TRUE
```

কিন্তু:

```text
B2 = 60
C2 = 30
```

তাহলে:

```text
FALSE
```

কারণ দুইটা condition-এর একটি FALSE।

---

# 9️⃣ IF + AND

এটা খুব গুরুত্বপূর্ণ combination।

ধরো একজন student-এর:

- Math = 60
    
- English = 55
    

Pass করার rule:

```text
Math >= 40
AND
English >= 40
```

Formula:

```excel
=IF(AND(B2>=40,C2>=40),"Pass","Fail")
```

### Example

|Student|Math|English|Result|
|---|--:|--:|---|
|Rahim|60|70|Pass|
|Karim|60|30|Fail|
|Hasan|35|80|Fail|
|Jony|70|50|Pass|

কারণ **দুটো subject-এই** minimum 40 লাগবে।

---

# 🔟 OR()

`OR()` তখন TRUE হবে যখন **কমপক্ষে একটি condition TRUE** হবে।

Example:

```excel
=OR(B2>=80,C2>=80)
```

যদি:

```text
B2 = 90
C2 = 50
```

Result:

```text
TRUE
```

কারণ B2 condition TRUE।

---

# 1️⃣1️⃣ IF + OR

ধরো:

```text
Math >= 80
OR
English >= 80
```

যেকোনো একটি subject-এ 80 পেলেই special consideration।

Formula:

```excel
=IF(OR(B2>=80,C2>=80),"Eligible","Not Eligible")
```

Example:

|Student|Math|English|Result|
|---|--:|--:|---|
|Rahim|90|50|Eligible|
|Karim|60|85|Eligible|
|Hasan|70|60|Not Eligible|

---

# 1️⃣2️⃣ NOT()

`NOT()` একটি condition-এর result উল্টে দেয়।

```excel
=NOT(A1="IT")
```

যদি A1 = `IT`

তাহলে:

```text
FALSE
```

যদি A1 = `HR`

তাহলে:

```text
TRUE
```

কারণ `NOT` TRUE → FALSE এবং FALSE → TRUE করে।

---

# 1️⃣3️⃣ AND বনাম OR

এটা খুব ভালোভাবে বুঝো।

### AND

**সবগুলো condition সত্য হতে হবে।**

```excel
=AND(A1>50,B1>50)
```

```text
A = 60
B = 70

TRUE
```

কিন্তু:

```text
A = 60
B = 40

FALSE
```

---

### OR

**কমপক্ষে একটি condition সত্য হলেই হবে।**

```excel
=OR(A1>50,B1>50)
```

```text
A = 60
B = 40

TRUE
```

---

### মনে রাখার সহজ Trick 🧠

```text
AND → সবাইকে Pass করতে হবে
OR  → একজন Pass করলেই হবে
```

---

# 1️⃣4️⃣ IF + AND + OR

এখন একটি real-world example।

ধরো scholarship পাওয়ার rule:

```text
Marks >= 80
AND
Attendance >= 75
```

Formula:

```excel
=IF(AND(B2>=80,C2>=75),"Scholarship","Not Eligible")
```

---

আরেকটি rule:

```text
Marks >= 90
OR
Attendance >= 95
```

Formula:

```excel
=IF(OR(B2>=90,C2>=95),"Special","Normal")
```

---

# 1️⃣5️⃣ Multiple Conditions — Nested IF

এখন ধরো grading system:

|Marks|Grade|
|--:|---|
|80+|A+|
|70–79|A|
|60–69|B|
|50–59|C|
|40–49|D|
|Below 40|F|

এখানে একাধিক condition আছে।

Formula:

```excel
=IF(B2>=80,"A+",
 IF(B2>=70,"A",
 IF(B2>=60,"B",
 IF(B2>=50,"C",
 IF(B2>=40,"D","F")))))
```

এটাকে বলে **Nested IF**।

Excel-এ এটা অনেক ব্যবহার হয়।

---

# 1️⃣6️⃣ Beginner Mistakes ⚠️

### ❌ ভুল

```excel
=IF(B2>=40,Pass,Fail)
```

Text হলে quotation mark দরকার।

### ✅ সঠিক

```excel
=IF(B2>=40,"Pass","Fail")
```

---

### ❌ ভুল

```excel
=IF(B2=>40,"Pass","Fail")
```

### ✅ সঠিক

```excel
=IF(B2>=40,"Pass","Fail")
```

Operator-এর order:

```text
>=
<=
```

---

### ❌ ভুল ধারণা

`AND` মানে যোগ করা নয়।

```excel
=AND(B2,C2)
```

এটা marks যোগ করবে না।

AND হলো **logical condition checker**।

---

# 🎯 Class 5 Practical Assignment

Excel-এ এই dataset বানাও:

|Student|Math|English|Attendance|
|---|--:|--:|--:|
|Rahim|80|75|90|
|Karim|65|85|70|
|Hasan|35|80|85|
|Jony|90|95|95|
|Sakib|45|35|80|

### Task 1 — Pass/Fail

Rule:

```text
Math >= 40 AND English >= 40
```

Formula লিখবে:

```excel
=IF(AND(B2>=40,C2>=40),"Pass","Fail")
```

---

### Task 2 — Attendance Status

Rule:

```text
Attendance >= 75 → Good
Otherwise → Low
```

---

### Task 3 — Scholarship

Rule:

```text
Math >= 80 AND Attendance >= 80
```

তাহলে:

```text
Eligible
```

না হলে:

```text
Not Eligible
```

---

### Task 4 — Special Candidate

Rule:

```text
Math >= 90 OR English >= 90
```

---

### Task 5 — Grade

Nested IF ব্যবহার করে:

```text
80+ → A+
70+ → A
60+ → B
50+ → C
40+ → D
Below 40 → F
```

---

# 📝 Class 5 Quiz

**1. IF function কী করে?**

A. যোগ করে  
B. Condition check করে  
C. Average বের করে  
D. Sort করে

**2. সঠিক formula কোনটি?**

A. `IF(B2>40 Pass Fail)`  
B. `=IF(B2>40,"Pass","Fail")`  
C. `=IF(B2>40,Pass,Fail)`  
D. `IF(B2>40)`

**3. AND কখন TRUE হবে?**

A. যেকোনো একটি condition TRUE হলে  
B. সব condition TRUE হলে  
C. সব FALSE হলে  
D. কখনো না

**4. OR কখন TRUE হবে?**

A. সব condition TRUE হলে  
B. কোনো condition TRUE না হলে  
C. কমপক্ষে একটি condition TRUE হলে  
D. সবসময়

**5. `NOT(TRUE)` এর result কী?**

A. TRUE  
B. FALSE  
C. 1  
D. Error

**6. Math >= 40 এবং English >= 40 হলে কোনটা ব্যবহার করবে?**

A. OR  
B. AND  
C. NOT  
D. MAX

**7. Math >= 80 অথবা English >= 80 হলে কোনটা ব্যবহার করবে?**

A. AND  
B. OR  
C. SUM  
D. COUNT

**8. Multiple grading conditions-এর জন্য কোন technique ব্যবহার করা যায়?**

A. Nested IF  
B. SUM  
C. COUNT  
D. MIN

---

## 🧠 আজকের Cheat Sheet

```text
IF      → যদি...তাহলে...
AND     → সব condition সত্য হতে হবে
OR      → অন্তত একটি সত্য হলেই হবে
NOT     → result উল্টে দেয়

>       → বড়
<       → ছোট
>=      → বড় বা সমান
<=      → ছোট বা সমান
=       → সমান
<>      → সমান নয়
```

**Class 5-এর সবচেয়ে গুরুত্বপূর্ণ skill:** `IF + AND + OR`। এগুলো ভালোভাবে পারলে পরের Excel classes অনেক সহজ হবে।

---
# 📊 Excel Mastery — Class 6

## 📝 Text Functions — Excel-এ Text নিয়ে কাজ

Class 5-এ আমরা **IF, AND, OR, NOT** শিখেছি।  
আজ শিখব Excel-এর খুব গুরুত্বপূর্ণ একটি অংশ:

> **Text Functions**

Data Analyst / Database / Data Cleaning কাজের জন্য এগুলো অনেক গুরুত্বপূর্ণ।

---

# 1️⃣ কেন Text Function দরকার?

বাস্তব dataset-এ অনেক সময় data এমন থাকে:

```text
"  Rahim  "
"rahim"
"RAHIM"
"Dhaka "
"atiar@example.com"
"01712345678"
```

আমাদের করতে হতে পারে:

- Extra space remove
    
- সব uppercase করা
    
- সব lowercase করা
    
- First letter uppercase করা
    
- First name আলাদা করা
    
- Last name আলাদা করা
    
- Text-এর length বের করা
    
- Text-এর অংশ বের করা
    
- দুইটা text একসাথে করা
    

এসবের জন্য Text Functions ব্যবহার করব।

---

# 2️⃣ LEN()

`LEN()` কোনো text-এ মোট কতটি character আছে সেটা count করে।

Example:

```excel
=LEN("Rahim")
```

Result:

```text
5
```

কারণ:

```text
R a h i m
1 2 3 4 5
```

### Cell-এর ক্ষেত্রে

A2:

```text
Bangladesh
```

Formula:

```excel
=LEN(A2)
```

Result:

```text
10
```

---

# 3️⃣ Space-ও Character হিসেবে Count হয় ⚠️

ধরো:

```text
" Rahim "
```

এখানে শুরু ও শেষে space আছে।

```excel
=LEN(A2)
```

এখানে space-ও count হবে।

এটা data cleaning-এর সময় সমস্যা তৈরি করতে পারে।

---

# 4️⃣ TRIM()

`TRIM()` extra spaces remove করে।

ধরো A2:

```text
"   Md. Atiar Rahman   "
```

Formula:

```excel
=TRIM(A2)
```

Result:

```text
Md. Atiar Rahman
```

### কেন দরকার?

Database/Excel dataset-এ:

```text
"Dhaka"
```

এবং

```text
" Dhaka "
```

দেখতে প্রায় একই হলেও Excel-এর কাছে এগুলো আলাদা text হতে পারে।

তাই cleaning-এর সময়:

```excel
=TRIM(A2)
```

খুব useful।

---

# 5️⃣ UPPER()

Text-এর সব letter uppercase করে।

```excel
=UPPER(A2)
```

যদি A2:

```text
rahim
```

Result:

```text
RAHIM
```

আর:

```text
=UPPER("Dhaka")
```

Result:

```text
DHAKA
```

---

# 6️⃣ LOWER()

সব letter lowercase করে।

```excel
=LOWER(A2)
```

যদি:

```text
RAHIM
```

তাহলে:

```text
rahim
```

### Email cleaning-এ useful

```excel
=LOWER(A2)
```

Example:

```text
ATIAR@GMAIL.COM
```

হয়ে যাবে:

```text
atiar@gmail.com
```

---

# 7️⃣ PROPER()

প্রতিটি word-এর প্রথম letter capital করে।

```excel
=PROPER(A2)
```

Example:

```text
md atiar rahman
```

Result:

```text
Md Atiar Rahman
```

আর:

```text
dhaka city
```

Result:

```text
Dhaka City
```

---

# 🧠 তিনটা মনে রাখো

```text
UPPER  → সব CAPITAL
LOWER  → সব small
PROPER → Every Word First Letter Capital
```

---

# 8️⃣ LEFT()

Text-এর **বাম দিক থেকে** নির্দিষ্ট সংখ্যক character নেয়।

ধরো:

```text
Bangladesh
```

Formula:

```excel
=LEFT(A2,4)
```

Result:

```text
Bang
```

কারণ প্রথম 4 character:

```text
B a n g
```

---

# 9️⃣ RIGHT()

Text-এর **ডান দিক থেকে** character নেয়।

```text
Bangladesh
```

Formula:

```excel
=RIGHT(A2,3)
```

Result:

```text
esh
```

কারণ শেষ 3 character হলো:

```text
e s h
```

---

# 🔟 MID()

`MID()` text-এর **মাঝখান থেকে** character নেয়।

Syntax:

```excel
=MID(text,start_num,num_chars)
```

Example:

```text
Bangladesh
```

Formula:

```excel
=MID(A2,2,4)
```

মানে:

```text
Start = 2
Characters = 4
```

Result:

```text
angl
```

কারণ:

```text
B a n g l a n d e s h
1 2 3 4 5 ...
```

2 নম্বর position থেকে 4টি:

```text
a n g l
```

---

# 1️⃣1️⃣ CONCAT()

দুই বা তার বেশি text একসাথে করা যায়।

ধরো:

|First Name|Last Name|
|---|---|
|Atiar|Rahman|

Formula:

```excel
=CONCAT(A2,B2)
```

Result:

```text
AtiarRahman
```

কিন্তু আমরা সাধারণত মাঝখানে space চাই।

```excel
=CONCAT(A2," ",B2)
```

Result:

```text
Atiar Rahman
```

---

# 1️⃣2️⃣ `&` Operator

Text join করার আরেকটি সহজ উপায় হলো `&`।

```excel
=A2&" "&B2
```

Result:

```text
Atiar Rahman
```

অনেক Excel user `&` খুব বেশি ব্যবহার করে।

---

# 1️⃣3️⃣ TEXTJOIN()

Multiple text সুন্দরভাবে join করতে `TEXTJOIN()` ব্যবহার করা যায়।

ধরো:

|A|B|C|
|---|---|---|
|Md.|Atiar|Rahman|

Formula:

```excel
=TEXTJOIN(" ",TRUE,A2:C2)
```

Result:

```text
Md. Atiar Rahman
```

এখানে:

```text
" "   → separator হিসেবে space
TRUE  → blank cell ignore করবে
A2:C2 → যেসব cell join করবে
```

---

# 1️⃣4️⃣ FIND()

কোনো text-এর ভিতরে একটি character/word কোথায় আছে সেটা বের করতে `FIND()` ব্যবহার করা হয়।

ধরো:

```text
atiar@gmail.com
```

Formula:

```excel
=FIND("@",A2)
```

Result:

```text
6
```

কারণ:

```text
a t i a r @
1 2 3 4 5 6
```

---

# 1️⃣5️⃣ SEARCH()

`SEARCH()`-ও text খুঁজে বের করে।

```excel
=SEARCH("@",A2)
```

Email-এর `@` position বের করতে useful।

### FIND বনাম SEARCH

Beginner level-এ শুধু এটুকু মনে রাখো:

|Function|কাজ|
|---|---|
|FIND|text position খুঁজে|
|SEARCH|text position খুঁজে|

দুটোর মধ্যে কিছু technical difference আছে, যেটা পরে advanced class-এ দেখব।

---

# 1️⃣6️⃣ SUBSTITUTE()

একটি text-এর অংশ অন্য text দিয়ে replace করতে ব্যবহার হয়।

ধরো:

```text
Dhaka Bangladesh
```

Formula:

```excel
=SUBSTITUTE(A2,"Dhaka","Chittagong")
```

Result:

```text
Chittagong Bangladesh
```

### আরেকটি example

```text
017-123-45678
```

Hyphen remove করতে:

```excel
=SUBSTITUTE(A2,"-","")
```

Result:

```text
01712345678
```

এটা **data cleaning**-এ খুব useful।

---

# 1️⃣7️⃣ REPLACE()

`REPLACE()` position ব্যবহার করে text replace করে।

ধরো:

```text
ABCDEFG
```

Formula:

```excel
=REPLACE(A2,2,3,"XYZ")
```

মানে:

```text
Start position = 2
কতগুলো character = 3
নতুন text = XYZ
```

Result:

```text
AXYZEFG
```

---

# 1️⃣8️⃣ Text Cleaning Example

ধরো dataset:

|Raw Name|
|---|
|`RAHIM`|
|`karim`|
|`HASAN`|
|`jony`|

Clean করার জন্য:

```excel
=PROPER(TRIM(A2))
```

Result:

|Raw|Clean|
|---|---|
|`RAHIM`|Rahim|
|`karim`|Karim|
|`HASAN`|Hasan|
|`jony`|Jony|

এখানে আমরা **দুইটা function একসাথে** ব্যবহার করেছি।

```text
TRIM → extra space remove
PROPER → name format ঠিক করে
```

এটাকে বলে **Nested Function**।

---

# 1️⃣9️⃣ Email থেকে Username বের করা

ধরো:

```text
atiar@gmail.com
```

আমরা শুধু:

```text
atiar
```

চাই।

এখানে `LEFT()` + `FIND()` ব্যবহার করতে পারি:

```excel
=LEFT(A2,FIND("@",A2)-1)
```

কী হচ্ছে?

প্রথমে:

```excel
FIND("@",A2)
```

`@` কোথায় আছে সেটা বের করে।

তারপর:

```text
-1
```

করায় `@` বাদ পড়ে।

শেষে `LEFT()` username নিয়ে নেয়।

Result:

```text
atiar
```

---

# 2️⃣0️⃣ বাস্তব Data Cleaning Workflow

ধরো customer data:

|Raw Name|Email|Phone|
|---|---|---|
|`RAHIM`|`RAHIM@GMAIL.COM`|`017-111-22222`|
|`karim`|`KARIM@YAHOO.COM`|`018-222-33333`|

Clean Name:

```excel
=PROPER(TRIM(A2))
```

Clean Email:

```excel
=LOWER(TRIM(B2))
```

Clean Phone:

```excel
=SUBSTITUTE(C2,"-","")
```

এখন data হবে:

|Name|Email|Phone|
|---|---|---|
|Rahim|[rahim@gmail.com](mailto:rahim@gmail.com)|01711122222|
|Karim|[karim@yahoo.com](mailto:karim@yahoo.com)|01822233333|

🔥 এটাই real-world Excel data cleaning-এর একটি basic example।

---

# 🧠 Class 6 Cheat Sheet

|Function|কাজ|
|---|---|
|`LEN()`|Character count|
|`TRIM()`|Extra space remove|
|`UPPER()`|CAPITAL|
|`LOWER()`|lowercase|
|`PROPER()`|First letter capital|
|`LEFT()`|বাম থেকে text|
|`RIGHT()`|ডান থেকে text|
|`MID()`|মাঝখান থেকে text|
|`CONCAT()`|Text join|
|`TEXTJOIN()`|Multiple text join|
|`FIND()`|Position খোঁজা|
|`SEARCH()`|Position খোঁজা|
|`SUBSTITUTE()`|Text replace|
|`REPLACE()`|Position অনুযায়ী replace|

---

# 🎯 Class 6 Assignment

এই dataset Excel-এ তৈরি করো:

|Raw Name|Email|Phone|
|---|---|---|
|`RAHIM`|`RAHIM@GMAIL.COM`|`017-111-22222`|
|`karim`|`KARIM@YAHOO.COM`|`018-222-33333`|
|`HASAN`|`HASAN@OUTLOOK.COM`|`019-333-44444`|
|`jony`|`JONY@GMAIL.COM`|`016-444-55555`|

### Task 1

Clean Name বের করো:

```excel
=PROPER(TRIM(A2))
```

### Task 2

Email lowercase করো:

```excel
=LOWER(TRIM(B2))
```

### Task 3

Phone থেকে `-` remove করো।

### Task 4

Name-এর character count বের করো।

### Task 5

Email থেকে username বের করো।

Example:

```text
rahim@gmail.com
        ↓
rahim
```

### Task 6

Email থেকে domain বের করার চেষ্টা করো।

Example:

```text
rahim@gmail.com
        ↓
gmail.com
```

**Hint:** `FIND()` + `RIGHT()` ব্যবহার করে চেষ্টা করো।

---

# 📝 Class 6 Quiz

**1. Extra spaces remove করতে কোন function?**

A. CLEAN  
B. TRIM  
C. SPACE  
D. REMOVE

**2. `UPPER("hello")` result কী?**

A. hello  
B. Hello  
C. HELLO  
D. hELLO

**3. `LOWER("HELLO")` result?**

A. HELLO  
B. Hello  
C. hello  
D. Error

**4. `"Bangladesh"` থেকে প্রথম 4 character নিতে?**

A. `RIGHT(A1,4)`  
B. `LEFT(A1,4)`  
C. `MID(A1,4)`  
D. `LEN(A1,4)`

**5. `"Bangladesh"` থেকে শেষ 3 character নিতে?**

A. `LEFT(A1,3)`  
B. `RIGHT(A1,3)`  
C. `MID(A1,3)`  
D. `END(A1,3)`

**6. `=A2&" "&B2` কী করে?**

A. যোগ করে  
B. Text combine করে  
C. Text delete করে  
D. Text count করে

**7. Text-এর length বের করতে?**

A. LEN  
B. COUNT  
C. SIZE  
D. LENGTH

**8. `"017-123-456"` থেকে `-` remove করতে কোন function useful?**

A. TRIM  
B. SUBSTITUTE  
C. UPPER  
D. FIND

**9. `PROPER("rahim karim")` কী হবে?**

A. RAHIM KARIM  
B. rahim karim  
C. Rahim Karim  
D. Rahimkarim

**10. `FIND("@",A2)` কী বের করে?**

A. Email address  
B. `@`-এর position  
C. Username  
D. Domain

### ⭐ আজকের সবচেয়ে গুরুত্বপূর্ণ 5টি

```text
TRIM
PROPER
LOWER
LEFT / RIGHT
SUBSTITUTE
```

এগুলো ভালোভাবে আয়ত্ত করো। **Class 7-এ আমরা Date & Time Functions** শিখব—`TODAY()`, `NOW()`, `DATE()`, `YEAR()`, `MONTH()`, `DAY()`, বয়স/tenure বের করা, এবং joining date থেকে কত বছর কাজ করেছে এসব real-world example দিয়ে।

---
# 📊 Excel Mastery — Class 7

## 📅 Date & Time Functions

Class 6-এ আমরা **Text Functions** শিখেছি।  
আজ শিখব Excel-এ **Date & Time নিয়ে কাজ**।

Data Analyst, HR, Sales, Finance, Database—প্রায় সব জায়গাতেই Date নিয়ে কাজ করতে হয়।

আজকের topics:

```text
TODAY()
NOW()
DATE()
YEAR()
MONTH()
DAY()
HOUR()
MINUTE()
SECOND()
DATEDIF()
```

---

# 1️⃣ Excel-এ Date কী?

Excel date-কে একটি বিশেষ value হিসেবে store করে।

যেমন:

```text
13/09/2026
```

এটা শুধু text নয়; Excel এটাকে date হিসেবে চিনতে পারলে এর ওপর calculation করা যায়।

উদাহরণ:

```text
Joining Date → 01/01/2024
Today        → 13/09/2026
```

আমরা বের করতে পারি:

> Employee কতদিন ধরে কাজ করছে?

---

# 2️⃣ TODAY()

`TODAY()` বর্তমান date দেয়।

```excel
=TODAY()
```

আজ যদি 13 September 2026 হয়, Excel দেখাবে:

```text
13/09/2026
```

⚠️ এটি automatically update হয়।

অর্থাৎ আজকের date কাল আবার খুললে পরিবর্তিত হবে।

### কোথায় ব্যবহার হয়?

- Current date
    
- Due date calculation
    
- Employee tenure
    
- Age calculation
    
- Expiry tracking
    

---

# 3️⃣ NOW()

`NOW()` বর্তমান **Date + Time** দেয়।

```excel
=NOW()
```

Example:

```text
13/09/2026 07:30
```

অর্থাৎ:

```text
TODAY() → শুধু Date
NOW()   → Date + Time
```

### মনে রাখো

|Function|Result|
|---|---|
|`TODAY()`|Date|
|`NOW()`|Date + Time|

---

# 4️⃣ DATE()

নিজে Year, Month, Day দিয়ে একটি date তৈরি করতে:

```excel
=DATE(2026,9,13)
```

Result:

```text
13/09/2026
```

Syntax:

```text
DATE(year, month, day)
```

Example:

```excel
=DATE(2025,12,25)
```

➡️ 25 December 2025

---

# 5️⃣ YEAR()

একটি date থেকে শুধু year বের করে।

ধরো A2:

```text
15/06/2024
```

Formula:

```excel
=YEAR(A2)
```

Result:

```text
2024
```

---

# 6️⃣ MONTH()

Date থেকে month number বের করে।

```excel
=MONTH(A2)
```

যদি A2:

```text
15/06/2024
```

Result:

```text
6
```

কারণ June হলো 6th month।

---

# 7️⃣ DAY()

Date থেকে day বের করে।

```excel
=DAY(A2)
```

A2:

```text
15/06/2024
```

Result:

```text
15
```

---

# 🧠 YEAR + MONTH + DAY

ধরো:

```text
A2 = 15/06/2024
```

তাহলে:

```excel
=YEAR(A2)
```

➡️ `2024`

```excel
=MONTH(A2)
```

➡️ `6`

```excel
=DAY(A2)
```

➡️ `15`

সহজে মনে রাখো:

```text
YEAR  → বছর
MONTH → মাস
DAY   → দিন
```

---

# 8️⃣ Employee Dataset

এখন একটা real-world dataset দেখি।

|Employee|Joining Date|
|---|---|
|Rahim|10/01/2022|
|Karim|15/05/2023|
|Hasan|20/08/2024|
|Jony|01/02/2025|

ধরো Joining Date B2-তে।

Joining Year বের করতে:

```excel
=YEAR(B2)
```

Joining Month:

```excel
=MONTH(B2)
```

Joining Day:

```excel
=DAY(B2)
```

---

# 9️⃣ Date Difference — খুব গুরুত্বপূর্ণ

ধরো:

```text
Joining Date = 10/01/2022
Today        = 13/09/2026
```

আমরা জানতে চাই:

> Employee কতদিন কাজ করেছে?

Simple calculation:

```excel
=TODAY()-B2
```

যদি B2-তে joining date থাকে, result হবে মোট **days**।

---

# 🔟 DATEDIF()

`DATEDIF()` দুইটি date-এর মধ্যে difference বের করতে পারে।

Syntax:

```excel
=DATEDIF(start_date,end_date,unit)
```

### Unit:

|Unit|অর্থ|
|---|---|
|`"Y"`|Complete years|
|`"M"`|Complete months|
|`"D"`|Total days|

---

# 1️⃣1️⃣ Employee কত বছর কাজ করেছে?

ধরো:

```text
B2 = 10/01/2022
```

আজ পর্যন্ত complete years:

```excel
=DATEDIF(B2,TODAY(),"Y")
```

যদি 4 complete years হয়ে থাকে:

```text
4
```

---

# 1️⃣2️⃣ কত মাস কাজ করেছে?

```excel
=DATEDIF(B2,TODAY(),"M")
```

এটা total complete months দেবে।

---

# 1️⃣3️⃣ কতদিন কাজ করেছে?

```excel
=DATEDIF(B2,TODAY(),"D")
```

এটা total days দেবে।

---

# 1️⃣4️⃣ Age বের করা

ধরো:

|Person|Birth Date|
|---|---|
|Rahim|15/06/2000|

B2-তে Birth Date আছে।

Age:

```excel
=DATEDIF(B2,TODAY(),"Y")
```

এতে **পূর্ণ বছর হিসেবে বয়স** পাওয়া যাবে।

---

# 1️⃣5️⃣ Exact Age — Years + Months + Days

আরও সুন্দরভাবে চাইলে:

```excel
=DATEDIF(B2,TODAY(),"Y")&" Years "&DATEDIF(B2,TODAY(),"YM")&" Months "&DATEDIF(B2,TODAY(),"MD")&" Days"
```

Example result:

```text
26 Years 2 Months 29 Days
```

এখানে:

```text
"Y"  → complete years
"YM" → years বাদ দেওয়ার পর remaining months
"MD" → months বাদ দেওয়ার পর remaining days
```

---

# 1️⃣6️⃣ HOUR()

Time থেকে hour বের করতে:

```excel
=HOUR(A2)
```

যদি:

```text
A2 = 14:35:20
```

Result:

```text
14
```

---

# 1️⃣7️⃣ MINUTE()

```excel
=MINUTE(A2)
```

Result:

```text
35
```

---

# 1️⃣8️⃣ SECOND()

```excel
=SECOND(A2)
```

Result:

```text
20
```

তাহলে:

```text
14:35:20

HOUR   → 14
MINUTE → 35
SECOND → 20
```

---

# 1️⃣9️⃣ Date Formatting

ধরো Excel-এ date আছে:

```text
13/09/2026
```

Format পরিবর্তন করে করতে পারো:

```text
13-Sep-2026
Sep 13, 2026
13 September 2026
09/13/2026
```

⚠️ **Date formatting পরিবর্তন করলে সাধারণত underlying date value পরিবর্তন হয় না; শুধু display পরিবর্তন হয়।**

---

# 2️⃣0️⃣ Date থেকে Month Name

`MONTH()` দিলে:

```text
6
```

কিন্তু আমরা চাই:

```text
June
```

একটি useful technique:

```excel
=TEXT(A2,"mmmm")
```

Result:

```text
June
```

Short month:

```excel
=TEXT(A2,"mmm")
```

Result:

```text
Jun
```

---

# 2️⃣1️⃣ Date থেকে Day Name

ধরো A2:

```text
13/09/2026
```

Day name:

```excel
=TEXT(A2,"dddd")
```

Result:

```text
Sunday
```

Short version:

```excel
=TEXT(A2,"ddd")
```

Result:

```text
Sun
```

---

# 2️⃣2️⃣ Due Date Calculation

এটা খুব useful।

ধরো:

```text
Start Date = 01/09/2026
```

30 দিন পরে due date:

```excel
=A2+30
```

Result:

```text
01/10/2026
```

Excel date calculation করতে পারে।

---

# 2️⃣3️⃣ Days Remaining

ধরো:

```text
Due Date = 30/09/2026
```

আজ থেকে কতদিন বাকি?

```excel
=A2-TODAY()
```

যদি result positive হয় → এখনও সময় আছে।

যদি result negative হয় → deadline চলে গেছে।

---

# 2️⃣4️⃣ IF + TODAY()

এখন Class 5-এর IF ব্যবহার করি।

ধরো A2-তে Due Date:

```text
30/09/2026
```

Formula:

```excel
=IF(A2>=TODAY(),"Pending","Expired")
```

Result:

```text
Pending
```

অর্থাৎ Date এখনও পার হয়নি।

এখানে আমরা combine করেছি:

```text
Class 5 → IF
Class 7 → TODAY
```

🔥 Excel-এ এভাবেই বিভিন্ন function একসাথে ব্যবহার করা হয়।

---

# 2️⃣5️⃣ Real-World Example — Employee

এই dataset তৈরি করো:

|Employee|Joining Date|
|---|---|
|Rahim|10/01/2022|
|Karim|15/05/2023|
|Hasan|20/08/2024|
|Jony|01/02/2025|
|Sakib|10/06/2026|

তারপর columns বানাও:

|Employee|Joining Date|Year|Month|Day|Experience|
|---|---|--:|--:|--:|--:|

### Year

```excel
=YEAR(B2)
```

### Month

```excel
=MONTH(B2)
```

### Day

```excel
=DAY(B2)
```

### Experience

```excel
=DATEDIF(B2,TODAY(),"Y")
```

---

# ⚠️ Beginner Mistakes

### Mistake 1 — Date হিসেবে Text

যদি Excel date-কে text হিসেবে ধরে, তাহলে:

```excel
=YEAR(A2)
```

ঠিকভাবে কাজ নাও করতে পারে।

তাই date data entry করার সময় consistent format ব্যবহার করো।

---

### Mistake 2 — `TODAY()` বনাম `NOW()`

```text
TODAY() → Date
NOW()   → Date + Time
```

---

### Mistake 3 — Month number দেখে month name মনে করা

```excel
=MONTH(A2)
```

দেবে:

```text
9
```

এটা September-এর **number**, `"September"` নয়।

Month name চাইলে:

```excel
=TEXT(A2,"mmmm")
```

---

### Mistake 4 — Age-এ শুধু YEAR subtraction

অনেকে করে:

```excel
=YEAR(TODAY())-YEAR(B2)
```

এতে birthday এখনও না এলে age 1 বেশি দেখাতে পারে।

Age-এর জন্য:

```excel
=DATEDIF(B2,TODAY(),"Y")
```

বেশি reliable।

---

# 🧠 Class 7 Cheat Sheet

|Function|কাজ|
|---|---|
|`TODAY()`|আজকের date|
|`NOW()`|বর্তমান date + time|
|`DATE()`|Date তৈরি|
|`YEAR()`|Year বের করা|
|`MONTH()`|Month number|
|`DAY()`|Day বের করা|
|`HOUR()`|Hour|
|`MINUTE()`|Minute|
|`SECOND()`|Second|
|`DATEDIF()`|দুই date-এর difference|
|`TEXT()`|Date formatting/name|

---

# 🎯 Class 7 Assignment

এই dataset তৈরি করো:

|Employee|Birth Date|Joining Date|
|---|---|---|
|Rahim|15/06/2000|10/01/2022|
|Karim|20/03/1999|15/05/2023|
|Hasan|05/11/2001|20/08/2024|
|Jony|10/02/2000|01/02/2025|
|Sakib|25/08/2002|10/06/2026|

তারপর বের করো:

### Task 1

প্রত্যেকের Age:

```excel
=DATEDIF(B2,TODAY(),"Y")
```

### Task 2

Joining Year

```excel
=YEAR(C2)
```

### Task 3

Joining Month

```excel
=MONTH(C2)
```

### Task 4

Joining Month Name

```excel
=TEXT(C2,"mmmm")
```

### Task 5

Joining Day

```excel
=DAY(C2)
```

### Task 6

প্রত্যেক employee কত বছর ধরে কাজ করছে?

```excel
=DATEDIF(C2,TODAY(),"Y")
```

### Task 7

Joining Date থেকে আজ পর্যন্ত total days:

```excel
=DATEDIF(C2,TODAY(),"D")
```

---

# 📝 Class 7 Quiz

**1. শুধু আজকের date পাওয়ার function কোনটি?**

A. `NOW()`  
B. `DATE()`  
C. `TODAY()`  
D. `DAY()`

**2. Date + Time পেতে?**

A. TODAY  
B. NOW  
C. TIME  
D. DATE

**3. `=YEAR(A2)` কী দেয়?**

A. Day  
B. Month  
C. Year  
D. Time

**4. `=MONTH(A2)` কী দেয়?**

A. Month number  
B. Month name  
C. Day  
D. Year

**5. `=DAY(A2)` কী দেয়?**

A. Year  
B. Month  
C. Day  
D. Week

**6. দুই date-এর মধ্যে complete years বের করতে কোনটি useful?**

A. `YEAR()`  
B. `DATEDIF(...,"Y")`  
C. `DAY()`  
D. `MONTH()`

**7. Date থেকে `September` বের করতে কোনটি ব্যবহার করা যায়?**

A. `=MONTH(A2)`  
B. `=TEXT(A2,"mmmm")`  
C. `=YEAR(A2)`  
D. `=DAY(A2)`

**8. Date থেকে `Sun` বের করতে?**

A. `=TEXT(A2,"ddd")`  
B. `=TEXT(A2,"mmm")`  
C. `=DAY(A2)`  
D. `=HOUR(A2)`

**9. TODAY() এবং NOW()-এর প্রধান পার্থক্য কী?**

A. কোনো পার্থক্য নেই  
B. TODAY date, NOW date + time  
C. TODAY time, NOW date  
D. দুটোই শুধু year দেয়

**10. Due date পার হয়েছে কিনা check করতে কোন combination useful?**

A. SUM + MAX  
B. IF + TODAY  
C. COUNT + MIN  
D. LEFT + RIGHT

---

### ⭐ আজকের Core Skills

```text
TODAY()
NOW()
YEAR()
MONTH()
DAY()
DATEDIF()
TEXT()
```

**বিশেষ করে `DATEDIF + TODAY` ভালোভাবে practice করো।** Data Analyst/HR/Business dataset-এ date calculation অনেক বেশি কাজে লাগবে।

**পরের Class 8 → Lookup Functions: `VLOOKUP`, `XLOOKUP`, `HLOOKUP`, `INDEX + MATCH`** — Excel Master হওয়ার জন্য এটি খুব গুরুত্বপূর্ণ chapter।



----
# 📊 Excel Mastery — Class 8

## 🔎 Lookup Functions — VLOOKUP, XLOOKUP, HLOOKUP, INDEX + MATCH

আজকের Class খুবই গুরুত্বপূর্ণ। কারণ বাস্তব Excel/Business dataset-এ প্রায়ই এমন হয়:

> একটি table থেকে ID দিয়ে অন্য table থেকে Name, Salary, Department, Price ইত্যাদি খুঁজে বের করতে হবে।

এ কাজের জন্য **Lookup Functions** ব্যবহার করি।

আজ শিখব:

```text
VLOOKUP()
XLOOKUP()
HLOOKUP()
INDEX()
MATCH()
INDEX + MATCH
```

---

# 1️⃣ Lookup কী?

ধরো আমাদের Employee ID দেওয়া আছে:

```text
E103
```

আমাদের জানতে হবে:

> E103 employee-এর নাম কী এবং salary কত?

আমাদের কাছে অন্য একটি table আছে:

|Employee ID|Name|Department|Salary|
|---|---|---|--:|
|E101|Rahim|IT|30000|
|E102|Karim|HR|35000|
|E103|Hasan|IT|40000|
|E104|Jony|Sales|28000|
|E105|Sakib|IT|45000|

যদি আমরা শুধু লিখি:

```text
E103
```

তাহলে Excel দিয়ে automatically Hasan-এর information বের করতে পারি।

এটাই **Lookup**।

---

# 2️⃣ VLOOKUP()

`VLOOKUP` মানে:

> **Vertical Lookup**

অর্থাৎ table-এর **vertical/column-wise** data থেকে খুঁজবে।

### Syntax

```excel
=VLOOKUP(lookup_value, table_array, col_index_num, range_lookup)
```

প্রথমবার দেখলে কঠিন মনে হতে পারে। আস্তে আস্তে বুঝি।

---

# 3️⃣ Basic VLOOKUP Example

ধরো A2:D6:

|A|B|C|D|
|---|---|---|--:|
|ID|Name|Department|Salary|
|E101|Rahim|IT|30000|
|E102|Karim|HR|35000|
|E103|Hasan|IT|40000|
|E104|Jony|Sales|28000|
|E105|Sakib|IT|45000|

F2-তে:

```text
E103
```

আমরা Name বের করতে চাই।

Formula:

```excel
=VLOOKUP(F2,A2:D6,2,FALSE)
```

Result:

```text
Hasan
```

---

# 4️⃣ Formula ভেঙে বুঝি

```excel
=VLOOKUP(F2,A2:D6,2,FALSE)
```

|অংশ|অর্থ|
|---|---|
|`F2`|কী খুঁজব?|
|`A2:D6`|কোথায় খুঁজব?|
|`2`|কোন column থেকে result নেব?|
|`FALSE`|Exact match চাই|

অর্থাৎ:

> F2-এর ID-টি A2:D6 table-এ খুঁজে দ্বিতীয় column-এর value দাও।

---

# 5️⃣ Column Number কীভাবে বুঝব?

Table:

|Column|Number|
|---|--:|
|ID|1|
|Name|2|
|Department|3|
|Salary|4|

তাই:

### Name

```excel
=VLOOKUP(F2,A2:D6,2,FALSE)
```

### Department

```excel
=VLOOKUP(F2,A2:D6,3,FALSE)
```

### Salary

```excel
=VLOOKUP(F2,A2:D6,4,FALSE)
```

---

# 6️⃣ FALSE কেন?

এটা খুব গুরুত্বপূর্ণ।

```excel
FALSE
```

মানে:

> **Exact match**

যদি F2 = `E103` হয়, Excel ঠিক `E103`-ই খুঁজবে।

সাধারণ ID, Name, Product Code ইত্যাদির lookup-এ সাধারণত:

```excel
FALSE
```

ব্যবহার করো।

---

# 7️⃣ TRUE কী?

```excel
TRUE
```

মানে approximate match।

এটি কিছু নির্দিষ্ট ক্ষেত্রে useful, যেমন:

- Grade
    
- Tax slab
    
- Commission
    
- Price range
    

উদাহরণ:

|Minimum Score|Grade|
|--:|---|
|0|F|
|40|D|
|50|C|
|60|B|
|70|A|
|80|A+|

এখানে approximate lookup ব্যবহার করা যায়।

তবে beginner হিসেবে আপাতত সবচেয়ে বেশি মনে রাখো:

```text
ID/Product Code/Name lookup → FALSE
```

---

# 8️⃣ VLOOKUP-এর বড় Limitation ⚠️

VLOOKUP-এর একটি গুরুত্বপূর্ণ limitation আছে।

**যে value খুঁজবে সেটি table-এর প্রথম column-এ থাকতে হবে।**

যেমন:

|ID|Name|Salary|
|---|---|--:|
|E101|Rahim|30000|
|E102|Karim|35000|

ID দিয়ে Name খোঁজা যায়।

কিন্তু Name দিয়ে ID খুঁজতে গেলে:

```text
Name → ID
```

VLOOKUP সহজে করতে পারে না, কারণ Name প্রথম column নয়।

এখানেই **XLOOKUP** অনেক better।

---

# 9️⃣ XLOOKUP()

Modern Excel-এ `XLOOKUP()` অত্যন্ত useful।

এটি VLOOKUP-এর তুলনায় অনেক flexible।

### Basic Syntax

```excel
=XLOOKUP(lookup_value, lookup_array, return_array)
```

---

# 🔟 XLOOKUP Example

আগের table:

|ID|Name|Department|Salary|
|---|---|---|--:|
|E101|Rahim|IT|30000|
|E102|Karim|HR|35000|
|E103|Hasan|IT|40000|
|E104|Jony|Sales|28000|
|E105|Sakib|IT|45000|

F2:

```text
E103
```

Name:

```excel
=XLOOKUP(F2,A2:A6,B2:B6)
```

Result:

```text
Hasan
```

এখানে:

```text
A2:A6 → ID খুঁজবে
B2:B6 → Name return করবে
```

---

# 1️⃣1️⃣ XLOOKUP দিয়ে Salary

```excel
=XLOOKUP(F2,A2:A6,D2:D6)
```

Result:

```text
40000
```

---

# 1️⃣2️⃣ Name দিয়ে ID খোঁজা

এটাই XLOOKUP-এর শক্তি।

ধরো F2:

```text
Hasan
```

ID বের করতে:

```excel
=XLOOKUP(F2,B2:B6,A2:A6)
```

Result:

```text
E103
```

🔥 এখানে lookup column এবং return column-এর যেকোনো direction হতে পারে।

---

# 1️⃣3️⃣ VLOOKUP বনাম XLOOKUP

|Feature|VLOOKUP|XLOOKUP|
|---|---|---|
|Vertical lookup|✅|✅|
|Exact match|✅|✅|
|Left-side lookup|❌|✅|
|Column number দরকার|✅|❌|
|Flexible|কম|বেশি|
|Modern|পুরোনো|নতুন|
|Missing value handling|সীমিত|সহজ|

### Practical recommendation

যদি তোমার Excel version-এ XLOOKUP থাকে:

> **XLOOKUP শেখা এবং ব্যবহার করা বেশি ভালো।**

তবে চাকরি/পুরোনো Excel files-এর জন্য **VLOOKUP অবশ্যই জানতে হবে।**

---

# 1️⃣4️⃣ XLOOKUP-এ Not Found Message

ধরো F2:

```text
E999
```

কিন্তু E999 table-এ নেই।

সাধারণ XLOOKUP error দেখাতে পারে।

তুমি custom message দিতে পারো:

```excel
=XLOOKUP(F2,A2:A6,B2:B6,"Not Found")
```

তাহলে:

```text
E999
```

এর জন্য:

```text
Not Found
```

দেখাবে।

🔥 Real-world dashboard/data cleaning-এ এটি useful।

---

# 1️⃣5️⃣ HLOOKUP()

`HLOOKUP` মানে:

> **Horizontal Lookup**

VLOOKUP যেখানে column-wise খোঁজে, HLOOKUP row-wise খোঁজে।

ধরো:

||Jan|Feb|Mar|Apr|
|---|--:|--:|--:|--:|
|Sales|50000|60000|55000|70000|

যদি Jan-এর sales খুঁজতে চাই:

```excel
=HLOOKUP("Jan",B1:E2,2,FALSE)
```

Result:

```text
50000
```

### মনে রাখো

```text
VLOOKUP → Vertical
HLOOKUP → Horizontal
```

বর্তমানে HLOOKUP-এর ব্যবহার তুলনামূলক কম, কারণ XLOOKUP বেশি flexible।

---

# 1️⃣6️⃣ MATCH()

`MATCH()` কোনো value **কোন position-এ আছে** সেটা খুঁজে দেয়।

ধরো:

|A|
|---|
|Rahim|
|Karim|
|Hasan|
|Jony|
|Sakib|

Formula:

```excel
=MATCH("Hasan",A2:A6,0)
```

Result:

```text
3
```

কারণ range-এর মধ্যে Hasan হলো 3rd item।

```text
Rahim → 1
Karim → 2
Hasan → 3
Jony  → 4
Sakib → 5
```

---

# 1️⃣7️⃣ MATCH-এর `0`

```excel
=MATCH("Hasan",A2:A6,0)
```

এখানে:

```text
0 → Exact Match
```

ID/name-এর মতো exact lookup-এর জন্য এটা useful।

---

# 1️⃣8️⃣ INDEX()

`INDEX()` একটি range থেকে নির্দিষ্ট position-এর value দেয়।

ধরো:

|A|
|---|
|Rahim|
|Karim|
|Hasan|
|Jony|
|Sakib|

```excel
=INDEX(A2:A6,3)
```

Result:

```text
Hasan
```

কারণ range-এর 3rd value হলো Hasan।

---

# 1️⃣9️⃣ INDEX + MATCH

এখন Excel-এর একটি খুব powerful combination শিখি:

```text
INDEX + MATCH
```

ধরো:

|ID|Name|Salary|
|---|---|--:|
|E101|Rahim|30000|
|E102|Karim|35000|
|E103|Hasan|40000|
|E104|Jony|28000|
|E105|Sakib|45000|

F2:

```text
E103
```

Salary বের করতে:

```excel
=INDEX(C2:C6,MATCH(F2,A2:A6,0))
```

Result:

```text
40000
```

---

# 2️⃣0️⃣ INDEX + MATCH কীভাবে কাজ করছে?

Formula:

```excel
=INDEX(C2:C6,MATCH(F2,A2:A6,0))
```

প্রথমে:

```excel
MATCH(F2,A2:A6,0)
```

E103 কোথায়?

```text
3
```

তারপর:

```excel
INDEX(C2:C6,3)
```

3rd salary:

```text
40000
```

তাই final result:

```text
40000
```

---

# 🧠 সহজভাবে মনে রাখো

```text
MATCH → Position খুঁজে দেয়
INDEX → সেই position-এর value দেয়
```

অর্থাৎ:

```text
MATCH = কোথায়?
INDEX = সেখানে কী আছে?
```

---

# 2️⃣1️⃣ Real-World Example — Product Price

ধরো Product table:

|Product ID|Product|Price|
|---|---|--:|
|P101|Laptop|80000|
|P102|Mouse|1000|
|P103|Keyboard|2000|
|P104|Monitor|20000|
|P105|Headphone|3000|

F2:

```text
P104
```

XLOOKUP:

```excel
=XLOOKUP(F2,A2:A6,C2:C6)
```

Result:

```text
20000
```

---

# 2️⃣2️⃣ Product Name-ও বের করা

```excel
=XLOOKUP(F2,A2:A6,B2:B6)
```

Result:

```text
Monitor
```

এভাবে একটি Product ID দিয়ে পুরো product information বের করা যায়।

---

# 2️⃣3️⃣ Multiple Information Lookup

ধরো F2:

```text
P103
```

G2:

```excel
=XLOOKUP(F2,A2:A6,B2:B6)
```

→ Keyboard

H2:

```excel
=XLOOKUP(F2,A2:A6,C2:C6)
```

→ 2000

এখন তোমার একটি ছোট lookup system তৈরি হয়ে গেল।

---

# ⚠️ Beginner Mistakes

### Mistake 1 — VLOOKUP-এর column number ভুল

```excel
=VLOOKUP(F2,A2:D6,3,FALSE)
```

এখানে 3 মানে Department।

4 দিলে Salary।

---

### Mistake 2 — FALSE না দেওয়া

ID lookup-এর ক্ষেত্রে:

```excel
=VLOOKUP(F2,A2:D6,2,FALSE)
```

Exact match ব্যবহার করাই safest।

---

### Mistake 3 — Lookup column প্রথমে না রাখা

VLOOKUP:

```text
ID → Name
```

সহজে পারে।

কিন্তু:

```text
Name → ID
```

সরাসরি পারে না।

XLOOKUP পারে।

---

### Mistake 4 — XLOOKUP না পাওয়া

কিছু পুরোনো Excel version-এ `XLOOKUP()` available নাও থাকতে পারে।

তখন:

```text
VLOOKUP
INDEX + MATCH
```

ব্যবহার করা যায়।

---

# 🧠 Class 8 Cheat Sheet

```text
VLOOKUP
→ Vertical lookup

XLOOKUP
→ Modern & flexible lookup

HLOOKUP
→ Horizontal lookup

MATCH
→ Position খুঁজে

INDEX
→ Position থেকে value দেয়

INDEX + MATCH
→ Powerful lookup combination
```

---

# 🎯 Class 8 Assignment

দুটি table তৈরি করো।

### Table 1 — Employee

|Employee ID|Name|Department|
|---|---|---|
|E101|Rahim|IT|
|E102|Karim|HR|
|E103|Hasan|IT|
|E104|Jony|Sales|
|E105|Sakib|IT|

### Table 2 — Salary

|Employee ID|Salary|
|---|--:|
|E101|30000|
|E102|35000|
|E103|40000|
|E104|28000|
|E105|45000|

এখন Table 1-এ নতুন column বানাও:

```text
Employee ID | Name | Department | Salary
```

### Task 1

VLOOKUP দিয়ে Salary বের করো।

### Task 2

XLOOKUP দিয়ে Salary বের করো।

### Task 3

XLOOKUP দিয়ে Department বের করো।

### Task 4

`MATCH()` ব্যবহার করে `E103` কোন position-এ আছে বের করো।

### Task 5

`INDEX()` ব্যবহার করে 3rd employee-এর Name বের করো।

### Task 6

INDEX + MATCH দিয়ে E104-এর Salary বের করো।

### Task 7 ⭐

একটি cell-এ Employee ID input দিলে অন্য cell-এ automatically:

```text
Name
Department
Salary
```

দেখানোর চেষ্টা করো।

এটা করলে তুমি একটি **mini Employee Lookup System** বানিয়ে ফেলবে।

---

# 📝 Class 8 Quiz

**1. VLOOKUP-এর V কী বোঝায়?**

A. Value  
B. Vertical  
C. Variable  
D. Visual

**2. VLOOKUP-এ exact match-এর জন্য সাধারণত কী ব্যবহার করি?**

A. TRUE  
B. FALSE  
C. 1  
D. -1

**3. VLOOKUP-এর 3 কী বোঝায়?**

A. Row number  
B. Search value  
C. Column index  
D. Number of rows

**4. কোন function left-side lookup করতে পারে?**

A. VLOOKUP  
B. XLOOKUP  
C. HLOOKUP  
D. SUM

**5. MATCH কী return করে?**

A. Value  
B. Position  
C. Table  
D. Column

**6. INDEX কী করে?**

A. Position থেকে value retrieve করে  
B. Data sort করে  
C. Data delete করে  
D. Number count করে

**7. HLOOKUP কোন direction-এ কাজ করে?**

A. Vertical  
B. Horizontal  
C. Diagonal  
D. Random

**8. `=MATCH("Hasan",A2:A6,0)`-এর `0` কী বোঝায়?**

A. Approximate match  
B. Exact match  
C. First row  
D. Last row

**9. `INDEX + MATCH` কেন useful?**

A. Formatting-এর জন্য  
B. Flexible lookup-এর জন্য  
C. Chart তৈরির জন্য  
D. Cell color-এর জন্য

**10. Modern Excel-এ সাধারণত VLOOKUP-এর চেয়ে কোনটি বেশি flexible?**

A. SUM  
B. HLOOKUP  
C. XLOOKUP  
D. COUNT

---

## ⭐ আজকের সবচেয়ে গুরুত্বপূর্ণ অংশ

শুধু সবগুলো মুখস্থ না করে এই flow-টা বুঝো:

```text
VLOOKUP
   ↓
XLOOKUP
   ↓
MATCH → Position
INDEX → Value
   ↓
INDEX + MATCH → Powerful Lookup
```

**বিশেষ করে `VLOOKUP` এবং `XLOOKUP` হাতে-কলমে 5–10 বার practice করো।** পরের **Class 9**-এ আমরা `SUMIF`, `COUNTIF`, `AVERAGEIF`, `SUMIFS`, `COUNTIFS`, `AVERAGEIFS` শিখব—এগুলো দিয়ে condition অনুযায়ী data থেকে **Total, Count এবং Average** বের করা যাবে।


---
# 📊 Excel Mastery — Class 9

## 🎯 Conditional Functions — SUMIF, COUNTIF, AVERAGEIF, SUMIFS, COUNTIFS, AVERAGEIFS

Class 8-এ আমরা **Lookup** শিখেছি।  
আজ শিখব Excel-এর সবচেয়ে useful analytical functions-এর একটি group।

ধরো তোমার কাছে 1,000 employee-এর data আছে।

তুমি জানতে চাও:

- শুধু **IT department-এর total salary** কত?
    
- **Dhaka-এর কতজন employee** আছে?
    
- **IT department-এর average salary** কত?
    
- **IT + Dhaka**—দুই condition মিলে total salary কত?
    

প্রতিটি row manually calculate করার দরকার নেই।

এখানেই:

```text
SUMIF
COUNTIF
AVERAGEIF
SUMIFS
COUNTIFS
AVERAGEIFS
```

---

# 1️⃣ IF আর IF-based functions-এর পার্থক্য

Class 5-এ:

```excel
=IF(B2>=40,"Pass","Fail")
```

এটা **প্রতিটি row-এর condition** check করে।

আজ:

```excel
=SUMIF(...)
```

মানে:

> Condition অনুযায়ী অনেকগুলো row-এর data **যোগ** করো।

---

# 2️⃣ COUNTIF()

## একটি condition অনুযায়ী কতগুলো data আছে

ধরো:

|Employee|Department|
|---|---|
|Rahim|IT|
|Karim|HR|
|Hasan|IT|
|Jony|Sales|
|Sakib|IT|

আমরা জানতে চাই:

> কতজন IT department-এ আছে?

Formula:

```excel
=COUNTIF(B2:B6,"IT")
```

Result:

```text
3
```

কারণ:

```text
Rahim → IT
Hasan → IT
Sakib → IT
```

---

# 3️⃣ COUNTIF Syntax

```excel
=COUNTIF(range, criteria)
```

|অংশ|অর্থ|
|---|---|
|`range`|কোথায় condition check করবে|
|`criteria`|কী খুঁজবে|

Example:

```excel
=COUNTIF(B2:B6,"IT")
```

```text
B2:B6 → Department column
"IT"  → condition
```

---

# 4️⃣ COUNTIF দিয়ে City Count

|Employee|City|
|---|---|
|Rahim|Dhaka|
|Karim|Chittagong|
|Hasan|Dhaka|
|Jony|Sylhet|
|Sakib|Dhaka|

Dhaka-তে কতজন?

```excel
=COUNTIF(B2:B6,"Dhaka")
```

Result:

```text
3
```

---

# 5️⃣ COUNTIF with Number

ধরো Marks:

|Student|Marks|
|---|--:|
|Rahim|80|
|Karim|35|
|Hasan|65|
|Jony|45|
|Sakib|90|

40 বা তার বেশি কতজন?

```excel
=COUNTIF(B2:B6,">=40")
```

Result:

```text
4
```

⚠️ এখানে condition quotation mark-এর মধ্যে থাকবে:

```excel
">=40"
```

---

# 6️⃣ COUNTIF-এর কিছু গুরুত্বপূর্ণ Criteria

|Requirement|Formula|
|---|---|
|50-এর বেশি|`">50"`|
|50-এর বেশি/সমান|`">=50"`|
|50-এর কম|`"<50"`|
|50-এর কম/সমান|`"<=50"`|
|50 নয়|`"<>50"`|
|ঠিক 50|`50`|

---

# 7️⃣ SUMIF()

এখন আমরা condition অনুযায়ী **যোগ** করব।

Dataset:

|Employee|Department|Salary|
|---|---|--:|
|Rahim|IT|30000|
|Karim|HR|35000|
|Hasan|IT|40000|
|Jony|Sales|28000|
|Sakib|IT|45000|

Question:

> IT department-এর total salary কত?

Formula:

```excel
=SUMIF(B2:B6,"IT",C2:C6)
```

Result:

```text
115000
```

কারণ:

```text
30000 + 40000 + 45000
= 115000
```

---

# 8️⃣ SUMIF Syntax

```excel
=SUMIF(range, criteria, sum_range)
```

এখানে:

```text
range
↓
যেখানে condition check করবে

criteria
↓
কোন condition?

sum_range
↓
কোন column যোগ করবে?
```

Example:

```excel
=SUMIF(B2:B6,"IT",C2:C6)
```

```text
B2:B6 → Department
"IT"  → condition
C2:C6 → Salary যোগ করবে
```

---

# 9️⃣ SUMIF — Sales Example

|Product|Category|Sales|
|---|---|--:|
|Laptop|Electronics|80000|
|Shirt|Clothing|3000|
|Mouse|Electronics|1000|
|Pant|Clothing|2500|
|Monitor|Electronics|20000|

Electronics-এর total sales:

```excel
=SUMIF(B2:B6,"Electronics",C2:C6)
```

Result:

```text
101000
```

---

# 🔟 AVERAGEIF()

Condition অনুযায়ী **average** বের করে।

আগের employee dataset:

|Employee|Department|Salary|
|---|---|--:|
|Rahim|IT|30000|
|Karim|HR|35000|
|Hasan|IT|40000|
|Jony|Sales|28000|
|Sakib|IT|45000|

IT employees-এর average salary:

```excel
=AVERAGEIF(B2:B6,"IT",C2:C6)
```

Result:

```text
38333.33
```

কারণ:

```text
(30000 + 40000 + 45000) / 3
= 38333.33
```

---

# 1️⃣1️⃣ AVERAGEIF Syntax

```excel
=AVERAGEIF(range, criteria, average_range)
```

অর্থাৎ:

```text
কোন range-এ condition?
        ↓
কী condition?
        ↓
কোন values-এর average?
```

---

# 1️⃣2️⃣ এখন Multiple Conditions 🔥

এখন আসল advanced অংশ।

ধরো:

|Employee|Department|City|Salary|
|---|---|---|--:|
|Rahim|IT|Dhaka|30000|
|Karim|HR|Dhaka|35000|
|Hasan|IT|Chittagong|40000|
|Jony|Sales|Dhaka|28000|
|Sakib|IT|Dhaka|45000|

Question:

> **IT AND Dhaka** employees-এর total salary কত?

এখানে দুইটি condition:

```text
Department = IT
AND
City = Dhaka
```

এখানে `SUMIFS()` ব্যবহার করব।

---

# 1️⃣3️⃣ SUMIFS()

Formula:

```excel
=SUMIFS(D2:D6,B2:B6,"IT",C2:C6,"Dhaka")
```

Result:

```text
75000
```

কারণ:

```text
Rahim → IT + Dhaka → 30000
Sakib → IT + Dhaka → 45000

Total = 75000
```

---

# 1️⃣4️⃣ SUMIF বনাম SUMIFS

### SUMIF

একটি condition:

```excel
=SUMIF(B2:B6,"IT",D2:D6)
```

### SUMIFS

Multiple conditions:

```excel
=SUMIFS(D2:D6,B2:B6,"IT",C2:C6,"Dhaka")
```

মনে রাখো:

```text
SUMIF  → 1 condition
SUMIFS → 2 বা তার বেশি conditions
```

---

# 1️⃣5️⃣ SUMIFS-এর Syntax

```excel
=SUMIFS(sum_range, criteria_range1, criteria1, criteria_range2, criteria2)
```

Example:

```excel
=SUMIFS(D2:D6,B2:B6,"IT",C2:C6,"Dhaka")
```

এখানে:

```text
D2:D6      → Salary যোগ করবে

B2:B6      → প্রথম condition range
"IT"       → প্রথম condition

C2:C6      → দ্বিতীয় condition range
"Dhaka"    → দ্বিতীয় condition
```

---

# 1️⃣6️⃣ COUNTIFS()

একাধিক condition মিলে কতগুলো row আছে সেটা count করে।

উপরের dataset:

> কতজন **IT + Dhaka** employee আছে?

```excel
=COUNTIFS(B2:B6,"IT",C2:C6,"Dhaka")
```

Result:

```text
2
```

Rahim এবং Sakib।

---

# 1️⃣7️⃣ AVERAGEIFS()

Multiple conditions অনুযায়ী average।

Question:

> IT + Dhaka employees-এর average salary কত?

```excel
=AVERAGEIFS(D2:D6,B2:B6,"IT",C2:C6,"Dhaka")
```

Result:

```text
37500
```

কারণ:

```text
(30000 + 45000) / 2
= 37500
```

---

# 1️⃣8️⃣ তিনটি Multiple-condition Function

এগুলো পাশাপাশি মনে রাখো:

```text
SUMIFS
↓
Condition অনুযায়ী Total

COUNTIFS
↓
Condition অনুযায়ী Count

AVERAGEIFS
↓
Condition অনুযায়ী Average
```

---

# 1️⃣9️⃣ Number Condition

ধরো:

|Employee|Department|Salary|
|---|---|--:|
|Rahim|IT|30000|
|Karim|HR|55000|
|Hasan|IT|60000|
|Jony|Sales|28000|
|Sakib|IT|70000|

IT department-এ salary `>=50000` এমন কতজন?

```excel
=COUNTIFS(B2:B6,"IT",C2:C6,">=50000")
```

Result:

```text
2
```

Hasan এবং Sakib।

---

# 2️⃣0️⃣ SUMIFS + Number Condition

IT department-এর যাদের salary `>=50000`, তাদের salary total:

```excel
=SUMIFS(C2:C6,B2:B6,"IT",C2:C6,">=50000")
```

Result:

```text
130000
```

কারণ:

```text
60000 + 70000
= 130000
```

---

# 2️⃣1️⃣ Cell Reference ব্যবহার করা ⭐

Criteria সরাসরি লেখার পাশাপাশি cell reference ব্যবহার করা যায়।

ধরো:

```text
F2 = IT
```

Formula:

```excel
=COUNTIF(B2:B6,F2)
```

এখন F2-তে `IT` বদলে `HR` লিখলে formula automatically HR count করবে।

🔥 Dashboard তৈরির সময় এটা খুব useful।

---

# 2️⃣2️⃣ Dynamic Condition

ধরো:

```text
F2 = 50000
```

আমরা চাই:

> Salary 50000-এর বেশি কতজন?

Formula:

```excel
=COUNTIF(C2:C6,">"&F2)
```

এখানে:

```text
">"
```

এবং:

```text
F2
```

কে `&` দিয়ে combine করেছি।

Result:

```text
2
```

---

# 2️⃣3️⃣ Wildcard — Text Search

এখন একটা নতুন concept।

### `*`

`*` মানে যেকোনো সংখ্যক character।

ধরো:

|Name|
|---|
|Rahim|
|Karim|
|Hasan|
|Rahman|

যেসব name `Rah` দিয়ে শুরু:

```excel
=COUNTIF(A2:A5,"Rah*")
```

এতে:

```text
Rahim
Rahman
```

match হবে।

---

# 2️⃣4️⃣ `?` Wildcard

`?` একটি character represent করে।

ধরো:

```text
Cat
Cut
Cot
Cart
```

Formula:

```excel
=COUNTIF(A2:A5,"C?t")
```

এতে:

```text
Cat
Cut
Cot
```

match হবে।

কারণ:

```text
C + one character + t
```

---

# 2️⃣5️⃣ Real-World Sales Analysis

এই dataset তৈরি করো:

|Product|Category|City|Sales|
|---|---|---|--:|
|Laptop|Electronics|Dhaka|80000|
|Mouse|Electronics|Dhaka|1000|
|Shirt|Clothing|Dhaka|3000|
|Keyboard|Electronics|Chittagong|2000|
|Monitor|Electronics|Dhaka|20000|
|Pant|Clothing|Chittagong|2500|
|Headphone|Electronics|Dhaka|3000|

### Question 1

Electronics product কতটি?

```excel
=COUNTIF(B2:B8,"Electronics")
```

---

### Question 2

Electronics-এর total sales:

```excel
=SUMIF(B2:B8,"Electronics",D2:D8)
```

---

### Question 3

Electronics-এর average sales:

```excel
=AVERAGEIF(B2:B8,"Electronics",D2:D8)
```

---

### Question 4

Dhaka-এর total sales:

```excel
=SUMIF(C2:C8,"Dhaka",D2:D8)
```

---

### Question 5

Electronics + Dhaka-এর total sales:

```excel
=SUMIFS(D2:D8,B2:B8,"Electronics",C2:C8,"Dhaka")
```

---

### Question 6

Electronics + Dhaka product count:

```excel
=COUNTIFS(B2:B8,"Electronics",C2:C8,"Dhaka")
```

---

### Question 7

Electronics + Dhaka-এর average sales:

```excel
=AVERAGEIFS(D2:D8,B2:B8,"Electronics",C2:C8,"Dhaka")
```

---

# ⚠️ Beginner Mistakes

### Mistake 1 — SUMIF-এর order ভুল করা

❌:

```excel
=SUMIF("IT",B2:B6,C2:C6)
```

✅:

```excel
=SUMIF(B2:B6,"IT",C2:C6)
```

---

### Mistake 2 — SUMIF vs SUMIFS

```text
SUMIF
→ এক condition

SUMIFS
→ multiple conditions
```

---

### Mistake 3 — Number criteria-তে quotation ভুল

সঠিক:

```excel
=COUNTIF(C2:C10,">=50")
```

Dynamic হলে:

```excel
=COUNTIF(C2:C10,">="&F2)
```

---

### Mistake 4 — Criteria range ও sum range-এর size আলাদা

যেমন:

```excel
B2:B10
```

এর সঙ্গে:

```excel
C2:C10
```

ব্যবহার করো।

একটি B2:B10 এবং অন্যটি C2:C15 হলে ভুল result/error হতে পারে।

---

# 🧠 Class 9 Cheat Sheet

|Function|কাজ|
|---|---|
|`COUNTIF`|1 condition → Count|
|`SUMIF`|1 condition → Total|
|`AVERAGEIF`|1 condition → Average|
|`COUNTIFS`|Multiple conditions → Count|
|`SUMIFS`|Multiple conditions → Total|
|`AVERAGEIFS`|Multiple conditions → Average|

### সবচেয়ে সহজ Memory Trick:

```text
COUNT → কতজন?
SUM → মোট কত?
AVERAGE → গড় কত?

IF → ১ condition
IFS → Multiple conditions
```

---

# 📝 Class 9 Quiz

**1. IT department-এর employee count করতে কোন function?**

A. `SUMIF`  
B. `COUNTIF`  
C. `AVERAGEIF`  
D. `COUNT`

**2. IT department-এর total salary বের করতে?**

A. `COUNTIF`  
B. `SUMIF`  
C. `SUMIFS`  
D. `AVERAGEIF`

**3. একটি condition অনুযায়ী average বের করতে?**

A. `AVERAGEIF`  
B. `AVERAGEIFS`  
C. `SUMIF`  
D. `COUNTIF`

**4. IT + Dhaka employee count করতে?**

A. `COUNTIF`  
B. `COUNTIFS`  
C. `SUMIF`  
D. `COUNTA`

**5. IT + Dhaka-এর total salary বের করতে?**

A. `SUMIF`  
B. `SUMIFS`  
C. `COUNTIFS`  
D. `AVERAGEIF`

**6. `">=50000"` কী ধরনের criteria?**

A. Text  
B. Number condition  
C. Function  
D. Range

**7. `SUMIF`-এ প্রথম argument কী?**

A. Sum range  
B. Criteria  
C. Criteria range  
D. Cell

**8. `*` wildcard-এর অর্থ কী?**

A. একটি character  
B. যেকোনো সংখ্যক character  
C. Number only  
D. Blank

**9. `?` wildcard-এর অর্থ কী?**

A. যেকোনো সংখ্যক character  
B. একটি character  
C. Number  
D. Space

**10. `COUNTIF(B2:B10,"IT")` কী করবে?**

A. IT-এর salary যোগ করবে  
B. IT-এর average করবে  
C. IT কতবার আছে count করবে  
D. IT delete করবে

---

## 🎯 আজকের Mastery Target

আজ এই pattern-টা মাথায় বসাও:

```text
                1 Condition       Multiple Conditions

COUNT           COUNTIF           COUNTIFS
SUM             SUMIF             SUMIFS
AVERAGE         AVERAGEIF         AVERAGEIFS
```

এটা বুঝে গেলে Excel-এর **data analysis** অনেক শক্তিশালী হয়ে যাবে।

**পরের Class 10 → Data Cleaning & Data Preparation:** `TRIM`, `CLEAN`, `Remove Duplicates`, `Text to Columns`, `Find & Replace`, blanks/missing data, inconsistent values এবং একটি messy dataset-কে professional dataset-এ convert করা।



----
# 📘 Excel Mastery — Class 10

## Data Cleaning & Data Preparation

আজ থেকে আমরা Excel-এর **real-world data handling** শুরু করছি। এতদিন formula/function শিখেছি; এখন শিখব **messy data → clean professional data** বানানো।

> **Goal:** একটি raw dataset দেখে সমস্যা identify করা → clean করা → analysis-এর জন্য ready করা।

---

# 1️⃣ Data Cleaning কী?

ধরো তোমাকে এই data দেওয়া হলো:

|Name|Department|City|Salary|
|---|---|---|--:|
|atiar rahman|IT|Dhaka|35000|
|Atiar Rahman|IT|Dhaka|35000|
|Rahim|it|DHAKA|40000|
|Karim|IT|Chittagong||
|Nusrat|HR|Dhaka|45000|

এখানে বিভিন্ন সমস্যা আছে:

- Duplicate record
    
- Extra spaces
    
- `IT` / `it`
    
- `Dhaka` / `DHAKA`
    
- Missing salary
    

এই সমস্যাগুলো ঠিক করাই **Data Cleaning**।

---

# 2️⃣ TRIM — Extra Space Remove

Class 6-এ আমরা TRIM শিখেছিলাম। আজ এটাকে real dataset-এ ব্যবহার করব।

### Example

A2:

```text
   Rahim Ahmed   
```

Formula:

```excel
=TRIM(A2)
```

Result:

```text
Rahim Ahmed
```

### TRIM কী করে?

Extra spaces remove করে।

বিশেষ করে user input বা অন্য system থেকে data import করার সময় খুব useful।

---

# 3️⃣ CLEAN — Hidden/Non-printing Character Remove

কখনো অন্য system থেকে copy করা data-তে invisible/non-printing characters থাকতে পারে।

```excel
=CLEAN(A2)
```

আর যদি extra space-ও থাকে:

```excel
=TRIM(CLEAN(A2))
```

### ⭐ মনে রাখবে

```text
TRIM  → Extra spaces
CLEAN → Non-printing characters
```

দুটো একসাথে:

```excel
=TRIM(CLEAN(A2))
```

---

# 4️⃣ TRIM + PROPER

Name clean করার জন্য খুব useful combination:

```excel
=PROPER(TRIM(A2))
```

যদি A2 হয়:

```text
   atiar rahman
```

Result:

```text
Atiar Rahman
```

### কিন্তু সাবধান ⚠️

সব ধরনের data-তে PROPER ব্যবহার করা যাবে না।

যেমন:

```text
iPhone
SQL
USA
```

এগুলোর capitalization পরিবর্তন হয়ে যেতে পারে।

তাই **name-এর মতো data-তে** PROPER ব্যবহার করা বেশি appropriate।

---

# 5️⃣ CLEAN করার পর Original Data কী করব?

এটা beginner-দের খুব common problem।

ধরো A column-এ original Name:

|A|
|---|
|`atiar rahman`|
|`rahim`|

B column:

```excel
=PROPER(TRIM(A2))
```

তারপর:

|A|B|
|---|---|
|`atiar rahman`|Atiar Rahman|
|`rahim`|Rahim|

এখন B হলো cleaned data।

### কিন্তু B formula-এর উপর নির্ভর করছে A-এর উপর।

তাই final করার সময়:

**Copy → Paste Special → Values**

করতে হয়।

তখন formula না থেকে শুধু cleaned value থাকবে।

---

# 6️⃣ Remove Duplicates

এটি খুব important।

ধরো:

|Employee_ID|Name|Department|
|---|---|---|
|101|Atiar|IT|
|102|Rahim|HR|
|101|Atiar|IT|
|103|Karim|IT|

Employee `101` duplicate।

### Remove করার নিয়ম:

1. পুরো dataset select করো
    
2. **Data**
    
3. **Remove Duplicates**
    
4. কোন column দিয়ে duplicate identify করবে select করো
    
5. **OK**
    

Excel duplicate records identify করে remove করবে।

---

# 7️⃣ খুব গুরুত্বপূর্ণ: কোন column দিয়ে duplicate?

এখানে বুঝতে হবে **duplicate বলতে কী বোঝানো হচ্ছে।**

ধরো:

|ID|Name|City|
|---|---|---|
|101|Atiar|Dhaka|
|102|Atiar|Dhaka|

Name একই হলেও employee আলাদা।

তাই শুধু `Name` দিয়ে duplicate remove করা ভুল হতে পারে।

যদি `Employee_ID` unique হয়, তাহলে Employee_ID হলো better identifier।

### ⭐ Rule

> Duplicate remove করার আগে বুঝবে **কোন field uniquely identifies a record**।

---

# 8️⃣ Find & Replace

ধরো Department-এ আছে:

```text
IT
it
It
```

তুমি সবগুলোকে:

```text
IT
```

করতে চাও।

### Method

**Ctrl + H**

তারপর:

Find:

```text
it
```

Replace with:

```text
IT
```

তারপর **Replace All**।

---

# 9️⃣ City Standardization

ধরো:

|City|
|---|
|Dhaka|
|DHAKA|
|dhaka|
|Dhaka|
|Chittagong|
|chittagong|

এগুলো analysis-এর জন্য inconsistent।

একটি standard format দরকার।

Formula দিয়ে:

```excel
=PROPER(TRIM(A2))
```

Result:

|Original|Clean|
|---|---|
|`DHAKA`|Dhaka|
|`dhaka`|Dhaka|
|`Dhaka`|Dhaka|
|`chittagong`|Chittagong|

---

# 🔟 Text to Columns

এটা খুব important Excel skill।

ধরো A column:

```text
Atiar,IT,Dhaka
Rahim,HR,Chittagong
Karim,IT,Khulna
```

তুমি এগুলো আলাদা column করতে চাও:

|Name|Department|City|
|---|---|---|
|Atiar|IT|Dhaka|
|Rahim|HR|Chittagong|
|Karim|IT|Khulna|

### Steps:

**Data → Text to Columns**

তারপর:

**Delimited → Next**

Comma select করো:

```text
,
```

তারপর **Finish**।

Excel comma অনুযায়ী data ভাগ করে দেবে।

---

# 1️⃣1️⃣ Delimiter কী?

Delimiter হলো এমন একটি character যা data আলাদা করে।

Common delimiter:

|Delimiter|Example|
|---|---|
|Comma `,`|Atiar,IT,Dhaka|
|Space|Atiar Rahman|
|Tab|data imported from another system|
|Semicolon `;`|Atiar;IT;Dhaka|
|Pipe `|`|

Text to Columns-এ delimiter correctly select করতে হয়।

---

# 1️⃣2️⃣ Flash Fill

Excel-এর একটি smart feature।

ধরো:

|Full Name|First Name|
|---|---|
|Atiar Rahman|Atiar|
|Rahim Ahmed||
|Karim Hasan||

প্রথম row manually লিখলে:

```text
Atiar
```

তারপর Excel অনেক সময় pattern বুঝে remaining rows automatically suggest করতে পারে।

Shortcut:

```text
Ctrl + E
```

এটাকে **Flash Fill** বলে।

### ⚠️ Important

Flash Fill formula-based না। তাই source data change হলে formula-এর মতো automatically recalculate করবে না।

---

# 1️⃣3️⃣ Missing Data

ধরো:

|Name|Salary|
|---|--:|
|Atiar|35000|
|Rahim||
|Karim|45000|

Rahim-এর salary missing।

এখন কী করব?

**নিজে থেকে 40000 লিখে দেওয়া যাবে না।**

কারণ আমরা জানি না আসল salary কত।

Possible approaches:

### Option 1 — Leave blank

যদি সত্যিই data unavailable হয়।

### Option 2 — `N/A`

যদি system অনুযায়ী ব্যবহার করা হয়।

### Option 3 — Source থেকে verify

সবচেয়ে ভালো option যদি original source available থাকে।

### Option 4 — Statistical replacement

যেমন average/median দিয়ে fill করা যায় **কিছু analytical situation-এ**, কিন্তু সেটা business context-এর উপর নির্ভর করে।

---

# 1️⃣4️⃣ Blank বনাম Zero

এটা খুব important।

```text
Blank ≠ 0
```

ধরো:

|Employee|Sales|
|---|--:|
|Atiar|50000|
|Rahim||
|Karim|0|

এখানে:

- Rahim → data missing
    
- Karim → actual sales may be zero
    

তাই missing value-কে blindly `0` করা যাবে না।

---

# 1️⃣5️⃣ Inconsistent Category

ধরো Department:

|Department|
|---|
|IT|
|IT|
|it|
|Information Technology|
|HR|
|Hr|

এগুলো একই category বোঝাতে পারে।

Clean করার পর ideally:

|Department|
|---|
|IT|
|IT|
|IT|
|IT|
|HR|
|HR|

কিন্তু `Information Technology → IT` conversion করার আগে business rule নিশ্চিত করতে হবে।

---

# 1️⃣6️⃣ Complete Data Cleaning Workflow ⭐

Real-world Excel কাজের সময় এই sequence follow করতে পারো:

```text
Raw Data
   ↓
Understand Columns
   ↓
Check Missing Values
   ↓
Check Duplicates
   ↓
Remove Extra Spaces
   ↓
Fix Text/Casing
   ↓
Standardize Categories
   ↓
Split Columns if Needed
   ↓
Fix Data Types
   ↓
Validate Data
   ↓
Clean Dataset
```

---

# 1️⃣7️⃣ Real Example — Raw → Clean

### 🔴 Raw Data

|ID|Name|Department|City|Salary|
|---|---|---|---|--:|
|101|`atiar rahman`|it|DHAKA|35000|
|102|`Rahim`|HR|dhaka|40000|
|101|`atiar rahman`|it|DHAKA|35000|
|103|Karim|IT|Chittagong||
|104|`nusrat`|hr|Dhaka|45000|

### Problems

1. Extra spaces
    
2. Lowercase department
    
3. Different city casing
    
4. Duplicate ID 101
    
5. Missing salary
    

### 🟢 Cleaned Data

|ID|Name|Department|City|Salary|
|---|---|---|---|--:|
|101|Atiar Rahman|IT|Dhaka|35000|
|102|Rahim|HR|Dhaka|40000|
|103|Karim|IT|Chittagong||
|104|Nusrat|HR|Dhaka|45000|

এখন dataset analysis-এর জন্য অনেক বেশি reliable।

---

# 🧠 Class 10 Cheat Sheet

|Problem|Tool/Formula|
|---|---|
|Extra spaces|`TRIM()`|
|Hidden characters|`CLEAN()`|
|Clean + spaces|`TRIM(CLEAN())`|
|Name capitalization|`PROPER()`|
|Duplicate records|Remove Duplicates|
|Find/replace values|`Ctrl + H`|
|Split one column|Text to Columns|
|Pattern-based filling|Flash Fill / `Ctrl + E`|
|Missing data|Investigate/handle carefully|
|Category inconsistency|Standardization|

---

# 📝 Class 10 Assignment

এই dataset Excel-এ তৈরি করো:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|`atiar rahman`|it|DHAKA|35000|
|102|`Rahim Ahmed`|HR|dhaka|40000|
|101|`atiar rahman`|it|DHAKA|35000|
|103|`karim`|IT|Chittagong||
|104|`NUSRAT`|hr|DHAKA|45000|
|105|`Hasan`|it|dhaka|50000|

### তোমার কাজ:

1. Name clean করো।
    
2. Department standardize করো।
    
3. City standardize করো।
    
4. Duplicate record remove করো।
    
5. Missing Salary identify করো।
    
6. কোন value missing সেটা আলাদা করে বলো।
    
7. Final cleaned dataset তৈরি করো।
    
8. Original data এবং cleaned data আলাদা রাখো।
    

---

# 🎯 Class 10 Quiz

**1. Extra spaces remove করতে কোন function ব্যবহার করা হয়?**

A. CLEAN  
B. TRIM  
C. REMOVE  
D. SPACE

**2. Duplicate records remove করার জন্য কোন option ব্যবহার হয়?**

A. Data Validation  
B. Remove Duplicates  
C. Flash Fill  
D. Text to Columns

**3. `Atiar,IT,Dhaka`-কে তিনটি column-এ ভাগ করতে কোন tool ব্যবহার করা যায়?**

A. Text to Columns  
B. SUMIF  
C. PivotTable  
D. Conditional Formatting

**4. `TRIM(CLEAN(A2))` কী করতে পারে?**

A. Number calculate  
B. Space + non-printing character clean  
C. Duplicate remove  
D. Date convert

**5. Blank salary মানেই কি salary = 0?**

A. Yes  
B. No

**6. `Ctrl + H` কীসের জন্য?**

A. Find & Replace  
B. Help  
C. Hide  
D. History

**7. Flash Fill-এর shortcut কোনটি?**

A. Ctrl + F  
B. Ctrl + E  
C. Ctrl + D  
D. Ctrl + T

**8. Duplicate remove করার আগে সবচেয়ে important কী বুঝতে হবে?**

A. Font size  
B. Unique identifier  
C. Row height  
D. Color

**9. `DHAKA`, `dhaka`, `Dhaka`—এগুলোকে একই standard format করা কোন কাজের উদাহরণ?**

A. Data sorting  
B. Data standardization  
C. Data deletion  
D. Data visualization

**10. Data cleaning-এর মূল উদ্দেশ্য কী?**

A. Dataset সুন্দর রঙ করা  
B. Data reliable এবং analysis-ready করা  
C. Formula বেশি ব্যবহার করা  
D. File size বাড়ানো


----
# 📘 Excel Mastery — Class 11

## Sort, Filter & Advanced Data Selection

আজ আমরা শিখব **dataset থেকে প্রয়োজনীয় data খুঁজে বের করা, সাজানো এবং multiple conditions দিয়ে filter করা**।

এগুলো Data Analyst-এর জন্য খুবই important।

---

# 1️⃣ Sorting কী?

**Sorting = data-কে নির্দিষ্ট order-এ সাজানো।**

যেমন Salary:

|Name|Salary|
|---|--:|
|Atiar|35000|
|Rahim|50000|
|Karim|30000|
|Nusrat|45000|

### Small → Large

```text
30000
35000
45000
50000
```

এটাকে **Ascending Order** বলে।

### Large → Small

```text
50000
45000
35000
30000
```

এটাকে **Descending Order** বলে।

---

# 2️⃣ Text Sorting

Name-ও sort করা যায়।

### A → Z

```text
Atiar
Karim
Nusrat
Rahim
```

### Z → A

```text
Rahim
Nusrat
Karim
Atiar
```

---

# 3️⃣ Excel-এ Sort করার নিয়ম

ধরো dataset:

|ID|Name|Department|Salary|
|--:|---|---|--:|
|101|Atiar|IT|35000|
|102|Rahim|HR|50000|
|103|Karim|IT|30000|
|104|Nusrat|HR|45000|

### Salary অনুযায়ী sort:

1. পুরো dataset select করো
    
2. **Data → Sort**
    
3. Sort by → `Salary`
    
4. Order → **Smallest to Largest**
    
5. OK
    

---

# ⚠️ Beginner Mistake

শুধু Salary column select করে sort করলে অন্য columns-এর সাথে employee information mismatch হয়ে যেতে পারে।

❌ ভুল:

```text
শুধু Salary column sort
```

✅ ভালো:

```text
পুরো dataset select
↓
Data → Sort
```

তাহলে পুরো row একসাথে move করবে।

---

# 4️⃣ Filter কী?

**Filter = dataset-এর মধ্যে শুধু প্রয়োজনীয় records দেখানো।**

ধরো:

|Name|Department|City|Salary|
|---|---|---|--:|
|Atiar|IT|Dhaka|35000|
|Rahim|HR|Dhaka|50000|
|Karim|IT|Chittagong|30000|
|Nusrat|HR|Dhaka|45000|

তুমি শুধু:

```text
Department = IT
```

চাও।

Filter দিলে:

|Name|Department|City|Salary|
|---|---|---|--:|
|Atiar|IT|Dhaka|35000|
|Karim|IT|Chittagong|30000|

অন্য rows **delete হয়নি**।

শুধু temporarily hide হয়েছে।

---

# 5️⃣ Filter চালু করা

Dataset-এর ভিতরে click করো:

**Data → Filter**

অথবা shortcut:

```text
Ctrl + Shift + L
```

Header-এর পাশে dropdown arrow আসবে।

---

# 6️⃣ Text Filter

Department:

```text
IT
HR
Finance
Sales
```

Filter দিয়ে:

```text
IT
```

select করলে শুধু IT employees দেখা যাবে।

---

# 7️⃣ Number Filter

Salary-এর ক্ষেত্রে অনেক useful।

ধরো তুমি দেখতে চাও:

> Salary ≥ 40000

Dropdown:

**Salary → Number Filters → Greater Than or Equal To**

তারপর:

```text
40000
```

Result:

|Name|Salary|
|---|--:|
|Rahim|50000|
|Nusrat|45000|

---

# 8️⃣ Between Filter

ধরো salary:

```text
30000 থেকে 45000
```

তাহলে:

**Number Filters → Between**

দাও:

```text
Minimum = 30000
Maximum = 45000
```

এতে ওই range-এর records দেখা যাবে।

---

# 9️⃣ Date Filter

ধরো:

|Name|Joining Date|
|---|---|
|Atiar|01/01/2024|
|Rahim|15/03/2024|
|Karim|20/06/2023|
|Nusrat|10/02/2024|

তুমি চাইলে:

```text
Year = 2024
```

অথবা:

```text
After 01/01/2024
```

এরকম date filter করতে পারো।

---

# 🔟 Multiple Filters ⭐

এটা খুব important।

ধরো তুমি চাও:

> Department = IT  
> এবং City = Dhaka

প্রথমে Department filter:

```text
IT
```

তারপর City filter:

```text
Dhaka
```

Result:

|Name|Department|City|
|---|---|---|
|Atiar|IT|Dhaka|

এখানে:

```text
Department = IT
AND
City = Dhaka
```

---

# 1️⃣1️⃣ Filter vs Sort

এই দুইটা confuse করবে না।

|Sort|Filter|
|---|---|
|Data-এর order পরিবর্তন করে|নির্দিষ্ট rows দেখায়|
|Small → Large|IT only|
|A → Z|Salary > 40000|
|সব records থাকে|কিছু records temporarily hidden|

### সহজভাবে:

**Sort = সাজানো**

**Filter = বেছে দেখা**

---

# 1️⃣2️⃣ Sort by Multiple Columns ⭐

এখন একটু advanced।

ধরো:

|Name|Department|Salary|
|---|---|--:|
|Atiar|IT|50000|
|Karim|IT|30000|
|Rahim|HR|50000|
|Nusrat|HR|40000|

তুমি চাও:

> প্রথমে Department অনুযায়ী A-Z  
> তারপর একই Department-এর মধ্যে Salary বড় থেকে ছোট।

### Data → Sort

**Sort by:**

```text
Department → A to Z
```

তারপর:

**Add Level**

```text
Then by → Salary
Order → Largest to Smallest
```

Result:

|Name|Department|Salary|
|---|---|--:|
|Rahim|HR|50000|
|Nusrat|HR|40000|
|Atiar|IT|50000|
|Karim|IT|30000|

---

# 1️⃣3️⃣ Custom Sort

Alphabetical বা numeric order ছাড়াও custom order করা যায়।

ধরো Priority:

```text
High
Medium
Low
```

তুমি চাও:

```text
High
Medium
Low
```

alphabetical নয়।

Excel-এর **Custom List** ব্যবহার করে এই ধরনের ordering করা যায়।

---

# 1️⃣4️⃣ Filter Search Box

ধরো 1000 employee আছে।

Department dropdown খুললে search box ব্যবহার করে:

```text
IT
```

লিখতে পারো।

তাহলে IT-related values দ্রুত খুঁজে পাওয়া যাবে।

---

# 1️⃣5️⃣ Clear Filter

Filter করার পর আবার সব data দেখতে চাইলে:

**Data → Clear**

অথবা individual column-এর dropdown থেকে:

**Clear Filter From...**

মনে রাখবে:

> **Clear Filter ≠ Delete Data**

Filter clear করলে records আবার দেখা যায়।

---

# 1️⃣6️⃣ Filter করলে কি Data Delete হয়?

❌ না।

ধরো 100 records আছে।

তুমি IT filter করলে 30 records দেখাচ্ছে।

এর মানে:

```text
100 records → এখনও 100
```

শুধু 70টি temporarily hidden।

---

# 1️⃣7️⃣ Excel Table ব্যবহার করলে আরও সহজ ⭐

Dataset select করে:

```text
Ctrl + T
```

দিলে Excel এটাকে **Table** বানাতে পারে।

তখন:

- Header automatically থাকে
    
- Filter dropdown থাকে
    
- New row automatically table-এর অংশ হতে পারে
    
- Formula automatically fill হতে পারে
    
- Table reference ব্যবহার করা যায়
    

Example:

```excel
=SUM(EmployeeTable[Salary])
```

---

# 1️⃣8️⃣ Sort/Filter করার আগে Dataset Rules

Professional dataset:

```text
✅ One header row
✅ No unnecessary blank rows
✅ Consistent data types
✅ Each row = one record
✅ Each column = one attribute
```

Avoid:

```text
❌ Merged cells inside dataset
❌ Multiple header rows
❌ Random blank rows
❌ Mixed data types
```

---

# 🧠 Class 11 Cheat Sheet

|Task|Tool|
|---|---|
|Small → Large|Sort Ascending|
|Large → Small|Sort Descending|
|A → Z|Sort|
|শুধু IT দেখা|Filter|
|Salary > 40000|Number Filter|
|Date অনুযায়ী|Date Filter|
|Multiple conditions|Multiple Filters|
|Multiple-level sorting|Add Level|
|Filter remove|Clear Filter|
|Table তৈরি|Ctrl + T|
|Filter on/off|Ctrl + Shift + L|

---

# 📝 Class 11 Assignment

এই dataset তৈরি করো:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Atiar|IT|Dhaka|35000|
|102|Rahim|HR|Dhaka|50000|
|103|Karim|IT|Chittagong|30000|
|104|Nusrat|HR|Dhaka|45000|
|105|Hasan|IT|Dhaka|55000|
|106|Rafi|Sales|Khulna|28000|
|107|Sumaiya|IT|Dhaka|45000|
|108|Fahim|Sales|Dhaka|40000|

### Tasks

1. Salary **Largest → Smallest** sort করো।
    
2. Name **A → Z** sort করো।
    
3. শুধু **IT** employees filter করো।
    
4. Salary **≥ 40000** filter করো।
    
5. `Department = IT` এবং `City = Dhaka` একসাথে filter করো।
    
6. Department A-Z এবং একই Department-এর মধ্যে Salary high-low sort করো।
    
7. Dataset-কে **Table (Ctrl + T)** বানাও।
    

---

# 🎯 Class 11 Quiz

**1. Sort-এর মূল কাজ কী?**

A. Data delete করা  
B. Data সাজানো  
C. Data hide করা  
D. Formula তৈরি করা

**2. Filter-এর মূল কাজ কী?**

A. Selected records দেখানো  
B. Data permanently delete করা  
C. Cell merge করা  
D. Chart তৈরি করা

**3. Smallest → Largest কোন order?**

A. Descending  
B. Ascending  
C. Random  
D. Custom

**4. Salary > 50000 করতে কোন filter ব্যবহার করবে?**

A. Text Filter  
B. Number Filter  
C. Date Filter  
D. Color Filter

**5. Filter করলে কি original data delete হয়?**

A. Yes  
B. No

**6. Multiple filters সাধারণত কোন logic-এর মতো কাজ করে?**

A. AND  
B. NOT  
C. XOR  
D. None

**7. Multiple-level sorting করতে কোন option ব্যবহার করা যায়?**

A. Add Level  
B. Add Cell  
C. Add Formula  
D. Add Chart

**8. Excel Table তৈরি করার shortcut কোনটি?**

A. Ctrl + T  
B. Ctrl + L  
C. Ctrl + R  
D. Ctrl + E

**9. Filter on/off করার shortcut কোনটি?**

A. Ctrl + F  
B. Ctrl + Shift + L  
C. Ctrl + H  
D. Ctrl + D

**10. Sort করার সময় পুরো dataset select করার প্রধান কারণ কী?**

A. Formatting সুন্দর করা  
B. Row-এর data যেন mismatch না হয়  
C. Formula delete করা  
D. File ছোট করা


----

# 📘 Excel Mastery — Class 12

## Excel Tables & Structured References ⭐

আজ আমরা শিখব **Excel Table** properly ব্যবহার করা। Class 11-এ `Ctrl + T` দিয়ে Table-এর কথা দেখেছি; আজ এর ভিতরের important features, structured references, automatic expansion এবং professional data management শিখব।

---

# 1️⃣ Excel Table কী?

সাধারণ dataset:

|ID|Name|Department|Salary|
|--:|---|---|--:|
|101|Atiar|IT|35000|
|102|Rahim|HR|40000|
|103|Karim|IT|45000|

এটাকে Excel Table বানালে Excel dataset-টাকে একটি **structured data object** হিসেবে manage করবে।

### Table বানানোর shortcut

```text
Ctrl + T
```

তারপর:

```text
My table has headers
```

select করে **OK**।

---

# 2️⃣ Table-এর সুবিধা

Table বানানোর পর automatically পাওয়া যায়:

- Filter dropdown
    
- Automatic formatting
    
- New row automatically included
    
- Formula auto-fill
    
- Structured references
    
- Easy sorting/filtering
    
- Table name
    
- Total Row
    
- Table expansion
    

এগুলো Data Analyst-এর জন্য খুব useful।

---

# 3️⃣ Table Name

Table তৈরি করলে Excel সাধারণত নাম দেয়:

```text
Table1
```

তুমি এটাকে meaningful name দিতে পারো।

যেমন:

```text
EmployeeTable
```

### কোথায়?

**Table Design → Table Name**

এভাবে নাম দিলে formula বুঝতে সহজ হয়।

---

# 4️⃣ Structured Reference কী? ⭐

এটাই আজকের সবচেয়ে important concept।

Normal formula:

```excel
=SUM(E2:E10)
```

যদি Salary column table-এর মধ্যে থাকে, তাহলে:

```excel
=SUM(EmployeeTable[Salary])
```

এটাকে বলে **Structured Reference**।

এখানে:

```text
EmployeeTable → Table-এর নাম
Salary        → Column-এর নাম
```

---

# 5️⃣ কেন Structured Reference ব্যবহার করব?

ধরো আজ তোমার data:

```text
E2:E10
```

আগামীকাল নতুন employee যোগ হলো:

```text
E2:E11
```

Normal range নিয়ে কাজ করলে range update করার দরকার হতে পারে।

কিন্তু Table-এর structured reference:

```excel
=SUM(EmployeeTable[Salary])
```

ব্যবহার করলে নতুন table row automatically সেই column-এর অংশ হয়।

---

# 6️⃣ Table-এর একটি Column ব্যবহার

ধরো Table:

```text
EmployeeTable
```

এর column:

```text
ID
Name
Department
City
Salary
```

Salary column:

```excel
EmployeeTable[Salary]
```

Name:

```excel
EmployeeTable[Name]
```

Department:

```excel
EmployeeTable[Department]
```

---

# 7️⃣ SUM with Table

সব salary-এর total:

```excel
=SUM(EmployeeTable[Salary])
```

---

# 8️⃣ AVERAGE with Table

Average salary:

```excel
=AVERAGE(EmployeeTable[Salary])
```

---

# 9️⃣ COUNT with Table

Salary column-এ কতগুলো numeric value আছে:

```excel
=COUNT(EmployeeTable[Salary])
```

---

# 🔟 MAX / MIN

Highest salary:

```excel
=MAX(EmployeeTable[Salary])
```

Lowest salary:

```excel
=MIN(EmployeeTable[Salary])
```

---

# 1️⃣1️⃣ COUNTIF + Table ⭐

ধরো IT employee কতজন:

```excel
=COUNTIF(EmployeeTable[Department],"IT")
```

এটা অনেক cleaner:

```excel
=COUNTIF(C2:C100,"IT")
```

এর তুলনায়।

---

# 1️⃣2️⃣ SUMIF + Table

IT department-এর total salary:

```excel
=SUMIF(EmployeeTable[Department],"IT",EmployeeTable[Salary])
```

Logic:

```text
Department → কোথায় condition check করবে
"IT"       → condition
Salary     → কোন values যোগ করবে
```

---

# 1️⃣3️⃣ Multiple Conditions

IT department এবং Dhaka city:

```excel
=COUNTIFS(
EmployeeTable[Department],"IT",
EmployeeTable[City],"Dhaka"
)
```

অর্থাৎ:

```text
Department = IT
AND
City = Dhaka
```

---

# 1️⃣4️⃣ Calculated Column ⭐

এটা Table-এর খুব powerful feature।

ধরো Table-এ:

|Product|Price|Quantity|
|---|--:|--:|
|Laptop|50000|2|
|Mouse|1000|5|
|Keyboard|2000|3|

একটি নতুন column:

```text
Total
```

প্রথম row-তে:

```excel
=[@Price]*[@Quantity]
```

Result:

|Product|Price|Quantity|Total|
|---|--:|--:|--:|
|Laptop|50000|2|100000|
|Mouse|1000|5|5000|
|Keyboard|2000|3|6000|

Excel Table-এর বাকি rows-এ formula automatically apply করতে পারে।

---

# 1️⃣5️⃣ `@` চিহ্নের অর্থ

এই formula:

```excel
=[@Price]*[@Quantity]
```

এখানে:

```text
@Price
```

মানে **current row-এর Price**।

আর:

```text
@Quantity
```

মানে **current row-এর Quantity**।

সহজভাবে:

```text
[@Column]
      ↓
current row-এর সেই column
```

---

# 1️⃣6️⃣ Table Total Row

Table select করে:

**Table Design → Total Row**

enable করলে নিচে Total Row আসবে।

তারপর Salary column-এ নির্বাচন করতে পারো:

```text
Sum
Average
Count
Max
Min
```

ইত্যাদি।

---

# 1️⃣7️⃣ Table Automatically Expand

ধরো Table:

|ID|Name|Salary|
|--:|---|--:|
|101|Atiar|35000|
|102|Rahim|40000|

এর নিচে নতুন row লিখলে:

|ID|Name|Salary|
|--:|---|--:|
|101|Atiar|35000|
|102|Rahim|40000|
|103|Karim|45000|

Excel সাধারণত নতুন row-টাকেও Table-এর অংশ করে নেয়।

এটা normal range-এর তুলনায় বড় সুবিধা।

---

# 1️⃣8️⃣ Table vs Normal Range

|Feature|Normal Range|Excel Table|
|---|---|---|
|Filter|Manually|Automatic|
|New row|Manually manage|Automatically expands|
|Formula|Normal references|Structured references|
|Formatting|Manual|Table style|
|Total row|Manual|Built-in|
|Data management|Basic|Advanced|

---

# 1️⃣9️⃣ Table Style

Table Design থেকে বিভিন্ন style ব্যবহার করা যায়।

কিন্তু মনে রাখবে:

> **Professional data-এর জন্য fancy color-এর চেয়ে clean structure বেশি important।**

---

# 2️⃣0️⃣ Table Filter + Sort

Table তৈরি করলে header-এ dropdown automatically থাকবে।

যেমন:

```text
Department ▼
```

তারপর:

```text
IT
HR
Sales
```

থেকে নির্বাচন করতে পারবে।

Class 11-এর Filter এবং Sort এখানেও ব্যবহার করা যাবে।

---

# 2️⃣1️⃣ Table-এর একটি গুরুত্বপূর্ণ Rule

Table-এর মধ্যে:

❌ unnecessary blank rows  
❌ merged cells  
❌ multiple headers

avoid করবে।

কারণ Table মূলত **structured dataset**-এর জন্য।

---

# 🧠 Real-world Example

ধরো তোমার employee table:

```text
EmployeeTable
```

Columns:

```text
Employee_ID
Name
Department
City
Salary
```

তাহলে:

### Total Salary

```excel
=SUM(EmployeeTable[Salary])
```

### Average Salary

```excel
=AVERAGE(EmployeeTable[Salary])
```

### Highest Salary

```excel
=MAX(EmployeeTable[Salary])
```

### IT Employee Count

```excel
=COUNTIF(EmployeeTable[Department],"IT")
```

### IT Total Salary

```excel
=SUMIF(EmployeeTable[Department],"IT",EmployeeTable[Salary])
```

### IT + Dhaka Employee Count

```excel
=COUNTIFS(
EmployeeTable[Department],"IT",
EmployeeTable[City],"Dhaka"
)
```

এগুলোই ধীরে ধীরে **professional Excel analysis**-এর দিকে নিয়ে যাবে।

---

# ⚠️ Class 12 Beginner Mistakes

### Mistake 1: Table-এর নাম না দেওয়া

`Table1` কাজ করবে, কিন্তু:

```text
EmployeeTable
SalesTable
ProductTable
```

এরকম meaningful name ভালো।

---

### Mistake 2: Table-এর ভিতরে merged cells

❌ Avoid.

---

### Mistake 3: Formula ভুল column-এ দেওয়া

যেমন:

```excel
=[@Price]*[@Quantity]
```

এটা Total column-এ থাকা উচিত।

---

### Mistake 4: `@` বুঝতে না পারা

```excel
[@Salary]
```

মানে পুরো Salary column নয়।

এটা **current row-এর Salary**।

পুরো column:

```excel
EmployeeTable[Salary]
```

---

# 🎯 Class 12 Cheat Sheet

```text
Ctrl + T
     ↓
Create Table

Table Name:
EmployeeTable

Column:
EmployeeTable[Salary]

Current row:
[@Salary]

Total:
=SUM(EmployeeTable[Salary])

Average:
=AVERAGE(EmployeeTable[Salary])

Condition:
=COUNTIF(EmployeeTable[Department],"IT")

Multiple conditions:
=COUNTIFS(...)
```

---

# 📝 Class 12 Assignment

এই dataset Excel-এ তৈরি করো:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Atiar|IT|Dhaka|35000|
|102|Rahim|HR|Dhaka|40000|
|103|Karim|IT|Chittagong|45000|
|104|Nusrat|HR|Dhaka|50000|
|105|Hasan|IT|Dhaka|55000|
|106|Rafi|Sales|Khulna|30000|

### Tasks

1. `Ctrl + T` দিয়ে Table বানাও।
    
2. Table-এর নাম দাও:
    
    ```text
    EmployeeTable
    ```
    
3. Total Salary বের করো।
    
4. Average Salary বের করো।
    
5. Maximum Salary বের করো।
    
6. Minimum Salary বের করো।
    
7. IT employee count বের করো।
    
8. IT employees-এর total salary বের করো।
    
9. `IT + Dhaka` employee count বের করো।
    
10. নতুন employee add করে দেখো Table automatically expand হয় কি না।
    

---

# 🎯 Class 12 Quiz

**1. Excel Table তৈরি করার shortcut কী?**

A. Ctrl + T  
B. Ctrl + E  
C. Ctrl + R  
D. Ctrl + L

**2. `EmployeeTable[Salary]` কী?**

A. Cell reference  
B. Structured reference  
C. Text function  
D. Named cell

**3. `[@Salary]` কী বোঝায়?**

A. পুরো Salary column  
B. Current row-এর Salary  
C. প্রথম row-এর Salary  
D. Last row-এর Salary

**4. EmployeeTable-এর Salary total কোনটি?**

A. `=SUM(Salary)`  
B. `=SUM(EmployeeTable[Salary])`  
C. `=TOTAL(EmployeeTable[Salary])`  
D. `=ADD(EmployeeTable[Salary])`

**5. IT employee count:**

A. `=COUNT(EmployeeTable[Department],"IT")`  
B. `=COUNTIF(EmployeeTable[Department],"IT")`  
C. `=SUMIF(EmployeeTable[Department],"IT")`  
D. `=IF(EmployeeTable[Department],"IT")`

**6. Table-এর মধ্যে new row add করলে কী সুবিধা হতে পারে?**

A. Table automatically expand করতে পারে  
B. সব data delete হয়  
C. Formula বন্ধ হয়ে যায়  
D. Workbook বন্ধ হয়

**7. `=SUMIF(EmployeeTable[Department],"IT",EmployeeTable[Salary])` কী বের করবে?**

A. IT employee count  
B. IT employees-এর total salary  
C. সব employee salary  
D. IT average salary

**8. Table-এর Total Row কোথা থেকে enable করা যায়?**

A. Insert  
B. Table Design  
C. Review  
D. View

**9. Table-এর meaningful name কোনটি ভালো?**

A. Table1  
B. ABC  
C. EmployeeTable  
D. X

**10. Excel Table-এর প্রধান উদ্দেশ্য কী?**

A. শুধু color করা  
B. Structured data manage করা  
C. ছবি তৈরি করা  
D. শুধু printing করা


---
# 📘 Excel Mastery — Class 13

## PivotTable — Data Analysis-এর Power Tool ⭐⭐⭐

আজ থেকে আমরা **Data Analysis**-এর সবচেয়ে important Excel feature-গুলোর একটি শিখব: **PivotTable**।

একটা বড় dataset থেকে কয়েক সেকেন্ডে আমরা বের করতে পারব:

- কোন department-এ কত employee?
    
- কোন city-তে কত sales?
    
- কোন category সবচেয়ে বেশি বিক্রি হয়েছে?
    
- Department অনুযায়ী total salary কত?
    
- Average salary কত?
    
- Monthly sales কত?
    
- বিভিন্ন category compare করা
    

---

# 1️⃣ PivotTable কী?

সহজ ভাষায়:

> **PivotTable হলো বড় dataset-কে summarize এবং analyze করার একটি Excel tool।**

ধরো তোমার কাছে 10,000 sales records আছে:

|Date|Salesperson|City|Category|Amount|
|---|---|---|---|--:|
|Jan 1|Atiar|Dhaka|Laptop|50000|
|Jan 1|Rahim|Chittagong|Mouse|2000|
|Jan 2|Karim|Dhaka|Laptop|60000|
|Jan 2|Nusrat|Khulna|Keyboard|3000|
|...|...|...|...|...|

তুমি জানতে চাও:

> **প্রতিটি City-তে total sales কত?**

Formula দিয়ে অনেক কাজ করতে হতে পারে।

PivotTable দিয়ে কয়েকটি drag-and-drop করেই result পাওয়া যায়।

---

# 2️⃣ PivotTable-এর মূল ধারণা ⭐

PivotTable-এ সাধারণত 4টি গুরুত্বপূর্ণ area থাকে:

```text
Rows
Columns
Values
Filters
```

এগুলো বুঝতে পারলে PivotTable-এর foundation clear।

---

# 3️⃣ Rows

**Rows = কোন category অনুযায়ী data group করবে।**

ধরো:

```text
City
```

Rows-এ দিলে:

|City|
|---|
|Chittagong|
|Dhaka|
|Khulna|

অর্থাৎ city অনুযায়ী data group হবে।

---

# 4️⃣ Values

**Values = কী calculate করবে।**

ধরো:

```text
Amount
```

Values-এ দিলে Excel সাধারণত:

```text
Sum of Amount
```

করবে।

Result:

|City|Sum of Amount|
|---|--:|
|Chittagong|120000|
|Dhaka|350000|
|Khulna|80000|

---

# 5️⃣ Rows + Values ⭐

এটাই সবচেয়ে basic PivotTable।

Dataset:

|City|Amount|
|---|--:|
|Dhaka|50000|
|Dhaka|30000|
|Chittagong|20000|
|Dhaka|40000|
|Chittagong|10000|

PivotTable:

**Rows → City**

**Values → Amount**

Result:

|City|Sum of Amount|
|---|--:|
|Chittagong|30000|
|Dhaka|120000|

Excel automatically একই City-এর records group করে sum করেছে।

---

# 6️⃣ PivotTable তৈরি করার নিয়ম

প্রথমে dataset-এর ভিতরে click করো।

তারপর:

```text
Insert
   ↓
PivotTable
```

Excel তোমাকে table/range select করতে বলবে।

তারপর:

```text
New Worksheet
```

select করে:

**OK**

---

# 7️⃣ PivotTable Fields

ডান পাশে সাধারণত field list দেখা যাবে।

ধরো:

```text
☐ Date
☐ Salesperson
☐ City
☐ Category
☐ Amount
```

নিচে থাকবে:

```text
Filters
Columns
Rows
Values
```

এখন drag-and-drop করবে।

---

# 8️⃣ Example: City-wise Sales

তুমি:

```text
City → Rows
Amount → Values
```

দাও।

Result:

|City|Total Sales|
|---|--:|
|Chittagong|30,000|
|Dhaka|120,000|
|Khulna|80,000|

---

# 9️⃣ Department-wise Employee Count

Employee dataset:

|Name|Department|Salary|
|---|---|--:|
|Atiar|IT|35000|
|Rahim|HR|40000|
|Karim|IT|45000|
|Nusrat|HR|50000|
|Hasan|IT|55000|

তুমি চাও:

> প্রতিটি department-এ কত employee?

### Fields:

```text
Department → Rows
Name → Values
```

Excel সাধারণত:

```text
Count of Name
```

দেবে।

Result:

|Department|Employee Count|
|---|--:|
|HR|2|
|IT|3|

---

# 🔟 Sum বনাম Count

এটা খুব important।

যদি Values-এ:

```text
Salary
```

দাও → Excel সাধারণত **Sum** করবে।

যদি:

```text
Name
```

দাও → Excel সাধারণত **Count** করবে।

### Example

```text
Salary → Sum
Name → Count
```

---

# 1️⃣1️⃣ Average বের করা

ধরো:

```text
Department → Rows
Salary → Values
```

Excel default হিসেবে Sum দিতে পারে।

কিন্তু তুমি Average চাও।

### Steps:

Values-এর field-এর dropdown:

```text
Sum of Salary
        ↓
Value Field Settings
        ↓
Average
```

Result:

|Department|Average Salary|
|---|--:|
|HR|45000|
|IT|45000|

---

# 1️⃣2️⃣ Multiple Values ⭐

একই PivotTable-এ multiple calculations করা যায়।

ধরো:

```text
Department → Rows

Salary → Values
Salary → Values
```

তারপর:

প্রথম Salary:

```text
Sum
```

দ্বিতীয় Salary:

```text
Average
```

Result:

|Department|Sum Salary|Average Salary|
|---|--:|--:|
|HR|90000|45000|
|IT|135000|45000|

একই dataset থেকে multiple analysis!

---

# 1️⃣3️⃣ Columns

Columns ব্যবহার করলে comparison আরও সুন্দর হয়।

ধরো:

|City|Category|Amount|
|---|---|--:|
|Dhaka|Laptop|50000|
|Dhaka|Mouse|2000|
|Dhaka|Laptop|60000|
|Khulna|Laptop|30000|
|Khulna|Mouse|5000|

Fields:

```text
City → Rows
Category → Columns
Amount → Values
```

Result-এর structure হবে:

|City|Laptop|Mouse|
|---|--:|--:|
|Dhaka|110000|2000|
|Khulna|30000|5000|

এখন খুব সহজে compare করা যাচ্ছে।

---

# 1️⃣4️⃣ Filters

Filter area ব্যবহার করে পুরো PivotTable-কে একটি field দিয়ে filter করতে পারো।

যেমন:

```text
City → Rows
Amount → Values
Category → Filters
```

তারপর Category থেকে:

```text
Laptop
```

select করলে শুধু Laptop-এর sales দেখাবে।

---

# 1️⃣5️⃣ PivotTable Filter vs Normal Filter

|Normal Filter|PivotTable|
|---|---|
|Original records filter করে|Summary data analyze করে|
|Row hide করে|Aggregated result দেখায়|
|Raw dataset-এর জন্য|Analysis-এর জন্য|
|Sort/filter focused|Group + summarize focused|

---

# 1️⃣6️⃣ Grouping — Date

এটা খুব useful।

ধরো Date field:

```text
01-Jan-2026
05-Jan-2026
15-Jan-2026
02-Feb-2026
10-Feb-2026
```

PivotTable-এ Date দিলে অনেক individual date দেখা যেতে পারে।

Date-এর উপর right-click করে:

```text
Group
```

তারপর:

```text
Months
```

বা:

```text
Months + Quarters + Years
```

select করা যায়।

তখন monthly analysis করা সহজ হয়।

---

# 1️⃣7️⃣ Monthly Sales Analysis ⭐

Fields:

```text
Date → Rows
Amount → Values
```

তারপর Date:

```text
Right Click
→ Group
→ Months
```

Result:

|Month|Sales|
|---|--:|
|January|250000|
|February|310000|
|March|280000|

এটা Data Analyst-এর খুব common কাজ।

---

# 1️⃣8️⃣ PivotTable Refresh ⭐

ধরো original Table-এ নতুন data যোগ করলে PivotTable সবসময় immediately update নাও হতে পারে।

তখন:

**Right Click → Refresh**

অথবা:

**Data → Refresh All**

ব্যবহার করতে পারো।

### মনে রাখবে:

```text
New Data
   ↓
Refresh
   ↓
Updated PivotTable
```

---

# 1️⃣9️⃣ PivotTable-এর বড় সুবিধা

ধরো 100,000 rows আছে।

তুমি চাইলে খুব দ্রুত বের করতে পারো:

```text
Total Sales
Average Sales
Sales by City
Sales by Product
Sales by Employee
Monthly Sales
Department-wise Salary
Employee Count
```

একই dataset থেকে।

---

# 2️⃣0️⃣ PivotTable-এর Real-world Workflow ⭐

একজন Data Analyst সাধারণত:

```text
Raw Data
    ↓
Data Cleaning
    ↓
Excel Table
    ↓
PivotTable
    ↓
Analysis
    ↓
PivotChart
    ↓
Dashboard
```

আমরা এখন সেই workflow-এর মাঝখানে চলে এসেছি।

---

# 🧠 Class 13 Cheat Sheet

|Area|কাজ|
|---|---|
|Rows|Group/category|
|Columns|Side-by-side comparison|
|Values|Calculation|
|Filters|PivotTable filter|
|Sum|Total|
|Count|Number of records|
|Average|Mean|
|Group|Date/category grouping|
|Refresh|Updated data আনতে|
|PivotTable|Summary & analysis|

### সবচেয়ে গুরুত্বপূর্ণ:

```text
Rows    → What do I want to group by?
Values  → What do I want to calculate?
Columns → What do I want to compare?
Filters → What do I want to filter?
```

---

# 📝 Class 13 Practical Assignment

এই dataset ব্যবহার করো:

|Date|Employee|Department|City|Product|Sales|
|---|---|---|---|---|--:|
|01-Jan-26|Atiar|IT|Dhaka|Laptop|50000|
|05-Jan-26|Rahim|HR|Dhaka|Mouse|2000|
|10-Jan-26|Karim|IT|Chittagong|Laptop|60000|
|15-Jan-26|Nusrat|HR|Dhaka|Keyboard|3000|
|20-Jan-26|Hasan|IT|Dhaka|Laptop|55000|
|02-Feb-26|Rafi|Sales|Khulna|Mouse|5000|
|10-Feb-26|Atiar|IT|Dhaka|Keyboard|4000|
|15-Feb-26|Rahim|HR|Chittagong|Laptop|45000|
|20-Feb-26|Karim|IT|Dhaka|Mouse|2500|
|25-Feb-26|Hasan|IT|Dhaka|Laptop|70000|

### Tasks

**1.** City-wise total sales বের করো।

```text
City → Rows
Sales → Values
```

**2.** Department-wise sales বের করো।

**3.** Product-wise total sales বের করো।

**4.** Employee-wise sales বের করো।

**5.** Department-wise average sales বের করো।

**6.** City + Product অনুযায়ী sales analysis করো।

**7.** January বনাম February sales compare করো।

**8.** PivotTable refresh করার practice করো।

---

# 🎯 Class 13 Quiz

**1. PivotTable-এর মূল উদ্দেশ্য কী?**

A. Data entry  
B. Data summarize ও analyze করা  
C. ছবি edit করা  
D. Programming করা

**2. কোন area-তে category group করা হয়?**

A. Values  
B. Rows  
C. Filters  
D. Formula

**3. কোন area-তে calculation করা হয়?**

A. Values  
B. Rows  
C. Columns  
D. Header

**4. Department-wise employee count করতে:**

A. Department → Values, Name → Rows  
B. Department → Rows, Name → Values  
C. Name → Rows only  
D. Salary → Rows

**5. `Salary → Values` দিলে সাধারণত কী পাওয়া যায়?**

A. Sum  
B. Text  
C. Date  
D. Filter

**6. Average Salary পেতে কী করতে হবে?**

A. Value Field Settings → Average  
B. Data → Sort  
C. Insert → Chart  
D. Ctrl + E

**7. PivotTable-এর data update করার জন্য কী করতে হয়?**

A. Delete  
B. Refresh  
C. Merge  
D. Hide

**8. Date-কে Month অনুযায়ী analyze করতে কোন feature useful?**

A. Group  
B. Remove Duplicates  
C. Text to Columns  
D. Flash Fill

**9. PivotTable-এ Columns area-এর প্রধান উদ্দেশ্য কী?**

A. Data delete  
B. Side-by-side comparison/grouping  
C. Formula লেখা  
D. Cell formatting

**10. `Rows → City` এবং `Values → Sales` দিলে কী ধরনের analysis হবে?**

A. City-wise total sales  
B. Sales-wise city name  
C. Employee count  
D. Date analysis


----
# 📘 Excel Mastery — Class 14

## PivotChart & Data Visualization ⭐⭐⭐

Class 13-এ আমরা **PivotTable** দিয়ে data summarize করেছি।  
আজ সেই summarized data-কে **Chart/Graph** দিয়ে visually বুঝতে শিখব।

> **Goal:** Raw Data → PivotTable → PivotChart → সহজে insight বের করা

---

# 1️⃣ Chart কেন দরকার?

ধরো PivotTable-এ:

|City|Total Sales|
|---|--:|
|Dhaka|350000|
|Chittagong|220000|
|Khulna|120000|
|Rajshahi|80000|

Table দেখে comparison করা যায়।

কিন্তু Chart দেখলে এক নজরেই বোঝা যায়:

```text
Dhaka       ███████████████
Chittagong  █████████
Khulna      █████
Rajshahi    ███
```

এটাই **Data Visualization**।

---

# 2️⃣ PivotChart কী?

**PivotChart = PivotTable-এর summarized data-এর উপর তৈরি interactive chart।**

PivotTable-এ তুমি যদি:

```text
City → Rows
Sales → Values
```

দাও, তাহলে সেই PivotTable থেকে Chart তৈরি করা যায়।

---

# 3️⃣ PivotChart তৈরি করার নিয়ম

প্রথমে PivotTable-এর ভিতরে click করো।

তারপর:

```text
Insert
   ↓
PivotChart
```

তারপর Chart type নির্বাচন করো।

---

# 4️⃣ কোন Chart কখন ব্যবহার করব? ⭐

এটা খুব important।

|Chart|Best use|
|---|---|
|Column|Category comparison|
|Bar|অনেক category compare|
|Line|Time trend|
|Pie|Part/percentage|
|Area|Trend + magnitude|
|Scatter|দুই numeric variable-এর relationship|

---

# 5️⃣ Column Chart

ধরো:

|Department|Sales|
|---|--:|
|IT|150000|
|HR|100000|
|Sales|220000|

**Column Chart** ব্যবহার করলে:

```text
Sales
 ↑
 |       █
 | █     █
 | █  █  █
 +------------
   IT HR Sales
```

### Best for:

> "কোন category বেশি?"

---

# 6️⃣ Bar Chart

Bar Chart হলো horizontal comparison।

```text
IT      ███████████
HR      ███████
Sales   ███████████████
```

যখন category name বড় হয়, Bar Chart অনেক সময় বেশি readable।

Example:

```text
Chittagong Division
Dhaka Division
Rajshahi Division
```

Long names হলে horizontal bar useful।

---

# 7️⃣ Line Chart ⭐

Line Chart সবচেয়ে useful যখন **time-এর সাথে change** দেখতে চাও।

ধরো:

|Month|Sales|
|---|--:|
|Jan|100000|
|Feb|150000|
|Mar|130000|
|Apr|200000|
|May|250000|

Line Chart:

```text
Sales
250k |              ●
200k |          ●
150k |     ●
100k | ●
     +----------------
       Jan Feb Mar Apr May
```

এখানে trend বোঝা যায়।

### Question:

> Sales কি বাড়ছে নাকি কমছে?

Line Chart excellent।

---

# 8️⃣ Pie Chart

Pie Chart একটি total-এর মধ্যে বিভিন্ন অংশ দেখাতে useful।

ধরো:

|Product|Sales|
|---|--:|
|Laptop|500000|
|Mouse|100000|
|Keyboard|150000|
|Monitor|250000|

এখানে জানতে চাই:

> Total sales-এর কত অংশ কোন product থেকে এসেছে?

Pie Chart ব্যবহার করা যায়।

### ⚠️ কিন্তু

অনেক category থাকলে Pie Chart confusing হয়ে যায়।

যেমন 20–30 category হলে Pie Chart avoid করা ভালো।

---

# 9️⃣ Percentage বোঝার জন্য Pie

ধরো:

```text
Laptop    → 50%
Monitor   → 25%
Keyboard  → 15%
Mouse     → 10%
```

Pie Chart visually এই proportion দেখাবে।

---

# 🔟 PivotChart-এর সবচেয়ে বড় সুবিধা ⭐

PivotTable-এর filter change করলে Chart-ও update হয়।

ধরো:

```text
All Products
```

থেকে:

```text
Laptop
```

select করলে PivotChart-ও Laptop-এর data দেখাবে।

অর্থাৎ:

```text
PivotTable Filter
       ↓
PivotTable Update
       ↓
PivotChart Update
```

---

# 1️⃣1️⃣ PivotChart Fields

PivotChart-এর ক্ষেত্রেও field structure থাকে।

যেমন:

```text
Axis
Legend
Values
Filters
```

এগুলো PivotTable-এর:

```text
Rows
Columns
Values
Filters
```

এর সঙ্গে related।

---

# 1️⃣2️⃣ Axis কী?

Chart-এর category direction।

ধরো:

```text
Jan Feb Mar Apr
```

এগুলো **X-axis/category axis**-এ থাকতে পারে।

Sales amount:

```text
100k
200k
300k
```

এগুলো **Y-axis/value axis**।

সহজভাবে:

```text
X-axis → Category/Time
Y-axis → Numeric value
```

---

# 1️⃣3️⃣ Legend কী?

যখন Chart-এ একাধিক series থাকে, তখন কোন series কোনটা সেটা বোঝাতে **Legend** ব্যবহার হয়।

Example:

```text
Sales
 ├── Laptop
 ├── Mouse
 └── Keyboard
```

Legend দেখাবে:

```text
■ Laptop
■ Mouse
■ Keyboard
```

---

# 1️⃣4️⃣ Multiple Series Chart ⭐

ধরো:

|Month|Laptop|Mouse|
|---|--:|--:|
|Jan|100000|20000|
|Feb|120000|25000|
|Mar|150000|30000|

এখানে:

```text
X-axis → Month
Values → Laptop + Mouse
```

তাহলে দুই product-এর trend একই chart-এ compare করা যাবে।

---

# 1️⃣5️⃣ Chart Title

Chart-এর title meaningful হওয়া উচিত।

❌ Bad:

```text
Chart 1
```

✅ Better:

```text
Monthly Sales — 2026
```

আরও specific:

```text
Monthly Laptop Sales — 2026
```

---

# 1️⃣6️⃣ Data Labels

Chart-এর bar/column-এর উপর exact value দেখাতে:

**Chart → Data Labels**

enable করতে পারো।

Example:

```text
Dhaka
██████████ 350,000
```

এতে exact number দেখতে সুবিধা হয়।

---

# 1️⃣7️⃣ Avoid 3D Charts ⚠️

Beginner হিসেবে 3D chart দেখতে attractive লাগতে পারে।

কিন্তু Data Analysis-এ:

> **Simple 2D charts সাধারণত easier to read.**

তাই unnecessary 3D effects avoid করো।

---

# 1️⃣8️⃣ Chart Selection — খুব সহজ Rule ⭐

মনে রাখো:

```text
Comparison
   ↓
Column / Bar

Trend over Time
   ↓
Line

Part of Whole
   ↓
Pie

Relationship between 2 numbers
   ↓
Scatter
```

---

# 1️⃣9️⃣ Real-world Data Analyst Example

ধরো Sales dataset:

|Date|City|Product|Sales|
|---|---|---|--:|
|Jan|Dhaka|Laptop|50000|
|Jan|Dhaka|Mouse|5000|
|Jan|Khulna|Laptop|40000|
|Feb|Dhaka|Laptop|60000|
|Feb|Khulna|Mouse|7000|

প্রথমে PivotTable:

```text
Date → Rows
Sales → Values
```

তারপর:

```text
Insert → PivotChart → Line
```

Result:

**Monthly Sales Trend**

এখন manager এক নজরে বুঝতে পারবে sales কোন দিকে যাচ্ছে।

---

# 2️⃣0️⃣ Dashboard-এর দিকে আমরা এগোচ্ছি 🚀

আমাদের শেখার sequence এখন:

```text
Class 10
Data Cleaning
      ↓
Class 11
Sort & Filter
      ↓
Class 12
Excel Table
      ↓
Class 13
PivotTable
      ↓
Class 14
PivotChart
      ↓
Class 15+
Advanced Analysis
      ↓
Dashboard
```

অর্থাৎ আমরা ধীরে ধীরে **Data Analyst workflow** তৈরি করছি।

---

# 🧠 Class 14 Cheat Sheet

|Need|Chart|
|---|---|
|Category comparison|Column|
|Long category names|Bar|
|Time trend|Line|
|Percentage/part of whole|Pie|
|Relationship|Scatter|
|Exact values|Data Labels|
|Multiple categories/series|Legend|
|Horizontal axis|X-axis|
|Vertical numeric axis|Y-axis|

### Golden Rule ⭐

> **Chart সুন্দর হওয়া গুরুত্বপূর্ণ নয়; Chart দেখে information দ্রুত বোঝা যায় কি না—সেটাই গুরুত্বপূর্ণ।**

---

# 📝 Class 14 Assignment

Class 13-এর sales dataset ব্যবহার করো।

### Task 1 — City Sales Chart

PivotTable:

```text
City → Rows
Sales → Values
```

তারপর:

```text
PivotChart → Column
```

---

### Task 2 — Monthly Sales Trend

```text
Date → Rows
Sales → Values
```

Date-কে Month অনুযায়ী Group করো।

তারপর:

```text
PivotChart → Line
```

---

### Task 3 — Product Comparison

```text
Product → Rows
Sales → Values
```

তারপর:

```text
PivotChart → Bar
```

---

### Task 4 — Product Contribution

Product-wise sales দিয়ে:

```text
PivotChart → Pie
```

তৈরি করো।

---

### Task 5 — Professional Chart

তোমার একটি chart:

- Meaningful title দাও
    
- Data Labels add করো
    
- unnecessary 3D effect বাদ দাও
    
- readable size রাখো
    
- unnecessary colors/effects ব্যবহার করো না
    

---

# 🎯 Class 14 Quiz

**1. PivotChart মূলত কী?**

A. Data entry tool  
B. PivotTable-এর data-এর visualization  
C. Formula  
D. Database

**2. Monthly sales trend দেখাতে কোন Chart সবচেয়ে suitable?**

A. Pie  
B. Line  
C. Doughnut  
D. Bar

**3. Category comparison-এর জন্য কোনটি ভালো?**

A. Column  
B. Line  
C. Scatter  
D. Pie

**4. Part of whole দেখাতে কোন Chart ব্যবহার করা যায়?**

A. Line  
B. Pie  
C. Scatter  
D. Column

**5. X-axis-এ সাধারণত কী থাকতে পারে?**

A. Category/Time  
B. Formula  
C. Workbook  
D. Cell address

**6. Y-axis-এ সাধারণত কী থাকে?**

A. Numeric values  
B. Sheet name  
C. File name  
D. Formula name

**7. Multiple series identify করতে কোনটি ব্যবহার হয়?**

A. Legend  
B. Filter  
C. Header  
D. Name Box

**8. PivotTable-এর filter change করলে PivotChart-এর কী হতে পারে?**

A. Update হয়  
B. Delete হয়  
C. Workbook বন্ধ হয়  
D. Formula মুছে যায়

**9. Exact value chart-এর উপর দেখাতে কী ব্যবহার করা যায়?**

A. Data Labels  
B. Legend  
C. Axis  
D. Filter

**10. Data analysis-এর জন্য সাধারণত কোনটি বেশি readable?**

A. অতিরিক্ত 3D effect  
B. Simple 2D chart  
C. 20টি color  
D. অনেক decorative effect


----
# 📘 Excel Mastery — Class 15

## Advanced Formulas: IF + Lookup + Conditional Analysis ⭐⭐⭐

Class 14 পর্যন্ত আমরা **PivotTable + PivotChart** দিয়ে data summarize এবং visualize করেছি।

আজ থেকে আমরা আবার **Formula-based Analysis**-এ ঢুকব। আজকের class-এর মূল লক্ষ্য:

> **একাধিক Excel function একসাথে combine করে real-world problem solve করা।**

আজ শিখব:

1. IF + AND / OR
    
2. IF + XLOOKUP
    
3. IFERROR
    
4. SUMIFS + XLOOKUP
    
5. COUNTIFS + conditions
    
6. AVERAGEIFS
    
7. Formula nesting
    
8. Real-world employee analysis
    

---

# 1️⃣ Formula Nesting কী?

একটি function-এর ভিতরে আরেকটি function ব্যবহার করাকে **Nesting** বলে।

Simple:

```excel
=IF(B2>=40,"Pass","Fail")
```

Nested:

```excel
=IF(AND(B2>=40,C2>=40),"Pass","Fail")
```

এখানে:

```text
IF
 └── AND
```

একটি function অন্য function-এর ভিতরে আছে।

---

# 2️⃣ IF + AND ⭐

ধরো Student-এর:

|Name|Theory|Practical|
|---|--:|--:|
|Atiar|70|80|
|Rahim|35|70|
|Karim|80|30|

Rule:

> Theory এবং Practical—দুটিতেই ≥ 40 হলে Pass।

Formula:

```excel
=IF(AND(B2>=40,C2>=40),"Pass","Fail")
```

### Atiar:

```text
70 >= 40 → TRUE
80 >= 40 → TRUE

AND → TRUE

Result → Pass
```

### Karim:

```text
80 >= 40 → TRUE
30 >= 40 → FALSE

AND → FALSE

Result → Fail
```

---

# 3️⃣ IF + OR

Rule:

> Theory অথবা Practical-এর যেকোনো একটিতে ≥ 80 হলে Special Candidate।

```excel
=IF(OR(B2>=80,C2>=80),"Yes","No")
```

Karim:

```text
Theory = 80
Practical = 30

OR → TRUE

Result → Yes
```

---

# 4️⃣ IF + XLOOKUP ⭐⭐⭐

এটা খুব powerful combination।

ধরো Employee ID:

|ID|Name|
|--:|---|
|101|Atiar|
|102|Rahim|
|103|Karim|

তুমি একটি ID input দিলে:

```text
F2 = 102
```

Name বের করতে:

```excel
=XLOOKUP(F2,A2:A4,B2:B4)
```

Result:

```text
Rahim
```

এখন যদি ID না পাওয়া যায়?

```excel
=IFERROR(XLOOKUP(F2,A2:A4,B2:B4),"Not Found")
```

এটা professional approach।

---

# 5️⃣ IFERROR কী?

`IFERROR()` কোনো formula error করলে alternative result দেখাতে পারে।

Syntax:

```excel
=IFERROR(value,value_if_error)
```

Example:

```excel
=IFERROR(A2/B2,0)
```

যদি B2 = 0 হয় এবং division error হয়, তাহলে:

```text
0
```

দেখাবে।

আর lookup-এর ক্ষেত্রে:

```excel
=IFERROR(XLOOKUP(F2,A2:A10,B2:B10),"Not Found")
```

ID না থাকলে:

```text
Not Found
```

---

# 6️⃣ XLOOKUP + IF

ধরো:

|Product ID|Product|Price|
|---|---|--:|
|P101|Laptop|50000|
|P102|Mouse|1000|
|P103|Keyboard|2000|

F2:

```text
P102
```

Product বের করতে:

```excel
=XLOOKUP(F2,A2:A4,B2:B4)
```

Price বের করতে:

```excel
=XLOOKUP(F2,A2:A4,C2:C4)
```

Price-এর উপর condition:

> Price ≥ 5000 হলে "Expensive", না হলে "Affordable"

```excel
=IF(XLOOKUP(F2,A2:A4,C2:C4)>=5000,"Expensive","Affordable")
```

এখানে:

```text
IF
 └── XLOOKUP
```

---

# 7️⃣ SUMIFS + Cell Reference ⭐

Class 9-এ SUMIFS শিখেছিলে।

আজ এটাকে dynamic করি।

ধরো:

|Department|City|Salary|
|---|---|--:|
|IT|Dhaka|35000|
|IT|Chittagong|45000|
|HR|Dhaka|40000|
|IT|Dhaka|55000|

ধরো F2:

```text
IT
```

G2:

```text
Dhaka
```

IT + Dhaka-এর total salary:

```excel
=SUMIFS(C2:C5,A2:A5,F2,B2:B5,G2)
```

Result:

```text
90000
```

এখন F2/G2 পরিবর্তন করলে formula automatically অন্য combination-এর result দেবে।

এটাই **dynamic analysis**।

---

# 8️⃣ COUNTIFS + Cell Reference

একই dataset:

> IT + Dhaka-তে কয়জন employee?

```excel
=COUNTIFS(A2:A5,F2,B2:B5,G2)
```

Result:

```text
2
```

---

# 9️⃣ AVERAGEIFS

একাধিক condition অনুযায়ী average বের করতে:

```excel
=AVERAGEIFS(C2:C5,A2:A5,F2,B2:B5,G2)
```

এখানে:

```text
Average Salary
where Department = F2
AND City = G2
```

---

# 🔟 Dynamic Criteria ⭐

Hardcoded:

```excel
=SUMIFS(C2:C100,A2:A100,"IT",B2:B100,"Dhaka")
```

Dynamic:

```excel
=SUMIFS(C2:C100,A2:A100,F2,B2:B100,G2)
```

### কেন dynamic ভালো?

কারণ তুমি শুধু:

```text
F2 = IT
G2 = Dhaka
```

থেকে পরিবর্তন করে:

```text
F2 = HR
G2 = Chittagong
```

করলেই result পরিবর্তন হবে।

---

# 1️⃣1️⃣ Criteria Operator + Cell Reference

ধরো F2:

```text
40000
```

তুমি চাও:

> Salary ≥ 40000 কতজন?

Formula:

```excel
=COUNTIF(C2:C100,">="&F2)
```

এখানে:

```text
">=" & F2
```

মানে:

```text
>=40000
```

---

# 1️⃣2️⃣ SUMIFS + Numeric Condition

ধরো IT employees-এর মধ্যে salary ≥ 40000 হলে total salary:

```excel
=SUMIFS(
C2:C100,
A2:A100,"IT",
C2:C100,">=40000"
)
```

অর্থাৎ:

```text
Department = IT
AND
Salary >= 40000
```

---

# 1️⃣3️⃣ Nested IF — Grade Classification

ধরো Score:

|Student|Score|
|---|--:|
|Atiar|85|
|Rahim|72|
|Karim|55|
|Nusrat|35|

Rules:

```text
80+ → A+
70+ → A
60+ → B
50+ → C
40+ → D
<40 → F
```

Formula:

```excel
=IF(B2>=80,"A+",
 IF(B2>=70,"A",
 IF(B2>=60,"B",
 IF(B2>=50,"C",
 IF(B2>=40,"D","F")))))
```

এটা **Nested IF**।

---

# 1️⃣4️⃣ Nested IF-এর সমস্যা

অনেক condition হলে formula অনেক বড় হয়ে যায়।

যেমন:

```text
IF
 IF
  IF
   IF
    IF
```

এটা maintain করা কঠিন।

তাই modern Excel-এ `IFS()` ব্যবহার করা যায়।

```excel
=IFS(
B2>=80,"A+",
B2>=70,"A",
B2>=60,"B",
B2>=50,"C",
B2>=40,"D",
B2<40,"F"
)
```

এটা তুলনামূলকভাবে readable।

---

# 1️⃣5️⃣ IFS বনাম IF

|IF|IFS|
|---|---|
|One/few conditions|Multiple conditions|
|Nested করা যায়|Multiple conditions directly|
|Simple|Cleaner|
|Old/common|Modern Excel|

---

# 1️⃣6️⃣ Real-world Employee Analysis ⭐⭐⭐

ধরো:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Atiar|IT|Dhaka|35000|
|102|Rahim|HR|Dhaka|40000|
|103|Karim|IT|Chittagong|45000|
|104|Nusrat|HR|Dhaka|50000|
|105|Hasan|IT|Dhaka|55000|

### Task 1: Salary Status

Salary ≥ 40000 হলে High:

```excel
=IF(E2>=40000,"High","Normal")
```

---

### Task 2: IT + Dhaka employee count

```excel
=COUNTIFS(C2:C6,"IT",D2:D6,"Dhaka")
```

Result:

```text
2
```

---

### Task 3: IT + Dhaka total salary

```excel
=SUMIFS(E2:E6,C2:C6,"IT",D2:D6,"Dhaka")
```

Result:

```text
90000
```

---

### Task 4: IT average salary

```excel
=AVERAGEIF(C2:C6,"IT",E2:E6)
```

IT salaries:

```text
35000
45000
55000
```

Average:

```text
45000
```

---

# 1️⃣7️⃣ Formula Building Strategy ⭐

একসাথে বড় formula লেখার চেষ্টা করবে না।

ধরো তোমার দরকার:

> IT + Dhaka + Salary ≥ 40000-এর total salary।

প্রথমে ভাবো:

### Step 1

কোন function?

```text
SUMIFS
```

### Step 2

Sum range?

```text
Salary
```

### Step 3

Condition 1?

```text
Department = IT
```

### Step 4

Condition 2?

```text
City = Dhaka
```

### Step 5

Condition 3?

```text
Salary >= 40000
```

তারপর:

```excel
=SUMIFS(
E2:E100,
C2:C100,"IT",
D2:D100,"Dhaka",
E2:E100,">=40000"
)
```

এভাবেই complex formula build করবে।

---

# ⚠️ Class 15 Beginner Mistakes

### ❌ Mistake 1 — IF-এ text quotation ভুল

ভুল:

```excel
=IF(A2=IT,"Yes","No")
```

সঠিক:

```excel
=IF(A2="IT","Yes","No")
```

---

### ❌ Mistake 2 — AND বনাম OR confuse করা

```text
AND → সব condition TRUE
OR  → অন্তত একটি TRUE
```

---

### ❌ Mistake 3 — Criteria operator ভুল

ভুল:

```excel
=COUNTIF(A2:A10,>=40)
```

সঠিক:

```excel
=COUNTIF(A2:A10,">=40")
```

Cell reference হলে:

```excel
=COUNTIF(A2:A10,">="&F2)
```

---

### ❌ Mistake 4 — SUMIFS range mismatch

এগুলো একই size-এর হওয়া উচিত:

```text
Sum Range
Criteria Range 1
Criteria Range 2
```

যেমন:

```text
E2:E100
C2:C100
D2:D100
```

---

# 🧠 Class 15 Cheat Sheet

```text
IF
→ One condition

AND
→ All conditions TRUE

OR
→ At least one TRUE

IFS
→ Multiple conditions

XLOOKUP
→ Find corresponding value

IFERROR
→ Handle errors

SUMIFS
→ Conditional total

COUNTIFS
→ Conditional count

AVERAGEIFS
→ Conditional average
```

### Formula hierarchy:

```text
Basic Formula
     ↓
Function
     ↓
Multiple Functions
     ↓
Nested Formula
     ↓
Dynamic Analysis
```

---

# 📝 Class 15 Assignment

এই dataset ব্যবহার করো:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Atiar|IT|Dhaka|35000|
|102|Rahim|HR|Dhaka|40000|
|103|Karim|IT|Chittagong|45000|
|104|Nusrat|HR|Dhaka|50000|
|105|Hasan|IT|Dhaka|55000|
|106|Rafi|Sales|Khulna|30000|
|107|Sumaiya|IT|Dhaka|45000|
|108|Fahim|Sales|Dhaka|40000|

### Tasks

**1.** Salary ≥ 40000 হলে `"High"`, otherwise `"Normal"`।

**2.** `IT + Dhaka` employee count বের করো।

**3.** `IT + Dhaka` total salary বের করো।

**4.** `IT + Dhaka` average salary বের করো।

**5.** Salary ≥ 45000 employee count বের করো।

**6.** Salary ≥ 45000 এবং Department = IT employee count বের করো।

**7.** Nested IF দিয়ে Salary classification করো:

```text
50000+ → Excellent
40000+ → Good
30000+ → Average
Below 30000 → Low
```

**8.** F2 cell-এ Department লিখে dynamic `SUMIFS` তৈরি করো।

যেমন:

```text
F2 = IT
```

তারপর formula যেন IT-এর total salary দেয়।

F2 পরিবর্তন করে:

```text
HR
Sales
```

দিলে result পরিবর্তন হতে হবে।

---

# 🎯 Class 15 Quiz

**1. `AND()` কী করে?**

A. একটি condition check করে  
B. সব conditions TRUE কিনা check করে  
C. Data sort করে  
D. Lookup করে

**2. `OR()` কখন TRUE দেয়?**

A. সব condition TRUE হলে  
B. কোনো condition TRUE না হলে  
C. অন্তত একটি condition TRUE হলে  
D. কখনো না

**3. `IFERROR()` কেন ব্যবহার করা হয়?**

A. Error handle করতে  
B. Data sort করতে  
C. Chart বানাতে  
D. Duplicate remove করতে

**4. `XLOOKUP()` কী কাজে ব্যবহৃত হয়?**

A. Conditional sum  
B. Lookup  
C. Formatting  
D. Sorting

**5. `SUMIFS()` কী করে?**

A. Multiple conditions অনুযায়ী sum  
B. Multiple conditions অনুযায়ী count  
C. Average  
D. Lookup

**6. `COUNTIFS()` কী করে?**

A. Total  
B. Multiple conditions অনুযায়ী count  
C. Maximum  
D. Minimum

**7. `">="&F2` কেন ব্যবহার করা হয়?**

A. Text join করার জন্য  
B. Cell-এর value-এর সাথে comparison operator combine করতে  
C. Sort করার জন্য  
D. Lookup করার জন্য

**8. `IFS()` কেন useful?**

A. Multiple conditions handle করতে  
B. Data delete করতে  
C. Chart তৈরি করতে  
D. Table তৈরি করতে

**9. `[@Salary]` কী বোঝায়?**

A. Entire Salary column  
B. Current row-এর Salary  
C. First Salary  
D. Last Salary

**10. Complex formula বানানোর সবচেয়ে ভালো approach কোনটি?**

A. একবারে পুরো formula লিখে ফেলা  
B. ছোট ছোট অংশে formula build এবং test করা  
C. Random formula copy করা  
D. সবসময় nested IF ব্যবহার করা


----
# 📘 Excel Mastery — Class 15

## Advanced Formulas: IF + Lookup + Conditional Analysis

আজ আমরা Excel-এর **advanced formula building** শিখব। এই Class-এর লক্ষ্য হলো একাধিক function একসাথে ব্যবহার করে real-world problem solve করা।

---

# 1️⃣ Formula Nesting কী?

যখন একটি function-এর ভিতরে আরেকটি function ব্যবহার করি, তাকে **Nested Formula** বলা হয়।

### Simple IF

```excel
=IF(B2>=40,"Pass","Fail")
```

### IF + AND

```excel
=IF(AND(B2>=40,C2>=40),"Pass","Fail")
```

এখানে:

- `AND()` → দুই condition check করছে
    
- `IF()` → result দিচ্ছে
    

---

# 2️⃣ IF + AND

ধরি:

|Student|Math|English|
|---|--:|--:|
|Rahim|70|65|
|Karim|35|70|
|Hasan|80|30|

Pass করতে হলে **দুই subject-এই ≥ 40** হতে হবে।

```excel
=IF(AND(B2>=40,C2>=40),"Pass","Fail")
```

### Result

|Student|Result|
|---|---|
|Rahim|Pass|
|Karim|Fail|
|Hasan|Fail|

কারণ `AND()`-এর সব condition TRUE হতে হয়।

---

# 3️⃣ IF + OR

ধরি, কোনো student-এর **Math অথবা English যেকোনো একটিতে 80+** হলে তাকে Special বলা হবে।

```excel
=IF(OR(B2>=80,C2>=80),"Special","Normal")
```

### মনে রাখবে

**AND → সব condition TRUE**

**OR → অন্তত একটি TRUE**

---

# 4️⃣ XLOOKUP

এটি modern Excel-এর সবচেয়ে useful lookup functions-এর একটি।

ধরি:

|ID|Name|Salary|
|---|---|--:|
|101|Rahim|40000|
|102|Karim|50000|
|103|Hasan|60000|

F2-তে ID:

```text
102
```

Name বের করতে:

```excel
=XLOOKUP(F2,A2:A4,B2:B4)
```

Result:

```text
Karim
```

Salary বের করতে:

```excel
=XLOOKUP(F2,A2:A4,C2:C4)
```

Result:

```text
50000
```

---

# 5️⃣ XLOOKUP + IFERROR

যদি ID না পাওয়া যায় তাহলে Excel `#N/A` দেখাতে পারে।

আমরা সুন্দর message দিতে পারি:

```excel
=IFERROR(XLOOKUP(F2,A2:A4,B2:B4),"Not Found")
```

যদি F2 = `105`

Result:

```text
Not Found
```

### IFERROR-এর basic idea

```excel
=IFERROR(formula, alternative_result)
```

অর্থাৎ:

> Formula error হলে alternative result দেখাও।

---

# 6️⃣ IF + XLOOKUP

এখন দুইটা function combine করি।

ধরি:

|ID|Name|Salary|
|---|---|--:|
|101|Rahim|40000|
|102|Karim|50000|
|103|Hasan|60000|

F2:

```text
102
```

আমরা check করতে চাই salary ≥ 50000 হলে `"Expensive"` otherwise `"Affordable"`।

```excel
=IF(XLOOKUP(F2,A2:A4,C2:C4)>=50000,"Expensive","Affordable")
```

Result:

```text
Expensive
```

এটা real-world reporting-এ অনেক useful।

---

# 7️⃣ SUMIFS — Multiple Conditions

ধরি:

|Department|City|Salary|
|---|---|--:|
|IT|Dhaka|50000|
|HR|Dhaka|40000|
|IT|Chittagong|45000|
|IT|Dhaka|60000|

আমরা চাই:

> Dhaka-এর IT employees-এর total salary।

```excel
=SUMIFS(C2:C5,A2:A5,"IT",B2:B5,"Dhaka")
```

Result:

```text
110000
```

কারণ:

```text
50000 + 60000 = 110000
```

---

# 8️⃣ Dynamic SUMIFS

Hardcode না করে cell reference ব্যবহার করা better।

ধরি:

```text
F2 = IT
G2 = Dhaka
```

Formula:

```excel
=SUMIFS(C2:C100,A2:A100,F2,B2:B100,G2)
```

এখন F2/G2 change করলে result automatically change হবে।

যেমন:

```text
F2 = HR
G2 = Dhaka
```

তাহলে HR + Dhaka-এর salary আসবে।

এটাই **dynamic analysis**।

---

# 9️⃣ COUNTIFS

একাধিক condition অনুযায়ী কতগুলো record আছে সেটা বের করতে:

```excel
=COUNTIFS(A2:A100,F2,B2:B100,G2)
```

যদি:

```text
F2 = IT
G2 = Dhaka
```

তাহলে:

> IT department-এর Dhaka employees কতজন?

সেটা return করবে।

---

# 🔟 AVERAGEIFS

একাধিক condition অনুযায়ী average বের করতে:

```excel
=AVERAGEIFS(C2:C100,A2:A100,F2,B2:B100,G2)
```

অর্থাৎ:

> নির্দিষ্ট Department + City-এর average salary।

---

# 1️⃣1️⃣ Criteria-এর সাথে Cell Reference

এটা খুব important।

ধরি F2-তে:

```text
40000
```

আমরা চাই salary ≥ 40000 কতজন।

❌ ভুল:

```excel
=COUNTIF(C2:C100,>=F2)
```

✅ সঠিক:

```excel
=COUNTIF(C2:C100,">="&F2)
```

এখানে:

```text
">=" & F2
```

দিয়ে criteria তৈরি করা হয়েছে।

---

# 1️⃣2️⃣ SUMIFS + Multiple Conditions

ধরি আমরা চাই:

> IT department এবং salary ≥ 40000 — মোট salary কত?

```excel
=SUMIFS(C2:C100,A2:A100,"IT",C2:C100,">=40000")
```

আর যদি threshold F2-তে থাকে:

```excel
=SUMIFS(C2:C100,A2:A100,"IT",C2:C100,">="&F2)
```

এটা আরও flexible।

---

# 1️⃣3️⃣ Nested IF — Grade System

ধরি:

|Mark|Grade|
|--:|---|
|80+|A+|
|70+|A|
|60+|B|
|50+|C|
|40+|D|
|<40|F|

Formula:

```excel
=IF(B2>=80,"A+",
IF(B2>=70,"A",
IF(B2>=60,"B",
IF(B2>=50,"C",
IF(B2>=40,"D","F")))))
```

এখানে একাধিক IF একসাথে nested হয়েছে।

---

# 1️⃣4️⃣ IFS — Nested IF-এর সহজ Version

একই grade system IFS দিয়ে:

```excel
=IFS(
B2>=80,"A+",
B2>=70,"A",
B2>=60,"B",
B2>=50,"C",
B2>=40,"D",
B2<40,"F"
)
```

অনেক condition থাকলে `IFS()` পড়তে সহজ।

---

# 🧠 Formula Building Strategy

Advanced formula দেখে ভয় পাবে না।

এইভাবে চিন্তা করবে:

### Step 1 — কী result চাই?

Example:

> Dhaka IT employees-এর total salary

### Step 2 — কোন function?

Total → `SUMIFS`

### Step 3 — কোন range?

Salary:

```text
C2:C100
```

Department:

```text
A2:A100
```

City:

```text
B2:B100
```

### Step 4 — Conditions

```text
IT
Dhaka
```

### Step 5 — Formula

```excel
=SUMIFS(C2:C100,A2:A100,"IT",B2:B100,"Dhaka")
```

এই approach follow করলে complex formula অনেক সহজ হয়ে যাবে।

---

# ⚠️ Class 15-এর Beginner Mistakes

### ❌ Mistake 1 — AND এবং OR গুলিয়ে ফেলা

```excel
AND
```

মানে সব condition দরকার।

```excel
OR
```

মানে যেকোনো একটি হলেই হবে।

---

### ❌ Mistake 2 — Criteria quotation ভুল

❌

```excel
=COUNTIF(C2:C10,>=40)
```

✅

```excel
=COUNTIF(C2:C10,">=40")
```

Cell reference হলে:

```excel
=COUNTIF(C2:C10,">="&F2)
```

---

### ❌ Mistake 3 — SUMIF/SUMIFS range mismatch

সব range-এর row count compatible হতে হবে।

যেমন:

```text
A2:A100
B2:B100
C2:C100
```

ভালো।

---

### ❌ Mistake 4 — XLOOKUP-এ ভুল range

```excel
=XLOOKUP(F2,A2:A100,C2:C100)
```

এখানে lookup range এবং return range logically matching হতে হবে।

---

# 📌 Class 15 Cheat Sheet

|Function|কাজ|
|---|---|
|`IF`|condition|
|`AND`|সব condition TRUE|
|`OR`|যেকোনো একটি TRUE|
|`IFERROR`|error handle|
|`XLOOKUP`|lookup|
|`SUMIFS`|multiple condition total|
|`COUNTIFS`|multiple condition count|
|`AVERAGEIFS`|multiple condition average|
|`IFS`|multiple conditions|
|`&`|text/criteria combine|

---

# 📝 Class 15 Assignment

এই dataset বানাও:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Rahim|IT|Dhaka|50000|
|102|Karim|HR|Dhaka|40000|
|103|Hasan|IT|Chittagong|45000|
|104|Sakib|IT|Dhaka|60000|
|105|Nila|HR|Chittagong|55000|
|106|Rafi|IT|Dhaka|70000|

তারপর:

### Task 1

IT employees-এর total salary বের করো।

### Task 2

Dhaka-এর IT employees-এর total salary বের করো।

### Task 3

Dhaka-এর IT employees কতজন?

### Task 4

Dhaka-এর IT employees-এর average salary।

### Task 5

F2-তে Department লিখে dynamic total salary বের করো।

### Task 6

Salary ≥ 50000 হলে `"High"` otherwise `"Normal"`।

### Task 7

ID দিয়ে Name বের করতে XLOOKUP ব্যবহার করো।

### Task 8

ভুল ID দিলে `"Not Found"` দেখাও।

---

# 🧪 Class 15 Quiz

**1. `AND()` কী করে?**

A. One condition  
B. All conditions must be TRUE  
C. Search করে  
D. Sum করে

**2. `OR()` কখন TRUE হয়?**

A. সব FALSE হলে  
B. অন্তত একটি TRUE হলে  
C. সব TRUE না হলে  
D. কখনো না

**3. XLOOKUP-এর মূল কাজ কী?**

A. Formatting  
B. Lookup  
C. Sorting  
D. Chart

**4. Error handle করতে কোন function ব্যবহার করা যায়?**

A. SUM  
B. IFERROR  
C. COUNT  
D. MAX

**5. Multiple conditions দিয়ে total বের করতে?**

A. SUM  
B. SUMIF  
C. SUMIFS  
D. COUNTIFS

**6. Multiple conditions দিয়ে count করতে?**

A. COUNTIFS  
B. SUMIFS  
C. AVERAGE  
D. XLOOKUP

**7. `">="&F2` কেন ব্যবহার করি?**

A. Formatting  
B. Cell reference দিয়ে criteria তৈরি করতে  
C. Sorting  
D. Lookup

**8. Nested IF কী?**

A. IF-এর ভিতরে IF  
B. IF-এর আগে SUM  
C. IF delete করা  
D. IF format করা

**9. `IFS()` কী কাজে useful?**

A. Multiple conditions  
B. Chart  
C. Database connection  
D. File save

**10. Dhaka + IT employees-এর total salary-এর জন্য কোনটি সবচেয়ে appropriate?**

A. COUNT  
B. SUMIFS  
C. XLOOKUP  
D. MAX

**তুমি চাইলে এখন শুধু 1–10-এর answer দাও**, আমি check করে ভুলগুলো explain করব। এরপর **Class 16: Dynamic Arrays — FILTER, SORT, UNIQUE, SORTBY, SEQUENCE** শুরু করব।



----
# 📘 Excel Mastery — Class 16

## 🚀 Dynamic Arrays — FILTER, SORT, UNIQUE, SORTBY, SEQUENCE

আজকের Class খুব important, কারণ **Dynamic Array** জানলে Excel-এ এক formula দিয়ে অনেকগুলো result automatically বের করা যায়।

> **Note:** এগুলো মূলত **Microsoft 365 / Excel 2021+**-এর modern Excel functions। পুরোনো Excel version হলে কিছু function নাও থাকতে পারে।

---

# 1️⃣ Dynamic Array কী?

সাধারণ formula সাধারণত একটি cell-এ একটি result দেয়।

যেমন:

```excel
=SUM(A2:A10)
```

Result → একটি cell।

কিন্তু Dynamic Array formula **একটি formula থেকে একাধিক cell-এ result ছড়িয়ে দিতে পারে।**

এটাকে বলে:

### 👉 Spill

উদাহরণ:

```excel
=UNIQUE(A2:A10)
```

যদি A column-এ থাকে:

```text
Dhaka
Dhaka
Chittagong
Dhaka
Rajshahi
Chittagong
```

তাহলে formula নিজে থেকেই নিচে result ছড়িয়ে দেবে:

```text
Dhaka
Chittagong
Rajshahi
```

তোমাকে আলাদা আলাদা formula লিখতে হবে না।

---

# 2️⃣ FILTER Function

`FILTER()` ব্যবহার করে condition অনুযায়ী data বের করা যায়।

ধরি:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Rahim|IT|Dhaka|50000|
|102|Karim|HR|Dhaka|40000|
|103|Hasan|IT|Chittagong|45000|
|104|Sakib|IT|Dhaka|60000|
|105|Nila|HR|Chittagong|55000|

আমরা শুধু **IT employees** চাই।

```excel
=FILTER(A2:E6,C2:C6="IT")
```

Result automatically:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Rahim|IT|Dhaka|50000|
|103|Hasan|IT|Chittagong|45000|
|104|Sakib|IT|Dhaka|60000|

### Formula structure

```excel
=FILTER(array,include)
```

এখানে:

- `array` → কোন data return করবে
    
- `include` → কোন condition-এর record চাই
    

---

# 3️⃣ FILTER + Custom Message

যদি কোনো matching data না থাকে?

```excel
=FILTER(A2:E6,C2:C6="Marketing","No Data Found")
```

তাহলে Marketing না থাকলে:

```text
No Data Found
```

দেখাবে।

---

# 4️⃣ Multiple Conditions দিয়ে FILTER

এটা খুব important।

আমরা চাই:

> **IT + Dhaka employees**

```excel
=FILTER(A2:E6,(C2:C6="IT")*(D2:D6="Dhaka"))
```

এখানে:

```text
*
```

মানে এখানে **AND** হিসেবে কাজ করছে।

অর্থাৎ:

```text
Department = IT
AND
City = Dhaka
```

---

# 5️⃣ FILTER-এ OR Condition

এখন চাই:

> IT **OR** HR employees

```excel
=FILTER(A2:E6,(C2:C6="IT")+(C2:C6="HR"))
```

এখানে:

```text
+
```

মানে **OR** logic হিসেবে কাজ করছে।

### মনে রাখো:

```text
* → AND
+ → OR
```

Dynamic Array-এর ক্ষেত্রে এটা খুব useful trick।

---

# 6️⃣ SORT Function

`SORT()` দিয়ে data automatically sort করা যায়।

ধরি:

```excel
=SORT(A2:E6,5,1)
```

এখানে:

```text
A2:E6 → data
5      → 5th column দিয়ে sort
1      → ascending
```

অর্থাৎ Salary অনুযায়ী ছোট থেকে বড়।

### Descending:

```excel
=SORT(A2:E6,5,-1)
```

এখানে:

```text
1  → Ascending
-1 → Descending
```

---

# 7️⃣ SORT by Name

Name হলো 2nd column।

```excel
=SORT(A2:E6,2,1)
```

Result:

```text
Hasan
Karim
Nila
Rahim
Sakib
```

---

# 8️⃣ SORTBY Function

`SORT()` এবং `SORTBY()` দেখতে similar হলেও concept একটু আলাদা।

### SORT

```excel
=SORT(A2:E6,5,-1)
```

অর্থাৎ:

> Array-এর 5th column দিয়ে sort করো।

### SORTBY

```excel
=SORTBY(A2:E6,E2:E6,-1)
```

অর্থাৎ:

> A2:E6 data-কে E2:E6 salary অনুযায়ী descending sort করো।

`SORTBY()` অনেক সময় বেশি readable এবং flexible।

---

# 9️⃣ UNIQUE Function

Duplicate বাদ দিয়ে unique values বের করতে:

```excel
=UNIQUE(C2:C6)
```

যদি Department হয়:

```text
IT
HR
IT
IT
HR
```

Result:

```text
IT
HR
```

---

# 🔟 UNIQUE + SORT

Unique department alphabetically sort করতে:

```excel
=SORT(UNIQUE(C2:C100))
```

Result:

```text
Finance
HR
IT
Marketing
```

এখানে দুই function combine হয়েছে:

```text
UNIQUE → duplicate remove
SORT   → sort
```

---

# 1️⃣1️⃣ FILTER + SORT

এখন advanced combination।

আমরা চাই:

> IT employees বের করো এবং salary অনুযায়ী highest থেকে lowest সাজাও।

```excel
=SORT(FILTER(A2:E6,C2:C6="IT"),5,-1)
```

Execution concept:

```text
FILTER
   ↓
শুধু IT employees
   ↓
SORT
   ↓
Salary descending
```

এটাই formula nesting-এর practical ব্যবহার।

---

# 1️⃣2️⃣ FILTER + SORT + UNIQUE

ধরি City column থেকে শুধু IT employees-এর unique city চাই।

```excel
=UNIQUE(FILTER(D2:D100,C2:C100="IT"))
```

আর sorted চাইলে:

```excel
=SORT(UNIQUE(FILTER(D2:D100,C2:C100="IT")))
```

এখানে:

```text
FILTER → IT employees
UNIQUE → duplicate city বাদ
SORT → alphabetically সাজানো
```

🔥 এই ধরনের formula Data Analyst কাজেও অনেক useful।

---

# 1️⃣3️⃣ SEQUENCE Function

`SEQUENCE()` দিয়ে automatic sequence তৈরি করা যায়।

```excel
=SEQUENCE(10)
```

Result:

```text
1
2
3
4
5
6
7
8
9
10
```

---

## 10 Rows + 1 Column

```excel
=SEQUENCE(10,1)
```

মানে:

```text
10 rows
1 column
```

---

## 5 Rows + 3 Columns

```excel
=SEQUENCE(5,3)
```

Result:

|1|2|3|
|---|---|---|
|4|5|6|
|7|8|9|
|10|11|12|
|13|14|15|

---

# 1️⃣4️⃣ SEQUENCE Starting Value

ধরি 100 থেকে শুরু করতে চাই:

```excel
=SEQUENCE(10,1,100,1)
```

Result:

```text
100
101
102
103
104
105
106
107
108
109
```

Syntax:

```excel
=SEQUENCE(rows,columns,start,step)
```

---

# 1️⃣5️⃣ Reverse / Decreasing Sequence

100 থেকে শুরু করে 10 করে কমাতে:

```excel
=SEQUENCE(10,1,100,-10)
```

Result:

```text
100
90
80
70
60
50
40
30
20
10
```

---

# 1️⃣6️⃣ TRANSPOSE

Rows ↔ Columns পরিবর্তন করতে `TRANSPOSE()` ব্যবহার করা যায়।

ধরি:

```text
A1 = Dhaka
B1 = Chittagong
C1 = Rajshahi
```

Formula:

```excel
=TRANSPOSE(A1:C1)
```

Result:

```text
Dhaka
Chittagong
Rajshahi
```

অর্থাৎ horizontal data → vertical data।

আবার vertical → horizontal-ও করা যায়।

---

# 1️⃣7️⃣ Spill কী?

এটাই Dynamic Array-এর সবচেয়ে important concept।

ধরি B2-তে লিখলে:

```excel
=UNIQUE(A2:A10)
```

Excel B2 থেকে নিচের cells-গুলোতে automatically result বসাবে।

এগুলোকে বলা হয়:

### Spill Range

---

# 1️⃣8️⃣ `#SPILL!` Error

ধরি B2-তে:

```excel
=UNIQUE(A2:A10)
```

কিন্তু B3/B4/B5-এর মধ্যে আগে থেকেই data আছে।

Excel তখন বলতে পারে:

```text
#SPILL!
```

কারণ formula-এর result ছড়ানোর জায়গা নেই।

### Solution

Spill area-এর existing data remove করো।

---

# 1️⃣9️⃣ Spill Operator `#`

ধরি B2:

```excel
=UNIQUE(A2:A10)
```

এবং result B2:B5 পর্যন্ত spill করেছে।

তখন পুরো spilled range reference করতে পারো:

```excel
=B2#
```

অর্থাৎ:

> B2 থেকে যে পুরো dynamic result spill হয়েছে, সেটাকে reference করো।

এটা পরবর্তী advanced Excel work-এ খুব useful।

---

# 2️⃣0️⃣ Dynamic Dropdown-এর Foundation

ধরি Department column:

```text
IT
HR
IT
Finance
HR
Marketing
```

Unique department list:

```excel
=SORT(UNIQUE(C2:C100))
```

এতে automatically unique sorted list তৈরি হবে।

এই list পরবর্তীতে **Data Validation dropdown**-এর source হিসেবে ব্যবহার করা যায়।

👉 Data Validation আমরা পরের classes-এ বিস্তারিত করব।

---

# 🧠 Real-World Example

ধরি তোমার কাছে 10,000 employee records আছে।

Manager বললো:

> "শুধু Dhaka-এর IT employees দেখাও এবং highest salary থেকে lowest salary সাজাও।"

তুমি এক formula-তেই করতে পারো:

```excel
=SORT(
    FILTER(A2:E10001,
    (C2:C10001="IT")*(D2:D10001="Dhaka")),
    5,-1
)
```

Result automatically তৈরি হবে।

এটাই Dynamic Array-এর power। 🚀

---

# 📌 Class 16 Cheat Sheet

|Function|কাজ|
|---|---|
|`FILTER()`|Condition অনুযায়ী data বের করা|
|`SORT()`|Data sort করা|
|`SORTBY()`|অন্য range অনুযায়ী sort|
|`UNIQUE()`|Duplicate বাদ দেওয়া|
|`SEQUENCE()`|Automatic number sequence|
|`TRANSPOSE()`|Row ↔ Column|
|`#`|পুরো spilled range reference|
|`*`|FILTER-এ AND|
|`+`|FILTER-এ OR|

### সবচেয়ে গুরুত্বপূর্ণ combinations

```excel
=UNIQUE(A2:A100)
```

```excel
=SORT(A2:E100,5,-1)
```

```excel
=FILTER(A2:E100,C2:C100="IT")
```

```excel
=SORT(FILTER(A2:E100,C2:C100="IT"),5,-1)
```

```excel
=SORT(UNIQUE(C2:C100))
```

```excel
=UNIQUE(FILTER(D2:D100,C2:C100="IT"))
```

---

# ⚠️ Class 16 Beginner Mistakes

### 1. Spill area blocked

```text
#SPILL!
```

→ নিচের/পাশের cells-এর data check করো।

### 2. `*` এবং `+` ভুল করা

```text
* → AND
+ → OR
```

### 3. SORT-এর direction ভুল

```text
1  → Ascending
-1 → Descending
```

### 4. FILTER condition-এর range mismatch

❌

```excel
=FILTER(A2:E100,C2:C50="IT")
```

✅

```excel
=FILTER(A2:E100,C2:C100="IT")
```

### 5. পুরোনো Excel version

`FILTER`, `SORT`, `UNIQUE`, `SEQUENCE` সব version-এ available নয়।

---

# 📝 Class 16 Assignment

এই dataset ব্যবহার করো:

|ID|Name|Department|City|Salary|
|--:|---|---|---|--:|
|101|Rahim|IT|Dhaka|50000|
|102|Karim|HR|Dhaka|40000|
|103|Hasan|IT|Chittagong|45000|
|104|Sakib|IT|Dhaka|60000|
|105|Nila|HR|Chittagong|55000|
|106|Rafi|IT|Dhaka|70000|
|107|Tania|Finance|Dhaka|65000|
|108|Fahim|IT|Rajshahi|48000|

### Task 1

শুধু IT employees বের করো।

### Task 2

শুধু Dhaka-এর employees বের করো।

### Task 3

IT + Dhaka employees বের করো।

### Task 4

IT employees salary অনুযায়ী descending order-এ দেখাও।

### Task 5

Unique Department list বের করো।

### Task 6

Unique City list বের করে alphabetically sort করো।

### Task 7

IT employees-এর unique City বের করো।

### Task 8

1–20 পর্যন্ত number automatically generate করো।

### Task 9

100 থেকে 10 করে কমতে থাকা 10টি number generate করো।

### Task 10 ⭐

**IT + Dhaka employees → salary highest থেকে lowest** এক formula-তে বের করো।

---

# 🧪 Class 16 Quiz

**1. Dynamic Array-এর প্রধান বৈশিষ্ট্য কী?**

A. শুধু একটি cell-এ result  
B. Multiple cells-এ automatically result spill করতে পারে  
C. শুধু formatting করে  
D. শুধু chart তৈরি করে

**2. Duplicate values remove করতে কোন function?**

A. SORT  
B. FILTER  
C. UNIQUE  
D. SEQUENCE

**3. Condition অনুযায়ী records বের করতে?**

A. FILTER  
B. SORT  
C. TRANSPOSE  
D. SEQUENCE

**4. Ascending sort-এর জন্য SORT-এর third argument কী?**

A. -1  
B. 0  
C. 1  
D. 2

**5. FILTER-এ `*` সাধারণত কী বোঝায়?**

A. OR  
B. AND  
C. NOT  
D. SORT

**6. FILTER-এ `+` সাধারণত কী বোঝায়?**

A. AND  
B. OR  
C. NOT  
D. UNIQUE

**7. `=SEQUENCE(5)` কী তৈরি করবে?**

A. 5 columns  
B. 5 rows-এর sequence  
C. 5 charts  
D. 5 filters

**8. `#SPILL!` সাধারণত কেন হয়?**

A. Formula missing  
B. Spill করার জায়গা blocked  
C. Workbook closed  
D. Sheet renamed

**9. `SORTBY()` কী কাজে ব্যবহৃত হয়?**

A. Data delete  
B. অন্য range/array অনুযায়ী sort  
C. Duplicate remove  
D. Error handling

**10. IT employees-কে salary descending order-এ বের করতে কোনটি সঠিক?**

A.

```excel
=SORT(FILTER(A2:E100,C2:C100="IT"),5,-1)
```

B.

```excel
=UNIQUE(A2:E100)
```

C.

```excel
=SEQUENCE(A2:E100)
```

D.

```excel
=TRANSPOSE(A2:E100)
```

**Class 16-এর Quiz-এর 1–10 answer দাও।** তারপর আমরা **Class 17 — Data Validation + Smart Dropdown + Input Control** শিখব।


-----
# 📘 Excel Mastery — Class 17

## ✅ Data Validation + Smart Dropdown + Input Control

আজকের Class-এ আমরা Excel sheet-কে **user-friendly এবং error-resistant** করব।

ধরো তুমি একটি Employee Management Sheet বানাচ্ছো। User যেন Department-এর জায়গায় ভুল করে `IT`, `It`, `it`, `Information Technology` না লিখে শুধু নির্দিষ্ট option select করতে পারে—এটাই **Data Validation**-এর কাজ।

---

# 1️⃣ Data Validation কী?

**Data Validation** হলো Excel-এর এমন একটি feature, যেটা নির্ধারণ করে:

> একটি cell-এ user কী ধরনের data দিতে পারবে।

উদাহরণ:

```text
Department
────────────
IT
HR
Finance
Marketing
```

User যেন অন্য কিছু লিখতে না পারে।

### কোথায় পাব?

**Data → Data Validation**

---

# 2️⃣ কেন Data Validation দরকার?

ধরো Department column-এ 1000 employee আছে।

কেউ লিখল:

```text
IT
It
it
I.T.
Information Technology
```

Computer এগুলোকে আলাদা value হিসেবে দেখতে পারে।

এর ফলে:

```excel
=COUNTIF(C2:C1000,"IT")
```

সঠিক result নাও দিতে পারে।

তাই data entry-এর সময় থেকেই control করা ভালো।

---

# 3️⃣ Data Validation-এর প্রধান Types

Data Validation-এ বিভিন্ন ধরনের rule দেওয়া যায়:

|Type|ব্যবহার|
|---|---|
|Whole Number|পূর্ণ সংখ্যা|
|Decimal|দশমিক সংখ্যা|
|List|Dropdown|
|Date|নির্দিষ্ট date|
|Time|নির্দিষ্ট time|
|Text Length|text-এর length|
|Custom|নিজের formula দিয়ে rule|

আজ আমরা এগুলো practical example দিয়ে শিখব।

---

# 4️⃣ Whole Number Validation

ধরি Age column।

আমরা চাই:

> Age অবশ্যই 18 থেকে 60-এর মধ্যে হতে হবে।

### Steps

1. Age cells select করো
    
2. **Data → Data Validation**
    
3. Allow → **Whole Number**
    
4. Data → **between**
    
5. Minimum → `18`
    
6. Maximum → `60`
    

এখন:

```text
25 ✅
40 ✅
60 ✅
17 ❌
65 ❌
```

---

# 5️⃣ Decimal Validation

ধরি Product Rating:

```text
0 → 5
```

আমরা চাই rating শুধু 0 থেকে 5-এর মধ্যে হবে।

Data Validation:

```text
Allow → Decimal
Data → between
Minimum → 0
Maximum → 5
```

তাহলে:

```text
4.5 ✅
3.2 ✅
5 ✅
6 ❌
-1 ❌
```

---

# 6️⃣ সবচেয়ে Important — Dropdown List

ধরি Department:

```text
IT
HR
Finance
Marketing
```

আমরা চাই user manually type না করে dropdown থেকে select করুক।

### Steps

Department cells select করো:

**Data → Data Validation**

তারপর:

```text
Allow → List
```

Source:

```text
IT,HR,Finance,Marketing
```

এখন cell-এ dropdown arrow দেখা যাবে।

User select করবে:

```text
▼ IT
  HR
  Finance
  Marketing
```

---

# 7️⃣ Dropdown-এর সুবিধা

Dropdown ব্যবহার করলে:

❌ ভুল spelling কমে

❌ inconsistent data কমে

❌ data cleaning কম লাগে

✅ data analysis সহজ হয়

✅ PivotTable accurate হয়

---

# 8️⃣ Dropdown-এর জন্য আলাদা List ব্যবহার করা ⭐

Directly লিখতে পারো:

```text
IT,HR,Finance,Marketing
```

কিন্তু professional Excel file-এ আলাদা list রাখা ভালো।

ধরি `Lists` নামে একটি sheet আছে।

|A|
|---|
|IT|
|HR|
|Finance|
|Marketing|

তাহলে এই list-কে source হিসেবে ব্যবহার করা যায়।

এতে future-এ নতুন Department add করা সহজ হয়।

---

# 9️⃣ Smart Dropdown with Excel Table

এখন আরও professional approach।

একটি Table বানাও:

|Department|
|---|
|IT|
|HR|
|Finance|
|Marketing|

`Ctrl + T`

Table-এর নাম ধরো:

```text
DepartmentTable
```

এখন নতুন department যোগ করলে Table automatically expand করতে পারে।

এটা large workbook-এর জন্য useful।

---

# 🔟 Dynamic Dropdown with UNIQUE ⭐⭐⭐

Class 16-এ আমরা শিখেছিলাম:

```excel
=SORT(UNIQUE(C2:C100))
```

এখন এটাকে dropdown-এর foundation হিসেবে ব্যবহার করতে পারি।

ধরি raw employee data:

|Department|
|---|
|IT|
|HR|
|IT|
|Finance|
|HR|
|Marketing|

একটি আলাদা জায়গায় লিখো:

```excel
=SORT(UNIQUE(C2:C100))
```

ধরি formula `H2`-তে আছে।

তাহলে result spill করবে:

```text
H2  Finance
H3  HR
H4  IT
H5  Marketing
```

এই generated list ব্যবহার করে dropdown তৈরি করা যায়।

---

# 1️⃣1️⃣ Spill Range `#` আবার মনে রাখো

যদি:

```excel
=SORT(UNIQUE(C2:C100))
```

H2-তে থাকে, পুরো spilled range reference:

```excel
=H2#
```

অর্থাৎ:

> H2 থেকে যতগুলো result automatically spill করেছে, সবগুলো।

এটি Dynamic Dropdown তৈরিতে খুব useful।

---

# 1️⃣2️⃣ Input Message

Data Validation-এ শুধু restriction না, user-কে instruction-ও দেওয়া যায়।

ধরি Salary cell।

Input Message:

```text
Title:
Salary

Input Message:
Enter monthly salary in BDT.
```

User cell select করলে instruction দেখতে পাবে।

এটা professional forms-এর জন্য useful।

---

# 1️⃣3️⃣ Error Alert

ধরি Age 18–60-এর মধ্যে হতে হবে।

User যদি লিখে:

```text
15
```

তাহলে Error Alert দেখাতে পারো।

### Style

**Stop**

এতে invalid data block হবে।

Message:

```text
Please enter an age between 18 and 60.
```

---

# 1️⃣4️⃣ Error Alert-এর তিনটি Style

|Style|Behaviour|
|---|---|
|Stop|Invalid input block করে|
|Warning|Warning দেখায়|
|Information|Information দেখায়|

### সাধারণভাবে

Strict data entry হলে:

**Stop** ব্যবহার করা ভালো।

---

# 1️⃣5️⃣ Date Validation

ধরি Joining Date।

আমরা চাই:

> Date অবশ্যই 1 January 2020 থেকে 31 December 2026-এর মধ্যে হবে।

Data Validation:

```text
Allow → Date
Data → between
Start date → 01/01/2020
End date → 31/12/2026
```

এখন:

```text
15/05/2024 ✅
10/01/2026 ✅
15/03/2019 ❌
```

---

# 1️⃣6️⃣ Future Date Block করা

ধরি Leave Request Date।

আমরা চাই user future date দিতে পারবে না।

এখানে Custom validation ব্যবহার করা যায়।

ধরি cell A2।

Formula:

```excel
=A2<=TODAY()
```

অর্থাৎ:

> A2-এর date আজকের date-এর চেয়ে বড় হতে পারবে না।

---

# 1️⃣7️⃣ Text Length Validation

ধরি Employee ID অবশ্যই 6 characters হবে।

Data Validation:

```text
Allow → Text Length
Data → equal to
Length → 6
```

তাহলে:

```text
EMP101 ✅
EMP102 ✅
EMP1 ❌
EMP123456 ❌
```

---

# 1️⃣8️⃣ Custom Validation

এটা একটু advanced।

ধরি Salary অবশ্যই 10,000-এর বেশি হতে হবে।

Custom formula:

```excel
=A2>=10000
```

যদি A2 salary cell হয়।

---

# 1️⃣9️⃣ Custom Validation — Unique ID ⭐

ধরি Employee ID A2:A1000।

আমরা চাই duplicate ID allowed হবে না।

A2-এর জন্য Custom formula:

```excel
=COUNTIF($A$2:$A$1000,A2)=1
```

এর concept:

> এই ID পুরো range-এ মাত্র একবার থাকতে হবে।

তাহলে:

```text
EMP001 ✅
EMP002 ✅
EMP001 ❌
```

এটা database-এর **unique constraint** concept-এর সাথে খুব similar।

---

# 2️⃣0️⃣ Dependent Dropdown ⭐⭐⭐

এটি Data Validation-এর advanced topic।

ধরি:

### Country

```text
Bangladesh
India
Nepal
```

Country অনুযায়ী City change হবে।

Bangladesh:

```text
Dhaka
Chittagong
Rajshahi
```

India:

```text
Delhi
Mumbai
Kolkata
```

Nepal:

```text
Kathmandu
Pokhara
Lalitpur
```

অর্থাৎ:

```text
Country
   ↓
City Dropdown
```

এটাকে বলে:

### Dependent Dropdown

Real-world forms-এ এটা অনেক ব্যবহার হয়।

---

# 2️⃣1️⃣ Dependent Dropdown-এর Concept

ধরি:

```text
A2 = Country
B2 = City
```

User A2-তে select করল:

```text
Bangladesh
```

তখন B2-তে শুধু Bangladesh-এর cities দেখাবে:

```text
Dhaka
Chittagong
Rajshahi
```

India select করলে:

```text
Delhi
Mumbai
Kolkata
```

এখানে প্রথম dropdown-এর value দ্বিতীয় dropdown-এর options determine করে।

---

# 2️⃣2️⃣ Excel Form-এর মতো Input Sheet

তুমি একটি professional data-entry form-এর মতো sheet বানাতে পারো:

|Field|Input|
|---|---|
|Employee ID|`EMP001`|
|Name|Atiar|
|Department|▼ IT|
|City|▼ Dhaka|
|Age|25|
|Joining Date|10/09/2026|
|Salary|50000|

এখানে:

- Department → Dropdown
    
- City → Dropdown
    
- Age → Whole Number
    
- Date → Date Validation
    
- Salary → Decimal/Whole Number
    
- Employee ID → Unique validation
    

🔥 এটাই Data Validation-এর practical power।

---

# 2️⃣3️⃣ Database-এর সাথে Connection

তুমি যেহেতু Database Design শিখছো, এই conceptটা মনে রাখো।

Excel:

```text
Data Validation
      ↓
Bad data কমানো
```

Database:

```text
Constraints
      ↓
Bad data prevent করা
```

উদাহরণ:

|Excel|Database|
|---|---|
|Dropdown|Controlled value / FK|
|Unique validation|UNIQUE|
|Required input|NOT NULL|
|Number validation|CHECK|
|Date validation|CHECK|
|Valid related value|FOREIGN KEY|

Excel database নয়, কিন্তু **data quality control-এর concept** অনেকটা একই।

---

# ⚠️ Class 17 Beginner Mistakes

### ❌ Mistake 1: পুরো column-এ validation না দেওয়া

শুধু C2-তে validation দিয়ে C3:C1000-এ data entry করলে control থাকবে না।

প্রয়োজনীয় পুরো range select করো।

---

### ❌ Mistake 2: Dropdown source-এ inconsistent values

❌

```text
IT
It
it
I.T
```

✅

```text
IT
HR
Finance
Marketing
```

---

### ❌ Mistake 3: Validation = Data Cleaning মনে করা

Data Validation **আগে থেকেই ভুল data আটকাতে** সাহায্য করে।

আর Data Cleaning:

> ইতিমধ্যে থাকা dirty data ঠিক করে।

---

### ❌ Mistake 4: `#SPILL!`

Dynamic dropdown-এর source list-এর spill area blocked হলে:

```text
#SPILL!
```

হতে পারে।

---

# 📌 Class 17 Cheat Sheet

|Requirement|Validation|
|---|---|
|Age 18–60|Whole Number|
|Rating 0–5|Decimal|
|Department select|List|
|Joining Date|Date|
|Time input|Time|
|Employee ID 6 chars|Text Length|
|Custom rule|Custom|
|Duplicate prevent|`COUNTIF()`|
|Future date prevent|`TODAY()`|
|Smart unique list|`SORT(UNIQUE())`|

### গুরুত্বপূর্ণ formulas

**No future date:**

```excel
=A2<=TODAY()
```

**Unique ID:**

```excel
=COUNTIF($A$2:$A$1000,A2)=1
```

**Dynamic unique list:**

```excel
=SORT(UNIQUE(C2:C100))
```

---

# 📝 Class 17 Assignment

একটি **Employee Registration Sheet** বানাও।

Columns:

```text
Employee ID
Name
Department
City
Age
Joining Date
Salary
```

### Task 1

Employee ID-এর জন্য **6-character validation** দাও।

### Task 2

Employee ID duplicate হলে block করো।

### Task 3

Department-এর জন্য dropdown:

```text
IT
HR
Finance
Marketing
```

### Task 4

Age শুধু:

```text
18–60
```

হতে পারবে।

### Task 5

Joining Date future date হতে পারবে না।

### Task 6

Salary minimum:

```text
10000
```

করো।

### Task 7 ⭐

Employee data থেকে:

```excel
=SORT(UNIQUE(C2:C100))
```

দিয়ে dynamic Department list তৈরি করো।

### Task 8 ⭐⭐

Country → City **Dependent Dropdown** তৈরি করার চেষ্টা করো।

---

# 🧪 Class 17 Quiz

**1. Data Validation-এর মূল উদ্দেশ্য কী?**

A. Chart তৈরি  
B. Input control করা  
C. PivotTable তৈরি  
D. Formula delete করা

**2. Dropdown তৈরি করতে কোন Validation type?**

A. Date  
B. List  
C. Decimal  
D. Text Length

**3. Age 18–60 হলে কোন type appropriate?**

A. Whole Number  
B. List  
C. Text Length  
D. Time

**4. Invalid data সম্পূর্ণ block করতে কোন Error Alert style?**

A. Information  
B. Warning  
C. Stop  
D. Ignore

**5. Duplicate Employee ID prevent করতে কোন function useful?**

A. SUM  
B. COUNTIF  
C. AVERAGE  
D. SORT

**6. `=A2<=TODAY()` কী check করছে?**

A. Salary  
B. Duplicate  
C. Future date  
D. Text length

**7. `SORT(UNIQUE())` কী করে?**

A. Duplicate তৈরি  
B. Unique values বের করে sort করে  
C. Data delete করে  
D. Chart বানায়

**8. Country অনুযায়ী City dropdown change হলে সেটাকে কী বলে?**

A. Static Dropdown  
B. Dependent Dropdown  
C. Pivot Dropdown  
D. Formula Dropdown

**9. Database-এর `UNIQUE` constraint-এর সাথে Excel-এর কোন concept সবচেয়ে কাছাকাছি?**

A. Dropdown  
B. Unique ID validation  
C. Sort  
D. Filter

**10. Data Validation এবং Data Cleaning-এর মধ্যে সঠিক statement কোনটি?**

A. দুটো একই  
B. Validation আগে থেকেই ভুল input আটকাতে পারে  
C. Cleaning শুধু dropdown তৈরি করে  
D. Validation শুধু chart-এর জন্য

---

### 🎯 তোমার Excel Progress

**17 / 22+ Classes Complete ✅**

তুমি এখন Excel-এর **fundamentals → formulas → lookup → conditional analysis → PivotTable → Dynamic Arrays → Data Validation** পর্যন্ত চলে এসেছো।

পরের ধাপে **Class 18 — Conditional Formatting + Advanced Rules + Formula-Based Formatting** শিখলে Excel-এর data visually analyze করা আরও powerful হবে।


----
# 📘 Excel Mastery — Class 18

## 🎨 Conditional Formatting + Advanced Rules + Formula-Based Formatting

আজ আমরা Excel-এর **Conditional Formatting** শিখব। এর মাধ্যমে Excel নিজে নিজে condition অনুযায়ী cell-এর **color, font, icon, data bar** ইত্যাদি পরিবর্তন করতে পারে।

এটা Data Analyst-এর জন্য খুব useful, কারণ বড় dataset থেকে **important information চোখে দ্রুত খুঁজে পাওয়া যায়।**

---

# 1️⃣ Conditional Formatting কী?

সহজভাবে:

> **Condition সত্য হলে Excel automatically formatting করবে।**

উদাহরণ:

|Student|Mark|
|---|--:|
|Rahim|85|
|Karim|35|
|Hasan|72|
|Sakib|28|

আমরা চাই:

- `40-এর নিচে` → highlight
    
- `80 বা তার বেশি` → highlight
    

Excel automatically বুঝবে কোন cell-এর formatting পরিবর্তন করতে হবে।

---

# 2️⃣ কোথায় পাব?

প্রথমে range select করো।

তারপর:

**Home → Conditional Formatting**

সেখানে বিভিন্ন option দেখতে পাবে।

---

# 3️⃣ Highlight Cells Rules

এটা সবচেয়ে basic এবং important section।

এর মধ্যে সাধারণত থাকে:

- Greater Than
    
- Less Than
    
- Between
    
- Equal To
    
- Text That Contains
    
- A Date Occurring
    
- Duplicate Values
    

---

# 4️⃣ Greater Than

ধরি Salary:

|Employee|Salary|
|---|--:|
|Rahim|35000|
|Karim|55000|
|Hasan|45000|
|Sakib|70000|

আমরা চাই:

> Salary > 50000 হলে highlight।

### Steps:

1. Salary range select করো
    
2. Home → Conditional Formatting
    
3. Highlight Cells Rules
    
4. Greater Than
    
5. লিখো:
    

```text
50000
```

তারপর formatting select করো।

Result:

```text
35000
55000 ← Highlight
45000
70000 ← Highlight
```

---

# 5️⃣ Less Than

ধরি student marks:

```text
85
72
39
28
66
```

আমরা চাই:

> 40-এর নিচে marks highlight।

Rule:

```text
Less Than → 40
```

Result:

```text
85
72
39  ← Highlight
28  ← Highlight
66
```

---

# 6️⃣ Between

ধরি Salary:

```text
30000
45000
55000
70000
90000
```

আমরা চাই:

> 40,000 থেকে 60,000-এর মধ্যে salary highlight।

Rule:

```text
Between
40000
60000
```

তাহলে:

```text
30000
45000 ← Highlight
55000 ← Highlight
70000
90000
```

---

# 7️⃣ Equal To

ধরি Department:

```text
IT
HR
Finance
IT
Marketing
```

আমরা শুধু `"IT"` highlight করতে চাই।

Rule:

**Highlight Cells Rules → Equal To**

Value:

```text
IT
```

---

# 8️⃣ Text That Contains

ধরি employee names:

```text
Rahim
Karim
Rahman
Hasan
Rafi
```

যদি `"Rah"` contains এমন সব text highlight করতে চাই:

**Text That Contains → `Rah`**

তাহলে:

```text
Rahim   ← Highlight
Karim
Rahman  ← Highlight
Hasan
Rafi
```

---

# 9️⃣ Duplicate Values ⭐

এটা Data Cleaning-এর জন্য খুব useful।

ধরি Employee ID:

```text
EMP001
EMP002
EMP003
EMP002
EMP004
EMP001
```

Range select করো:

**Conditional Formatting → Highlight Cells Rules → Duplicate Values**

Excel duplicate values visually identify করবে।

এটা খুব useful যখন dataset-এ duplicate record খুঁজছো।

---

# 🔟 Top/Bottom Rules

Conditional Formatting-এর আরেকটি powerful section হলো:

**Top/Bottom Rules**

এখানে পাওয়া যায়:

- Top 10 Items
    
- Top 10%
    
- Bottom 10 Items
    
- Bottom 10%
    
- Above Average
    
- Below Average
    

---

# 1️⃣1️⃣ Top 10 Items

ধরি:

```text
45000
70000
55000
90000
40000
65000
80000
```

Top 10 Items rule দিলে highest values highlight হবে।

তুমি `10` পরিবর্তন করে:

```text
Top 3
```

করতে পারো।

তাহলে শুধু top 3 salary highlight হবে।

---

# 1️⃣2️⃣ Above Average

ধরি:

```text
40
50
60
70
80
```

Conditional Formatting:

**Top/Bottom Rules → Above Average**

Excel automatically average calculate করে average-এর বেশি values highlight করবে।

Average:

```text
60
```

তাই:

```text
70 ← Highlight
80 ← Highlight
```

---

# 1️⃣3️⃣ Data Bars 📊

Data Bar numeric data visually compare করার জন্য খুব useful।

ধরি:

|Employee|Sales|
|---|--:|
|Rahim|20000|
|Karim|50000|
|Hasan|80000|
|Sakib|40000|

Select Sales column:

**Conditional Formatting → Data Bars**

তাহলে cells-এর ভিতরে bar দেখা যাবে।

Concept:

```text
20000  ███
50000  ███████
80000  ███████████
40000  ██████
```

বড় value → বড় bar।

---

# 1️⃣4️⃣ Color Scales 🌈

Color Scale দিয়ে low → medium → high visually বোঝা যায়।

উদাহরণ:

```text
20
40
60
80
100
```

Excel values অনুযায়ী different shades দেখাবে।

এটা:

- Sales
    
- Marks
    
- Profit
    
- Performance
    
- Rating
    

ইত্যাদির জন্য useful।

---

# 1️⃣5️⃣ Icon Sets

Icon Set দিয়ে numerical values-এর পাশে icons দেখানো যায়।

উদাহরণ:

```text
Sales Growth

↑  25%
→  10%
↓  -5%
```

সাধারণত:

- Green/up → good
    
- Yellow/middle → average
    
- Red/down → poor
    

⚠️ তবে সবসময় color/icon-এর meaning logically define করে ব্যবহার করবে।

---

# 1️⃣6️⃣ Formula-Based Conditional Formatting ⭐⭐⭐

এটাই আজকের সবচেয়ে important topic।

এখানে আমরা নিজের formula লিখে formatting control করতে পারি।

ধরি:

|Name|Salary|
|---|--:|
|Rahim|50000|
|Karim|35000|
|Hasan|60000|
|Sakib|45000|

আমরা চাই:

> Salary ≥ 50000 হলে **পুরো row highlight** হবে।

### Steps:

1. পুরো dataset select করো:
    

```text
A2:B5
```

2. Conditional Formatting
    
3. New Rule
    
4. **Use a formula to determine which cells to format**
    
5. Formula:
    

```excel
=$B2>=50000
```

তারপর formatting select করো।

---

# 1️⃣7️⃣ `$B2` কেন?

এখানে `$` খুব important।

```excel
=$B2>=50000
```

মানে:

```text
$B → Column B fixed
2   → Row relative
```

যখন Excel নিচের row check করবে:

```text
B2
B3
B4
B5
```

কিন্তু column B-তেই থাকবে।

---

# 1️⃣8️⃣ Entire Row Highlight

এই technique Data Analyst-এর জন্য খুব useful।

Dataset:

|Name|Department|Salary|
|---|---|--:|
|Rahim|IT|50000|
|Karim|HR|35000|
|Hasan|IT|60000|
|Sakib|Finance|45000|

আমরা চাই:

> Salary ≥ 50000 হলে পুরো row highlight।

Select:

```text
A2:C5
```

Formula:

```excel
=$C2>=50000
```

Result:

```text
Rahim   IT       50000 ← Entire row
Karim   HR       35000
Hasan   IT       60000 ← Entire row
Sakib   Finance  45000
```

---

# 1️⃣9️⃣ Department অনুযায়ী পুরো Row Highlight

ধরি:

|Name|Department|Salary|
|---|---|--:|
|Rahim|IT|50000|
|Karim|HR|35000|
|Hasan|IT|60000|
|Sakib|Finance|45000|

আমরা শুধু IT employees-এর entire row highlight করতে চাই।

Formula:

```excel
=$B2="IT"
```

Select:

```text
A2:C5
```

Result:

```text
Rahim   IT       50000 ← Highlight
Karim   HR       35000
Hasan   IT       60000 ← Highlight
Sakib   Finance  45000
```

---

# 2️⃣0️⃣ Multiple Conditions — AND

এখন advanced।

আমরা চাই:

> Department = IT **AND** Salary ≥ 50000

Formula:

```excel
=AND($B2="IT",$C2>=50000)
```

এখন শুধুমাত্র:

```text
IT + Salary >= 50000
```

rows highlight হবে।

---

# 2️⃣1️⃣ Multiple Conditions — OR

আমরা চাই:

> Department IT **OR** HR

Formula:

```excel
=OR($B2="IT",$B2="HR")
```

এতে IT অথবা HR-এর পুরো row highlight হবে।

---

# 2️⃣2️⃣ Highlight Blank Cells

ধরি Email column:

|Name|Email|
|---|---|
|Rahim|[rahim@gmail.com](mailto:rahim@gmail.com)|
|Karim||
|Hasan|[hasan@gmail.com](mailto:hasan@gmail.com)|
|Sakib||

Blank cell identify করতে:

```excel
=ISBLANK(B2)
```

এটা দিয়ে blank cells highlight করা যায়।

---

# 2️⃣3️⃣ Highlight Non-Blank Cells

Formula:

```excel
=B2<>""
```

মানে:

> B2 empty নয়।

---

# 2️⃣4️⃣ Duplicate Highlight with Formula

ধরি Employee ID A column।

Duplicate ID highlight করতে:

```excel
=COUNTIF($A$2:$A$100,A2)>1
```

যদি কোনো ID একাধিকবার থাকে → TRUE।

Excel সেই cell format করবে।

---

# 2️⃣5️⃣ Expired Date Highlight ⭐

ধরি Due Date:

|Task|Due Date|
|---|---|
|Task A|01/09/2026|
|Task B|20/09/2026|
|Task C|05/09/2026|

আমরা চাই:

> আজকের date-এর আগের due date → highlight।

Formula:

```excel
=B2<TODAY()
```

এতে expired dates automatically highlight হবে।

---

# 2️⃣6️⃣ Due Soon

আরও advanced।

আমরা চাই:

> আগামী 7 দিনের মধ্যে due হবে এমন date highlight।

Formula:

```excel
=AND(B2>=TODAY(),B2<=TODAY()+7)
```

এখানে:

```text
B2 >= TODAY()
```

→ আজ বা future date

এবং:

```text
B2 <= TODAY()+7
```

→ আগামী 7 দিনের মধ্যে।

---

# 2️⃣7️⃣ Conditional Formatting + Dynamic Analysis

Class 15–17-এর knowledge combine করলে powerful system তৈরি হয়।

যেমন:

```text
Data
 ↓
Data Validation
 ↓
Formula
 ↓
Conditional Formatting
 ↓
Dashboard
```

উদাহরণ:

**Salary ≥ 70000**

→ entire row highlight

**Expired task**

→ highlight

**Duplicate ID**

→ highlight

**Top 5 sales**

→ highlight

**Low performance**

→ highlight

---

# 🧠 `$` Reference এখানে খুব Important

Conditional Formatting formula-তে `$` বুঝতে হবে।

ধরি:

```excel
=$C2>=50000
```

### `$C2`

```text
$C → column fixed
2  → row changes
```

### `C$2`

```text
C → column changes
$2 → row fixed
```

### `$C$2`

```text
column fixed
row fixed
```

এটা Class 3-এর absolute/mixed reference-এর সাথে directly related।

---

# ⚠️ Common Beginner Mistakes

### ❌ Mistake 1

পুরো row highlight করতে গিয়ে:

```excel
=C2>=50000
```

ব্যবহার করা।

অনেক ক্ষেত্রে column reference shift হয়ে যেতে পারে।

সাধারণত row-based formatting-এর জন্য:

```excel
=$C2>=50000
```

ভালো।

---

### ❌ Mistake 2 — Wrong Apply Range

Formula:

```excel
=$C2>=50000
```

কিন্তু Apply To শুধু:

```text
C2:C100
```

দিলে পুরো row highlight হবে না।

পুরো dataset select করতে হবে:

```text
A2:F100
```

---

### ❌ Mistake 3 — Conditional Formatting-কে permanent formatting ভাবা

Conditional Formatting condition-এর উপর নির্ভর করে।

Value পরিবর্তন করলে formatting-ও automatically change হতে পারে।

---

### ❌ Mistake 4 — Too many colors

Professional dashboard-এ অনেক রং ব্যবহার করলে data বোঝা কঠিন হয়।

**Purposeful formatting** ব্যবহার করো।

---

# 📌 Class 18 Cheat Sheet

|Requirement|Rule/Formula|
|---|---|
|> 50000|Greater Than|
|< 40|Less Than|
|40–60|Between|
|IT|Equal To|
|Duplicate|Duplicate Values|
|Top 5|Top/Bottom|
|Visual comparison|Data Bars|
|Low → High|Color Scale|
|Performance indicators|Icon Sets|
|Salary ≥ 50000|`=$C2>=50000`|
|Department IT|`=$B2="IT"`|
|IT + Salary ≥ 50000|`=AND($B2="IT",$C2>=50000)`|
|IT or HR|`=OR($B2="IT",$B2="HR")`|
|Blank|`=ISBLANK(B2)`|
|Duplicate formula|`=COUNTIF($A$2:$A$100,A2)>1`|
|Expired date|`=B2<TODAY()`|
|Due within 7 days|`=AND(B2>=TODAY(),B2<=TODAY()+7)`|

---

# 📝 Class 18 Assignment

এই dataset তৈরি করো:

|ID|Name|Department|Salary|Joining Date|Performance|
|--:|---|---|--:|---|--:|
|101|Rahim|IT|50000|01/01/2024|85|
|102|Karim|HR|35000|15/03/2025|65|
|103|Hasan|IT|75000|10/06/2023|92|
|104|Sakib|Finance|45000|20/02/2024|55|
|105|Nila|IT|60000|05/05/2025|78|
|106|Rafi|HR|30000|10/01/2026|35|

### Task 1

Salary > 50000 highlight করো।

### Task 2

Performance < 40 highlight করো।

### Task 3

Top 3 Performance highlight করো।

### Task 4

Performance-এর জন্য **Data Bars** ব্যবহার করো।

### Task 5

Salary-এর জন্য **Color Scale** ব্যবহার করো।

### Task 6 ⭐

Salary ≥ 50000 হলে পুরো row highlight করো।

Formula:

```excel
=$D2>=50000
```

### Task 7 ⭐

শুধু IT employees-এর পুরো row highlight করো।

```excel
=$C2="IT"
```

### Task 8 ⭐⭐

IT + Salary ≥ 50000:

```excel
=AND($C2="IT",$D2>=50000)
```

### Task 9 ⭐⭐

Duplicate ID highlight করো:

```excel
=COUNTIF($A$2:$A$100,A2)>1
```

### Task 10 ⭐⭐⭐

Joining Date যদি আজকের আগের হয়, তাহলে expired/old record highlight করো:

```excel
=E2<TODAY()
```

---

# 🧪 Class 18 Quiz

**1. Conditional Formatting কী করে?**

A. Data delete করে  
B. Condition অনুযায়ী formatting পরিবর্তন করে  
C. Formula remove করে  
D. Workbook তৈরি করে

**2. Duplicate values দ্রুত identify করতে কোন option?**

A. Data Bars  
B. Duplicate Values  
C. Color Scale  
D. Icon Sets

**3. Numeric values-এর visual bar-এর জন্য?**

A. Data Bars  
B. Text Filter  
C. Dropdown  
D. XLOOKUP

**4. Low → High visually দেখাতে কোনটি useful?**

A. Color Scales  
B. VLOOKUP  
C. Data Validation  
D. SUMIFS

**5. পুরো row highlight করতে salary column C হলে কোন formula appropriate?**

A. `=C2>=50000`  
B. `=$C2>=50000`  
C. `=$C$2>=50000`  
D. `=C$2>=50000`

**6. `=$C2`-এ কোনটি fixed?**

A. Row  
B. Column  
C. দুটোই  
D. কোনোটিই না

**7. IT এবং Salary ≥ 50000 check করতে?**

A. `OR()`  
B. `AND()`  
C. `NOT()`  
D. `COUNT()`

**8. Duplicate ID formula কোনটি?**

A. `=SUM(A2)>1`  
B. `=COUNTIF($A$2:$A$100,A2)>1`  
C. `=UNIQUE(A2)`  
D. `=SORT(A2)`

**9. Expired date highlight করতে?**

A. `=B2>TODAY()`  
B. `=B2<TODAY()`  
C. `=B2=TODAY()`  
D. `=B2+TODAY()`

**10. আগামী 7 দিনের মধ্যে due date identify করতে কোনটি?**

A. `=B2<TODAY()`  
B. `=AND(B2>=TODAY(),B2<=TODAY()+7)`  
C. `=SUM(B2)`  
D. `=UNIQUE(B2)`

---

## 🎯 Progress

**18 / 22+ Classes Complete ✅**

এখন তুমি Excel-এর **Data Validation + Dynamic Arrays + Conditional Formatting** পর্যন্ত শিখে ফেলেছো।

পরবর্তী গুরুত্বপূর্ণ ধাপ হবে:

### **Class 19 — Advanced Charts & Professional Data Visualization 📊**

এখানে আমরা শিখব **Column, Bar, Line, Combo Chart, Scatter Plot, KPI-style visualization, chart formatting এবং কোন data-এর জন্য কোন chart নির্বাচন করতে হবে।**



----
# 📘 Excel Mastery — Class 19

## 📊 Advanced Charts & Professional Data Visualization

আজ আমরা শুধু **chart বানানো** শিখব না—বরং **কোন data-এর জন্য কোন chart ব্যবহার করতে হবে, কীভাবে professional chart তৈরি করতে হবে, এবং chart থেকে business insight বের করতে হবে** সেটা শিখব।

তুমি যেহেতু **Data Analyst → Data Engineer** roadmap follow করছো, এই অংশটা খুব গুরুত্বপূর্ণ।

---

# 1️⃣ Data Visualization কী?

অনেক data table দেখে বুঝতে সময় লাগে।

যেমন:

|Month|Sales|
|---|--:|
|Jan|50,000|
|Feb|60,000|
|Mar|55,000|
|Apr|75,000|
|May|90,000|

Table দেখে trend বোঝা যায়, কিন্তু chart করলে চোখে সঙ্গে সঙ্গে বোঝা যায়:

**Sales overall increase করছে।**

এটাই Data Visualization।

---

# 2️⃣ কোন Data-এর জন্য কোন Chart?

এটা মুখস্থ না করে concept বুঝো।

|উদ্দেশ্য|Best Chart|
|---|---|
|Category comparison|Column / Bar|
|Time trend|Line|
|Ranking|Bar|
|Part of whole|Pie / Doughnut|
|Two numeric variables relationship|Scatter|
|দুই ধরনের metric|Combo|
|Monthly sales|Line|
|Department salary comparison|Column|
|Top 10 products|Bar|
|Sales + Profit|Combo|

### Golden Rule ⭐

> **Question → Data Type → Chart**

---

# 3️⃣ Column Chart

Column Chart ব্যবহার করো যখন:

> কয়েকটি category-এর value compare করতে হবে।

উদাহরণ:

|Department|Employees|
|---|--:|
|IT|40|
|HR|20|
|Finance|30|
|Marketing|25|

Chart:

### কখন ব্যবহার করবে?

- Department comparison
    
- Product sales
    
- City-wise revenue
    
- Employee count
    

---

# 4️⃣ Bar Chart

Bar Chart হলো horizontal comparison।

ধরি product names অনেক বড়:

```text
Advanced Laptop Model
Professional Office Monitor
Wireless Mechanical Keyboard
```

এক্ষেত্রে horizontal bar chart বেশি readable।

বিশেষ করে **Top 10 products** দেখাতে Bar Chart খুব ভালো।

---

# 5️⃣ Line Chart 📈

Line Chart সবচেয়ে useful:

> **Time-এর সাথে value কীভাবে পরিবর্তন হচ্ছে** সেটা দেখাতে।

উদাহরণ:

|Month|Sales|
|---|--:|
|Jan|50,000|
|Feb|60,000|
|Mar|55,000|
|Apr|75,000|
|May|90,000|
|Jun|85,000|

এখানে আমরা দেখতে পাচ্ছি:

- Feb → increase
    
- Mar → decrease
    
- Apr → increase
    
- May → strong increase
    
- Jun → slight decrease
    

এটাই trend analysis।

---

# 6️⃣ Pie Chart 🥧

Pie Chart ব্যবহার করো যখন:

> একটি total-এর মধ্যে category-গুলোর share দেখাতে হবে।

উদাহরণ:

|Product|Sales|
|---|--:|
|Laptop|50|
|Phone|30|
|Tablet|20|

Total:

```text
50 + 30 + 20 = 100
```

তাই:

```text
Laptop → 50%
Phone  → 30%
Tablet → 20%
```

Pie Chart appropriate।

### ⚠️ কখন Pie Chart ব্যবহার করবে না?

যদি 15–20টি category থাকে।

তখন chart খুব confusing হয়ে যায়।

---

# 7️⃣ Scatter Plot

Scatter Plot ব্যবহার করা হয়:

> **দুটি numerical variable-এর relationship** দেখতে।

উদাহরণ:

|Study Hours|Exam Score|
|--:|--:|
|1|45|
|2|50|
|3|58|
|4|65|
|5|72|
|6|80|

এখানে প্রশ্ন:

> Study Hours বাড়লে Exam Score কি বাড়ে?

Scatter Plot ব্যবহার করবে।

এখানে positive relationship দেখা যাচ্ছে।

---

# 8️⃣ Combo Chart ⭐⭐⭐

এটা professional Excel reporting-এ খুব useful।

ধরি:

|Month|Sales|Profit|
|---|--:|--:|
|Jan|100000|20000|
|Feb|120000|25000|
|Mar|150000|35000|

আমরা একই chart-এ:

- Sales → Column
    
- Profit → Line
    

দেখাতে চাই।

এটা **Combo Chart**।

### Create:

**Insert → Combo Chart**

তারপর:

```text
Sales  → Column
Profit → Line
```

### কখন ব্যবহার করবে?

- Sales + Profit
    
- Revenue + Growth
    
- Actual + Target
    
- Sales + Margin
    

---

# 9️⃣ Actual vs Target

Business dashboard-এ এটা খুব common।

|Month|Actual|Target|
|---|--:|--:|
|Jan|90|100|
|Feb|110|100|
|Mar|95|100|
|Apr|120|100|

এখানে manager জানতে চাইবে:

> Target achieve হয়েছে কি?

Combo বা Column chart ব্যবহার করা যায়।

---

# 🔟 Chart Title

❌ Bad:

```text
Chart 1
```

❌

```text
Sales
```

Better:

```text
Monthly Sales — 2026
```

আরও meaningful:

```text
Monthly Sales Trend — 2026
```

Chart title দেখেই যেন user বুঝতে পারে chart কী দেখাচ্ছে।

---

# 1️⃣1️⃣ Axis Titles

Chart-এর axis-এর meaning clear হওয়া দরকার।

Example:

```text
X-axis → Month
Y-axis → Sales (BDT)
```

তাই:

**Chart Design → Add Chart Element → Axis Titles**

ব্যবহার করতে পারো।

---

# 1️⃣2️⃣ Data Labels

Data Label chart-এর data value directly দেখায়।

যেমন:

```text
IT       40
HR       20
Finance  30
```

Small chart বা presentation-এর ক্ষেত্রে useful।

কিন্তু অনেক data point থাকলে সব label দিলে chart cluttered হয়ে যেতে পারে।

---

# 1️⃣3️⃣ Legend

যখন chart-এ multiple series থাকে, Legend বলে দেয় কোন series কোনটি।

উদাহরণ:

```text
■ Sales
■ Profit
```

যদি শুধু একটি series থাকে, অনেক সময় legend-এর প্রয়োজন নেই।

---

# 1️⃣4️⃣ Gridlines

Gridlines comparison সহজ করতে পারে।

কিন্তু অতিরিক্ত visual elements chart-কে messy করে।

Professional chart-এর লক্ষ্য:

> **Simple + Clear + Useful**

---

# 1️⃣5️⃣ Chart Formatting

Professional chart বানানোর সময়:

### রাখবে:

✅ Clear title  
✅ Meaningful axis  
✅ Proper number format  
✅ Readable labels  
✅ Appropriate chart type  
✅ Enough spacing

### Avoid করবে:

❌ 3D chart  
❌ Too many colors  
❌ Unnecessary decoration  
❌ Too many labels  
❌ Huge legend  
❌ Misleading axis

---

# 1️⃣6️⃣ 3D Chart কেন Avoid?

Beginnerরা প্রায়ই:

```text
3D Pie
3D Column
3D Bar
```

ব্যবহার করে।

দেখতে attractive হলেও data comparison কঠিন হতে পারে।

Data Analyst-এর লক্ষ্য:

> **Beauty নয়, clarity।**

---

# 1️⃣7️⃣ Axis Scale-এর ব্যাপারে সতর্কতা ⭐

ধরি:

```text
A = 95
B = 97
C = 99
```

যদি Y-axis:

```text
90 → 100
```

থেকে শুরু হয়, difference অনেক বড় মনে হতে পারে।

কখনো কখনো এটা misleading হতে পারে।

তাই chart-এর axis scale carefully set করবে।

বিশেষ করে:

- percentages
    
- survey results
    
- performance comparisons
    

---

# 1️⃣8️⃣ Number Formatting

ধরি value:

```text
1250000
```

Chart-এ এটা:

```text
1,250,000
```

এর বদলে compact format:

```text
1.25M
```

হতে পারে।

Business dashboard-এ readable number format অনেক গুরুত্বপূর্ণ।

---

# 1️⃣9️⃣ Top-N Chart

ধরি 100টি product আছে।

Manager বললো:

> Top 5 products দেখাও।

প্রথমে data sort/filter করে Top 5 বের করতে পারো।

তারপর Bar Chart।

Example:

```text
Laptop       ██████████
Monitor      ████████
Keyboard     ██████
Mouse        █████
Headphone    ████
```

Top-N analysis খুব common business task।

---

# 2️⃣0️⃣ Dynamic Chart

এখন Excel-এর advanced power।

ধরি তুমি dropdown থেকে Department select করবে:

```text
Department: ▼ IT
```

IT select করলে chart শুধু IT-এর data দেখাবে।

HR select করলে:

```text
Department: ▼ HR
```

Chart automatically HR data দেখাবে।

এখানে combine করা যায়:

```text
Data Validation
       ↓
XLOOKUP / FILTER
       ↓
Chart
```

🔥 এই concept dashboard তৈরির foundation।

---

# 2️⃣1️⃣ Dashboard-এর Basic Architecture

একটি professional Excel dashboard এমন হতে পারে:

```text
┌──────────────────────────────────────┐
│        SALES PERFORMANCE DASHBOARD   │
├──────────┬──────────┬───────────────┤
│ Revenue  │ Profit   │ Orders        │
│ 1.2M     │ 250K     │ 1,250         │
├──────────┴──────────┴───────────────┤
│        Monthly Sales Trend           │
│             📈                       │
├──────────────────┬──────────────────┤
│ Sales by Product │ Sales by City    │
│      📊          │      📊          │
└──────────────────┴──────────────────┘
```

এটাই আমরা পরবর্তীতে আরও advancedভাবে বানাব।

---

# 2️⃣2️⃣ KPI কী?

**KPI = Key Performance Indicator**

Business-এর important measurement।

উদাহরণ:

```text
Revenue
Profit
Orders
Customers
Conversion Rate
Average Order Value
```

Dashboard-এর top section-এ KPI cards রাখা যায়।

---

# 2️⃣3️⃣ Example KPI Formulas

ধরি Sales amount C2:C1000।

### Total Revenue

```excel
=SUM(C2:C1000)
```

### Average Sale

```excel
=AVERAGE(C2:C1000)
```

### Number of Orders

```excel
=COUNTA(A2:A1000)
```

### Maximum Sale

```excel
=MAX(C2:C1000)
```

এগুলোকে dashboard-এর KPI হিসেবে দেখানো যায়।

---

# 2️⃣4️⃣ Chart Selection Cheat Sheet ⭐

একটা question দেখলেই এভাবে চিন্তা করবে:

### "কোন department বেশি salary দেয়?"

→ **Column / Bar**

### "গত 12 মাসে sales কীভাবে change করেছে?"

→ **Line**

### "কোন 5টি product সবচেয়ে বেশি বিক্রি হয়েছে?"

→ **Bar**

### "Total sales-এর কত % কোন product?"

→ **Pie**

### "Advertising spending এবং revenue-এর relationship কী?"

→ **Scatter**

### "Sales এবং Profit একসাথে compare করতে চাই"

→ **Combo**

---

# 2️⃣5️⃣ Real Data Analyst Workflow

একজন Data Analyst সাধারণত:

```text
Raw Data
   ↓
Data Cleaning
   ↓
Data Validation
   ↓
Formula / Calculation
   ↓
PivotTable
   ↓
Analysis
   ↓
Chart
   ↓
Dashboard
   ↓
Business Insight
```

তুমি Class 1 থেকে এখন পর্যন্ত আসলে এই workflow-এর অনেকগুলো অংশ শিখে ফেলেছো। 🔥

---

# ⚠️ Class 19-এর Common Beginner Mistakes

### ❌ Mistake 1

সব data-এর জন্য Pie Chart ব্যবহার করা।

### ❌ Mistake 2

Time series-এর জন্য Column Chart ব্যবহার করা, যখন Line Chart trend আরও পরিষ্কারভাবে দেখাতে পারে।

### ❌ Mistake 3

এক chart-এ 10+ series ঢুকিয়ে দেওয়া।

### ❌ Mistake 4

3D chart ব্যবহার করা শুধু সুন্দর দেখানোর জন্য।

### ❌ Mistake 5

Chart title না দেওয়া।

### ❌ Mistake 6

Y-axis-এর unit না বোঝানো।

### ❌ Mistake 7

অতিরিক্ত colors/labels ব্যবহার করা।

### ❌ Mistake 8

Data না বুঝে chart type select করা।

---

# 📌 Class 19 Cheat Sheet

|Chart|Best Use|
|---|---|
|Column|Category comparison|
|Bar|Ranking / long labels|
|Line|Time trend|
|Pie|Part-to-whole|
|Scatter|Relationship|
|Combo|Two different metrics|
|Data Bar|Quick in-cell comparison|

### Golden Rule:

```text
Comparison → Bar/Column
Trend → Line
Composition → Pie
Relationship → Scatter
Different Metrics → Combo
```

---

# 📝 Class 19 Assignment

এই dataset বানাও:

|Month|Sales|Profit|Orders|
|---|--:|--:|--:|
|Jan|80000|15000|80|
|Feb|95000|18000|95|
|Mar|90000|16000|88|
|Apr|110000|22000|105|
|May|125000|28000|120|
|Jun|140000|32000|135|

### Task 1

Monthly Sales-এর **Line Chart** তৈরি করো।

### Task 2

Monthly Profit-এর Line Chart তৈরি করো।

### Task 3

Month-wise Sales comparison-এর Column Chart তৈরি করো।

### Task 4 ⭐

Sales + Profit দিয়ে **Combo Chart** তৈরি করো।

### Task 5

Orders-এর Column Chart তৈরি করো।

### Task 6

সব chart-এর meaningful title দাও।

### Task 7

Axis title যোগ করো।

### Task 8

একটি KPI বানাও:

```text
Total Sales
Total Profit
Total Orders
```

### Task 9 ⭐⭐

Sales-এর Top 3 month বের করে Bar Chart বানাও।

### Task 10 ⭐⭐⭐

একটি mini dashboard তৈরি করো:

```text
Total Sales
Total Profit
Total Orders
       ↓
Sales Trend
       ↓
Profit Trend
       ↓
Monthly Comparison
```

---

# 🧪 Class 19 Quiz

**1. Time trend দেখানোর জন্য সবচেয়ে appropriate chart কোনটি?**

A. Pie  
B. Line  
C. Scatter  
D. Doughnut

**2. Category comparison-এর জন্য?**

A. Column  
B. Line  
C. Scatter  
D. Pie

**3. দুইটি numerical variable-এর relationship দেখতে?**

A. Pie  
B. Bar  
C. Scatter  
D. Column

**4. Part-to-whole relationship-এর জন্য?**

A. Pie  
B. Line  
C. Scatter  
D. Bar

**5. Sales + Profit একই chart-এ দেখাতে কোনটি useful?**

A. Pie  
B. Combo  
C. Scatter  
D. Doughnut

**6. Top 10 products দেখাতে কোন chart সবচেয়ে appropriate?**

A. Bar  
B. Pie  
C. Line  
D. Area

**7. KPI-এর full form কী?**

A. Key Process Input  
B. Key Performance Indicator  
C. Key Product Information  
D. Knowledge Performance Index

**8. Professional chart-এর ক্ষেত্রে কোনটি avoid করা ভালো?**

A. Clear title  
B. Proper labels  
C. Excessive 3D effects  
D. Meaningful axis

**9. Monthly Sales-এর trend analysis করতে কোনটি best?**

A. Line Chart  
B. Pie Chart  
C. Scatter Plot  
D. Doughnut Chart

**10. Dashboard-এর primary goal কী?**

A. শুধু সুন্দর করা  
B. অনেক chart যোগ করা  
C. Important information দ্রুত বোঝানো  
D. Formula hide করা

---

## 🎯 Excel Mastery Progress

**19 / 22+ Classes Complete ✅**

এখন তুমি শিখেছো:

**Fundamentals → Formulas → Functions → Lookup → Data Cleaning → PivotTable → Dynamic Arrays → Data Validation → Conditional Formatting → Professional Visualization**

পরের বড় ধাপ হবে **Class 20 — Power Query: Data Import, Cleaning & Automated ETL**। এখানে Excel-এর সবচেয়ে গুরুত্বপূর্ণ **Data Analyst/ETL skill**-গুলোর একটি শুরু হবে।

**Employees by department**

Illustrative employee counts across departments.

|department|employees|
|---|---|
|IT|40|
|HR|20|
|Finance|30|
|Marketing|25|

**Monthly sales trend**

Illustrative monthly sales from January to June.

|month|sales|
|---|---|
|Jan|50,000|
|Feb|60,000|
|Mar|55,000|
|Apr|75,000|
|May|90,000|
|Jun|85,000|

**Study hours vs exam score**

Illustrative relationship between study time and exam performance.

|studyHours|score|
|---|---|
|1|45|
|2|50|
|3|58|
|4|65|
|5|72|
|6|80|



----
# 📘 Excel Mastery — Class 20

## 🔄 Power Query: Data Import, Cleaning & Automated ETL

আজকের Classটা **খুবই গুরুত্বপূর্ণ**—বিশেষ করে তুমি যেহেতু **Data Analyst → Data Engineer** হতে চাচ্ছো।

এখন পর্যন্ত আমরা Excel-এ অনেক কাজ করেছি। কিন্তু বড় প্রশ্ন হলো:

> প্রতিদিন নতুন CSV/Excel file এলে কি প্রতিবার manually cleaning করতে হবে?

❌ না।

এখানেই **Power Query** আসে।

---

# 1️⃣ Power Query কী?

সহজ ভাষায়:

> **Power Query হলো data import, cleaning, transformation এবং loading automate করার Excel tool।**

এটা অনেকটা ছোটখাটো **ETL pipeline**।

```text
Data Source
     ↓
Extract
     ↓
Transform
     ↓
Load
     ↓
Excel / PivotTable / Dashboard
```

ETL:

- **E = Extract**
    
- **T = Transform**
    
- **L = Load**
    

---

# 2️⃣ Power Query কেন শিখবে?

ধরো প্রতিদিন তোমার কাছে CSV আসে:

```text
sales_01.csv
sales_02.csv
sales_03.csv
...
sales_30.csv
```

প্রতিটি file-এ:

- extra spaces
    
- duplicate rows
    
- wrong data type
    
- blank values
    
- inconsistent names
    
- unnecessary columns
    

আছে।

Manual Excel দিয়ে প্রতিদিন clean করা:

```text
😫 অনেক সময়
```

Power Query দিয়ে একবার transformation steps বানিয়ে রাখলে:

```text
New File
   ↓
Refresh
   ↓
Automatically Clean
   ↓
Updated Result
```

🔥 এটাই automation।

---

# 3️⃣ Power Query কোথায়?

Microsoft 365-এর Excel-এ সাধারণত:

**Data → Get & Transform Data**

এই section-এ Power Query-এর tools পাওয়া যায়।

যেমন:

- From Table/Range
    
- From Workbook
    
- From Text/CSV
    
- From Folder
    
- From Web
    
- Get Data
    

---

# 4️⃣ Power Query-এর Basic Workflow

একটি সাধারণ workflow:

```text
CSV / Excel
     ↓
Get Data
     ↓
Power Query Editor
     ↓
Clean
     ↓
Transform
     ↓
Close & Load
     ↓
Excel
```

---

# 5️⃣ CSV Import করা

ধরি তোমার file:

```text
sales.csv
```

এতে আছে:

|Order_ID|Customer|City|Sales|
|---|---|---|--:|
|1001|Rahim|Dhaka|5000|
|1002|Karim|Chittagong|7000|
|1003|Hasan|Dhaka|6000|

### Steps

**Data → Get Data → From File → From Text/CSV**

তারপর CSV select করো।

Preview আসবে।

তারপর:

**Transform Data**

এটা চাপলে Power Query Editor খুলবে।

---

# 6️⃣ Power Query Editor

Power Query Editor হলো যেখানে আমরা data transform করব।

সাধারণভাবে interface-এ থাকবে:

```text
┌──────────────────────────────┐
│ Home Transform Add Column... │
├──────────────────────────────┤
│                              │
│       DATA TABLE             │
│                              │
├──────────────────────────────┤
│ Applied Steps                │
│  Source                      │
│  Promoted Headers            │
│  Changed Type                │
│  ...                         │
└──────────────────────────────┘
```

সবচেয়ে important অংশ:

## Applied Steps

Power Query তোমার করা প্রতিটি transformation step record করে।

---

# 7️⃣ Applied Steps কী?

ধরি তুমি:

1. CSV import করলে
    
2. Header ঠিক করলে
    
3. Salary type number করলে
    
4. Blank rows remove করলে
    
5. Duplicate remove করলে
    

Power Query এগুলো track করবে:

```text
Source
↓
Promoted Headers
↓
Changed Type
↓
Removed Blank Rows
↓
Removed Duplicates
```

🔥 তাই আবার নতুন data এলে একই steps repeat করা যায়।

---

# 8️⃣ Column Data Type

Power Query-তে প্রতিটি column-এর data type ঠিক করা খুব important।

Common types:

|Data Type|Example|
|---|---|
|Text|Rahim|
|Whole Number|25|
|Decimal Number|25.5|
|Date|10/09/2026|
|Date/Time|10/09/2026 10:30|
|True/False|TRUE|

ধরি Salary ভুলভাবে Text:

```text
"50000"
```

এটা number করতে হবে।

Column select:

**Transform → Data Type → Whole Number**

---

# 9️⃣ Remove Columns

ধরি dataset:

|ID|Name|Age|Email|Salary|Password|
|---|---|--:|---|--:|---|

Analysis-এর জন্য Password column দরকার নেই।

Column select:

**Home → Remove Columns**

অথবা:

Right click → Remove

Result:

```text
ID
Name
Age
Email
Salary
```

---

# 🔟 Choose Columns

আরও ভালো approach:

> শুধু প্রয়োজনীয় columns রাখো।

**Home → Choose Columns**

যেমন:

```text
ID
Name
Department
Salary
```

শুধু এগুলো রাখতে পারো।

---

# 1️⃣1️⃣ Remove Rows

Power Query-তে rows remove করার options আছে:

- Remove Top Rows
    
- Remove Bottom Rows
    
- Remove Alternate Rows
    
- Remove Blank Rows
    
- Remove Duplicates
    
- Remove Errors
    

---

# 1️⃣2️⃣ Remove Duplicate Rows

ধরি:

|ID|Name|Salary|
|--:|---|--:|
|101|Rahim|50000|
|102|Karim|40000|
|101|Rahim|50000|

Duplicate record আছে।

Select columns → **Remove Rows → Remove Duplicates**

Result:

|ID|Name|Salary|
|--:|---|--:|
|101|Rahim|50000|
|102|Karim|40000|

---

# 1️⃣3️⃣ Filter Rows

Power Query-তেও Filter আছে।

ধরি শুধু:

```text
Department = IT
```

চাই।

Department column-এর dropdown:

```text
☑ IT
☐ HR
☐ Finance
```

Apply।

---

# 1️⃣4️⃣ Sort Rows

Salary descending:

```text
70000
60000
50000
40000
```

Column select:

**Sort Descending**

---

# 1️⃣5️⃣ Replace Values

এটা data cleaning-এর জন্য খুব useful।

ধরি City:

```text
Dhaka
DHAKA
dhaka
Dhaka City
```

আমরা standardize করতে চাই।

**Transform → Replace Values**

Example:

```text
DHAKA → Dhaka
dhaka → Dhaka
```

---

# 1️⃣6️⃣ Trim Text

এটা Class 10-এর Data Cleaning-এর সাথে related।

ধরি:

```text
"  Rahim  "
```

Power Query:

**Transform → Format → Trim**

Result:

```text
"Rahim"
```

---

# 1️⃣7️⃣ Clean Text

Hidden/non-printing characters থাকলে:

**Transform → Format → Clean**

এটা data cleaning-এ useful।

---

# 1️⃣8️⃣ Upper / Lower / Capitalize

Power Query-তে text transformation করা যায়।

### Uppercase

```text
rahim
```

→

```text
RAHIM
```

### Lowercase

```text
RAHIM
```

→

```text
rahim
```

### Capitalize Each Word

```text
rahim ahmed
```

→

```text
Rahim Ahmed
```

---

# 1️⃣9️⃣ Split Column ⭐

ধরি:

|Full Name|
|---|
|Rahim Ahmed|
|Karim Hasan|
|Hasan Ali|

আমরা Name এবং Last Name আলাদা করতে চাই।

**Transform → Split Column → By Delimiter**

Delimiter:

```text
Space
```

Result:

|First Name|Last Name|
|---|---|
|Rahim|Ahmed|
|Karim|Hasan|
|Hasan|Ali|

---

# 2️⃣0️⃣ Merge Columns

উল্টো কাজও করা যায়।

ধরি:

|First Name|Last Name|
|---|---|
|Rahim|Ahmed|
|Karim|Hasan|

দুই column combine:

**Transform → Merge Columns**

Result:

```text
Rahim Ahmed
Karim Hasan
```

---

# 2️⃣1️⃣ Add Custom Column ⭐⭐⭐

এটা Power Query-এর powerful feature।

ধরি:

|Product|Price|Quantity|
|---|--:|--:|
|Laptop|50000|2|
|Mouse|1000|5|

আমরা Total তৈরি করতে চাই:

```text
Price × Quantity
```

**Add Column → Custom Column**

Formula:

```text
[Price] * [Quantity]
```

Result:

|Product|Price|Quantity|Total|
|---|--:|--:|--:|
|Laptop|50000|2|100000|
|Mouse|1000|5|5000|

এখানে Excel formula-এর বদলে Power Query expression ব্যবহার করছি।

---

# 2️⃣2️⃣ Conditional Column

Power Query-তে IF-এর মতো logic করা যায়।

ধরি:

```text
Salary >= 50000 → High
Salary < 50000 → Normal
```

**Add Column → Conditional Column**

Rule:

```text
If Salary >= 50000
Then "High"
Else "Normal"
```

Result:

|Name|Salary|Category|
|---|--:|---|
|Rahim|60000|High|
|Karim|40000|Normal|

---

# 2️⃣3️⃣ Group By ⭐⭐⭐

এটা খুব important।

ধরি sales data:

|City|Sales|
|---|--:|
|Dhaka|5000|
|Dhaka|7000|
|Chittagong|6000|
|Chittagong|4000|

আমরা চাই:

> City-wise total sales।

Power Query:

**Transform → Group By**

Group by:

```text
City
```

Operation:

```text
Sum
```

Column:

```text
Sales
```

Result:

|City|Total Sales|
|---|--:|
|Dhaka|12000|
|Chittagong|10000|

---

# 2️⃣4️⃣ Group By — Count

ধরি employee data।

আমরা চাই:

> Department-wise employee count।

Group By:

```text
Department
```

Operation:

```text
Count Rows
```

Result:

|Department|Count|
|---|--:|
|IT|40|
|HR|20|
|Finance|30|

---

# 2️⃣5️⃣ Merge Queries ⭐⭐⭐

এটা Database-এর **JOIN** concept-এর মতো।

ধরি:

### Employee

|ID|Name|Dept_ID|
|--:|---|--:|
|101|Rahim|1|
|102|Karim|2|
|103|Hasan|1|

### Department

|Dept_ID|Department|
|--:|---|
|1|IT|
|2|HR|

আমরা দুই table combine করতে চাই।

Power Query:

**Home → Merge Queries**

Join column:

```text
Employee.Dept_ID
       ↓
Department.Dept_ID
```

এটা database-এর:

```sql
JOIN
```

concept-এর সাথে similar।

---

# 2️⃣6️⃣ Merge vs Append ⭐⭐⭐

এগুলো খুব important।

### Merge

দুই table-এর **columns combine** করে।

```text
Table A + Table B
       ↓
JOIN
```

### Append

দুই table-এর **rows combine** করে।

```text
January
+
February
↓
January + February
```

---

# 2️⃣7️⃣ Append Queries

ধরি:

### January

|ID|Sales|
|--:|--:|
|1|5000|
|2|6000|

### February

|ID|Sales|
|--:|--:|
|3|7000|
|4|8000|

Append করলে:

|ID|Sales|
|--:|--:|
|1|5000|
|2|6000|
|3|7000|
|4|8000|

### মনে রাখো:

```text
Merge  → Columns / JOIN
Append → Rows / UNION-like
```

---

# 2️⃣8️⃣ From Folder ⭐⭐⭐

এটাই Power Query-এর automation-এর সবচেয়ে powerful featureগুলোর একটি।

ধরি একটি folder:

```text
Sales/
├── Jan.csv
├── Feb.csv
├── Mar.csv
├── Apr.csv
```

প্রতিটি file-এর structure একই।

Power Query:

**Data → Get Data → From File → From Folder**

Folder select করো।

Power Query files combine করতে পারে।

তারপর:

```text
Jan
Feb
Mar
Apr
 ↓
Combined Dataset
```

🔥 নতুন `May.csv` folder-এ দিলে refresh-এর মাধ্যমে সেটাও pipeline-এ আনা সম্ভব—যদি query structure/logic compatible থাকে।

---

# 2️⃣9️⃣ Refresh — Automation-এর Key

ধরি তুমি আজ Power Query দিয়ে:

```text
CSV
 ↓
Clean
 ↓
Transform
 ↓
Load
```

করলে।

আগামীকাল নতুন data এসেছে।

তখন সব manually আবার করার দরকার নেই।

### Refresh

**Data → Refresh All**

Power Query আবার recorded steps execute করবে।

```text
New Data
   ↓
Refresh
   ↓
Same Transformations
   ↓
Updated Data
```

🔥 এটিই Power Query-এর main advantage।

---

# 3️⃣0️⃣ Close & Load

Transformation শেষ হলে:

**Home → Close & Load**

Data Excel worksheet-এ load হবে।

অথবা:

**Close & Load To...**

দিয়ে choose করতে পারো কোথায় load করবে।

যেমন:

- Table
    
- PivotTable
    
- Data Model
    

---

# 3️⃣1️⃣ Power Query vs Excel Formula

|Excel Formula|Power Query|
|---|---|
|Cell-based calculation|Data transformation|
|Real-time cell result|Refresh-based workflow|
|`SUM`, `IF`, `XLOOKUP`|Transform / Merge / Append|
|Small/medium calculations|Repeated data preparation|
|Cell formulas visible|Applied Steps|
|Manual formula copying|Transformation automation|

দুটো একে অপরের replacement নয়।

**Excel Formula + Power Query** একসাথে ব্যবহার করাই powerful।

---

# 3️⃣2️⃣ Power Query vs PivotTable

এগুলোও গুলিয়ে ফেলবে না।

```text
Power Query
    ↓
Clean + Transform
    ↓
Clean Dataset
    ↓
PivotTable
    ↓
Analysis
    ↓
Chart
    ↓
Dashboard
```

### Power Query

> Data প্রস্তুত করে।

### PivotTable

> Prepared data summarize করে।

---

# 3️⃣3️⃣ Power Query + Your Data Analyst Workflow

তোমার জন্য ideal workflow:

```text
CSV / Excel / Database
          ↓
      Power Query
          ↓
   Data Cleaning
          ↓
   Transformation
          ↓
   Merge / Append
          ↓
      Clean Data
          ↓
     PivotTable
          ↓
       Charts
          ↓
      Dashboard
```

এটা real-world analytics workflow-এর কাছাকাছি।

---

# 3️⃣4️⃣ Power Query এবং Database

তুমি যেহেতু database design শিখছো, এই mappingটা খুব useful:

|Power Query|Database Concept|
|---|---|
|Merge|JOIN|
|Append|UNION-এর মতো row combination|
|Filter|WHERE|
|Choose Columns|SELECT columns|
|Group By|GROUP BY|
|Remove Duplicates|DISTINCT-এর মতো উদ্দেশ্য|
|Rename Column|Alias/renaming|
|Custom Column|Derived expression|
|Refresh|পুনরায় data pipeline চালানো|

Power Query SQL নয়, কিন্তু relational data manipulation-এর অনেক familiar concept আছে।

---

# 3️⃣5️⃣ Power Query-এর সবচেয়ে গুরুত্বপূর্ণ 10 Skills

এই Class থেকে এগুলো ভালোভাবে শিখবে:

```text
1. Import CSV
2. Import Excel
3. Data Types
4. Remove Rows/Columns
5. Filter
6. Replace Values
7. Split/Merge Columns
8. Custom/Conditional Column
9. Group By
10. Merge + Append
```

এর মধ্যে **Merge + Append + Group By + From Folder** বিশেষভাবে important।

---

# ⚠️ Beginner Mistakes

### ❌ 1. Data type ঠিক না করা

Date যদি Text থাকে, date analysis সমস্যা করবে।

---

### ❌ 2. Source data-এর structure বারবার পরিবর্তন করা

From Folder ব্যবহার করলে files-এর column structure compatible রাখা ভালো।

---

### ❌ 3. Merge আর Append গুলিয়ে ফেলা

মনে রাখো:

```text
Merge  = JOIN
Append = Rows combine
```

---

### ❌ 4. Applied Steps না বোঝা

Power Query-এর আসল power হলো:

```text
Step 1
↓
Step 2
↓
Step 3
↓
Step 4
```

প্রতিটি transformation বুঝে তৈরি করবে।

---

### ❌ 5. Manual cleaning চালিয়ে যাওয়া

Power Query শেখার উদ্দেশ্যই হলো:

> **Repeatable transformation তৈরি করা।**

---

# 📌 Class 20 Cheat Sheet

|Task|Power Query|
|---|---|
|CSV import|From Text/CSV|
|Excel import|From Workbook|
|Folder-এর multiple files|From Folder|
|Remove column|Remove Columns|
|Remove duplicate|Remove Duplicates|
|Filter|Filter Rows|
|Sort|Sort|
|Clean spaces|Trim|
|Hidden characters|Clean|
|Split name|Split Column|
|Combine columns|Merge Columns|
|Create formula column|Custom Column|
|IF-like logic|Conditional Column|
|Summary|Group By|
|JOIN|Merge Queries|
|Combine rows|Append Queries|
|Update pipeline|Refresh|

---

# 📝 Class 20 Assignment — Real Data Project 🔥

এবার একটু serious practice।

একটি folder তৈরি করো:

```text
Excel_Practice/
└── Sales/
    ├── January.csv
    ├── February.csv
    └── March.csv
```

প্রতিটি CSV-তে:

|Order_ID|Customer|City|Product|Quantity|Price|
|--:|---|---|---|--:|--:|
|1001|Rahim|Dhaka|Laptop|2|50000|
|1002|Karim|Dhaka|Mouse|5|1000|
|1003|Hasan|Chittagong|Laptop|1|50000|

### Task 1

Power Query দিয়ে CSV import করো।

### Task 2

Data type ঠিক করো।

### Task 3

Customer column Trim করো।

### Task 4

Duplicate records remove করো।

### Task 5

Custom Column তৈরি করো:

```text
Total Sales = Quantity × Price
```

### Task 6

শুধু প্রয়োজনীয় columns রাখো।

### Task 7

City অনুযায়ী total sales বের করতে Group By ব্যবহার করো।

### Task 8 ⭐

January + February + March files **Append** করো।

### Task 9 ⭐⭐

একটি separate Customer table এবং Sales table বানিয়ে **Merge Queries** practice করো।

### Task 10 ⭐⭐⭐

সব monthly CSV একটি folder থেকে **From Folder** দিয়ে combine করো।

তারপর নতুন:

```text
April.csv
```

যোগ করো এবং:

**Refresh All**

দিয়ে দেখো নতুন data pipeline-এ আসে কি না।

---

# 🧪 Class 20 Quiz

**1. Power Query-এর প্রধান কাজ কী?**

A. শুধু chart তৈরি  
B. Data import ও transformation  
C. শুধু formula calculation  
D. শুধু formatting

**2. ETL-এর E কী?**

A. Edit  
B. Extract  
C. Execute  
D. Export

**3. Power Query-তে transformation history কোথায় দেখা যায়?**

A. Formula Bar  
B. Applied Steps  
C. Name Box  
D. Status Bar

**4. দুই table-এর columns combine করতে কোনটি?**

A. Append  
B. Merge  
C. Sort  
D. Group By

**5. দুই table-এর rows combine করতে?**

A. Merge  
B. Append  
C. Filter  
D. Split

**6. City-wise total sales বের করতে কোন feature?**

A. Group By  
B. Split Column  
C. Remove Column  
D. Replace Value

**7. Salary × Quantity-এর নতুন column তৈরি করতে?**

A. Custom Column  
B. Group By  
C. Merge  
D. Append

**8. Power Query-তে JOIN-এর সবচেয়ে কাছাকাছি concept কোনটি?**

A. Append  
B. Merge Queries  
C. Sort  
D. Filter

**9. প্রতিদিন নতুন CSV এলে একই transformation আবার চালাতে কী ব্যবহার করা যায়?**

A. Refresh  
B. Rename  
C. Merge  
D. Delete

**10. একই structure-এর অনেক CSV এক folder থেকে combine করার জন্য সবচেয়ে useful feature কোনটি?**

A. From Folder  
B. From Cell  
C. From Chart  
D. From Formula

---

## 🎯 Excel Mastery Progress

### **20 / 22+ Classes Complete ✅**

তোমার skill progression এখন:

```text
Excel Fundamentals
       ↓
Formulas & Functions
       ↓
Lookup & Conditional Analysis
       ↓
Data Cleaning
       ↓
Tables
       ↓
PivotTable / PivotChart
       ↓
Dynamic Arrays
       ↓
Data Validation
       ↓
Conditional Formatting
       ↓
Professional Visualization
       ↓
🔥 Power Query / ETL
```

**পরের Class 21 হবে — Power Pivot + Data Model + Relationships + DAX Basics**।  
এখানে Excel-এর ভিতরে **database-style multiple tables, relationships এবং DAX calculations** শুরু হবে—তোমার database-design লক্ষ্যটির সাথেও এই অংশটা বিশেষভাবে relevant।


----
# 📘 Excel Mastery — Class 21

## Power Pivot + Data Model + Relationships + DAX Basics

আজকের Class হলো Excel-এর **advanced analytics/database level**।  
বিশেষ করে তুমি যেহেতু **Database Designer + Data Analyst/Data Engineer** হতে চাও, এই Classটা খুব গুরুত্বপূর্ণ।

আজ আমরা শিখব:

1. Power Pivot কী
    
2. Data Model কী
    
3. একাধিক table কেন দরকার
    
4. Primary Key / Foreign Key relationship
    
5. One-to-Many relationship
    
6. Fact & Dimension table
    
7. Power Pivot-এ relationship তৈরি
    
8. Calculated Column
    
9. Measure
    
10. DAX basics
    
11. SUM, COUNTROWS, DISTINCTCOUNT, DIVIDE
    
12. CALCULATE-এর foundation
    
13. Power Pivot + PivotTable
    
14. Real-world project
    

---

# 1️⃣ Power Pivot কী?

সহজভাবে:

> **Power Pivot হলো Excel-এর একটি data modeling এবং advanced calculation engine।**

Normal Excel-এ আমরা অনেক সময় একটা বড় table নিয়ে কাজ করি:

```text
Sales
--------------------------------
Order_ID
Customer
City
Product
Category
Quantity
Price
Date
```

কিন্তু real-world database-এ সাধারণত সব information এক table-এ রাখা হয় না।

বরং:

```text
Customers
Products
Orders
Sales
Date
```

আলাদা table থাকতে পারে।

Power Pivot এই multiple tables-কে **একটি Data Model-এর মধ্যে relationship দিয়ে connect** করতে পারে।

---

# 2️⃣ Normal Excel বনাম Power Pivot

### Normal Excel

```text
One big table
      ↓
Formula
      ↓
PivotTable
```

### Power Pivot

```text
Customers ───┐
             │
Products ────┼──→ Data Model
             │
Sales ───────┤
             │
Date ────────┘
                ↓
              DAX
                ↓
           PivotTable
                ↓
            Dashboard
```

এটাই বড় difference।

---

# 3️⃣ Data Model কী?

**Data Model** হলো একাধিক related table-এর collection।

ধরি আমাদের database:

### Customers

|Customer_ID|Customer_Name|City|
|---|---|---|
|C001|Rahim|Dhaka|
|C002|Karim|Chittagong|
|C003|Hasan|Dhaka|

### Products

|Product_ID|Product_Name|Category|
|---|---|---|
|P001|Laptop|Electronics|
|P002|Mouse|Accessories|
|P003|Keyboard|Accessories|

### Sales

|Order_ID|Customer_ID|Product_ID|Quantity|Sales|
|---|---|---|--:|--:|
|O001|C001|P001|2|100000|
|O002|C002|P002|5|5000|
|O003|C001|P003|3|9000|

এগুলো আলাদা হলেও relationship দিয়ে connected:

```text
Customers
   │
   │ Customer_ID
   ↓
Sales
   ↑
   │ Product_ID
Products
```

এটাই **Data Model**।

---

# 4️⃣ Database-এর সাথে Connection ⭐

তুমি database শিখছো, তাই এই mappingটা খুব ভালোভাবে বুঝো।

|Database|Power Pivot|
|---|---|
|Table|Table|
|Primary Key|Unique key|
|Foreign Key|Related key|
|Relationship|Relationship|
|JOIN|Model relationship|
|Aggregate Query|Measure|
|SQL calculation|DAX calculation|

Power Pivot database-এর replacement নয়, কিন্তু relational modeling-এর অনেক concept একই ধরনের।

---

# 5️⃣ Primary Key কী?

ধরি:

### Customers

|Customer_ID|Name|
|---|---|
|C001|Rahim|
|C002|Karim|
|C003|Hasan|

`Customer_ID` প্রতিটি customer-এর জন্য unique।

তাই:

```text
Customer_ID = Primary Key
```

একই ID ideally duplicate হবে না।

---

# 6️⃣ Foreign Key কী?

Sales table:

|Order_ID|Customer_ID|Sales|
|---|---|--:|
|O001|C001|10000|
|O002|C002|20000|
|O003|C001|15000|

এখানে `Customer_ID` customer table-কে reference করছে।

তাই Sales-এর:

```text
Customer_ID
```

হলো **Foreign Key**।

---

# 7️⃣ Relationship কী?

Customers:

```text
C001
C002
C003
```

Sales:

```text
C001
C002
C001
C003
C001
```

একজন customer অনেক sales করতে পারে।

তাই:

```text
Customers
    1
    │
    │
    ∞
    │
   Sales
```

এটা:

> **One-to-Many Relationship**

---

# 8️⃣ One-to-Many খুব ভালোভাবে বুঝো

একজন customer:

```text
Rahim
```

অনেক order করতে পারে:

```text
Order 1
Order 2
Order 3
Order 4
```

তাই:

```text
Customer → Sales
    1         Many
```

Database design-এ এটা সবচেয়ে common relationship।

---

# 9️⃣ Fact Table কী?

সাধারণভাবে যে table-এ **business transactions/events** থাকে, তাকে Fact Table বলা হয়।

উদাহরণ:

```text
Sales
Orders
Transactions
Payments
```

Sales table:

|Order_ID|Customer_ID|Product_ID|Quantity|Sales|
|---|---|---|--:|--:|
|O001|C001|P001|2|100000|
|O002|C002|P002|5|5000|

এটা **Fact Table** হতে পারে।

---

# 🔟 Dimension Table কী?

Dimension table সাধারণত descriptive information রাখে।

Examples:

```text
Customer
Product
Employee
City
Date
Category
```

Customer:

|Customer_ID|Name|City|
|---|---|---|
|C001|Rahim|Dhaka|
|C002|Karim|Chittagong|

Product:

|Product_ID|Product|Category|
|---|---|---|
|P001|Laptop|Electronics|
|P002|Mouse|Accessories|

---

# 1️⃣1️⃣ Star Schema ⭐⭐⭐

Data analytics-এ খুব important model:

```text
             Customers
                 │
                 │
Products ──── Sales ──── Date
                 │
                 │
              Stores
```

মাঝখানে:

```text
Sales = Fact Table
```

চারপাশে:

```text
Customers
Products
Date
Stores
```

হলো Dimension tables।

এই structure-কে সাধারণভাবে:

> **Star Schema**

বলা হয়।

---

# 1️⃣2️⃣ Power Pivot কোথায়?

Excel-এর version অনুযায়ী interface কিছুটা আলাদা হতে পারে।

সাধারণভাবে:

**Power Pivot → Manage**

যদি Power Pivot tab না দেখা যায়, Excel-এর:

**Options → Add-ins**

থেকে Power Pivot add-in enable করতে হতে পারে।

---

# 1️⃣3️⃣ Table-কে Data Model-এ Add করা

ধরি Excel-এ তিনটি Table আছে:

```text
Customers
Products
Sales
```

প্রতিটি table select করে:

**Power Pivot → Add to Data Model**

করতে পারো।

অথবা data import করার সময়:

**Add this data to the Data Model**

option ব্যবহার করা যায়।

---

# 1️⃣4️⃣ Relationship তৈরি করা ⭐

ধরি:

### Customers

```text
Customer_ID
```

### Sales

```text
Customer_ID
```

Relationship:

```text
Customers[Customer_ID]
          ↓
Sales[Customer_ID]
```

Power Pivot:

**Diagram View**

এ গিয়ে table-এর key column থেকে related column-এ relationship তৈরি করা যায়।

Result:

```text
Customers
Customer_ID
     │
     │
     ↓
Sales
Customer_ID
```

---

# 1️⃣5️⃣ Relationship-এর Rule

সবচেয়ে গুরুত্বপূর্ণ rule:

### Dimension side

Unique values থাকা উচিত।

```text
Customers
C001
C002
C003
```

### Fact side

একই ID বহুবার থাকতে পারে।

```text
Sales
C001
C001
C002
C001
C003
```

তাই:

```text
Customers = 1
Sales     = Many
```

---

# 1️⃣6️⃣ কেন সব Data এক Table-এ রাখব না?

ধরি:

|Customer|City|Product|Category|Sales|
|---|---|---|---|--:|
|Rahim|Dhaka|Laptop|Electronics|100000|
|Rahim|Dhaka|Mouse|Accessories|5000|
|Rahim|Dhaka|Keyboard|Accessories|9000|

এখানে `Rahim` এবং `Dhaka` বারবার repeat হচ্ছে।

অনেক বড় data হলে:

- redundancy বাড়ে
    
- file বড় হয়
    
- update সমস্যা হয়
    
- data consistency সমস্যা হতে পারে
    

তাই:

```text
Customers
Products
Sales
```

আলাদা রাখা ভালো।

---

# 1️⃣7️⃣ Calculated Column কী?

Power Pivot-এ table-এর প্রতিটি row-এর জন্য calculation করতে পারো।

ধরি:

|Quantity|Price|
|--:|--:|
|2|50000|
|3|1000|

Calculated Column:

```text
Total = Quantity × Price
```

DAX:

```text
=[Quantity] * [Price]
```

Result:

|Quantity|Price|Total|
|--:|--:|--:|
|2|50000|100000|
|3|1000|3000|

---

# 1️⃣8️⃣ Calculated Column বনাম Measure ⭐⭐⭐

এটা খুব গুরুত্বপূর্ণ।

### Calculated Column

প্রতিটি row-এর জন্য calculation।

```text
Quantity × Price
```

### Measure

পুরো dataset-এর context অনুযায়ী calculation।

যেমন:

```text
Total Sales
Average Sales
Total Orders
Profit
```

সহজভাবে:

```text
Calculated Column → Row-level
Measure           → Aggregation/Analysis
```

---

# 1️⃣9️⃣ Measure কী?

ধরি Sales table:

|Sales|
|--:|
|5000|
|7000|
|3000|

আমরা Total Sales চাই।

Measure:

```text
Total Sales = SUM(Sales[Sales])
```

Result:

```text
15000
```

---

# 2️⃣0️⃣ DAX কী?

**DAX = Data Analysis Expressions**

Power Pivot / Power BI-তে calculations করার জন্য DAX ব্যবহার করা হয়।

এটা Excel formula-এর মতো দেখতে হলেও conceptually বেশি powerful।

Example:

```text
=SUM(Sales[Sales])
```

---

# 2️⃣1️⃣ DAX SUM

সব sales যোগ:

```text
Total Sales =
SUM(Sales[Sales])
```

---

# 2️⃣2️⃣ COUNTROWS

Table-এ কত row আছে:

```text
Total Rows =
COUNTROWS(Sales)
```

যদি:

```text
1000 rows
```

থাকে:

```text
Total Rows = 1000
```

---

# 2️⃣3️⃣ DISTINCTCOUNT ⭐

Unique customer count:

```text
Unique Customers =
DISTINCTCOUNT(Sales[Customer_ID])
```

ধরি:

```text
C001
C001
C002
C003
C001
```

Total rows:

```text
5
```

Unique customers:

```text
3
```

---

# 2️⃣4️⃣ AVERAGE

Average sales:

```text
Average Sales =
AVERAGE(Sales[Sales])
```

---

# 2️⃣5️⃣ MIN এবং MAX

```text
Minimum Sale =
MIN(Sales[Sales])
```

```text
Maximum Sale =
MAX(Sales[Sales])
```

---

# 2️⃣6️⃣ DIVIDE ⭐

ধরি:

```text
Profit = 20000
Sales = 100000
```

Profit margin:

```text
20%
```

DAX:

```text
Profit Margin =
DIVIDE(
    [Total Profit],
    [Total Sales],
    0
)
```

`DIVIDE()` ব্যবহার করা ভালো কারণ denominator 0 হলে error handling করা যায়।

---

# 2️⃣7️⃣ CALCULATE — DAX-এর Superpower ⭐⭐⭐

এটা আজ শুধু foundation level-এ বুঝব।

ধরি:

```text
Total Sales =
SUM(Sales[Sales])
```

এখন আমরা চাই:

> শুধু IT category-এর Sales।

Conceptually:

```text
IT Sales =
CALCULATE(
    [Total Sales],
    Products[Category] = "IT"
)
```

`CALCULATE()` মূলত calculation-এর **filter context পরিবর্তন** করতে সাহায্য করে।

এটা DAX-এর সবচেয়ে important functions-এর একটি।

---

# 2️⃣8️⃣ Filter Context কী?

ধরি total sales:

```text
100,000
```

এখন PivotTable-এ:

```text
City = Dhaka
```

filter দিলে DAX measure শুধু Dhaka-এর data-এর উপর calculate হতে পারে।

অর্থাৎ:

```text
All Sales
   ↓
Filter: Dhaka
   ↓
Dhaka Sales
```

এটাই সহজভাবে **filter context** বোঝার শুরু।

---

# 2️⃣9️⃣ Power Pivot + PivotTable ⭐⭐⭐

Data Model তৈরি করার পরে:

**Insert → PivotTable → From Data Model**

এরপর multiple table-এর fields ব্যবহার করতে পারো।

ধরি:

Rows:

```text
Customers[City]
```

Values:

```text
[Total Sales]
```

Result:

|City|Total Sales|
|---|--:|
|Dhaka|150000|
|Chittagong|90000|
|Sylhet|50000|

Sales table-এ City না থাকলেও সমস্যা নেই।

কারণ:

```text
Customers
   ↓ relationship
Sales
```

এর মাধ্যমে information model-এর মধ্যে connected।

🔥 এটাই Data Model-এর power।

---

# 3️⃣0️⃣ Real Example

আমাদের তিনটি table:

### Customers

|Customer_ID|Customer|City|
|---|---|---|
|C001|Rahim|Dhaka|
|C002|Karim|Chittagong|
|C003|Hasan|Dhaka|

### Products

|Product_ID|Product|Category|
|---|---|---|
|P001|Laptop|Electronics|
|P002|Mouse|Accessories|
|P003|Keyboard|Accessories|

### Sales

|Order_ID|Customer_ID|Product_ID|Quantity|Sales|
|---|---|---|--:|--:|
|O001|C001|P001|2|100000|
|O002|C002|P002|5|5000|
|O003|C001|P003|3|9000|
|O004|C003|P001|1|50000|

Relationships:

```text
Customers[Customer_ID]
          │
          │ 1 : Many
          ↓
Sales[Customer_ID]


Products[Product_ID]
          │
          │ 1 : Many
          ↓
Sales[Product_ID]
```

---

# 3️⃣1️⃣ এরপর কী প্রশ্ন করা সম্ভব?

এই Data Model দিয়ে আমরা প্রশ্ন করতে পারি:

### Total Sales

```text
SUM(Sales[Sales])
```

### Total Orders

```text
COUNTROWS(Sales)
```

### Unique Customers

```text
DISTINCTCOUNT(Sales[Customer_ID])
```

### Average Sales

```text
AVERAGE(Sales[Sales])
```

### City-wise Sales

```text
Customers[City]
        +
[Total Sales]
```

### Product-wise Sales

```text
Products[Product]
        +
[Total Sales]
```

🔥 এখানে একই `[Total Sales]` measure বিভিন্ন dimension দিয়ে analyze করা যায়।

---

# 3️⃣2️⃣ Measure কেন এত Powerful?

একটি measure:

```text
Total Sales =
SUM(Sales[Sales])
```

একবার তৈরি করলেই PivotTable-এ:

```text
City
Product
Customer
Category
Month
```

যে context-এ বসাবে, সেই অনুযায়ী result calculate হতে পারে।

এটাই measure-এর power।

---

# 3️⃣3️⃣ Important DAX Cheat Sheet

|Requirement|DAX|
|---|---|
|Total|`SUM()`|
|Average|`AVERAGE()`|
|Row count|`COUNTROWS()`|
|Unique count|`DISTINCTCOUNT()`|
|Minimum|`MIN()`|
|Maximum|`MAX()`|
|Safe division|`DIVIDE()`|
|Change filter context|`CALCULATE()`|

---

# 3️⃣4️⃣ Excel Formula বনাম DAX

|Excel|DAX|
|---|---|
|`SUM(A2:A100)`|`SUM(Sales[Sales])`|
|Cell-oriented|Model-oriented|
|Worksheet-based|Table/relationship-based|
|Row formula common|Measures very important|
|`$A$1` references|Filter context|
|Normal spreadsheet|Data Model analytics|

---

# 3️⃣5️⃣ Power Query + Power Pivot 🔥

এই দুইটা একসাথে খুব powerful।

```text
Raw CSV / Excel
       ↓
  Power Query
       ↓
Cleaning
       ↓
Transformation
       ↓
Multiple Tables
       ↓
  Power Pivot
       ↓
Data Model
       ↓
Relationships
       ↓
    DAX
       ↓
   Measures
       ↓
 PivotTable
       ↓
 Dashboard
```

তুমি এখন প্রায় **Excel-based BI workflow**-এর core অংশে চলে এসেছো।

---

# ⚠️ Beginner Mistakes

### ❌ 1. Fact এবং Dimension উল্টো করা

সাধারণ pattern:

```text
Fact → transactions
Dimension → descriptions
```

---

### ❌ 2. Relationship-এর দুই পাশে duplicate key রাখা

Dimension side-এর key সাধারণত unique হওয়া উচিত।

---

### ❌ 3. Calculated Column আর Measure গুলিয়ে ফেলা

মনে রাখো:

```text
Column → প্রতিটি row
Measure → analysis calculation
```

---

### ❌ 4. সব calculation calculated column দিয়ে করা

Analytics-এর জন্য অনেক ক্ষেত্রে measure বেশি appropriate।

---

### ❌ 5. `CALCULATE()` মুখস্থ করা

শুধু syntax মুখস্থ করলে হবে না।

প্রথমে বুঝবে:

```text
Calculation
+
Filter Context
=
CALCULATE
```

---

# 🧠 Class 21 Mental Model

এই diagramটা মনে রাখো:

```text
             DIMENSION
          ┌─────────────┐
          │ Customers   │
          └──────┬──────┘
                 │
                 │ 1 : Many
                 ↓
          ┌─────────────┐
          │    SALES    │
          │ FACT TABLE  │
          └──────┬──────┘
                 ↑
                 │ 1 : Many
          ┌──────┴──────┐
          │  Products   │
          └─────────────┘

                 ↓
           Power Pivot
                 ↓
             DAX
                 ↓
             Measures
                 ↓
           PivotTable
                 ↓
            Dashboard
```

---

# 📝 Class 21 Assignment — Mini Business Data Model

এবার একটা **real-world mini project** করবে।

## Table 1 — Customers

কমপক্ষে 10 customers:

```text
Customer_ID
Customer_Name
City
```

---

## Table 2 — Products

কমপক্ষে 10 products:

```text
Product_ID
Product_Name
Category
Price
```

---

## Table 3 — Sales

কমপক্ষে 30 transactions:

```text
Order_ID
Customer_ID
Product_ID
Quantity
Sales
Order_Date
```

---

## Task 1

তিনটি Excel Table তৈরি করো।

```text
Customers
Products
Sales
```

## Task 2

সবগুলো Data Model-এ add করো।

## Task 3

Relationship তৈরি করো:

```text
Customers[Customer_ID]
        ↓
Sales[Customer_ID]
```

এবং:

```text
Products[Product_ID]
        ↓
Sales[Product_ID]
```

## Task 4

একটি calculated column তৈরি করো:

```text
Revenue = Quantity × Price
```

## Task 5

এই measures তৈরি করো:

```text
Total Revenue
Total Orders
Average Revenue
Unique Customers
Maximum Revenue
Minimum Revenue
```

## Task 6 ⭐

PivotTable দিয়ে বের করো:

```text
City-wise Revenue
```

## Task 7 ⭐

বের করো:

```text
Product-wise Revenue
```

## Task 8 ⭐⭐

বের করো:

```text
Category-wise Revenue
```

## Task 9 ⭐⭐⭐

একটি KPI section বানাও:

```text
Total Revenue
Total Orders
Unique Customers
Average Order Value
```

---

# 🧪 Class 21 Quiz

**1. Power Pivot-এর প্রধান উদ্দেশ্য কী?**

A. শুধু formatting  
B. Data modeling ও advanced analysis  
C. শুধু typing  
D. শুধু chart

**2. Data Model কী?**

A. একটি chart  
B. Related multiple tables-এর collection  
C. একটি formula  
D. একটি worksheet

**3. Customer table-এর unique Customer_ID কী হতে পারে?**

A. Foreign Key  
B. Primary Key  
C. Measure  
D. DAX

**4. Sales table-এর Customer_ID সাধারণত কী?**

A. Primary Key  
B. Foreign Key  
C. Measure  
D. Dimension

**5. একজন customer অনেক order করলে relationship কী?**

A. One-to-One  
B. One-to-Many  
C. Many-to-One only  
D. None

**6. Sales সাধারণত কোন ধরনের table?**

A. Dimension  
B. Fact  
C. Lookup only  
D. Calendar only

**7. Product/Customer table সাধারণত কী?**

A. Fact  
B. Dimension  
C. Measure  
D. Formula

**8. DAX-এর full form কী?**

A. Data Analysis Expressions  
B. Data Advanced Excel  
C. Database Analysis Extension  
D. Dynamic Analytics Excel

**9. Unique customer count-এর জন্য কোন DAX function?**

A. COUNTROWS  
B. SUM  
C. DISTINCTCOUNT  
D. MAX

**10. Filter context পরিবর্তনের জন্য সবচেয়ে গুরুত্বপূর্ণ DAX function কোনটি?**

A. SUM  
B. CALCULATE  
C. COUNT  
D. MIN

---

## 🎯 তোমার Excel Mastery Progress

**21 / 22+ Classes Complete ✅**

এখন তোমার skill chain:

```text
Excel Basics
   ↓
Formulas & Functions
   ↓
Advanced Functions
   ↓
Data Cleaning
   ↓
Tables
   ↓
PivotTable
   ↓
Charts
   ↓
Dynamic Arrays
   ↓
Validation
   ↓
Conditional Formatting
   ↓
Power Query
   ↓
🔥 Power Pivot
   ↓
🔥 Data Model
   ↓
🔥 Relationships
   ↓
🔥 DAX
```

### পরের ধাপ — **Class 22: Advanced DAX + Time Intelligence + Professional Dashboard**

সেখানে আমরা `CALCULATE`, `FILTER`, `ALL`, `SUMX`, `RELATED`, `DATE`, `TOTALYTD`, Month-over-Month growth, Year-over-Year growth এবং **একটি complete business dashboard** বানানোর দিকে যাব।


----
# 📘 Excel Mastery — Class 22

## Advanced DAX + Time Intelligence + Professional Dashboard

🎯 **আজকের Class = Excel Mastery-এর সবচেয়ে advanced অংশগুলোর একটি।**

আজ আমরা আগের Class-এর basic DAX থেকে উঠে যাব **real BI analysis**-এ।

আজকের flow:

```text
Data
 ↓
Power Query
 ↓
Data Model
 ↓
Relationships
 ↓
DAX Measures
 ↓
Time Intelligence
 ↓
KPI
 ↓
Dashboard
 ↓
Business Insights
```

---

# 1️⃣ প্রথমে DAX-এর ২টা গুরুত্বপূর্ণ Concept

Advanced DAX শেখার আগে এই দুইটা বুঝতে হবে:

### Row Context

একটি row-এর data নিয়ে calculation।

যেমন:

```text
Quantity × Price
```

প্রতিটি row-এর জন্য।

---

### Filter Context

কোন data বর্তমানে filter-এর মধ্যে আছে।

যেমন PivotTable-এ:

```text
City = Dhaka
```

তাহলে measure Dhaka-এর data অনুযায়ী calculate হতে পারে।

সহজভাবে:

```text
Row Context   → Current row
Filter Context → Current filtered data
```

---

# 2️⃣ CALCULATE() ⭐⭐⭐

এটাই Advanced DAX-এর সবচেয়ে গুরুত্বপূর্ণ function।

Basic:

```text
Total Sales =
SUM(Sales[Sales])
```

এখন শুধু Dhaka-এর Sales:

```text
Dhaka Sales =
CALCULATE(
    [Total Sales],
    Customers[City] = "Dhaka"
)
```

মানে:

```text
Total Sales
     ↓
Filter = Dhaka
     ↓
Dhaka Sales
```

### Mental Model

> **CALCULATE = calculation + modified filter context**

---

# 3️⃣ CALCULATE-এর Dynamic Example

ধরি PivotTable-এ City আছে:

```text
Dhaka
Chittagong
Sylhet
```

এবং measure:

```text
Total Sales =
SUM(Sales[Sales])
```

PivotTable নিজেই প্রতিটি City-এর filter context তৈরি করবে।

তাই:

```text
City          Total Sales
-------------------------
Dhaka          150,000
Chittagong      90,000
Sylhet          50,000
```

একই measure বিভিন্ন context-এ different result দেয়।

---

# 4️⃣ FILTER() ⭐⭐⭐

`FILTER()` একটি table/filter condition তৈরি করতে ব্যবহার করা যায়।

Example:

```text
High Value Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        Sales,
        Sales[Sales] > 50000
    )
)
```

Concept:

```text
Sales
 ↓
Sales > 50,000
 ↓
Filtered Sales
 ↓
Total
```

⚠️ `FILTER()` advanced DAX-এ খুব powerful, কিন্তু শুরুতে অপ্রয়োজনীয়ভাবে সব জায়গায় ব্যবহার করবে না।

---

# 5️⃣ ALL() ⭐⭐⭐

`ALL()` filter remove করার কাজে ব্যবহার হয়।

ধরি PivotTable:

```text
City       Sales
----------------
Dhaka      150K
Chittagong 90K
Sylhet      50K
```

আমরা চাই:

> প্রতিটি city-এর sales / total company sales

Measure:

```text
Sales % of Total =
DIVIDE(
    [Total Sales],
    CALCULATE(
        [Total Sales],
        ALL(Customers[City])
    )
)
```

এখানে:

```text
ALL(Customers[City])
```

City filter remove করে।

---

# 6️⃣ Sales % of Total

ধরি:

```text
Total Company Sales = 290,000
```

Dhaka:

```text
150,000
```

তাহলে:

```text
150000 / 290000
≈ 51.72%
```

DAX:

```text
Sales % of Total =
DIVIDE(
    [Total Sales],
    CALCULATE(
        [Total Sales],
        ALL(Customers[City])
    )
)
```

Result:

|City|Sales|% Total|
|---|--:|--:|
|Dhaka|150,000|51.72%|
|Chittagong|90,000|31.03%|
|Sylhet|50,000|17.24%|

---

# 7️⃣ SUMX() ⭐⭐⭐

এখন আসি iterator-এ।

ধরি Sales table:

|Quantity|Price|
|--:|--:|
|2|50000|
|3|1000|
|5|500|

আমরা চাই:

```text
Quantity × Price
```

প্রতিটি row-তে calculate করে সব যোগ করতে।

DAX:

```text
Total Revenue =
SUMX(
    Sales,
    Sales[Quantity] * Sales[Price]
)
```

এটা conceptually:

```text
Row 1 → 2 × 50000
Row 2 → 3 × 1000
Row 3 → 5 × 500

       ↓
      SUM
```

---

# 8️⃣ SUM vs SUMX

এটা খুব important।

### SUM

একটি column-এর existing values যোগ করে:

```text
SUM(Sales[Revenue])
```

### SUMX

প্রতিটি row-তে expression calculate করে তারপর যোগ করে:

```text
SUMX(
    Sales,
    Sales[Quantity] * Sales[Price]
)
```

মনে রাখো:

```text
SUM  → Column aggregate
SUMX → Row-by-row expression + aggregate
```

---

# 9️⃣ RELATED() ⭐⭐⭐

Relationship থাকলে অন্য table থেকে related value আনতে `RELATED()` ব্যবহার করা যায়।

ধরি:

### Products

|Product_ID|Category|
|---|---|
|P001|Electronics|
|P002|Accessories|

Sales table-এ:

```text
Product_ID
```

আছে।

Relationship তৈরি করা আছে।

Calculated Column:

```text
Category =
RELATED(Products[Category])
```

তাহলে Sales table-এ category পাওয়া যাবে।

---

# 🔟 Time Intelligence কী?

এখন আসি আজকের সবচেয়ে important section-এ।

Business analysis-এ শুধু:

```text
Sales = 100,000
```

জানলেই হয় না।

আমরা জানতে চাই:

- গত মাসের sales কত?
    
- এই মাসে কত growth?
    
- গত বছরের একই সময়ে কত ছিল?
    
- Year-to-Date sales কত?
    
- Target-এর কত % achieve হয়েছে?
    

এগুলো হলো **Time Intelligence**।

---

# 1️⃣1️⃣ Date Table কেন দরকার?

Time Intelligence-এর জন্য একটি proper Date Table ব্যবহার করা best practice।

Example:

|Date|Year|Month|Month Number|Quarter|
|---|--:|---|--:|---|
|01-Jan-2026|2026|January|1|Q1|
|02-Jan-2026|2026|January|1|Q1|
|...|...|...|...|...|

Date table:

```text
DateTable
```

এবং Sales:

```text
Sales[Order_Date]
```

Relationship:

```text
DateTable[Date]
       │
       │ 1 : Many
       ↓
Sales[Order_Date]
```

---

# 1️⃣2️⃣ Date Table তৈরি

Power Pivot/DAX-এ basic date table তৈরি করা যায়:

```text
DateTable =
CALENDAR(
    DATE(2026,1,1),
    DATE(2026,12,31)
)
```

এতে:

```text
01-Jan-2026
02-Jan-2026
03-Jan-2026
...
31-Dec-2026
```

তৈরি হবে।

তারপর calculated columns:

```text
Year =
YEAR(DateTable[Date])
```

```text
Month =
FORMAT(DateTable[Date], "MMMM")
```

```text
Month Number =
MONTH(DateTable[Date])
```

```text
Quarter =
"Q" & FORMAT(DateTable[Date], "Q")
```

---

# 1️⃣3️⃣ Month Sort Problem ⚠️

যদি Month text হয়:

```text
April
August
December
February
...
```

alphabetical order হতে পারে।

তাই:

```text
Month Number
```

ব্যবহার করে Month-কে sort করতে হবে।

```text
January   → 1
February  → 2
March     → 3
...
```

এটা dashboard-এর জন্য খুব important।

---

# 1️⃣4️⃣ Total Sales Measure

প্রথমে basic measure:

```text
Total Sales =
SUM(Sales[Sales])
```

---

# 1️⃣5️⃣ YTD — Year to Date ⭐⭐⭐

YTD মানে:

> বছরের শুরু থেকে বর্তমান date পর্যন্ত total।

DAX:

```text
Sales YTD =
TOTALYTD(
    [Total Sales],
    DateTable[Date]
)
```

ধরি:

January:

```text
100K
```

February:

```text
150K
```

March:

```text
120K
```

তাহলে March YTD:

```text
100K + 150K + 120K
= 370K
```

---

# 1️⃣6️⃣ Previous Year Sales

গত বছরের corresponding period-এর sales বের করতে:

```text
Sales LY =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(DateTable[Date])
)
```

LY = Last Year.

---

# 1️⃣7️⃣ YoY Growth ⭐⭐⭐

YoY = **Year over Year**

ধরি:

```text
Current Year = 120,000
Last Year    = 100,000
```

Growth:

```text
(120000 - 100000) / 100000
= 20%
```

DAX:

```text
YoY Growth % =
DIVIDE(
    [Total Sales] - [Sales LY],
    [Sales LY],
    0
)
```

---

# 1️⃣8️⃣ YoY Growth-এর Meaning

যদি:

```text
+20%
```

→ Sales 20% বেড়েছে।

যদি:

```text
-10%
```

→ Sales 10% কমেছে।

Business dashboard-এ এটা খুব common KPI।

---

# 1️⃣9️⃣ Previous Month Analysis

Previous month analysis-এর জন্য time-intelligence functions ব্যবহার করা যায়।

Concept:

```text
Current Month
     ↓
Previous Month
     ↓
Compare
```

একটি common DAX pattern:

```text
Sales Previous Month =
CALCULATE(
    [Total Sales],
    DATEADD(
        DateTable[Date],
        -1,
        MONTH
    )
)
```

---

# 2️⃣0️⃣ MoM Growth ⭐⭐⭐

MoM = Month over Month.

ধরি:

```text
January = 100K
February = 120K
```

Growth:

```text
(120 - 100) / 100
= 20%
```

DAX:

```text
MoM Growth % =
DIVIDE(
    [Total Sales] - [Sales Previous Month],
    [Sales Previous Month],
    0
)
```

---

# 2️⃣1️⃣ Target vs Actual

Business dashboard-এ খুব common।

ধরি:

```text
Target = 500,000
Actual = 450,000
```

Achievement:

```text
450000 / 500000
= 90%
```

DAX:

```text
Achievement % =
DIVIDE(
    [Total Sales],
    [Total Target],
    0
)
```

---

# 2️⃣2️⃣ Variance

Actual - Target:

```text
Variance =
[Total Sales] - [Total Target]
```

যদি:

```text
Actual = 450K
Target = 500K
```

তাহলে:

```text
Variance = -50K
```

অর্থাৎ target-এর নিচে।

---

# 2️⃣3️⃣ Professional KPI Cards

Dashboard-এর top section-এ সাধারণত KPI:

```text
┌─────────────┐
│ Total Sales │
│   450,000   │
└─────────────┘

┌─────────────┐
│ Total Orders│
│    1,250    │
└─────────────┘

┌─────────────┐
│ Customers   │
│      430    │
└─────────────┘

┌─────────────┐
│ YoY Growth  │
│    +18.5%   │
└─────────────┘
```

---

# 2️⃣4️⃣ Dashboard Architecture ⭐⭐⭐

একটি professional dashboard এমন হতে পারে:

```text
┌───────────────────────────────────────────┐
│           SALES DASHBOARD                 │
├──────────┬──────────┬──────────┬──────────┤
│ Revenue  │ Orders   │ Customers│ YoY %    │
├──────────┴──────────┴──────────┴──────────┤
│                                           │
│       Monthly Sales Trend                 │
│              LINE CHART                   │
│                                           │
├──────────────────────┬────────────────────┤
│ City Sales           │ Category Sales     │
│ BAR CHART             │ COLUMN CHART       │
├──────────────────────┴────────────────────┤
│ Product Performance / Target vs Actual    │
└───────────────────────────────────────────┘
```

---

# 2️⃣5️⃣ Dashboard-এ কী রাখবে?

### KPI

- Total Sales
    
- Total Orders
    
- Unique Customers
    
- Profit
    
- Profit Margin
    
- YoY Growth
    

### Charts

- Monthly Sales → Line
    
- City Sales → Bar
    
- Category Sales → Column
    
- Actual vs Target → Combo/Column
    
- Product performance → Bar
    

### Filters/Slicers

- Year
    
- Month
    
- City
    
- Category
    
- Product
    

---

# 2️⃣6️⃣ Slicer কী?

Slicer হলো visual filter।

ধরি dashboard-এ:

```text
City

☐ Dhaka
☐ Chittagong
☐ Sylhet
```

Dhaka click করলে dashboard-এর connected PivotTables/charts সেই filter অনুযায়ী update করতে পারে।

এটা dashboard-কে interactive করে।

---

# 2️⃣7️⃣ Timeline

Date filtering-এর জন্য Timeline ব্যবহার করা যায়।

যেমন:

```text
2026
Jan ─ Feb ─ Mar ─ Apr ─ May ─ Jun
```

User date period select করলে report update হতে পারে।

---

# 2️⃣8️⃣ Dashboard-এর Golden Rule ⭐

Dashboard বানানোর আগে প্রশ্ন করো:

> **এই chart দেখে business user কী decision নেবে?**

শুধু সুন্দর chart বানানো dashboard নয়।

Example:

❌ `Sales Chart`

ভালো:

✅ `Monthly Sales Trend`

আরও ভালো:

✅ `Monthly Sales vs Target`

কারণ এতে business decision নেওয়া সহজ।

---

# 2️⃣9️⃣ Professional Dashboard Workflow

তোমার পুরো Excel workflow এখন:

```text
                    RAW DATA
                       ↓
                ┌─────────────┐
                │ Power Query │
                └──────┬──────┘
                       ↓
               CLEAN DATA
                       ↓
                DATA MODEL
                       ↓
             ┌─────────┴─────────┐
             ↓                   ↓
        Dimensions            Fact
             │                   │
             └───────┬───────────┘
                     ↓
               Relationships
                     ↓
                   DAX
                     ↓
                 Measures
                     ↓
                PivotTables
                     ↓
                   Charts
                     ↓
                 Slicers
                     ↓
               DASHBOARD
                     ↓
            BUSINESS INSIGHTS
```

🔥 এই workflowটা মনে রাখবে।

---

# 3️⃣0️⃣ Complete DAX Measure Set

একটি sales dashboard-এর জন্য আমরা এমন measures রাখতে পারি:

### Total Sales

```text
Total Sales =
SUM(Sales[Sales])
```

### Total Orders

```text
Total Orders =
COUNTROWS(Sales)
```

### Unique Customers

```text
Unique Customers =
DISTINCTCOUNT(Sales[Customer_ID])
```

### Average Sales

```text
Average Sales =
AVERAGE(Sales[Sales])
```

### Sales YTD

```text
Sales YTD =
TOTALYTD(
    [Total Sales],
    DateTable[Date]
)
```

### Sales Last Year

```text
Sales LY =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(DateTable[Date])
)
```

### YoY Growth

```text
YoY Growth % =
DIVIDE(
    [Total Sales] - [Sales LY],
    [Sales LY],
    0
)
```

### Previous Month

```text
Sales Previous Month =
CALCULATE(
    [Total Sales],
    DATEADD(
        DateTable[Date],
        -1,
        MONTH
    )
)
```

### MoM Growth

```text
MoM Growth % =
DIVIDE(
    [Total Sales] - [Sales Previous Month],
    [Sales Previous Month],
    0
)
```

---

# 3️⃣1️⃣ Advanced DAX Cheat Sheet

|Function|Main Purpose|
|---|---|
|`SUM()`|Total|
|`AVERAGE()`|Average|
|`COUNTROWS()`|Row count|
|`DISTINCTCOUNT()`|Unique count|
|`DIVIDE()`|Safe division|
|`CALCULATE()`|Modify filter context|
|`FILTER()`|Filter table|
|`ALL()`|Remove filters|
|`SUMX()`|Row-by-row calculation|
|`RELATED()`|Get related value|
|`TOTALYTD()`|Year-to-date|
|`SAMEPERIODLASTYEAR()`|Previous-year comparison|
|`DATEADD()`|Shift date period|

---

# 3️⃣2️⃣ খুব গুরুত্বপূর্ণ Difference

### Power Query

```text
Data Preparation
```

### Power Pivot

```text
Data Modeling
```

### DAX

```text
Analysis / Calculation
```

### PivotTable

```text
Summarization
```

### Dashboard

```text
Visualization + Decision Support
```

এগুলো একসাথে গুলিয়ে ফেলবে না।

---

# ⚠️ Common Beginner Mistakes

### ❌ 1. Date Table ছাড়া Time Intelligence শুরু করা

Proper date dimension ব্যবহার করাই ভালো।

---

### ❌ 2. Month name দিয়ে sorting না করা

January → February → March...

chronological order নিশ্চিত করো।

---

### ❌ 3. সব জায়গায় `FILTER()` ব্যবহার করা

Simple filter condition হলে `CALCULATE()`-এর direct filter অনেক সময় যথেষ্ট।

---

### ❌ 4. `SUM()` এবং `SUMX()` গুলিয়ে ফেলা

```text
SUM  → existing column
SUMX → row expression
```

---

### ❌ 5. Measure বনাম Calculated Column ভুল করা

```text
Calculated Column → row-level
Measure           → dynamic analysis
```

---

### ❌ 6. Dashboard-এ অতিরিক্ত chart

একটি dashboard-এ 15টা chart রাখলে সেটা professional হয় না।

> **Less but meaningful.**

---

# 📝 Class 22 Final Project 🔥🔥🔥

এটা হবে তোমার **Excel Mastery Capstone Project**।

## Dataset

তিনটি table:

### Customers

```text
Customer_ID
Customer_Name
City
```

### Products

```text
Product_ID
Product_Name
Category
Price
```

### Sales

```text
Order_ID
Customer_ID
Product_ID
Order_Date
Quantity
Sales
```

কমপক্ষে:

```text
Customers → 20
Products  → 20
Sales     → 200+
```

records তৈরি করো।

---

## Step 1 — Power Query

Data clean:

```text
✓ Remove duplicates
✓ Trim
✓ Correct data types
✓ Remove unnecessary columns
✓ Handle blanks
```

---

## Step 2 — Data Model

Relationships:

```text
Customers
     │
     ↓
   Sales
     ↑
     │
Products
```

Date Table:

```text
DateTable
     │
     ↓
   Sales
```

---

## Step 3 — DAX Measures

Create:

```text
Total Sales
Total Orders
Unique Customers
Average Sales
Sales YTD
Sales LY
YoY Growth %
Previous Month Sales
MoM Growth %
```

---

## Step 4 — PivotTables

Create:

### Pivot 1

```text
Monthly Sales
```

### Pivot 2

```text
City-wise Sales
```

### Pivot 3

```text
Category-wise Sales
```

### Pivot 4

```text
Product-wise Sales
```

---

## Step 5 — Dashboard

Create:

```text
┌─────────────────────────────────────────────┐
│              SALES DASHBOARD                │
├───────────┬───────────┬───────────┬─────────┤
│ Sales     │ Orders    │ Customers │ YoY %  │
├───────────┴───────────┴───────────┴─────────┤
│                                             │
│          Monthly Sales Trend                │
│                                             │
├─────────────────────┬───────────────────────┤
│ City Performance    │ Category Performance  │
├─────────────────────┴───────────────────────┤
│              Product Performance            │
└─────────────────────────────────────────────┘
```

Add:

```text
✓ Slicer: City
✓ Slicer: Category
✓ Slicer: Year
✓ Timeline: Date
```

---

# 🧪 Class 22 Quiz

**1. `CALCULATE()` মূলত কী পরিবর্তন করতে সাহায্য করে?**

A. Cell size  
B. Filter context  
C. Font  
D. Worksheet

**2. `SUMX()` কী করে?**

A. শুধু column যোগ করে  
B. Row-by-row expression calculate করে aggregate করে  
C. Chart বানায়  
D. Filter remove করে

**3. `ALL()` সাধারণত কী কাজে ব্যবহৃত হয়?**

A. Data delete  
B. Filter remove  
C. Sorting  
D. Formatting

**4. `DISTINCTCOUNT()` কী দেয়?**

A. সব row  
B. Average  
C. Unique values-এর count  
D. Maximum

**5. YTD-এর অর্থ কী?**

A. Year Total Data  
B. Year to Date  
C. Year Time Difference  
D. Year Table Data

**6. গত বছরের একই period-এর data বের করতে কোন function useful?**

A. SUMX  
B. SAMEPERIODLASTYEAR  
C. RELATED  
D. COUNTROWS

**7. YoY-এর অর্থ কী?**

A. Year over Year  
B. Yield over Year  
C. Year of Yield  
D. Year Order Yield

**8. `DIVIDE()` কেন ব্যবহার করা ভালো?**

A. Sorting-এর জন্য  
B. Safe division-এর জন্য  
C. Duplicate remove-এর জন্য  
D. Date তৈরির জন্য

**9. Month chronological order ঠিক রাখতে কী useful?**

A. Month Number  
B. Customer ID  
C. Sales ID  
D. Price

**10. Dashboard-এর main purpose কী?**

A. শুধু সুন্দর দেখানো  
B. Business insights ও decision support  
C. Data entry  
D. File size বাড়ানো

---

# 🏆 তোমার Excel Mastery এখন কোথায়?

**22 / 22+ Classes Complete 🎉**

তুমি এখন শুধু basic Excel user নও।

তোমার learning chain:

```text
Excel Fundamentals
        ↓
Formulas
        ↓
Functions
        ↓
Logical Analysis
        ↓
Text & Date
        ↓
Lookup
        ↓
Conditional Analysis
        ↓
Data Cleaning
        ↓
Tables
        ↓
PivotTable
        ↓
PivotChart
        ↓
Dynamic Arrays
        ↓
Data Validation
        ↓
Conditional Formatting
        ↓
Visualization
        ↓
Power Query
        ↓
Power Pivot
        ↓
Data Model
        ↓
Relationships
        ↓
DAX
        ↓
Time Intelligence
        ↓
🔥 Professional Dashboard
```

### 🎯 এখন সবচেয়ে গুরুত্বপূর্ণ কাজ

**আর নতুন topic-এ যাওয়ার আগে Class 20–22-এর তিনটি জিনিস হাতে-কলমে practice করো:**

```text
Power Query
    +
Data Model / Relationships
    +
DAX Measures
```

কারণ এই তিনটা হলো Excel থেকে **BI/Data Analytics-এর দিকে যাওয়ার bridge**।


-----

হ্যাঁ, অবশ্যই। **Class 22 দিয়ে Excel-এর core syllabus শেষ**, কিন্তু Mastery করার জন্য আমি তোমাকে আরও কিছু **advanced + practical classes** করাবো।

### 📚 Excel Mastery — Next Classes

|Class|Topic|গুরুত্ব|
|---|---|---|
|**23**|Advanced DAX Practice|⭐⭐⭐|
|**24**|Advanced Power Query & ETL|⭐⭐⭐|
|**25**|Excel Dashboard — Full Project|⭐⭐⭐|
|**26**|Excel Data Cleaning Project|⭐⭐⭐|
|**27**|Sales/Business Analytics Project|⭐⭐⭐|
|**28**|HR Analytics Project|⭐⭐|
|**29**|Financial Analytics Project|⭐⭐|
|**30**|Excel Interview Questions + MCQ|⭐⭐⭐|
|**31**|Excel Practical Test|⭐⭐⭐|
|**32**|Excel Automation + VBA Basics|⭐⭐|
|**33**|Excel → SQL Connection Concepts|⭐⭐⭐|
|**34**|Excel → Power BI Transition|⭐⭐⭐|
|**35**|Final Excel Mastery Capstone|⭐⭐⭐|

### 🎯 আমার recommendation

তোমার ক্ষেত্রে সবচেয়ে ভালো হবে:

```text
Class 22
   ↓
Class 23 — Advanced DAX Practice
   ↓
Class 24 — Advanced Power Query
   ↓
Class 25 — Complete Dashboard
   ↓
Class 26–29 — Real Projects
   ↓
Class 30 — Interview + MCQ
   ↓
Class 31 — Practical Exam
   ↓
Class 32 — VBA
   ↓
Class 33 — Excel → SQL
   ↓
Class 34 — Excel → Power BI
   ↓
Class 35 — Final Project
```

**তাহলে Excel শুধু মুখস্থ শেখা হবে না—portfolio-level কাজ করার মতো skill হবে।**

👉 চাইলে এখনই **Class 23 — Advanced DAX Practice: CALCULATE, FILTER, ALL, SUMX, RELATED + 20 Practical Problems** শুরু করি।



-----


# 📘 Excel Mastery — Class 23

## 🔥 Advanced DAX Practice

### `CALCULATE()` + `FILTER()` + `ALL()` + `SUMX()` + `RELATED()`

আজকের Class-এ আমরা **শুধু theory না**, practical problem solving করব।

তোমার লক্ষ্য হবে:

> **DAX formula দেখে বোঝা → formula নিজে লেখা → business question থেকে DAX বানানো।**

---

# 🧠 Part 1 — আমাদের Practice Dataset

আজ সব problem একই ধরনের dataset দিয়ে করব।

## Customers

|Customer_ID|Customer_Name|City|Segment|
|---|---|---|---|
|C001|Rahim|Dhaka|Retail|
|C002|Karim|Chittagong|Corporate|
|C003|Hasan|Dhaka|Retail|
|C004|Jamil|Sylhet|Corporate|
|C005|Nabil|Dhaka|Corporate|

---

## Products

|Product_ID|Product_Name|Category|Price|
|---|---|---|--:|
|P001|Laptop|Electronics|50000|
|P002|Mouse|Accessories|1000|
|P003|Keyboard|Accessories|2000|
|P004|Monitor|Electronics|20000|
|P005|Printer|Electronics|15000|

---

## Sales

|Order_ID|Customer_ID|Product_ID|Quantity|Sales|
|---|---|---|--:|--:|
|O001|C001|P001|2|100000|
|O002|C002|P002|5|5000|
|O003|C001|P003|3|6000|
|O004|C003|P004|2|40000|
|O005|C004|P005|1|15000|
|O006|C005|P001|1|50000|
|O007|C003|P002|10|10000|
|O008|C002|P004|3|60000|

Relationships:

```text
Customers
Customer_ID
     │
     │ 1 : Many
     ↓
Sales
Customer_ID


Products
Product_ID
     │
     │ 1 : Many
     ↓
Sales
Product_ID
```

---

# Part 2 — Basic Measures

Advanced DAX করার আগে foundation ঠিক করি।

## Problem 1 — Total Sales

### Question:

> সব sales-এর total কত?

```text
Total Sales =
SUM(Sales[Sales])
```

আমাদের data অনুযায়ী:

```text
100000 + 5000 + 6000 + 40000
+ 15000 + 50000 + 10000 + 60000

= 286000
```

✅ **Answer: 286,000**

---

# Problem 2 — Total Orders

```text
Total Orders =
COUNTROWS(Sales)
```

Sales table-এ 8টি order।

✅ **Answer: 8**

---

# Problem 3 — Unique Customers

```text
Unique Customers =
DISTINCTCOUNT(Sales[Customer_ID])
```

Customers:

```text
C001
C002
C003
C004
C005
```

✅ **Answer: 5**

---

# 🔥 Part 3 — CALCULATE()

এখন আসল practice।

---

# Problem 4 — Dhaka Sales

### Business Question:

> শুধু Dhaka-এর customers-এর total sales কত?

Formula:

```text
Dhaka Sales =
CALCULATE(
    [Total Sales],
    Customers[City] = "Dhaka"
)
```

Dhaka customers:

```text
C001
C003
C005
```

তাদের sales:

```text
C001 → 106000
C003 → 50000
C005 → 50000
```

Total:

```text
206000
```

✅ **Answer: 206,000**

---

# Problem 5 — Corporate Sales

Question:

> Corporate customers-এর total sales কত?

```text
Corporate Sales =
CALCULATE(
    [Total Sales],
    Customers[Segment] = "Corporate"
)
```

Corporate:

```text
C002 → 65000
C004 → 15000
C005 → 50000
```

Total:

```text
130000
```

✅ **Answer: 130,000**

---

# Problem 6 — Electronics Sales

Products table-এ:

```text
Category = Electronics
```

DAX:

```text
Electronics Sales =
CALCULATE(
    [Total Sales],
    Products[Category] = "Electronics"
)
```

Electronics products:

```text
Laptop
Monitor
Printer
```

Sales:

```text
100000
40000
15000
50000
60000
```

Total:

```text
265000
```

✅ **Answer: 265,000**

---

# 🧠 CALCULATE Pattern

এই patternটা মুখস্থ না করে বুঝো:

```text
CALCULATE(
    Existing Measure,
    Filter
)
```

Examples:

```text
CALCULATE(
    [Total Sales],
    Customers[City] = "Dhaka"
)
```

অথবা:

```text
CALCULATE(
    [Total Sales],
    Products[Category] = "Electronics"
)
```

---

# 🔥 Part 4 — Multiple Filters

# Problem 7 — Dhaka + Corporate Sales

Question:

> Dhaka-এর Corporate customers-এর sales কত?

```text
Dhaka Corporate Sales =
CALCULATE(
    [Total Sales],
    Customers[City] = "Dhaka",
    Customers[Segment] = "Corporate"
)
```

Dhaka Corporate customer:

```text
C005
```

Sales:

```text
50000
```

✅ **Answer: 50,000**

---

# Problem 8 — Electronics + Dhaka

```text
Dhaka Electronics Sales =
CALCULATE(
    [Total Sales],
    Customers[City] = "Dhaka",
    Products[Category] = "Electronics"
)
```

Dhaka customers-এর electronics sales:

```text
100000
+ 40000
+ 50000
= 190000
```

✅ **Answer: 190,000**

---

# 🔥 Part 5 — FILTER()

`FILTER()` ব্যবহার করি যখন condition একটু complex হয়।

---

# Problem 9 — Sales Greater Than 20,000

Question:

> শুধু 20,000-এর বেশি individual sales-এর total কত?

```text
High Value Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        Sales,
        Sales[Sales] > 20000
    )
)
```

Values:

```text
100000
40000
50000
60000
```

Total:

```text
250000
```

✅ **Answer: 250,000**

---

# Problem 10 — Quantity >= 5

Question:

> যেসব transaction-এ quantity কমপক্ষে 5, তাদের sales কত?

```text
Bulk Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        Sales,
        Sales[Quantity] >= 5
    )
)
```

Matching:

```text
5  → 5000
10 → 10000
```

Total:

```text
15000
```

✅ **Answer: 15,000**

---

# ⚠️ FILTER-এর একটা গুরুত্বপূর্ণ বিষয়

Simple condition হলে:

```text
CALCULATE(
    [Total Sales],
    Customers[City] = "Dhaka"
)
```

যথেষ্ট হতে পারে।

Complex table filtering হলে:

```text
FILTER(...)
```

ব্যবহার করতে পারো।

---

# 🔥 Part 6 — ALL()

এখন আমরা **percentage of total** বানাবো।

---

# Problem 11 — Sales % of Total

Base measure:

```text
Total Sales =
SUM(Sales[Sales])
```

Formula:

```text
Sales % Total =
DIVIDE(
    [Total Sales],
    CALCULATE(
        [Total Sales],
        ALL(Customers[City])
    ),
    0
)
```

ধরি PivotTable-এ City:

|City|Sales|
|---|--:|
|Dhaka|206000|
|Chittagong|65000|
|Sylhet|15000|

Total:

```text
286000
```

Dhaka percentage:

```text
206000 / 286000
≈ 72.03%
```

---

# 🧠 ALL() কী করছে?

যদি current context:

```text
City = Dhaka
```

হয়, তাহলে:

```text
ALL(Customers[City])
```

City filter remove করতে সাহায্য করে।

তাই denominator হয়:

```text
Company Total Sales
```

---

# Problem 12 — Category % of Total

```text
Category % Total =
DIVIDE(
    [Total Sales],
    CALCULATE(
        [Total Sales],
        ALL(Products[Category])
    ),
    0
)
```

এখন PivotTable-এ Category রাখলে প্রতিটি category company total-এর percentage দেখাতে পারবে।

---

# 🔥 Part 7 — SUMX()

এখন row-by-row calculation।

---

# Problem 13 — Revenue from Quantity × Price

ধরি Sales table-এ `Sales` column না থাকলেও আমাদের কাছে:

```text
Quantity
```

এবং Product table-এ:

```text
Price
```

আছে।

Relationship আছে।

আমরা চাই:

```text
Quantity × Product Price
```

DAX:

```text
Total Revenue =
SUMX(
    Sales,
    Sales[Quantity] * RELATED(Products[Price])
)
```

এখানে:

```text
Sales → current row
RELATED → Product table থেকে Price
```

---

# Problem 14 — High Value Revenue

Question:

> Quantity × Price হিসাব করে শুধু Quantity >= 5 transactions-এর revenue কত?

```text
Bulk Revenue =
SUMX(
    FILTER(
        Sales,
        Sales[Quantity] >= 5
    ),
    Sales[Quantity] * RELATED(Products[Price])
)
```

এখানে তিনটি concept একসাথে:

```text
FILTER
   ↓
SUMX
   ↓
RELATED
```

🔥 এ ধরনের combination Advanced DAX-এর real power।

---

# 🔥 Part 8 — RELATED()

# Problem 15 — Product Category আনো

Sales table-এ নতুন calculated column:

```text
Category =
RELATED(Products[Category])
```

Relationship-এর মাধ্যমে:

```text
Sales[Product_ID]
       ↓
Products[Product_ID]
       ↓
Products[Category]
```

প্রতিটি Sales row তার Product-এর Category পাবে।

---

# Problem 16 — Product Price আনো

Sales table:

```text
Product Price =
RELATED(Products[Price])
```

যেমন:

```text
P001 → 50000
P002 → 1000
P003 → 2000
```

---

# 🧠 RELATED বনাম XLOOKUP

Excel-এ আমরা করতাম:

```text
XLOOKUP()
```

Data Model-এ relationship থাকলে:

```text
RELATED()
```

অনেক ক্ষেত্রে natural approach।

---

# 🔥 Part 9 — CALCULATE + FILTER + ALL

এখন advanced combination।

---

# Problem 17 — High Value Sales %

Question:

> 20,000-এর বেশি sales company total-এর কত শতাংশ?

High Value:

```text
High Value Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        Sales,
        Sales[Sales] > 20000
    )
)
```

Percentage:

```text
High Value Sales % =
DIVIDE(
    [High Value Sales],
    CALCULATE(
        [Total Sales],
        ALL(Sales)
    ),
    0
)
```

আমাদের data:

```text
High Value = 250000
Total = 286000
```

Percentage:

```text
≈ 87.41%
```

---

# 🔥 Part 10 — CALCULATE + SUMX

# Problem 18 — Dhaka Revenue

Question:

> Dhaka customers-এর Quantity × Product Price revenue কত?

```text
Dhaka Revenue =
CALCULATE(
    SUMX(
        Sales,
        Sales[Quantity] *
        RELATED(Products[Price])
    ),
    Customers[City] = "Dhaka"
)
```

এখানে:

```text
CALCULATE
    ↓
Filter Dhaka
    ↓
SUMX
    ↓
Quantity × Price
    ↓
Revenue
```

---

# 🔥 Part 11 — Dynamic Business Analysis

# Problem 19 — Best Customer

আমরা চাই:

> Customer-wise sales বের করে সবচেয়ে বেশি sales করা customer খুঁজে বের করতে।

প্রথমে measure:

```text
Total Sales =
SUM(Sales[Sales])
```

PivotTable:

```text
Rows:
Customer_Name

Values:
Total Sales
```

Result:

|Customer|Sales|
|---|--:|
|Rahim|106000|
|Karim|65000|
|Hasan|50000|
|Jamil|15000|
|Nabil|50000|

তাই:

```text
Best Customer = Rahim
Sales = 106000
```

💡 এখানে সবসময় complicated DAX দরকার নেই। অনেক business question PivotTable + measure দিয়েই solve করা যায়।

---

# 🔥 Problem 20 — Average Order Value

এটা খুব useful business KPI।

Formula:

```text
Average Order Value =
DIVIDE(
    [Total Sales],
    [Total Orders],
    0
)
```

আমাদের:

```text
Total Sales = 286000
Total Orders = 8
```

তাই:

```text
AOV = 35,750
```

AOV = **Average Order Value**

---

# 🏆 20 Practical Problems — Summary

|#|Problem|Main Concept|
|--:|---|---|
|1|Total Sales|`SUM`|
|2|Total Orders|`COUNTROWS`|
|3|Unique Customers|`DISTINCTCOUNT`|
|4|Dhaka Sales|`CALCULATE`|
|5|Corporate Sales|`CALCULATE`|
|6|Electronics Sales|`CALCULATE`|
|7|Dhaka + Corporate|Multiple filters|
|8|Dhaka + Electronics|Multiple filters|
|9|Sales > 20K|`FILTER`|
|10|Quantity ≥ 5|`FILTER`|
|11|Sales % Total|`ALL`|
|12|Category % Total|`ALL`|
|13|Quantity × Price|`SUMX + RELATED`|
|14|Bulk Revenue|`FILTER + SUMX + RELATED`|
|15|Category column|`RELATED`|
|16|Product Price|`RELATED`|
|17|High Value %|`FILTER + ALL`|
|18|Dhaka Revenue|`CALCULATE + SUMX`|
|19|Best Customer|Measure + Pivot|
|20|Average Order Value|`DIVIDE`|

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ ৫টি Formula Pattern

## Pattern 1 — Filter

```text
CALCULATE(
    [Measure],
    Table[Column] = "Value"
)
```

---

## Pattern 2 — Complex Filter

```text
CALCULATE(
    [Measure],
    FILTER(
        Table,
        Condition
    )
)
```

---

## Pattern 3 — Remove Filter

```text
CALCULATE(
    [Measure],
    ALL(Table[Column])
)
```

---

## Pattern 4 — Row-by-row Calculation

```text
SUMX(
    Table,
    Expression
)
```

---

## Pattern 5 — Related Table Value

```text
RELATED(
    OtherTable[Column]
)
```

---

# 🔥 সবচেয়ে Powerful Combination

এই formula patternটা ভালোভাবে বোঝো:

```text
CALCULATE(
    SUMX(
        FILTER(
            Sales,
            Sales[Quantity] >= 5
        ),
        Sales[Quantity] *
        RELATED(Products[Price])
    ),
    Customers[City] = "Dhaka"
)
```

এখানে একসাথে:

```text
CALCULATE
    ↓
FILTER
    ↓
SUMX
    ↓
RELATED
```

ব্যবহার হয়েছে।

এটা দেখলে ভয় পাওয়ার দরকার নেই।

Formula-টাকে ভেঙে পড়ো:

```text
1. কোন customer? → Dhaka
2. কোন rows? → Quantity >= 5
3. প্রতি row কী? → Quantity × Price
4. সব যোগ? → SUMX
```

এভাবেই complex DAX তৈরি করতে হয়।

---

# ⚠️ Advanced DAX-এর 7 Common Mistakes

### 1. `SUMX()` না বুঝে ব্যবহার করা

আগে প্রশ্ন করো:

> আমার কি row-by-row calculation দরকার?

যদি না লাগে, `SUM()` যথেষ্ট হতে পারে।

---

### 2. `RELATED()` কাজ না করা

সাধারণ কারণ:

- relationship নেই
    
- relationship ভুল direction/model
    
- calculated column-এর context সঠিক নয়
    

---

### 3. `ALL()` কী remove করছে না বোঝা

```text
ALL(Customers[City])
```

শুধু City filter-এর behaviour পরিবর্তন করে; পুরো Customers table-এর সব filter remove করার জন্য একই expression নয়।

---

### 4. Measure আর Column গুলিয়ে ফেলা

```text
Calculated Column → row-level
Measure → dynamic aggregation
```

---

### 5. `FILTER()` সব জায়গায় ব্যবহার করা

Simple condition হলে direct `CALCULATE` filter অনেক সময় cleaner।

---

### 6. Relationship ছাড়া RELATED ব্যবহার করা

`RELATED()` relationship-এর উপর নির্ভর করে।

---

### 7. Formula মুখস্থ করা

DAX শেখার সবচেয়ে ভালো পদ্ধতি:

```text
Business Question
       ↓
Required Data
       ↓
Filter?
       ↓
Row Calculation?
       ↓
Aggregation?
       ↓
DAX
```

---

# 🎯 Class 23 Practice Challenge

এবার উপরের solved examples না দেখে নিজে লেখার চেষ্টা করো।

### Challenge A

শুধু **Sylhet** customer-এর sales।

### Challenge B

শুধু **Accessories** category-এর sales।

### Challenge C

যেসব transaction-এর sales `>= 50,000`, তাদের total।

### Challenge D

Total sales-এর মধ্যে **Dhaka sales percentage**।

### Challenge E

Quantity × Product Price দিয়ে total revenue।

### Challenge F

Corporate customers-এর revenue।

### Challenge G ⭐

Quantity `>= 5` এবং City = Dhaka — এই দুই condition-এর revenue।

### Challenge H ⭐⭐

Company total-এর তুলনায় Electronics category কত %?

### Challenge I ⭐⭐

Average Order Value বের করো।

### Challenge J ⭐⭐⭐

**Dhaka + Quantity >= 5 + Quantity × Product Price** — এই তিনটি concept একসাথে ব্যবহার করে revenue বের করো।

---

# 🏁 আজকের সবচেয়ে গুরুত্বপূর্ণ Mental Model

```text
CALCULATE
   │
   ├── Change Filter Context
   │
   └── Calculate Measure


FILTER
   │
   └── Select specific rows


ALL
   │
   └── Remove/ignore specified filters


SUMX
   │
   └── Row-by-row calculation + SUM


RELATED
   │
   └── Get value from related table
```

আর পুরো Advanced DAX-এর formula-building logic:

```text
Business Question
       ↓
"কোন data?"
       ↓
"কোন filter?"
       ↓
"প্রতি row-তে calculation?"
       ↓
"Total/Average/Count?"
       ↓
CALCULATE / FILTER / SUMX / RELATED
       ↓
DAX Measure
       ↓
PivotTable
       ↓
Business Insight
```

**Class 23-এর মূল লক্ষ্য formula মুখস্থ করা নয়—এই চিন্তার process আয়ত্ত করা।**


-----
# 📘 Excel Mastery — Class 24

## 🚀 Advanced Power Query & ETL

আজকের Class-এ আমরা Excel-এর **Power Query-কে ছোট একটা ETL tool হিসেবে** ব্যবহার করব।

আগের Class 20-এ Power Query-এর basic শিখেছিলে। আজকে আমরা সেটা দিয়ে **real-world data pipeline** বানাবো।

### আজকের লক্ষ্য

```text
Raw Data
   ↓
Import
   ↓
Clean
   ↓
Transform
   ↓
Merge
   ↓
Append
   ↓
Group By
   ↓
Custom Columns
   ↓
Load
   ↓
Refresh
```

---

# 1️⃣ ETL কী?

ETL =

|Letter|Meaning|কাজ|
|---|---|---|
|E|Extract|Data আনা|
|T|Transform|Data clean/change করা|
|L|Load|Final data load করা|

উদাহরণ:

```text
January.xlsx
February.xlsx
March.xlsx
       ↓
   Power Query
       ↓
Clean + Transform
       ↓
   Final Sales Table
```

এটাই একটা basic ETL pipeline।

---

# 2️⃣ আজকের Real-World Project

ধরো একটা company-এর প্রতি মাসের sales data আলাদা Excel file-এ আছে।

```text
Sales_Data/
│
├── January.xlsx
├── February.xlsx
├── March.xlsx
└── April.xlsx
```

প্রতিটি file:

|Order_ID|Customer_ID|Product_ID|Quantity|Sales|
|---|---|---|--:|--:|
|O001|C001|P001|2|100000|
|O002|C002|P002|5|5000|

সমস্যা:

- কিছু নামের extra space
    
- কিছু duplicate
    
- কিছু blank
    
- City-এর spelling inconsistent
    
- আলাদা file-এ data
    
- Product information আলাদা table-এ
    

আমাদের Power Query দিয়ে সব ঠিক করতে হবে।

---

# 3️⃣ Power Query Open করা

Excel:

```text
Data
   ↓
Get Data
```

তারপর source অনুযায়ী:

```text
From File
├── From Excel Workbook
├── From Text/CSV
└── From Folder
```

---

# 4️⃣ From Folder — সবচেয়ে Important

যদি অনেক monthly file থাকে:

```text
Data
↓
Get Data
↓
From File
↓
From Folder
```

Folder select করো।

Excel দেখাবে:

```text
January.xlsx
February.xlsx
March.xlsx
April.xlsx
```

তারপর:

**Combine & Transform Data**

এটাই powerful feature।

---

# 5️⃣ Append vs Merge

এটা খুব ভালোভাবে বুঝতে হবে।

## Append

দুই table-এর **rows একসাথে করে**।

```text
January
↓
February
↓
March
↓
One Big Table
```

SQL-এর:

```sql
UNION ALL
```

এর মতো।

### Example

January:

|Order|Sales|
|---|--:|
|O1|1000|
|O2|2000|

February:

|Order|Sales|
|---|--:|
|O3|3000|
|O4|4000|

Append:

|Order|Sales|
|---|--:|
|O1|1000|
|O2|2000|
|O3|3000|
|O4|4000|

---

# 6️⃣ Merge

Merge হলো অন্য table থেকে related information আনা।

ধরো:

### Sales

|Product_ID|Quantity|
|---|--:|
|P001|2|
|P002|5|

### Products

|Product_ID|Product|Category|
|---|---|---|
|P001|Laptop|Electronics|
|P002|Mouse|Accessories|

Merge করার পরে:

|Product_ID|Quantity|Product|Category|
|---|--:|---|---|
|P001|2|Laptop|Electronics|
|P002|5|Mouse|Accessories|

SQL-এর:

```sql
JOIN
```

এর মতো।

---

# 🧠 মনে রাখবে

```text
APPEND
→ Rows combine
→ UNION ALL-like


MERGE
→ Columns/data from related table
→ JOIN-like
```

---

# 7️⃣ Data Type ঠিক করা

Power Query-তে প্রতিটি column-এর data type ঠিক রাখা খুব important।

উদাহরণ:

```text
Order_ID     → Text
Customer_ID  → Text
Quantity     → Whole Number
Sales        → Decimal Number
Order_Date   → Date
```

Column-এর পাশে data type icon থাকবে।

যদি Quantity:

```text
"5"
```

হিসেবে Text হয়, পরে calculation-এ সমস্যা হতে পারে।

তাই:

```text
Column
↓
Data Type
↓
Whole Number
```

---

# 8️⃣ Remove Unnecessary Columns

ধরো data:

|Order_ID|Customer|Email|Phone|Quantity|Sales|Temporary|
|---|---|---|---|--:|--:|---|

`Temporary` দরকার নেই।

Power Query:

```text
Select Column
↓
Right Click
↓
Remove
```

অথবা:

```text
Home → Remove Columns
```

---

# 9️⃣ Remove Duplicate Rows

ধরো:

|Order_ID|Customer|Sales|
|---|---|--:|
|O001|Rahim|1000|
|O002|Karim|2000|
|O001|Rahim|1000|

O001 duplicate।

Select:

```text
Order_ID
↓
Remove Rows
↓
Remove Duplicates
```

⚠️ কিন্তু সবসময় পুরো row duplicate কিনা বুঝতে হবে।

Business key অনুযায়ী duplicate নির্ধারণ করা উচিত।

---

# 🔟 Remove Blank Rows

Power Query:

```text
Home
↓
Remove Rows
↓
Remove Blank Rows
```

Blank row analysis নষ্ট করতে পারে।

---

# 1️⃣1️⃣ Trim Data

ধরো:

```text
" Dhaka "
```

আসলে:

```text
Dhaka
```

হওয়া উচিত।

Power Query:

```text
Transform
↓
Format
↓
Trim
```

এতে unnecessary spaces remove হয়।

---

# 1️⃣2️⃣ Clean

কখনও text-এর মধ্যে hidden/non-printable characters থাকতে পারে।

Power Query:

```text
Transform
↓
Format
↓
Clean
```

---

# 1️⃣3️⃣ Replace Values

ধরো City:

```text
Dhaka
DHAKA
dhaka
Dacca
```

আমরা standard করতে চাই:

```text
Dhaka
```

Power Query:

```text
Right Click Column
↓
Replace Values
```

Example:

```text
DHAKA → Dhaka
dhaka → Dhaka
```

---

# 1️⃣4️⃣ Split Column

ধরো:

```text
Full_Name
```

contains:

```text
Rahim Hasan
```

আমরা চাই:

```text
First_Name | Last_Name
```

Power Query:

```text
Transform
↓
Split Column
↓
By Delimiter
```

Delimiter:

```text
Space
```

Result:

|First_Name|Last_Name|
|---|---|
|Rahim|Hasan|

---

# 1️⃣5️⃣ Merge Columns

উল্টো কাজও করা যায়।

```text
First_Name | Last_Name
Rahim      | Hasan
```

Select both:

```text
Transform
↓
Merge Columns
```

Result:

```text
Rahim Hasan
```

---

# 🔥 1️⃣6️⃣ Custom Column

এটা খুব important।

ধরো:

|Quantity|Price|
|--:|--:|
|2|50000|
|5|1000|

আমরা চাই:

```text
Revenue = Quantity × Price
```

Power Query:

```text
Add Column
↓
Custom Column
```

Formula:

```text
[Quantity] * [Price]
```

Result:

|Quantity|Price|Revenue|
|--:|--:|--:|
|2|50000|100000|
|5|1000|5000|

---

# 1️⃣7️⃣ Conditional Column

এটা Excel-এর `IF()`-এর মতো।

ধরো:

```text
Sales >= 50000
```

হলে:

```text
High
```

না হলে:

```text
Normal
```

Power Query:

```text
Add Column
↓
Conditional Column
```

Logic:

```text
If Sales >= 50000
Then "High"
Else "Normal"
```

Result:

|Sales|Sales_Level|
|--:|---|
|100000|High|
|5000|Normal|
|60000|High|

---

# 1️⃣8️⃣ Group By

ধরো:

|City|Sales|
|---|--:|
|Dhaka|10000|
|Dhaka|20000|
|Sylhet|5000|
|Sylhet|7000|

Question:

> City-wise total sales কত?

Power Query:

```text
Home
↓
Group By
```

Group by:

```text
City
```

Operation:

```text
Sum
```

Column:

```text
Sales
```

Result:

|City|Total Sales|
|---|--:|
|Dhaka|30000|
|Sylhet|12000|

SQL-এর:

```sql
SELECT City, SUM(Sales)
FROM Sales
GROUP BY City;
```

এর মতো।

---

# 1️⃣9️⃣ Multiple Aggregation

একই Group By-তে:

```text
Total Sales
Average Sales
Count Orders
Maximum Sales
```

এগুলোও বের করতে পারো।

উদাহরণ:

|City|Total Sales|Average Sales|Orders|
|---|--:|--:|--:|
|Dhaka|30000|15000|2|
|Sylhet|12000|6000|2|

🔥 Analytics-এর জন্য খুব useful।

---

# 2️⃣0️⃣ Fill Down

ধরো data:

|Month|Sales|
|---|--:|
|January|10000|
|blank|15000|
|blank|20000|
|February|30000|
|blank|40000|

আমরা চাই:

|Month|Sales|
|---|--:|
|January|10000|
|January|15000|
|January|20000|
|February|30000|
|February|40000|

Power Query:

```text
Transform
↓
Fill
↓
Down
```

এটা messy reports clean করতে অনেক কাজে লাগে।

---

# 2️⃣1️⃣ Fill Up

উল্টো direction:

```text
Transform
↓
Fill
↓
Up
```

---

# 2️⃣2️⃣ Remove Errors

কখনও calculation-এ:

```text
Error
```

আসতে পারে।

Power Query:

```text
Home
↓
Remove Rows
↓
Remove Errors
```

তবে ⚠️ error blindly delete করা উচিত নয়।

আগে বুঝতে হবে:

> Error কেন হচ্ছে?

---

# 2️⃣3️⃣ Replace Errors

কিছু ক্ষেত্রে error-এর পরিবর্তে:

```text
0
```

বা:

```text
Unknown
```

দেওয়া যায়।

```text
Transform
↓
Replace Errors
```

---

# 🔥 2️⃣4️⃣ Applied Steps

Power Query-এর সবচেয়ে powerful feature-এর একটি হলো:

### Applied Steps

ধরো তুমি করেছো:

```text
Source
↓
Changed Type
↓
Removed Columns
↓
Trimmed Text
↓
Removed Duplicates
↓
Added Revenue
↓
Grouped Rows
```

Power Query এগুলো **record করে রাখে**।

পরেরবার নতুন data এলে:

```text
Refresh
```

করলেই transformation steps আবার execute হবে।

---

# 🧠 Excel Formula বনাম Power Query

|Excel Formula|Power Query|
|---|---|
|Row-by-row calculation|Transformation pipeline|
|Formula manually copied|Steps automatically applied|
|Good for interactive calculations|Good for data cleaning|
|Data preparation limited|Powerful cleaning|
|`IF()`|Conditional Column|
|`XLOOKUP()`|Merge|
|Stack rows manually|Append|
|`SUMIF()`|Group By|

---

# 🔥 2️⃣5️⃣ Real ETL Pipeline

এখন পুরো workflow দেখো:

```text
             RAW DATA
                │
       ┌────────┼────────┐
       ↓        ↓        ↓
    Excel      CSV     Database
       │        │        │
       └────────┼────────┘
                ↓
          POWER QUERY
                ↓
         Change Data Type
                ↓
         Remove Duplicates
                ↓
             Trim
                ↓
        Replace Values
                ↓
          Remove Errors
                ↓
             Merge
                ↓
             Append
                ↓
        Custom Columns
                ↓
          Conditional
                ↓
            Group By
                ↓
         CLEAN DATASET
                ↓
          Excel / Data Model
                ↓
          PivotTable
                ↓
           Dashboard
```

এটাই তোমার **ETL foundation**।

---

# 🧪 Class 24 Practical Project

এবার real practice করবে।

## Step 1

একটা folder বানাও:

```text
Sales_Data
```

এর মধ্যে:

```text
January.xlsx
February.xlsx
March.xlsx
```

রাখো।

প্রতিটি file-এ অন্তত 10–20 rows রাখবে।

Columns:

```text
Order_ID
Order_Date
Customer_ID
Customer_Name
City
Product_ID
Quantity
Price
Sales
```

---

## Step 2 — Power Query Import

```text
Data
→ Get Data
→ From Folder
```

সব files combine করো।

---

## Step 3 — Cleaning

করবে:

- Data type ঠিক করা
    
- Blank rows remove
    
- Duplicate remove
    
- Customer_Name → Trim
    
- City → standardize
    
- Errors check
    
- Unnecessary column remove
    

---

## Step 4 — Custom Column

তৈরি করো:

```text
Revenue
```

Formula:

```text
[Quantity] * [Price]
```

---

## Step 5 — Conditional Column

তৈরি করো:

```text
Sales_Level
```

Logic:

```text
>= 50000 → High
>= 20000 → Medium
< 20000 → Low
```

---

## Step 6 — Group By

City-wise:

```text
Total Revenue
Order Count
Average Revenue
```

---

## Step 7 — Product Merge

আরেকটি table বানাও:

```text
Product_ID
Product_Name
Category
```

তারপর Sales table-এর সাথে:

```text
Merge Queries
```

করো।

Join:

```text
Sales[Product_ID]
       =
Products[Product_ID]
```

---

## Step 8 — Load

শেষে:

```text
Home
↓
Close & Load
```

---

# 🔥 Class 24 Challenge

নিজে solve করবে:

### Q1

January + February + March কীভাবে এক table করবে?

### Q2

Product information কীভাবে Sales table-এ আনবে?

### Q3

`Quantity × Price` কীভাবে নতুন column বানাবে?

### Q4

City-wise total sales কীভাবে বের করবে?

### Q5

Sales > 50,000 হলে `"High"` কীভাবে করবে?

### Q6

Customer names-এর extra spaces কীভাবে remove করবে?

### Q7

Duplicate Order_ID কীভাবে handle করবে?

### Q8

নতুন April file যোগ করার পর existing transformation কীভাবে আবার চালাবে?

### Q9

Append আর Merge-এর মধ্যে difference কী?

### Q10 ⭐

একটি complete pipeline design করো:

```text
4 Monthly CSV
      ↓
Power Query
      ↓
Clean
      ↓
Append
      ↓
Merge Product
      ↓
Revenue
      ↓
Group By
      ↓
Final Dataset
      ↓
Dashboard
```

---

# 🧠 Class 24 Cheat Sheet

```text
From Folder
→ Multiple files import

Append
→ Rows combine

Merge
→ Related tables combine

Trim
→ Extra spaces remove

Clean
→ Hidden/unprintable characters clean

Split
→ One column → multiple columns

Merge Columns
→ Multiple columns → one column

Custom Column
→ Calculation

Conditional Column
→ IF-like logic

Group By
→ Aggregation

Fill Down
→ Previous value নিচে copy

Applied Steps
→ Transformation history

Refresh
→ New data-এর উপর same pipeline পুনরায় run
```

---

## 🎯 Class 24-এর মূল শিক্ষা

তুমি এখন Excel-কে শুধু **formula করার software** হিসেবে দেখবে না।

বরং:

```text
Excel
   +
Power Query
   +
Power Pivot/DAX
   ↓
Mini Data Analytics Platform
```

আর তোমার Data Analyst → Data Engineer journey-তে **Power Query-এর সবচেয়ে গুরুত্বপূর্ণ skill হলো “repeatable data transformation”**—একবার pipeline বানালে নতুন monthly data এলে বারবার manually clean করার প্রয়োজন কমে যায়।

----
# 📘 Excel Mastery — Class 25

## 🏆 Excel Dashboard — Full Real-World Project

আজ আমরা **একটা complete professional Sales Dashboard** বানানোর process শিখব।

আগের classes-এ তুমি আলাদাভাবে শিখেছ:

```text
Excel Formulas
↓
Data Cleaning
↓
Tables
↓
PivotTable
↓
PivotChart
↓
Power Query
↓
Power Pivot + DAX
```

আজ এগুলোকে **একটা project-এ combine** করব।

---

# 🎯 Class 25-এর Goal

শেষে আমাদের dashboard দেখতে conceptually এমন হবে:

```text
┌─────────────────────────────────────────────────────┐
│              SALES PERFORMANCE DASHBOARD            │
├──────────────┬──────────────┬──────────────┬─────────┤
│ Total Sales  │ Total Profit │ Total Orders │ Customers│
│   ৳286K      │    ৳52K      │      120     │    45   │
├──────────────┴──────────────┴──────────────┴─────────┤
│                                                     │
│              Monthly Sales Trend                   │
│                    📈                               │
│                                                     │
├──────────────────────────┬──────────────────────────┤
│      Sales by City       │    Sales by Category     │
│          📊              │          📊              │
├──────────────────────────┼──────────────────────────┤
│     Top Products         │      Sales by Segment    │
│          📊              │          📊              │
└──────────────────────────┴──────────────────────────┘

Filters:
Year | Month | City | Category | Segment
```

এটা একটা **analytics dashboard**, শুধু সুন্দর chart-এর collection না।

---

# 1️⃣ Dashboard-এর জন্য Dataset

আজ আমরা এই structure ব্যবহার করব:

## Sales Table

|Order_ID|Date|Customer_ID|Product_ID|City|Segment|Quantity|Sales|Cost|
|---|---|---|---|---|---|--:|--:|--:|
|O001|01-Jan|C001|P001|Dhaka|Retail|2|100000|80000|
|O002|05-Jan|C002|P002|Chittagong|Corporate|5|5000|3500|
|O003|10-Jan|C003|P003|Dhaka|Retail|3|6000|4000|
|O004|15-Feb|C004|P004|Sylhet|Corporate|2|40000|30000|
|O005|20-Feb|C005|P005|Dhaka|Corporate|1|15000|11000|

বাস্তব project-এ আমরা অনেক বেশি rows ব্যবহার করব:

```text
500+
1000+
10000+
```

---

# 2️⃣ প্রথমে Data Architecture

একটা professional dashboard বানানোর আগে data structure বুঝতে হবে।

আমরা রাখব:

```text
Customers
Products
Sales
Date
```

### Relationship

```text
              Customers
                  │
                  │
                  ↓
Products ────── Sales ────── Date
```

আর একটু detail:

```text
Customers
Customer_ID
     │
     │ 1 : Many
     ↓
Sales
Customer_ID


Products
Product_ID
     │
     │ 1 : Many
     ↓
Sales
Product_ID


DateTable
Date
     │
     │ 1 : Many
     ↓
Sales
Order_Date
```

এটাই আমাদের **Data Model**।

---

# 3️⃣ Dashboard বানানোর আগে Data Clean

Power Query দিয়ে:

```text
Raw Data
   ↓
Remove Duplicates
   ↓
Remove Blank Rows
   ↓
Trim Text
   ↓
Fix Data Types
   ↓
Remove Errors
   ↓
Standardize City
   ↓
Load to Data Model
```

⚠️ Dashboard-এর আগে data clean না করলে dashboard সুন্দর হলেও **wrong insight** দিতে পারে।

---

# 4️⃣ Date Table তৈরি

Power Pivot/DAX-এ:

```text
DateTable =
CALENDAR(
    DATE(2026,1,1),
    DATE(2026,12,31)
)
```

তারপর calculated columns:

### Year

```text
Year =
YEAR(DateTable[Date])
```

### Month

```text
Month =
FORMAT(DateTable[Date],"MMMM")
```

### Month Number

```text
Month Number =
MONTH(DateTable[Date])
```

### Quarter

```text
Quarter =
"Q" & FORMAT(DateTable[Date],"Q")
```

---

# ⚠️ Month-এর গুরুত্বপূর্ণ সমস্যা

যদি শুধু:

```text
January
February
March
...
```

ব্যবহার করো, Excel alphabetically সাজাতে পারে:

```text
April
August
December
February
...
```

❌ ভুল।

তাই:

```text
Month
+
Month Number
```

ব্যবহার করব।

তারপর:

```text
Month
→ Sort by Column
→ Month Number
```

তাহলে:

```text
January
February
March
April
...
```

হবে।

---

# 5️⃣ প্রথম KPI — Total Sales

Measure:

```text
Total Sales =
SUM(Sales[Sales])
```

Dashboard-এ এটা একটা **KPI Card** হবে।

---

# 6️⃣ KPI — Total Profit

Profit:

```text
Sales - Cost
```

DAX:

```text
Total Profit =
SUMX(
    Sales,
    Sales[Sales] - Sales[Cost]
)
```

অথবা Sales ও Cost column-এর structure অনুযায়ী:

```text
Total Profit =
SUM(Sales[Sales]) - SUM(Sales[Cost])
```

দুটোর মধ্যে context অনুযায়ী appropriate version ব্যবহার করা যায়।

---

# 7️⃣ KPI — Total Orders

```text
Total Orders =
COUNTROWS(Sales)
```

যদি Order_ID duplicate হতে পারে এবং প্রতিটি order-এর একাধিক product row থাকে, তখন:

```text
Total Orders =
DISTINCTCOUNT(Sales[Order_ID])
```

🔥 বাস্তব business data-তে এই distinction খুব গুরুত্বপূর্ণ।

---

# 8️⃣ KPI — Unique Customers

```text
Unique Customers =
DISTINCTCOUNT(
    Sales[Customer_ID]
)
```

---

# 9️⃣ KPI — Average Order Value

```text
AOV =
DIVIDE(
    [Total Sales],
    [Total Orders],
    0
)
```

AOV = Average Order Value.

---

# 🔥 Dashboard-এর প্রথম Section

এখন dashboard-এর top অংশে:

```text
┌─────────────┬─────────────┬─────────────┬─────────────┐
│ TOTAL SALES │ TOTAL PROFIT│TOTAL ORDERS │  CUSTOMERS  │
│             │             │             │             │
│   ৳286K     │    ৳52K     │     120     │     45      │
└─────────────┴─────────────┴─────────────┴─────────────┘
```

এগুলো হলো **KPI Cards**।

---

# 10️⃣ Monthly Sales Trend

এখন business question:

> কোন মাসে sales বাড়ছে বা কমছে?

PivotTable তৈরি করো।

### Rows

```text
DateTable[Month]
```

### Values

```text
[Total Sales]
```

Result:

|Month|Sales|
|---|--:|
|January|111000|
|February|55000|
|March|70000|
|April|50000|

তারপর:

```text
Insert
→ Line Chart
```

### কেন Line Chart?

কারণ আমরা **time trend** দেখছি।

```text
January → February → March → April
```

---

# 11️⃣ Monthly Profit Trend

আরেকটি PivotTable:

```text
Rows:
Month

Values:
Total Profit
```

Line chart বা combo chart ব্যবহার করা যায়।

---

# 12️⃣ Sales by City

Business Question:

> কোন city সবচেয়ে বেশি sales করছে?

PivotTable:

```text
Rows:
Customers[City]

Values:
[Total Sales]
```

Example:

|City|Sales|
|---|--:|
|Dhaka|150000|
|Chittagong|80000|
|Sylhet|56000|

তারপর:

```text
Insert
→ Bar Chart
```

### কেন Bar?

City ranking compare করা সহজ হয়।

---

# 13️⃣ Sales by Category

PivotTable:

```text
Rows:
Products[Category]

Values:
[Total Sales]
```

Example:

|Category|Sales|
|---|--:|
|Electronics|200000|
|Accessories|60000|
|Furniture|26000|

তারপর:

```text
Column Chart
```

---

# 14️⃣ Sales by Segment

PivotTable:

```text
Rows:
Customers[Segment]

Values:
[Total Sales]
```

Example:

|Segment|Sales|
|---|--:|
|Retail|170000|
|Corporate|116000|

Chart:

```text
Column / Bar
```

---

# 🔥 15️⃣ Top 5 Products

Business question:

> কোন products সবচেয়ে বেশি sales generate করছে?

PivotTable:

```text
Rows:
Products[Product_Name]

Values:
[Total Sales]
```

তারপর:

```text
Sort
→ Largest to Smallest
```

Top 5 দেখাও।

Example:

|Product|Sales|
|---|--:|
|Laptop|100000|
|Monitor|60000|
|Printer|40000|
|Keyboard|30000|
|Mouse|20000|

---

# 16️⃣ Target vs Actual

এখন dashboard আরও professional করি।

ধরো monthly target:

|Month|Target|
|---|--:|
|January|100000|
|February|60000|
|March|80000|

Measure:

```text
Total Target =
SUM(Target[Target])
```

### Achievement %

```text
Achievement % =
DIVIDE(
    [Total Sales],
    [Total Target],
    0
)
```

### Variance

```text
Variance =
[Total Sales] - [Total Target]
```

---

# 17️⃣ Actual vs Target Chart

PivotTable:

```text
Month
↓
Sales
Target
```

তারপর:

```text
Insert
→ Combo Chart
```

Concept:

```text
Sales   → Column
Target  → Line
```

এতে খুব সহজে বোঝা যায়:

> কোথায় target achieve হয়েছে?

---

# 🔥 18️⃣ Slicer — Dashboard-এর সবচেয়ে Useful Feature

Dashboard-এ user যেন filter করতে পারে।

যেমন:

```text
┌───────────────┐
│ City          │
├───────────────┤
│ Dhaka         │
│ Chittagong    │
│ Sylhet        │
└───────────────┘
```

আর:

```text
Year
Month
Category
Segment
```

এর জন্যও Slicer।

---

# 19️⃣ Slicer তৈরি

PivotTable select করো:

```text
PivotTable Analyze
↓
Insert Slicer
```

Select:

```text
City
Category
Segment
Year
```

তারপর dashboard-এ সাজাও।

---

# 20️⃣ একই Slicer একাধিক PivotTable-এ

এটা professional dashboard-এর খুব important feature।

ধরো:

```text
City Slicer
```

change করলে:

```text
Monthly Sales
City Sales
Category Sales
Product Sales
Profit
```

সব update হওয়া উচিত।

এর জন্য:

```text
Slicer
→ Report Connections
```

তারপর প্রয়োজনীয় PivotTable-গুলো select করো।

---

# 🧠 Dashboard-এর Architecture

এখন পুরো structure:

```text
                     DASHBOARD
                         │
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
      KPI              Charts           Filters
        │                │                │
        ↓                ↓                ↓
 Sales/Profit       Monthly Trend       City
 Orders/Customer    City Analysis       Category
 AOV                Product Analysis    Segment
                    Target Analysis
```

---

# 21️⃣ Dashboard Layout

একটা clean layout রাখো:

```text
┌─────────────────────────────────────────────────────┐
│              SALES PERFORMANCE DASHBOARD            │
│                                                     │
│  [Year] [Month] [City] [Category] [Segment]        │
├───────────┬───────────┬───────────┬─────────────────┤
│ Sales     │ Profit    │ Orders    │ Customers       │
│ ৳286K     │ ৳52K      │ 120       │ 45              │
├───────────────────────┬─────────────────────────────┤
│                       │                             │
│ Monthly Sales Trend   │ Sales by City              │
│                       │                             │
├───────────────────────┼─────────────────────────────┤
│                       │                             │
│ Sales by Category     │ Sales by Segment            │
│                       │                             │
├───────────────────────┴─────────────────────────────┤
│                                                     │
│             Top 5 Products                          │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

# 22️⃣ Dashboard Design Rules

Professional dashboard মানে অনেক chart না।

### Rule 1

এক screen-এ important information রাখো।

### Rule 2

প্রতিটি chart-এর meaningful title দাও।

❌

```text
Chart 1
```

✅

```text
Monthly Sales Trend
```

---

### Rule 3

Unnecessary 3D chart avoid করো।

❌

```text
3D Pie
3D Column
```

---

### Rule 4

Too many colors ব্যবহার করো না।

একটা consistent visual theme রাখাই ভালো।

---

### Rule 5

Numbers readable রাখো।

যেমন:

```text
286000
```

এর বদলে dashboard-এ:

```text
৳286K
```

দেখানো যেতে পারে।

---

# 23️⃣ Dashboard-এর Business Insight

Dashboard-এর সবচেয়ে important অংশ হলো:

> **So what?**

Chart বানালেই কাজ শেষ না।

ধরো dashboard বলছে:

```text
Dhaka Sales = 65%
Chittagong = 25%
Sylhet = 10%
```

Insight:

> Dhaka is the company's strongest market.

আর যদি:

```text
March Sales ↓
```

তাহলে question:

> March-এ sales কেন কমেছে?

আর যদি:

```text
Laptop = 45% of Sales
```

তাহলে:

> Business heavily depends on Laptop sales.

এটাই **Data Analysis**।

---

# 🔥 24️⃣ Dashboard Refresh Workflow

এটাই Power Query + Power Pivot-এর আসল power।

আগে:

```text
January
February
March
```

ছিল।

এখন:

```text
April.xlsx
```

যোগ করলাম।

তারপর:

```text
Data
↓
Refresh All
```

Power Query:

```text
New Data
↓
Clean
↓
Transform
↓
Load
```

তারপর:

```text
Data Model
↓
DAX Measures
↓
PivotTables
↓
Charts
↓
Dashboard
```

সব update হতে পারে।

🔥 এটাই **automated reporting workflow**।

---

# 🧩 Full Project Architecture

```text
                RAW FILES
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
    January     February      March
        │           │           │
        └───────────┼───────────┘
                    ↓
              POWER QUERY
                    ↓
              DATA CLEANING
                    ↓
             TRANSFORMATION
                    ↓
              MERGE / APPEND
                    ↓
               DATA MODEL
                    ↓
       ┌────────────┼────────────┐
       ↓            ↓            ↓
   Customers     Products      Date
       │            │            │
       └────────────┼────────────┘
                    ↓
                  Sales
                    ↓
                  DAX
                    ↓
            ┌───────┼────────┐
            ↓       ↓        ↓
          KPI    PivotTable  Measures
                    ↓
                PivotChart
                    ↓
                 Slicer
                    ↓
               DASHBOARD
                    ↓
             BUSINESS INSIGHT
```

---

# 🎯 Class 25 Final Project

এবার তোমার **Excel Mastery Capstone-এর first major project**।

## Dataset

কমপক্ষে:

```text
Customers → 30+
Products  → 20+
Sales     → 500+
```

থাকবে।

### Sales columns

```text
Order_ID
Order_Date
Customer_ID
Product_ID
Quantity
Sales
Cost
```

### Customer columns

```text
Customer_ID
Customer_Name
City
Segment
```

### Product columns

```text
Product_ID
Product_Name
Category
Price
```

---

# ✅ তোমার Task List

### Data Preparation

-  Power Query import
    
-  Data types
    
-  Remove duplicates
    
-  Remove blanks
    
-  Trim text
    
-  Fix inconsistent values
    
-  Merge Products
    
-  Append monthly data
    

### Data Model

-  Customers table
    
-  Products table
    
-  Sales fact table
    
-  Date table
    
-  Relationships
    

### DAX

তৈরি করবে:

```text
Total Sales
Total Profit
Total Orders
Unique Customers
AOV
Achievement %
Variance
```

### Dashboard

তৈরি করবে:

-  KPI Cards
    
-  Monthly Sales Trend
    
-  Sales by City
    
-  Sales by Category
    
-  Sales by Segment
    
-  Top 5 Products
    
-  Actual vs Target
    
-  Slicers
    

### Final

কমপক্ষে **5টি business insights** লিখবে।

---

# 🧠 Class 25 Cheat Sheet

```text
POWER QUERY
→ Clean + Transform

DATA MODEL
→ Connect Tables

DAX
→ Calculate Business Metrics

PIVOTTABLE
→ Summarize Data

PIVOTCHART
→ Visualize Data

SLICER
→ Interactive Filtering

DASHBOARD
→ Decision Making

BUSINESS INSIGHT
→ "What does the data tell us?"
```

---

# 🏆 আজ পর্যন্ত তোমার Excel Journey

```text
Class 1–4
Excel Foundation
       ↓
Class 5–9
Functions + Logic + Lookup
       ↓
Class 10–12
Data Cleaning + Tables
       ↓
Class 13–19
Pivot + Charts + Visualization
       ↓
Class 20
Power Query
       ↓
Class 21–22
Power Pivot + DAX
       ↓
Class 23
Advanced DAX
       ↓
Class 24
Advanced Power Query + ETL
       ↓
🔥 Class 25
FULL DASHBOARD PROJECT
```

**পরবর্তী ধাপে Class 26 হবে → `Excel Data Cleaning Project`**, যেখানে আমরা ইচ্ছাকৃতভাবে messy/dirty dataset নিয়ে **zero থেকে production-ready clean dataset** বানাবো।



----
# 📘 Excel Mastery — Class 26

## 🧹 Excel Data Cleaning Project — Real-World Messy Dataset

আজ আমরা নতুন কোনো বড় function শেখার চেয়ে বেশি গুরুত্বপূর্ণ একটা skill practice করব:

> **Messy/dirty data → Clean data → Analysis-ready data**

Data Analyst হিসেবে এটা খুব গুরুত্বপূর্ণ, কারণ বাস্তব data সাধারণত সরাসরি analysis করার মতো clean থাকে না।

---

# 🎯 আজকের Project

আমরা একটি fictional **Sales Customer Dataset** clean করব।

Raw data দেখতে এমন:

|Customer ID|Name|Email|Phone|City|Gender|Age|Salary|Join Date|
|---|---|---|---|---|---|--:|--:|---|
|C001|`Rahim Hasan`|`RAHIM@GMAIL.COM`|`01711-123456`|dhaka|M|25|`45000`|01/01/2026|
|C002|`karim ahmed`|`karim@gmail.com`|`01712 123457`|DHAKA|Male|31|`55000`|02/01/2026|
|C003|`Hasan Ali`|`HASAN@YAHOO.COM`|`01713-123458`|Chittagong|male|`29`|`60000`|03/01/2026|
|C003|`Hasan Ali`|`hasan@yahoo.com`|`01713-123458`|Chittagong|Male|29|60000|03/01/2026|
|C004|`JAMIL`|`jamil@gmail.com`|`01714-123459`|Chattogram|M|22|35000|`04-01-2026`|
|C005|`Nabil Rahman`|`nabil@gmail.com`|blank|Sylhet|Male|blank|40000|05/01/2026|

এখানে অনেক problem আছে।

---

# 🔎 Part 1 — Dirty Data Identify করা

প্রথম কাজ **clean করা নয়**।

প্রথম কাজ:

> **Problem identify করা।**

আমাদের dataset-এ:

### Problem 1 — Extra Spaces

```text
" Rahim Hasan "
"  Hasan Ali"
```

---

### Problem 2 — Name Case Inconsistent

```text
karim ahmed
JAMIL
```

কিন্তু চাই:

```text
Karim Ahmed
Jamil
```

---

### Problem 3 — Email Case

```text
RAHIM@GMAIL.COM
```

এটা standard করতে পারি:

```text
rahim@gmail.com
```

---

### Problem 4 — Phone Format

```text
01711-123456
01712 123457
```

একই format রাখা দরকার।

---

### Problem 5 — City Inconsistent

```text
dhaka
DHAKA
Dhaka
```

এবং:

```text
Chittagong
Chattogram
```

এখানে business rule ঠিক করতে হবে—দুটোকে একই city হিসেবে treat করব কিনা।

---

### Problem 6 — Gender Inconsistent

```text
M
Male
male
```

সবকে:

```text
Male
```

করা যায়।

---

### Problem 7 — Numeric Data as Text

```text
"29"
"60000 "
```

এগুলো Text হতে পারে।

---

### Problem 8 — Missing Data

```text
Phone = blank
Age = blank
```

---

### Problem 9 — Duplicate

```text
C003
```

দুইবার আছে।

---

### Problem 10 — Date Inconsistent

```text
01/01/2026
04-01-2026
```

Date format consistent করা দরকার।

---

# 🧠 Data Cleaning-এর Golden Rule

একটা খুব গুরুত্বপূর্ণ principle:

> **Missing data আর wrong data এক জিনিস নয়।**

উদাহরণ:

```text
Age = blank
```

এটা missing।

কিন্তু:

```text
Age = 250
```

এটা invalid/wrong data।

দুটোর treatment একই হবে না।

---

# 🧹 Part 2 — Create Raw Data Backup

সবচেয়ে আগে:

```text
Raw_Data
```

sheet-টা untouched রাখো।

তার copy:

```text
Cleaned_Data
```

বানাও।

Workflow:

```text
Raw_Data
     ↓
Cleaned_Data
     ↓
Analysis
```

❌ Raw data directly modify না করাই ভালো।

---

# 3️⃣ Convert Range → Excel Table

Cleaned data select:

```text
Ctrl + T
```

তারপর:

```text
My table has headers
```

select করো।

Table name:

```text
Customers
```

দিলে পরে structured references ব্যবহার করতে পারবে।

---

# 🧹 Part 3 — Clean Names

Raw:

```text
 Rahim Hasan 
karim ahmed
  Hasan Ali
JAMIL
```

Formula:

```excel
=PROPER(TRIM(B2))
```

### `TRIM()`

extra spaces remove করে।

### `PROPER()`

প্রতিটি word-এর প্রথম letter capital করে।

Result:

```text
Rahim Hasan
Karim Ahmed
Hasan Ali
Jamil
```

---

# 4️⃣ Clean Email

Formula:

```excel
=LOWER(TRIM(C2))
```

Result:

```text
rahim@gmail.com
karim@gmail.com
hasan@yahoo.com
```

---

# 5️⃣ Clean Phone

ধরো:

```text
01711-123456
01712 123457
```

আমরা hyphen/space remove করতে চাই।

Formula:

```excel
=SUBSTITUTE(SUBSTITUTE(TRIM(D2),"-","")," ","")
```

Result:

```text
01711123456
01712123457
```

---

# ⚠️ Phone Number নিয়ে Important Point

Phone number সাধারণত **number নয়, identifier/text** হিসেবে রাখা ভালো।

কারণ:

```text
01711123456
```

এর ওপর mathematical calculation করার দরকার নেই।

আর leading zero থাকলে numeric format সমস্যা করতে পারে।

তাই:

```text
Phone → Text
```

রাখা safer।

---

# 🧹 Part 4 — Standardize City

Raw:

```text
dhaka
DHAKA
Dhaka
```

প্রথমে:

```excel
=PROPER(TRIM(E2))
```

ফলে:

```text
Dhaka
Dhaka
Dhaka
```

কিন্তু:

```text
Chittagong
Chattogram
```

এটা শুধু `PROPER()` দিয়ে solve হবে না।

এখানে **business standard** দরকার।

ধরো company সিদ্ধান্ত নিল:

```text
Chattogram → Chittagong
```

তাহলে:

```text
=IF(TRIM(E2)="Chattogram","Chittagong",PROPER(TRIM(E2)))
```

---

# 🧠 Data Standardization

এখানে একটা important concept:

```text
Cleaning
≠
Standardization
```

### Cleaning

```text
" Dhaka "
↓
"Dhaka"
```

### Standardization

```text
Chattogram
↓
Chittagong
```

Standardization-এর জন্য business rule থাকতে পারে।

---

# 🧹 Part 5 — Gender Standardization

Raw:

```text
M
Male
male
```

Formula:

```excel
=IF(OR(TRIM(F2)="M",LOWER(TRIM(F2))="male"),"Male",TRIM(F2))
```

Female থাকলে:

```excel
=IF(
   OR(
      TRIM(F2)="F",
      LOWER(TRIM(F2))="female"
   ),
   "Female",
   TRIM(F2)
)
```

আর বড় dataset হলে Power Query দিয়ে Replace Values করাও ভালো।

---

# 🔥 Part 6 — Numeric Data Clean

Salary:

```text
45000
55000
60000 
```

Extra spaces থাকলে:

```excel
=VALUE(TRIM(H2))
```

`VALUE()` text-number কে actual number-এ convert করতে সাহায্য করে।

---

# 7️⃣ Age Clean

যদি:

```text
"29"
```

Text হিসেবে থাকে:

```excel
=VALUE(TRIM(G2))
```

তারপর verify করো:

```text
Data Type → Number
```

---

# 🚨 Part 7 — Validate Age

Clean করলেই হবে না।

Data validation check করব।

ধরো valid age:

```text
18–60
```

Formula:

```excel
=AND(G2>=18,G2<=60)
```

Result:

```text
TRUE
```

মানে valid।

---

# 8️⃣ Invalid Age Flag

নতুন column:

```text
Age_Status
```

Formula:

```excel
=IF(
   G2="",
   "Missing",
   IF(
      AND(G2>=18,G2<=60),
      "Valid",
      "Invalid"
   )
)
```

Result:

|Age|Status|
|--:|---|
|25|Valid|
|31|Valid|
|blank|Missing|
|15|Invalid|
|80|Invalid|

🔥 Data cleaning-এ **flagging** খুব useful।

---

# 🧹 Part 8 — Missing Data

ধরো:

```text
Phone = blank
Age = blank
```

প্রথমে count করো।

### Missing Age

```excel
=COUNTBLANK(G2:G100)
```

### Missing Phone

```excel
=COUNTBLANK(D2:D100)
```

---

# ⚠️ Missing Data কীভাবে Handle করবে?

সবসময় blank → 0 করা যাবে না।

উদাহরণ:

```text
Age = blank
```

❌

```text
Age = 0
```

করো না।

কারণ 0 একটি actual value হতে পারে এবং meaning বদলে যায়।

---

# 9️⃣ Missing Data Strategy

|Situation|Possible Action|
|---|---|
|Optional phone|Blank রাখা|
|Missing age|Source থেকে collect|
|Missing category|Unknown|
|Missing salary|Investigate|
|Critical ID missing|Reject/flag|

---

# 🔥 Part 9 — Duplicate Detection

Customer_ID unique হওয়া উচিত।

Formula:

```excel
=COUNTIF($A$2:$A$100,A2)>1
```

যদি:

```text
TRUE
```

তাহলে duplicate।

---

# 10️⃣ Duplicate Flag

```text
Duplicate_Status
```

Formula:

```excel
=IF(
   COUNTIF($A$2:$A$100,A2)>1,
   "Duplicate",
   "Unique"
)
```

Result:

|Customer_ID|Status|
|---|---|
|C001|Unique|
|C002|Unique|
|C003|Duplicate|
|C003|Duplicate|
|C004|Unique|

---

# 🧠 কিন্তু Duplicate মানেই Delete নয়!

এটা খুব গুরুত্বপূর্ণ।

ধরো:

```text
C003
```

দুইবার আছে।

দুটো row একই হলে:

```text
Remove Duplicate
```

করতে পারো।

কিন্তু:

```text
C003 | Hasan | Dhaka
C003 | Hasan | Chittagong
```

হলে?

❌ blindly delete করবে না।

এটা data quality issue হতে পারে।

---

# 🧹 Part 10 — Remove Duplicates

Excel:

```text
Data
↓
Remove Duplicates
```

তারপর business key নির্বাচন করো।

যেমন:

```text
Customer_ID
```

কিন্তু আগে নিশ্চিত হতে হবে:

> Customer_ID সত্যিই unique হওয়ার কথা কি না?

---

# 🔥 Part 11 — Email Validation

Email-এর basic validation করতে পারো।

উদাহরণ:

```excel
=AND(
   ISNUMBER(SEARCH("@",C2)),
   ISNUMBER(SEARCH(".",C2))
)
```

Result:

```text
TRUE
```

মানে basic pattern valid।

⚠️ এটা complete email validation নয়; শুধু basic quality check।

---

# 12️⃣ Email Status

```excel
=IF(C2="","Missing",
   IF(
      AND(
         ISNUMBER(SEARCH("@",C2)),
         ISNUMBER(SEARCH(".",C2))
      ),
      "Valid",
      "Invalid"
   )
)
```

---

# 🔥 Part 12 — Date Cleaning

Raw data:

```text
01/01/2026
04-01-2026
```

প্রথমে Excel এগুলো actual date হিসেবে recognize করেছে কিনা check করো।

Cell select করে:

```text
Home
→ Number Format
→ Short Date
```

অথবা:

```excel
=DATEVALUE(I2)
```

যদি date text হিসেবে stored থাকে।

---

# 13️⃣ Date Validation

ধরো future date allowed নয়।

Formula:

```excel
=I2<=TODAY()
```

যদি:

```text
TRUE
```

→ valid.

---

# 🧹 Part 13 — Find & Replace

ধরো:

```text
Male
male
M
```

Power Query বা Excel Find & Replace:

```text
Ctrl + H
```

এখানে:

```text
Find:
M

Replace:
Male
```

⚠️ সাবধান।

শুধু exact intended values replace করতে হবে, না হলে অন্য text-এর অংশও accidentally replace হতে পারে।

---

# 🔥 Part 14 — Flash Fill

ধরো:

```text
Full Name
Rahim Hasan
Karim Ahmed
```

তুমি পাশের column-এ লিখলে:

```text
Rahim
```

তারপর:

```text
Ctrl + E
```

Excel pattern বুঝে First Name fill করতে পারে।

---

# 🧠 কিন্তু Flash Fill বনাম Formula

|Flash Fill|Formula|
|---|---|
|Quick|Reproducible|
|Pattern-based|Rule-based|
|Manual transformation|Dynamic|
|One-time cleaning|Better for repeatable workflows|

Large/repeatable dataset হলে **Power Query** আরও ভালো।

---

# 🔥 Part 15 — Power Query দিয়ে একই Project

এখন একই cleaning Power Query-তে করলে workflow হবে:

```text
Raw Excel
    ↓
Get Data
    ↓
Power Query
    ↓
Changed Type
    ↓
Trim
    ↓
Clean
    ↓
Replace Values
    ↓
Remove Duplicates
    ↓
Remove Errors
    ↓
Custom Columns
    ↓
Final Dataset
```

এটাই Class 24-এর সাথে direct connection।

---

# 16️⃣ Power Query — Text Cleaning

Column select:

```text
Transform
↓
Format
↓
Trim
```

তারপর:

```text
Format
↓
Clean
```

তারপর প্রয়োজন অনুযায়ী:

```text
UPPERCASE
lowercase
Capitalize Each Word
```

---

# 17️⃣ Power Query — Replace City

Column:

```text
City
```

তারপর:

```text
Replace Values
```

করো:

```text
Chattogram → Chittagong
```

---

# 18️⃣ Power Query — Remove Duplicates

Customer_ID select:

```text
Home
↓
Remove Rows
↓
Remove Duplicates
```

---

# 19️⃣ Power Query — Missing Values

Blank value detect করে business rule অনুযায়ী:

```text
null
```

রাখতে পারো।

কিছু ক্ষেত্রে:

```text
null → Unknown
```

করতে পারো।

কিন্তু numeric fields-এ arbitrary `0` বসানোর আগে সাবধান।

---

# 🔥 Part 16 — Data Quality Report

Professional analyst শুধু clean dataset বানাবে না।

একটা **Data Quality Report** বানাবে।

Example:

|Check|Result|
|---|--:|
|Total Rows|1000|
|Duplicate IDs|12|
|Missing Phone|25|
|Missing Age|8|
|Invalid Age|4|
|Invalid Email|7|
|Invalid Date|3|
|City Issues|15|

এতে বোঝা যায় data কতটা reliable।

---

# 🏆 Part 17 — Data Quality Score

একটা simple concept:

ধরো:

```text
Total Records = 1000
Valid Records = 940
```

তাহলে:

```excel
=940/1000
```

অথবা:

```excel
=ValidRecords/TotalRecords
```

Result:

```text
94%
```

এটা একটি **simple data quality indicator** হিসেবে dashboard-এ দেখাতে পারো।

---

# 🔥 Full Data Cleaning Pipeline

এখন পুরো Class 26 একসাথে:

```text
                 RAW DATA
                     ↓
              BACKUP / COPY
                     ↓
              IDENTIFY ISSUES
                     ↓
        ┌────────────┼────────────┐
        ↓            ↓            ↓
      Text        Numeric        Dates
        ↓            ↓            ↓
     TRIM          VALUE        Date Type
     CLEAN         Validate     Validate
     PROPER
        ↓            ↓            ↓
        └────────────┼────────────┘
                     ↓
              STANDARDIZATION
                     ↓
              DUPLICATE CHECK
                     ↓
              MISSING DATA CHECK
                     ↓
               ERROR CHECK
                     ↓
              QUALITY REPORT
                     ↓
              CLEAN DATASET
                     ↓
              DATA ANALYSIS
```

---

# 🧪 Class 26 Final Project

এবার তোমার assignment একটু বড়।

## Dataset বানাও

কমপক্ষে:

```text
500 rows
```

Columns:

```text
Customer_ID
Name
Email
Phone
City
Gender
Age
Salary
Join_Date
Department
```

ইচ্ছা করে কিছু dirty data রাখবে:

- extra spaces
    
- uppercase/lowercase
    
- duplicate IDs
    
- missing values
    
- invalid ages
    
- inconsistent cities
    
- inconsistent gender
    
- numbers stored as text
    
- inconsistent dates
    
- invalid emails
    

---

# ✅ Cleaning Checklist

### Text

-  `TRIM`
    
-  `CLEAN`
    
-  `PROPER`
    
-  `LOWER`
    
-  Standardize values
    

### Numeric

-  Convert text → number
    
-  Detect invalid values
    
-  Check ranges
    

### Date

-  Convert to Date
    
-  Detect invalid dates
    
-  Check future dates
    

### Duplicates

-  Duplicate ID detection
    
-  Remove genuine duplicates
    
-  Investigate suspicious duplicates
    

### Missing Data

-  Count blanks
    
-  Decide business rule
    
-  Don't blindly replace blanks with zero
    

### Quality

-  Data Quality Report
    
-  Valid/Invalid flags
    
-  Final clean dataset
    

---

# 🧠 Class 26 Interview Questions

### Q1. What is data cleaning?

Raw/dirty data-কে consistent, valid এবং analysis-ready করার process।

### Q2. Why is TRIM used?

Extra spaces remove করার জন্য।

### Q3. Why shouldn't blank age always become 0?

কারণ blank এবং zero-এর business meaning আলাদা।

### Q4. Duplicate data কী?

একই logical record একাধিকবার থাকা।

### Q5. Append vs Merge?

```text
Append → Rows
Merge → Related columns/data
```

### Q6. Excel formula দিয়ে cleaning করা যায়?

হ্যাঁ।

কিন্তু repeatable large-scale transformation-এর জন্য Power Query বেশি suitable।

### Q7. Data validation কেন দরকার?

Invalid data যেন system-এ ঢুকতে না পারে বা detect করা যায়।

---

# 🎯 আজকের 10টি Practice Question

নিজে solve করার চেষ্টা করো।

### 1.

`" ATIAR RAHMAN "` → clean + proper case।

### 2.

`"ATIAR@GMAIL.COM "` → lowercase + trim।

### 3.

`"01711-123456"` → hyphen remove।

### 4.

`"dhaka"` → `Dhaka`।

### 5.

`"Chattogram"` → `Chittagong` standardize।

### 6.

Age 18–60 না হলে `"Invalid"` দেখাও।

### 7.

Duplicate Customer_ID detect করো।

### 8.

Missing Age এবং Missing Phone count করো।

### 9.

Invalid email detect করো।

### 10 ⭐

একটি **Data Quality Report** তৈরি করো যেখানে থাকবে:

```text
Total Rows
Duplicate Rows
Missing Values
Invalid Values
Valid Records
Data Quality %
```

---

# 🏆 Class 26-এর সবচেয়ে গুরুত্বপূর্ণ শিক্ষা

Data Analyst হওয়ার জন্য শুধু:

```text
SUM
AVERAGE
VLOOKUP
XLOOKUP
PivotTable
```

জানলেই হবে না।

বাস্তবে সবচেয়ে common workflow:

```text
Dirty Data
    ↓
Understand Data
    ↓
Find Problems
    ↓
Clean
    ↓
Validate
    ↓
Standardize
    ↓
Quality Check
    ↓
Analysis
```

আর তুমি এখন Excel-এর তিনটি বড় layer একসাথে ব্যবহার করতে পারছ:

```text
Excel Functions
      +
Power Query
      +
Power Pivot / DAX
      ↓
Professional Analytics Workflow
```

**পরবর্তী Class 27 → `Sales & Business Analytics Project`** — সেখানে clean dataset নিয়ে আমরা **Revenue, Profit, Growth, AOV, Top Products, Customer Analysis, KPI এবং business insights** বের করব।


-----
# 📊 Excel Mastery — Class 27

## Sales & Business Analytics Project

আজ থেকে আমরা শুধু Excel function শেখা না—**real-world business data analysis** করব।

### 🎯 আজকের Goal

একটা Sales dataset থেকে বের করব:

- Revenue
    
- Cost
    
- Profit
    
- Profit %
    
- AOV
    
- Growth %
    
- Top Products
    
- Customer Analysis
    
- KPI
    
- Business Insights
    

---

# 1️⃣ Real-World Dataset

Excel-এ নিচের data তৈরি করো:

|Order_ID|Date|Customer|City|Product|Category|Qty|Price|Cost|
|---|---|---|---|---|---|--:|--:|--:|
|O001|01-Jan-2026|Rahim|Dhaka|Laptop|Electronics|2|50000|40000|
|O002|03-Jan-2026|Karim|Chittagong|Mouse|Accessories|5|1000|700|
|O003|05-Jan-2026|Hasan|Dhaka|Monitor|Electronics|2|20000|15000|
|O004|08-Jan-2026|Jamil|Sylhet|Keyboard|Accessories|3|2000|1400|
|O005|12-Jan-2026|Nabil|Dhaka|Laptop|Electronics|1|50000|40000|
|O006|15-Jan-2026|Rahim|Dhaka|Mouse|Accessories|10|1000|700|
|O007|20-Jan-2026|Karim|Chittagong|Monitor|Electronics|3|20000|15000|
|O008|25-Jan-2026|Hasan|Dhaka|Keyboard|Accessories|4|2000|1400|
|O009|02-Feb-2026|Jamil|Sylhet|Laptop|Electronics|1|50000|40000|
|O010|05-Feb-2026|Nabil|Dhaka|Monitor|Electronics|2|20000|15000|
|O011|10-Feb-2026|Rahim|Dhaka|Laptop|Electronics|1|50000|40000|
|O012|15-Feb-2026|Karim|Chittagong|Mouse|Accessories|8|1000|700|
|O013|20-Feb-2026|Hasan|Dhaka|Laptop|Electronics|2|50000|40000|
|O014|25-Feb-2026|Jamil|Sylhet|Keyboard|Accessories|5|2000|1400|
|O015|28-Feb-2026|Nabil|Dhaka|Mouse|Accessories|10|1000|700|

---

# 2️⃣ Convert Data to Table

পুরো dataset select করো:

```text
Ctrl + T
```

তারপর Table-এর নাম দাও:

```text
SalesTable
```

এটা খুব important, কারণ আমরা পরে **Structured Reference** ব্যবহার করব।

---

# 3️⃣ Revenue Calculate

Revenue:

```text
Quantity × Price
```

নতুন column তৈরি করো:

```text
Revenue
```

Formula:

```excel
=[@Qty]*[@Price]
```

Example:

```text
2 × 50000 = 100000
```

---

# 4️⃣ Total Cost

আরেকটি column:

```text
Total Cost
```

Formula:

```excel
=[@Qty]*[@Cost]
```

যেমন:

```text
2 × 40000 = 80000
```

---

# 5️⃣ Profit

নতুন column:

```text
Profit
```

Formula:

```excel
=[@Revenue]-[@[Total Cost]]
```

অথবা:

```excel
=[@Qty]*([@Price]-[@Cost])
```

Example:

```text
Revenue = 100000
Cost    = 80000

Profit = 20000
```

---

# 6️⃣ Profit %

Business analysis-এ Profit % খুব important।

Formula:

```excel
=IFERROR([@Profit]/[@Revenue],0)
```

তারপর Percentage format দাও।

Example:

```text
Profit = 20,000
Revenue = 100,000

Profit % = 20%
```

---

# 7️⃣ KPI তৈরি করি

Dataset-এর উপরে বা পাশে KPI section বানাও।

### Total Revenue

```excel
=SUM(SalesTable[Revenue])
```

### Total Cost

```excel
=SUM(SalesTable[Total Cost])
```

### Total Profit

```excel
=SUM(SalesTable[Profit])
```

### Total Orders

```excel
=COUNTA(SalesTable[Order_ID])
```

### Total Quantity

```excel
=SUM(SalesTable[Qty])
```

### Average Order Value

```excel
=AVERAGE(SalesTable[Revenue])
```

---

# 8️⃣ AOV কী?

**AOV = Average Order Value**

মানে একজন customer/order-এ average কত টাকা sales হচ্ছে।

Formula:

```text
Total Revenue ÷ Total Orders
```

Excel:

```excel
=SUM(SalesTable[Revenue])/COUNTA(SalesTable[Order_ID])
```

অথবা:

```excel
=AVERAGE(SalesTable[Revenue])
```

---

# 9️⃣ City-wise Sales

এখন জানতে চাই:

> কোন city থেকে সবচেয়ে বেশি sales হচ্ছে?

Formula:

### Dhaka

```excel
=SUMIF(SalesTable[City],"Dhaka",SalesTable[Revenue])
```

### Chittagong

```excel
=SUMIF(SalesTable[City],"Chittagong",SalesTable[Revenue])
```

### Sylhet

```excel
=SUMIF(SalesTable[City],"Sylhet",SalesTable[Revenue])
```

আরও professional way:

|City|Revenue|
|---|--:|
|Dhaka|formula|
|Chittagong|formula|
|Sylhet|formula|

B2:

```excel
=SUMIF(SalesTable[City],A2,SalesTable[Revenue])
```

তারপর নিচে drag করো।

---

# 🔟 Category-wise Sales

|Category|Revenue|
|---|--:|
|Electronics|formula|
|Accessories|formula|

Formula:

```excel
=SUMIF(SalesTable[Category],A2,SalesTable[Revenue])
```

এখানে A2 যদি `Electronics` হয় তাহলে Electronics-এর total revenue আসবে।

---

# 1️⃣1️⃣ Product-wise Sales

|Product|Revenue|
|---|--:|
|Laptop||
|Monitor||
|Mouse||
|Keyboard||

Formula:

```excel
=SUMIF(SalesTable[Product],A2,SalesTable[Revenue])
```

এখন আমরা বুঝতে পারব:

> কোন product সবচেয়ে বেশি revenue generate করছে?

---

# 1️⃣2️⃣ Top Product

Product revenue table তৈরি করার পর:

```text
Data
→ Sort
→ Largest to Smallest
```

তাহলে:

```text
Laptop
Monitor
Mouse
Keyboard
```

এর মতো ranking দেখতে পারবে।

---

# 1️⃣3️⃣ Customer Analysis

একইভাবে:

|Customer|Revenue|
|---|--:|
|Rahim||
|Karim||
|Hasan||
|Jamil||
|Nabil||

Formula:

```excel
=SUMIF(SalesTable[Customer],A2,SalesTable[Revenue])
```

এতে বের হবে:

> কোন customer সবচেয়ে বেশি revenue দিয়েছে?

---

# 1️⃣4️⃣ Customer Order Count

শুধু revenue নয়, customer কতগুলো order করেছে সেটাও জানতে হবে।

Formula:

```excel
=COUNTIF(SalesTable[Customer],A2)
```

Example:

|Customer|Orders|
|---|--:|
|Rahim|3|
|Karim|3|
|Hasan|3|
|Jamil|3|
|Nabil|3|

---

# 1️⃣5️⃣ High-Value Order

ধরি:

```text
Revenue >= 50000
```

তাহলে High Value।

New column:

```text
Order Type
```

Formula:

```excel
=IF([@Revenue]>=50000,"High Value","Normal")
```

Result:

```text
100000 → High Value
5000   → Normal
40000  → Normal
```

---

# 1️⃣6️⃣ Monthly Sales

এখন business-এর খুব important question:

> January বনাম February—কোন মাসে বেশি sales?

নতুন column:

```text
Month
```

Formula:

```excel
=TEXT([@Date],"mmmm")
```

তারপর:

|Month|Revenue|
|---|--:|
|January||
|February||

Formula:

```excel
=SUMIF(SalesTable[Month],A2,SalesTable[Revenue])
```

---

# 1️⃣7️⃣ Growth %

ধরো:

|Month|Sales|
|---|--:|
|January|500000|
|February|700000|

Growth:

```text
(February - January) / January
```

Excel:

```excel
=(B3-B2)/B2
```

অথবা:

```excel
=IFERROR((B3-B2)/B2,0)
```

Percentage format:

```text
40%
```

মানে sales **40% বৃদ্ধি পেয়েছে**।

---

# 1️⃣8️⃣ Business Insight

এটাই সবচেয়ে important part।

Excel শুধু calculation করার জন্য না।

Data থেকে **decision** বের করতে হবে।

Example:

### Insight 1

যদি Dhaka revenue সবচেয়ে বেশি হয়:

> Dhaka is the strongest sales market.

### Insight 2

যদি Laptop সবচেয়ে বেশি revenue generate করে:

> Laptop is the company's top-performing product.

### Insight 3

যদি February sales January থেকে বেশি হয়:

> Sales performance improved in February.

### Insight 4

যদি Accessories-এর profit margin বেশি হয়:

> Accessories may be a high-margin product category.

---

# 1️⃣9️⃣ Conditional Formatting

Revenue column select করে:

```text
Home
→ Conditional Formatting
→ Data Bars
```

ব্যবহার করো।

তাহলে visually বুঝতে পারবে কোন order বড়।

Profit column-এ:

```text
Color Scale
```

ব্যবহার করতে পারো।

---

# 2️⃣0️⃣ PivotTable দিয়ে Analysis

এখন একই data PivotTable দিয়ে করব।

```text
Insert
→ PivotTable
```

### Analysis 1 — City Sales

```text
Rows    → City
Values  → Revenue
```

---

### Analysis 2 — Product Sales

```text
Rows    → Product
Values  → Revenue
```

---

### Analysis 3 — Category Profit

```text
Rows    → Category
Values  → Profit
```

---

### Analysis 4 — Customer Sales

```text
Rows    → Customer
Values  → Revenue
```

---

### Analysis 5 — Monthly Trend

```text
Rows    → Date
Values  → Revenue
```

Date-কে Month অনুযায়ী Group করতে পারো।

---

# 2️⃣1️⃣ Charts

এখন PivotTable থেকে charts তৈরি করো।

### Chart 1

**Monthly Sales**

→ Line Chart

কারণ time trend দেখতে চাই।

### Chart 2

**City Sales**

→ Bar Chart

### Chart 3

**Product Sales**

→ Column Chart

### Chart 4

**Category Contribution**

→ Pie/Doughnut Chart

---

# 2️⃣2️⃣ Final Mini Dashboard

একটি নতুন sheet তৈরি করো:

```text
Dashboard
```

Layout:

```text
┌──────────────────────────────────────┐
│          SALES DASHBOARD             │
├──────────┬──────────┬──────────┬─────┤
│ Revenue  │ Profit   │ Orders   │ AOV │
├──────────┴──────────┴──────────┴─────┤
│          Monthly Sales Trend          │
├───────────────────┬──────────────────┤
│   City Sales      │ Product Sales     │
├───────────────────┼──────────────────┤
│ Category Sales    │ Customer Sales    │
└───────────────────┴──────────────────┘
```

এটাই তোমার প্রথম **Business Analytics Dashboard**।

---

# 🧠 Class 27-এর Core Concepts

|Concept|Meaning|
|---|---|
|Revenue|Sales থেকে পাওয়া টাকা|
|Cost|Product-এর খরচ|
|Profit|Revenue − Cost|
|Profit %|Profit / Revenue|
|AOV|Average Order Value|
|KPI|গুরুত্বপূর্ণ business metric|
|Growth %|সময়ের সাথে পরিবর্তন|
|Top Product|সবচেয়ে বেশি performing product|
|Customer Analysis|Customer-wise performance|
|Business Insight|Data থেকে সিদ্ধান্ত|

---

# 🎯 Class 27 Assignment

এই project নিজে Excel-এ তৈরি করো।

### Part A — Calculations

1. Revenue
    
2. Total Cost
    
3. Profit
    
4. Profit %
    
5. Order Type
    
6. Month
    

### Part B — KPI

7. Total Revenue
    
8. Total Cost
    
9. Total Profit
    
10. Total Orders
    
11. Total Quantity
    
12. AOV
    

### Part C — Analysis

13. City-wise Revenue
    
14. Category-wise Revenue
    
15. Product-wise Revenue
    
16. Customer-wise Revenue
    
17. Customer-wise Order Count
    
18. Monthly Revenue
    
19. Monthly Growth %
    

### Part D — Visualization

20. Monthly Sales Line Chart
    
21. City Sales Bar Chart
    
22. Product Sales Column Chart
    
23. Category Sales Chart
    
24. Mini Dashboard
    

### Part E — Business Insights

শেষে **কমপক্ষে 5টি insight** লিখবে।

---

## 🧪 Class 27 Quiz

**1. Revenue-এর basic formula কোনটি?**

A. Price + Qty  
B. Price × Qty  
C. Price − Qty  
D. Price / Qty

**2. Profit = ?**

A. Cost − Revenue  
B. Revenue + Cost  
C. Revenue − Cost  
D. Revenue × Cost

**3. AOV-এর অর্থ কী?**

A. Average Overall Value  
B. Average Order Value  
C. Annual Order Value  
D. Average Output Value

**4. Monthly sales trend দেখাতে কোন chart সবচেয়ে suitable?**

A. Line  
B. Pie  
C. Doughnut  
D. Scatter

**5. `SUMIF` কী কাজে লাগে?**

A. Text clean  
B. Conditional total  
C. Lookup  
D. Date calculation

**6. `COUNTIF` কী করে?**

A. Conditional count  
B. Conditional sum  
C. Average  
D. Lookup

**7. Profit percentage-এর formula কোনটি?**

A. Profit × Revenue  
B. Revenue / Profit  
C. Profit / Revenue  
D. Cost / Profit

**8. কোনটি KPI-এর example?**

A. Total Revenue  
B. Cell Color  
C. Font Size  
D. Column Width

**9. Product-wise revenue বের করতে কোন function ব্যবহার করা যায়?**

A. SUMIF  
B. LEFT  
C. LEN  
D. TODAY

**10. Business Analytics-এর final objective কী?**

A. শুধু সুন্দর Excel বানানো  
B. শুধু formula মুখস্থ করা  
C. Data থেকে useful business decision/insight বের করা  
D. শুধু chart বানানো

**তুমি 1–10-এর উত্তর দাও। এরপর আমরা Class 28-এ যাব: _HR / Employee Analytics Project_ — যেখানে Salary, Department, Age, Experience, Performance, Attrition এবং Employee KPI নিয়ে real-world analysis করব।**

----
# 📊 Excel Mastery — Class 28

## 👨‍💼 HR / Employee Analytics Project

আজ আমরা **Sales Analytics থেকে HR Analytics**-এ যাব। এই project-এর মাধ্যমে Excel-এর আগের শেখা বিষয়গুলো বাস্তবভাবে ব্যবহার করব:

**Cleaning → Formula → IF → SUMIF/COUNTIF → AVERAGEIF → PivotTable → Charts → KPI → Business Insight**

---

# 🎯 Class 28 Goal

Employee data থেকে বের করব:

- Total Employees
    
- Average Salary
    
- Department-wise Employees
    
- Department-wise Salary
    
- Average Age
    
- Experience
    
- Performance
    
- Employee Status
    
- Salary Level
    
- Attrition Rate
    
- Top-performing employees
    
- HR Dashboard
    

---

# 1️⃣ Employee Dataset

Excel-এ নিচের dataset তৈরি করো:

|ID|Name|Department|City|Age|Experience|Salary|Performance|Attrition|
|---|---|---|---|--:|--:|--:|--:|---|
|E001|Rahim|IT|Dhaka|25|2|45000|85|No|
|E002|Karim|HR|Dhaka|30|5|55000|78|No|
|E003|Hasan|IT|Chittagong|28|4|60000|92|No|
|E004|Jamil|Finance|Sylhet|35|8|70000|88|No|
|E005|Nabil|Marketing|Dhaka|27|3|40000|72|Yes|
|E006|Sakib|IT|Dhaka|32|7|75000|95|No|
|E007|Fahim|HR|Chittagong|29|4|50000|80|No|
|E008|Rafi|Finance|Dhaka|40|12|90000|91|No|
|E009|Tanvir|Marketing|Sylhet|26|2|38000|68|Yes|
|E010|Arif|IT|Dhaka|24|1|35000|75|No|
|E011|Imran|Finance|Chittagong|38|10|85000|94|No|
|E012|Shuvo|HR|Dhaka|33|6|62000|83|No|
|E013|Rakib|Marketing|Dhaka|31|5|48000|76|Yes|
|E014|Siam|IT|Sylhet|29|3|52000|89|No|
|E015|Mahin|Finance|Dhaka|36|9|78000|87|No|

---

# 2️⃣ Convert to Table

পুরো dataset select করো:

```text
Ctrl + T
```

Table-এর নাম:

```text
EmployeeTable
```

এখন আমরা structured reference ব্যবহার করব।

---

# 3️⃣ Employee Status

নতুন column:

```text
Status
```

ধরি Performance:

- 80 বা তার বেশি → Excellent
    
- 70–79 → Good
    
- 60–69 → Average
    
- <60 → Poor
    

Formula:

```excel
=IF([@Performance]>=80,"Excellent",
IF([@Performance]>=70,"Good",
IF([@Performance]>=60,"Average","Poor")))
```

Example:

```text
95 → Excellent
85 → Excellent
75 → Good
68 → Average
```

---

# 4️⃣ Salary Level

নতুন column:

```text
Salary Level
```

Rule:

```text
>= 70000 → High
>= 50000 → Medium
< 50000 → Low
```

Formula:

```excel
=IF([@Salary]>=70000,"High",
IF([@Salary]>=50000,"Medium","Low"))
```

---

# 5️⃣ Experience Level

নতুন column:

```text
Experience Level
```

Rule:

```text
>= 10 → Senior
>= 5 → Mid-Level
< 5 → Junior
```

Formula:

```excel
=IF([@Experience]>=10,"Senior",
IF([@Experience]>=5,"Mid-Level","Junior"))
```

---

# 6️⃣ Age Group

নতুন column:

```text
Age Group
```

Formula:

```excel
=IF([@Age]<25,"Young",
IF([@Age]<=35,"Adult","Senior"))
```

এখানে **Senior** বলতে age group বোঝাচ্ছি, job seniority নয়।

---

# 7️⃣ Basic HR KPIs

এখন Dashboard-এর জন্য KPI তৈরি করি।

### Total Employees

```excel
=COUNTA(EmployeeTable[ID])
```

Result:

```text
15
```

---

### Average Salary

```excel
=AVERAGE(EmployeeTable[Salary])
```

---

### Maximum Salary

```excel
=MAX(EmployeeTable[Salary])
```

---

### Minimum Salary

```excel
=MIN(EmployeeTable[Salary])
```

---

### Average Age

```excel
=AVERAGE(EmployeeTable[Age])
```

---

### Average Experience

```excel
=AVERAGE(EmployeeTable[Experience])
```

---

# 8️⃣ Department-wise Employee Count

Table বানাও:

|Department|Employees|
|---|--:|
|IT||
|HR||
|Finance||
|Marketing||

Formula:

```excel
=COUNTIF(EmployeeTable[Department],A2)
```

তারপর নিচে drag করো।

এখন বুঝতে পারবে কোন department-এ কতজন employee আছে।

---

# 9️⃣ Department-wise Average Salary

|Department|Average Salary|
|---|--:|
|IT||
|HR||
|Finance||
|Marketing||

Formula:

```excel
=AVERAGEIF(EmployeeTable[Department],A2,EmployeeTable[Salary])
```

এটা HR Analytics-এ খুব useful।

---

# 🔟 Department-wise Total Salary

```excel
=SUMIF(EmployeeTable[Department],A2,EmployeeTable[Salary])
```

এতে বোঝা যাবে:

> কোন department-এর জন্য company-এর salary expense বেশি?

---

# 1️⃣1️⃣ Excellent Employee Count

Performance status অনুযায়ী:

```excel
=COUNTIF(EmployeeTable[Status],"Excellent")
```

---

# 1️⃣2️⃣ Department + Performance Analysis

ধরি জানতে চাই:

> IT department-এ কয়জন Excellent employee আছে?

```excel
=COUNTIFS(
EmployeeTable[Department],"IT",
EmployeeTable[Status],"Excellent"
)
```

আর dynamic version:

```excel
=COUNTIFS(
EmployeeTable[Department],A2,
EmployeeTable[Status],"Excellent"
)
```

---

# 1️⃣3️⃣ High Salary Employee Count

```excel
=COUNTIF(EmployeeTable[Salary Level],"High")
```

---

# 1️⃣4️⃣ Attrition Analysis

এখন HR-এর সবচেয়ে গুরুত্বপূর্ণ metrics-এর একটি।

**Attrition** বলতে এখানে employee company ছেড়ে যাওয়ার status বোঝাচ্ছি।

আমাদের dataset-এ:

```text
Yes = Left
No = Stayed
```

### Total Attrition

```excel
=COUNTIF(EmployeeTable[Attrition],"Yes")
```

---

# 1️⃣5️⃣ Attrition Rate

Formula:

```text
Attrition Rate =
Employees who left
-------------------
Total Employees
```

Excel:

```excel
=COUNTIF(EmployeeTable[Attrition],"Yes")/COUNTA(EmployeeTable[ID])
```

তারপর Percentage format দাও।

---

# 1️⃣6️⃣ Department-wise Attrition

|Department|Attrition|
|---|--:|
|IT||
|HR||
|Finance||
|Marketing||

Formula:

```excel
=COUNTIFS(
EmployeeTable[Department],A2,
EmployeeTable[Attrition],"Yes"
)
```

এখন দেখতে পারবে কোন department-এ attrition বেশি।

---

# 1️⃣7️⃣ High Performer + Attrition

একটি গুরুত্বপূর্ণ HR question:

> High-performing employee কি company ছাড়ছে?

Formula:

```excel
=COUNTIFS(
EmployeeTable[Status],"Excellent",
EmployeeTable[Attrition],"Yes"
)
```

এটা HR-এর জন্য গুরুত্বপূর্ণ warning indicator হতে পারে।

---

# 1️⃣8️⃣ Salary vs Performance

এখন আমরা দেখতে চাই:

> বেশি salary পাওয়া employees কি বেশি perform করছে?

একটি summary তৈরি করো:

|Employee|Salary|Performance|
|---|--:|--:|
|Rahim|45000|85|
|Karim|55000|78|
|Hasan|60000|92|
|...|...|...|

তারপর:

```text
Insert
→ Scatter Chart
```

এখানে:

**X-axis = Salary**

**Y-axis = Performance**

এতে relationship visually দেখতে পারবে।

⚠️ তবে chart দেখে সরাসরি বলা যাবে না যে salary-ই performance-এর কারণ। এটা শুধু relationship দেখায়।

---

# 1️⃣9️⃣ Department Performance

|Department|Average Performance|
|---|--:|
|IT||
|HR||
|Finance||
|Marketing||

Formula:

```excel
=AVERAGEIF(
EmployeeTable[Department],
A2,
EmployeeTable[Performance]
)
```

এখন department-wise performance compare করা যাবে।

---

# 2️⃣0️⃣ PivotTable Analysis

এবার professional analysis।

## PivotTable 1 — Department Overview

```text
Rows:
Department

Values:
ID → Count
Salary → Average
Performance → Average
```

তাহলে একসাথে দেখতে পারবে:

|Department|Employees|Avg Salary|Avg Performance|
|---|--:|--:|--:|
|IT||||
|HR||||
|Finance||||
|Marketing||||

---

# 2️⃣1️⃣ PivotTable 2 — Attrition

```text
Rows → Department
Columns → Attrition
Values → ID → Count
```

তাহলে দেখতে পারবে:

```text
Department | No | Yes
IT         |    |    
HR         |    |
Finance    |    |
Marketing  |    |
```

এটা খুব useful HR report।

---

# 2️⃣2️⃣ PivotTable 3 — Salary Level

```text
Rows → Department
Columns → Salary Level
Values → ID → Count
```

এতে বোঝা যাবে প্রতিটি department-এ:

```text
Low
Medium
High
```

salary employees কতজন।

---

# 2️⃣3️⃣ PivotTable 4 — Performance

```text
Rows → Department
Columns → Status
Values → ID → Count
```

এতে:

```text
Excellent
Good
Average
Poor
```

employee distribution দেখতে পারবে।

---

# 2️⃣4️⃣ HR Charts

### Chart 1 — Employees by Department

**Bar Chart**

---

### Chart 2 — Average Salary by Department

**Column Chart**

---

### Chart 3 — Average Performance

**Column/Bar Chart**

---

### Chart 4 — Attrition

**Doughnut/Pie Chart**

---

### Chart 5 — Salary vs Performance

**Scatter Chart**

---

# 2️⃣5️⃣ HR Dashboard

একটি নতুন sheet:

```text
HR Dashboard
```

Layout:

```text
┌───────────────────────────────────────────┐
│             HR ANALYTICS DASHBOARD        │
├──────────┬──────────┬──────────┬─────────┤
│ Employees│ Avg Salary│ Avg Perf │Attrition│
├──────────┴──────────┴──────────┴─────────┤
│         Employees by Department           │
├──────────────────────┬────────────────────┤
│ Average Salary       │ Average Performance │
├──────────────────────┼────────────────────┤
│ Attrition Analysis   │ Salary vs Performance│
└──────────────────────┴────────────────────┘
```

---

# 2️⃣6️⃣ Conditional Formatting

### Performance

Performance column select করো:

```text
Conditional Formatting
→ Color Scale
```

---

### Salary

Salary:

```text
Conditional Formatting
→ Data Bars
```

---

### Attrition

`Yes` values highlight করো।

```text
Conditional Formatting
→ Highlight Cells Rules
→ Text That Contains
```

---

# 2️⃣7️⃣ Business Insights

এটাই সবচেয়ে গুরুত্বপূর্ণ।

শুধু বলবে না:

> IT has 5 employees.

বরং বলবে:

> **IT is one of the largest departments and also shows strong average performance.**

আরও examples:

### Insight 1

যদি কোনো department-এর average salary সবচেয়ে বেশি:

> Finance has the highest average salary among the departments.

### Insight 2

যদি Marketing-এর attrition বেশি:

> Marketing shows comparatively higher employee attrition and may require HR investigation.

### Insight 3

যদি IT-এর performance বেশি:

> IT demonstrates strong average employee performance.

### Insight 4

যদি high-performing employee attrition থাকে:

> The company should investigate why some high-performing employees are leaving.

### Insight 5

যদি salary ও performance-এর relationship দুর্বল হয়:

> Salary alone may not explain employee performance; other factors should be analyzed.

---

# 🧠 Class 28-এর Important Formula Cheat Sheet

|কাজ|Formula|
|---|---|
|Employee count|`COUNTA()`|
|Average salary|`AVERAGE()`|
|Total salary|`SUM()`|
|Department count|`COUNTIF()`|
|Department salary|`SUMIF()`|
|Department avg salary|`AVERAGEIF()`|
|Multiple conditions|`COUNTIFS()`|
|Employee classification|`IF()`|
|Attrition count|`COUNTIF()`|
|Attrition rate|Attrition / Total|
|Relationship|Scatter Chart|

---

# 🎯 Class 28 Assignment

নিজে Excel-এ complete project তৈরি করো।

### Part A — Employee Classification

1. Status
    
2. Salary Level
    
3. Experience Level
    
4. Age Group
    

### Part B — KPI

5. Total Employees
    
6. Average Salary
    
7. Maximum Salary
    
8. Minimum Salary
    
9. Average Age
    
10. Average Experience
    
11. Attrition Rate
    

### Part C — Analysis

12. Department employee count
    
13. Department average salary
    
14. Department total salary
    
15. Department average performance
    
16. Department attrition
    
17. Excellent employee count
    
18. High salary employee count
    

### Part D — Charts

19. Employees by Department
    
20. Average Salary by Department
    
21. Average Performance by Department
    
22. Attrition Chart
    
23. Salary vs Performance Scatter Chart
    

### Part E — Dashboard

একটি professional **HR Analytics Dashboard** তৈরি করো।

### Part F — Insights

কমপক্ষে **5টি business insight** লিখবে।

---

# 🧪 Class 28 Quiz

**1.** Employee count করার জন্য কোন function সবচেয়ে suitable?

A. SUM  
B. COUNTA  
C. MAX  
D. LEFT

**2.** Department অনুযায়ী average salary বের করতে?

A. SUMIF  
B. COUNTIF  
C. AVERAGEIF  
D. XLOOKUP

**3.** Multiple conditions-এর জন্য?

A. COUNTIFS  
B. COUNT  
C. SUM  
D. LEN

**4.** Attrition Rate-এর basic formula কী?

A. Total Employees / Left Employees  
B. Left Employees / Total Employees  
C. Salary / Employees  
D. Performance / Employees

**5.** Salary ও Performance-এর relationship দেখতে কোন chart ভালো?

A. Pie  
B. Line  
C. Scatter  
D. Doughnut

**6.** `IF()` function এখানে কী কাজে ব্যবহার করেছি?

A. Employee classification  
B. Chart তৈরি  
C. Sorting  
D. Filtering

**7.** `SUMIF()` কী বের করতে পারে?

A. Department-wise total salary  
B. Average age  
C. Employee name  
D. Date

**8.** `COUNTIFS()` কী করতে পারে?

A. Multiple-condition counting  
B. Text cleaning  
C. Date formatting  
D. Chart formatting

**9.** HR Dashboard-এর উদ্দেশ্য কী?

A. শুধু decoration  
B. শুধু formula দেখানো  
C. HR data থেকে useful information ও insight পাওয়া  
D. শুধু employee নাম দেখানো

**10.** High-performing employee চলে গেলে সেটা কী হতে পারে?

A. Potential HR warning signal  
B. Always good news  
C. Formula error  
D. Excel error

**তুমি চাইলে এখন 1–10-এর উত্তর দাও। তারপর Class 29-এ আমরা আরও গুরুত্বপূর্ণ project করব: 📦 _Inventory & Supply Chain Analytics_ — Stock, Reorder Level, Inventory Turnover, Dead Stock, Stock Value, ABC Analysis এবং Inventory Dashboard।**


----
# 📦 Excel Mastery — Class 29

## Inventory & Supply Chain Analytics Project

আজ আমরা Excel দিয়ে একটি **real-world Inventory Management System-এর analytics part** তৈরি করব।

এখানে শিখব:

- Stock Quantity
    
- Stock Value
    
- Sales/Usage
    
- Reorder Level
    
- Reorder Status
    
- Inventory Turnover
    
- Dead Stock
    
- Low Stock
    
- ABC Analysis
    
- Supplier Analysis
    
- Inventory KPI
    
- Inventory Dashboard
    

---

# 🎯 1. Inventory কী?

সহজভাবে:

> **Company-এর কাছে বর্তমানে কী কী product কত quantity আছে—সেটাই Inventory।**

উদাহরণ:

|Product|Stock|
|---|--:|
|Laptop|20|
|Mouse|100|
|Keyboard|50|

---

# 2️⃣ Real-World Dataset

Excel-এ এই dataset তৈরি করো:

|Product_ID|Product|Category|Supplier|Unit Cost|Unit Price|Opening Stock|Purchased|Sold|Reorder Level|
|---|---|---|---|--:|--:|--:|--:|--:|--:|
|P001|Laptop|Electronics|ABC Ltd|40000|50000|20|15|12|10|
|P002|Mouse|Accessories|XYZ Ltd|700|1000|100|50|90|30|
|P003|Keyboard|Accessories|XYZ Ltd|1400|2000|60|30|50|20|
|P004|Monitor|Electronics|ABC Ltd|15000|20000|30|20|25|15|
|P005|Printer|Electronics|Tech Ltd|12000|15000|25|10|20|10|
|P006|Headphone|Accessories|Sound Ltd|2000|3000|40|20|10|15|
|P007|Webcam|Accessories|Tech Ltd|2500|4000|30|10|25|15|
|P008|SSD|Storage|ABC Ltd|5000|7000|35|20|30|15|
|P009|RAM|Storage|XYZ Ltd|3000|4500|50|25|40|20|
|P010|Router|Networking|Net Ltd|2500|4000|45|20|15|15|

---

# 3️⃣ Table তৈরি

Dataset select করো:

```text
Ctrl + T
```

Table name:

```text
InventoryTable
```

এখন structured references ব্যবহার করতে পারবে।

---

# 4️⃣ Current Stock

সবচেয়ে গুরুত্বপূর্ণ formula:

```text
Current Stock
=
Opening Stock + Purchased - Sold
```

নতুন column:

**Current Stock**

Formula:

```excel
=[@[Opening Stock]]+[@Purchased]-[@Sold]
```

উদাহরণ:

Laptop:

```text
20 + 15 - 12
= 23
```

তাহলে Laptop-এর current stock:

**23**

---

# 5️⃣ Stock Value

এখন জানতে চাই:

> বর্তমানে warehouse-এ থাকা stock-এর মূল্য কত?

Formula:

```text
Current Stock × Unit Cost
```

নতুন column:

**Stock Value**

```excel
=[@[Current Stock]]*[@[Unit Cost]]
```

Laptop:

```text
23 × 40,000
= 920,000
```

অর্থাৎ Laptop-এর current inventory cost value:

**৳920,000**

---

# 6️⃣ Potential Sales Value

Current stock যদি সব বিক্রি হয় তাহলে সম্ভাব্য sales value কত?

```text
Current Stock × Unit Price
```

Formula:

```excel
=[@[Current Stock]]*[@[Unit Price]]
```

Laptop:

```text
23 × 50,000
= 1,150,000
```

---

# 7️⃣ Potential Profit

Potential profit:

```text
Potential Sales Value - Stock Value
```

Formula:

```excel
=[@[Potential Sales Value]]-[@[Stock Value]]
```

অথবা:

```excel
=[@[Current Stock]]*([@[Unit Price]]-[@[Unit Cost]])
```

---

# 8️⃣ Reorder Status

এখন সবচেয়ে practical question:

> কোন product আবার কিনতে হবে?

যদি:

```text
Current Stock <= Reorder Level
```

তাহলে:

```text
REORDER
```

নতুন column:

**Reorder Status**

Formula:

```excel
=IF([@[Current Stock]]<=[@[Reorder Level]],"REORDER","OK")
```

---

### Example

ধরো:

```text
Current Stock = 8
Reorder Level = 10
```

তাহলে:

```text
8 <= 10
```

Result:

**REORDER**

---

# 9️⃣ Low Stock

আরও একটি classification করতে পারো।

Rule:

```text
Current Stock <= Reorder Level
→ Low Stock

Otherwise
→ Normal
```

এখানে Reorder Status-ই যথেষ্ট, তাই duplicate column না করলেও হবে।

---

# 🔟 Reorder Quantity

ধরি company চায় minimum stock রাখতে:

```text
Target Stock = 50
```

তাহলে reorder quantity:

```text
Target Stock - Current Stock
```

নতুন cell-এ Target Stock রাখো:

```text
B2 = 50
```

Formula:

```excel
=MAX(0,$B$2-[@[Current Stock]])
```

উদাহরণ:

```text
Target = 50
Current = 23

Reorder Qty = 27
```

---

# 1️⃣1️⃣ Total Inventory Value

সব product-এর stock value যোগ:

```excel
=SUM(InventoryTable[Stock Value])
```

এটাই তোমার একটি গুরুত্বপূর্ণ **Inventory KPI**।

---

# 1️⃣2️⃣ Total Products

```excel
=COUNTA(InventoryTable[Product_ID])
```

---

# 1️⃣3️⃣ Total Current Stock

```excel
=SUM(InventoryTable[Current Stock])
```

---

# 1️⃣4️⃣ Total Units Sold

```excel
=SUM(InventoryTable[Sold])
```

---

# 1️⃣5️⃣ Total Purchase

```excel
=SUM(InventoryTable[Purchased])
```

---

# 1️⃣6️⃣ Reorder Product Count

```excel
=COUNTIF(InventoryTable[Reorder Status],"REORDER")
```

এতে বুঝবে কতগুলো product পুনরায় order করা দরকার।

---

# 1️⃣7️⃣ Category-wise Inventory

ধরো:

|Category|Stock Value|
|---|--:|
|Electronics||
|Accessories||
|Storage||
|Networking||

Formula:

```excel
=SUMIF(
InventoryTable[Category],
A2,
InventoryTable[Stock Value]
)
```

এখন বুঝতে পারবে কোন category-তে company-এর বেশি টাকা inventory হিসেবে আটকে আছে।

---

# 1️⃣8️⃣ Supplier Analysis

Supplier-wise stock value:

|Supplier|Stock Value|
|---|--:|
|ABC Ltd||
|XYZ Ltd||
|Tech Ltd||
|Sound Ltd||
|Net Ltd||

Formula:

```excel
=SUMIF(
InventoryTable[Supplier],
A2,
InventoryTable[Stock Value]
)
```

এতে supplier dependency সম্পর্কে ধারণা পাওয়া যায়।

---

# 1️⃣9️⃣ Inventory Turnover

এটি খুব গুরুত্বপূর্ণ business metric।

সহজভাবে:

> Inventory কত দ্রুত বিক্রি/ব্যবহৃত হচ্ছে?

Basic formula:

```text
Inventory Turnover
=
Cost of Goods Sold
÷
Average Inventory
```

আমাদের simplified dataset-এ একটা approximate version practice করতে পারি।

### COGS

Sold × Unit Cost:

নতুন column:

**COGS**

```excel
=[@Sold]*[@[Unit Cost]]
```

---

# 2️⃣0️⃣ Average Inventory

Simple approximation:

```text
(Opening Stock + Current Stock) / 2
```

নতুন column:

**Average Inventory**

```excel
=([@[Opening Stock]]+[@[Current Stock]])/2
```

---

# 2️⃣1️⃣ Inventory Turnover Formula

```excel
=IFERROR(
[@COGS]/[@[Average Inventory]],
0
)
```

### Example

যদি:

```text
COGS = 480000
Average Inventory = 860000
```

তাহলে:

```text
Turnover ≈ 0.56
```

⚠️ Real accounting analysis-এ period এবং inventory valuation-এর definition business অনুযায়ী ঠিক করতে হবে। আজকের formula শেখার উদ্দেশ্যে simplified version ব্যবহার করছি।

---

# 2️⃣2️⃣ Dead Stock

Dead stock বলতে সাধারণভাবে এমন inventory বোঝায় যা দীর্ঘসময় ধরে বিক্রি/ব্যবহৃত হচ্ছে না।

আমাদের dataset-এ `Sold` দিয়ে simple rule বানাই:

```text
Sold = 0
→ Dead Stock
```

Formula:

```excel
=IF([@Sold]=0,"Dead Stock","Active")
```

আমাদের current dataset-এ সব product-এর Sold > 0, তাই Dead Stock আসবে না।

Practice-এর জন্য একটি product-এর Sold:

```text
0
```

করে দেখো।

---

# 2️⃣3️⃣ Fast Moving vs Slow Moving

Sold quantity অনুযায়ী classification:

```text
Sold >= 50 → Fast Moving
Sold >= 20 → Medium Moving
Sold < 20 → Slow Moving
```

Formula:

```excel
=IF([@Sold]>=50,"Fast Moving",
IF([@Sold]>=20,"Medium Moving","Slow Moving"))
```

এতে inventory movement বুঝতে সুবিধা হবে।

---

# 2️⃣4️⃣ ABC Analysis — Important 🔥

Inventory management-এ **ABC Analysis** খুব useful।

মূল ধারণা:

### A Category

High-value products

→ বেশি attention

### B Category

Medium-value products

→ moderate attention

### C Category

Low-value products

→ comparatively less attention

---

# 2️⃣5️⃣ ABC Analysis-এর সহজ Version

Stock Value-এর উপর ভিত্তি করে ranking তৈরি করো।

নতুন column:

**Rank**

```excel
=RANK.EQ(
[@[Stock Value]],
InventoryTable[Stock Value],
0
)
```

এখানে:

```text
1 = Highest Stock Value
2 = Second Highest
...
```

---

# 2️⃣6️⃣ ABC Classification

Practice-এর জন্য:

```text
Rank 1–3 → A
Rank 4–7 → B
Rank 8–10 → C
```

Formula:

```excel
=IF([@Rank]<=3,"A",
IF([@Rank]<=7,"B","C"))
```

⚠️ এটা **learning simplification**। Real ABC analysis সাধারণত cumulative inventory value contribution/percentage-এর ভিত্তিতে করা হয়।

---

# 2️⃣7️⃣ Conditional Formatting

### Reorder

`Reorder Status` column select করো:

```text
Home
→ Conditional Formatting
→ Text that Contains
→ REORDER
```

---

### Stock Value

```text
Conditional Formatting
→ Data Bars
```

---

### Inventory Turnover

```text
Color Scale
```

---

# 2️⃣8️⃣ PivotTable — Inventory Analysis

## PivotTable 1

Department-এর বদলে এখানে:

```text
Rows → Category
Values → Stock Value
```

Result:

> Category-wise inventory investment

---

## PivotTable 2

```text
Rows → Supplier
Values → Stock Value
```

Result:

> Supplier-wise inventory value

---

## PivotTable 3

```text
Rows → Product
Values → Sold
```

তারপর largest to smallest sort।

Result:

> Best-selling / fast-moving products

---

## PivotTable 4

```text
Rows → Reorder Status
Values → Product_ID → Count
```

Result:

```text
OK
REORDER
```

---

# 2️⃣9️⃣ Inventory Charts

### Chart 1 — Category Stock Value

**Column Chart**

---

### Chart 2 — Supplier Stock Value

**Bar Chart**

---

### Chart 3 — Product Sales Quantity

**Bar Chart**

---

### Chart 4 — Reorder Status

**Doughnut Chart**

---

# 3️⃣0️⃣ Inventory Dashboard

নতুন sheet:

```text
Inventory Dashboard
```

Layout:

```text
┌──────────────────────────────────────────┐
│       INVENTORY ANALYTICS DASHBOARD      │
├──────────┬──────────┬──────────┬────────┤
│ Products │ Stock Qty│ Stock Value│Reorder│
├──────────┴──────────┴──────────┴────────┤
│          Category Stock Value             │
├─────────────────────┬────────────────────┤
│ Supplier Analysis   │ Product Sales      │
├─────────────────────┼────────────────────┤
│ Reorder Status      │ Fast/Slow Moving   │
└─────────────────────┴────────────────────┘
```

---

# 3️⃣1️⃣ Inventory KPI

Dashboard-এ এই KPI রাখো:

|KPI|Formula|
|---|---|
|Total Products|`COUNTA()`|
|Total Stock Qty|`SUM()`|
|Inventory Value|`SUM()`|
|Units Sold|`SUM()`|
|Purchase Units|`SUM()`|
|Reorder Products|`COUNTIF()`|
|Avg Inventory|`AVERAGE()`|
|Inventory Turnover|COGS / Avg Inventory|

---

# 3️⃣2️⃣ Business Insights

এখানে Excel analyst-এর আসল skill।

শুধু:

> Laptop stock = 23

বললে সেটা শুধু information।

কিন্তু:

> Laptop has a high inventory value, so inventory planning for this product should receive higher attention.

এটা **business insight**।

আরও examples:

### Insight 1

কোনো product `REORDER` হলে:

> This product has reached its reorder threshold and may require replenishment.

### Insight 2

কোনো category-এর stock value অনেক বেশি হলে:

> A large amount of capital is currently tied up in this inventory category.

### Insight 3

কোনো product fast-moving হলে:

> This product has relatively high sales volume and may require closer stock monitoring.

### Insight 4

Slow-moving product:

> Slow-moving inventory may increase holding costs and should be reviewed.

### Insight 5

Supplier concentration বেশি হলে:

> Heavy dependence on one supplier may create supply-chain risk.

---

# 🧠 Class 29 Core Concepts

|Concept|Meaning|
|---|---|
|Current Stock|বর্তমানে available quantity|
|Stock Value|Current Stock × Cost|
|Reorder Level|যে level-এ আবার purchase দরকার|
|Reorder Qty|কত quantity আবার কিনতে হবে|
|COGS|Sold quantity-এর cost|
|Inventory Turnover|Inventory কত দ্রুত move করছে|
|Dead Stock|দীর্ঘসময় unused/unsold inventory|
|Fast Moving|দ্রুত বিক্রি হচ্ছে|
|ABC Analysis|Inventory importance/value classification|
|KPI|Important inventory metric|

---

# 🔥 Real-World Flow

তোমার Excel workflow এখন এমন হচ্ছে:

```text
Raw Inventory Data
       ↓
Data Cleaning
       ↓
Excel Table
       ↓
Calculated Columns
       ↓
KPI
       ↓
SUMIF / COUNTIF / AVERAGEIF
       ↓
PivotTable
       ↓
Charts
       ↓
Dashboard
       ↓
Business Insights
```

এটাই একজন **Junior Data Analyst / BI Analyst**-এর practical workflow-এর একটি simplified version।

---

# 🎯 Class 29 Assignment

### Part A — Calculations

1. Current Stock
    
2. Stock Value
    
3. Potential Sales Value
    
4. Potential Profit
    
5. Reorder Status
    
6. Reorder Quantity
    
7. COGS
    
8. Average Inventory
    
9. Inventory Turnover
    
10. Movement Status
    

### Part B — KPI

11. Total Products
    
12. Total Stock Quantity
    
13. Total Inventory Value
    
14. Total Units Sold
    
15. Total Purchased Units
    
16. Reorder Product Count
    

### Part C — Analysis

17. Category-wise Stock Value
    
18. Supplier-wise Stock Value
    
19. Product-wise Sales
    
20. Fast-moving Products
    
21. Slow-moving Products
    
22. Reorder Products
    
23. ABC Classification
    

### Part D — Visualization

24. Category Stock Value Chart
    
25. Supplier Stock Value Chart
    
26. Product Sales Chart
    
27. Reorder Status Chart
    

### Part E — Dashboard

একটি **Inventory Analytics Dashboard** বানাও।

### Part F — Business Insights

কমপক্ষে **5টি actionable business insight** লিখবে।

---

# 🧪 Class 29 Quiz

**1. Current Stock-এর formula কোনটি?**

A. Opening + Sold − Purchased  
B. Opening + Purchased − Sold  
C. Purchased − Opening − Sold  
D. Opening × Purchased

**2. Stock Value = ?**

A. Current Stock × Unit Cost  
B. Sold × Unit Price  
C. Purchased × Unit Price  
D. Opening Stock × Sold

**3. Current Stock Reorder Level-এর নিচে গেলে কী হতে পারে?**

A. REORDER  
B. Delete  
C. Profit  
D. Dead Stock automatically

**4. COGS-এর simplified formula কী?**

A. Sold × Unit Cost  
B. Sold × Unit Price  
C. Stock × Unit Price  
D. Purchased × Unit Price

**5. Inventory Turnover-এর basic concept কী?**

A. Employee performance  
B. Inventory movement speed  
C. Customer count  
D. Supplier count

**6. ABC Analysis-এর A category সাধারণত কী represent করে?**

A. Highest-priority/high-value inventory  
B. Always cheapest items  
C. Expired products  
D. New products

**7. Supplier-wise inventory value বের করতে কোন function ব্যবহার করা যায়?**

A. SUMIF  
B. LEFT  
C. TODAY  
D. LEN

**8. Fast-moving products identify করতে কোন data useful?**

A. Sold Quantity  
B. Font Size  
C. Cell Color  
D. Employee Age

**9. Dead Stock-এর simple practice rule আমরা কী ব্যবহার করেছি?**

A. Sold = 0  
B. Sold > 100  
C. Price = 0  
D. Stock = 0 only

**10. Inventory Dashboard-এর প্রধান উদ্দেশ্য কী?**

A. Decoration  
B. Inventory situation ও decision-making সহজ করা  
C. শুধু formulas hide করা  
D. Excel file ছোট করা

**Class 29-এর উত্তর 1–10 দাও। এরপর Class 30-এ আমরা করব 🔥 `Finance & Financial Analytics Project` — Revenue, Expense, Profit, Budget vs Actual, Cash Flow, ROI, Margin, Growth এবং Financial Dashboard।**


----
# 📊 Excel Mastery — Class 30

## 💰 Finance & Financial Analytics Project

আজ আমরা Excel দিয়ে একটি **real-world financial analysis system** বানাব।

আজকের class-এ আগের অনেকগুলো skill একসাথে ব্যবহার করব:

**Data → Revenue → Expense → Profit → Margin → Budget vs Actual → Growth → ROI → Cash Flow → PivotTable → Dashboard → Business Insights**

---

# 🎯 Class 30 Goal

আজকের শেষে তুমি পারবে:

- Revenue calculate করতে
    
- Expense calculate করতে
    
- Profit বের করতে
    
- Profit Margin বের করতে
    
- Budget vs Actual analysis করতে
    
- Variance বের করতে
    
- Growth % calculate করতে
    
- ROI calculate করতে
    
- Cash Flow বুঝতে
    
- Monthly financial analysis করতে
    
- Financial Dashboard বানাতে
    

---

# 1️⃣ Real-World Finance Dataset

Excel-এ নিচের dataset তৈরি করো:

|Month|Revenue|Cost of Goods|Salaries|Marketing|Rent|Other Expense|Budget|
|---|--:|--:|--:|--:|--:|--:|--:|
|January|500000|250000|80000|30000|40000|15000|480000|
|February|550000|270000|80000|35000|40000|18000|520000|
|March|620000|300000|85000|40000|40000|20000|580000|
|April|580000|280000|85000|35000|40000|18000|600000|
|May|700000|330000|90000|45000|40000|22000|650000|
|June|760000|350000|90000|50000|40000|25000|700000|
|July|720000|340000|95000|45000|40000|23000|720000|
|August|800000|370000|95000|50000|40000|25000|760000|
|September|850000|390000|100000|55000|40000|28000|800000|
|October|900000|410000|100000|60000|40000|30000|850000|
|November|950000|430000|105000|65000|40000|32000|900000|
|December|1100000|500000|110000|80000|40000|35000|1000000|

---

# 2️⃣ Excel Table তৈরি

Dataset select:

```text
Ctrl + T
```

Table name:

```text
FinanceTable
```

এখন আমরা structured references ব্যবহার করব।

---

# 3️⃣ Total Operating Expense

আমাদের expense-এর কয়েকটি অংশ আছে:

```text
Cost of Goods
+
Salaries
+
Marketing
+
Rent
+
Other Expense
```

নতুন column তৈরি করো:

**Total Expense**

Formula:

```excel
=[@[Cost of Goods]]+[@Salaries]+[@Marketing]+[@Rent]+[@[Other Expense]]
```

---

# 4️⃣ Gross Profit

Gross Profit:

```text
Revenue - Cost of Goods
```

নতুন column:

**Gross Profit**

```excel
=[@Revenue]-[@[Cost of Goods]]
```

### Example — January

```text
Revenue = 500,000
COGS    = 250,000

Gross Profit = 250,000
```

---

# 5️⃣ Net Profit

Net Profit:

```text
Revenue - Total Expense
```

Formula:

```excel
=[@Revenue]-[@[Total Expense]]
```

January:

```text
Revenue       = 500,000
Total Expense = 415,000

Net Profit = 85,000
```

---

# 6️⃣ Gross Profit Margin

Formula:

```text
Gross Profit / Revenue
```

Excel:

```excel
=IFERROR([@[Gross Profit]]/[@Revenue],0)
```

Percentage format দাও।

January:

```text
250,000 / 500,000
= 50%
```

---

# 7️⃣ Net Profit Margin

Formula:

```text
Net Profit / Revenue
```

Excel:

```excel
=IFERROR([@[Net Profit]]/[@Revenue],0)
```

January:

```text
85,000 / 500,000
= 17%
```

---

# 🧠 Gross vs Net Profit

এটা ভালোভাবে বুঝো।

### Gross Profit

শুধু:

```text
Revenue - COGS
```

### Net Profit

সব expense বাদ দেওয়ার পর:

```text
Revenue - All Expenses
```

Example:

```text
Revenue          500,000
COGS            -250,000
-------------------------
Gross Profit     250,000

Salary           -80,000
Marketing        -30,000
Rent             -40,000
Other            -15,000
-------------------------
Net Profit        85,000
```

---

# 8️⃣ Budget vs Actual

এখন business question:

> Company যে budget করেছিল, actual revenue কি তার চেয়ে বেশি হয়েছে?

আমাদের:

```text
Revenue = Actual
Budget = Planned
```

নতুন column:

**Revenue Variance**

Formula:

```excel
=[@Revenue]-[@Budget]
```

---

# 9️⃣ Variance Interpretation

যদি:

```text
Actual > Budget
```

তাহলে positive variance।

যদি:

```text
Actual < Budget
```

তাহলে negative variance।

Example:

```text
January:

Revenue = 500,000
Budget  = 480,000

Variance = +20,000
```

মানে budget-এর চেয়ে 20,000 বেশি revenue হয়েছে।

---

# 🔟 Budget Status

নতুন column:

**Budget Status**

Formula:

```excel
=IF([@[Revenue Variance]]>=0,"Above Budget","Below Budget")
```

Result:

```text
+20,000 → Above Budget
-20,000 → Below Budget
```

---

# 1️⃣1️⃣ Achievement %

Budget-এর কত শতাংশ achieve হয়েছে?

Formula:

```text
Actual Revenue / Budget
```

Excel:

```excel
=IFERROR([@Revenue]/[@Budget],0)
```

January:

```text
500,000 / 480,000
≈ 104.17%
```

অর্থাৎ company budget-এর 104.17% revenue achieve করেছে।

---

# 1️⃣2️⃣ Monthly Growth %

এখন সবচেয়ে important analytics metric।

নতুন column:

**Growth %**

January-এর জন্য previous month নেই।

February থেকে formula:

```excel
=IFERROR(([@Revenue]-A2)/A2,0)
```

তবে Table-এ structured reference ব্যবহার করার সময় previous-row reference নিয়ে কাজ করতে হবে। Beginner হিসেবে সহজভাবে আলাদা summary table ব্যবহার করা ভালো।

---

# 1️⃣3️⃣ Growth Summary Table

নতুন জায়গায়:

|Month|Revenue|Growth %|
|---|--:|--:|
|January|500000|-|
|February|550000||
|March|620000||
|April|580000||

February:

```excel
=(B3-B2)/B2
```

March:

```excel
=(B4-B3)/B3
```

তারপর নিচে drag করো।

### Example

January:

```text
500,000
```

February:

```text
550,000
```

Growth:

```text
(550,000 - 500,000) / 500,000
= 10%
```

---

# 1️⃣4️⃣ Expense Ratio

Business জানতে চাইতে পারে:

> Revenue-এর কত শতাংশ expense?

Formula:

```text
Total Expense / Revenue
```

Excel:

```excel
=IFERROR([@[Total Expense]]/[@Revenue],0)
```

Percentage format।

---

# 1️⃣5️⃣ Marketing Expense Ratio

Marketing কতটা revenue consume করছে?

```excel
=IFERROR([@Marketing]/[@Revenue],0)
```

Example:

```text
Marketing = 30,000
Revenue = 500,000

Ratio = 6%
```

---

# 1️⃣6️⃣ ROI — Return on Investment

সহজভাবে:

```text
ROI =
Return / Investment × 100
```

ধরি Marketing-এ investment হিসেবে expense ব্যবহার করে simple practice করছি।

Formula:

```excel
=IFERROR([@[Net Profit]]/[@Marketing],0)
```

⚠️ Real-world finance-এ ROI-এর numerator/denominator context অনুযায়ী নির্ধারণ করতে হয়। এখানে concept শেখার জন্য simplified version ব্যবহার করছি।

---

# 1️⃣7️⃣ Cash Flow

সহজভাবে:

```text
Cash Inflow - Cash Outflow
```

আমাদের simplified model-এ:

```text
Cash Inflow = Revenue
Cash Outflow = Total Expense
```

তাই:

```text
Net Cash Flow = Revenue - Total Expense
```

Formula:

```excel
=[@Revenue]-[@[Total Expense]]
```

এখানে এই simplified dataset-এ Net Cash Flow এবং Net Profit একই হবে।

Real business-এ দুটো সবসময় একই হয় না, কারণ depreciation, receivables, payables, financing, capital expenditure ইত্যাদি বিষয় থাকে।

---

# 1️⃣8️⃣ Total Yearly Revenue

KPI:

```excel
=SUM(FinanceTable[Revenue])
```

---

# 1️⃣9️⃣ Total Yearly Expense

```excel
=SUM(FinanceTable[Total Expense])
```

---

# 2️⃣0️⃣ Total Yearly Profit

```excel
=SUM(FinanceTable[Net Profit])
```

---

# 2️⃣1️⃣ Average Monthly Revenue

```excel
=AVERAGE(FinanceTable[Revenue])
```

---

# 2️⃣2️⃣ Average Monthly Profit

```excel
=AVERAGE(FinanceTable[Net Profit])
```

---

# 2️⃣3️⃣ Highest Revenue Month

Maximum revenue:

```excel
=MAX(FinanceTable[Revenue])
```

তারপর কোন month সেটা XLOOKUP দিয়ে বের করতে পারো:

```excel
=XLOOKUP(
MAX(FinanceTable[Revenue]),
FinanceTable[Revenue],
FinanceTable[Month]
)
```

এটা তোমাকে highest revenue month দেবে।

---

# 2️⃣4️⃣ Lowest Revenue Month

```excel
=XLOOKUP(
MIN(FinanceTable[Revenue]),
FinanceTable[Revenue],
FinanceTable[Month]
)
```

---

# 2️⃣5️⃣ Highest Profit Month

```excel
=XLOOKUP(
MAX(FinanceTable[Net Profit]),
FinanceTable[Net Profit],
FinanceTable[Month]
)
```

---

# 2️⃣6️⃣ Above-Budget Months

কতগুলো month budget-এর উপরে?

```excel
=COUNTIF(FinanceTable[Budget Status],"Above Budget")
```

---

# 2️⃣7️⃣ Below-Budget Months

```excel
=COUNTIF(FinanceTable[Budget Status],"Below Budget")
```

---

# 2️⃣8️⃣ Total Revenue Variance

```excel
=SUM(FinanceTable[Revenue Variance])
```

এতে পুরো বছরের:

> Actual Revenue বনাম Budget-এর total difference

পাবে।

---

# 2️⃣9️⃣ PivotTable — Financial Analysis

এখন PivotTable তৈরি করো।

```text
Insert
→ PivotTable
```

---

## PivotTable 1 — Monthly Financial Overview

```text
Rows:
Month

Values:
Revenue
Total Expense
Gross Profit
Net Profit
Budget
```

এতে পুরো বছরের financial picture পাওয়া যাবে।

---

# 3️⃣0️⃣ PivotTable 2 — Budget Performance

```text
Rows → Budget Status
Values → Revenue
```

দেখতে পারবে:

```text
Above Budget
Below Budget
```

---

# 3️⃣1️⃣ PivotTable 3 — Profit Analysis

```text
Rows → Month
Values → Net Profit
```

তারপর largest → smallest sort করলে:

> কোন month সবচেয়ে profitable?

বুঝতে পারবে।

---

# 3️⃣2️⃣ Financial Charts

### Chart 1 — Revenue Trend

**Line Chart**

```text
Month → Revenue
```

---

### Chart 2 — Revenue vs Budget

**Column/Combo Chart**

দুইটা metric:

```text
Actual Revenue
Budget
```

compare করো।

---

### Chart 3 — Profit Trend

**Line Chart**

```text
Month → Net Profit
```

---

### Chart 4 — Expense Breakdown

Expense columns নিয়ে:

```text
COGS
Salary
Marketing
Rent
Other
```

**Stacked Column Chart** ব্যবহার করতে পারো।

---

# 3️⃣3️⃣ Conditional Formatting

### Revenue

Data Bars:

```text
Home
→ Conditional Formatting
→ Data Bars
```

### Profit

Color Scale ব্যবহার করো।

### Revenue Variance

Positive/negative values visually identify করো।

---

# 3️⃣4️⃣ Financial KPI Dashboard

নতুন sheet:

```text
Financial Dashboard
```

Structure:

```text
┌────────────────────────────────────────────┐
│          FINANCIAL ANALYTICS DASHBOARD     │
├────────────┬────────────┬──────────┬───────┤
│Total Revenue│Total Profit│Avg Revenue│Margin│
├────────────┴────────────┴──────────┴───────┤
│             Revenue vs Budget               │
├─────────────────────────┬──────────────────┤
│ Monthly Revenue Trend   │ Profit Trend     │
├─────────────────────────┼──────────────────┤
│ Expense Breakdown       │ Budget Status    │
└─────────────────────────┴──────────────────┘
```

---

# 3️⃣5️⃣ Dashboard KPI

কমপক্ষে এগুলো রাখো:

### Total Revenue

```excel
=SUM(FinanceTable[Revenue])
```

### Total Expense

```excel
=SUM(FinanceTable[Total Expense])
```

### Total Net Profit

```excel
=SUM(FinanceTable[Net Profit])
```

### Net Profit Margin

```excel
=IFERROR(
SUM(FinanceTable[Net Profit])/
SUM(FinanceTable[Revenue]),
0
)
```

### Average Revenue

```excel
=AVERAGE(FinanceTable[Revenue])
```

### Above Budget Months

```excel
=COUNTIF(FinanceTable[Budget Status],"Above Budget")
```

---

# 3️⃣6️⃣ Business Insights

এখানেই একজন analyst-এর value।

শুধু:

> December revenue = 1.1 million

এটা information।

কিন্তু:

> **December generated the highest revenue of the year, indicating strong year-end sales performance.**

এটা business insight।

---

### Insight 1 — Revenue Growth

যদি বছরের শেষের দিকে revenue বাড়ে:

> Revenue shows an overall upward trend toward the end of the year.

### Insight 2 — Profit

যদি revenue বাড়ার সাথে profit-ও বাড়ে:

> Revenue growth is accompanied by improved absolute profitability.

### Insight 3 — Budget

যদি কোনো month budget-এর নিচে থাকে:

> The month underperformed its revenue target and may require investigation.

### Insight 4 — Expense

যদি expense ratio বেশি হয়:

> A high expense-to-revenue ratio may put pressure on profitability.

### Insight 5 — Marketing

Marketing expense বাড়লেও revenue না বাড়লে:

> Marketing spending should be evaluated against the revenue generated.

---

# 🧠 Class 30 Formula Cheat Sheet

|Analysis|Formula|
|---|---|
|Total Expense|COGS + Salary + Marketing + Rent + Other|
|Gross Profit|Revenue − COGS|
|Net Profit|Revenue − Total Expense|
|Gross Margin|Gross Profit / Revenue|
|Net Margin|Net Profit / Revenue|
|Variance|Actual − Budget|
|Achievement|Actual / Budget|
|Growth|(Current − Previous) / Previous|
|Expense Ratio|Expense / Revenue|
|ROI|Return / Investment|
|Cash Flow|Inflow − Outflow|
|Highest Revenue|MAX|
|Lowest Revenue|MIN|
|Highest Month|XLOOKUP + MAX|

---

# 🔥 Class 30 পর্যন্ত তোমার Excel Journey

এখন তুমি শুধু basic Excel শিখছ না। আমরা বিভিন্ন **real-world analytics projects** করেছি:

```text
Class 1–4
Excel Fundamentals
       ↓
Class 5–9
Formulas & Functions
       ↓
Class 10–12
Cleaning + Tables
       ↓
Class 13–16
PivotTable + Dynamic Arrays
       ↓
Class 17–19
Validation + Visualization
       ↓
Class 20–24
Power Query + Power Pivot + DAX
       ↓
Class 25
Sales Dashboard
       ↓
Class 26
Data Cleaning Project
       ↓
Class 27
Sales & Business Analytics
       ↓
Class 28
HR Analytics
       ↓
Class 29
Inventory Analytics
       ↓
Class 30
Financial Analytics
```

এখন Excel-এর **business analytics side** অনেক শক্ত হয়েছে।

---

# 🎯 Class 30 Final Assignment

একটি complete **Financial Analytics Dashboard** তৈরি করো।

### Part A — Calculations

1. Total Expense
    
2. Gross Profit
    
3. Net Profit
    
4. Gross Profit Margin
    
5. Net Profit Margin
    
6. Revenue Variance
    
7. Budget Status
    
8. Achievement %
    
9. Growth %
    
10. Expense Ratio
    
11. Marketing Ratio
    
12. ROI
    
13. Net Cash Flow
    

### Part B — KPI

14. Total Revenue
    
15. Total Expense
    
16. Total Profit
    
17. Average Revenue
    
18. Average Profit
    
19. Highest Revenue
    
20. Lowest Revenue
    
21. Highest Revenue Month
    
22. Highest Profit Month
    
23. Above-Budget Months
    

### Part C — PivotTable

24. Monthly Financial Overview
    
25. Budget Performance
    
26. Monthly Profit Analysis
    

### Part D — Charts

27. Revenue Trend
    
28. Revenue vs Budget
    
29. Profit Trend
    
30. Expense Breakdown
    

### Part E — Dashboard

একটি professional **Financial Analytics Dashboard** বানাও।

### Part F — Business Insights

কমপক্ষে **5টি actionable insight** লিখবে।

---

# 🧪 Class 30 Quiz

**1. Gross Profit = ?**

A. Revenue − COGS  
B. Revenue − Salary  
C. Revenue − All Expenses  
D. Revenue + COGS

**2. Net Profit = ?**

A. Revenue + Expense  
B. Revenue − Total Expense  
C. COGS − Revenue  
D. Revenue × Expense

**3. Net Profit Margin = ?**

A. Revenue / Profit  
B. Profit / Revenue  
C. Expense / Revenue  
D. Profit × Revenue

**4. Budget Variance = ?**

A. Budget − Actual only  
B. Actual − Budget  
C. Actual + Budget  
D. Actual × Budget

**5. Achievement % = ?**

A. Budget / Actual  
B. Actual / Budget  
C. Profit / Cost  
D. Expense / Revenue

**6. Monthly Revenue Growth calculate করতে কোন data দরকার?**

A. Current এবং Previous Revenue  
B. শুধু Salary  
C. শুধু Cost  
D. শুধু Budget

**7. Highest Revenue Month বের করতে কোন combination ব্যবহার করা যায়?**

A. LEFT + RIGHT  
B. XLOOKUP + MAX  
C. TODAY + LEN  
D. COUNTIF + TRIM

**8. Revenue vs Budget compare করতে কোন chart useful?**

A. Combo/Column  
B. Scatter only  
C. Pie only  
D. Doughnut only

**9. Financial Dashboard-এর মূল উদ্দেশ্য কী?**

A. Decoration  
B. Financial performance দ্রুত বোঝা ও decision support  
C. শুধু formula hide করা  
D. Excel file বড় করা

**10. Data Analyst-এর সবচেয়ে valuable final output কোনটি?**

A. শুধু raw data  
B. শুধু formulas  
C. Business insight  
D. শুধু formatting

**Class 30 শেষ হলে পরের বড় phase হবে Excel-এর বাইরে গিয়ে `SQL for Data Analysis`—কারণ তুমি যেহেতু database/data engineering দিকে যেতে চাচ্ছ, Excel → SQL transitionটাই হবে সবচেয়ে গুরুত্বপূর্ণ next step।**


----
# 📘 Excel Mastery — Class 31

## 🚀 Excel → SQL Transition: Why SQL Matters for Data Analysts

Class 1–30-এ আমরা Excel দিয়ে **data cleaning, formulas, PivotTable, Power Query, DAX, dashboard এবং business analytics** করেছি।

এখন খুব গুরুত্বপূর্ণ একটা transition:

```text
Excel
  ↓
SQL
  ↓
Python + Pandas
  ↓
Power BI
  ↓
Data Engineering
```

তুমি যেহেতু database-এর দিকেও যেতে চাও, **SQL হবে তোমার সবচেয়ে গুরুত্বপূর্ণ next skill**।

---

## 🎯 Class 31 Goal

আজ SQL-এর পুরো course শুরু করছি না। আজ বুঝব:

1. SQL কী?
    
2. Database কী?
    
3. Table কী?
    
4. Row/Column কী?
    
5. Excel আর SQL-এর relationship
    
6. SELECT
    
7. WHERE
    
8. ORDER BY
    
9. LIMIT
    
10. Basic SQL thinking
    

---

## 1️⃣ SQL কী?

**SQL = Structured Query Language**

Database থেকে data:

- দেখতে
    
- filter করতে
    
- sort করতে
    
- calculate করতে
    
- update করতে
    
- insert করতে
    
- delete করতে
    

SQL ব্যবহার করা হয়।

উদাহরণ:

```sql
SELECT *
FROM employees;
```

মানে:

> employees table-এর সব data দেখাও।

---

# 2️⃣ Excel বনাম Database

Excel-এ:

|ID|Name|Department|Salary|
|---|---|---|--:|
|E001|Rahim|IT|45000|
|E002|Karim|HR|55000|
|E003|Hasan|IT|60000|

Database-এও একই ধরনের structure থাকতে পারে:

```text
employees
-----------------------------
id | name | department | salary
```

অর্থাৎ তুমি Excel-এ যে table concept শিখেছ, SQL database-এ সেই concept আরও structured এবং scalable ভাবে ব্যবহার করবে।

---

# 3️⃣ SQL Table

ধরি আমাদের table:

```text
employees
```

Columns:

```text
id
name
department
city
salary
```

Rows:

```text
E001 | Rahim | IT | Dhaka | 45000
E002 | Karim | HR | Dhaka | 55000
E003 | Hasan | IT | Dhaka | 60000
E004 | Jamil | Finance | Sylhet | 70000
E005 | Nabil | Marketing | Dhaka | 40000
```

---

# 4️⃣ SELECT — Data দেখা

সব column:

```sql
SELECT *
FROM employees;
```

`*` মানে:

> সব columns

---

# 5️⃣ নির্দিষ্ট Column

শুধু Name এবং Salary:

```sql
SELECT name, salary
FROM employees;
```

Result:

|name|salary|
|---|--:|
|Rahim|45000|
|Karim|55000|
|Hasan|60000|
|Jamil|70000|
|Nabil|40000|

---

# 6️⃣ SELECT-এর Mental Model

Excel-এ তুমি ভাবতে:

> কোন column দেখতে চাই?

SQL-এ:

```sql
SELECT column1, column2
```

মানে:

> এই columns আমাকে দেখাও।

---

# 7️⃣ WHERE — Filter

Excel-এ Filter ব্যবহার করেছ।

SQL-এ:

```sql
WHERE
```

ধরি শুধু IT employees:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

Result:

|id|name|department|salary|
|---|---|---|--:|
|E001|Rahim|IT|45000|
|E003|Hasan|IT|60000|

---

# 8️⃣ Salary Filter

Salary 50,000-এর বেশি:

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

Result:

```text
Karim
Hasan
Jamil
```

---

# 9️⃣ Salary >= 50,000

```sql
SELECT *
FROM employees
WHERE salary >= 50000;
```

এখানে 50,000-ও include হবে।

---

# 🔟 Text Condition

Dhaka-এর employees:

```sql
SELECT *
FROM employees
WHERE city = 'Dhaka';
```

⚠️ Text সাধারণত single quote-এর মধ্যে:

```sql
'Dhaka'
'IT'
'Rahim'
```

---

# 1️⃣1️⃣ Multiple Conditions — AND

IT department এবং Dhaka:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND city = 'Dhaka';
```

মানে:

```text
department = IT
       AND
city = Dhaka
```

দুই condition-ই true হতে হবে।

---

# 1️⃣2️⃣ OR

IT অথবা HR:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
OR department = 'HR';
```

এখানে যেকোনো একটি condition true হলেই হবে।

---

# 🧠 Excel বনাম SQL

তুমি আগে Excel-এ শিখেছ:

```excel
=IF(AND(B2="IT",C2="Dhaka"),"Yes","No")
```

SQL-এ filtering:

```sql
WHERE department = 'IT'
AND city = 'Dhaka'
```

Concept একই:

```text
Excel Logic → SQL Logic
```

---

# 1️⃣3️⃣ ORDER BY

Excel-এ Sort করেছ।

SQL-এ:

```sql
ORDER BY
```

Salary ছোট থেকে বড়:

```sql
SELECT *
FROM employees
ORDER BY salary ASC;
```

`ASC` = Ascending

---

# 1️⃣4️⃣ বড় থেকে ছোট

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

`DESC` = Descending

Result:

```text
Jamil    70000
Hasan    60000
Karim    55000
Rahim    45000
Nabil    40000
```

---

# 1️⃣5️⃣ Multiple Sorting

ধরি:

প্রথমে Department অনুযায়ী sort, তারপর Salary descending:

```sql
SELECT *
FROM employees
ORDER BY department ASC, salary DESC;
```

SQL প্রথমে department দেখবে।

একই department-এর মধ্যে salary অনুযায়ী sort করবে।

---

# 1️⃣6️⃣ LIMIT

ধরি শুধু top 3 highest-paid employees:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

Result:

```text
Jamil
Hasan
Karim
```

🔥 খুব গুরুত্বপূর্ণ pattern:

```sql
SELECT *
FROM employees
ORDER BY salary DESC
LIMIT 3;
```

মানে:

> Highest salary-এর top 3 employee।

---

# 1️⃣7️⃣ DISTINCT

Unique departments দেখতে চাই:

```sql
SELECT DISTINCT department
FROM employees;
```

Result:

```text
IT
HR
Finance
Marketing
```

Excel-এর **Remove Duplicates / UNIQUE()** concept-এর সাথে তুলনা করতে পারো।

---

# 1️⃣8️⃣ COUNT

Employee কয়জন?

```sql
SELECT COUNT(*)
FROM employees;
```

Result:

```text
5
```

---

# 1️⃣9️⃣ COUNT with WHERE

IT employee কতজন?

```sql
SELECT COUNT(*)
FROM employees
WHERE department = 'IT';
```

---

# 2️⃣0️⃣ SUM

সব employee-এর salary total:

```sql
SELECT SUM(salary)
FROM employees;
```

Excel-এর:

```excel
=SUM(EmployeeTable[Salary])
```

এর SQL equivalent concept:

```sql
SUM(salary)
```

---

# 2️⃣1️⃣ AVG

Average salary:

```sql
SELECT AVG(salary)
FROM employees;
```

Excel:

```excel
=AVERAGE(EmployeeTable[Salary])
```

SQL:

```sql
AVG(salary)
```

---

# 2️⃣2️⃣ MIN / MAX

Minimum salary:

```sql
SELECT MIN(salary)
FROM employees;
```

Maximum:

```sql
SELECT MAX(salary)
FROM employees;
```

---

# 🧠 Excel → SQL Cheat Sheet

|Excel|SQL|
|---|---|
|Select columns|`SELECT`|
|Filter|`WHERE`|
|Sort|`ORDER BY`|
|Unique|`DISTINCT`|
|Top N|`LIMIT`|
|SUM|`SUM()`|
|Average|`AVG()`|
|Count|`COUNT()`|
|Minimum|`MIN()`|
|Maximum|`MAX()`|
|AND|`AND`|
|OR|`OR`|

---

# 2️⃣3️⃣ একটি Complete Query

Question:

> Dhaka-এর IT employees-এর মধ্যে highest salary পাওয়া top 2 employee দেখাও।

SQL:

```sql
SELECT id, name, salary
FROM employees
WHERE city = 'Dhaka'
AND department = 'IT'
ORDER BY salary DESC
LIMIT 2;
```

এখানে আমরা একসাথে ব্যবহার করেছি:

```text
SELECT
WHERE
AND
ORDER BY
DESC
LIMIT
```

এটাই SQL শেখার সবচেয়ে ভালো পদ্ধতি:

> **Business question → SQL query**

---

# 2️⃣4️⃣ আরেকটি Example

Question:

> Salary 50,000-এর বেশি employees-এর নাম ও salary দেখাও।

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000
ORDER BY salary DESC;
```

---

# 2️⃣5️⃣ SQL Query পড়ার নিয়ম

এই query:

```sql
SELECT name, salary
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC
LIMIT 3;
```

এভাবে পড়বে:

```text
SELECT
↓
কোন columns?

FROM
↓
কোন table?

WHERE
↓
কোন rows?

ORDER BY
↓
কীভাবে sort?

LIMIT
↓
কতগুলো result?
```

---

# 🔥 SQL শেখার Golden Pattern

প্রায় প্রতিটি beginner query-তে এই structure মাথায় রাখো:

```sql
SELECT columns
FROM table
WHERE condition
ORDER BY column
LIMIT number;
```

সব অংশ সবসময় লাগবে না।

যেমন:

```sql
SELECT *
FROM employees;
```

এটাই valid।

---

# 🎯 Class 31 Practical Assignment

এই `employees` table নিয়ে নিচের queries নিজে লেখো।

### Q1

সব employees দেখাও।

### Q2

শুধু `name` এবং `salary` দেখাও।

### Q3

শুধু IT employees দেখাও।

### Q4

Salary 50,000-এর বেশি employees দেখাও।

### Q5

Dhaka-এর employees দেখাও।

### Q6

Dhaka-এর IT employees দেখাও।

### Q7

IT অথবা Finance employees দেখাও।

### Q8

Salary highest থেকে lowest sort করো।

### Q9

Top 3 highest-paid employees দেখাও।

### Q10

Unique departments দেখাও।

### Q11

Total employees count করো।

### Q12

Total salary বের করো।

### Q13

Average salary বের করো।

### Q14

Highest salary বের করো।

### Q15

Lowest salary বের করো।

---

# 🧪 Class 31 Quiz

**1. SQL-এর full form কী?**

A. Simple Query Language  
B. Structured Query Language  
C. Standard Question Language  
D. System Query Logic

**2. Table-এর data দেখতে কোন command?**

A. SELECT  
B. SHOWDATA  
C. GET  
D. VIEW

**3. Data filter করতে?**

A. SORT  
B. WHERE  
C. FILTER  
D. GROUP

**4. Sort করতে?**

A. ORDER BY  
B. SORT BY  
C. ARRANGE  
D. ORDER

**5. Highest থেকে lowest?**

A. ASC  
B. DESC  
C. HIGH  
D. TOP

**6. Unique values পেতে?**

A. UNIQUE  
B. DISTINCT  
C. DIFFERENT  
D. ONLY

**7. Employee count?**

A. SUM(_)  
B. COUNT(_)  
C. TOTAL(_)  
D. NUMBER(_)

**8. Average salary?**

A. MEAN()  
B. AVG()  
C. AVERAGE()  
D. MID()

**9. Top 5 records পেতে কোনটা useful?**

A. TOP 5  
B. LIMIT 5  
C. FIRST 5  
D. MAX 5

**10. SQL শেখার সবচেয়ে ভালো approach কোনটি?**

A. শুধু syntax মুখস্থ করা  
B. Business question → SQL query  
C. শুধু SELECT শেখা  
D. শুধু database তৈরি করা

---

### 🚀 পরের Class 32

**SQL Fundamentals — Database + Table Creation**

সেখানে আমরা শিখব:

```text
CREATE DATABASE
CREATE TABLE
Data Types
PRIMARY KEY
INSERT INTO
NULL
NOT NULL
DEFAULT
UNIQUE
CHECK
```

এবং Excel-এর **row/column** concept থেকে কীভাবে একটি proper relational database তৈরি হয়, সেটা হাতে-কলমে দেখব।


----
# 📘 Excel Mastery → SQL — Class 32

## 🗄️ Database & Table Creation Fundamentals

Class 31-এ আমরা শিখেছি:

```text
SELECT
FROM
WHERE
ORDER BY
LIMIT
DISTINCT
COUNT
SUM
AVG
MIN
MAX
```

আজ থেকে আমরা SQL-এর **Database Design side** শুরু করব। এটা তোমার database designer হওয়ার জন্য খুব important।

আজ শিখব:

- Database
    
- DBMS
    
- CREATE DATABASE
    
- CREATE TABLE
    
- Data Types
    
- PRIMARY KEY
    
- NOT NULL
    
- UNIQUE
    
- DEFAULT
    
- CHECK
    
- INSERT INTO
    
- NULL
    
- Basic constraints
    

---

# 1️⃣ Database কী?

সহজভাবে:

> **Database হলো organized data-এর collection।**

ধরো একটি company-এর employee information আছে:

```text
Employee ID
Name
Department
Salary
City
```

এই data সুন্দরভাবে store করার জন্য database ব্যবহার করা যায়।

---

# 2️⃣ DBMS কী?

**DBMS = Database Management System**

এটি database তৈরি, সংরক্ষণ, query এবং manage করার software।

Examples:

- PostgreSQL
    
- MySQL
    
- SQL Server
    
- Oracle Database
    
- SQLite
    

তুমি যেহেতু MySQL already ব্যবহার করেছ, আজকের SQL examples MySQL/PostgreSQL দুটোতেই সহজে বোঝা যাবে। কিছু syntax পরে আলাদা হতে পারে।

---

# 3️⃣ Database → Table → Row → Column

এই hierarchy মনে রাখো:

```text
Database
   ↓
Tables
   ↓
Rows
   ↓
Columns
```

Example:

```text
CompanyDB
   │
   ├── employees
   │      ├── id
   │      ├── name
   │      ├── department
   │      └── salary
   │
   ├── departments
   │
   └── projects
```

একটি database-এর ভিতরে অনেক table থাকতে পারে।

---

# 4️⃣ CREATE DATABASE

ধরি database-এর নাম:

```text
company_db
```

SQL:

```sql
CREATE DATABASE company_db;
```

Database তৈরি হয়ে গেল।

---

# 5️⃣ Database ব্যবহার করা

### MySQL

```sql
USE company_db;
```

এর অর্থ:

> এখন `company_db` database-এর ভিতরে কাজ করব।

PostgreSQL-এ database connection/select করার পদ্ধতি client অনুযায়ী হয়; `USE` command নেই।

---

# 6️⃣ CREATE TABLE

এখন employee table তৈরি করি।

```sql
CREATE TABLE employees (
    id INT,
    name VARCHAR(100),
    department VARCHAR(50),
    city VARCHAR(50),
    salary DECIMAL(10,2)
);
```

---

# 7️⃣ প্রতিটি অংশ বুঝি

```sql
id INT
```

মানে:

```text
id → column name
INT → data type
```

---

```sql
name VARCHAR(100)
```

মানে:

```text
name → column
VARCHAR(100) → maximum 100 characters-এর variable-length text
```

---

```sql
salary DECIMAL(10,2)
```

মানে:

> Decimal number; মোট precision 10 digits, যার মধ্যে decimal-এর পরে 2 digits।

উদাহরণ:

```text
45000.50
```

---

# 8️⃣ Common SQL Data Types

|Data Type|ব্যবহার|
|---|---|
|INT|পূর্ণ সংখ্যা|
|BIGINT|অনেক বড় পূর্ণ সংখ্যা|
|DECIMAL|টাকা/precise decimal|
|VARCHAR|Text|
|CHAR|Fixed-length text|
|TEXT|বড় text|
|DATE|Date|
|TIME|Time|
|DATETIME/TIMESTAMP|Date + Time|
|BOOLEAN|True/False|

---

# 9️⃣ INT

পূর্ণ সংখ্যা:

```sql
age INT
```

Examples:

```text
18
25
40
100
```

---

# 🔟 VARCHAR

Text:

```sql
name VARCHAR(100)
```

Examples:

```text
Rahim
Karim
Hasan
```

---

# 1️⃣1️⃣ DECIMAL

Financial data-এর জন্য খুব useful:

```sql
salary DECIMAL(10,2)
```

উদাহরণ:

```text
45000.00
```

💡 Money-এর ক্ষেত্রে সাধারণত floating-point-এর বদলে appropriate exact decimal type ব্যবহার করা ভালো।

---

# 1️⃣2️⃣ DATE

```sql
birth_date DATE
```

Example:

```text
2001-05-20
```

SQL date সাধারণত:

```text
YYYY-MM-DD
```

format-এ দেখা যায়।

---

# 1️⃣3️⃣ BOOLEAN

```sql
is_active BOOLEAN
```

Value:

```text
TRUE
FALSE
```

---

# 1️⃣4️⃣ PRIMARY KEY 🔥

এটা খুব গুরুত্বপূর্ণ।

**Primary Key = প্রতিটি row-কে uniquely identify করে এমন column বা column combination।**

Example:

```text
id
```

আমাদের:

```text
E001
E002
E003
```

প্রতিটি আলাদা।

---

# 1️⃣5️⃣ Primary Key Example

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10,2)
);
```

এখন:

```text
id
```

হচ্ছে Primary Key।

---

# 1️⃣6️⃣ Primary Key-এর Rules

একটি Primary Key:

✅ Unique হতে হবে

✅ NULL হতে পারবে না

✅ প্রতিটি row uniquely identify করবে

উদাহরণ:

```text
id
---
1
2
3
```

ভালো।

কিন্তু:

```text
1
1
2
```

Primary Key হিসেবে valid নয়।

---

# 1️⃣7️⃣ NOT NULL

ধরো employee-এর name অবশ্যই থাকতে হবে।

```sql
name VARCHAR(100) NOT NULL
```

এখন:

```text
name = NULL
```

allowed নয়।

Complete example:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50),
    salary DECIMAL(10,2)
);
```

---

# 1️⃣8️⃣ NULL কী?

**NULL মানে value জানা নেই / দেওয়া হয়নি / প্রযোজ্য নয়।**

NULL:

```text
0 নয়
```

NULL:

```text
empty string '' নয়
```

NULL মানে:

> এখানে value নেই/unknown।

---

# 1️⃣9️⃣ UNIQUE

ধরো employee email unique হওয়া উচিত।

```sql
email VARCHAR(150) UNIQUE
```

তাহলে:

```text
rahim@gmail.com
```

একবার থাকতে পারবে।

একই email আবার insert করলে constraint violation হবে।

---

# 2️⃣0️⃣ DEFAULT

ধরো নতুন employee-এর active status automatically:

```text
TRUE
```

হবে।

```sql
is_active BOOLEAN DEFAULT TRUE
```

তাহলে value না দিলেও default value আসবে।

---

# 2️⃣1️⃣ CHECK

ধরো salary negative হতে পারবে না।

```sql
salary DECIMAL(10,2) CHECK (salary >= 0)
```

অথবা age:

```sql
age INT CHECK (age >= 18)
```

এটা database-level validation।

---

# 2️⃣2️⃣ Complete Employee Table 🔥

এবার সব একসাথে:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    age INT CHECK (age >= 18),
    department VARCHAR(50),
    city VARCHAR(50),
    salary DECIMAL(10,2) CHECK (salary >= 0),
    is_active BOOLEAN DEFAULT TRUE
);
```

এটা এখন অনেক বেশি professional table design।

---

# 2️⃣3️⃣ Excel বনাম SQL

তুমি Excel-এ শিখেছিলে Data Validation।

এখন compare করো:

|Excel|Database|
|---|---|
|Unique validation|`UNIQUE`|
|Required value|`NOT NULL`|
|Numeric validation|`CHECK`|
|Default value|`DEFAULT`|
|Unique ID|`PRIMARY KEY`|
|Dropdown/valid related value|পরে `FOREIGN KEY`|

এটাই Excel → Database transition।

---

# 2️⃣4️⃣ INSERT INTO

Table তৈরি হয়েছে।

এখন data ঢুকাতে হবে।

```sql
INSERT INTO employees
(id, name, email, age, department, city, salary)
VALUES
(1, 'Rahim', 'rahim@gmail.com', 25, 'IT', 'Dhaka', 45000);
```

---

# 2️⃣5️⃣ একসাথে Multiple Rows

```sql
INSERT INTO employees
(id, name, email, age, department, city, salary)
VALUES
(2, 'Karim', 'karim@gmail.com', 30, 'HR', 'Dhaka', 55000),
(3, 'Hasan', 'hasan@gmail.com', 28, 'IT', 'Chittagong', 60000),
(4, 'Jamil', 'jamil@gmail.com', 35, 'Finance', 'Sylhet', 70000);
```

---

# 2️⃣6️⃣ Data Check

এখন:

```sql
SELECT *
FROM employees;
```

Result:

|id|name|email|age|department|city|salary|
|--:|---|---|--:|---|---|--:|
|1|Rahim|[rahim@gmail.com](mailto:rahim@gmail.com)|25|IT|Dhaka|45000|
|2|Karim|[karim@gmail.com](mailto:karim@gmail.com)|30|HR|Dhaka|55000|
|3|Hasan|[hasan@gmail.com](mailto:hasan@gmail.com)|28|IT|Chittagong|60000|
|4|Jamil|[jamil@gmail.com](mailto:jamil@gmail.com)|35|Finance|Sylhet|70000|

---

# 2️⃣7️⃣ Primary Key Violation

ধরি আবার:

```sql
INSERT INTO employees
(id, name)
VALUES
(1, 'Nabil');
```

সমস্যা হবে।

কারণ:

```text
id = 1
```

আগেই আছে।

Primary Key duplicate হতে দেয় না।

---

# 2️⃣8️⃣ NOT NULL Violation

আমাদের:

```sql
name VARCHAR(100) NOT NULL
```

তাই:

```sql
INSERT INTO employees
(id, email)
VALUES
(5, 'test@gmail.com');
```

এখানে `name` দেওয়া হয়নি।

Database reject করবে।

---

# 2️⃣9️⃣ UNIQUE Violation

ধরি:

```text
rahim@gmail.com
```

আগেই আছে।

আবার:

```sql
INSERT INTO employees
(id, name, email)
VALUES
(5, 'Nabil', 'rahim@gmail.com');
```

করলে `UNIQUE` constraint violation হবে।

---

# 3️⃣0️⃣ CHECK Constraint

আমাদের:

```sql
salary DECIMAL(10,2) CHECK (salary >= 0)
```

তাই:

```sql
INSERT INTO employees
(id, name, salary)
VALUES
(5, 'Nabil', -5000);
```

এটা reject হওয়ার কথা।

কারণ:

```text
-5000 < 0
```

---

# 3️⃣1️⃣ DEFAULT

আমাদের:

```sql
is_active BOOLEAN DEFAULT TRUE
```

তাই:

```sql
INSERT INTO employees
(id, name)
VALUES
(5, 'Nabil');
```

করলে `is_active` explicitly না দিলেও default value `TRUE` হতে পারে।

---

# 🧠 Constraint Mental Model

এটা মুখস্থ না করে logic বুঝো:

```text
PRIMARY KEY
     ↓
Who is this row?

NOT NULL
     ↓
Must this value exist?

UNIQUE
     ↓
Can duplicates exist?

CHECK
     ↓
Is this value valid?

DEFAULT
     ↓
What should happen if value is omitted?
```

---

# 3️⃣2️⃣ Full Example

```sql
CREATE DATABASE company_db;
```

MySQL হলে:

```sql
USE company_db;
```

তারপর:

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE,
    age INT CHECK (age >= 18),
    department VARCHAR(50),
    city VARCHAR(50),
    salary DECIMAL(10,2) CHECK (salary >= 0),
    is_active BOOLEAN DEFAULT TRUE
);
```

Data:

```sql
INSERT INTO employees
(id, name, email, age, department, city, salary)
VALUES
(1, 'Rahim', 'rahim@gmail.com', 25, 'IT', 'Dhaka', 45000),
(2, 'Karim', 'karim@gmail.com', 30, 'HR', 'Dhaka', 55000),
(3, 'Hasan', 'hasan@gmail.com', 28, 'IT', 'Chittagong', 60000),
(4, 'Jamil', 'jamil@gmail.com', 35, 'Finance', 'Sylhet', 70000);
```

তারপর:

```sql
SELECT *
FROM employees;
```

---

# 🔥 Class 32-এর সবচেয়ে Important Concept

Database design মানে শুধু:

```sql
CREATE TABLE
```

লেখা নয়।

তোমাকে ভাবতে হবে:

> **এই data-এর rules কী?**

উদাহরণ:

Employee:

```text
ID → unique
Name → required
Email → unique
Age → minimum 18
Salary → cannot be negative
Active → default TRUE
```

তারপর সেই business rules database constraint হিসেবে implement করবে।

এটাই **database design thinking**।

---

# 🎯 Class 32 Assignment

`company_db` তৈরি করে `employees` table বানাও।

### Table columns:

```text
id
name
email
age
department
city
salary
is_active
```

### Rules:

- `id` → Primary Key
    
- `name` → NOT NULL
    
- `email` → UNIQUE
    
- `age` → >= 18
    
- `salary` → >= 0
    
- `is_active` → DEFAULT TRUE
    

তারপর অন্তত **10 employees** insert করো।

এরপর এই queries লেখো:

### Q1

সব employee:

```sql
SELECT *
FROM employees;
```

### Q2

শুধু name + salary।

### Q3

IT employees।

### Q4

Salary > 50,000।

### Q5

Dhaka employees।

### Q6

Salary highest → lowest।

### Q7

Top 3 employees।

### Q8

Unique departments।

### Q9

Total salary।

### Q10

Average salary।

---

# 🧪 Class 32 Quiz

**1. Database কী?**

A. শুধু একটি Excel file  
B. Organized collection of data  
C. শুধু একটি table  
D. শুধু একটি query

**2. Database manage করার software-কে কী বলে?**

A. DBMS  
B. HTML  
C. IDE  
D. API

**3. Primary Key-এর প্রধান কাজ কী?**

A. Data sort করা  
B. Row uniquely identify করা  
C. Table delete করা  
D. Calculation করা

**4. Primary Key কি NULL হতে পারে?**

A. Yes  
B. No  
C. Sometimes  
D. শুধু MySQL-এ

**5. Duplicate value prevent করতে?**

A. DEFAULT  
B. CHECK  
C. UNIQUE  
D. NULL

**6. Value অবশ্যই দিতে হবে এমন condition?**

A. NOT NULL  
B. UNIQUE  
C. DEFAULT  
D. ORDER BY

**7. Salary negative prevent করতে কোনটি ভালো?**

A. PRIMARY KEY  
B. CHECK  
C. UNIQUE  
D. DEFAULT

**8. Value না দিলে automatically value দেওয়ার জন্য?**

A. CHECK  
B. DEFAULT  
C. NULL  
D. DISTINCT

**9. Data insert করতে?**

A. ADD DATA  
B. INSERT INTO  
C. PUT  
D. CREATE ROW

**10. `VARCHAR(100)` কী বোঝায়?**

A. 100 integer  
B. Variable-length character/text field with declared maximum length 100  
C. 100 rows  
D. 100 tables

---

## 🚀 Next: Class 33

পরের class-এ আমরা যাব **SQL Data Manipulation & Filtering — INSERT, UPDATE, DELETE, NULL, LIKE, IN, BETWEEN, IS NULL**-এ।

বিশেষ করে শিখব:

```sql
UPDATE
DELETE
LIKE
IN
BETWEEN
IS NULL
IS NOT NULL
```

এবং **কীভাবে ভুল UPDATE/DELETE করে পুরো table-এর data নষ্ট হয়ে যেতে পারে এবং কীভাবে safe query লিখতে হয়**—এটা database designer-এর জন্য খুব গুরুত্বপূর্ণ।




----

# 📘 SQL — Class 33

## ✏️ INSERT, UPDATE, DELETE + LIKE, IN, BETWEEN, NULL

Class 32-এ আমরা শিখেছি:

```text
CREATE DATABASE
CREATE TABLE
Data Types
PRIMARY KEY
NOT NULL
UNIQUE
CHECK
DEFAULT
INSERT INTO
```

আজ আমরা শিখব কীভাবে existing data **change, search এবং delete** করতে হয়।

---

# 1️⃣ INSERT INTO — আবার একটু Practice

ধরি আমাদের table:

```text
employees
```

Columns:

```text
id
name
email
age
department
city
salary
is_active
```

একজন employee:

```sql
INSERT INTO employees
(id, name, email, age, department, city, salary)
VALUES
(5, 'Nabil', 'nabil@gmail.com', 27, 'Marketing', 'Dhaka', 40000);
```

---

# 2️⃣ UPDATE — Existing Data পরিবর্তন

ধরি Rahim-এর salary:

```text
45000
```

এখন salary 50000 করতে চাই।

```sql
UPDATE employees
SET salary = 50000
WHERE id = 1;
```

এখানে:

```text
UPDATE → কোন table?
SET    → কী পরিবর্তন?
WHERE  → কোন row?
```

---

# ⚠️ 3️⃣ UPDATE-এর সবচেয়ে গুরুত্বপূর্ণ Rule

**WHERE ভুলে যেও না।**

❌ বিপজ্জনক:

```sql
UPDATE employees
SET salary = 50000;
```

এটা table-এর **সব employee-এর salary 50000** করে দিতে পারে।

সঠিক:

```sql
UPDATE employees
SET salary = 50000
WHERE id = 1;
```

---

# 4️⃣ Multiple Column Update

Rahim-এর:

```text
salary = 50000
city = Dhaka
```

একসাথে:

```sql
UPDATE employees
SET salary = 50000,
    city = 'Dhaka'
WHERE id = 1;
```

---

# 5️⃣ Condition দিয়ে UPDATE

IT department-এর salary 10% increase:

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department = 'IT';
```

এখানে:

```text
salary * 1.10
```

মানে current salary + 10%।

Example:

```text
50000 → 55000
60000 → 66000
```

---

# 6️⃣ DELETE — Row Delete

ধরি ID 5 employee delete করতে চাই:

```sql
DELETE FROM employees
WHERE id = 5;
```

---

# ⚠️ DELETE-এর ক্ষেত্রেও WHERE খুব গুরুত্বপূর্ণ

❌ বিপজ্জনক:

```sql
DELETE FROM employees;
```

এতে table-এর **সব rows delete** হয়ে যেতে পারে।

সঠিক:

```sql
DELETE FROM employees
WHERE id = 5;
```

---

# 🧠 UPDATE বনাম DELETE

|Command|কাজ|
|---|---|
|INSERT|নতুন row যোগ|
|UPDATE|existing row পরিবর্তন|
|DELETE|row মুছে ফেলা|
|SELECT|data দেখা|

Mental model:

```text
INSERT → Add
SELECT → Read
UPDATE → Change
DELETE → Remove
```

এগুলোকে একসাথে অনেক সময় **CRUD** বলা হয়:

```text
C → Create
R → Read
U → Update
D → Delete
```

---

# 7️⃣ LIKE — Pattern Search

ধরি এমন employee খুঁজতে চাই যাদের নাম `R` দিয়ে শুরু।

```sql
SELECT *
FROM employees
WHERE name LIKE 'R%';
```

এখানে `%` খুব গুরুত্বপূর্ণ।

---

# 8️⃣ `%` কী?

`%` মানে:

> Zero বা more characters

Example:

```sql
LIKE 'R%'
```

মানে:

```text
Rahim
Rafi
Rakib
R
```

সব match করতে পারে।

---

# 9️⃣ Name শেষ হবে `n` দিয়ে

```sql
SELECT *
FROM employees
WHERE name LIKE '%n';
```

Match হতে পারে:

```text
Rahman
Hasan
```

---

# 🔟 Name-এর মধ্যে `ha`

```sql
SELECT *
FROM employees
WHERE name LIKE '%ha%';
```

মানে name-এর যেকোনো জায়গায় `ha` থাকলে match করবে।

---

# 1️⃣1️⃣ `_` Wildcard

`_` মানে **exactly one character**।

Example:

```sql
WHERE name LIKE 'R_him';
```

এখানে:

```text
R
_
h
i
m
```

`_` একটি character represent করছে।

---

# 🧠 `%` বনাম `_`

|Symbol|Meaning|
|---|---|
|`%`|Zero or more characters|
|`_`|Exactly one character|

---

# 1️⃣2️⃣ IN

ধরি IT অথবা HR অথবা Finance department-এর employees চাই।

এভাবে লিখতে পারো:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
   OR department = 'HR'
   OR department = 'Finance';
```

কিন্তু আরও clean:

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR', 'Finance');
```

`IN` মানে:

> এই list-এর মধ্যে যেকোনো একটি value।

---

# 1️⃣3️⃣ NOT IN

IT এবং HR বাদ দিয়ে:

```sql
SELECT *
FROM employees
WHERE department NOT IN ('IT', 'HR');
```

---

# 1️⃣4️⃣ BETWEEN

Salary 40,000 থেকে 60,000-এর মধ্যে:

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 60000;
```

সাধারণভাবে `BETWEEN` দুই boundary-ই include করে।

অর্থাৎ:

```text
40000 ✓
50000 ✓
60000 ✓
```

---

# 1️⃣5️⃣ Date-এর সাথে BETWEEN

ধরি `join_date` column আছে।

January 2026-এর data:

```sql
SELECT *
FROM employees
WHERE join_date BETWEEN '2026-01-01' AND '2026-01-31';
```

Date/time column হলে boundary handling নিয়ে আরও সতর্ক হতে হয়; পরে আমরা proper date-range query শিখব।

---

# 1️⃣6️⃣ NULL

ধরি কিছু employee-এর email নেই:

```text
id | name | email
-------------------------
1  | Rahim | rahim@gmail.com
2  | Karim | NULL
3  | Hasan | hasan@gmail.com
```

এখন যাদের email নেই তাদের খুঁজতে:

❌ এভাবে নয়:

```sql
WHERE email = NULL;
```

সঠিক:

```sql
SELECT *
FROM employees
WHERE email IS NULL;
```

---

# 1️⃣7️⃣ IS NOT NULL

যাদের email আছে:

```sql
SELECT *
FROM employees
WHERE email IS NOT NULL;
```

---

# 🔥 কেন `= NULL` কাজ করে না?

SQL-এ NULL একটি ordinary value নয়।

NULL বলতে বোঝায়:

> value unknown / missing / absent।

তাই SQL-এ:

```sql
email IS NULL
```

ব্যবহার করতে হয়।

---

# 1️⃣8️⃣ Practical Examples

### Example 1 — Dhaka employees

```sql
SELECT *
FROM employees
WHERE city = 'Dhaka';
```

### Example 2 — Salary 50K-এর বেশি

```sql
SELECT *
FROM employees
WHERE salary > 50000;
```

### Example 3 — Salary 40K–60K

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 40000 AND 60000;
```

### Example 4 — IT অথবা HR

```sql
SELECT *
FROM employees
WHERE department IN ('IT', 'HR');
```

### Example 5 — Name starts with A

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

### Example 6 — Missing email

```sql
SELECT *
FROM employees
WHERE email IS NULL;
```

---

# 1️⃣9️⃣ একাধিক Condition

Dhaka-এর IT employees:

```sql
SELECT *
FROM employees
WHERE city = 'Dhaka'
AND department = 'IT';
```

Dhaka-এর IT অথবা HR:

```sql
SELECT *
FROM employees
WHERE city = 'Dhaka'
AND department IN ('IT', 'HR');
```

Salary 50K-এর বেশি এবং IT:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
AND salary > 50000;
```

---

# 2️⃣0️⃣ UPDATE + LIKE

যাদের department Marketing:

```sql
UPDATE employees
SET is_active = FALSE
WHERE department = 'Marketing';
```

---

# 2️⃣1️⃣ UPDATE + IN

IT এবং HR employees-এর salary 5% increase:

```sql
UPDATE employees
SET salary = salary * 1.05
WHERE department IN ('IT', 'HR');
```

---

# 2️⃣2️⃣ DELETE + Condition

Marketing department-এর inactive employee delete:

```sql
DELETE FROM employees
WHERE department = 'Marketing'
AND is_active = FALSE;
```

---

# ⚠️ 2️⃣3️⃣ Safe UPDATE/DELETE Technique

Real database-এ সরাসরি UPDATE/DELETE করার আগে **SELECT দিয়ে একই condition test করা** ভালো অভ্যাস।

ধরি:

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department = 'IT';
```

আগে:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

দেখো কোন rows affected হবে।

তারপর UPDATE।

একইভাবে DELETE:

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
AND is_active = FALSE;
```

ঠিক rows হলে তারপর:

```sql
DELETE FROM employees
WHERE department = 'Marketing'
AND is_active = FALSE;
```

এটা খুব valuable database habit। 🔥

---

# 2️⃣4️⃣ CRUD পুরোটা

এখন তোমার CRUD understanding:

### Create

```sql
INSERT INTO employees (...)
VALUES (...);
```

### Read

```sql
SELECT *
FROM employees;
```

### Update

```sql
UPDATE employees
SET salary = 50000
WHERE id = 1;
```

### Delete

```sql
DELETE FROM employees
WHERE id = 1;
```

---

# 🧠 Excel → SQL Connection

তুমি Excel-এ already এগুলোর concept দেখেছ:

|Excel|SQL|
|---|---|
|Add row|INSERT|
|Filter|WHERE|
|Search pattern|LIKE|
|Multiple choices|IN|
|Range condition|BETWEEN|
|Blank check|IS NULL|
|Sort|ORDER BY|
|Edit data|UPDATE|
|Remove row|DELETE|

তাই SQL তোমার জন্য completely নতুন concept নয়।

---

# 🔥 Class 33 Query Challenge

ধরি:

```text
employees
```

এর মধ্যে 10+ records আছে।

নিজে query লেখো:

### Q1

ID 3-এর employee-এর salary 65,000 করো।

### Q2

সব IT employee-এর salary 10% increase করো।

### Q3

HR এবং Finance employees দেখাও।

### Q4

Salary 45,000 থেকে 70,000-এর মধ্যে employees দেখাও।

### Q5

যাদের name `A` দিয়ে শুরু তাদের দেখাও।

### Q6

যাদের name `n` দিয়ে শেষ তাদের দেখাও।

### Q7

যাদের email নেই তাদের দেখাও।

### Q8

যাদের email আছে তাদের দেখাও।

### Q9

IT এবং HR ছাড়া employees দেখাও।

### Q10

ID 10-এর employee delete করো।

### Q11

Dhaka-এর Marketing employees-এর salary 5% increase করো।

### Q12

যাদের salary 60,000-এর বেশি তাদের inactive করো।

---

# 🧪 Class 33 Quiz

**1. Existing data পরিবর্তন করতে কোন command?**

A. CHANGE  
B. UPDATE  
C. MODIFY  
D. EDIT

**2. Row delete করতে?**

A. REMOVE  
B. DROP ROW  
C. DELETE  
D. CLEAR

**3. `LIKE 'A%'` কী বোঝায়?**

A. A দিয়ে শেষ  
B. A দিয়ে শুরু  
C. শুধু A  
D. A নেই

**4. `%` কী বোঝায়?**

A. Exactly one character  
B. Zero or more characters  
C. Number  
D. Space

**5. `IN ('IT','HR')` কী বোঝায়?**

A. IT এবং HR দুটোই একই row-তে  
B. IT অথবা HR-এর মধ্যে যেকোনো একটি  
C. IT বাদ  
D. HR বাদ

**6. 40,000 থেকে 60,000 range-এর জন্য?**

A. RANGE  
B. BETWEEN  
C. WITHIN  
D. INSIDE

**7. NULL check করতে?**

A. `= NULL`  
B. `IS NULL`  
C. `NULL =`  
D. `CHECK NULL`

**8. সব rows update করতে কোনটি dangerous?**

A. UPDATE + WHERE  
B. UPDATE without WHERE  
C. UPDATE + ORDER BY  
D. UPDATE + LIMIT

**9. Safe DELETE-এর আগে কী করা ভালো?**

A. SELECT দিয়ে condition verify  
B. DROP DATABASE  
C. Restart computer  
D. CREATE TABLE

**10. CRUD-এর U কী?**

A. Upload  
B. Update  
C. Undo  
D. Unique

---

## 📌 Class 33 Cheat Sheet

```sql
-- INSERT
INSERT INTO employees (...)
VALUES (...);

-- UPDATE
UPDATE employees
SET salary = 50000
WHERE id = 1;

-- DELETE
DELETE FROM employees
WHERE id = 1;

-- LIKE
WHERE name LIKE 'A%';

-- IN
WHERE department IN ('IT', 'HR');

-- BETWEEN
WHERE salary BETWEEN 40000 AND 60000;

-- NULL
WHERE email IS NULL;

-- NOT NULL
WHERE email IS NOT NULL;
```

### ⭐ আজকের সবচেয়ে গুরুত্বপূর্ণ ৩টি rule

```text
1. UPDATE → WHERE carefully
2. DELETE → WHERE carefully
3. NULL → IS NULL / IS NOT NULL
```

**Next Class 34:** `GROUP BY + HAVING + Aggregate Functions` — এখানে Excel-এর **PivotTable + SUMIF/COUNTIF/AVERAGEIF** concept-কে SQL-এর powerful analysis query-তে convert করব।


----
# 📘 SQL — Class 34

## 📊 GROUP BY + HAVING + Aggregate Functions

Class 33-এ আমরা শিখেছি:

```text
INSERT
UPDATE
DELETE
LIKE
IN
BETWEEN
IS NULL
IS NOT NULL
```

আজ থেকে আমরা SQL দিয়ে **real data analysis** শুরু করব।

আজকের topic খুব important কারণ Excel-এর:

- PivotTable
    
- SUMIF
    
- COUNTIF
    
- AVERAGEIF
    

— এগুলোর SQL equivalent বুঝতে শুরু করবে।

---

# 🎯 আজকের Learning Goals

আজ শিখবে:

1. Aggregate Functions
    
2. `COUNT()`
    
3. `SUM()`
    
4. `AVG()`
    
5. `MIN()`
    
6. `MAX()`
    
7. `GROUP BY`
    
8. `HAVING`
    
9. `WHERE` বনাম `HAVING`
    
10. Multiple-column grouping
    
11. Business questions → SQL
    

---

# 1️⃣ Aggregate Function কী?

Aggregate function অনেকগুলো row-এর data নিয়ে **একটি summary result** তৈরি করে।

উদাহরণ:

```sql
SELECT SUM(salary)
FROM employees;
```

অনেক employee-এর salary → একটি total।

---

# 2️⃣ COUNT()

Employee কতজন?

```sql
SELECT COUNT(*)
FROM employees;
```

ধরি 10 জন employee আছে:

```text
COUNT
-----
10
```

---

# 3️⃣ COUNT(column)

```sql
SELECT COUNT(email)
FROM employees;
```

এখানে `email` যেসব row-তে NULL নয়, সেগুলো count হবে।

তাই:

```text
COUNT(*)       → rows count
COUNT(email)   → non-NULL email count
```

এটা খুব important difference।

---

# 4️⃣ SUM()

সব employee-এর salary total:

```sql
SELECT SUM(salary)
FROM employees;
```

Excel equivalent:

```excel
=SUM(EmployeeTable[Salary])
```

---

# 5️⃣ AVG()

Average salary:

```sql
SELECT AVG(salary)
FROM employees;
```

Excel:

```excel
=AVERAGE(EmployeeTable[Salary])
```

---

# 6️⃣ MIN()

সবচেয়ে কম salary:

```sql
SELECT MIN(salary)
FROM employees;
```

---

# 7️⃣ MAX()

সবচেয়ে বেশি salary:

```sql
SELECT MAX(salary)
FROM employees;
```

---

# 8️⃣ একসাথে Multiple Aggregate

```sql
SELECT
    COUNT(*) AS total_employees,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees;
```

Result হতে পারে:

|total_employees|total_salary|average_salary|minimum_salary|maximum_salary|
|--:|--:|--:|--:|--:|
|10|580000|58000|35000|85000|

---

# 9️⃣ `AS` কী?

```sql
SUM(salary) AS total_salary
```

`AS` দিয়ে column-এর temporary readable name দিচ্ছি।

Without:

```text
SUM(salary)
```

With:

```text
total_salary
```

এটাকে **alias** বলে।

---

# 🔥 10️⃣ GROUP BY

এখন আসল topic।

ধরি আমাদের employee data:

|Name|Department|Salary|
|---|---|--:|
|Rahim|IT|45000|
|Hasan|IT|60000|
|Karim|HR|55000|
|Jamil|Finance|70000|
|Nabil|HR|50000|

Question:

> প্রতিটি department-এ কয়জন employee আছে?

Excel-এ PivotTable করতে।

SQL:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

Result:

|department|employee_count|
|---|--:|
|IT|2|
|HR|2|
|Finance|1|

---

# 1️⃣1️⃣ GROUP BY-এর সহজ ধারণা

`GROUP BY` বলছে:

> একই value-গুলোকে group করো।

যেমন:

```text
IT
IT
HR
Finance
HR
```

Group করলে:

```text
IT       → 2
HR       → 2
Finance  → 1
```

---

# 1️⃣2️⃣ Department-wise Total Salary

Question:

> প্রতিটি department-এর total salary কত?

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department;
```

Result:

|department|total_salary|
|---|--:|
|IT|105000|
|HR|105000|
|Finance|70000|

---

# 1️⃣3️⃣ Department-wise Average Salary

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

---

# 1️⃣4️⃣ Department-wise Highest Salary

```sql
SELECT
    department,
    MAX(salary) AS highest_salary
FROM employees
GROUP BY department;
```

---

# 1️⃣5️⃣ Department-wise Lowest Salary

```sql
SELECT
    department,
    MIN(salary) AS lowest_salary
FROM employees
GROUP BY department;
```

---

# 1️⃣6️⃣ এক Query-তে সব

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary,
    MIN(salary) AS minimum_salary,
    MAX(salary) AS maximum_salary
FROM employees
GROUP BY department;
```

এটা অনেকটা Excel PivotTable-এর মতো:

```text
Rows → Department

Values:
Count of Employees
Sum of Salary
Average Salary
Minimum Salary
Maximum Salary
```

🔥 এই connectionটা খুব ভালোভাবে বুঝে রাখো।

---

# 1️⃣7️⃣ Excel PivotTable → SQL

Excel:

```text
Rows:
Department

Values:
Count of ID
Sum of Salary
Average of Salary
```

SQL:

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    SUM(salary) AS total_salary,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```

---

# 1️⃣8️⃣ GROUP BY City

Question:

> City অনুযায়ী employee count।

```sql
SELECT
    city,
    COUNT(*) AS employee_count
FROM employees
GROUP BY city;
```

---

# 1️⃣9️⃣ City-wise Average Salary

```sql
SELECT
    city,
    AVG(salary) AS average_salary
FROM employees
GROUP BY city;
```

---

# 2️⃣0️⃣ Multiple Columns GROUP BY

এখন ধরো:

> Department এবং City অনুযায়ী employee count।

```sql
SELECT
    department,
    city,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department, city;
```

এখানে group হবে:

```text
IT + Dhaka
IT + Chittagong
HR + Dhaka
Finance + Sylhet
```

---

# 2️⃣1️⃣ WHERE + GROUP BY

ধরি শুধু Dhaka employees নিয়ে department-wise count চাই।

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE city = 'Dhaka'
GROUP BY department;
```

এখানে প্রথমে:

```text
WHERE city = Dhaka
```

তারপর:

```text
GROUP BY department
```

---

# 🧠 Query Processing-এর সহজ ধারণা

এই query:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
WHERE city = 'Dhaka'
GROUP BY department;
```

Conceptually:

```text
employees
    ↓
WHERE city = Dhaka
    ↓
Filtered rows
    ↓
GROUP BY department
    ↓
AVG(salary)
    ↓
Result
```

---

# 2️⃣2️⃣ HAVING

এখন ধরো:

> যেসব department-এ 2-এর বেশি employee আছে, শুধু সেগুলো দেখাও।

এখানে `WHERE` ব্যবহার করা যাবে না, কারণ আমরা **group-এর result** filter করছি।

তাই:

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;
```

---

# 2️⃣3️⃣ WHERE বনাম HAVING 🔥

এটা খুব important।

### WHERE

**Rows filter করে।**

```sql
WHERE salary > 50000
```

### HAVING

**Groups filter করে।**

```sql
HAVING COUNT(*) > 2
```

Mental model:

```text
WHERE
↓
individual rows

GROUP BY
↓
groups

HAVING
↓
groups filter
```

---

# 2️⃣4️⃣ Example

Question:

> যেসব department-এর average salary 60,000-এর বেশি, সেগুলো দেখাও।

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

---

# 2️⃣5️⃣ WHERE + GROUP BY + HAVING

এখন আরও realistic query:

> Dhaka-এর employees নিয়ে এমন department দেখাও যেখানে employee count 2-এর বেশি।

```sql
SELECT
    department,
    COUNT(*) AS employee_count
FROM employees
WHERE city = 'Dhaka'
GROUP BY department
HAVING COUNT(*) > 2;
```

Concept:

```text
সব employees
      ↓
শুধু Dhaka
      ↓
Department অনুযায়ী group
      ↓
যেখানে count > 2
```

---

# 2️⃣6️⃣ GROUP BY + ORDER BY

Department-wise total salary বের করে highest total salary আগে দেখাতে:

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department
ORDER BY total_salary DESC;
```

Result:

```text
Finance   150000
IT        130000
HR        110000
```

---

# 2️⃣7️⃣ Top Department

সবচেয়ে বেশি total salary-এর top department:

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department
ORDER BY total_salary DESC
LIMIT 1;
```

🔥 Real-world analytics query।

---

# 2️⃣8️⃣ Department with Highest Average Salary

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
ORDER BY average_salary DESC
LIMIT 1;
```

---

# 2️⃣9️⃣ COUNT + HAVING

যেসব city-তে অন্তত 3 জন employee আছে:

```sql
SELECT
    city,
    COUNT(*) AS employee_count
FROM employees
GROUP BY city
HAVING COUNT(*) >= 3;
```

---

# 3️⃣0️⃣ SUM + HAVING

যেসব department-এর total salary 200,000-এর বেশি:

```sql
SELECT
    department,
    SUM(salary) AS total_salary
FROM employees
GROUP BY department
HAVING SUM(salary) > 200000;
```

---

# 3️⃣1️⃣ AVG + HAVING

Average salary 50,000-এর বেশি:

```sql
SELECT
    department,
    AVG(salary) AS average_salary
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

---

# 🔥 3️⃣2️⃣ SQL Query Structure

আজকের সবচেয়ে important pattern:

```sql
SELECT
    column,
    AGGREGATE_FUNCTION(column)
FROM table
WHERE condition
GROUP BY column
HAVING aggregate_condition
ORDER BY column
LIMIT number;
```

সব clause সবসময় লাগবে না।

---

# 3️⃣3️⃣ Example — Business Question

### Question:

> Dhaka-এর কোন departments-এ 2-এর বেশি employee আছে এবং তাদের average salary 50,000-এর বেশি?

Query:

```sql
SELECT
    department,
    COUNT(*) AS employee_count,
    AVG(salary) AS average_salary
FROM employees
WHERE city = 'Dhaka'
GROUP BY department
HAVING COUNT(*) > 2
   AND AVG(salary) > 50000
ORDER BY average_salary DESC;
```

🔥 এই ধরনের query Data Analyst interview-এ খুব useful।

---

# 3️⃣4️⃣ Excel Function বনাম SQL

|Excel|SQL|
|---|---|
|`SUM()`|`SUM()`|
|`AVERAGE()`|`AVG()`|
|`COUNT()`|`COUNT()`|
|`MIN()`|`MIN()`|
|`MAX()`|`MAX()`|
|PivotTable Rows|`GROUP BY`|
|PivotTable Values|Aggregate functions|
|Pivot filter on aggregate|`HAVING`|
|Normal Filter|`WHERE`|
|Sort|`ORDER BY`|

---

# 🧠 একটি গুরুত্বপূর্ণ Difference

Excel:

```text
SUMIF
COUNTIF
AVERAGEIF
```

SQL-এ অনেক সময়:

```text
WHERE + GROUP BY + SUM()
WHERE + GROUP BY + COUNT()
WHERE + GROUP BY + AVG()
```

উদাহরণ:

### Excel

```excel
=SUMIF(DepartmentRange,"IT",SalaryRange)
```

### SQL

```sql
SELECT SUM(salary)
FROM employees
WHERE department = 'IT';
```

---

# 3️⃣5️⃣ GROUP BY vs DISTINCT

দুটোকে confuse করবে না।

### Unique departments:

```sql
SELECT DISTINCT department
FROM employees;
```

এটা শুধু unique values দেয়।

### Department-wise count:

```sql
SELECT
    department,
    COUNT(*)
FROM employees
GROUP BY department;
```

এখানে grouping + calculation হচ্ছে।

---

# 🎯 Class 34 Practical Assignment

এই `employees` table ব্যবহার করে query লেখো।

### Q1

Total employee count।

### Q2

Total salary।

### Q3

Average salary।

### Q4

Department-wise employee count।

### Q5

Department-wise total salary।

### Q6

Department-wise average salary।

### Q7

City-wise employee count।

### Q8

City-wise average salary।

### Q9

Department + City অনুযায়ী employee count।

### Q10

শুধু Dhaka employees নিয়ে department-wise average salary।

### Q11

যেসব department-এ 3-এর বেশি employee আছে।

### Q12

যেসব department-এর average salary 60,000-এর বেশি।

### Q13

Department-wise total salary highest থেকে lowest।

### Q14

Highest average salary-এর department।

### Q15

যেসব city-তে 2-এর বেশি employee আছে এবং average salary 50,000-এর বেশি।

---

# 🧪 Class 34 Quiz

**1. অনেক rows থেকে summary calculation করার function কী?**

A. Aggregate Function  
B. Filter Function  
C. Search Function  
D. Sort Function

**2. Total বের করতে?**

A. TOTAL()  
B. SUM()  
C. ADD()  
D. PLUS()

**3. Average বের করতে?**

A. AVERAGE()  
B. AVG()  
C. MEAN()  
D. MID()

**4. Department-wise calculation করতে কোনটি ব্যবহার করব?**

A. GROUP BY  
B. ORDER BY  
C. SORT BY  
D. DISTINCT

**5. Row filter করতে?**

A. HAVING  
B. WHERE  
C. GROUP  
D. FILTER BY

**6. Group filter করতে?**

A. WHERE  
B. HAVING  
C. GROUP  
D. SELECT

**7. `COUNT(*)` কী করে?**

A. Salary যোগ করে  
B. Rows count করে  
C. Average বের করে  
D. Duplicate delete করে

**8. Department-এর total salary বের করতে?**

A. `COUNT(salary)`  
B. `AVG(salary)`  
C. `SUM(salary)`  
D. `MAX(salary)`

**9. Highest total salary department প্রথমে দেখাতে?**

A. `ORDER BY total_salary DESC`  
B. `ORDER BY total_salary ASC`  
C. `SORT total_salary`  
D. `HAVING total_salary`

**10. `HAVING COUNT(*) > 2` কী করে?**

A. প্রতিটি row-এর count > 2 করে  
B. যেসব group-এর count > 2 শুধু সেগুলো রাখে  
C. 2 rows delete করে  
D. 2 rows add করে

---

# ⭐ Class 34 Cheat Sheet

```sql
-- COUNT
SELECT COUNT(*)
FROM employees;

-- SUM
SELECT SUM(salary)
FROM employees;

-- AVG
SELECT AVG(salary)
FROM employees;

-- GROUP BY
SELECT department, COUNT(*)
FROM employees
GROUP BY department;

-- WHERE + GROUP BY
SELECT department, AVG(salary)
FROM employees
WHERE city = 'Dhaka'
GROUP BY department;

-- HAVING
SELECT department, COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 2;

-- GROUP + ORDER
SELECT department, SUM(salary) AS total_salary
FROM employees
GROUP BY department
ORDER BY total_salary DESC;
```

## 🧠 আজকের Golden Rule

```text
WHERE  → Row filter
GROUP BY → Rows → Groups
HAVING → Group filter
ORDER BY → Sort result
```

আর Excel-এর ভাষায়:

```text
Excel PivotTable
      ↓
SQL GROUP BY

Excel Filter
      ↓
SQL WHERE

Pivot aggregate filter
      ↓
SQL HAVING
```

**পরের Class 35:** `SQL JOIN — INNER JOIN, LEFT JOIN, RIGHT JOIN`। এখানে আমরা প্রথমবার **দুই বা তার বেশি table একসাথে combine** করব—এটা database designer এবং Data Analyst দুজনের জন্যই অত্যন্ত গুরুত্বপূর্ণ।


----
# 📘 SQL — Class 35

## 🔗 JOIN — Multiple Tables একসাথে ব্যবহার

Class 34-এ আমরা শিখেছি:

```text
COUNT()
SUM()
AVG()
MIN()
MAX()
GROUP BY
HAVING
ORDER BY
```

আজ SQL-এর **সবচেয়ে গুরুত্বপূর্ণ topic-এর একটি — JOIN** শুরু করছি।

Database designer বা Data Analyst হিসেবে JOIN না জানলে real database-এর data নিয়ে কাজ করা কঠিন।

---

# 🎯 আজকের Learning Goals

আজ শিখবে:

1. কেন multiple table লাগে
    
2. Primary Key
    
3. Foreign Key
    
4. Relationship
    
5. INNER JOIN
    
6. LEFT JOIN
    
7. RIGHT JOIN
    
8. JOIN + WHERE
    
9. JOIN + GROUP BY
    
10. JOIN-এর real-world use
    

---

# 1️⃣ কেন Multiple Table?

ধরো একটি company-তে customer এবং order আছে।

একটি বড় table বানালে:

|Order_ID|Customer_ID|Customer_Name|City|Product|Price|
|---|---|---|---|---|--:|
|O001|C001|Rahim|Dhaka|Laptop|50000|
|O002|C002|Karim|Chittagong|Mouse|1000|
|O003|C001|Rahim|Dhaka|Keyboard|2000|

এখানে `Rahim`, `Dhaka` বারবার repeat হচ্ছে।

অনেক বড় database হলে redundancy বাড়বে।

তাই আলাদা table:

### Customers

|Customer_ID|Name|City|
|---|---|---|
|C001|Rahim|Dhaka|
|C002|Karim|Chittagong|
|C003|Hasan|Sylhet|

### Orders

|Order_ID|Customer_ID|Product|Amount|
|---|---|---|--:|
|O001|C001|Laptop|50000|
|O002|C002|Mouse|1000|
|O003|C001|Keyboard|2000|

এখন দুই table-এর common column:

```text
Customers.Customer_ID
Orders.Customer_ID
```

এই relationship ব্যবহার করে data combine করব।

---

# 2️⃣ Primary Key

Customers table:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(50)
);
```

এখানে:

```text
customer_id
```

হলো Primary Key।

প্রতিটি customer-এর unique ID।

---

# 3️⃣ Foreign Key

Orders table:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product VARCHAR(100),
    amount DECIMAL(10,2),
    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

এখানে:

```text
orders.customer_id
```

হলো Foreign Key।

এটি `customers.customer_id`-কে reference করছে।

---

# 🧠 Primary Key বনাম Foreign Key

|Primary Key|Foreign Key|
|---|---|
|Row uniquely identify করে|অন্য table-এর row reference করে|
|সাধারণত unique|Repeat হতে পারে|
|NULL নয়|NULL হতে পারে, যদি relationship optional হয়|
|Parent/Referenced table-এ থাকে|Child/Referencing table-এ থাকে|

Example:

```text
customers
    customer_id ← PRIMARY KEY
          ↑
          │
          │ FOREIGN KEY
          │
orders
    customer_id
```

---

# 4️⃣ Relationship

এখানে:

```text
One Customer
     ↓
Many Orders
```

এটা:

> **One-to-Many Relationship**

একজন customer অনেক order করতে পারে।

---

# 5️⃣ JOIN কী?

সহজ ভাষায়:

> **JOIN দুই বা তার বেশি table-এর related data একসাথে দেখায়।**

Example:

Customers:

```text
C001 → Rahim
C002 → Karim
```

Orders:

```text
O001 → C001
O002 → C002
```

JOIN করলে:

```text
O001 | Rahim | Laptop
O002 | Karim | Mouse
```

---

# 6️⃣ INNER JOIN 🔥

সবচেয়ে আগে `INNER JOIN`।

```sql
SELECT
    orders.order_id,
    customers.name,
    orders.product,
    orders.amount
FROM orders
INNER JOIN customers
    ON orders.customer_id = customers.customer_id;
```

---

# 7️⃣ `ON` কী?

```sql
ON orders.customer_id = customers.customer_id
```

এটাই বলে:

> কোন column-এর ভিত্তিতে দুই table match করবে?

অর্থাৎ:

```text
orders.customer_id
        =
customers.customer_id
```

---

# 8️⃣ INNER JOIN-এর Result

Customers:

|customer_id|name|city|
|---|---|---|
|1|Rahim|Dhaka|
|2|Karim|Chittagong|
|3|Hasan|Sylhet|

Orders:

|order_id|customer_id|product|amount|
|---|--:|---|--:|
|O001|1|Laptop|50000|
|O002|2|Mouse|1000|
|O003|1|Keyboard|2000|

INNER JOIN:

|order_id|name|product|amount|
|---|---|---|--:|
|O001|Rahim|Laptop|50000|
|O002|Karim|Mouse|1000|
|O003|Rahim|Keyboard|2000|

---

# 9️⃣ INNER JOIN Mental Model

```text
Table A       Table B
   │             │
   └──── MATCH ──┘
          ↓
     Matching rows
```

অর্থাৎ:

> দুই table-এ match আছে এমন data।

---

# 🔟 LEFT JOIN

এবার ধরো:

Customers:

```text
Rahim
Karim
Hasan
```

কিন্তু Hasan এখনো কোনো order করেনি।

Orders:

```text
Rahim → Laptop
Karim → Mouse
```

আমরা চাই **সব customers**, order থাকুক বা না থাকুক।

তখন:

```sql
SELECT
    customers.customer_id,
    customers.name,
    orders.order_id,
    orders.product
FROM customers
LEFT JOIN orders
    ON customers.customer_id = orders.customer_id;
```

---

# 1️⃣1️⃣ LEFT JOIN Result

|customer_id|name|order_id|product|
|--:|---|---|---|
|1|Rahim|O001|Laptop|
|2|Karim|O002|Mouse|
|3|Hasan|NULL|NULL|

Hasan-এর order নেই।

তাই:

```text
order_id = NULL
product = NULL
```

---

# 🧠 LEFT JOIN Mental Model

```text
LEFT TABLE
    ↓
সব rows থাকবে
    +
RIGHT TABLE-এর matching rows
```

অর্থাৎ:

> **Left table-এর সব data রাখো।**

---

# 1️⃣2️⃣ RIGHT JOIN

RIGHT JOIN হলো LEFT JOIN-এর reverse concept।

```sql
SELECT
    customers.name,
    orders.order_id,
    orders.product
FROM customers
RIGHT JOIN orders
    ON customers.customer_id = orders.customer_id;
```

এখানে:

> Right table-এর সব rows থাকবে।

---

# 1️⃣3️⃣ INNER vs LEFT vs RIGHT

|JOIN|কী রাখে?|
|---|---|
|INNER JOIN|দুই table-এর matching rows|
|LEFT JOIN|Left table-এর সব rows + matching right rows|
|RIGHT JOIN|Right table-এর সব rows + matching left rows|

Visual:

```text
INNER JOIN

A ∩ B
```

```text
LEFT JOIN

A + matching B
```

```text
RIGHT JOIN

B + matching A
```

---

# 1️⃣4️⃣ LEFT JOIN কেন খুব Useful?

Question:

> কোন customers কোনো order করেনি?

```sql
SELECT
    customers.customer_id,
    customers.name
FROM customers
LEFT JOIN orders
    ON customers.customer_id = orders.customer_id
WHERE orders.order_id IS NULL;
```

Result:

```text
Hasan
```

🔥 খুব common real-world query।

---

# 1️⃣5️⃣ JOIN + WHERE

Question:

> Dhaka-এর customers-এর orders দেখাও।

```sql
SELECT
    customers.name,
    customers.city,
    orders.product,
    orders.amount
FROM customers
INNER JOIN orders
    ON customers.customer_id = orders.customer_id
WHERE customers.city = 'Dhaka';
```

এখানে:

```text
JOIN
 ↓
Related data
 ↓
WHERE
 ↓
Dhaka filter
```

---

# 1️⃣6️⃣ JOIN + ORDER BY

Highest order amount আগে:

```sql
SELECT
    customers.name,
    orders.product,
    orders.amount
FROM customers
INNER JOIN orders
    ON customers.customer_id = orders.customer_id
ORDER BY orders.amount DESC;
```

---

# 1️⃣7️⃣ JOIN + GROUP BY 🔥

এখন real analytics।

Question:

> প্রত্যেক customer মোট কত টাকা purchase করেছে?

```sql
SELECT
    customers.name,
    SUM(orders.amount) AS total_purchase
FROM customers
INNER JOIN orders
    ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_id, customers.name;
```

Result:

|name|total_purchase|
|---|--:|
|Rahim|52000|
|Karim|1000|

---

# 1️⃣8️⃣ কেন GROUP BY-তে ID-ও দিলাম?

আমরা লিখেছি:

```sql
GROUP BY customers.customer_id, customers.name;
```

কারণ customer-এর unique identity হিসেবে ID ব্যবহার করা ভালো practice।

বিশেষ করে এমন database-এ যেখানে একই name-এর একাধিক customer থাকতে পারে।

---

# 1️⃣9️⃣ Customer Order Count

প্রতিটি customer কতটি order করেছে?

```sql
SELECT
    customers.name,
    COUNT(orders.order_id) AS order_count
FROM customers
LEFT JOIN orders
    ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_id, customers.name;
```

LEFT JOIN ব্যবহারের কারণে order না করা customer-ও result-এ থাকবে।

---

# 2️⃣0️⃣ `COUNT(*)` বনাম `COUNT(order_id)`

এটা খুব important।

LEFT JOIN-এর ক্ষেত্রে:

```sql
COUNT(*)
```

এবং

```sql
COUNT(orders.order_id)
```

এক জিনিস নয়।

Order না থাকা customer-এর জন্য:

```text
orders.order_id = NULL
```

তাই:

```sql
COUNT(orders.order_id)
```

সাধারণত তার actual orders count করতে সাহায্য করে।

---

# 2️⃣1️⃣ Customers Without Orders

আরেকবার:

```sql
SELECT
    customers.name
FROM customers
LEFT JOIN orders
    ON customers.customer_id = orders.customer_id
WHERE orders.order_id IS NULL;
```

Mental model:

```text
LEFT JOIN
    ↓
সব customer
    ↓
যাদের order নেই
    ↓
WHERE order_id IS NULL
```

---

# 2️⃣2️⃣ JOIN + HAVING

Question:

> যেসব customer 50,000-এর বেশি purchase করেছে।

```sql
SELECT
    customers.name,
    SUM(orders.amount) AS total_purchase
FROM customers
INNER JOIN orders
    ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_id, customers.name
HAVING SUM(orders.amount) > 50000;
```

এখানে:

```text
WHERE
→ individual row filter

HAVING
→ grouped result filter
```

---

# 2️⃣3️⃣ তিনটি Table JOIN

Real database-এ দুইটির বেশি table join করা খুব common।

ধরি:

```text
customers
products
orders
```

Orders:

```text
order_id
customer_id
product_id
quantity
```

Products:

```text
product_id
product_name
price
```

তাহলে:

```sql
SELECT
    customers.name,
    products.product_name,
    orders.quantity
FROM orders
INNER JOIN customers
    ON orders.customer_id = customers.customer_id
INNER JOIN products
    ON orders.product_id = products.product_id;
```

এখানে:

```text
orders
   │
   ├──── customers
   │
   └──── products
```

---

# 2️⃣4️⃣ Three-Table Business Query

Question:

> Customer-এর নাম, product-এর নাম এবং order amount দেখাও।

```sql
SELECT
    customers.name AS customer_name,
    products.product_name,
    orders.amount
FROM orders
INNER JOIN customers
    ON orders.customer_id = customers.customer_id
INNER JOIN products
    ON orders.product_id = products.product_id;
```

---

# 2️⃣5️⃣ JOIN + Aggregate + GROUP BY

Question:

> Category-wise total sales কত?

ধরি products table-এ:

```text
product_id
product_name
category
```

Query:

```sql
SELECT
    products.category,
    SUM(orders.amount) AS total_sales
FROM orders
INNER JOIN products
    ON orders.product_id = products.product_id
GROUP BY products.category;
```

🔥 এটা Data Analyst-এর real-world query।

---

# 2️⃣6️⃣ Excel-এর সাথে Connection

Excel-এ তোমার data যদি হয়:

```text
Customers
Products
Sales
```

Power Pivot-এ relationship তৈরি করেছিলে।

SQL-এ সেই relationship-এর মাধ্যমে:

```sql
JOIN
```

ব্যবহার করি।

---

# Excel → SQL Mapping

|Excel / Power Pivot|SQL|
|---|---|
|Relationship|JOIN condition|
|Related tables|JOIN|
|Lookup|JOIN|
|PivotTable|GROUP BY|
|Slicer/filter|WHERE|
|Aggregate filter|HAVING|
|Dimension|Related descriptive table|
|Fact table|Transaction table|

---

# 2️⃣7️⃣ JOIN-এর সবচেয়ে Important Rule

JOIN করার সময় নিজেকে প্রশ্ন করো:

> **কোন column দুই table-এর relationship তৈরি করছে?**

Example:

```text
customers.customer_id
        ↕
orders.customer_id
```

তারপর:

```sql
ON customers.customer_id = orders.customer_id
```

---

# 2️⃣8️⃣ Common Beginner Mistake

ভুল:

```sql
SELECT *
FROM customers
JOIN orders;
```

Database বুঝবে না কীভাবে match করবে।

সাধারণত দরকার:

```sql
ON customers.customer_id = orders.customer_id
```

---

# 2️⃣9️⃣ Another Common Mistake — Wrong Relationship

ধরি:

```text
customers.customer_id
products.product_id
```

এগুলো unrelated IDs।

তাই:

```sql
ON customers.customer_id = products.product_id
```

লেখা logically ভুল হতে পারে।

Relationship বুঝে JOIN করতে হবে।

---

# 3️⃣0️⃣ JOIN Summary

```text
INNER JOIN
→ শুধু matching rows

LEFT JOIN
→ left-এর সব + matching right

RIGHT JOIN
→ right-এর সব + matching left
```

সবচেয়ে বেশি ব্যবহার করবে:

```text
INNER JOIN
LEFT JOIN
```

---

# 🧠 Query Building Formula

Real-world JOIN query বানানোর সময়:

```text
1. কোন data চাই?
        ↓
2. কোন table-এ আছে?
        ↓
3. কোন common key আছে?
        ↓
4. JOIN
        ↓
5. Filter দরকার?
        ↓
6. WHERE
        ↓
7. Summary দরকার?
        ↓
8. GROUP BY
        ↓
9. Group filter?
        ↓
10. HAVING
```

---

# 🎯 Class 35 Assignment

ধরি তিনটি table:

### Customers

```text
customer_id
name
city
```

### Products

```text
product_id
product_name
category
price
```

### Orders

```text
order_id
customer_id
product_id
quantity
amount
```

নিজে query লেখো:

### Q1

Orders-এর সাথে customer name দেখাও।

### Q2

Order-এর সাথে product name দেখাও।

### Q3

Customer name + product name + amount দেখাও।

### Q4

শুধু Dhaka customers-এর orders দেখাও।

### Q5

প্রতিটি customer-এর total purchase বের করো।

### Q6

প্রতিটি customer-এর order count বের করো।

### Q7

যেসব customer কোনো order করেনি তাদের বের করো।

### Q8

Category-wise total sales বের করো।

### Q9

সবচেয়ে বেশি purchase করা customer বের করো।

### Q10

50,000-এর বেশি purchase করা customers বের করো।

### Q11

প্রতিটি product কত units sold হয়েছে বের করো।

### Q12

প্রতিটি category-এর average order amount বের করো।

---

# 🧪 Class 35 Quiz

**1. দুই table-এর related data combine করতে?**

A. GROUP  
B. JOIN  
C. MERGE DATA  
D. CONNECT

**2. দুই table-এর matching rows?**

A. INNER JOIN  
B. LEFT JOIN  
C. RIGHT JOIN  
D. FULL JOIN

**3. Left table-এর সব rows রাখতে?**

A. INNER JOIN  
B. LEFT JOIN  
C. RIGHT JOIN  
D. CROSS JOIN

**4. JOIN-এর matching condition সাধারণত কোথায় লেখা হয়?**

A. WHERE  
B. ON  
C. GROUP  
D. MATCH

**5. Primary key অন্য table-এ reference করলে সেটি কী?**

A. Candidate Key  
B. Foreign Key  
C. Super Key  
D. Alternate Key

**6. Customer-এর order না থাকলেও customer দেখাতে চাইলে?**

A. INNER JOIN  
B. LEFT JOIN  
C. RIGHT JOIN  
D. None

**7. Customer-wise total purchase বের করতে কোন combination useful?**

A. JOIN + GROUP BY + SUM  
B. JOIN + ORDER BY only  
C. WHERE only  
D. DISTINCT only

**8. Group-এর result filter করতে?**

A. WHERE  
B. HAVING  
C. ON  
D. FILTER

**9. `ON customers.id = orders.customer_id` কী করছে?**

A. Sort  
B. Join relationship define  
C. Delete  
D. Group

**10. Real-world database-এ সবচেয়ে বেশি useful JOIN কোনগুলো?**

A. INNER এবং LEFT  
B. শুধু RIGHT  
C. শুধু CROSS  
D. শুধু FULL

---

# ⭐ Class 35 Cheat Sheet

```sql
-- INNER JOIN
SELECT *
FROM orders
INNER JOIN customers
ON orders.customer_id = customers.customer_id;
```

```sql
-- LEFT JOIN
SELECT *
FROM customers
LEFT JOIN orders
ON customers.customer_id = orders.customer_id;
```

```sql
-- Customer-wise total
SELECT
    customers.name,
    SUM(orders.amount) AS total_purchase
FROM customers
JOIN orders
ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_id, customers.name;
```

```sql
-- Customers without orders
SELECT customers.name
FROM customers
LEFT JOIN orders
ON customers.customer_id = orders.customer_id
WHERE orders.order_id IS NULL;
```

## 🔥 আজকের Golden Mental Model

```text
PRIMARY KEY
     ↓
Unique identity

FOREIGN KEY
     ↓
Relationship

JOIN
     ↓
Combine related tables

GROUP BY
     ↓
Summarize

HAVING
     ↓
Filter summary
```

**Next Class 36:** আমরা JOIN আরও গভীরে যাব — **SELF JOIN, FULL OUTER JOIN concept, CROSS JOIN, multiple JOIN এবং JOIN-এর common mistakes**। এরপর আমরা **Subquery + CTE**-তে যাব, যা SQL interview এবং Data Analytics-এর জন্য খুব গুরুত্বপূর্ণ।

----
# 📘 SQL — Class 36

## 🔗 Advanced JOIN: SELF JOIN, FULL OUTER JOIN, CROSS JOIN & Multiple JOIN

Class 35-এ আমরা শিখেছি:

```text
INNER JOIN
LEFT JOIN
RIGHT JOIN
PRIMARY KEY
FOREIGN KEY
ON
JOIN + GROUP BY
```

আজ JOIN-এর advanced concepts শিখব। এগুলো বুঝলে real-world relational database অনেক বেশি পরিষ্কার হবে।

---

# 🎯 আজকের Learning Goals

আজ শিখবে:

1. Multiple JOIN
    
2. SELF JOIN
    
3. FULL OUTER JOIN
    
4. CROSS JOIN
    
5. JOIN-এর common mistakes
    
6. JOIN + GROUP BY + HAVING
    
7. JOIN + aggregate
    
8. কখন কোন JOIN ব্যবহার করবে
    

---

# 1️⃣ Multiple JOIN

বাস্তব database-এ সাধারণত শুধু দুইটি table থাকে না।

ধরি:

```text
customers
products
orders
```

Relationship:

```text
customers
    │
    │ customer_id
    ↓
orders
    │
    │ product_id
    ↓
products
```

---

## Example Tables

### Customers

|customer_id|name|city|
|---|---|---|
|1|Rahim|Dhaka|
|2|Karim|Chittagong|
|3|Hasan|Sylhet|

### Products

|product_id|product_name|category|price|
|---|---|---|--:|
|101|Laptop|Electronics|50000|
|102|Mouse|Accessories|1000|
|103|Monitor|Electronics|20000|

### Orders

|order_id|customer_id|product_id|quantity|
|---|--:|--:|--:|
|O001|1|101|2|
|O002|2|102|5|
|O003|1|103|1|

---

# 2️⃣ Three Table JOIN

Question:

> কোন customer কোন product কিনেছে?

```sql
SELECT
    customers.name,
    products.product_name,
    orders.quantity
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
JOIN products
    ON orders.product_id = products.product_id;
```

Result:

|name|product_name|quantity|
|---|---|--:|
|Rahim|Laptop|2|
|Karim|Mouse|5|
|Rahim|Monitor|1|

---

# 🧠 Query-টা কীভাবে চিন্তা করবে?

Start:

```text
orders
```

তারপর:

```text
orders → customers
```

তারপর:

```text
orders → products
```

অর্থাৎ:

```text
Orders
   │
   ├── Customer
   │
   └── Product
```

---

# 3️⃣ Multiple JOIN + Calculation

Question:

> প্রতিটি order-এর total price কত?

যেহেতু:

```text
quantity × product price
```

তাই:

```sql
SELECT
    orders.order_id,
    customers.name,
    products.product_name,
    orders.quantity,
    products.price,
    orders.quantity * products.price AS total_amount
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
JOIN products
    ON orders.product_id = products.product_id;
```

Result:

|order_id|name|product|qty|price|total_amount|
|---|---|---|--:|--:|--:|
|O001|Rahim|Laptop|2|50000|100000|
|O002|Karim|Mouse|5|1000|5000|
|O003|Rahim|Monitor|1|20000|20000|

🔥 এই ধরনের query Data Analytics-এ খুব common।

---

# 4️⃣ JOIN + GROUP BY

Question:

> Customer-wise total spending কত?

```sql
SELECT
    customers.customer_id,
    customers.name,
    SUM(orders.quantity * products.price) AS total_spending
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
JOIN products
    ON orders.product_id = products.product_id
GROUP BY
    customers.customer_id,
    customers.name;
```

Result:

|customer|total_spending|
|---|--:|
|Rahim|120000|
|Karim|5000|

---

# 5️⃣ JOIN + GROUP BY + HAVING

Question:

> যেসব customer 50,000-এর বেশি spend করেছে তাদের দেখাও।

```sql
SELECT
    customers.customer_id,
    customers.name,
    SUM(orders.quantity * products.price) AS total_spending
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
JOIN products
    ON orders.product_id = products.product_id
GROUP BY
    customers.customer_id,
    customers.name
HAVING SUM(orders.quantity * products.price) > 50000;
```

এখানে:

```text
JOIN
 ↓
Related data
 ↓
GROUP BY
 ↓
Customer-wise summary
 ↓
HAVING
 ↓
High-value customers
```

---

# 6️⃣ SELF JOIN 🔥

এখন একটু interesting concept।

**SELF JOIN = একই table-কে নিজের সাথে JOIN করা।**

কেন দরকার?

ধরো employee table:

|id|name|manager_id|
|--:|---|--:|
|1|Rahim|NULL|
|2|Karim|1|
|3|Hasan|1|
|4|Jamil|2|

এখানে:

```text
Rahim
 ├── Karim
 └── Hasan

Karim
 └── Jamil
```

`manager_id` employee table-এরই অন্য employee-এর `id` reference করছে।

---

# 7️⃣ SELF JOIN Query

Question:

> Employee-এর নাম এবং তার manager-এর নাম দেখাও।

```sql
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON e.manager_id = m.id;
```

এখানে:

```text
e = employee
m = manager
```

দুটোই একই table-এর alias।

Result:

|employee|manager|
|---|---|
|Rahim|NULL|
|Karim|Rahim|
|Hasan|Rahim|
|Jamil|Karim|

---

# 8️⃣ Alias কেন ব্যবহার করলাম?

একই table দুইবার ব্যবহার করছি:

```sql
employees e
```

এবং:

```sql
employees m
```

এগুলো alias।

তাই:

```sql
e.name
```

মানে employee side-এর name।

আর:

```sql
m.name
```

মানে manager side-এর name।

---

# 🧠 SELF JOIN Mental Model

```text
employees
   │
   ├── e = employee
   │
   └── m = manager
```

একই table:

```text
employees → employees
```

---

# 9️⃣ SELF JOIN কোথায় ব্যবহার হয়?

Common examples:

- Employee → Manager
    
- Category → Parent Category
    
- Location → Parent Location
    
- Organization hierarchy
    
- Referral relationship
    
- Family tree type data
    

---

# 🔟 FULL OUTER JOIN

Concept:

> দুই table-এর **সব rows** রাখবে।

ধরি:

Table A:

```text
1
2
3
```

Table B:

```text
2
3
4
```

FULL OUTER JOIN result:

```text
1
2
3
4
```

Matching হলে combine করবে।

---

# 1️⃣1️⃣ Important: MySQL

MySQL-এ native:

```sql
FULL OUTER JOIN
```

সরাসরি supported নয়।

PostgreSQL-এ:

```sql
FULL OUTER JOIN
```

supported।

---

# 1️⃣2️⃣ FULL OUTER JOIN Concept

PostgreSQL example:

```sql
SELECT
    customers.customer_id,
    customers.name,
    orders.order_id
FROM customers
FULL OUTER JOIN orders
    ON customers.customer_id = orders.customer_id;
```

এতে:

- order আছে এমন customer
    
- order নেই এমন customer
    
- customer-এর match নেই এমন order
    

সব side-এর rows preserve করার চেষ্টা করবে।

---

# 1️⃣3️⃣ CROSS JOIN

**CROSS JOIN = প্রতিটি row-এর সাথে অন্য table-এর প্রতিটি row combine করে।**

ধরি:

Table A:

```text
Red
Blue
```

Table B:

```text
Small
Large
```

CROSS JOIN:

```text
Red   Small
Red   Large
Blue  Small
Blue  Large
```

Total:

```text
2 × 2 = 4 rows
```

---

# 1️⃣4️⃣ CROSS JOIN Query

```sql
SELECT
    colors.color,
    sizes.size
FROM colors
CROSS JOIN sizes;
```

এখানে `ON` condition লাগে না।

---

# 1️⃣5️⃣ CROSS JOIN-এর Practical Use

ধরো:

Products:

```text
Laptop
Mouse
```

Sizes:

```text
Small
Large
```

সব possible combination:

```text
Laptop → Small
Laptop → Large
Mouse  → Small
Mouse  → Large
```

Product variants generate করতে কাজে লাগতে পারে।

⚠️ কিন্তু বড় table-এর ক্ষেত্রে rows খুব দ্রুত বেড়ে যেতে পারে।

যেমন:

```text
1000 × 1000
= 1,000,000 rows
```

তাই CROSS JOIN সাবধানে ব্যবহার করতে হয়।

---

# 1️⃣6️⃣ JOIN Types — Complete Picture

|JOIN|Result|
|---|---|
|INNER JOIN|Matching rows|
|LEFT JOIN|Left-এর সব + matching right|
|RIGHT JOIN|Right-এর সব + matching left|
|FULL OUTER JOIN|দুই side-এর সব rows|
|CROSS JOIN|Every combination|
|SELF JOIN|Same table-এর সাথে নিজেই JOIN|

---

# 1️⃣7️⃣ কোন JOIN কখন?

### INNER JOIN

যখন শুধু matching data দরকার।

```text
Customers + Orders
```

যাদের order আছে।

---

### LEFT JOIN

যখন left table-এর **সব records** রাখতে হবে।

Example:

> সব customers, তাদের order থাকুক বা না থাকুক।

---

### RIGHT JOIN

যখন right table-এর সব records রাখতে হবে।

তবে অনেক developer LEFT JOIN-কে বেশি prefer করে, কারণ table order বদলে একই logic clearer করা যায়।

---

### FULL OUTER JOIN

যখন দুই side-এর unmatched data-ও দরকার।

---

### SELF JOIN

যখন table-এর ভিতরেই hierarchy/relationship আছে।

---

### CROSS JOIN

যখন intentionalভাবে সব possible combinations দরকার।

---

# 1️⃣8️⃣ JOIN-এর Common Mistake — Missing ON

ভুল:

```sql
SELECT *
FROM customers
JOIN orders;
```

সঠিক:

```sql
SELECT *
FROM customers
JOIN orders
ON customers.customer_id = orders.customer_id;
```

---

# 1️⃣9️⃣ Common Mistake — Wrong Column

ধরি:

```text
customers.customer_id
orders.customer_id
```

তাহলে:

```sql
ON customers.customer_id = orders.customer_id
```

ঠিক।

কিন্তু:

```sql
ON customers.customer_id = orders.order_id
```

সাধারণত ভুল relationship।

---

# 2️⃣0️⃣ Common Mistake — Duplicate Rows

ধরো একজন customer-এর 10টি order আছে।

Customer-কে Orders-এর সাথে JOIN করলে customer-এর name **10 rows-এ দেখা যেতে পারে**।

এটা error নয়।

কারণ relationship:

```text
1 Customer
   ↓
10 Orders
```

তাই result-এ 10 matching rows আসবে।

---

# 2️⃣1️⃣ JOIN করলে Row কেন বাড়ে?

ধরো:

Customers:

```text
Rahim
```

Orders:

```text
O001
O002
O003
```

JOIN:

```text
Rahim | O001
Rahim | O002
Rahim | O003
```

একজন customer তিনটি order করেছে।

তাই তিনটি result row।

---

# 2️⃣2️⃣ JOIN + DISTINCT

যদি শুধু unique customers চাই:

```sql
SELECT DISTINCT
    customers.customer_id,
    customers.name
FROM customers
JOIN orders
    ON customers.customer_id = orders.customer_id;
```

এতে একই customer-এর multiple order থাকলেও customer একবার আসবে।

---

# 2️⃣3️⃣ JOIN + WHERE + GROUP BY + HAVING

একটি full real-world example:

> Dhaka customers-এর মধ্যে যেসব customer 50,000-এর বেশি spend করেছে তাদের নাম ও total spending দেখাও।

```sql
SELECT
    customers.customer_id,
    customers.name,
    SUM(orders.quantity * products.price) AS total_spending
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
JOIN products
    ON orders.product_id = products.product_id
WHERE customers.city = 'Dhaka'
GROUP BY
    customers.customer_id,
    customers.name
HAVING SUM(orders.quantity * products.price) > 50000
ORDER BY total_spending DESC;
```

🔥 এই একটি query-তে:

```text
JOIN
WHERE
GROUP BY
SUM
HAVING
ORDER BY
```

সব ব্যবহার হয়েছে।

---

# 2️⃣4️⃣ SQL Query Building Strategy

কোনো complex question দেখলে একসাথে query লিখতে যেও না।

এই order follow করো:

### Step 1 — কোন table লাগবে?

```text
customers
orders
products
```

### Step 2 — Relationship কী?

```text
customers.customer_id
        ↓
orders.customer_id

products.product_id
        ↓
orders.product_id
```

### Step 3 — JOIN

### Step 4 — Filter হলে WHERE

### Step 5 — Calculation হলে SUM/AVG/COUNT

### Step 6 — Group হলে GROUP BY

### Step 7 — Group filter হলে HAVING

### Step 8 — Sort হলে ORDER BY

### Step 9 — Top N হলে LIMIT

---

# 🧠 Full SQL Mental Model

```text
Tables
  ↓
JOIN
  ↓
WHERE
  ↓
GROUP BY
  ↓
HAVING
  ↓
SELECT
  ↓
ORDER BY
  ↓
LIMIT
```

এটা conceptual processing order-এর simplified learning model; SQL engine internally আরও sophisticatedভাবে optimize করতে পারে।

---

# 🎯 Class 36 Assignment

ধরি:

### Employees

```text
id
name
manager_id
department
salary
```

### Customers

```text
customer_id
name
city
```

### Products

```text
product_id
product_name
category
price
```

### Orders

```text
order_id
customer_id
product_id
quantity
```

নিজে query লেখো:

### Q1

Customer + order information দেখাও।

### Q2

Customer + product + quantity দেখাও।

### Q3

Customer-এর total spending বের করো।

### Q4

Category-wise total sales বের করো।

### Q5

যেসব customer 50,000-এর বেশি spend করেছে।

### Q6

যেসব customer কোনো order করেনি।

### Q7

প্রতিটি product কত units sold হয়েছে।

### Q8

সবচেয়ে বেশি units sold হওয়া product।

### Q9

Employee এবং Manager-এর নাম দেখাও।  
**Hint: SELF JOIN**

### Q10

শুধু যেসব employee-এর manager আছে তাদের দেখাও।

### Q11

Unique customers যারা অন্তত একটি order করেছে।

### Q12

Dhaka customers-এর category-wise sales।

---

# 🧪 Class 36 Quiz

**1. Same table-এর সাথে নিজেকেই JOIN করলে?**

A. INNER JOIN  
B. SELF JOIN  
C. CROSS JOIN  
D. FULL JOIN

**2. Every possible combination কোন JOIN তৈরি করে?**

A. LEFT  
B. INNER  
C. CROSS  
D. SELF

**3. FULL OUTER JOIN-এর মূল উদ্দেশ্য?**

A. শুধু matching rows  
B. শুধু left rows  
C. দুই side-এর সব rows রাখা  
D. সব rows delete

**4. MySQL-এ native FULL OUTER JOIN আছে?**

A. Yes  
B. No

**5. Employee-manager relationship-এর জন্য কোন JOIN useful?**

A. SELF JOIN  
B. CROSS JOIN  
C. FULL JOIN  
D. None

**6. JOIN-এর relationship condition সাধারণত?**

A. ON  
B. HAVING  
C. ORDER  
D. LIMIT

**7. একজন customer-এর 5 orders থাকলে normal JOIN result-এ customer কতবার আসতে পারে?**

A. 1  
B. 2  
C. 5  
D. 0

**8. Unique customer list বের করতে?**

A. DISTINCT  
B. UNIQUE JOIN  
C. ONLY  
D. SINGLE

**9. Product + Customer + Orders-এর জন্য?**

A. Multiple JOIN  
B. শুধু WHERE  
C. শুধু GROUP BY  
D. শুধু DISTINCT

**10. বড় table-এর উপর CROSS JOIN কেন risky?**

A. Data delete হয়  
B. Result rows খুব দ্রুত বেড়ে যেতে পারে  
C. Primary key automatically change হয়  
D. JOIN কাজ করে না

---

# ⭐ Class 36 Cheat Sheet

```sql
-- Multiple JOIN
SELECT ...
FROM orders
JOIN customers
ON orders.customer_id = customers.customer_id
JOIN products
ON orders.product_id = products.product_id;
```

```sql
-- SELF JOIN
SELECT
    e.name AS employee,
    m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.id;
```

```sql
-- CROSS JOIN
SELECT *
FROM colors
CROSS JOIN sizes;
```

```sql
-- JOIN + GROUP BY
SELECT
    customers.name,
    SUM(orders.amount) AS total
FROM customers
JOIN orders
ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_id, customers.name;
```

```sql
-- JOIN + HAVING
SELECT
    customers.name,
    SUM(orders.amount) AS total
FROM customers
JOIN orders
ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_id, customers.name
HAVING SUM(orders.amount) > 50000;
```

## 🔥 আজকের Golden Mental Model

```text
PRIMARY KEY
      ↓
FOREIGN KEY
      ↓
RELATIONSHIP
      ↓
JOIN
      ↓
GROUP BY
      ↓
HAVING
      ↓
BUSINESS INSIGHT
```

পরের ধাপে আমরা **Class 37: Subquery** শুরু করব—যেখানে একটি SQL query-এর result আরেকটি query-এর ভিতরে ব্যবহার করব। তারপর **CTE (`WITH`)**, Window Functions এবং Advanced SQL Analytics-এর দিকে যাব।


----
# 📘 SQL — Class 37

## 🧩 Subquery — Query-এর ভিতরে Query

Class 35–36-এ আমরা JOIN শিখেছি। আজ আমরা SQL-এর আরেকটি powerful concept শিখব:

> **Subquery = একটি SQL query-এর ভিতরে আরেকটি SQL query।**

এটা Data Analyst, Database Designer এবং SQL interview—তিন জায়গাতেই গুরুত্বপূর্ণ।

---

# 🎯 আজকের Learning Goals

আজ শিখবে:

1. Subquery কী
    
2. Single-row Subquery
    
3. Multiple-row Subquery
    
4. `IN` + Subquery
    
5. `>` `<` `=` + Subquery
    
6. Subquery with `AVG()`, `MAX()`, `MIN()`
    
7. Correlated Subquery-এর ধারণা
    
8. Subquery বনাম JOIN
    
9. Real-world business questions
    

---

# 1️⃣ Subquery কী?

সাধারণ query:

```sql
SELECT *
FROM employees;
```

Subquery হলে:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

এখানে:

```sql
SELECT AVG(salary)
FROM employees
```

হলো **inner query / subquery**।

আর:

```sql
SELECT *
FROM employees
WHERE salary > (...);
```

হলো **outer query**।

---

# 2️⃣ সহজ Example

ধরি salaries:

|Name|Salary|
|---|--:|
|Rahim|40000|
|Karim|50000|
|Hasan|60000|
|Jamil|80000|

Average:

```text
57500
```

Question:

> Average salary-এর চেয়ে বেশি salary যাদের, তাদের দেখাও।

প্রথমে average বের করা যায়:

```sql
SELECT AVG(salary)
FROM employees;
```

তারপর:

```sql
SELECT *
FROM employees
WHERE salary > 57500;
```

কিন্তু manually `57500` লিখতে হবে না।

Subquery:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

🔥 এটাই Subquery।

---

# 3️⃣ Query কীভাবে কাজ করছে?

ভেতরের query:

```sql
SELECT AVG(salary)
FROM employees;
```

ধরি result:

```text
57500
```

তখন outer query conceptually হয়ে যায়:

```sql
SELECT *
FROM employees
WHERE salary > 57500;
```

---

# 4️⃣ Subquery-এর Basic Structure

```sql
SELECT ...
FROM ...
WHERE column operator (
    SELECT ...
    FROM ...
);
```

যেমন:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# 5️⃣ Subquery + MAX()

Question:

> সবচেয়ে বেশি salary পাওয়া employee দেখাও।

প্রথমে:

```sql
SELECT MAX(salary)
FROM employees;
```

তারপর:

```sql
SELECT *
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

এখানে subquery maximum salary বের করছে।

---

# 6️⃣ Subquery + MIN()

সবচেয়ে কম salary:

```sql
SELECT *
FROM employees
WHERE salary = (
    SELECT MIN(salary)
    FROM employees
);
```

---

# 7️⃣ Subquery + COUNT()

Question:

> যেসব department-এ 3-এর বেশি employee আছে, তাদের department দেখাও।

একভাবে `GROUP BY + HAVING` দিয়ে করা যায়:

```sql
SELECT department
FROM employees
GROUP BY department
HAVING COUNT(*) > 3;
```

Subquery দিয়ে আরও complex situations-এ similar logic তৈরি করা যায়।

তবে **শুধু সহজ aggregation-এর জন্য অকারণে subquery ব্যবহার করা উচিত নয়**।

---

# 8️⃣ Multiple-Row Subquery

এখন গুরুত্বপূর্ণ বিষয়।

ধরি:

```sql
SELECT department
FROM employees
WHERE city = 'Dhaka';
```

এটা একাধিক department return করতে পারে:

```text
IT
HR
Finance
```

এখন যদি query লিখি:

```sql
SELECT *
FROM employees
WHERE department = (
    SELECT department
    FROM employees
    WHERE city = 'Dhaka'
);
```

সমস্যা হতে পারে, কারণ `=` সাধারণত একটি single value expect করে।

এক্ষেত্রে `IN` ব্যবহার করা যায়।

---

# 9️⃣ IN + Subquery 🔥

```sql
SELECT *
FROM employees
WHERE department IN (
    SELECT department
    FROM employees
    WHERE city = 'Dhaka'
);
```

ভেতরের query:

```sql
SELECT department
FROM employees
WHERE city = 'Dhaka';
```

ধরি result:

```text
IT
HR
Finance
```

Outer query:

```text
department IN ('IT', 'HR', 'Finance')
```

---

# 🔟 Real Example — Customer Orders

ধরি:

### Customers

|customer_id|name|city|
|---|---|---|
|1|Rahim|Dhaka|
|2|Karim|Chittagong|
|3|Hasan|Dhaka|

### Orders

|order_id|customer_id|amount|
|---|--:|--:|
|O001|1|50000|
|O002|2|1000|
|O003|3|70000|

Question:

> Dhaka-এর customers-এর orders দেখাও।

Subquery:

```sql
SELECT *
FROM orders
WHERE customer_id IN (
    SELECT customer_id
    FROM customers
    WHERE city = 'Dhaka'
);
```

---

# 1️⃣1️⃣ এখানে কী হচ্ছে?

Inner query:

```sql
SELECT customer_id
FROM customers
WHERE city = 'Dhaka';
```

Result:

```text
1
3
```

Outer query:

```sql
SELECT *
FROM orders
WHERE customer_id IN (1, 3);
```

Result:

```text
O001
O003
```

---

# 1️⃣2️⃣ Subquery + `>`

Question:

> Average order amount-এর চেয়ে বেশি orders দেখাও।

```sql
SELECT *
FROM orders
WHERE amount > (
    SELECT AVG(amount)
    FROM orders
);
```

---

# 1️⃣3️⃣ Subquery + `<`

Average-এর চেয়ে কম:

```sql
SELECT *
FROM orders
WHERE amount < (
    SELECT AVG(amount)
    FROM orders
);
```

---

# 1️⃣4️⃣ Subquery + `>=`

Average-এর সমান বা বেশি:

```sql
SELECT *
FROM employees
WHERE salary >= (
    SELECT AVG(salary)
    FROM employees
);
```

---

# 1️⃣5️⃣ Subquery + `NOT IN`

Dhaka customers ছাড়া অন্য customers-এর orders:

```sql
SELECT *
FROM orders
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM customers
    WHERE city = 'Dhaka'
);
```

⚠️ `NOT IN` এবং `NULL` একসাথে থাকলে unexpected behavior হতে পারে। Real SQL-এ NULL handling সম্পর্কে সতর্ক থাকতে হয়।

---

# 1️⃣6️⃣ Subquery in SELECT

Subquery শুধু `WHERE`-এর মধ্যে নয়, `SELECT`-এর মধ্যেও থাকতে পারে।

Example:

```sql
SELECT
    name,
    salary,
    (SELECT AVG(salary) FROM employees) AS average_salary
FROM employees;
```

Result conceptually:

|name|salary|average_salary|
|---|--:|--:|
|Rahim|40000|57500|
|Karim|50000|57500|
|Hasan|60000|57500|
|Jamil|80000|57500|

---

# 1️⃣7️⃣ Salary Difference

এখন:

> প্রত্যেক employee-এর salary এবং company average salary-এর difference দেখাও।

```sql
SELECT
    name,
    salary,
    salary - (
        SELECT AVG(salary)
        FROM employees
    ) AS difference_from_average
FROM employees;
```

Result conceptually:

|name|salary|difference|
|---|--:|--:|
|Rahim|40000|-17500|
|Karim|50000|-7500|
|Hasan|60000|2500|
|Jamil|80000|22500|

🔥 এটা analytics-এ useful।

---

# 1️⃣8️⃣ Subquery in FROM

Subquery-কে temporary table-এর মতোও ব্যবহার করা যায়।

Example:

```sql
SELECT *
FROM (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
) AS dept_summary;
```

ভেতরের query:

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

এটা temporary result তৈরি করে।

তারপর outer query সেটার উপর কাজ করে।

---

# 1️⃣9️⃣ Subquery in FROM — Filter

ধরি department-wise average salary বের করলাম।

তারপর শুধু average salary > 50,000 departments চাই:

```sql
SELECT *
FROM (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
) AS dept_summary
WHERE avg_salary > 50000;
```

এখানে খুব সুন্দর pattern:

```text
employees
   ↓
GROUP BY department
   ↓
average salary
   ↓
temporary result
   ↓
WHERE avg_salary > 50000
```

---

# 2️⃣0️⃣ Correlated Subquery 🔥

এটা একটু advanced।

সাধারণ subquery:

```sql
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

Inner query independent।

কিন্তু **Correlated Subquery**-তে inner query outer query-এর current row-এর উপর depend করে।

Example:

> প্রত্যেক employee-এর department-এর average salary-এর চেয়ে বেশি salary যাদের, তাদের দেখাও।

```sql
SELECT
    e.name,
    e.department,
    e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e.department
);
```

---

# 2️⃣1️⃣ এই Query কী করছে?

ধরি:

```text
IT
Rahim   45000
Hasan   60000

HR
Karim   55000
Nabil   50000
```

Rahim-এর জন্য inner query:

```text
IT average
```

Hasan-এর জন্যও:

```text
IT average
```

Karim-এর জন্য:

```text
HR average
```

অর্থাৎ inner query outer row-এর department অনুযায়ী change হচ্ছে।

---

# 🧠 Correlated Subquery Mental Model

```text
Outer row
    ↓
Inner query
    ↓
Current row-এর সাথে related calculation
    ↓
Next outer row
    ↓
Inner query আবার
```

এজন্য correlated subquery অনেক ক্ষেত্রে বেশি expensive হতে পারে।

---

# 2️⃣2️⃣ Subquery বনাম JOIN

একই problem দুইভাবে solve করা যায়।

### Subquery

```sql
SELECT *
FROM orders
WHERE customer_id IN (
    SELECT customer_id
    FROM customers
    WHERE city = 'Dhaka'
);
```

### JOIN

```sql
SELECT orders.*
FROM orders
JOIN customers
    ON orders.customer_id = customers.customer_id
WHERE customers.city = 'Dhaka';
```

দুটোই valid হতে পারে।

---

# 2️⃣3️⃣ কখন JOIN?

যখন:

> দুই বা তার বেশি table-এর columns একসাথে output-এ দরকার।

Example:

```text
Customer Name
Product Name
Order Amount
```

তখন JOIN natural choice।

---

# 2️⃣4️⃣ কখন Subquery?

যখন:

> একটি query-এর result আরেকটি query-এর condition বা calculation হিসেবে দরকার।

Example:

> Average salary-এর চেয়ে বেশি salary।

```sql
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
```

---

# 2️⃣5️⃣ JOIN vs Subquery — Simple Rule

```text
Need columns from another table?
        ↓
JOIN

Need result of another query?
        ↓
Subquery
```

তবে একই problem দুইভাবে solve করা সম্ভব হতে পারে। Performance ও readability অনুযায়ী choice করতে হয়।

---

# 2️⃣6️⃣ Business Question → Subquery

### Question 1

> Average salary-এর বেশি salary কার?

```sql
SELECT name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

### Question 2

> Highest salary কার?

```sql
SELECT name, salary
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

---

### Question 3

> Lowest salary কার?

```sql
SELECT name, salary
FROM employees
WHERE salary = (
    SELECT MIN(salary)
    FROM employees
);
```

---

### Question 4

> Dhaka customers-এর orders দেখাও।

```sql
SELECT *
FROM orders
WHERE customer_id IN (
    SELECT customer_id
    FROM customers
    WHERE city = 'Dhaka'
);
```

---

### Question 5

> Company average-এর চেয়ে বেশি salary পাওয়া employees-এর count কত?

```sql
SELECT COUNT(*)
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

---

# 2️⃣7️⃣ Important: `=` বনাম `IN`

### Inner query এক value দিলে:

```sql
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
```

`AVG()` → একটি value।

তাই `>`, `<`, `=` ইত্যাদি ব্যবহার করা যায়।

### Inner query multiple values দিলে:

```sql
WHERE customer_id IN (
    SELECT customer_id
    FROM customers
    WHERE city = 'Dhaka'
)
```

এখানে multiple IDs আসতে পারে।

তাই `IN` useful।

---

# 2️⃣8️⃣ Common Mistakes

### Mistake 1 — Multiple rows-এর সাথে `=`

ভুল হতে পারে:

```sql
WHERE department = (
    SELECT department
    FROM employees
    WHERE city = 'Dhaka'
);
```

যদি inner query multiple departments দেয়।

Better:

```sql
WHERE department IN (
    SELECT department
    FROM employees
    WHERE city = 'Dhaka'
);
```

---

### Mistake 2 — Subquery-তে wrong column

যদি outer query:

```text
customer_id
```

চায়, inner query-তে সেই compatible value দিতে হবে।

---

### Mistake 3 — NULL with NOT IN

`NOT IN` এবং NULL থাকলে SQL three-valued logic-এর কারণে unexpected result হতে পারে।

এই ধরনের case-এ `NOT EXISTS` অনেক সময় safer pattern। এটা আমরা পরে শিখব।

---

# 2️⃣9️⃣ SQL Subquery Cheat Sheet

```sql
-- Above average
SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

```sql
-- Maximum
SELECT *
FROM employees
WHERE salary = (
    SELECT MAX(salary)
    FROM employees
);
```

```sql
-- Minimum
SELECT *
FROM employees
WHERE salary = (
    SELECT MIN(salary)
    FROM employees
);
```

```sql
-- Multiple values
SELECT *
FROM orders
WHERE customer_id IN (
    SELECT customer_id
    FROM customers
    WHERE city = 'Dhaka'
);
```

```sql
-- Subquery in FROM
SELECT *
FROM (
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
) AS dept_summary;
```

```sql
-- Correlated Subquery
SELECT e.name, e.department, e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e.department
);
```

---

# 🎯 Class 37 Assignment

নিজে query লেখো।

### Q1

Average salary-এর চেয়ে বেশি salary পাওয়া employees।

### Q2

Average salary-এর চেয়ে কম salary পাওয়া employees।

### Q3

Highest salary পাওয়া employee।

### Q4

Lowest salary পাওয়া employee।

### Q5

Average salary-এর বেশি salary পাওয়া employee-এর count।

### Q6

Dhaka customers-এর orders।

### Q7

Dhaka customers ছাড়া অন্য customers-এর orders।

### Q8

প্রতিটি employee-এর salary এবং company average salary দেখাও।

### Q9

প্রতিটি employee-এর salary company average-এর তুলনায় কত বেশি/কম তা বের করো।

### Q10

প্রতিটি department-এর average salary বের করে শুধু যেসব department-এর average > 50,000 সেগুলো দেখাও।

### Q11 — ⭐ Advanced

Employee-এর department average salary-এর চেয়ে বেশি salary যাদের, তাদের বের করো।

### Q12 — ⭐ Advanced

প্রতিটি customer-এর total spending বের করে company-wide average customer spending-এর চেয়ে বেশি spending করা customers বের করার চেষ্টা করো।

---

# 🧪 Class 37 Quiz

**1. Query-এর ভিতরে query কী?**

A. JOIN  
B. Subquery  
C. Function  
D. Trigger

**2. Average salary-এর চেয়ে বেশি salary বের করতে কোন pattern?**

A. `salary > AVG()`  
B. `salary > (SELECT AVG(...))`  
C. `salary = GROUP BY`  
D. `salary HAVING AVG`

**3. Inner query একটি value return করলে কোন operator ব্যবহার করা যায়?**

A. `=`  
B. `>`  
C. `<`  
D. সবগুলো

**4. Inner query multiple values return করলে কোনটি useful?**

A. IN  
B. =  
C. ONLY  
D. SAME

**5. `MAX(salary)` সাধারণত কয়টি value return করে?**

A. অনেক  
B. একটি  
C. শূন্য সবসময়  
D. table-এর সমান

**6. Correlated subquery-এর inner query কীসের উপর depend করে?**

A. Database name  
B. Outer query-এর current row  
C. Table name only  
D. ORDER BY

**7. অন্য table-এর columns output-এ আনতে কোনটি সাধারণত natural?**

A. JOIN  
B. LIMIT  
C. HAVING  
D. DISTINCT

**8. Subquery `FROM`-এর মধ্যে থাকলে তাকে কীভাবে ভাবা যায়?**

A. Temporary result/table  
B. Primary key  
C. Foreign key  
D. Index

**9. `IN (subquery)` কেন ব্যবহার করা হয়?**

A. Multiple possible values match করতে  
B. Sorting করতে  
C. Delete করতে  
D. Table create করতে

**10. `NOT IN` + NULL-এর ক্ষেত্রে কী হতে পারে?**

A. কোনো সমস্যা নেই সবসময়  
B. Unexpected/unknown results হতে পারে  
C. Automatically NULL delete হয়  
D. Table drop হয়

---

# ⭐ আজকের Golden Mental Model

```text
SUBQUERY
   ↓
একটি query
   ↓
আরেকটি query-এর result তৈরি করে
   ↓
Outer query সেই result ব্যবহার করে
```

সবচেয়ে গুরুত্বপূর্ণ তিনটি pattern:

```sql
-- 1. Single value
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

```sql
-- 2. Multiple values
WHERE customer_id IN (
    SELECT customer_id
    FROM customers
    WHERE city = 'Dhaka'
);
```

```sql
-- 3. Correlated
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e.department
);
```

### 🧠 মনে রাখো:

**JOIN = related tables combine করার tool**

**Subquery = একটি query-এর result অন্য query-তে ব্যবহার করার tool**

**GROUP BY = data summarize করার tool**

**HAVING = summarized group filter করার tool**

**Next Class 38:** **CTE (`WITH`) + Subquery-এর cleaner alternative** — complex SQL query কীভাবে ছোট ছোট logical steps-এ লেখা যায়, এবং `WITH` ব্যবহার করে readable, professional SQL তৈরি করা যায়।



----
# 📘 SQL — Class 38

## 🧩 CTE (`WITH`) — Clean & Professional SQL

Class 37-এ আমরা **Subquery** শিখেছি। আজ শিখব **CTE — Common Table Expression**।

CTE মূলত complex query-কে ছোট ছোট logical অংশে ভাগ করে **readable, maintainable এবং professional** করে।

---

# 🎯 আজকের Learning Goals

আজ শিখবে:

1. CTE কী
    
2. `WITH` syntax
    
3. Simple CTE
    
4. CTE + WHERE
    
5. CTE + GROUP BY
    
6. Multiple CTE
    
7. CTE + JOIN
    
8. CTE বনাম Subquery
    
9. CTE দিয়ে real-world analytics
    
10. Recursive CTE-এর introduction
    

---

# 1️⃣ CTE কী?

**CTE = Common Table Expression**

সহজ ভাষায়:

> একটি query-এর result-কে temporary named result হিসেবে তৈরি করে, তারপর পরের query-তে ব্যবহার করা।

Basic structure:

```sql
WITH cte_name AS (
    SELECT ...
    FROM ...
)
SELECT *
FROM cte_name;
```

এখানে:

```text
WITH
 ↓
CTE তৈরি
 ↓
তারপর CTE ব্যবহার
```

---

# 2️⃣ সবচেয়ে সহজ Example

ধরি আমাদের employees table:

|id|name|department|salary|
|--:|---|---|--:|
|1|Rahim|IT|45000|
|2|Karim|HR|55000|
|3|Hasan|IT|60000|
|4|Jamil|Finance|70000|

Question:

> যাদের salary 50,000-এর বেশি তাদের দেখাও।

CTE:

```sql
WITH high_salary AS (
    SELECT *
    FROM employees
    WHERE salary > 50000
)
SELECT *
FROM high_salary;
```

Result:

|id|name|department|salary|
|--:|---|---|--:|
|2|Karim|HR|55000|
|3|Hasan|IT|60000|
|4|Jamil|Finance|70000|

---

# 3️⃣ CTE-এর Structure

```sql
WITH high_salary AS (
    SELECT *
    FROM employees
    WHERE salary > 50000
)
SELECT *
FROM high_salary;
```

ভেঙে দেখি:

### Part 1

```sql
WITH high_salary AS (...)
```

নাম দিলাম:

```text
high_salary
```

### Part 2

```sql
(
    SELECT *
    FROM employees
    WHERE salary > 50000
)
```

এই query result তৈরি করছে।

### Part 3

```sql
SELECT *
FROM high_salary;
```

এখন সেই result ব্যবহার করছি।

---

# 4️⃣ CTE কেন দরকার?

ধরি complex query:

```sql
SELECT *
FROM (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
) AS dept_summary
WHERE avg_salary > 50000;
```

এটা কাজ করবে।

কিন্তু CTE version:

```sql
WITH dept_summary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_summary
WHERE avg_salary > 50000;
```

দ্বিতীয়টা অনেক easier to read।

---

# 5️⃣ CTE + GROUP BY

Question:

> Department-wise average salary বের করো।

```sql
WITH dept_salary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_salary;
```

Result:

|department|avg_salary|
|---|--:|
|IT|52500|
|HR|55000|
|Finance|70000|

---

# 6️⃣ CTE Result-এর উপর Filter

এখন চাই:

> যেসব department-এর average salary 50,000-এর বেশি।

```sql
WITH dept_salary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_salary
WHERE avg_salary > 50000;
```

এখানে খুব clear workflow:

```text
employees
   ↓
GROUP BY department
   ↓
AVG salary
   ↓
dept_salary CTE
   ↓
WHERE avg_salary > 50000
```

---

# 7️⃣ CTE + ORDER BY

```sql
WITH dept_salary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_salary
ORDER BY avg_salary DESC;
```

Highest average salary আগে আসবে।

---

# 8️⃣ CTE + LIMIT

Top 2 departments:

```sql
WITH dept_salary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_salary
ORDER BY avg_salary DESC
LIMIT 2;
```

---

# 9️⃣ Multiple CTE 🔥

একটি query-তে একাধিক CTE থাকতে পারে।

ধরি আমরা চাই:

1. Department-wise average salary
    
2. Department-wise employee count
    

```sql
WITH dept_salary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
),
dept_count AS (
    SELECT
        department,
        COUNT(*) AS employee_count
    FROM employees
    GROUP BY department
)
SELECT
    dept_salary.department,
    dept_salary.avg_salary,
    dept_count.employee_count
FROM dept_salary
JOIN dept_count
    ON dept_salary.department = dept_count.department;
```

Result:

|department|avg_salary|employee_count|
|---|--:|--:|
|IT|52500|2|
|HR|55000|1|
|Finance|70000|1|

---

# 🔟 Multiple CTE Mental Model

```text
employees
   │
   ├──→ dept_salary
   │
   └──→ dept_count
          │
          ↓
        JOIN
          ↓
      Final Result
```

এটাই complex SQL organize করার একটি powerful technique।

---

# 1️⃣1️⃣ CTE + JOIN

ধরি:

### customers

```text
customer_id
name
city
```

### orders

```text
order_id
customer_id
amount
```

Question:

> Customer-wise total spending বের করো।

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_spending
    FROM orders
    GROUP BY customer_id
)
SELECT
    customers.name,
    customers.city,
    customer_sales.total_spending
FROM customers
JOIN customer_sales
    ON customers.customer_id = customer_sales.customer_id;
```

---

# 1️⃣2️⃣ CTE + JOIN + HAVING Equivalent

Question:

> যেসব customer 50,000-এর বেশি spend করেছে তাদের দেখাও।

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_spending
    FROM orders
    GROUP BY customer_id
)
SELECT
    customers.name,
    customer_sales.total_spending
FROM customers
JOIN customer_sales
    ON customers.customer_id = customer_sales.customer_id
WHERE customer_sales.total_spending > 50000;
```

এখানে aggregation আগে CTE-তে হয়ে গেছে।

---

# 1️⃣3️⃣ CTE বনাম Subquery

একই problem দুইভাবে করা যায়।

### Subquery

```sql
SELECT *
FROM (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
) AS dept_summary
WHERE avg_salary > 50000;
```

### CTE

```sql
WITH dept_summary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_summary
WHERE avg_salary > 50000;
```

### Difference

|Subquery|CTE|
|---|---|
|Query-এর ভিতরে থাকে|Query-এর শুরুতে named result|
|ছোট query-তে convenient|Complex query-তে readable|
|Nested হলে difficult হতে পারে|Multiple steps সহজ|
|Reuse সীমিত|একই CTE query-এর মধ্যে reuse করা সহজ|

---

# 1️⃣4️⃣ CTE কেন Professional SQL-এ Useful?

ধরি তোমার query 50 lines।

সব একসাথে লিখলে:

```text
SELECT
JOIN
JOIN
WHERE
GROUP BY
CASE
SUBQUERY
...
```

বোঝা কঠিন।

CTE ব্যবহার করলে:

```text
Step 1 → clean data
Step 2 → aggregate
Step 3 → calculate
Step 4 → filter
Step 5 → final result
```

এতে debugging-ও সহজ হয়।

---

# 1️⃣5️⃣ Real Data Analytics Example 🔥

Question:

> কোন customer-এর total purchase 50,000-এর বেশি এবং তাদের city কী?

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_purchase
    FROM orders
    GROUP BY customer_id
)
SELECT
    c.name,
    c.city,
    cs.total_purchase
FROM customers c
JOIN customer_sales cs
    ON c.customer_id = cs.customer_id
WHERE cs.total_purchase > 50000
ORDER BY cs.total_purchase DESC;
```

এখানে:

```text
Orders
 ↓
Customer-wise SUM
 ↓
customer_sales CTE
 ↓
JOIN Customers
 ↓
Filter > 50000
 ↓
Sort
```

🔥 এটা real-world analytics query-এর খুব common structure।

---

# 1️⃣6️⃣ CTE + CASE

CTE-এর ভিতরে calculated column-ও বানানো যায়।

```sql
WITH employee_status AS (
    SELECT
        name,
        department,
        salary,
        CASE
            WHEN salary >= 70000 THEN 'High'
            WHEN salary >= 50000 THEN 'Medium'
            ELSE 'Low'
        END AS salary_level
    FROM employees
)
SELECT *
FROM employee_status;
```

Result:

|name|department|salary|salary_level|
|---|---|--:|---|
|Rahim|IT|45000|Low|
|Karim|HR|55000|Medium|
|Hasan|IT|60000|Medium|
|Jamil|Finance|70000|High|

---

# 1️⃣7️⃣ CTE + Window Function Preview

এখন একটা important preview।

ধরি আমরা department-wise salary ranking করতে চাই।

```sql
WITH employee_rank AS (
    SELECT
        name,
        department,
        salary,
        RANK() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
)
SELECT *
FROM employee_rank;
```

এখানে আমরা নতুন concept দেখলাম:

```text
RANK()
OVER()
PARTITION BY
```

🔥 এগুলো **Window Functions**।

এগুলো পরের advanced SQL phase-এর অত্যন্ত গুরুত্বপূর্ণ অংশ।

---

# 1️⃣8️⃣ Recursive CTE — Introduction

CTE-এর আরেকটি powerful type:

> **Recursive CTE**

যেখানে CTE নিজেকেই reference করতে পারে।

Hierarchy data-এর জন্য useful।

Example:

```text
CEO
 ↓
Manager
 ↓
Team Lead
 ↓
Employee
```

Employee-manager hierarchy বের করতে Recursive CTE ব্যবহার করা যায়।

Basic structure:

```sql
WITH RECURSIVE employee_tree AS (
    -- Anchor
    SELECT
        id,
        name,
        manager_id
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive part
    SELECT
        e.id,
        e.name,
        e.manager_id
    FROM employees e
    JOIN employee_tree et
        ON e.manager_id = et.id
)
SELECT *
FROM employee_tree;
```

এটা এখন মুখস্থ করার দরকার নেই।

শুধু concept মনে রাখো:

```text
Recursive CTE
      ↓
Hierarchy / Tree
      ↓
Parent → Child → Grandchild
```

আমরা পরে আলাদা করে এটা practice করব।

---

# 1️⃣9️⃣ CTE-এর Important Rules

### Rule 1

CTE সাধারণত `WITH` দিয়ে শুরু হয়:

```sql
WITH name AS (...)
```

### Rule 2

Multiple CTE comma দিয়ে আলাদা হয়:

```sql
WITH
cte1 AS (...),
cte2 AS (...),
cte3 AS (...)
SELECT ...
```

### Rule 3

শেষে একটি main query থাকতে হয়।

```sql
WITH data AS (...)
SELECT *
FROM data;
```

### Rule 4

CTE-কে table-এর মতো reference করা যায়:

```sql
FROM data
```

---

# 2️⃣0️⃣ CTE-এর Common Mistakes

### ❌ Mistake 1 — CTE-এর পরে main query না দেওয়া

```sql
WITH data AS (
    SELECT *
    FROM employees
);
```

সাধারণভাবে CTE definition-এর পরে consuming query লাগবে।

সঠিক:

```sql
WITH data AS (
    SELECT *
    FROM employees
)
SELECT *
FROM data;
```

---

### ❌ Mistake 2 — Multiple CTE-তে ভুল comma

সঠিক:

```sql
WITH cte1 AS (...),
cte2 AS (...)
SELECT ...
```

---

### ❌ Mistake 3 — CTE-এর column alias ভুলে যাওয়া

যেমন:

```sql
AVG(salary)
```

এর বদলে:

```sql
AVG(salary) AS avg_salary
```

দেওয়া অনেক বেশি readable।

---

# 2️⃣1️⃣ CTE Query Building Strategy

Complex problem দেখলে:

### Step 1 — Raw data

```text
employees
```

### Step 2 — প্রথম calculation

```text
department-wise salary
```

### Step 3 — CTE

```sql
WITH dept_salary AS (...)
```

### Step 4 — দ্বিতীয় calculation/filter

```text
avg_salary > 50000
```

### Step 5 — JOIN দরকার হলে JOIN

### Step 6 — Final ORDER BY / LIMIT

---

# 🧠 Professional SQL Thinking

আগে তুমি হয়তো ভাবতে:

> "একটা huge query কীভাবে লিখব?"

এখন ভাববে:

> **"Problem-টাকে কয়েকটি logical step-এ কীভাবে ভাঙব?"**

উদাহরণ:

```text
Business Question
      ↓
Raw Data
      ↓
CTE 1: Clean / Filter
      ↓
CTE 2: Aggregate
      ↓
CTE 3: Calculate
      ↓
JOIN
      ↓
Final Filter
      ↓
ORDER BY
```

এটাই professional SQL thinking-এর গুরুত্বপূর্ণ অংশ।

---

# 🎯 Class 38 Assignment

নিজে query লেখার চেষ্টা করো।

### Q1

একটি CTE ব্যবহার করে salary > 50,000 employees দেখাও।

### Q2

Department-wise average salary বের করে average > 50,000 departments দেখাও।

### Q3

Department-wise employee count বের করে employee count > 3 departments দেখাও।

### Q4

Customer-wise total spending বের করো CTE ব্যবহার করে।

### Q5

50,000-এর বেশি spending করা customers দেখাও।

### Q6

Customer-এর name, city এবং total spending দেখাও।

### Q7

CTE ব্যবহার করে salary level তৈরি করো:

```text
>=70000 → High
>=50000 → Medium
<50000 → Low
```

### Q8 ⭐

Customer-wise total spending এবং customer city দেখাও, তারপর Dhaka customers filter করো।

### Q9 ⭐

দুইটি CTE তৈরি করো:

```text
CTE 1 → department average salary
CTE 2 → department employee count
```

তারপর JOIN করে একসাথে দেখাও।

### Q10 ⭐

CTE + `RANK()` ব্যবহার করে department-এর ভিতরে salary ranking করার চেষ্টা করো।

---

# 🧪 Class 38 Quiz

**1. CTE-এর পূর্ণরূপ কী?**

A. Common Table Expression  
B. Common Table Entity  
C. Create Table Expression  
D. Column Table Expression

**2. CTE কোন keyword দিয়ে শুরু হয়?**

A. `TABLE`  
B. `WITH`  
C. `CTE`  
D. `TEMP`

**3. CTE-এর result কীভাবে ব্যবহার করা যায়?**

A. Table-এর মতো  
B. শুধু INSERT-এর জন্য  
C. শুধু DELETE-এর জন্য  
D. ব্যবহার করা যায় না

**4. Multiple CTE কীভাবে আলাদা করা হয়?**

A. `AND`  
B. `JOIN`  
C. Comma `,`  
D. `OR`

**5. CTE complex query-তে কী improve করে?**

A. Readability  
B. Maintainability  
C. Logical organization  
D. সবগুলো

**6. CTE এবং Subquery-এর মধ্যে কোনটি complex multi-step query-তে সাধারণত বেশি readable?**

A. CTE  
B. DELETE  
C. INSERT  
D. DISTINCT

**7. Recursive CTE কোথায় useful?**

A. Hierarchy  
B. Tree structure  
C. Parent-child relationship  
D. সবগুলো

**8. নিচের কোনটি CTE-এর সঠিক শুরু?**

A. `CREATE CTE`  
B. `WITH data AS (...)`  
C. `START CTE`  
D. `TABLE data AS`

**9. Window function-এর সাথে CTE ব্যবহার করা যায়?**

A. Yes  
B. No

**10. CTE কি database-এর permanent table?**

A. Yes  
B. No

---

# ⭐ Class 38 Cheat Sheet

### Simple CTE

```sql
WITH data AS (
    SELECT *
    FROM employees
)
SELECT *
FROM data;
```

### CTE + GROUP BY

```sql
WITH dept_salary AS (
    SELECT
        department,
        AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_salary
WHERE avg_salary > 50000;
```

### Multiple CTE

```sql
WITH
dept_salary AS (
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
),
dept_count AS (
    SELECT department, COUNT(*) AS employee_count
    FROM employees
    GROUP BY department
)
SELECT *
FROM dept_salary
JOIN dept_count
ON dept_salary.department = dept_count.department;
```

### CTE + JOIN

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
)
SELECT
    c.name,
    c.city,
    cs.total_sales
FROM customers c
JOIN customer_sales cs
ON c.customer_id = cs.customer_id;
```

---

# 🔥 Class 31 → 38 পর্যন্ত তোমার SQL Progress

```text
Class 31 → SELECT, WHERE, ORDER BY
        ↓
Class 32 → CREATE TABLE, Constraints
        ↓
Class 33 → INSERT, UPDATE, DELETE, LIKE, IN, NULL
        ↓
Class 34 → GROUP BY, HAVING, Aggregation
        ↓
Class 35 → INNER/LEFT/RIGHT JOIN
        ↓
Class 36 → SELF/FULL/CROSS/MULTIPLE JOIN
        ↓
Class 37 → Subquery
        ↓
Class 38 → CTE
```

এখন তুমি **basic SQL থেকে intermediate SQL-এর দিকে চলে এসেছো।**

### 🚀 Next: Class 39 — Window Functions

এখানে আমরা শিখব:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
OVER()
PARTITION BY
ORDER BY inside OVER()
LAG()
LEAD()
Running Total
Top N per Group
```

এটা **Data Analyst / Data Engineer-এর জন্য খুব গুরুত্বপূর্ণ SQL topic**, বিশেষ করে ranking, sales analysis, salary analysis এবং time-series analysis-এর ক্ষেত্রে।



-----


# 📘 SQL — Class 39

## 🪟 Window Functions — `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `LAG()`, `LEAD()`

Class 38-এ আমরা **CTE** শিখেছি। আজ থেকে SQL-এর একটি খুব important advanced topic শুরু করছি:

> **Window Functions**

Data Analyst, BI Analyst, Data Engineer এবং SQL interview—সব জায়গাতেই এটা গুরুত্বপূর্ণ।

---

# 🎯 আজকের Learning Goals

আজ শিখবে:

1. Window Function কী
    
2. `OVER()`
    
3. `ORDER BY` inside `OVER()`
    
4. `PARTITION BY`
    
5. `ROW_NUMBER()`
    
6. `RANK()`
    
7. `DENSE_RANK()`
    
8. তিনটির difference
    
9. Top N per Group
    
10. `LAG()`
    
11. `LEAD()`
    
12. Running Total
    
13. CTE + Window Function
    

---

# 1️⃣ Window Function কী?

সহজভাবে:

> **Window Function rows-কে group না করে, প্রতিটি row-এর পাশে অতিরিক্ত calculation result দেয়।**

এটাই সবচেয়ে গুরুত্বপূর্ণ ধারণা।

---

## GROUP BY বনাম Window Function

ধরি:

|name|department|salary|
|---|---|--:|
|Rahim|IT|45000|
|Hasan|IT|60000|
|Karim|HR|55000|
|Jamil|HR|70000|

### GROUP BY

```sql
SELECT
    department,
    AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

Result:

|department|avg_salary|
|---|--:|
|IT|52500|
|HR|62500|

Original employee rows আর থাকে না।

---

### Window Function

```sql
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM employees;
```

Result:

|name|department|salary|department_avg|
|---|---|--:|--:|
|Rahim|IT|45000|52500|
|Hasan|IT|60000|52500|
|Karim|HR|55000|62500|
|Jamil|HR|70000|62500|

🔥 **Rows থাকল + calculation-এর result পাশে পেলাম।**

---

# 2️⃣ `OVER()` কী?

Window Function-এর মূল অংশ:

```sql
OVER()
```

Example:

```sql
SELECT
    name,
    salary,
    AVG(salary) OVER () AS company_avg
FROM employees;
```

এখানে পুরো table-এর average প্রতিটি row-তে দেখাবে।

---

# 3️⃣ `OVER()` + `ORDER BY`

এবার ranking করি।

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

ধরি:

|name|salary|
|---|--:|
|Jamil|70000|
|Hasan|60000|
|Karim|55000|
|Rahim|45000|

Result:

|name|salary|row_num|
|---|--:|--:|
|Jamil|70000|1|
|Hasan|60000|2|
|Karim|55000|3|
|Rahim|45000|4|

---

# 4️⃣ `ROW_NUMBER()`

`ROW_NUMBER()` প্রতিটি row-কে unique sequential number দেয়।

```sql
SELECT
    name,
    salary,
    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num
FROM employees;
```

Result:

```text
70000 → 1
60000 → 2
55000 → 3
45000 → 4
```

---

# 5️⃣ Duplicate Salary হলে কী হবে?

ধরি:

|name|salary|
|---|--:|
|Jamil|70000|
|Hasan|60000|
|Karim|60000|
|Rahim|45000|

`ROW_NUMBER()`:

|name|salary|row_num|
|---|--:|--:|
|Jamil|70000|1|
|Hasan|60000|2|
|Karim|60000|3|
|Rahim|45000|4|

দুইজনের salary একই হলেও number আলাদা।

---

# 6️⃣ `RANK()`

এখন `RANK()`।

```sql
SELECT
    name,
    salary,
    RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

Result:

|name|salary|rank|
|---|--:|--:|
|Jamil|70000|1|
|Hasan|60000|2|
|Karim|60000|2|
|Rahim|45000|4|

Notice:

```text
1
2
2
4
```

**3 বাদ গেছে।**

---

# 7️⃣ `DENSE_RANK()`

```sql
SELECT
    name,
    salary,
    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS salary_rank
FROM employees;
```

Result:

|name|salary|dense_rank|
|---|--:|--:|
|Jamil|70000|1|
|Hasan|60000|2|
|Karim|60000|2|
|Rahim|45000|3|

এখানে:

```text
1
2
2
3
```

কোনো number skip হয়নি।

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ Difference

ধরি salary:

```text
70000
60000
60000
45000
```

### ROW_NUMBER

```text
1
2
3
4
```

### RANK

```text
1
2
2
4
```

### DENSE_RANK

```text
1
2
2
3
```

---

# ⭐ সহজে মনে রাখো

|Function|Duplicate হলে|Gap হয়?|
|---|---|---|
|`ROW_NUMBER()`|আলাদা number|না|
|`RANK()`|একই rank|**হ্যাঁ**|
|`DENSE_RANK()`|একই rank|**না**|

---

# 8️⃣ `PARTITION BY`

এটা Window Function-এর সবচেয়ে important conceptগুলোর একটি।

> `PARTITION BY` data-কে logical groups-এ ভাগ করে, কিন্তু rows delete করে না।

---

## Example

Department-wise salary ranking:

```sql
SELECT
    name,
    department,
    salary,
    RANK() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS dept_rank
FROM employees;
```

Result:

|name|department|salary|dept_rank|
|---|---|--:|--:|
|Hasan|IT|60000|1|
|Rahim|IT|45000|2|
|Jamil|HR|70000|1|
|Karim|HR|55000|2|

এখানে IT এবং HR আলাদাভাবে rank হয়েছে।

---

# 9️⃣ `PARTITION BY` Mental Model

```text
Employees
     ↓
PARTITION BY department
     ↓
 ┌─────────────┐
 │ IT          │
 │ Rahim       │
 │ Hasan       │
 └─────────────┘

 ┌─────────────┐
 │ HR          │
 │ Karim       │
 │ Jamil       │
 └─────────────┘
     ↓
প্রতিটি group-এর ভিতরে ranking
```

---

# 🔟 Top Employee Per Department 🔥

এটা interview-এর খুব common problem।

Question:

> প্রতিটি department-এর highest-paid employee বের করো।

প্রথমে:

```sql
WITH ranked_employees AS (
    SELECT
        name,
        department,
        salary,
        RANK() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS dept_rank
    FROM employees
)
SELECT *
FROM ranked_employees
WHERE dept_rank = 1;
```

Result:

```text
IT → Hasan
HR → Jamil
```

🔥 এখানে আমরা ব্যবহার করেছি:

```text
CTE
+
RANK()
+
PARTITION BY
```

---

# 1️⃣1️⃣ Top 2 Employees Per Department

```sql
WITH ranked_employees AS (
    SELECT
        name,
        department,
        salary,
        RANK() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS dept_rank
    FROM employees
)
SELECT *
FROM ranked_employees
WHERE dept_rank <= 2;
```

এটাই:

> **Top N per Group**

---

# 1️⃣2️⃣ `ROW_NUMBER()` দিয়ে Top 1

```sql
WITH ranked_employees AS (
    SELECT
        name,
        department,
        salary,
        ROW_NUMBER() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rn
    FROM employees
)
SELECT *
FROM ranked_employees
WHERE rn = 1;
```

### কিন্তু একটা গুরুত্বপূর্ণ difference:

যদি একই department-এ দুইজনের salary একই এবং দুজনই highest হয়:

`ROW_NUMBER()` → একজনকে 1, অন্যজনকে 2 দেবে।

`RANK()` → দুজনকেই 1 দেবে।

তাই:

```text
একজন winner দরকার → ROW_NUMBER()
সব tied winner দরকার → RANK()
```

---

# 1️⃣3️⃣ `LAG()`

এবার ranking থেকে time-series analysis-এর দিকে যাই।

`LAG()`:

> বর্তমান row-এর আগের row-এর value দেয়।

ধরি sales:

|month|sales|
|---|--:|
|Jan|100000|
|Feb|120000|
|Mar|150000|
|Apr|130000|

Query:

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_sales
FROM monthly_sales;
```

Result:

|month|sales|previous_sales|
|---|--:|--:|
|Jan|100000|NULL|
|Feb|120000|100000|
|Mar|150000|120000|
|Apr|130000|150000|

---

# 1️⃣4️⃣ LAG দিয়ে Growth

Current sales:

```text
120000
```

Previous:

```text
100000
```

Growth:

```text
(120000 - 100000) / 100000
= 20%
```

SQL:

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_sales,
    ROUND(
        100.0 * (sales - LAG(sales) OVER (
            ORDER BY month
        ))
        / NULLIF(LAG(sales) OVER (
            ORDER BY month
        ), 0),
        2
    ) AS growth_percent
FROM monthly_sales;
```

প্রথম month-এর previous value নেই, তাই `NULL` থাকবে।

---

# 1️⃣5️⃣ `LEAD()`

`LEAD()` হলো `LAG()`-এর opposite।

> পরের row-এর value দেয়।

```sql
SELECT
    month,
    sales,
    LEAD(sales) OVER (
        ORDER BY month
    ) AS next_sales
FROM monthly_sales;
```

Result:

|month|sales|next_sales|
|---|--:|--:|
|Jan|100000|120000|
|Feb|120000|150000|
|Mar|150000|130000|
|Apr|130000|NULL|

---

# 🧠 LAG vs LEAD

```text
LAG
← Previous row

Current row

LEAD
→ Next row
```

সহজে:

```text
LAG  = পিছনে তাকাও
LEAD = সামনে তাকাও
```

---

# 1️⃣6️⃣ Running Total 🔥

এবার খুব useful analytics concept।

Sales:

|Month|Sales|
|---|--:|
|Jan|100|
|Feb|200|
|Mar|150|
|Apr|300|

Running total:

```text
Jan = 100
Feb = 300
Mar = 450
Apr = 750
```

SQL:

```sql
SELECT
    month,
    sales,
    SUM(sales) OVER (
        ORDER BY month
    ) AS running_total
FROM monthly_sales;
```

Result:

|month|sales|running_total|
|---|--:|--:|
|Jan|100|100|
|Feb|200|300|
|Mar|150|450|
|Apr|300|750|

🔥 Data Analytics-এ এটি খুব common।

---

# 1️⃣7️⃣ Department-wise Running Total

ধরি employee salary data।

```sql
SELECT
    name,
    department,
    salary,
    SUM(salary) OVER (
        PARTITION BY department
        ORDER BY salary
    ) AS running_salary
FROM employees;
```

এখানে প্রতিটি department আলাদাভাবে cumulative sum করবে।

---

# 1️⃣8️⃣ `AVG() OVER()`

Window Function শুধু ranking-এর জন্য নয়।

Company average:

```sql
SELECT
    name,
    salary,
    AVG(salary) OVER () AS company_avg
FROM employees;
```

প্রতিটি row-তে company average থাকবে।

---

# 1️⃣9️⃣ Department Average

```sql
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg
FROM employees;
```

এটা আগের GROUP BY-এর মতো aggregate করছে, কিন্তু employee rows রেখে দিচ্ছে।

---

# 2️⃣0️⃣ Salary vs Department Average

Question:

> Employee-এর salary তার department average-এর তুলনায় কত বেশি/কম?

```sql
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    ) AS department_avg,
    salary - AVG(salary) OVER (
        PARTITION BY department
    ) AS difference
FROM employees;
```

এটা খুব useful analytical query।

---

# 2️⃣1️⃣ Multiple Window Functions

একই query-তে অনেকগুলো window function ব্যবহার করা যায়।

```sql
SELECT
    name,
    department,
    salary,

    ROW_NUMBER() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS row_num,

    RANK() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS salary_rank,

    DENSE_RANK() OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS dense_rank

FROM employees;
```

---

# 2️⃣2️⃣ `OVER()`-এর তিনটি Important Part

একটা window expression:

```sql
RANK() OVER (
    PARTITION BY department
    ORDER BY salary DESC
)
```

এখানে:

### `PARTITION BY`

Group তৈরি করে।

### `ORDER BY`

Group-এর ভিতরে order ঠিক করে।

### Function

```text
RANK()
ROW_NUMBER()
SUM()
AVG()
LAG()
LEAD()
```

---

# 🧠 Window Function Formula

```text
FUNCTION()
    ↓
OVER(
    PARTITION BY ...
    ORDER BY ...
)
```

সবসময় তিনটিই লাগবে না।

Example:

```sql
AVG(salary) OVER ()
```

এখানে partition/order নেই।

---

# 2️⃣3️⃣ GROUP BY vs Window Function

|GROUP BY|Window Function|
|---|---|
|Rows collapse করে|Rows রাখে|
|প্রতি group-এ summary row|প্রতিটি original row থাকে|
|Aggregate analysis|Row-level + aggregate analysis|
|`GROUP BY`|`OVER()`|
|Department total|Employee + department total|

---

## Example

GROUP BY:

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

Window:

```sql
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    )
FROM employees;
```

**এই difference খুব ভালোভাবে বুঝে রাখো।**

---

# 2️⃣4️⃣ Real-world Example — Top 3 Products Per Category

ধরি:

```text
products
product_name
category
sales
```

Query:

```sql
WITH ranked_products AS (
    SELECT
        product_name,
        category,
        sales,
        RANK() OVER (
            PARTITION BY category
            ORDER BY sales DESC
        ) AS product_rank
    FROM products
)
SELECT *
FROM ranked_products
WHERE product_rank <= 3;
```

এটা বাস্তব Data Analyst-এর common query pattern।

---

# 2️⃣5️⃣ Real-world Example — Monthly Sales Growth

```sql
WITH sales_data AS (
    SELECT
        month,
        sales,
        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales
    FROM monthly_sales
)
SELECT
    month,
    sales,
    previous_sales,
    ROUND(
        100.0 * (sales - previous_sales)
        / NULLIF(previous_sales, 0),
        2
    ) AS growth_percent
FROM sales_data;
```

এখানে:

```text
CTE
 ↓
LAG
 ↓
Previous Month
 ↓
Growth %
```

🔥 এটা তোমার Excel-এর monthly growth calculation-এর SQL version হিসেবে ভাবতে পারো।

---

# 2️⃣6️⃣ Excel → SQL Connection

তুমি যেহেতু Excel Mastery শেষ করে SQL শিখছো, mappingটা খুব useful:

|Excel|SQL|
|---|---|
|Sort|ORDER BY|
|Filter|WHERE|
|PivotTable|GROUP BY|
|Pivot filter|HAVING|
|VLOOKUP/XLOOKUP|JOIN|
|Running Total|`SUM() OVER()`|
|Ranking|`RANK()`|
|Previous row|`LAG()`|
|Next row|`LEAD()`|
|Unique ranking|`ROW_NUMBER()`|
|Group-wise analysis|`PARTITION BY`|

---

# 🎯 Class 39 Assignment

নিজে query লেখার চেষ্টা করো।

### Q1

সব employees-কে salary অনুযায়ী descending `ROW_NUMBER()` দাও।

### Q2

Salary অনুযায়ী `RANK()` বের করো।

### Q3

Salary অনুযায়ী `DENSE_RANK()` বের করো।

### Q4

Department-এর ভিতরে salary ranking করো।

### Q5

প্রতিটি department-এর highest-paid employee বের করো।

### Q6

প্রতিটি department-এর Top 2 employee বের করো।

### Q7

প্রতিটি employee-এর department average salary দেখাও।

### Q8

Employee salary এবং department average-এর difference বের করো।

### Q9

Monthly sales-এর previous month sales বের করো `LAG()` দিয়ে।

### Q10

Monthly sales-এর next month sales বের করো `LEAD()` দিয়ে।

### Q11

Monthly running sales total বের করো।

### Q12 ⭐

প্রতিটি category-এর Top 3 products বের করো।

### Q13 ⭐

Monthly sales growth percentage বের করো।

### Q14 ⭐

প্রতিটি department-এর salary ranking + department average একসাথে দেখাও।

### Q15 🔥

CTE + `RANK()` ব্যবহার করে প্রতিটি department-এর highest-paid employee বের করো।

---

# 🧪 Class 39 Quiz

**1. Window Function-এর মূল keyword কোনটি?**

A. `WINDOW`  
B. `OVER()`  
C. `GROUP`  
D. `PARTITION()`

**2. `ROW_NUMBER()` duplicate value হলে কী করে?**

A. একই number দেয়  
B. Unique sequential number দেয়  
C. NULL দেয়  
D. Row delete করে

**3. `RANK()`-এ tie হলে কী হয়?**

A. Rank একই হয় এবং gap হতে পারে  
B. সব rank unique  
C. সবসময় gap হয় না  
D. Row delete হয়

**4. `DENSE_RANK()` এবং `RANK()`-এর প্রধান difference কী?**

A. DENSE_RANK tie support করে না  
B. DENSE_RANK gap skip করে না  
C. RANK sort করতে পারে না  
D. কোনো difference নেই

**5. Group-wise ranking-এর জন্য কোনটি ব্যবহার করা হয়?**

A. `PARTITION BY`  
B. `GROUP BY` only  
C. `LIMIT`  
D. `DISTINCT`

**6. Previous row-এর value পেতে?**

A. LEAD  
B. LAG  
C. RANK  
D. ROW

**7. Next row-এর value পেতে?**

A. LAG  
B. LEAD  
C. NEXT  
D. FORWARD

**8. Running total-এর জন্য কোন pattern useful?**

A. `SUM() OVER (ORDER BY ...)`  
B. `COUNT() ONLY`  
C. `AVG() GROUP`  
D. `SUM() WHERE`

**9. Window Function ব্যবহার করলে original rows সাধারণত কী হয়?**

A. Collapse হয়  
B. থাকে  
C. Delete হয়  
D. Duplicate সবসময় হয়

**10. Top 3 employees per department বের করার জন্য সবচেয়ে useful combination কোনটি?**

A. `RANK() + PARTITION BY`  
B. `DELETE + GROUP BY`  
C. `DISTINCT + LIMIT 3`  
D. `COUNT + HAVING`

---

# ⭐ Class 39 Cheat Sheet

### 1. Row Number

```sql
ROW_NUMBER() OVER (
    ORDER BY salary DESC
)
```

### 2. Rank

```sql
RANK() OVER (
    ORDER BY salary DESC
)
```

### 3. Dense Rank

```sql
DENSE_RANK() OVER (
    ORDER BY salary DESC
)
```

### 4. Department Ranking

```sql
RANK() OVER (
    PARTITION BY department
    ORDER BY salary DESC
)
```

### 5. Previous Row

```sql
LAG(sales) OVER (
    ORDER BY month
)
```

### 6. Next Row

```sql
LEAD(sales) OVER (
    ORDER BY month
)
```

### 7. Running Total

```sql
SUM(sales) OVER (
    ORDER BY month
)
```

### 8. Group Average

```sql
AVG(salary) OVER (
    PARTITION BY department
)
```

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ Mental Model

```text
                Window Function
                       ↓
                    OVER()
                       ↓
             ┌─────────┴─────────┐
             ↓                   ↓
       PARTITION BY          ORDER BY
       "কোন group?"          "কোন order?"
             ↓                   ↓
             └─────────┬─────────┘
                       ↓
             Calculation per row
```

আর এই তিনটা খুব ভালোভাবে মনে রাখো:

```text
ROW_NUMBER → 1,2,3,4
RANK       → 1,2,2,4
DENSE_RANK → 1,2,2,3
```

**Class 40**-এ আমরা Window Functions-এর আরও powerful অংশে যাব: **`FIRST_VALUE()`, `LAST_VALUE()`, `NTH_VALUE()`, window frame (`ROWS BETWEEN`), moving average, cumulative percentage এবং advanced running calculations**।


----
# 📘 SQL — Class 40

## 🪟 Advanced Window Functions — Window Frame, `FIRST_VALUE()`, `LAST_VALUE()`, Moving Average & Cumulative Analysis

Class 39-এ আমরা শিখেছি:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
PARTITION BY
LAG()
LEAD()
SUM() OVER()
```

আজ এগুলোর ওপর ভিত্তি করে **advanced analytics** করব।

---

# 🎯 আজকের Learning Goals

আজ শিখবে:

1. `FIRST_VALUE()`
    
2. `LAST_VALUE()`
    
3. `NTH_VALUE()`
    
4. Window Frame
    
5. `ROWS BETWEEN`
    
6. Running Total
    
7. Moving Average
    
8. Rolling Sum
    
9. Cumulative Percentage
    
10. Previous/Next comparison
    
11. Advanced CTE + Window Function
    

---

# 1️⃣ `FIRST_VALUE()`

`FIRST_VALUE()` একটি window-এর প্রথম row-এর value দেয়।

ধরি:

|month|sales|
|---|--:|
|Jan|100000|
|Feb|120000|
|Mar|150000|
|Apr|130000|

Query:

```sql
SELECT
    month,
    sales,
    FIRST_VALUE(sales) OVER (
        ORDER BY month
    ) AS first_sales
FROM monthly_sales;
```

Result:

|month|sales|first_sales|
|---|--:|--:|
|Jan|100000|100000|
|Feb|120000|100000|
|Mar|150000|100000|
|Apr|130000|100000|

অর্থাৎ প্রথম month's sales প্রত্যেক row-তে দেখাবে।

---

# 2️⃣ Practical Use

Question:

> Current month's sales এবং year's first month's sales compare করো।

```sql
SELECT
    month,
    sales,
    FIRST_VALUE(sales) OVER (
        ORDER BY month
    ) AS first_month_sales
FROM monthly_sales;
```

তারপর difference:

```sql
SELECT
    month,
    sales,
    FIRST_VALUE(sales) OVER (
        ORDER BY month
    ) AS first_month_sales,
    sales - FIRST_VALUE(sales) OVER (
        ORDER BY month
    ) AS difference
FROM monthly_sales;
```

---

# 3️⃣ `LAST_VALUE()`

`LAST_VALUE()` শুনতে সহজ হলেও এখানে একটি **খুব important window-frame issue** আছে।

Basic example:

```sql
SELECT
    month,
    sales,
    LAST_VALUE(sales) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING
    ) AS last_sales
FROM monthly_sales;
```

Result:

|month|sales|last_sales|
|---|--:|--:|
|Jan|100000|130000|
|Feb|120000|130000|
|Mar|150000|130000|
|Apr|130000|130000|

এখানে সব row-তে final month's sales এসেছে।

---

# ⚠️ কেন `ROWS BETWEEN` দিলাম?

কারণ `LAST_VALUE()`-এর ক্ষেত্রে window-এর **বর্তমান frame** খুব গুরুত্বপূর্ণ।

আমরা explicitly বলেছি:

```sql
ROWS BETWEEN UNBOUNDED PRECEDING
AND UNBOUNDED FOLLOWING
```

মানে:

```text
শুরু থেকে
   ↓
পুরো window
   ↓
শেষ পর্যন্ত
```

তাই সত্যিকারের last row-এর value পাওয়া যায়।

---

# 4️⃣ Window Frame কী?

এটা Class 40-এর সবচেয়ে গুরুত্বপূর্ণ concept।

Window-এর ভিতরে কোন rows calculation-এর অংশ হবে, সেটা **window frame** দিয়ে নির্ধারণ করা যায়।

Example:

```sql
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
```

মানে:

```text
আগের 2 rows
+
বর্তমান row
```

---

# 5️⃣ `UNBOUNDED PRECEDING`

মানে:

> Window-এর একদম শুরু থেকে।

```sql
ROWS BETWEEN UNBOUNDED PRECEDING
AND CURRENT ROW
```

এটা running total-এর জন্য খুব useful।

---

# 6️⃣ `CURRENT ROW`

মানে:

> বর্তমান row।

Example:

```sql
ROWS BETWEEN 2 PRECEDING
AND CURRENT ROW
```

---

# 7️⃣ `UNBOUNDED FOLLOWING`

মানে:

> Window-এর একদম শেষ পর্যন্ত।

```sql
ROWS BETWEEN CURRENT ROW
AND UNBOUNDED FOLLOWING
```

---

# 🧠 Window Frame Mental Model

ধরি:

```text
Jan
Feb
Mar
Apr
May
```

যদি current row = Mar এবং:

```sql
ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
```

তাহলে frame:

```text
Jan ←
Feb ←
Mar ← Current
```

অর্থাৎ:

```text
Jan + Feb + Mar
```

---

# 8️⃣ Running Total — Advanced Version

Class 39-এ আমরা লিখেছিলাম:

```sql
SELECT
    month,
    sales,
    SUM(sales) OVER (
        ORDER BY month
    ) AS running_total
FROM monthly_sales;
```

আরও explicit version:

```sql
SELECT
    month,
    sales,
    SUM(sales) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_total
FROM monthly_sales;
```

Result:

|month|sales|running_total|
|---|--:|--:|
|Jan|100|100|
|Feb|200|300|
|Mar|150|450|
|Apr|300|750|

---

# 9️⃣ Moving Average 🔥

এটা Data Analytics-এর খুব important concept।

ধরি:

|Month|Sales|
|---|--:|
|Jan|100|
|Feb|200|
|Mar|150|
|Apr|300|
|May|250|

আমরা **3-month moving average** চাই।

অর্থাৎ:

### Jan

শুধু Jan:

```text
100
```

### Feb

```text
(100 + 200) / 2 = 150
```

### Mar

```text
(100 + 200 + 150) / 3 = 150
```

### Apr

```text
(200 + 150 + 300) / 3
= 216.67
```

### May

```text
(150 + 300 + 250) / 3
= 233.33
```

SQL:

```sql
SELECT
    month,
    sales,
    AVG(sales) OVER (
        ORDER BY month
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS moving_avg_3
FROM monthly_sales;
```

🔥 এটাকে **3-period moving average** বলা হয়।

---

# 🔟 কেন Moving Average দরকার?

Real sales data:

```text
100
500
120
600
150
700
```

এখানে ওঠানামা অনেক বেশি।

Moving average:

```text
trend
───────→
```

দেখতে সাহায্য করে।

ব্যবহার:

- Sales trend
    
- Stock demand
    
- Website traffic
    
- Revenue forecasting-এর preliminary analysis
    
- Performance monitoring
    

---

# 1️⃣1️⃣ 3-Month Rolling Sum

Moving average-এর মতো rolling sum করা যায়।

```sql
SELECT
    month,
    sales,
    SUM(sales) OVER (
        ORDER BY month
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS rolling_3_month_sales
FROM monthly_sales;
```

Example:

|Month|Sales|Rolling 3 Month|
|---|--:|--:|
|Jan|100|100|
|Feb|200|300|
|Mar|150|450|
|Apr|300|650|
|May|250|700|

---

# 1️⃣2️⃣ 2-Row Moving Average

```sql
SELECT
    month,
    sales,
    AVG(sales) OVER (
        ORDER BY month
        ROWS BETWEEN 1 PRECEDING AND CURRENT ROW
    ) AS moving_avg_2
FROM monthly_sales;
```

Frame:

```text
Previous row
+
Current row
```

---

# 1️⃣3️⃣ `NTH_VALUE()`

`NTH_VALUE()` window-এর নির্দিষ্ট position-এর value নিতে পারে।

Example:

```sql
SELECT
    month,
    sales,
    NTH_VALUE(sales, 2) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING
    ) AS second_month_sales
FROM monthly_sales;
```

Result:

```text
সব row-তে
second month's sales
```

ধরি February = 120000:

|month|sales|second_month_sales|
|---|--:|--:|
|Jan|100000|120000|
|Feb|120000|120000|
|Mar|150000|120000|
|Apr|130000|120000|

---

# 1️⃣4️⃣ `FIRST_VALUE()` vs `LAST_VALUE()` vs `NTH_VALUE()`

|Function|কাজ|
|---|---|
|`FIRST_VALUE()`|প্রথম value|
|`LAST_VALUE()`|শেষ value|
|`NTH_VALUE()`|N-th value|

Example:

```text
100
200
300
400
```

```text
FIRST_VALUE → 100
LAST_VALUE  → 400
NTH_VALUE(..., 3) → 300
```

---

# 1️⃣5️⃣ Cumulative Percentage 🔥

ধরি monthly sales:

|Month|Sales|
|---|--:|
|Jan|100|
|Feb|200|
|Mar|300|
|Apr|400|

Total:

```text
1000
```

Running total:

```text
100
300
600
1000
```

Cumulative %:

```text
10%
30%
60%
100%
```

SQL:

```sql
SELECT
    month,
    sales,
    SUM(sales) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_total,

    100.0 *
    SUM(sales) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    )
    /
    SUM(sales) OVER () AS cumulative_percentage

FROM monthly_sales;
```

---

# 1️⃣6️⃣ Percentage of Total

এটা Data Analytics-এ খুব useful।

Question:

> প্রতিটি product মোট sales-এর কত % করেছে?

```sql
SELECT
    product,
    sales,
    100.0 * sales / SUM(sales) OVER () AS percentage_of_total
FROM product_sales;
```

Example:

|Product|Sales|% Total|
|---|--:|--:|
|Laptop|500|50%|
|Monitor|300|30%|
|Mouse|200|20%|

---

# 1️⃣7️⃣ Department-wise Percentage

ধরি:

|Department|Employee|Salary|
|---|---|--:|
|IT|Rahim|45000|
|IT|Hasan|60000|
|HR|Karim|50000|
|HR|Jamil|70000|

Question:

> Department-এর total salary-এর মধ্যে প্রত্যেক employee-এর salary কত %?

```sql
SELECT
    name,
    department,
    salary,
    100.0 * salary /
    SUM(salary) OVER (
        PARTITION BY department
    ) AS department_salary_percentage
FROM employees;
```

এখানে:

```text
SUM(salary) OVER(PARTITION BY department)
```

প্রতিটি department-এর total salary বের করছে।

---

# 1️⃣8️⃣ Previous vs Current

`LAG()` দিয়ে:

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_sales
FROM monthly_sales;
```

তারপর difference:

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_sales,
    
    sales - LAG(sales) OVER (
        ORDER BY month
    ) AS sales_difference
FROM monthly_sales;
```

---

# 1️⃣9️⃣ Growth Percentage

আরও professional version:

```sql
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_sales,

    100.0 *
    (sales - LAG(sales) OVER (
        ORDER BY month
    ))
    / NULLIF(
        LAG(sales) OVER (
            ORDER BY month
        ),
        0
    ) AS growth_percentage

FROM monthly_sales;
```

### `NULLIF()` কেন?

যদি previous sales = 0 হয়:

```text
division by zero
```

problem হতে পারে।

তাই:

```sql
NULLIF(previous_sales, 0)
```

0 হলে NULL করে দেয়।

---

# 2️⃣0️⃣ LAG + CTE — Cleaner Version

Repeated `LAG()` না লিখে:

```sql
WITH sales_comparison AS (
    SELECT
        month,
        sales,
        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales
    FROM monthly_sales
)
SELECT
    month,
    sales,
    previous_sales,
    100.0 * (sales - previous_sales)
    / NULLIF(previous_sales, 0) AS growth_percentage
FROM sales_comparison;
```

এটা অনেক cleaner।

🔥 **CTE + Window Function** খুব powerful combination।

---

# 2️⃣1️⃣ `PARTITION BY` + Moving Average

ধরি আমাদের sales আছে:

|Month|City|Sales|
|---|---|--:|
|Jan|Dhaka|100|
|Feb|Dhaka|200|
|Mar|Dhaka|300|
|Jan|Chittagong|50|
|Feb|Chittagong|100|
|Mar|Chittagong|150|

Question:

> City-wise 3-month moving average।

```sql
SELECT
    month,
    city,
    sales,
    AVG(sales) OVER (
        PARTITION BY city
        ORDER BY month
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS moving_avg_3
FROM city_sales;
```

এখানে Dhaka এবং Chittagong-এর calculations আলাদা হবে।

---

# 2️⃣2️⃣ Advanced Example — Top 3 + Percentage

প্রতিটি category-এর Top 3 products এবং category sales-এর percentage:

```sql
WITH product_analysis AS (
    SELECT
        product,
        category,
        sales,

        RANK() OVER (
            PARTITION BY category
            ORDER BY sales DESC
        ) AS product_rank,

        SUM(sales) OVER (
            PARTITION BY category
        ) AS category_total

    FROM product_sales
)
SELECT
    product,
    category,
    sales,
    product_rank,
    100.0 * sales / NULLIF(category_total, 0)
        AS category_percentage
FROM product_analysis
WHERE product_rank <= 3;
```

🔥 এই query-তে:

```text
CTE
+
RANK
+
PARTITION BY
+
SUM OVER
+
Percentage
+
Filter
```

সব একসাথে আছে।

---

# 2️⃣3️⃣ Window Frame Cheat Sheet

### শুরু থেকে বর্তমান পর্যন্ত

```sql
ROWS BETWEEN UNBOUNDED PRECEDING
AND CURRENT ROW
```

➡️ Running Total

---

### আগের 2 + Current

```sql
ROWS BETWEEN 2 PRECEDING
AND CURRENT ROW
```

➡️ 3-row moving average/sum

---

### Current + পরের 2

```sql
ROWS BETWEEN CURRENT ROW
AND 2 FOLLOWING
```

➡️ Forward-looking window

---

### পুরো window

```sql
ROWS BETWEEN UNBOUNDED PRECEDING
AND UNBOUNDED FOLLOWING
```

➡️ পুরো partition/window

---

# 2️⃣4️⃣ `ROWS` বনাম `RANGE` — Important Preview

দুটো দেখতে similar হলেও সবসময় একই নয়।

```sql
ROWS BETWEEN ...
```

সাধারণত physical rows-এর ভিত্তিতে frame তৈরি করে।

`RANGE` ordering value-এর peer/value range-এর ভিত্তিতে কাজ করতে পারে এবং duplicate ordering values থাকলে behavior আলাদা হতে পারে।

Beginner হিসেবে এখন:

> **Moving average / exact previous N rows → `ROWS` মনে রাখো।**

`RANGE` পরে advanced practice-এ আরও গভীরভাবে দেখব।

---

# 2️⃣5️⃣ GROUP BY বনাম Window — Final Understanding

### GROUP BY

```sql
SELECT
    department,
    AVG(salary)
FROM employees
GROUP BY department;
```

Output:

```text
IT → 52500
HR → 62500
```

Rows collapse হয়েছে।

---

### Window

```sql
SELECT
    name,
    department,
    salary,
    AVG(salary) OVER (
        PARTITION BY department
    )
FROM employees;
```

Output:

```text
Rahim → IT → 45000 → 52500
Hasan → IT → 60000 → 52500
Karim → HR → 55000 → 62500
Jamil → HR → 70000 → 62500
```

Rows আছে।

### 🔥 Golden Rule

> **GROUP BY = rows কমায়।**

> **Window Function = rows রেখে calculation যোগ করে।**

---

# 🎯 Class 40 Assignment

নিজে solve করার চেষ্টা করো।

### Q1

প্রতিটি employee-এর সাথে company-এর first salary দেখাও।

### Q2

প্রতিটি employee-এর সাথে company-এর last salary দেখাও।

### Q3

প্রতিটি employee-এর সাথে second-highest salary/value related analysis করো `NTH_VALUE()` দিয়ে।

### Q4

Monthly sales-এর running total বের করো।

### Q5

Monthly sales-এর 3-month moving average বের করো।

### Q6

Monthly sales-এর 3-month rolling sum বের করো।

### Q7

প্রতিটি product-এর total sales-এর percentage বের করো।

### Q8

প্রতিটি department-এর মধ্যে employee salary-এর percentage বের করো।

### Q9

Previous month's sales এবং current month's sales difference বের করো।

### Q10

Monthly sales growth percentage বের করো।

### Q11 ⭐

প্রতিটি city-এর 3-month moving average বের করো।

### Q12 ⭐

প্রতিটি department-এর Top 3 employees এবং department-এর total salary-এর মধ্যে তাদের percentage বের করো।

### Q13 🔥

CTE + `LAG()` ব্যবহার করে monthly sales growth report বানাও:

```text
Month
Current Sales
Previous Sales
Difference
Growth %
```

### Q14 🔥

CTE + `RANK()` + `SUM() OVER()` ব্যবহার করে:

```text
Category
Product
Sales
Rank
Category Total
Category %
```

এবং শুধু Top 3 products দেখাও।

---

# 🧪 Class 40 Quiz

**1. `FIRST_VALUE()` কী দেয়?**

A. প্রথম row-এর value  
B. শেষ row-এর value  
C. Average  
D. Rank

**2. `LAST_VALUE()` সঠিকভাবে পুরো window-এর শেষ value পেতে কোন concept গুরুত্বপূর্ণ?**

A. `WHERE`  
B. Window Frame  
C. `GROUP BY`  
D. `DISTINCT`

**3. `ROWS BETWEEN 2 PRECEDING AND CURRENT ROW` কতগুলো row পর্যন্ত include করতে পারে?**

A. সর্বোচ্চ 2  
B. বর্তমানসহ সর্বোচ্চ 3  
C. 4  
D. সব

**4. Running Total-এর জন্য কোনটি useful?**

A. `SUM() OVER()`  
B. `AVG() ONLY`  
C. `RANK()`  
D. `LEAD()`

**5. Previous row-এর value?**

A. LEAD  
B. LAG  
C. LAST_VALUE  
D. NTH_VALUE

**6. Next row-এর value?**

A. LAG  
B. LEAD  
C. FIRST_VALUE  
D. RANK

**7. 3-month moving average-এর জন্য কোন frame useful?**

A. `ROWS BETWEEN 2 PRECEDING AND CURRENT ROW`  
B. `ROWS BETWEEN 10 FOLLOWING`  
C. `GROUP BY month`  
D. `LIMIT 3`

**8. Percentage of total বের করতে কোন pattern useful?**

```text
A. value / SUM(value) OVER()
B. value / GROUP BY
C. value / ORDER BY
D. value / LIMIT
```

**9. `PARTITION BY city` করলে কী হবে?**

A. City অনুযায়ী logical window তৈরি হবে  
B. Table delete হবে  
C. City column remove হবে  
D. সব data sort হবে

**10. Window Function-এর সবচেয়ে বড় সুবিধা কী?**

A. Original rows রেখে analytical calculation করা যায়  
B. সব rows delete করা যায়  
C. Table automatically normalize হয়  
D. Database তৈরি হয়

---

# ⭐ Class 40 Cheat Sheet

### First Value

```sql
FIRST_VALUE(sales) OVER (
    ORDER BY month
)
```

### Last Value

```sql
LAST_VALUE(sales) OVER (
    ORDER BY month
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND UNBOUNDED FOLLOWING
)
```

### N-th Value

```sql
NTH_VALUE(sales, 2) OVER (
    ORDER BY month
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND UNBOUNDED FOLLOWING
)
```

### Running Total

```sql
SUM(sales) OVER (
    ORDER BY month
    ROWS BETWEEN UNBOUNDED PRECEDING
    AND CURRENT ROW
)
```

### Moving Average

```sql
AVG(sales) OVER (
    ORDER BY month
    ROWS BETWEEN 2 PRECEDING
    AND CURRENT ROW
)
```

### Percentage of Total

```sql
100.0 * sales / SUM(sales) OVER ()
```

### Previous Value

```sql
LAG(sales) OVER (
    ORDER BY month
)
```

### Next Value

```sql
LEAD(sales) OVER (
    ORDER BY month
)
```

---

# 🧠 Class 31 → 40 পর্যন্ত তোমার SQL Journey

```text
31 → SELECT / WHERE / ORDER BY
32 → CREATE TABLE / Constraints
33 → INSERT / UPDATE / DELETE
34 → GROUP BY / HAVING
35 → JOIN
36 → Advanced JOIN
37 → Subquery
38 → CTE
39 → Window Functions
40 → Advanced Window Functions
```

এখন তুমি SQL-এর **intermediate → advanced analytics** অংশে ঢুকে গেছো।

**পরের Class 41**-এ আমরা Window Functions-এর উপর একটি **full SQL Analytics Project** করব—Sales dataset নিয়ে `CTE + JOIN + GROUP BY + RANK + LAG + Running Total + Moving Average + Growth %` একসাথে ব্যবহার করে একটি বাস্তব Data Analyst-এর মতো analysis তৈরি করব।

----
# 📘 SQL — Class 41

## 🏆 Full SQL Analytics Project — Sales Analysis

আজ আমরা শুধু নতুন একটা function শিখব না। বরং **Class 31–40 পর্যন্ত শেখা SQL একসাথে ব্যবহার করে একটি real-world Sales Analytics Project** বানাব।

আজকের project-এ আমরা ব্যবহার করব:

```text
SELECT
WHERE
JOIN
GROUP BY
HAVING
CTE
CASE
RANK()
LAG()
SUM() OVER()
AVG() OVER()
PARTITION BY
ROWS BETWEEN
```

---

# 🎯 Project Goal

ধরি, একটি কোম্পানির 3টি table আছে:

```text
customers
products
orders
```

আমরা বের করব:

1. Total sales
    
2. Customer-wise sales
    
3. Product-wise sales
    
4. Category-wise sales
    
5. Top products
    
6. Top customers
    
7. Monthly sales
    
8. Previous month sales
    
9. Monthly growth %
    
10. Running total
    
11. 3-month moving average
    
12. Category-wise product ranking
    
13. Top 3 products per category
    
14. Customer ranking
    
15. Final business insights
    

---

# 1️⃣ Database Structure

## Customers

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    city VARCHAR(50)
);
```

Data:

```sql
INSERT INTO customers VALUES
(1, 'Rahim', 'Dhaka'),
(2, 'Karim', 'Chittagong'),
(3, 'Hasan', 'Dhaka'),
(4, 'Jamil', 'Khulna'),
(5, 'Nayeem', 'Dhaka');
```

---

# 2️⃣ Products Table

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2)
);
```

Data:

```sql
INSERT INTO products VALUES
(101, 'Laptop', 'Electronics', 80000),
(102, 'Monitor', 'Electronics', 30000),
(103, 'Keyboard', 'Accessories', 3000),
(104, 'Mouse', 'Accessories', 1500),
(105, 'Chair', 'Furniture', 10000),
(106, 'Desk', 'Furniture', 20000);
```

---

# 3️⃣ Orders Table

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    order_date DATE,
    quantity INT,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id),

    FOREIGN KEY (product_id)
        REFERENCES products(product_id)
);
```

Data:

```sql
INSERT INTO orders VALUES
(1, 1, 101, '2026-01-05', 1),
(2, 2, 102, '2026-01-10', 2),
(3, 3, 103, '2026-01-15', 5),
(4, 1, 104, '2026-02-05', 4),
(5, 4, 105, '2026-02-12', 2),
(6, 5, 101, '2026-02-20', 1),
(7, 2, 106, '2026-03-03', 2),
(8, 3, 102, '2026-03-10', 1),
(9, 1, 103, '2026-03-15', 10),
(10, 5, 104, '2026-04-05', 5),
(11, 4, 106, '2026-04-12', 1),
(12, 2, 101, '2026-04-20', 1);
```

---

# 4️⃣ প্রথম কাজ — Full Sales Dataset

প্রথমে আমাদের তিনটা table JOIN করতে হবে।

```sql
SELECT
    o.order_id,
    o.order_date,
    c.customer_name,
    c.city,
    p.product_name,
    p.category,
    o.quantity,
    p.price,
    o.quantity * p.price AS total_amount
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id
JOIN products p
    ON o.product_id = p.product_id;
```

এখন আমাদের কাছে একটি analytical dataset তৈরি হলো।

### গুরুত্বপূর্ণ:

```text
orders
   ↓
JOIN customers
   ↓
JOIN products
   ↓
Sales Analysis Dataset
```

---

# 5️⃣ Total Sales

```sql
SELECT
    SUM(o.quantity * p.price) AS total_sales
FROM orders o
JOIN products p
    ON o.product_id = p.product_id;
```

এখানে:

```text
quantity × price
```

= Order Revenue

---

# 6️⃣ Customer-wise Sales

Question:

> কোন customer কত টাকা spend করেছে?

```sql
SELECT
    c.customer_id,
    c.customer_name,
    SUM(o.quantity * p.price) AS total_sales
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    c.customer_id,
    c.customer_name
ORDER BY total_sales DESC;
```

এখানে Class 34-এর:

```text
GROUP BY
SUM()
ORDER BY
```

একসাথে ব্যবহার হয়েছে।

---

# 7️⃣ Customer Ranking 🔥

এখন প্রত্যেক customer-এর ranking চাই।

```sql
WITH customer_sales AS (
    SELECT
        c.customer_id,
        c.customer_name,
        SUM(o.quantity * p.price) AS total_sales
    FROM orders o
    JOIN customers c
        ON o.customer_id = c.customer_id
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        c.customer_id,
        c.customer_name
)

SELECT
    customer_name,
    total_sales,

    RANK() OVER (
        ORDER BY total_sales DESC
    ) AS customer_rank

FROM customer_sales;
```

এখানে structure:

```text
JOIN
 ↓
GROUP BY
 ↓
CTE
 ↓
RANK()
```

---

# 8️⃣ Top 3 Customers

আগের query-কে CTE দিয়ে wrap করতে পারি:

```sql
WITH customer_sales AS (
    SELECT
        c.customer_id,
        c.customer_name,
        SUM(o.quantity * p.price) AS total_sales
    FROM orders o
    JOIN customers c
        ON o.customer_id = c.customer_id
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        c.customer_id,
        c.customer_name
),

ranked_customers AS (
    SELECT
        customer_name,
        total_sales,
        RANK() OVER (
            ORDER BY total_sales DESC
        ) AS customer_rank
    FROM customer_sales
)

SELECT *
FROM ranked_customers
WHERE customer_rank <= 3;
```

🔥 এটা একটি very common Data Analyst pattern:

```text
Raw Data
   ↓
Aggregation
   ↓
CTE
   ↓
Ranking
   ↓
Filter
```

---

# 9️⃣ Product-wise Sales

```sql
SELECT
    p.product_name,
    p.category,
    SUM(o.quantity * p.price) AS total_sales
FROM orders o
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    p.product_name,
    p.category
ORDER BY total_sales DESC;
```

---

# 🔟 Category-wise Sales

```sql
SELECT
    p.category,
    SUM(o.quantity * p.price) AS category_sales
FROM orders o
JOIN products p
    ON o.product_id = p.product_id
GROUP BY p.category
ORDER BY category_sales DESC;
```

---

# 1️⃣1️⃣ Category-এর ভিতরে Product Ranking 🔥

Question:

> প্রতিটি category-এর মধ্যে কোন product #1?

```sql
WITH product_sales AS (
    SELECT
        p.product_id,
        p.product_name,
        p.category,
        SUM(o.quantity * p.price) AS total_sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        p.product_id,
        p.product_name,
        p.category
)

SELECT
    product_name,
    category,
    total_sales,

    RANK() OVER (
        PARTITION BY category
        ORDER BY total_sales DESC
    ) AS category_rank

FROM product_sales;
```

এখানে সবচেয়ে গুরুত্বপূর্ণ:

```sql
PARTITION BY category
```

মানে:

```text
Electronics
   → ranking আলাদা

Accessories
   → ranking আলাদা

Furniture
   → ranking আলাদা
```

---

# 1️⃣2️⃣ Top 1 Product per Category

```sql
WITH product_sales AS (
    SELECT
        p.product_name,
        p.category,
        SUM(o.quantity * p.price) AS total_sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        p.product_name,
        p.category
),

ranked_products AS (
    SELECT
        product_name,
        category,
        total_sales,

        RANK() OVER (
            PARTITION BY category
            ORDER BY total_sales DESC
        ) AS category_rank

    FROM product_sales
)

SELECT *
FROM ranked_products
WHERE category_rank = 1;
```

---

# 1️⃣3️⃣ Monthly Sales

এবার date থেকে month বের করব।

MySQL:

```sql
SELECT
    DATE_FORMAT(o.order_date, '%Y-%m') AS month,
    SUM(o.quantity * p.price) AS monthly_sales
FROM orders o
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    DATE_FORMAT(o.order_date, '%Y-%m')
ORDER BY month;
```

Result conceptually:

```text
2026-01 → ...
2026-02 → ...
2026-03 → ...
2026-04 → ...
```

---

# 1️⃣4️⃣ Monthly Sales + Previous Month

এখন Class 39-এর `LAG()` ব্যবহার করব।

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(o.order_date, '%Y-%m') AS month,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        DATE_FORMAT(o.order_date, '%Y-%m')
)

SELECT
    month,
    sales,

    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_month_sales

FROM monthly_sales;
```

---

# 1️⃣5️⃣ Monthly Growth %

এখন:

```text
Current Sales
Previous Sales
Difference
Growth %
```

সব বের করব।

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(o.order_date, '%Y-%m') AS month,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        DATE_FORMAT(o.order_date, '%Y-%m')
),

sales_comparison AS (
    SELECT
        month,
        sales,

        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales

    FROM monthly_sales
)

SELECT
    month,
    sales,
    previous_sales,

    sales - previous_sales AS difference,

    ROUND(
        100.0 * (sales - previous_sales)
        / NULLIF(previous_sales, 0),
        2
    ) AS growth_percentage

FROM sales_comparison;
```

🔥 এই query একটি real business report-এর মতো।

---

# 1️⃣6️⃣ Running Total

এখন cumulative sales:

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(o.order_date, '%Y-%m') AS month,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        DATE_FORMAT(o.order_date, '%Y-%m')
)

SELECT
    month,
    sales,

    SUM(sales) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_total

FROM monthly_sales;
```

Concept:

```text
Jan       100
Feb       200
Mar       300

Running:
Jan       100
Feb       300
Mar       600
```

---

# 1️⃣7️⃣ 3-Month Moving Average

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(o.order_date, '%Y-%m') AS month,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        DATE_FORMAT(o.order_date, '%Y-%m')
)

SELECT
    month,
    sales,

    ROUND(
        AVG(sales) OVER (
            ORDER BY month
            ROWS BETWEEN 2 PRECEDING
            AND CURRENT ROW
        ),
        2
    ) AS moving_average_3

FROM monthly_sales;
```

---

# 1️⃣8️⃣ Cumulative Percentage

Question:

> বছরের total sales-এর কত % এখন পর্যন্ত অর্জিত হয়েছে?

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(o.order_date, '%Y-%m') AS month,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        DATE_FORMAT(o.order_date, '%Y-%m')
)

SELECT
    month,
    sales,

    SUM(sales) OVER (
        ORDER BY month
        ROWS BETWEEN UNBOUNDED PRECEDING
        AND CURRENT ROW
    ) AS running_total,

    ROUND(
        100.0 *
        SUM(sales) OVER (
            ORDER BY month
            ROWS BETWEEN UNBOUNDED PRECEDING
            AND CURRENT ROW
        )
        / SUM(sales) OVER (),
        2
    ) AS cumulative_percentage

FROM monthly_sales;
```

---

# 1️⃣9️⃣ Final Analytics Query 🔥🔥

এখন আমরা একটি বড় report বানাব:

```text
Month
Sales
Previous Sales
Growth %
Running Total
Moving Average
Cumulative %
```

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(o.order_date, '%Y-%m') AS month,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        DATE_FORMAT(o.order_date, '%Y-%m')
),

analysis AS (
    SELECT
        month,
        sales,

        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales,

        SUM(sales) OVER (
            ORDER BY month
            ROWS BETWEEN UNBOUNDED PRECEDING
            AND CURRENT ROW
        ) AS running_total,

        AVG(sales) OVER (
            ORDER BY month
            ROWS BETWEEN 2 PRECEDING
            AND CURRENT ROW
        ) AS moving_average

    FROM monthly_sales
)

SELECT
    month,
    sales,
    previous_sales,

    sales - previous_sales AS difference,

    ROUND(
        100.0 * (sales - previous_sales)
        / NULLIF(previous_sales, 0),
        2
    ) AS growth_percentage,

    running_total,

    ROUND(moving_average, 2)
        AS moving_average,

    ROUND(
        100.0 * running_total
        / SUM(sales) OVER (),
        2
    ) AS cumulative_percentage

FROM analysis
ORDER BY month;
```

🔥🔥 **এটাই Class 41-এর মূল query।**

---

# 🧠 Query-টা কীভাবে চিন্তা করবে?

একসাথে পুরো query মুখস্থ করবে না।

এভাবে চিন্তা করবে:

```text
Step 1
JOIN
↓
Sales data তৈরি

Step 2
GROUP BY
↓
Monthly Sales

Step 3
CTE
↓
Monthly result temporarily store

Step 4
LAG()
↓
Previous month

Step 5
SUM() OVER()
↓
Running Total

Step 6
AVG() OVER()
↓
Moving Average

Step 7
Calculation
↓
Growth %

Step 8
Final SELECT
↓
Business Report
```

---

# ⭐ Data Analyst-এর সবচেয়ে গুরুত্বপূর্ণ Pattern

এই pattern মনে রাখো:

```text
Raw Tables
     ↓
JOIN
     ↓
GROUP BY
     ↓
CTE
     ↓
Window Functions
     ↓
Business Calculation
     ↓
Final Report
```

এটা বাস্তব SQL analytics-এ খুব common workflow।

---

# 📝 Class 41 Assignment

এবার তোমার practice।

### Level 1

**Q1.** Customer-wise total sales বের করো।

**Q2.** Product-wise total sales বের করো।

**Q3.** Category-wise total sales বের করো।

**Q4.** Top 3 customers বের করো।

---

### Level 2

**Q5.** প্রতিটি category-এর মধ্যে product ranking বের করো।

**Q6.** প্রতিটি category-এর Top 2 products বের করো।

**Q7.** Monthly sales বের করো।

**Q8.** Monthly sales-এর previous month বের করো।

---

### Level 3

**Q9.** Monthly growth percentage বের করো।

**Q10.** Monthly running total বের করো।

**Q11.** 3-month moving average বের করো।

**Q12.** Cumulative percentage বের করো।

---

### 🔥 Challenge

একটি final query বানাও যার output হবে:

```text
month
sales
previous_sales
growth_percentage
running_total
moving_average_3
cumulative_percentage
```

**শর্ত:** কমপক্ষে **2টি CTE + 3টি Window Function** ব্যবহার করতে হবে।

---

# 🧪 Class 41 Quiz

**1. `LAG()` কী দেয়?**

A. Next row  
B. Previous row  
C. First row  
D. Average

**2. `PARTITION BY category` কেন ব্যবহার করি?**

A. Category delete করতে  
B. Category অনুযায়ী আলাদা window তৈরি করতে  
C. Category sort করতে  
D. Category filter করতে

**3. Running Total-এর জন্য কোনটি ব্যবহার করা হয়?**

A. `SUM() OVER()`  
B. `COUNT()`  
C. `RANK()`  
D. `LEAD()`

**4. 3-month moving average-এর frame কোনটি?**

A. `1 PRECEDING`  
B. `2 PRECEDING AND CURRENT ROW`  
C. `3 FOLLOWING`  
D. `UNBOUNDED FOLLOWING`

**5. `GROUP BY` করার পর ranking করতে কোন structure খুব useful?**

A. CTE + Window Function  
B. DELETE + JOIN  
C. INSERT + LIMIT  
D. UPDATE + WHERE

**6. Customer-এর মোট sales ranking করতে কোনটি ব্যবহার করা যায়?**

A. `RANK()`  
B. `LAG()`  
C. `LEAD()`  
D. `FIRST_VALUE()`

**7. `NULLIF(previous_sales, 0)` কেন ব্যবহার করা হয়?**

A. Sorting-এর জন্য  
B. Duplicate remove করতে  
C. Division by zero এড়াতে  
D. Ranking করতে

**8. Cumulative percentage কী বোঝায়?**

A. শুধু current row-এর percentage  
B. এখন পর্যন্ত accumulated total-এর percentage  
C. Maximum percentage  
D. Average percentage

**9. Category-এর ভিতরে product ranking-এর জন্য কোনটি সঠিক?**

```sql
RANK() OVER (
    PARTITION BY ______
    ORDER BY sales DESC
)
```

A. product  
B. category  
C. sales  
D. customer

**10. আজকের project-এ সবচেয়ে গুরুত্বপূর্ণ workflow কোনটি?**

A. `DELETE → UPDATE → INSERT`  
B. `JOIN → GROUP BY → CTE → Window Function → Analysis`  
C. `LIMIT → DISTINCT → DELETE`  
D. `ORDER BY → DROP → CREATE`


----

হ্যাঁ, **আরও Class দরকার**—তবে এখন থেকে শুধু নতুন SQL syntax শেখানোর চেয়ে **real-world SQL + Database Design + Performance**-এর দিকে যাওয়া বেশি useful হবে।

তুমি যেহেতু **Database Designer / Data Analyst → Data Engineer** দিকে যেতে চাচ্ছো, আমি এইভাবে এগোতে বলব:

|Class|Topic|গুরুত্ব|
|---|---|---|
|**42**|`CASE WHEN` + Advanced SQL Business Logic|⭐⭐⭐⭐⭐|
|**43**|`EXISTS`, `NOT EXISTS`, `IN`, `NOT IN`|⭐⭐⭐⭐⭐|
|**44**|Set Operations: `UNION`, `UNION ALL`, `INTERSECT`, `EXCEPT`|⭐⭐⭐⭐|
|**45**|Date & Time Analytics|⭐⭐⭐⭐⭐|
|**46**|Advanced String & NULL Handling|⭐⭐⭐⭐|
|**47**|SQL Views|⭐⭐⭐⭐⭐|
|**48**|Stored Procedures & Functions|⭐⭐⭐⭐|
|**49**|Triggers|⭐⭐⭐⭐|
|**50**|Transactions + ACID + `COMMIT`/`ROLLBACK`|⭐⭐⭐⭐⭐|
|**51**|Indexing|⭐⭐⭐⭐⭐|
|**52**|Query Optimization + `EXPLAIN`|⭐⭐⭐⭐⭐|
|**53**|Database Normalization|⭐⭐⭐⭐⭐|
|**54**|Database Design + ERD|⭐⭐⭐⭐⭐|
|**55**|Fact & Dimension / Star Schema|⭐⭐⭐⭐⭐|
|**56**|SQL Interview Problems|⭐⭐⭐⭐⭐|
|**57**|Full SQL Data Analyst Project|⭐⭐⭐⭐⭐|
|**58**|Full Database Designer Project|⭐⭐⭐⭐⭐|

### এরপর কী?

**Class 58-এর পর SQL-এর core অংশ মোটামুটি strong হয়ে যাবে।**

তারপর তোমার roadmap হবে:

```text
Excel ✅
   ↓
SQL ← এখন এখানে
   ↓
PostgreSQL
   ↓
Database Design
   ↓
Python
   ↓
Pandas
   ↓
Statistics
   ↓
Power BI
   ↓
ETL
   ↓
Airflow
   ↓
Docker
   ↓
Data Engineering
```

### আমার recommendation

এখন **Class 42 থেকে চালিয়ে যাও**। বিশেষ করে `EXISTS → Transactions → Indexing → EXPLAIN → Normalization → Database Design` অংশগুলো তোমার জন্য খুব গুরুত্বপূর্ণ।

**Class 42 হবে: `EXISTS, NOT EXISTS & Advanced Filtering`** — কারণ এগুলো real-world SQL এবং interview দুটোতেই কাজে লাগে।


----

অবশ্যই। এবার **Class 42**-কে আরও structuredভাবে করি—বিশেষ করে `EXISTS`, `NOT EXISTS`, `IN`, `NOT IN`, এবং advanced filtering-এর পার্থক্যগুলো যেন পরিষ্কার হয়ে যায়।

# 📘 SQL Class 42

## `EXISTS`, `NOT EXISTS` & Advanced Filtering

### আজকের লক্ষ্য

Class শেষে তুমি পারবে:

- `EXISTS` ব্যবহার করতে
    
- `NOT EXISTS` ব্যবহার করতে
    
- `EXISTS` বনাম `IN` বুঝতে
    
- `NOT EXISTS` বনাম `NOT IN` বুঝতে
    
- correlated subquery বুঝতে
    
- `EXISTS + JOIN`
    
- `EXISTS + GROUP BY + HAVING`
    
- real-world filtering query লিখতে
    

---

# 1. আগে একটা Dataset

ধরি আমাদের ৩টি table:

### `customers`

|customer_id|name|city|
|--:|---|---|
|1|Rahim|Dhaka|
|2|Karim|Chittagong|
|3|Hasan|Dhaka|
|4|Jamil|Khulna|
|5|Nayeem|Dhaka|

### `orders`

|order_id|customer_id|amount|
|--:|--:|--:|
|101|1|50000|
|102|1|30000|
|103|3|70000|
|104|5|20000|

তাহলে:

```text
Rahim  → 2 orders
Karim  → 0 orders
Hasan  → 1 order
Jamil  → 0 orders
Nayeem → 1 order
```

---

# 2. `EXISTS` কী?

সহজ ভাষায়:

> **কোনো matching row আছে কি না সেটা check করে।**

Syntax:

```sql
WHERE EXISTS (
    SELECT 1
    FROM table_name
    WHERE condition
)
```

---

# 3. Customers যাদের Order আছে

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

Result:

|customer_id|name|
|--:|---|
|1|Rahim|
|3|Hasan|
|5|Nayeem|

কারণ এদের প্রত্যেকের অন্তত একটি order আছে।

---

# 4. `SELECT 1` কেন?

এখানে:

```sql
SELECT 1
```

এর অর্থ এই নয় যে আমরা `1` data চাইছি।

`EXISTS` শুধু জানতে চায়:

> matching row পাওয়া গেছে কি?

তাই:

```sql
SELECT 1
```

একটি common convention।

---

# 5. `EXISTS` কীভাবে চিন্তা করবে?

এই query:

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

Rahim-এর জন্য:

```text
Rahim customer_id = 1
        ↓
orders-এ customer_id = 1 আছে?
        ↓
YES
        ↓
Rahim রাখো
```

Karim:

```text
Karim customer_id = 2
        ↓
orders-এ customer_id = 2 আছে?
        ↓
NO
        ↓
Karim বাদ
```

---

# 6. `NOT EXISTS`

এবার opposite।

> **Matching row নেই কি?**

```sql
SELECT *
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

Result:

```text
Karim
Jamil
```

### মনে রাখো:

```text
EXISTS
→ আছে?

NOT EXISTS
→ নেই?
```

---

# 7. `EXISTS` হলো Correlated Subquery

এই অংশটি লক্ষ্য করো:

```sql
o.customer_id = c.customer_id
```

ভেতরের query বাইরের query-এর `c.customer_id` ব্যবহার করছে।

এজন্য এটি:

> **Correlated Subquery**

```text
Outer Query
customers c
     ↓
c.customer_id
     ↓
Inner Query
orders o
```

---

# 8. `IN` বনাম `EXISTS`

একই problem:

> যেসব customer order করেছে তাদের বের করো।

### `IN`

```sql
SELECT *
FROM customers
WHERE customer_id IN (
    SELECT customer_id
    FROM orders
);
```

### `EXISTS`

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

দুটোই এখানে একই ধরনের result দিতে পারে।

---

# 9. কখন `IN` ব্যবহার করব?

যদি তোমার চিন্তা হয়:

> "এই value কি এই list-এর মধ্যে আছে?"

তাহলে:

```sql
IN
```

Example:

```sql
SELECT *
FROM customers
WHERE city IN ('Dhaka', 'Khulna');
```

অর্থাৎ:

```text
city কি Dhaka বা Khulna?
```

---

# 10. কখন `EXISTS` ব্যবহার করব?

যদি প্রশ্ন হয়:

> "এই row-এর সাথে matching record আছে?"

তাহলে `EXISTS` খুব natural।

Example:

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

---

# 11. `NOT IN` বনাম `NOT EXISTS` ⚠️

এটা খুব গুরুত্বপূর্ণ।

তাত্ত্বিকভাবে:

```sql
WHERE customer_id NOT IN (...)
```

দিয়ে missing customers বের করা যায়।

কিন্তু subquery-তে `NULL` থাকলে `NOT IN` unexpected result দিতে পারে।

তাই related record **নেই** check করার সময়:

```sql
NOT EXISTS
```

অনেক safer pattern।

### Practical rule:

```text
IN
→ list membership

EXISTS
→ existence

NOT EXISTS
→ absence
```

---

# 12. Product যেগুলো কখনো বিক্রি হয়নি

ধরি:

```text
products.product_id
orders.product_id
```

Query:

```sql
SELECT *
FROM products p
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.product_id = p.product_id
);
```

এখানে আমরা খুঁজছি:

> Product-এর matching order নেই।

---

# 13. Product যেগুলো বিক্রি হয়েছে

```sql
SELECT *
FROM products p
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.product_id = p.product_id
);
```

---

# 14. Advanced Filtering: Amount

Question:

> যেসব customer অন্তত একটি `50000`-এর বেশি order করেছে।

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
      AND o.amount > 50000
);
```

এখানে:

```text
customer match
+
amount > 50000
```

দুটো condition আছে।

---

# 15. Customer যারা 2026-এর March-এর পরে Order করেছে

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
      AND o.order_date >= '2026-03-01'
);
```

এটা real-world filtering-এর খুব common pattern।

---

# 16. `EXISTS + JOIN`

ধরি:

### `products`

|product_id|product_name|category|
|--:|---|---|
|101|Laptop|Electronics|
|102|Monitor|Electronics|
|103|Chair|Furniture|

Question:

> যেসব customer Electronics product কিনেছে।

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
      AND p.category = 'Electronics'
);
```

এখানে:

```text
customers
    ↓
EXISTS
    ↓
orders
    ↓
JOIN
    ↓
products
    ↓
category = Electronics
```

---

# 17. Laptop কিনেছে এমন Customer

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
      AND p.product_name = 'Laptop'
);
```

---

# 18. Electronics কখনো কেনেনি

```sql
SELECT *
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
      AND p.category = 'Electronics'
);
```

এখানে খুব সুন্দর একটা pattern:

```text
NOT EXISTS
+
JOIN
+
condition
```

---

# 19. Electronics এবং Furniture দুটোই কিনেছে

এখানে দুইটি `EXISTS` ব্যবহার করা যায়।

```sql
SELECT *
FROM customers c

WHERE EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
      AND p.category = 'Electronics'
)

AND EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
      AND p.category = 'Furniture'
);
```

Logic:

```text
Electronics?
   ↓ YES

Furniture?
   ↓ YES

Customer selected
```

---

# 20. `EXISTS + GROUP BY + HAVING`

এবার একটু advanced।

Question:

> যেসব customer কমপক্ষে 3টি order করেছে।

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
    GROUP BY o.customer_id
    HAVING COUNT(*) >= 3
);
```

এখানে:

```text
EXISTS
   +
GROUP BY
   +
HAVING
```

একসাথে ব্যবহার হচ্ছে।

---

# 21. Total Order Amount > 100000

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
    GROUP BY o.customer_id
    HAVING SUM(o.amount) > 100000
);
```

অর্থাৎ:

> Customer-এর সব order-এর total > 100000 কি না।

---

# 22. `EXISTS` + CTE

CTE-এর সাথেও ব্যবহার করা যায়।

```sql
WITH recent_orders AS (
    SELECT *
    FROM orders
    WHERE order_date >= '2026-03-01'
)

SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM recent_orders r
    WHERE r.customer_id = c.customer_id
);
```

Workflow:

```text
orders
   ↓
filter
   ↓
CTE
   ↓
EXISTS
   ↓
customers
```

---

# 23. JOIN বনাম EXISTS

একই প্রশ্ন:

> যেসব customer-এর order আছে।

### JOIN:

```sql
SELECT DISTINCT
    c.customer_id,
    c.name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

### EXISTS:

```sql
SELECT
    c.customer_id,
    c.name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

### Main difference

**JOIN:**

> Matching rows combine করে।

**EXISTS:**

> Matching row আছে কি না check করে।

---

# 24. JOIN-এ `DISTINCT` কেন?

Rahim-এর যদি 3টা order থাকে:

```text
Rahim
Rahim
Rahim
```

JOIN result-এ 3 rows আসতে পারে।

তাই:

```sql
DISTINCT
```

দিতে হতে পারে।

কিন্তু `EXISTS` শুধু existence check করে, তাই customer-এর row duplicate করে না।

---

# 25. Advanced Filtering-এর বড় Picture

SQL-এ filtering-এর জন্য এখন তোমার কাছে অনেক tools আছে:

```text
WHERE
 ├── =
 ├── >
 ├── <
 ├── >=
 ├── <=
 ├── <>
 ├── AND
 ├── OR
 ├── IN
 ├── NOT IN
 ├── BETWEEN
 ├── LIKE
 ├── IS NULL
 ├── IS NOT NULL
 ├── EXISTS
 └── NOT EXISTS
```

আর grouped data-এর জন্য:

```text
HAVING
```

---

# 🧠 সবচেয়ে গুরুত্বপূর্ণ পার্থক্য

|Problem|Use|
|---|---|
|Value list-এর মধ্যে আছে?|`IN`|
|Value list-এর মধ্যে নেই?|`NOT IN`|
|Related row আছে?|`EXISTS`|
|Related row নেই?|`NOT EXISTS`|
|Pattern match|`LIKE`|
|Range|`BETWEEN`|
|NULL|`IS NULL`|
|Group filter|`HAVING`|

---

# 🔥 Real-world Example

একজন Data Analyst-কে বলা হলো:

> "Find customers who have placed at least one order, have bought Electronics, but have never bought Furniture."

SQL:

```sql
SELECT *
FROM customers c

WHERE EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
)

AND EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
      AND p.category = 'Electronics'
)

AND NOT EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
      AND p.category = 'Furniture'
);
```

এখানে আমরা ব্যবহার করেছি:

```text
EXISTS
+
EXISTS
+
NOT EXISTS
+
JOIN
+
AND
```

এটাই **advanced filtering**।

---

# ⭐ Golden Rules

### Rule 1

```sql
EXISTS
```

মানে:

> **"আছে?"**

### Rule 2

```sql
NOT EXISTS
```

মানে:

> **"নেই?"**

### Rule 3

```sql
IN
```

মানে:

> **"এই list-এর মধ্যে আছে?"**

### Rule 4

Missing related records খুঁজতে:

```sql
NOT EXISTS
```

খুব useful।

### Rule 5

`NOT IN` + `NULL` থেকে সাবধান।

### Rule 6

`EXISTS` সাধারণত **data return করার জন্য নয়; existence check করার জন্য।**

---

# 📝 Class 42 Assignment

### Q1

যেসব customer অন্তত একটি order করেছে।

### Q2

যেসব customer কোনো order করেনি।

### Q3

যেসব product কখনো sell হয়নি।

### Q4

যেসব product অন্তত একবার sell হয়েছে।

### Q5

যেসব customer Electronics কিনেছে।

### Q6

যেসব customer Electronics কখনো কেনেনি।

### Q7

যেসব customer Laptop কিনেছে।

### Q8

যেসব customer `2026-03-01`-এর পরে order করেছে।

### Q9

যেসব customer অন্তত 3টি order করেছে।

### Q10

যেসব customer-এর total order amount `100000`-এর বেশি।

### 🔥 Q11

যেসব customer **Electronics এবং Furniture দুটোই** কিনেছে।

### 🔥 Q12

যেসব customer **order করেছে কিন্তু Electronics কখনো কেনেনি**।

---

# 🧪 Quiz

**1. `EXISTS` কী check করে?**

A. Sorting  
B. Matching row exists কি না  
C. Duplicate  
D. NULL

**2. `NOT EXISTS` কী check করে?**

A. Matching row আছে  
B. Matching row নেই  
C. Sorting  
D. Ranking

**3. `EXISTS`-এর ভিতরে common pattern কোনটি?**

A. `SELECT 1`  
B. `DELETE 1`  
C. `UPDATE 1`  
D. `DROP 1`

**4. Customer-এর কোনো order নেই—কোনটি সবচেয়ে natural?**

A. `EXISTS`  
B. `NOT EXISTS`  
C. `RANK()`  
D. `LEAD()`

**5. `NOT IN`-এর ক্ষেত্রে কোনটি বিশেষভাবে problematic হতে পারে?**

A. JOIN  
B. NULL  
C. ORDER BY  
D. LIMIT

**6. `EXISTS + GROUP BY`-এর aggregate condition কোথায় দেওয়া যায়?**

A. HAVING  
B. ORDER BY  
C. DISTINCT  
D. LIMIT

**7. Customer-এর অন্তত একটি order আছে কিনা check করতে সবচেয়ে direct approach কোনটি?**

A. `EXISTS`  
B. `RANK()`  
C. `AVG()`  
D. `CASE`

**8. JOIN-এর ফলে duplicate customer rows এলে unique করার জন্য কী ব্যবহার করা যায়?**

A. `DISTINCT`  
B. `HAVING`  
C. `LAG()`  
D. `BETWEEN`

**9. Missing related records-এর জন্য কোনটি সবচেয়ে useful?**

A. `NOT EXISTS`  
B. `ORDER BY`  
C. `LIMIT`  
D. `RANK()`

**10. `EXISTS` কি subquery-এর actual returned value-এর ওপর মূলত নির্ভর করে?**

A. Yes  
B. No — matching row আছে কি না সেটাই মূল বিষয়

---

## 🎯 আজকের ৩টি Query অবশ্যই বুঝবে

### Has orders

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

### Has no orders

```sql
SELECT *
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

### Bought Electronics

```sql
SELECT *
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    WHERE o.customer_id = c.customer_id
      AND p.category = 'Electronics'
);
```

### 🧠 One-line memory trick

> **`IN` = list-এর মধ্যে? | `EXISTS` = matching record আছে? | `NOT EXISTS` = matching record নেই?**


----

# 📘 Class 43 — SQL Set Operations

আজকে আমরা শিখব **Set Operations**:

- `UNION`
    
- `UNION ALL`
    
- `INTERSECT`
    
- `EXCEPT`
    
- Multiple Set Operations
    
- `ORDER BY` with Set Operations
    
- `JOIN vs UNION`
    
- Real-world Data Analytics examples
    
- Common mistakes
    
- Assignment + MCQ
    

---

# 1️⃣ Set Operation কী?

ধরো আমাদের দুইটা query আছে:

```sql
SELECT city FROM customers;
```

এবং

```sql
SELECT city FROM suppliers;
```

দুই query-এর result একসাথে combine করতে চাইলে **Set Operations** ব্যবহার করতে পারি।

সহজভাবে:

> **Set Operation = দুই বা তার বেশি SELECT query-এর result combine করা।**

---

# 2️⃣ UNION

`UNION` দুই query-এর result combine করে এবং **duplicate বাদ দেয়**।

### Example

Customers:

|name|city|
|---|---|
|Rahim|Dhaka|
|Karim|Chittagong|
|Hasan|Dhaka|

Suppliers:

|name|city|
|---|---|
|ABC|Dhaka|
|XYZ|Khulna|

Query:

```sql
SELECT city
FROM customers

UNION

SELECT city
FROM suppliers;
```

Result:

|city|
|---|
|Dhaka|
|Chittagong|
|Khulna|

`Dhaka` দুইবার থাকলেও একবার এসেছে।

### Golden Rule

> `UNION` = Combine + Remove Duplicate

---

# 3️⃣ UNION ALL

`UNION ALL` দুই result combine করে কিন্তু **duplicate রাখে**।

```sql
SELECT city
FROM customers

UNION ALL

SELECT city
FROM suppliers;
```

Result হতে পারে:

|city|
|---|
|Dhaka|
|Chittagong|
|Dhaka|
|Khulna|

এখানে Dhaka দুইবার এসেছে।

### Golden Rule

> `UNION ALL` = Combine + Keep Duplicate

---

# 4️⃣ UNION vs UNION ALL

|Feature|UNION|UNION ALL|
|---|---|---|
|Combine result|✅|✅|
|Duplicate remove|✅|❌|
|Duplicate রাখে|❌|✅|
|Usually faster|❌|✅|
|Use when|Unique result দরকার|সব records দরকার|

### Performance

যদি duplicate remove করার দরকার না থাকে:

```sql
UNION ALL
```

সাধারণত ভালো choice।

কারণ `UNION`-কে duplicate checking করতে হয়।

---

# 5️⃣ UNION-এর গুরুত্বপূর্ণ Rule

দুই query-তে **same number of columns** থাকতে হবে।

✅ Correct:

```sql
SELECT name, city
FROM customers

UNION

SELECT supplier_name, city
FROM suppliers;
```

দুই পাশে 2টি column।

---

❌ Incorrect:

```sql
SELECT name, city
FROM customers

UNION

SELECT supplier_name
FROM suppliers;
```

প্রথম query = 2 columns  
দ্বিতীয় query = 1 column

তাই error হবে।

---

# 6️⃣ Column Data Type Compatible হতে হবে

যেমন:

```sql
SELECT customer_id
FROM customers

UNION

SELECT supplier_id
FROM suppliers;
```

দুইটাই integer → ভালো।

কিন্তু:

```sql
SELECT customer_id
FROM customers

UNION

SELECT supplier_name
FROM suppliers;
```

একটি integer, অন্যটি text।

এটা সাধারণত logical/type সমস্যা তৈরি করবে।

---

# 7️⃣ Column Name কোথা থেকে আসে?

`UNION`-এর final column name সাধারণত **প্রথম SELECT** থেকে আসে।

Example:

```sql
SELECT city AS location
FROM customers

UNION

SELECT city
FROM suppliers;
```

Result column:

```text
location
```

দ্বিতীয় query-এর column name এখানে final name হবে না।

---

# 8️⃣ INTERSECT

`INTERSECT` দুই query-তে **common records** বের করে।

ধরো:

Customers:

```text
Dhaka
Chittagong
Khulna
```

Suppliers:

```text
Dhaka
Khulna
Rajshahi
```

Query:

```sql
SELECT city
FROM customers

INTERSECT

SELECT city
FROM suppliers;
```

Result:

```text
Dhaka
Khulna
```

কারণ দুই জায়গাতেই আছে।

### Golden Rule

> `INTERSECT` = Common records

---

# 9️⃣ Important: MySQL

এখানে একটি গুরুত্বপূর্ণ বিষয়।

**MySQL-এ traditional `INTERSECT` support version-dependent/modern versions-এ available**, কিন্তু অনেক পুরোনো MySQL environment-এ এটি ছিল না।

তুমি যেহেতু MySQL জানো, practical alternative হিসেবে `INNER JOIN` বা `EXISTS` ব্যবহার করতে পারো।

Example:

```sql
SELECT DISTINCT c.city
FROM customers c
JOIN suppliers s
ON c.city = s.city;
```

এটা common city বের করতে পারে।

---

# 🔟 EXCEPT

`EXCEPT` প্রথম query-তে আছে কিন্তু দ্বিতীয় query-তে নেই—এমন records দেয়।

Example:

Customers:

```text
Dhaka
Chittagong
Khulna
```

Suppliers:

```text
Dhaka
Khulna
Rajshahi
```

```sql
SELECT city
FROM customers

EXCEPT

SELECT city
FROM suppliers;
```

Result:

```text
Chittagong
```

কারণ:

```text
Customers → Dhaka, Chittagong, Khulna
Suppliers → Dhaka, Khulna

Difference → Chittagong
```

### Golden Rule

> `EXCEPT` = First result − Second result

---

# 1️⃣1️⃣ MySQL-এ EXCEPT-এর Alternative

যদি তোমার MySQL environment-এ `EXCEPT` না থাকে, তাহলে `NOT EXISTS` ব্যবহার করতে পারো।

```sql
SELECT DISTINCT c.city
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM suppliers s
    WHERE s.city = c.city
);
```

এটা customers-এর এমন city বের করবে যেগুলো suppliers-এর মধ্যে নেই।

এখানে Class 42-এর `NOT EXISTS` concept আবার কাজে লাগছে। 🔥

---

# 1️⃣2️⃣ UNION + ORDER BY

খুব গুরুত্বপূর্ণ।

```sql
SELECT city
FROM customers

UNION

SELECT city
FROM suppliers

ORDER BY city;
```

সাধারণত পুরো combined result-এর শেষে `ORDER BY` দেবে।

### ভুল approach

প্রতিটি SELECT-এর শেষে আলাদা `ORDER BY` দেওয়া unnecessary/সমস্যাজনক হতে পারে।

সাধারণ pattern:

```sql
SELECT ...
FROM ...

UNION

SELECT ...
FROM ...

ORDER BY ...;
```

---

# 1️⃣3️⃣ Real-World Example: Customer + Supplier Cities

ধরো company জানতে চায়:

> "আমাদের customer এবং supplier—দুই পক্ষের মোট কোন কোন city আছে?"

```sql
SELECT city
FROM customers

UNION

SELECT city
FROM suppliers

ORDER BY city;
```

এতে unique city list পাওয়া যাবে।

---

# 1️⃣4️⃣ UNION ALL — Real Business Example

ধরো আমাদের দুই বছরের sales table:

```text
sales_2025
sales_2026
```

দুই table-এর সব sales একসাথে আনতে চাই।

```sql
SELECT order_id, customer_id, amount
FROM sales_2025

UNION ALL

SELECT order_id, customer_id, amount
FROM sales_2026;
```

এখানে `UNION ALL` ব্যবহার করা ভালো।

কারণ আমরা **সব sales record রাখতে চাই**।

---

# 1️⃣5️⃣ UNION কেন এখানে ভুল হতে পারে?

ধরো:

```sql
sales_2025
```

এবং

```sql
sales_2026
```

দুই table-এ একই ধরনের order record থাকতে পারে।

যদি লিখো:

```sql
UNION
```

তাহলে exact duplicate rows remove হয়ে যেতে পারে।

কিন্তু sales analytics-এ প্রতিটি transaction গুরুত্বপূর্ণ হতে পারে।

তাই:

```sql
UNION ALL
```

সাধারণত better।

---

# 1️⃣6️⃣ JOIN vs UNION

এটা খুব গুরুত্বপূর্ণ interview question।

### JOIN

দুই table-এর **columns combine করে**।

Example:

```text
customers
+
orders
```

```sql
SELECT c.name, o.amount
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id;
```

Result:

|name|amount|
|---|--:|
|Rahim|50000|
|Karim|30000|

অর্থাৎ columns পাশাপাশি এসেছে।

---

### UNION

দুই query-এর **rows combine করে**।

```sql
SELECT name
FROM customers

UNION

SELECT supplier_name
FROM suppliers;
```

Result:

|name|
|---|
|Rahim|
|Karim|
|ABC|
|XYZ|

---

## 🧠 Golden Difference

> **JOIN = Columns পাশে পাশে combine করে**  
> **UNION = Rows উপর-নিচে combine করে**

Visual:

### JOIN

```text
Customer       Orders
--------       ------
Rahim    +     50000
Karim    +     30000
```

➡️ columns horizontally combine

### UNION

```text
Customers
---------
Rahim
Karim
  ↓
Suppliers
---------
ABC
XYZ
```

➡️ rows vertically combine

---

# 1️⃣7️⃣ Multiple UNION

তিনটি query-ও combine করা যায়।

```sql
SELECT city
FROM customers

UNION

SELECT city
FROM suppliers

UNION

SELECT city
FROM employees;
```

Result:

```text
Dhaka
Chittagong
Khulna
Rajshahi
```

Duplicate থাকলে `UNION` remove করবে।

---

# 1️⃣8️⃣ UNION ALL + Multiple Tables

```sql
SELECT email
FROM customers

UNION ALL

SELECT email
FROM employees

UNION ALL

SELECT email
FROM suppliers;
```

এটা সব email একসাথে আনবে এবং duplicate রাখবে।

---

# 1️⃣9️⃣ Set Operation + WHERE

প্রতিটি query-তে নিজের `WHERE` থাকতে পারে।

```sql
SELECT city
FROM customers
WHERE city = 'Dhaka'

UNION

SELECT city
FROM suppliers
WHERE city = 'Dhaka';
```

Result:

```text
Dhaka
```

---

# 2️⃣0️⃣ Set Operation + Aggregate

এটাও করা যায়।

```sql
SELECT COUNT(*) AS total_customers
FROM customers

UNION ALL

SELECT COUNT(*) AS total_suppliers
FROM suppliers;
```

Result:

|total_customers|
|--:|
|100|
|25|

---

# 2️⃣1️⃣ UNION + Label

Analytics report-এ খুব useful।

```sql
SELECT
    'Customer' AS source,
    name
FROM customers

UNION ALL

SELECT
    'Supplier' AS source,
    supplier_name
FROM suppliers;
```

Result:

|source|name|
|---|---|
|Customer|Rahim|
|Customer|Karim|
|Supplier|ABC|
|Supplier|XYZ|

এটা data warehouse/reporting-এ খুব useful technique।

---

# 2️⃣2️⃣ NULL-এর সাথে UNION

ধরো দুই table-এর structure আলাদা।

Customers:

```text
name
city
```

Suppliers:

```text
supplier_name
city
```

তবুও combine করা যাবে:

```sql
SELECT
    name,
    city,
    NULL AS company
FROM customers

UNION ALL

SELECT
    supplier_name,
    city,
    'Supplier Company' AS company
FROM suppliers;
```

এখানে দুই query-তেই 3 columns আছে।

---

# 2️⃣3️⃣ Set Operations Cheat Sheet

|Operator|Meaning|
|---|---|
|`UNION`|Combine + remove duplicates|
|`UNION ALL`|Combine + keep duplicates|
|`INTERSECT`|Common rows|
|`EXCEPT`|First − Second|

মনে রাখার shortcut:

```text
UNION       → OR
INTERSECT   → AND
EXCEPT      → DIFFERENCE
```

---

# 2️⃣4️⃣ Excel-এর সাথে Connection

তুমি Excel অনেক গভীরভাবে শিখেছো, তাই এভাবে মনে রাখো:

|Excel|SQL|
|---|---|
|Append Queries|`UNION ALL`|
|Remove duplicates after append|`UNION`|
|Common records|`INTERSECT`|
|Difference|`EXCEPT`|
|Merge Queries|`JOIN`|

বিশেষ করে Power Query-তে:

> **Append ≈ UNION ALL**

এটা খুব important connection।

---

# 2️⃣5️⃣ Common Beginner Mistakes

### ❌ Mistake 1: Column count different

```sql
SELECT name, city
FROM customers

UNION

SELECT supplier_name
FROM suppliers;
```

❌ ভুল।

---

### ❌ Mistake 2: JOIN আর UNION confuse করা

মনে রাখো:

```text
JOIN  → columns combine
UNION → rows combine
```

---

### ❌ Mistake 3: UNION ALL-এর বদলে UNION

Transaction data combine করার সময় unnecessary duplicate removal performance কমাতে পারে।

---

### ❌ Mistake 4: EXCEPT direction ভুল বোঝা

```sql
A EXCEPT B
```

মানে:

> A-তে আছে কিন্তু B-তে নেই।

এটা:

```text
A - B
```

---

# 🎯 Class 43 Assignment

ধরো তিনটি table:

```text
customers
---------
customer_id
name
city

employees
---------
employee_id
name
city

suppliers
---------
supplier_id
name
city
```

### Q1

Customers এবং employees-এর সব city combine করো, duplicate বাদ দিয়ে।

### Q2

Customers এবং employees-এর সব city combine করো, duplicate সহ।

### Q3

Customers এবং suppliers-এর common city বের করো।

### Q4

Customers-এর এমন city বের করো যা suppliers-এ নেই।

### Q5

Customers + employees + suppliers-এর unique city list বের করো।

### Q6

Customers এবং employees-এর names একসাথে আনো এবং source column তৈরি করো:

```text
source | name
```

### Q7

`UNION` এবং `UNION ALL`-এর মধ্যে পার্থক্য লিখো।

### Q8

`JOIN` এবং `UNION`-এর মূল পার্থক্য লিখো।

### Q9

Sales 2025 + Sales 2026 combine করার জন্য `UNION` নাকি `UNION ALL` বেশি উপযুক্ত? কেন?

### Q10

`A EXCEPT B` কী return করে?

---

# 🧠 Class 43 MCQ

**1. `UNION` কী করে?**

A. Duplicate রাখে  
B. Duplicate remove করে  
C. Table delete করে  
D. Table join করে

**2. `UNION ALL` কী করে?**

A. Duplicate remove করে  
B. Duplicate রাখে  
C. শুধু common rows দেয়  
D. শুধু NULL দেয়

**3. Common records পেতে কোন operator?**

A. UNION  
B. EXCEPT  
C. INTERSECT  
D. JOIN

**4. `A EXCEPT B` মানে কী?**

A. A এবং B-এর common  
B. B-তে আছে A-তে নেই  
C. A-তে আছে B-তে নেই  
D. সব records

**5. JOIN মূলত কী combine করে?**

A. Rows  
B. Columns  
C. Databases  
D. Indexes

**6. UNION মূলত কী combine করে?**

A. Rows/results  
B. Columns only  
C. Indexes  
D. Constraints

**7. দুই SELECT-এর UNION করতে হলে কী গুরুত্বপূর্ণ?**

A. একই table হতে হবে  
B. Same number of columns  
C. Same table name  
D. Same primary key

**8. Sales transactions combine করার ক্ষেত্রে সাধারণত কোনটি বেশি উপযুক্ত?**

A. UNION  
B. UNION ALL  
C. INTERSECT  
D. EXCEPT

**9. `UNION`-এর duplicate removal-এর কারণে কোনটি হতে পারে?**

A. Additional processing  
B. Table deletion  
C. Foreign key creation  
D. Database creation

**10. Power Query-এর Append-এর সবচেয়ে কাছাকাছি SQL operator কোনটি?**

A. JOIN  
B. UNION ALL  
C. EXISTS  
D. GROUP BY

---

## 🔥 আজকের সবচেয়ে গুরুত্বপূর্ণ ৪টি লাইন

```text
UNION      = Combine + Remove Duplicate
UNION ALL  = Combine + Keep Duplicate
INTERSECT  = Common
EXCEPT     = First − Second
```

এবং:

```text
JOIN  → Columns combine
UNION → Rows combine
```

**Class 43-এর পরের logical topic: Class 44 — SQL Date & Time Analytics**, যেখানে আমরা `YEAR()`, `MONTH()`, `DATEDIFF()`, monthly sales, monthly growth, date filtering, age/tenure এবং real-world date analysis করব।


----
# 📘 Class 44 — SQL Date & Time Analytics

আজকের class খুব important, কারণ **Data Analyst / Data Engineer / Database Designer** হিসেবে date নিয়ে কাজ প্রায় প্রতিদিনই করতে হবে।

আজ আমরা শিখব:

1. Date & Time data types
    
2. `YEAR()`, `MONTH()`, `DAY()`
    
3. `CURDATE()`, `NOW()`
    
4. Date filtering
    
5. `BETWEEN`
    
6. `DATEDIFF()`
    
7. Date addition/subtraction
    
8. Monthly/Yearly analysis
    
9. Monthly sales
    
10. Monthly growth
    
11. Age / Experience calculation
    
12. Date grouping
    
13. Common mistakes
    
14. Assignment + MCQ
    

---

# 1️⃣ SQL-এ Date কেন গুরুত্বপূর্ণ?

ধরো orders table:

|order_id|order_date|amount|
|--:|---|--:|
|1|2026-01-05|50000|
|2|2026-01-15|30000|
|3|2026-02-10|70000|
|4|2026-03-20|40000|

Business প্রশ্ন হতে পারে:

- January-তে কত sales?
    
- March-এ কত orders?
    
- গত 30 দিনে কত orders?
    
- দুই order-এর মধ্যে কত দিন?
    
- Customer কত বছর ধরে আছে?
    
- এই বছরের sales কত?
    
- Previous month থেকে growth কত?
    

এসবের জন্য Date & Time SQL জানা দরকার।

---

# 2️⃣ Common Date/Time Data Types

MySQL-এ প্রধানগুলো:

|Type|Example|ব্যবহার|
|---|---|---|
|`DATE`|`2026-09-13`|শুধু date|
|`TIME`|`14:30:00`|শুধু time|
|`DATETIME`|`2026-09-13 14:30:00`|date + time|
|`TIMESTAMP`|`2026-09-13 14:30:00`|timestamp/time tracking|

সাধারণ order date:

```sql
order_date DATE
```

Created time:

```sql
created_at DATETIME
```

---

# 3️⃣ DATE থেকে YEAR বের করা

```sql
SELECT
    order_date,
    YEAR(order_date) AS order_year
FROM orders;
```

Result:

|order_date|order_year|
|---|--:|
|2026-01-05|2026|
|2026-02-10|2026|
|2026-03-20|2026|

---

# 4️⃣ MONTH()

```sql
SELECT
    order_date,
    MONTH(order_date) AS order_month
FROM orders;
```

Result:

|order_date|order_month|
|---|--:|
|2026-01-05|1|
|2026-02-10|2|
|2026-03-20|3|

---

# 5️⃣ DAY()

```sql
SELECT
    order_date,
    DAY(order_date) AS order_day
FROM orders;
```

Result:

```text
05
10
20
```

---

# 6️⃣ একসাথে YEAR + MONTH + DAY

```sql
SELECT
    order_date,
    YEAR(order_date) AS year,
    MONTH(order_date) AS month,
    DAY(order_date) AS day
FROM orders;
```

এটা date analysis-এর basic foundation।

---

# 7️⃣ CURDATE()

আজকের date বের করতে:

```sql
SELECT CURDATE();
```

যেমন আজ যদি:

```text
2026-09-13
```

হয়, result হবে:

```text
2026-09-13
```

### Use case

আজকের orders:

```sql
SELECT *
FROM orders
WHERE order_date = CURDATE();
```

---

# 8️⃣ NOW()

Current date + time:

```sql
SELECT NOW();
```

Example:

```text
2026-09-13 09:30:25
```

Difference:

```text
CURDATE() → শুধু date
NOW()     → date + time
```

---

# 9️⃣ Current Year-এর Orders

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = YEAR(CURDATE());
```

এখানে:

```sql
YEAR(order_date)
```

order-এর year বের করছে।

আর:

```sql
YEAR(CURDATE())
```

বর্তমান year বের করছে।

---

# 🔟 নির্দিষ্ট Year Filter

2026 সালের orders:

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026;
```

---

# 1️⃣1️⃣ নির্দিষ্ট Month

January 2026:

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026
  AND MONTH(order_date) = 1;
```

---

# 1️⃣2️⃣ Date Range

ধরো January 1 থেকে January 31:

```sql
SELECT *
FROM orders
WHERE order_date BETWEEN '2026-01-01'
                     AND '2026-01-31';
```

### মনে রাখবে

`BETWEEN` inclusive।

অর্থাৎ:

```text
2026-01-01 ✅
2026-01-31 ✅
```

দুটিই included।

---

# 1️⃣3️⃣ `>=` এবং `<` দিয়ে Date Filtering

Production SQL-এ অনেক সময় এই pattern বেশি useful:

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
  AND order_date < '2026-02-01';
```

এখানে January পুরো month পাওয়া যাবে।

এটা বিশেষভাবে `DATETIME` column-এর ক্ষেত্রে গুরুত্বপূর্ণ।

---

# 1️⃣4️⃣ কেন `< next month` useful?

ধরো:

```text
2026-01-31 23:59:59
```

তখন শুধু:

```sql
<= '2026-01-31'
```

ব্যবহার করলে `DATETIME`-এর ক্ষেত্রে unexpected result হতে পারে।

তাই:

```sql
WHERE created_at >= '2026-01-01'
  AND created_at < '2026-02-01'
```

এটা clean pattern।

### Golden Rule ⭐

> Date range-এর ক্ষেত্রে অনেক production query-তে `>= start AND < next_period` pattern খুব useful।

---

# 1️⃣5️⃣ DATEDIFF()

দুই date-এর মধ্যে কত দিন difference তা বের করে।

```sql
SELECT DATEDIFF(
    '2026-09-13',
    '2026-09-01'
);
```

Result:

```text
12
```

কারণ 1 September → 13 September = 12 days।

---

# 1️⃣6️⃣ Order কতদিন আগে হয়েছে?

```sql
SELECT
    order_id,
    order_date,
    DATEDIFF(CURDATE(), order_date) AS days_ago
FROM orders;
```

Result:

|order_id|order_date|days_ago|
|--:|---|--:|
|1|2026-09-01|12|
|2|2026-09-05|8|

---

# 1️⃣7️⃣ Last 30 Days

```sql
SELECT *
FROM orders
WHERE order_date >= CURDATE() - INTERVAL 30 DAY;
```

এখানে:

```sql
INTERVAL 30 DAY
```

মানে 30 দিন।

---

# 1️⃣8️⃣ Last 7 Days

```sql
SELECT *
FROM orders
WHERE order_date >= CURDATE() - INTERVAL 7 DAY;
```

---

# 1️⃣9️⃣ Next 7 Days

যদি future date থাকে:

```sql
SELECT *
FROM appointments
WHERE appointment_date
      BETWEEN CURDATE()
      AND CURDATE() + INTERVAL 7 DAY;
```

---

# 2️⃣0️⃣ DATE_ADD()

কোনো date-এর সাথে সময় যোগ করতে:

```sql
SELECT DATE_ADD(
    '2026-01-01',
    INTERVAL 10 DAY
);
```

Result:

```text
2026-01-11
```

---

### 1 Month যোগ

```sql
SELECT DATE_ADD(
    '2026-01-01',
    INTERVAL 1 MONTH
);
```

Result:

```text
2026-02-01
```

---

# 2️⃣1️⃣ DATE_SUB()

Date থেকে সময় কমাতে:

```sql
SELECT DATE_SUB(
    '2026-09-13',
    INTERVAL 7 DAY
);
```

Result:

```text
2026-09-06
```

---

# 2️⃣2️⃣ YEAR-MONTH Analysis

এখন real analytics শুরু করি।

ধরো:

```text
orders
```

এবং:

```text
quantity
price
```

Monthly sales:

```sql
SELECT
    YEAR(o.order_date) AS year,
    MONTH(o.order_date) AS month,
    SUM(o.quantity * p.price) AS total_sales
FROM orders o
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    YEAR(o.order_date),
    MONTH(o.order_date)
ORDER BY
    year,
    month;
```

Result:

|year|month|total_sales|
|--:|--:|--:|
|2026|1|110000|
|2026|2|90000|
|2026|3|120000|
|2026|4|150000|

---

# 2️⃣3️⃣ Better Month Format

শুধু `1`, `2`, `3` না দেখিয়ে:

```text
2026-01
2026-02
2026-03
```

দেখাতে পারি।

MySQL-এ:

```sql
DATE_FORMAT(order_date, '%Y-%m')
```

Example:

```sql
SELECT
    DATE_FORMAT(order_date, '%Y-%m') AS month,
    COUNT(*) AS total_orders
FROM orders
GROUP BY DATE_FORMAT(order_date, '%Y-%m')
ORDER BY month;
```

---

# 2️⃣4️⃣ Month Name

```sql
SELECT
    MONTHNAME(order_date) AS month_name,
    COUNT(*) AS total_orders
FROM orders
GROUP BY MONTHNAME(order_date);
```

Result:

```text
January
February
March
```

⚠️ কিন্তু এখানে একটি problem আছে।

যদি multiple year থাকে:

```text
January 2025
January 2026
```

দুটো January একসাথে group হয়ে যাবে।

তাই business analytics-এ:

```sql
DATE_FORMAT(order_date, '%Y-%m')
```

অনেক বেশি useful।

---

# 2️⃣5️⃣ Yearly Sales

```sql
SELECT
    YEAR(order_date) AS year,
    SUM(amount) AS total_sales
FROM orders
GROUP BY YEAR(order_date)
ORDER BY year;
```

---

# 2️⃣6️⃣ Quarterly Analysis

এক বছরে 4টি quarter:

```text
Q1 → Jan-Mar
Q2 → Apr-Jun
Q3 → Jul-Sep
Q4 → Oct-Dec
```

MySQL-এ:

```sql
SELECT
    YEAR(order_date) AS year,
    QUARTER(order_date) AS quarter,
    SUM(amount) AS total_sales
FROM orders
GROUP BY
    YEAR(order_date),
    QUARTER(order_date)
ORDER BY
    year,
    quarter;
```

---

# 2️⃣7️⃣ Weekday Analysis

কোন দিনে বেশি orders?

```sql
SELECT
    DAYNAME(order_date) AS day_name,
    COUNT(*) AS total_orders
FROM orders
GROUP BY DAYNAME(order_date);
```

যেমন:

|day_name|total_orders|
|---|--:|
|Monday|15|
|Tuesday|22|
|Friday|30|

---

# 2️⃣8️⃣ Weekday Number

```sql
SELECT
    DAYOFWEEK(order_date) AS day_number
FROM orders;
```

MySQL-এ সাধারণভাবে:

```text
1 = Sunday
2 = Monday
...
7 = Saturday
```

---

# 2️⃣9️⃣ Age Calculation

ধরো customers:

```text
date_of_birth
```

Age:

```sql
SELECT
    name,
    TIMESTAMPDIFF(
        YEAR,
        date_of_birth,
        CURDATE()
    ) AS age
FROM customers;
```

এটা age calculation-এর practical pattern।

---

# 3️⃣0️⃣ Employee Experience

ধরো:

```text
joining_date
```

কত বছর কাজ করেছে:

```sql
SELECT
    name,
    TIMESTAMPDIFF(
        YEAR,
        joining_date,
        CURDATE()
    ) AS experience_years
FROM employees;
```

---

# 3️⃣1️⃣ Exact Months of Experience

```sql
SELECT
    name,
    TIMESTAMPDIFF(
        MONTH,
        joining_date,
        CURDATE()
    ) AS experience_months
FROM employees;
```

---

# 3️⃣2️⃣ Customer Retention-এর Basic Idea

Customer-এর first order date বের করা:

```sql
SELECT
    customer_id,
    MIN(order_date) AS first_order_date
FROM orders
GROUP BY customer_id;
```

Last order:

```sql
SELECT
    customer_id,
    MAX(order_date) AS last_order_date
FROM orders
GROUP BY customer_id;
```

এগুলো পরে **Customer Analytics / Retention / Cohort Analysis**-এ খুব useful হবে।

---

# 3️⃣3️⃣ Days Since Last Order

```sql
SELECT
    customer_id,
    MAX(order_date) AS last_order_date,
    DATEDIFF(
        CURDATE(),
        MAX(order_date)
    ) AS days_since_last_order
FROM orders
GROUP BY customer_id;
```

এখানে business প্রশ্ন:

> কোন customer অনেকদিন ধরে order করেনি?

---

# 3️⃣4️⃣ Inactive Customers

ধরো 90 দিন ধরে order নেই:

```sql
SELECT
    customer_id,
    MAX(order_date) AS last_order_date
FROM orders
GROUP BY customer_id
HAVING MAX(order_date)
       < CURDATE() - INTERVAL 90 DAY;
```

🔥 এখানে দেখো:

```text
WHERE → individual rows
HAVING → grouped customer result
```

এটা Class 34 + Class 44-এর combination।

---

# 3️⃣5️⃣ Monthly Growth

এটা আমরা Window Function-এ আগেও করেছি।

প্রথমে monthly sales:

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(order_date, '%Y-%m') AS month,
        SUM(amount) AS sales
    FROM orders
    GROUP BY DATE_FORMAT(order_date, '%Y-%m')
)
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_sales
FROM monthly_sales;
```

Result:

|month|sales|previous_sales|
|---|--:|--:|
|2026-01|100000|NULL|
|2026-02|120000|100000|
|2026-03|150000|120000|

---

# 3️⃣6️⃣ Monthly Growth %

এখন calculation:

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(order_date, '%Y-%m') AS month,
        SUM(amount) AS sales
    FROM orders
    GROUP BY DATE_FORMAT(order_date, '%Y-%m')
),
comparison AS (
    SELECT
        month,
        sales,
        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales
    FROM monthly_sales
)
SELECT
    month,
    sales,
    previous_sales,
    ROUND(
        100.0 * (sales - previous_sales)
        / NULLIF(previous_sales, 0),
        2
    ) AS growth_percentage
FROM comparison;
```

---

# 3️⃣7️⃣ কেন `NULLIF()`?

ধরো previous sales:

```text
0
```

তাহলে:

```sql
sales / 0
```

করলে division-by-zero problem হবে।

তাই:

```sql
NULLIF(previous_sales, 0)
```

0 হলে `NULL` করে দেয়।

### Golden Rule

> Division করার সময় denominator 0 হওয়ার সম্ভাবনা থাকলে `NULLIF(..., 0)` useful।

---

# 3️⃣8️⃣ Date Analytics Full Workflow

একজন Data Analyst হিসেবে তুমি অনেক query এভাবে build করবে:

```text
Raw Orders
    ↓
JOIN
    ↓
Date Extraction
    ↓
GROUP BY
    ↓
Monthly/Yearly Sales
    ↓
LAG()
    ↓
Growth %
    ↓
Business Insight
```

---

# 3️⃣9️⃣ Excel → SQL Mapping

তুমি Excel আগে শিখেছো, তাই connection:

|Excel|SQL|
|---|---|
|YEAR()|`YEAR()`|
|MONTH()|`MONTH()`|
|TODAY()|`CURDATE()`|
|NOW()|`NOW()`|
|Date Difference|`DATEDIFF()`|
|Add days|`DATE_ADD()`|
|Subtract days|`DATE_SUB()`|
|Pivot by Month|`GROUP BY` date|
|Previous Month|`LAG()`|
|Monthly Growth|`LAG()` + calculation|
|Current Date|`CURDATE()`|

---

# ⚠️ 4️⃣0️⃣ Common Beginner Mistakes

### ❌ Mistake 1

Date-কে string হিসেবে compare করা:

```sql
WHERE order_date = 'January';
```

ভুল।

Date column-এর actual format বুঝতে হবে।

---

### ❌ Mistake 2

Month-only grouping:

```sql
GROUP BY MONTH(order_date)
```

যদি multiple year থাকে, 2025 January এবং 2026 January একসাথে চলে আসবে।

Better:

```sql
GROUP BY
    YEAR(order_date),
    MONTH(order_date);
```

অথবা:

```sql
GROUP BY DATE_FORMAT(order_date, '%Y-%m');
```

---

### ❌ Mistake 3

`DATETIME`-এ শুধু শেষ date ব্যবহার করা

```sql
WHERE created_at <= '2026-01-31'
```

এর ফলে January 31-এর দিনের পরের time অংশ বাদ পড়তে পারে।

Better:

```sql
WHERE created_at >= '2026-01-01'
  AND created_at < '2026-02-01';
```

---

### ❌ Mistake 4

Age = Year difference

শুধু:

```sql
YEAR(CURDATE()) - YEAR(date_of_birth)
```

ব্যবহার করলে birthday এখনো আসেনি—এমন ক্ষেত্রে age 1 বছর বেশি হতে পারে।

Practical age-এর জন্য:

```sql
TIMESTAMPDIFF(YEAR, date_of_birth, CURDATE())
```

ব্যবহার করা ভালো।

---

# 🧠 Class 44 Golden Rules

```text
YEAR()       → Year বের করে
MONTH()      → Month বের করে
DAY()        → Day বের করে

CURDATE()    → আজকের date
NOW()        → current date + time

DATEDIFF()   → দুই date-এর day difference

DATE_ADD()   → date-এ যোগ
DATE_SUB()   → date থেকে বাদ

TIMESTAMPDIFF() → বছর/month/day difference

DATE_FORMAT()   → date সুন্দরভাবে format/group
```

সবচেয়ে important:

> **Date Analytics = Date Extraction + Filtering + Grouping + Difference + Window Functions**

---

# 📝 Class 44 Assignment

ধরো `orders` table:

```text
order_id
customer_id
order_date
amount
```

### Q1

সব order-এর year বের করো।

### Q2

সব order-এর month বের করো।

### Q3

2026 সালের সব orders বের করো।

### Q4

January 2026-এর orders বের করো।

### Q5

গত 30 দিনের orders বের করো।

### Q6

প্রতিটি order আজ থেকে কতদিন আগে হয়েছে বের করো।

### Q7

Year-wise total sales বের করো।

### Q8

Month-wise total sales বের করো `YYYY-MM` format-এ।

### Q9

Quarter-wise sales বের করো।

### Q10

প্রতিটি customer-এর last order date বের করো।

### Q11

প্রতিটি customer-এর last order থেকে কতদিন হয়েছে বের করো।

### Q12

90 দিনের বেশি সময় ধরে order করেনি এমন customer বের করো।

### Q13

Monthly sales এবং previous month sales বের করো।

### Q14

Monthly growth percentage বের করো।

### Q15 ⭐

একটি final query তৈরি করো যেখানে থাকবে:

```text
month
sales
previous_sales
growth_percentage
running_total
```

---

# 🧪 Class 44 MCQ

**1. শুধু current date পেতে কোন function?**

A. `NOW()`  
B. `CURDATE()`  
C. `DATE_NOW()`  
D. `CURRENT_YEAR()`

**2. দুই date-এর day difference বের করতে কোন function?**

A. `DATE_DIFF()`  
B. `DATEDIFF()`  
C. `DAYDIFF()`  
D. `DIFF_DATE()`

**3. Current date + time কোনটি?**

A. `CURDATE()`  
B. `NOW()`  
C. `TODAY()`  
D. `CURRENT_DAY()`

**4. 2026-এর month বের করতে কোন function?**

A. `YEAR()`  
B. `MONTH()`  
C. `DATE()`  
D. `MONTHNAME()`

**5. Date-এর সাথে 7 দিন যোগ করতে কোনটি?**

A. `DATE_ADD()`  
B. `DATE_PLUS()`  
C. `ADD_DATE()`  
D. `DATE_SUM()`

**6. Customer-এর age calculation-এর জন্য কোনটি বেশি appropriate?**

A. `YEAR(date)`  
B. `TIMESTAMPDIFF()`  
C. `MONTH()`  
D. `DAY()`

**7. Monthly sales বের করতে কোন combination useful?**

A. `GROUP BY` + date  
B. শুধু `ORDER BY`  
C. শুধু `JOIN`  
D. শুধু `WHERE`

**8. Previous month's sales পেতে কোন window function?**

A. `LEAD()`  
B. `LAG()`  
C. `RANK()`  
D. `FIRST_VALUE()`

**9. `DATE_FORMAT(order_date, '%Y-%m')` কী করতে সাহায্য করে?**

A. Date delete  
B. Date format/group  
C. Table create  
D. Row update

**10. Multiple years থাকলে শুধু `MONTH(order_date)` দিয়ে group করলে কী সমস্যা হতে পারে?**

A. Query চলবে না  
B. সব date NULL হবে  
C. Different years-এর একই month একসাথে group হবে  
D. Table delete হবে

---

## 🎯 আজকের সবচেয়ে গুরুত্বপূর্ণ concept

```text
DATE
 ↓
YEAR / MONTH / DAY
 ↓
WHERE / BETWEEN
 ↓
DATEDIFF
 ↓
GROUP BY Month
 ↓
LAG()
 ↓
Growth %
```

এটাই **real-world SQL Date Analytics pipeline**।

**Next: Class 45 — Advanced String & NULL Handling**: `COALESCE()`, `NULLIF()`, `IFNULL()`, `CASE`, text cleaning, email/phone extraction, NULL-safe calculations এবং real-world data cleaning।



----
# 📘 Class 45 — Advanced String & NULL Handling in SQL

আজকের class-এ আমরা SQL-এর **data cleaning + NULL handling** শিখব। Data Analyst এবং Database Designer—দুই ক্ষেত্রেই এগুলো খুব গুরুত্বপূর্ণ।

আজকের topics:

1. `NULL` আসলে কী?
    
2. `COALESCE()`
    
3. `IFNULL()`
    
4. `NULLIF()`
    
5. `CASE WHEN`
    
6. String functions
    
7. `CONCAT()`
    
8. `LOWER()` / `UPPER()`
    
9. `TRIM()`
    
10. `SUBSTRING()`
    
11. `LEFT()` / `RIGHT()`
    
12. `LENGTH()`
    
13. `REPLACE()`
    
14. Email/phone cleaning
    
15. NULL-safe calculation
    
16. Real-world data cleaning
    
17. Common mistakes
    
18. Assignment + MCQ
    

---

# 1️⃣ NULL কী?

`NULL` মানে:

> **Unknown / Missing / No value**

এটা `0` না।

এটা empty string `''`-ও না।

এমনকি:

```text
NULL ≠ 0
NULL ≠ ''
NULL ≠ 'NULL'
```

উদাহরণ:

|name|phone|salary|
|---|---|--:|
|Rahim|01711111111|50000|
|Karim|NULL|60000|
|Hasan|01822222222|NULL|

Karim-এর phone সম্পর্কে information নেই।

Hasan-এর salary সম্পর্কে information নেই।

---

# 2️⃣ NULL Check

❌ ভুল:

```sql
SELECT *
FROM employees
WHERE phone = NULL;
```

সঠিক:

```sql
SELECT *
FROM employees
WHERE phone IS NULL;
```

NULL নেই:

```sql
SELECT *
FROM employees
WHERE phone IS NOT NULL;
```

### Golden Rule ⭐

> `NULL` check করতে `=` নয় → `IS NULL`

---

# 3️⃣ COALESCE()

`COALESCE()` খুব গুরুত্বপূর্ণ।

এটি **প্রথম non-NULL value** return করে।

```sql
SELECT
    COALESCE(phone, 'No Phone') AS phone
FROM employees;
```

যদি:

|phone|
|---|
|01711111111|
|NULL|
|01822222222|

Result:

|phone|
|---|
|01711111111|
|No Phone|
|01822222222|

---

# 4️⃣ Multiple Values with COALESCE()

```sql
SELECT
    COALESCE(phone, email, 'No Contact') AS contact
FROM customers;
```

Logic:

```text
phone আছে?
   ↓
Yes → phone

No
 ↓
email আছে?
 ↓
Yes → email

No
 ↓
'No Contact'
```

অর্থাৎ:

> `COALESCE()` = প্রথম available value

---

# 5️⃣ IFNULL()

MySQL-এ:

```sql
IFNULL(value, replacement)
```

Example:

```sql
SELECT
    name,
    IFNULL(phone, 'No Phone') AS phone
FROM customers;
```

যদি phone NULL হয়:

```text
NULL → No Phone
```

---

# 6️⃣ COALESCE vs IFNULL

|Feature|COALESCE|IFNULL|
|---|---|---|
|Multiple values|✅|❌|
|দুই value|✅|✅|
|Standard SQL|✅|MySQL-specific|
|MySQL|✅|✅|

Example:

```sql
COALESCE(phone, email, address, 'Unknown')
```

এখানে একাধিক fallback আছে।

`IFNULL()`:

```sql
IFNULL(phone, 'No Phone')
```

শুধু দুইটি value।

### Beginner Rule

> MySQL-specific হলে `IFNULL()` বুঝবে।  
> Portable SQL চাইলে `COALESCE()` বেশি useful।

---

# 7️⃣ NULL Calculation Problem

ধরো:

|product|price|discount|
|---|--:|--:|
|Laptop|80000|5000|
|Monitor|30000|NULL|

Query:

```sql
SELECT
    product,
    price - discount AS final_price
FROM products;
```

দ্বিতীয় row:

```text
30000 - NULL = NULL
```

কারণ NULL-এর সাথে calculation করলে result সাধারণত NULL হয়।

---

# 8️⃣ COALESCE দিয়ে Fix

```sql
SELECT
    product,
    price - COALESCE(discount, 0) AS final_price
FROM products;
```

এখন:

```text
Monitor
30000 - 0
= 30000
```

🔥 Real-world data cleaning-এ এটি খুব common।

---

# 9️⃣ NULLIF()

`NULLIF()` এর syntax:

```sql
NULLIF(value1, value2)
```

যদি দুটো value equal হয় → `NULL`

Example:

```sql
SELECT NULLIF(10, 10);
```

Result:

```text
NULL
```

কিন্তু:

```sql
SELECT NULLIF(10, 5);
```

Result:

```text
10
```

---

# 🔟 NULLIF() কেন দরকার?

সবচেয়ে common use:

> **Division by zero prevent করা**

ধরো:

```sql
SELECT
    sales / quantity
FROM orders;
```

যদি quantity = 0 হয় → সমস্যা।

তাই:

```sql
SELECT
    sales / NULLIF(quantity, 0) AS average_price
FROM orders;
```

যদি:

```text
quantity = 0
```

তাহলে:

```text
NULLIF(0,0)
→ NULL
```

এবং:

```text
sales / NULL
→ NULL
```

Division-by-zero error এড়ানো যায়।

---

# 1️⃣1️⃣ COALESCE vs NULLIF

মনে রাখো:

```text
COALESCE()
↓
NULL হলে alternative value

NULLIF()
↓
দুই value same হলে NULL
```

Example:

```sql
COALESCE(phone, 'Unknown')
```

মানে:

> Phone NULL হলে Unknown।

আর:

```sql
NULLIF(quantity, 0)
```

মানে:

> Quantity 0 হলে NULL করো।

---

# 1️⃣2️⃣ CASE WHEN

SQL-এর অন্যতম important logic feature।

Syntax:

```sql
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
END
```

Example:

```sql
SELECT
    name,
    salary,
    CASE
        WHEN salary >= 80000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_level
FROM employees;
```

---

# 1️⃣3️⃣ CASE-এর Flow

ধরো salary:

```text
90000
60000
40000
```

Query:

```sql
CASE
    WHEN salary >= 80000 THEN 'High'
    WHEN salary >= 50000 THEN 'Medium'
    ELSE 'Low'
END
```

Result:

|salary|salary_level|
|--:|---|
|90000|High|
|60000|Medium|
|40000|Low|

---

# 1️⃣4️⃣ CASE + NULL

```sql
SELECT
    name,
    CASE
        WHEN salary IS NULL THEN 'Salary Missing'
        WHEN salary >= 50000 THEN 'Good'
        ELSE 'Below Target'
    END AS status
FROM employees;
```

এখানে NULL-এর জন্য আলাদা logic।

---

# 1️⃣5️⃣ CASE দিয়ে Data Classification

ধরো order amount:

```sql
SELECT
    order_id,
    amount,
    CASE
        WHEN amount >= 100000 THEN 'Large'
        WHEN amount >= 50000 THEN 'Medium'
        ELSE 'Small'
    END AS order_category
FROM orders;
```

এটা Data Analytics-এ খুব common।

---

# 1️⃣6️⃣ CASE + Aggregate

ধরো আমরা জানতে চাই:

> কতজন employee IT department-এ?

```sql
SELECT
    COUNT(
        CASE
            WHEN department = 'IT' THEN 1
        END
    ) AS it_employees
FROM employees;
```

আরেকটি pattern:

```sql
SELECT
    SUM(
        CASE
            WHEN department = 'IT' THEN 1
            ELSE 0
        END
    ) AS it_employees
FROM employees;
```

---

# 1️⃣7️⃣ Conditional SUM

ধরো IT department-এর total salary:

```sql
SELECT
    SUM(
        CASE
            WHEN department = 'IT'
            THEN salary
            ELSE 0
        END
    ) AS it_salary
FROM employees;
```

এটা খুব useful analytics technique।

---

# 1️⃣8️⃣ String Functions

এখন text cleaning শুরু করি।

Common functions:

|Function|কাজ|
|---|---|
|`UPPER()`|uppercase|
|`LOWER()`|lowercase|
|`TRIM()`|extra spaces remove|
|`LENGTH()`|string length|
|`LEFT()`|left characters|
|`RIGHT()`|right characters|
|`SUBSTRING()`|অংশ বের করা|
|`REPLACE()`|text replace|
|`CONCAT()`|text combine|

---

# 1️⃣9️⃣ UPPER()

```sql
SELECT
    UPPER(name) AS name_upper
FROM customers;
```

`rahim` →

```text
RAHIM
```

---

# 2️⃣0️⃣ LOWER()

```sql
SELECT
    LOWER(email) AS email
FROM customers;
```

Example:

```text
RAHIM@GMAIL.COM
```

→

```text
rahim@gmail.com
```

Email cleaning-এ useful।

---

# 2️⃣1️⃣ TRIM()

ধরো:

```text
'   Rahim   '
```

Query:

```sql
SELECT TRIM('   Rahim   ');
```

Result:

```text
Rahim
```

Database cleaning:

```sql
SELECT
    TRIM(name) AS clean_name
FROM customers;
```

---

# 2️⃣2️⃣ LEFT()

String-এর বাম দিক থেকে characters:

```sql
SELECT LEFT('Bangladesh', 4);
```

Result:

```text
Bang
```

---

# 2️⃣3️⃣ RIGHT()

```sql
SELECT RIGHT('Bangladesh', 4);
```

Result:

```text
desh
```

---

# 2️⃣4️⃣ SUBSTRING()

মাঝখান থেকে অংশ নিতে:

```sql
SELECT SUBSTRING('Bangladesh', 1, 4);
```

Result:

```text
Bang
```

Syntax:

```text
SUBSTRING(text, starting_position, length)
```

---

# 2️⃣5️⃣ Email Username বের করা

ধরো:

```text
atiar@gmail.com
```

`@`-এর আগের অংশ চাই।

MySQL-এ:

```sql
SELECT
    SUBSTRING_INDEX(email, '@', 1) AS username
FROM customers;
```

Result:

```text
atiar
```

এটা practical string analytics-এর example।

---

# 2️⃣6️⃣ Email Domain বের করা

```sql
SELECT
    SUBSTRING_INDEX(email, '@', -1) AS domain
FROM customers;
```

Result:

```text
gmail.com
```

---

# 2️⃣7️⃣ REPLACE()

Text-এর একটি অংশ অন্য text দিয়ে replace:

```sql
SELECT
    REPLACE(phone, '-', '') AS clean_phone
FROM customers;
```

যদি:

```text
017-123-45678
```

হয়:

```text
01712345678
```

---

# 2️⃣8️⃣ Multiple REPLACE

ধরো phone:

```text
017-123 45678
```

Hyphen এবং space দুটোই remove করতে:

```sql
SELECT
    REPLACE(
        REPLACE(phone, '-', ''),
        ' ',
        ''
    ) AS clean_phone
FROM customers;
```

Result:

```text
01712345678
```

---

# 2️⃣9️⃣ CONCAT()

দুই বা তার বেশি text combine করতে:

```sql
SELECT
    CONCAT(first_name, ' ', last_name) AS full_name
FROM customers;
```

Example:

```text
first_name = Md.
last_name = Atiar
```

Result:

```text
Md. Atiar
```

---

# 3️⃣0️⃣ CONCAT + NULL Problem

এখানে একটি important issue আছে।

```sql
CONCAT(first_name, ' ', last_name)
```

যদি কোনো value NULL হয়, MySQL-এর `CONCAT()`-এ পুরো result NULL হতে পারে।

তাই:

```sql
SELECT
    CONCAT(
        COALESCE(first_name, ''),
        ' ',
        COALESCE(last_name, '')
    ) AS full_name
FROM customers;
```

এটা safer।

---

# 3️⃣1️⃣ LENGTH()

String-এর length:

```sql
SELECT
    name,
    LENGTH(name) AS name_length
FROM customers;
```

Example:

```text
Rahim → 5
Karim → 5
```

---

# 3️⃣2️⃣ Data Cleaning Example

ধরো messy customer data:

|name|email|phone|
|---|---|---|
|`Rahim`|`RAHIM@GMAIL.COM`|`017-111-11111`|
|`karim`|`KARIM@YAHOO.COM`|`018 222 22222`|

Clean করার query:

```sql
SELECT
    TRIM(name) AS clean_name,

    LOWER(TRIM(email)) AS clean_email,

    REPLACE(
        REPLACE(TRIM(phone), '-', ''),
        ' ',
        ''
    ) AS clean_phone

FROM customers;
```

🔥 এটা real-world data cleaning-এর খুব practical pattern।

---

# 3️⃣3️⃣ Missing Data Label

```sql
SELECT
    name,
    COALESCE(phone, 'Missing') AS phone_status
FROM customers;
```

আরও useful:

```sql
SELECT
    name,
    CASE
        WHEN phone IS NULL THEN 'Missing'
        ELSE 'Available'
    END AS phone_status
FROM customers;
```

---

# 3️⃣4️⃣ NULL vs Empty String

খুব গুরুত্বপূর্ণ।

এগুলো আলাদা:

```text
NULL
''
'   '
```

`TRIM()` ব্যবহার করে spaces clean করা যায়:

```sql
TRIM(phone)
```

কিন্তু empty string:

```text
''
```

NULL নয়।

---

# 3️⃣5️⃣ Empty String-কে NULL করা

ধরো:

```text
phone = ''
```

এটাকে NULL করতে:

```sql
NULLIF(TRIM(phone), '')
```

এখানে:

```text
TRIM(phone)
```

প্রথমে spaces remove করবে।

তারপর:

```text
NULLIF(..., '')
```

empty string হলে NULL করবে।

Example:

```sql
SELECT
    NULLIF(TRIM(phone), '') AS clean_phone
FROM customers;
```

🔥 এটি খুব useful data-cleaning pattern।

---

# 3️⃣6️⃣ Powerful Cleaning Pattern

একটি phone field clean করতে:

```sql
SELECT
    COALESCE(
        NULLIF(
            REPLACE(
                REPLACE(TRIM(phone), '-', ''),
                ' ',
                ''
            ),
            ''
        ),
        'No Phone'
    ) AS clean_phone
FROM customers;
```

Flow:

```text
Raw phone
   ↓
TRIM
   ↓
REPLACE "-"
   ↓
REPLACE " "
   ↓
NULLIF empty string
   ↓
COALESCE missing value
   ↓
Clean phone
```

এটাই real-world SQL data cleaning-এর style।

---

# 3️⃣7️⃣ CASE + COALESCE

```sql
SELECT
    name,
    CASE
        WHEN COALESCE(salary, 0) = 0
            THEN 'Salary Missing'
        WHEN salary >= 50000
            THEN 'Good'
        ELSE 'Low'
    END AS salary_status
FROM employees;
```

---

# 3️⃣8️⃣ Data Quality Check

ধরো আমরা দেখতে চাই কোন employee-এর email missing:

```sql
SELECT
    name,
    CASE
        WHEN email IS NULL
             OR TRIM(email) = ''
        THEN 'Invalid/Missing'
        ELSE 'Valid'
    END AS email_status
FROM employees;
```

এখানে আমরা দুই ধরনের missing value ধরছি:

```text
NULL
''
```

---

# 3️⃣9️⃣ SQL Data Cleaning Workflow

তুমি Data Analyst হিসেবে এই workflow মনে রাখতে পারো:

```text
Raw Data
   ↓
TRIM()
   ↓
UPPER()/LOWER()
   ↓
REPLACE()
   ↓
NULLIF()
   ↓
COALESCE()
   ↓
CASE
   ↓
Validation
   ↓
Clean Data
```

---

# 4️⃣0️⃣ Excel → SQL Connection

তুমি Excel-এর Data Cleaning already শিখেছো।

|Excel|SQL|
|---|---|
|`TRIM()`|`TRIM()`|
|`UPPER()`|`UPPER()`|
|`LOWER()`|`LOWER()`|
|`LEFT()`|`LEFT()`|
|`RIGHT()`|`RIGHT()`|
|`MID()`|`SUBSTRING()`|
|`SUBSTITUTE()`|`REPLACE()`|
|`CONCAT()`|`CONCAT()`|
|`IF()`|`CASE WHEN`|
|IFERROR-like NULL handling|`COALESCE()` / `IFNULL()`|
|Missing check|`IS NULL`|

তাই Excel-এর skill SQL-এ সরাসরি কাজে লাগছে। 🔥

---

# ⚠️ Common Beginner Mistakes

### ❌ Mistake 1

```sql
WHERE salary = NULL
```

সঠিক:

```sql
WHERE salary IS NULL
```

---

### ❌ Mistake 2

```sql
salary + bonus
```

যদি bonus NULL হয়, result NULL হতে পারে।

Better:

```sql
salary + COALESCE(bonus, 0)
```

---

### ❌ Mistake 3

`NULL` এবং empty string একই মনে করা।

```text
NULL ≠ ''
```

---

### ❌ Mistake 4

`NOT IN` + NULL-এর danger ভুলে যাওয়া।

যেমন:

```sql
WHERE customer_id NOT IN (
    SELECT customer_id
    FROM orders
);
```

Subquery-তে NULL থাকলে unexpected result হতে পারে।

এই ধরনের missing-related logic-এ:

```sql
NOT EXISTS
```

অনেক ক্ষেত্রে safer।

---

# 🧠 Class 45 Golden Cheat Sheet

```text
IS NULL
    → NULL check

COALESCE()
    → প্রথম non-NULL value

IFNULL()
    → NULL হলে replacement

NULLIF()
    → দুই value same হলে NULL

CASE WHEN
    → SQL-এর IF/ELSE logic

TRIM()
    → extra spaces remove

UPPER()
    → uppercase

LOWER()
    → lowercase

REPLACE()
    → text replace

SUBSTRING()
    → text-এর অংশ বের করা

CONCAT()
    → text combine

LENGTH()
    → text length
```

সবচেয়ে important তিনটি:

> **COALESCE = NULL হলে alternative**

> **NULLIF = equal হলে NULL**

> **CASE WHEN = condition-based business logic**

---

# 📝 Class 45 Assignment

ধরো `customers` table:

```text
customer_id
first_name
last_name
email
phone
city
```

এবং `employees`:

```text
employee_id
name
salary
bonus
department
```

### Q1

NULL phone-কে `'No Phone'` হিসেবে দেখাও।

### Q2

NULL bonus-কে `0` ধরে salary + bonus calculate করো।

### Q3

সব customer name uppercase করো।

### Q4

সব email lowercase করো।

### Q5

Customer name-এর extra spaces remove করো।

### Q6

Phone থেকে `-` এবং spaces remove করো।

### Q7

Email থেকে username বের করো।

### Q8

Email থেকে domain বের করো।

### Q9

Salary classify করো:

```text
>= 80000 → High
>= 50000 → Medium
< 50000  → Low
```

### Q10

NULL বা empty email identify করো।

### Q11

`NULLIF(TRIM(phone), '')` কেন useful—নিজের ভাষায় explain করো।

### Q12 ⭐

একটি clean customer query লিখো যেখানে থাকবে:

```text
customer_id
clean_name
clean_email
clean_phone
email_status
```

### Q13 ⭐

Employee-এর জন্য:

```text
name
salary
bonus
total_salary
salary_level
```

calculate করো।

---

# 🧪 Class 45 MCQ

**1. NULL check করার সঠিক syntax কোনটি?**

A. `= NULL`  
B. `IS NULL`  
C. `== NULL`  
D. `NULL =`

**2. `COALESCE(a,b,c)` কী return করে?**

A. সব value  
B. শেষ NULL value  
C. প্রথম non-NULL value  
D. শুধু NULL

**3. `NULLIF(10,10)` কী return করবে?**

A. 10  
B. 0  
C. NULL  
D. Error

**4. Division by zero prevent করতে কোনটি useful?**

A. `COALESCE()`  
B. `NULLIF()`  
C. `TRIM()`  
D. `UPPER()`

**5. SQL-এর IF/ELSE logic কোনটি?**

A. CASE WHEN  
B. SWITCH  
C. IF ELSE ONLY  
D. LOOP

**6. Extra spaces remove করতে কোন function?**

A. `CLEAN()`  
B. `TRIM()`  
C. `SPACE()`  
D. `REMOVE()`

**7. String lowercase করতে কোনটি?**

A. `LOWER()`  
B. `SMALL()`  
C. `DOWN()`  
D. `MIN()`

**8. Text replace করতে কোন function?**

A. `CHANGE()`  
B. `REPLACE()`  
C. `UPDATE_TEXT()`  
D. `SUB()`

**9. Email-এর `@`-এর আগের অংশ বের করতে MySQL-এ কোনটি useful?**

A. `SUBSTRING_INDEX()`  
B. `LEFT_ONLY()`  
C. `EMAIL_PART()`  
D. `SPLIT_TEXT()`

**10. `NULL` এবং empty string সম্পর্কে কোনটি সঠিক?**

A. একই  
B. NULL = 0  
C. NULL এবং `''` আলাদা  
D. NULL = `'NULL'`

---

## 🎯 আজকের Core Skill

Class 45 শেষ করার পর তোমার এই query pattern খুব ভালোভাবে জানা উচিত:

```sql
SELECT
    TRIM(name) AS clean_name,

    LOWER(TRIM(email)) AS clean_email,

    COALESCE(
        NULLIF(
            REPLACE(REPLACE(TRIM(phone), '-', ''), ' ', ''),
            ''
        ),
        'No Phone'
    ) AS clean_phone,

    CASE
        WHEN email IS NULL OR TRIM(email) = ''
            THEN 'Missing'
        ELSE 'Available'
    END AS email_status

FROM customers;
```

এখানে একসাথে ব্যবহার হচ্ছে:

**TRIM + LOWER + REPLACE + NULLIF + COALESCE + CASE**

এটাই আজকের সবচেয়ে practical SQL data-cleaning pattern।


----
# 📘 Class 46 — SQL Views

আজ থেকে আমরা SQL-এর **Database Object** এবং production-level database concepts-এর দিকে যাচ্ছি।

আজকের topic:

1. View কী?
    
2. কেন View ব্যবহার করি?
    
3. `CREATE VIEW`
    
4. View থেকে `SELECT`
    
5. View + JOIN
    
6. View + GROUP BY
    
7. View + WHERE
    
8. `CREATE OR REPLACE VIEW`
    
9. `DROP VIEW`
    
10. View vs Table
    
11. View vs CTE
    
12. Real-world reporting
    
13. Security-এর জন্য View
    
14. Common mistakes
    
15. Assignment + MCQ
    

---

# 1️⃣ View কী?

সহজভাবে:

> **View হলো একটি saved SQL query, যেটাকে আমরা table-এর মতো ব্যবহার করতে পারি।**

ধরো প্রতিবার তোমাকে এই query লিখতে হচ্ছে:

```sql
SELECT
    c.customer_id,
    c.customer_name,
    c.city,
    SUM(o.quantity * p.price) AS total_spending
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    c.customer_id,
    c.customer_name,
    c.city;
```

Query অনেক বড়।

আমরা এটাকে একটি View হিসেবে save করতে পারি।

---

# 2️⃣ CREATE VIEW

```sql
CREATE VIEW customer_sales AS
SELECT
    c.customer_id,
    c.customer_name,
    c.city,
    SUM(o.quantity * p.price) AS total_spending
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    c.customer_id,
    c.customer_name,
    c.city;
```

এখন `customer_sales` হলো একটি View।

---

# 3️⃣ View থেকে Data দেখা

এখন:

```sql
SELECT *
FROM customer_sales;
```

তুমি এমন result পাবে:

|customer_id|customer_name|city|total_spending|
|--:|---|---|--:|
|1|Rahim|Dhaka|89000|
|2|Karim|Chittagong|120000|
|3|Hasan|Dhaka|73000|

এখানে মনে হবে যেন `customer_sales` একটি table।

কিন্তু এটি **সাধারণ table নয়**।

---

# 4️⃣ View-এর মূল ধারণা

```text
Original Tables
      ↓
     JOIN
      ↓
   GROUP BY
      ↓
   SQL Query
      ↓
     VIEW
      ↓
SELECT / WHERE / ORDER BY
```

### Golden Rule ⭐

> **View = Saved SQL Query + Table-like interface**

---

# 5️⃣ View কেন ব্যবহার করব?

ধরো company-তে একই report বারবার লাগে:

```text
Customer Sales Report
```

প্রতিবার 20 লাইনের query না লিখে:

```sql
SELECT *
FROM customer_sales;
```

এটাই যথেষ্ট।

### Benefits

- Query reuse
    
- Complex query সহজ করা
    
- Reporting সহজ
    
- Security improve করা যায়
    
- Application code সহজ করা
    
- Consistent business logic
    

---

# 6️⃣ View + WHERE

View-এর উপর আবার filtering করা যায়।

```sql
SELECT *
FROM customer_sales
WHERE total_spending > 100000;
```

মানে:

> যেসব customer-এর total spending 100000-এর বেশি।

---

# 7️⃣ View + ORDER BY

```sql
SELECT *
FROM customer_sales
ORDER BY total_spending DESC;
```

সবচেয়ে বেশি spending করা customer উপরে আসবে।

---

# 8️⃣ View + LIMIT

```sql
SELECT *
FROM customer_sales
ORDER BY total_spending DESC
LIMIT 5;
```

Top 5 customers।

---

# 9️⃣ View + JOIN

View-কে অন্য table-এর সাথে JOIN করা যায়।

ধরো:

```sql
SELECT
    cs.customer_name,
    cs.total_spending,
    c.email
FROM customer_sales cs
JOIN customers c
    ON cs.customer_id = c.customer_id;
```

অর্থাৎ:

```text
View
 +
Table
 ↓
JOIN
```

---

# 🔟 Simple View

সব View complex হতে হবে এমন নয়।

```sql
CREATE VIEW active_customers AS
SELECT
    customer_id,
    customer_name,
    city
FROM customers
WHERE is_active = TRUE;
```

তারপর:

```sql
SELECT *
FROM active_customers;
```

---

# 1️⃣1️⃣ View + JOIN Example

ধরো sales report দরকার:

```sql
CREATE VIEW sales_report AS
SELECT
    o.order_id,
    o.order_date,
    c.customer_name,
    c.city,
    p.product_name,
    p.category,
    o.quantity,
    p.price,
    o.quantity * p.price AS total_amount
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id
JOIN products p
    ON o.product_id = p.product_id;
```

এখন:

```sql
SELECT *
FROM sales_report;
```

Result:

|order_id|customer|product|quantity|total_amount|
|--:|---|---|--:|--:|
|1|Rahim|Laptop|1|80000|
|2|Karim|Monitor|2|60000|

এখন এই View-কে আমরা reporting layer হিসেবে ব্যবহার করতে পারি।

---

# 1️⃣2️⃣ View থেকে Specific Columns

```sql
SELECT
    customer_name,
    product_name,
    total_amount
FROM sales_report;
```

View-এর সব column নিতে হবে না।

---

# 1️⃣3️⃣ View + WHERE

```sql
SELECT *
FROM sales_report
WHERE category = 'Electronics';
```

শুধু Electronics sales।

---

# 1️⃣4️⃣ View + Date Filter

```sql
SELECT *
FROM sales_report
WHERE order_date >= '2026-01-01'
  AND order_date < '2026-02-01';
```

January sales।

---

# 1️⃣5️⃣ View + Aggregate

ধরো `sales_report` আছে।

এখন category-wise sales:

```sql
SELECT
    category,
    SUM(total_amount) AS total_sales
FROM sales_report
GROUP BY category;
```

Result:

|category|total_sales|
|---|--:|
|Electronics|265000|
|Furniture|70000|
|Accessories|45000|

🔥 এখানে একটি interesting concept:

আমরা প্রথমে complex JOIN View বানিয়েছি।

তারপর View-এর উপর analytics করেছি।

---

# 1️⃣6️⃣ View দিয়ে Business Logic Centralize করা

ধরো company-এর rule:

```text
Revenue = Quantity × Price
```

যদি 5টা application একই calculation করে, তাহলে inconsistency হতে পারে।

View:

```sql
CREATE VIEW sales_report AS
SELECT
    order_id,
    quantity,
    price,
    quantity * price AS revenue
FROM orders;
```

এখন সবাই:

```sql
SELECT revenue
FROM sales_report;
```

ব্যবহার করতে পারে।

### Golden Rule

> **View business logic centralize করতে সাহায্য করে।**

---

# 1️⃣7️⃣ CREATE OR REPLACE VIEW

View-এর definition পরিবর্তন করতে:

```sql
CREATE OR REPLACE VIEW active_customers AS
SELECT
    customer_id,
    customer_name,
    city,
    email
FROM customers
WHERE is_active = TRUE;
```

আগের View থাকলে definition replace/update করা যায়।

---

# 1️⃣8️⃣ DROP VIEW

View আর দরকার না হলে:

```sql
DROP VIEW active_customers;
```

তারপর View থাকবে না।

---

# 1️⃣9️⃣ DROP VIEW IF EXISTS

Production script-এ safe approach:

```sql
DROP VIEW IF EXISTS active_customers;
```

View না থাকলেও unnecessary error এড়ানো যায়।

---

# 2️⃣0️⃣ View vs Table

এটা interview-এর জন্য খুব important।

|Feature|Table|View|
|---|---|---|
|Physical table|✅|সাধারণত ❌|
|Data store করে|✅|সাধারণত query result represent করে|
|`CREATE TABLE`|✅|❌|
|`CREATE VIEW`|❌|✅|
|Complex query save|❌|✅|
|JOIN-based report|Possible|Very useful|
|Direct data storage|✅|❌|
|Query reuse|Limited|✅|

সহজভাবে:

> **Table = Data রাখে**

> **View = Query-এর result-এর interface দেয়**

---

# 2️⃣1️⃣ View কি Data Copy করে?

সাধারণ View-এর ক্ষেত্রে:

**না।**

যেমন:

```sql
CREATE VIEW active_customers AS
SELECT *
FROM customers
WHERE is_active = TRUE;
```

এটা সাধারণত customer data-এর নতুন physical copy তৈরি করে না।

View-এর underlying query থেকে data আসে।

তাই original table update হলে View-তে নতুন data দেখা যেতে পারে।

---

# 2️⃣2️⃣ Example

প্রথমে:

```text
customers

Rahim → Active
Karim → Active
Hasan → Inactive
```

View:

```sql
CREATE VIEW active_customers AS
SELECT *
FROM customers
WHERE is_active = TRUE;
```

Result:

```text
Rahim
Karim
```

পরে Hasan active হলে:

```sql
UPDATE customers
SET is_active = TRUE
WHERE customer_id = 3;
```

তারপর:

```sql
SELECT *
FROM active_customers;
```

Hasan-ও দেখা যাবে।

অর্থাৎ View সাধারণত current underlying data-এর উপর query করে।

---

# 2️⃣3️⃣ View vs CTE

এটা খুব গুরুত্বপূর্ণ কারণ তুমি Class 38-এ CTE শিখেছো।

### CTE

```sql
WITH customer_sales AS (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
)
SELECT *
FROM customer_sales;
```

CTE সাধারণত **একটি query-এর জন্য**।

---

### View

```sql
CREATE VIEW customer_sales AS
SELECT
    customer_id,
    SUM(amount) AS total_sales
FROM orders
GROUP BY customer_id;
```

তারপর অনেক query-তে ব্যবহার করা যায়:

```sql
SELECT * FROM customer_sales;
```

```sql
SELECT *
FROM customer_sales
WHERE total_sales > 100000;
```

```sql
SELECT *
FROM customer_sales
ORDER BY total_sales DESC;
```

### Golden Rule ⭐

> **CTE = Temporary query-level result**

> **View = Saved database-level query object**

---

# 2️⃣4️⃣ View vs Subquery

Subquery:

```sql
SELECT *
FROM (
    SELECT
        customer_id,
        SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
) AS x
WHERE total_sales > 100000;
```

এখানে query-এর মধ্যেই subquery আছে।

View:

```sql
CREATE VIEW customer_sales AS
SELECT
    customer_id,
    SUM(amount) AS total_sales
FROM orders
GROUP BY customer_id;
```

তারপর:

```sql
SELECT *
FROM customer_sales
WHERE total_sales > 100000;
```

### মনে রাখো:

```text
Subquery → one query-এর ভিতরে
CTE      → one query-এর শুরুতে
View     → database-এ saved query
```

---

# 2️⃣5️⃣ Security-এর জন্য View

এটা Database Designer হিসেবে তোমার জন্য খুব important।

ধরো employees table:

```text
employee_id
name
email
salary
department
nid
address
```

HR application-এর সাধারণ employee user-কে salary/NID দেখাতে চাই না।

তাহলে:

```sql
CREATE VIEW employee_public AS
SELECT
    employee_id,
    name,
    email,
    department
FROM employees;
```

Application:

```sql
SELECT *
FROM employee_public;
```

এতে sensitive columns expose না করেই data access করা যায়।

### Important

View security-এর জন্য useful হলেও **View একাই complete security system নয়**।

Proper permissions/privileges-ও দরকার।

---

# 2️⃣6️⃣ Real-World Architecture

Production application-এ conceptually:

```text
             Database Tables
                    ↓
              JOIN / Logic
                    ↓
                  VIEW
                    ↓
           Reporting / API Layer
                    ↓
             Frontend / Dashboard
```

যেমন:

```text
customers
products
orders
    ↓
sales_report VIEW
    ↓
Django / DRF
    ↓
React / Power BI
```

তোমার Django + DRF background-এর সাথে এই concept খুব useful।

---

# 2️⃣7️⃣ View + Window Function

Advanced example:

```sql
CREATE VIEW customer_ranking AS
SELECT
    customer_id,
    customer_name,
    total_spending,
    RANK() OVER (
        ORDER BY total_spending DESC
    ) AS customer_rank
FROM customer_sales;
```

এখন:

```sql
SELECT *
FROM customer_ranking
WHERE customer_rank <= 3;
```

Top 3 customers।

🔥 এখানে আমরা ব্যবহার করছি:

```text
View
+
Window Function
```

---

# 2️⃣8️⃣ View + CASE

```sql
CREATE VIEW customer_segment AS
SELECT
    customer_id,
    customer_name,
    total_spending,
    CASE
        WHEN total_spending >= 100000
            THEN 'Premium'
        WHEN total_spending >= 50000
            THEN 'Regular'
        ELSE 'Low'
    END AS segment
FROM customer_sales;
```

তারপর:

```sql
SELECT *
FROM customer_segment
WHERE segment = 'Premium';
```

---

# 2️⃣9️⃣ View-এর Limitation

View সবসময় magic solution নয়।

### কিছু limitation:

- Complex View performance-heavy হতে পারে
    
- অনেক JOIN থাকলে query expensive হতে পারে
    
- সব View সহজে update করা যায় না
    
- Nested Views complexity তৈরি করতে পারে
    
- Underlying table structure পরিবর্তন করলে View break করতে পারে
    

---

# 3️⃣0️⃣ Updatable View

কিছু simple View-এর মাধ্যমে underlying table update করা সম্ভব হতে পারে।

Example:

```sql
CREATE VIEW active_customers AS
SELECT
    customer_id,
    customer_name,
    city
FROM customers
WHERE is_active = TRUE;
```

কিছু DBMS পরিস্থিতিতে:

```sql
UPDATE active_customers
SET city = 'Dhaka'
WHERE customer_id = 1;
```

underlying `customers` table-এ change করতে পারে।

কিন্তু complex View—বিশেষ করে:

```text
GROUP BY
Aggregate
DISTINCT
UNION
Multiple complex JOIN
```

থাকলে updateability সীমিত বা unavailable হতে পারে।

### Beginner Rule

> **View primarily reporting/read abstraction হিসেবে ব্যবহার করো; update করার আগে DBMS-specific rules বুঝবে।**

---

# 3️⃣1️⃣ Materialized View — ধারণা

Normal View:

```text
Query definition saved
        ↓
Data usually calculated when queried
```

Materialized View:

```text
Query result physically stored
        ↓
Faster reads
        ↓
Needs refresh
```

এটা large analytics system-এ useful হতে পারে।

তবে MySQL/PostgreSQL implementation details আলাদা।

এখন শুধু concept মনে রাখো।

---

# 3️⃣2️⃣ Normal View vs Materialized View

||View|Materialized View|
|---|---|---|
|Query definition|Save|Save|
|Result physically store|সাধারণত না|হ্যাঁ|
|Freshness|সাধারণত current underlying data|Refresh-এর উপর নির্ভর|
|Read performance|Query-dependent|Often faster|
|Storage|কম|বেশি|
|Analytics|✅|✅|

---

# 3️⃣3️⃣ Real-World Sales View

এবার পুরো একটি practical example:

```sql
CREATE VIEW sales_report AS
SELECT
    o.order_id,
    o.order_date,

    c.customer_id,
    c.customer_name,
    c.city,

    p.product_id,
    p.product_name,
    p.category,

    o.quantity,
    p.price,

    o.quantity * p.price AS revenue

FROM orders o

JOIN customers c
    ON o.customer_id = c.customer_id

JOIN products p
    ON o.product_id = p.product_id;
```

এখন business analyst:

```sql
SELECT *
FROM sales_report;
```

Monthly sales:

```sql
SELECT
    DATE_FORMAT(order_date, '%Y-%m') AS month,
    SUM(revenue) AS monthly_sales
FROM sales_report
GROUP BY DATE_FORMAT(order_date, '%Y-%m')
ORDER BY month;
```

Category sales:

```sql
SELECT
    category,
    SUM(revenue) AS total_sales
FROM sales_report
GROUP BY category
ORDER BY total_sales DESC;
```

Top customers:

```sql
SELECT
    customer_name,
    SUM(revenue) AS total_spending
FROM sales_report
GROUP BY customer_id, customer_name
ORDER BY total_spending DESC
LIMIT 5;
```

🔥 একটি View থেকে অনেক ধরনের report তৈরি করা যাচ্ছে।

---

# 3️⃣4️⃣ Common Beginner Mistakes

### ❌ Mistake 1: View-কে physical table মনে করা

View সাধারণত data-এর নতুন copy নয়।

---

### ❌ Mistake 2: View এবং CTE একই মনে করা

```text
CTE → query-level
View → database-level saved object
```

---

### ❌ Mistake 3: View বানালেই performance সবসময় বাড়বে

না।

View complex হলে underlying query আবার expensive হতে পারে।

---

### ❌ Mistake 4: Security সম্পূর্ণ View-এর উপর ছেড়ে দেওয়া

View data exposure কমাতে সাহায্য করতে পারে, কিন্তু database permissions-ও দরকার।

---

### ❌ Mistake 5: সব query-এর জন্য View বানানো

একবার ব্যবহার করা ছোট query-এর জন্য View বানানোর দরকার নেই।

Repeated / reusable / reporting logic-এর জন্য View বেশি useful।

---

# 🧠 Class 46 Cheat Sheet

```text
CREATE VIEW
    ↓
Saved SQL Query

SELECT FROM view
    ↓
View ব্যবহার

CREATE OR REPLACE VIEW
    ↓
View definition update

DROP VIEW
    ↓
View delete

View
    ↓
Reusable query

CTE
    ↓
Temporary query-level result

Table
    ↓
Actual stored data

Materialized View
    ↓
Stored query result
```

### ⭐ Golden Rules

> **Table = Data**

> **View = Saved Query**

> **CTE = Temporary Query Result**

> **Materialized View = Stored Query Result**

---

# 📝 Class 46 Assignment

ধরো tables:

```text
customers
products
orders
```

### Q1

একটি `active_customers` View তৈরি করো।

### Q2

একটি `sales_report` View তৈরি করো যেখানে থাকবে:

```text
order_id
order_date
customer_name
city
product_name
category
quantity
price
revenue
```

### Q3

`sales_report` View থেকে category-wise sales বের করো।

### Q4

`sales_report` View থেকে monthly sales বের করো।

### Q5

`sales_report` View থেকে top 5 customers বের করো।

### Q6

একটি `customer_sales` View তৈরি করো যেখানে থাকবে:

```text
customer_id
customer_name
total_spending
```

### Q7

এই View থেকে `total_spending > 100000` customer বের করো।

### Q8

Customer ranking-এর জন্য View তৈরি করো যেখানে `RANK()` থাকবে।

### Q9

`employee_public` View তৈরি করো যেখানে salary এবং sensitive fields থাকবে না।

### Q10 ⭐

নিজের ভাষায় explain করো:

```text
Table vs View vs CTE
```

---

# 🧪 Class 46 MCQ

**1. View কী?**

A. Physical storage only  
B. Saved SQL query  
C. Index  
D. Database

**2. View তৈরি করতে কোন command?**

A. `CREATE TABLE`  
B. `CREATE QUERY`  
C. `CREATE VIEW`  
D. `MAKE VIEW`

**3. View থেকে data নিতে?**

A. `SELECT FROM view`  
B. `GET VIEW`  
C. `READ VIEW`  
D. `OPEN VIEW`

**4. CTE-এর তুলনায় View-এর প্রধান সুবিধা কী?**

A. Query-এর মধ্যে শুধু একবার ব্যবহার করা যায়  
B. Database-এ reusable object হিসেবে থাকে  
C. সব data copy করে  
D. Index তৈরি করে

**5. View-এর underlying table update হলে সাধারণ View-তে কী দেখা যেতে পারে?**

A. নতুন data reflect হতে পারে  
B. সব data delete হবে  
C. View automatically table হবে  
D. Database বন্ধ হবে

**6. View security-তে কীভাবে সাহায্য করতে পারে?**

A. Password generate করে  
B. নির্দিষ্ট columns expose করে  
C. Database encrypt করে  
D. Backup তৈরি করে

**7. View delete করতে?**

A. `DELETE VIEW`  
B. `DROP VIEW`  
C. `REMOVE VIEW`  
D. `CLEAR VIEW`

**8. Materialized View-এর বৈশিষ্ট্য কী?**

A. Result physically store করতে পারে  
B. কখনো refresh লাগে না  
C. সবসময় faster  
D. Table-এর synonym

**9. View কি সবসময় performance improve করে?**

A. হ্যাঁ  
B. না  
C. শুধু JOIN থাকলে  
D. শুধু MySQL-এ

**10. কোনটি সঠিক?**

A. Table = Saved Query  
B. View = Physical Data Storage  
C. CTE = Query-level temporary result  
D. View = Index

---

## 🎯 আজকের মূল concept

```text
TABLE
  ↓
Actual Data

CTE
  ↓
Temporary Query Result

VIEW
  ↓
Reusable Saved Query

MATERIALIZED VIEW
  ↓
Stored Query Result
```

**পরের ধাপ: Class 47 — Stored Procedures & Functions**, যেখানে আমরা শিখব database-এর ভিতরে reusable logic কীভাবে তৈরি করা হয়, `CREATE PROCEDURE`, parameters, `CALL`, functions, `IF`, variables এবং real-world business logic।

----
# 📘 Class 47 — SQL Stored Procedures & Functions

আজকে আমরা SQL-এর **Reusable Database Logic** শিখব।

এখন পর্যন্ত তুমি শিখেছো:

```text
SELECT
WHERE
GROUP BY
JOIN
Subquery
CTE
Window Function
EXISTS
Date Analytics
NULL Handling
View
```

এখন আমরা শিখব:

> **Database-এর ভিতরেই reusable logic কীভাবে তৈরি করা যায়।**

আজকের topics:

1. Stored Procedure কী?
    
2. Procedure কেন ব্যবহার করি?
    
3. `CREATE PROCEDURE`
    
4. `CALL`
    
5. Parameters
    
6. `IN`, `OUT`, `INOUT`
    
7. Variables
    
8. `IF`
    
9. Procedure + SELECT
    
10. Procedure + UPDATE
    
11. Stored Function
    
12. Procedure vs Function
    
13. Real-world examples
    
14. Common mistakes
    
15. Assignment + MCQ
    

---

# 1️⃣ Stored Procedure কী?

সহজভাবে:

> **Stored Procedure হলো database-এর ভিতরে save করা এক বা একাধিক SQL statement-এর reusable group।**

ধরো তুমি বারবার এই কাজ করো:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

এটা একটি procedure হিসেবে save করা যায়।

তারপর:

```sql
CALL get_it_employees();
```

করলেই query execute হবে।

---

# 2️⃣ Procedure কেন ব্যবহার করব?

ধরো একটি banking/application system-এ:

```text
Transfer Money
    ↓
Check balance
    ↓
Deduct money
    ↓
Add money
    ↓
Record transaction
```

এই ধরনের multiple SQL operation database-এর একটি procedure-এর মধ্যে রাখা যেতে পারে।

Benefits:

- Logic reuse
    
- Centralized business logic
    
- Application code কমানো
    
- Database-side processing
    
- Parameters ব্যবহার
    
- Multiple SQL statements একসাথে execute করা
    

---

# 3️⃣ Basic Stored Procedure

MySQL example:

```sql
DELIMITER //

CREATE PROCEDURE get_employees()
BEGIN
    SELECT *
    FROM employees;
END //

DELIMITER ;
```

এখানে:

```text
CREATE PROCEDURE
        ↓
Procedure তৈরি
```

এবং:

```sql
BEGIN
...
END
```

এর মধ্যে procedure-এর statements থাকে।

---

# 4️⃣ DELIMITER কেন?

Normally MySQL:

```sql
;
```

দেখলেই statement শেষ মনে করে।

কিন্তু procedure-এর ভিতরে অনেকগুলো statement থাকতে পারে।

তাই আমরা temporarily delimiter পরিবর্তন করি:

```sql
DELIMITER //
```

তারপর:

```sql
END //
```

শেষে আবার:

```sql
DELIMITER ;
```

### মনে রাখবে

> `DELIMITER` SQL logic-এর অংশ নয়; MySQL client-কে statement boundary বোঝাতে ব্যবহৃত হয়।

---

# 5️⃣ Procedure Execute করা

Procedure তৈরি করার পর:

```sql
CALL get_employees();
```

এতে:

```sql
SELECT *
FROM employees;
```

execute হবে।

---

# 6️⃣ Procedure with WHERE

```sql
DELIMITER //

CREATE PROCEDURE get_it_employees()
BEGIN
    SELECT *
    FROM employees
    WHERE department = 'IT';
END //

DELIMITER ;
```

Run:

```sql
CALL get_it_employees();
```

---

# 7️⃣ Parameter কী?

Procedure-কে বাইরে থেকে value পাঠাতে চাইলে parameter ব্যবহার করি।

যেমন:

```text
department = 'IT'
```

hardcode না করে user যেন department পাঠাতে পারে।

---

# 8️⃣ IN Parameter

সবচেয়ে common parameter:

```sql
IN
```

Example:

```sql
DELIMITER //

CREATE PROCEDURE get_employees_by_department(
    IN dept_name VARCHAR(50)
)
BEGIN
    SELECT *
    FROM employees
    WHERE department = dept_name;
END //

DELIMITER ;
```

এখন:

```sql
CALL get_employees_by_department('IT');
```

অথবা:

```sql
CALL get_employees_by_department('HR');
```

একই procedure, different input।

---

# 9️⃣ Procedure Flow

```text
CALL procedure('IT')
       ↓
dept_name = 'IT'
       ↓
SELECT employees
WHERE department = 'IT'
       ↓
Result
```

---

# 🔟 Multiple Parameters

ধরো city এবং minimum salary দুটোই দিতে চাই।

```sql
DELIMITER //

CREATE PROCEDURE search_employees(
    IN emp_city VARCHAR(50),
    IN min_salary DECIMAL(10,2)
)
BEGIN
    SELECT *
    FROM employees
    WHERE city = emp_city
      AND salary >= min_salary;
END //

DELIMITER ;
```

Call:

```sql
CALL search_employees('Dhaka', 50000);
```

---

# 1️⃣1️⃣ Procedure + Date

```sql
DELIMITER //

CREATE PROCEDURE get_orders_after(
    IN start_date DATE
)
BEGIN
    SELECT *
    FROM orders
    WHERE order_date >= start_date;
END //

DELIMITER ;
```

Call:

```sql
CALL get_orders_after('2026-03-01');
```

---

# 1️⃣2️⃣ Procedure + UPDATE

Procedure শুধু SELECT-এর জন্য নয়।

Employee salary increase:

```sql
DELIMITER //

CREATE PROCEDURE increase_salary(
    IN dept_name VARCHAR(50),
    IN increase_percent DECIMAL(5,2)
)
BEGIN
    UPDATE employees
    SET salary = salary * (1 + increase_percent / 100)
    WHERE department = dept_name;
END //

DELIMITER ;
```

Call:

```sql
CALL increase_salary('IT', 10);
```

IT department-এর salary 10% increase হবে।

---

# 1️⃣3️⃣ Procedure + INSERT

নতুন customer insert:

```sql
DELIMITER //

CREATE PROCEDURE add_customer(
    IN p_name VARCHAR(100),
    IN p_city VARCHAR(50)
)
BEGIN
    INSERT INTO customers(customer_name, city)
    VALUES(p_name, p_city);
END //

DELIMITER ;
```

Call:

```sql
CALL add_customer('Rahim', 'Dhaka');
```

---

# 1️⃣4️⃣ Procedure + DELETE

```sql
DELIMITER //

CREATE PROCEDURE delete_customer(
    IN p_customer_id INT
)
BEGIN
    DELETE FROM customers
    WHERE customer_id = p_customer_id;
END //

DELIMITER ;
```

Call:

```sql
CALL delete_customer(5);
```

⚠️ Production system-এ delete করার আগে foreign key এবং business rules carefully handle করতে হবে।

---

# 1️⃣5️⃣ Variable

Procedure-এর ভিতরে local variable তৈরি করা যায়।

Syntax:

```sql
DECLARE variable_name data_type;
```

Example:

```sql
DELIMITER //

CREATE PROCEDURE test_variable()
BEGIN
    DECLARE total INT DEFAULT 0;

    SET total = 100;

    SELECT total;
END //

DELIMITER ;
```

Call:

```sql
CALL test_variable();
```

Result:

```text
100
```

---

# 1️⃣6️⃣ Variable + SELECT INTO

Database থেকে value এনে variable-এ রাখা যায়।

```sql
DELIMITER //

CREATE PROCEDURE get_employee_count()
BEGIN
    DECLARE total_employees INT;

    SELECT COUNT(*)
    INTO total_employees
    FROM employees;

    SELECT total_employees AS employee_count;
END //

DELIMITER ;
```

Call:

```sql
CALL get_employee_count();
```

---

# 1️⃣7️⃣ IF Statement

Procedure-এর ভিতরে condition ব্যবহার করা যায়।

```sql
DELIMITER //

CREATE PROCEDURE check_salary(
    IN emp_salary DECIMAL(10,2)
)
BEGIN
    IF emp_salary >= 50000 THEN
        SELECT 'Good Salary' AS result;
    ELSE
        SELECT 'Below Target' AS result;
    END IF;
END //

DELIMITER ;
```

Call:

```sql
CALL check_salary(60000);
```

Result:

```text
Good Salary
```

---

# 1️⃣8️⃣ IF / ELSEIF / ELSE

```sql
DELIMITER //

CREATE PROCEDURE salary_level(
    IN emp_salary DECIMAL(10,2)
)
BEGIN
    IF emp_salary >= 80000 THEN
        SELECT 'High' AS level;

    ELSEIF emp_salary >= 50000 THEN
        SELECT 'Medium' AS level;

    ELSE
        SELECT 'Low' AS level;
    END IF;
END //

DELIMITER ;
```

এখানে:

```text
>= 80000 → High
>= 50000 → Medium
< 50000  → Low
```

---

# 1️⃣9️⃣ IN vs OUT vs INOUT

Stored Procedure-এর parameters তিন ধরনের হতে পারে:

```text
IN
OUT
INOUT
```

---

## `IN`

Input নেওয়ার জন্য।

```sql
IN p_id INT
```

---

## `OUT`

Procedure থেকে result বাইরে পাঠাতে।

```sql
OUT total INT
```

---

## `INOUT`

Input নেয় এবং পরিবর্তিত value output করতে পারে।

```sql
INOUT value INT
```

---

# 2️⃣0️⃣ OUT Parameter Example

Employee count:

```sql
DELIMITER //

CREATE PROCEDURE get_employee_count(
    OUT total_employees INT
)
BEGIN
    SELECT COUNT(*)
    INTO total_employees
    FROM employees;
END //

DELIMITER ;
```

Call:

```sql
CALL get_employee_count(@total);
```

তারপর:

```sql
SELECT @total;
```

Result:

```text
15
```

এখানে:

```text
@total
```

একটি MySQL session variable।

---

# 2️⃣1️⃣ OUT Parameter Flow

```text
CALL procedure
      ↓
Database calculates
      ↓
OUT parameter
      ↓
@total
      ↓
SELECT @total
```

---

# 2️⃣2️⃣ INOUT Example

ধরো input:

```text
100
```

Procedure 10 add করবে।

```sql
DELIMITER //

CREATE PROCEDURE add_ten(
    INOUT value INT
)
BEGIN
    SET value = value + 10;
END //

DELIMITER ;
```

Call:

```sql
SET @number = 100;

CALL add_ten(@number);

SELECT @number;
```

Result:

```text
110
```

---

# 2️⃣3️⃣ Stored Function কী?

এখন আসি **Function**-এ।

> **Stored Function হলো database-এর ভিতরে save করা reusable logic যা একটি value return করে।**

Procedure:

```text
CALL procedure()
```

Function:

```text
SELECT function()
```

---

# 2️⃣4️⃣ Simple Function

ধরো Celsius → Fahrenheit:

```sql
DELIMITER //

CREATE FUNCTION celsius_to_fahrenheit(
    celsius DECIMAL(10,2)
)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN (celsius * 9 / 5) + 32;
END //

DELIMITER ;
```

Use:

```sql
SELECT celsius_to_fahrenheit(30);
```

Result:

```text
86
```

---

# 2️⃣5️⃣ Function in SELECT

Employee salary bonus:

```sql
SELECT
    name,
    salary,
    salary * 0.10 AS bonus
FROM employees;
```

এটা সরাসরি query-তে করা যায়।

কিন্তু reusable complex logic হলে function ব্যবহার করা যেতে পারে।

---

# 2️⃣6️⃣ Custom Function Example

```sql
DELIMITER //

CREATE FUNCTION salary_with_bonus(
    salary DECIMAL(10,2),
    bonus_percent DECIMAL(5,2)
)
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    RETURN salary + (salary * bonus_percent / 100);
END //

DELIMITER ;
```

Use:

```sql
SELECT
    name,
    salary,
    salary_with_bonus(salary, 10) AS final_salary
FROM employees;
```

---

# 2️⃣7️⃣ Procedure vs Function

Interview-এর জন্য খুব important।

|Feature|Procedure|Function|
|---|---|---|
|`CALL`|✅|❌|
|`SELECT`-এ directly|সাধারণত ❌|✅|
|Return value|একাধিক OUT/result হতে পারে|একটি return value|
|Main purpose|Perform operation|Calculate/return value|
|INSERT/UPDATE/DELETE|✅|Function restrictions apply|
|Parameters|IN/OUT/INOUT|সাধারণত input parameters|

### সহজভাবে:

> **Procedure = কাজ করো**

> **Function = value return করো**

---

# 2️⃣8️⃣ Real-World Example

ধরো e-commerce system।

### Procedure:

```text
Place Order
    ↓
Create Order
    ↓
Reduce Inventory
    ↓
Create Payment Record
    ↓
Create Order History
```

এখানে Procedure useful।

### Function:

```text
Calculate Discount
Calculate Tax
Calculate Final Price
Calculate Customer Score
```

এখানে Function useful।

---

# 2️⃣9️⃣ Procedure + Business Logic

ধরো customer-এর total spending:

```sql
DELIMITER //

CREATE PROCEDURE get_customer_spending(
    IN p_customer_id INT
)
BEGIN
    SELECT
        c.customer_id,
        c.customer_name,
        COALESCE(SUM(o.amount), 0) AS total_spending
    FROM customers c
    LEFT JOIN orders o
        ON c.customer_id = o.customer_id
    WHERE c.customer_id = p_customer_id
    GROUP BY
        c.customer_id,
        c.customer_name;
END //

DELIMITER ;
```

Call:

```sql
CALL get_customer_spending(1);
```

---

# 3️⃣0️⃣ Procedure + CASE

```sql
DELIMITER //

CREATE PROCEDURE customer_segment(
    IN p_customer_id INT
)
BEGIN
    DECLARE total_spending DECIMAL(12,2);

    SELECT
        COALESCE(SUM(amount), 0)
    INTO total_spending
    FROM orders
    WHERE customer_id = p_customer_id;

    IF total_spending >= 100000 THEN
        SELECT 'Premium' AS segment;

    ELSEIF total_spending >= 50000 THEN
        SELECT 'Regular' AS segment;

    ELSE
        SELECT 'Basic' AS segment;
    END IF;
END //

DELIMITER ;
```

এখানে একসাথে:

```text
Procedure
+
Variable
+
SELECT INTO
+
COALESCE
+
IF
```

🔥 এটি production-style database logic-এর foundation।

---

# 3️⃣1️⃣ Procedure vs View

তুমি Class 46-এ View শিখেছো।

### View:

```text
Saved Query
↓
Mostly data reading/reporting
```

### Procedure:

```text
Saved SQL Logic
↓
Can perform operations
```

Example:

```text
View
→ Customer Sales Report

Procedure
→ Increase Customer Credit
```

---

# 3️⃣2️⃣ Procedure vs CTE

```text
CTE
→ Temporary query structure

View
→ Saved query

Procedure
→ Saved executable logic

Function
→ Saved calculation returning value
```

এটা চারটা concept একসাথে মনে রাখো।

---

# 3️⃣3️⃣ Common Beginner Mistakes

### ❌ Mistake 1 — `DELIMITER` ভুলে যাওয়া

MySQL client-এ multi-statement procedure তৈরি করার সময় delimiter ঠিকভাবে manage করতে হবে।

---

### ❌ Mistake 2 — Parameter name conflict

যেমন:

```sql
WHERE department = department;
```

এতে ambiguity হতে পারে।

Better:

```sql
WHERE department = p_department;
```

Naming convention:

```text
p_ → parameter
v_ → local variable
```

যেমন:

```text
p_customer_id
p_salary
v_total
```

---

### ❌ Mistake 3 — Procedure আর Function একই মনে করা

মনে রাখো:

```text
Procedure → CALL
Function  → RETURN
```

---

### ❌ Mistake 4 — সব business logic database-এ রাখা

Application এবং database-এর responsibility carefully design করতে হবে।

সব logic Stored Procedure-এ ঢুকিয়ে দিলে application architecture unnecessarily complex হতে পারে।

---

# 🧠 Class 47 Golden Cheat Sheet

```text
CREATE PROCEDURE
    ↓
Reusable SQL operation

CALL
    ↓
Procedure execute

IN
    ↓
Input

OUT
    ↓
Output

INOUT
    ↓
Input + Output

DECLARE
    ↓
Local variable

SET
    ↓
Variable value set

SELECT ... INTO
    ↓
Query result → variable

IF / ELSEIF / ELSE
    ↓
Conditional logic

CREATE FUNCTION
    ↓
Reusable calculation

RETURN
    ↓
Function result
```

### সবচেয়ে গুরুত্বপূর্ণ:

> **Procedure = Perform an operation**

> **Function = Return a value**

> **View = Saved query**

> **CTE = Temporary query result**

---

# 📝 Class 47 Assignment

ধরো তোমার `employees` table:

```text
employee_id
name
department
salary
city
```

এবং `orders`:

```text
order_id
customer_id
order_date
amount
```

### Q1

একটি procedure তৈরি করো যেটা সব employees দেখাবে।

### Q2

একটি procedure তৈরি করো যেটা `department` parameter নিয়ে employees দেখাবে।

### Q3

`city` এবং `minimum_salary` parameter নিয়ে employee search procedure তৈরি করো।

### Q4

একটি procedure তৈরি করো যেটা একটি department-এর salary 10% increase করবে।

### Q5

একটি procedure তৈরি করো যেটা customer ID নিয়ে তার সব orders দেখাবে।

### Q6

একটি procedure তৈরি করো যেটা customer ID নিয়ে total order amount বের করবে।

### Q7

`OUT` parameter ব্যবহার করে total employee count return করো।

### Q8

একটি function তৈরি করো:

```text
salary + 10% bonus
```

### Q9

একটি function তৈরি করো যা salary থেকে level return করবে:

```text
>= 80000 → High
>= 50000 → Medium
< 50000 → Low
```

### Q10 ⭐

নিজের ভাষায় explain করো:

```text
Procedure
Function
View
CTE
```

কখন কোনটি ব্যবহার করবে?

---

# 🧪 Class 47 MCQ

**1. Stored Procedure কী?**

A. Temporary table  
B. Saved executable SQL logic  
C. Index  
D. Database

**2. Procedure execute করতে কোন command?**

A. `RUN`  
B. `EXECUTE ONLY`  
C. `CALL`  
D. `START`

**3. `IN` parameter কী?**

A. Output  
B. Input  
C. Table  
D. Variable only

**4. `OUT` parameter কী করে?**

A. Input দেয়  
B. Result বাইরে দেয়  
C. Table তৈরি করে  
D. Query delete করে

**5. Local variable declare করতে?**

A. `DECLARE`  
B. `DEFINE ONLY`  
C. `VAR`  
D. `CREATE VARIABLE`

**6. Function-এর প্রধান বৈশিষ্ট্য কী?**

A. একটি value return করে  
B. Table delete করে  
C. Database তৈরি করে  
D. শুধু SELECT করে

**7. Function result ফেরত দিতে কোন keyword?**

A. `OUTPUT`  
B. `RETURN`  
C. `SEND`  
D. `RESULT`

**8. কোনটি বেশি সঠিক?**

A. Procedure = calculation only  
B. Function = operation only  
C. Procedure = operation, Function = return value  
D. দুটো সম্পূর্ণ একই

**9. MySQL procedure-এ `BEGIN ... END` কেন ব্যবহার করি?**

A. Multiple statements group করতে  
B. Table create করতে  
C. Index করতে  
D. Database delete করতে

**10. `DELIMITER` মূলত কী সাহায্য করে?**

A. Data type change  
B. Statement boundary manage  
C. Index create  
D. NULL remove

---

## 🎯 আজকের পুরো SQL Object Map

```text
                    SQL
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
       CTE          VIEW       PROCEDURE
        │            │            │
 temporary       saved query   executable
 query result                   logic
                                   │
                                   ↓
                               FUNCTION
                                   │
                              return value
```

আর Database Designer হিসেবে এই distinction খুব ভালোভাবে মাথায় রাখো:

```text
TABLE
→ Data

VIEW
→ Reusable Query

CTE
→ Temporary Query Structure

PROCEDURE
→ Reusable Operation

FUNCTION
→ Reusable Calculation
```

**Next: Class 48 — SQL Transactions + ACID + `COMMIT`, `ROLLBACK`, `SAVEPOINT`**। এটা তোমার DBMS preparation-এর সাথেও সরাসরি connect করবে এবং banking/e-commerce-এর মতো systems কীভাবে safe database operations করে সেটা বুঝতে সাহায্য করবে।

----
# 📘 Class 48 — SQL Transactions & ACID

আজকের classটা **খুবই important**—বিশেষ করে তুমি যেহেতু **Database Designer** হতে চাও।

আজ আমরা শিখব:

1. Transaction কী?
    
2. কেন Transaction দরকার?
    
3. `COMMIT`
    
4. `ROLLBACK`
    
5. `SAVEPOINT`
    
6. ACID Properties
    
7. Atomicity
    
8. Consistency
    
9. Isolation
    
10. Durability
    
11. Banking example
    
12. E-commerce example
    
13. Transaction-এর common mistakes
    
14. Practice + MCQ
    

---

# 1️⃣ Transaction কী?

সহজ ভাষায়:

> **Transaction হলো database-এর এক বা একাধিক operation-এর এমন একটি logical unit, যেটা সম্পূর্ণ সফল হবে অথবা পুরোপুরি বাতিল হবে।**

ধরো:

**Rahim → Karim = ৳1000 transfer**

এখানে দুইটি operation:

```text
1. Rahim-এর account থেকে 1000 কমানো
2. Karim-এর account-এ 1000 যোগ করা
```

দুটো operation একসাথে সফল হওয়া দরকার।

যদি:

```text
Rahim -1000 ✅
Karim +1000 ❌
```

হয়, তাহলে database-এর data ভুল হয়ে যাবে।

তাই transaction ব্যবহার করি।

---

# 2️⃣ Transaction-এর Basic Flow

```text
BEGIN TRANSACTION
       ↓
Operation 1
       ↓
Operation 2
       ↓
সব ঠিক?
   ↙       ↘
 YES       NO
  ↓         ↓
COMMIT    ROLLBACK
  ↓         ↓
Save      Undo
```

এটাই আজকের সবচেয়ে important flow।

---

# 3️⃣ Transaction শুরু করা

MySQL-এ:

```sql
START TRANSACTION;
```

অথবা:

```sql
BEGIN;
```

তারপর SQL statements।

---

# 4️⃣ COMMIT কী?

`COMMIT` মানে:

> **Transaction-এর changes permanently save করো।**

Example:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

এখানে `COMMIT` করার পরে changes save হয়ে যাবে।

---

# 5️⃣ ROLLBACK কী?

`ROLLBACK` মানে:

> **Transaction-এর uncommitted changes বাতিল করে আগের অবস্থায় ফিরে যাও।**

Example:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

ROLLBACK;
```

Result:

```text
আগের balance ফিরে আসবে।
```

---

# 6️⃣ COMMIT vs ROLLBACK

|Command|কাজ|
|---|---|
|`START TRANSACTION`|Transaction শুরু|
|`COMMIT`|Changes permanently save|
|`ROLLBACK`|Uncommitted changes undo|
|`SAVEPOINT`|Transaction-এর ভিতরে checkpoint|

সহজভাবে:

```text
COMMIT   → Save
ROLLBACK → Undo
```

---

# 7️⃣ Banking Example

ধরো:

```text
Account A = 10,000
Account B = 5,000
```

A থেকে B-তে 2,000 transfer।

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 2000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 2000
WHERE account_id = 2;

COMMIT;
```

Final:

```text
A = 8,000
B = 7,000
```

Total:

```text
10,000 + 5,000 = 15,000
```

এখন transaction-এর মাধ্যমে total money consistent থাকে।

---

# 8️⃣ মাঝখানে Error হলে?

ধরো:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 2000
WHERE account_id = 1;

-- এখানে কোনো error হলো

UPDATE accounts
SET balance = balance + 2000
WHERE account_id = 2;

ROLLBACK;
```

Rollback করলে প্রথম update-টাও undo হবে।

তাই:

```text
A থেকে টাকা কমেছে ❌
B-তে টাকা যোগ হয়নি ❌

ROLLBACK
↓
দুটো change বাতিল
```

---

# 9️⃣ SAVEPOINT কী?

Transaction-এর ভিতরে **checkpoint** তৈরি করতে `SAVEPOINT` ব্যবহার করি।

Example:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

SAVEPOINT point1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;
```

এখন চাইলে:

```sql
ROLLBACK TO point1;
```

করতে পারি।

এতে পুরো transaction বাতিল হবে না।

`point1`-এর পরের changes rollback হবে।

---

# 🔟 SAVEPOINT Flow

```text
START TRANSACTION
       ↓
Update A
       ↓
SAVEPOINT P1
       ↓
Update B
       ↓
ROLLBACK TO P1
       ↓
Update B cancelled
       ↓
Update A remains
```

শেষে:

```sql
COMMIT;
```

করলে remaining changes save হবে।

---

# 1️⃣1️⃣ Multiple SAVEPOINT

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

SAVEPOINT p1;

UPDATE accounts
SET balance = balance + 500
WHERE account_id = 2;

SAVEPOINT p2;

UPDATE accounts
SET balance = balance + 500
WHERE account_id = 3;

ROLLBACK TO p2;

COMMIT;
```

এখানে `p2`-এর পরের changes rollback হবে।

---

# 1️⃣2️⃣ এখন আসি ACID-এ 🔥

Database transaction-এর চারটি গুরুত্বপূর্ণ property:

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

অর্থাৎ:

> **ACID**

এটা DBMS exam + interview দুটোর জন্যই অত্যন্ত গুরুত্বপূর্ণ।

---

# 1️⃣3️⃣ A — Atomicity

Atomicity মানে:

> **Transaction-এর সব operation সফল হবে অথবা কোনো operation-ই final হবে না।**

অর্থাৎ:

```text
ALL or NOTHING
```

Bank transfer:

```text
Debit ✅
Credit ❌
```

এভাবে হওয়া যাবে না।

Transaction fail করলে:

```text
Debit ❌
Credit ❌
```

Rollback হবে।

### Golden Rule:

> **Atomicity = All or Nothing**

---

# 1️⃣4️⃣ C — Consistency

Consistency মানে:

> **Transaction-এর আগে এবং পরে database valid state-এ থাকতে হবে।**

ধরো:

```text
A = 10,000
B = 5,000
Total = 15,000
```

A → B 2,000 transfer:

```text
A = 8,000
B = 7,000
Total = 15,000
```

Database-এর defined rules/constraints ভাঙা যাবে না।

যেমন:

```text
balance < 0
```

যদি business rule অনুযায়ী allowed না হয়, তাহলে transaction fail করতে হবে।

### Golden Rule:

> **Consistency = Valid state → Valid state**

---

# 1️⃣5️⃣ Atomicity vs Consistency

এই দুইটা অনেকেই confuse করে।

### Atomicity:

```text
সব operation হবে
অথবা
কোনোটাই হবে না
```

### Consistency:

```text
Database rules/constraints ঠিক থাকবে
```

Example:

```text
Atomicity
→ Debit + Credit দুটো একসাথে হবে

Consistency
→ Transfer-এর পর total balance এবং constraints valid থাকবে
```

---

# 1️⃣6️⃣ I — Isolation

Isolation মানে:

> **একটি transaction-এর intermediate/uncommitted changes অন্য concurrent transaction যেন অনাকাঙ্ক্ষিতভাবে দেখতে বা প্রভাবিত করতে না পারে।**

ধরো:

```text
Transaction A
        ↓
Balance update করছে

Transaction B
        ↓
একই balance পড়ছে
```

A এখনো `COMMIT` করেনি।

B যেন A-এর incomplete state-এর কারণে ভুল result না পায়—এই ধরনের সমস্যা control করতে isolation ব্যবহৃত হয়।

---

# 1️⃣7️⃣ Isolation কেন দরকার?

একাধিক user একই সময়ে database ব্যবহার করে।

যেমন:

```text
User A → Bank Account
User B → Same Bank Account
User C → Same Bank Account
```

সবাই একই সময়ে operation করতে পারে।

Isolation না থাকলে concurrency problems হতে পারে।

---

# 1️⃣8️⃣ Common Isolation Problems

চারটি নাম মনে রাখো:

```text
Dirty Read
Non-Repeatable Read
Phantom Read
Lost Update
```

আজ এগুলোর basic concept বুঝি।

---

## Dirty Read

Transaction A data পরিবর্তন করেছে কিন্তু এখনো commit করেনি।

Transaction B সেই uncommitted data পড়ে ফেলল।

```text
A → UPDATE
      ↓
   uncommitted
      ↓
B → reads it ❌
```

এটাই Dirty Read।

---

# 1️⃣9️⃣ Non-Repeatable Read

একই transaction-এর মধ্যে একই row দুইবার read করা হলো।

প্রথমবার:

```text
salary = 50,000
```

অন্য transaction update করল।

দ্বিতীয়বার:

```text
salary = 60,000
```

একই transaction-এ একই row-এর value বদলে গেল।

এটাই Non-Repeatable Read।

---

# 2️⃣0️⃣ Phantom Read

একই condition দিয়ে query দুইবার চালানো হলো।

প্রথমবার:

```text
5 employees
```

অন্য transaction নতুন matching row insert করল।

দ্বিতীয়বার:

```text
6 employees
```

নতুন row যেন "phantom" হিসেবে দেখা দিল।

এটাই Phantom Read।

---

# 2️⃣1️⃣ Lost Update

দুই transaction একই data update করতে গিয়ে একজনের update অন্যজন overwrite করে ফেললে Lost Update হতে পারে।

```text
Initial salary = 50,000

A reads → 50,000
B reads → 50,000

A → 55,000
B → 52,000

Final → 52,000
```

A-এর update হারিয়ে গেল।

---

# 2️⃣2️⃣ D — Durability

Durability মানে:

> **COMMIT হয়ে গেলে transaction-এর changes database failure হলেও হারিয়ে যাওয়া উচিত নয়।**

ধরো:

```text
Transaction
    ↓
COMMIT
    ↓
Server crash
    ↓
Restart
```

তারপরও committed data থাকার কথা।

Database সাধারণত logging/recovery mechanisms ব্যবহার করে durability support করে।

### Golden Rule:

> **Durability = Committed data stays saved**

---

# 2️⃣3️⃣ ACID এক লাইনে

|Property|সহজ অর্থ|
|---|---|
|Atomicity|All or Nothing|
|Consistency|Valid state বজায় রাখা|
|Isolation|Concurrent transactions-এর interference control|
|Durability|Commit-এর পর data স্থায়ী|

### Shortcut:

```text
A → All or Nothing
C → Correct/Valid State
I → Independent/Isolated execution
D → Data stays after commit
```

---

# 2️⃣4️⃣ ACID Real-Life Example

ধরো ATM থেকে টাকা তুলছো।

```text
ATM Withdrawal
      ↓
Check balance
      ↓
Deduct money
      ↓
Record transaction
      ↓
Complete
```

### Atomicity

টাকা deduction এবং transaction operation মাঝপথে ভেঙে গেলে partial result হওয়া উচিত নয়।

### Consistency

Invalid balance state তৈরি করা যাবে না।

### Isolation

একই account নিয়ে concurrent transactions safely handle করতে হবে।

### Durability

Successful transaction commit হওয়ার পর record হারানো যাবে না।

---

# 2️⃣5️⃣ Transaction + Constraints

Transaction শুধু rollback-এর জন্য নয়।

Database constraints-এর সাথে কাজ করে:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
CHECK
NOT NULL
```

যদি transaction-এর কোনো operation constraint violate করে এবং application/database logic failure handle করে rollback করে, তাহলে database invalid state থেকে রক্ষা পেতে পারে।

---

# 2️⃣6️⃣ Transaction-এর একটি গুরুত্বপূর্ণ Rule

ধরো:

```sql
START TRANSACTION;

UPDATE accounts
SET balance = balance - 1000
WHERE account_id = 1;

UPDATE accounts
SET balance = balance + 1000
WHERE account_id = 2;

COMMIT;
```

`COMMIT` করার আগে changes সাধারণত transaction-এর অংশ।

কিন্তু `COMMIT` করার পরে:

```sql
ROLLBACK;
```

দিয়ে committed transaction undo করা যায় না।

### মনে রাখো:

> **ROLLBACK works on uncommitted changes.**

---

# 2️⃣7️⃣ Autocommit

MySQL-এ সাধারণত autocommit enabled থাকতে পারে।

মানে একটি statement সফলভাবে execute হলে সেটি automatically commit হতে পারে।

তাই multiple statements-এর transaction control করতে:

```sql
START TRANSACTION;
```

ব্যবহার করা গুরুত্বপূর্ণ।

---

# 2️⃣8️⃣ Transaction কখন ব্যবহার করব?

বিশেষ করে যখন multiple operations **একসাথে সফল হওয়া দরকার**।

Examples:

### Banking

```text
Debit
+
Credit
```

### E-commerce

```text
Create Order
+
Reduce Stock
+
Create Payment
```

### Hotel

```text
Create Booking
+
Reserve Room
+
Create Payment
```

### Ticket System

```text
Reserve Seat
+
Create Booking
+
Payment Record
```

---

# 2️⃣9️⃣ Database Designer হিসেবে ভাবো

ধরো Hotel Management System:

```text
Customer books room
        ↓
Check availability
        ↓
Create booking
        ↓
Update room availability
        ↓
Create payment
```

এই কাজগুলো আলাদা আলাদা SQL statement হতে পারে।

কিন্তু booking operation-এর logical unit হিসেবে transaction ব্যবহার করা যেতে পারে।

```text
START TRANSACTION
       ↓
Check/Reserve
       ↓
Booking Insert
       ↓
Room Update
       ↓
Payment Record
       ↓
COMMIT
```

কোনো critical step fail হলে:

```text
ROLLBACK
```

---

# 3️⃣0️⃣ Transaction + Stored Procedure

Class 47-এর সাথে connect করি।

Stored Procedure-এর ভিতরেও transaction logic থাকতে পারে।

Conceptually:

```text
CALL place_order()
       ↓
START TRANSACTION
       ↓
Create Order
       ↓
Reduce Stock
       ↓
Create Payment
       ↓
COMMIT
```

Error হলে:

```text
ROLLBACK
```

এটা real-world backend/database design-এর গুরুত্বপূর্ণ pattern।

---

# 3️⃣1️⃣ Common Beginner Mistakes

### ❌ Mistake 1

শুধু:

```sql
START TRANSACTION;
```

লিখে `COMMIT`/`ROLLBACK` না করা।

---

### ❌ Mistake 2

মনে করা `ROLLBACK` সব historical data undo করতে পারে।

না।

> Rollback মূলত current transaction-এর uncommitted changes-এর জন্য।

---

### ❌ Mistake 3

Atomicity এবং Consistency একই মনে করা।

```text
Atomicity
→ All or Nothing

Consistency
→ Valid State
```

---

### ❌ Mistake 4

Isolation মানে "database-এর সব transaction একটার পর একটা চলবে" মনে করা।

Isolation-এর উদ্দেশ্য concurrency control—সব transaction necessarily serially execute করানো নয়।

---

### ❌ Mistake 5

প্রতিটি SELECT-এর জন্য transaction ব্যবহার করা।

সব query-তে complex transaction দরকার হয় না। Business operation অনুযায়ী transaction boundary design করতে হয়।

---

# 🧠 Class 48 Golden Cheat Sheet

```text
TRANSACTION
↓
Logical unit of work

START TRANSACTION
↓
Begin

COMMIT
↓
Save permanently

ROLLBACK
↓
Undo uncommitted changes

SAVEPOINT
↓
Create checkpoint
```

ACID:

```text
A = Atomicity
    All or Nothing

C = Consistency
    Valid State

I = Isolation
    Concurrent transaction control

D = Durability
    Committed data remains
```

---

# 📝 Class 48 Assignment

### Q1

একটি transaction লিখো যেখানে:

```text
Account 1 থেকে 500 টাকা কমবে
Account 2-তে 500 টাকা যোগ হবে
```

তারপর `COMMIT` করবে।

---

### Q2

উপরের transaction-এ দ্বিতীয় operation fail করলে কীভাবে `ROLLBACK` করবে?

---

### Q3

`SAVEPOINT` ব্যবহার করে:

```text
Update A
SAVEPOINT
Update B
ROLLBACK TO SAVEPOINT
COMMIT
```

লিখো।

---

### Q4

নিজের ভাষায় explain করো:

```text
Atomicity
Consistency
Isolation
Durability
```

---

### Q5 ⭐

Bank transfer-এর ক্ষেত্রে কেন transaction দরকার?

---

### Q6 ⭐

এই চারটির difference explain করো:

```text
COMMIT
ROLLBACK
SAVEPOINT
ROLLBACK TO SAVEPOINT
```

---

# 🧪 Class 48 MCQ

**1. Transaction কী?**

A. Table  
B. Logical unit of work  
C. Index  
D. Column

**2. Permanentভাবে transaction changes save করতে?**

A. SAVE  
B. COMMIT  
C. STORE  
D. ACCEPT

**3. Uncommitted changes বাতিল করতে?**

A. DELETE  
B. DROP  
C. ROLLBACK  
D. CLEAR

**4. ACID-এর A কী?**

A. Access  
B. Atomicity  
C. Accuracy  
D. Authorization

**5. "All or Nothing" কোন property?**

A. Consistency  
B. Isolation  
C. Atomicity  
D. Durability

**6. Database valid state বজায় রাখার property?**

A. Atomicity  
B. Consistency  
C. Isolation  
D. Durability

**7. Concurrent transactions-এর interference control-এর সাথে কোনটি সম্পর্কিত?**

A. Isolation  
B. Atomicity  
C. Durability  
D. Backup

**8. Commit-এর পরে data persistence কোন property?**

A. Atomicity  
B. Consistency  
C. Isolation  
D. Durability

**9. Transaction-এর ভিতরে checkpoint তৈরি করতে?**

A. CHECKPOINT ONLY  
B. SAVEPOINT  
C. MARK  
D. HOLD

**10. `ROLLBACK TO p1` কী করে?**

A. পুরো database delete করে  
B. পুরো transaction permanently commit করে  
C. নির্দিষ্ট savepoint-এ ফিরে যায়  
D. Table drop করে

---

## 🎯 আজকের সবচেয়ে গুরুত্বপূর্ণ ৫টি লাইন

```text
Transaction = Logical Unit of Work

COMMIT = Save

ROLLBACK = Undo uncommitted changes

SAVEPOINT = Checkpoint

ACID = Atomicity + Consistency + Isolation + Durability
```

**Next → Class 49: SQL Triggers** — `BEFORE/AFTER INSERT`, `UPDATE`, `DELETE`, audit log, automatic validation এবং real-world database automation।

---

# 📘 Class 49 — SQL Triggers

আজকে আমরা শিখব **SQL Trigger**।

তুমি Class 47-এ শিখেছো **Stored Procedure**, Class 48-এ **Transaction**। এখন Trigger শিখলে database-এর **automatic actions** বুঝতে পারবে।

---

## 1️⃣ Trigger কী?

সহজভাবে:

> **Trigger হলো database-এর এমন একটি automatic program, যা কোনো নির্দিষ্ট database event ঘটলে নিজে থেকেই execute হয়।**

তুমি manually:

```sql
CALL procedure();
```

করবে না।

বরং:

```text
INSERT / UPDATE / DELETE
        ↓
   Event ঘটলো
        ↓
    TRIGGER
        ↓
Automatic Action
```

### Example

কেউ employee-এর salary update করল:

```text
Salary changed
      ↓
Trigger automatically runs
      ↓
Audit table-এ old/new salary save
```

---

# 2️⃣ Trigger কেন ব্যবহার করি?

Real-world database-এ Trigger ব্যবহার হতে পারে:

- Audit log
    
- Automatically update related data
    
- Data validation
    
- History maintain
    
- Inventory update
    
- Change tracking
    
- Automatic timestamp
    
- Delete history
    
- Business rule enforcement
    

---

# 3️⃣ Trigger-এর Basic Structure

MySQL:

```sql
DELIMITER //

CREATE TRIGGER trigger_name
BEFORE INSERT
ON table_name
FOR EACH ROW
BEGIN

    -- SQL statements

END //

DELIMITER ;
```

এখানে:

```text
BEFORE
↓
কখন?

INSERT
↓
কোন event?

ON table_name
↓
কোন table?

FOR EACH ROW
↓
কোন row-এর জন্য?
```

---

# 4️⃣ Trigger-এর তিনটি Main Event

সবচেয়ে গুরুত্বপূর্ণ:

```text
INSERT
UPDATE
DELETE
```

অর্থাৎ:

```text
INSERT → নতুন row
UPDATE → row পরিবর্তন
DELETE → row মুছে ফেলা
```

---

# 5️⃣ BEFORE vs AFTER

Trigger event-এর আগে অথবা পরে execute হতে পারে।

```text
BEFORE
AFTER
```

তাই basic combination:

```text
BEFORE INSERT
AFTER INSERT

BEFORE UPDATE
AFTER UPDATE

BEFORE DELETE
AFTER DELETE
```

---

# 6️⃣ BEFORE INSERT

ধরো employee insert করার আগে salary validation করতে চাই।

```sql
DELIMITER //

CREATE TRIGGER check_salary
BEFORE INSERT
ON employees
FOR EACH ROW
BEGIN

    IF NEW.salary < 0 THEN
        SET NEW.salary = 0;
    END IF;

END //

DELIMITER ;
```

এখানে:

```sql
NEW.salary
```

মানে হচ্ছে:

> যে নতুন row insert হতে যাচ্ছে, তার salary।

---

# 7️⃣ `NEW` কী?

Trigger-এ `NEW` খুব গুরুত্বপূর্ণ।

ধরো:

```sql
INSERT INTO employees
(name, salary)
VALUES
('Rahim', 50000);
```

Trigger-এর ভিতরে:

```sql
NEW.name
```

হবে:

```text
Rahim
```

আর:

```sql
NEW.salary
```

হবে:

```text
50000
```

### Golden Rule

> **NEW = নতুন value**

---

# 8️⃣ `OLD` কী?

`OLD` মানে:

> **আগের value**

বিশেষ করে UPDATE এবং DELETE trigger-এ বেশি ব্যবহৃত হয়।

ধরো salary আগে:

```text
50000
```

Update হয়ে:

```text
60000
```

তাহলে:

```text
OLD.salary = 50000
NEW.salary = 60000
```

---

# 9️⃣ NEW vs OLD

|Event|NEW|OLD|
|---|---|---|
|INSERT|✅|❌|
|UPDATE|✅|✅|
|DELETE|❌|✅|

এটা **খুব গুরুত্বপূর্ণ MCQ**।

মনে রাখো:

```text
INSERT → NEW
UPDATE → OLD + NEW
DELETE → OLD
```

---

# 🔟 BEFORE INSERT — Real Example

ধরো user email lowercase করতে চাই।

```sql
DELIMITER //

CREATE TRIGGER normalize_email
BEFORE INSERT
ON customers
FOR EACH ROW
BEGIN
    SET NEW.email = LOWER(TRIM(NEW.email));
END //

DELIMITER ;
```

এখন:

```sql
INSERT INTO customers
(name, email)
VALUES
('Rahim', '  RAHIM@GMAIL.COM  ');
```

Trigger automatically করবে:

```text
"  RAHIM@GMAIL.COM  "
          ↓
"rahim@gmail.com"
```

---

# 1️⃣1️⃣ AFTER INSERT

কখনো নতুন row insert হওয়ার **পরে** অন্য কাজ করতে চাই।

ধরো audit table:

```sql
CREATE TABLE customer_logs (
    log_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    action VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

এখন customer insert হলে automatically log:

```sql
DELIMITER //

CREATE TRIGGER customer_insert_log
AFTER INSERT
ON customers
FOR EACH ROW
BEGIN

    INSERT INTO customer_logs
    (customer_id, action)
    VALUES
    (NEW.customer_id, 'CUSTOMER_CREATED');

END //

DELIMITER ;
```

এখন:

```sql
INSERT INTO customers
(customer_name, city)
VALUES
('Karim', 'Dhaka');
```

তখন automatically:

```text
customers
   ↓
New customer

customer_logs
   ↓
CUSTOMER_CREATED
```

---

# 1️⃣2️⃣ BEFORE UPDATE

ধরো salary negative হতে দিতে চাই না।

```sql
DELIMITER //

CREATE TRIGGER validate_salary_update
BEFORE UPDATE
ON employees
FOR EACH ROW
BEGIN

    IF NEW.salary < 0 THEN
        SET NEW.salary = 0;
    END IF;

END //

DELIMITER ;
```

যদি:

```sql
UPDATE employees
SET salary = -5000
WHERE employee_id = 1;
```

তাহলে Trigger:

```text
NEW.salary = -5000
       ↓
Check
       ↓
< 0
       ↓
Set = 0
```

---

# 1️⃣3️⃣ AFTER UPDATE

এবার salary change history রাখি।

History table:

```sql
CREATE TABLE salary_history (
    history_id INT AUTO_INCREMENT PRIMARY KEY,
    employee_id INT,
    old_salary DECIMAL(10,2),
    new_salary DECIMAL(10,2),
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Trigger:

```sql
DELIMITER //

CREATE TRIGGER salary_change_log
AFTER UPDATE
ON employees
FOR EACH ROW
BEGIN

    IF OLD.salary <> NEW.salary THEN

        INSERT INTO salary_history
        (
            employee_id,
            old_salary,
            new_salary
        )
        VALUES
        (
            NEW.employee_id,
            OLD.salary,
            NEW.salary
        );

    END IF;

END //

DELIMITER ;
```

এখন:

```sql
UPDATE employees
SET salary = 60000
WHERE employee_id = 1;
```

Automatically history তৈরি হবে।

---

# 1️⃣4️⃣ কেন `OLD` এবং `NEW` দুটো দরকার?

কারণ আমরা জানতে চাই:

```text
আগে কত ছিল?
↓
OLD.salary

এখন কত?
↓
NEW.salary
```

Example:

```text
OLD.salary = 50000
NEW.salary = 60000
```

Audit system-এর জন্য এটা খুব useful।

---

# 1️⃣5️⃣ AFTER DELETE

ধরো employee delete করলে তার history রাখতে চাই।

```sql
CREATE TABLE deleted_employees (
    employee_id INT,
    name VARCHAR(100),
    deleted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Trigger:

```sql
DELIMITER //

CREATE TRIGGER employee_delete_log
AFTER DELETE
ON employees
FOR EACH ROW
BEGIN

    INSERT INTO deleted_employees
    (employee_id, name)
    VALUES
    (OLD.employee_id, OLD.name);

END //

DELIMITER ;
```

এখন:

```sql
DELETE FROM employees
WHERE employee_id = 5;
```

Delete হওয়ার পর:

```text
employees
   ↓
row deleted

deleted_employees
   ↓
old row saved
```

এখানে:

```sql
OLD.employee_id
OLD.name
```

ব্যবহার করেছি।

কারণ DELETE-এর পরে `NEW` row নেই।

---

# 1️⃣6️⃣ BEFORE DELETE

কখনো delete হওয়ার আগে restriction দিতে পারি।

Example:

```sql
DELIMITER //

CREATE TRIGGER prevent_employee_delete
BEFORE DELETE
ON employees
FOR EACH ROW
BEGIN

    IF OLD.department = 'Management' THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Management employee cannot be deleted';

    END IF;

END //

DELIMITER ;
```

এখন management employee delete করতে গেলে error হবে।

---

# 1️⃣7️⃣ `SIGNAL` কী?

MySQL-এ custom error তৈরি করতে:

```sql
SIGNAL SQLSTATE '45000'
```

ব্যবহার করা যায়।

Example:

```sql
SIGNAL SQLSTATE '45000'
SET MESSAGE_TEXT = 'Invalid salary';
```

Result:

```text
Error: Invalid salary
```

এটা database-level validation-এর জন্য useful।

---

# 1️⃣8️⃣ Inventory Example 🔥

এখন একটি খুব important real-world example।

ধরো:

```text
products
---------
product_id
name
stock
price
```

Order তৈরি হলে stock automatically কমবে।

Order insert:

```sql
INSERT INTO orders
(product_id, quantity)
VALUES
(10, 3);
```

Trigger:

```sql
DELIMITER //

CREATE TRIGGER reduce_stock
AFTER INSERT
ON orders
FOR EACH ROW
BEGIN

    UPDATE products
    SET stock = stock - NEW.quantity
    WHERE product_id = NEW.product_id;

END //

DELIMITER ;
```

এখন:

```text
Order quantity = 3
        ↓
Trigger
        ↓
Product stock - 3
```

---

# 1️⃣9️⃣ কিন্তু এখানে একটি Problem আছে ⚠️

শুধু stock কমালেই হবে না।

ধরো:

```text
Current stock = 2
Order quantity = 5
```

তাহলে:

```text
2 - 5 = -3
```

Stock negative হয়ে যাবে।

তাই validation দরকার।

---

# 2️⃣0️⃣ BEFORE INSERT Stock Validation

```sql
DELIMITER //

CREATE TRIGGER check_stock
BEFORE INSERT
ON orders
FOR EACH ROW
BEGIN

    DECLARE current_stock INT;

    SELECT stock
    INTO current_stock
    FROM products
    WHERE product_id = NEW.product_id;

    IF current_stock < NEW.quantity THEN

        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Insufficient stock';

    END IF;

END //

DELIMITER ;
```

Flow:

```text
New Order
   ↓
Check stock
   ↓
Enough?
 ↙      ↘
YES      NO
 ↓        ↓
Insert   Error
```

---

# 2️⃣1️⃣ Trigger + Transaction

Class 48-এর সাথে connect করি।

ধরো:

```text
Create Order
+
Reduce Stock
+
Payment
```

Transaction:

```text
START TRANSACTION
       ↓
INSERT order
       ↓
Trigger runs
       ↓
Stock update
       ↓
Payment
       ↓
COMMIT
```

কোনো critical operation fail করলে transaction rollback করা যায়।

---

# 2️⃣2️⃣ Trigger vs Procedure

খুব important comparison:

|Feature|Trigger|Procedure|
|---|---|---|
|Manually call|❌|✅ `CALL`|
|Automatically runs|✅|❌|
|Event based|✅|সাধারণত ❌|
|INSERT/UPDATE/DELETE event|✅|Logic-এর উপর নির্ভর|
|Parameters|Trigger parameters নেই|IN/OUT/INOUT|
|Audit|Excellent|Possible|
|Business operation|Limited/Use carefully|Excellent|

### সহজভাবে:

> **Procedure = তুমি ডাকো**

> **Trigger = Database নিজে ডাকে**

---

# 2️⃣3️⃣ Trigger vs Function

|Trigger|Function|
|---|---|
|Event-এর কারণে automatically execute|Query-তে call করা যায়|
|INSERT/UPDATE/DELETE event|Value return করে|
|Audit/automation|Calculation|
|`NEW`/`OLD`|Parameters|
|Directly `CALL` নয়|`SELECT function()`|

---

# 2️⃣4️⃣ Trigger vs View

```text
VIEW
→ Data দেখানোর reusable query

TRIGGER
→ Event ঘটলে automatic action

PROCEDURE
→ Explicitly call করা reusable operation

FUNCTION
→ Reusable calculation
```

এখন তোমার SQL object knowledge:

```text
TABLE
↓
Actual Data

VIEW
↓
Saved Query

CTE
↓
Temporary Query Structure

FUNCTION
↓
Return Value

PROCEDURE
↓
Executable Logic

TRIGGER
↓
Automatic Event-Based Logic
```

---

# 2️⃣5️⃣ Trigger কখন ব্যবহার করা ভালো?

### ভালো use case:

```text
Audit Log
History
Automatic timestamp
Data validation
Automatic related update
Inventory synchronization
```

---

# 2️⃣6️⃣ Trigger কখন Avoid করা উচিত?

Trigger powerful হলেও বেশি ব্যবহার করলে application বুঝতে কঠিন হয়ে যেতে পারে।

ধরো:

```sql
INSERT INTO orders ...
```

তুমি ভাবলে শুধু order insert হচ্ছে।

কিন্তু database-এর ভিতরে:

```text
Trigger 1
↓
Update stock

Trigger 2
↓
Create log

Trigger 3
↓
Update customer points

Trigger 4
↓
Create history
```

তখন debugging কঠিন হতে পারে।

### Golden Rule:

> **Trigger ব্যবহার করো যখন automatic database-level behavior সত্যিই দরকার।**

সব business logic trigger-এ ঢুকিয়ে দিও না।

---

# 2️⃣7️⃣ Common Beginner Mistakes

### ❌ Mistake 1

`INSERT` trigger-এ `OLD` ব্যবহার করা।

ভুল:

```sql
OLD.salary
```

INSERT-এর ক্ষেত্রে `OLD` নেই।

---

### ❌ Mistake 2

DELETE trigger-এ `NEW` ব্যবহার করা।

DELETE-এর ক্ষেত্রে:

```text
OLD ✅
NEW ❌
```

---

### ❌ Mistake 3

একই table-এর জন্য duplicate trigger name তৈরি করা।

Trigger name database/schema অনুযায়ী unique রাখতে হবে।

---

### ❌ Mistake 4

Trigger-এর ভিতরে ভুলভাবে recursive operation করা।

একটি trigger অন্য trigger-কে indirectly activate করলে logic complex হতে পারে।

---

### ❌ Mistake 5

Trigger দিয়ে সব business logic করা।

এতে debugging এবং maintenance কঠিন হতে পারে।

---

# 2️⃣8️⃣ Trigger দেখার Command

MySQL-এ:

```sql
SHOW TRIGGERS;
```

নির্দিষ্ট trigger-এর definition:

```sql
SHOW CREATE TRIGGER trigger_name;
```

---

# 2️⃣9️⃣ Trigger Delete

Trigger আর দরকার না হলে:

```sql
DROP TRIGGER trigger_name;
```

Safe version:

```sql
DROP TRIGGER IF EXISTS trigger_name;
```

---

# 🧠 Class 49 Golden Cheat Sheet

```text
TRIGGER
↓
Automatic database action
```

Events:

```text
INSERT
UPDATE
DELETE
```

Timing:

```text
BEFORE
AFTER
```

NEW/OLD:

```text
INSERT → NEW

UPDATE → OLD + NEW

DELETE → OLD
```

সবচেয়ে গুরুত্বপূর্ণ:

```text
Procedure
→ Manually CALL

Trigger
→ Automatically fires

Function
→ Returns value

View
→ Saved query
```

---

# 📝 Class 49 Assignment

ধরো তোমার database:

### `products`

```text
product_id
name
stock
price
```

### `orders`

```text
order_id
product_id
quantity
order_date
```

### `price_history`

```text
history_id
product_id
old_price
new_price
changed_at
```

### Task 1

একটি `BEFORE INSERT` trigger তৈরি করো যাতে:

```text
quantity <= 0
```

হলে error দেখায়।

---

### Task 2

একটি `AFTER INSERT` trigger তৈরি করো যাতে order তৈরি হলে product stock automatically কমে যায়।

---

### Task 3 ⭐

একটি `BEFORE INSERT` trigger তৈরি করো যাতে insufficient stock হলে:

```text
Insufficient stock
```

error দেয়।

---

### Task 4

Product-এর price পরিবর্তন হলে `price_history` table-এ:

```text
old_price
new_price
```

automatically save করো।

---

### Task 5

নিজের ভাষায় explain করো:

```text
NEW
OLD
BEFORE
AFTER
```

---

### Task 6 ⭐

এই চারটির difference লিখো:

```text
Procedure
Function
Trigger
View
```

---

# 🧪 Class 49 MCQ

**1. Trigger কী?**

A. Saved table  
B. Automatically executed database logic  
C. Index  
D. Database

**2. Trigger কোন event-এর উপর কাজ করতে পারে?**

A. INSERT  
B. UPDATE  
C. DELETE  
D. All of the above

**3. INSERT-এর ক্ষেত্রে কোনটি available?**

A. OLD  
B. NEW  
C. OLD + NEW  
D. কোনোটিই নয়

**4. DELETE-এর ক্ষেত্রে কোনটি available?**

A. NEW  
B. OLD  
C. OLD + NEW  
D. Parameter

**5. UPDATE-এর ক্ষেত্রে?**

A. শুধু OLD  
B. শুধু NEW  
C. OLD + NEW  
D. কোনোটিই নয়

**6. Trigger manually `CALL` করা হয়?**

A. Yes  
B. No

**7. Custom MySQL error তৈরি করতে কোনটি ব্যবহার করা যায়?**

A. SIGNAL  
B. ERROR()  
C. THROW ONLY  
D. STOP

**8. Audit log-এর জন্য কোনটি useful?**

A. Trigger  
B. Index only  
C. Database name  
D. Column alias

**9. `BEFORE INSERT` trigger কখন execute হয়?**

A. Insert-এর আগে  
B. Insert-এর পরে  
C. Database বন্ধ হওয়ার পরে  
D. SELECT-এর সময়

**10. কোন statement trigger delete করে?**

A. DELETE TRIGGER  
B. REMOVE TRIGGER  
C. DROP TRIGGER  
D. CLEAR TRIGGER

---

## 🎯 আজকের ৬টা Golden Line

```text
1. Trigger = Automatic database logic

2. BEFORE = Event-এর আগে

3. AFTER = Event-এর পরে

4. INSERT → NEW

5. UPDATE → OLD + NEW

6. DELETE → OLD
```

**Next → Class 50: SQL Indexing** — Primary Index, Secondary Index, Composite Index, Unique Index, B-Tree concept, কেন index query দ্রুত করে, কখন index ব্যবহার করা উচিত/উচিত নয়, এবং `EXPLAIN` দিয়ে query performance বোঝার foundation।

---
# 📘 Class 50 — SQL Indexing

আজকের classটা **Database Designer** হওয়ার জন্য খুবই গুরুত্বপূর্ণ।

এখন পর্যন্ত তুমি SQL-এর query writing, JOIN, CTE, Window Function, View, Procedure, Transaction, Trigger শিখেছো।

আজ থেকে আমরা query **কীভাবে দ্রুত এবং efficiently execute করানো যায়** সেটা শিখব।

আজকের topics:

1. Index কী?
    
2. কেন Index দরকার?
    
3. Without Index vs With Index
    
4. `CREATE INDEX`
    
5. Unique Index
    
6. Composite Index
    
7. Primary Key Index
    
8. Foreign Key Index
    
9. Index কখন ব্যবহার করবে?
    
10. Index কখন ব্যবহার করবে না?
    
11. B-Tree concept
    
12. Composite Index-এর column order
    
13. Covering Index concept
    
14. `EXPLAIN` introduction
    
15. Common mistakes
    
16. Assignment + MCQ
    

---

# 1️⃣ Index কী?

সহজভাবে:

> **Index হলো database-এর একটি data structure, যা নির্দিষ্ট data দ্রুত খুঁজে পেতে সাহায্য করে।**

একটা বই চিন্তা করো।

তুমি যদি বইয়ের মধ্যে:

```text
Database
```

শব্দটা খুঁজতে চাও, তাহলে পুরো 500 page পড়বে না।

বইয়ের শেষে:

```text
Index

Database ............ Page 120
Database Design ..... Page 250
Database Security ... Page 380
```

থাকলে সরাসরি relevant page-এ যেতে পারো।

Database index একই ধরনের ধারণা।

---

# 2️⃣ Without Index কী হয়?

ধরো:

```sql
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

এবং table-এ:

```text
10,000,000 rows
```

থাকে।

যদি suitable index না থাকে, database-কে অনেক row পরীক্ষা করতে হতে পারে।

Conceptually:

```text
1
2
3
4
5
...
10,000,000
```

---

# 3️⃣ With Index

যদি:

```sql
CREATE INDEX idx_customer_email
ON customers(email);
```

থাকে, database email lookup-এর জন্য index ব্যবহার করতে পারে।

Conceptually:

```text
Index
  ↓
Find email
  ↓
Find row location
  ↓
Read row
```

তাই search অনেক efficient হতে পারে।

---

# 4️⃣ Index-এর মূল উদ্দেশ্য

```text
Index
  ↓
Faster Data Retrieval
```

বিশেষ করে:

```sql
WHERE
JOIN
ORDER BY
GROUP BY
```

এর কিছু ক্ষেত্রে index খুব useful হতে পারে।

তবে **সব query automatically faster হবে না**।

---

# 5️⃣ Basic Index তৈরি

```sql
CREATE INDEX idx_customer_email
ON customers(email);
```

Structure:

```text
CREATE INDEX index_name
ON table_name(column_name);
```

---

# 6️⃣ Index List দেখা

MySQL:

```sql
SHOW INDEX FROM customers;
```

এতে table-এর indexes দেখতে পারবে।

---

# 7️⃣ Index Delete

Index আর দরকার না হলে:

```sql
DROP INDEX idx_customer_email
ON customers;
```

---

# 8️⃣ Primary Key কি Index?

হ্যাঁ।

যেমন:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

`PRIMARY KEY` সাধারণত একটি index structure তৈরি করে।

তাই আলাদাভাবে:

```sql
CREATE INDEX idx_customer_id
ON customers(customer_id);
```

করার সাধারণত দরকার নেই।

---

# 9️⃣ UNIQUE Index

ধরো customer email unique হতে হবে।

```sql
CREATE UNIQUE INDEX idx_unique_email
ON customers(email);
```

এতে একই email duplicate insert করা যাবে না।

Example:

```text
rahim@gmail.com ✅

rahim@gmail.com ❌
```

### তবে যদি column-এ আগে থেকেই:

```sql
email VARCHAR(255) UNIQUE
```

থাকে, database ইতিমধ্যে uniqueness enforce করার জন্য appropriate index তৈরি করতে পারে। তাই duplicate index তৈরি করা উচিত নয়।

---

# 🔟 Index + WHERE

সবচেয়ে common use case:

```sql
SELECT *
FROM employees
WHERE department = 'IT';
```

যদি এই ধরনের query খুব frequently চলে:

```sql
CREATE INDEX idx_employee_department
ON employees(department);
```

তাহলে optimizer পরিস্থিতি অনুযায়ী index ব্যবহার করতে পারে।

---

# 1️⃣1️⃣ Index + JOIN

ধরো:

```sql
SELECT *
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id;
```

এখানে:

```text
orders.customer_id
```

একটি important join column।

তাই appropriate index useful হতে পারে।

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

তবে actual performance `EXPLAIN` দিয়ে verify করা উচিত।

---

# 1️⃣2️⃣ Foreign Key এবং Index

ধরো:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

`customer_id`-তে index থাকা সাধারণত useful, বিশেষ করে JOIN এবং parent-child operations-এর জন্য।

কিছু MySQL/InnoDB পরিস্থিতিতে foreign key constraint-এর জন্য প্রয়োজনীয় index automatically তৈরি/ব্যবহৃত হতে পারে।

তাই blindly duplicate index তৈরি না করে:

```sql
SHOW INDEX FROM orders;
```

দিয়ে আগে check করবে।

---

# 1️⃣3️⃣ Composite Index

এখন important topic।

ধরো query:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
  AND city = 'Dhaka';
```

দুই column-এর উপর একসাথে index তৈরি করা যায়:

```sql
CREATE INDEX idx_dept_city
ON employees(department, city);
```

এটাকে বলে:

> **Composite Index / Multi-column Index**

---

# 1️⃣4️⃣ Composite Index-এর Structure

```text
(department, city)
```

এখানে:

```text
1st column → department
2nd column → city
```

Column order গুরুত্বপূর্ণ।

---

# 1️⃣5️⃣ Leftmost Prefix Rule 🔥

এটা খুব গুরুত্বপূর্ণ।

Index:

```sql
CREATE INDEX idx_dept_city
ON employees(department, city);
```

এই index ভালোভাবে কাজে লাগতে পারে যখন query শুরু করছে:

```sql
WHERE department = 'IT'
```

অথবা:

```sql
WHERE department = 'IT'
AND city = 'Dhaka'
```

কিন্তু শুধু:

```sql
WHERE city = 'Dhaka'
```

এর ক্ষেত্রে এই composite index সাধারণত পুরোপুরি equivalent সুবিধা দেবে না।

কারণ index order:

```text
department → city
```

---

# 1️⃣6️⃣ কেন Order গুরুত্বপূর্ণ?

ধরো telephone directory:

```text
Last Name
   ↓
First Name
```

যদি তুমি শুধু first name জানো:

```text
Rahim
```

তাহলে last name না জেনে পুরো structure থেকে efficiently locate করা কঠিন হতে পারে।

একইভাবে:

```text
(department, city)
```

এবং:

```text
(city, department)
```

এক জিনিস নয়।

---

# 1️⃣7️⃣ Composite Index Example

Query:

```sql
SELECT *
FROM orders
WHERE customer_id = 10
  AND order_date >= '2026-01-01';
```

Potential index:

```sql
CREATE INDEX idx_customer_date
ON orders(customer_id, order_date);
```

এখানে:

```text
customer_id → first
order_date  → second
```

এই query pattern-এর সাথে ভালোভাবে match করে।

---

# 1️⃣8️⃣ Single vs Composite Index

ধরো:

```text
WHERE department = ?
AND city = ?
```

Possible:

### Option A

```sql
CREATE INDEX idx_department
ON employees(department);

CREATE INDEX idx_city
ON employees(city);
```

### Option B

```sql
CREATE INDEX idx_department_city
ON employees(department, city);
```

কোনটা better?

> **Query pattern, data distribution, workload এবং optimizer plan-এর উপর নির্ভর করে।**

শুধু "দুইটা condition আছে, তাই composite index"—এমন fixed rule নেই।

---

# 1️⃣9️⃣ Index + ORDER BY

ধরো:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

Frequently used workload হলে:

```sql
CREATE INDEX idx_salary
ON employees(salary);
```

optimizer পরিস্থিতি অনুযায়ী index ব্যবহার করতে পারে।

---

# 2️⃣0️⃣ Index + WHERE + ORDER BY

আরও interesting:

```sql
SELECT *
FROM employees
WHERE department = 'IT'
ORDER BY salary DESC;
```

Potential index:

```sql
CREATE INDEX idx_department_salary
ON employees(department, salary);
```

এখানে index query-এর filtering এবং ordering pattern-এর সাথে match করতে পারে।

তবে actual execution plan অবশ্যই check করবে।

---

# 2️⃣1️⃣ Index-এর Cost আছে ⚠️

অনেকে ভাবে:

> "অনেক index দিলে database আরো fast হবে।"

❌ ভুল।

Index-এর সুবিধা আছে, কিন্তু cost-ও আছে।

কারণ:

```text
INSERT
UPDATE
DELETE
```

করলে index-ও maintain/update করতে হয়।

তাই:

```text
More Indexes
     ↓
Faster Reads
     +
More Storage
     +
More Write Maintenance
```

---

# 2️⃣2️⃣ INSERT কেন slower হতে পারে?

ধরো table-এ:

```text
1 million rows
```

এবং:

```text
5 indexes
```

আছে।

নতুন row insert হলে শুধু table-এ data রাখলেই হবে না।

Relevant index structures-ও update করতে হবে।

তাই অনেক unnecessary index থাকলে write performance খারাপ হতে পারে।

---

# 2️⃣3️⃣ UPDATE-এর ক্ষেত্রেও

যদি indexed column update করো:

```sql
UPDATE employees
SET department = 'HR'
WHERE employee_id = 10;
```

তাহলে `department` indexed হলে index structure-ও maintain করতে হবে।

---

# 2️⃣4️⃣ DELETE-এর ক্ষেত্রেও

```sql
DELETE FROM employees
WHERE employee_id = 10;
```

Row delete হওয়ার সাথে সাথে relevant indexes থেকেও entry remove/update করতে হবে।

---

# 2️⃣5️⃣ কখন Index ব্যবহার করব?

সাধারণত consider করবে যখন column:

### 1. Frequently searched

```sql
WHERE email = ?
```

### 2. Frequently joined

```sql
ON orders.customer_id = customers.customer_id
```

### 3. Frequently sorted

```sql
ORDER BY created_at
```

### 4. Frequently filtered

```sql
WHERE status = 'active'
```

### 5. High-cardinality column

যেমন:

```text
email
user_id
order_id
```

এগুলোতে অনেক unique/distinct value থাকতে পারে।

---

# 2️⃣6️⃣ Low Cardinality Column

ধরো:

```text
gender
```

শুধু:

```text
Male
Female
```

অথবা:

```text
status
```

শুধু:

```text
Active
Inactive
```

এ ধরনের low-cardinality column-এ index সব query-তে খুব effective নাও হতে পারে।

### কিন্তু!

এটা absolute rule নয়।

যদি table বিশাল হয় এবং query pattern appropriate হয়, low-cardinality column-এও index useful হতে পারে।

তাই:

> **Cardinality + table size + query pattern + execution plan—সব consider করবে।**

---

# 2️⃣7️⃣ B-Tree Index কী?

এখন একটু ভিতরে যাই।

Relational databases-এ common index structure হলো:

> **B-Tree / B+Tree family**

সহজভাবে:

```text
             [50]
           /      \
       [20]       [80]
      /   \       /   \
    [10] [30]  [60] [90]
```

Data sorted structure-এ organized থাকে।

তাই database পুরো table scan না করে search space দ্রুত narrow করতে পারে।

---

# 2️⃣8️⃣ Binary Search-এর সাথে সম্পর্ক

ধরো sorted data:

```text
10
20
30
40
50
60
70
80
90
```

তুমি `80` খুঁজছো।

Sequentially:

```text
10 → 20 → 30 → ...
```

না খুঁজে tree/search structure ব্যবহার করে search space দ্রুত ছোট করা যায়।

Database index-এর internal structure অনেক বেশি sophisticated এবং disk/page oriented, কিন্তু basic intuition হলো:

> **Organized search structure → fewer data pages/entries examined**

---

# 2️⃣9️⃣ Clustered vs Secondary Index — Concept

এটা Database Designer হিসেবে জানা ভালো।

### Clustered Index

Table data-এর physical/logical organization index order-এর সাথে closely associated।

### Secondary Index

Table data-এর আলাদা index structure থাকে, যা মূল data row-তে locate করতে সাহায্য করে।

MySQL InnoDB-তে:

> **Primary key হলো clustered index-এর ভিত্তি।**

আর অন্যান্য indexes সাধারণত secondary indexes।

---

# 3️⃣0️⃣ InnoDB-এর Important Concept

MySQL InnoDB table-এ:

```text
Primary Key
     ↓
Clustered Index
     ↓
Actual row data
```

Secondary index-এর leaf entries primary key value-ও carry করে, যাতে corresponding clustered row locate করা যায়।

এ কারণে primary key design গুরুত্বপূর্ণ।

---

# 3️⃣1️⃣ Primary Key ছোট রাখা কেন ভালো?

ধরো:

```text
PRIMARY KEY = BIGINT
```

এবং table-এর অনেক secondary indexes আছে।

InnoDB secondary index entries-এ primary key value ব্যবহার হওয়ায় খুব বড় primary key হলে index size বাড়তে পারে।

তাই সাধারণভাবে:

> **Primary key ছোট, stable এবং appropriate type-এর রাখা ভালো।**

---

# 3️⃣2️⃣ Covering Index কী?

Advanced concept।

ধরো query:

```sql
SELECT customer_id, order_date
FROM orders
WHERE customer_id = 10;
```

যদি index:

```sql
CREATE INDEX idx_customer_date
ON orders(customer_id, order_date);
```

থাকে, তাহলে index-এর মধ্যেই query-এর প্রয়োজনীয় columns থাকতে পারে।

এমন situation-কে সাধারণভাবে:

> **Covering Index**

বলা হয়।

তখন database-কে মূল table row-এ ফিরে যেতে নাও হতে পারে।

এতে কিছু query আরও efficient হতে পারে।

---

# 3️⃣3️⃣ EXPLAIN — আজকের সবচেয়ে Important Tool 🔥

Index তৈরি করলেই কাজ শেষ নয়।

আমাদের দেখতে হবে:

> Database আসলে index ব্যবহার করছে কি না?

এর জন্য:

```sql
EXPLAIN
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

---

# 3️⃣4️⃣ EXPLAIN কী করে?

`EXPLAIN` query-এর execution plan সম্পর্কে information দেয়।

অর্থাৎ database query execute করার জন্য কী strategy নিতে পারে তা বুঝতে সাহায্য করে।

---

# 3️⃣5️⃣ EXPLAIN-এ Important Columns

MySQL-এ তুমি এগুলো দেখতে পারো:

```text
type
possible_keys
key
key_len
rows
Extra
```

সব এখন মুখস্থ করার দরকার নেই।

আজ important:

### `possible_keys`

কোন index ব্যবহার করা যেতে পারে।

### `key`

Actually কোন index choose করা হয়েছে।

### `rows`

Optimizer আনুমানিক কত rows examine করতে হতে পারে।

### `type`

Access strategy সম্পর্কে ধারণা দেয়।

---

# 3️⃣6️⃣ Example

Index:

```sql
CREATE INDEX idx_email
ON customers(email);
```

তারপর:

```sql
EXPLAIN
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

যদি:

```text
possible_keys → idx_email
key           → idx_email
```

দেখো, তাহলে optimizer index ব্যবহার করছে।

---

# 3️⃣7️⃣ Full Table Scan

যদি index না থাকে:

```text
Table
↓
Read many/all rows
↓
Check condition
```

এটাকে broadly:

> **Full Table Scan**

বলা হয়।

EXPLAIN-এ MySQL-এ `type = ALL` অনেক সময় full table scan নির্দেশ করে।

কিন্তু `ALL` দেখলেই সবসময় query খারাপ—এমন নয়।

যদি table ছোট হয়, full scan কখনো index lookup-এর চেয়ে efficient হতে পারে।

---

# 3️⃣8️⃣ Index Scan সবসময় Fast?

❌ না।

এটা খুব important।

ধরো table:

```text
100 rows
```

এবং query:

```sql
SELECT *
FROM employees;
```

এখানে index ব্যবহার করার কোনো দরকার নেই।

Database সরাসরি table পড়তে পারে।

---

# 3️⃣9️⃣ Selectivity

একটি index কতটা useful হতে পারে সেটা বোঝার জন্য **selectivity** গুরুত্বপূর্ণ।

ধরো:

```text
1,000,000 rows
```

Email:

```text
999,000 different values
```

খুব selective।

কিন্তু:

```text
status = active/inactive
```

শুধু 2 values।

কম selective।

তবে আবার বলি:

> Low selectivity ≠ useless index.

Actual workload এবং execution plan দেখতে হবে।

---

# 4️⃣0️⃣ Index Design-এর Golden Rule

❌ ভুল approach:

```text
"এই table-এ 20টা column আছে,
সব column-এ index বানাই।"
```

✅ ভালো approach:

```text
Query Pattern
     ↓
WHERE?
JOIN?
ORDER BY?
GROUP BY?
     ↓
Candidate Index
     ↓
EXPLAIN
     ↓
Measure
     ↓
Keep / Change / Remove
```

---

# 4️⃣1️⃣ Real-world Example

ধরো তোমার hotel management system:

```text
rooms
---------
room_id
hotel_id
room_type
price
status
```

Frequently query:

```sql
SELECT *
FROM rooms
WHERE hotel_id = 10
  AND status = 'available';
```

Potential index:

```sql
CREATE INDEX idx_rooms_hotel_status
ON rooms(hotel_id, status);
```

তারপর:

```sql
EXPLAIN
SELECT *
FROM rooms
WHERE hotel_id = 10
  AND status = 'available';
```

দিয়ে verify করবে।

---

# 4️⃣2️⃣ Database Designer Mindset 🔥

একজন beginner ভাবে:

> "Query কাজ করছে।"

একজন database designer ভাবে:

> "Query 10 rows-এর উপর কাজ করছে, নাকি 10 million rows scan করছে?"

আর production database-এ এই difference বিশাল।

---

# 4️⃣3️⃣ Indexing + Your Data Engineer Goal

তুমি যেহেতু Database Designer/Data Engineering-এর দিকে যেতে চাচ্ছো, এই flowটা মনে রাখো:

```text
Database Design
      ↓
Tables
      ↓
Relationships
      ↓
Queries
      ↓
Indexes
      ↓
EXPLAIN
      ↓
Optimization
```

এটাই আমাদের পরের class-এর foundation।

---

# 4️⃣4️⃣ Common Beginner Mistakes

### ❌ 1. সব column index করা

Index-এর storage এবং write cost আছে।

---

### ❌ 2. Duplicate index

যেমন:

```text
INDEX(email)
UNIQUE INDEX(email)
```

একই উদ্দেশ্যে unnecessary duplicate structure তৈরি করা উচিত নয়।

---

### ❌ 3. Composite index-এর order ignore করা

```text
(department, city)
```

এবং:

```text
(city, department)
```

এক নয়।

---

### ❌ 4. EXPLAIN না দেখা

Index তৈরি করে ধরে নেওয়া:

> "অবশ্যই database এটা ব্যবহার করছে।"

ভুল।

---

### ❌ 5. Small table-এ blindly index

Small table-এর full scan কখনো faster হতে পারে।

---

### ❌ 6. Index মানেই সব query fast

না।

> **Correct index + correct query pattern + good execution plan = performance improvement**

---

# 🧠 Class 50 Golden Cheat Sheet

```text
INDEX
↓
Fast data lookup

CREATE INDEX
↓
Create normal index

UNIQUE INDEX
↓
Uniqueness + index

COMPOSITE INDEX
↓
Multiple columns

PRIMARY KEY
↓
Indexed key; InnoDB uses it as clustered index

NEW/OLD
↓
Trigger concept

EXPLAIN
↓
Check query execution plan
```

### Most Important:

```text
More Index ≠ Always Better

Good Index
=
Query Pattern
+
Data Distribution
+
Workload
+
EXPLAIN
```

---

# 📝 Class 50 Assignment

ধরো:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(255),
    city VARCHAR(50),
    status VARCHAR(20),
    created_at DATE
);
```

### Q1

`email`-এর উপর একটি index তৈরি করো।

### Q2

`email` unique করার জন্য Unique Index তৈরি করো।

### Q3

`city` এবং `status` নিয়ে একটি composite index তৈরি করো।

### Q4

নিচের query-এর জন্য suitable index design করো:

```sql
SELECT *
FROM customers
WHERE city = 'Dhaka'
AND status = 'active';
```

### Q5 ⭐

এই query-এর execution plan দেখাও:

```sql
EXPLAIN
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

এবং explain করো:

```text
possible_keys
key
rows
type
```

### Q6 ⭐

কেন excessive indexes `INSERT`, `UPDATE`, `DELETE` slow করতে পারে?

---

# 🧪 Class 50 MCQ

**1. Index-এর প্রধান উদ্দেশ্য কী?**

A. Data delete করা  
B. Query/data retrieval দ্রুত করতে সাহায্য করা  
C. Table তৈরি করা  
D. Backup নেওয়া

**2. Index তৈরি করতে কোন command?**

A. `MAKE INDEX`  
B. `CREATE INDEX`  
C. `BUILD INDEX ONLY`  
D. `NEW INDEX`

**3. Composite Index কী?**

A. Multiple tables  
B. Multiple databases  
C. Multiple columns-এর index  
D. Multiple users

**4. `(department, city)` composite index-এর ক্ষেত্রে কোন column first?**

A. city  
B. department  
C. দুটোই একই  
D. কোনোটিই নয়

**5. Query execution plan দেখতে?**

A. `PLAN`  
B. `EXPLAIN`  
C. `SHOW QUERY`  
D. `CHECK QUERY`

**6. কোন operation-এর উপর excessive indexes performance cost তৈরি করতে পারে?**

A. INSERT  
B. UPDATE  
C. DELETE  
D. All of the above

**7. `INSERT` trigger-এ কোনটি available?**

A. OLD  
B. NEW  
C. OLD + NEW  
D. None

**8. InnoDB-তে primary key-এর সাথে কোন concept strongly associated?**

A. Clustered index  
B. Trigger  
C. View  
D. CTE

**9. কোনটি true?**

A. More indexes always means faster database  
B. Index has no storage cost  
C. Index can improve reads but adds maintenance cost  
D. Index only works for DELETE

**10. `WHERE city = 'Dhaka'` query-এর জন্য `(department, city)` index সম্পর্কে কোন statement সবচেয়ে সঠিক?**

A. অবশ্যই পুরো index ব্যবহার করবে  
B. সাধারণত leading column না থাকায় এর সুবিধা সীমিত হতে পারে  
C. এটি city index-এর সমান  
D. এটি অবশ্যই query-কে slower করবে

---

## 🎯 আজকের ৫টা Golden Line

```text
1. Index = Faster data retrieval-এর জন্য data structure

2. Primary Key সাধারণত indexed

3. Composite Index-এ column order গুরুত্বপূর্ণ

4. More Index ≠ Always Better

5. EXPLAIN = Query কীভাবে execute হচ্ছে তা বোঝার প্রধান tool
```

**Next → Class 51: SQL Query Optimization + `EXPLAIN` Deep Dive** — `type`, `key`, `rows`, `Extra`, Full Table Scan, Index Scan, Composite Index optimization, slow query diagnosis এবং practical performance tuning।


----
# 📘 Class 51 — SQL Query Optimization + EXPLAIN Deep Dive

আজকের ক্লাসটা **Database Designer / Data Engineer** হওয়ার জন্য খুব important।

Class 50-এ আমরা শিখেছি **Index**।  
আজ শিখব:

> **Query slow কেন? কোন index ব্যবহার করছে? Database কীভাবে query execute করছে? কীভাবে query fast করব?**

---

# 1. Query Optimization কী?

ধরো তোমার database-এ **10 million rows** আছে।

তুমি লিখলে:

```sql
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

Database-এর সামনে দুইটা রাস্তা থাকতে পারে:

### Option A — Full Table Scan

```text
Row 1 → check
Row 2 → check
Row 3 → check
...
Row 10,000,000 → check
```

খুব slow হতে পারে।

### Option B — Index ব্যবহার

যদি `email`-এ index থাকে:

```sql
CREATE INDEX idx_customer_email
ON customers(email);
```

তাহলে database index ব্যবহার করে দ্রুত matching row খুঁজতে পারে।

```text
Index
  ↓
rahim@gmail.com
  ↓
Customer row
```

এটাই Query Optimization-এর basic idea।

---

# 2. EXPLAIN কী?

SQL query চালানোর আগে আমরা database-কে জিজ্ঞেস করতে পারি:

> "এই query তুমি কীভাবে execute করবে?"

এর জন্য:

```sql
EXPLAIN
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

এটা query-এর **execution plan** দেখাবে।

---

# 3. EXPLAIN কেন গুরুত্বপূর্ণ?

ধরো query:

```sql
SELECT *
FROM orders
WHERE customer_id = 10;
```

তুমি ভাবতে পারো index ব্যবহার হচ্ছে।

কিন্তু database হয়তো বলছে:

```text
Full Table Scan
```

অর্থাৎ index থাকলেও optimizer সেটি ব্যবহার না-ও করতে পারে।

তাই:

```text
Query লিখলাম
      ↓
EXPLAIN
      ↓
Execution Plan দেখলাম
      ↓
Problem identify
      ↓
Index / Query optimize
```

---

# 4. EXPLAIN-এর গুরুত্বপূর্ণ Columns

MySQL-এ `EXPLAIN` করলে অনেক column দেখা যায়।

সবচেয়ে important:

|Column|Meaning|
|---|---|
|id|Query block identifier|
|select_type|Query type|
|table|কোন table access করছে|
|partitions|Partition information|
|type|কী ধরনের access হচ্ছে|
|possible_keys|কোন index ব্যবহার করা সম্ভব|
|key|কোন index actually ব্যবহার করছে|
|key_len|index-এর কত অংশ ব্যবহার করছে|
|ref|কোন value/column-এর সাথে match করছে|
|rows|আনুমানিক কত row examine করবে|
|filtered|কত % row filter pass করবে|
|Extra|অতিরিক্ত execution information|

আজ সবচেয়ে important:

> `type`, `possible_keys`, `key`, `rows`, `Extra`

---

# 5. `type` — সবচেয়ে গুরুত্বপূর্ণ

`type` দেখে আমরা বুঝতে পারি database কী ধরনের access করছে।

সাধারণভাবে ভালো থেকে খারাপের দিকে:

```text
system
const
eq_ref
ref
range
index
ALL
```

সবসময় এই ranking blindly apply করবে না, কিন্তু basic diagnosis-এর জন্য useful।

---

# 6. `type = ALL`

এটা সাধারণত:

> **Full Table Scan**

উদাহরণ:

```sql
SELECT *
FROM customers
WHERE city = 'Dhaka';
```

যদি `city`-তে index না থাকে, database অনেক row scan করতে পারে।

EXPLAIN:

```text
type = ALL
```

মানে:

```text
পুরো table scan করার সম্ভাবনা
```

⚠️ তবে ছোট table হলে `ALL` দেখালেই panic করার দরকার নেই।

যেমন:

```text
customers = 50 rows
```

৫০টা row scan করা অনেক সময় index lookup-এর চেয়েও practical হতে পারে।

---

# 7. `type = const`

খুব efficient access।

সাধারণত primary key বা unique indexed value দিয়ে একটি row খুঁজলে।

```sql
SELECT *
FROM customers
WHERE customer_id = 10;
```

যদি:

```sql
customer_id PRIMARY KEY
```

হয়, optimizer খুব দ্রুত row locate করতে পারে।

Concept:

```text
Primary Key
     ↓
customer_id = 10
     ↓
One row
```

---

# 8. `type = eq_ref`

এটা বিশেষ করে JOIN-এর ক্ষেত্রে দেখা যায়।

উদাহরণ:

```sql
SELECT *
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id;
```

যদি `customers.customer_id` primary key হয়, প্রতিটি order-এর জন্য একটি নির্দিষ্ট customer row পাওয়া যায়।

এটা সাধারণত efficient JOIN access।

---

# 9. `type = ref`

Non-unique index দিয়ে matching rows খোঁজার ক্ষেত্রে `ref` দেখা যায়।

ধরো:

```sql
CREATE INDEX idx_customer_city
ON customers(city);
```

তারপর:

```sql
SELECT *
FROM customers
WHERE city = 'Dhaka';
```

একাধিক customer Dhaka-তে থাকতে পারে।

তাই:

```text
city index
   ↓
Dhaka
   ↓
multiple rows
```

এখানে `ref` দেখা যেতে পারে।

---

# 10. `type = range`

Range condition-এর জন্য।

যেমন:

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
  AND order_date < '2026-02-01';
```

অথবা:

```sql
WHERE price BETWEEN 1000 AND 5000
```

Index থাকলে:

```text
range scan
```

হতে পারে।

---

# 11. `possible_keys`

এটা বলে:

> এই query-এর জন্য কোন কোন index ব্যবহার করা সম্ভব?

উদাহরণ:

```text
possible_keys:
idx_customer_email
```

কিন্তু গুরুত্বপূর্ণ বিষয়:

**possible_keys মানেই index ব্যবহার করেছে না।**

---

# 12. `key`

এটা আরও important।

`key` বলে:

> Database শেষ পর্যন্ত কোন index ব্যবহার করেছে?

ধরো:

```text
possible_keys = idx_email
key           = idx_email
```

তাহলে index actually ব্যবহার করেছে।

কিন্তু:

```text
possible_keys = idx_email
key           = NULL
```

মানে index available ছিল, কিন্তু optimizer ব্যবহার করেনি।

---

# 13. `possible_keys` বনাম `key`

মনে রাখো:

```text
possible_keys
     ↓
Could use

key
     ↓
Actually used
```

এটা interview-তে খুব useful।

---

# 14. `rows`

`rows` হলো optimizer-এর estimated number of rows যা examine করতে হতে পারে।

ধরো:

```text
rows = 1000000
```

তাহলে query potentially অনেক rows examine করছে।

আর:

```text
rows = 1
```

সাধারণত ভালো sign।

⚠️ এটা exact result count নয়।

এটা **optimizer-এর estimate**।

---

# 15. `Extra`

`Extra` অনেক useful information দেয়।

Common values:

```text
Using where
Using index
Using temporary
Using filesort
```

---

# 16. `Using where`

Example:

```sql
SELECT *
FROM customers
WHERE city = 'Dhaka';
```

Database additional filtering করছে।

এটা নিজে থেকেই bad না।

---

# 17. `Using index`

এটা অনেক সময় ভালো sign।

মানে query-এর প্রয়োজনীয় data index থেকেই পাওয়া যাচ্ছে।

এটাকে **covering index** situation-এর সাথে সম্পর্কিত করা যায়।

Example:

```sql
CREATE INDEX idx_city_name
ON customers(city, customer_name);
```

Query:

```sql
SELECT customer_name
FROM customers
WHERE city = 'Dhaka';
```

Index-এর মধ্যেই দরকারি information থাকতে পারে।

---

# 18. `Using filesort`

নাম দেখে ভয় পাওয়ার দরকার নেই।

এটা সাধারণত বলে database-কে sorting-এর জন্য additional work করতে হচ্ছে।

Example:

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

যদি appropriate index না থাকে, sorting করতে extra work হতে পারে।

Large dataset-এ এটি expensive হতে পারে।

---

# 19. `Using temporary`

কিছু query intermediate temporary structure ব্যবহার করতে পারে।

বিশেষ করে complex:

```sql
GROUP BY
ORDER BY
DISTINCT
```

এর combination-এ দেখা যেতে পারে।

Example:

```sql
SELECT department, COUNT(*)
FROM employees
GROUP BY department
ORDER BY COUNT(*) DESC;
```

`Using temporary` দেখালেই query অবশ্যই bad—এমন না।

---

# 20. সবচেয়ে common optimization mistake

ধরো:

```sql
SELECT *
FROM customers
WHERE YEAR(created_at) = 2026;
```

এখানে `created_at` indexed হলেও function ব্যবহার করার কারণে index-এর সুবিধা কমে যেতে পারে।

Better:

```sql
SELECT *
FROM customers
WHERE created_at >= '2026-01-01'
  AND created_at < '2027-01-01';
```

এটাকে বলা হয় **Sargability**-এর basic idea।

---

# 21. Sargability কী?

সহজভাবে:

> এমনভাবে condition লেখা যাতে database index efficiently ব্যবহার করতে পারে।

### Less index-friendly

```sql
WHERE YEAR(order_date) = 2026
```

### More index-friendly

```sql
WHERE order_date >= '2026-01-01'
  AND order_date < '2027-01-01'
```

Golden Rule:

> **Indexed column-এর উপর unnecessary function প্রয়োগ না করাই ভালো।**

---

# 22. আরেকটি common mistake — `SELECT *`

ধরো:

```sql
SELECT *
FROM customers
WHERE email = 'a@gmail.com';
```

কিন্তু তোমার দরকার শুধু:

```text
customer_id
customer_name
```

তাহলে:

```sql
SELECT customer_id, customer_name
FROM customers
WHERE email = 'a@gmail.com';
```

Better।

কারণ:

```text
SELECT *
    ↓
unnecessary columns
    ↓
more data transfer
    ↓
more I/O
```

বিশেষ করে large table এবং application/API response-এর ক্ষেত্রে গুরুত্বপূর্ণ।

---

# 23. WHERE দিয়ে আগে Filter করা

ধরো:

```sql
SELECT
    c.city,
    SUM(o.quantity * p.price)
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id
GROUP BY c.city;
```

যদি তোমার দরকার শুধু 2026 সালের orders:

```sql
SELECT
    c.city,
    SUM(o.quantity * p.price)
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id
WHERE o.order_date >= '2026-01-01'
  AND o.order_date < '2027-01-01'
GROUP BY c.city;
```

এতে unnecessary rows processing কমতে পারে।

---

# 24. JOIN Optimization

ধরো:

```sql
SELECT *
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id;
```

Important columns:

```text
orders.customer_id
customers.customer_id
```

সঠিক indexing JOIN দ্রুত করতে সাহায্য করতে পারে।

বিশেষ করে:

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

এবং `customers.customer_id` যদি primary key হয়, সেখানে already index থাকে।

---

# 25. Composite Index Optimization

আগের class-এ শিখেছিলাম:

```sql
CREATE INDEX idx_customer_date
ON orders(customer_id, order_date);
```

এখানে:

```text
1st → customer_id
2nd → order_date
```

এখন:

### Query A

```sql
WHERE customer_id = 10
```

✅ ভালো candidate

### Query B

```sql
WHERE customer_id = 10
AND order_date >= '2026-01-01'
```

✅ আরও ভালো use case

### Query C

```sql
WHERE order_date >= '2026-01-01'
```

⚠️ এই index-এর জন্য সাধারণত ideal use case নয়, কারণ প্রথম column `customer_id` বাদ গেছে।

এটাই **Leftmost Prefix Rule**-এর basic idea।

---

# 26. ORDER BY Optimization

Query:

```sql
SELECT *
FROM orders
ORDER BY order_date DESC
LIMIT 10;
```

যদি appropriate index থাকে:

```sql
CREATE INDEX idx_order_date
ON orders(order_date);
```

তাহলে database sorting work কমাতে পারে।

এখানে:

```sql
LIMIT 10
```

খুব useful হতে পারে।

কারণ তোমার দরকার মাত্র ১০টা row।

---

# 27. LIMIT Optimization

ধরো:

```sql
SELECT *
FROM products
ORDER BY price DESC;
```

তুমি সব products চাও না।

শুধু top 10:

```sql
SELECT *
FROM products
ORDER BY price DESC
LIMIT 10;
```

এতে application-এর জন্য unnecessary rows return করা কমে।

---

# 28. Query Optimization-এর একটা Real Example

ধরো table:

```text
orders
```

Rows:

```text
10,000,000
```

Query:

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026;
```

### Problem

`YEAR()` function ব্যবহার করছি।

### Better

```sql
SELECT order_id, customer_id, order_date, quantity
FROM orders
WHERE order_date >= '2026-01-01'
  AND order_date < '2027-01-01';
```

আর index:

```sql
CREATE INDEX idx_orders_date
ON orders(order_date);
```

তারপর:

```sql
EXPLAIN
SELECT order_id, customer_id, order_date, quantity
FROM orders
WHERE order_date >= '2026-01-01'
  AND order_date < '2027-01-01';
```

তারপর execution plan দেখে সিদ্ধান্ত নেব।

---

# 29. Query Optimization Workflow

একজন Database Engineer হিসেবে workflow হবে:

```text
Slow Query
    ↓
EXPLAIN
    ↓
Check type
    ↓
Check possible_keys
    ↓
Check key
    ↓
Check rows
    ↓
Check Extra
    ↓
Identify bottleneck
    ↓
Optimize Query / Index
    ↓
EXPLAIN Again
    ↓
Compare
```

এটা খুব important workflow।

---

# 30. শুধু Index দিলেই হবে?

❌ না।

ধরো:

```sql
CREATE INDEX idx_name
ON customers(name);
```

তারপর:

```sql
WHERE age = 25
```

এই index কোনো সাহায্য করবে না।

কারণ query condition:

```text
age
```

কিন্তু index:

```text
name
```

---

# 31. বেশি Index দিলেই Query Fast?

❌ না।

ধরো:

```text
10টা index
20টা index
30টা index
```

প্রতিটা index-এর:

```text
Storage cost
+
INSERT cost
+
UPDATE cost
+
DELETE maintenance
```

আছে।

তাই:

> **Index strategically তৈরি করতে হয়।**

---

# 32. Query Optimization-এর Golden Rules ⭐

### Rule 1

```text
EXPLAIN first
```

Guess করো না।

### Rule 2

```text
possible_keys ≠ actual key
```

`key` দেখো।

### Rule 3

```text
rows কমানো important
```

### Rule 4

Unnecessary:

```sql
SELECT *
```

avoid করো।

### Rule 5

Indexed column-এর উপর unnecessary function avoid করো।

### Rule 6

Composite index-এর column order গুরুত্বপূর্ণ।

### Rule 7

সব query-তে index দরকার নেই।

### Rule 8

Optimization করার পরে আবার:

```sql
EXPLAIN
```

করো।

---

# 🧠 Class 51 Cheat Sheet

```text
EXPLAIN
   ↓
Execution Plan

type
   ↓
Access method

possible_keys
   ↓
Possible indexes

key
   ↓
Actually used index

rows
   ↓
Estimated rows examined

Extra
   ↓
Additional execution information
```

### Important `type`

```text
const
eq_ref
ref
range
index
ALL
```

বিশেষভাবে মনে রাখবে:

```text
ALL = Full Table Scan
range = Range scan
ref = Indexed lookup with multiple possible matches
const = Very efficient single-row lookup
```

---

# 🎯 Practice Assignment

ধরো:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10,2)
);
```

### Task 1

`customer_id` দিয়ে search করার জন্য index তৈরি করো।

### Task 2

`order_date` দিয়ে search করার জন্য index তৈরি করো।

### Task 3

এই query-এর EXPLAIN লিখো:

```sql
SELECT *
FROM orders
WHERE customer_id = 100;
```

### Task 4

এই query optimize করো:

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026;
```

### Task 5

এই query-এর জন্য suitable composite index চিন্তা করো:

```sql
SELECT *
FROM orders
WHERE customer_id = 100
AND order_date >= '2026-01-01'
AND order_date < '2026-02-01';
```

---

# 📝 MCQ

**1. `EXPLAIN` কী দেখায়?**

A. Table data  
B. Query execution plan  
C. Database password  
D. Backup

**2. `key` কী নির্দেশ করে?**

A. Possible index  
B. Actually used index  
C. Primary key only  
D. Foreign key

**3. `type = ALL` সাধারণত কী বোঝায়?**

A. Index lookup  
B. Full table scan  
C. Unique lookup  
D. Range lookup

**4. কোনটি সাধারণত index-friendly?**

A.

```sql
WHERE YEAR(order_date) = 2026
```

B.

```sql
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01'
```

**5. Composite index:**

```sql
(customer_id, order_date)
```

এর ক্ষেত্রে কোন query সবচেয়ে natural use case?

A.

```sql
WHERE order_date = '2026-01-01'
```

B.

```sql
WHERE customer_id = 10
AND order_date = '2026-01-01'
```

C. কোনোটাই না

---

### ⭐ আজকের সবচেয়ে গুরুত্বপূর্ণ concept

```text
Index তৈরি করা
      ≠
Query optimized হওয়া

EXPLAIN
      ↓
Database কী করছে দেখো
      ↓
Problem identify করো
      ↓
Query + Index optimize করো
      ↓
EXPLAIN আবার চালাও
```

**Class 52 হবে → Database Normalization (1NF, 2NF, 3NF, BCNF) — Database Designer হওয়ার জন্য খুব গুরুত্বপূর্ণ ক্লাস।**


----

# 📘 Class 52 — Database Normalization

আজকের ক্লাসটা **Database Designer** হওয়ার জন্য সবচেয়ে গুরুত্বপূর্ণ topics-এর একটি।

আমরা শিখব:

- Normalization কী?
    
- কেন দরকার?
    
- Data redundancy
    
- Update/Insert/Delete anomaly
    
- Functional Dependency
    
- 1NF
    
- 2NF
    
- 3NF
    
- BCNF
    
- Normalization কীভাবে step-by-step করতে হয়
    
- Real-world example
    
- Common mistakes
    
- Assignment + MCQ
    

---

# 1. Normalization কী?

সহজ ভাষায়:

> **Database-এর data এমনভাবে organize করা যাতে unnecessary duplication কমে এবং data consistency বজায় থাকে—এটাই Normalization।**

ধরো আমাদের table:

|StudentID|StudentName|Course|Teacher|TeacherPhone|
|---|---|---|---|---|
|1|Atiar|Database|Rahim|01711|
|2|Karim|Database|Rahim|01711|
|3|Nila|SQL|Hasan|01822|

এখানে:

```text
Database → Rahim → 01711
```

বারবার duplicate হচ্ছে।

আর:

```text
SQL → Hasan → 01822
```

এটাও repeat হতে পারে।

এটাই **data redundancy**।

---

# 2. Data Redundancy কী?

একই information unnecessarily বারবার store হওয়া।

Example:

```text
Student 1 → Database → Rahim → 01711
Student 2 → Database → Rahim → 01711
Student 3 → Database → Rahim → 01711
Student 4 → Database → Rahim → 01711
```

`Rahim` এবং `01711` বারবার এসেছে।

Problem:

```text
More duplicate data
        ↓
More storage
        ↓
More update problems
        ↓
Inconsistency
```

---

# 3. Normalization কেন দরকার?

মূল উদ্দেশ্য:

### 1. Redundancy কমানো

### 2. Data consistency বজায় রাখা

### 3. Update anomaly কমানো

### 4. Insert anomaly কমানো

### 5. Delete anomaly কমানো

---

# 4. Anomaly কী?

Database-এ ভুল/অস্বাভাবিক data operation-এর সমস্যা।

তিনটি famous anomaly:

```text
1. Update Anomaly
2. Insert Anomaly
3. Delete Anomaly
```

এগুলো exam-এ খুব common।

---

# 5. Update Anomaly

ধরো:

|Student|Course|Teacher|Phone|
|---|---|---|---|
|Atiar|DBMS|Rahim|01711|
|Karim|DBMS|Rahim|01711|
|Nila|DBMS|Rahim|01711|

Rahim-এর phone number পরিবর্তন হলো:

```text
01711 → 01999
```

তাহলে ৩টি row update করতে হবে।

যদি ভুল করে:

```text
Row 1 → 01999
Row 2 → 01999
Row 3 → 01711
```

হয়ে যায়?

একই teacher-এর দুইটা phone number হয়ে গেল!

এটাই **Update Anomaly**।

---

# 6. Insert Anomaly

ধরো Course table-এর তথ্য:

|Student|Course|Teacher|
|---|---|---|
|Atiar|DBMS|Rahim|
|Karim|DBMS|Rahim|

এখন নতুন course:

```text
Python
Teacher = Hasan
```

কিন্তু এখনো কোনো student Python course নেয়নি।

আমাদের table-এ Student column required হলে কীভাবে শুধু:

```text
Python → Hasan
```

insert করব?

পারছি না।

অর্থাৎ:

> নতুন information insert করতে অন্য unrelated information প্রয়োজন হচ্ছে।

এটাই **Insert Anomaly**।

---

# 7. Delete Anomaly

ধরো:

|Student|Course|Teacher|
|---|---|---|
|Atiar|DBMS|Rahim|
|Karim|DBMS|Rahim|
|Nila|Python|Hasan|

এখন Nila Python course থেকে চলে গেল।

আমরা Nila-এর row delete করলাম।

```text
Nila → Python → Hasan
```

তাহলে Python course সম্পর্কে একমাত্র information-ও চলে গেল।

অর্থাৎ:

> একটি unrelated record delete করার কারণে দরকারি information হারিয়ে গেল।

এটাই **Delete Anomaly**।

---

# 8. Normalization-এর Main Idea

আমরা বড় table:

```text
One giant table
```

কে logically ছোট ছোট table-এ ভাগ করি।

Example:

### Students

|student_id|student_name|
|---|---|
|1|Atiar|
|2|Karim|

### Courses

|course_id|course_name|teacher_id|
|---|---|---|
|101|DBMS|1|
|102|Python|2|

### Teachers

|teacher_id|teacher_name|phone|
|---|---|---|
|1|Rahim|01711|
|2|Hasan|01822|

### Enrollment

|student_id|course_id|
|---|---|
|1|101|
|2|101|
|1|102|

এখন duplicate কমেছে।

---

# 9. Normal Forms

Normalization-এর বিভিন্ন level আছে:

```text
UNF
 ↓
1NF
 ↓
2NF
 ↓
3NF
 ↓
BCNF
```

সবচেয়ে commonly discussed:

> **1NF → 2NF → 3NF**

---

# 10. 1NF — First Normal Form

1NF-এর basic rule:

> **প্রতিটি cell-এ atomic/single value থাকতে হবে।**

অর্থাৎ এক cell-এ multiple values রাখা যাবে না।

---

## ❌ Not 1NF

|StudentID|Name|Phone|
|---|---|---|
|1|Atiar|01711, 01822|

একটি cell-এ:

```text
01711, 01822
```

দুইটা value।

এটা atomic না।

---

## ✅ 1NF

|StudentID|Name|Phone|
|---|---|---|
|1|Atiar|01711|
|1|Atiar|01822|

প্রতিটি cell-এ single value।

---

# 11. আরেকটি 1NF Example

❌

|Student|Courses|
|---|---|
|Atiar|DBMS, SQL, Python|

Courses cell-এ multiple values।

1NF করতে:

|Student|Course|
|---|---|
|Atiar|DBMS|
|Atiar|SQL|
|Atiar|Python|

---

# ⭐ 1NF Golden Rule

```text
One Cell
   ↓
One Atomic Value
```

---

# 12. কিন্তু 1NF-এর সমস্যা কী?

1NF করলাম:

|StudentID|CourseID|StudentName|CourseName|Teacher|
|---|---|---|---|---|
|1|101|Atiar|DBMS|Rahim|
|1|102|Atiar|SQL|Hasan|
|2|101|Karim|DBMS|Rahim|

এখন:

```text
Atiar → Atiar
DBMS → DBMS
Rahim → Rahim
```

আবার repeat হচ্ছে।

এখন আসবে **2NF**।

---

# 13. Functional Dependency

2NF বোঝার আগে Functional Dependency বুঝতে হবে।

ধরো:

```text
StudentID → StudentName
```

এর অর্থ:

> StudentID জানা থাকলে StudentName uniquely determine করা যায়।

Example:

```text
StudentID = 1
      ↓
StudentName = Atiar
```

তাই:

```text
StudentID → StudentName
```

---

# 14. Functional Dependency Example

ধরো:

|StudentID|StudentName|
|---|---|
|1|Atiar|
|2|Karim|

এখানে:

```text
StudentID → StudentName
```

কিন্তু:

```text
StudentName → StudentID
```

সবসময় valid নাও হতে পারে।

কারণ দুইজন student-এর নাম একই হতে পারে।

---

# 15. Determinant কী?

Functional Dependency:

```text
A → B
```

এখানে:

> `A` হলো **determinant**।

Example:

```text
StudentID → StudentName
```

এখানে:

```text
StudentID = Determinant
```

---

# 16. 2NF — Second Normal Form

2NF-এর জন্য table-কে:

### Condition 1

1NF হতে হবে।

### Condition 2

**Partial Dependency থাকতে পারবে না।**

এখন প্রশ্ন:

> Partial Dependency কী?

---

# 17. Composite Primary Key

ধরো Enrollment table:

|StudentID|CourseID|StudentName|CourseName|Grade|
|---|---|---|---|---|
|1|101|Atiar|DBMS|A|
|1|102|Atiar|SQL|B|
|2|101|Karim|DBMS|A|

Primary key:

```text
(StudentID, CourseID)
```

কারণ:

```text
StudentID alone
```

একটা enrollment uniquely identify করতে পারে না।

এবং:

```text
CourseID alone
```

এটাও পারে না।

কিন্তু:

```text
StudentID + CourseID
```

একটি enrollment uniquely identify করতে পারে।

---

# 18. Partial Dependency

এখন দেখো:

```text
(StudentID, CourseID) → Grade
```

ঠিক আছে।

কিন্তু:

```text
StudentID → StudentName
```

এখানে `StudentName` পুরো composite key-এর উপর depend করছে না।

শুধু:

```text
StudentID
```

এর উপর depend করছে।

এটাই:

> **Partial Dependency**

---

# 19. 2NF Violation

আমাদের table:

```text
(StudentID, CourseID, StudentName, CourseName, Grade)
```

Dependencies:

```text
StudentID → StudentName

CourseID → CourseName

(StudentID, CourseID) → Grade
```

তাই:

```text
StudentName
CourseName
```

partial dependency তৈরি করছে।

❌ Table 2NF-এ নেই।

---

# 20. 2NF করতে কী করব?

Table ভেঙে দেব।

### Students

|StudentID|StudentName|
|---|---|
|1|Atiar|
|2|Karim|

### Courses

|CourseID|CourseName|
|---|---|
|101|DBMS|
|102|SQL|

### Enrollment

|StudentID|CourseID|Grade|
|---|---|---|
|1|101|A|
|1|102|B|
|2|101|A|

এখন:

```text
StudentID → StudentName
CourseID → CourseName
(StudentID, CourseID) → Grade
```

Partial dependency নেই।

✅ 2NF।

---

# ⭐ 2NF Golden Rule

> **1NF + No Partial Dependency**

আরেকটা important shortcut:

> **2NF problem সাধারণত composite primary key থাকলেই দেখা যায়।**

যদি primary key single column হয়, partial dependency সাধারণত থাকে না।

---

# 21. 3NF — Third Normal Form

3NF-এর জন্য:

### Condition 1

Table অবশ্যই 2NF হতে হবে।

### Condition 2

**Transitive Dependency থাকতে পারবে না।**

এখন Transitive Dependency কী?

---

# 22. Transitive Dependency

ধরো:

```text
StudentID → DepartmentID
DepartmentID → DepartmentName
```

তাহলে indirectly:

```text
StudentID → DepartmentName
```

হচ্ছে।

অর্থাৎ:

```text
StudentID
    ↓
DepartmentID
    ↓
DepartmentName
```

এটাই **Transitive Dependency**।

---

# 23. 3NF Example

ধরো:

|StudentID|StudentName|DepartmentID|DepartmentName|
|---|---|---|---|
|1|Atiar|10|CSE|
|2|Karim|10|CSE|
|3|Nila|20|EEE|

Dependencies:

```text
StudentID → StudentName
StudentID → DepartmentID

DepartmentID → DepartmentName
```

তাই:

```text
StudentID → DepartmentID → DepartmentName
```

এখানে `DepartmentName` student-এর উপর directly depend করছে না।

এটা DepartmentID-এর উপর depend করছে।

❌ Transitive dependency।

---

# 24. 3NF করতে কী করব?

দুইটি table:

### Students

|StudentID|StudentName|DepartmentID|
|---|---|---|
|1|Atiar|10|
|2|Karim|10|
|3|Nila|20|

### Departments

|DepartmentID|DepartmentName|
|---|---|
|10|CSE|
|20|EEE|

এখন:

```text
DepartmentID → DepartmentName
```

Department information আলাদা table-এ।

✅ 3NF।

---

# ⭐ 3NF Golden Rule

```text
2NF
 +
No Transitive Dependency
 =
3NF
```

---

# 25. 1NF vs 2NF vs 3NF

|Normal Form|Main Problem|
|---|---|
|1NF|Multiple/non-atomic values|
|2NF|Partial dependency|
|3NF|Transitive dependency|

Shortcut:

```text
1NF → Atomic

2NF → No Partial Dependency

3NF → No Transitive Dependency
```

এটা অবশ্যই মুখস্থ রাখবে। ⭐

---

# 26. Complete Example

ধরো initial table:

|StudentID|StudentName|CourseID|CourseName|TeacherID|TeacherName|
|---|---|---|---|---|---|
|1|Atiar|101|DBMS|T1|Rahim|
|1|Atiar|102|SQL|T2|Hasan|
|2|Karim|101|DBMS|T1|Rahim|

Primary key:

```text
(StudentID, CourseID)
```

Dependencies:

```text
StudentID → StudentName

CourseID → CourseName
CourseID → TeacherID

TeacherID → TeacherName

(StudentID, CourseID) → Enrollment information
```

---

## Step 1 — 1NF

সব cell atomic।

তাই:

✅ 1NF

---

## Step 2 — 2NF

Problem:

```text
StudentID → StudentName
```

এবং:

```text
CourseID → CourseName
CourseID → TeacherID
```

এগুলো composite key-এর অংশের উপর depend করছে।

তাই table split:

### Students

```text
StudentID
StudentName
```

### Courses

```text
CourseID
CourseName
TeacherID
```

### Enrollment

```text
StudentID
CourseID
```

---

# Step 3 — 3NF

Courses table:

```text
CourseID → TeacherID

TeacherID → TeacherName
```

তাই:

```text
CourseID → TeacherID → TeacherName
```

Transitive dependency আছে।

তাই:

### Courses

|CourseID|CourseName|TeacherID|
|---|---|---|

### Teachers

|TeacherID|TeacherName|
|---|---|

Final structure:

```text
Students
   ↓
Enrollment
   ↓
Courses
   ↓
Teachers
```

এটাই normalized relational design-এর basic pattern।

---

# 27. Normalization এবং JOIN

অনেকে ভাবে:

> "Table ভেঙে ফেললে তো অনেক JOIN লাগবে!"

হ্যাঁ, JOIN লাগতে পারে।

কিন্তু normalization-এর লক্ষ্য:

```text
Data integrity
+
Less redundancy
+
Better maintainability
```

তারপর প্রয়োজন অনুযায়ী JOIN করা হয়।

Example:

```sql
SELECT
    s.student_name,
    c.course_name,
    t.teacher_name
FROM enrollment e
JOIN students s
    ON e.student_id = s.student_id
JOIN courses c
    ON e.course_id = c.course_id
JOIN teachers t
    ON c.teacher_id = t.teacher_id;
```

---

# 28. Normalization কি সবসময় যত বেশি সম্ভব করা উচিত?

❌ না।

Real-world database design-এ কখনো কখনো **denormalization** করা হয়।

কারণ অতিরিক্ত normalization করলে:

```text
Too many tables
      ↓
Too many JOINs
      ↓
Complex queries
      ↓
Potential performance cost
```

তাই practical database design-এ balance দরকার।

---

# 29. Normalization vs Denormalization

|Normalization|Denormalization|
|---|---|
|Redundancy কমায়|কিছু redundancy intentionally রাখে|
|Data integrity ভালো|Read performance improve করতে পারে|
|More tables হতে পারে|Fewer tables হতে পারে|
|JOIN বেশি হতে পারে|JOIN কম হতে পারে|
|OLTP systems-এ common|Analytics/read-heavy systems-এ useful হতে পারে|

---

# 30. BCNF — Boyce-Codd Normal Form

3NF-এর থেকেও stronger normal form হলো:

> **BCNF**

Basic rule:

> প্রতিটি non-trivial functional dependency `X → Y`-এর ক্ষেত্রে `X` অবশ্যই a **superkey** হতে হবে।

সহজভাবে:

```text
Every determinant
      ↓
Must be a candidate/super key
```

BCNF একটু advanced topic।

Exam-এর জন্য basic definition মনে রাখো।

---

# 🧠 Normalization Master Cheat Sheet

```text
Normalization
      ↓
Reduce redundancy
      ↓
Improve consistency
      ↓
Avoid anomalies
```

### Anomalies

```text
Update
Insert
Delete
```

### Normal Forms

```text
1NF
 ↓
Atomic values

2NF
 ↓
1NF + No Partial Dependency

3NF
 ↓
2NF + No Transitive Dependency

BCNF
 ↓
Every determinant is a superkey
```

---

# ⭐ সবচেয়ে গুরুত্বপূর্ণ Example

মনে রাখো:

```text
StudentID → StudentName
```

এটা Functional Dependency।

```text
(StudentID, CourseID) → Grade
```

Composite key-এর উপর full dependency।

```text
StudentID → StudentName
```

যদি key হয়:

```text
(StudentID, CourseID)
```

তাহলে এটা **Partial Dependency**।

আর:

```text
StudentID → DepartmentID
DepartmentID → DepartmentName
```

তাহলে:

```text
StudentID → DepartmentName
```

হলো **Transitive Dependency**।

---

# 📝 Class 52 Assignment

নিচের table দেখো:

|OrderID|ProductID|ProductName|CustomerID|CustomerName|CustomerCity|
|---|---|---|---|---|---|
|1|P1|Laptop|C1|Atiar|Dhaka|
|2|P2|Mouse|C1|Atiar|Dhaka|
|3|P1|Laptop|C2|Karim|Chittagong|

### তোমার কাজ:

**1.** এখানে কোন কোন data redundant?

**2.** Primary key কী হতে পারে?

**3.** Functional dependencies লিখো।

**4.** এখানে Partial Dependency আছে কি?

**5.** Transitive Dependency আছে কি?

**6.** Table-টি 3NF পর্যন্ত normalize করো।

**7.** Final tables-এর মধ্যে Primary Key এবং Foreign Key identify করো।

---

# 🎯 MCQ

**1. Normalization-এর প্রধান উদ্দেশ্য কী?**

A. Data redundancy বাড়ানো  
B. Data redundancy কমানো  
C. Database delete করা  
D. Query বন্ধ করা

**2. 1NF-এর প্রধান requirement কী?**

A. No transitive dependency  
B. No partial dependency  
C. Atomic values  
D. Foreign key বাধ্যতামূলক

**3. 2NF কী remove করে?**

A. Atomicity  
B. Partial dependency  
C. Transitive dependency  
D. Primary key

**4. 3NF কী remove করে?**

A. Partial dependency  
B. Transitive dependency  
C. Foreign key  
D. Composite key

**5. কোনটি Transitive Dependency?**

A.

```text
StudentID → StudentName
```

B.

```text
StudentID → DepartmentID
DepartmentID → DepartmentName
```

C.

```text
CourseID → CourseName
```

D.

```text
OrderID → OrderDate
```

**6. কোন anomaly-তে data update করার সময় inconsistent data হতে পারে?**

A. Insert  
B. Delete  
C. Update  
D. Select

---

## 🔥 Class 52-এর 5-line Revision

```text
1NF → Atomic values

2NF → 1NF + No Partial Dependency

3NF → 2NF + No Transitive Dependency

Normalization → Redundancy + Anomaly কমানো

BCNF → Every determinant should be a superkey
```

পরের ধাপে **Class 53 — Database Design + ER Diagram + Entity + Attribute + Relationship + Cardinality + Primary/Foreign Key** শেখা হবে।


----
# 📘 Class 53 — Database Design + ER Diagram

আজকের ক্লাসটা তোমার **Database Designer** goal-এর জন্য খুব গুরুত্বপূর্ণ।

Class 52-এ আমরা শিখেছি **Normalization**।  
আজ শিখব কীভাবে requirement থেকে actual database design তৈরি করতে হয়।

আজকের flow:

```text
Business Requirement
        ↓
Entities
        ↓
Attributes
        ↓
Relationships
        ↓
Cardinality
        ↓
Primary Key
        ↓
Foreign Key
        ↓
ER Diagram
        ↓
Normalized Tables
        ↓
SQL Tables
```

---

# 1. Database Design কী?

সহজভাবে:

> **কোন data কোথায় থাকবে, কোন table হবে, tableগুলোর মধ্যে কী relationship থাকবে—এগুলো পরিকল্পনা করাই Database Design।**

ধরো তুমি একটা **Hotel Management System** বানাবে।

Requirement:

```text
Customer hotel room booking করবে।
একজন customer অনেক booking করতে পারবে।
একটি room বিভিন্ন সময়ে অনেকবার booked হতে পারে।
প্রতিটি booking-এর একটি payment থাকতে পারে।
```

এখন সরাসরি SQL লিখে ফেললে ভুল হওয়ার সম্ভাবনা আছে।

আগে design:

```text
Customer
   ↓
Booking
   ↓
Room
```

তারপর:

```text
Booking → Payment
```

---

# 2. Entity কী?

> **যে real-world object বা concept সম্পর্কে আমরা data store করতে চাই, সেটাই Entity।**

Hotel system-এ:

```text
Customer
Room
Booking
Payment
Hotel
```

এগুলো Entity হতে পারে।

---

# 3. Entity-এর Real-world Example

ধরো University system:

```text
Student
Teacher
Course
Department
Enrollment
```

E-commerce:

```text
Customer
Product
Order
Payment
Category
Supplier
```

Hospital:

```text
Patient
Doctor
Appointment
Prescription
Department
```

---

# 4. Entity বনাম Table

Conceptually:

```text
Entity
   ↓
Database Table
```

যেমন:

```text
Customer
   ↓
customers table
```

তবে Entity আর table **একই concept নয়**।

Entity হলো design-level concept।

Table হলো database implementation।

---

# 5. Attribute কী?

> Entity-এর properties/information হলো Attribute।

Customer entity:

```text
Customer
 ├── customer_id
 ├── name
 ├── email
 ├── phone
 └── city
```

এখানে:

```text
customer_id
name
email
phone
city
```

সবগুলো attribute।

---

# 6. Entity এবং Attribute

উদাহরণ:

### Student

|Attribute|
|---|
|student_id|
|name|
|email|
|phone|
|date_of_birth|

Entity:

```text
Student
```

Attributes:

```text
student_id
name
email
phone
date_of_birth
```

---

# 7. Attribute-এর Types

Important types:

```text
1. Simple Attribute
2. Composite Attribute
3. Single-valued Attribute
4. Multi-valued Attribute
5. Derived Attribute
6. Key Attribute
```

---

# 8. Simple Attribute

যে attribute আর ছোট meaningful অংশে ভাঙার প্রয়োজন নেই।

Example:

```text
Age
Salary
Gender
```

---

# 9. Composite Attribute

একটি attribute-কে logical sub-parts-এ ভাগ করা যায়।

Example:

```text
Name
 ├── First Name
 └── Last Name
```

Address:

```text
Address
 ├── Street
 ├── City
 ├── District
 └── Country
```

---

# 10. Single-valued Attribute

একজন student-এর:

```text
date_of_birth
```

সাধারণত একটি value থাকবে।

```text
Student → DOB = 2001-05-10
```

এটা single-valued।

---

# 11. Multi-valued Attribute

একজন customer-এর একাধিক phone থাকতে পারে:

```text
Customer
   ↓
Phone
   ├── 01711...
   ├── 01822...
   └── 01933...
```

এটা multi-valued attribute-এর concept।

⚠️ Relational database-এ সাধারণত comma-separated phone না রেখে আলাদা related table করা ভালো।

যেমন:

```text
customers
customer_phones
```

---

# 12. Derived Attribute

যে value অন্য data থেকে calculate করা যায়।

Example:

```text
date_of_birth
       ↓
     Age
```

Age stored না করেও calculate করা যায়।

আরেকটি:

```text
quantity × unit_price
        ↓
      total
```

`total` derived হতে পারে।

---

# 13. Key Attribute

যে attribute entity-কে uniquely identify করে।

Student:

```text
student_id
```

Customer:

```text
customer_id
```

Product:

```text
product_id
```

সাধারণত এগুলো Primary Key হিসেবে ব্যবহার করা হয়।

---

# 14. Primary Key

> **একটি table-এর প্রতিটি row uniquely identify করে এমন key হলো Primary Key।**

Example:

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

এখানে:

```text
student_id = Primary Key
```

---

# 15. Primary Key-এর Properties

Primary key:

- Unique
    
- NULL হতে পারে না
    
- একটি row uniquely identify করে
    
- একটি table-এ একটি primary key constraint থাকে
    
- Primary key single বা composite হতে পারে
    

---

# 16. Composite Primary Key

কখনো একাধিক column মিলে row uniquely identify করে।

Enrollment:

```text
student_id
course_id
```

একসাথে:

```text
(student_id, course_id)
```

Primary Key হতে পারে।

SQL:

```sql
CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    grade CHAR(2),

    PRIMARY KEY (student_id, course_id)
);
```

---

# 17. Foreign Key

> একটি table-এর column যখন অন্য table-এর primary key-কে reference করে, তখন সেটি Foreign Key।

Example:

### Customers

```text
customer_id PK
```

### Orders

```text
order_id PK
customer_id FK
```

Relationship:

```text
customers
    │
    │ customer_id
    ↓
orders
```

SQL:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

---

# 18. Relationship কী?

> দুই বা ততোধিক entity-এর মধ্যে logical connection হলো Relationship।

Example:

```text
Customer ─── places ─── Order
```

মানে:

> Customer order places করে।

আর:

```text
Student ─── enrolls ─── Course
```

---

# 19. Relationship-এর Degree

Relationship কতগুলো entity involve করছে তার উপর degree নির্ভর করে।

### Unary

একটি entity:

```text
Employee
   ↕
manages
```

Employee নিজেকেই relate করছে।

---

### Binary

দুইটি entity:

```text
Student ─── enrolls ─── Course
```

সবচেয়ে common।

---

### Ternary

তিনটি entity:

```text
Supplier
    \
     Supply
    /     \
Product   Project
```

তিন entity এক relationship-এ।

---

# 20. Cardinality কী?

এটা খুব important।

> **একটি entity-এর কতগুলো instance অন্য entity-এর কতগুলো instance-এর সাথে related হতে পারে—এটাই Cardinality।**

Main types:

```text
1 : 1
1 : N
N : 1
M : N
```

---

# 21. One-to-One — 1:1

একজন person-এর একটি passport।

```text
Person ───── Passport
  1             1
```

Example:

```text
Person 1 → Passport 1
Passport 1 → Person 1
```

---

# 22. One-to-Many — 1:N

একজন customer অনেক order করতে পারে।

```text
Customer
   1
   │
   │
   N
 Order
```

অর্থাৎ:

```text
One Customer
      ↓
Many Orders
```

Database:

### customers

```text
customer_id PK
```

### orders

```text
order_id PK
customer_id FK
```

---

# 23. Many-to-One — N:1

একই relationship অন্য দিক থেকে দেখলে:

```text
Orders
   N
   │
   │
   1
Customer
```

অর্থাৎ:

```text
Many Orders
     ↓
One Customer
```

তাই:

```text
1:N = N:1
```

শুধু viewpoint আলাদা।

---

# 24. Many-to-Many — M:N

একজন student অনেক course নিতে পারে।

একটি course অনেক student নিতে পারে।

```text
Student
   M
   │
   │
   N
 Course
```

এটা M:N।

কিন্তু relational database-এ সরাসরি M:N relationship সাধারণত table দিয়ে implement করি না।

আমরা junction/bridge table ব্যবহার করি।

---

# 25. M:N কীভাবে Table-এ Convert করব?

Original:

```text
Student M:N Course
```

Convert:

```text
Students
    ↓
Enrollment
    ↓
Courses
```

Enrollment:

```text
student_id
course_id
```

Example:

### students

|student_id|name|
|---|---|
|1|Atiar|
|2|Karim|

### courses

|course_id|name|
|---|---|
|101|DBMS|
|102|SQL|

### enrollment

|student_id|course_id|
|---|---|
|1|101|
|1|102|
|2|101|

এখানে `Enrollment` হলো **junction/associative table**।

---

# 26. ER Diagram কী?

ER = **Entity Relationship**

> Entity, Attribute এবং Relationship visually represent করার diagram হলো ER Diagram।

Basic structure:

```text
[Student] ───────< [Enrollment] >────── [Course]
```

আরেকভাবে:

```text
Student 1 ─── N Enrollment N ─── 1 Course
```

---

# 27. ER Diagram-এর Common Symbols

Traditional ER notation:

|Symbol|Meaning|
|---|---|
|Rectangle|Entity|
|Oval|Attribute|
|Diamond|Relationship|
|Double Oval|Multivalued Attribute|
|Dashed Oval|Derived Attribute|
|Underlined Attribute|Key Attribute|
|Double Rectangle|Weak Entity|
|Double Diamond|Identifying Relationship|

Exam-এর জন্য এগুলো খুব important।

---

# 28. Example ER Diagram Concept

University:

```text
                 ┌───────────┐
                 │  STUDENT  │
                 └─────┬─────┘
                       │
                       │ enrolls
                       │
                 ┌─────▼─────┐
                 │   COURSE  │
                 └───────────┘
```

আর যদি Enrollment-এর নিজের attributes থাকে:

```text
Student
   │
   │
Enrollment
   │
   │
Course

Enrollment:
 ├── enrollment_date
 └── grade
```

এটা important।

---

# 29. Relationship-এর Attribute

কখনো relationship-এরও নিজস্ব information থাকে।

Example:

```text
Student ─── enrolls ─── Course
```

`enrollment_date` কার property?

Student-এর নয়।

Course-এরও নয়।

বরং:

```text
Student + Course
       ↓
Enrollment
       ↓
enrollment_date
grade
```

তাই এগুলো relationship/junction entity-তে রাখা ভালো।

---

# 30. Optionality

সব relationship mandatory নয়।

Example:

```text
Customer → Order
```

একজন customer হয়তো এখনো কোনো order করেনি।

তাই:

```text
Customer → 0 or many Orders
```

অন্যদিকে একটি order-এর অবশ্যই একজন customer থাকতে পারে:

```text
Order → exactly 1 Customer
```

এখানে minimum/maximum cardinality গুরুত্বপূর্ণ।

---

# 31. `0..1`, `1..1`, `0..N`, `1..N`

এগুলো practical database design-এ খুব useful।

### `0..1`

Zero অথবা one।

Example:

```text
Employee → ParkingSpot
```

কেউ parking spot নাও পেতে পারে।

---

### `1..1`

Exactly one।

---

### `0..N`

Zero বা many।

Customer:

```text
0..N Orders
```

---

### `1..N`

At least one, potentially many।

---

# 32. ER Design থেকে SQL

ধরো requirement:

> একজন customer অনেক order করতে পারে।

Design:

```text
Customer 1 ───── N Order
```

Tables:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100)
);
```

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT NOT NULL,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id)
);
```

এখানে relationship implement হয়েছে:

```text
customers.customer_id
        ↑
        │ FK
orders.customer_id
```

---

# 33. Database Design-এর Complete Process

একজন Database Designer সাধারণত এভাবে কাজ করবে:

### Step 1 — Requirement collect

```text
Business কী চায়?
```

### Step 2 — Entities identify

```text
Customer
Product
Order
Payment
```

### Step 3 — Attributes identify

```text
Customer:
id
name
email
phone
```

### Step 4 — Primary Keys

```text
customer_id
product_id
order_id
```

### Step 5 — Relationships

```text
Customer → Order
Order → Product
Order → Payment
```

### Step 6 — Cardinality

```text
Customer 1:N Order
Order M:N Product
Order 1:1 Payment
```

### Step 7 — Normalize

```text
1NF
2NF
3NF
```

### Step 8 — Foreign Keys

### Step 9 — Constraints

```text
NOT NULL
UNIQUE
CHECK
DEFAULT
FK
```

### Step 10 — Indexing

Query pattern অনুযায়ী।

---

# 34. Real-world E-commerce Design

একটা ছোট e-commerce system:

```text
Customer
Product
Category
Order
OrderItem
Payment
```

Relationships:

```text
Customer 1 ─── N Order

Order 1 ─── N OrderItem

Product 1 ─── N OrderItem

Category 1 ─── N Product

Order 1 ─── 1 Payment
```

এখানে:

```text
Order
   ↓
OrderItem
   ↓
Product
```

কারণ এক order-এ multiple products থাকতে পারে।

---

# 35. কেন OrderItem দরকার?

ধরো Order #100:

```text
Laptop × 1
Mouse × 2
Keyboard × 1
```

একটা order-এর মধ্যে multiple products।

তাই:

```text
orders
```

এবং:

```text
products
```

এর মধ্যে M:N relationship।

আমরা bridge table বানাই:

```text
order_items
```

যেখানে:

```text
order_id
product_id
quantity
unit_price
```

থাকতে পারে।

---

# 36. Order-এর Final Structure

```text
customers
-----------
customer_id PK
name
email


orders
-----------
order_id PK
customer_id FK
order_date


products
-----------
product_id PK
product_name
price


order_items
-----------
order_id FK
product_id FK
quantity
unit_price
```

Composite PK:

```text
PRIMARY KEY (order_id, product_id)
```

হতে পারে, অথবা আলাদা `order_item_id` ব্যবহার করা যায়—business requirements অনুযায়ী।

---

# 37. Database Designer-এর সবচেয়ে গুরুত্বপূর্ণ চিন্তা

Database design করার সময় শুধু:

> "কোন কোন table বানাব?"

ভাববে না।

বরং:

```text
1. What data?
2. Who owns the data?
3. What uniquely identifies it?
4. How are entities related?
5. How many can relate?
6. Is relationship optional?
7. Will data repeat?
8. What constraints are needed?
9. What queries will be common?
10. What indexes will be needed?
```

---

# ⭐ Class 53 Golden Rules

### Rule 1

```text
Entity → Thing
Attribute → Property
Relationship → Connection
```

### Rule 2

```text
1:N
```

relationship implement করার সময় সাধারণত **N-side table-এ FK** থাকে।

Example:

```text
Customer 1:N Order

Order.customer_id → Customer.customer_id
```

### Rule 3

```text
M:N
```

relationship → **junction/bridge table**

### Rule 4

Relationship-এর নিজস্ব attributes থাকলে associative entity/table লাগতে পারে।

### Rule 5

Design আগে, SQL পরে।

```text
Requirement
 ↓
ERD
 ↓
Normalization
 ↓
Tables
 ↓
Constraints
 ↓
Indexes
```

---

# 🧠 Class 53 Cheat Sheet

```text
Entity
↓
Real-world object/concept

Attribute
↓
Entity-এর property

Primary Key
↓
Unique row identification

Foreign Key
↓
Another table-এর key reference

Relationship
↓
Entity-এর connection

1:1
↓
One-to-One

1:N
↓
One-to-Many

M:N
↓
Many-to-Many
↓
Junction Table

ERD
↓
Entity + Attribute + Relationship-এর visual design
```

---

# 📝 Assignment

ধরো তুমি একটি **University Management System** design করবে।

Requirements:

1. একজন student অনেক course নিতে পারে।
    
2. একটি course অনেক student নিতে পারে।
    
3. একজন teacher অনেক course teach করতে পারে।
    
4. একটি course একজন teacher-এর অধীনে থাকবে।
    
5. Student-এর `student_id`, `name`, `email` থাকবে।
    
6. Course-এর `course_id`, `course_name`, `credit` থাকবে।
    
7. Enrollment-এর `enrollment_date` এবং `grade` থাকবে।
    

### তোমার কাজ:

**1.** সব Entity identify করো।

**2.** প্রতিটি Entity-এর Attributes লিখো।

**3.** Primary Key identify করো।

**4.** Relationships identify করো।

**5.** Cardinality লিখো।

**6.** M:N relationship কোথায় আছে?

**7.** Junction table-এর নাম কী হবে?

**8.** কোন table-এ কোন Foreign Key থাকবে?

**9.** Final tables-এর structure লিখো।

---

# 🎯 MCQ

**1. Entity কী?**

A. Table-এর row  
B. Real-world object/concept  
C. SQL query  
D. Constraint

**2. Attribute কী?**

A. Entity-এর property  
B. Database server  
C. Relationship  
D. Foreign key only

**3. Customer এবং Order-এর relationship সাধারণত কোনটি?**

A. 1:1  
B. 1:N  
C. N:1 only  
D. M:N

**4. M:N relationship relational database-এ সাধারণত কী দিয়ে implement করা হয়?**

A. Index  
B. Trigger  
C. Junction table  
D. View

**5. 1:N relationship-এ সাধারণত Foreign Key কোথায় থাকে?**

A. 1-side  
B. N-side  
C. দুই side-এই বাধ্যতামূলক  
D. কোথাও না

**6. `enrollment_date` কোনটির attribute হতে পারে?**

A. শুধু Student  
B. শুধু Course  
C. Enrollment relationship/entity  
D. Database

**7. কোনটি Primary Key-এর বৈশিষ্ট্য?**

A. Duplicate হতে পারে  
B. NULL হতে পারে  
C. Row uniquely identify করে  
D. সবসময় VARCHAR হতে হবে

---

## 🔥 আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়

একজন **Database Designer** হিসেবে এই pattern মাথায় রাখো:

```text
Business Requirement
        ↓
Identify Entities
        ↓
Identify Attributes
        ↓
Choose Primary Keys
        ↓
Identify Relationships
        ↓
Determine Cardinality
        ↓
Resolve M:N with Junction Table
        ↓
Normalize to 3NF
        ↓
Add Foreign Keys & Constraints
        ↓
Add Indexes based on query patterns
        ↓
Implement SQL
```

**Class 54 → Fact Table + Dimension Table + Star Schema + Snowflake Schema — এখান থেকে আমরা Database Design থেকে Data Warehouse/Analytics Design-এর দিকে যাব।**

---
# 📘 Class 54 — Fact Table, Dimension Table & Star Schema

আজকের ক্লাস থেকে আমরা **Database Design → Data Warehouse / Analytics Database Design**-এ ঢুকছি।

Class 53-এ ছিল:

```text
Entity
Attribute
Relationship
ERD
Primary Key
Foreign Key
Normalization
```

আজ শিখব:

```text
Fact Table
Dimension Table
Measure
Grain
Star Schema
Snowflake Schema
OLTP vs Data Warehouse
Star Schema কীভাবে design করতে হয়
```

---

# 1. Data Warehouse কী?

সহজভাবে:

> **বিভিন্ন source থেকে data সংগ্রহ করে analytics/reporting-এর জন্য organize করা বড় data store হলো Data Warehouse।**

OLTP database-এর লক্ষ্য:

```text
Transaction
```

Data Warehouse-এর লক্ষ্য:

```text
Analysis
Reporting
BI
Dashboard
```

উদাহরণ:

### Hotel Management

OLTP:

```text
Customer books room
Payment করা
Booking cancel করা
```

Data Warehouse:

```text
কোন মাসে বেশি booking?
কোন room type সবচেয়ে popular?
কোন city থেকে সবচেয়ে বেশি customer?
মাসভিত্তিক revenue কত?
```

---

# 2. OLTP বনাম Data Warehouse

|OLTP|Data Warehouse|
|---|---|
|Transaction|Analytics|
|INSERT/UPDATE/DELETE বেশি|SELECT/aggregation বেশি|
|Current data|Historical data|
|Highly normalized|Often dimensional model|
|Application-এর জন্য|Reporting/BI-এর জন্য|
|Example: Django backend DB|Example: Analytics warehouse|

সহজ shortcut:

```text
OLTP → Business runs
DW   → Business analysis
```

---

# 3. Dimensional Modeling কী?

Data Warehouse design করার একটি জনপ্রিয় পদ্ধতি হলো:

> **Dimensional Modeling**

এর মূল দুই ধরনের table:

```text
Fact Table
Dimension Table
```

---

# 4. Fact Table কী?

> **Business event বা measurable transaction-এর data রাখে Fact Table।**

E-commerce:

```text
Sales
```

Hotel:

```text
Bookings
```

Bank:

```text
Transactions
```

Hospital:

```text
Medical visits
```

---

# 5. Fact Table-এর মধ্যে কী থাকে?

সাধারণত:

### 1. Foreign Keys

এগুলো dimension table-এর দিকে point করে।

### 2. Measures

যে numerical values আমরা analyze করতে চাই।

Example:

```text
quantity
sales_amount
discount
profit
```

---

# 6. Dimension Table কী?

> **Business event-এর context বা description দেয় Dimension Table।**

Example:

Sales-এর ক্ষেত্রে:

```text
DimCustomer
DimProduct
DimDate
DimStore
```

এগুলো answer করে:

```text
Who?
What?
When?
Where?
```

---

# 7. Fact + Dimension Example

ধরো:

```text
Customer Atiar
Laptop
Dhaka
2026-09-13
Quantity = 2
Sales = 150000
```

এখানে:

### Dimensions

```text
Customer → Atiar
Product → Laptop
Location → Dhaka
Date → 2026-09-13
```

### Fact

```text
Quantity = 2
Sales = 150000
```

---

# 8. Dimension Table-এর Example

### `dim_customer`

|customer_key|customer_id|name|city|
|---|---|---|---|
|1|C001|Atiar|Dhaka|
|2|C002|Karim|Chittagong|

এখানে:

```text
customer_key
customer_id
name
city
```

Customer-এর descriptive information।

---

# 9. Product Dimension

### `dim_product`

|product_key|product_id|product_name|category|brand|
|---|---|---|---|---|
|1|P001|Laptop|Electronics|Dell|
|2|P002|Mouse|Accessories|Logitech|

---

# 10. Date Dimension

Data Warehouse-এ Date Dimension খুব important।

### `dim_date`

|date_key|full_date|year|month|month_name|quarter|
|---|---|--:|--:|---|---|
|20260913|2026-09-13|2026|9|September|Q3|

এখানে আমরা date-এর অনেক analytical information রাখতে পারি:

```text
year
quarter
month
month_name
week
day
day_name
is_weekend
```

---

# 11. Fact Table Example

### `fact_sales`

|date_key|customer_key|product_key|quantity|sales_amount|
|---|---|---|--:|--:|
|20260913|1|1|2|150000|
|20260913|2|2|5|5000|

এখানে:

### Foreign Keys

```text
date_key
customer_key
product_key
```

### Measures

```text
quantity
sales_amount
```

---

# 12. Fact Table + Dimension Table

Relationship:

```text
                  dim_date
                     │
                     │
                     ▼
dim_customer ─── fact_sales ─── dim_product
```

Fact table হলো center।

Dimensions চারপাশে।

এটাই আমাদের নিয়ে যায়:

# ⭐ Star Schema

---

# 13. Star Schema কী?

> **একটি central Fact Table-এর চারপাশে multiple Dimension Table থাকলে তাকে Star Schema বলে।**

Visual:

```text
                  ┌──────────────┐
                  │   DimDate    │
                  └──────┬───────┘
                         │
                         │
┌──────────────┐    ┌────▼─────┐    ┌──────────────┐
│ DimCustomer  │────│FactSales │────│ DimProduct   │
└──────────────┘    └────▲─────┘    └──────────────┘
                         │
                         │
                  ┌──────┴───────┐
                  │   DimStore   │
                  └──────────────┘
```

দেখতে star-এর মতো।

তাই নাম:

> **Star Schema**

---

# 14. Star Schema-এর সুবিধা

### 1. সহজ structure

বোঝা সহজ।

### 2. Analytics-friendly

Dashboard/report query সহজ হয়।

### 3. JOIN তুলনামূলক straightforward

Fact-এর সাথে dimensions join করা হয়।

### 4. BI tools-এর জন্য ভালো

Power BI, Tableau ইত্যাদির dimensional analytics-এর জন্য খুব common pattern।

---

# 15. Fact Table-এর Grain

আজকের সবচেয়ে important conceptগুলোর একটি:

# ⭐ Grain

> **Fact table-এর একটি row ঠিক কী represent করে—এটাই Grain।**

ধরো:

```text
fact_sales
```

এর grain যদি হয়:

> **One row = One product sold in one order**

তাহলে:

```text
Order 100
 ├── Laptop
 ├── Mouse
 └── Keyboard
```

হলে তিনটি fact row হতে পারে।

---

# 16. Grain আগে কেন নির্ধারণ করতে হয়?

যদি grain পরিষ্কার না থাকে, fact table ভুল design হতে পারে।

Example:

তুমি যদি বলো:

```text
fact_sales
```

কিন্তু জানো না row কী represent করে:

```text
One order?
One product?
One customer per day?
One store per day?
```

তাহলে:

```text
quantity
sales
profit
```

এর meaning-ও ambiguous হয়ে যাবে।

---

# 17. Golden Rule ⭐

> **Fact Table design করার আগে Grain define করো।**

Example:

```text
Grain:
One row = One product line in one order
```

তারপর columns:

```text
order_id
product_key
customer_key
date_key
quantity
sales_amount
discount
profit
```

---

# 18. Measures কী?

Fact table-এর numerical values যেগুলো aggregate/analyze করা যায়।

Example:

```text
quantity
sales_amount
discount_amount
cost
profit
```

SQL:

```sql
SELECT
    SUM(sales_amount),
    AVG(sales_amount),
    SUM(quantity)
FROM fact_sales;
```

---

# 19. Additive Measure

যে measure সব dimension বরাবর SUM করা যায়।

Example:

```text
sales_amount
quantity
```

ধরো:

```text
Dhaka = 10000
Chittagong = 15000
```

Total:

```text
25000
```

এগুলো সাধারণত **Additive Measures**।

---

# 20. Semi-Additive Measure

কিছু dimension-এ sum করা যায়, কিন্তু সব dimension-এ নয়।

Classic example:

```text
Account Balance
```

সময় অনুযায়ী:

```text
Monday = 10,000
Tuesday = 12,000
Wednesday = 15,000
```

এগুলো যোগ করে:

```text
37,000
```

বললে meaningful নাও হতে পারে।

কিন্তু customer বা branch dimension অনুযায়ী কিছু aggregation সম্ভব হতে পারে।

তাই:

> **Semi-additive**

---

# 21. Non-Additive Measure

যে measure সাধারণভাবে SUM করা যায় না।

Example:

```text
Percentage
Ratio
Average
```

যেমন:

```text
Conversion Rate = 25%
```

দুই campaign-এর:

```text
25%
40%
```

যোগ করে:

```text
65%
```

করলে অর্থপূর্ণ নয়।

---

# 22. Dimension-এর Surrogate Key

Data Warehouse-এ আমরা অনেক সময় natural/business key-এর বদলে:

> **Surrogate Key**

ব্যবহার করি।

Example:

Business key:

```text
customer_id = C1001
```

Warehouse key:

```text
customer_key = 501
```

Dimension:

```text
customer_key PK
customer_id
name
city
```

Fact table:

```text
customer_key FK
```

---

# 23. Surrogate Key কেন?

কারণ source system-এর ID সবসময় stable/unique across systems নাও হতে পারে।

ধরো:

```text
CRM:
customer_id = 101

Website:
customer_id = 101
```

দুটো 101 একই customer নাও হতে পারে।

Warehouse-এ:

```text
customer_key = 1
customer_key = 2
```

দিয়ে আলাদা করা যায়।

---

# 24. Natural Key বনাম Surrogate Key

|Natural Key|Surrogate Key|
|---|---|
|Business meaning আছে|Artificial/generated|
|Example: customer_id|Example: customer_key|
|Source system থেকে আসে|Warehouse তৈরি করে|
|Business change হতে পারে|সাধারণত stable|
|Integration-এ সমস্যা হতে পারে|Warehouse design-এ useful|

---

# 25. Star Schema-এর Full Example

ধরো Sales Data Warehouse।

### Dimension Tables

```text
dim_date
dim_customer
dim_product
dim_store
```

### Fact Table

```text
fact_sales
```

Structure:

```text
                   dim_date
                      │
                      │
                      ▼
dim_customer ─── fact_sales ─── dim_product
                      ▲
                      │
                      │
                  dim_store
```

---

# 26. SQL Design

### Date Dimension

```sql
CREATE TABLE dim_date (
    date_key INT PRIMARY KEY,
    full_date DATE,
    year INT,
    month INT,
    month_name VARCHAR(20),
    quarter INT
);
```

### Customer Dimension

```sql
CREATE TABLE dim_customer (
    customer_key INT PRIMARY KEY,
    customer_id VARCHAR(50),
    customer_name VARCHAR(100),
    city VARCHAR(100)
);
```

### Product Dimension

```sql
CREATE TABLE dim_product (
    product_key INT PRIMARY KEY,
    product_id VARCHAR(50),
    product_name VARCHAR(100),
    category VARCHAR(100)
);
```

### Fact

```sql
CREATE TABLE fact_sales (
    date_key INT,
    customer_key INT,
    product_key INT,

    quantity INT,
    sales_amount DECIMAL(12,2),
    discount_amount DECIMAL(12,2),

    FOREIGN KEY (date_key)
        REFERENCES dim_date(date_key),

    FOREIGN KEY (customer_key)
        REFERENCES dim_customer(customer_key),

    FOREIGN KEY (product_key)
        REFERENCES dim_product(product_key)
);
```

---

# 27. Star Schema Query

এখন প্রশ্ন:

> 2026 সালে category-wise sales কত?

```sql
SELECT
    p.category,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_date d
    ON f.date_key = d.date_key
JOIN dim_product p
    ON f.product_key = p.product_key
WHERE d.year = 2026
GROUP BY p.category
ORDER BY total_sales DESC;
```

এটাই dimensional model-এর power।

---

# 28. Customer-wise Sales

```sql
SELECT
    c.customer_name,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_customer c
    ON f.customer_key = c.customer_key
GROUP BY
    c.customer_key,
    c.customer_name
ORDER BY total_sales DESC;
```

---

# 29. Monthly Sales

```sql
SELECT
    d.year,
    d.month,
    d.month_name,
    SUM(f.sales_amount) AS total_sales
FROM fact_sales f
JOIN dim_date d
    ON f.date_key = d.date_key
GROUP BY
    d.year,
    d.month,
    d.month_name
ORDER BY
    d.year,
    d.month;
```

---

# 30. Snowflake Schema

Star Schema-তে dimension table সাধারণত relatively denormalized থাকে।

কিন্তু dimension-কে আবার ছোট ছোট table-এ ভাগ করলে:

> **Snowflake Schema**

Example:

### Star

```text
fact_sales
    |
dim_product
    |
category
```

সব product information `dim_product`-এ থাকতে পারে।

Snowflake:

```text
fact_sales
     |
dim_product
     |
dim_category
```

---

# 31. Star vs Snowflake

### Star

```text
Fact
 ├── Dim Customer
 ├── Dim Product
 ├── Dim Date
 └── Dim Store
```

### Snowflake

```text
Fact
 └── Dim Product
       └── Dim Category
             └── Dim Department
```

---

# 32. Star Schema vs Snowflake Schema

|Star|Snowflake|
|---|---|
|Simpler|More complex|
|Dimension বেশি denormalized|Dimension more normalized|
|Fewer JOINs|More JOINs|
|Query সহজ|Query তুলনামূলক complex|
|BI-friendly|Storage/redundancy কমাতে useful হতে পারে|

---

# 33. OLTP Database কি Star Schema?

সাধারণত না।

OLTP:

```text
customers
orders
order_items
products
categories
payments
```

এখানে normalized design common।

Data Warehouse:

```text
             dim_customer
                  |
dim_date — fact_sales — dim_product
                  |
              dim_store
```

এখানে dimensional model common।

---

# 34. OLTP → Data Warehouse

Real-world architecture:

```text
Application DB
      ↓
   ETL / ELT
      ↓
Data Warehouse
      ↓
   BI / Reports
      ↓
Power BI / Tableau / Dashboard
```

তুমি যেহেতু Excel + SQL + Data Analysis শিখছ, এই pipeline খুব গুরুত্বপূর্ণ।

---

# 35. তোমার শেখার Journey-এর সাথে সম্পর্ক

তুমি এতদিন:

```text
Excel
 ↓
SQL
 ↓
Database Design
```

শিখেছ।

এখন:

```text
Database
 ↓
Data Warehouse
 ↓
Dimensional Modeling
 ↓
BI
 ↓
Data Engineering
```

এর দিকে যেতে পারবে।

---

# ⭐ Class 54 Golden Rules

### Rule 1

```text
Fact → What happened?
```

### Rule 2

```text
Dimension → Who / What / When / Where?
```

### Rule 3

```text
Fact → Measures + Foreign Keys
```

### Rule 4

> **Fact table-এর Grain আগে define করো।**

### Rule 5

```text
Star Schema
=
Central Fact
+
Dimension Tables
```

### Rule 6

```text
M:N relationship
```

OLTP-তে যেমন junction table লাগে, dimensional model-এ business event অনুযায়ী fact table তৈরি হতে পারে।

---

# 🧠 Class 54 Cheat Sheet

```text
Data Warehouse
      ↓
Analytics / Reporting

Fact Table
      ↓
Business event
      ↓
Measures + Dimension Keys

Dimension Table
      ↓
Business context
      ↓
Customer / Product / Date / Store

Grain
      ↓
What exactly does one fact row represent?

Star Schema
      ↓
Fact in center
Dimensions around it

Snowflake
      ↓
Normalized dimensions
```

---

# 📝 Assignment

একটি **Hotel Data Warehouse** design করো।

Business requirements:

- Customer hotel booking করে
    
- Customer-এর city আছে
    
- Room-এর room type আছে
    
- Hotel-এর location আছে
    
- Booking-এর date আছে
    
- Booking-এর number of nights আছে
    
- Room price আছে
    
- Discount আছে
    
- Total revenue calculate করা যাবে
    

### তোমার কাজ:

**1.** কোনটি Fact Table?

**2.** কোন কোন Dimension Table হবে?

**3.** Fact table-এর **Grain** কী হবে?

**4.** কোনগুলো measure?

**5.** কোনগুলো dimension?

**6.** একটি Star Schema structure আঁকো/লিখো।

**7.** `fact_booking` table-এর সম্ভাব্য columns লিখো।

**8.** `dim_date`, `dim_customer`, `dim_room`, `dim_hotel`-এর columns লিখো।

---

# 🎯 MCQ

**1. Fact Table মূলত কী রাখে?**

A. শুধু customer information  
B. Business events/measures  
C. শুধু addresses  
D. Database users

**2. কোনটি Dimension Table-এর example?**

A. FactSales  
B. DimCustomer  
C. TransactionAmount  
D. Quantity

**3. Fact Table-এর Grain কী?**

A. Primary key-এর type  
B. One fact row কী represent করে  
C. Index-এর size  
D. Database size

**4. Star Schema-তে কী থাকে?**

A. শুধু Dimension  
B. শুধু Fact  
C. Central Fact + Dimensions  
D. শুধু normalized tables

**5. কোনটি সাধারণত Additive Measure?**

A. Sales Amount  
B. Percentage  
C. Conversion Rate  
D. Ratio

**6. `customer_key` কী হতে পারে?**

A. Surrogate Key  
B. Measure  
C. Dimension attribute only  
D. Aggregate function

**7. Snowflake Schema-এর প্রধান বৈশিষ্ট্য কী?**

A. Dimension আরও normalized  
B. Fact table থাকে না  
C. কোনো relationship থাকে না  
D. শুধু একটি table থাকে

---

## 🔥 আজকের 10-second revision

```text
Fact       → Event
Dimension  → Context
Measure    → Numeric value
Grain      → One row means what?
Star       → Fact + Dimensions
Snowflake  → Normalized Dimensions
```

**পরের ক্লাস: Class 55 — SQL Interview Problems + Advanced Query Challenges** — সেখানে এখন পর্যন্ত শেখা `JOIN + CTE + Window Function + Subquery + GROUP BY + CASE + Date + EXISTS + Index` একসাথে ব্যবহার করে বাস্তব interview-level problem solve করব।

---
# 📘 Class 55 — SQL Interview Problems + Advanced Query Challenges

আজকের ক্লাসে আমরা নতুন syntax কম শিখব। বরং **আগের Class 31–54-এর concepts একসাথে ব্যবহার করে interview-level SQL problem solve** করব।

আজকের লক্ষ্য:

```text
SELECT
WHERE
GROUP BY
HAVING
JOIN
Subquery
CTE
Window Function
CASE
EXISTS
Date
NULL
Set Operation
Index/EXPLAIN
        ↓
Real SQL Problem Solving
```

---

# 1. Interview SQL Problem Solving Strategy

SQL problem দেখেই query লেখা শুরু করবে না।

এই 5-step process follow করবে:

```text
Step 1 → What output is needed?
Step 2 → Which tables contain the data?
Step 3 → How are tables related?
Step 4 → Do I need filtering/grouping/ranking?
Step 5 → Write + test + optimize
```

### Golden Rule ⭐

> **Question → Data relationship → Logic → SQL**

---

# 2. আমাদের Practice Database

আজকের examples-এর জন্য ধরো:

### customers

```text
customer_id
customer_name
city
```

### products

```text
product_id
product_name
category
price
```

### orders

```text
order_id
customer_id
product_id
order_date
quantity
```

Revenue:

```text
quantity * price
```

---

# Problem 1 — সব customer যারা order করেছে

Question:

> Find customers who have placed at least one order.

### Solution

```sql
SELECT DISTINCT
    c.customer_id,
    c.customer_name
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

### Alternative: EXISTS

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

### Interview Point

`JOIN` এবং `EXISTS` দুটোই ব্যবহার করা যায়, কিন্তু logical requirement যদি হয়:

> "related row exists কি?"

তাহলে `EXISTS` খুব natural।

---

# Problem 2 — যেসব customer কোনো order করেনি

এটা interview-এর classic problem।

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

### Alternative

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
LEFT JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

এটা খুব গুরুত্বপূর্ণ pattern:

```text
LEFT JOIN
+
WHERE right_table.id IS NULL
```

মানে:

> Matching record নেই।

---

# Problem 3 — Customer-wise total sales

Revenue:

```text
quantity × price
```

Query:

```sql
SELECT
    c.customer_id,
    c.customer_name,
    SUM(o.quantity * p.price) AS total_sales
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    c.customer_id,
    c.customer_name;
```

এখানে ব্যবহার করেছি:

```text
JOIN
+
SUM
+
GROUP BY
```

---

# Problem 4 — Top 5 customers by sales

```sql
SELECT
    c.customer_id,
    c.customer_name,
    SUM(o.quantity * p.price) AS total_sales
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    c.customer_id,
    c.customer_name
ORDER BY total_sales DESC
LIMIT 5;
```

### Pattern

```text
GROUP BY
→ calculate
→ ORDER BY DESC
→ LIMIT
```

---

# Problem 5 — Customers whose sales are greater than 100,000

```sql
SELECT
    c.customer_id,
    c.customer_name,
    SUM(o.quantity * p.price) AS total_sales
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    c.customer_id,
    c.customer_name
HAVING SUM(o.quantity * p.price) > 100000;
```

### Important

Aggregate condition:

```sql
HAVING
```

not:

```sql
WHERE
```

কারণ:

```text
WHERE → before grouping
HAVING → after grouping
```

---

# Problem 6 — Second highest salary

ধরো:

```text
employees
-----------
employee_id
name
salary
```

একটি simple solution:

```sql
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

Logic:

```text
Maximum salary
      ↓
Remove maximum
      ↓
Find maximum again
      ↓
Second highest
```

---

# Problem 7 — Top 3 salaries

Window function ব্যবহার করি:

```sql
SELECT *
FROM (
    SELECT
        employee_id,
        name,
        salary,
        DENSE_RANK() OVER (
            ORDER BY salary DESC
        ) AS salary_rank
    FROM employees
) x
WHERE salary_rank <= 3;
```

### কেন `DENSE_RANK()`?

যদি:

```text
100000
90000
90000
80000
```

তাহলে:

```text
100000 → 1
90000  → 2
90000  → 2
80000  → 3
```

তাই top 3 salary levels পাওয়া যাবে।

---

# Problem 8 — Highest salary in each department

এটা খুব common interview question।

```sql
SELECT *
FROM (
    SELECT
        employee_id,
        name,
        department,
        salary,
        RANK() OVER (
            PARTITION BY department
            ORDER BY salary DESC
        ) AS rnk
    FROM employees
) x
WHERE rnk = 1;
```

এখানে:

```text
PARTITION BY department
```

মানে:

> প্রতিটি department আলাদাভাবে ranking হবে।

---

# Problem 9 — Employees earning above department average

এটা একটু advanced।

প্রথমে department average বের করতে পারি:

```sql
SELECT
    e.employee_id,
    e.name,
    e.department,
    e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department = e.department
);
```

এটা **correlated subquery**।

---

# Problem 10 — একই problem Window Function দিয়ে

```sql
SELECT *
FROM (
    SELECT
        employee_id,
        name,
        department,
        salary,

        AVG(salary) OVER (
            PARTITION BY department
        ) AS dept_avg_salary

    FROM employees
) x
WHERE salary > dept_avg_salary;
```

এখানে:

```text
department
     ↓
average salary
     ↓
compare employee salary
```

---

# Problem 11 — Monthly sales

```sql
SELECT
    DATE_FORMAT(o.order_date, '%Y-%m') AS month,
    SUM(o.quantity * p.price) AS total_sales
FROM orders o
JOIN products p
    ON o.product_id = p.product_id
GROUP BY
    DATE_FORMAT(o.order_date, '%Y-%m')
ORDER BY month;
```

---

# Problem 12 — Month-over-month growth

প্রথমে monthly sales:

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(o.order_date, '%Y-%m') AS month,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY DATE_FORMAT(o.order_date, '%Y-%m')
)
SELECT
    month,
    sales,
    LAG(sales) OVER (
        ORDER BY month
    ) AS previous_sales
FROM monthly_sales;
```

এখন growth:

```sql
WITH monthly_sales AS (
    SELECT
        DATE_FORMAT(o.order_date, '%Y-%m') AS month,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY DATE_FORMAT(o.order_date, '%Y-%m')
),
sales_with_previous AS (
    SELECT
        month,
        sales,
        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales
    FROM monthly_sales
)
SELECT
    month,
    sales,
    previous_sales,
    ROUND(
        100 * (sales - previous_sales)
        / NULLIF(previous_sales, 0),
        2
    ) AS growth_percent
FROM sales_with_previous;
```

এখানে একসাথে:

```text
CTE
+
GROUP BY
+
LAG
+
NULLIF
+
Calculation
```

ব্যবহার করেছি।

---

# Problem 13 — Highest-selling product

```sql
SELECT
    p.product_id,
    p.product_name,
    SUM(o.quantity) AS total_quantity
FROM products p
JOIN orders o
    ON p.product_id = o.product_id
GROUP BY
    p.product_id,
    p.product_name
ORDER BY total_quantity DESC
LIMIT 1;
```

---

# Problem 14 — Highest-selling product in each category

এটা advanced interview problem।

```sql
WITH product_sales AS (
    SELECT
        p.product_id,
        p.product_name,
        p.category,
        SUM(o.quantity) AS total_quantity
    FROM products p
    JOIN orders o
        ON p.product_id = o.product_id
    GROUP BY
        p.product_id,
        p.product_name,
        p.category
),
ranked_products AS (
    SELECT
        *,
        RANK() OVER (
            PARTITION BY category
            ORDER BY total_quantity DESC
        ) AS rnk
    FROM product_sales
)
SELECT *
FROM ranked_products
WHERE rnk = 1;
```

### Pattern:

```text
Aggregate
   ↓
CTE
   ↓
Window Function
   ↓
Filter Rank
```

⭐ এটা খুব important interview pattern।

---

# Problem 15 — Customers with at least 3 orders

```sql
SELECT
    c.customer_id,
    c.customer_name,
    COUNT(o.order_id) AS total_orders
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
GROUP BY
    c.customer_id,
    c.customer_name
HAVING COUNT(o.order_id) >= 3;
```

---

# Problem 16 — Customers who bought every product in a category

এটা advanced logic।

ধরো category:

```text
Electronics
```

আমরা জানতে চাই:

> কোন customer Electronics category-এর **সব product** কিনেছে?

এ ধরনের problem-এ `NOT EXISTS` খুব powerful।

Concept:

```sql
SELECT c.customer_id
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM products p
    WHERE p.category = 'Electronics'
      AND NOT EXISTS (
          SELECT 1
          FROM orders o
          WHERE o.customer_id = c.customer_id
            AND o.product_id = p.product_id
      )
);
```

Logic:

```text
Customer
   ↓
There does NOT exist
   ↓
a required product
   ↓
that customer did NOT buy
```

অর্থাৎ:

> এমন কোনো required product নেই যেটা customer কেনেনি।

---

# Problem 17 — Duplicate emails

ধরো:

```text
customers
-----------
customer_id
email
```

Duplicate email খুঁজতে:

```sql
SELECT
    email,
    COUNT(*) AS total
FROM customers
GROUP BY email
HAVING COUNT(*) > 1;
```

Classic interview question।

---

# Problem 18 — Find duplicate rows

ধরো:

```text
name
city
```

একই name + city কতবার এসেছে:

```sql
SELECT
    name,
    city,
    COUNT(*) AS total
FROM customers
GROUP BY
    name,
    city
HAVING COUNT(*) > 1;
```

---

# Problem 19 — Employees with same salary

```sql
SELECT
    salary,
    COUNT(*) AS employee_count
FROM employees
GROUP BY salary
HAVING COUNT(*) > 1;
```

---

# Problem 20 — First order of each customer

Window function:

```sql
SELECT *
FROM (
    SELECT
        o.*,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date
        ) AS rn
    FROM orders o
) x
WHERE rn = 1;
```

এখানে:

```text
PARTITION BY customer_id
```

প্রতিটি customer-এর order আলাদা group হিসেবে ধরছে।

তারপর:

```text
ORDER BY order_date
```

সবচেয়ে পুরোনো order:

```text
ROW_NUMBER = 1
```

---

# Problem 21 — Latest order of each customer

শুধু order direction পরিবর্তন:

```sql
SELECT *
FROM (
    SELECT
        o.*,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id
            ORDER BY order_date DESC
        ) AS rn
    FROM orders o
) x
WHERE rn = 1;
```

### Pattern মনে রাখো:

```text
First
→ ROW_NUMBER + ASC

Latest
→ ROW_NUMBER + DESC
```

---

# Problem 22 — Running total

```sql
SELECT
    month,
    sales,
    SUM(sales) OVER (
        ORDER BY month
    ) AS running_total
FROM monthly_sales;
```

Example:

```text
Month   Sales   Running
Jan     100     100
Feb     200     300
Mar     150     450
```

---

# Problem 23 — Customers' percentage of total sales

```sql
WITH customer_sales AS (
    SELECT
        c.customer_id,
        c.customer_name,
        SUM(o.quantity * p.price) AS sales
    FROM customers c
    JOIN orders o
        ON c.customer_id = o.customer_id
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY
        c.customer_id,
        c.customer_name
)
SELECT
    customer_name,
    sales,
    ROUND(
        100 * sales / SUM(sales) OVER (),
        2
    ) AS sales_percentage
FROM customer_sales;
```

এখানে:

```text
SUM(sales) OVER ()
```

মানে পুরো result-এর total।

---

# Problem 24 — Customers whose latest order was more than 30 days ago

প্রথমে latest order:

```sql
WITH latest_orders AS (
    SELECT
        customer_id,
        MAX(order_date) AS latest_order_date
    FROM orders
    GROUP BY customer_id
)
SELECT
    c.customer_id,
    c.customer_name,
    l.latest_order_date
FROM customers c
JOIN latest_orders l
    ON c.customer_id = l.customer_id
WHERE l.latest_order_date < CURRENT_DATE - INTERVAL 30 DAY;
```

এটা customer retention / inactive customer analysis-এ useful।

---

# Problem 25 — Category contribution to total sales

```sql
WITH category_sales AS (
    SELECT
        p.category,
        SUM(o.quantity * p.price) AS sales
    FROM orders o
    JOIN products p
        ON o.product_id = p.product_id
    GROUP BY p.category
)
SELECT
    category,
    sales,
    ROUND(
        100 * sales / SUM(sales) OVER (),
        2
    ) AS contribution_percent
FROM category_sales
ORDER BY sales DESC;
```

---

# 🔥 Interview-এর Most Important SQL Patterns

এখন পর্যন্ত শেখা problemগুলোকে pattern হিসেবে মনে রাখো।

### Pattern 1 — Top N

```sql
ORDER BY value DESC
LIMIT N;
```

---

### Pattern 2 — Top N per group

```sql
ROW_NUMBER()
OVER (
    PARTITION BY group
    ORDER BY value DESC
)
```

---

### Pattern 3 — Rank with ties

```sql
RANK()
OVER (
    PARTITION BY group
    ORDER BY value DESC
)
```

---

### Pattern 4 — Previous row

```sql
LAG(value)
OVER (
    ORDER BY date
)
```

---

### Pattern 5 — Next row

```sql
LEAD(value)
OVER (
    ORDER BY date
)
```

---

### Pattern 6 — Running total

```sql
SUM(value)
OVER (
    ORDER BY date
)
```

---

### Pattern 7 — Group average comparison

```sql
AVG(value)
OVER (
    PARTITION BY group
)
```

---

### Pattern 8 — No related record

```sql
NOT EXISTS (...)
```

অথবা:

```sql
LEFT JOIN ...
WHERE right.id IS NULL
```

---

### Pattern 9 — Duplicate

```sql
GROUP BY column
HAVING COUNT(*) > 1
```

---

### Pattern 10 — Previous period growth

```text
LAG
+
calculation
+
NULLIF
```

---

# 🧠 SQL Interview Decision Tree

Question দেখলে নিজেকে জিজ্ঞেস করো:

```text
Need individual rows?
        ↓
     SELECT

Need filtering?
        ↓
     WHERE

Need groups?
        ↓
   GROUP BY

Need aggregate filter?
        ↓
    HAVING

Need multiple tables?
        ↓
      JOIN

Need existence?
        ↓
     EXISTS

Need nested logic?
        ↓
    Subquery / CTE

Need ranking?
        ↓
 Window Function

Need previous/next?
        ↓
 LAG / LEAD

Need Top N per group?
        ↓
 RANK / DENSE_RANK / ROW_NUMBER

Need performance?
        ↓
 EXPLAIN + Index
```

---

# ⚠️ Common Interview Mistakes

### Mistake 1

Aggregate condition-এ `WHERE` ব্যবহার করা।

❌

```sql
WHERE SUM(sales) > 100000
```

✅

```sql
HAVING SUM(sales) > 100000
```

---

### Mistake 2

`COUNT(*)` এবং `COUNT(column)`-এর difference না বোঝা।

```text
COUNT(*)       → rows
COUNT(column)  → non-NULL values
```

---

### Mistake 3

`NOT IN` + NULL problem ভুলে যাওয়া।

Related-record existence problem-এ অনেক সময়:

```sql
NOT EXISTS
```

safer choice।

---

### Mistake 4

Top N এবং Top N per group-কে একই মনে করা।

### Overall Top 5:

```sql
ORDER BY salary DESC
LIMIT 5;
```

### Each department-এর Top 5:

```sql
ROW_NUMBER()
OVER (
    PARTITION BY department
    ORDER BY salary DESC
)
```

---

### Mistake 5

`RANK()` বনাম `ROW_NUMBER()` না বোঝা।

```text
ROW_NUMBER
→ unique sequential number

RANK
→ ties get same rank, gaps possible

DENSE_RANK
→ ties get same rank, no gaps
```

Example:

```text
Salary
100
90
90
80
```

```text
ROW_NUMBER  → 1,2,3,4
RANK        → 1,2,2,4
DENSE_RANK  → 1,2,2,3
```

---

# ⭐ Class 55 Golden Rules

```text
Simple filter
→ WHERE

Group filter
→ HAVING

Multiple tables
→ JOIN

Existence
→ EXISTS

No existence
→ NOT EXISTS

Top N
→ ORDER BY + LIMIT

Top N per group
→ Window Function

Previous row
→ LAG

Next row
→ LEAD

Running total
→ SUM() OVER()

Duplicate
→ GROUP BY + HAVING COUNT(*) > 1

Performance
→ EXPLAIN
```

---

# 📝 Class 55 Challenge Set

এগুলো নিজে solve করার চেষ্টা করো।

### Challenge 1

প্রতিটি department-এর **second highest salary** বের করো।

### Challenge 2

যেসব customer **কখনো order করেনি** তাদের বের করো।

### Challenge 3

প্রতিটি customer-এর **latest order** বের করো।

### Challenge 4

প্রতিটি category-এর **top 3 products by sales** বের করো।

### Challenge 5

প্রতি মাসের sales এবং **previous month's sales** দেখাও।

### Challenge 6

প্রতি মাসের **sales growth percentage** বের করো।

### Challenge 7

যেসব customer-এর total spending **average customer spending-এর চেয়ে বেশি**, তাদের বের করো।

### Challenge 8

Duplicate customer email বের করো।

### Challenge 9

প্রতিটি department-এর employee count এবং average salary বের করো, কিন্তু শুধু যেসব department-এ **at least 5 employees** আছে।

### Challenge 10 ⭐

প্রতিটি customer-এর:

```text
customer_name
total_orders
total_sales
average_order_value
latest_order_date
customer_rank_by_sales
```

এক query-তে বের করার চেষ্টা করো।

---

# 🎯 Class 55 MCQ

**1. Aggregate result filter করার জন্য কোনটি ব্যবহার করা হয়?**

A. WHERE  
B. HAVING  
C. ORDER BY  
D. JOIN

**2. Top 5 overall records বের করতে সবচেয়ে simple pattern কোনটি?**

A. `GROUP BY + HAVING`  
B. `ORDER BY DESC + LIMIT 5`  
C. `LAG()`  
D. `EXISTS`

**3. প্রতিটি department-এর top 3 employee বের করতে কোনটি সবচেয়ে suitable?**

A. LIMIT 3  
B. ROW_NUMBER/RANK/DENSE_RANK + PARTITION BY  
C. DISTINCT  
D. UNION

**4. Previous row-এর value পেতে কোন function?**

A. LEAD  
B. LAG  
C. RANK  
D. FIRST_VALUE

**5. Duplicate value খুঁজতে কোন pattern useful?**

A. `GROUP BY + HAVING COUNT(*) > 1`  
B. `ORDER BY + LIMIT`  
C. `LAG()`  
D. `EXISTS`

**6. `ROW_NUMBER()`-এর একটি গুরুত্বপূর্ণ বৈশিষ্ট্য কী?**

A. Tie হলে একই number দেয়  
B. প্রতিটি row-কে unique sequence number দেয়  
C. শুধু aggregate করে  
D. শুধু date-এর জন্য কাজ করে

**7. Query performance investigate করতে কোনটি সবচেয়ে useful?**

A. DISTINCT  
B. EXPLAIN  
C. UNION  
D. CASE

---

## 🔥 Final Revision

Class 31 থেকে Class 55 পর্যন্ত তোমার SQL journey এখন:

```text
SQL Basics
   ↓
CRUD
   ↓
GROUP BY
   ↓
JOIN
   ↓
Subquery
   ↓
CTE
   ↓
Window Functions
   ↓
Date/String/NULL
   ↓
Views
   ↓
Procedures/Functions
   ↓
Transactions
   ↓
Triggers
   ↓
Indexes
   ↓
EXPLAIN
   ↓
Normalization
   ↓
Database Design
   ↓
Star Schema
   ↓
⭐ Interview Problem Solving
```

**Class 56 হবে — Full SQL Data Analyst Project: একটি বাস্তব Sales Analytics database নিয়ে শুরু থেকে data analysis, KPI, customer analysis, product analysis, monthly trend, ranking এবং final dashboard-ready SQL তৈরি।**


---
# 📘 Class 56 — Full SQL Data Analyst Project

আজ আমরা **একটা complete Sales Analytics Project** করব।  
এটা শুধু SQL syntax practice না—এখানে তুমি একজন **Junior Data Analyst** হিসেবে business data থেকে answer বের করবে।

### আজকের Project

> **E-Commerce Sales Analytics**

আমরা বের করব:

```text
Sales KPI
↓
Monthly Sales
↓
Customer Analysis
↓
Product Analysis
↓
Category Analysis
↓
Top Customers
↓
Top Products
↓
Customer Ranking
↓
Growth Analysis
↓
Business Insights
```

---

# 1. Project Database Design

আমাদের 3টি main table থাকবে:

```text
customers
products
orders
```

Relationship:

```text
customers
    │
    │ 1
    │
    │ N
  orders
    │
    │ N
    │
    │ 1
 products
```

অর্থাৎ:

```text
Customer 1 ──── N Orders
Product  1 ──── N Orders
```

---

# 2. Create Tables

### Customers

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    city VARCHAR(50),
    email VARCHAR(100),
    signup_date DATE
);
```

### Products

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10,2)
);
```

### Orders

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    order_date DATE,
    quantity INT,

    FOREIGN KEY (customer_id)
        REFERENCES customers(customer_id),

    FOREIGN KEY (product_id)
        REFERENCES products(product_id)
);
```

---

# 3. Sample Data

### Customers

```sql
INSERT INTO customers
(customer_id, customer_name, city, email, signup_date)
VALUES
(1, 'Rahim', 'Dhaka', 'rahim@gmail.com', '2025-01-10'),
(2, 'Karim', 'Chittagong', 'karim@gmail.com', '2025-02-15'),
(3, 'Sadia', 'Dhaka', 'sadia@gmail.com', '2025-03-20'),
(4, 'Nadia', 'Sylhet', 'nadia@gmail.com', '2025-04-12'),
(5, 'Hasan', 'Dhaka', 'hasan@gmail.com', '2025-05-01'),
(6, 'Tanvir', 'Rajshahi', 'tanvir@gmail.com', '2025-06-10');
```

### Products

```sql
INSERT INTO products
(product_id, product_name, category, price)
VALUES
(1, 'Laptop', 'Electronics', 80000),
(2, 'Phone', 'Electronics', 40000),
(3, 'Headphone', 'Electronics', 5000),
(4, 'Chair', 'Furniture', 10000),
(5, 'Table', 'Furniture', 20000),
(6, 'Keyboard', 'Accessories', 3000);
```

### Orders

```sql
INSERT INTO orders
(order_id, customer_id, product_id, order_date, quantity)
VALUES
(1, 1, 1, '2026-01-05', 1),
(2, 2, 2, '2026-01-10', 2),
(3, 1, 3, '2026-01-15', 2),
(4, 3, 4, '2026-01-20', 1),
(5, 4, 5, '2026-02-05', 2),
(6, 2, 6, '2026-02-10', 3),
(7, 5, 2, '2026-02-15', 1),
(8, 1, 2, '2026-03-01', 1),
(9, 3, 1, '2026-03-10', 1),
(10, 5, 4, '2026-03-15', 2),
(11, 2, 3, '2026-03-20', 2),
(12, 4, 1, '2026-04-05', 1);
```

---

# 4. প্রথম কাজ — Understand the Data

প্রথমে কখনো complex query লিখবে না।

Check:

```sql
SELECT *
FROM customers;
```

```sql
SELECT *
FROM products;
```

```sql
SELECT *
FROM orders;
```

তারপর row count:

```sql
SELECT COUNT(*) AS total_customers
FROM customers;
```

```sql
SELECT COUNT(*) AS total_products
FROM products;
```

```sql
SELECT COUNT(*) AS total_orders
FROM orders;
```

---

# 5. Revenue Calculation

Orders table-এ revenue নেই।

আমাদের calculate করতে হবে:

```text
Revenue = quantity × product price
```

Query:

```sql
SELECT
    o.order_id,
    o.order_date,
    p.product_name,
    o.quantity,
    p.price,
    o.quantity * p.price AS revenue
FROM orders o
JOIN products p
    ON o.product_id = p.product_id;
```

এটা project-এর সবচেয়ে important calculation।

---

# 6. ⭐ Create Sales View

যেহেতু একই JOIN বারবার লাগবে, আমরা একটা View বানাতে পারি।

```sql
CREATE VIEW sales_data AS
SELECT
    o.order_id,
    o.order_date,

    c.customer_id,
    c.customer_name,
    c.city,

    p.product_id,
    p.product_name,
    p.category,
    p.price,

    o.quantity,

    o.quantity * p.price AS revenue

FROM orders o

JOIN customers c
    ON o.customer_id = c.customer_id

JOIN products p
    ON o.product_id = p.product_id;
```

এখন:

```sql
SELECT *
FROM sales_data;
```

আমাদের analysis সহজ হয়ে গেল।

---

# 7. KPI — Key Performance Indicators

একটি business dashboard-এর প্রথম অংশ সাধারণত KPI।

আমরা বের করব:

```text
Total Revenue
Total Orders
Total Customers
Total Quantity
Average Order Value
```

### Total Revenue

```sql
SELECT
    SUM(revenue) AS total_revenue
FROM sales_data;
```

### Total Orders

```sql
SELECT
    COUNT(DISTINCT order_id) AS total_orders
FROM sales_data;
```

### Total Quantity

```sql
SELECT
    SUM(quantity) AS total_quantity
FROM sales_data;
```

### Average Order Value

```sql
SELECT
    SUM(revenue)
    / COUNT(DISTINCT order_id) AS average_order_value
FROM sales_data;
```

---

# 8. KPI এক Query-তে

Real dashboard-এর জন্য:

```sql
SELECT
    SUM(revenue) AS total_revenue,

    COUNT(DISTINCT order_id) AS total_orders,

    COUNT(DISTINCT customer_id) AS total_customers,

    SUM(quantity) AS total_quantity,

    ROUND(
        SUM(revenue)
        / COUNT(DISTINCT order_id),
        2
    ) AS average_order_value

FROM sales_data;
```

এটাই একটি basic **Sales KPI Query**।

---

# 9. Monthly Sales Analysis

Business জানতে চাইবে:

> কোন মাসে কত sales হয়েছে?

```sql
SELECT
    DATE_FORMAT(order_date, '%Y-%m') AS month,
    SUM(revenue) AS monthly_sales
FROM sales_data
GROUP BY
    DATE_FORMAT(order_date, '%Y-%m')
ORDER BY month;
```

Result concept:

```text
Month       Sales
--------------------
2026-01     ...
2026-02     ...
2026-03     ...
2026-04     ...
```

---

# 10. Monthly Orders

```sql
SELECT
    DATE_FORMAT(order_date, '%Y-%m') AS month,
    COUNT(DISTINCT order_id) AS total_orders
FROM sales_data
GROUP BY
    DATE_FORMAT(order_date, '%Y-%m')
ORDER BY month;
```

---

# 11. Monthly Average Order Value

```sql
SELECT
    DATE_FORMAT(order_date, '%Y-%m') AS month,

    SUM(revenue) AS sales,

    COUNT(DISTINCT order_id) AS orders,

    ROUND(
        SUM(revenue) /
        COUNT(DISTINCT order_id),
        2
    ) AS average_order_value

FROM sales_data

GROUP BY
    DATE_FORMAT(order_date, '%Y-%m')

ORDER BY month;
```

---

# 12. 📈 Month-over-Month Growth

এখন আমাদের analytics একটু advanced হবে।

```sql
WITH monthly_sales AS (

    SELECT
        DATE_FORMAT(order_date, '%Y-%m') AS month,
        SUM(revenue) AS sales

    FROM sales_data

    GROUP BY
        DATE_FORMAT(order_date, '%Y-%m')
),

sales_with_previous AS (

    SELECT
        month,
        sales,

        LAG(sales) OVER (
            ORDER BY month
        ) AS previous_sales

    FROM monthly_sales
)

SELECT
    month,
    sales,
    previous_sales,

    ROUND(
        100 * (sales - previous_sales)
        / NULLIF(previous_sales, 0),
        2
    ) AS growth_percent

FROM sales_with_previous;
```

এখানে একসাথে:

```text
View
+
CTE
+
GROUP BY
+
LAG
+
NULLIF
+
Calculation
```

ব্যবহার হয়েছে।

---

# 13. Customer Sales Analysis

Business question:

> কোন customer সবচেয়ে বেশি টাকা spend করেছে?

```sql
SELECT
    customer_id,
    customer_name,
    SUM(revenue) AS total_spending
FROM sales_data
GROUP BY
    customer_id,
    customer_name
ORDER BY total_spending DESC;
```

---

# 14. Top 5 Customers

```sql
SELECT
    customer_id,
    customer_name,
    SUM(revenue) AS total_spending
FROM sales_data
GROUP BY
    customer_id,
    customer_name
ORDER BY total_spending DESC
LIMIT 5;
```

---

# 15. Customer Order Frequency

```sql
SELECT
    customer_id,
    customer_name,
    COUNT(DISTINCT order_id) AS total_orders
FROM sales_data
GROUP BY
    customer_id,
    customer_name
ORDER BY total_orders DESC;
```

---

# 16. Customer Average Order Value

```sql
SELECT
    customer_id,
    customer_name,

    SUM(revenue) AS total_sales,

    COUNT(DISTINCT order_id) AS total_orders,

    ROUND(
        SUM(revenue)
        / COUNT(DISTINCT order_id),
        2
    ) AS average_order_value

FROM sales_data

GROUP BY
    customer_id,
    customer_name

ORDER BY total_sales DESC;
```

---

# 17. Customer Ranking

এখন window function ব্যবহার করব।

```sql
WITH customer_sales AS (

    SELECT
        customer_id,
        customer_name,
        SUM(revenue) AS total_sales

    FROM sales_data

    GROUP BY
        customer_id,
        customer_name
)

SELECT
    customer_id,
    customer_name,
    total_sales,

    RANK() OVER (
        ORDER BY total_sales DESC
    ) AS sales_rank

FROM customer_sales;
```

Result:

```text
Customer    Sales       Rank
-----------------------------
Rahim       ...          1
Karim       ...          2
Sadia       ...          3
...
```

---

# 18. Customer Contribution %

এখন জানতে চাই:

> Total sales-এর কত % কোন customer generate করেছে?

```sql
WITH customer_sales AS (

    SELECT
        customer_id,
        customer_name,
        SUM(revenue) AS total_sales

    FROM sales_data

    GROUP BY
        customer_id,
        customer_name
)

SELECT
    customer_name,
    total_sales,

    ROUND(
        100 * total_sales
        / SUM(total_sales) OVER (),
        2
    ) AS contribution_percent

FROM customer_sales

ORDER BY total_sales DESC;
```

---

# 19. Product Analysis

সবচেয়ে বেশি quantity কোন product বিক্রি হয়েছে?

```sql
SELECT
    product_id,
    product_name,
    SUM(quantity) AS total_quantity
FROM sales_data
GROUP BY
    product_id,
    product_name
ORDER BY total_quantity DESC;
```

---

# 20. Product Revenue Ranking

```sql
WITH product_sales AS (

    SELECT
        product_id,
        product_name,
        SUM(quantity) AS quantity_sold,
        SUM(revenue) AS total_revenue

    FROM sales_data

    GROUP BY
        product_id,
        product_name
)

SELECT
    *,
    RANK() OVER (
        ORDER BY total_revenue DESC
    ) AS revenue_rank

FROM product_sales;
```

---

# 21. Category Analysis

```sql
SELECT
    category,
    SUM(quantity) AS total_quantity,
    SUM(revenue) AS total_sales
FROM sales_data
GROUP BY category
ORDER BY total_sales DESC;
```

এতে business জানতে পারবে:

> কোন category সবচেয়ে profitable/revenue-generating?

**Note:** এখানে আমরা `profit` calculate করছি না—তাই technically এটা **sales/revenue analysis**, profit analysis নয়।

---

# 22. Category Contribution %

```sql
WITH category_sales AS (

    SELECT
        category,
        SUM(revenue) AS sales

    FROM sales_data

    GROUP BY category
)

SELECT
    category,
    sales,

    ROUND(
        100 * sales /
        SUM(sales) OVER (),
        2
    ) AS contribution_percent

FROM category_sales

ORDER BY sales DESC;
```

---

# 23. Top Product per Category ⭐

এটা interview + analyst দুটোতেই important।

```sql
WITH product_sales AS (

    SELECT
        category,
        product_id,
        product_name,
        SUM(revenue) AS sales

    FROM sales_data

    GROUP BY
        category,
        product_id,
        product_name
),

ranked_products AS (

    SELECT
        *,
        RANK() OVER (
            PARTITION BY category
            ORDER BY sales DESC
        ) AS rnk

    FROM product_sales
)

SELECT *
FROM ranked_products
WHERE rnk = 1;
```

Logic:

```text
Product Sales
     ↓
Group by Category
     ↓
Rank products
     ↓
Take Rank = 1
```

---

# 24. City-wise Sales

```sql
SELECT
    city,
    SUM(revenue) AS total_sales,
    COUNT(DISTINCT customer_id) AS customers
FROM sales_data
GROUP BY city
ORDER BY total_sales DESC;
```

এটা geographical/business analysis।

---

# 25. Customer Segmentation

আমরা customer-দের spending অনুযায়ী segment করতে পারি।

```sql
WITH customer_sales AS (

    SELECT
        customer_id,
        customer_name,
        SUM(revenue) AS total_sales

    FROM sales_data

    GROUP BY
        customer_id,
        customer_name
)

SELECT
    customer_id,
    customer_name,
    total_sales,

    CASE

        WHEN total_sales >= 100000
            THEN 'VIP'

        WHEN total_sales >= 50000
            THEN 'High Value'

        WHEN total_sales >= 20000
            THEN 'Medium Value'

        ELSE 'Low Value'

    END AS customer_segment

FROM customer_sales;
```

### Important

এখানে threshold example হিসেবে দেওয়া হয়েছে। Real business-এ threshold business requirement/data distribution অনুযায়ী ঠিক করতে হবে।

---

# 26. Inactive Customers

যারা কোনো order করেনি:

```sql
SELECT
    c.customer_id,
    c.customer_name
FROM customers c
WHERE NOT EXISTS (

    SELECT 1

    FROM orders o

    WHERE o.customer_id = c.customer_id
);
```

এটা **customer retention analysis**-এর basic অংশ।

---

# 27. Latest Order per Customer

```sql
SELECT
    customer_id,
    customer_name,
    MAX(order_date) AS latest_order_date
FROM sales_data
GROUP BY
    customer_id,
    customer_name;
```

---

# 28. Customer Activity Status

```sql
SELECT
    customer_id,
    customer_name,
    MAX(order_date) AS latest_order_date,

    CASE

        WHEN MAX(order_date)
             >= CURRENT_DATE - INTERVAL 30 DAY
        THEN 'Active'

        ELSE 'Inactive'

    END AS status

FROM sales_data

GROUP BY
    customer_id,
    customer_name;
```

**Note:** sample dataset-এর historical dates হলে current date-এর সাথে compare করলে সবাই inactive হতে পারে। Real project-এ analysis date বা reporting period carefully define করতে হবে।

---

# 29. Running Total of Sales

```sql
WITH monthly_sales AS (

    SELECT
        DATE_FORMAT(order_date, '%Y-%m') AS month,
        SUM(revenue) AS sales

    FROM sales_data

    GROUP BY
        DATE_FORMAT(order_date, '%Y-%m')
)

SELECT
    month,
    sales,

    SUM(sales) OVER (
        ORDER BY month
    ) AS cumulative_sales

FROM monthly_sales;
```

---

# 30. Moving Average

3-month moving average:

```sql
WITH monthly_sales AS (

    SELECT
        DATE_FORMAT(order_date, '%Y-%m') AS month,
        SUM(revenue) AS sales

    FROM sales_data

    GROUP BY
        DATE_FORMAT(order_date, '%Y-%m')
)

SELECT
    month,
    sales,

    AVG(sales) OVER (
        ORDER BY month
        ROWS BETWEEN 2 PRECEDING
        AND CURRENT ROW
    ) AS moving_average

FROM monthly_sales;
```

---

# 31. Final Dashboard Dataset ⭐

একজন Data Analyst হিসেবে তুমি BI tool-এ dashboard বানাতে চাইলে এমন summary dataset useful হবে।

```sql
WITH customer_summary AS (

    SELECT
        customer_id,
        customer_name,

        COUNT(DISTINCT order_id) AS total_orders,

        SUM(revenue) AS total_sales,

        MAX(order_date) AS latest_order

    FROM sales_data

    GROUP BY
        customer_id,
        customer_name
)

SELECT
    customer_id,
    customer_name,
    total_orders,
    total_sales,

    ROUND(
        total_sales / total_orders,
        2
    ) AS average_order_value,

    latest_order,

    RANK() OVER (
        ORDER BY total_sales DESC
    ) AS sales_rank

FROM customer_summary

ORDER BY sales_rank;
```

এই output Excel / Power BI / Tableau-তে নিয়ে dashboard তৈরি করা যায়।

---

# 🧠 Project Architecture

আজকের project-এর পুরো flow:

```text
                    DATABASE
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
      Customers     Orders      Products
          │            │            │
          └────────────┼────────────┘
                       ↓
                   JOIN
                       ↓
                  sales_data
                       ↓
              ┌────────┴────────┐
              ↓                 ↓
          Aggregation        Window
              ↓                 ↓
        GROUP BY/HAVING    RANK/LAG
              │                 │
              └────────┬────────┘
                       ↓
                   Analysis
                       ↓
          ┌────────────┼────────────┐
          ↓            ↓            ↓
       Customer      Product      Monthly
       Analysis      Analysis      Trend
          │            │            │
          └────────────┼────────────┘
                       ↓
                     KPI
                       ↓
                  Dashboard
```

---

# ⭐ Class 56 — Most Important Queries

তুমি এই 10টা pattern ভালোভাবে আয়ত্ত করলে অনেক Data Analyst SQL problem solve করতে পারবে:

```text
1. JOIN
2. GROUP BY
3. HAVING
4. CTE
5. CASE
6. RANK()
7. ROW_NUMBER()
8. LAG()
9. SUM() OVER()
10. NOT EXISTS
```

---

# ⚠️ Common Mistakes

### 1. Revenue ভুলভাবে calculate করা

❌

```sql
SUM(price)
```

যদি multiple quantity থাকে।

✅

```sql
SUM(quantity * price)
```

---

### 2. Order count ভুল করা

যদি order table-এ multiple product row থাকে, তাহলে:

```sql
COUNT(*)
```

সবসময় unique order count দেবে না।

প্রয়োজনে:

```sql
COUNT(DISTINCT order_id)
```

---

### 3. Customer ranking-এর আগে aggregation না করা

❌ সরাসরি raw order-এর উপর customer ranking।

সঠিক:

```text
Orders
 ↓
Customer-wise SUM
 ↓
RANK
```

---

### 4. `WHERE` বনাম `HAVING`

```text
WHERE  → individual rows filter
HAVING → groups filter
```

---

### 5. Profit আর Revenue একই মনে করা

```text
Revenue = Selling amount

Profit = Revenue - Cost
```

আমাদের বর্তমান database-এ `cost` নেই, তাই আমরা **sales/revenue analytics** করছি।

---

# 📝 Class 56 Assignment — Full Analyst Challenge

এবার তোমার জন্য বাস্তব assignment। **নিজে query লিখবে।**

### Level 1

**1.** Total revenue বের করো।

**2.** Total number of orders বের করো।

**3.** প্রতিটি product-এর total quantity sold বের করো।

**4.** প্রতিটি category-এর total revenue বের করো।

---

### Level 2

**5.** Top 3 customers by revenue বের করো।

**6.** প্রতিটি customer-এর total orders এবং total revenue বের করো।

**7.** প্রতিটি city-এর total revenue বের করো।

**8.** যেসব customer 2টির বেশি order করেছে তাদের বের করো।

---

### Level 3

**9.** প্রতিটি category-এর highest-revenue product বের করো।

**10.** প্রতিটি customer-এর sales rank বের করো।

**11.** Monthly sales এবং previous month sales বের করো।

**12.** Monthly growth percentage বের করো।

---

### 🔥 Level 4 — Interview Challenge

**13.** প্রতিটি customer-এর:

```text
customer_name
total_orders
total_sales
average_order_value
latest_order_date
sales_rank
```

একটি query-তে বের করো।

**14.** প্রতিটি category-এর:

```text
category
total_sales
sales_percentage
rank
```

বের করো।

**15.** এমন customer বের করো যাদের spending **average customer spending-এর চেয়ে বেশি**।

---

# 🎯 Class 56 MCQ

**1. Revenue সাধারণত কীভাবে calculate করা হচ্ছে?**

A. `price + quantity`  
B. `price - quantity`  
C. `price * quantity`  
D. `price / quantity`

**2. Unique order count-এর জন্য কোনটি safer?**

A. `COUNT(*)`  
B. `COUNT(DISTINCT order_id)`  
C. `SUM(order_id)`  
D. `AVG(order_id)`

**3. Customer ranking করার আগে সাধারণত কী করতে হবে?**

A. Customer-wise aggregate  
B. DELETE  
C. INSERT  
D. DROP

**4. Previous month's sales পেতে কোন function?**

A. LEAD  
B. LAG  
C. RANK  
D. COUNT

**5. Category-এর top product বের করতে কোন pattern useful?**

A. `LIMIT 1`  
B. `RANK() OVER(PARTITION BY category...)`  
C. `COUNT(*)`  
D. `DISTINCT`

**6. Revenue এবং Profit-এর মধ্যে সঠিক সম্পর্ক কোনটি?**

A. সবসময় একই  
B. Profit = Revenue + Cost  
C. Profit = Revenue − Cost  
D. Revenue = Profit − Cost

---

## 🏆 Class 56 Golden Rule

```text
Raw Tables
    ↓
JOIN
    ↓
Create Analysis Dataset/View
    ↓
Aggregate
    ↓
Window Functions
    ↓
KPI
    ↓
Business Questions
    ↓
Insights
    ↓
Dashboard
```

**Class 57 হবে — Full Database Designer Project:** requirement থেকে শুরু করে **ER Diagram → entities → relationships → normalization → PK/FK → constraints → indexes → SQL schema → production-ready database design**।



----
হ্যাঁ, **আরও class লাগবে**—তবে এখন তোমার SQL foundation অনেক strong হয়ে গেছে। Class 31–58 পর্যন্ত তুমি SQL + Database Design-এর বড় অংশ cover করেছ।

আমি এখন আর ২০–৩০টা random class না করে **আরও প্রায় 12টি focused class** করার পর একটি solid Database Designer/Junior Database Engineer level-এ যেতে বলব।

### 📚 Proposed Final Database Roadmap

|Class|Topic|
|---|---|
|**59**|Advanced Indexing & Query Performance|
|**60**|EXPLAIN / EXPLAIN ANALYZE + Slow Query Optimization|
|**61**|Advanced SQL: Cursors, Recursive CTE, Advanced Window|
|**62**|Advanced Transactions & Isolation|
|**63**|Locking, Deadlock & Concurrency — Advanced|
|**64**|Database Partitioning|
|**65**|Database Security, Users, Roles & Privileges|
|**66**|Backup, Restore & Disaster Recovery|
|**67**|PostgreSQL Advanced Features|
|**68**|Database Scaling, Replication & Read/Write Architecture|
|**69**|Production Database Design & Best Practices|
|**70**|**Final Database Designer Project** ⭐|

### তারপর?

Class 70-এর project-এ আমরা একদম বাস্তব project design করব:

```text
Business Requirement
        ↓
ER Diagram
        ↓
Normalization
        ↓
Schema
        ↓
PK / FK / Constraints
        ↓
Indexes
        ↓
Transactions
        ↓
Security
        ↓
Performance
        ↓
PostgreSQL
        ↓
Django/DRF Integration
        ↓
Production Database
```

### 🎯 আমার recommendation

তোমার লক্ষ্য যেহেতু **Database Designer** হওয়া, তাই **Class 70 পর্যন্ত যাওয়া worth it**।

এরপর আর শুধু SQL class চালিয়ে যাওয়ার দরকার নেই। বরং:

**SQL + Database Design → PostgreSQL → Real Projects → Data Engineering basics**

এই path-এ যাওয়া বেশি useful হবে।

**তাই next হবে Class 59 — Advanced Indexing & Query Performance.**


-----
# 📚 Class 59 — Advanced Indexing & Query Performance

আজকের class খুব important, কারণ **Database Designer** হিসেবে শুধু query লিখলেই হবে না—query **কত দ্রুত execute হচ্ছে** সেটাও বুঝতে হবে।

আজ আমরা শিখব:

1. B-Tree / B+Tree
    
2. Composite Index
    
3. Leftmost Prefix Rule
    
4. Covering Index
    
5. Clustered vs Secondary Index
    
6. Index Selectivity
    
7. EXPLAIN ANALYZE
    
8. Slow Query
    
9. Filesort
    
10. Temporary Table
    
11. Pagination Optimization
    
12. Keyset Pagination
    

---

# 1️⃣ প্রথমে বুঝি — Index আসলে কেন দরকার?

ধরো `customers` table-এ:

```text
10,000,000 customers
```

তুমি query করলে:

```sql
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

Index না থাকলে database-কে অনেক row পরীক্ষা করতে হতে পারে।

এটাকে সহজভাবে ভাবো:

```text
No Index

Row 1  → check
Row 2  → check
Row 3  → check
...
Row 10,000,000 → check
```

Index থাকলে:

```text
Index
  ↓
email = rahim@gmail.com
  ↓
matching row
```

অর্থাৎ:

> **Index হলো database-এর জন্য একটি দ্রুত lookup structure।**

---

# 2️⃣ B-Tree / B+Tree কী?

Relational database-এ সাধারণ index implementation হিসেবে **B-Tree family** খুব common।

একটা সহজ ধারণা:

```text
                 [50]
               /      \
          [20,30]     [70,80]
          /  |  \      / |  \
        ... ... ...   ... ... ...
```

Database সরাসরি সব record search না করে tree structure ব্যবহার করে দ্রুত target location খুঁজতে পারে।

### কেন Tree?

কারণ data যদি sorted structure-এ থাকে:

```text
10
20
30
40
50
60
70
80
90
```

তাহলে binary-search-এর মতো ধারণা ব্যবহার করে দ্রুত search করা যায়।

---

# 3️⃣ B+Tree ধারণা

Database indexing-এর ক্ষেত্রে **B+Tree** ধারণাটা বিশেষভাবে important।

Simplified structure:

```text
             Root
              |
       ----------------
       |              |
    Internal       Internal
       |              |
   -----------     -----------
   | | | | | |     | | | | | |
   Leaf nodes → → → → → → → →
```

Leaf nodes-এ sorted key/value references থাকে এবং leaf level সাধারণত sequential traversal-এর জন্য linked থাকে।

তাই range query-এর জন্য খুব useful:

```sql
SELECT *
FROM products
WHERE price BETWEEN 1000 AND 5000;
```

Index সাহায্য করতে পারে:

```text
1000 → 1200 → 1500 → 2000 → 2500 → ... → 5000
```

---

# 4️⃣ সব query-তে Index দরকার?

❌ না।

এটা খুব important।

ধরো table:

```text
100 rows
```

এখানে full table scan অনেক সময় index ব্যবহারের চেয়েও সহজ/দ্রুত হতে পারে।

কিন্তু:

```text
50 million rows
```

এখানে ভালো index huge difference করতে পারে।

### Golden Rule

> **Index blindly create করবে না। Query pattern দেখে index design করবে।**

---

# 5️⃣ Composite Index

একাধিক column নিয়ে তৈরি index:

```sql
CREATE INDEX idx_customer_date
ON orders(customer_id, order_date);
```

এখানে:

```text
customer_id
      +
order_date
```

একসাথে index করা হয়েছে।

---

# 6️⃣ Composite Index কেন দরকার?

ধরো query:

```sql
SELECT *
FROM orders
WHERE customer_id = 10
AND order_date >= '2026-01-01';
```

এই query-এর জন্য:

```sql
(customer_id, order_date)
```

index খুব useful হতে পারে।

কারণ index structure:

```text
customer_id
     ↓
order_date
     ↓
matching rows
```

---

# 7️⃣ সবচেয়ে Important — Leftmost Prefix Rule ⭐

ধরো:

```sql
CREATE INDEX idx_orders
ON orders(customer_id, order_date, status);
```

Column order:

```text
1. customer_id
2. order_date
3. status
```

এখন কোন query index-এর leading part ব্যবহার করতে পারবে?

### ✅ ভালো candidates

```sql
WHERE customer_id = 10
```

```sql
WHERE customer_id = 10
AND order_date = '2026-09-14'
```

```sql
WHERE customer_id = 10
AND order_date = '2026-09-14'
AND status = 'CONFIRMED'
```

কারণ তারা শুরু করছে:

```text
customer_id
```

দিয়ে।

---

### ⚠️ শুধু order_date

```sql
WHERE order_date = '2026-09-14'
```

এই composite index-এর জন্য সাধারণত leading-column সুবিধা পাবে না।

কারণ:

```text
(customer_id, order_date, status)
  ↑
প্রথম column বাদ
```

---

### ⚠️ শুধু status

```sql
WHERE status = 'CONFIRMED'
```

এটাও leading prefix নয়।

---

# 8️⃣ Column Order কেন এত important?

ধরো:

```sql
INDEX(customer_id, order_date)
```

এবং

```text
customer_id
    ↓
order_date
```

Database প্রথমে customer অনুযায়ী organize করতে পারে, তারপর customer-এর ভিতরে date অনুযায়ী।

কিন্তু:

```sql
INDEX(order_date, customer_id)
```

হলে structure-এর priority বদলে যায়।

তাই:

> **Composite index-এর column order query pattern-এর উপর নির্ভর করে।**

---

# 9️⃣ Covering Index ⭐

এটা advanced কিন্তু খুব important।

ধরো:

```sql
CREATE INDEX idx_customer_email
ON customers(customer_id, email);
```

Query:

```sql
SELECT customer_id, email
FROM customers
WHERE customer_id = 10;
```

Query-এর জন্য দরকার:

```text
customer_id
email
```

দুটোই index-এর মধ্যে আছে।

তাই database অনেক ক্ষেত্রে মূল table-এ গিয়ে row fetch না করেই index থেকেই result দিতে পারে।

এটাকে বলে:

> **Covering Index**

---

### সহজভাবে

Normal:

```text
Index
 ↓
Find row
 ↓
Go to table
 ↓
Get data
```

Covering:

```text
Index
 ↓
Find + return required data
```

এতে I/O কমতে পারে।

---

# 🔟 Clustered Index

এখন খুব important distinction।

**MySQL InnoDB**-তে primary key clustered index-এর ভিত্তি হিসেবে কাজ করে।

Conceptually:

```text
Primary Key Index
       ↓
actual table data
```

অর্থাৎ primary key-এর B-tree structure-এর leaf level-এ row data থাকে।

ধরো:

```sql
CREATE TABLE users (
    id BIGINT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);
```

এখানে InnoDB-তে:

```text
PRIMARY KEY (id)
        ↓
Clustered Index
        ↓
Table data
```

---

# 1️⃣1️⃣ Secondary Index

Primary key ছাড়া অন্য index:

```sql
CREATE INDEX idx_email
ON users(email);
```

এটা:

```text
Secondary Index
```

InnoDB-তে secondary index-এর leaf entries সাধারণত primary key value-ও ধরে।

Conceptually:

```text
email index
     ↓
email → primary_key
             ↓
        clustered data
```

তাই secondary index দিয়ে search করার পরে প্রয়োজন হলে primary-key lookup করতে হতে পারে।

---

# 1️⃣2️⃣ Clustered vs Secondary

|বিষয়|Clustered|Secondary|
|---|---|---|
|Data|leaf-এ table data|সাধারণত index entries|
|InnoDB PK|হ্যাঁ|না|
|Primary key|ভিত্তি|অন্য index|
|Table lookup|কম হতে পারে|প্রয়োজন হতে পারে|
|সংখ্যা|একটি clustered structure|একাধিক secondary index|

### Golden Rule

```text
Primary Key → Clustered structure in InnoDB
Other indexes → Secondary indexes
```

---

# 1️⃣3️⃣ Index Selectivity ⭐

Selectivity মানে সহজভাবে:

> একটি column কতটা effectively rows আলাদা করতে পারে।

ধরো:

### Gender

```text
Male
Female
```

শুধু 2 ধরনের value।

Selectivity relatively low।

---

### Email

```text
rahim@gmail.com
karim@gmail.com
sadia@gmail.com
...
```

প্রায় প্রতিটি row আলাদা।

Selectivity high।

---

### Example

10 million rows:

```text
status:
ACTIVE     → 9,000,000
INACTIVE   → 1,000,000
```

এখানে:

```sql
WHERE status = 'ACTIVE'
```

index সবসময় huge benefit নাও দিতে পারে, কারণ matching rows অনেক বেশি।

অন্যদিকে:

```sql
WHERE email = 'x@example.com'
```

খুব selective।

---

# 1️⃣4️⃣ High vs Low Selectivity

```text
High Selectivity
        ↓
Email
Phone
UUID
Unique ID

Low Selectivity
        ↓
Gender
Boolean
Status
```

তবে মনে রাখবে:

> **Low-selectivity column-এ index কখনোই useful নয়—এটা ভুল।**

Composite index, query pattern, table size, data distribution এবং optimizer decision সব matter করে।

---

# 1️⃣5️⃣ EXPLAIN — Database কী করছে দেখব কীভাবে?

Query:

```sql
EXPLAIN
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

এতে database query execution plan সম্পর্কে information দেয়।

---

# 1️⃣6️⃣ EXPLAIN-এর গুরুত্বপূর্ণ অংশ

MySQL-এ তুমি এগুলো দেখবে:

```text
id
select_type
table
type
possible_keys
key
key_len
ref
rows
filtered
Extra
```

সব মুখস্থ করার দরকার নেই। Importantগুলো আগে বুঝো।

---

## `possible_keys`

Database কোন index ব্যবহার করতে **পারতে পারে**।

---

## `key`

Database শেষ পর্যন্ত কোন index **choose করেছে**।

Example:

```text
possible_keys → idx_email
key           → idx_email
```

Good sign হতে পারে।

কিন্তু:

```text
possible_keys → idx_email
key           → NULL
```

মানে index available হলেও optimizer সেটা ব্যবহার করেনি।

---

# 1️⃣7️⃣ `rows`

Optimizer আনুমানিক কত rows examine করতে পারে।

Example:

```text
rows = 5
```

সাধারণত:

```text
rows = 5
```

better than:

```text
rows = 5,000,000
```

কিন্তু এটা **estimate**, actual exact number নয়।

---

# 1️⃣8️⃣ EXPLAIN `type`

Important values:

```text
const
eq_ref
ref
range
index
ALL
```

Roughly efficient → less efficient direction:

```text
const
 ↓
eq_ref
 ↓
ref
 ↓
range
 ↓
index
 ↓
ALL
```

---

# 1️⃣9️⃣ `ALL` কী?

```text
type = ALL
```

সাধারণত full table scan বোঝায়।

Example:

```text
10 million rows
        ↓
check many/all rows
```

তবে ছোট table হলে:

```text
100 rows
```

`ALL` দেখলেই panic করার দরকার নেই।

---

# 2️⃣0️⃣ `Using filesort`

ধরো:

```sql
SELECT *
FROM orders
ORDER BY order_date DESC;
```

যদি suitable index না থাকে, database-এর অতিরিক্ত sorting operation লাগতে পারে।

EXPLAIN-এর `Extra`-তে দেখতে পারো:

```text
Using filesort
```

নাম দেখে ভাববে না যে অবশ্যই disk-এ file তৈরি হচ্ছে।

এটা MySQL-এর execution-plan terminology; sorting operation বোঝায়।

---

# 2️⃣1️⃣ `Using temporary`

কিছু query-তে intermediate result রাখার জন্য temporary structure ব্যবহার হতে পারে।

বিশেষ করে complex:

```text
GROUP BY
ORDER BY
DISTINCT
JOIN
```

এর combination-এ দেখা যেতে পারে।

Example:

```sql
SELECT city, COUNT(*)
FROM customers
GROUP BY city
ORDER BY COUNT(*) DESC;
```

EXPLAIN-এ:

```text
Using temporary
Using filesort
```

দুটোই দেখা যেতে পারে।

এটা দেখলেই query bad—এমন নয়।

---

# 2️⃣2️⃣ Query Optimization Workflow ⭐

এটা তোমার সবচেয়ে important workflow:

```text
Slow Query
    ↓
EXPLAIN
    ↓
Check type
    ↓
Check possible_keys
    ↓
Check key
    ↓
Check rows
    ↓
Check Extra
    ↓
Optimize
    ↓
EXPLAIN Again
```

### Golden Rule

> **Guess করে optimization নয় — EXPLAIN দিয়ে verify করবে।**

---

# 2️⃣3️⃣ Sargability

একটা গুরুত্বপূর্ণ performance concept।

ধরো:

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026;
```

এখানে indexed column-এর উপর function চালানো হচ্ছে।

অনেক ক্ষেত্রে এটা index-এর efficient use বাধাগ্রস্ত করতে পারে।

এর পরিবর্তে:

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01';
```

এটা range-based এবং index-friendly হতে পারে।

---

# 2️⃣4️⃣ Pagination Problem

ধরো website-এ:

```text
Page 1
Page 2
Page 3
...
Page 100000
```

Traditional pagination:

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20 OFFSET 1000000;
```

Problem:

```text
OFFSET 1,000,000
```

Database-কে অনেক preceding rows skip করতে হতে পারে।

Large dataset-এ এটা expensive হতে পারে।

---

# 2️⃣5️⃣ Traditional OFFSET Pagination

Example:

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20 OFFSET 100;
```

Page 1:

```text
OFFSET 0
```

Page 2:

```text
OFFSET 20
```

Page 3:

```text
OFFSET 40
```

Simple এবং common।

কিন্তু huge offset:

```text
OFFSET 1,000,000
```

problematic হতে পারে।

---

# 2️⃣6️⃣ Keyset Pagination ⭐⭐⭐

Large dataset-এর জন্য powerful technique।

ধরো previous page-এর শেষ ID:

```text
last_id = 100
```

Next page:

```sql
SELECT *
FROM products
WHERE product_id > 100
ORDER BY product_id
LIMIT 20;
```

Database সরাসরি:

```text
id > 100
```

এর জায়গা থেকে continue করতে পারে।

---

# 2️⃣7️⃣ OFFSET vs Keyset

### OFFSET

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20 OFFSET 1000000;
```

Concept:

```text
Skip 1,000,000
      ↓
Take 20
```

### Keyset

```sql
SELECT *
FROM products
WHERE product_id > 1000000
ORDER BY product_id
LIMIT 20;
```

Concept:

```text
Start after 1,000,000
        ↓
Take 20
```

---

# 2️⃣8️⃣ Keyset Pagination-এর সুবিধা

Large table:

```text
100 million rows
```

Traditional:

```text
OFFSET 90,000,000
```

খুব expensive হতে পারে।

Keyset:

```sql
WHERE id > last_seen_id
```

অনেক বেশি scalable হতে পারে, যদি appropriate index থাকে।

---

# 2️⃣9️⃣ Django/DRF-এ কেন Important?

তুমি যেহেতু Django/DRF করো, production API-তে এটা খুব useful।

Example:

```text
GET /api/products/?cursor=...
```

DRF-এর cursor-based pagination এই ধরনের scalability concept ব্যবহার করে।

তাই database performance জানা থাকলে backend API design-ও better হবে।

---

# 3️⃣0️⃣ Hotel Project-এ Apply করি

তোমার hotel database মনে করো:

```text
bookings
---------
booking_id
customer_id
room_id
check_in
check_out
status
```

আমরা আগে index দিয়েছিলাম:

```sql
CREATE INDEX idx_bookings_room_dates
ON bookings(room_id, check_in, check_out);
```

Availability query:

```sql
SELECT 1
FROM bookings
WHERE room_id = 101
AND status IN ('PENDING', 'CONFIRMED')
AND check_in < '2026-09-14'
AND check_out > '2026-09-12';
```

এখন প্রশ্ন:

> এই index আসলেই query-তে useful হচ্ছে?

Guess করবে না।

Check করবে:

```sql
EXPLAIN
SELECT 1
FROM bookings
WHERE room_id = 101
AND status IN ('PENDING', 'CONFIRMED')
AND check_in < '2026-09-14'
AND check_out > '2026-09-12';
```

তারপর দেখবে:

```text
possible_keys
key
rows
type
Extra
```

---

# 3️⃣1️⃣ Production Database Designer Mindset

একজন beginner ভাবে:

> "Query কাজ করছে।"

একজন database designer ভাবে:

> "Query কাজ করছে, কিন্তু 10 million rows হলে কী হবে?"

আর একজন production engineer ভাবে:

```text
Query
 ↓
Index
 ↓
Execution Plan
 ↓
Rows examined
 ↓
Concurrency
 ↓
Latency
 ↓
Scalability
```

এই mindset develop করাই Class 59-এর মূল লক্ষ্য।

---

# 🧠 আজকের Golden Rules

```text
1. Index → Faster data retrieval

2. B-Tree/B+Tree → Common index structure

3. Composite Index → Multiple columns

4. Column order matters

5. Leftmost Prefix → Leading columns matter

6. Covering Index → Required columns available in index

7. InnoDB PK → Clustered index basis

8. Other indexes → Secondary indexes

9. High selectivity → Often better filtering

10. possible_keys ≠ actual key

11. EXPLAIN → Query execution plan

12. rows → Optimizer estimate

13. ALL → Usually full table scan

14. filesort → Sorting operation

15. temporary → Temporary intermediate structure

16. OFFSET → Large values can become expensive

17. Keyset → Better for large-scale pagination

18. EXPLAIN → Optimize → EXPLAIN again
```

---

# 📝 Class 59 Assignment

### Part A — Index

এই table ধরো:

```sql
CREATE TABLE orders (
    order_id BIGINT PRIMARY KEY,
    customer_id BIGINT,
    order_date DATE,
    status VARCHAR(20),
    total_amount DECIMAL(10,2)
);
```

### Task 1

`customer_id`-এর জন্য index তৈরি করো।

### Task 2

`customer_id + order_date` composite index তৈরি করো।

### Task 3

Explain করো:

```sql
WHERE customer_id = 10
```

এবং

```sql
WHERE order_date = '2026-09-14'
```

এর মধ্যে কোনটি `(customer_id, order_date)` index-এর জন্য বেশি natural fit এবং কেন।

### Task 4

Covering index বলতে কী বোঝায়?

### Task 5

Clustered এবং Secondary Index-এর difference লিখো।

---

## 🔥 Challenge

এই query optimize করার চেষ্টা করো:

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026
ORDER BY order_date;
```

তারপর তোমার optimized query লিখবে।

---

## 🎯 Final Challenge

ধরো:

```text
products = 50 million rows
```

User শেষবার দেখেছে:

```text
product_id = 9,500,000
```

Next 20 products আনতে তুমি কোনটা prefer করবে?

**A**

```sql
LIMIT 20 OFFSET 9500000;
```

**B**

```sql
WHERE product_id > 9500000
ORDER BY product_id
LIMIT 20;
```

👉 **A/B + কারণ** লিখে দাও।

তারপর আমরা **Class 60 — EXPLAIN / EXPLAIN ANALYZE + Slow Query Optimization**-এ যাব।

----
# 📚 Class 60 — EXPLAIN / EXPLAIN ANALYZE + Slow Query Optimization

আজকের class হলো **SQL Performance-এর practical side**।  
Class 59-এ আমরা Index শিখেছি। আজ শিখব:

> **Database কেন একটি query slow করছে এবং কীভাবে সেটা identify + optimize করতে হয়।**

আজকের topics:

1. EXPLAIN কী?
    
2. EXPLAIN output পড়া
    
3. `type`
    
4. `possible_keys` vs `key`
    
5. `rows`
    
6. `filtered`
    
7. `Extra`
    
8. EXPLAIN ANALYZE
    
9. Slow Query
    
10. Full Table Scan
    
11. Index ব্যবহার না হওয়ার কারণ
    
12. Sargable vs Non-Sargable
    
13. ORDER BY optimization
    
14. JOIN optimization
    
15. GROUP BY optimization
    
16. Query optimization workflow
    
17. Real-world hotel example
    

---

# 1️⃣ EXPLAIN কী?

ধরো তুমি লিখলে:

```sql
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

তুমি জানো query-এর result কী হবে।

কিন্তু তুমি জানো না:

> Database internally **কীভাবে** result বের করছে?

এইটা দেখার জন্য:

```sql
EXPLAIN
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

EXPLAIN database-এর **execution plan** দেখায়।

সহজভাবে:

```text
SQL Query
   ↓
EXPLAIN
   ↓
Database কীভাবে query execute করবে?
```

---

# 2️⃣ EXPLAIN কেন দরকার?

ধরো:

```text
customers = 10 million rows
```

Query:

```sql
SELECT *
FROM customers
WHERE email = 'x@gmail.com';
```

তুমি ভাবলে:

> "email-এর index আছে, তাই fast."

কিন্তু database হয়তো index ব্যবহার করছে না।

EXPLAIN দিয়ে জানতে পারবে:

```text
Index available?
Index used?
How many rows estimated?
Full scan?
Sorting?
Temporary table?
```

---

# 3️⃣ Basic EXPLAIN

```sql
EXPLAIN
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

Conceptually output:

```text
type        ref
possible_keys idx_email
key         idx_email
rows        1
Extra       Using index condition
```

এখন একে একে বুঝি।

---

# 4️⃣ `table`

কোন table access করা হচ্ছে।

Example:

```text
table
-----
customers
```

Multiple JOIN থাকলে multiple table-এর execution information দেখতে পারো।

---

# 5️⃣ `type` ⭐

`type` খুব important।

Common values:

```text
system
const
eq_ref
ref
range
index
ALL
```

এগুলো broadly access method বোঝায়।

---

## `const`

খুব efficient single-row lookup-এর ক্ষেত্রে দেখা যেতে পারে।

Example:

```sql
SELECT *
FROM users
WHERE id = 10;
```

যদি `id` primary key হয়:

```text
type = const
```

হতে পারে।

---

# 6️⃣ `eq_ref`

JOIN-এর ক্ষেত্রে highly efficient lookup।

Example:

```sql
SELECT *
FROM orders o
JOIN customers c
    ON o.customer_id = c.customer_id;
```

যদি `c.customer_id` unique/primary key হয়, relevant access-এর ক্ষেত্রে `eq_ref` দেখা যেতে পারে।

---

# 7️⃣ `ref`

Non-unique indexed lookup-এর ক্ষেত্রে common।

Example:

```sql
SELECT *
FROM orders
WHERE customer_id = 10;
```

যদি:

```sql
CREATE INDEX idx_customer
ON orders(customer_id);
```

থাকে, তাহলে:

```text
type = ref
```

দেখা যেতে পারে।

---

# 8️⃣ `range`

Range condition-এর ক্ষেত্রে।

Example:

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2026-02-01';
```

যদি `order_date` indexed হয়:

```text
type = range
```

হতে পারে।

---

# 9️⃣ `ALL` ⚠️

এটা সাধারণত full table scan।

Example:

```sql
SELECT *
FROM customers
WHERE city = 'Dhaka';
```

যদি suitable index না থাকে:

```text
type = ALL
```

হতে পারে।

মানে database-কে অনেক/all rows examine করতে হচ্ছে।

---

# 🔟 কিন্তু `ALL` মানেই bad নয়

ধরো:

```text
customers = 50 rows
```

Full scan:

```text
50 rows
```

এটা perfectly fine হতে পারে।

Problem:

```text
customers = 50,000,000
```

এবং:

```text
type = ALL
```

তখন investigation দরকার।

### Golden Rule

> **EXPLAIN-এর কোনো একটি value দেখে query-কে automatically bad বলবে না।**

Context দেখতে হবে।

---

# 1️⃣1️⃣ `possible_keys`

Database কোন কোন index consider করতে পারে।

Example:

```text
possible_keys
-------------
idx_email
```

মানে:

> `idx_email` potentially useful হতে পারে।

কিন্তু এখনো নিশ্চিত নয় যে database এটা ব্যবহার করবে।

---

# 1️⃣2️⃣ `key` ⭐

Database শেষ পর্যন্ত কোন index choose করেছে।

Example:

```text
possible_keys → idx_email
key           → idx_email
```

Good indication।

কিন্তু:

```text
possible_keys → idx_email
key           → NULL
```

মানে index available ছিল, কিন্তু optimizer সেটি choose করেনি।

---

# 1️⃣3️⃣ কেন Index থাকা সত্ত্বেও ব্যবহার নাও হতে পারে?

অনেক কারণ আছে।

### কারণ ১ — Table ছোট

```text
100 rows
```

Full scan cheaper হতে পারে।

### কারণ ২ — Low selectivity

```text
status = 'ACTIVE'
```

যদি 95% rows ACTIVE হয়, index খুব useful নাও হতে পারে।

### কারণ ৩ — Function ব্যবহার

```sql
WHERE YEAR(order_date) = 2026
```

### কারণ ৪ — Data distribution

Optimizer statistics অনুযায়ী অন্য strategy cheaper হতে পারে।

### কারণ ৫ — Composite index-এর ভুল column usage

```text
INDEX(customer_id, order_date)
```

কিন্তু query করছে শুধু:

```text
order_date
```

---

# 1️⃣4️⃣ `rows` ⭐

`rows` হলো optimizer-এর estimate:

> Query execution-এর সময় আনুমানিক কত rows examine করতে হতে পারে।

Example:

```text
rows = 5
```

vs

```text
rows = 5,000,000
```

সাধারণত প্রথমটা better।

কিন্তু মনে রাখবে:

> `rows` exact result count নয়।

---

# 1️⃣5️⃣ `filtered`

MySQL EXPLAIN output-এ `filtered` আনুমানিক percentage বোঝাতে পারে যে examined rows-এর কত শতাংশ পরবর্তী condition-এ pass করবে।

Example:

```text
rows = 100000
filtered = 1.00
```

Roughly:

```text
100,000 examined
       ↓
~1% passes
```

অর্থাৎ filtering অনেক পরে হচ্ছে—এটা optimization investigation-এর clue হতে পারে।

---

# 1️⃣6️⃣ `Extra` ⭐⭐⭐

`Extra` খুব useful।

এখানে database-এর additional execution information পাওয়া যায়।

Common values:

```text
Using where
Using index
Using filesort
Using temporary
```

---

# 1️⃣7️⃣ `Using where`

মানে WHERE condition apply হচ্ছে।

এটা নিজে problem নয়।

Example:

```sql
WHERE city = 'Dhaka'
```

EXPLAIN-এ:

```text
Using where
```

দেখতে পারো।

---

# 1️⃣8️⃣ `Using index` ⭐

এটা সাধারণত **covering index**-এর মতো situation-এর indication হতে পারে।

Example:

```sql
CREATE INDEX idx_customer_email
ON customers(customer_id, email);
```

Query:

```sql
SELECT customer_id, email
FROM customers
WHERE customer_id = 10;
```

Required columns index-এর মধ্যে থাকলে table data access না করেই result পাওয়া যেতে পারে।

EXPLAIN:

```text
Extra = Using index
```

দেখাতে পারে।

---

# 1️⃣9️⃣ `Using filesort`

এটা sorting operation-এর indication।

Example:

```sql
SELECT *
FROM products
ORDER BY price DESC;
```

যদি appropriate index না থাকে, MySQL-এর EXPLAIN-এ:

```text
Using filesort
```

দেখতে পারো।

⚠️ `filesort` নাম দেখে ধরে নেবে না যে অবশ্যই disk-এর physical file ব্যবহার হচ্ছে।

এটা MySQL-এর sorting execution terminology।

---

# 2️⃣0️⃣ `Using temporary`

Database intermediate result রাখার জন্য temporary structure ব্যবহার করছে।

Example:

```sql
SELECT city, COUNT(*)
FROM customers
GROUP BY city
ORDER BY COUNT(*) DESC;
```

EXPLAIN-এ কখনো:

```text
Using temporary
Using filesort
```

দেখতে পারো।

এগুলো automatically error নয়।

---

# 2️⃣1️⃣ EXPLAIN-এর একটা mental model

EXPLAIN দেখার সময় এই sequence follow করো:

```text
1. কোন table?
       ↓
2. type কী?
       ↓
3. possible_keys কী?
       ↓
4. key কোনটা?
       ↓
5. rows কত?
       ↓
6. filtered কত?
       ↓
7. Extra কী?
```

---

# 2️⃣2️⃣ Slow Query কী?

যে query application-এর জন্য unacceptable time নেয় বা excessive resources ব্যবহার করে, তাকে practically slow query বলা যায়।

Example:

```text
API request
   ↓
Django
   ↓
SQL
   ↓
Database
   ↓
5 seconds
```

User-এর জন্য:

```text
🐌 Slow
```

---

# 2️⃣3️⃣ Slow Query-এর common কারণ

```text
Missing Index
      ↓
Full Table Scan
      ↓
Huge Rows Examined
      ↓
Slow Query
```

আরও:

```text
SELECT *
Large JOIN
Bad JOIN condition
Unnecessary sorting
Large OFFSET
Functions on indexed columns
Too many rows returned
Poor composite index
N+1 queries
```

---

# 2️⃣4️⃣ Example — Slow Query

ধরো:

```sql
SELECT *
FROM orders
WHERE customer_id = 50000;
```

Table:

```text
100 million orders
```

Index নেই।

EXPLAIN:

```text
type = ALL
rows = 100000000
```

এটা warning sign।

---

# 2️⃣5️⃣ Optimization

Create index:

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

তারপর:

```sql
EXPLAIN
SELECT *
FROM orders
WHERE customer_id = 50000;
```

এখন সম্ভবত access method indexed lookup-এর দিকে যাবে।

কিন্তু exact plan database statistics এবং data distribution-এর উপর নির্ভর করবে।

---

# 2️⃣6️⃣ Sargability ⭐

এটা interview-এ আসতে পারে।

**Sargable** condition হলো এমন predicate যা database-কে indexed column efficiently search করতে সাহায্য করতে পারে।

ধরো:

```sql
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01'
```

এটা সাধারণত index-friendly range condition।

অন্যদিকে:

```sql
WHERE YEAR(order_date) = 2026
```

এখানে column-এর উপর function apply করা হচ্ছে।

এতে সাধারণ B-tree index-এর efficient range access বাধাগ্রস্ত হতে পারে।

---

# 2️⃣7️⃣ Bad vs Better

### ❌

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026;
```

### ✅

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01';
```

এবং:

```sql
CREATE INDEX idx_order_date
ON orders(order_date);
```

থাকলে range query-এর জন্য index ব্যবহার করার সুযোগ তৈরি হয়।

---

# 2️⃣8️⃣ `SELECT *` কেন avoid করব?

ধরো:

```text
customers
-------------
id
name
email
phone
address
city
country
created_at
...
```

তোমার দরকার শুধু:

```text
id
name
email
```

কিন্তু তুমি লিখলে:

```sql
SELECT *
FROM customers;
```

Database অনেক unnecessary data retrieve/transfer করতে পারে।

Better:

```sql
SELECT id, name, email
FROM customers;
```

### Golden Rule

> **যা দরকার শুধু সেটাই SELECT করো।**

---

# 2️⃣9️⃣ JOIN Optimization

ধরো:

```sql
SELECT
    c.customer_name,
    o.order_date
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id;
```

Important columns:

```text
customers.customer_id
orders.customer_id
```

`orders.customer_id`-এ suitable index query plan-এর জন্য useful হতে পারে।

```sql
CREATE INDEX idx_orders_customer
ON orders(customer_id);
```

তারপর:

```sql
EXPLAIN
SELECT ...
```

দিয়ে verify করবে।

---

# 3️⃣0️⃣ JOIN + Filter

ধরো:

```sql
SELECT
    c.customer_name,
    o.order_date
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
WHERE c.city = 'Dhaka';
```

এখানে:

```text
city
customer_id
```

দুটোই query-এর অংশ।

কোন index best হবে সেটা workload ও data distribution-এর উপর নির্ভর করবে।

Possible candidates:

```text
customers(city)
orders(customer_id)
```

তারপর EXPLAIN দিয়ে verify।

---

# 3️⃣1️⃣ ORDER BY Optimization

Query:

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20;
```

যদি `product_id` primary key হয়, database ordered index access ব্যবহার করতে পারে।

এটা বড় dataset-এ helpful।

---

# 3️⃣2️⃣ ORDER BY + LIMIT

এই pattern খুব common:

```sql
SELECT *
FROM products
ORDER BY product_id DESC
LIMIT 20;
```

Database-এর জন্য:

```text
Need:
latest/highest 20
```

সব 50 million rows sort না করে suitable index ব্যবহার করার সুযোগ থাকতে পারে।

---

# 3️⃣3️⃣ Pagination Performance

Bad for huge offsets:

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20 OFFSET 5000000;
```

Better scalable approach:

```sql
SELECT *
FROM products
WHERE product_id > 5000000
ORDER BY product_id
LIMIT 20;
```

এটাই **Keyset/Cursor-style pagination** concept।

---

# 3️⃣4️⃣ EXPLAIN ANALYZE ⭐⭐⭐

এখন আসল advanced topic।

`EXPLAIN`:

> Optimizer কী plan করেছে?

`EXPLAIN ANALYZE`:

> Query execute করার সময় বাস্তবে কী ঘটেছে?

MySQL 8+ এবং PostgreSQL-এ syntax/format আলাদা হতে পারে।

### MySQL example

```sql
EXPLAIN ANALYZE
SELECT *
FROM orders
WHERE customer_id = 50000;
```

এটি query execute করে actual execution statistics দেখাতে পারে।

⚠️ তাই `EXPLAIN ANALYZE` read query হলেও **বাস্তবে query execute করে**—production environment-এ ব্যবহার করার আগে সতর্ক থাকবে।

---

# 3️⃣5️⃣ EXPLAIN vs EXPLAIN ANALYZE

|বিষয়|EXPLAIN|EXPLAIN ANALYZE|
|---|---|---|
|Plan|✅|✅|
|Actual execution|সাধারণত না|✅|
|Estimated rows|✅|✅|
|Actual timing|না|✅|
|Actual rows|না|✅|
|Query execute|সাধারণ EXPLAIN-এ না|✅|

---

# 3️⃣6️⃣ Estimated vs Actual

এটা খুব important।

ধরো optimizer বলল:

```text
estimated rows = 10
```

কিন্তু actual execution:

```text
actual rows = 500,000
```

Huge difference!

মানে optimizer-এর estimation ভুল হতে পারে।

এতে query plan খারাপ হতে পারে।

---

# 3️⃣7️⃣ কেন Estimate ভুল হতে পারে?

Possible reasons:

```text
Outdated statistics
Data distribution changed
Skewed data
Correlated columns
Complex predicates
```

Database statistics optimizer-কে plan নির্বাচন করতে সাহায্য করে।

---

# 3️⃣8️⃣ Optimization কখন শুরু করবে?

এই mistake করবে না:

> "EXPLAIN-এ filesort আছে, তাই index বানাই।"

বরং:

```text
User reports slow
       ↓
Measure
       ↓
EXPLAIN
       ↓
Understand bottleneck
       ↓
Create/change index or query
       ↓
Test
       ↓
EXPLAIN again
       ↓
Benchmark
```

---

# 3️⃣9️⃣ Real-World Hotel Example ⭐

আমাদের hotel database:

```text
bookings
----------------
booking_id
customer_id
room_id
check_in
check_out
status
```

Availability query:

```sql
SELECT 1
FROM bookings
WHERE room_id = 101
AND status IN ('PENDING', 'CONFIRMED')
AND check_in < '2026-09-14'
AND check_out > '2026-09-12';
```

ধরো bookings:

```text
20 million rows
```

এখন:

```sql
EXPLAIN
SELECT 1
FROM bookings
WHERE room_id = 101
AND status IN ('PENDING', 'CONFIRMED')
AND check_in < '2026-09-14'
AND check_out > '2026-09-12';
```

তুমি investigate করবে:

```text
type
possible_keys
key
rows
Extra
```

---

# 4️⃣0️⃣ কোন index consider করা যায়?

একটি candidate:

```sql
CREATE INDEX idx_room_dates
ON bookings(room_id, check_in, check_out);
```

কিন্তু `status`-সহ আরও index বানানোর আগে workload এবং actual EXPLAIN plan দেখা উচিত।

কারণ:

> **Best index theoretically নয়—actual workload-এর জন্য effective index।**

---

# 4️⃣1️⃣ Database Designer-এর Optimization Checklist

Slow query পেলে:

### Step 1

Query reproduce করো।

### Step 2

```sql
EXPLAIN
```

চালাও।

### Step 3

দেখো:

```text
type
key
rows
Extra
```

### Step 4

Check করো:

```text
Missing index?
Wrong index?
Composite index order?
Too many rows?
Function on indexed column?
Unnecessary SELECT *?
Large OFFSET?
Expensive JOIN?
Sorting?
```

### Step 5

Optimization করো।

### Step 6

আবার:

```sql
EXPLAIN
```

### Step 7

প্রয়োজনে:

```sql
EXPLAIN ANALYZE
```

দিয়ে actual behavior যাচাই করো।

---

# 4️⃣2️⃣ একটি Complete Example

ধরো:

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026
ORDER BY order_date DESC;
```

### Problem

```text
YEAR(order_date)
```

indexed column-এর উপর function।

### Better query

```sql
SELECT order_id, customer_id, order_date, total_amount
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01'
ORDER BY order_date DESC;
```

Index:

```sql
CREATE INDEX idx_orders_date
ON orders(order_date);
```

তারপর:

```sql
EXPLAIN
SELECT order_id, customer_id, order_date, total_amount
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01'
ORDER BY order_date DESC;
```

তারপর plan compare করবে।

---

# 4️⃣3️⃣ সবচেয়ে গুরুত্বপূর্ণ Mental Model ⭐⭐⭐

Database optimization এভাবে চিন্তা করবে:

```text
                    Query
                      ↓
                   EXPLAIN
                      ↓
        ┌─────────────┼─────────────┐
        ↓             ↓             ↓
      Index          Rows          Extra
        ↓             ↓             ↓
     Used?       Too many?      Sort/temp?
        ↓             ↓             ↓
        └─────────────┼─────────────┘
                      ↓
                  Optimize
                      ↓
                EXPLAIN AGAIN
                      ↓
                 Verify Gain
```

---

# 🧠 Class 60 Golden Rules

```text
1. EXPLAIN → Execution plan বোঝার tool

2. possible_keys → সম্ভাব্য index

3. key → actually selected index

4. rows → estimated rows examined

5. ALL → Usually full table scan

6. ref/range → Often useful indexed access patterns

7. Extra → Additional execution information

8. Using filesort → Sorting operation

9. Using temporary → Temporary intermediate structure

10. EXPLAIN ≠ EXPLAIN ANALYZE

11. EXPLAIN ANALYZE → Actual execution information

12. Function on indexed column → Can hurt index usage

13. SELECT * → Unnecessary data retrieval হতে পারে

14. Large OFFSET → Pagination slow হতে পারে

15. Keyset pagination → Large dataset-এর জন্য scalable approach

16. Index blindly create করবে না

17. EXPLAIN first → Optimize → EXPLAIN again

18. Estimated ≠ Actual
```

---

# 📝 Class 60 Assignment

### Task 1 — Basic EXPLAIN

এই query-এর জন্য EXPLAIN লিখো:

```sql
SELECT *
FROM customers
WHERE email = 'rahim@gmail.com';
```

---

### Task 2 — Identify Problem

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2026;
```

**কেন performance problem হতে পারে?**

এটার optimized version লেখো।

---

### Task 3 — Index

এই query-এর জন্য একটি suitable index propose করো:

```sql
SELECT *
FROM orders
WHERE customer_id = 100
AND order_date >= '2026-01-01'
AND order_date < '2026-02-01';
```

---

### Task 4 — EXPLAIN Interpretation

ধরো EXPLAIN output:

```text
type = ALL
possible_keys = idx_customer
key = NULL
rows = 10,000,000
```

এখানে কী বুঝবে?

---

### Task 5 — Concept

Difference লেখো:

```text
EXPLAIN
vs
EXPLAIN ANALYZE
```

---

### 🔥 Task 6 — Pagination Challenge

Products table-এ 50 million rows আছে।

কোনটা prefer করবে?

**A**

```sql
SELECT *
FROM products
ORDER BY product_id
LIMIT 20 OFFSET 5000000;
```

**B**

```sql
SELECT *
FROM products
WHERE product_id > 5000000
ORDER BY product_id
LIMIT 20;
```

**A/B + কেন** লিখবে।

---

### 🎯 Interview Challenge

একজন interviewer বলল:

> **"Your Django API is taking 5 seconds to return a list of customers. How would you investigate and optimize it?"**

তুমি যদি এই প্রশ্নের উত্তর **Database Designer/Backend Developer হিসেবে** দিতে পারো, তাহলে Class 59–60-এর concepts practically বুঝেছ।

**Next: Class 61 — Advanced SQL: Recursive CTE, Advanced Window Functions & Cursors.**

---
# 📚 Class 61 — Advanced SQL: Recursive CTE, Advanced Window Functions & Cursors

আজকের class-এ আমরা SQL-এর **advanced programming + analytical features** শিখব।

Class 38-এ আমরা সাধারণ CTE শিখেছিলাম। আজ সেটাকে আরও advanced level-এ নিয়ে যাব।

### আজকের Topics

1. Recursive CTE
    
2. Hierarchical Data
    
3. Employee → Manager Tree
    
4. Recursive CTE-এর stopping condition
    
5. Advanced Window Functions
    
6. Window Frame
    
7. `FIRST_VALUE()`
    
8. `LAST_VALUE()`
    
9. `NTH_VALUE()`
    
10. `PERCENT_RANK()`
    
11. `CUME_DIST()`
    
12. `NTILE()`
    
13. Cursors
    
14. Cursor কখন ব্যবহার করা হয়
    
15. Cursor বনাম Set-based SQL
    
16. Real-world examples
    
17. Database Designer best practices
    

---

# Part 1 — Recursive CTE

## 1️⃣ Recursive CTE কী?

সাধারণ CTE:

```sql
WITH sales AS (
    SELECT *
    FROM orders
)
SELECT *
FROM sales;
```

এটা একবার query করে result তৈরি করে।

কিন্তু **Recursive CTE নিজেকেই reference করতে পারে।**

অর্থাৎ:

```text
CTE
 ↓
নিজেকে আবার call
 ↓
নতুন row
 ↓
আবার নিজেকে call
 ↓
...
```

এটা বিশেষভাবে useful:

- Organization hierarchy
    
- Employee → Manager
    
- Category → Subcategory
    
- Folder → Subfolder
    
- Parent → Child
    
- Tree structure
    
- Number/date sequence
    

---

# 2️⃣ Recursive CTE-এর Basic Structure

Structure:

```sql
WITH RECURSIVE cte_name AS (

    -- Anchor
    SELECT ...

    UNION ALL

    -- Recursive
    SELECT ...
    FROM cte_name
    WHERE ...

)

SELECT *
FROM cte_name;
```

এখানে দুইটা অংশ:

```text
Anchor
   ↓
Starting rows

Recursive
   ↓
Next rows
```

---

# 3️⃣ Anchor Member কী?

Anchor হলো recursion-এর **starting point**।

Example:

```sql
SELECT 1 AS number
```

এখান থেকে শুরু:

```text
1
```

---

# 4️⃣ Recursive Member কী?

Recursive part previous result-এর উপর কাজ করে।

```sql
SELECT number + 1
FROM numbers
WHERE number < 10
```

তাহলে:

```text
1
↓
2
↓
3
↓
4
↓
...
↓
10
```

---

# 5️⃣ প্রথম Recursive CTE Example ⭐

1 থেকে 10 পর্যন্ত number:

```sql
WITH RECURSIVE numbers AS (

    SELECT 1 AS number

    UNION ALL

    SELECT number + 1
    FROM numbers
    WHERE number < 10
)

SELECT *
FROM numbers;
```

Output:

```text
number
------
1
2
3
4
5
6
7
8
9
10
```

---

# 6️⃣ এটা কীভাবে কাজ করছে?

Step by step:

```text
Anchor:
1

Recursive:
1 + 1 = 2

2 + 1 = 3

3 + 1 = 4

...

9 + 1 = 10
```

তারপর:

```text
number = 10
```

এখন:

```sql
WHERE number < 10
```

false।

তাই recursion stop।

---

# 7️⃣ Stopping Condition ⭐⭐⭐

Recursive CTE-তে সবচেয়ে important বিষয়:

> **Recursion কখন stop করবে সেটা অবশ্যই design করতে হবে।**

Example:

```sql
WHERE number < 10
```

না থাকলে recursion চলতে থাকবে/DBMS recursion limit-এ গিয়ে error দিতে পারে।

### Golden Rule

```text
Recursive CTE
     ↓
Start
     ↓
Generate next
     ↓
Check condition
     ↓
Stop?
  ↙     ↘
No       Yes
↓         ↓
Repeat    Finish
```

---

# 8️⃣ Date Sequence তৈরি করা

ধরো:

```text
2026-09-01
থেকে
2026-09-07
```

```sql
WITH RECURSIVE dates AS (

    SELECT DATE('2026-09-01') AS date_value

    UNION ALL

    SELECT DATE_ADD(date_value, INTERVAL 1 DAY)
    FROM dates
    WHERE date_value < '2026-09-07'
)

SELECT *
FROM dates;
```

Output:

```text
2026-09-01
2026-09-02
2026-09-03
2026-09-04
2026-09-05
2026-09-06
2026-09-07
```

এটা analytics-এ useful।

---

# 9️⃣ Hierarchical Data

এখন আসল real-world example।

ধরো company:

```text
CEO
│
├── Manager A
│   ├── Employee 1
│   └── Employee 2
│
└── Manager B
    ├── Employee 3
    └── Employee 4
```

এখানে employee table:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    manager_id INT
);
```

Data:

```text
employee_id | name        | manager_id
---------------------------------------
1           | CEO         | NULL
2           | Manager A   | 1
3           | Employee 1  | 2
4           | Employee 2  | 2
5           | Manager B   | 1
6           | Employee 3  | 5
7           | Employee 4  | 5
```

এখানে:

```text
manager_id
```

নিজের table-এর:

```text
employee_id
```

কে reference করছে।

এটাকে **self-referencing relationship** বলে।

---

# 🔟 Recursive CTE দিয়ে hierarchy

CEO থেকে শুরু করে পুরো hierarchy বের করি:

```sql
WITH RECURSIVE employee_tree AS (

    -- Anchor
    SELECT
        employee_id,
        name,
        manager_id,
        0 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    -- Recursive
    SELECT
        e.employee_id,
        e.name,
        e.manager_id,
        et.level + 1
    FROM employees e
    JOIN employee_tree et
        ON e.manager_id = et.employee_id
)

SELECT *
FROM employee_tree
ORDER BY level, employee_id;
```

Output conceptually:

```text
employee       level
--------------------
CEO              0
Manager A        1
Manager B        1
Employee 1       2
Employee 2       2
Employee 3       2
Employee 4       2
```

---

# 1️⃣1️⃣ `level` কেন রাখলাম?

```sql
0 AS level
```

CEO:

```text
level = 0
```

Manager:

```text
level = 1
```

Employee:

```text
level = 2
```

এতে hierarchy depth বোঝা যায়।

---

# 1️⃣2️⃣ Recursive CTE-এর Real Applications

```text
Organization
      ↓
Employee hierarchy

E-commerce
      ↓
Category hierarchy

File system
      ↓
Folder → Subfolder

Location
      ↓
Country → State → City

Comments
      ↓
Parent comment → Reply
```

---

# Part 2 — Advanced Window Functions

Class 39–40-এ আমরা Window Functions শিখেছি।

আজ আরও advanced functions দেখব।

---

# 1️⃣3️⃣ `FIRST_VALUE()`

একটি partition/group-এর প্রথম value বের করে।

Example:

```sql
SELECT
    employee_id,
    department,
    salary,
    FIRST_VALUE(salary) OVER (
        PARTITION BY department
        ORDER BY salary DESC
    ) AS highest_salary
FROM employees;
```

Output concept:

```text
department | salary | highest_salary
------------------------------------
IT         | 90000  | 90000
IT         | 70000  | 90000
IT         | 50000  | 90000

HR         | 80000  | 80000
HR         | 60000  | 80000
```

---

# 1️⃣4️⃣ `LAST_VALUE()` ⚠️

এখানে common mistake আছে।

অনেকে লিখে:

```sql
LAST_VALUE(salary) OVER (
    PARTITION BY department
    ORDER BY salary
)
```

এবং আশা করে:

> পুরো department-এর lowest salary আসবে।

কিন্তু default window frame-এর কারণে result অনেক সময় প্রত্যাশামতো হবে না।

সঠিকভাবে পুরো partition-এর last value পেতে:

```sql
LAST_VALUE(salary) OVER (
    PARTITION BY department
    ORDER BY salary
    ROWS BETWEEN
        UNBOUNDED PRECEDING
        AND UNBOUNDED FOLLOWING
) AS lowest_salary
```

### Golden Rule ⭐

`LAST_VALUE()` ব্যবহার করলে **window frame explicitly বুঝতে হবে**।

---

# 1️⃣5️⃣ Window Frame

Window frame মানে:

> Current row-এর জন্য window-এর কোন rows consider হবে।

Example:

```sql
ROWS BETWEEN
2 PRECEDING
AND CURRENT ROW
```

মানে:

```text
2 rows before
+
current row
```

---

# 1️⃣6️⃣ Moving Average

ধরো monthly sales:

```text
Jan 100
Feb 200
Mar 300
Apr 400
```

3-month moving average:

```sql
SELECT
    month,
    sales,
    AVG(sales) OVER (
        ORDER BY month
        ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
    ) AS moving_avg
FROM monthly_sales;
```

Concept:

```text
Jan → 100

Feb → (100+200)/2

Mar → (100+200+300)/3

Apr → (200+300+400)/3
```

---

# 1️⃣7️⃣ `NTH_VALUE()`

Partition-এর N-th value বের করে।

Example:

```sql
SELECT
    employee_id,
    department,
    salary,
    NTH_VALUE(salary, 2) OVER (
        PARTITION BY department
        ORDER BY salary DESC
        ROWS BETWEEN
            UNBOUNDED PRECEDING
            AND UNBOUNDED FOLLOWING
    ) AS second_highest
FROM employees;
```

এখানে:

```text
N = 2
```

অর্থাৎ second value।

---

# 1️⃣8️⃣ `NTILE()`

Rows-কে প্রায় সমান সংখ্যক group/bucket-এ ভাগ করে।

Example:

```sql
SELECT
    employee_id,
    salary,
    NTILE(4) OVER (
        ORDER BY salary DESC
    ) AS salary_quartile
FROM employees;
```

Output:

```text
salary | quartile
-----------------
90000  | 1
85000  | 1
80000  | 2
70000  | 2
60000  | 3
50000  | 3
40000  | 4
30000  | 4
```

এখানে:

```text
1 → Top 25%
2 → Next 25%
3 → Next 25%
4 → Bottom 25%
```

Exact row distribution depends on number of rows.

---

# 1️⃣9️⃣ `PERCENT_RANK()`

একটি row-এর relative rank percentage হিসেবে দেখায়।

```sql
SELECT
    employee_id,
    salary,
    PERCENT_RANK() OVER (
        ORDER BY salary
    ) AS percentile_rank
FROM employees;
```

Conceptually:

```text
Lowest → 0
Highest → 1
```

মাঝের rows-এর value 0 থেকে 1-এর মধ্যে।

---

# 2️⃣0️⃣ `CUME_DIST()`

Cumulative distribution।

```sql
SELECT
    employee_id,
    salary,
    CUME_DIST() OVER (
        ORDER BY salary
    ) AS cumulative_distribution
FROM employees;
```

এটা বলে:

> বর্তমান salary-এর চেয়ে **less than or equal** salary কত proportion rows-এর মধ্যে আছে।

---

# 2️⃣1️⃣ PERCENT_RANK vs CUME_DIST

|Function|ধারণা|
|---|---|
|`PERCENT_RANK()`|Relative rank|
|`CUME_DIST()`|Cumulative distribution|

সহজভাবে:

```text
PERCENT_RANK → আমার rank কোথায়?
CUME_DIST    → আমার value পর্যন্ত কতজন?
```

---

# 2️⃣2️⃣ Advanced Ranking Example

ধরো employee salary:

```text
100k
90k
80k
70k
60k
50k
```

আমরা একসাথে:

```sql
SELECT
    employee_id,
    salary,

    ROW_NUMBER() OVER (
        ORDER BY salary DESC
    ) AS row_num,

    RANK() OVER (
        ORDER BY salary DESC
    ) AS rank_num,

    DENSE_RANK() OVER (
        ORDER BY salary DESC
    ) AS dense_rank_num,

    NTILE(4) OVER (
        ORDER BY salary DESC
    ) AS quartile,

    PERCENT_RANK() OVER (
        ORDER BY salary DESC
    ) AS percent_rank

FROM employees;
```

এতে এক query-তে multiple analytical metrics পাওয়া যায়।

---

# Part 3 — Cursors

এখন SQL-এর আরেকটা advanced topic।

## 2️⃣3️⃣ Cursor কী?

Cursor হলো database-এর result set-এর rows **একটি করে process করার mechanism**।

সাধারণ SQL:

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department = 'IT';
```

এটা **set-based operation**।

Database এক operation-এ matching rows process করতে পারে।

Cursor approach:

```text
Row 1 → process
Row 2 → process
Row 3 → process
Row 4 → process
...
```

---

# 2️⃣4️⃣ Cursor কেন দরকার?

কিছু procedural logic-এ row-by-row processing প্রয়োজন হতে পারে।

যেমন:

```text
Employee list
   ↓
Each employee
   ↓
Complex calculation
   ↓
Special business rule
   ↓
Generate result
```

কিন্তু গুরুত্বপূর্ণ কথা:

> **Cursor হলো advanced tool; default solution নয়।**

---

# 2️⃣5️⃣ Cursor-এর Basic Flow

MySQL stored procedure-এ সাধারণ flow:

```text
DECLARE cursor
      ↓
OPEN cursor
      ↓
FETCH row
      ↓
Process row
      ↓
FETCH next
      ↓
No more rows?
      ↓
CLOSE cursor
```

---

# 2️⃣6️⃣ Cursor Example

ধরো employees:

```text
employee_id
name
salary
```

Procedure-এর ভিতরে cursor:

```sql
DELIMITER //

CREATE PROCEDURE process_employees()
BEGIN

    DECLARE done INT DEFAULT FALSE;
    DECLARE emp_id INT;
    DECLARE emp_salary DECIMAL(10,2);

    DECLARE emp_cursor CURSOR FOR
        SELECT employee_id, salary
        FROM employees;

    DECLARE CONTINUE HANDLER FOR NOT FOUND
        SET done = TRUE;

    OPEN emp_cursor;

    read_loop: LOOP

        FETCH emp_cursor
        INTO emp_id, emp_salary;

        IF done THEN
            LEAVE read_loop;
        END IF;

        -- process current employee

    END LOOP;

    CLOSE emp_cursor;

END //

DELIMITER ;
```

এখানে অনেক syntax আছে, তাই concept আগে বুঝো।

---

# 2️⃣7️⃣ Cursor-এর Important Parts

### Cursor declaration

```sql
DECLARE emp_cursor CURSOR FOR
SELECT employee_id, salary
FROM employees;
```

---

### Open

```sql
OPEN emp_cursor;
```

---

### Fetch

```sql
FETCH emp_cursor
INTO emp_id, emp_salary;
```

---

### Close

```sql
CLOSE emp_cursor;
```

---

# 2️⃣8️⃣ `NOT FOUND Handler`

Cursor যখন আর কোনো row পায় না:

```sql
DECLARE CONTINUE HANDLER FOR NOT FOUND
    SET done = TRUE;
```

তারপর:

```sql
IF done THEN
    LEAVE read_loop;
END IF;
```

মানে:

```text
No more rows
      ↓
done = TRUE
      ↓
Exit loop
```

---

# 2️⃣9️⃣ Cursor vs Set-Based SQL ⭐⭐⭐

এটা খুব important।

### Cursor

```text
Row 1
 ↓
Row 2
 ↓
Row 3
 ↓
...
```

### Set-based

```text
Whole matching set
       ↓
One SQL operation
```

সাধারণভাবে:

> **Set-based SQL prefer করবে।**

---

# 3️⃣0️⃣ Example

ধরো সবাইকে 10% salary increase দিতে হবে।

### ❌ Cursor unnecessary

```text
Employee 1 → update
Employee 2 → update
Employee 3 → update
...
```

### ✅ Set-based

```sql
UPDATE employees
SET salary = salary * 1.10;
```

এটা simpler এবং সাধারণত বেশি efficient।

---

# 3️⃣1️⃣ Cursor কখন ব্যবহার করব?

Cursor consider করা যেতে পারে যখন:

```text
Complex row-specific logic
        +
Set-based SQL দিয়ে সহজে express করা যায় না
```

উদাহরণ:

```text
Row
 ↓
Complex procedural calculation
 ↓
External-like sequencing/business logic
 ↓
Next row
```

তবে অনেক ক্ষেত্রে cursor-এর বদলে application code, batch processing, অথবা set-based SQL ভালো solution হতে পারে।

---

# 3️⃣2️⃣ Cursor-এর Disadvantages

```text
Slower
More procedural
More resource usage
Harder to maintain
Large datasets-এ problematic হতে পারে
```

বিশেষ করে:

```text
1 million rows
```

কে একে একে process করলে overhead হতে পারে।

---

# 3️⃣3️⃣ Database Designer হিসেবে Priority

তোমার priority:

```text
1. Set-based SQL
       ↓
2. Optimized Query
       ↓
3. Batch Processing
       ↓
4. Application Logic
       ↓
5. Cursor — যখন সত্যিই দরকার
```

এটা absolute rule নয়, কিন্তু good engineering mindset।

---

# 3️⃣4️⃣ Recursive CTE vs Cursor

|Feature|Recursive CTE|Cursor|
|---|---|---|
|Main purpose|Hierarchy/recursive query|Row-by-row processing|
|Style|Declarative|Procedural|
|Tree data|⭐⭐⭐|সাধারণত না|
|Sequence|⭐⭐⭐|সম্ভব|
|Large dataset|Query-dependent|Often expensive|
|Preferred|যখন recursion দরকার|যখন row-by-row logic unavoidable|

---

# 3️⃣5️⃣ Real-World Example — Category Tree

ধরো:

```text
Electronics
├── Laptop
│   ├── Gaming Laptop
│   └── Business Laptop
└── Phone
    ├── Android
    └── iPhone
```

Table:

```text
categories
----------------
category_id
name
parent_id
```

Recursive CTE:

```sql
WITH RECURSIVE category_tree AS (

    SELECT
        category_id,
        name,
        parent_id,
        0 AS level
    FROM categories
    WHERE parent_id IS NULL

    UNION ALL

    SELECT
        c.category_id,
        c.name,
        c.parent_id,
        ct.level + 1
    FROM categories c
    JOIN category_tree ct
        ON c.parent_id = ct.category_id
)

SELECT *
FROM category_tree
ORDER BY level, category_id;
```

এটাই real-world application:

```text
Django
   ↓
Category API
   ↓
Recursive SQL
   ↓
Nested category tree
```

---

# 3️⃣6️⃣ Recursive CTE-এর সবচেয়ে বড় Mistake

এই query:

```sql
WITH RECURSIVE numbers AS (
    SELECT 1

    UNION ALL

    SELECT number + 1
    FROM numbers
)
SELECT *
FROM numbers;
```

এখানে stopping condition নেই।

❌ Dangerous.

Better:

```sql
WHERE number < 100
```

### Golden Rule

> **Recursive query-তে termination condition design করো।**

---

# 3️⃣7️⃣ Class 61 Complete Mental Model

```text
                 Advanced SQL
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
   Recursive CTE            Window Functions
          ↓                       ↓
 Hierarchical Data          Advanced Analytics
          ↓                       ↓
 Parent → Child             Ranking
 Tree                        Distribution
 Sequence                    Moving Analysis
          │
          └───────────┬───────────┘
                      ↓
                   Cursor
                      ↓
             Row-by-row processing
```

---

# 🧠 Class 61 Golden Rules

```text
1. Recursive CTE → CTE নিজেকে reference করতে পারে

2. Anchor → Starting point

3. Recursive member → Next rows generate করে

4. Recursive CTE → Termination condition দরকার

5. Hierarchical data → Recursive CTE-এর major use case

6. FIRST_VALUE → First value

7. LAST_VALUE → Window frame carefully define করতে হয়

8. NTH_VALUE → N-th value

9. NTILE → Rows into buckets

10. PERCENT_RANK → Relative rank

11. CUME_DIST → Cumulative distribution

12. Window frame → কোন rows consider হবে

13. Cursor → Row-by-row processing

14. OPEN → Cursor শুরু

15. FETCH → Row আনা

16. CLOSE → Cursor বন্ধ

17. NOT FOUND → Cursor শেষ

18. Set-based SQL → সাধারণত cursor-এর আগে prefer

19. Cursor → যখন row-by-row logic সত্যিই দরকার

20. Recursive CTE ≠ Cursor
```

---

# 📝 Class 61 Assignment

### Task 1 — Recursive Number

Recursive CTE ব্যবহার করে:

```text
1 → 20
```

generate করো।

---

### Task 2 — Date

এই date range generate করো:

```text
2026-09-01
to
2026-09-10
```

Recursive CTE দিয়ে।

---

### Task 3 — Employee Hierarchy ⭐

এই table:

```text
employees
-----------------------------
id
name
manager_id
```

থেকে CEO থেকে সব employee-এর hierarchy বের করো এবং:

```text
employee_id
name
manager_id
level
```

দেখাও।

---

### Task 4 — Window Function

Employee table থেকে বের করো:

```text
employee_id
department
salary
highest_salary_in_department
lowest_salary_in_department
```

`FIRST_VALUE()` এবং `LAST_VALUE()` ব্যবহার করে।

---

### Task 5 — NTILE

Employees-কে salary অনুযায়ী 4 group-এ ভাগ করো:

```text
1 → Top 25%
2 → 25–50%
3 → 50–75%
4 → Bottom 25%
```

`NTILE(4)` ব্যবহার করে।

---

### Task 6 — Concept

Explain করো:

```text
Recursive CTE
vs
Cursor
```

কখন কোনটা ব্যবহার করবে?

---

# 🔥 Interview Challenge

Interviewer জিজ্ঞেস করল:

> **"You have an employee table where every employee stores their manager_id. How would you retrieve the complete management hierarchy starting from the CEO?"**

Best answer-এর core হবে:

```text
Self-referencing relationship
        ↓
Recursive CTE
        ↓
Anchor = CEO
        ↓
Recursive JOIN = manager_id → employee_id
        ↓
level/depth
        ↓
Termination
```

এটা বুঝতে পারলে তুমি SQL-এর **advanced querying level**-এ ঢুকে গেছ।

**পরবর্তী: Class 62 — Advanced Transactions & Isolation Levels** — এখানে আমরা real-world banking, hotel booking, inventory এবং concurrent transactions আরও গভীরভাবে দেখব।

----
# 📚 Class 62 — Advanced Transactions & Isolation Levels

আজকের class-এ আমরা **Transaction + Concurrency + Isolation Level**-কে আরও গভীরে বুঝব।

Class 48-এ আমরা ACID এবং basic transaction শিখেছিলাম। Class 58-এ locking-এর introduction পেয়েছিলে। আজকের লক্ষ্য হলো:

> **একই সময়ে অনেক user database ব্যবহার করলে data কীভাবে correct রাখা যায়?**

---

# 🎯 আজকে যা শিখব

1. Transaction আবার একটু গভীরভাবে
    
2. Concurrency কী?
    
3. Isolation কেন দরকার?
    
4. Dirty Read
    
5. Non-Repeatable Read
    
6. Phantom Read
    
7. Lost Update
    
8. Isolation Levels
    
9. READ UNCOMMITTED
    
10. READ COMMITTED
    
11. REPEATABLE READ
    
12. SERIALIZABLE
    
13. Snapshot/MVCC concept
    
14. `SELECT ... FOR UPDATE`
    
15. Optimistic vs Pessimistic concurrency
    
16. Hotel booking example
    
17. Inventory example
    
18. Django `transaction.atomic()`
    
19. Production best practices
    

---

# 1️⃣ Transaction কী?

Transaction হলো database operation-এর একটি **logical unit of work**।

ধরো bank transfer:

```text
Account A → -1000
Account B → +1000
```

দুটো operation-ই সফল হতে হবে।

```text
A -1000 ✅
B +1000 ✅
```

তাহলে:

```sql
COMMIT;
```

কিন্তু:

```text
A -1000 ✅
B +1000 ❌
```

হলে পুরো transaction rollback করতে চাই:

```sql
ROLLBACK;
```

---

# 2️⃣ ACID আবার মনে করি

```text
A → Atomicity
C → Consistency
I → Isolation
D → Durability
```

### Atomicity

```text
সব হবে
অথবা
কিছুই হবে না
```

### Consistency

Database valid state-এ থাকবে।

### Isolation

এক transaction-এর intermediate কাজ অন্য concurrent transaction-এর জন্য কীভাবে visible হবে তা নিয়ন্ত্রণ করে।

### Durability

COMMIT-এর পর data persist করবে।

---

# 3️⃣ Concurrency কী?

ধরো hotel website-এ একই room:

```text
Room 101
```

এবং একই সময়ে:

```text
User A → Room 101 book করতে চায়
User B → Room 101 book করতে চায়
```

দুটো request একই সময়ে database-এ এলো।

```text
User A ─────┐
            ├──→ Database
User B ─────┘
```

এটাই concurrency।

---

# 4️⃣ Problem কোথায়?

ধরো available room:

```text
Room 101 = AVAILABLE
```

দুই transaction:

```text
T1 → check room
T2 → check room
```

দুটোই দেখে:

```text
AVAILABLE
```

তারপর:

```text
T1 → booking
T2 → booking
```

ফলে:

```text
❌ Double Booking
```

এটাই concurrency problem-এর classic example।

---

# 5️⃣ Isolation কেন দরকার?

এক transaction-এর কাজ অন্য transaction-এর সঙ্গে কীভাবে interact করবে সেটা control করতে হয়।

```text
Transaction A
       ↕
   Isolation
       ↕
Transaction B
```

Isolation ঠিকভাবে না থাকলে বিভিন্ন anomaly হতে পারে।

---

# 6️⃣ Four Important Problems ⭐⭐⭐

মনে রাখবে:

```text
1. Dirty Read
2. Non-Repeatable Read
3. Phantom Read
4. Lost Update
```

---

# 7️⃣ Dirty Read

Transaction A এমন data পড়ল যেটা Transaction B পরিবর্তন করেছে কিন্তু এখনো COMMIT করেনি।

Example:

### T1

```sql
START TRANSACTION;

UPDATE accounts
SET balance = 5000
WHERE account_id = 1;
```

এখনো:

```text
COMMIT হয়নি
```

### T2

```sql
SELECT balance
FROM accounts
WHERE account_id = 1;
```

T2 যদি `5000` দেখে, কিন্তু T1 পরে:

```sql
ROLLBACK;
```

তাহলে T2 এমন data পড়েছিল যা শেষ পর্যন্ত database-এ থাকলই না।

এটাই:

> **Dirty Read**

---

# 8️⃣ Non-Repeatable Read

এক transaction একই row দুইবার পড়ে কিন্তু দুইবার different value পায়।

### T1

```sql
SELECT balance
FROM accounts
WHERE account_id = 1;
```

Result:

```text
10000
```

এর মধ্যে T2:

```sql
UPDATE accounts
SET balance = 8000
WHERE account_id = 1;

COMMIT;
```

T1 আবার:

```sql
SELECT balance
FROM accounts
WHERE account_id = 1;
```

Result:

```text
8000
```

একই transaction-এর মধ্যে:

```text
First read  → 10000
Second read → 8000
```

এটাই:

> **Non-Repeatable Read**

---

# 9️⃣ Phantom Read

এবার row-এর value বদলায়নি।

বরং **নতুন matching rows** এসেছে।

ধরো T1:

```sql
SELECT *
FROM orders
WHERE customer_id = 10;
```

Result:

```text
3 rows
```

এর মধ্যে T2:

```sql
INSERT INTO orders (...)
VALUES (..., 10, ...);

COMMIT;
```

T1 আবার একই query চালালো:

```sql
SELECT *
FROM orders
WHERE customer_id = 10;
```

এবার:

```text
4 rows
```

নতুন matching row যেন "phantom" হিসেবে দেখা দিল।

এটাই:

> **Phantom Read**

---

# 🔟 Lost Update

দুই transaction একই data read করে এবং পরে update করে।

ধরো:

```text
stock = 10
```

### T1

```text
read → 10
```

### T2

```text
read → 10
```

T1:

```text
10 - 3 = 7
```

T2:

```text
10 - 5 = 5
```

তারপর:

```text
T1 → stock = 7
T2 → stock = 5
```

T1-এর update effectively হারিয়ে গেল।

এটাই:

> **Lost Update**

---

# 1️⃣1️⃣ Isolation Levels ⭐⭐⭐

SQL standard-এ commonly চারটি isolation level:

```text
READ UNCOMMITTED
       ↓
READ COMMITTED
       ↓
REPEATABLE READ
       ↓
SERIALIZABLE
```

সাধারণভাবে নিচের দিকে গেলে isolation stronger হয়, তবে concurrency/performance trade-off থাকে।

---

# 1️⃣2️⃣ READ UNCOMMITTED

সবচেয়ে weak standard isolation level।

এখানে dirty read সম্ভব।

Concept:

```text
T1 changes data
       ↓
T2 may see uncommitted data
```

### Advantage

Concurrency বেশি হতে পারে।

### Disadvantage

Data consistency খুব weak।

সাধারণ business transaction-এর জন্য সাধারণত desirable নয়।

---

# 1️⃣3️⃣ READ COMMITTED

এখানে:

> অন্য transaction-এর **uncommitted changes** পড়বে না।

অর্থাৎ:

```text
Dirty Read → ❌
```

কিন্তু:

```text
Non-Repeatable Read → সম্ভব
Phantom Read → DBMS/implementation অনুযায়ী handling ভিন্ন হতে পারে
```

Example:

```sql
SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

---

# 1️⃣4️⃣ REPEATABLE READ ⭐

এক transaction-এর মধ্যে একই row বারবার পড়লে consistent view পাওয়ার লক্ষ্য থাকে।

```text
First read  → 10000
Second read → 10000
```

এটি database implementation-এর উপর নির্ভর করে MVCC/snapshot mechanisms ব্যবহার করতে পারে।

### MySQL InnoDB

MySQL InnoDB-এর default isolation level সাধারণত:

> **REPEATABLE READ**

Check:

```sql
SELECT @@transaction_isolation;
```

---

# 1️⃣5️⃣ SERIALIZABLE

সবচেয়ে strong standard isolation level।

Conceptually concurrent transactions এমনভাবে execute হওয়ার guarantee পেতে পারে যেন তারা serial order-এ execute হয়েছে।

```text
T1
 ↓
T2
 ↓
T3
```

Concurrency কমে যেতে পারে।

Potential result:

```text
More locking/contention
      ↓
Less concurrency
      ↓
Potentially lower throughput
```

তবে exact behavior DBMS-এর implementation-এর উপর নির্ভর করে।

---

# 1️⃣6️⃣ Isolation Comparison ⭐

|Isolation|Dirty Read|Non-Repeatable|Phantom|
|---|---|---|---|
|READ UNCOMMITTED|Possible|Possible|Possible|
|READ COMMITTED|Prevented|Possible|Possible|
|REPEATABLE READ|Prevented|Prevented for consistent reads|DBMS-dependent|
|SERIALIZABLE|Prevented|Prevented|Prevented|

এখানে একটা important point:

> SQL standard-এর anomaly table এবং বাস্তব DBMS-এর implementation একেবারে identical নয়।

বিশেষ করে **MySQL InnoDB** MVCC ও locking ব্যবহার করে।

---

# 1️⃣7️⃣ MVCC কী?

MVCC = **Multi-Version Concurrency Control**

সহজভাবে:

> Database একই data-এর বিভিন্ন version ব্যবহার করে concurrent reads/writes manage করতে পারে।

Concept:

```text
Row
 ↓
Version 1
Version 2
Version 3
```

একজন transaction পুরনো consistent version দেখতে পারে, আর অন্য transaction নতুন committed version নিয়ে কাজ করতে পারে।

এতে read/write concurrency improve করা যায়।

---

# 1️⃣8️⃣ MVCC-এর সহজ উদাহরণ

ধরো:

```text
balance = 10000
```

T1 update করছে:

```text
balance = 8000
```

একই সময়ে T2 consistent read করছে।

MVCC implementation অনুযায়ী T2 তার transaction-এর জন্য appropriate committed version দেখতে পারে।

এতে সব read-এর জন্য blocking lock দরকার হয় না।

---

# 1️⃣9️⃣ `SELECT ... FOR UPDATE` ⭐⭐⭐

এখন খুব important।

ধরো hotel booking:

```sql
START TRANSACTION;

SELECT *
FROM rooms
WHERE room_id = 101
FOR UPDATE;
```

`FOR UPDATE` transactional context-এ selected rows-এর উপর update-oriented lock নিতে বলে।

তারপর:

```sql
-- check availability

INSERT INTO bookings (...);

COMMIT;
```

এখানে অন্য concurrent transaction একই locked resource update করতে চাইলে অপেক্ষা করতে হতে পারে।

---

# 2️⃣0️⃣ Hotel Booking Example

ধরো:

```text
Room 101
```

দুই user:

```text
User A → Book
User B → Book
```

### T1

```sql
START TRANSACTION;

SELECT *
FROM rooms
WHERE room_id = 101
FOR UPDATE;
```

এখন relevant row lock হয়েছে।

তারপর:

```text
Check availability
      ↓
Create booking
      ↓
COMMIT
```

### T2

একই room-এর locked row access/update করতে গেলে তাকে T1-এর transaction শেষ হওয়ার জন্য অপেক্ষা করতে হতে পারে।

এতে race condition control করা সহজ হয়।

---

# 2️⃣1️⃣ কিন্তু একটা গুরুত্বপূর্ণ বিষয় ⚠️

শুধু:

```sql
SELECT ...
FOR UPDATE
```

লিখলেই hotel double-booking problem magically solved হবে না।

তোমাকে পুরো transaction এবং overlap logic সঠিকভাবে design করতে হবে।

যেমন:

```text
BEGIN
 ↓
Lock relevant resource
 ↓
Check overlapping booking
 ↓
If available
    ↓
Create booking
 ↓
COMMIT
```

---

# 2️⃣2️⃣ Inventory Example

ধরো:

```text
stock = 10
```

দুই user:

```text
User A buys 7
User B buys 5
```

Naive approach:

```text
A reads 10
B reads 10

A → 3
B → 5
```

Incorrect result হতে পারে।

Better atomic update:

```sql
UPDATE products
SET stock = stock - 7
WHERE product_id = 10
AND stock >= 7;
```

তারপর application check করবে:

```text
affected rows = 1?
```

হলে সফল।

তারপর B:

```sql
UPDATE products
SET stock = stock - 5
WHERE product_id = 10
AND stock >= 5;
```

যদি stock insufficient হয়:

```text
affected rows = 0
```

---

# 2️⃣3️⃣ Atomic UPDATE কেন Powerful?

কারণ:

```text
Read stock
   ↓
Calculate
   ↓
Write stock
```

এর বদলে database-এর condition-এর ভিতরেই:

```text
UPDATE
WHERE stock >= requested_quantity
```

দেওয়া হয়েছে।

এতে race condition reduce করার ভালো সুযোগ তৈরি হয়।

---

# 2️⃣4️⃣ Optimistic Concurrency

এখানে আমরা ধরে নিই:

> Conflict খুব frequent নয়।

তাই আগে lock না করে version check করি।

Table:

```text
id
stock
version
```

Current:

```text
stock = 10
version = 5
```

Application update করে:

```sql
UPDATE products
SET
    stock = 7,
    version = version + 1
WHERE product_id = 10
AND version = 5;
```

যদি:

```text
affected rows = 1
```

Success।

যদি:

```text
affected rows = 0
```

তাহলে অন্য transaction আগে update করেছে।

এটাই conflict detection।

---

# 2️⃣5️⃣ Pessimistic Concurrency

এখানে assumption:

> Conflict হতে পারে, তাই আগে থেকেই lock করি।

Example:

```sql
SELECT *
FROM products
WHERE product_id = 10
FOR UPDATE;
```

তারপর update।

---

# 2️⃣6️⃣ Optimistic vs Pessimistic

||Optimistic|Pessimistic|
|---|---|---|
|Lock early|❌|✅|
|Version check|সাধারণত ✅|সাধারণত না|
|Conflict handling|পরে detect|আগে prevent/block|
|High contention|সবসময় ideal নয়|useful হতে পারে|
|Low contention|Often good|May be unnecessary|
|Example|version column|`FOR UPDATE`|

---

# 2️⃣7️⃣ Deadlock

ধরো:

### T1

```text
Lock A
 ↓
Waiting for B
```

### T2

```text
Lock B
 ↓
Waiting for A
```

```text
T1 → B-এর জন্য অপেক্ষা
T2 → A-এর জন্য অপেক্ষা
```

কেউ এগোতে পারছে না।

এটাই:

> **Deadlock**

---

# 2️⃣8️⃣ Deadlock Prevention

### Rule 1 — Consistent Lock Order

সব transaction:

```text
A → B
```

এই order-এ lock করবে।

কেউ:

```text
B → A
```

করবে না।

---

### Rule 2 — Short Transactions

❌

```text
BEGIN
 ↓
5 minutes processing
 ↓
COMMIT
```

Better:

```text
BEGIN
 ↓
minimum DB work
 ↓
COMMIT
```

---

### Rule 3 — Proper Indexes

Poor index-এর কারণে বেশি rows lock/search করতে হতে পারে।

---

### Rule 4 — Retry

Application layer-এ deadlock হলে transaction retry strategy রাখা যেতে পারে।

---

# 2️⃣9️⃣ Django-তে Transaction

Django:

```python
from django.db import transaction

with transaction.atomic():
    # create booking
    # create payment
    # other related updates
    pass
```

Block-এর ভিতরের database operations একটি atomic unit হিসেবে কাজ করে।

Exception হলে transaction rollback হতে পারে।

---

# 3️⃣0️⃣ Django + `select_for_update()`

Hotel example:

```python
from django.db import transaction

with transaction.atomic():

    room = (
        Room.objects
        .select_for_update()
        .get(id=101)
    )

    # check booking overlap

    # create booking
```

এটা database-level row locking-এর Django abstraction।

---

# 3️⃣1️⃣ Isolation Level কখন Change করব?

Default isolation level blindly change করবে না।

প্রথমে বুঝবে:

```text
Business requirement
        ↓
Consistency requirement
        ↓
Concurrency requirement
        ↓
Performance
        ↓
Isolation choice
```

Example:

```text
Simple reporting
→ lower isolation may be sufficient

Financial transaction
→ stronger consistency may be needed

Hotel booking
→ proper locking + transaction design important
```

এখানে exact choice workload এবং DBMS-এর behavior-এর উপর নির্ভর করবে।

---

# 3️⃣2️⃣ Isolation Level Set করা

MySQL example:

```sql
SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

তারপর transaction:

```sql
START TRANSACTION;

...

COMMIT;
```

Current setting:

```sql
SELECT @@transaction_isolation;
```

---

# 3️⃣3️⃣ Important — Isolation ≠ Locking

এটা interview-এ খুব useful।

```text
Isolation Level
      +
Locks
      +
MVCC
      +
Transaction Design
```

সব মিলে concurrency behavior তৈরি হয়।

শুধু isolation level জানলেই পুরো concurrency বুঝে ফেলা যায় না।

---

# 3️⃣4️⃣ Hotel Booking — Production Flow ⭐⭐⭐

একটা ভালো transaction flow:

```text
User requests Room 101
        ↓
START TRANSACTION
        ↓
Lock relevant room/resource
        ↓
Check room status
        ↓
Check overlapping bookings
        ↓
Available?
   ↙          ↘
 YES           NO
 ↓              ↓
Create         ROLLBACK
Booking
 ↓
Create Payment
 ↓
COMMIT
```

যদি মাঝখানে error:

```text
ROLLBACK
```

---

# 3️⃣5️⃣ সবচেয়ে Common Mistake

এইটা:

```python
if room_available():
    create_booking()
```

যদি `room_available()` এবং `create_booking()` আলাদা transaction/context-এ হয়, তাহলে দুই concurrent request একই সময়ে available দেখে booking করতে পারে।

এটাই race condition।

Better:

```text
availability check
       +
booking creation
       ↓
same transaction
       +
proper locking/concurrency control
```

---

# 3️⃣6️⃣ Isolation Level Selection — Simple Mental Model

```text
READ UNCOMMITTED
       ↓
Fast / weak consistency

READ COMMITTED
       ↓
No dirty reads

REPEATABLE READ
       ↓
Stable consistent reads

SERIALIZABLE
       ↓
Strongest standard isolation
```

কিন্তু:

```text
Stronger isolation
       ↓
Potentially more contention
       ↓
Potentially lower concurrency
```

---

# 3️⃣7️⃣ Database Designer-এর Real Mindset

Beginner:

> "আমার query correct."

Database designer:

> "Concurrent users থাকলে correct থাকবে?"

Production engineer:

> "Concurrent users + failure + retry + deadlock + high load—সব অবস্থায় কী হবে?"

এই level-এর চিন্তা develop করাই Class 62-এর মূল লক্ষ্য।

---

# 🧠 Class 62 Golden Rules ⭐⭐⭐

```text
1. Transaction → Logical unit of work

2. Isolation → Concurrent transactions-এর interaction control

3. Dirty Read → Uncommitted data read

4. Non-Repeatable Read → Same row, different value

5. Phantom Read → New matching rows appear

6. Lost Update → One update overwrites another

7. READ UNCOMMITTED → Weakest

8. READ COMMITTED → No dirty reads

9. REPEATABLE READ → Stable consistent reads

10. SERIALIZABLE → Strongest standard isolation

11. MVCC → Multiple row versions help concurrency

12. FOR UPDATE → Lock rows for transactional update

13. Optimistic → Version/conflict check

14. Pessimistic → Lock early

15. Deadlock → Transactions waiting on each other

16. Short transactions → Better concurrency

17. Consistent lock order → Helps prevent deadlocks

18. Atomic UPDATE → Useful for inventory

19. Django atomic() → Transaction boundary

20. Isolation level alone ≠ complete concurrency solution
```

---

# 📝 Class 62 Assignment

### Task 1 — Concepts

নিজের ভাষায় explain করো:

```text
Dirty Read
Non-Repeatable Read
Phantom Read
Lost Update
```

---

### Task 2 — Isolation

এই table পূরণ করো:

|Isolation|Dirty Read|Non-Repeatable Read|Phantom|
|---|---|---|---|
|READ UNCOMMITTED|?|?|?|
|READ COMMITTED|?|?|?|
|REPEATABLE READ|?|?|?|
|SERIALIZABLE|?|?|?|

---

### Task 3 — Inventory ⭐

Current stock:

```text
stock = 10
```

User A:

```text
buy 7
```

User B:

```text
buy 5
```

একটি **atomic UPDATE query** লেখো যাতে stock negative না হয়।

---

### Task 4 — Hotel Booking ⭐⭐⭐

দুই user একই সময়ে:

```text
Room 101
2026-09-20 → 2026-09-25
```

book করতে চায়।

একটি transaction flow লেখো:

```text
BEGIN
↓
?
↓
?
↓
?
↓
COMMIT / ROLLBACK
```

---

### Task 5 — Optimistic Concurrency

Current:

```text
stock = 10
version = 5
```

একজন user 3 units কিনছে।

`version` ব্যবহার করে UPDATE query লেখো।

---

### 🔥 Task 6 — Interview Challenge

Interviewer:

> **"Two users try to book the same hotel room at exactly the same time. How would you prevent double booking?"**

তোমার answer-এ ideally থাকবে:

```text
Transaction
+
Lock / appropriate concurrency control
+
Availability check
+
Overlap detection
+
Create booking
+
COMMIT
+
ROLLBACK on failure
```

---

## 🎯 Class 62-এর সবচেয়ে গুরুত্বপূর্ণ ৫টি জিনিস

যদি আজ সবকিছু মনে না থাকে, অন্তত এগুলো solid করো:

```text
1. Isolation Level
2. Dirty / Non-repeatable / Phantom
3. Lost Update
4. SELECT ... FOR UPDATE
5. Optimistic vs Pessimistic Concurrency
```

**পরবর্তী: Class 63 — Locking, Deadlock & Concurrency — Advanced**। সেখানে আমরা **Shared Lock, Exclusive Lock, Row Lock, Gap Lock, Next-Key Lock, Deadlock Analysis, Lock Order এবং real concurrent transaction scenarios** আরও গভীরভাবে করব।

----
# 📚 Class 63 — Locking, Deadlock & Concurrency — Advanced

আজকের class হলো **Database Concurrency-এর advanced level**।

Class 62-এ আমরা Isolation Level, Dirty Read, Lost Update, `FOR UPDATE`, Optimistic/Pessimistic Concurrency শিখেছি।

আজ আমরা আরও গভীরে যাব:

1. Lock কী?
    
2. Shared Lock
    
3. Exclusive Lock
    
4. Row Lock
    
5. Table Lock
    
6. Gap Lock
    
7. Next-Key Lock
    
8. Record Lock
    
9. Lock Compatibility
    
10. Deadlock কীভাবে তৈরি হয়
    
11. Deadlock analysis
    
12. Lock order
    
13. Real concurrent transaction
    
14. Hotel booking
    
15. Inventory
    
16. Bank transfer
    
17. Django concurrency
    
18. Production best practices
    

---

# 1️⃣ Lock কী?

সহজভাবে:

> **Lock হলো database-এর mechanism যা concurrent transactions-এর conflicting access control করে।**

ধরো:

```text
Account A
balance = 10000
```

দুই transaction একই সময়ে balance update করতে চায়:

```text
T1 ─────→ Account A
T2 ─────→ Account A
```

Database-কে decide করতে হবে:

```text
কে আগে access করবে?
কে wait করবে?
কখন দ্বিতীয় transaction access পাবে?
```

এখানে lock সাহায্য করে।

---

# 2️⃣ Lock-এর প্রধান দুই ধরনের ধারণা

আজকের সবচেয়ে important:

```text
Shared Lock (S)
       ↓
Read

Exclusive Lock (X)
       ↓
Write
```

---

# 3️⃣ Shared Lock — S Lock

Shared lock সাধারণত **read-এর জন্য** ব্যবহৃত হয়।

Concept:

```text
T1 → S Lock → Row A
```

আরেক transaction-ও compatible shared lock পেতে পারে:

```text
T1 → S Lock
T2 → S Lock
```

দুজনেই read করতে পারে।

কিন্তু অন্য transaction যদি conflicting exclusive lock চায়:

```text
T1 → S
T2 → X
```

T2-কে wait করতে হতে পারে।

---

# 4️⃣ Exclusive Lock — X Lock

Exclusive lock সাধারণত update/delete-এর মতো write operation-এর জন্য ব্যবহৃত হয়।

```text
T1 → X Lock → Row A
```

এখন অন্য transaction একই row-তে conflicting access চাইলে অপেক্ষা করতে হতে পারে।

Concept:

```text
X Lock
  ↓
Other conflicting lock
  ↓
WAIT
```

---

# 5️⃣ Shared vs Exclusive

||Shared (S)|Exclusive (X)|
|---|---|---|
|Read|✅|সম্ভব/implementation-specific context|
|Write|❌|✅|
|Multiple transactions|Shared locks compatible হতে পারে|Generally exclusive|
|Main purpose|Read protection|Write protection|

Simplified compatibility:

|Existing|New S|New X|
|---|--:|--:|
|S|✅|❌|
|X|❌|❌|

এটা conceptual compatibility table; exact locking behavior DBMS ও isolation-এর উপর নির্ভর করে।

---

# 6️⃣ Row Lock ⭐

Row lock মানে পুরো table lock না করে নির্দিষ্ট row-এর উপর lock।

ধরো:

```text
customers

id | name
---------
1  | Rahim
2  | Karim
3  | Sadia
4  | Nadia
```

T1:

```sql
SELECT *
FROM customers
WHERE id = 2
FOR UPDATE;
```

Relevant row:

```text
Karim
```

transaction-এর context-এ update-oriented row lock নেওয়া হতে পারে।

অন্য transaction:

```text
UPDATE customers
SET name = 'Karim Ahmed'
WHERE id = 2;
```

প্রয়োজনে wait করতে পারে যতক্ষণ না প্রথম transaction lock release করে।

---

# 7️⃣ Row Lock কেন ভালো?

ধরো 1 million rows-এর table।

যদি একজন user শুধু:

```text
Row 500
```

update করে, তাহলে ideally অন্য user যেন:

```text
Row 700
```

update করতে পারে।

Row-level locking এই ধরনের concurrency support করে।

```text
T1 → Row 500 🔒
T2 → Row 700 🔒

Both can potentially proceed
```

---

# 8️⃣ Table Lock

Table-level lock:

```text
Entire Table
     🔒
```

তখন অন্য transaction-এর access বেশি restricted হতে পারে।

Large concurrent applications-এ unnecessary broad locks problematic হতে পারে।

### তাই:

```text
Row lock
   ↓
Usually finer-grained

Table lock
   ↓
Broader
```

তবে কোন lock ব্যবহার হবে তা DBMS এবং statement-এর উপর নির্ভর করে।

---

# 9️⃣ `SELECT ... FOR UPDATE` আবার দেখি ⭐⭐⭐

```sql
START TRANSACTION;

SELECT *
FROM products
WHERE product_id = 10
FOR UPDATE;

-- update stock

COMMIT;
```

এখানে উদ্দেশ্য:

```text
Read row
   ↓
Lock for transactional update
   ↓
Perform logic
   ↓
COMMIT
```

---

# 🔟 Important: Lock কতক্ষণ থাকে?

সাধারণ transactional row lock transaction শেষ হওয়া পর্যন্ত থাকতে পারে:

```text
BEGIN
 ↓
Lock
 ↓
Queries
 ↓
COMMIT / ROLLBACK
 ↓
Lock release
```

তাই:

> **Long transaction = Long lock duration = More contention**

---

# 1️⃣1️⃣ Lock Contention

ধরো:

```text
T1 → Row 100 🔒
```

T2:

```text
T2 → Row 100
      ↓
    WAIT
```

এটাকে বলা যায়:

> **Lock contention**

অর্থাৎ multiple transactions একই resource-এর জন্য compete করছে।

---

# 1️⃣2️⃣ Lock Wait

Concept:

```text
T1
 ↓
Lock Row A
 ↓
Processing...
 ↓
COMMIT

T2
 ↓
Needs Row A
 ↓
WAIT ⏳
 ↓
T1 commits
 ↓
T2 continues
```

যদি T1 unnecessarily অনেক সময় ধরে transaction open রাখে, T2-এর wait time বাড়তে পারে।

---

# 1️⃣3️⃣ Gap Lock ⭐⭐⭐

এটা MySQL InnoDB-এর advanced locking concept।

ধরো indexed values:

```text
10
20
30
40
```

এখানে values-এর মাঝেও gaps আছে:

```text
(-∞,10)
(10,20)
(20,30)
(30,40)
(40,+∞)
```

**Gap lock** কোনো existing row-কে নয়, index-এর **gap/range between records**-কে lock করতে পারে।

এর উদ্দেশ্যের একটি গুরুত্বপূর্ণ অংশ হলো concurrent inserts-এর behavior control করা।

---

# 1️⃣4️⃣ Gap Lock কেন দরকার?

ধরো T1 একটি range scan করছে:

```sql
SELECT *
FROM orders
WHERE order_id BETWEEN 10 AND 20
FOR UPDATE;
```

তারপর অন্য transaction যদি একই locked range-এর মধ্যে নতুন row insert করতে চায়, InnoDB-এর isolation/locking behavior অনুযায়ী তাকে block করা হতে পারে।

এখানে:

```text
10 ─────── 20
   🔒 GAP
```

Gap lock concept relevant।

---

# 1️⃣5️⃣ Record Lock vs Gap Lock

### Record Lock

Existing index record-এর উপর lock।

```text
10
🔒
```

### Gap Lock

দুই record-এর মাঝের gap-এর উপর lock।

```text
10      20
  🔒🔒🔒
```

---

# 1️⃣6️⃣ Next-Key Lock ⭐⭐⭐

এটা একটু advanced।

**Next-key lock = Record Lock + Gap Lock**

Concept:

```text
Gap + Record
```

অর্থাৎ:

```text
(previous value, current record]
```

ধরো:

```text
10
20
30
```

20-এর next-key locking conceptually:

```text
(10, 20]
```

অর্থাৎ:

```text
Gap between 10 and 20
        +
Record 20
```

---

# 1️⃣7️⃣ Gap Lock vs Next-Key Lock

||Gap Lock|Next-Key Lock|
|---|---|---|
|Existing record lock|❌|✅|
|Gap lock|✅|✅|
|Main idea|Gap protect|Gap + record protect|
|MySQL InnoDB|Important concept|Important concept|

---

# 1️⃣8️⃣ কেন এইগুলো জানা দরকার?

Database designer হিসেবে তোমাকে প্রতিদিন:

```text
Gap Lock
Next-Key Lock
```

ব্যবহার করতে হবে না।

কিন্তু production debugging-এ যদি:

```text
"Why is my INSERT waiting?"
```

এই ধরনের problem আসে, তখন এই concepts helpful।

---

# 1️⃣9️⃣ Deadlock ⭐⭐⭐

এখন সবচেয়ে important অংশ।

Deadlock:

> **দুই বা তার বেশি transaction একে অন্যের locked resource-এর জন্য অপেক্ষা করছে।**

Classic example:

```text
T1 locks A
T2 locks B

T1 wants B
T2 wants A
```

Diagram:

```text
T1 ──locks──→ A
 ↑             ↓
 │           wants
 │             ↓
 B ←──locks── T2
```

দুজনেই wait করছে।

---

# 2️⃣0️⃣ Deadlock Example

ধরো:

```text
Account 1
Account 2
```

### T1

```sql
START TRANSACTION;

SELECT *
FROM accounts
WHERE account_id = 1
FOR UPDATE;
```

T1:

```text
Account 1 🔒
```

তারপর T1:

```sql
SELECT *
FROM accounts
WHERE account_id = 2
FOR UPDATE;
```

---

### একই সময়ে T2

```sql
START TRANSACTION;

SELECT *
FROM accounts
WHERE account_id = 2
FOR UPDATE;
```

T2:

```text
Account 2 🔒
```

তারপর:

```sql
SELECT *
FROM accounts
WHERE account_id = 1
FOR UPDATE;
```

এখন:

```text
T1 owns Account 1
T2 owns Account 2

T1 wants Account 2
T2 wants Account 1
```

💥 **Deadlock**

---

# 2️⃣1️⃣ Deadlock Graph

এভাবে মনে রাখো:

```text
T1
 │
 │ holds
 ↓
 A
 │
 │ wants
 ↓
 B
 ↑
 │ holds
 │
T2
 │
 │ wants
 ↓
 A
```

অর্থাৎ:

```text
T1 → T2 → T1
```

একটা cycle তৈরি হয়েছে।

---

# 2️⃣2️⃣ Database কী করে?

Modern DBMS সাধারণত deadlock detect করতে পারে।

তারপর একটি transaction victim হিসেবে rollback করে:

```text
T1 ───┐
      ├── Deadlock
T2 ───┘
       ↓
DB detects
       ↓
One transaction rollback
       ↓
Other continues
```

অর্থাৎ:

> Deadlock হলে database necessarily permanently stuck হয়ে থাকবে না।

---

# 2️⃣3️⃣ Deadlock কেন সবসময় Application Bug নয়?

Concurrent system-এ deadlock ঘটতে পারে।

Important হলো:

```text
Prevent where possible
+
Detect
+
Retry safely
```

---

# 2️⃣4️⃣ Deadlock Prevention — Lock Order ⭐⭐⭐

সবচেয়ে practical technique:

> **সব transaction একই order-এ resource lock করবে।**

ধরো:

```text
Account 1
Account 2
```

সব transaction:

```text
1 → 2
```

এই order-এ lock করবে।

তাহলে:

```text
T1 → 1 → 2
T2 → 1 → 2
```

T2 হয়তো 1-এর জন্য wait করবে।

কিন্তু:

```text
T2 → 2 → 1
```

এর মতো reverse order না হলে cycle তৈরির chance কমে।

---

# 2️⃣5️⃣ Lock Order Golden Rule ⭐

```text
Multiple resources
       ↓
Always lock
       ↓
Same deterministic order
```

Example:

```text
Customer ID ascending
Product ID ascending
Account ID ascending
```

যে domain-এর resource হোক, consistent order গুরুত্বপূর্ণ।

---

# 2️⃣6️⃣ Bank Transfer — Correct Design

ধরো:

```text
Account A → Account B
```

Transaction:

```text
BEGIN
 ↓
Lock smaller account ID first
 ↓
Lock larger account ID
 ↓
Check balance
 ↓
Debit
 ↓
Credit
 ↓
COMMIT
```

যদি transfer reverse direction হয়, তবুও:

```text
smaller ID → larger ID
```

order maintain করবে।

এতে deadlock risk কমে।

---

# 2️⃣7️⃣ Hotel Booking — Advanced Concurrency ⭐⭐⭐

আমাদের hotel system:

```text
Room 101
```

দুই user:

```text
A → Sept 20–25
B → Sept 20–25
```

Transaction:

```text
BEGIN
 ↓
Lock relevant room/resource
 ↓
Check existing bookings
 ↓
Check overlap
 ↓
Available?
 ↓
Create booking
 ↓
COMMIT
```

---

# 2️⃣8️⃣ Overlap Condition

Existing booking:

```text
check_in  = Sept 20
check_out = Sept 25
```

New booking:

```text
check_in  = Sept 22
check_out = Sept 24
```

Overlap:

```text
new_check_in < existing_check_out
AND
new_check_out > existing_check_in
```

SQL:

```sql
SELECT 1
FROM bookings
WHERE room_id = 101
AND status IN ('PENDING', 'CONFIRMED')
AND check_in < '2026-09-25'
AND check_out > '2026-09-20'
FOR UPDATE;
```

তবে এখানে একটা subtle point আছে:

> Exact locking behavior নির্ভর করবে index, isolation level, query plan এবং DBMS-এর implementation-এর উপর।

শুধু query দেখে locking behavior assume করা উচিত নয়।

---

# 2️⃣9️⃣ Inventory — Concurrent Purchase

Stock:

```text
100
```

User A:

```text
buy 60
```

User B:

```text
buy 50
```

Naive:

```text
A reads 100
B reads 100
```

দুজনই ধরে নেয় stock available।

Problem:

```text
100 - 60 - 50
= -10
```

---

# 3️⃣0️⃣ Better — Atomic UPDATE

```sql
UPDATE products
SET stock = stock - 60
WHERE product_id = 10
AND stock >= 60;
```

তারপর:

```text
affected_rows = 1
```

হলে success।

B:

```sql
UPDATE products
SET stock = stock - 50
WHERE product_id = 10
AND stock >= 50;
```

যদি insufficient stock হয়:

```text
affected_rows = 0
```

---

# 3️⃣1️⃣ কেন এটা ভালো?

কারণ condition + update একই database operation-এর মধ্যে:

```text
stock >= quantity
       +
stock = stock - quantity
```

এতে application-level read-modify-write race কমানো যায়।

---

# 3️⃣2️⃣ Locking + Indexing ⭐

এখানে Class 59–60-এর knowledge দরকার।

ধরো:

```sql
SELECT *
FROM bookings
WHERE room_id = 101
AND check_in < '2026-09-25'
AND check_out > '2026-09-20'
FOR UPDATE;
```

Appropriate indexes না থাকলে database-কে বেশি rows inspect করতে হতে পারে।

ফলে:

```text
Poor index
 ↓
More rows examined
 ↓
More locking work/contention
 ↓
Slower transaction
 ↓
Higher deadlock/wait risk
```

তাই:

> **Index শুধু query speed-এর জন্য নয়; concurrency behavior-এর উপরও প্রভাব ফেলতে পারে।**

---

# 3️⃣3️⃣ Long Transaction কেন Dangerous?

❌

```text
BEGIN
 ↓
Lock
 ↓
API call
 ↓
External processing
 ↓
User input
 ↓
More processing
 ↓
COMMIT
```

এটা avoid করা উচিত।

কারণ lock অনেকক্ষণ ধরে থাকতে পারে।

Better:

```text
Prepare data
 ↓
BEGIN
 ↓
Lock
 ↓
DB operations
 ↓
COMMIT
```

### Golden Rule

> **Transaction যত short করা যায় তত ভালো।**

---

# 3️⃣4️⃣ Application-এর ভিতরে External API Call

ধরো:

```python
with transaction.atomic():
    # lock room

    call_payment_gateway()

    # create booking
```

এটা risky হতে পারে যদি payment API 5 seconds নেয়।

কারণ:

```text
DB Lock
   ↓
Payment API waits 5 sec
   ↓
Lock held 5 sec
```

এতে অন্য requests block হতে পারে।

Production design-এ payment workflow সাধারণত carefully designed হয় যাতে unnecessary DB lock external network call-এর জন্য ধরে রাখা না হয়।

---

# 3️⃣5️⃣ Django + Row Lock

```python
from django.db import transaction

with transaction.atomic():

    room = (
        Room.objects
        .select_for_update()
        .get(id=101)
    )

    # check booking conflicts

    Booking.objects.create(
        room=room,
        ...
    )
```

Concept:

```text
atomic()
   +
select_for_update()
   +
validation
   +
write
```

---

# 3️⃣6️⃣ Django + Optimistic Locking

ধরো model:

```text
product_id
stock
version
```

Update:

```python
updated = Product.objects.filter(
    id=10,
    version=5
).update(
    stock=7,
    version=6
)
```

যদি:

```text
updated == 1
```

Success।

যদি:

```text
updated == 0
```

Conflict হয়েছে।

---

# 3️⃣7️⃣ Pessimistic vs Optimistic — আবার

### Pessimistic

```text
Lock first
   ↓
Then work
```

Example:

```python
.select_for_update()
```

### Optimistic

```text
Work assuming no conflict
        ↓
Check version
        ↓
Conflict?
```

---

# 3️⃣8️⃣ Deadlock Debugging Mindset

Production-এ deadlock error এলে:

### Step 1

কোন দুই transaction involved?

### Step 2

কোন resource lock করেছে?

### Step 3

কোন resource চাইছে?

### Step 4

Lock order কী?

### Step 5

দুই transaction কি opposite order-এ lock করছে?

### Step 6

Transaction কি unnecessarily long?

### Step 7

Index কি appropriate?

---

# 3️⃣9️⃣ Deadlock Analysis Example

ধরো logs:

```text
Transaction A:
Lock Product 10
Waiting for Product 20

Transaction B:
Lock Product 20
Waiting for Product 10
```

Diagram:

```text
A ──holds──→ 10
A ──wants──→ 20

B ──holds──→ 20
B ──wants──→ 10
```

Cycle:

```text
A → B → A
```

### Solution

সব transaction:

```text
Lock 10
then
Lock 20
```

---

# 4️⃣0️⃣ Deadlock বনাম Lock Wait

এ দুটো এক না।

### Lock Wait

```text
T1 → holds A
T2 → waits A
```

T1 commit করলে:

```text
T2 continues
```

### Deadlock

```text
T1 → waits B
T2 → waits A
```

এবং:

```text
T1 → T2 → T1
```

cycle।

---

# 4️⃣1️⃣ Lock Wait বনাম Deadlock

||Lock Wait|Deadlock|
|---|---|---|
|Waiting|✅|✅|
|Cycle|❌|✅|
|Eventually resolve|Usually yes|Requires intervention by DB|
|DB rollback victim|Not necessarily|Typically one transaction|
|Main solution|Short transactions|Lock ordering + design|

---

# 4️⃣2️⃣ Production Best Practices ⭐⭐⭐

### 1. Transaction short রাখো

```text
BEGIN
 ↓
minimum DB work
 ↓
COMMIT
```

### 2. Consistent lock order

```text
Always:
A → B
```

### 3. Proper indexes

যাতে unnecessary rows scan/lock না হয়।

### 4. Atomic operations

Inventory-এর মতো ক্ষেত্রে:

```sql
UPDATE ... WHERE stock >= quantity
```

### 5. Deadlock retry

Application layer-এ safe retry strategy রাখো।

### 6. External API transaction-এর ভিতরে unnecessarily call করো না

### 7. Lock everything করো না

যেখানে প্রয়োজন সেখানে lock।

---

# 4️⃣3️⃣ Complete Concurrency Architecture

একজন Database Designer হিসেবে চিন্তা করবে:

```text
User Request
     ↓
Django API
     ↓
Transaction
     ↓
Appropriate Lock
     ↓
Read / Validate
     ↓
Business Logic
     ↓
Write
     ↓
COMMIT
```

যদি conflict:

```text
Conflict
   ↓
Wait / Retry / Rollback
```

যদি deadlock:

```text
Deadlock
   ↓
DB detects
   ↓
One transaction rollback
   ↓
Application may retry
```

---

# 🧠 Class 63 Golden Rules ⭐⭐⭐

```text
1. Lock → Concurrent access control

2. Shared Lock → Read-oriented lock

3. Exclusive Lock → Write-oriented lock

4. Row Lock → Specific row/resource

5. Table Lock → Broad table-level lock

6. Lock Contention → Multiple transactions compete for same resource

7. Gap Lock → Index gap protection

8. Record Lock → Existing index record protection

9. Next-Key Lock → Record Lock + Gap Lock

10. Deadlock → Transactions waiting for each other

11. Lock Wait ≠ Deadlock

12. Consistent Lock Order → Deadlock risk কমায়

13. Short Transaction → Better concurrency

14. Proper Index → Less unnecessary scanning/locking

15. Atomic UPDATE → Race condition কমাতে useful

16. FOR UPDATE → Transactional update locking

17. Optimistic → Version check

18. Pessimistic → Lock first

19. Deadlock → Application retry strategy useful হতে পারে

20. Transaction-এর ভিতরে unnecessary external API call avoid

21. Lock only what you need

22. Database concurrency = Transaction + Isolation + Locking + Good Design
```

---

# 📝 Class 63 Assignment

## Task 1 — Lock

Explain করো:

```text
Shared Lock
Exclusive Lock
Row Lock
Table Lock
```

---

## Task 2 — Lock Compatibility

এই table পূরণ করো:

|Existing|New Shared|New Exclusive|
|---|--:|--:|
|Shared|?|?|
|Exclusive|?|?|

---

## Task 3 — Deadlock ⭐

এই situation explain করো:

```text
T1 → locks Account 1
T2 → locks Account 2

T1 → wants Account 2
T2 → wants Account 1
```

**কেন deadlock হবে?**

---

## Task 4 — Deadlock Prevention

উপরের problem কীভাবে **consistent lock order** দিয়ে solve করবে?

---

## Task 5 — Inventory ⭐

Stock:

```text
stock = 10
```

User A:

```text
buy = 7
```

User B:

```text
buy = 5
```

একটি atomic SQL UPDATE লেখো যাতে stock negative না হয়।

---

## Task 6 — Hotel Booking ⭐⭐⭐

দুই user একই room একই date-এ book করছে।

একটি complete flow লেখো:

```text
BEGIN
↓
?
↓
?
↓
?
↓
?
↓
COMMIT / ROLLBACK
```

---

# 🔥 Interview Challenge

Interviewer জিজ্ঞেস করল:

> **"Your application is experiencing frequent database deadlocks. How would you diagnose and reduce them?"**

তোমার answer-এর structure:

```text
1. Identify conflicting transactions
        ↓
2. Check lock order
        ↓
3. Find opposite lock ordering
        ↓
4. Make lock order consistent
        ↓
5. Shorten transactions
        ↓
6. Review indexes
        ↓
7. Avoid unnecessary locks
        ↓
8. Add safe retry strategy
        ↓
9. Monitor and test again
```

---

## 🎯 Class 63-এর সবচেয়ে গুরুত্বপূর্ণ 6টি বিষয়

```text
Shared Lock
Exclusive Lock
Row Lock
Gap/Next-Key Lock
Deadlock
Consistent Lock Order
```

এই 6টা ভালোভাবে বুঝলে তুমি **basic SQL → advanced SQL → database engineering** transition-এর একটা গুরুত্বপূর্ণ অংশ পার করে ফেলেছ।

**Next: Class 64 — Database Partitioning**। সেখানে আমরা শিখব **Partition কী, Range/List/Hash Partition, Partition Pruning, বড় table কীভাবে ভাগ করা হয়, কখন partition ব্যবহার করা উচিত/উচিত নয়, এবং orders/logs/booking table-এ practical design**।


---
# 📚 Class 64 — Database Partitioning

আজকের topic **Database Engineering-এর খুব গুরুত্বপূর্ণ একটি বিষয়**।

এখন পর্যন্ত আমরা শিখেছি:

```text
SQL
→ JOIN
→ Subquery
→ CTE
→ Window Function
→ View
→ Transaction
→ Locking
→ Index
→ EXPLAIN
→ Query Optimization
```

এখন প্রশ্ন:

> **একটা table যদি 10 কোটি বা 50 কোটি row হয়ে যায়, তখন কীভাবে manage করব?**

এখানেই আসে **Database Partitioning**।

---

# 1️⃣ Partition কী?

সহজ ভাষায়:

> **একটি বড় table-কে logicalভাবে কয়েকটি ছোট অংশে ভাগ করাকে Partitioning বলে।**

ধরো:

```text
orders
100 million rows
```

একটা বিশাল table:

```text
orders
────────────────────
100,000,000 rows
```

আমরা এটাকে বছর অনুযায়ী ভাগ করলাম:

```text
orders
│
├── orders_2024
├── orders_2025
├── orders_2026
└── orders_2027
```

Logicalভাবে application-এর কাছে এটি এখনও:

```text
orders
```

কিন্তু database ভিতরে data partition অনুযায়ী রাখে।

---

# 2️⃣ Partition ≠ Multiple Tables ⭐

এটা খুব গুরুত্বপূর্ণ।

অনেকে মনে করে:

```text
orders_2024
orders_2025
orders_2026
```

তাহলে এগুলো manually আলাদা table।

Partitioning-এ সাধারণত:

```text
Parent Table
     ↓
Partitions
```

Database partitioning mechanism এগুলোকে একটি partitioned table-এর অংশ হিসেবে manage করে।

---

# 3️⃣ Partition কেন ব্যবহার করব?

ধরো:

```text
orders = 500 million rows
```

Query:

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01';
```

যদি table partitioned হয়:

```text
orders
│
├── 2024
├── 2025
├── 2026  ← relevant
└── 2027
```

Database অনেক ক্ষেত্রে শুধু relevant partition scan করতে পারে।

এটাকে বলা হয়:

# ⭐ Partition Pruning

---

# 4️⃣ Partition Pruning ⭐⭐⭐

Partition pruning হলো:

> Query-এর condition দেখে database unnecessary partitions বাদ দিয়ে শুধু relevant partitionগুলো access করা।

ধরো:

```text
P1 → 2024
P2 → 2025
P3 → 2026
P4 → 2027
```

Query:

```sql
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01'
```

তাহলে:

```text
P1 ❌
P2 ❌
P3 ✅
P4 ❌
```

এটাই partition pruning।

---

# 5️⃣ Partitioning-এর প্রধান ধরন

আজ আমরা 3টি প্রধান type শিখব:

```text
1. RANGE
2. LIST
3. HASH
```

আর কিছু DBMS-এ আরও partitioning strategy আছে।

---

# 6️⃣ RANGE Partitioning ⭐⭐⭐

সবচেয়ে common practical use case:

> **Date / time অনুযায়ী data ভাগ করা।**

যেমন:

```text
2024
2025
2026
2027
```

---

## Example

ধরো:

```text
orders
```

আমরা order date অনুযায়ী partition করব।

Conceptually:

```text
2024 → Partition 1
2025 → Partition 2
2026 → Partition 3
2027 → Partition 4
```

MySQL example:

```sql
CREATE TABLE orders (
    order_id BIGINT NOT NULL,
    customer_id BIGINT NOT NULL,
    order_date DATE NOT NULL,
    amount DECIMAL(12,2)
)
PARTITION BY RANGE (YEAR(order_date)) (
    PARTITION p2024 VALUES LESS THAN (2025),
    PARTITION p2025 VALUES LESS THAN (2026),
    PARTITION p2026 VALUES LESS THAN (2027),
    PARTITION p2027 VALUES LESS THAN (2028),
    PARTITION pmax VALUES LESS THAN MAXVALUE
);
```

এখানে:

```text
YEAR(order_date)
```

দেখে partition select হবে।

---

# 7️⃣ `VALUES LESS THAN` বুঝি

এই অংশ:

```sql
PARTITION p2025 VALUES LESS THAN (2026)
```

মানে:

```text
2025 সালের data
```

কারণ 2026-এর আগের year।

Example:

```text
2025-01-01 → p2025
2025-07-15 → p2025
2025-12-31 → p2025
```

---

# 8️⃣ RANGE Partition Visualization

```text
orders
│
├── p2024
│    └── 2024 data
│
├── p2025
│    └── 2025 data
│
├── p2026
│    └── 2026 data
│
└── p2027
     └── 2027 data
```

Query:

```sql
SELECT *
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2027-01-01';
```

Potentially:

```text
Partition Pruning
       ↓
p2026 only
```

---

# 9️⃣ Monthly RANGE Partition

বড় logs/orders table হলে yearly partition যথেষ্ট নাও হতে পারে।

তখন:

```text
2026-01
2026-02
2026-03
2026-04
...
```

Concept:

```text
p2026_01
p2026_02
p2026_03
...
```

এতে পুরনো data archive/drop করাও সহজ হতে পারে।

---

# 🔟 LIST Partitioning

LIST partitioning ব্যবহার করি যখন নির্দিষ্ট category/value অনুযায়ী data ভাগ করতে চাই।

ধরো:

```text
country
```

বা:

```text
region
```

Example:

```text
Dhaka
Chittagong
Rajshahi
Sylhet
```

Conceptually:

```sql
PARTITION BY LIST (region)
```

তারপর:

```text
p_dhaka
p_chittagong
p_other
```

---

# 1️⃣1️⃣ LIST Example

MySQL-style example:

```sql
CREATE TABLE customers (
    customer_id BIGINT NOT NULL,
    name VARCHAR(100),
    region INT NOT NULL
)
PARTITION BY LIST (region) (
    PARTITION p_dhaka VALUES IN (1),
    PARTITION p_chittagong VALUES IN (2),
    PARTITION p_rajshahi VALUES IN (3),
    PARTITION p_sylhet VALUES IN (4)
);
```

ধরো:

```text
region = 1
```

তাহলে:

```text
p_dhaka
```

---

# 1️⃣2️⃣ LIST Partition কখন useful?

যখন values discrete এবং business meaning আছে।

যেমন:

```text
Region
Country
Business Unit
Tenant Group
Status category
```

কিন্তু একটা গুরুত্বপূর্ণ বিষয়:

> High-cardinality column দিয়ে LIST partition করা সবসময় ভালো design নয়।

যেমন:

```text
customer_id
```

এর millions of unique values থাকলে millions partition বানানো absurd।

---

# 1️⃣3️⃣ HASH Partitioning ⭐⭐⭐

Hash partitioning-এ database একটি hash function ব্যবহার করে row-কে partition-এ distribute করে।

Concept:

```text
customer_id
     ↓
   HASH
     ↓
Partition
```

ধরো:

```text
4 partitions
```

তাহলে data roughly distribute হতে পারে:

```text
P0
P1
P2
P3
```

---

# 1️⃣4️⃣ HASH Example

```sql
CREATE TABLE orders (
    order_id BIGINT NOT NULL,
    customer_id BIGINT NOT NULL,
    amount DECIMAL(12,2)
)
PARTITION BY HASH(customer_id)
PARTITIONS 4;
```

Database `customer_id` থেকে hash value তৈরি করে row partition-এ রাখে।

---

# 1️⃣5️⃣ RANGE vs LIST vs HASH

|Type|ভাগ করার ভিত্তি|Common Use|
|---|---|---|
|RANGE|Range|Date/time|
|LIST|Specific values|Region/category|
|HASH|Hash distribution|Even distribution|

সহজভাবে:

```text
Date → RANGE
Category/Region → LIST
Distribution → HASH
```

---

# 1️⃣6️⃣ Partitioning বনাম Indexing ⭐⭐⭐

এটা interview-এর জন্য খুব important।

### Index

```text
একটি table
     ↓
Index
     ↓
দ্রুত specific rows খুঁজে পাওয়া
```

### Partition

```text
একটি বড় table
     ↓
Multiple partitions
     ↓
Unnecessary partitions বাদ দেওয়া
```

অর্থাৎ:

> **Index এবং Partition একে অপরের replacement নয়।**

একসাথে ব্যবহার করা যায়।

---

# 1️⃣7️⃣ Example

ধরো:

```text
orders = 500 million rows
```

Partition:

```text
2024
2025
2026
2027
```

আর প্রতিটি partition-এ appropriate indexes থাকতে পারে।

Query:

```sql
WHERE order_date >= ...
AND customer_id = 100;
```

তখন:

```text
Partition pruning
       ↓
Relevant partition
       ↓
Index
       ↓
Matching rows
```

---

# 1️⃣8️⃣ Partitioning বনাম Sharding

দুটো এক জিনিস নয়।

### Partitioning

একই database-এর ভিতরে table ভাগ:

```text
One DB
│
└── orders
    ├── P1
    ├── P2
    └── P3
```

### Sharding

Data multiple database/server-এ ভাগ করা:

```text
DB Server 1 → customers 1–1M
DB Server 2 → customers 1M–2M
DB Server 3 → customers 2M–3M
```

সহজভাবে:

```text
Partitioning → One DB/table structure split
Sharding → Multiple database/server split
```

---

# 1️⃣9️⃣ কখন Partition ব্যবহার করব?

Partitioning সাধারণত useful হতে পারে যখন:

### ✅ 1. Table অনেক বড়

যেমন:

```text
100M+
500M+
1B+ rows
```

তবে **row count একাই partition করার কারণ নয়**।

---

### ✅ 2. Queries naturally partition key filter করে

যেমন:

```sql
WHERE order_date >= ...
AND order_date < ...
```

Date-based queries হলে RANGE partitioning meaningful হতে পারে।

---

### ✅ 3. Historical data আছে

যেমন:

```text
2020
2021
2022
2023
2024
2025
2026
```

Old partitions archive/manage করা সহজ হতে পারে।

---

### ✅ 4. Data lifecycle আছে

ধরো:

```text
Keep logs for 12 months
```

তাহলে পুরনো partition drop/archive করা efficient হতে পারে।

---

# 2️⃣0️⃣ কখন Partition ব্যবহার করব না? ❌

এটা খুব গুরুত্বপূর্ণ।

### ❌ Small table

```text
10,000 rows
```

এখানে partition করার প্রয়োজন সাধারণত নেই।

---

### ❌ শুধু performance-এর আশায়

অনেকে ভাবে:

> Partition করলেই query fast হবে।

না।

Partition key query-তে ব্যবহার না হলে pruning নাও হতে পারে।

---

### ❌ Too many partitions

যেমন:

```text
10 million partitions
```

খুব খারাপ design।

Partition-এরও management overhead আছে।

---

### ❌ Wrong partition key

ধরো business query:

```sql
WHERE customer_id = 100
```

কিন্তু partition:

```text
order_status
```

তাহলে partitioning হয়তো query-তে খুব বেশি সাহায্য করবে না।

---

# 2️⃣1️⃣ Partition Key কী?

যে column/expression দিয়ে table partition করা হয় সেটাই:

> **Partition Key**

Example:

```sql
PARTITION BY RANGE (YEAR(order_date))
```

এখানে:

```text
Partition Key = order_date / YEAR(order_date) expression
```

---

# 2️⃣2️⃣ Good Partition Key

Good partition key-এর বৈশিষ্ট্য:

```text
Frequently filtered
Predictable
Meaningful ranges
Manageable number of partitions
Good data distribution
```

Date খুব common কারণ:

```text
orders
logs
events
bookings
transactions
```

সবগুলোতেই time dimension থাকে।

---

# 2️⃣3️⃣ Orders Table — Practical Design ⭐⭐⭐

ধরো:

```text
orders
1 billion rows
```

Fields:

```text
order_id
customer_id
order_date
status
amount
```

Business query:

```sql
SELECT SUM(amount)
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2026-02-01';
```

এখানে:

```text
RANGE(order_date)
```

ভালো candidate হতে পারে।

---

# 2️⃣4️⃣ Logs Table — Best Practical Example

Logs naturally time-based।

```text
application_logs
```

Data:

```text
2026-01
2026-02
2026-03
...
```

তাই:

```text
RANGE(date/time)
```

খুব natural।

Architecture:

```text
application_logs
│
├── p2026_01
├── p2026_02
├── p2026_03
├── p2026_04
└── ...
```

---

# 2️⃣5️⃣ Log Retention ⭐⭐⭐

ধরো requirement:

> Keep logs only 12 months.

Partitioning থাকলে conceptual workflow:

```text
Current
│
├── Jan
├── Feb
├── ...
└── Dec
```

পুরনো partition:

```text
archive/drop
```

করার মাধ্যমে lifecycle management সহজ হতে পারে।

এটা huge log table-এ বিশেষভাবে useful।

---

# 2️⃣6️⃣ Booking Table — Practical Design

আমাদের hotel system:

```text
bookings
```

Columns:

```text
booking_id
customer_id
room_id
check_in
check_out
status
created_at
```

ধরো:

```text
500 million bookings
```

Business queries:

```text
Recent bookings
Monthly bookings
Yearly revenue
Historical booking analysis
```

এখানে time-based partitioning candidate হতে পারে।

Possible key:

```text
created_at
```

অথবা business requirement অনুযায়ী:

```text
check_in
```

কিন্তু কোনটা নেব তা query pattern-এর উপর নির্ভর করবে।

---

# 2️⃣7️⃣ `created_at` vs `check_in`

এখানে database designer হিসেবে চিন্তা করতে হবে।

যদি query:

```sql
WHERE created_at BETWEEN ...
```

তাহলে:

```text
created_at
```

logical partition key।

যদি query:

```sql
WHERE check_in BETWEEN ...
```

হয়, তাহলে:

```text
check_in
```

আরও relevant হতে পারে।

### Golden Rule:

> **Partition key business query pattern দেখে নির্বাচন করো।**

---

# 2️⃣8️⃣ Partition Pruning Example

ধরো:

```text
p2024
p2025
p2026
p2027
```

Query:

```sql
SELECT COUNT(*)
FROM orders
WHERE order_date >= '2026-01-01'
AND order_date < '2026-02-01';
```

Database ideally:

```text
p2024 ❌
p2025 ❌
p2026 ✅
p2027 ❌
```

তারপর p2026-এর relevant rows search করবে।

এটাই:

# Partition Pruning

---

# 2️⃣9️⃣ Query যদি Partition Key না ব্যবহার করে?

ধরো partition:

```text
RANGE(order_date)
```

কিন্তু query:

```sql
SELECT *
FROM orders
WHERE customer_id = 100;
```

এখানে database customer_id খুঁজতে multiple partitions consider করতে হতে পারে।

তাই:

```text
Partitioning
≠
Automatically faster
```

---

# 3️⃣0️⃣ Partition + Index

Strong production design অনেক সময়:

```text
Partition
   +
Index
   +
Good Query
```

Example:

```text
orders
│
├── p2025
│    └── indexes
│
├── p2026
│    └── indexes
│
└── p2027
     └── indexes
```

Exact index/partition behavior অবশ্য DBMS-specific।

---

# 3️⃣1️⃣ Partition Maintenance

Large systems-এ future partitions আগে থেকে plan করতে হয়।

ধরো:

```text
2026
2027
2028
```

কিন্তু 2029 এ data insert করতে হবে।

তাহলে partition strategy-তে future range handle করতে হবে।

কিছু DBMS-এ:

```text
ADD PARTITION
SPLIT PARTITION
MERGE PARTITION
DROP PARTITION
```

এর মতো operations আছে।

Syntax DBMS অনুযায়ী আলাদা।

---

# 3️⃣2️⃣ Partition Drop বনাম DELETE ⭐⭐⭐

ধরো January 2025-এর সব logs remove করতে হবে।

Traditional:

```sql
DELETE FROM logs
WHERE log_date >= '2025-01-01'
AND log_date < '2025-02-01';
```

Huge dataset হলে অনেক rows individually process করতে হতে পারে।

Partitioned design-এ পুরো partition lifecycle operation ব্যবহার করা যেতে পারে:

```text
p2025_01
    ↓
DROP / archive
```

এটি retention management-এ অনেক বেশি efficient হতে পারে।

**তবে DROP PARTITION destructive operation—production-এ আগে backup/retention policy নিশ্চিত করতে হবে।**

---

# 3️⃣3️⃣ Partitioning-এর Cost

Partitioning-এর সুবিধা আছে, কিন্তু free নয়।

Potential drawbacks:

```text
More complexity
More administration
Partition management
Query planning overhead
Wrong design → little/no benefit
Too many partitions → overhead
Constraints/index behavior can be DBMS-specific
```

তাই:

> **Partition because you have a problem it solves—not because partitioning sounds advanced.**

---

# 3️⃣4️⃣ Partitioning Decision Flow ⭐⭐⭐

Database designer হিসেবে:

```text
Table কি খুব বড়?
       ↓
      YES
       ↓
Queries কি naturally কোনো range/value filter করে?
       ↓
      YES
       ↓
Partition pruning সম্ভব?
       ↓
      YES
       ↓
Partition key নির্বাচন
       ↓
Partition count design
       ↓
Indexes design
       ↓
EXPLAIN / benchmark
       ↓
Production
```

---

# 3️⃣5️⃣ Partitioning + Query Optimization

আমাদের আগের workflow:

```text
Slow Query
   ↓
EXPLAIN
   ↓
Index
   ↓
Optimize
```

Large table-এ এখন:

```text
Slow Query
   ↓
EXPLAIN
   ↓
Partition pruning হচ্ছে?
   ↓
Index ব্যবহার হচ্ছে?
   ↓
Rows examined?
   ↓
Optimize
```

---

# 3️⃣6️⃣ Partitioning + Database Designer

তুমি যদি ভবিষ্যতে database designer হও, তাহলে তোমাকে এই প্রশ্নগুলো করতে হবে:

```text
1. Table কত বড় হবে?
2. Data growth rate কত?
3. Query pattern কী?
4. Historical data কতদিন থাকবে?
5. Date-based filtering আছে?
6. Partition pruning সম্ভব?
7. কত partition হবে?
8. Index কোথায় লাগবে?
9. Archive policy কী?
10. Backup/restore strategy কী?
```

---

# 3️⃣7️⃣ Real Architecture

ধরো একটি e-commerce company:

```text
orders
500M rows
```

Design:

```text
orders
│
├── 2024
│
├── 2025
│
├── 2026
│
└── 2027
```

প্রতিটি partition-এ appropriate indexing:

```text
order_date
customer_id
```

Query:

```text
2026 orders
      ↓
Partition pruning
      ↓
p2026
      ↓
Index
      ↓
Rows
```

---

# 3️⃣8️⃣ Partitioning vs Normalization

এগুলো completely different concepts।

### Normalization

Data structure/design:

```text
Reduce redundancy
Improve consistency
```

### Partitioning

Large table management:

```text
Split physical/logical data access
Improve manageability
Enable pruning
```

অর্থাৎ:

```text
Normalization → Data design
Partitioning → Large-scale data organization
```

একসাথে ব্যবহার করা যায়।

---

# 3️⃣9️⃣ Partitioning vs Sharding vs Index

|Feature|Index|Partitioning|Sharding|
|---|---|---|---|
|Main purpose|Faster lookup|Split large table|Distribute data|
|Scope|Table access structure|Table partitions|Multiple DB/server|
|Multiple servers|❌|Usually ❌|✅|
|Pruning|❌|✅|Routing/shard pruning|
|Complexity|Low–Medium|Medium|High|
|Typical scale|Small → Huge|Huge tables|Very large distributed systems|

---

# 4️⃣0️⃣ Interview Questions ⭐⭐⭐

### Q1. What is database partitioning?

**Answer:**

> Database partitioning is the technique of dividing a large table into smaller logical partitions based on a partition key, while presenting the data as one logical table.

---

### Q2. What is partition pruning?

> Partition pruning is the optimizer's ability to skip irrelevant partitions and access only partitions that can contain rows matching the query predicate.

---

### Q3. RANGE vs LIST vs HASH?

```text
RANGE → ranges, especially dates
LIST → predefined values
HASH → hash-based distribution
```

---

### Q4. Does partitioning replace indexing?

**No.**

```text
Partitioning ≠ Indexing
```

They solve different problems and can work together.

---

### Q5. When should you avoid partitioning?

```text
Small table
No useful partition key
No pruning benefit
Too many partitions
Complexity not justified
```

---

# 🧠 Class 64 Golden Rules

```text
1. Partitioning → Large table ভাগ করা

2. Partition Key → যে value/expression দিয়ে partition করা হয়

3. RANGE → Range/date-based data

4. LIST → Specific values

5. HASH → Hash-based distribution

6. Partition Pruning → Unnecessary partitions skip করা

7. Partitioning ≠ Indexing

8. Partitioning ≠ Sharding

9. Large table ≠ Automatically partition করতে হবে

10. Query pattern দেখে partition key নির্বাচন করো

11. Date/time → Common RANGE partition candidate

12. Logs → Time-based partition খুব common

13. Orders → Date-based partition useful হতে পারে

14. Booking → created_at/check_in query pattern অনুযায়ী নির্বাচন

15. Too many partitions → Bad

16. Small table → Usually unnecessary

17. Partition + Index একসাথে ব্যবহার করা যায়

18. Retention management-এ partition useful

19. DROP partition → powerful but destructive

20. EXPLAIN/benchmark দিয়ে verify করো

21. Partitioning solves a specific scale/management problem

22. Good database design = Requirement + Query Pattern + Data Growth
```

---

# 📝 Class 64 Assignment

## Task 1 — Basic

Explain:

```text
Partition
Partition Key
Partition Pruning
```

---

## Task 2 — Type

নিচের ক্ষেত্রে কোন partitioning সবচেয়ে logical?

```text
A. Orders by year
B. Customers by region
C. Data evenly distributed using customer_id
```

Choose:

```text
RANGE
LIST
HASH
```

---

## Task 3 — Orders Design ⭐

তোমার `orders` table:

```text
order_id
customer_id
order_date
amount
```

Data:

```text
500 million rows
```

এটাকে 2024, 2025, 2026, 2027 অনুযায়ী partition করার design লেখো।

---

## Task 4 — Partition Pruning ⭐⭐⭐

Partitions:

```text
p2024
p2025
p2026
p2027
```

Query:

```sql
SELECT SUM(amount)
FROM orders
WHERE order_date >= '2026-05-01'
AND order_date < '2026-06-01';
```

**কোন partition(s) relevant হতে পারে এবং কেন?**

---

## Task 5 — Hotel Booking

Hotel system:

```text
500 million bookings
```

Columns:

```text
booking_id
customer_id
room_id
check_in
check_out
created_at
status
```

প্রশ্ন:

**`created_at` নাকি `check_in`—কোনটাকে partition key হিসেবে নেবে?**

শুধু answer নয়, **query pattern দিয়ে justification** দাও।

---

## Task 6 — Interview Challenge 🔥

একজন interviewer বলল:

> **"Our orders table has 800 million rows. Should we partition it?"**

তুমি সরাসরি `YES` বলবে না।

তোমার answer হওয়া উচিত:

```text
First:
→ Query patterns
→ Data growth
→ Retention policy
→ Partition key
→ Partition pruning possibility
→ Existing indexes
→ EXPLAIN / benchmark
→ Operational complexity

Then:
→ Decide whether partitioning is justified
```

---

## 🎯 আজকের সবচেয়ে গুরুত্বপূর্ণ Concept

এক লাইনে মনে রাখো:

```text
Huge Table
    ↓
Partition Key
    ↓
Partitions
    ↓
Query Filter
    ↓
Partition Pruning
    ↓
Only relevant data
    ↓
Better performance / management
```

আর **Database Designer-এর Golden Rule**:

> **“Partitioning করব কারণ table বড়—এটা যথেষ্ট কারণ নয়; partitioning করব কারণ data/query/retention pattern থেকে measurable benefit পাওয়া যাবে।”**

**Next → Class 65: Database Replication & High Availability**  
সেখানে আমরা শিখব **Primary/Replica, Read Replica, Replication, Failover, High Availability, Backup বনাম Replication, এবং Django application-এ read/write database routing**।


----

# 📚 Class 65 — Database Replication & High Availability

আজ আমরা Database Engineering-এর আরেকটি **production-level topic** শিখব।

Class 64-এ আমরা বড় table কীভাবে **Partition** করা যায় শিখেছি।

আজকের প্রশ্ন:

> **Database server যদি down হয়ে যায়, তাহলে application কী করবে?**

অথবা:

> **একসাথে হাজার হাজার user database থেকে read করলে কীভাবে load কমাব?**

এখানেই আসে:

```text
Replication
High Availability
Read Replica
Failover
Backup
Database Routing
```

---

# 1️⃣ Replication কী?

সহজভাবে:

> **একটি database-এর data অন্য database server-এ কপি/replicate করে রাখাকে Database Replication বলে।**

ধরো আমাদের primary database:

```text
id="p7m3x1"
Primary DB
    │
    │ Replication
    ↓
Replica DB
```

আরও replica থাকতে পারে:

```text
id="k4q8n2"
             ┌──→ Replica 1
Primary DB ──┼──→ Replica 2
             └──→ Replica 3
```

---

# 2️⃣ Primary এবং Replica কী?

### Primary

যে database সাধারণত application-এর **write operations** গ্রহণ করে।

```text
INSERT
UPDATE
DELETE
```

উদাহরণ:

```text
id="x8r2m5"
Primary DB
   ↑
INSERT order
UPDATE stock
DELETE user
```

### Replica

Primary থেকে data replicate করে রাখা database server।

অনেক architecture-এ replica মূলত **read traffic** handle করে।

```text
id="v3q7k1"
Replica
   ↑
SELECT
SELECT
SELECT
```

তাই একে বলা হয়:

# Read Replica

---

# 3️⃣ Basic Architecture ⭐⭐⭐

একটা simple production architecture:

```text
                 ┌──────────────┐
                 │   Django     │
                 │ Application  │
                 └──────┬───────┘
                        │
                 ┌──────┴──────┐
                 │             │
              WRITE          READ
                 │             │
                 ↓             ↓
            ┌─────────┐   ┌─────────┐
            │ Primary │──→│ Replica │
            │   DB    │   │   DB    │
            └─────────┘   └─────────┘
```

---

# 4️⃣ Replication কীভাবে কাজ করে?

ধরো:

```text
Primary
orders = 100
```

User নতুন order দিল:

```sql
INSERT INTO orders (...);
```

Primary:

```text
100
 ↓
101
```

Replication mechanism-এর মাধ্যমে replica-তেও পরিবর্তন পৌঁছায়:

```text
Primary = 101
Replica = 101
```

Conceptually:

```text
Application
     ↓
Primary
     ↓
Replication
     ↓
Replica
```

বাস্তব replication mechanism DBMS অনুযায়ী আলাদা।

---

# 5️⃣ Primary → Replica

একাধিক replica:

```text
                    ┌── Replica 1
                    │
Primary ────────────┼── Replica 2
                    │
                    └── Replica 3
```

এখন read workload distribute করা যায়।

যেমন:

```text
100,000 SELECT requests
```

একটা server-এর বদলে:

```text
Replica 1 → 33k
Replica 2 → 33k
Replica 3 → 34k
```

এটা architecture/load balancing strategy-এর উপর নির্ভর করবে।

---

# 6️⃣ Read Replica কেন দরকার?

ধরো application-এ:

```text
10% → WRITE
90% → READ
```

যেমন:

```text
INSERT order
UPDATE profile
```

কিন্তু:

```text
SELECT products
SELECT categories
SELECT orders
SELECT dashboard
SELECT reports
```

অনেক বেশি।

তখন:

```text
Primary
  ↓
Writes

Replicas
  ↓
Reads
```

করলে primary-এর read workload কমানো যেতে পারে।

---

# 7️⃣ Read Scaling ⭐⭐⭐

ধরো:

```text
Primary
CPU = 90%
```

কারণ:

```text
READ + WRITE
```

আমরা read replicas যোগ করলাম:

```text
Primary
  ↓
Write

Replica 1 → Read
Replica 2 → Read
Replica 3 → Read
```

এখন read workload scale করা সহজ হতে পারে।

---

# 8️⃣ কিন্তু Replica কি সবসময় Up-to-Date?

না।

এটাই খুব important।

Replication-এ কিছু ক্ষেত্রে:

```text
Primary
   ↓
   101
```

Replica হয়তো:

```text
Replica
   ↓
   100
```

কিছু সময়ের জন্য।

এটাকে বলা হয়:

# Replication Lag

---

# 9️⃣ Replication Lag ⭐⭐⭐

ধরো:

```text
T1:
INSERT order 500
```

Primary immediately:

```text
order = 500
```

কিন্তু replica-তে change পৌঁছাতে একটু সময় লাগতে পারে।

তখন:

```text
Primary → 500
Replica → 499
```

এই difference হলো:

> **Replication Lag**

---

# 🔟 Real Problem

User order create করল:

```text
POST /orders
```

Write গেল:

```text
Primary
```

তারপর immediately:

```text
GET /orders
```

যদি GET replica-তে যায়:

```text
Primary → order exists
Replica → order not arrived yet
```

User দেখতে পারে:

```text
"No order"
```

যদিও order successfully তৈরি হয়েছে।

এটাকে বলা যায়:

# Read-after-write consistency problem

---

# 1️⃣1️⃣ Read-after-write Solution

Critical read-এর ক্ষেত্রে:

```text
WRITE
 ↓
Primary
 ↓
Immediately READ
 ↓
Primary
```

অথবা system অনুযায়ী এমন consistency strategy ব্যবহার করতে হবে যাতে replica lag-এর কারণে incorrect UX না হয়।

---

# 1️⃣2️⃣ Primary/Replica Routing

Concept:

```text
INSERT
UPDATE
DELETE
    ↓
Primary
```

আর:

```text
SELECT
    ↓
Replica
```

কিন্তু সব SELECT blindly replica-তে পাঠানো ঠিক নয়।

---

# 1️⃣3️⃣ কোন Read Primary-তে যাবে?

যেমন:

```text
User just updated profile
```

তারপর:

```text
GET profile
```

Immediate consistency দরকার হলে primary ব্যবহার করা ভালো হতে পারে।

অন্যদিকে:

```text
Product catalog
```

যেখানে কয়েক milliseconds/seconds lag acceptable:

```text
Replica
```

ব্যবহার করা যেতে পারে।

---

# 1️⃣4️⃣ Failover কী?

ধরো:

```text
Primary DB
     ↓
     💥 DOWN
```

Application আর write করতে পারছে না।

তখন একটি healthy replica-কে নতুন primary করা হতে পারে।

```text
Before:

Primary
   ↓
Replica


After:

Old Primary 💥

Replica
   ↓
New Primary
```

এটাকে বলে:

# Failover

---

# 1️⃣5️⃣ High Availability — HA ⭐⭐⭐

High Availability-এর উদ্দেশ্য:

> **System যেন failure হলেও যতটা সম্ভব available থাকে।**

Architecture:

```text
Application
     ↓
DB layer
  ┌──┴──┐
  ↓     ↓
Primary Replica
```

Primary fail করলে:

```text
Replica
   ↓
Promote
   ↓
New Primary
```

তারপর application নতুন primary-তে write করবে।

---

# 1️⃣6️⃣ HA ≠ Replication

এটা interview-এর জন্য খুব important।

Replication:

```text
Data copies
```

High Availability:

```text
System remains available despite failures
```

Replication HA-এর একটি component হতে পারে।

কিন্তু শুধু replication থাকলেই complete HA architecture হয় না।

---

# 1️⃣7️⃣ Failover Flow

```text
Primary
   ↓
Health Check
   ↓
Failure detected
   ↓
Choose healthy replica
   ↓
Promote replica
   ↓
Update routing
   ↓
Application reconnects
```

---

# 1️⃣8️⃣ Automatic vs Manual Failover

### Manual

Admin manually:

```text
Replica → Primary
```

করবে।

### Automatic

Monitoring/orchestration system:

```text
Failure detected
       ↓
Automatic promotion
       ↓
Routing updated
```

করতে পারে।

Production systems-এ automation useful, তবে incorrect automatic failover-এর risk-ও আছে।

---

# 1️⃣9️⃣ Split Brain ⭐

Advanced HA problem।

ধরো ভুলভাবে দুই server-ই মনে করছে:

```text
"I am Primary"
```

তাহলে:

```text
DB1 → Primary
DB2 → Primary
```

দু জায়গায় conflicting writes হতে পারে।

এটা:

# Split Brain

HA system design-এ এটি prevent করা অত্যন্ত গুরুত্বপূর্ণ।

---

# 2️⃣0️⃣ Backup বনাম Replication ⭐⭐⭐

অনেক beginner ভাবে:

> Replica আছে → Backup দরকার নেই।

❌ ভুল।

Replication এবং Backup-এর উদ্দেশ্য আলাদা।

---

# 2️⃣1️⃣ Replication

```text
Primary
   ↓
Replica
```

যদি Primary-তে ভুল করে:

```sql
DELETE FROM customers;
```

হয় এবং সেই change replicate হয়ে যায়:

```text
Primary → DELETE
Replica → DELETE
```

Replica-ও data হারাতে পারে।

---

# 2️⃣2️⃣ Backup

Backup হলো:

> নির্দিষ্ট সময়ের database copy/snapshot/data recovery source রাখা।

যেমন:

```text
Monday Backup
Tuesday Backup
Wednesday Backup
```

যদি ভুল করে:

```text
DELETE all customers
```

হয়ে যায়, backup থেকে recovery করা সম্ভব হতে পারে।

---

# 2️⃣3️⃣ Backup বনাম Replication

||Backup|Replication|
|---|---|---|
|Main purpose|Recovery|Availability/read scaling|
|Historical recovery|✅|❌|
|Server failure|সাহায্য করতে পারে|দ্রুত failover-এ useful|
|Accidental DELETE|Recovery source হতে পারে|DELETE replicate হতে পারে|
|Read scaling|❌|✅|
|HA|নিজে complete HA নয়|HA architecture-এর অংশ হতে পারে|

### Golden Rule ⭐

> **Replication is not a backup.**

---

# 2️⃣4️⃣ RPO এবং RTO ⭐⭐⭐

আজকের class-এর important production concepts।

## RPO — Recovery Point Objective

প্রশ্ন:

> Failure হলে সর্বোচ্চ কত data loss tolerate করতে পারি?

ধরো:

```text
RPO = 5 minutes
```

মানে business এমন architecture চায় যাতে recovery scenario-তে প্রায় 5 মিনিটের বেশি data loss না হয়।

---

# 2️⃣5️⃣ RTO — Recovery Time Objective

প্রশ্ন:

> Failure-এর পর কত সময়ের মধ্যে system restore করতে হবে?

ধরো:

```text
RTO = 10 minutes
```

মানে:

```text
Failure
 ↓
Recovery
 ↓
≤ 10 minutes target
```

---

# 2️⃣6️⃣ RPO vs RTO

মনে রাখো:

```text
RPO → How much data can we lose?
RTO → How much time can we be down?
```

---

# 2️⃣7️⃣ Django Multiple Database

Django multiple database support করে।

`settings.py`:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "app_db",
        "USER": "postgres",
        "PASSWORD": "password",
        "HOST": "primary-db",
        "PORT": "5432",
    },

    "replica": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "app_db",
        "USER": "postgres",
        "PASSWORD": "password",
        "HOST": "replica-db",
        "PORT": "5432",
    },
}
```

এখানে:

```text
default → Primary
replica → Read Replica
```

---

# 2️⃣8️⃣ Django Direct Database Selection

Primary:

```python
Order.objects.using("default").create(
    customer_id=1,
    amount=500
)
```

Replica:

```python
orders = Order.objects.using("replica").all()
```

---

# 2️⃣9️⃣ Django Database Router ⭐⭐⭐

প্রতিবার `.using()` manually লেখা inconvenient।

তাই Django-তে:

> **Database Router**

ব্যবহার করা যায়।

Concept:

```text
SELECT
 ↓
Replica

INSERT
UPDATE
DELETE
 ↓
Primary
```

---

# 3️⃣0️⃣ Basic Router

```python
class DatabaseRouter:

    def db_for_read(self, model, **hints):
        return "replica"

    def db_for_write(self, model, **hints):
        return "default"
```

তারপর:

```python
DATABASE_ROUTERS = [
    "myapp.routers.DatabaseRouter"
]
```

---

# 3️⃣1️⃣ Router-এর সমস্যা

এই simple router production-ready নয়।

কারণ:

```text
WRITE → Primary
READ → Replica
```

কিন্তু write-এর পর immediate read করলে replication lag problem হতে পারে।

Example:

```text
POST /order
   ↓
Primary

GET /order
   ↓
Replica

Replica lag
   ↓
Order not found
```

তাই real production architecture-এ routing rules আরও sophisticated হতে পারে।

---

# 3️⃣2️⃣ Better Django Strategy

Conceptually:

```text
Normal read
    ↓
Replica

Critical read after write
    ↓
Primary
```

আর failover হলে:

```text
Current Primary
      ↓
Failure
      ↓
New Primary
      ↓
Routing configuration/service discovery
```

---

# 3️⃣3️⃣ Read Replica Load Balancing

যদি 3 replicas থাকে:

```text
Primary
 ├── Replica 1
 ├── Replica 2
 └── Replica 3
```

Read traffic:

```text
SELECT
 ↓
Load Balancer / DB proxy / routing layer
 ↓
Replica 1/2/3
```

এতে application-কে প্রতিটি replica individually manage করতে নাও হতে পারে।

---

# 3️⃣4️⃣ Database Proxy Concept

Production architecture:

```text
Django
   ↓
DB Proxy
   ↓
┌───────────┬───────────┐
│           │           │
Primary   Replica1    Replica2
```

Proxy:

```text
WRITE → Primary
READ → Replica
```

করতে পারে এবং failover/routing সহজ করতে পারে—specific technology অনুযায়ী behavior আলাদা।

---

# 3️⃣5️⃣ Replication Types — Basic Concept

Replication বিভিন্নভাবে হতে পারে।

### Synchronous

```text
Primary
  ↓
wait
  ↓
Replica confirms
  ↓
Commit/ack
```

Data consistency বেশি strong হতে পারে, কিন্তু latency বাড়তে পারে।

### Asynchronous

```text
Primary
  ↓
Commit
  ↓
Replica receives later
```

Performance/latency ভালো হতে পারে, কিন্তু replication lag হতে পারে।

---

# 3️⃣6️⃣ Sync vs Async

||Synchronous|Asynchronous|
|---|---|---|
|Replica confirmation|অপেক্ষা করে|সাধারণত অপেক্ষা করে না|
|Consistency|Stronger সম্ভাবনা|Lag possible|
|Latency|বেশি হতে পারে|কম হতে পারে|
|Complexity|Higher|তুলনামূলক সহজ|
|Data loss risk on failure|architecture অনুযায়ী কম হতে পারে|recent unreplicated data থাকতে পারে|

বাস্তব DBMS implementation অনেক বেশি nuanced।

---

# 3️⃣7️⃣ Hotel Management Example ⭐⭐⭐

আমাদের hotel system:

```text
Django
  ↓
Database
```

Production-এ:

```text
                    ┌── Replica 1
                    │
Django → Primary ───┼── Replica 2
                    │
                    └── Replica 3
```

### Booking create

```text
POST /bookings
       ↓
Primary
```

### Available rooms search

```text
GET /rooms/available
       ↓
Replica
```

কিন্তু final booking confirmation-এর critical availability check:

```text
Transaction
   ↓
Primary
   ↓
Lock
   ↓
Check availability
   ↓
Create booking
```

এখানে consistency গুরুত্বপূর্ণ।

---

# 3️⃣8️⃣ Hotel Failure Scenario

Primary:

```text
💥 DOWN
```

System:

```text
Replica 1
    ↓
Promote
    ↓
New Primary
```

Routing:

```text
Django
   ↓
New Primary
```

Read replicas architecture অনুযায়ী পুনরায় configure হতে পারে।

---

# 3️⃣9️⃣ E-commerce Example

Traffic:

```text
1000 requests/sec
```

ধরো:

```text
900 reads
100 writes
```

Architecture:

```text
                 Django
                   │
             ┌─────┴─────┐
             ↓           ↓
           WRITE        READ
             ↓           ↓
          Primary    Read Router
                        │
                  ┌─────┼─────┐
                  ↓     ↓     ↓
                 R1    R2    R3
```

এটাই read scaling-এর basic idea।

---

# 4️⃣0️⃣ Replication + Partitioning

দুটো একসাথে ব্যবহার করা যায়।

```text
Database
  │
  ├── Partitioning
  │      ↓
  │   Large table split
  │
  └── Replication
         ↓
      DB copies
```

Different problems solve করে:

```text
Partitioning → Large table/data organization
Replication → Availability/read scaling
```

---

# 4️⃣1️⃣ Replication + Indexing

এগুলোকেও combine করা যায়:

```text
Application
    ↓
Replica
    ↓
Partition
    ↓
Index
    ↓
Rows
```

Database architecture এখন:

```text
Index
+
Partition
+
Replication
+
Transactions
+
Locking
```

সবগুলো আলাদা সমস্যার solution।

---

# 4️⃣2️⃣ Full Production Architecture ⭐⭐⭐

একটি mature application:

```text
                 Users
                   ↓
              Load Balancer
                   ↓
             Django Servers
                   ↓
              DB Proxy
                   ↓
          ┌────────┴────────┐
          ↓                 ↓
       Primary           Replicas
          │              ┌──┴──┐
          │              ↓     ↓
          └──────────→   R1    R2
```

আর:

```text
Backup System
      ↓
Object Storage / Backup Storage
```

Monitoring:

```text
Monitoring
   ↓
DB health
Replication lag
CPU
Memory
Connections
Disk
Errors
```

---

# 4️⃣3️⃣ Monitoring কী কী?

Production database-এ monitor করতে পারো:

```text
CPU
Memory
Disk usage
Connections
Query latency
Slow queries
Replication lag
Lock waits
Deadlocks
Replication status
Backup status
```

---

# 4️⃣4️⃣ Database Failure-এর সময় কী হবে?

ধরো:

```text
Primary 💥
```

### Without HA

```text
Application
   ↓
Primary ❌
   ↓
Application down
```

### With HA

```text
Primary ❌
   ↓
Failover
   ↓
New Primary
   ↓
Application continues
```

Recovery speed architecture অনুযায়ী নির্ভর করবে।

---

# 4️⃣5️⃣ Backup Strategy

একটি production database-এর জন্য সাধারণভাবে ভাবতে হবে:

```text
Primary
   +
Replica(s)
   +
Backup
   +
Monitoring
   +
Failover Strategy
```

একটা জিনিসের উপর depend করা উচিত নয়।

---

# 4️⃣6️⃣ Common Mistakes ❌

### ❌ Mistake 1

> Replica = Backup

ভুল।

---

### ❌ Mistake 2

> Replication থাকলে database কখনো down হবে না।

ভুল।

---

### ❌ Mistake 3

> সব SELECT replica-তে পাঠাব।

ভুল।

Consistency requirements বুঝতে হবে।

---

### ❌ Mistake 4

> Failover মানেই application automatically ঠিক হয়ে যাবে।

সবসময় না।

Routing, connection handling, health checks, promotion, DNS/proxy/service discovery ইত্যাদি properly design করতে হয়।

---

### ❌ Mistake 5

> অনেক replica = unlimited scaling

ভুল।

Replication নিজেও network, storage এবং write/replication overhead তৈরি করে।

---

# 🧠 Class 65 Golden Rules ⭐⭐⭐

```text
1. Replication → Database data copy রাখা

2. Primary → Usually handles writes

3. Replica → Copy of primary data

4. Read Replica → Read workload handle করতে পারে

5. Replication Lag → Primary ও Replica data-এর temporary difference

6. Read-after-write → Replica lag-এর কারণে সমস্যা হতে পারে

7. Failover → Failed primary-এর বদলে another DB promote করা

8. High Availability → Failure-এর পর service available রাখার goal

9. Replication ≠ High Availability

10. Replication ≠ Backup

11. Backup → Disaster / accidental deletion recovery

12. RPO → Acceptable data loss

13. RTO → Acceptable recovery time

14. Synchronous → Stronger consistency, potentially higher latency

15. Asynchronous → Lower latency, replication lag possible

16. Django → Multiple DB support করে

17. Database Router → Read/write routing করতে পারে

18. Write → Primary

19. Read → Replica, when consistency allows

20. Critical read → Primary হতে পারে

21. Deadlock/locking → Concurrency control

22. Partitioning → Large table management

23. Replication → Availability/read scaling

24. Indexing → Query performance

25. Production DB → Backup + Replication + Monitoring + Failover
```

---

# 📝 Class 65 Assignment

## Task 1 — Basic

Explain:

```text
Primary
Replica
Read Replica
Replication
Replication Lag
Failover
High Availability
```

---

## Task 2 — Architecture ⭐

এই architecture complete করো:

```text
Django
  ↓
?
  ↓
┌───────────────┐
│               │
?               ?
│               │
Write           Read
```

---

## Task 3 — Backup vs Replication ⭐⭐⭐

এই scenario:

> একজন admin ভুল করে `customers` table-এর সব rows delete করে ফেলেছে। সেই DELETE replica-তেও replicate হয়েছে।

প্রশ্ন:

**কেন replica থেকে সহজে recovery করা যাবে না এবং এখানে backup কেন দরকার?**

---

## Task 4 — Replication Lag

Timeline:

```text
10:00:00 → User creates order
10:00:00 → Primary has order
10:00:01 → Replica still hasn't received it
```

User যদি `GET /orders` করে এবং request replica-তে যায়, কী সমস্যা হতে পারে?

---

## Task 5 — Django Router ⭐⭐⭐

এই requirement:

```text
INSERT → Primary
UPDATE → Primary
DELETE → Primary
SELECT → Replica
```

একটি basic Django `DatabaseRouter` লেখো।

---

## Task 6 — Hotel System 🔥

আমাদের hotel application-এর জন্য architecture design করো:

```text
Django
Primary
Replica 1
Replica 2
Backup
Failover
```

তারপর explain করো:

1. Booking কোথায় write হবে?
    
2. Room search কোথায় read হবে?
    
3. Final availability check কোথায় হবে?
    
4. Primary down হলে কী হবে?
    
5. Backup কেন আলাদা রাখতে হবে?
    

---

# 🎯 Interview Challenge

Interviewer জিজ্ঞেস করল:

> **"We have a Django e-commerce application. The database receives 90% reads and 10% writes. How would you scale the database?"**

Strong answer:

```text
Current DB
    ↓
Analyze workload
    ↓
Primary + Read Replicas
    ↓
Writes → Primary
Reads → Replicas
    ↓
Monitor replication lag
    ↓
Critical read → Primary when needed
    ↓
Load balancing / routing
    ↓
Backup
    ↓
Failover strategy
    ↓
Monitoring
```

আর যদি জিজ্ঞেস করে:

> **"Is replication a backup?"**

তোমার এক লাইনের answer:

> **No. Replication improves availability/read scaling, while backups are primarily for recovery and historical restore.**

---

## 🏆 আজকের সবচেয়ে গুরুত্বপূর্ণ ধারণা

পুরো Class 65-কে এভাবে মনে রাখো:

```text
                 DATABASE
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
    Indexing     Partitioning  Replication
        │            │            │
   Query Speed   Large Table   HA / Read Scale
                                  │
                         ┌────────┴────────┐
                         ↓                 ↓
                      Primary           Replica
                         │
                       WRITE
                                           │
                                         READ
```

এবং পুরো production mindset:

```text
Database Engineering
       ↓
Transactions
       ↓
Locking
       ↓
Indexing
       ↓
Partitioning
       ↓
Replication
       ↓
Backup
       ↓
Failover
       ↓
High Availability
```

**Next → Class 66: Database Security & Access Control** — সেখানে আমরা শিখব **Database User/Role, GRANT, REVOKE, Least Privilege, Authentication vs Authorization, SQL Injection, Django DB security, sensitive data protection এবং production database security design**।

---
# 📚 Class 66 — Database Security & Access Control

আজকের Class 66 খুবই গুরুত্বপূর্ণ, কারণ **ভালো database design শুধু fast হওয়া যথেষ্ট নয়—secure-ও হতে হবে।**

আমরা শিখব:

1. Database Security কী
    
2. User & Role
    
3. Authentication vs Authorization
    
4. `GRANT`
    
5. `REVOKE`
    
6. Least Privilege
    
7. SQL Injection
    
8. Django Database Security
    
9. Sensitive Data Protection
    
10. Password Security
    
11. Secrets Management
    
12. Production Database Security Architecture
    
13. Common Security Mistakes
    
14. Database Security Checklist
    

---

# 1️⃣ Database Security কী?

সহজভাবে:

> **Database-এর data এবং database operations-কে unauthorized access, modification, deletion এবং leakage থেকে protect করাকে Database Security বলে।**

ধরো hotel application-এর database:

```text
customers
rooms
bookings
payments
```

সব user-এর সব data access করা উচিত নয়।

যেমন:

```text
Customer
   ↓
নিজের booking দেখতে পারবে

Receptionist
   ↓
Booking manage করতে পারবে

Finance
   ↓
Payment-related data দেখতে পারবে

DB Admin
   ↓
Database administration
```

এটাই access control-এর ধারণা।

---

# 2️⃣ Database Security-এর Main Goals ⭐

```text
Confidentiality
Integrity
Availability
```

### Confidentiality

Unauthorized person যেন data দেখতে না পারে।

### Integrity

Unauthorized/invalid modification যেন না হয়।

### Availability

Authorized user যেন প্রয়োজনের সময় database ব্যবহার করতে পারে।

এগুলোকে অনেক সময় **CIA Triad** বলা হয়:

```text
C → Confidentiality
I → Integrity
A → Availability
```

---

# 3️⃣ Authentication vs Authorization ⭐⭐⭐

এটা অবশ্যই পরিষ্কার করতে হবে।

## Authentication

> **তুমি কে?**

Example:

```text
Username
Password
```

User login করল।

```text
Rahim
   ↓
Login
   ↓
Identity verified
```

---

## Authorization

> **তুমি কী করতে পারবে?**

ধরো Rahim authenticated।

কিন্তু সে:

```text
DELETE customers
```

করতে পারবে কি?

এটা authorization-এর বিষয়।

---

# 4️⃣ সহজে মনে রাখো

```text
Authentication
      ↓
WHO are you?

Authorization
      ↓
WHAT can you do?
```

### Example

```text
Login successful
        ↓
Authentication ✅
        ↓
Can delete users?
        ↓
Authorization
```

---

# 5️⃣ Database User কী?

Database server-এ আলাদা user account থাকতে পারে।

যেমন:

```text
root
app_user
report_user
readonly_user
admin_user
```

প্রত্যেক user-এর permission আলাদা হতে পারে।

---

# 6️⃣ কেন Application-এর জন্য `root` ব্যবহার করা উচিত নয়? ❌

ধরো Django application:

```text
Django
   ↓
root database user
```

যদি application-এর কোনো security vulnerability হয় এবং attacker database credential/access পেয়ে যায়:

```text
Attacker
   ↓
root
   ↓
Full DB control
```

খুব dangerous।

Better:

```text
Django
   ↓
app_user
   ↓
Only required permissions
```

---

# 7️⃣ Role কী?

Role হলো permissions-এর একটি logical collection।

ধরো:

```text
role_readonly
role_app
role_reporting
role_admin
```

একজন user-কে role দেওয়া যায়।

Concept:

```text
User
 ↓
Role
 ↓
Permissions
```

---

# 8️⃣ User বনাম Role

```text
User
= কে database access করছে

Role
= সে কী ধরনের permission পাবে
```

Example:

```text
Rahim
   ↓
reporting_role
   ↓
SELECT permission
```

---

# 9️⃣ GRANT ⭐⭐⭐

`GRANT` দিয়ে permission দেওয়া হয়।

MySQL example:

```sql
GRANT SELECT
ON hotel_db.*
TO 'report_user'@'localhost';
```

মানে:

```text
report_user
     ↓
SELECT
     ↓
hotel_db
```

---

# 🔟 Multiple Permission

```sql
GRANT SELECT, INSERT, UPDATE
ON hotel_db.bookings
TO 'booking_user'@'localhost';
```

এই user:

```text
SELECT    ✅
INSERT    ✅
UPDATE    ✅
DELETE    ❌
```

---

# 1️⃣1️⃣ All Privileges

```sql
GRANT ALL PRIVILEGES
ON hotel_db.*
TO 'admin_user'@'localhost';
```

এটা powerful permission।

Production application user-কে blindly `ALL PRIVILEGES` দেওয়া উচিত নয়।

---

# 1️⃣2️⃣ REVOKE ⭐⭐⭐

Permission remove করতে:

```sql
REVOKE UPDATE
ON hotel_db.bookings
FROM 'booking_user'@'localhost';
```

এখন:

```text
SELECT → ✅
INSERT → ✅
UPDATE → ❌
```

---

# 1️⃣3️⃣ GRANT বনাম REVOKE

|Command|কাজ|
|---|---|
|`GRANT`|Permission দেওয়া|
|`REVOKE`|Permission সরানো|

মনে রাখো:

```text
GRANT  → Give
REVOKE → Remove
```

---

# 1️⃣4️⃣ Least Privilege ⭐⭐⭐

আজকের সবচেয়ে গুরুত্বপূর্ণ security principle:

> **একজন user/application-কে তার কাজের জন্য যতটুকু permission দরকার, শুধু ততটুকুই দেওয়া উচিত।**

এটাই:

# Principle of Least Privilege

---

# 1️⃣5️⃣ Example

ধরো reporting application শুধু report read করবে।

❌ Bad:

```text
report_user
→ SELECT
→ INSERT
→ UPDATE
→ DELETE
→ DROP
→ ALTER
```

এটা unnecessary।

✅ Better:

```text
report_user
→ SELECT
```

---

# 1️⃣6️⃣ Django Application User

ধরো Django application শুধু:

```text
SELECT
INSERT
UPDATE
```

করবে।

তাহলে application database user-এর:

```text
DELETE database
DROP table
ALTER database
```

permission দেওয়ার দরকার নেই—যদি application-এর প্রয়োজন না থাকে।

---

# 1️⃣7️⃣ Why Least Privilege Important?

ধরো application vulnerable হলো।

Attacker somehow application DB credential-এর access পেল।

### Full privilege:

```text
Attacker
   ↓
DB user
   ↓
DROP
DELETE
ALTER
UPDATE
```

Damage huge হতে পারে।

### Limited privilege:

```text
Attacker
   ↓
Limited DB user
   ↓
Limited operations
```

Blast radius কমে।

---

# 1️⃣8️⃣ SQL Injection ⭐⭐⭐⭐⭐

এটা database security-এর সবচেয়ে famous vulnerability-গুলোর একটি।

SQL Injection হলো:

> **Untrusted user input এমনভাবে SQL query-তে ঢুকে যায় যে attacker query-এর intended meaning পরিবর্তন করতে পারে।**

---

# 1️⃣9️⃣ Vulnerable SQL Example

ধরো application username input নিচ্ছে:

```text
rahim
```

Developer ভুলভাবে string concatenate করল:

```python
query = (
    "SELECT * FROM users "
    "WHERE username = '" + username + "'"
)
```

এটা unsafe pattern।

কারণ user input SQL syntax-এর অংশ হয়ে যেতে পারে।

---

# 2️⃣0️⃣ কেন Dangerous?

Database query হওয়া উচিত:

```text
SQL structure
      +
User data
```

কিন্তু unsafe concatenation করলে:

```text
SQL structure
      +
User input treated as SQL
```

হয়ে যেতে পারে।

---

# 2️⃣1️⃣ SQL Injection Prevention ⭐⭐⭐

সবচেয়ে গুরুত্বপূর্ণ:

> **Parameterized Queries / Prepared Statements ব্যবহার করো।**

Concept:

```text
SQL structure
      ↓
Parameter
      ↓
User input treated as data
```

---

# 2️⃣2️⃣ Django কি SQL Injection থেকে Safe?

Django ORM সাধারণত parameterized queries ব্যবহার করে।

Example:

```python
User.objects.filter(
    username=username
)
```

এটা raw string concatenation-এর চেয়ে নিরাপদ।

---

# 2️⃣3️⃣ Dangerous Django Pattern

❌ Avoid:

```python
query = f"""
    SELECT *
    FROM users
    WHERE username = '{username}'
"""
```

এখানে user input directly SQL string-এর মধ্যে ঢুকছে।

---

# 2️⃣4️⃣ Django Raw SQL

Raw SQL দরকার হলে parameterized form ব্যবহার করো।

```python
from django.db import connection

with connection.cursor() as cursor:
    cursor.execute(
        "SELECT * FROM users WHERE username = %s",
        [username]
    )
```

এখানে:

```text
SQL structure → fixed
username → parameter
```

---

# 2️⃣5️⃣ Django ORM — Preferred

যেখানে সম্ভব:

```python
User.objects.filter(
    email=email
)
```

অথবা:

```python
Booking.objects.filter(
    room_id=room_id,
    status="CONFIRMED"
)
```

ORM ব্যবহার করলে query construction safer এবং maintainable হয়।

তবে ORM ব্যবহার করলেই application-এর সব security problem magically চলে যায় না।

---

# 2️⃣6️⃣ Input Validation ⭐

User input validate করা উচিত।

যেমন:

```text
Email
Phone
Date
Quantity
ID
```

কিন্তু মনে রাখবে:

> **Validation alone SQL Injection prevention-এর replacement নয়।**

Primary defense:

```text
Parameterized query
```

---

# 2️⃣7️⃣ Sensitive Data কী?

Database-এ কিছু data বিশেষভাবে protect করতে হয়।

যেমন:

```text
Passwords
API secrets
Authentication tokens
Personal information
Payment-related sensitive data
Private business information
```

---

# 2️⃣8️⃣ Password কখনো Plain Text রাখবে না ❌

Bad:

```text
users

username | password
-------------------
rahim    | 123456
```

যদি database leak হয়:

```text
Attacker
 ↓
Password directly visible
```

---

# 2️⃣9️⃣ Password Hashing ⭐⭐⭐

Password-এর জন্য **secure password hashing algorithm** ব্যবহার করতে হয়।

Concept:

```text
Password
   ↓
Password Hashing
   ↓
Hash
   ↓
Database
```

Login:

```text
Entered Password
      ↓
Verify against stored hash
      ↓
Match?
```

Django-এর built-in password hashing system ব্যবহার করা উচিত।

---

# 3️⃣0️⃣ Hashing vs Encryption

এটা important।

### Hashing

সাধারণভাবে one-way transformation।

```text
Password
   ↓
Hash
```

মূল password থেকে hash তৈরি হয় এবং verification করা হয়।

### Encryption

Data encrypt করা হয়:

```text
Plaintext
   ↓
Encryption + Key
   ↓
Ciphertext
```

Appropriate key থাকলে decrypt করা যায়।

সহজে:

```text
Password → Hash

Recoverable sensitive data → Encryption may be appropriate
```

---

# 3️⃣1️⃣ Encryption at Rest

Database/storage-এর data disk-এ encrypted রাখা।

```text
Database
   ↓
Encrypted Storage
```

যদি storage বা disk improperly accessed হয়, plaintext data exposure কমাতে সাহায্য করতে পারে।

---

# 3️⃣2️⃣ Encryption in Transit ⭐

Application → Database connection-ও secure হওয়া উচিত।

```text
Django
   │
   │ TLS/SSL
   ↓
Database
```

এতে network-এর মাধ্যমে transmitted data protect করা যায়।

---

# 3️⃣3️⃣ Database Credentials কোথায় রাখবে? ⭐⭐⭐

❌ Bad:

```python
DATABASES = {
    "PASSWORD": "my_super_secret_password"
}
```

Source code-এ secret commit করলে repository leak হলে credential exposed হতে পারে।

---

# 3️⃣4️⃣ Environment Variables

Better:

```python
import os

DATABASE_PASSWORD = os.environ["DB_PASSWORD"]
```

Environment:

```text
DB_PASSWORD=********
```

Production-এ আরও ভালোভাবে dedicated **secret manager** ব্যবহার করা যেতে পারে।

---

# 3️⃣5️⃣ `.env` File

Development-এ:

```text
.env
```

এ রাখা হতে পারে:

```text
DB_NAME=hotel_db
DB_USER=app_user
DB_PASSWORD=secret
```

এবং:

```text
.env
```

কে Git repository-তে commit করা যাবে না।

`.gitignore`-এ:

```text
.env
```

রাখা উচিত।

---

# 3️⃣6️⃣ Production Secret Management

Production environment-এ:

```text
Django
   ↓
Secret Manager
   ↓
DB credentials
```

Cloud/platform অনুযায়ী managed secret storage ব্যবহার করা যায়।

মূল principle:

> **Secrets source code-এর মধ্যে hard-code করো না।**

---

# 3️⃣7️⃣ Database Network Security

Database ideally public internet-এর জন্য unnecessarily exposed থাকা উচিত নয়।

Bad architecture:

```text
Internet
   ↓
Database
```

Better:

```text
Internet
   ↓
Django/API
   ↓
Private Network
   ↓
Database
```

---

# 3️⃣8️⃣ Firewall

Database server-এর access সীমিত করা যায়:

```text
Allowed:
Django Server → Database

Blocked:
Random Internet → Database
```

Database port publicly open রাখার প্রয়োজন আছে কি না carefully evaluate করতে হবে।

---

# 3️⃣9️⃣ Database Access Layers

Production architecture:

```text
User
 ↓
Frontend
 ↓
API
 ↓
Django
 ↓
Database User
 ↓
Database
```

User ideally সরাসরি database-এ connect করবে না।

---

# 4️⃣0️⃣ Application vs Database Authorization

ধরো:

```text
Customer
Receptionist
Admin
```

Django application-level authorization:

```text
Customer
 → own booking

Receptionist
 → booking management

Admin
 → system management
```

এটা application layer-এর authorization।

Database permissions:

```text
app_user
report_user
admin_user
```

এগুলো database-level access control।

### দুই layer-ই useful।

---

# 4️⃣1️⃣ Defense in Depth ⭐⭐⭐

Security-এর একটি গুরুত্বপূর্ণ principle:

> **একটি security control-এর উপর depend না করে multiple security layers ব্যবহার করা।**

Architecture:

```text
Authentication
      ↓
Authorization
      ↓
Input Validation
      ↓
Parameterized Queries
      ↓
Database Permissions
      ↓
Network Security
      ↓
Encryption
      ↓
Monitoring
      ↓
Backup
```

---

# 4️⃣2️⃣ Django Security Settings

Production Django application-এ security-related settings carefully configure করতে হয়।

যেমন:

```python
DEBUG = False
```

Production-এ:

```python
ALLOWED_HOSTS = [
    "example.com"
]
```

আর HTTPS ব্যবহার করলে secure cookie settings-এর মতো configuration বিবেচনা করতে হয়।

---

# 4️⃣3️⃣ Django Authentication

Django authentication system ব্যবহার করলে password hashing, sessions ইত্যাদি অনেক security mechanism framework-level support পায়।

Custom authentication বানালেও security principles maintain করতে হবে।

বিশেষ করে:

```text
Password hashing
Session/token security
Authorization
CSRF protection where applicable
HTTPS
```

---

# 4️⃣4️⃣ SQL Injection ছাড়াও কী কী Risk আছে?

Database security শুধু SQL Injection না।

আরও আছে:

```text
Broken access control
Weak passwords
Credential leakage
Excessive database privileges
Unencrypted connections
Public database exposure
Sensitive data leakage
Poor backup security
Insufficient logging
Insecure raw SQL
```

---

# 4️⃣5️⃣ Audit Logging ⭐⭐⭐

Important database actions track করা যায়:

```text
Who?
What?
When?
```

Example:

```text
user_id = 25
action = UPDATE_BOOKING
booking_id = 101
time = 10:30
```

এতে suspicious activity investigate করা সহজ হয়।

---

# 4️⃣6️⃣ Audit Log Example

```sql
CREATE TABLE audit_logs (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    user_id BIGINT,
    action VARCHAR(100),
    table_name VARCHAR(100),
    record_id BIGINT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Example:

```text
25 | UPDATE_BOOKING | bookings | 101
```

---

# 4️⃣7️⃣ Sensitive Payment Data

একটা important rule:

> Application database-এ unnecessary raw payment-card data store করা উচিত নয়।

বিশেষ করে:

```text
CVV
Full card details
```

নিজের database-এ casually store করা উচিত নয়।

Payment provider-এর secure tokenization/payment system ব্যবহার করা সাধারণ production approach।

---

# 4️⃣8️⃣ Data Minimization ⭐

যে data দরকার নেই:

```text
Don't collect
```

যে data দরকার:

```text
Collect minimum necessary
```

কারণ:

```text
Less sensitive data
       ↓
Less exposure risk
```

---

# 4️⃣9️⃣ Production Database Security Architecture ⭐⭐⭐

একটি secure architecture:

```text
                 Internet
                    ↓
              Load Balancer
                    ↓
               Django API
                    ↓
          Authentication/Authorization
                    ↓
             Application DB User
                    ↓
             Private DB Network
                    ↓
             Primary Database
                    ↓
              Read Replica
                    ↓
               Encrypted Backup
```

এখানে:

```text
Authentication
Authorization
Least Privilege
TLS
Private Network
Parameterized Queries
Encryption
Backup
Monitoring
```

সব একসাথে কাজ করছে।

---

# 5️⃣0️⃣ Hotel System Security Design ⭐⭐⭐

আমাদের hotel project-এ:

```text
Customer
Receptionist
Manager
Admin
```

Application-level:

```text
Customer
 ↓
Own bookings

Receptionist
 ↓
Booking management

Manager
 ↓
Reports

Admin
 ↓
System administration
```

Database-level:

```text
Django app
 ↓
app_user
```

এবং reporting:

```text
Reporting service
 ↓
report_user
 ↓
SELECT only
```

---

# 5️⃣1️⃣ Hotel Payment Security

Database:

```text
payments
----------------
payment_id
booking_id
amount
payment_method
status
```

Store করা যেতে পারে:

```text
amount
payment_method
transaction/reference ID
status
```

কিন্তু unnecessary sensitive payment credentials/card security data নিজের DB-তে রাখবে না।

---

# 5️⃣2️⃣ Database Security Checklist ⭐⭐⭐

Production database deploy করার আগে:

```text
☑ Strong authentication
☑ Least privilege
☑ Separate DB users
☑ No root for application
☑ Parameterized queries
☑ Django ORM where appropriate
☑ DEBUG=False
☑ HTTPS/TLS
☑ Private DB network
☑ Secrets outside source code
☑ Password hashing
☑ Sensitive data protection
☑ Audit logging
☑ Monitoring
☑ Secure backups
☑ Tested restore procedure
```

---

# 5️⃣3️⃣ Most Common Mistakes ❌

### Mistake 1

```text
Django → root DB user
```

❌

---

### Mistake 2

```python
query = f"SELECT ... '{user_input}'"
```

❌

---

### Mistake 3

Source code:

```text
DB_PASSWORD=123456
```

❌

---

### Mistake 4

সব user-কে:

```text
Admin
```

করে দেওয়া।

❌

---

### Mistake 5

Password:

```text
123456
```

plain text database-এ রাখা।

❌

---

### Mistake 6

Database:

```text
0.0.0.0/0
```

থেকে publicly accessible করে রাখা।

❌

---

### Mistake 7

Replica আছে বলে backup বন্ধ করা।

❌

---

# 5️⃣4️⃣ Security Architecture Mindset

Database designer হিসেবে এখন তোমার চিন্তা হবে:

```text
Who can access?
       ↓
What can they access?
       ↓
What can they modify?
       ↓
What if credentials leak?
       ↓
What if application is hacked?
       ↓
What if data is deleted?
       ↓
Can we detect it?
       ↓
Can we recover?
```

এটাই production security mindset।

---

# 🧠 Class 66 Golden Rules ⭐⭐⭐⭐⭐

```text
1. Authentication → Who are you?

2. Authorization → What can you do?

3. User → Database identity

4. Role → Collection of permissions

5. GRANT → Give permission

6. REVOKE → Remove permission

7. Least Privilege → Minimum required permission

8. Application should not use DB root/admin unnecessarily

9. SQL Injection → Untrusted input changes SQL meaning

10. Parameterized Query → Primary SQL injection defense

11. Django ORM → Generally uses parameterized queries

12. Password → Never store plain text

13. Password → Use secure password hashing

14. Hashing ≠ Encryption

15. TLS → Protect data in transit

16. Encryption at rest → Protect stored data

17. Secrets → Never hard-code in source code

18. Database → Prefer private network

19. Audit Log → Who + What + When

20. Data Minimization → Don't store unnecessary sensitive data

21. Replication ≠ Backup

22. Defense in Depth → Multiple security layers

23. Database security ≠ Only SQL Injection

24. Application Authorization + Database Permissions
    should work together

25. Production DB → Security + Monitoring + Backup + Recovery
```

---

# 📝 Class 66 Assignment

## Task 1 — Authentication vs Authorization

Explain:

```text
Authentication
Authorization
```

একটা hotel example দাও।

---

## Task 2 — GRANT / REVOKE

`report_user`-কে শুধু:

```text
hotel_db
```

এর `bookings` table-এ `SELECT` permission দেওয়ার SQL লেখো।

তারপর permission remove করার SQL লেখো।

---

## Task 3 — Least Privilege ⭐

একটি Django application-এর জন্য নিচের permissions:

```text
SELECT
INSERT
UPDATE
DELETE
DROP
ALTER
```

এর মধ্যে কোনগুলো প্রয়োজন হতে পারে এবং কোনগুলো unnecessarily dangerous?

**Reason করো—সব application-এর একই permission set হয় না।**

---

## Task 4 — SQL Injection ⭐⭐⭐

এই code-এর security problem identify করো:

```python
query = f"""
SELECT *
FROM customers
WHERE email = '{email}'
"""
```

তারপর Django-তে safer approach লেখো।

---

## Task 5 — Password

Explain:

```text
Password
   ↓
Hash
   ↓
Database
```

এবং:

**Hashing আর Encryption-এর মধ্যে difference কী?**

---

## Task 6 — Production Security ⭐⭐⭐

এই architecture-কে secure করো:

```text
Internet
   ↓
Django
   ↓
Database
```

কমপক্ষে **8টি security improvement** লিখো।

---

# 🔥 Interview Challenge

Interviewer জিজ্ঞেস করল:

> **"How would you secure a production Django application database?"**

একটা strong answer:

```text
1. Use a dedicated application DB user
2. Apply least privilege
3. Never use root unnecessarily
4. Use Django ORM / parameterized queries
5. Prevent SQL injection
6. Hash passwords securely
7. Keep DB credentials out of source code
8. Use environment/secret management
9. Use TLS for DB connections where appropriate
10. Keep database on a private network
11. Protect sensitive data
12. Enable audit/monitoring
13. Maintain secure backups
14. Test restoration
15. Control application-level authorization
```

---

# 🏆 এখন পর্যন্ত Database Engineering Journey

তুমি এখন এই level পর্যন্ত এসেছ:

```text
Class 31
SQL Fundamentals
      ↓
32–40
Advanced SQL
      ↓
41–46
SQL Analytics + Views
      ↓
47–49
Procedures + Transactions + Triggers
      ↓
50–51
Indexing + Query Optimization
      ↓
52–53
Normalization + Database Design
      ↓
54
Data Warehouse
      ↓
55–57
Interview + Full Database Projects
      ↓
58–63
Concurrency + Locking + Deadlock
      ↓
64
Partitioning
      ↓
65
Replication + High Availability
      ↓
66
Security + Access Control
```

### 🎯 Database Designer হিসেবে এখন তোমার core stack:

```text
SQL
+
Database Design
+
Normalization
+
ERD
+
Indexing
+
Query Optimization
+
Transactions
+
Concurrency
+
Partitioning
+
Replication
+
Security
```

এখন তুমি শুধু **SQL query writer** level-এ নেই; আমরা ধীরে ধীরে **Database Engineer / Database Designer mindset**-এর দিকে যাচ্ছি।

**Next → Class 67: Database Backup, Recovery & Disaster Recovery** — সেখানে আমরা শিখব **Full/Incremental/Differential Backup, Point-in-Time Recovery (PITR), RPO/RTO practical design, Restore, Disaster Recovery, Backup strategy এবং production database recovery architecture**।

---
# 📚 Class 67 — Database Backup, Recovery & Disaster Recovery

আজকের class-এ আমরা **Database Reliability-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি** শিখব।

আগের classes-এ:

- Class 58–63 → Transaction, Concurrency, Locking, Deadlock
    
- Class 64 → Partitioning
    
- Class 65 → Replication & High Availability
    
- Class 66 → Database Security
    

আজ:

> **Database নষ্ট/ডিলিট/corrupt হলে কীভাবে data recover করব?**

আমরা শিখব:

```text
1. Full Backup
2. Incremental Backup
3. Differential Backup
4. Restore
5. Point-in-Time Recovery (PITR)
6. RPO
7. RTO
8. Disaster Recovery
9. Backup Strategy
10. Production Recovery Architecture
```

---

# 1️⃣ Backup কী?

সহজ ভাষায়:

> **Database-এর data-এর একটি recoverable copy নিরাপদ জায়গায় সংরক্ষণ করাই Backup।**

ধরো:

```text
Production Database
       │
       ↓
     Backup
       │
       ↓
Backup Storage
```

যদি database নষ্ট হয়:

```text
Database ❌
   │
   ↓
Restore
   │
   ↓
Backup
   │
   ↓
Recovered Database
```

---

# 2️⃣ কেন Backup প্রয়োজন?

Production database-এ অনেক ধরনের সমস্যা হতে পারে:

```text
❌ Accidental DELETE
❌ Accidental UPDATE
❌ Application bug
❌ Database corruption
❌ Disk failure
❌ Server failure
❌ Ransomware
❌ Human error
❌ Cloud/Infrastructure failure
❌ Natural disaster
```

Example:

```sql
DELETE FROM bookings;
```

ভুল করে execute হলো।

শুধু replication থাকলে:

```text
Primary
   │
   ↓
DELETE
   │
   ↓
Replica
```

Replica-তেও সেই change replicate হতে পারে।

কিন্তু backup থাকলে:

```text
Backup
   ↓
Restore
   ↓
Recover
```

---

# 3️⃣ Backup বনাম Replication ⭐⭐⭐

এটা খুব ভালোভাবে বুঝতে হবে।

|Backup|Replication|
|---|---|
|Recovery-এর জন্য|Availability/read scaling-এর জন্য|
|Historical copy রাখা যায়|সাধারণত current state replicate করে|
|Accidental deletion recover করতে useful|Delete replicate হতে পারে|
|Restore করা যায়|Failover/read-এর জন্য useful|
|Long-term retention করা যায়|Continuous copy|
|Disaster Recovery-এর গুরুত্বপূর্ণ অংশ|HA-এর গুরুত্বপূর্ণ অংশ|

### Golden Rule

> **Replication ≠ Backup**

---

# 4️⃣ Full Backup ⭐⭐⭐

Full Backup মানে:

> **পুরো database-এর backup নেওয়া।**

ধরো:

```text
Database:

A
B
C
D
E
```

Full backup:

```text
Backup
 ↓
A B C D E
```

---

# 5️⃣ Full Backup Example

ধরো Sunday:

```text
Sunday
↓
Full Backup
↓
A B C D E
```

Monday-তে নতুন data এসেছে:

```text
F G
```

পরের full backup:

```text
Monday
↓
Full Backup
↓
A B C D E F G
```

অর্থাৎ প্রত্যেক full backup পুরো database capture করে।

---

# 6️⃣ Full Backup-এর সুবিধা/অসুবিধা

### সুবিধা

```text
✅ Restore সহজ
✅ Backup chain কম
✅ Recovery straightforward
```

### অসুবিধা

```text
❌ Storage বেশি লাগে
❌ Large DB হলে backup নিতে বেশি সময় লাগে
❌ Network bandwidth বেশি লাগতে পারে
```

---

# 7️⃣ Incremental Backup ⭐⭐⭐

Incremental Backup:

> **শেষ backup-এর পর যে data পরিবর্তিত হয়েছে, শুধু সেটার backup।**

ধরো:

```text
Sunday
Full → A B C
```

Monday:

```text
New → D E
Incremental → D E
```

Tuesday:

```text
New → F
Incremental → F
```

Wednesday:

```text
New → G H
Incremental → G H
```

Architecture:

```text
Sunday
Full
 A B C
  │
  ├── Monday → D E
  │
  ├── Tuesday → F
  │
  └── Wednesday → G H
```

---

# 8️⃣ Incremental Restore

Wednesday পর্যন্ত recover করতে হলে:

```text
Full Backup
     ↓
Monday Incremental
     ↓
Tuesday Incremental
     ↓
Wednesday Incremental
```

সব relevant backup chain ঠিকভাবে apply করতে হবে।

তাই:

```text
Backup size ↓
Restore complexity ↑
```

---

# 9️⃣ Differential Backup ⭐⭐⭐

Differential Backup:

> **শেষ Full Backup-এর পর থেকে যত changes হয়েছে, সেগুলোর backup।**

ধরো:

### Sunday

```text
Full
A B C
```

### Monday

নতুন:

```text
D E
```

Differential:

```text
D E
```

### Tuesday

নতুন:

```text
F
```

Tuesday differential:

```text
D E F
```

### Wednesday

নতুন:

```text
G
```

Wednesday differential:

```text
D E F G
```

---

# 🔟 Incremental বনাম Differential

ধরো:

```text
Sunday = Full
Monday = 10 GB changes
Tuesday = 5 GB changes
Wednesday = 8 GB changes
```

### Incremental

```text
Monday    → 10 GB
Tuesday   → 5 GB
Wednesday → 8 GB
```

### Differential

```text
Monday    → 10 GB
Tuesday   → 15 GB
Wednesday → 23 GB
```

কারণ differential প্রতিবার **শেষ Full Backup থেকে** হিসাব করে।

---

# 1️⃣1️⃣ Final Comparison ⭐⭐⭐⭐⭐

|বিষয়|Full|Incremental|Differential|
|---|---|---|---|
|কী backup করে|সব|Last backup-এর পর changes|Last full-এর পর changes|
|Backup size|বড়|ছোট|মাঝারি/ধীরে বড়|
|Backup speed|ধীর|দ্রুত|মাঝারি|
|Restore|সহজ|বেশি steps|তুলনামূলক সহজ|
|Storage|বেশি|কম|মাঝারি|
|Restore chain|কম|বেশি|কম|

### মনে রাখো:

```text
Incremental
→ Since LAST BACKUP

Differential
→ Since LAST FULL BACKUP
```

---

# 1️⃣2️⃣ Restore কী?

Backup নেওয়া হলো:

```text
Database
   ↓
Backup
```

এখন backup থেকে database পুনরায় তৈরি করা:

```text
Backup
   ↓
Restore
   ↓
Database
```

এটাই Restore।

---

# 1️⃣3️⃣ Backup আছে মানেই Recovery নিশ্চিত? ❌

না।

এটা production-এর খুব common mistake।

ধরো:

```text
Backup: SUCCESS ✅
```

কিন্তু disaster-এর সময়:

```text
Restore ❌
Backup corrupted ❌
Wrong credentials ❌
Missing backup files ❌
Incomplete backup ❌
```

তাই:

> **Backup success ≠ Recovery success**

---

# 1️⃣4️⃣ Restore Testing ⭐⭐⭐⭐⭐

Regularly test করতে হবে:

```text
Backup
   ↓
Restore
   ↓
Database starts?
   ↓
Data correct?
   ↓
Application works?
```

এটাকে বলা যায়:

> **Recovery Drill / Restore Test**

Production database-এর জন্য এটি অত্যন্ত গুরুত্বপূর্ণ।

---

# 1️⃣5️⃣ Point-in-Time Recovery — PITR ⭐⭐⭐⭐⭐

এখন সবচেয়ে গুরুত্বপূর্ণ topic।

PITR মানে:

> **Database-কে একটি নির্দিষ্ট সময়ের অবস্থায় recover করার capability।**

ধরো:

```text
10:00 → Normal
10:30 → Booking created
10:40 → Payment created
10:45 → Application bug
10:46 → Important records deleted ❌
```

আমরা চাই:

```text
10:45:59
```

অর্থাৎ deletion-এর ঠিক আগের state।

এটাই:

# Point-in-Time Recovery

---

# 1️⃣6️⃣ PITR-এর Basic Architecture

Conceptually:

```text
Full/Base Backup
       +
Transaction Logs
       ↓
Recovery
       ↓
Desired Time
```

Database system অনুযায়ী log mechanism আলাদা হতে পারে।

### PostgreSQL

```text
Base Backup
+
WAL
```

### MySQL

```text
Full Backup
+
Binary Log
```

---

# 1️⃣7️⃣ PITR Example 🔥

ধরো:

```text
02:00 → Full Backup
```

এরপর:

```text
02:10 → Booking 101
02:20 → Booking 102
02:30 → Payment 201
02:40 → Booking 103
02:45 → ❌ Accidental DELETE
```

আমরা recover করতে চাই:

```text
02:44:59
```

Recovery concept:

```text
02:00 Full Backup
       │
       +
02:00 → 02:44:59 Logs
       │
       ↓
Database at 02:44:59
```

---

# 1️⃣8️⃣ PITR কেন গুরুত্বপূর্ণ?

শুধু daily backup থাকলে:

```text
Monday 02:00
       ↓
Tuesday 02:00
```

এর মধ্যে disaster হলে অনেক hours-এর data loss হতে পারে।

PITR ব্যবহার করলে:

```text
Full Backup
+
Continuous Log Information
```

থেকে much finer recovery point পাওয়া সম্ভব।

---

# 1️⃣9️⃣ RPO — Recovery Point Objective ⭐⭐⭐

RPO প্রশ্ন করে:

> **Disaster হলে maximum কত data loss acceptable?**

ধরো:

```text
RPO = 15 minutes
```

এর অর্থ business-এর recovery target হলো approximately:

```text
Maximum acceptable data loss ≈ 15 minutes
```

এটি architecture-এর achievable target; exact result backup/logging design-এর উপর নির্ভর করে।

---

# 2️⃣0️⃣ RTO — Recovery Time Objective ⭐⭐⭐

RTO প্রশ্ন করে:

> **Disaster হওয়ার পর কত সময়ের মধ্যে system আবার চালু করতে হবে?**

ধরো:

```text
RTO = 1 hour
```

মানে target:

```text
Failure
  ↓
Recovery
  ↓
Service restored within ~1 hour
```

---

# 2️⃣1️⃣ RPO vs RTO ⭐⭐⭐⭐⭐

এটা interview-এ খুব common।

```text
RPO → DATA LOSS
RTO → DOWNTIME
```

আরও সহজ:

> **RPO = How much data can we lose?**

> **RTO = How long can we be down?**

---

# 2️⃣2️⃣ Practical Example

আমাদের hotel application:

```text
RPO = 15 minutes
RTO = 1 hour
```

এর অর্থ:

```text
Data loss target
→ ~15 minutes-এর বেশি না

Downtime target
→ ~1 hour-এর মধ্যে recovery
```

এখন daily backup যথেষ্ট হবে?

**না**, কারণ daily backup দিয়ে 15-minute RPO reliably meet করা কঠিন।

তাই architecture-এ frequent backups এবং/or transaction-log based recovery দরকার হতে পারে।

---

# 2️⃣3️⃣ RPO/RTO Business অনুযায়ী

সব application-এর requirement এক নয়।

### Personal Blog

```text
RPO = 24 hours
RTO = 24 hours
```

হতে পারে acceptable।

### E-commerce

```text
RPO → Low
RTO → Low
```

### Banking / Critical System

```text
RPO → Very Low
RTO → Very Low
```

ফলে:

```text
Business Criticality ↑
        ↓
Recovery Requirement ↑
        ↓
Infrastructure Complexity ↑
```

---

# 2️⃣4️⃣ Disaster Recovery — DR ⭐⭐⭐⭐⭐

Disaster Recovery হলো:

> **Major failure/disaster-এর পর system, database এবং services recover করার পরিকল্পনা ও architecture।**

Disaster হতে পারে:

```text
Database failure
Server failure
Disk failure
Datacenter failure
Cloud outage
Cyber incident
Human error
Natural disaster
```

---

# 2️⃣5️⃣ Backup বনাম Disaster Recovery

```text
Backup
→ Data copy

Disaster Recovery
→ Complete recovery strategy
```

DR-এর মধ্যে থাকতে পারে:

```text
Backup
+
Restore
+
Replication
+
Failover
+
Standby infrastructure
+
Monitoring
+
Recovery procedures
```

---

# 2️⃣6️⃣ Backup কোথায় রাখবে? ❌

Bad architecture:

```text
Server
 ├── Production DB
 └── Backup
```

Server নষ্ট হলে:

```text
Database ❌
Backup ❌
```

তাই backup আলাদা infrastructure/storage-এ রাখা উচিত।

---

# 2️⃣7️⃣ Better Architecture

```text
Production DB
      │
      ↓
Backup System
      │
      ↓
Separate Storage
```

আরও resilient:

```text
Production Region
       │
       ↓
Backup
       │
       ↓
Different Storage / Region
```

---

# 2️⃣8️⃣ 3-2-1 Backup Rule ⭐⭐⭐

Classic backup principle:

```text
3 copies
2 different storage/media
1 offsite copy
```

Example:

```text
Original Database
       +
Backup Storage 1
       +
Offsite Backup Storage 2
```

বাস্তব environment-এ business requirement অনুযায়ী policy পরিবর্তিত হতে পারে।

---

# 2️⃣9️⃣ Immutable Backup ⭐⭐⭐

Immutable backup হলো এমন backup যা নির্দিষ্ট retention period-এর মধ্যে সহজে পরিবর্তন/মুছে ফেলা যায় না।

Architecture:

```text
Production DB
      ↓
Backup
      ↓
Immutable Storage
```

এটি ransomware বা malicious deletion-এর বিরুদ্ধে useful protection দিতে পারে।

---

# 3️⃣0️⃣ Backup Encryption

Backup-এর মধ্যেও sensitive information থাকতে পারে।

তাই:

```text
Production Data
      ↓
Encrypted Backup
      ↓
Secure Storage
```

এখানে encryption key management-ও অত্যন্ত গুরুত্বপূর্ণ।

---

# 3️⃣1️⃣ Backup Retention

সব backup চিরকাল রাখতে হয় না।

Example policy:

```text
Daily   → 30 days
Weekly  → 3 months
Monthly → 1 year
```

এগুলো শুধু example।

Actual retention নির্ভর করবে:

```text
Business
Legal requirements
Compliance
Storage cost
Recovery needs
```

---

# 3️⃣2️⃣ Production Backup Strategy ⭐⭐⭐⭐⭐

একটি practical design:

```text
                  Production DB
                       │
             ┌─────────┴─────────┐
             ↓                   ↓
          Replica          Backup System
                                 │
                       ┌─────────┴─────────┐
                       ↓                   ↓
                   Full Backup       Incremental/
                                      Log Backup
                       │
                       ↓
                Secure Storage
                       │
                       ↓
                  Offsite Copy
```

---

# 3️⃣3️⃣ Hotel Management System Example 🔥

আমাদের database:

```text
customers
rooms
room_types
bookings
payments
```

ধরো:

```text
02:00 → Full Backup
```

তারপর:

```text
02:10 → Booking 101
02:20 → Payment 201
02:30 → Booking 102
02:40 → Payment 202
02:45 → Application bug
```

আমরা চাই:

```text
02:44:59
```

তাহলে conceptually:

```text
Full Backup
     +
WAL/Binlog
     ↓
PITR
     ↓
02:44:59
```

---

# 3️⃣4️⃣ Complete Disaster Scenario

ধরো:

```text
Primary DB Server ❌
```

Recovery process:

```text
Detect Failure
      ↓
Assess Incident
      ↓
Choose Recovery Target
      ↓
Provision/Prepare DB
      ↓
Restore Full Backup
      ↓
Apply Incremental/Logs
      ↓
Verify Data
      ↓
Reconnect Application
      ↓
Monitor System
```

---

# 3️⃣5️⃣ Recovery Verification

Database restore করার পর শুধু:

```text
Database started ✅
```

বললেই হবে না।

Check করতে হবে:

```text
✅ Database connection
✅ Tables
✅ Row counts
✅ Indexes
✅ Constraints
✅ Recent transactions
✅ Application login
✅ Critical API
✅ Booking creation
✅ Payment history
```

Hotel application-এ:

```text
Can customer create booking?
Can receptionist view booking?
Can room availability work?
Can payment history load?
```

---

# 3️⃣6️⃣ Recovery Drill ⭐⭐⭐⭐⭐

Production team periodically simulate করে:

```text
"Primary database is unavailable."
```

তারপর:

```text
Backup
 ↓
Restore
 ↓
Recovery
 ↓
Application Test
 ↓
Measure Time
```

এতে বোঝা যায়:

> **আমাদের stated RTO সত্যিই achievable কিনা।**

---

# 3️⃣7️⃣ Replication + Backup + DR

Class 65-এর replication-এর সঙ্গে আজকের backup combine করি:

```text
                       Application
                            │
                            ↓
                         Primary
                        /       \
                       ↓         ↓
                  Replica 1   Replica 2
                                   │
                                   ↓
                                Backup
                                   │
                                   ↓
                            Secure Storage
                                   │
                                   ↓
                               DR Site
```

এখানে:

```text
Replica
→ Availability / Read Scaling

Backup
→ Recovery

DR
→ Major Disaster Recovery
```

---

# 3️⃣8️⃣ Production Database Recovery Architecture ⭐⭐⭐⭐⭐

একটি mature architecture:

```text
                    Users
                      │
                      ↓
               Django Application
                      │
                      ↓
                 Primary DB
                  /       \
                 /         \
                ↓           ↓
          Read Replica   Backup System
                              │
                         WAL/Binlog
                              │
                 ┌────────────┴────────────┐
                 ↓                         ↓
          Backup Storage             Offsite Storage
                                           │
                                           ↓
                                        DR Site
```

---

# 3️⃣9️⃣ Recovery Strategy Design

Database designer হিসেবে শুধু:

> "Backup নেব"

বললে হবে না।

এই প্রশ্নগুলো করতে হবে:

```text
1. Database কত বড়?
2. প্রতিদিন কত data change হয়?
3. RPO কত?
4. RTO কত?
5. Backup কতদিন রাখতে হবে?
6. Backup কোথায় রাখা হবে?
7. Offsite copy দরকার?
8. PITR দরকার?
9. Encryption দরকার?
10. Immutable backup দরকার?
11. Restore কত দ্রুত করতে হবে?
12. Restore test কত ঘন ঘন হবে?
13. Disaster হলে কে recovery করবে?
```

---

# 4️⃣0️⃣ Small Project বনাম Production

### Small Django Project

```text
Daily Backup
+
Separate Storage
+
Periodic Restore Test
```

অনেক ক্ষেত্রে যথেষ্ট হতে পারে।

### Production System

```text
Full Backup
+
Incremental / Log Backup
+
PITR
+
Offsite Backup
+
Encryption
+
Retention
+
Monitoring
+
Restore Testing
+
DR Plan
+
RPO/RTO
```

---

# 🧠 Class 67 Golden Rules ⭐⭐⭐⭐⭐

```text
FULL
→ Entire database

INCREMENTAL
→ Changes since last backup

DIFFERENTIAL
→ Changes since last full backup

RESTORE
→ Backup থেকে database পুনরায় তৈরি

PITR
→ Specific point in time-এ recovery

RPO
→ Acceptable data loss

RTO
→ Acceptable downtime

Replication
→ Availability / Read Scaling

Backup
→ Recovery

DR
→ Complete recovery strategy

Replication ≠ Backup

Backup ≠ Disaster Recovery

Backup success ≠ Recovery success

Backup should be stored separately

Offsite backup → Major infrastructure failure protection

Immutable backup → Tampering/deletion protection

Encryption → Protect backup data

Retention → কতদিন backup রাখা হবে

Restore Test → Backup সত্যিই recoverable কিনা যাচাই

Recovery Drill → পুরো recovery process practice

RPO/RTO → Backup architecture design-এর key requirements
```

---

# 📝 Class 67 Assignment

### Task 1

ধরো:

```text
Sunday → Full Backup
Monday → 10 GB changes
Tuesday → 5 GB changes
Wednesday → 8 GB changes
```

বল:

**Incremental backup-এ প্রতিদিন কত GB backup হবে?**

এবং:

**Differential backup-এ প্রতিদিন কত GB backup হবে?**

---

### Task 2 — RPO/RTO

একটি hotel application:

```text
RPO = 15 minutes
RTO = 1 hour
```

Explain:

1. RPO 15 minutes কী?
    
2. RTO 1 hour কী?
    
3. Daily-only backup কেন এই requirement-এর জন্য যথেষ্ট নাও হতে পারে?
    

---

### Task 3 — PITR 🔥

Timeline:

```text
01:00 → Full Backup
01:10 → Booking created
01:20 → Payment created
01:30 → Booking created
01:40 → Payment created
01:45 → Important data accidentally deleted
```

Question:

> **01:44:59 পর্যন্ত database recover করতে কীভাবে PITR ব্যবহার করবে?**

---

### Task 4 — Replication

Explain:

> Primary database থেকে Replica-তে accidental DELETE replicate হয়ে গেলে কেন Replica-কে backup বলা যাবে না?

---

### Task 5 — Production Architecture ⭐⭐⭐⭐⭐

Complete করো:

```text
Django
   ↓
Primary DB
   ↓
Replica
   ↓
?
   ↓
?
   ↓
Offsite / DR
```

প্রতিটি component-এর কাজ লিখবে।

---

# 🔥 Interview Challenge

Interviewer:

> **"Your production database was accidentally modified at 2:45 PM. The last full backup was at 2:00 AM. How would you recover the database to 2:44 PM?"**

Strong answer:

```text
02:00 AM Full Backup
        ↓
WAL / Binary Logs
        ↓
Replay changes
        ↓
Stop at desired recovery time
        ↓
02:44 PM state
        ↓
Verify data
        ↓
Make recovered DB available
        ↓
Reconnect application
```

তারপর interviewer জিজ্ঞেস করলে:

> **"How do you know your backup strategy actually works?"**

Answer:

```text
Regular restore testing
+
Recovery drills
+
Backup monitoring
+
Documented recovery procedure
+
Measured RPO/RTO
```

---

# 🏆 এখন পর্যন্ত Database Engineering Journey

```text
SQL
 ↓
Advanced SQL
 ↓
Database Design
 ↓
Normalization
 ↓
ERD
 ↓
Indexing
 ↓
Query Optimization
 ↓
Transactions
 ↓
Concurrency
 ↓
Locking
 ↓
Deadlock
 ↓
Partitioning
 ↓
Replication
 ↓
High Availability
 ↓
Security
 ↓
Backup
 ↓
PITR
 ↓
Disaster Recovery
```

এখন তোমার সবচেয়ে গুরুত্বপূর্ণ mental model:

```text
                  DATABASE
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
 Performance     Reliability    Security
       │             │             │
   Indexing      Transaction    Access Control
   Partition     Replication    Encryption
   Optimize      Backup         SQL Injection
                 PITR
                 Failover
                 DR
```

### ⭐ পাঁচটি concept এক লাইনে

```text
Indexing
→ Query দ্রুত করে

Partitioning
→ Large table manage করতে সাহায্য করে

Replication
→ Availability / Read Scaling

Backup
→ Data Recovery

Disaster Recovery
→ Major disaster-এর পর পুরো system recover
```

**Next → Class 68: Database Monitoring, Logging & Observability** — সেখানে আমরা শিখব **Database Metrics, Slow Query Log, Error Log, Audit Log, Connection Monitoring, CPU/Memory/Disk, Replication Lag, Lock/Deadlock Monitoring, Alerting এবং Production Database Observability Architecture**।

---
# 📚 Class 68 — Database Monitoring, Logging & Observability

আজ আমরা Database-এর **production monitoring** শিখব।

আগের class-এ আমরা শিখেছি:

```text
Class 65 → Replication & High Availability
Class 66 → Security
Class 67 → Backup, Recovery & Disaster Recovery
```

এখন প্রশ্ন:

> **Production database-এ আসলে কী ঘটছে, সেটা কীভাবে বুঝব?**

যেমন:

- Database slow কেন?
    
- CPU কেন 95%?
    
- Memory শেষ হয়ে যাচ্ছে কেন?
    
- কোন query 10 seconds নিচ্ছে?
    
- কতগুলো connection আছে?
    
- Deadlock হচ্ছে কি?
    
- Replica কতটা পিছিয়ে আছে?
    
- Database error হচ্ছে কি?
    
- কোন user sensitive data access করছে?
    
- কখন alert পাঠাব?
    

এসবের জন্য দরকার:

# Database Observability

---

# 1️⃣ Monitoring কী?

Monitoring মানে:

> **Database-এর health এবং performance নিয়মিত measure করা এবং সমস্যা হলে detect করা।**

সহজভাবে:

```text
Database
   ↓
Metrics
   ↓
Monitoring
   ↓
Problem Detection
   ↓
Alert
   ↓
Action
```

---

# 2️⃣ Observability কী?

Monitoring বলে:

> **"Problem আছে কি?"**

Observability আরও বড় প্রশ্ন করে:

> **"কেন problem হচ্ছে?"**

Example:

```text
API slow
   ↓
Database slow
   ↓
Query slow
   ↓
Missing index
```

Monitoring:

```text
DB latency = 5 sec ❌
```

Observability:

```text
Which query?
Why slow?
How many rows scanned?
Which index?
What happened at that time?
```

### Golden Rule ⭐

```text
Monitoring
→ What is happening?

Observability
→ Why is it happening?
```

---

# 3️⃣ Database Observability-এর 3 Pillars ⭐⭐⭐⭐⭐

সাধারণ observability model:

```text
Metrics
Logs
Traces
```

Database-এর ক্ষেত্রে:

```text
        Observability
             │
      ┌──────┼──────┐
      ↓      ↓      ↓
   Metrics  Logs  Traces
```

### Metrics

Numeric measurements:

```text
CPU = 80%
Connections = 150
Query latency = 300 ms
Disk = 75%
```

### Logs

Events:

```text
ERROR
WARNING
Slow Query
Authentication event
```

### Traces

একটি request-এর পুরো journey:

```text
User Request
    ↓
Django
    ↓
Service
    ↓
Database
    ↓
Query
```

কোন অংশ কত সময় নিল তা বোঝাতে tracing useful।

---

# 4️⃣ Database-এর গুরুত্বপূর্ণ Metrics

Production DB monitor করার সময় অনেক metrics থাকে।

সবচেয়ে important:

```text
CPU
Memory
Disk
Connections
Query Latency
Queries/sec
Transactions/sec
Cache Hit Ratio
Locks
Deadlocks
Replication Lag
Disk I/O
```

---

# 5️⃣ CPU Monitoring ⭐⭐⭐

ধরো:

```text
CPU = 95%
```

সম্ভাব্য কারণ:

```text
Heavy Query
Large JOIN
Missing Index
Sort
Aggregation
Too many concurrent queries
```

কিন্তু:

> **CPU 95% দেখলেই database problem বলা যাবে না।**

Context দেখতে হবে।

Example:

```text
CPU = 95%
Query latency = 20 ms
System healthy
```

হতে পারে workload intentionally high।

অন্যদিকে:

```text
CPU = 95%
Query latency = 10 sec
Requests failing
```

এটা serious problem।

---

# 6️⃣ Memory Monitoring

Database memory-এর জন্য গুরুত্বপূর্ণ।

যদি memory pressure হয়:

```text
Memory
 ↓
Cache efficiency ↓
 ↓
Disk I/O ↑
 ↓
Query latency ↑
```

Possible symptoms:

```text
Slow queries
Swapping
High disk I/O
Application timeout
```

---

# 7️⃣ Disk Monitoring ⭐⭐⭐⭐⭐

Database-এর জন্য disk অত্যন্ত গুরুত্বপূর্ণ।

Monitor:

```text
Disk Usage
Disk IOPS
Read latency
Write latency
Disk throughput
```

ধরো:

```text
Disk = 98%
```

এটা critical হতে পারে।

কারণ database-এর জন্য প্রয়োজন হতে পারে:

```text
Data files
Indexes
Logs
Temporary files
WAL/Binary logs
```

Disk full হলে database/application severe সমস্যা করতে পারে।

---

# 8️⃣ Connection Monitoring ⭐⭐⭐

Database-এ application কতগুলো connection খুলছে?

ধরো:

```text
max_connections = 200
current_connections = 195
```

Danger zone হতে পারে।

কারণ নতুন request:

```text
Django
  ↓
DB connection
  ↓
❌ Connection unavailable
```

---

# 9️⃣ Connection Pool

Modern applications সাধারণত connection management করে।

Concept:

```text
Django
 │ │ │ │ │
 └─┴─┴─┴─→ Connection Pool
                  │
          ┌───────┼───────┐
          ↓       ↓       ↓
         DB      DB      DB
```

Pool-এর সুবিধা:

```text
Connection reuse
Less connection overhead
Controlled concurrency
```

কিন্তু pool size ভুল হলে সমস্যা হতে পারে।

---

# 🔟 Too Many Connections

Symptoms:

```text
Connection refused
Timeout
Database overloaded
Application errors
```

Possible causes:

```text
Connection leak
Pool too large
Too many application instances
Long-running connections
Database max connection limit too low
```

---

# 1️⃣1️⃣ Query Latency ⭐⭐⭐⭐⭐

Query কত সময় নিচ্ছে?

Example:

```text
Query A → 5 ms
Query B → 20 ms
Query C → 8 sec ❌
```

Query C investigate করতে হবে।

Monitor:

```text
Average latency
P95 latency
P99 latency
Maximum latency
```

---

# 1️⃣2️⃣ P95 / P99 কেন?

ধরো 100 requests:

```text
95 requests → fast
5 requests → very slow
```

Average দেখে problem লুকিয়ে যেতে পারে।

P95:

> 95% requests এই latency-এর মধ্যে complete করেছে।

P99:

> 99% requests এই latency-এর মধ্যে complete করেছে।

Example:

```text
Average = 100 ms
P95 = 300 ms
P99 = 5 sec
```

মানে কিছু request অত্যন্ত slow।

---

# 1️⃣3️⃣ Queries Per Second — QPS

Database কত query process করছে?

```text
QPS = Queries Per Second
```

Example:

```text
10:00 → 1,000 QPS
10:05 → 10,000 QPS
```

হঠাৎ workload বেড়েছে।

তার সঙ্গে:

```text
CPU ↑
Latency ↑
Connections ↑
```

হলে investigation দরকার।

---

# 1️⃣4️⃣ Slow Query Log ⭐⭐⭐⭐⭐

Slow Query Log database-এর অত্যন্ত গুরুত্বপূর্ণ tool।

এর উদ্দেশ্য:

> **যেসব query নির্দিষ্ট সময়ের বেশি নেয়, সেগুলো record করা।**

Example:

```text
Query
↓
Execution time = 7.2 sec
↓
Slow Query Log
```

---

# 1️⃣5️⃣ Slow Query Example

ধরো:

```sql
SELECT *
FROM bookings
WHERE customer_id = 100;
```

Execution:

```text
7.5 seconds ❌
```

Slow query log বলছে:

```text
Query: SELECT * FROM bookings ...
Time: 7.5 sec
```

এখন:

```text
EXPLAIN
```

দিয়ে investigate করব।

---

# 1️⃣6️⃣ Slow Query → EXPLAIN

আমাদের আগের Class 60 মনে করো:

```text
Slow Query
    ↓
EXPLAIN
    ↓
type
key
rows
Extra
    ↓
Optimization
```

Example:

```sql
EXPLAIN
SELECT *
FROM bookings
WHERE customer_id = 100;
```

যদি:

```text
type = ALL
key = NULL
rows = 5,000,000
```

হয়, index missing হতে পারে।

তখন candidate:

```sql
CREATE INDEX idx_bookings_customer
ON bookings(customer_id);
```

তারপর আবার:

```text
EXPLAIN
```

---

# 1️⃣7️⃣ Error Log ⭐⭐⭐⭐⭐

Database error হলে error log useful।

Example:

```text
ERROR
Connection failed
Disk full
Database crash
Authentication failure
Permission denied
Recovery error
```

Error log বলে:

> **Database system-এর ভিতরে কী ধরনের error ঘটছে।**

---

# 1️⃣8️⃣ Error Log বনাম Slow Query Log

|Slow Query Log|Error Log|
|---|---|
|Slow query|Database errors|
|Performance investigation|Failure investigation|
|Query-centric|System/database-centric|
|Optimization-এর জন্য|Troubleshooting-এর জন্য|

মনে রাখো:

```text
Slow Query Log
→ "কোন query slow?"

Error Log
→ "Database-এ কী error হচ্ছে?"
```

---

# 1️⃣9️⃣ Audit Log ⭐⭐⭐⭐⭐

Audit Log-এর উদ্দেশ্য:

> **কে কী database operation করেছে তা record করা।**

Example:

```text
User: admin
Action: UPDATE
Table: customers
Time: 10:35
```

আরেকটি:

```text
User: report_user
Action: SELECT
Table: payments
Time: 11:02
```

---

# 2️⃣0️⃣ Audit Log কেন দরকার?

Security:

```text
Who?
What?
When?
```

মানে:

```text
Who accessed data?
What did they do?
When did they do it?
```

Useful for:

```text
Security investigation
Compliance
Troubleshooting
Accountability
Sensitive data monitoring
```

---

# 2️⃣1️⃣ Audit Log বনাম Error Log

```text
Audit Log
→ User activity

Error Log
→ Database/system error

Slow Query Log
→ Slow SQL
```

এই তিনটি confuse করবে না।

---

# 2️⃣2️⃣ Replication Lag ⭐⭐⭐⭐⭐

Class 65-এ আমরা replication শিখেছিলাম।

ধরো:

```text
Primary
  ↓
Replica
```

Primary:

```text
Order #100
```

Replica এখনো:

```text
Order #99
```

তাহলে replica পিছিয়ে আছে।

এটাই:

> **Replication Lag**

---

# 2️⃣3️⃣ Replication Lag কেন হয়?

সম্ভাব্য কারণ:

```text
High write workload
Network latency
Replica overloaded
Slow disk
Long-running transaction
Replication bottleneck
```

---

# 2️⃣4️⃣ Replication Lag Problem

User:

```text
POST /orders
```

Write হলো:

```text
Primary
```

তারপর immediately:

```text
GET /orders
```

যদি read যায়:

```text
Replica
```

তাহলে নতুন order নাও দেখা যেতে পারে।

কারণ:

```text
Primary
  ↓
Replication Lag
  ↓
Replica
```

---

# 2️⃣5️⃣ Read-after-write Consistency

এই problem-কে আমরা Class 65-এ দেখেছিলাম।

Flow:

```text
User creates booking
       ↓
Primary DB
       ↓
Success
       ↓
User immediately views booking
       ↓
Replica
       ↓
Booking missing ❌
```

Solution:

Critical read:

```text
Primary
```

অথবা consistency-aware routing।

---

# 2️⃣6️⃣ Lock Monitoring ⭐⭐⭐⭐⭐

Class 63-এর locking মনে করো।

Database-এ transaction একে অপরকে block করতে পারে।

Example:

```text
Transaction A
   ↓
Locks Row 10

Transaction B
   ↓
Needs Row 10
   ↓
WAIT
```

Monitoring-এ দেখতে চাই:

```text
Who is waiting?
Who is blocking?
Which table?
Which query?
How long?
```

---

# 2️⃣7️⃣ Lock Wait

Example:

```text
T1 → Row 100 locked
T2 → waiting
T3 → waiting
```

যদি T1 অনেকক্ষণ ধরে transaction open রাখে:

```text
Waiting transactions ↑
      ↓
Latency ↑
      ↓
Requests timeout
```

---

# 2️⃣8️⃣ Deadlock Monitoring ⭐⭐⭐⭐⭐

Class 63:

```text
T1 locks A
T2 locks B

T1 → wants B
T2 → wants A
```

Result:

```text
T1 ↔ T2
Waiting forever
```

Database সাধারণত deadlock detect করে এবং একটি transaction abort/rollback করতে পারে।

Monitoring-এর কাজ:

```text
Deadlock count
Deadlock frequency
Affected queries
Affected tables
```

---

# 2️⃣9️⃣ Deadlock Log

Production investigation:

```text
Deadlock detected
   ↓
Find transactions
   ↓
Find queries
   ↓
Find lock order
   ↓
Fix application/database logic
```

Common fix:

```text
Consistent lock order
Short transactions
Proper indexes
Avoid unnecessary locking
Retry aborted transaction where appropriate
```

---

# 3️⃣0️⃣ Database Disk I/O

Database শুধু CPU ব্যবহার করে না।

Disk I/O অত্যন্ত গুরুত্বপূর্ণ।

Monitor:

```text
Read IOPS
Write IOPS
Read latency
Write latency
Throughput
```

যদি:

```text
Disk latency ↑
```

হয়:

```text
Query latency ↑
```

হতে পারে।

---

# 3️⃣1️⃣ Cache Hit Ratio

Database frequently accessed data memory-তে রাখার চেষ্টা করে।

Cache hit হলে:

```text
Memory
 ↓
Fast
```

Miss হলে:

```text
Disk
 ↓
Relatively slower
```

তাই cache efficiency monitor করা useful।

তবে:

> **একটি metric-এর threshold blindly apply করা যাবে না।**

Database engine, workload এবং workload pattern বুঝতে হবে।

---

# 3️⃣2️⃣ Database Health Dashboard

Production dashboard-এ আমরা দেখতে পারি:

```text
┌─────────────────────────────────┐
│       DATABASE DASHBOARD        │
├─────────────────────────────────┤
│ CPU             65%             │
│ Memory          72%             │
│ Disk            68%             │
│ Connections     120 / 500       │
│ Query Latency   85 ms           │
│ P95 Latency     210 ms          │
│ QPS             4,500           │
│ Slow Queries    12              │
│ Deadlocks       0               │
│ Lock Waits      3               │
│ Replica Lag     2 sec           │
└─────────────────────────────────┘
```

এক নজরে database health বোঝা যায়।

---

# 3️⃣3️⃣ Alerting ⭐⭐⭐⭐⭐

Monitoring আছে কিন্তু alert নেই?

তাহলে engineer manually dashboard দেখছে।

Production-এ দরকার:

```text
Metric
 ↓
Threshold / Condition
 ↓
Alert
 ↓
Engineer
```

---

# 3️⃣4️⃣ Example Alerts

### CPU

```text
CPU > 90%
for 10 minutes
```

→ Alert

---

### Disk

```text
Disk > 85%
```

→ Warning

```text
Disk > 95%
```

→ Critical

---

### Connections

```text
Connections > 90% of limit
```

→ Alert

---

### Replication

```text
Replica lag > acceptable threshold
```

→ Alert

---

### Query

```text
P95 latency > target
```

→ Alert

---

### Deadlock

```text
Deadlock detected
```

→ Alert depending on severity/frequency.

---

# 3️⃣5️⃣ Warning বনাম Critical

সব alert একই priority না।

```text
INFO
 ↓
WARNING
 ↓
CRITICAL
```

Example:

```text
Disk = 80%
→ WARNING

Disk = 95%
→ CRITICAL
```

---

# 3️⃣6️⃣ Alert Fatigue ❌

অনেক বেশি alert দিলে:

```text
Engineer
 ↓
100 alerts/day
 ↓
সব ignore
```

এটা dangerous।

তাই:

> **Alert only when an engineer needs to take action.**

---

# 3️⃣7️⃣ Good Alert Example

Bad:

```text
CPU = 70%
ALERT!!!
```

Better:

```text
CPU > 90%
AND
Query latency > 2 sec
for 10 minutes
```

Context-aware alert অনেক useful।

---

# 3️⃣8️⃣ Django + Database Monitoring

আমাদের architecture:

```text
User
 ↓
React / Next.js
 ↓
Django / DRF
 ↓
Database
```

Monitoring করা যায়:

```text
Frontend
API
Database
Infrastructure
```

Database level:

```text
Connections
Queries
Latency
Locks
Deadlocks
CPU
Memory
Disk
Replication
```

---

# 3️⃣9️⃣ Request → Database Observability

একটি request:

```text
POST /api/bookings/
        ↓
Django
        ↓
Service Logic
        ↓
SQL Query
        ↓
Database
```

ধরো API response:

```text
3.5 sec
```

Tracing/metrics দিয়ে দেখা গেল:

```text
Django logic → 100 ms
Database → 3.3 sec
```

এখন বোঝা গেল bottleneck database।

---

# 4️⃣0️⃣ Database Bottleneck Investigation ⭐⭐⭐⭐⭐

Production API slow:

```text
API Slow
   ↓
Is Django slow?
   ↓
Is DB slow?
   ↓
Which query?
   ↓
Slow Query Log
   ↓
EXPLAIN
   ↓
Rows?
Index?
Lock?
I/O?
```

আরও systematically:

```text
Observe
 ↓
Measure
 ↓
Identify
 ↓
Investigate
 ↓
Fix
 ↓
Verify
```

---

# 4️⃣1️⃣ Slow Query Investigation Example 🔥

Hotel API:

```text
GET /api/available-rooms/
```

Latency:

```text
6 seconds ❌
```

Investigation:

```text
API
 ↓
Django = 100ms
 ↓
DB = 5.9 sec
```

Slow Query Log:

```text
SELECT ...
FROM bookings
WHERE room_id = ...
```

তারপর:

```sql
EXPLAIN
SELECT ...
FROM bookings
WHERE room_id = 101
  AND check_in < '2026-09-20'
  AND check_out > '2026-09-18';
```

দেখলাম:

```text
type = ALL
rows = 10,000,000
```

Potential optimization:

```sql
CREATE INDEX idx_booking_room_dates
ON bookings(room_id, check_in, check_out);
```

তারপর আবার:

```text
EXPLAIN
```

এবং actual performance benchmark করতে হবে।

---

# 4️⃣2️⃣ Monitoring ≠ Optimization

খুব important distinction।

```text
Monitoring
→ Problem detect

Optimization
→ Problem fix
```

Example:

```text
Monitoring
→ Query latency = 8 sec

Optimization
→ EXPLAIN
→ Index
→ Query rewrite
→ Verify
```

---

# 4️⃣3️⃣ Logging Strategy

Production-এ বিভিন্ন log:

```text
Application Log
Database Error Log
Slow Query Log
Audit Log
Access Log
Security Log
```

প্রতিটির purpose আলাদা।

---

# 4️⃣4️⃣ Centralized Logging ⭐⭐⭐

Production-এ শুধু server-এর local file-এ log রেখে দেওয়া সবসময় ideal নয়।

Concept:

```text
Database
   ↓
Logs
   ↓
Central Log System
   ↓
Search / Dashboard / Alert
```

তাতে multiple server-এর logs এক জায়গায় investigate করা সহজ হয়।

---

# 4️⃣5️⃣ Production Observability Architecture ⭐⭐⭐⭐⭐

```text
                         Users
                           │
                           ↓
                    React / Next.js
                           │
                           ↓
                      Django / DRF
                           │
                           ↓
                     ┌───────────┐
                     │  Primary  │
                     │    DB     │
                     └─────┬─────┘
                           │
             ┌─────────────┼─────────────┐
             ↓             ↓             ↓
          Metrics         Logs       Replication
             │             │             │
             ↓             ↓             ↓
       Monitoring      Log System      Replica
             │
             ↓
          Dashboard
             │
             ↓
           Alerts
             │
             ↓
          Engineer
```

---

# 4️⃣6️⃣ Full Production Flow

```text
                    Production
                        │
       ┌────────────────┼────────────────┐
       ↓                ↓                ↓
    Metrics           Logs            Traces
       │                │                │
       ↓                ↓                ↓
Monitoring         Log Analysis     Request Flow
       │
       └──────────────┬─────────────────┘
                      ↓
                   Dashboard
                      ↓
                    Alert
                      ↓
                  Engineer
                      ↓
                  Investigation
                      ↓
                    Fix
```

---

# 4️⃣7️⃣ What Should We Monitor?

Database engineer হিসেবে minimum checklist:

```text
Infrastructure
├── CPU
├── Memory
├── Disk
└── Network

Database
├── Connections
├── Query latency
├── QPS
├── Transactions
├── Cache
├── Locks
├── Deadlocks
└── Errors

Replication
├── Lag
├── Replica health
└── Replication status

Queries
├── Slow queries
├── Query frequency
├── Execution time
└── EXPLAIN plans

Security
├── Authentication
├── Authorization
└── Audit events
```

---

# 4️⃣8️⃣ Monitoring-এর 5টি প্রশ্ন

যেকোনো production database-এ এই ৫টি প্রশ্ন করতে পারবে:

### 1. Is it healthy?

```text
CPU
Memory
Disk
Errors
```

### 2. Is it fast?

```text
Latency
P95
P99
Slow queries
```

### 3. Is it overloaded?

```text
Connections
QPS
CPU
I/O
```

### 4. Is it blocked?

```text
Locks
Lock waits
Deadlocks
```

### 5. Is replication healthy?

```text
Lag
Replica status
Replication errors
```

---

# 4️⃣9️⃣ Common Mistakes ❌

### Mistake 1

শুধু CPU monitor করা।

❌

Database performance অনেক কিছু depend করে।

---

### Mistake 2

শুধু average latency দেখা।

❌

P95/P99-ও গুরুত্বপূর্ণ।

---

### Mistake 3

Slow query log না রাখা।

❌

---

### Mistake 4

Replica আছে কিন্তু replication lag monitor করি না।

❌

---

### Mistake 5

Deadlock হচ্ছে কিন্তু log/metrics নেই।

❌

---

### Mistake 6

প্রতিটি ছোট metric-এর জন্য alert।

❌

Alert fatigue হবে।

---

### Mistake 7

Monitoring আছে কিন্তু action plan নেই।

❌

Alert:

```text
Disk 95%
```

তারপর কী?

```text
Expand disk?
Delete old logs?
Investigate growth?
Failover?
```

Runbook দরকার।

---

# 5️⃣0️⃣ Monitoring + Runbook ⭐⭐⭐⭐⭐

Good production system:

```text
Alert
 ↓
Runbook
 ↓
Investigation
 ↓
Action
```

Example:

```text
Alert:
Replica lag > 60 sec
```

Runbook:

```text
1. Check replica status
2. Check network
3. Check replica CPU/I/O
4. Check long-running queries
5. Check primary write rate
6. Check replication errors
7. Decide mitigation
```

---

# 🧠 Class 68 Golden Rules ⭐⭐⭐⭐⭐

```text
Monitoring
→ Database health measure করা

Observability
→ System কেন এমন behave করছে তা বোঝা

Metrics
→ Numeric measurements

Logs
→ Events/details

Traces
→ Request journey

CPU
→ Compute pressure

Memory
→ Memory pressure/cache

Disk
→ Capacity + I/O health

Connections
→ Database connection load

Query Latency
→ Query কত দ্রুত/ধীরে চলছে

P95/P99
→ Tail latency বোঝায়

QPS
→ Queries per second

Slow Query Log
→ Slow SQL identify

Error Log
→ Database/system errors

Audit Log
→ Who + What + When

Replication Lag
→ Replica কতটা পিছিয়ে

Lock Monitoring
→ Who is waiting/blocking

Deadlock Monitoring
→ Circular lock conflict detect

Alert
→ Problem হলে engineer-কে notify

Alert Fatigue
→ Too many useless alerts

Monitoring ≠ Optimization

Slow Query
→ EXPLAIN
→ Investigate
→ Optimize
→ Verify

Backup
→ Recovery

Replication
→ Availability / Read Scaling

Monitoring
→ Know what is happening

Observability
→ Understand why
```

---

# 📝 Class 68 Assignment

## Task 1 — Metrics

একটি production DB:

```text
CPU = 92%
Memory = 85%
Disk = 91%
Connections = 480 / 500
P95 Query Latency = 4 sec
Deadlocks = 15/hour
Replica Lag = 120 sec
```

প্রতিটির জন্য বলো:

**Normal / Warning / Critical — এবং কেন?**

---

## Task 2 — Slow Query 🔥

Query:

```sql
SELECT *
FROM bookings
WHERE customer_id = 100;
```

যদি:

```text
Execution time = 8 seconds
rows examined = 10,000,000
key = NULL
```

তাহলে investigation-এর steps লিখো।

---

## Task 3 — Replication

Scenario:

```text
POST /api/orders/
       ↓
Primary
       ↓
Success

GET /api/orders/
       ↓
Replica
       ↓
New order missing
```

**কেন এমন হলো?**

এবং কীভাবে solve করবে?

---

## Task 4 — Deadlock

```text
T1:
LOCK A
WAIT B

T2:
LOCK B
WAIT A
```

Explain:

1. এটা কী?
    
2. কেন হচ্ছে?
    
3. কীভাবে prevent করবে?
    
4. Monitoring-এ কী দেখবে?
    

---

## Task 5 — Production Architecture ⭐⭐⭐⭐⭐

এই architecture complete করো:

```text
Django
   ↓
Primary DB
   ↓
Replica

Primary DB
   ↓
?
   ↓
Dashboard
   ↓
Alert
   ↓
Engineer
```

এখানে:

- Metrics
    
- Logs
    
- Slow Query
    
- Replication Lag
    
- Deadlock
    

কোথায় যাবে সেটা দেখাও।

---

# 🔥 Interview Challenge

Interviewer:

> **"Your Django API suddenly became 8 seconds slower. How would you determine whether the database is responsible?"**

Strong answer:

```text
API latency
    ↓
Check Django/application metrics
    ↓
Measure DB query time
    ↓
Check database CPU / memory / disk I/O
    ↓
Check connections
    ↓
Check slow query log
    ↓
Identify expensive query
    ↓
EXPLAIN / EXPLAIN ANALYZE
    ↓
Check index / rows / locks
    ↓
Check deadlocks / lock waits
    ↓
Optimize
    ↓
Measure again
```

আর interviewer যদি জিজ্ঞেস করে:

> **"How will you know whether your production database is healthy?"**

বলবে:

```text
CPU
Memory
Disk
Connections
Query latency
P95/P99
QPS
Slow queries
Errors
Locks
Deadlocks
Replication lag
Backup status
```

---

# 🏆 Database Engineering এখন কোথায়?

তোমার learning progression এখন:

```text
SQL
 ↓
Advanced SQL
 ↓
Database Design
 ↓
Normalization
 ↓
ERD
 ↓
Indexing
 ↓
Query Optimization
 ↓
Transactions
 ↓
Concurrency
 ↓
Locking
 ↓
Deadlock
 ↓
Partitioning
 ↓
Replication
 ↓
High Availability
 ↓
Security
 ↓
Backup
 ↓
PITR
 ↓
Disaster Recovery
 ↓
Monitoring
 ↓
Logging
 ↓
Observability
```

এখন database-কে শুধু **"table + SQL"** হিসেবে না দেখে এভাবে চিন্তা করবে:

```text
                 DATABASE SYSTEM
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
 Performance       Reliability       Security
       │               │               │
   Indexing        Replication      Access Control
   Partitioning    Backup           Encryption
   Optimization    PITR             Audit
       │           Failover
       ↓           Disaster Recovery
   Monitoring
       │
       ↓
 Observability
```

### ⭐ সবচেয়ে গুরুত্বপূর্ণ distinction

```text
Indexing
→ Faster Query

Partitioning
→ Large Data Management

Replication
→ Availability / Read Scaling

Backup
→ Recovery

DR
→ Major Failure Recovery

Monitoring
→ Detect Problems

Observability
→ Understand Problems
```

**Next → Class 69: Database High Availability, Failover & Disaster Recovery Architecture** — এখানে আমরা আগের **Replication + Backup + PITR + Monitoring** concepts একসাথে নিয়ে **Single Point of Failure, Failover, Automatic Failover, Primary/Replica Architecture, Read/Write Routing, Health Checks, RPO/RTO-based HA design এবং production-grade database architecture** design করব।

---

# 📚 Class 69 — Database High Availability, Failover & Disaster Recovery Architecture

আজকের class-টা খুব গুরুত্বপূর্ণ, কারণ আগের কয়েকটি class-এর concept একসাথে ব্যবহার করব:

```text
Class 65 → Replication
Class 67 → Backup + PITR + DR
Class 68 → Monitoring + Logging + Observability
```

আজকের লক্ষ্য:

> **একটা Production Database কীভাবে এমনভাবে design করব, যাতে Primary DB নষ্ট হলেও application যত দ্রুত সম্ভব আবার চালু হতে পারে?**

আমরা শিখব:

```text
1. Single Point of Failure (SPOF)
2. High Availability (HA)
3. Primary/Replica Architecture
4. Failover
5. Automatic Failover
6. Read/Write Routing
7. Health Checks
8. RPO/RTO-based HA Design
9. Backup + PITR + HA একসাথে
10. Production-grade Database Architecture
```

---

# 1️⃣ High Availability — HA কী?

High Availability মানে:

> **System failure হলেও service যতটা সম্ভব available রাখা।**

ধরো আমাদের application:

```text
User
 ↓
Django
 ↓
Database
```

যদি database server নষ্ট হয়:

```text
Database ❌
 ↓
Django ❌
 ↓
Application ❌
```

এটা low availability।

HA architecture:

```text
                 Django
                   │
                   ↓
               DB System
              /          \
             ↓            ↓
         Primary       Replica
```

Primary failure হলে:

```text
Primary ❌
   ↓
Failover
   ↓
Replica becomes Primary
```

Application আবার database-এর সঙ্গে কাজ করতে পারে।

---

# 2️⃣ Single Point of Failure — SPOF ⭐⭐⭐⭐⭐

SPOF মানে:

> **System-এর এমন একটি component যার failure পুরো service বন্ধ করে দিতে পারে।**

Example:

```text
Django
  ↓
ONE Database
```

এখানে:

```text
Database = SPOF
```

কারণ:

```text
DB failure
   ↓
Application unavailable
```

---

# 3️⃣ SPOF Example

ধরো:

```text
              Application
                   │
                   ↓
              Primary DB
```

এখানে একটাই database।

Primary:

```text
Healthy → Application works
Failed  → Application stops
```

তাই:

> **Single DB architecture = database-level SPOF**

---

# 4️⃣ SPOF কীভাবে কমাব?

একটি replica যোগ করি:

```text
               Application
                    │
                    ↓
                Primary
                    │
                    ↓
                 Replica
```

এখন Primary failure হলে:

```text
Primary ❌
   ↓
Replica
   ↓
Promote
   ↓
New Primary
```

এটাই failover-এর basic idea।

---

# 5️⃣ Primary + Replica Architecture ⭐⭐⭐⭐⭐

Basic:

```text
                    Application
                         │
                         ↓
                      Primary
                         │
                  Replication
                         │
                         ↓
                      Replica
```

Primary সাধারণত:

```text
WRITE
```

Replica:

```text
READ
```

তবে exact routing architecture-এর উপর নির্ভর করে।

---

# 6️⃣ Read/Write Routing ⭐⭐⭐⭐⭐

আমাদের Django application:

```text
                Django
              /        \
          WRITE         READ
            ↓             ↓
         Primary       Replica
```

Example:

### Create order

```python
Order.objects.using("default").create(...)
```

→ Primary

### Read orders

```python
Order.objects.using("replica").all()
```

→ Replica

---

# 7️⃣ কিন্তু একটা সমস্যা আছে ⚠️

Replication asynchronous হলে:

```text
Primary
  ↓
Replication Lag
  ↓
Replica
```

Primary-তে data এসেছে কিন্তু replica এখনো পায়নি।

Example:

```text
POST /orders
      ↓
Primary
      ↓
Order #100 created ✅
```

তারপর:

```text
GET /orders
      ↓
Replica
      ↓
Order #100 missing ❌
```

এটাকে বলে:

# Read-after-write consistency problem

---

# 8️⃣ Solution: Critical Read → Primary

যদি user刚 write করেছে এবং immediately সেই data দরকার:

```text
WRITE
 ↓
Primary

Immediate READ
 ↓
Primary
```

আর normal read:

```text
READ
 ↓
Replica
```

---

# 9️⃣ Practical Routing Strategy

```text
                    Django
                       │
          ┌────────────┴────────────┐
          ↓                         ↓
       WRITE                     READ
          ↓                         ↓
      Primary                Read Replica
                                  │
                         ┌────────┴────────┐
                         ↓                 ↓
                     Replica 1        Replica 2
```

এতে:

```text
Writes → Primary
Reads → Replicas
```

হলে read workload scale করা যায়।

---

# 🔟 Failover কী?

Failover:

> **Primary database failure হলে অন্য healthy database server-কে primary হিসেবে ব্যবহার করা।**

Before:

```text
Primary
   ↓
Replica
```

After Primary failure:

```text
Primary ❌

Replica
   ↓
PROMOTE
   ↓
New Primary
```

---

# 1️⃣1️⃣ Manual Failover

Engineer manually:

```text
Detect Primary Failure
        ↓
Verify Replica
        ↓
Promote Replica
        ↓
Update DB Routing
        ↓
Application reconnect
```

Advantages:

```text
More control
```

Disadvantages:

```text
Human intervention
Recovery takes longer
Human error possible
```

---

# 1️⃣2️⃣ Automatic Failover ⭐⭐⭐⭐⭐

Automatic failover:

```text
Primary
   ↓
Health Check
   ↓
❌ Failure detected
   ↓
Failover Controller
   ↓
Promote Replica
   ↓
Update Routing
   ↓
Application
```

Human manually intervene না করেও system failover করতে পারে।

---

# 1️⃣3️⃣ Automatic Failover-এর Risk ⚠️

Automatic failover powerful হলেও dangerous হতে পারে।

ধরো network সমস্যা:

```text
Primary
   │
   X
   │
Monitoring system
```

Monitoring system ভাবল:

> Primary dead!

কিন্তু আসলে Primary alive।

তখন যদি Replica-কে primary বানায়:

```text
Old Primary → thinks it's Primary
New Primary → thinks it's Primary
```

তাহলে:

# Split Brain

হতে পারে।

---

# 1️⃣4️⃣ Split Brain ⭐⭐⭐⭐⭐

Split brain:

> **একই সময়ে দুই বা তার বেশি node নিজেকে Primary হিসেবে মনে করা।**

Example:

```text
        Primary A
        ↙      ↘
      Writes  Writes
        ↘      ↙
        Primary B
```

এটা data consistency-এর জন্য extremely dangerous।

তাই production failover architecture-এ:

```text
Leader election
+
Quorum / consensus mechanisms
+
Fencing
+
Health checks
```

জাতীয় mechanism প্রয়োজন হতে পারে।

---

# 1️⃣5️⃣ Health Check ⭐⭐⭐⭐⭐

Failover system কীভাবে জানবে database healthy?

Health checks।

Check করা যেতে পারে:

```text
Database reachable?
Connection possible?
Accepting queries?
Replication healthy?
Replication lag?
Disk available?
CPU overloaded?
Read/write working?
```

---

# 1️⃣6️⃣ Simple Health Check

Concept:

```text
Health Checker
     ↓
SELECT 1
     ↓
Database
```

যদি response:

```text
Success → Healthy
Failure → Investigate
```

কিন্তু production health check শুধু `SELECT 1` হওয়া যথেষ্ট নয়।

---

# 1️⃣7️⃣ Liveness বনাম Readiness

এটি production architecture-এ গুরুত্বপূর্ণ।

### Liveness

> Process/system alive কিনা?

```text
Is DB process responding?
```

### Readiness

> Traffic নেওয়ার জন্য DB actually ready কিনা?

```text
Can this node safely serve application traffic?
```

একটি node alive হতে পারে কিন্তু:

```text
Replication broken
Disk full
Read-only
Recovery চলছে
```

তখন সে healthy-looking হলেও traffic নেওয়ার জন্য ready নাও হতে পারে।

---

# 1️⃣8️⃣ Failover-এর সময় কী কী check করবে?

```text
1. Primary really failed?
2. Replica healthy?
3. Replica sufficiently caught up?
4. Any replication lag?
5. Any transactions in flight?
6. Promote candidate?
7. Prevent old primary from writing?
8. Update routing?
9. Application reconnect?
10. Verify writes?
```

---

# 1️⃣9️⃣ RPO + Failover ⭐⭐⭐⭐⭐

ধরো:

```text
Primary
   ↓
Replica
```

Replication asynchronous।

Primary failure-এর সময়:

```text
Primary → 100 orders
Replica → 97 orders
```

তাহলে latest 3 orders replica-তে নেই।

Potential data loss:

```text
3 orders
```

এখানেই RPO গুরুত্বপূর্ণ।

---

# 2️⃣0️⃣ RPO-based Architecture

### RPO = 24 hours

Simple system:

```text
Daily Backup
```

### RPO = 1 hour

```text
Frequent Backup
```

### RPO = minutes

```text
Frequent Backup
+
Transaction Logs / PITR
+
Replication
```

### Very low RPO

Stronger replication/recovery architecture প্রয়োজন হতে পারে।

---

# 2️⃣1️⃣ RTO + Failover ⭐⭐⭐⭐⭐

ধরো:

```text
RTO = 10 minutes
```

Manual process:

```text
Detect
 ↓
Engineer wakes up
 ↓
Investigate
 ↓
Promote
 ↓
Routing
 ↓
Test
```

সময় 10 মিনিট ছাড়িয়ে যেতে পারে।

তাই low RTO চাইলে:

```text
Automatic Detection
+
Automatic/fast Failover
+
Automated Routing
+
Pre-tested Recovery
```

প্রয়োজন হতে পারে।

---

# 2️⃣2️⃣ RPO/RTO Relationship

মনে রাখো:

```text
RPO → Data Recovery Requirement
RTO → Time Recovery Requirement
```

Architecture:

```text
Lower RPO
   ↓
More frequent/continuous data protection

Lower RTO
   ↓
Faster failover/recovery infrastructure
```

---

# 2️⃣3️⃣ Backup + PITR + Replication

এগুলো একে অপরের replacement নয়।

```text
Replication
→ Fast availability/failover

Backup
→ Historical recovery

PITR
→ Recover to a specific time

DR
→ Major infrastructure disaster
```

---

# 2️⃣4️⃣ কেন Replica যথেষ্ট নয়?

ধরো:

```text
10:00 → Good
10:30 → Good
11:00 → Application bug
11:01 → Bad UPDATE
```

Replication:

```text
Primary
  ↓
Bad UPDATE
  ↓
Replica
```

Replica-তেও bad update চলে যেতে পারে।

কিন্তু PITR:

```text
Backup
 +
Logs
 ↓
10:59:59
```

এখন আগের state recover করা সম্ভব হতে পারে।

---

# 2️⃣5️⃣ Production Architecture — Level 1

Small production:

```text
                 Django
                   │
                   ↓
                Primary
                   │
                   ↓
                Replica
                   │
                   ↓
                Backup
```

এখানে:

```text
Primary → Writes
Replica → Reads / Failover
Backup → Recovery
```

---

# 2️⃣6️⃣ Production Architecture — Level 2

আরও robust:

```text
                  Django
                    │
               DB Router
               /       \
              ↓         ↓
          Primary      Replicas
                       /       \
                      ↓         ↓
                 Replica 1  Replica 2

Primary
   ↓
Backup
   ↓
Offsite Storage
```

---

# 2️⃣7️⃣ Production Architecture — Level 3 ⭐⭐⭐⭐⭐

এখন সব concepts combine করি:

```text
                         Users
                           │
                           ↓
                    Load Balancer
                           │
                           ↓
                     Django Cluster
                           │
                     DB Proxy/Router
                           │
              ┌────────────┴────────────┐
              ↓                         ↓
          Primary DB              Read Replicas
              │                   /           \
              │                  ↓             ↓
              │             Replica 1      Replica 2
              │
              ├──────────→ WAL/Binlog
              │
              ↓
         Backup System
              │
        ┌─────┴──────┐
        ↓            ↓
    Local Backup  Offsite Backup
                       │
                       ↓
                    DR Site
```

Monitoring:

```text
All components
      ↓
Metrics + Logs
      ↓
Monitoring
      ↓
Alerts
```

---

# 2️⃣8️⃣ Database Proxy/Router

Application সরাসরি database node-গুলোর address জানলে failover management complicated হতে পারে।

Instead:

```text
Django
   ↓
DB Proxy / Router
   ↓
Primary / Replica
```

Proxy layer করতে পারে:

```text
Connection routing
Health checking
Failover routing
Read/write separation
Connection management
```

---

# 2️⃣9️⃣ Failover Flow ⭐⭐⭐⭐⭐

Normal:

```text
Django
 ↓
Proxy
 ↓
Primary
```

Failure:

```text
Primary ❌
 ↓
Health Check
 ↓
Failover Controller
 ↓
Replica Promotion
 ↓
New Primary
 ↓
Proxy updates route
 ↓
Django
```

Application-এর perspective থেকে ideally:

```text
Django
 ↓
Same DB endpoint
```

থাকে।

---

# 3️⃣0️⃣ Why Stable DB Endpoint?

Bad design:

```text
Django
 ↓
primary-db-1
```

Primary change হলে application configuration change করতে হতে পারে।

Better:

```text
Django
 ↓
db.example.internal
 ↓
Current Primary
```

Failover হলে:

```text
db.example.internal
       ↓
New Primary
```

Routing layer update করে।

---

# 3️⃣1️⃣ Health Check + Routing

Architecture:

```text
             DB Proxy
                │
       ┌────────┼────────┐
       ↓        ↓        ↓
   Primary   Replica1  Replica2
       │
    Health
     Check
```

Primary healthy:

```text
WRITE → Primary
```

Primary failed:

```text
WRITE → New Primary
```

Read:

```text
READ → Healthy Replicas
```

---

# 3️⃣2️⃣ Automatic Failover-এর গুরুত্বপূর্ণ components

```text
Health Checker
+
Failover Controller
+
Leader Election
+
Fencing
+
DB Proxy
+
Replication
+
Monitoring
```

সব system-এ exact implementation একই হবে না।

---

# 3️⃣3️⃣ Fencing কী?

Advanced concept।

ধরো old primary-এর network issue হয়েছে এবং system তাকে inactive ধরে ফেলেছে।

Failover করার আগে নিশ্চিত করতে হবে:

> **Old primary আর writes করতে পারবে না।**

এটাকে broadly fencing বলা হয়।

Concept:

```text
Old Primary
     ↓
FENCE / isolate
     ↓
Cannot write

New Primary
     ↓
Accept writes
```

এটি split-brain risk কমাতে সাহায্য করে।

---

# 3️⃣4️⃣ Quorum Concept

Multiple nodes থাকলে decision নেওয়ার জন্য majority concept ব্যবহার করা যায়।

ধরো:

```text
Node A
Node B
Node C
```

Majority:

```text
2 out of 3
```

এতে এক node-এর ভুল সিদ্ধান্তে পুরো cluster বিভ্রান্ত হওয়ার risk কমে।

Exact quorum/consensus implementation depends on the HA technology.

---

# 3️⃣5️⃣ DR Site ⭐⭐⭐⭐⭐

ধরো পুরো primary datacenter:

```text
Region A ❌
```

তখন:

```text
Region B
   ↓
DR Infrastructure
```

ব্যবহার করা যেতে পারে।

Architecture:

```text
             Region A
        ┌────────────────┐
        │ App + Primary  │
        │ DB + Replica   │
        └───────┬────────┘
                │
            Replication/
             Backup
                │
                ↓
             Region B
        ┌────────────────┐
        │ DR Environment │
        └────────────────┘
```

---

# 3️⃣6️⃣ Regional Disaster

ধরো:

```text
Region A
   ❌
```

তাহলে recovery:

```text
DR Region
   ↓
Promote / Restore
   ↓
Application
   ↓
Users
```

RTO/RPO অনুযায়ী architecture-এর complexity নির্ধারিত হবে।

---

# 3️⃣7️⃣ Full Recovery Strategy

Production database-এর জন্য:

```text
                  DATABASE
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
   Replication     Backup      Monitoring
        │            │            │
        ↓            ↓            ↓
    Failover       PITR        Alerts
        │            │
        └──────┬─────┘
               ↓
              DR
```

---

# 3️⃣8️⃣ Hotel System — Production Example 🔥

আমাদের hotel system:

```text
customers
rooms
room_types
bookings
payments
```

Traffic:

```text
Customers
    ↓
Django
    ↓
DB Proxy
```

Writes:

```text
Booking
Payment
Customer update
     ↓
Primary
```

Reads:

```text
Room search
Booking history
Reports
     ↓
Read Replicas
```

Critical booking availability:

```text
Primary
+
Transaction
+
Lock
```

Backup:

```text
Primary
 ↓
Backup
 ↓
Offsite Storage
```

Monitoring:

```text
CPU
Memory
Disk
Latency
Connections
Locks
Deadlocks
Replication Lag
Backup Status
```

---

# 3️⃣9️⃣ Hotel Double Booking + HA

একটি গুরুত্বপূর্ণ distinction:

HA থাকা মানেই double booking problem solve হবে না।

Double booking prevent করতে:

```text
Transaction
+
Correct overlap logic
+
Locking
+
Proper concurrency control
```

দরকার।

HA solve করে:

```text
Database availability
```

Business correctness solve করে:

```text
Transaction + Concurrency Design
```

---

# 4️⃣0️⃣ HA বনাম Backup বনাম DR

|Technology|Main Purpose|
|---|---|
|Index|Query performance|
|Partition|Large data management|
|Replication|Availability/read scaling|
|Failover|Continue service after node failure|
|Backup|Data recovery|
|PITR|Recover specific time|
|DR|Major disaster recovery|
|Monitoring|Detect problems|

---

# 4️⃣1️⃣ RPO/RTO-Based Architecture

### Scenario A

```text
RPO = 24h
RTO = 24h
```

Possible:

```text
Daily Full Backup
+
Simple Restore
```

---

### Scenario B

```text
RPO = 1h
RTO = 4h
```

Possible:

```text
Frequent Backup
+
Offsite Backup
+
Restore Procedure
```

---

### Scenario C

```text
RPO = 15 min
RTO = 1h
```

Possible architecture:

```text
Replication
+
Frequent Backup
+
PITR
+
Monitoring
+
Fast Failover
```

---

### Scenario D

```text
Very Low RPO
Very Low RTO
```

এক্ষেত্রে:

```text
Redundant infrastructure
+
Strong replication
+
Automated failover
+
PITR
+
Offsite/DR
+
Continuous monitoring
+
Regular recovery drills
```

প্রয়োজন হতে পারে।

---

# 4️⃣2️⃣ Production Readiness Checklist ⭐⭐⭐⭐⭐

Database production-এ যাওয়ার আগে:

```text
□ Primary + Replica
□ Replication monitoring
□ Replication lag monitoring
□ Backup
□ PITR capability
□ Offsite backup
□ Backup encryption
□ Restore test
□ Failover test
□ Health checks
□ Stable DB endpoint
□ Connection management
□ Slow query monitoring
□ Lock monitoring
□ Deadlock monitoring
□ CPU monitoring
□ Memory monitoring
□ Disk monitoring
□ Alerts
□ Runbooks
□ RPO defined
□ RTO defined
□ DR plan
```

---

# 4️⃣3️⃣ Common Mistakes ❌

### ❌ 1. Replica আছে মানেই HA complete

না।

Need:

```text
Failover
Health checks
Routing
Monitoring
Testing
```

---

### ❌ 2. Replica = Backup

না।

---

### ❌ 3. Automatic failover = always safe

না।

Split brain risk আছে।

---

### ❌ 4. শুধু `SELECT 1` health check

এটা basic liveness check হতে পারে; production readiness বোঝার জন্য আরও signals দরকার।

---

### ❌ 5. RPO/RTO define না করা

Architecture blindly design করা যাবে না।

---

### ❌ 6. Failover কখনো test না করা

Disaster-এর দিন প্রথমবার failover test করা উচিত নয়।

---

### ❌ 7. Backup restore test না করা

Backup আছে বললেই হবে না।

---

### ❌ 8. Read replica-তে critical immediate read পাঠানো

Replication lag থাকলে stale data দেখা যেতে পারে।

---

# 🧠 Class 69 Golden Rules ⭐⭐⭐⭐⭐

```text
SPOF
→ Single failure point

HA
→ Keep service available despite failures

Primary
→ Usually handles writes

Replica
→ Read scaling / failover candidate

Replication
→ Keeps database copies synchronized

Failover
→ Move service to another DB node

Automatic Failover
→ Failure detection + automated promotion/routing

Health Check
→ Determine node health/readiness

Read/Write Routing
→ Write → Primary
→ Read → Replica when appropriate

Read-after-write
→ Critical reads may need Primary

Replication Lag
→ Replica may temporarily be behind

Split Brain
→ Multiple nodes think they are Primary

Fencing
→ Prevent old Primary from writing

Quorum
→ Majority-based decision concept

RPO
→ Acceptable data loss

RTO
→ Acceptable recovery time

Backup
→ Historical recovery

PITR
→ Recover to a specific time

DR
→ Major disaster recovery

Monitoring
→ Detect system problems

Failover ≠ Backup

Replication ≠ Backup

HA ≠ Disaster Recovery

Low RTO
→ Faster/more automated recovery needed

Low RPO
→ More continuous data protection needed

Failover must be tested

Restore must be tested

Production HA
→ Replication + Failover + Monitoring + Backup + DR
```

---

# 📝 Class 69 Assignment

## Task 1 — SPOF

এই architecture:

```text
Django
  ↓
Primary DB
```

Identify:

1. SPOF কোনটি?
    
2. Primary fail করলে কী হবে?
    
3. কীভাবে architecture improve করবে?
    

---

## Task 2 — Read/Write Routing

এই operations:

```text
1. Create Booking
2. Search Rooms
3. View Booking History
4. Create Payment
5. Generate Report
6. Immediately after booking → Show booking
```

প্রতিটির জন্য বলো:

```text
Primary
নাকি
Replica
```

এবং **কেন**।

---

## Task 3 — Failover 🔥

এই architecture:

```text
Primary
   ↓
Replica
```

Primary suddenly fails।

পুরো failover process step-by-step লিখো।

---

## Task 4 — RPO/RTO

একটি hotel system-এর requirement:

```text
RPO = 15 minutes
RTO = 30 minutes
```

Design করো:

```text
Backup
Replication
PITR
Monitoring
Failover
DR
```

---

## Task 5 — Split Brain ⭐⭐⭐⭐⭐

Explain:

```text
Why can automatic failover cause split brain?

How can we reduce this risk?
```

তোমার answer-এ ব্যবহার করবে:

```text
Health Check
Leader Election
Quorum
Fencing
```

---

# 🔥 Interview Challenge

Interviewer:

> **"Design a production database architecture for a Django hotel booking system. The system requires RPO ≤ 15 minutes and RTO ≤ 30 minutes."**

একটি strong high-level answer এমন হতে পারে:

```text
                         Users
                           │
                           ↓
                    Load Balancer
                           │
                           ↓
                    Django Cluster
                           │
                           ↓
                      DB Proxy
                       /     \
                      ↓       ↓
                  Primary   Replicas
                      │
                      ↓
                 WAL/Binlog
                      │
              ┌───────┴────────┐
              ↓                ↓
          Backup            Monitoring
              │                │
              ↓                ↓
       Offsite Storage       Alerts
              │
              ↓
           DR Site
```

তারপর explain করবে:

```text
Primary
→ Writes

Replicas
→ Read scaling + failover candidate

DB Proxy
→ Routing + failover abstraction

Replication
→ Low RPO / availability

PITR
→ Recover from accidental changes

Backup
→ Historical recovery

Monitoring
→ Detect failures

Automatic/fast failover
→ Meet RTO

Offsite DR
→ Regional disaster recovery
```

সবশেষে বলবে:

> **"I would validate the design with regular failover drills, restore tests, replication-lag monitoring, and measured RPO/RTO."**

এটাই একজন **Database Designer / Data Engineer-এর production-level চিন্তা**।



----
