Here is **A–Z full explanation of LaTeX text alignment**, with all commands, environments, examples, and tips — everything in one place.

---

# ⭐ **LaTeX Text Alignment — Full Guide (A to Z)**

LaTeX supports **four basic text alignments**:

1. **Left**
    
2. **Right**
    
3. **Center**
    
4. **Justify (default)**
    

Additionally, several special alignment tools exist:

- `\raggedright`, `\raggedleft`, `\centering`
    
- `flushleft`, `flushright`, `center` environments
    
- Horizontal fill (`\hfill`)
    
- Vertical alignment (`\vfill`)
    
- Alignment inside tables, figures, minipages
    

Below is the complete explanation.

---

# 🔹 **1. Default Alignment (Justified Text)**

LaTeX automatically **justifies text** → stretches spacing so both left and right edges are aligned.

Example:

```latex
This is normal text. LaTeX will justify it automatically.
```

---

# 🔹 **2. Left Alignment**

### **Method 1: `\raggedright` (inline declaration)**

Does **not justify** the text. Leaves ragged right margin.

```latex
{\raggedright
This text is aligned left.
}
```

### **Method 2: `flushleft` environment**

```latex
\begin{flushleft}
This text is left-aligned.
\end{flushleft}
```

---

# 🔹 **3. Right Alignment**

### **Method 1: `\raggedleft`**

```latex
{\raggedleft
This text is right-aligned.
}
```

### **Method 2: `flushright` environment**

```latex
\begin{flushright}
Right aligned text here.
\end{flushright}
```

---

# 🔹 **4. Center Alignment**

### **Method 1: `\centering`**

```latex
{\centering
This text is centered.
}
```

### **Method 2: `center` environment**

```latex
\begin{center}
This text is centered.
\end{center}
```

---

# 🔹 **5. Inline horizontal alignment using `\hfill`**

`\hfill` pushes items far apart on the **same line**.

### Example: Left and right text

```latex
Left side text \hfill Right side text
```

### Example: Centering on a line

```latex
\hfill This is centered \hfill
```

---

# 🔹 **6. Vertical Alignment using `\vfill`**

`\vfill` pushes elements apart vertically.

### Top and bottom text:

```latex
Top text
\vfill
Bottom text
```

### Vertically centered text:

```latex
\vfill
Centered text
\vfill
```

---

# 🔹 **7. Alignment inside `minipage`**

A `minipage` has **its own alignment**.

```latex
\begin{minipage}{0.5\textwidth}
\raggedright
Left aligned text inside minipage.
\end{minipage}
```

---

# 🔹 **8. Alignment in Math Mode**

### Centered math (default)

```latex
\[
E = mc^2
\]
```

### Left-aligned math

```latex
\begin{flalign*}
E &= mc^2 &&
\end{flalign*}
```

### Right-aligned math

```latex
\begin{align*}
&& E = mc^2
\end{align*}
```

---

# 🔹 **9. Alignment in Tables**

Using column specifiers:

- `l` = left
    
- `c` = center
    
- `r` = right
    

Example:

```latex
\begin{tabular}{lcr}
Left & Center & Right \\
\end{tabular}
```

---

# 🔹 **10. Paragraph Alignment Commands**

You can set alignment for an entire section:

### Left:

```latex
\raggedright
```

### Center:

```latex
\centering
```

### Right:

```latex
\raggedleft
```

These apply until the group `{ ... }` ends.

---

# 🔹 **11. Page-Level Text Alignment**

Some classes or packages allow page-level alignment:

Use:

```latex
\usepackage{ragged2e}
```

Then:

### Justified:

```latex
\justifying
```

### Improved left alignment:

```latex
\RaggedRight
```

---

# 📌 **Quick Summary Table**

|Command / Env|Alignment|Notes|
|---|---|---|
|`\raggedright`|Left|Ragged right margin|
|`\raggedleft`|Right|Ragged left margin|
|`\centering`|Center|Inline|
|`flushleft`|Left|Environment|
|`flushright`|Right|Environment|
|`center`|Center|Environment|
|`\hfill`|Horizontal spacing|Spread items on same line|
|`\vfill`|Vertical spacing|Spread items on page|
|Table `l c r`|Alignment in tables|Column-wise|
|`minipage` + alignment|Mixed alignment|Local scope|

---

# 🎯 Want a full PDF example or Overleaf-ready template?

Just tell me — I can create a ready-to-use LaTeX file demonstrating **all alignment types**!