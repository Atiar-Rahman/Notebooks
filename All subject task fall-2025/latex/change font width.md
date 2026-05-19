LaTeX-এ **font width (weight)** বলতে বোঝায় — **bold**, **medium**, **light**, **ultralight**, **semibold** ইত্যাদি।  
ডিফল্ট `article` বা `report` ক্লাসে শুধু ২টি weight থাকে:

- **Normal**
    
- **Bold** → `\textbf{...}`
    

যদি আপনি **thin / light / semibold / heavy** ইত্যাদি চান, তাহলে **font package** ব্যবহার করতে হবে।

---

# ✅ 1. Default LaTeX: Normal + Bold

```latex
\textbf{This is bold text.}
\textmd{Medium text (default).}
```

---

# ✅ 2. More Font Weights (Recommended package → `lmodern`)

```latex
\usepackage{lmodern}
\usepackage[T1]{fontenc}
```

তারপর:

```latex
\textbf{Bold text}
\textnormal{Normal text}
\textmd{Medium text}
```

**Note:** Still only normal + bold available.

---

# ✅ 3. Professional Font Weights → Using `\usepackage[sfdefault]{roboto}`

This gives **Thin to Black** fonts.

```latex
\usepackage[sfdefault]{roboto}
```

Now you can use:

```latex
{\fontseries{ultralight}\selectfont Ultra Light Text}

{\fontseries{light}\selectfont Light Text}

{\fontseries{medium}\selectfont Medium Text}

{\fontseries{sb}\selectfont Semi Bold Text}

{\fontseries{b}\selectfont Bold Text}

{\fontseries{black}\selectfont Black (extra bold) Text}
```

---

# 🎯 4. Universal Method → `\fontseries{}`

If the font supports different widths:

```latex
{\fontseries{l}\selectfont Light}
{\fontseries{m}\selectfont Medium}
{\fontseries{b}\selectfont Bold}
{\fontseries{bx}\selectfont Extra Bold}
```

---

# 📌 Full Example LaTeX File (with multiple font widths)

```latex
\documentclass{article}
\usepackage[T1]{fontenc}
\usepackage[sfdefault]{roboto}  % use Roboto font
\usepackage{lipsum}

\begin{document}

{\fontseries{ultralight}\selectfont
UltraLight font weight example.
}

{\fontseries{light}\selectfont
Light font weight example.
}

{\fontseries{m}\selectfont
Medium font weight example.
}

{\fontseries{sb}\selectfont
SemiBold font weight example.
}

{\fontseries{b}\selectfont
Bold font example.
}

{\fontseries{black}\selectfont
Black / Extra bold font weight example.
}

\end{document}
```

---

# ⭐ Summary: How to Change Font Width

|Width|Command|
|---|---|
|Thin/Ultra Light|`\fontseries{ultralight}\selectfont`|
|Light|`\fontseries{light}\selectfont`|
|Medium (default)|`\fontseries{m}\selectfont`|
|Semi Bold|`\fontseries{sb}\selectfont`|
|Bold|`\fontseries{b}\selectfont`|
|Extra Bold / Black|`\fontseries{black}\selectfont`|

---

আপনি চাইলে আমি আপনাকে  
📌 Sans-serif (Roboto),  
📌 Serif (Times),  
📌 Monospace (Inconsolata)  
সবগুলোর font weight examples সহ complete template বানিয়ে দিতে পারি।



-------
# LaTeX-এ **font family** পরিবর্তন করার বেশ কয়েকটি উপায় আছে। নিচে **beginner → advanced** সব পদ্ধতি সহজ ভাষায় দেওয়া হলো।

---

# ✅ **1. Built-in Font Families**

LaTeX-এ ৩টি default font family আছে:

### ✔ Serif (Default)

```latex
{\rmfamily This is serif font.}
```

### ✔ Sans-serif

```latex
{\sffamily This is sans-serif font.}
```

### ✔ Monospace

```latex
{\ttfamily This is monospace font.}
```

---

# ✅ **2. Set a font family for the whole document**

### ▶ Option A: Entire document in sans-serif

```latex
\renewcommand{\familydefault}{\sfdefault}
```

### ▶ Option B: Entire document in monospace

```latex
\renewcommand{\familydefault}{\ttdefault}
```

---

# ✅ **3. Using Popular Fonts (Recommended)**

এগুলো দেখতে সুন্দর ও আধুনিক—Overleaf-এ সব কাজ করে।

## ⭐ Roboto (Sans-serif)

```latex
\usepackage[sfdefault]{roboto}
```

## ⭐ Times New Roman

```latex
\usepackage{newtxtext,newtxmath}
```

## ⭐ Helvetica

```latex
\usepackage{helvet}
\renewcommand{\familydefault}{\sfdefault}
```

## ⭐ Latin Modern Roman (Better default)

```latex
\usepackage{lmodern}
```

## ⭐ Inconsolata (Beautiful monospace)

```latex
\usepackage{inconsolata}
```

---

# ✅ **4. Locally change font family (only specific text)**

### Serif:

```latex
{\rmfamily This part is serif.}
```

### Sans-serif:

```latex
{\sffamily This part is sans-serif.}
```

### Monospace:

```latex
{\ttfamily This is monospace.}
```

### Custom Font (e.g., Roboto)

```latex
{\fontfamily{Roboto-Regular}\selectfont Custom Roboto text.}
```

_(Works only if font supports it)_

---

# ✅ **5. Full Example LaTeX (All font families)**

```latex
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage{lmodern}       % Better default fonts
\usepackage[T1]{fontenc}
\usepackage{roboto}        % Extra font example
\usepackage{inconsolata}   % monospace

\begin{document}

\section*{Default Serif}
This uses the default serif font.

\section*{Sans-serif}
{\sffamily This paragraph uses sans-serif font.}

\section*{Monospace}
{\ttfamily This text is monospace like code.}

\section*{Roboto Font}
{\fontfamily{Roboto-Regular}\selectfont
This paragraph uses Roboto font family.
}

\section*{Inconsolata Font}
{\fontfamily{zi4}\selectfont
This uses Inconsolata monospace font.
}

\end{document}
```

---

# ⭐ Want something special?

আমি আপনাকে নিচের মতো templates বানিয়ে দিতে পারি:  
📌 Full document with Times New Roman  
📌 Full document with Sans-serif (professional style)  
📌 Heading different font + body different font  
📌 Resume template with custom fonts

Just tell me!