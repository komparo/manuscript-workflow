## Module types

In the benchmarking workflow, we define four types of modules. In our experience, these four modules are in most cases enough to construct a fully comprehensive benchmark of certain group of methods.

### Dataset generators

This module will generate a dataset, which can from very simple "toy" data, synthetic data which try to mimic the characteristics of real data as best as possible, or real datasets. Optionally, a dataset generator can also use another dataset as input, for example when generating some synthetic data based on some real data. Only rarely will a dataset generator contain some primary data itself. Rather, data should be gathered directly from primary sources, for example using APIs by various databases or by downloading the data directly from data management systems such as Zenodo or Figshare.

### Methods

A method module reads in (parts) of a dataset, and uses this to generate a model. Some special types of methods can be helpful to include at the start of a benchmark. Positive controls, for example a method that simply return the reference model of the dataset, and negative controls, for example a method which generate a random model, could be useful to make sure the metrics work correctly. _Off-the-shelf_ methods, methods that can be easily implemented with just a few lines of code, could be helpful as a baseline to other methods and to assess the difficulty of particular datasets.

A common issue when benchmarking is the selection method parameters. It is not uncommon that the authors of a method disagree on what parameter settings were used for benchmarking [@doi:10.1101/385534; ]. <!---- TODO: find other recent biorxiv paper here -----> In our workflow, method authors are required to define for each parameter a default value, but also a distribution of values which can be used for parameter tuning in any form. <!---- TODO #5 : Expand with examples of types of parameter settings in benchmarks: manual tuning, automatic tuning, just defaults. And their advantages ----->

### Metrics

Metric modules score the output of a model. Some metrics assess the accuracy of a model by comparing it with some reference model present in the dataset. Others will look at the resources consumed by the method, such as CPU time and memory, to assess its scalability. Models can also be compared to other models, for example to examine the stability of a method. Finally, some qualitative metrics can also be defined here, for example those that look at the usability of a method.

### Report generators
In the end, the scores are aggregated and interpreted using a report generator. This modules generates a report which can be static, such as a markdown document with some figures, or dynamic in the form of a web application. By crowdsourcing the interpretation of the benchmark in this way, it would become much less authorative and instead promote open discussion in the field [@doi:10.1038/526189a]. It might certainly happen that different reports would contain contradicting results, but because each reports starts from the same set of data, it would be immediatly clear why the conclusions differ. For example, there might be subtle differences in how the scores have been averaged. Or, a report may only have focused on only a subset of the dataset which the authors found the most relevant for their method.
