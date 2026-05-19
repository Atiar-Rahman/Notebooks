
```latex
\documentclass{article}

\begin{document}
\textbf{hello world}\hfill34534\hfill346768
\end{document}
```

Here is a **clear and simple explanation** of `\hfill` and `\vfill` in LaTeX, with examples you can remember easily.

---

# ⭐ `\hfill` and `\vfill` in LaTeX — Full Explanation

LaTeX gives you “stretchable space” commands, and these two are the most commonly used:

---

# 🟦 **1. `\hfill` — Horizontal Fill**

`\hfill` creates **flexible horizontal space** (left ↔ right).

It pushes content **as far apart as possible** on the **same line**.

### ✔ Example 1: Text on left and right

```latex
Name: Atiar \hfill Date: 21 Nov 2025
```

This will place:

- **“Name: Atiar”** on the _left_
    
- **“Date: 21 Nov 2025”** on the _right_
    

Like this:

```
Name: Atiar                                            Date: 21 Nov 2025
```

### ✔ Example 2: Center a text between two `\hfill`

```latex
\hfill Hello \hfill
```

This centers **Hello** in the line.

---

# 🟩 **2. `\vfill` — Vertical Fill**

`\vfill` creates **flexible vertical space** (top ↕ bottom).

It pushes content **toward top and bottom** on the **page**.

### ✔ Example: Text at top and bottom of page

```latex
This is top text
\vfill
This is bottom text
```

Output:

- “This is top text” goes **to the top**
    
- “This is bottom text” moves **to the bottom**
    

### ✔ Example: Center something vertically

```latex
\vfill
This text is vertically centered
\vfill
```

---

# 🎯 Summary Table

|Command|Direction|Purpose|Typical Use|
|---|---|---|---|
|`\hfill`|Horizontal|Push items apart left↔right|Title on left + date on right|
|`\vfill`|Vertical|Push items apart top↕bottom|Footer at bottom, vertical centering|

---

# ✔ When to Use

### Use **`\hfill`** when:

- You want content on the same line to spread apart
    
- You want something aligned right or centered
    

### Use **`\vfill`** when:

- You want content pushed down the page
    
- You want vertical centering
    

---

If you want, I can also create **visual diagrams** or a **mini LaTeX file** demonstrating both!