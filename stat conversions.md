**How to convert statistics from \(P\), \(LSD\), or \(MSD\) to \(SE\)**

Many statistical transformations are implemented in the [transformstats](https://github.com/PecanProject/pecan/blob/master/utils/R/transformstats.R) function within the PEcAn.utils package. 
However, these transformations make conservative (variance inflating) assumptions about study-specific experimental design (especially degrees of freedom) that is not captured in the BETYdb schema, for example HSD, LSD, P.

More accuate estimates of SE can be obtained at time of data entry using the formulas in ["Transforming ANOVA and Regression statistics for Meta-analysis"](https://www.authorea.com/users/5574/articles/6811/).