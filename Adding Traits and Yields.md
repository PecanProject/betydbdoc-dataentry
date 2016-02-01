# [Adding a Trait](https://www.betydb.org/traits/new) 

![](figures/Addnewtrait1/Addnewtrait1.jpg)



In general, a 'trait' is a phenotype (a characteristic that the plant
exhibits). The traits that we are primarily interested in collecting
data for are listed in Table \ref{tab:traits}. Before adding trait data, it is necessary to have the citation, treatments, and site information already entered. If the correct
citation is not identified at the top of the page [Figure 8](#Figure 8). To add a new Trait,
go to the [new trait](http://www.betydb.org/traits/new)
page: `Trait` → `new`.

Presently, we are also using the Trait table to record ecosystem level
measurements other than Yield. Such ecosystem level measurements can
include leaf area index or net primary productivity, but are only
collected when required for a particular project. Most of the fields in the Traits table are also used in the Yields table. Here is a list of the fields with a brief description, followed
by more thorough explanations:


* **Species**: Search for species in the database using the search box; if species
    is not found, then the new species should be added to the database. 
* **Cultivar**:   primarily used for crops; If the cultivar being used is not found in
    drop-down box  
* **DateLOC**:   Date Level of confidence. See for values.  
* **TimeLOC**:   Time Level of confidence. See for values.
* **Mean**:  For yield, mean is in units of tons per hectare per year (t/ha)  
* **Stat name**:   is the name of the statistical method used (usually one of SE, SD, MSE,
    CI, LSD, HSD, MSD). See for more details.  
* **Statistic**:   is the value of the statistic associated with Stat name.  
* **N**:   Always record N if provided. N is the number of experimental
    replicates, often referred to as the sample size; N represents the
    number of independent units within each treatment: in a field
    setting, this is often the number of plots in each treatment, but in
    a greenhouse, growth chamber, or pot-study this may be the number of
    chambers, pots, or individual plants. Sometimes this value is not
    clearly stated.
  

## Uncertainty in Date or Time

### DateLOC

The date level of confidence (DateLOC, Table \ref{tab:dateloc}) provides an indication of how accurately the date associated with the trait or yield observation is known. 
It provides the values that should be entered in this field. 
If the event occurred at a level of precision not defined by an integer in this table, then use fractions. For example, we commonly use 5.5 to indicate a one week level of precision. 
If the exact year is not known, but the time of year is, then use 91 to 97, with the second digit to indicate the information known within the year.




**Table Date level of confidence (DateLOC) field** Numbering convention for the DateLOC (Date level of confidence) and TimeLOC (Time level of confidence) field, used in managements, traits, and yields table. 

| Dateloc | Definition |
|:--------|:-----------|
| 9 | no data |
| 8 | year |
| 7 | season |
| 6 | month |
| 5 | day |
| 95 | unknown year, known day |
| 96 | unknown year, known month |
| ...etc | | 




### TimeLOC

The time level of confidence (TimeLOC) provides an indication of how accurately the time associated with the trait or yield observation is known. 
It provides the values that should be entered in this field. 

| Timeloc | Definition |
|:--------|:-----------|
| 9 | no data |
| 4 | time of day i.e. morning, afternoon |
| 3 | hour |
| 2 | minute |
| 1 | second |


## Statistics

Our goal is to record statistics that can be used to estimate standard
deviation or standard error (https://www.authorea.com/users/5574/articles/6811/). 
Many different methods can be used to summarize data, and this is reflected in the diversity of statistics that are reported. 
An overview of these methods is given in a
description below.

Where available, direct estimates of variance are preferred, including
Standard Error (SE), sample Standard Deviation (SD), or Mean Squared
Error (MSE). SE is usually presented in the format of mean 
(±SE). MSE is usually presented in a table. When
extracting SE or SD from a figure, measure from the mean to the upper or
lower bound. This is different than confidence intervals and range
statistics (described below), for which the entire range is collected.

If MSE, SD, or SE are not provided, it is possible that LSD, MSD, HSD,
or CI will be provided. These are range statistics and the most
frequently found range statistics include a Confidence Interval (95%CI),
Fisher’s Least Significant Difference (LSD), Tukey’s Honestly
Significant Difference (HSD), and Minimum Significant Difference (MSD).
Fundamentally, these methods calculate a range that indicates whether
two means are different or not, and this range uses different approaches
to penalize multiple comparisons. The important point is that these are
ranges and that we record the entire range.

Another type of statistic is a “test statistic”; most frequently there
will be an F-value that can be useful, but this should not be recorded
if MSE is available. Only if there is no other information available should you
record the P-value.


# [Adding a Yield](http://www.betydb.org/yields/new)

The protocol for entering yield data is identical to entering data for a
trait, with a few exceptions:

1.  There are no covariates associated with yield data

2.  Yield data is always the dry harvestable biomass; if necessary,
    moisture content can be added as a trait

Yield is equivalent to aboveground biomass on a per-area
basis, and has units of Mg ha^-1 y^-1  


# [Adding a Covariate](http:www.betydb.org/covariates/new)

Covariates are required for many of the traits. Covariates generally
indicate the environmental conditions under which a measurement was
made. Without covariate information, the trait data will have limited
value.

A complete list of required covariates can be found in Table \ref{tab:covariates}. For all
respiration rates and photosynthetic parameters, temperature is recorded
as a covariate. Soil moisture, humidity, and other such variables that
were measured at the time of the measurement may be required in
order to standardize across studies.

When root data is recorded, the root size class needs to be entered as a
covariate. The term ’fine root’ often refers to the \(<\)2mm size class,
and in this case, the covariate `root_maximum_diameter` would be set to 2. 
If the size class is a range, then the `root_minimum_diameter` can also be used.


