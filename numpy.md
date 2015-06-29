#NumPy Cheat Sheet

##Data Types
Type Name | Type Code | Description
---  | --- | ---
`int8` `uint8` | `i1` `u1` | 8-bit integer
`int16` `uint16` | `i2` `u2` | 16-bit integer
`int32` `uint32` | `i4` `u4` | 32-bit integer
`int64` `uint64` | `i8` `u8` | 64-bit integer
`float16` | `f2` | Half-precision float
`float32` | `f4` `f` | Standard single-precision float
`float64` | `f8` `d` | Standard double-precision float
`float128` | `f16` `g` | Extended-precision float
`complex64` | `c8` | Complex represented by two 32-bit floats
`complex128` | `c16` | Complex represented by two 64-bit floats
`complex256` | `c32` | Complex represented by two 128-bit floats
`bool` | `?` | Boolean
`object` | `0` | Python object type
`string_` | `S` | Fixed-length string with 1 byte per char (e.g. S10 for a string of length 10)
`unicode_` | `U` | Fixed-length unicode string (e.g. U10 for a unicode string of length 10)

##Creating Arrays
Expression | Description
--- | ---
`np.array([1, 2.5, -3])` | A 1D ndarray object
`np.array([1, 2, 3], dtype=np.float32)` | A 1D ndarray object with the specified element type
`np.array([[1, 2],[3, 4]])` | A 2D ndarray object
`np.zeros(5)` | A 1D ndarray object of length 5 with zeros
`np.zeros((2, 3))` | A 2D ndarray object of size 2x3 with zeros
`np.zeros_like(a)` | A ndarray object with the shape of `a` with zeros
`np.ones(5)` | A 1D ndarray object of length 5 with ones
`np.ones((2, 3))` | A 2D ndarray object of size 2x3 with ones
`np.ones_like(a)` | A ndarray object with the shape of `a` with ones
`np.empty(5)` | A 1D ndarray object of length 5 with uninitialized values
`np.empty((2, 3))` | A 2D ndarray object of size 2x3 with uninitialized values
`np.empty_like(a)` | A ndarray object with the shape of `a` with uninitialized values
`np.eye(3)` `np.identity(3)` | An identity matrix of size 3
`np.arange(10)` | Python's range but it returns a ndarray object
`np.asarray(a)` | `a` as an ndarray object (does not copy if it already is one) 

##Array Attributes and Member Functions
Attribute/Function | Description
---  | ---
`a.ndim` | Dimensionality (int)
`a.shape` | Shape (a touple containing the length in each of the dimensions)
`a.dtype` | Data Type
`a.astype(np.float64)` | Return a new array with the converted elements
`a.reshape((3, 5))` | Reshape the ndarray object (the number of elements must be the same)
`a.swapaxes((1, 0))` | Swaps the specified axis pair
`...` |

##Array Indexing
Expression | Description
---  | ---
`a[3]` | An element or subarray
`a[0, 3, 1]` | An element or subarray at the specified position of each of the dimensions
`a[2:6]` `a[:2]` `a[1:,2]`| A slice of elements or subarrays
`a[a > 5]` `a[(a > 5) \| (a == -1)]` `a[a > 5, 2:]` | A boolean index returns only the elements or subarrays where the expression is true
`a[[0, 1], [0, 1]]` | A list of elements or subarrays that have their coordinate dimensions specified by the sublists (i.e. in the example the first list holds the 1st axis coordinates and the second list holds the 2nd axis coordinates so the length of the two lists must be equal)
`a[np.ix_([1, 2],[0, 5, 2])]` | A rectangular area specified by selecting the specified coordinates along the axes

##Operations between Arrays and Scalars
Expression | Description
---  | ---
`a + b` `a * b` `a / b` `a ** b` `...`| Elementwise operation between the two matrices
`a + 5` `a * 5` `a / 5` `a ** 5` `...`| Elementwise operation between the elements of the matrix and the scalar
`a > 5` `a == 5` `...`| Elementwise comparison between the elements of the matrix and the scalar

##Unary Universal Functions on Arrays
Expression | Description
---  | ---
`np.sqrt(a)` | Elementwise square root
`np.square(a)` | Elementwise square
`np.exp(a)` | Elementwise exp
`np.log(a)` `np.log10(a)` `np.log2(a)` `np.log1p(a)` | Elementwise log, log2, log10 and log(1+x)
`np.abs(a)` `np.fabs(a)` | Elementwise abs (`fabs` is faster for non-complex values)
`np.sign(a)` | Elementwise sign (-1, 0, 1)
`np.ceil(a)` `np.floor(a)` `np.rint(a)` | Elementwise rounding
`np.modf(a)` | Elementwise `divmod`
`np.isnan(a)` | Elementwise `NaN` detection
`np.isinfinite(a)` `np.isinf(a)` | Elementwise `inf` detection
`np.sin(a)` `np.sinh(a)` `np.cos(a)` `np.cosh(a)` `np.tan(a)` `np.tanh(a)` | Elementwise trigonometric functions
`np.logical_not(a)` | Elementwise boolean negation 

