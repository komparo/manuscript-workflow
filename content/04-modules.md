## Modules

Our pipeline consists of several "modules", which are integrated and connected to ultimately produce a full crowd-sourced benchmarking pipeline. These modules contain the code to generate some datasets, run a method and compare the output. Moreover, to assure a balanced interpretation of the results, report modules will aggregate and summarise the results, and provide some interpretation.

While the idea of creating a more modular benchmarking workflow is not new (SummarizedBenchmark [@doi:10.1093/bioinformatics/bty627] and Dynamic Statistical Comparisons, https://github.com/stephenslab/dsc)

A module also contains several other components which are in our view necessary to make the workflow easily extendable.

### Scripts and packages

A very varied set of programming languages used in bioinformatics, even within particular a particular subfield (such as single-cell bioinformatics [@doi:10.1371/journal.pcbi.1006245]). A collaborative workflow should therefore avoid a "lock-in" to a particular language.

### Portable environment

### Pipeline manager

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
