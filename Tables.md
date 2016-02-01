#  Reference Tables


 


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
 
