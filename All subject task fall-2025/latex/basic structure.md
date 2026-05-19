
In every LaTeX document, **commands must be written in the correct part of the document**.  
A LaTeX file has **two main parts**:

---

# 🟦 **1. Preamble (Before `\begin{document}`)**

This is the **setup area** where you define:

### ✔ Document Class

```latex
\documentclass{article}
```

### ✔ Packages

```latex
\usepackage{graphicx}
\usepackage{amsmath}
\usepackage{xcolor}
```

### ✔ Custom commands

```latex
\newcommand{\myname}{Atiar}
```

### ✔ Page settings

```latex
\geometry{margin=1in}
```

### ⚠ Important rule:

➡ **NO content or text is written in the preamble**  
➡ Only **settings, configuration, and imports**

---

# 🟦 **2. Document Body (Between `\begin{document}` and `\end{document}`)**

This is where you write your **actual content**, such as:

### ✔ Title

```latex
\maketitle
```

### ✔ Sections / Chapters

```latex
\section{Introduction}
\chapter{Overview} % only for report/book
```

### ✔ Paragraph text

```latex
This is my paragraph.
```

### ✔ Images

```latex
\includegraphics{image.png}
```

### ✔ Tables

```latex
\begin{tabular}{|c|c|}
\hline
A & B \\ \hline
\end{tabular}
```

### ✔ Math

```latex
\[
E = mc^2
\]
```

### ✔ Page breaks

```latex
\newpage
```

---

# 🧩 **FULL SIMPLE STRUCTURE**

Here is the correct LaTeX structure:

```latex
\documentclass{article}   % Preamble

% Packages (Preamble)
\usepackage{graphicx}
\usepackage{xcolor}
\usepackage{amsmath}

% Custom Commands (Preamble)
\newcommand{\myname}{Md. Atiar Rahman}

\begin{document}           % Start Document Body

\title{My First LaTeX Document}
\author{\myname}
\date{\today}
\maketitle

\section{Introduction}
This is my first section.

\newpage

\section{CSS}
CSS means Cascading Style Sheets.

\end{document}            % End Document Body
```

---

# 🎯 **Where to write what? (Quick Summary)**

|Part|What you write|
|---|---|
|**Preamble**|Document class, packages, settings, custom commands|
|**Body**|Content: text, sections, chapters, images, tables, math|

---


You can create **multiple columns** in LaTeX using a few different methods depending on what you need.  
Below are all the commonly used ways—from simple to advanced.

---

# ✅ **1. Easiest Way: `multicol` Package**

Use the `multicol` package:

```latex
\usepackage{multicol}
```

### ✔ Two Columns Example

```latex
\begin{multicols}{2}
This is column 1 and column 2 text.  
LaTeX will automatically balance columns.
\end{multicols}
```

### ✔ Three Columns Example

```latex
\begin{multicols}{3}
Your text here...
\end{multicols}
```

---

# ✅ **2. Newspaper-Style Columns (Entire Document)**

If you want the **whole document** in two columns, use:

```latex
\documentclass[twocolumn]{article}
```

### Example:

```latex
\documentclass[twocolumn]{article}

\begin{document}

This entire document will be in two columns.

\end{document}
```

---

# ✅ **3. Side-by-Side Content using `minipage`**

Useful if you want **images + text** side-by-side.

### Example:

```latex
\begin{minipage}{0.45\textwidth}
This is the left column.
\end{minipage}
\hfill
\begin{minipage}{0.45\textwidth}
This is the right column.
\end{minipage}
```

---

# ✅ **4. Two-Column Layout with Separation Line**

Add package:

```latex
\usepackage{multicol}
\setlength{\columnsep}{1cm}   % gap between columns
\setlength{\columnseprule}{0.4pt} % line between columns
```

Then:

```latex
\begin{multicols}{2}
Your text...
\end{multicols}
```

---

# 📌 Which method should YOU use?

|Goal|Best Method|
|---|---|
|Make only part of the document multi-column|`multicols` (best)|
|Full document 2-column style|`\documentclass[twocolumn]{article}`|
|Keep exact control (side-by-side images/text)|`minipage`|
|Newspaper/magazine layout|`multicol` with rules/gaps|

---



You can use **two or more columns** in LaTeX in **three different places**, depending on your purpose.  
Below I explain **where** and **when** to use multi-column layout.

