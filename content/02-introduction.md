## Introduction

<!-- Benchmarking ---------------------------------------------------------------------------------------------------->

Evaluating the performance of a new method, and comparing it to the state-of-the-art, is a critical step in the development of bioinformatics methods. Benchmarks are essential to showcase the advantages and weaknesses of a method, and assure that new tools improve upon related methods. Despite this, well-designed and balanced benchmarking strategy can be difficult to create, especially when a ground truth on real data is not available.

The breadth of a benchmark is influenced by its purpose. In some studies, the goal is to review the methods available in the field, and highlight current challenges. Such independent benchmarks are usually very comprehensive, involving many datasets and different metrics ranging assessing the accuracy, scalability and robustness of a method. A special case of such a benchmark are competitions, where the focus lies on promoting the development of new methods within the field, while using existing methods as baseline. Other benchmarks are used as a companion to a study proposing a new method, demonstrating its improvements and usefulness.

<!-- Problem setting ---------------------------------------------------------------------------------------------------->

While benchmarks are unmistakingly important, the way benchmarking is usually done has some limitations:

* Benchmarks are quickly outdated when new methods come along.
* Benchmarks are difficult to extend, as this is usually only added as an afterthought. <!-- examples: @doi:10.1101/463927 -->
* While benchmarks often reach different conclusions, they are difficult to compare, because of (unclear) differences in datasets, method parameters, metric implementation and aggregation.
* Independent benchmarks and competitions tend to be authoritative, with only a small group of people deciding on how methods should be compared.
* Independent benchmarks are usually published quite late, only after a lot of methods are already available.
* Companion benchmarks represent in some way a lot of wasted effort, because datasets are often reanalysed, metrics reimplemented, and methods rewrapped.

<!---
Only the most relevant limitations are discussed here, others:

* Easy to overfit on what is available / ideas of the benchmarker. Examples include the Trapnell trajectory datasets, MINST dataset, but there are several others to be found. At the same time, it is also useful to only have a limited number of "reference" datasets available, to make it easier to develop new methods, so this makes this limitation somewhat controversial. In any case, the datasets should be a good representation of what the method should find "in the wild".
* Companion benchmarks always come down to the same thing.

--->

<!-- Goals  --------------------------------------------------------------------------------------------------------------->

To resolve these issues, we created a workflow for benchmarking which centers around the following three core concepts:

* **Modular**: It should be possible to extend the benchmark simply by adding a self-contained "module". Such a module could be: a dataset generator, a method, a set of metrics, or a report generator that interpretes the results and produces a report. Several tools exist already for making benchmarks modular: SummarizedBenchmark [@doi:10.1093/bioinformatics/bty627], [Dynamic Statistical Comparisons](https://github.com/stephens999/dscr) and iCOBRA [@doi:10.1038/nmeth.3805]. <!--- TODO #1 --->
* **Collaborative**: Anyone with a computer and internet connection should be able to run and contribute to the benchmark. This can range from contributing a module, to changing the structure of the benchmark itself. Discussions on the benchmark or any of the reports should also be open. The collaborative aspect of benchmarking has usually focused on the level of methods, with countless competitions and challenges, such as those organised by [DREAM](http://dreamchallenges.org/) or [kaggle](https://www.kaggle.com/).
* **Continuous**: A benchmark should be continously updated when new modules are added. This has quite a long history in bioinformatics, particularly in structure prediction [@doi:10.1002/prot.25415], but also in other fields [@doi:10.1186/s13059-016-0940-1]. <!---- TODO #2 ---->

To construct a workflow which fulfills combines these three concepts, we used several ideas and tools coming from modern software development, such as continuous integration, containerisation and workflow management.

<!-- General overview ------------------------------------------------------------------------------------------------------->

In brief, our workflow is structured as follows. We define several different **types of modules** (Figure {@fig:overview}a): dataset generators that can generate datasets and optionally use another dataset as input, methods that use a dataset to generate some model, metrics which calculate some scores using the model and optionally also parts of the dataset, and finally a report generator which summarise the datasets, models and scores into a report. Each type of module can generate a set of files which are constrained to a particular set of **formats** (Figure {@fig:overview}b). Each format has an unambiguous description, a set of good and bad examples, and includes a validator which validates the output files generated by each module. While each format is defined beforehand, new formats can be added over time as the field progresses. A **module** (Figure {@fig:overview}c) is a set of scripts and packages, which are run inside a portable environment. This module is put under version control, shared on a code sharing platform, and tested automatically using continuous integration. When all tests of a module are succesful, these modules can be integrated into the actual **benchmarking workflow** (Figure {@fig:overview}d). Within this workflow, modules are connected through a particular design, which is executed using a workflow manager. The output of the benchmark are a set of reports and apps, which are made available through a publishing platforms. To add a new module, a pull request is created to integrate the module within the benchmarking workflow, after which the contribution is reviewed openly. When accepted, the module is automatically integrated within the workflow, and the necessary parts of the workflow are re-executed. Finally, in regular time intervals (e.g. monthly), the full set of reports and apps are gathered and versioned.

<!-- Test case ------------------------------------------------------------------------------------------------------------->

As a test case, we developed a proof-of-concept benchmark for single-cell trajectory differential expression (TDE) methods. TDE methods try to find genes which are differentially expressed along a trajectory, the latter of which is an positioning of cells along a graph structure. Given that only a few of such methods have been developed yet [@doi:10.1101/060442; @doi:10.1101/079509; @doi:10.1038/nmeth.4402], this is the ideal scenario for developing the idea of a continuous and collaborative benchmark, and try to find solutions to the inevitable challenges which will come up as the field develops.

We will further discuss each element of the workflow in detail, along with how we currently implemented it in practice. It is important to acknowledge here that this is only one possible implementation, and that other tools, some of which still have to be developed, could better fit the benchmarking use-case. What is the most important is not the way the benchmark is implemented, but the ideas behind its implementation.

![The pipeline.](images/pipeline.png){#fig:overview width="100%"}
