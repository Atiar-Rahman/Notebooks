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

| Name  | Email                                     | Phone       |
| ----- | ----------------------------------------- | ----------- |
| Rahim | [rahim@gmail.com](mailto:rahim@gmail.com) | 01711122222 |
| Karim | [karim@yahoo.com](mailto:karim@yahoo.com) | 01822233333 |

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

---
হ্যাঁ, screenshot দেখে বুঝতে পারছি। 👍

আপনার **email B column-এ**, আর username আপনি **D column-এ** বের করতে চাচ্ছেন।

আপনার ক্ষেত্রে:

- `B2` → `atiar@gmail.com`
    
- `B3` → `rahim@gmail.com`
    
- `B4` → `karim@gmail.com`
    

### LibreOffice Calc-এ D2-তে এই formula দিন:

```calc
=LEFT(B2;SEARCH("@";B2)-1)
```

তারপর **Enter** চাপুন।

Result হবে:

```text
D2 → atiar
```

এরপর D2-এর নিচের ডান পাশের ছোট square ধরে **নিচে drag** করুন।

তাহলে:

|A|B|D|
|---|---|---|
|Atiar|[atiar@gmail.com](mailto:atiar@gmail.com)|atiar|
|rahim|[rahim@gmail.com](mailto:rahim@gmail.com)|rahim|
|korim|[karim@gmail.com](mailto:karim@gmail.com)|karim|
|rashd|[rashed@gmail.com](mailto:rashed@gmail.com)|rashed|
|kalid|[khalid@gmail.com](mailto:khalid@gmail.com)|khalid|
|nafic|[nafic@gmail.com](mailto:nafic@gmail.com)|nafic|

### ⚠️ আপনার screenshot অনুযায়ী গুরুত্বপূর্ণ

আপনি যদি **D column-এ uppercase** চান, তাহলে:

```calc
=UPPER(LEFT(B2;SEARCH("@";B2)-1))
```

Result:

```text
ATIAR
RAHIM
KARIM
RASHED
KHALID
NAFIC
```

**আপনার screenshot-এর D column-এর মতো uppercase result চাইলে দ্বিতীয় formula-টাই ব্যবহার করুন।**


---

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

| Employee | Birth Date | Joining Date |
| -------- | ---------- | ------------ |
| Rahim    | 15/06/2000 | 10/01/2022   |
| Karim    | 20/03/1999 | 15/05/2023   |
| Hasan    | 05/11/2001 | 20/08/2024   |
| Jony     | 10/02/2000 | 01/02/2025   |
| Sakib    | 25/08/2002 | 10/06/2026   |

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
অবশ্যই। একদম **সহজ example দিয়ে step-by-step** বুঝাই।

তোমার formula:

```
=VLOOKUP($A$2,'Sheet-1'!$A$1:$G$382,MATCH(B1,'Sheet-1'!$A$1:$G$1,0),0)
```

ধরো **Sheet-1** এ data এমন:

|A|B|C|D|E|F|G|
|---|---|---|---|---|---|---|
|Order No|Order Date|City|Account Manager|Order Priority|Product Name|Product Category|
|5071-1|05-05-13|Dhaka|Affia Siddika|Medium|Laser Neon Mac Format Diskettes|Technology|
|5072-1|06-05-13|Chittagong|Rahim|High|Printer|Office|

আর তোমার অন্য sheet-এ:

|A|B|C|D|
|---|---|---|---|
|**Order No**|**Order Date**|**City**|**Account Manager**|
|5071-1|?|?|?|

---

## ১. `$A$2` কী করছে?

Formula-এর প্রথম অংশ:

```
$A$2
```

মানে Excel **A2 cell-এর value** নেবে।

A2-তে আছে:

```
5071-1
```

অর্থাৎ Excel বলছে:

> "আমি 5071-1 order-টা খুঁজব।"

`$` থাকার কারণে formula copy করলেও A2 পরিবর্তন হবে না।

---

## ২. `'Sheet-1'!$A$1:$G$382` কী?

এটা হলো **কোথায় search করবে**।

```
'Sheet-1'!$A$1:$G$382
```

মানে:

> Sheet-1-এর A1 থেকে G382 পর্যন্ত পুরো table-এর মধ্যে খুঁজবে।

সহজভাবে:

**Search করার জায়গা = Sheet-1-এর A1:G382**

---

## ৩. এখন আসল interesting part: `MATCH`

Formula-এর এই অংশটা:

```
MATCH(B1,'Sheet-1'!$A$1:$G$1,0)
```

ধরো তোমার B1-এ লেখা:

```
Order Date
```

আর Sheet-1-এর প্রথম row:

|A1|B1|C1|D1|E1|F1|G1|
|---|---|---|---|---|---|---|
|Order No|Order Date|City|Account Manager|Order Priority|Product Name|Product Category|

তাহলে:

```
MATCH("Order Date",A1:G1,0)
```

Excel দেখবে:

