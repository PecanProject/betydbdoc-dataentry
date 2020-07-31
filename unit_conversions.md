
# Common Unit Conversions

For many transformations, particularly when automated, please use the udunits2 software where possible. For example, in R, you can use

    library(udunits2)
    ## transform meters to mm
    ud.convert(10, "m", "mm")
    ## equivalently, via the udunits synonym database
    ud.convert(10, "meters", "millimeters")
    ## it can also handle more complex units
    ud.convert(10, "m/s", "mm/d")

NB: Many of these conversions have been automated within [PEcAn](https://github.com/PecanProject/pecan){target="_blank"}.


Table: Useful conversions for entering site, management, yield, and trait data [**To-Do: Fix these!**]

| From (\(X\)) | to (\(Y\)) | Conversion | Notes |
|:-----------|:---------|:-----------|:------|
| \(X_2=\) root production | \(X_1=\) root biomass & root turnover rate | \(Y = X_2/X_1\) | Gill (2000) |
| DD\(^{\circ}\) MM' SS'' | XX.ZZZZ | \(\textrm{XX.ZZZZ} = \textrm{DD} + \textrm{MM}/60+\textrm{SS}/3600\) | to convert latitude or longitude from degrees, minutes, seconds to  decimal degrees |
| lb | kg | \(Y=X\times 2.2\) | |
| mm/s | \(\mu\) mol CO\(_2\) m\(^{2}\) s\(^{-1}\) | \(Y=X\times 0.04\) | |
| m\(^2\) | ha | \(Y = X/10^4\) | |
| g/m\(^2\) | kg/ha | \(Y=X\times 10\) | |
| US ton/acre | Mg/ha | \(Y = X\times 2.24\) | |
| m\(^3\)/ha | cm | \(Y=X/100\) | units used for irrigation and rainfall |
| % roots | root:shoot (q) | \(Y=\frac{X}{1-X}\) | \(\% \text{roots} = \frac{\text{root biomass}}{\text{total biomass}}\) |
| \(\mu\) mol cm\(^{-2}\) s\(^{-1}\) | mmol m\(^{-2}\) s\(^{-1}\) | \(Y = X/10\) | |
| mol m\(^{-2}\) s\(^{-1}\) | mmol m\(^{-2}\) s\(^{-1}\) | \(Y = X/10^6\) | |
| mol  m\(^{-2}\) s\(^{-1}\) | \(\mu\) mol cm\(^{-2}\) s\(^{-1}\) | \(Y = X/ 10^5\) | |
| mm s\(^{-2}\) | mmol m\(^{-3}\) s\(^{-1}\) | \(Y=X/41\) | Korner et al. [1988] |
| mg CO\(_2\) g\(^{-1}\) h\(^{-1}\) | \(\mu\) mol kg\(^{-1}\) s\(^{-1}\) | \(Y = X\times 6.31\) | used for root\_respiration\_rate |
| \(\mu\) mol | mol | \(Y= X\times 10^6\) | |
| julian day (1--365) | date | | see [https://www-air.larc.nasa.gov/tools/jday.htm](https://www-air.larc.nasa.gov/tools/jday.htm){target="_blank"} (NASA Julian Calendar)
| spacing (m) | density (plants m\(^{2}\)) | \(Y=\frac{1}{\textrm{row spacing}\times\textrm{plant spacing}}\)  | |
| kg ha\(^{-1}\) y\(^{-1}\) | Mg ha\(^{-1}\) y\(^{-1}\) | \(Y= X/1000\) | |
| g m\(^{-2}\) y\(^{-1}\) | Mg ha\(^{-1}\) y\(^{-1}\)  | \(Y= X/100\) | |
| kg | mg | \(Y=X\times 10^6\) | |
| cm\(^2\)  | m\(^2\) | \(Y=X\times 10^4\)  | |

