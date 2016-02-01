#  Reference Tables



**Table \ref{tab:dateloc}: Date level of confidence (DateLOC) field** Numbering convention for the DateLOC (Date level of confidence) and TimeLOC (Time level of confidence) field, used in managements, traits, and yields table. \label{tab:dateloc}.

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


| Timeloc | Definition |
|:--------|:-----------|
| 9 | no data |
| 4 | time of day i.e. morning, afternoon |
| 3 | hour |
| 2 | minute |
| 1 | second |

 

**Table \ref{tab:stats}: List of statistical summaries** \label{tab:stats} List of the statistics that can be entered into the statname field of traits and yields tables. Please see David (or Mike) if you have questions about statistics that do not appear in this list. If you have P, or LSD in a study with \(n\neq b\) (e.g. not a RCBD, see Table 8), please convert these values prior to entering the data, and add a note that stat was transformed to the table. Note: These are listed in order of preference, e.g., if SD, SE, or MSE are provided then use these values.

| Statname | Name | Definition | Notes |
|:----------|:-----|:-----------|:------|
| SD | Standard Deviation | \(\sqrt{\frac{1}{N} \sum{(x_i - \bar{x})^2}}\) | \(\bar{x}\) is the mean |
| SE | Standard Error | \(\frac{s}{\sqrt{n}}\)&  | |
| MSE | Mean Squared Error | | | like SD, but with multiple treatments; in R: \(\frac{mean(aov(y~x)\)residuals{^2}\(/{aov(y~x)df}\) |
| 95\%CI | 95% Confidence Interval| \(t_{1-^{\alpha}/_2,n}*s\) | measure the 95% CI from the mean, this is actually \(^1/_2\) of the CI |
| LSD | Least Significant Difference | \(t_{1-\frac{\alpha}{2},n}\sqrt{2\text{MSE}/b}\) | \(b\) is the number of blocks (Rosenberg 2004) |
| MSD | Minimum Significant Difference |  |  |


**Table \ref{tab:traits} Key Trait Variables** \label{tab:traits}

| Variable | Units | Median (90%CI) or Range | Definition |
|:---------|:------|:------------------------|:-----------|
| Vcmax | \(\mu\) mol CO\(_2\) m\(^{2}\) s\(^{-1}\) | \(44 (12, 125)\) | maximum rubisco carboxylation capacity |
| SLA | m\(^2\) kg\(^{-1}\) | \(15(4,27)\) | Specific Leaf Area area of leaf per unit mass of leaf |
| LMA | kg m\(^{-2}\) | \(0.09 (0.03, 0.33)\) | Leaf Mass Area (LMA = SLM = 1/SLA) mass of leaf per unit area of leaf |
| leafN | % | \(2.2(0.8, 17)\) | leaf percent nitrogen |
| c2n leaf | leaf C:N ratio | \(39(21,79)\) | use only if leafN not provided |
| leaf turnover rate | 1/year | \(0.28(0.03,1.0) \) | |
| Jmax | \(\mu\) mol photons m\(^{-2}\) s\(^{-1}\) | \(121(30, 262)\) | maximum rate of electron transport |
| stomatal slope | | \(9(1, 20)\) | |
| GS | | | stomatal conductance (= gs\(_{\textrm{max}}\) |
| q* | | 0.2--5 | ratio of fine root to leaf biomass |
| **grasses* | ratio of root:leaf = below:above ground biomass | | |
| aboveground biomass | g m\(^{-2}\) *or* g plant\(^{-1}\) | | |
| root biomass | g m\(^{-2}\) *or* g plant\(^{-1}\) | | |
| **trees* | ratio of fine root:leaf biomass | | |
| leaf biomass | g m\(^{-2}\) *or* g plant\(^{-1}\) | | |
| fine root biomass (<2mm) | g m\(^{-2}\) *or* g plant\(^{-1}\) | | |
| root turnover rate | 1/year | 0.1--10 | rate of fine root loss (temperature dependent) year\(^{-1}\) |
| leaf width | mm | 22(5,102) | |
| growth respiration factor | % | 0--1 | proportion of daily carbon gain lost to growth respiration |
| R\(_{\textrm{dark}}\) | | \(\mu\) mol CO\(_2\) m\(^{-2}\) s\(^{-1}\) | dark respiration |
| quantum efficiency | % | 0--1 | efficiency of light conversion to carbon fixation, see Farqhuar model |
| dark respiration factor | % | 0--1 | converts Vm to leaf respiration |
| seedling mortality | % | 0--1 | proportion of seedlings that die | 
| r fraction | % |0--1 | fraction of storage to seed reproduction |
| root respiration rate* | CO\(_2\) kg\(^{-1}\) fine roots s\(^{-1}\) | 1--100 | rate of fine root respiration at reference soil temperature |
| f labile | % | 0--1 | fraction of litter that goes into the labile carbon pool
| water conductance | | |


**Table \ref{tab:covariates}: Traits with required covariates** \label{tab:covariates} 
A list of traits and the covariates that must be recorded along with the trait value in order to be converted to a constant scale from across studies.*notes:* stomatal conductance (`gs`) is only useful when reported in conjunction with other photosynthetic data, such as `Amax`. 
Specifically, if we have `Amax` and `gs`, then estimation of `Vcmax` only covaries with `dark_respiration_factor` and atmospheric CO2 concentration.  
We also now have information to help constrain `stomatal_slope`. If we have `Amax` but not `gs`, then our estimate of `Vcmax` will covary with: `dark_respiration_factor`, `CO2`, `stomatal_slope`, `cuticular_conductance`, and vapor-pressure deficit `VPD` (which is more difficult to estimate than CO2, but still possible given lat, lon, and date). 
Most important, there will be a strong covariance between `Vcmax` and `stomatal_slope`.


| Variable | Required Covariates | Optional Covariates |
|:---------|:--------------------|:--------------------|
| vcmax |  temperature (leafT or airT) |irradiance |
|any leaf measurement | | canopy_height or canopy_layer |
| root\_respiration\_rate | temperature (rootT or soilT)| soil moisture |
| | root\_diameter\_max | root size class (usually 2mm) |
| any respiration | temperature | |
| root biomass | | min. size cutoff, max. size cutoff |
| root, soil | depth (cm) | used for max and min depths of soil, if only one value, assume min depth = 0; negative values indicate above ground |
| gs (stomatal conductance) | \(A_{max}\) | see notes in caption |
| stomatal\_slope (m) | humidity, temperature | specific humidity, assume leaf T =  air T | |SLA| | canopy_level|
 