---

# 🟦 **1. Entire Document in Two Columns**

Use this when your **whole paper** should be in two columns (like research papers).

### 📍 Where to put?

➡ **In the preamble** (top of the document)

```latex
\documentclass[twocolumn]{article}
```

### ✔ Best for:

- Research papers
    
- Conference papers
    
- Journals
    
- IEEE-style writing
    

---

# 🟦 **2. Only a Part of the Document in Columns**

Use this when you want **only specific sections** in two columns.

### 📍 Where to put?

➡ Put this **inside the document body**:

```latex
\usepackage{multicol}   % (in preamble)
```

Then in the document:

```latex
\begin{multicols}{2}
Your text here...
\end{multicols}
```

### ✔ Best for:

- Newspaper-style paragraphs
    
- Comparison content
    
- Multi-column notes
    
- Short texts with 2–3 columns
    

---

# 🟦 **3. Side-by-Side Elements (Text / Images / Tables)**

Use `minipage` when you want **custom columns** like:

- Two images side by side
    
- Text on left + image on right
    
- Two tables next to each other
    

### 📍 Where to put?

➡ These go **only inside the document body**.

Example:

```latex
\begin{minipage}{0.45\textwidth}
Left column content
\end{minipage}
\hfill
\begin{minipage}{0.45\textwidth}
Right column content
\end{minipage}
```

### ✔ Best for:

- Image + explanation
    
- Comparison tables
    
- Resume templates
    
- Custom layouts
    

---

# 🧩 **Summary: When & Where to Use Columns**

|Purpose|Where to Use|Command|
|---|---|---|
|Full document in columns|Preamble|`\documentclass[twocolumn]{article}`|
|Specific part in columns|Document body|`\begin{multicols}{2} ...`|
|Side-by-side content|Document body|`minipage`|

---

Ah! Now I understand exactly what you want:

- Your document is using `\documentclass[twocolumn]{article}`, which makes **everything two columns by default**.
    
- You want a **section in one column** **without starting a new page**.
    
- The problem: `\onecolumn` **always forces a page break** in LaTeX when using the `twocolumn` option.
    

✅ **Solution:** You **cannot use `\onecolumn`** for the same page in a `twocolumn` document. Instead, you should use the `multicol` package to manage **multiple columns manually**. This way, you can have **part two columns → part one column → part two columns** all **on the same page**.

---

# **Correct Way Using `multicol`**

```latex
\documentclass{article}
\usepackage{multicol}
\usepackage{lipsum} % for dummy text

\begin{document}

% -------------------------
% TOP: Two Columns
% -------------------------
\begin{multicols}{2}
Printers in the 1500s scrambled the words from Cicero's "De Finibus Bonorum et Malorum'' after mixing the words in each sentence. The familiar "lorem ipsum dolor sit amet" text emerged when 16th-century printers adapted Cicero's original work, beginning with the phrase "dolor sit amet consectetur."

They abbreviated "dolorem" (meaning "pain") to "lorem," which carries no meaning in Latin. "Ipsum" translates to "itself," and the text frequently includes phrases such as "consectetur adipiscing elit" and "ut labore et dolore." These Latin fragments, derived from Cicero's philosophical treatise, were rearranged to create the standard dummy text that has become a fundamental tool in design and typography across generations.
\end{multicols}

% -------------------------
% MIDDLE: One Column (same page)
% -------------------------
Text here will be ONE column. They abbreviated "dolorem" (meaning "pain") to "lorem," which carries no meaning in Latin. "Ipsum" translates to "itself," and the text frequently includes phrases such as "consectetur adipiscing elit" and "ut labore et dolore." These Latin fragments, derived from Cicero's philosophical treatise, were rearranged to create the standard dummy text that has become a fundamental tool in design and typography across generations.

% -------------------------
% BOTTOM: Two Columns again
% -------------------------
\begin{multicols}{2}
You can continue two-column text here. More content in two columns...
\end{multicols}

\end{document}
```

---

# **✅ Key Points**

1. Do **NOT** use `\onecolumn` inside a `twocolumn` document — it **forces a page break**.
    
2. Use the **`multicol` package**:
    
    - `\begin{multicols}{2} ... \end{multicols}` → two columns
        
    - Outside `multicols` → single column (full width)
        
3. You can repeat `multicols` multiple times in the same page for flexible layouts.
    

---

