# Estimating Standard Error from other summary statistics (_P_, _LSD_, _MSD_)


When conducting a meta-analysis that includes previously published data, differences between treatments reported with P-values, least significant differences (LSD), and other statistics provide no direct estimate of the variance.

In the context of the statistical meta-analysis models that we use, overestimates of variance are okay, because this effectively reduces the weight of a study in the overall analysis relative to an exact estimate, but provides more information than either excluding the study or excluding any estimate of uncertainty (though there are limits to this assumption).

Where available, direct estimates of variance are preferred, including Standard Error (SE), sample Standard Deviation (SD), or Mean Squared Error (MSE). SE is usually presented in the format of mean  (±SE). MSE is usually presented in a table. When extracting SE or SD from a figure, measure from the mean to the upper or lower bound. This is different than confidence intervals and range statistics (described below), for which the entire range is collected.

If MSE, SD, or SE are not provided, it is possible that LSD, MSD, HSD, or CI will be provided.
These are range statistics and the most frequently found range statistics include a Confidence Interval (95%CI), Fisher’s Least Significant Difference (LSD), Tukey’s Honestly
Significant Difference (HSD), and Minimum Significant Difference (MSD).
Fundamentally, these methods calculate a range that indicates whether two means are different or not, and this range uses different approaches to penalize multiple comparisons.
The important point is that these are ranges and that we record the entire range.

Another type of statistic is a “test statistic”; most frequently there will be an F-value that can be useful, but this should not be recorded if MSE is available. Only if there is no other information available should you record the P-value.

## Further Reading {-}

Many statistical transformations are implemented in the [`transformstats`](https://github.com/PecanProject/pecan/blob/master/base/utils/R/transformstats.R){target="_blank"} function within the PEcAn.utils package.
However, these transformations make conservative (variance inflating) assumptions about study-specific experimental design (especially degrees of freedom) that is not captured in the BETYdb schema, for example HSD, LSD, P.

More accurate estimates of SE can be obtained at time of data entry using the formulas in ["Transforming ANOVA and Regression statistics for Meta-analysis"](https://www.authorea.com/users/5574/articles/6811/){target="_blank"}.
