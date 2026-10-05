# OEAS805 LTS(Lafayette Time Series)

This project aims to relate dry wind events to chlorophyll flux in the Lafayette river. To explore this relationship, I use historical continuous monitoring data of: Vertical profiles, Continuous in-situ monitors, and extracted nutrient and chlorophyll data comparing to Norfolk International Airport, VA (ASOS/AWOS - AKQ) wind data spanning from 2015 to 2026. Portions of this data were collected by myself however a majority of the data is a result of many collaborators within the Mulholland Lab at Old Dominion University. This analysis aims to justify future research in hydrodynamic affects on HAB (Harmful Algae Bloom) initiation via sediment resuspension and the associated impacts on water quality. 

## Data
	KORF_2015-2025.csv Scrapped using Data Scraper Loop on **Iowa Environmental Mesonet**
	Access: https://mesonet.agron.iastate.edu/request/download.phtml

	NYCC_TS_2015_2025_Master.xlsx QA/QC'ed By Mav Ventura from Mulholland Lab Lafayette Continuous Monitoring Project
	Access: Proprietary 

	2015_2025_Vert.csv from Mulholland Lab Lafayette Continuous Monitoring Project utilizing Exo2 YSI's and 6600's
	Access: Proprietary

## EDA Conclusions
### Wind Data
	Wind data is very clean, and only ~1% is nan, for hourly measurements overt the course of 10 years this is fantastic.
	Wind speed shows a right skew and a gap at low wind speeds. This indicates some sort of instrument bottom detection limit that should be considered in following analysis.
	Wind direction seems bimodal with apex's at ~35 and 220 degrees. This makes sense as the area is largely impacted by Nor' Easters.
### Vertical Profiles
	Vertical Profiles contain some outlier data in Turbidity and Chlorophyll. Chlorophyll data will need to be corrected to extracted values in the "TS" (Time Series) dataset.
	Turbidity does not appear to be comparable between the instruments as the range and precision do not match between Exo2 and the 6600V2.
	Depth between the two instruments is comparable with similar ranges. EXO2's histogram shows a large spike at 0-0.2m indicating the upper limits of the YSI's may need to be corrected with atmospheric pressure.
### Nutrient/Chl Time Series
	Nutrient/Chl Time Series data is very clean with >75% valid cells in all variables except TDN. This is expected as TDN has been notoriously "difficult" with SOP's lost between students. The TDN variable will not be usable across this timescale but may be an interesting variable to look at for a nitrogen budget. As it appears to be normally distributed.
	All other variables showed a right skew and that many are low or below detection limit. This indicates that the nutrient suite we are analyzing are likely the ones that are preferentially taken up by microbiota.
	Chlorophyll-a (extracted chlorophyll in ug/L) show an average of ~40 uM  with some distinct spikes durring what appears to be mid summer of several years. These are likely blooms which makes sense in context of recent years as we have not observed a bloom since 2020. 
### Spatial and Temporal Coverage
	Wind data spanned the entire time with hourly intervals and few Nan values. Nutrients and Chl show primarily summer sampling was performed, with no distance gap between sample days. Vertical profiles followed almost exactly the same distribution as the Nutrient/chl-a dataset. In the perspective of season, most sampling occurred from June through August and partially in September. Thus, cross year comparison can only work between these months. For time of day, Vertical Profiles and Nutrient/Chla again fall short. A majority of the sampling occurred between 9 and 15:00, with most of these occurring from 13-15:00. Thus comparisons our resolution for "good" data will be larger than hourly timescale. 
	Spatially, All of these sample should have occurred at the same location, NYCC (Norfolk Yacht and Country Club) However, some vertical profiles show a maximum depth of >6m which is unlikely unless severe flooding at NYCC. This indicates these vertical profiles may have been mislabeled or the depth sensor was not working. This will be need to be investigated further prior to analysis.

