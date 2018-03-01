## TwilightFree method of geolocation

A new method of geolocation using GLS tag (ambient light) data. TwilightFree has no explicit dependence on being able to estimate or identify the time of twilight, making it very robust to noise (sensor shading or obscuration) in the light data. It uses SST, plausible movement, land/sea masks, and fixes at known locations to improve position estimates.

Please cite:
Bindoff AD, Wotherspoon SJ, Guinet C, Hindell MA. Twilight-free geolocation from noisy light data. *Methods Ecol Evol.* 2017;00:1–9. https://doi.org/10.1111/2041-210X.12953  

Known bugs:  
- the default track using `trip(fit, type = "full")` returns the maximum *a posteori* estimate (MAP estimate) for each day. If possible locations straddle the equator, sometimes the MAP estimate for a particularly day is obviously in the wrong hemisphere (the algorithm picks a mathematically plausible but ecologically implausible solution). Calling `essieRaster(fit)` and finding the MAP estimate for the appropriate hemisphere is a useful solution, but a simpler solution is currently in development.  
- you may need to run `install.packages("raster", repos = "https://cran.csiro.au/")` before you can load TwilightFree or SGAT. If you already have `raster` installed, you may need to run `remove.packages("raster")` first and re-install it from the repo at CSIRO. It's one of the great mysteries.  
- if a location cannot be determined on a day, `trip` will fail. This prevents as mismatch between locations and days. `SGAT:essie` will also throw warnings.  


### Installation:  

`# install.packages("devtools")`  
`# install.packages("raster", repos = "https://cran.csiro.au/")`  
`devtools::install_github("SWotherspoon/SGAT")`  
`devtools::install_github("SWotherspoon/BAStag")`  
`devtools::install_github("ABindoff/TwilightFree")`  

Linux users (tested Ubuntu 17.10 Artful) may also need to install the following (from a terminal) in order to install `devtools` and `ncdf4` package:  
sudo apt-get install libssl-dev  
sudo apt-get install libcurl4-openssl-dev  

sudo apt-get install netcdf-bin  
sudo apt-get install libnetcdf-dev  
sudo apt-get install udunits-bin  
sudo apt-get install libudunits2-dev  

