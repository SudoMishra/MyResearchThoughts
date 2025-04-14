### Motivation for this Series

I want to see CPUs and GPUs burn.
![[GPU Burning.png]]

Link to ChatGPT chat: [Matrix Chat](https://chatgpt.com/share/67f398b1-37c0-8002-830a-4e4fea18557e)

Mathematically, matrix-vector multiplication is a special case of matrix-matrix multiplication, but that's not necessarily true of them as realized in a software library.

They support different options. For example, gemv supports strided access to the vectors on which it is operating, whereas gemm does not support strided matrix layouts. In the C language bindings, gemm requires that you specify the storage ordering of all three matrices, whereas that is unnecessary in gemv for the vector arguments because it would be meaningless.

Besides supporting different options, there are families of optimizations that might be performed on gemm that are not applicable to gemv. If you know that you are doing a matrix-vector product, you don't want the library to waste time figuring out that's the case before switching into a code path that is optimized for that case; you'd rather call it directly instead.
  
Let's break down the explanation into two parts: one that explains the distinction between matrix-vector and matrix-matrix multiplication in libraries, and another that explains what “strided matrix layouts” mean.

Let's break down the explanation into two parts: one that explains the distinction between matrix-vector and matrix-matrix multiplication in libraries, and another that explains what “strided matrix layouts” mean.

---

### 1. [[GEMM vs GEMV Software Implementations]]

**Matrix-vector multiplication (gemv)** is a special case of matrix-matrix multiplication but has its own function because:
  - It can be optimized without extra checks or overhead.
  - It has a simpler interface that does not require specifying storage order for a vector.
  - It can support strided vector access, which is useful when vectors are not stored contiguously.

 **Matrix-matrix multiplication (gemm)** is more general:
  - It requires knowledge of the storage order of both matrices to perform efficient multiplication.
  - It typically assumes standard contiguous memory layouts to leverage high-performance optimizations.
  - Handling arbitrary strided layouts in `gemm` would add unnecessary complexity and reduce performance.

**Segmented Gather Matrix-Vector multiplication (SGMV)** : is a specialized approach to performing matrix–vector multiplication, designed primarily to handle situations where the vector (or parts of it) must be accessed in a non-contiguous, irregular pattern. This irregularity is common in sparse or structured matrices where only selected elements of the input vector are needed for each output element.
### 2. [[Memory Layouts]]


---

In essence, even though the mathematical operations are related, the different requirements and opportunities for optimization in real-world software libraries have led to the development of separate functions with different capabilities and interfaces.

#### Are there specific matrix or vector types for which additional optimisation techniques are present. For example, one such case is the sparse vectors and sparse matrices. Another example could be matrices like Vandermonde Matrices. Are there specific optimisations that can be leveraged based on the properties of the matrix 

There are indeed many cases where the structure or properties of a matrix or vector can be exploited to improve performance, reduce computational cost, or lower memory requirements. Below are some common categories and the specialized techniques that can be applied:

## [[Matrix Types]]

### 1. Sparse Matrices and Vectors

**Key Characteristics:**  
Sparse matrices or vectors have a large number of zero entries. Directly applying dense algorithms wastes both time (performing unnecessary multiplications by zero) and memory.

**Optimizations:**  
- **Specialized Storage Formats:**  
  Formats such as Compressed Sparse Row (CSR), Compressed Sparse Column (CSC), and others allow storage of only nonzero elements along with their indices. This reduces memory usage significantly.
  
- **Algorithmic Improvements:**  
  Multiplication routines (e.g., sparse BLAS libraries) are designed to iterate only over nonzero elements. This can turn an \( O(n^2) \) or \( O(n^3) \) operation into something much more efficient, especially when the density of nonzero elements is very low.
  
- **Graph and Network Algorithms:**  
  Often, sparse matrices arise in graph problems, where additional insights (like using breadth-first search or other graph-based methods) can further optimize computations.

---

### 2. Structured Matrices

Many matrices come with inherent structures that allow for more efficient computations than would be possible with a general dense matrix. Some common structured matrices include:

**Vandermonde Matrices:**  
- **Properties:**  
  These matrices have elements that follow a geometric progression along each row (or column). They appear in polynomial interpolation problems and systems of equations.
  
- **Optimizations:**  
  Specialized algorithms can exploit the structure to perform matrix-vector multiplications faster. For example, fast multiplication techniques using the Fast Fourier Transform (FFT) can reduce computational complexity from \( O(n^2) \) to \( O(n \log n) \) in some cases.
  
**Toeplitz and Circulant Matrices:**  
- **Properties:**  
  In Toeplitz matrices, each descending diagonal from left to right is constant. Circulant matrices are a special kind of Toeplitz matrix where the rows are cyclic permutations of each other.
  
- **Optimizations:**  
  These matrices can be multiplied using FFT-based techniques. For circulant matrices, the multiplication can be performed very efficiently via the convolution theorem.

**Banded Matrices:**  
- **Properties:**  
  Banded matrices have nonzero entries concentrated around the main diagonal.
  
- **Optimizations:**  
  Algorithms that are designed to work with the band structure only perform operations on the nonzero “band” elements. This reduces both the arithmetic operations and memory footprint compared to full dense matrix operations.

**Diagonal and Block-Diagonal Matrices:**  
- **Properties:**  
  Diagonal matrices have nonzero elements only on the main diagonal, while block-diagonal matrices are composed of smaller dense blocks along the diagonal.
  
- **Optimizations:**  
  Diagonal matrices lead to very simple multiplications (element-wise multiplication), and block-diagonal matrices can be processed in parallel for each block, improving performance.

---

### 3. Other Special Cases

**Symmetric/Hermitian Matrices:**  
- **Properties:**  
  These matrices satisfy \( A = A^T \) (or \( A = A^* \) for complex matrices), meaning only half the matrix needs to be stored.
  
- **Optimizations:**  
  Many libraries provide routines that take advantage of this property to reduce computational workload (for example, only processing the upper or lower triangular part) and memory usage.

**Orthogonal/Unitary Matrices:**  
- **Properties:**  
  These matrices preserve norms and are often represented implicitly (for example, via Householder reflectors).
  
- **Optimizations:**  
  Multiplications involving these matrices can be optimized by avoiding explicit formation of the full matrix and using compact representations.

**Low-Rank Approximations:**  
- **Properties:**  
  Some matrices can be approximated well by a product of two much smaller matrices.
  
- **Optimizations:**  
  Techniques such as Singular Value Decomposition (SVD), CUR decompositions, or randomized low-rank approximation can be used to reduce the effective size of the matrix and speed up computations like matrix multiplication or solving linear systems.

---
### Summary

In summary, exploiting the properties of matrices and vectors—whether it be sparsity, specific patterns (like Vandermonde, Toeplitz, circulant, or banded structures), or special characteristics (like symmetry or orthogonality)—can lead to significant improvements in computational efficiency. Libraries and algorithms that are aware of these properties are able to bypass the general-purpose routines and apply targeted optimizations, which is why specialized functions exist for many of these cases.

