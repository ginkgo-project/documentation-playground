# Executor

- executor interface
- abstract type to define executor
- general advise:
  - create specific executor 
  - but always use abstract interface in user code
  - only use specific type if certain code will only run on that backend
- specific type for each backend
- main functionality
  - defines where kernels are run on
  - defines where memory is allocated on
- provide cross-executor copies
  - mostly for transfers between host and device
  - but also available for other combinations
- all specific types always available
- if backend not available on system, then exception if kernel on that backend tried to execute

executor operations
- get_master
- synchronize
- low level
  - run
  - alloc
  - free
  - copy

generic operations
- gko::clone


:::{toctree}
executors/reference
executors/omp
executors/cuda
executors/hip
executors/sycl
:::