##Binary Universal Functions on Arrays
Expression | Description
---  | ---
`np.add(a, b)` | Elementwise add
`np.subtract(a, b)` | Elementwise subtract
`np.multiply(a, b)` | Elementwise multiply
`np.divide(a, b)` `np.floor_divide(a, b)` | Elementwise divide
`np.power(a, b)` | Elementwise power
`np.maximum(a, b)` `np.fmax(a, b)` | Elementwise maximum (`fmax` ignores `NaN`s)
`np.minimum(a, b)` `np.fmin(a, b)` | Elementwise minimum (`fmax` ignores `NaN`s)
`np.mod(a, b)` | Elementwise `mod`
`np.copysign(a, b)` | Copy the sign of the values in b to values of a
`np.equal(a, b)` `np.not_equal(a, b)` `np.greater(a, b)` `np.greater_equal(a, b)` `np.less(a, b)` `np.less_equal(a, b)` | Elementwise comparison
`np.logical_and(a, b)` `np.logical_or(a, b)` `np.logical_xor(a, b)` | Elementwise logical operators

##Statistical Functions on Arrays
Expression | Description
---  | ---
`a.mean()` `a.mean(2)` | Mean along the specified axes
`a.min()` `a.max(2)` | Find minimum/maximum for each element or subarray for the specified axes
`a.argmin()` `a.argmax(2)` | Find the index of minimum/maximum for each element or subarray for the specified axes
`a.sum()` `a.sum(2)` | Sum along the specified axes
`a.prod()` `a.prod(2)` | Product along the specified axes
`a.cumsum()` `a.cumsum(2)` | Cumulative sum along the specified axes
`a.cumprod()` `a.cumprod(2)` | Cumulative product along the specified axes
`a.std()` `a.var()` | Standard deviation and variance

##Set Logic on Arrays
Expression | Description
---  | ---
`np.unique(a)` | Sorted unique
`np.intersect1d(a, b)` | Sorted intersection
`np.union1d(a, b)` | Sorted union
`np.in1d(a, b)` | For each element of `a` decide if it one of `b`'s elements
`np.setdiff1d(a, b)` | Sorted difference
`np.setxor1d(a, b)` | Sorted symmetric difference

##Linear Algebra on Arrays
Expression | Description
---  | ---
`a.T` | Transpose
`a.transpose((1, 0))` | Pivot the matrix on the specified list of axes
`np.diag(a)` | Returns the diagonal elements as an ndarray or convert a 1D array to a diagonal matrix
`np.dot(a, b)` | Dot (matrix) product
`np.trace(a)` | Trace 
`np.linalg.det(a)` | Matrix determinant
`np.linalg.eig(a)` | Eigenvalues and eigenvectors
`np.linalg.inv(a)` | Inverse of a square matrix
`np.linalg.pinv(a)` | Pseudo-inverse
`np.linalg.qr(a)` | QR decomposition
`np.linalg.svd(a)` | SVD
`np.linalg.solve(A, b)` | Solve linear equation `Ax=b`
`np.linalg.lstsq(A, b)` | Least squares solution for `Ax=b`

##Random Numbers
Expression | Description
---  | ---
`np.random.seed(4)` | Set the seed of the random number generation
`np.random.permutation(a)` | Random permutation of a sequence or a permuted range
`np.random.shuffle(a)` | Shuffle a sequence in place
`np.random.rand()` | Draw from a uniform distibution
`np.random.randint()` | Draw from a uniform distibution
`np.random.normal()` | Draw from a normal distibution
`np.random.randn()` | Draw from a normal distibution (mean=0, std=1)
`np.random.binomial()` | Draw from a binomial distibution
`np.random.beta()` | Draw from a beta distibution
`np.random.chisquare()` | Draw from a Chi-square distibution
`np.random.gamma()` | Draw from a gamma distibution
`np.random.uniform()` | Draw from a uniform `[0,1)` distibution

##File I/O
Expression | Description
---  | ---
`np.save('a.npy', a)` | Save to file
`np.load('a.npy')` | Load from file
`np.savetxt('foo.txt', a)` | Save into a text file
`np.loadtxt('foo.txt')` | Load text file

##Misc
Expression | Description
--- | ---
`np.meshgrid(xs, ys)` | A 2D grid of points from 2 1D ndarrays
`a.sort()` `a.sort(1)` | In-place sort an ndarray along the specified axes
`a.any()` `a.all()` | Decide if any/all of the elements of an ndarray is True
`np.where(cond, a, b)` | Chooses elementwise between two ndarrays `a` and `b` based on `cond`
