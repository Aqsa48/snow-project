SWE2HS calibration and validation data
======================================

The data in this repository was used for the calibration and validation of the 
SWE2HS model in the following publication:

Aschauer, J., Michel, A., Jonas, T., & Marty, C. (2023). An empirical model to 
calculate snow depth from daily snow water equivalent: SWE2HS 1.0. Geoscientific 
Model Development Discussions, 1-19. https://doi.org/10.5194/gmd-2022-258

Contains daily snow water equivalent and snow depth timeseries from stations in 
the European Alps.

Contents
--------

The following files are included:

- automatic_stations_validation_data.csv

  Daily data from the automatic weather stations used for validation.

  Data sources and providers are listed in the SWE2HS paper, Table 1.

  Columns:
    - date: timestamp of the format YYYY-MM-DD
    - HS_[m]: snow depth in [m]
    - SWE_[m]: snow water equivalent in [m]
    - site_id: code for the measurement site
    - HS_interpolated: boolean flag for interpolated values
    - SWE_interpolated: : boolean flag for interpolated values

- coordinates_swe2hs_paper_stations.csv

  Coordinates of all measurement sites used in the SWE2HS paper.

  Columns:
    - site_id: code for the measurement site
    - location_name: location name of the measurement site
    - lon_[wgs84]: longitude in WGS84
    - lat_[wgs84]: latitude in WGS84
    - elevation_[m]: atitude of the measurement site in [m]
    - dataset: dataset in which the station is included

- manual_station_calibration_data.csv

  Calibration data from the Swiss manual observer stations. Long station records
  trmmed to 15 random water-years.

  Columns:
    - date: timestamp of the format YYYY-MM-DD
    - HS_[m]: snow depth in [m]
    - SWE_[m]: snow water equivalent in [m]
    - SWE_from_profile_[m]: biweekly measurement from the SWE in the measurement 
      pit. Corrected with the bulk density in order to  match the snow depth from 
      the measurement stake. Please refer to the paper for further details.
    - site_id: code for the measurement site

- manual_stations_validation_data.csv

  Validation data from the Swiss manual observer stations. Remaining water-years
  from the long sttaion record not used for the calibration data.

  Columns:
    - date: timestamp of the format YYYY-MM-DD
    - HS_[m]: snow depth in [m]
    - SWE_[m]: snow water equivalent in [m]
    - SWE_from_profile_[m]: biweekly measurement from the SWE in the measurement 
      pit. Corrected with the bulk density in order to  match the snow depth from 
      the measurement stake. Please refer to the paper for further details.
    - site_id: code for the measurement site

- manual_stations_used_deltasnow_parameters.csv

  Site specific DeltaSNOW model parameters used for the calculation of the daily 
  SWE series in 'manual_stations_calibration_data.csv' and 
  'manual_stations_validation_data.csv'.

  Parameters were optimized by reducing RMSE to the biweekly snow pit SWE measurements. 
  Please refer to the paper for further details.

  A python implementation of the DeltaSNOW model was used for the calculation:
  pydeltasnow (https://pypi.org/project/pydeltasnow/)

  For a detailed description of the DeltaSNOW model parameters please see the 
  respective publication:

  Winkler, M., Schellander, H., & Gruber, S. (2021). Snow water equivalents 
  exclusively from snow depths and their temporal changes: the Δ snow model. 
  Hydrology and Earth System Sciences, 25(3), 1165-1187.

  Columns:
    - site_id: code for the measurement site
    - rho_max: Maximum density of an individual snow layer produced by the DeltaSNOW model in [kg/m3]
    - rho_null: Fresh snow density for a newly created layer [kg/m3
    - c_ov: Overburden factor due to fresh snow [-]
    - k_ov: Defines the impact of the individual layer density on the compaction due to overburden [-]
    - k: Exponent of the exponential-law compaction [m3/kg]
    - tau: Uncertainty bound [m]
    - eta_null: Effective compactive viscosity of snow for “zero-density” [Pa s]
