# GENERAL INFORMATION

### Dataset Title: 

- *Dataset accompanying "Observing formation and early evolution of contrails formed by IAGOS aircraft using high-resolution LEO satellite imagery"*

### Authors: 

* Thymen Woldhuis ([@ThymenW](https://github.com/ThymenW), ![ORCID logo](https://info.orcid.org/wp-content/uploads/2019/11/orcid_16x16.png) [0009-0000-2237-1839](https://orcid.org/0009-0000-2237-1839), t.woldhuis-1@tudelft.nl, Technische Universiteit Delft.
* Vincent Meijer
* Zebediah Engberg
* Susanne Rohs

## DESCRIPTION

This dataset supports the study of contrail formation and early evolution using high-resolution Low Earth Orbit (LEO) satellite imagery *collocated* with in situ aircraft observations. It combines data from Copernicus Sentinel-2 (2016-2022) and Landsat (2013-2022) with atmospheric and aircraft position measurements from In-service Aicraft for a Global Observing System (IAGOS) equipped aircraft. 

The data has been organized into subfolders, each describing a single *collocation* (i.e. individual case in which an IAGOS-equipped aircraft is detected within the field of view of a satellite image). The collocations were found by running [pycontrails intersection function](https://py.contrails.org/notebooks/Sentinel.html) on the [IAGOS flight trajectory data](https://www.iagos.org/iagos-data/). The dataset comprises a total of 421 Sentinel-2 collocations and 342 Landsat collocations.

For each collocation, the dataset contains:  

- IAGOS flight trajectory   
- ERA5 meteorological data  
- Satellite imagery   
- Metadata describing the collocation   
    - Satellite information (e.g. sensing time, platform, crs, extent, directory to image location)  
    - Annotations (e.g. contrail formation (yes/no) and contrail labels)   
    - Directory paths and filenames for the associated IAGOS and ERA5 data files  

The dataset accompanies the paper: *Observing formation and early evolution of contrails formed by IAGOS aircraft using high-resolution LEO satellite imagery*, which can be found at https://egusphere.copernicus.org/preprints/2026/egusphere-2026-1171/ .

**Keywords:** Contrails - Remote Sensing - Sentinel-2 - Landsat - IAGOS - SAC - CoCiP

**Date of data collection (YYYY-MM-DD):** 2025-02-01 until 2025-12-31

**Date of dataset publication (YYYY-MM-DD):** 2026-06-29
	
**Funding:** The project has been funded by Technische Universiteit Delft (TU Delft)


## ACCESS INFORMATION

### License

The data available in this repository is released under a Creative Commons Attribution 4.0 International licence (CC BY 4.0). See legal code [here](https://creativecommons.org/licenses/by/4.0/legalcode). 

### Dataset DOI

Dataset DOI: [10.4121/2d66d65e-8041-4435-ab3c-0af3fdfc5d23](https://doi.org/10.4121/2d66d65e-8041-4435-ab3c-0af3fdfc5d23)

### Attribution Notice

This dataset includes:

- Copernicus Sentinel-2 L1C data (2016-2022)  
- Modified Copernicus Sentinel data (2016-2022)  
- Landsat data (2013-2022)  
- IAGOS in-service aircraft measurements (2013-2022) 
- ERA5 climate data from Copernicus Climate Change service  


## VERSIONING AND PROVENANCE

**Last modification date (YYYY-MM-DD):** 2026-06-29
 

## METHODOLOGICAL INFORMATION

**Description of data collection methods:**

- Download all IAGOS flights from 2013 until the end of 2022.   
- Run the [pycontrails intersection function](https://py.contrails.org/notebooks/Sentinel.html) for both the Landsat and Sentinel-2 to find which flights are visible in the satellite imagery.  
- Download and annotate the contrail in each satellite image. **Note:** for Sentinel-2, this was done with the [Copernicus Browser Hub](https://browser.dataspace.copernicus.eu/) to avoid downloading every file; and for Landsat this was done with a database hosted on a Google Cloud server.  
- Append IAGOS and ERA5 weather data to useful annotations.  
- Run Aircraft Performance Models (APMs) on the flights.  

All derived collocations can be found in a csv file in the related code repository (see `landsat_sentinel_collocations_20260216.csv` in [[10.4121/a1e4d5b4-5af2-4a13-8152-a1e8d49c297f]](https://doi.org/10.4121/a1e4d5b4-5af2-4a13-8152-a1e8d49c297f).  


**Methods for processing the data:**

The code used to process the data is archived at the [4TU.ResearchData](https://doi.org/10.4121/a1e4d5b4-5af2-4a13-8152-a1e8d49c297f). Ongoing development and  improvements of the code are maintained in [GitHub](https://github.com/ThymenW/IAGOS_Sentinel2_Landsat_Collocations).  

The code repository contains the Python toolkit with the functionalities used to process the data, as well as Jupyter notebooks to reproduce the figures of the related article, Woldhuis et al. (2026) (see **REFERENCES**).  


## FILE OVERVIEW

Directory structure of `collocations`:

```
.
├── intersects_landsat
│   └── {year}
│       └── {collocation_id}
│           ├── {IAGOS_id}.nc4
│           ├── arco-era5-cc.nc4
│           ├── arco-era5.nc4
│           └── metadata.json
└── intersects_sentinel
    └── {year}
        └── {collocation_id}
            ├── {IAGOS_id}.nc4
            ├── arco-era5-cc.nc4
            ├── arco-era5.nc4
            ├── imagery
            │   ├── DATASTRIP
            │   │   └── *.xml
            │   ├── GRANULE
            │   │   ├── *.xml
            │   │   └── QI_DATA
            │   │       └── *.jp2
            │   ├── b10*.png
            │   └── rgb*.png
            └── metadata.json
```

Files are structured per collocation. Each collocation contains:  

- `{IAGOS_id}.nc4`: .nc4 files containing IAGOS flight trajectory data and measurements.  
- `arco-era5(-cc).nc4`: ERA5 data for 1 hour before and after the sensing time. `cc` indicates that the weather product contains the `cloud cover` parameter as well. Only downloaded collocations in the final analysis (see paper). 
- `imagery/`: folder containing image data for Sentinel-2.  
- `metadata.json`: file containing the satellite information, annotations, IAGOS and ERA5 paths.  

DATASTRIP and GRANULE folders represent the metadata used to do the improved Sentinel/Landsat collocations. The location has been moved to the `pycontrails` cache folder halfway through the project, but these are still there for testing.


## ACKNOWLEDGEMENTS 

This project used IAGOS data for which the following acknowledgements apply:  

* The European Commission for their support of earlier projects since 1993.   
* The partner institutions of the IAGOS Research Infrastructure : FZJ, DLR, MPI, KIT in Germany, CNRS, Météo-France, Université Paul Sabatier in France and University of Manchester in United Kingdom.   
* AERIS, the French Data and Services cluster for Atmosphere, for hosting the data centre.  
* The participating airlines (Lufthansa, Air France, China Airlines, Iberia, Cathay Pacific, Hawaiian Airlines) for the provision of free transport of the instrumentation.  


## REFERENCES

**Sentinel-2:** 

Drusch, M., Del Bello, U., Carlier, S., Colin, O., Fernandez, V., Gascon, F., Hoersch, B., Isola, C., Laberinti, P., Martimort, P., Meygret, A., Spoto, F., Sy, O., Marchese, F., and Bargellini, P.: Sentinel-2: ESA’s Optical High-Resolution Mission for GMES Operational Services,Remote Sensing of Environment, 120, 25–36, https://doi.org/10.1016/j.rse.2011.11.026, 2012.

**Landsat:**

Irons, J. R., Dwyer, J. L., and Barsi, J. A.: The next Landsat satellite: The Landsat Data Continuity Mission, Remote Sensing of Environment, 122, 11–21, https://doi.org/10.1016/j.rse.2011.08.026, 2012.  

U.S. Geological Survey. Landsat [satellite] [sensor] [processing level] data, acquired [date], [path/row or scene ID], retrieved from EarthExplorer, accessed [date].  

**IAGOS:** 

Petzold, A., Thouret, V., Gerbig, C., Zahn, A., Brenninkmeijer, C. A. M., Gallagher, M., Hermann, M., Pontaud, M., Ziereis, H., Boulanger, D., Marshall, J., Nédélec, P., Smit, H. G. J., Friess, U., Flaud, J.-M., Wahner, A., Cammas, J.-P., Volz-Thomas, A., and Team, I.: Global-scale atmosphere monitoring by in-service aircraft – current achievements and future prospects of the European Research Infrastructure IAGOS, Tellus B: Chemical and Physical Meteorology, 67, https://doi.org/10.3402/tellusb.v67.28452, 2015.

**ERA5:**

Hersbach, H., Bell, B., Berrisford, P., Hirahara, S., Horányi, A., Muñoz-Sabater, J., Nicolas, J., Peubey, C., Radu, R., Schepers, D., Simmons, A., Soci, C., Abdalla, S., Abellan, X., Balsamo, G., Bechtold, P., Biavati, G., Bidlot, J., Bonavita, M., De Chiara, G., Dahlgren, P., Dee, D., Diamantakis, M., Dragani, R., Flemming, J., Forbes, R., Fuentes, M., Geer, A., Haimberger, L., Healy, S., Hogan, R. J., Hólm, E., Janisková, M., Keeley, S., Laloyaux, P., Lopez, P., Lupu, C., Radnoti, G., de Rosnay, P., Rozum, I., Vamborg, F., Villaume, S., and Thépaut, J.-N.: The ERA5 global reanalysis, Quarterly Journal of the Royal Meteorological Society, 146, 1999–2049, https://doi.org/10.1002/qj.3803, _eprint: https://rmets.onlinelibrary.wiley.com/doi/pdf/10.1002/qj.3803, 2020.

**Poll-Schumann:**

Poll, D. and Schumann, U.: An estimation method for the fuel burn and other performance characteristics of civil transport aircraft in the cruise. Part 1 fundamental quantities and governing relations for a general atmosphere, The Aeronautical Journal, 125, 257–295, https://doi.org/10.1017/aer.2020.62, 2021a.

**BADA 4.2:**

EUROCONTROL: User manual for the base of aircraft data (BADA) family 4, EEC Technical/Scientific Report 12/11/22-58, EUROCONTROL Experimental Centre (EEC), https://www.eurocontrol.int/model/bada, 2016.