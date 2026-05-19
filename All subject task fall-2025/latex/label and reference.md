LaTeX-এ **`\ref`**, **`\label`**, এবং **`\cite`** সবচেয়ে বেশি ব্যবহার হওয়া রেফারেন্সিং কমান্ড। নিচে সবকিছু খুব সহজভাবে ব্যাখ্যা করছি:

---

# ✅ **1. `\label` এবং `\ref` — Section, Figure, Table রেফারেন্স**

LaTeX-এ কোনো কিছু রেফার করতে চাইলে প্রথমে **`\label{}`** দিতে হয়, পরে **`\ref{}`** ব্যবহার করা হয়।

---

# 🟦 **(A) Section Reference**

```latex
\section{Introduction}\label{sec:intro}

In section \ref{sec:intro}, we discuss the basics.
```

👉 এখানে `\ref{sec:intro}` স্বয়ংক্রিয়ভাবে section number দেখাবে।  
যদি section = 1 হয়, আউটপুট হবে: **In section 1 ...**

---

# 🟦 **(B) Figure Reference**

```latex
\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\textwidth]{img.png}
    \caption{Sample Image}
    \label{fig:sample}
\end{figure}

Figure \ref{fig:sample} shows the result.
```

👉 আউটপুট → **Figure 1 shows the result.**

---

# 🟦 **(C) Table Reference**

```latex
\begin{table}[h]
\centering
\caption{Marks Table}
\label{tab:marks}
\begin{tabular}{c c}
Name & Marks \\
\hline
A & 90
\end{tabular}
\end{table}

Table \ref{tab:marks} provides the data.
```

---

# 🟦 **(D) Equation Reference**

```latex
\begin{equation}\label{eq:main}
E = mc^2
\end{equation}

From equation \ref{eq:main}, we get the relationship...
```

---

# ⭐ Important Tip

**Always put `\label` after `\caption`** (figure/table এ), না হলে numbering ভুল হবে।

---

# ✅ **2. `\pageref` — page number reference**

```latex
See page \pageref{sec:intro}.
```

→ আউটপুট: **See page 3** (যেখানে সেই section আছে)

---

# ✅ **3. `\nameref` — Section name reference**

`hyperref` package ব্যবহার করলে কাজ করবে:

```latex
\usepackage{hyperref}

\section{Methodology}\label{sec:method}

As discussed in \nameref{sec:method}...
```

→ আউটপুট: **As discussed in Methodology...**

---

# 🟦 `\ref` vs `\autoref` (Recommended)

`hyperref` প্যাকেজে `\autoref` অত্যন্ত সুবিধাজনক:

```latex
\usepackage{hyperref}

\autoref{fig:sample}
```

→ আউটপুট: **Figure 1** (automatic)

---

# 🟩 **4. Full Example (Everything Working Together)**

```latex
\documentclass{article}
\usepackage{graphicx}
\usepackage{hyperref}

\begin{document}

\section{Introduction}\label{sec:intro}
This is the introduction.

\section{Method}\label{sec:method}
Discussed in section \ref{sec:intro} on page \pageref{sec:intro}.

\begin{figure}[h]
    \centering
    \includegraphics[width=4cm]{sample.png}
    \caption{My Figure}
    \label{fig:myfig}
\end{figure}

Figure \ref{fig:myfig} is our sample figure.

\end{document}
```

---

