LaTeX-এ **text color পরিবর্তন** করতে `xcolor` প্যাকেজ ব্যবহার করা হয়।

---

# ✅ **Step 1: Add xcolor package**

```latex
\usepackage{xcolor}
```

---

# ✅ **1. Single word or short text color**

```latex
\textcolor{red}{This is red text.}
\textcolor{blue}{This is blue text.}
\textcolor{green}{This is green text.}
```

---

# ✅ **2. Whole paragraph color**

```latex
{\color{purple}
This entire paragraph is purple in color.
You can color many lines inside this block.
}
```

---

# ✅ **3. Custom RGB color**

```latex
\definecolor{mycolor}{RGB}{10, 120, 180}
\textcolor{mycolor}{This is custom RGB color text.}
```

---

# ✅ **4. Custom HTML HEX color**

```latex
\definecolor{darkred}{HTML}{CC0000}
\textcolor{darkred}{This is HEX color text.}
```

---

# 🎨 **Available Built-in Colors**

Common built-in colors you can use:

```
red, blue, green, yellow, black, white,
gray, darkgray, lightgray,
orange, violet, purple, brown, cyan, magenta
```

---

# 📌 **Full Example LaTeX File**

```latex
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage{xcolor}

\begin{document}

\section*{Basic Colors}
This is normal text.

\textcolor{red}{This text is red.}

\textcolor{blue}{This text is blue.}

\textcolor{green}{This text is green.}

\section*{Paragraph Color}
{\color{purple}
This whole paragraph is purple and spans multiple lines.
}

\section*{Custom RGB Color}
\definecolor{skyblue}{RGB}{80,150,255}
\textcolor{skyblue}{This text uses a custom RGB color.}

\section*{HEX Color}
\definecolor{darkred}{HTML}{BB0000}
\textcolor{darkred}{This text uses a custom HEX color.}

\end{document}
```

---

চাইলে আমি আপনাকে **colored boxes, background color, highlighted text, framed box** সব কিছু উদাহরণ সহ দিতে পারি।