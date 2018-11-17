## Module types

In the benchmarking workflow, we define four types of modules. These types should, at least in our experience, be enough to construct a fully comprehensive benchmark of certain group of methods:

* **Dataset generators**: This module will generate a dataset, which range from very simple "toy" datasets, to synthetic data which try to mimic real data, onto real data. Optionally, a dataset generator can also use another dataset as input, for example when wanting to generate some synthetic data based on some real data to assess the robustness to noise and scalability of a method. Only rarely will a dataset generator contain some primary data itself. Rather, data should be gathered directly from primary sources, for example using APIs by the NCBI/EBI or by downloading the data directly from data management systems such as Zenodo or Figshare.
* **Methods**: 
* **Metrics**
* **Report generators**

### Test case
