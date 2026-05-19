Below is the **most complete LaTeX command list for beginners → advanced**, organized with **explanations + examples**.  
You can keep this as your personal cheatsheet.

---

# 📘 **LaTeX Commands List (Beginner → Advanced)**

All important commands with simple explanations.

---

# 1️⃣ **Document Structure**

|Command|Meaning|Example|
|---|---|---|
|`\documentclass{}`|Sets document type|`\documentclass{article}`|
|`\begin{document} ... \end{document}`|Start & end document|—|
|`\title{}`|Document title|`\title{My Report}`|
|`\author{}`|Author name|`\author{Atiar}`|
|`\date{}`|Date|`\date{\today}`|
|`\maketitle`|Generates title page|—|
|`%`|Comment|`% This is comment`|

---

# 2️⃣ **Text Formatting**

|Command|Output|
|---|---|
|`\textbf{text}`|**Bold**|
|`\textit{text}`|_Italic_|
|`\underline{text}`|Underline|
|`\texttt{text}`|Monospace text|
|`\textcolor{red}{text}`|Colored text (needs `xcolor`)|
|`\Large`, `\huge`, `\small`|Text sizes|

---

# 3️⃣ **Sections / Headings**

```latex
\section{Introduction}
\subsection{Background}
\subsubsection{Details}
\paragraph{Title} Text...
```

---

# 4️⃣ **Line Breaks / Spacing**

|Command|Meaning|
|---|---|
|`\\`|New line|
|`\newline`|New line|
|`\vspace{1cm}`|Vertical space|
|`\hspace{1cm}`|Horizontal space|
|`\noindent`|Remove indentation|

---

# 5️⃣ **Lists**

### ✔ Bullet List

```latex
\begin{itemize}
  \item First item
  \item Second item
\end{itemize}
```

### ✔ Number List

```latex
\begin{enumerate}
  \item First
  \item Second
\end{enumerate}
```

---

# 6️⃣ **Math Mode**

### ✔ Inline Math:

`$a^2 + b^2 = c^2$`

### ✔ Display Math:

```latex
\[
E = mc^2
\]
```

### ✔ Common Math Commands

|Command|Meaning|
|---|---|
|`\frac{a}{b}`|Fraction|
|`\sqrt{x}`|Square root|
|`\sum_{i=1}^{n}`|Summation|
|`\int_a^b`|Integral|
|`\alpha, \beta, \gamma`|Greek letters|
|`a^{2}`, `b_{1}`|Superscript, subscript|
|`\pm, \times, \div`|Math symbols|

---

# 7️⃣ **Math Environments (Advanced)**

Requires:

```latex
\usepackage{amsmath}
```

### ✔ Align Equations

```latex
\begin{align}
a &= b + c \\
x &= y - z
\end{align}
```

### ✔ Cases

```latex
\begin{cases}
x^2 & x>0 \\
0 & \text{otherwise}
\end{cases}
```

### ✔ Matrices

```latex
\begin{bmatrix}
1 & 2 \\
3 & 4
\end{bmatrix}
```

---

# 8️⃣ **Tables**

```latex
\begin{tabular}{|c|c|c|}
\hline
A & B & C \\ \hline
1 & 2 & 3 \\ \hline
\end{tabular}
```

Add caption + label:

```latex
\begin{table}[h]
\centering
\caption{Sample Table}
\label{tab:sample}
\begin{tabular}{|c|c|}
\hline
X & Y \\
\hline
\end{tabular}
\end{table}
```

---

# 9️⃣ **Insert Images**

Requires:

```latex
\usepackage{graphicx}
```

### ✔ Image Command

```latex
\begin{figure}[h]
\centering
\includegraphics[width=0.5\textwidth]{image.png}
\caption{My image}
\label{fig:myimage}
\end{figure}
```

---

# 🔟 **Hyperlinks**

Requires:

```latex
\usepackage{hyperref}
```

