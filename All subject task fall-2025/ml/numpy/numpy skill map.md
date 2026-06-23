If you want **100% practical NumPy knowledge** so you can handle almost any NumPy operation in Data Science / ML, focus on these topics in order:

# NumPy Complete Topic Roadmap

## 1. NumPy Fundamentals (Must)

- Installing NumPy
    
- Importing NumPy
    
- `np.array()`
    
- Array creation
    
    - `zeros()`
        
    - `ones()`
        
    - `full()`
        
    - `arange()`
        
    - `linspace()`
        
    - `eye()`
        
- Data types (`dtype`)
    
- `shape`
    
- `size`
    
- `ndim`
    

---

# 2. Indexing & Slicing (Very Important)

Learn:

- 1D indexing
    
- 2D indexing
    
- 3D indexing
    
- Negative indexing
    
- Slicing
    
- Step slicing
    

Examples:

```python
a[2]
a[1:5]
a[:,0]
a[0,:]
```

---

# 3. Array Manipulation (Core Skill)

Learn:

- `reshape()`
    
- `resize()`
    
- `flatten()`
    
- `ravel()`
    
- `transpose()`
    
- `.T`
    
- `swapaxes()`
    
- `expand_dims()`
    
- `squeeze()`
    

---

# 4. Array Joining & Splitting

Learn:

Joining:

- `concatenate()`
    
- `stack()`
    
- `vstack()`
    
- `hstack()`
    
- `dstack()`
    

Splitting:

- `split()`
    
- `hsplit()`
    
- `vsplit()`
    

---

# 5. Mathematical Operations

Learn:

Basic:

- `+`
    
- `-`
    
- `*`
    
- `/`
    
- `//`
    
- `%`
    
- `**`
    

Functions:

- `np.add`
    
- `np.subtract`
    
- `np.multiply`
    
- `np.divide`
    
- `np.power`
    

---

# 6. Universal Functions (ufunc) ⭐

Very important.

Learn:

Math:

- `sqrt()`
    
- `exp()`
    
- `log()`
    
- `sin()`
    
- `cos()`
    
- `tan()`
    

Rounding:

- `round()`
    
- `floor()`
    
- `ceil()`
    

---

# 7. Broadcasting ⭐⭐⭐

Master this.

Topics:

- Scalar broadcasting
    
- Row broadcasting
    
- Column broadcasting
    
- Shape compatibility rules
    

Example:

```python
A + B
```

when shapes differ.

---

# 8. Aggregation Functions

Learn:

- `sum()`
    
- `mean()`
    
- `median()`
    
- `min()`
    
- `max()`
    
- `std()`
    
- `var()`
    
- `prod()`
    

With:

```python
axis=0
axis=1
```

---

# 9. Conditional Operations ⭐⭐⭐

Learn:

- Boolean masking
    
- Filtering
    
- `where()`
    
- `select()`
    
- `any()`
    
- `all()`
    

Example:

```python
a[a>10]

np.where(a>10)
```

---

# 10. Sorting & Searching

Learn:

Sorting:

- `sort()`
    
- `argsort()`
    

Searching:

- `where()`
    
- `searchsorted()`
    

Unique:

- `unique()`
    

---

# 11. Random Module ⭐⭐

Learn:

Generation:

- `rand()`
    
- `randn()`
    
- `randint()`
    

Sampling:

- `choice()`
    
- `shuffle()`
    
- `permutation()`
    

Control:

- `seed()`
    

---

# 12. Linear Algebra ⭐⭐⭐

Very important for ML.

Learn:

Matrix:

- Matrix multiplication `@`
    
- `dot()`
    

Solve:

- `inv()`
    
- `det()`
    
- `solve()`
    

Decomposition:

- Eigenvalues
    
- Eigenvectors
    

```python
np.linalg.eig()
```

---

# 13. Statistics

Learn:

- Mean
    
- Median
    
- Variance
    
- Standard deviation
    
- Percentile
    
- Correlation
    

Functions:

```python
np.corrcoef()
```

---

# 14. Copy vs View ⭐

Must know.

Learn:

- `copy()`
    
- `view()`
    

Difference:

Memory sharing.

---

# 15. File Handling

Learn:

Binary:

- `save()`
    
- `load()`
    

Text:

- `savetxt()`
    
- `loadtxt()`
    

CSV handling.

---

# 16. Data Type Handling

Learn:

Convert:

```python
astype()
```

Examples:

```python
int → float
float → int
```

---

# 17. Memory Optimization

Learn:

- dtype selection
    
- memory size
    
- avoiding copies
    
- vectorization
    

Example:

```python
np.int8
np.float32
```

---

# 18. Performance Optimization ⭐⭐⭐

Master:

- Vectorization
    
- Avoid loops
    
- Broadcasting
    
- Efficient indexing
    

Example:

Bad:

```python
for i in range(len(a)):
    a[i]*2
```

Good:

```python
a*2
```

---

# 19. Advanced Indexing

Learn:

Integer indexing:

```python
a[[1,3,5]]
```

Boolean indexing:

```python
a[a>5]
```

---

# 20. Structured Arrays

Learn:

Custom data:

```python
dtype=[
('name','U10'),
('age','i4')
]
```

---

# 21. NumPy + Pandas Connection

Learn:

Convert:

NumPy → Pandas

```python
pd.DataFrame(array)
```

Pandas → NumPy

```python
df.values
```

---

# 22. NumPy for Machine Learning

Must know:

- Feature scaling
    
- Normalization
    
- One-hot encoding
    
- Matrix operations
    
- Dataset preparation
    

---

# 23. Image Processing NumPy

Learn:

- Image as array
    
- Pixel manipulation
    
- RGB channels
    
- Masking
    

---

# 24. NumPy Internals (Advanced)

Learn:

- Memory layout
    
- C-order vs F-order
    
- Strides
    
- Broadcasting rules
    

---

## If you master these 24 topics:

You can handle:

✅ Data cleaning  
✅ Data analysis  
✅ Machine learning preprocessing  
✅ Neural network matrix operations  
✅ Image arrays  
✅ Scientific computing  
✅ Large datasets

A practical order:

**Beginner**  
→ 1,2,3,5,8,9

**Intermediate**  
→ 4,7,10,11,13,14,15

**Advanced**  
→ 12,17,18,19,22,23,24

This is basically the complete NumPy skill map.




---------------

