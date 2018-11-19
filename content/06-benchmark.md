## Combining modules within a benchmark

To make the benchmark as inclusive as possible, it should be possible for anyone to extend or adapt the benchmark for their own purposes. At the same, it would also be useful to have a central place which lists all the modules and provides the most up-to-date set of reports for interested readers. To reconcile these two criteria, our benchmarking workflow has one "main" repository, which lists the location of the different modules and how they are combined in the benchmark. Anyone can however create a fork of this repository, adapt the modules or benchmarking design in any way, and run it using their own infrastructure.

### Executing the benchmark

For the execution of the modules, a pipeline manager such as snakemake [@doi:10.1093/bioinformatics/bts480] or nextflow [@doi:10.1038/nbt.3820] is almost indispensable. These tools make sure the modules are executed in the correct order and within a reproducible environment. Moreover, to make the benchmark scalable, a pipeline manager will only rerun those exeuctions for which any inputs have changed, which includes changes to any scripts or packages inside the portable environment. Within our benchmarking workflow, we created a custom pipeline manager for this, which provided us with some features that are lacking in most current pipeline managers, such as incrementality at the level of the portable environment, output validation and fixation of the pseudo-random number generator.

### Adding or updating a module

While anyone is able to fork and modify the benchmark repository, modifications to the main repository, such as additions or updates of a module, still requires some form of control by a group of maintainers. This group of maintainers, which would primarily consist of authors of other modules, are responsible for checking whether the module has passed all automated checks. and give feedback regarding data formats and testing results. Important here is that this reviewing happens in a completely open fashion, similar as to what is done in some open-source communities such as Bioconductor and ropensci ([https://github.com/ropensci/onboarding](https://github.com/ropensci/onboarding)).

In our workflow, adding or updating a module can be done by cloning the repository, making the necessary changes, and then creating a pull request on Github.

### Continuous benchmarking and versioning

Every time the main repository is updated, for example with a new version of a module, an update of the whole benchmark workflow is triggered. Only those modules with outdated input, because the code, environment or some input files changed, are rerun.

The end results of the benchmark are one or more reports, which are freely accessible online. On regulator time intervals, such as on a monthly basis, all the reports are gathered and released as a new "version", which includes a changelog of updates to any of the modules made before the last release. This release is given a digital object identifier and registered at an open-access repository such as zenodo or figshare.