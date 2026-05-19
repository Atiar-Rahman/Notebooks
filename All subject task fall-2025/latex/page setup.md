
# 🟦 **1. Document Class (Base Page Setup)**

```latex
\documentclass[options]{article}
```

### Common Options

|Option|Meaning|
|---|---|
|`a4paper`, `letterpaper`|পেজ সাইজ|
|`12pt`, `11pt`, `10pt`|ফন্ট সাইজ|
|`oneside`, `twoside`|সিঙ্গেল/ডাবল সাইড|
|`onecolumn`, `twocolumn`|কলাম সংখ্যা|
|`draft`|ড্রাফট মোড (ওভারফুল বক্স দেখায়)|

**Example:**

```latex
\documentclass[a4paper,12pt,oneside]{article}
```

---

# 🟦 **2. Geometry Package (Page Margin Control)**

সর্বাধিক জনপ্রিয় প্যাকেজ → `geometry`

```latex
\usepackage[
    a4paper,
    margin=1in
]{geometry}
```

### Useful Parameters

|Parameter|Meaning|
|---|---|
|`margin=1in`|সব পাশে ১ ইঞ্চি|
|`left=`, `right=`, `top=`, `bottom=`|আলাদা আলাদা মার্জিন|
|`includehead`, `includefoot`|হেডার/ফুটার মার্জিনে যোগ|
|`heightrounded`|height রাউন্ড করে|

**Example:**

```latex
\usepackage[left=2cm, right=2cm, top=1cm, bottom=2cm]{geometry}
```

---

# 🟦 **3. Page Dimensions (Without Geometry)**

LaTeX নেটিভ কমান্ড:

```latex
\setlength{\textwidth}{6.5in}      % Text width
\setlength{\textheight}{9in}       % Text height
\setlength{\oddsidemargin}{0in}    % Left margin (odd pages)
\setlength{\evensidemargin}{0in}   % Right margin (even pages)
\setlength{\topmargin}{-0.5in}     % Top margin
\setlength{\headheight}{12pt}      % Header height
\setlength{\headsep}{25pt}         % Header to text distance
\setlength{\footskip}{30pt}        % Footer position
```

---

# 🟦 **4. Page Numbering**

```latex
\pagenumbering{arabic}   % 1,2,3
\pagenumbering{roman}    % i,ii,iii
\pagenumbering{Roman}    % I, II, III
\pagenumbering{alph}     % a,b,c
\pagenumbering{Alph}     % A,B,C
```

**Start numbering from another page:**

```latex
\setcounter{page}{5}
```

---

# 🟦 **5. Header & Footer Setup** (`fancyhdr`)

```latex
\usepackage{fancyhdr}
\pagestyle{fancy}

\fancyhf{}               % clear all
\fancyhead[L]{My Title}  % left header
\fancyhead[R]{\thepage}  % right header
\fancyfoot[C]{Footer}    % center footer
```

---

# 🟦 **6. Line Spacing** (`setspace`)

```latex
\usepackage{setspace}

\singlespacing
\onehalfspacing
\doublespacing

% Specific part
\begin{spacing}{1.3}
This paragraph has 1.3 line spacing.
\end{spacing}
```

---

# 🟦 **7. Paragraph Setup**

```latex
\setlength{\parindent}{0pt}    % No indentation
\setlength{\parskip}{6pt}      % Space between paragraphs
```

---

# 🟦 **8. Page Break Controls**

```latex
\newpage        % Force new page
\clearpage      % Clear floats then new page
\pagebreak      % Page break with flexibility
\nopagebreak    % Prevent page break
```

---

# 🟦 **9. Page Style**

```latex
\pagestyle{empty}     % No page numbers
\pagestyle{plain}     % Default
\pagestyle{headings}  % Section name in header
\pagestyle{fancy}     % Using fancyhdr
```

---

# 🟦 **10. Landscape Page**

```latex
\usepackage{lscape}         % Temporary landscape
\begin{landscape}
Your content
\end{landscape}
```

Permanent landscape:

```latex
\documentclass[landscape]{article}
```

---

# 🟦 **11. Title Page Setup**

```latex
\begin{titlepage}
\centering
{\Huge My Report Title \par}
{\large Author Name \par}
\vfill
{\large \today \par}
\end{titlepage}
```

---

# 🟦 **12. Columns (Multi-column Page)**

```latex
\usepackage{multicol}
\begin{multicols}{2}
Your text here...
\end{multicols}
```

---

# 🟦 **13. Adjust Page Background (Color/Image)**

### Background Color

```latex
\usepackage{xcolor}
\pagecolor{gray!10}
```

### Background Image

```latex
\usepackage{wallpaper}
\CenterWallPaper{0.3}{background.jpg}
```

---

# 🟦 **14. Section Spacing**

```latex
\usepackage{titlesec}
\titlespacing*{\section}{0pt}{10pt}{4pt}
\titlespacing*{\subsection}{0pt}{8pt}{3pt}
```

---

# 🟦 **15. Custom Page Size**

```latex
\usepackage{geometry}
\geometry{
  paperwidth=7in,
  paperheight=10in,
  margin=1in
}
```

---

# 🟦 **16. Adjust Float Placement (Tables/Images)**

```latex
\usepackage{float}
\begin{figure}[H]
    \centering
    \includegraphics{img.png}
\end{figure}
```

---

# 🟦 **17. Full Page (No Margins)**

```latex
\usepackage[margin=0cm]{geometry}
```

---

# 🟦 **18. Page Color & Text Color**

```latex
\pagecolor{black}
\color{white}
```

---

# 🟦 **19. First Page Different Header/Footer**

```latex
\thispagestyle{empty}
```

---

# 🟦 **20. Custom Footnote Setup**

```latex
\setlength{\footskip}{20pt}
```

---

# ✅ চাইলে আমি একটি **Full Page Setup Template** ও বানিয়ে দিতে পারি

👉 শুধু বলুন: **“Give full page setup template”**

অথবা চাইলে বললে আমি **Overleaf ready full template** বানিয়ে দেবো!