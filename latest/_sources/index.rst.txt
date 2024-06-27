.. Ginkgo documentation master file, created by
   sphinx-quickstart on Fri Jun 14 15:40:37 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Ginkgo's documentation!
==================================

.. attention::

   what wording to use?

   - backend vs module
   - interfaces like transpose, conversion, etc under linop or under matrix?

user guide structure:
``user-guide/`` contains top level ``.md`` files that are the entry point to a certain concept.
This top level file should contain the most important bits of information.
Details should be left to files under ``concept/file.md``.
For example ``vectors.md`` mentions the creation function with arrays, but how to use this to get user data into vectors is done in ``vectors/user-data.md``

reading order:

#. getting-started: very high-level overview, introduces backends, example
#. build-install: getting ginkgo running
#. executors: introduce executor concept + specific executors
#. vectors: creating and handling of (dense) vectors
#. matrices: general creating and handling (apply) of matrices, link to matrix formats
#. linear-operators: generalize matrices, polymorphic object stuff
#. linear-solvers: iterative and direct solvers, preconditioners as links
#. distributed: larger category, recaps vectors, linops, solvers for distributed settings
#. object-configuration: description of config format
#. logging: adding loggers to objects
#. arrays: description of ginkgo arrays, is already referenced earlier
#. extensions
#. mixed-precision

.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: User Guide:

   user-guide/getting-started
   user-guide/build-install
   user-guide/executors
   user-guide/vectors
   user-guide/matrices
   user-guide/linear-operators
   user-guide/linear-solvers
   user-guide/factorizations
   user-guide/distributed
   user-guide/object-configuration
   user-guide/logging
   Arrays <user-guide/arrays>
   user-guide/extensions
   user-guide/mixed-precision


.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: Architecture:

   architecture/overview
   architecture/polymorphism
   architecture/adding-kernels
   architecture/lifetime
