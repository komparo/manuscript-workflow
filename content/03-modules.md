## Modules

Our pipeline consists of several "modules", which are integrated and connected to ultimately produce a full benchmarking pipeline. These modules contain the code to generate some datasets, run a method and compare the output. This is similar to some related work (SummarizedBenchmark [@doi:10.1093/bioinformatics/bty627] and Dynamic Statistical Comparisons, https://github.com/stephenslab/dsc). Moreover, to assure a balanced interpretation of the results, report modules will aggregate and summarise the results, and provide some interpretation.

A module in our proposed workflow is more than just code, but includes several 

### Scripts and packages

There large diversity in programming languages used in bio-informatics, even within particular a particular subfield (such as single-cell bioinformatics [@doi:10.1371/journal.pcbi.1006245]). A collaborative workflow should therefore never "lock-in" to a particular language, 

### Portable environment

### Pipeline manager

- Controls reproducible execution of the scripts within the environment
- Input and output should always be explicitely defined
- Rerunning the module, or parts of the module, should only be triggered if input has changed

### Version control

- Crucial for keeping track of what was changed when
- Also crucial for working together

### Code sharing platform

Code sharing is more than a place to deposit code:
- Create issues
- Create pull requests
- Versioning the code

### Automated testing and continuous integration

- 90% of the errors are caught here

### Environment registry

- Easily downloadable by anyone wanting to replicate the environment
