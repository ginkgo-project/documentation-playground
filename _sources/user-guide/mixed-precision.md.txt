# Mixed Precision

- ginkgo types are templated
- allows using objects with different precision in the same code
- can convert vectors and matrices between different precisions
- lin op apply can handle different precisions
  - matrix and any vector can have different precision
  - vectors are converted back and forth to matrix precision
  - some matrices can skip this step
    - ell and csr 