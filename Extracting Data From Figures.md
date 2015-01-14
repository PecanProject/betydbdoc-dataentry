#  Extracting information from figures \label{sec:extracting-data}

To extract information from a figure, the general method is: 

1. upload an image 
2. set the x and y scales by indicating the values at two points on each axis 
3. indicate if the scale is linear, log, etc, 
4. click on the points. 
 

Some software programs automatically recognize lines or points. However, since points are usually sought after, the results are often too inconsistent to be helpful even with 100s of points. Also, no program has yet been found to be able to distinguish different symbols. This feature could be worth the trouble for digitizing lines, but this is not commonly required.

The program returns each point as an x-y matrix.

Often it helps selecting points if the image is zoomed, either by uploading a zoomed version of the image or using the zooming feature available in some of the programs.



### List of available Programs

I have experience with the following programs. All of these work well fine. Except in contexts where measurement error is very small, error from graph scraping is insignificant (e.g. error from digitization << size of error bars or uncertainty in the estimate). I have not tested the accuracy of any of these programs, but it would be interesting to compare among users, among programs, and against the results of reproduced statistical analyses.


* [Digitizer](http://digitizer.sourceforge.net/) (shareware) auto point / line recognition. Available in Ubuntu repository (engauge-digitizer)
* [Get Data](http://www.getdata-graph-digitizer.com/) (shareware) has zoom window, auto point / line recognition
* [DigitizeIt](http://www.digitizeit.de/) (shareware) auto point / line recognition
* [ImageJ](http://rsbweb.nih.gov/ij/) (open source, most extensible after R digitize)
* [R digitize](http://cran.r-project.org/web/packages/digitize/index.html) (free, open source), because it simplifies the processs of getting data from the graph into an analysis by keeping all of the steps in R. See the [tutorial in R-Journal](http://journal.r-project.org/archive/2011-1/RJournal_2011-1_Poisot.pdf)
* [GrabIt!](http://www.datatrendsoftware.com/home.html) (free demo, $69) Excel 
plug-in 

I have not used these:

* [WebPlotDigitzer](http://arohatgi.info/WebPlotDigitizer/app/) (free, online). Extracts data from images. Demo [here](http://blog.plot.ly/post/70293893434/automatically-grab-data-from-an-image-with). 
* [GraphClick](http://www.arizona-software.ch/graphclick/) (Mac, $8)
* [g3data](http://www.frantz.fi/software/g3data.php) (open source - GNU GPL) Has zoom window, no auto-recognition. Available in Ubuntu repository.

See [related question on Stats.stackexchange](http://stats.stackexchange.com/a/14440/1381)

1.  Identify the data that is associated with each treatment
    *note:* If the experiment has many factors, the paper may not report the mean and statistics for each treatment. Often, the reported data will reflect the results of more than one treatment (for example, if there was no effect of the treatment on the quantity of interest). In some cases it will be possible to obtain the values for each treatment, e.g. if there are _n-1_ values and _n_ treatments. If this is not the case, the treatment names and definitions should be changed to indicate the data reflect the results of more than one experimental treatment. 
2.  Enter the mean value of the trait
3.  Enter the `statname`, `stat`, and number of replicates, `n` associated with the mean
 *  `stat` is the value of the `statname` (i.e. `statname` might be ’standard deviation’ (SD) and the `stat` is the numerical value of the statistic)
 *  Always measure size of error bar from the mean to the end of an error bar. This is the value when presented as ( _X_ ± _SE_) or _X(SE)_ and may be found in a table or on a graph.
 *  Sometimes CI and LSD are presented as the entire range from the lower to the upper end of the confidence interval. In this case, take 1/2 of the interval representing the distance from the mean to the upper or lower bound.

###  Extracting Data using R

To extract data from a jpg file in R using the digitize package:  

1.  Save image as a `*.jpg` file
2.  Open R
3.  Change the directory that R is using to the one where the image is
4.  Use R code below to extract data, display it, and save it in a `csv`
    file (steps below)
5.  Upload csv to the project file in google spreadsheet, or open as
    excel/openoffice and copy/paste to google spreadsheet

### Extracting Data From a Figure using GetData

1.  Open PDF in Adobe Reader.
2.  Zoom in on the figure
3.  Choose `Tools` → `Select and Zoom`
4.  Open Paint
5.  Paste Picture
6.  Save as `authorYYYYabc\_figX.jpg`
7.  Open Get Data
8.  `File` → `open` open figure
9.  Select button with two arrows (fourth from left)
10. Follow instructions to select x min, x max, y min and y max. If the
    x-axis has a categorical variable, it does not matter what values
    you use for x min and x max.
11. Make sure to set the correct values for the max and min of each
    axis, and indicate if the axis is log-scaled
12. Select the target button (seven from left)
13. Click over center of desired data points and error bars
14. Copy data to a Google spreadsheet. See [Google Spreadsheets] (#Section 3).
15. Calculate SE as the distance between the error bar upper bound and
    the mean (absolute value of difference between the two points)