- Order No → position **1**
    
- Order Date → position **2** ✅
    
- City → position 3
    
- Account Manager → position 4
    
- ...
    

তাই `MATCH` এর result হবে:

```
2
```

অর্থাৎ:

> **Order Date হলো table-এর 2 নম্বর column।**

---

# ৪. এবার VLOOKUP কী করবে?

Formula-এর structure:

```
VLOOKUP(কি খুঁজব, কোথায় খুঁজব, কোন column থেকে result আনব, exact/approximate)
```

তোমার formula:

```
VLOOKUP(
    $A$2,
    'Sheet-1'!$A$1:$G$382,
    MATCH(...),
    0
)
```

মানে:

### Step 1

A2 থেকে নাও:

```
5071-1
```

### Step 2

Sheet-1-এর A:G table-এ `5071-1` খুঁজো।

পেয়ে গেল:

|Order No|Order Date|City|
|---|---|---|
|**5071-1**|05-05-13|Dhaka|

### Step 3

`MATCH` বলেছে **Order Date = column 2**

তাই VLOOKUP বলবে:

> 5071-1-এর **2 নম্বর column-এর value** আমাকে দাও।

Result:

```
05-05-13
```

---

# ৫. তাহলে পুরো formula-টা মানুষের ভাষায়

এই formula:

```
=VLOOKUP($A$2,'Sheet-1'!$A$1:$G$382,MATCH(B1,'Sheet-1'!$A$1:$G$1,0),0)
```

সহজ বাংলায়:

> **A2-তে যে Order No. আছে, সেটা Sheet-1-এর table-এ খুঁজে বের করো। তারপর B1-এ যে heading আছে, সেই heading-এর column খুঁজে বের করে ওই Order No.-এর corresponding value দেখাও।**

---

# ৬. এখন formula copy করলে কী হয়?

এটাই formula-টির সবচেয়ে useful ব্যাপার।

B2-তে:

```
=VLOOKUP($A$2,'Sheet-1'!$A$1:$G$382,MATCH(B1,'Sheet-1'!$A$1:$G$1,0),0)
```

এখানে B1 = **Order Date**

তাই result:

**05-05-13**

এখন formula-টা C2-তে copy করলে:

```
=VLOOKUP($A$2,'Sheet-1'!$A$1:$G$382,MATCH(C1,'Sheet-1'!$A$1:$G$1,0),0)
```

C1 = **City**

তাই MATCH হবে:

```
City → column 3
```

Result হবে:

```
Dhaka
```

আবার D2-তে copy করলে:

```
D1 = Account Manager
```

MATCH করবে:

```
Account Manager → column 4
```

Result:

```
Affia Siddika
```

---

## পুরো ব্যাপারটা এক নজরে

```
A2 = 5071-1
       ↓
   VLOOKUP
       ↓
Sheet-1 এ 5071-1 খুঁজবে
       ↓
B1/C1/D1 দেখে কোন তথ্য চাই তা বুঝবে
       ↓
MATCH column number বের করবে
       ↓
VLOOKUP সেই column-এর value আনবে
```

### B2 → Order Date

```
5071-1 → Order Date → 05-05-13
```

### C2 → City

```
5071-1 → City → Dhaka
```

### D2 → Account Manager

```
5071-1 → Account Manager → Affia Siddika
```

### E2 → Order Priority

```
5071-1 → Order Priority → Medium
```

**এক কথায়:** `VLOOKUP` ঠিক করে **কোন Order খুঁজবে**, আর `MATCH` ঠিক করে **কোন তথ্য/column থেকে result আনবে**।



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
হ্যাঁ, এখানে তুমি **XLOOKUP** ব্যবহার করেছো। এটা আগের `VLOOKUP + MATCH` formula-এর তুলনায় আরও সহজভাবে কাজ করে।

তোমার formula:

```
=XLOOKUP($A$2,'Sheet-1'!$A$2:$A$382,'Sheet-1'!G2:G382)
```

চলো example দিয়ে বুঝি।

### ধরো Sheet-1 এ data এমন:

|A — Order No|B — Order Date|C — City|D — Account Manager|E — Order Priority|F — Product Name|G — Product Category|
|---|---|---|---|---|---|---|
|5145-2|29-06-13|Dhaka|Tabassum Khan|Low|Artisan Hi-Liter...|Office Supplies|
|5146-2|30-06-13|Chittagong|Rahim|High|Printer|Technology|

তোমার current sheet-এ:

|A|B|C|D|E|F|G|
|---|---|---|---|---|---|---|
|Order No|Order Date|City|Account Manager|Order Priority|Product Name|Product Category|
|**5145-2**|29-06-13|Dhaka|Tabassum Khan|Low|Artisan Hi-Liter...|**Office Supplies**|

---

## Formula-টা ৩টা অংশে ভাঙি

### ① `$A$2`

```
$A$2
```

এখানে A2-তে আছে:

