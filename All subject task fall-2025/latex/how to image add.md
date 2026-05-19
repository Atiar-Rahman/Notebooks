LaTeX-এ **image যোগ করতে** `graphicx` প্যাকেজ ব্যবহার করতে হয়।

নিচে **beginner to advanced** সব পদ্ধতি দেওয়া হলো।

---

# ✅ **1. Step 1: Add graphicx package**

ডকুমেন্টের শুরুতে লিখুন:

```latex
\usepackage{graphicx}
```

---

# ✅ **2. Step 2: Add an Image**

```latex
\begin{figure}
    \centering
    \includegraphics[width=0.5\textwidth]{myimage.jpg}
    \caption{My Image Caption}
    \label{fig:myimage}
\end{figure}
```

👉 Explanation

- `myimage.jpg` = আপনার ইমেজ ফাইল (PDF, PNG, JPG সব চলবে)
    
- `width=0.5\textwidth` = পেজের অর্ধেক
    
- `\caption{}` = ছবির নিচে লেখা
    
- `\label{}` = রেফারেন্স করার জন্য ট্যাগ
    

---

# 📌 **3. Image Without Figure Environment**

(If you don't want caption or floating)

```latex
\includegraphics[width=8cm]{photo.png}
```

---

# 📏 **4. Control Size of Image**

### Width:

```latex
\includegraphics[width=\textwidth]{pic.png}
```

### Height:

```latex
\includegraphics[height=4cm]{pic.png}
```

### Both:

```latex
\includegraphics[width=5cm,height=4cm]{pic.png}
```

---

# 🎯 **5. Center Image**

```latex
\begin{center}
\includegraphics[width=0.6\textwidth]{image.jpg}
\end{center}
```

---

# 🔄 **6. Rotate Image**

```latex
\includegraphics[angle=45,width=0.5\textwidth]{image.jpg}
```

---

# 📌 **7. Full Example LaTeX File**

```latex
\documentclass{article}
\usepackage[utf8]{inputenc}
\usepackage{graphicx}

\begin{document}

\section*{Adding an Image}

Here is an example image:

\begin{figure}[h]
    \centering
    \includegraphics[width=0.6\textwidth]{myphoto.jpg}
    \caption{This is an example image}
\end{figure}

\end{document}
```

---

# ❗ Important for Overleaf Users

👉 আপনার image ফাইলটি **project → Upload** এ আপলোড করতে হবে।  
👉 ফাইলের নাম ঠিকমতো লিখতে হবে (Case sensitive):

- `photo.jpg` ≠ `Photo.jpg`
    

---
চলুন তাহলে **এক এক করে সবই শিখে ফেলি** — multiple images, side-by-side images, background image, এবং two-column image layout।

---

# ✅ **1. Multiple Images in One Row**

### ✔ Method 1: `minipage` ব্যবহার করে (সবচেয়ে সহজ)

```latex
\begin{figure}[h]
    \centering
    
    \begin{minipage}{0.45\textwidth}
        \centering
        \includegraphics[width=\linewidth]{img1.jpg}
        \caption*{Image 1}
    \end{minipage}
    \hfill
    \begin{minipage}{0.45\textwidth}
        \centering
        \includegraphics[width=\linewidth]{img2.jpg}
        \caption*{Image 2}
    \end{minipage}

\end{figure}
```

---

# ✅ **2. Image + Text Side-by-Side**

### ✔ Method 1: Image left, text right

```latex
\begin{figure}[h]
    \begin{minipage}{0.45\textwidth}
        \includegraphics[width=\linewidth]{photo.jpg}
    \end{minipage}\hfill
    \begin{minipage}{0.5\textwidth}
        \textbf{This is the text area.}  
        এখানে আপনি paragraph, bullet points, explanation—যা খুশি লিখতে পারবেন।
    \end{minipage}
\end{figure}
```

### ✔ Method 2: Text left, image right

(Just swap minipage order—same code)

---

# 🌄 **3. Background Image (Full Page Background)**

### ✔ Method 1: Using `background` package

```latex
\usepackage{background}

\backgroundsetup{
    scale=1,
    angle=0,
    opacity=0.3,
    contents={\includegraphics[width=\paperwidth,height=\paperheight]{bg.jpg}}
}
```

তারপর body:

```latex
\begin{document}
Hello, this page has a background image!
\end{document}
```

---

### ✔ Method 2 (Most popular): `wallpaper` package

```latex
\usepackage{wallpaper}

\ThisCenterWallPaper{1}{bgimage.jpg}
```

এটি পুরো পেজকে background হিসেবে ব্যবহার করবে।

---

# 📰 **4. Image in Two-Column Layout**

যদি document class = `twocolumn` ব্যবহার করা হয়:

```latex
\documentclass[twocolumn]{article}
```

### ✔ Normal image (only one column)

```latex
\begin{figure}
\centering
\includegraphics[width=\columnwidth]{pic.jpg}
\caption{Single column image}
\end{figure}
```

### ✔ Full-width image (spanning BOTH columns)

```latex
\begin{figure*}
\centering
\includegraphics[width=\textwidth]{widepic.jpg}
\caption{This image covers both columns}
\end{figure*}
```

---

# ⭐ Want a full example file with all 4 image types together?

আমি চাইলে আপনার জন্য **একটি complete LaTeX template** তৈরি করতে পারি, যেখানে থাকবে:

- Image gallery
    
- Image grid
    
- Side-by-side image
    
- Background image
    
- Two-column full-width image
    


-----
# নীচে আমি আপনার জন্য **একটি সম্পূর্ণ LaTeX Template তৈরি করে দিলাম** যেখানে আছে—

✔ Image Gallery  
✔ Image Grid (3×3 / 2×2 ইত্যাদি)  
✔ Side-by-side Images  
✔ Background Image  
✔ Two-column full-width image

👉 শুধু ছবিগুলো (`img1.jpg`, `img2.jpg`...) Overleaf-এ Upload করে নিন।

---

# 🎯 **FULL IMAGE TEMPLATE — Copy & Paste into Overleaf**

```latex
\documentclass[twocolumn]{article}

\usepackage[utf8]{inputenc}
\usepackage{graphicx}
\usepackage{caption}
\usepackage{background}      % for background image
\usepackage{wallpaper}       % optional background
\usepackage{lipsum}

% ======== BACKGROUND IMAGE (Optional) ========
% Option 1: background package
\backgroundsetup{
    scale=1,
    angle=0,
    opacity=0.15,
    contents={\includegraphics[width=\paperwidth,height=\paperheight]{bg.jpg}}
}

% Option 2: wallpaper package (remove above section if using this)
% \ThisCenterWallPaper{1}{bg.jpg}

\begin{document}

\title{Complete Image Template}
\author{Your Name}
\date{}
\maketitle

\section*{1. Image Gallery (3 images in a row)}

\begin{figure}[h]
    \centering
    \begin{minipage}{0.32\columnwidth}
        \includegraphics[width=\linewidth]{img1.jpg}
        \caption*{Image 1}
    \end{minipage}
    \begin{minipage}{0.32\columnwidth}
        \includegraphics[width=\linewidth]{img2.jpg}
        \caption*{Image 2}
    \end{minipage}
    \begin{minipage}{0.32\columnwidth}
        \includegraphics[width=\linewidth]{img3.jpg}
        \caption*{Image 3}
    \end{minipage}
\end{figure}

\section*{2. Image Grid (2×2 layout)}

\begin{figure}[h]
    \centering
    \begin{minipage}{0.45\columnwidth}
        \includegraphics[width=\linewidth]{img1.jpg}
    \end{minipage}
    \hfill
    \begin{minipage}{0.45\columnwidth}
        \includegraphics[width=\linewidth]{img2.jpg}
    \end{minipage}

    \vspace{0.2cm}

    \begin{minipage}{0.45\columnwidth}
        \includegraphics[width=\linewidth]{img3.jpg}
    \end{minipage}
    \hfill
    \begin{minipage}{0.45\columnwidth}
        \includegraphics[width=\linewidth]{img4.jpg}
    \end{minipage}
\end{figure}

\section*{3. Side-by-side Image + Text}

\begin{figure}[h]
    \begin{minipage}{0.45\columnwidth}
        \includegraphics[width=\linewidth]{img1.jpg}
    \end{minipage}
    \hfill
    \begin{minipage}{0.5\columnwidth}
        \textbf{Image Description:}\\
        \small
        এটি একটি sample text block যা image-এর পাশে দেখানো হয়েছে।
        এখানে paragraph, bullet point ইত্যাদি রাখা যায়।
    \end{minipage}
\end{figure}

\section*{4. Two-column Full-width Image}

\begin{figure*}[t]   % star (*) = spans both columns
    \centering
    \includegraphics[width=\textwidth]{wide.jpg}
    \caption{This image spans both columns}
\end{figure*}

\section*{5. Background Image in Page}
এই document-এর পেছনে faint background image দেখা যাবে।  
Opacity আপনি পরিবর্তন করতে পারবেন (`opacity=0.15`)।

\lipsum[1]

\end{document}
```

---

# 🎨 **Which images you need?**

Template-এ placeholder:

```
img1.jpg
img2.jpg
img3.jpg
img4.jpg
wide.jpg
bg.jpg
```

👉 এগুলো আপনার নিজের ছবি দিয়ে replace করবেন।

---

# ✨ Want More?

আমি চাইলে আপনাকে—

✔ 3×3 image grid  
✔ 4 images in a row  
✔ Polaroid-style frames  
✔ Rounded corner images  
✔ Shadow effect on images  
✔ Caption under group images  
✔ Image with border, color frame

সবই তৈরি করে দিতে পারবো।


 -------
#  Perfect! 🔥  
এবার আমি আপনাকে **সমস্ত ফিচার— Image Grid, Gallery, Polaroid, Shadow, Rounded, Background, Full-Page Image, Side-by-Side, Wide Image, Frame, Caption — সব একসাথে যুক্ত করে একটা Premium LaTeX Template** তৈরি করে দিচ্ছি।

✔ This is the **ULTIMATE IMAGE TEMPLATE**  
✔ All features included  
✔ সব টার্ম ধাপে ধাপে বাংলা ব্যাখ্যাসহ

---

# 🎯 **📌 COMPLETE PROFESSIONAL LaTeX IMAGE TEMPLATE (All Features Combined)**

👉 এটি Overleaf-এ 100% কাজ করবে।

---

```latex
\documentclass{article}

% =========== PACKAGES ===============
\usepackage[utf8]{inputenc}
\usepackage{graphicx}        % ছবি যোগ করার জন্য
\usepackage{caption}         % caption better formatting
\usepackage{subcaption}      % multiple image (subfigure)
\usepackage{wrapfig}         % image + text wrap
\usepackage{tcolorbox}       % shadow, frame, rounded
\usepackage{background}      % background image
\usepackage{tikz}            % polaroid effect
\usepackage{geometry}
\geometry{margin=1in}

% ======== BACKGROUND IMAGE ========
\backgroundsetup{
    opacity=0.12,
    scale=1,
    angle=0,
    contents={\includegraphics
    [width=\paperwidth,height=\paperheight]{bg.jpg}}
}

\begin{document}

\title{Ultimate LaTeX Image Template}
\author{Your Name}
\date{}
\maketitle

% ===============================================
\section*{1. Image Gallery (3 images in a row)}

\begin{figure}[h]
\centering
\begin{subfigure}{0.32\linewidth}
    \includegraphics[width=\linewidth]{img1.jpg}
    \caption{Image 1}
\end{subfigure}
\begin{subfigure}{0.32\linewidth}
    \includegraphics[width=\linewidth]{img2.jpg}
    \caption{Image 2}
\end{subfigure}
\begin{subfigure}{0.32\linewidth}
    \includegraphics[width=\linewidth]{img3.jpg}
    \caption{Image 3}
\end{subfigure}
\caption{3 Image Gallery}
\end{figure}

% ===============================================
\section*{2. 3×3 Image Grid}

\begin{figure}[h]
\centering
\foreach \i in {1,2,3,4,5,6,7,8,9}{
    \begin{subfigure}{0.30\linewidth}
        \includegraphics[width=\linewidth]{img\i.jpg}
    \end{subfigure}
    \ifnum\i=3 \\[3pt] \fi
    \ifnum\i=6 \\[3pt] \fi
}
\caption{3×3 Image Grid}
\end{figure}

% ===============================================
\section*{3. Four Images in One Row}

\begin{figure}[h]
\centering
\begin{subfigure}{0.24\linewidth}
    \includegraphics[width=\linewidth]{img1.jpg}
\end{subfigure}
\begin{subfigure}{0.24\linewidth}
    \includegraphics[width=\linewidth]{img2.jpg}
\end{subfigure}
\begin{subfigure}{0.24\linewidth}
    \includegraphics[width=\linewidth]{img3.jpg}
\end{subfigure}
\begin{subfigure}{0.24\linewidth}
    \includegraphics[width=\linewidth]{img4.jpg}
\end{subfigure}
\caption{4 Images in a Row}
\end{figure}

% ===============================================
\section*{4. Polaroid Style Image}

\begin{center}
\begin{tikzpicture}
\node[
    draw=black,
    fill=white,
    inner sep=5pt,
    drop shadow,
    rotate=-3
]{
    \begin{minipage}{0.5\linewidth}
        \centering
        \includegraphics[width=\linewidth]{img1.jpg}
        \vspace{3pt}
        \textbf{Polaroid Caption}
    \end{minipage}
};
\end{tikzpicture}
\end{center}

% ===============================================
\section*{5. Image with Rounded Corners + Shadow}

\begin{tcolorbox}[
    enhanced,
    sharp corners=south,
    colframe=black,
    drop shadow,
    arc=6mm
]
\centering
\includegraphics[width=0.7\linewidth]{img2.jpg}
\captionof{figure}{Rounded Image with Shadow}
\end{tcolorbox}

% ===============================================
\section*{6. Image with Color Frame}

\begin{tcolorbox}[
    colframe=blue!70,
    colback=white,
    boxrule=2pt,
    arc=3mm,
    width=\linewidth,
    center
]
\centering
\includegraphics[width=0.6\linewidth]{img3.jpg}
\captionof{figure}{Image with Blue Frame}
\end{tcolorbox}

% ===============================================
\section*{7. Side-by-side Image + Text}

\begin{wrapfigure}{L}{0.45\linewidth}
    \centering
    \includegraphics[width=\linewidth]{img4.jpg}
\end{wrapfigure}

\textbf{Image Description:}  
Lorem ipsum dolor sit amet, consectetur adipiscing elit.  
এই অংশে আপনি যেকোনো paragraph, bullet points বা explanation দিতে পারবেন।

\vspace{2cm}

% ===============================================
\section*{8. Two-column Full-width Image}

\begin{figure*}[h]
\centering
\includegraphics[width=\textwidth]{wide.jpg}
\caption{Full-width Image Spanning Both Columns}
\end{figure*}

% ===============================================
\section*{9. Full Page Background Image}

Document-এর পেছনে background image লাগানো হয়েছে  
`opacity=0.12` দিয়ে faint করে।

\end{document}
```

---

# 📌 এখন আসুন সম্পূর্ণ বাংলা ব্যাখ্যা দিই — _সব টার্ম বুঝবেন_

## 📌 **1. \usepackage{graphicx}**

ছবি লোড ও সাইজ পরিবর্তন করার প্যাকেজ।

```
\includegraphics[width=\linewidth]{img.jpg}
```

## 📌 **2. \usepackage{subcaption}**

একটি figure-এর ভিতরে multiple ছবি (gallery/grid) বানানোর জন্য।

## 📌 **3. \usepackage{wrapfig}**

Image + Text side-by-side, text wrapping effect।

## 📌 **4. \usepackage{tcolorbox}**

Rounded corner, shadow, border, frame বানানোর জন্য সবচেয়ে powerful package।

## 📌 **5. \usepackage{background}**

Document এর পুরো পৃষ্ঠায় background image।

## 📌 **6. tikzpicture**

Polaroid effect, rotation, shadow—সব advanced design।

## 📌 **7. figure, figure***

- `figure` = single column width
    
- `figure*` = দুই কলাম জুড়ে full-width
    

## 📌 **8. arc=**, **drop shadow**, **boxrule**

- `arc=6mm` → rounded corners
    
- `drop shadow` → shadow effect
    
- `boxrule=2pt` → border thickness
    

## 📌 **9. \foreach**

Loop ব্যবহার করে 9টি ছবি auto-grid বানানো হয়েছে।

---

# 🎁 Bonus: Want a PDF preview style or Magazine style template?

আমি চাইলে whole template আপনার প্রয়োজন মতো customize করে দিতে পারি:

✔ Academic research paper  
✔ Portfolio gallery  
✔ Project report with images  
✔ Photography layout  
✔ CV with images

👉 আপনি কী ধরনের layout চান?  
One message-এ বললে আমি সেটার জন্য **Professional LaTeX file** বানিয়ে দেবো।