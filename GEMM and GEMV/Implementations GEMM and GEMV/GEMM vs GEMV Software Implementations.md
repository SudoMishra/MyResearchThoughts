**Mathematical Background**  
- **[[GEMV]]**
  In mathematics, multiplying a matrix by a vector is a special case of multiplying two matrices. For example, if you have an \( m x n \) matrix \( A \) and an \( n \)-dimensional vector \( x \), you can view \( x \) as an \( n x 1 \) matrix. The result is an \( m x 1 \) matrix (or vector).

- **[[GEMM]]**  
  This operation involves two matrices. For example, multiplying an \( m x n \) matrix \( A \) by an \( n x p \) matrix \( B \) produces an \( m x p \) matrix \( C \).

- [[SGMV]]:
  Segmented Gather Matrix-Vector multiplication (SGMV) is a specialized approach to performing matrix–vector multiplication, designed primarily to handle situations where the vector (or parts of it) must be accessed in a non-contiguous, irregular pattern. This irregularity is common in sparse or structured matrices where only selected elements of the input vector are needed for each output element.

**Software Library Implementations**  
While mathematically the matrix-vector case is a subset of the matrix-matrix case, many numerical libraries (such as BLAS) implement these operations as separate routines for several reasons:

- **Optimized Code Paths:**  
  - When you call a function designed specifically for matrix-vector multiplication (often referred to as `gemv`), the library already “knows” the structure of the operation. There is no need to check dimensions or set up for handling two-dimensional data where one factor is just a vector.  
  - For matrix-matrix multiplication (`gemm`), the function must accommodate a broader set of parameters and possible memory layouts. If it had to handle the vector case, it might spend extra time checking for special conditions (e.g., is one of the matrices really just a vector?) before it can switch to an optimized routine for that scenario.

- **Interface Differences:**  
  - In many libraries, `gemm` (general matrix multiplication) requires you to specify the layout (i.e., row-major or column-major ordering) for **all three** matrices involved. This is important because the multiplication algorithm and memory access patterns depend heavily on how the data is stored.
  - In contrast, for `gemv` (general matrix-vector multiplication), the vector’s storage order is usually implicit or irrelevant because a vector doesn’t have a second dimension that can be laid out in different orders. Therefore, the interface is simpler and doesn’t require the same kind of layout specification.

- **Avoiding Unnecessary Overhead:**  
  - By having separate functions, the library avoids the overhead of "figuring out" which case it is dealing with. When you know you’re doing a matrix-vector multiplication, you want to call the function directly optimized for that, rather than a general-purpose function that must perform extra checks.

### List of Optimisations
- [how-to-optimize-gemm](https://github.com/flame/how-to-optimize-gemm)
- [CUDA GEMM Worklog](https://siboehm.com/articles/22/CUDA-MMM)
- [CUDA GEMM Kernels](https://leimao.github.io/article/CUDA-Matrix-Multiplication-Optimization/)
- [MatMul CPU](https://salykova.github.io/matmul-cpu)

### Papers
- [Anatomy of High-Performance Matrix Multiplication](https://www.cs.utexas.edu/~flame/pubs/GotoTOMS_final.pdf)
- ---
