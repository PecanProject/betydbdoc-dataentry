# Finding data

BETYdb is designed for both previously published data and 'primary' data. 
Most of this documentation assumes that you have already identified a data set that you want to upload, or have a set of papers from which you would like to extract data and summary statistics.

## Meta-analyses

If you are planning to do a meta-analysis, even if this is not your first time, please read 'Uses and Misuses of Meta-analysis in Ecology" \cite{Koricheva_2014}. Many texts are available, but the recent "Handbook of Meta-analysis in Ecology and Evolution" is probably the most comprehensive and specific for plant sciences.

For a meta-analysis, the first step is to find papers that contain the target data.

The easiest approach to use a search engine such as [Web of Science](http://apps.webofknowledge.com/), [Google Scholar](https://www.scholar.google.com), or [Microsoft Academic Search](http://academic.research.microsoft.com/). Starting with queries such as "_scientific name_ + _trait_", and allowing these results to guide further queries. 
Often, the references (particularly of meta-analyses and reviews) and forward citations will point to other studies.

Another starting point for the programmatically inclined - which aids in documenting searches - is to submit queries programmatically. Carl Davidson wrote a [python script](https://github.com/PecanProject/pecan/blob/master/modules/meta.analysis/inst/citation_search.py) to search for citations based on species and trait name. In addition, the rOpenSci project has a [suite of R packages for searching publications](http://ropensci.org/packages/#literature).
