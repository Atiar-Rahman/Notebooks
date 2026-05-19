Here is the **A–Z simple and complete guide** on **how to create tables in LaTeX**, from beginner to advanced.

---

# ⭐ **How to Create a Table in LaTeX**

LaTeX tables are created using:

### ✔ `tabular` environment (basic table)

### ✔ `table` environment (floating table with caption)

---

# 🔹 **1. Basic Table Structure**

```latex
\begin{tabular}{|c|c|c|}
\hline
A & B & C \\ 
\hline
1 & 2 & 3 \\ 
\hline
\end{tabular}
```

### Output:

A simple 3-column table with borders.

---

# 🔹 **2. Column Alignment Options**

Inside `{ |c|c|c| }`:

|Symbol|Meaning|
|---|---|
|`l`|Left aligned column|
|`c`|Center aligned column|
|`r`|Right aligned column|
|`|`|

### Example:

```latex
\begin{tabular}{lcr}
Left & Center & Right \\
\end{tabular}
```

---

# 🔹 **3. Add Borders (`\hline`)**

```latex
\begin{tabular}{|l|c|r|}
\hline
Name & Age & Country \\ \hline
Atiar & 23 & Bangladesh \\ \hline
\end{tabular}
```

---

# 🔹 **4. Add Caption + Label (floating table)**

For proper placement & referencing:

```latex
\begin{table}[h]
\centering
\begin{tabular}{|c|c|}
\hline
ID & Score \\ \hline
1 & 95 \\ \hline
2 & 88 \\ \hline
\end{tabular}
\caption{Student Scores}
\label{tab:scores}
\end{table}
```

---

# 🔹 **5. Adjust Column Width (`p{}`)**

Useful for long text.

```latex
\begin{tabular}{|p{4cm}|p{6cm}|}
\hline
Title & Description \\ \hline
AI & Artificial intelligence is the simulation... \\ \hline
\end{tabular}
```

---

# 🔹 **6. Merge Columns (`\multicolumn`)**

```latex
\begin{tabular}{|c|c|c|}
\hline
\multicolumn{3}{|c|}{Student Info} \\ \hline
Name & Age & Grade \\ \hline
\end{tabular}
```

---

# 🔹 **7. Merge Rows (`multirow`)**

Requires package:

```latex
\usepackage{multirow}
```

Example:

```latex
\begin{tabular}{|c|c|}
\hline
\multirow{2}{*}{A} & X \\ \cline{2-2}
                   & Y \\ \hline
\end{tabular}
```

---

# 🔹 **8. Add Space Between Columns**

```latex
\setlength{\tabcolsep}{10pt}  % default 6pt
```

Add vertical row spacing:

```latex
\renewcommand{\arraystretch}{1.5}  % default 1.0
```

---

# 🔹 **9. Professional Table (booktabs package)**

Cleaner tables:

```latex
\usepackage{booktabs}

\begin{tabular}{lcr}
\toprule
Name & Age & Country \\ 
\midrule
Atiar & 23 & Bangladesh \\
Rahim & 22 & India \\
\bottomrule
\end{tabular}
```

---

# 🔹 **10. Full Example Table (Recommended Style)**

```latex
\begin{table}[h!]
\centering
\begin{tabular}{|l|c|r|}
\hline
Name & Age & Country \\ \hline
Atiar & 23 & Bangladesh \\ 
Rahim & 25 & India \\ 
Karim & 28 & Nepal \\ \hline
\end{tabular}
\caption{Sample Table}
\label{tab:sample}
\end{table}
```

---

# 📌 **Quick Summary**

|Feature|Command|
|---|---|
|Create table|`tabular`|
|Add caption|`table` environment|
|Column align|`l`, `c`, `r`|
|Row/column border|`\hline`, `|
|Merge columns|`\multicolumn{}`|
|Merge rows|`\multirow{}`|
|Table spacing|`\tabcolsep`, `\arraystretch`|
|Professional tables|`booktabs`|

---


# ⭐ **1. Full-Width Table (Basic Document: article/report/book)**

### ✔ Method 1: Use `\textwidth`

This is the simplest way.

```latex
\begin{table}[h!]
\centering
\begin{tabular}{|p{0.33\textwidth}|p{0.33\textwidth}|p{0.33\textwidth}|}
\hline
Column 1 & Column 2 & Column 3 \\ \hline
Long text example & More text & More content \\ \hline
\end{tabular}
\caption{Full width table using textwidth}
\end{table}
```

### 🔍 Why this works?

Each column is set to a percentage of the page width (`\textwidth`), so the whole table stretches across the page.

---

# ⭐ **2. Full-Width Table Using `tabularx` (Recommended)**

This produces **perfect auto-stretching full-width tables**.

### Add package:

```latex
\usepackage{tabularx}
```

### Table:

```latex
\begin{table}[h!]
\centering
\begin{tabularx}{\textwidth}{|X|X|X|}
\hline
Column 1 & Column 2 & Column 3 \\ \hline
Long text that wraps automatically & More text here & More content \\ \hline
\end{tabularx}
\caption{Full-width table with tabularx}
\end{table}
```

### ✔ Advantages:

- Automatically expands to full width
    
- Column width adjusts automatically
    
- Very clean and professional
    

---

# ⭐ **3. Full-Width Professional Table Using `tabu` (optional)**

```latex
\usepackage{tabu}
```

```latex
\begin{table}[h!]
\centering
\begin{tabu} to \textwidth {|X|X|X|}
\hline
Column 1 & Column 2 & Column 3 \\ \hline
\end{tabu}
\caption{Full-width table (tabu)}
\end{table}
```

---

# ⭐ **4. Full-Width Table in Two-Column Documents**

If you use:

```latex
\documentclass[twocolumn]{article}
```

Use `table*`:

```latex
\begin{table*}[t]
\centering
\begin{tabular}{|c|c|c|c|}
\hline
A & B & C & D \\ \hline
1 & 2 & 3 & 4 \\ \hline
\end{tabular}
\caption{Full-width table across both columns}
\end{table*}
```

---

# ⭐ **5. Full-Width Table With `booktabs` (professional style)**

```latex
\usepackage{booktabs, tabularx}
```

```latex
\begin{table}[h!]
\begin{tabularx}{\textwidth}{X X X}
\toprule
Name & Description & Value \\
\midrule
Item 1 & Long text that wraps & 10 \\
Item 2 & More long text & 20 \\
\bottomrule
\end{tabularx}
\caption{Professional full-width table}
\end{table}
```

---

# 📌 **Quick Summary — Best Choices**

|Goal|Best Method|
|---|---|
|Simple full width|`p{}` with percentages of `\textwidth`|
|Auto-adjusting full width|**tabularx**|
|Professional table|`booktabs + tabularx`|
|Two-column full width|`table*`|

---

