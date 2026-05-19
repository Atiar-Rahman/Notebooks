Linear algebra is a core mathematical foundation for machine learning, as most datasets and models are represented using vectors and matrices. It allows efficient computation, data manipulation and optimization, making complex tasks manageable.

- Data in ML is represented as vectors (features) and matrices (datasets).
- Operations like dot product, matrix multiplication and transformations power ML algorithms.
- Key concepts such as eigenvalues, eigenvectors and decompositions simplify dimensionality reduction, optimization and training.
- Algorithms like PCA, SVD, regression, SVMs and neural networks rely heavily on linear algebra.

![vector_tensor.webp](https://media.geeksforgeeks.org/wp-content/uploads/20250820180052737722/vector_tensor.webp)![vector_tensor.webp](https://media.geeksforgeeks.org/wp-content/uploads/20250820180052737722/vector_tensor.webp)

## Fundamental Concepts in Linear Algebra for Machine Learning

In [machine learning](https://www.geeksforgeeks.org/machine-learning/ml-machine-learning/), ****vectors****, ****matrices**** and ****scalars**** play key roles in handling and processing data.

### ****1. Vectors****

Vectors are quantities that have both magnitude and direction, often represented as arrows in space.

v=[2−14]v=⎣⎡​2−14​⎦⎤​

### ****2. Matrices****

Matrices are rectangular arrays of [numbers,](https://www.geeksforgeeks.org/maths/sum-of-squares-of-natural-numbers/) arranged in rows and columns. Matrices are used to represent linear transformations, systems of linear equations and data transformations in machine learning.

****Example:**** [123456789]⎣⎡​147​258​369​⎦⎤​u = [3, 4] v = [-1, 2].

### 3. Scalars

Scalars are single numerical values, without direction, magnitude only. Scalars are just single numbers that can multiply vectors or matrices. In machine learning, they’re used to adjust things like the weights in a model or the learning rate during training

****Example:**** Let's consider a scalar, k= 3 and a vector [v=[2−14]][v=⎣⎡​2−14​⎦⎤​]  
Scalar multiplication involves multiplying each component of the vector by the scalar. So, if we multiply the vector v by the scalar k= 3 we get:  
k⋅v=3⋅[2−14]=[3⋅23⋅(−1)3⋅4]=[6−312]k⋅v=3⋅⎣⎡​2−14​⎦⎤​=⎣⎡​3⋅23⋅(−1)3⋅4​⎦⎤​=⎣⎡​6−312​⎦⎤​

## Operations in Linear Algebra

****Addition & Subtraction:**** Add or subtract corresponding elements of vectors/matrices.  
****Example:****  
u = [ 2, −1, 4], v = [ 3, 0, −2]  
u +v = [ 5, −1, 2], u −v = [ −1, −1, 6]

****Scalar Multiplication:**** Multiply each element by a scalar.  
****Example:**** 3⋅ [ 2, −1, 4] = [ 6, −3, 12]

****Dot Product:**** Measures similarity of directions by multiplying matching elements and summing.  
****Example:**** u⋅ v= u1v1+ u2v2+ u3v3

****Cross Product:**** For 3D vectors, produces a new vector perpendicular to both.  
****Example:**** u ×v = [u2v3− u3v2, u3v1 −u1v3, u1v2−u2v1 ]

## Linear Transformations

[Linear transformations](https://www.geeksforgeeks.org/digital-logic/piece-wise-linear-transformation/) are basic operations in linear algebra that change vectors and matrices while keeping important properties like straight lines and proportionality. In machine learning, they are key for tasks like preparing data, creating features and training models. This section covers the definition, types and uses of linear transformations.

****Definition****: A transformation T is linear if it satisfies:

- ****Additivity****: T(u+v) = T(u)+T(v)
- ****Homogeneity****: T(kv) = k T(v)

****Common Types in ML****

- ****Translation**** : Centering data by subtracting the mean.
- ****Scaling**** : Normalizing features so no single feature dominates.
- ****Rotation**** : Turning data, often used in computer vision and robotics.

## Matrix Operations

[Matrix operations](https://www.geeksforgeeks.org/maths/matrix-operations/) are central to linear algebra and widely used in machine learning for data handling, transformations and model training. The most common ones are:

- ****Matrix Multiplication:**** Combines two matrices by taking the dot product of rows and columns. Used in feature transformations, parameter computation and neural network operations.  
    ****Example:**** A=[2112],B=[3012],A×B=[7254]A=[21​12​],B=[31​02​],A×B=[75​24​]
- ****Transpose:**** Flips a matrix across its diagonal (rows become columns). Denoted by AT.
- ****Inverse:**** The matrix A−1 satisfies A⋅A−1=IA⋅A−1=I. Exists only if det⁡(A) ≠ 0. Used in solving equations and optimization.
- ****Determinant:**** A scalar value indicating whether a matrix is invertible. If det⁡(A) = 0, the matrix cannot be inverted.

## Eigenvalues and Eigenvectors

[Eigenvalues and eigenvectors](https://www.geeksforgeeks.org/engineering-mathematics/eigen-values/) describe how matrices transform space, making them fundamental in many ML algorithms.

- ****Eigenvalues (λ):**** Scalars showing how much a transformation stretches or compresses along a direction.
- ****Eigenvectors (v):**** Non-zero vectors that only scale (not change direction) under transformation.

****Example****: For A=[2112]A=[21​12​]

solving det⁡(A−λI) = 0 gives λ1 = 1,λ2 = 3.

- λ1=1→v1=[1−1]λ1​=1→v1​=[1−1​]
- λ2=3→v2=[11]λ2​=3→v2​=[11​]

****Eigen Decomposition****: A=QΛQ−1A=QΛQ−1

where Q holds eigenvectors and Λ is diagonal with eigenvalues.

****Applications in ML****:

- ****Dimensionality Reduction (PCA):**** Keeps directions with largest eigenvalues (most variance).
- ****Matrix Factorization (SVD, NMF):**** Breaks large datasets into smaller, structured parts for feature extraction.

## Solving Linear Systems of equations

[Linear systems](https://www.geeksforgeeks.org/engineering-mathematics/system-linear-equations/) are common in machine learning for parameter estimation and optimization. Key methods include:

****1. Gaussian Elimination:**** Transforms a matrix into row-echelon form using row operations. Steps:

- Forward Elimination -> make entries below diagonal zero
- Back Substitution -> solve variables from last row upward
- Pivoting -> swap rows to avoid division by zero

****2. LU Decomposition:**** Splits a matrix into Lower (L) and Upper (U) triangular matrices. Solves systems efficiently using forward and back substitution.

****3. QR Decomposition:**** Splits a matrix into Orthogonal (Q) and Upper triangular (R). Useful for least squares problems and eigenvalue computation.

## Applications of Linear Algebra in Machine Learning

Linear algebra powers many ML algorithms by enabling data manipulation, model representation and optimization. Key applications include:

- [****PCA (Principal Component Analysis)****](https://www.geeksforgeeks.org/data-analysis/principal-component-analysis-pca/)****:**** Reduces dimensionality by computing covariance, eigenvalues/eigenvectors and projecting data onto principal components.
- [****SVD (Singular Value Decomposition)****](https://www.geeksforgeeks.org/machine-learning/singular-value-decomposition-svd/)****:**** Factorizes a matrix into A = UΣVT, used for dimensionality reduction, compression and noise filtering.
- [****Linear Regression****](https://www.geeksforgeeks.org/machine-learning/ml-linear-regression/)****:**** Models relationships via matrix form Y = Xβ+ ϵ, solved using the normal equation XTXβ = XTY.
- [****SVM (Support Vector Machines)****](https://www.geeksforgeeks.org/machine-learning/support-vector-machine-algorithm/)****:**** Uses the kernel trick and optimization to find decision boundaries for classification and regression.
- [****Neural Networks****](https://www.geeksforgeeks.org/machine-learning/neural-networks-a-beginners-guide/)****:**** Depend on matrix multiplications, gradient descent and weight initialization for training deep models.