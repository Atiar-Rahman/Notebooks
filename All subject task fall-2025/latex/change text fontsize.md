LaTeX-এ font size পরিবর্তন করার **দুটি উপায়** আছে:

---

# ✅ **1. পুরো ডকুমেন্টের ফন্ট সাইজ পরিবর্তন (Global Font Size)**

`documentclass` এ সাইজ সেট করা হয়:

```latex
\documentclass[12pt]{article}
```

অপশনসমূহ:

- `10pt` (default)
    
- `11pt`
    
- `12pt`
    

---

# ✅ **2. নির্দিষ্ট জায়গার ফন্ট সাইজ পরিবর্তন (Local Font Size)**

এই কমান্ডগুলো লাইনের শুরুতে লিখলেই ওই অংশের ফন্ট সাইজ পরিবর্তন হবে।

|Command|Size|
|---|---|
|`\tiny`|খুব ছোট|
|`\scriptsize`|ছোট|
|`\footnotesize`|নোট সাইজ|
|`\small`|একটু ছোট|
|`\normalsize`|Normal|
|`\large`|একটু বড়|
|`\Large`|বড়|
|`\LARGE`|বড়|
|`\huge`|খুব বড়|
|`\Huge`|অনেক বড়|

---

# ✨ **Example: Local font size**

```latex
This is normal text.

{\large This text is large.}

{\Huge This is HUGE text.}

{\small This text is small.}
```

> **Note:** `{ ... }` ব্যবহার করলে শুধু এই ব্লকের ভেতরেই সাইজ পরিবর্তন হবে।

---

# 📌 **3. Paragraph বা Section-এর Font Size পরিবর্তন**

```latex
{\Large \section*{Big Section Title}}
```

---

# 📌 **4. Custom Font Size (exact size)**

যদি নির্দিষ্ট করে px বা pt দিতে চান:

```latex
{\fontsize{14pt}{16pt}\selectfont
This is custom size text.
}
```

---


Here is a **full, clean, beginner-friendly LaTeX example file** showing **all font size commands**, including global font size, local changes, section sizes, and custom font sizing.

You can copy–paste directly into **Overleaf**.

---

# ✅ **Full Example LaTeX File (All Font Size Examples)**

```latex
\documentclass[12pt]{article}  % Global font size (10pt, 11pt, 12pt)

% Packages
\usepackage[utf8]{inputenc}
\usepackage{lipsum}   % Dummy text

\begin{document}

\section*{Global Font Size}
This entire document uses the global font size set in:
\texttt{\textbackslash documentclass[12pt]\{article\}}.

\section*{Local Font Size Commands}

{\tiny This is tiny text.}

{\scriptsize This is scriptsize text.}

{\footnotesize This is footnotesize text.}

{\small This is small text.}

{\normalsize This is normal text.}

{\large This is large text.}

{\Large This is Large text.}

{\LARGE This is LARGE text.}

{\huge This is huge text.}

{\Huge This is Huge text.}

\section*{Mixed Example Inside a Paragraph}

This paragraph uses normal text, but here is {\Large slightly bigger text}, 
and here is {\small smaller text}. Finally, here is {\Huge VERY BIG text} in the same line.

\section*{Custom Font Size (Exact Point Size)}

{\fontsize{16pt}{18pt}\selectfont
This text uses a custom size: 16pt font with 18pt line spacing.
}

{\fontsize{8pt}{10pt}\selectfont
This is a custom very-small text block using 8pt font.
}

\section*{Font Size Example With Lipsum Text}

% Normal
\normalsize
\lipsum[1]

% Large
{\Large
\lipsum[1]
}

% Huge
{\Huge
\lipsum[1]
}

\end{document}
```

---

# ✅ এই উদাহরণে আপনি পাবেন

✔ Global font size  
✔ Local font size commands  
✔ Section title resizing  
✔ Mixed font sizes in same line  
✔ Exact custom size (`\fontsize{..}{..}\selectfont`)  
✔ Paragraph examples with real text

---
