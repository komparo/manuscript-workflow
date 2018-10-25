---
author-meta:
- Wouter Saelens
- Robrecht Cannoodt
- Lukas Weber
- Charlotte Soneson
- Yvan Saeys
- Mark D. Robinson
date-meta: '2018-10-25'
keywords:
- bioinformatics
- methods
- benchmarking
- single-cell analysis
lang: en-US
title: A workflow for continuous and collaborative benchmarking
...






<small><em>
This manuscript
([permalink](https://komparo.github.io/manuscript-workflow/v/cb72fabb97e971784b57bac4a44f506399144783/))
was automatically generated
from [komparo/manuscript-workflow@cb72fab](https://github.com/komparo/manuscript-workflow/tree/cb72fabb97e971784b57bac4a44f506399144783)
on October 25, 2018.
</em></small>

## Authors



+ **Wouter Saelens**<br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0002-7114-6248](https://orcid.org/0000-0002-7114-6248)
    · ![GitHub icon](images/github.svg){height="13px" width="13px"}
    [zouter](https://github.com/zouter)
    · ![Twitter icon](images/twitter.svg){height="13px" width="13px"}
    [zouters](https://twitter.com/zouters)<br>
  <small>
     Ghent University
     · Funded by Fonds Wetenschappelijk Onderzoek
  </small>

+ **Robrecht Cannoodt**<br><br>
  <small>
  </small>

+ **Lukas Weber**<br><br>
  <small>
  </small>

+ **Charlotte Soneson**<br><br>
  <small>
  </small>

+ **Yvan Saeys**<br><br>
  <small>
  </small>

+ **Mark D. Robinson**<br><br>
  <small>
  </small>



## Abstract {.page_break_before}

Benchmarking is a critical step in the development of bioinformatics tools, but the way it is done at the moment has some limitations. Because each benchmark is developed in isolation, they tend to be hard to compare, extend and are rapidly outdated. To address this, we combined modern software development tools to create a workflow for continuous and collaborative benchmarking. The structure of the benchmark is highly modular, so that anyone can contribute a set of datasets, metrics, methods or interprete the results, and get credit for their input. We apply this worklow on two emerging types of methods in the single-cell analysis field: trajectory differential expression (https://github.com/komparo/tde) and trajectory alignment (https://github.com/komparo/ta).


## Introduction

![The pipeline.](images/pipeline.png){#fig:pipeline width="100%"}


## Modules

Our pipeline consists of several "modules", which are integrated and connected to ultimately produce a full benchmarking pipeline. These modules contain the code to generate some datasets, run a method and compare the output. This is similar to some related work (SummarizedBenchmark [@Yqv1RKnE] and Dynamic Statistical Comparisons, https://github.com/stephenslab/dsc). Moreover, to assure a balanced interpretation of the results, report modules will aggregate and summarise the results, and provide some interpretation.

A module in our proposed workflow is more than just code, but includes several 

### Scripts and packages

There large diversity in programming languages used in bio-informatics, even within particular a particular subfield (such as single-cell bioinformatics [@ekkzy8ZR]). A collaborative workflow should therefore never "lock-in" to a particular language, 

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


## Combining modules within a benchmark

### Combining modules

### Pipeline manager

### Execution

### Continuous publishing

### Adding or updating a module

### Continuous integration

### Versioning


## Outlook

The project as it stands now is meant to be a proof-of-concept. In the ideal case, a continuous benchmarking project should be supported by a larger consortium, such as the Human Cell Atlas, which would not only assure its continuity, but would also provide infrastructure support. Perhaps the code platform, continuous integration, and environment registry servers could be hosted by such as consortium. By providing a platform where old ideas are rigorously tested, and new ideas can be easily validated, 

A platform like this should be build upon the idea that future methods and output formats can never be predicted, but at least we can prepare for them.


## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>