```latex
\href{https://google.com}{Click Here}
\url{https://google.com}
```

---

# 1️⃣1️⃣ **Page Setup**

Package:

```latex
\usepackage{geometry}
```

### Example:

```latex
\geometry{margin=1in}
```

---

# 1️⃣2️⃣ **Custom Commands**

```latex
\newcommand{\R}{\mathbb{R}}     % Shortcut
\newcommand{\myname}{Md. Atiar} % Custom text
```

---

# 1️⃣3️⃣ **Bibliography (BibTeX)**

Main file:

```latex
This is cited: \cite{einstein}
\bibliographystyle{plain}
\bibliography{references}
```

`references.bib`:

```bibtex
@article{einstein,
  author = {Albert Einstein},
  title = {Relativity},
  year = {1905},
}
```

---

# 1️⃣4️⃣ **Boxes, Colors, Highlighting**

Requires:

```latex
\usepackage{xcolor}
```

### Colored box:

```latex
\colorbox{yellow}{Highlighted text}
```

---

# 1️⃣5️⃣ **Code Snippets**

Requires:

```latex
\usepackage{listings}
```

```latex
\begin{lstlisting}[language=Python]
print("Hello World")
\end{lstlisting}
```

---

# 1️⃣6️⃣ **Multi-file Projects**

```latex
\input{chapter1.tex}
\include{chapter2.tex}
```

---

# 1️⃣7️⃣ **Common Useful Packages**

|Package|Purpose|
|---|---|
|`amsmath`|Advanced math|
|`amssymb`|Math symbols|
|`graphicx`|Images|
|`hyperref`|Links|
|`geometry`|Page margin control|
|`xcolor`|Colors|
|`booktabs`|Professional tables|
|`fancyhdr`|Headers & footers|

---

To create a **new page in LaTeX**, you can use several commands depending on your need.

Here are the **3 most common ways**:

---

# ✅ **1. Force a New Page**

### Command:

```latex
\newpage
```

➡ Forces the content after this command to start on a **new page**.

---

# ✅ **2. Clear Page (Better for figures/tables)**

### Command:

```latex
\clearpage
```

➡ Starts a new page **and also prints all pending figures/tables**.

---

# ✅ **3. Page Break Suggestion**

### Command:

```latex
\pagebreak
```

➡ Requests a page break, but LaTeX may still decide based on formatting.

---

# 📝 Example:

```latex
This is page 1 text.

\newpage

This text starts on page 2.
```

---

# ⭐ Bonus: Start Chapter on New Page (Report/Book)

If you use `report` or `book` class, chapters automatically start on new page:

```latex
\chapter{Introduction}
```

---
Here’s the **correct way** to use `\pagebreak` and `\chapter{}` in LaTeX — plus the reason your example doesn’t work as expected.

---

# ✅ **Important Notes Before Fixing Your Code**

### ✔ `\chapter{}` works **only** in these document classes:

- `report`
    
- `book`
    

It does **not** work in `article`.

If you use `article`, use `\section{}` instead.

---

# ✅ **Correct Example (using report class)**

```latex
\documentclass{report}

\begin{document}

\pagebreak
This is my new page.

\chapter{Introduction}
CSS is Cascading Style Sheets.

\end{document}
```

✔ `\pagebreak` creates a new page  
✔ `\chapter{Introduction}` starts a chapter **on a new page automatically**  
✔ Your text appears correctly under the chapter

---

# ✅ **If you are using `article` class**

Use this instead:

```latex
\documentclass{article}

\begin{document}

\pagebreak
This is my new page.

\section{Introduction}
CSS is Cascading Style Sheets.

\end{document}
```

---

# 🔍 Why your example didn’t work?

Because:

- If your document class is `article`, `\chapter{}` is **undefined**.
    
- Also, text written directly after `\pagebreak` should be written as normal paragraphs.
    

---
