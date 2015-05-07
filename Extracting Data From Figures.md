#  Extracting information from figures \label{sec:extracting-data}

The easiest program to use for extracting points is [WebPlotDigitzer](http://arohatgi.info/WebPlotDigitizer/app/). WebPlotDigitizer is free, browser-based, and cross-platform. Extracts data from images. Demo [here](http://blog.plot.ly/post/70293893434/automatically-grab-data-from-an-image-with). 



See [related question on Stats.stackexchange](http://stats.stackexchange.com/a/14440/1381)

1.  Identify the data that is associated with each treatment
    *note:* If the experiment has many factors, the paper may not report the mean and statistics for each treatment. Often, the reported data will reflect the results of more than one treatment (for example, if there was no effect of the treatment on the quantity of interest). In some cases it will be possible to obtain the values for each treatment, e.g. if there are _n-1_ values and _n_ treatments. If this is not the case, the treatment names and definitions should be changed to indicate the data reflect the results of more than one experimental treatment. 
2.  Enter the mean value of the trait
3.  Enter the `statname`, `stat`, and number of replicates, `n` associated with the mean
 *  `stat` is the value of the `statname` (i.e. `statname` might be ’standard deviation’ (SD) and the `stat` is the numerical value of the statistic)
 *  Always measure size of error bar from the mean to the end of an error bar. This is the value when presented as ( _X_ ± _SE_) or _X(SE)_ and may be found in a table or on a graph.
 *  Sometimes CI and LSD are presented as the entire range from the lower to the upper end of the confidence interval. In this case, take 1/2 of the interval representing the distance from the mean to the upper or lower bound.
