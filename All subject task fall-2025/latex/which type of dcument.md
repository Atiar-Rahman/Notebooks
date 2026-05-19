In LaTeX, **document classes** decide the overall **structure, formatting, and layout** of your document.  
You choose a document class at the **top of your LaTeX file** like this:

```latex
\documentclass{article}
```

Below is a complete explanation of the **most important document classes**, what they are used for, and when you should use them.

---

# 📘 **1. `article` (Most Common)**

### ✔ Used for:

- Assignments
    
- Reports (short)
    
- Essays
    
- Notes
    
- Journals
    
- Small books (< 30 pages)
    

### ✔ Features:

- NO chapters
    
- Uses: `\section`, `\subsection`, `\subsubsection`
    

### Example:

```latex
\documentclass{article}
```

---

# 📘 **2. `report` (For long documents)**

### ✔ Used for:

- University reports
    
- Theses
    
- Project documentation
    
- Lab reports
    

### ✔ Features:

- Supports **chapters**
    
- Good for 30+ page documents
    

### Example:

```latex
\documentclass{report}
```

You can write:

```latex
\chapter{Introduction}
```

---

# 📘 **3. `book` (For real books)**

### ✔ Used for:

- Textbooks
    
- Novels
    
- Research books
    
- Multi-chapter books
    

### ✔ Features:

- Chapters
    
- Front matter (preface) + back matter
    
- Left/right page formatting
    

### Example:

```latex
\documentclass{book}
```

---

# 📘 **4. `beamer` (For presentations)**

### ✔ Used for:

- Slides
    
- Conferences
    
- Class presentations
    

### ✔ Features:

- Creates PowerPoint-style slides
    

### Example:

```latex
\documentclass{beamer}
```

---

# 📘 **5. `letter` (For letters)**

### ✔ Used for:

- Writing professional letters
    

### Example:

```latex
\documentclass{letter}
```

---

# 📘 **6. `IEEEtran` (For IEEE research papers)**

### ✔ Used for:

- IEEE conference papers
    
- Research publications
    

### Example:

```latex
\documentclass[conference]{IEEEtran}
```

---

# 📘 **7. `memoir` (Advanced custom book/report class)**

### ✔ Used for:

- Custom books
    
- Fancy thesis formatting
    

More powerful than `book` or `report`.

---

# 📌 **Where do you put the document class?**

Always at the **very top** of your `.tex` file:

```latex
\documentclass{article}
\usepackage{graphicx}

\begin{document}

Hello world!

\end{document}
```

---
