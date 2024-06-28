# Vectors

Sequential vectors of $\mathbb{R}^n$ or $\mathbb{C}^n$ are represented by `gko::matrix::Dense<T>`.
This class can also represent multiple vectors of the same length at once.
In this case they are treated as a dense matrix in $\mathbb{R}^{n \times m}$ or $\mathbb{C}^{n \times m}$, 
which is stored in a *row-major* format.
That means, the entry `(i, j)` is stored at the memory location `i * stride + j`, where `stride >= m` is the number of elements, including padding, in a row.

Unless specified, `stride` will default to the number of columns `stride == m`.
A non-default stride might be chosen to get better aligned memory accesses.
For example, increasing the stride to `stride == 8`, if `m == 7` and `double` value type is used,
will lead to each row be aligned by 64 bytes, which corresponds to a full cache line on typical CPU architectures.
If changing the stride is helpful depends on the application and needs to be evaluated for the intended use cases.

Objects of type `gko::matrix::Dense<T>` are managed through smart pointers.
These behave like 'normal' pointers, except that they automatically manage the lifetime of the object.
For more details on how Ginkgo uses smart pointers please refer to [](lifetime).

## Creating

A (multi-) vector of a specific size is created with

```c++
gko::dim<2> size(12, 10);
std::unique_ptr<gko::matrix::Dense<double>> vec = gko::matrix::Dense<double>::create(exec, size);
```

The `size` parameter determines the number of rows and columns of the matrix.
More details on the parameter are in [](vectors/dim.md).
Without the `size` parameter, an empty (multi-) vector will be created.
These can typically be filled at a later point using the functions in [](#vector-io).

The stride can be specified by passing it as an additional parameter.

```c++
gko::dim<2> size(12, 7);
gko::size_type stride(8);
std::unique_ptr<gko::matrix::Dense<double>> vec = gko::matrix::Dense<double>::create(exec, size, stride);
```

It is possible to create a vector and fill it with data that was created outside.
This requires to pass in an [array](arrays.md) that has the same size as the total number of stored elements, which includes possible padding elements.
For an $n \times m$ (multi-) vector with `stride = m' >= m`, the array has to have the size `n * m'`.

```c++
gko::array<double> arr = ...;
std::unique_ptr<gko::matrix::Dense<double>> vec = gko::matrix::Dense<double>::create(exec, size, arr, stride);
```

If the array `arr` is not needed afterward it is advised to pass it in by `std::move(arr)`, to reduce unnecessary copies.
More details on handling existing user data are discussed in [](vectors/user-data.md).

:::{note}
With the C++ `auto` specifier introduced in C++11, the type of the vector needs to be specified only once:
```c++
auto vec = gko::matrix::Dense<double>::create(exec, size);
```
:::

### Small Vectors

- gko::initialize

## Accessing Data

## BLAS Operations

- operations typical of elements of vector spaces
- norms
  - multiple columns 
- transpose

## Conversions

- precision conversions
- to matrix conversions
- to/from complex 

(vector-io)=
## IO

- read/write from/to matrix data [](matrices/matrix_data.md)
- mtx format for multiple columns is a single list, which has all entries in column major order

## Permutation

## Gathering Rows

## Submatrices

:::{toctree}
:hidden:

vectors/dim
vectors/user-data
:::