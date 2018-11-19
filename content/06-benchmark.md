## Combining modules within a benchmark

In principle, it should be possible for anyone to extend or adapt the benchmark for their own purposes. At the same, it is also important to have a central place which lists all the modules and provides the most up-to-date set of reports for interested readers. To make this possible, our benchmarking workflow has one "main" repository, which lists the location of the different modules and how they are combined in the benchmark. Anyone can however create a fork of this repository, adapt the modules or benchmarking design in any way, and run it using their own infrastructure. 

### Executing the benchmark

For the execution of the modules, a pipeline manager such as snakemake [@doi:10.1093/bioinformatics/bts480] or nextflow [@doi:10.1038/nbt.3820] is almost indispensable. These tools make sure the modules are executed in the correct order and within a reproducible environment. Moreover, to make the benchmark scalable, a pipeline manager will only rerun those exeuctions for which any inputs have changed, which includes changes to any scripts or packages inside the portable environment. Within our benchmarking workflow, we created a custom pipeline manager for this, which provided us with some features that are lacking in most current pipeline managers, such as incrementality at the level of the portable environment, output validation and fixation of the pseudo-random number generator.


### Pipeline manager

### Execution

### Continuous publishing

### Adding or updating a module

### Continuous integration

### Versioning
