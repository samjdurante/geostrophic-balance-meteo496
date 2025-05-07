
## Geostrophic Balance Evaluation in AI Weather Models

These scripts evaluate whether AI-generated weather forecasts preserve geostrophic balance

Geostrophic wind vectors are calculated from the model's inferred geopotential and compared to the model's inferred wind vectors. Pearson correlation and Root Mean Squared Error are calculated and graphed.

*Note: scripts currently only support panguweather and fourcastnet*

## Requirements
For script:
- Tested in a Jupyter Notebook with the Python 3.12 Kernel
For input:
- ECMWF's ```ai-models``` package for the model forecasts https://github.com/ecmwf-lab/ai-models (tested with version 0.7.4)
- ```ncl``` for GRIB to NetCDF conversion https://www.ncl.ucar.edu/Download/ (tested with version 6.6.2)

## Usage
Create a forecast using ai-models. For example, 
 
```ai-models --input cds --date 20241201 --lead-time 480 panguweather ```

Convert the output from .grib  to .nc 

```ncl_convert2nc panguweather.grib -L -nc4```

Place the netCDF file in the current working directory and run the Jupyter notebook

## Notebooks

- ```balance-panguweather.ipynb``` – for panguweather forecasts
- ```balance-fourcastnet.ipynb``` – for fourcastnet forecasts

The main difference is the naming for the pressure coordinate variables
- panguweather uses ```lv_ISBL0```
- fourcastnet uses ```lv_ISBL4``` for geopotential and ```lv_ISBL2``` for wind

Otherwise, both scripts are functionally identical.

## Note
- Latitudes between -5° to 5°, and beyond ±80° are excluded from the correlation / RMSE calculation to avoid instability (this can be changed)
- The code samples every 10th latitude / longitude to reduce compute time (can also be changed)
- The real / calculated wind data structures can be saved to disk to avoid recalculating in the future
