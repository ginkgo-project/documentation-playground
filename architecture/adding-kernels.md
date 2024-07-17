# Adding Kernels to Ginkgo

A Ginkgo kernel is a piece of an algorithm that will get dispatched to an `Executor`.
Let's look at how to add a new kernel and make sure that it can run on all `Executor`s.

As an example, assume we want to add `my_new_kernel` to be used in `TheModifiedSolver`.
Adding a new Ginkgo kernel will touch several parts of the code:

- In the relevant header file where you are adding the kernel (here, it would be `core/solver/[the_modified_solver]_kernels.hpp`), 
declare the new kernel and add a new macro for it with `GKO_DECLARE_[NAMESPACE]_[KERNEL_NAME]`. 

- In `core/device_hooks/common_kernels.inc.cpp`, find the correct namespace for `TheModifiedSolver`.
In that section, use the relevant `GKO_STUB` macro. This will depend on the template parameters. For example, if 
`my_new_kernel` only depends on the `ValueType` used in the solver, then we would use
`GKO_STUB_VALUE_TYPE(GKO_DECLARE_THE_MODIFIED_SOLVER_MY_NEW_KERNEL);`.

- In the core file where the kernel will be used (here, `core/solver/[the_modified_solver].cpp`), register the kernel with 
`GKO_REGISTER_OPERATION(my_new_kernel, the_modified_solver::my_new_kernel);`. The `GKO_REGISTER_OPERATION` macro
 inserts the necessary code to allow you to run the kernel with 
```
exec->run(the_modified_solver::make_my_new_kernel(...))
```
 
- Finally, we have to write the definition(s) of the kernel for the backends. We will always have, at minimum, two 
versions of the kernel (one in `Reference`, and one for the other backends), but we could have separate versions for 
all backends. In this example, we would add a `Reference` version to the relevant kernels file in `reference/solver`,
and to other backends as necessary. In each file where we add a version of the new kernel, we follow the definition with the 
relevant version of the `GKO_INSTANTIATE_FOR_EACH_` macro to instantiate the kernel.

- We also want to add tests for our new kernel. First, we add a test against a known solution/expected outcome to
 `reference/test/solver/[the_modified_solver]_kernels.cpp`. Then, we add a test comparing the other backends to `Reference`.
For a unified kernel in `common/unified`, this test would go in `test/solver/[the_modified_solver]_kernels.cpp`.
Tests for specialized backend implementations belong in `[backend]/test/solver/[the_modified_solver]_kernels.cpp``. 

In the next section, we will give more details about creating unified kernels in Ginkgo.

:::{toctree}
adding-kernels/unified-kernels
:::