```
5145-2
```

অর্থাৎ XLOOKUP বলছে:

> **আমি 5145-2 খুঁজবো।**

---

### ② `'Sheet-1'!$A$2:$A$382`

এটা হলো **কোথায় খুঁজবে**।

```
'Sheet-1'!$A$2:$A$382
```

অর্থাৎ Sheet-1-এর A2 থেকে A382 পর্যন্ত Order No খুঁজবে।

যেমন:

```
A2 → 5145-1
A3 → 5145-2  ← এখানে পেল!
A4 → 5145-3
...
```

তাই `5145-2` খুঁজে পেয়ে গেল।

---

### ③ `'Sheet-1'!G2:G382`

এটা হলো **কোথা থেকে result আনবে**।

```
'Sheet-1'!G2:G382
```

মানে, যে row-তে `5145-2` পাওয়া গেছে, সেই একই row-এর **G column-এর value** নিয়ে আসবে।

ধরো:

|A|G|
|---|---|
|5145-1|Technology|
|**5145-2**|**Office Supplies**|
|5145-3|Furniture|

`5145-2` পাওয়া গেছে 2nd data row-তে।

তাই একই row-এর G column থেকে result:

```
Office Supplies
```

---

# পুরো formula-এর বাংলা অর্থ

```
=XLOOKUP($A$2,'Sheet-1'!$A$2:$A$382,'Sheet-1'!G2:G382)
```

মানে:

> **A2-তে যে Order No আছে, সেটা Sheet-1-এর A2:A382-এর মধ্যে খুঁজো। যেই row-তে Order No পাওয়া যাবে, সেই row-এর G column-এর value আমাকে দেখাও।**

---

## কিন্তু একটা গুরুত্বপূর্ণ ব্যাপার 👇

তোমার screenshot-এ **G2**-তে formula আছে:

```
=XLOOKUP($A$2,'Sheet-1'!$A$2:$A$382,'Sheet-1'!G2:G382)
```

এখন তুমি যদি এই formula **B2 থেকে G2 পর্যন্ত copy করতে চাও**, তাহলে formula-টা এভাবে লেখা ভালো:

```
=XLOOKUP($A$2,'Sheet-1'!$A$2:$A$382,'Sheet-1'!B$2:B$382)
```

তারপর **ডানদিকে drag** করলে:

```
B2 → B column থেকে Order Date
C2 → C column থেকে City
D2 → D column থেকে Account Manager
E2 → E column থেকে Order Priority
F2 → F column থেকে Product Name
G2 → G column থেকে Product Category
```

কারণ এখানে `B$2:B$382`-এর **B column relative**, তাই ডানে drag করলে সেটা C, D, E, F, G হয়ে যাবে।

### ফলে:

```
A2 = 5145-2

B2 → 29-06-13
C2 → Dhaka
D2 → Tabassum Khan
E2 → Low
F2 → Artisan Hi-Liter Smear-Safe Highlight...
G2 → Office Supplies
```

**সহজভাবে মনে রাখো:**

> **XLOOKUP = "এই জিনিসটা খুঁজে, তার সাথে সম্পর্কিত অন্য তথ্যটা নিয়ে আসো।"**

এখানে **5145-2 খুঁজছে**, আর তার corresponding **Office Supplies** নিয়ে আসছে।

----


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

| Employee | Department |
| -------- | ---------- |
| Rahim    | IT         |
| Karim    | HR         |
| Hasan    | IT         |
| Jony     | Sales      |
| Sakib    | IT         |

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

| Employee | City       |
| -------- | ---------- |
| Rahim    | Dhaka      |
| Karim    | Chittagong |
| Hasan    | Dhaka      |
| Jony     | Sylhet     |
| Sakib    | Dhaka      |

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

| Student | Marks |
| ------- | ----: |
| Rahim   |    80 |
| Karim   |    35 |
| Hasan   |    65 |
| Jony    |    45 |
| Sakib   |    90 |

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

| Employee | Department | Salary |
| -------- | ---------- | -----: |
| Rahim    | IT         |  30000 |
| Karim    | HR         |  35000 |
| Hasan    | IT         |  40000 |
| Jony     | Sales      |  28000 |
| Sakib    | IT         |  45000 |

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

| Product | Category    | Sales |
| ------- | ----------- | ----: |
| Laptop  | Electronics | 80000 |
| Shirt   | Clothing    |  3000 |
| Mouse   | Electronics |  1000 |
| Pant    | Clothing    |  2500 |
| Monitor | Electronics | 20000 |

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

| Employee | Department | City       | Salary |
| -------- | ---------- | ---------- | -----: |
| Rahim    | IT         | Dhaka      |  30000 |
| Karim    | HR         | Dhaka      |  35000 |
| Hasan    | IT         | Chittagong |  40000 |
| Jony     | Sales      | Dhaka      |  28000 |
| Sakib    | IT         | Dhaka      |  45000 |

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






 