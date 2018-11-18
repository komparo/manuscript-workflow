## Data formats

The basis of any collaborative effort in computation biology is agreeing on how data will be interchanged, and benchmarking is no exception. Sometimes, the differences between data formats can be minor, for example whether the samples within a gene expression matrix are put in the rows or in the column. In other cases, different data formats can have a significant impact on storage and/or the speed by which the data can be processed. <!--- TODO #3 --->

In the benchmarking workflow presented here, a format represents how a particular part of a dataset, model, score or report should be represented on disk.

### What a format entails

<!-- Description ------------------------------------------------------------------------------------------------------------->

For a format to be useful, it should have an unambiguous description. In this way, someone developing a module can be sure how the inputs look like, even if these inputs do not exist yet, and can also be sure that the outputs will be useful as input for other modules.

<!-- Validation --------------------------------------------------------------------------------------------------------------->

While a description is meant to be readable by humans, this description should also be translated into a lanuage computers can understand, so that each data file produced by a module can be validated. In this way, developers of a module can get immediate feedback on whether their output matches the format description. To make a format validatable, it is one possibility to use one of the many "schemas" available, such as json-schema ([http://json-schema.org/](http://json-schema.org/)), XML schemas or Apache Arrow Schemas. Often, there are already validators available for these schemas (json-schemas for example: [https://json-schema.org/implementations.html#validators](https://json-schema.org/implementations.html#validators)). On the other hand, for more custom file formats or complex behaviour, we will have to implement the validator ourselves.

<!-- Examples ----------------------------------------------------------------------------------------------------------------->
Finally, connecting the human-readable description with the computation validation can be done with providing good and bad examples of the data format. These examples serve a double purpose, because they provide the module contributors several examples as a help to understand the description, but can also be used as test cases for the format validators.

### Formats change as the field progresses

Usually, the most optimal representation of a dataset or the output of a method only becomes apparent when several methods have been developed already. This means that any effort to make a benchmark collaborative and continuous should strive to make its data formats flexible. Flexibility can take several forms. New features could be added to the format, without invalidating the old data and modules. When this is not an option, new formats could be added alongside the old. When applicable, converters should then be written which convert the old formats into the new, so that old modules keep on functioning. Finally, in some extreme cases, old formats could be invalidated and replaced with new formats, which would require some versioning system to make sure modules are run on the version of the formats they were developed.

It is inevitable that disagreements about data representation will pop up in a collaborative effort. But in any case, having common formats, even if they are suboptimal for certain use cases, is usually better then having none at all.

### Test case

For the TDE use case, to keep the formats simple and accesible, we decided to mainly use text-based formats such as comma-separated values (CSV) and JSON files, as these can be rapidly parsed in almost any programming language. For each format, we wrote custom validators in R, although JSON files were also partly validated using a json schema validator (ajv, [https://ajv.js.org/](https://ajv.js.org/)). These validators are available as an R package ([https://github.com/komparo/tde_formats](https://github.com/komparo/tde_formats)). For each format, we also wrote a description and several examples, which are shown together in the contributor's guide ([https://komparo.github.io/tde/formats.html](https://komparo.github.io/tde/formats.html)).

To represent a dataset and a model, we needed to define several formats grouped within three categories:

* Single-cell expression datasets: This is relatively straightforward, given that the sheer number of single-cell RNA-seq tools available. As is commonly done, we represent the dataset as a matrix, together with two tables containing the metadata of the cells and features respectively.
* Trajectory: This is more difficult, given the vast diversity in outputs of trajectory inference methods. In our recent benchmarking of these methods, we already created a common format for trajectories, and included this format in this benchmark as well. However, as we also acknowledge in that study, alternative formats may be possible.
* Trajectory differential expression: This is the the most difficult, because we had to make some educated guesses about how we expect the field to progress. While it impossible to know beforehand what formats will be ultimately needed, we can at least try to already predict for them. Based on what is already done by some existing methods, we defined several types of trajectory differential expression such as oscillatory (within a cyclical trajectory), pseudotime (expression that changes along pseudotime), and branch point (expression that happens at a particular branch point). We extended this with some other types of differential expression, such as local (changes in expression at a particular point of the trajectory) and overall (changes in expression anywhere in the trajectory). Each kind of differential expression is represented in a table format, where each differential expression event is represented in a row which can contain information on the associated p-value, a ranking and/or effect size.

Scores and reports have less requirements regarding the formats. The most simplest format to represent a score is as an atomic value, in which each model can be summarized by one quantitave or qualitative value. Of course, more complex score formats are also possible. For reports, we included two formats. A static report with at least an index HTML or markdown file, together with any extra assets such as figures. A dynamic report on the other hand produces a software container which expose a web app through a port on execution.