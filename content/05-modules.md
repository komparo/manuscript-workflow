## Modules

### Scripts, packages and a portable environment

A module needs to contain at least one script, which will read in the input data, process it in some way, and ultimately write the output data in the correct format.

Given the large diversity of programming languages used in computation biology, a collaborative benchmarking effort should try to avoid imposing limits on the kind of programming languages that can be used. As an example, the single-cell analysis field is split between tools written for R and Python [@doi:10.1371/journal.pcbi.1006245], and choosing one of these two would therefore alienate a signficant part of the field. Moreover, a collaborative effort should also be open for new languages such as Julia [@arxiv:1411.1607], which could be more powerful and developer friendly for certain use cases.

Apart from being language agnostic, the execution of a module should also happen on any computer in exactly the same way. To make the execution reproducible, we therefore require that a module defines a portable environment, which contains the necessary operating system, language interpreters and other packages to execute the code within the module. An environment can be portable on many levels: within one programming language such as virtualenv for python or packrat for R or across languages using package managers such as Conda. The most complete level of reproducibility can be obtained by working at the level of the operating system, through container systems such as docker or singularity. Finally, to be able execute stochastic code in a reproducible manner, it is also necessary to fix the pseudo-random number generator in some way, for example by setting an a priori defined seed through R or numpy.

### Module metadata

- Provides an interface between different modules
- Controls reproducible execution of the scripts within the environment
- Input and output should always be explicitely defined
- Rerunning the module, or parts of the module, should only be triggered if input has changed
- Checks whether the inputs are present
- Checks whether the outputs are created and validates this output

### Version control

- Crucial for keeping track of what was changed when
- Also crucial for collaborating

### Code sharing platform

Code sharing is more than a place to deposit code:

- Create issues
- Create pull requests
- Versioning the code

### Automated testing and continuous integration

Testing a module:

- Checks the modules content, e.g. if the metadata is complete
- Checks whether it fullfills the requirement for this module, e.g. if it wil generate the required outputs
- Tests whether it can be loaded
- Tests whether it can be run using small input data
- Validates the produced output

While continuous integration for every module can sound like overdoing it, 90% of the errors are caught here. For small benchmarks, it is overkill, for large benchmarks, it is indispensible for maintainability

### Environment registry

- Easily downloadable by anyone wanting to replicate the environment
