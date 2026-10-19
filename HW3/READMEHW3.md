# OEAS805 HW3

This homework looks at Chesapeake Bay Program Surface Water Quality Parameters from 2021-2026  while utilizing Machine Learning approaches to regression.

## Data
	CBP_TWQM_MAIN_WQ_2021_2026_surface.csv
	Access: https://datahub.chesapeakebay.net/Home/WaterQuality
		Source: CBP Water Quality Data (1984-present)
		Data Type: Water Quality Data
		Start Date: 01/01/2021
		End Date: 10/15/2026
		Data Stream: All Data
		Program: TWQM - Tidal Water Quality Monitoring Program
		Project: Main - Tidal Mainstem Water Quality Monitoring Project
		Geographical Attribute: Monitoring Station
		Attribute Selection: CB4.1C - Upper Chesapeake Bay
		Parameter: ALL
	Post Processing: Only surface samples were used


# Analyses
## Exploration
	I chose Chlorophyll-a as my target variable as I would like to predict algal blooms using other variables. In other words I want to be able to predict when blooms occur based on environmental data. The predictor variables I chose were DIN (Dissolved Inorganic Nitrogen), 
	PO4F (Phosphate), and TSS (Total Suspended Solids). The raw data is visualized in two ways: Variable-Target Scatter Plots in cell 5, and TimeSeries in cell 10. The variable-target plots showed grouping at low target values so I chose to log-transform the target parameter to see if the distribution would normalize. The variable-logTarget scatterplots are shown in cell 8. This provided little improvement in target distribution and did not improve the multiple linear regression model.


## Multiple Linear Regression (MLR)
	Plain MLR resulted in the equation: CHLA = +9.27*DIN +28.50*PO4F +0.30*TSS +9.64, (R-squared) = -0.15, at a test random state of 9 (Cell  6). This means that the model generated from the data could not accurately predict chlorophyll-a. The model severealy over estimated chlorophyll after 20ug/L. and was poorly constrained even at lower concentrations. This result was expected especially with the poor distribution of DIN, Phosphate, and TSS. Phosphate was often observed near detection limit so this could be the large source of poor constraints on this model. After log transforming chlorophyll- a the distribution on the y axis improved signifcantly but found  no improvement in the model. : log(CHLA) = +0.21*DIN -17.83*PO4F +0.01*TSS +1.02, (R-squared) = -0.17 (Cell 9).


## K-Nearest-Neighbors Regression (KNN)
	For this approach, I dropped Phosphate, and TSS, as they seemed to be the least related to Chlorophyll-a based on visual analysis of time series data in cell 9. By iteratively testing KNN with k values of 5, I incrementally identified the upper and lower bounds of model performance to be within 5-10. Then I went through each value 5-10 to identify that at a random state of 14, the best k (# of nearest neighbors) was 9. giving an r^2 value of 0.01. This was a touch better than MLR in terms of model performance but seriously lacked for two reasons. 1, the model was not showing variability very well, this is likely due to How KNN works, but averaging the nearest k of samples. Additionally, the model seems to be severely affected by outliers or extreme values, in this case I do not believe they are outliers but extreme values. If you expect smooth transitions betweeen variables for whatever reason, I think KNN would be a good statistical tool to use.

## Multi-Layer Perceptron (MLP)
	This approach also only utilizes DIN to predict Chlorophyll-a. Testing from 10-100 nodes I found 25 to be the ideal number of nodes giving a training r^2 of 0.79 (well constrained) but giving a test, r^2 of -0.41. When looking at the model, I found this test r^2 to not be a good indicator of model success (cell 30). The model appears to predict high variability at low concentrations (0.0-0.1)mg/L DIN and at higher concentrations (0.4-0.5)mg/L. while remining realatively stable with low concentrations of chlorophyll in between and a stable higher beyond. Intiutively this makes sense as blooms rely on nitrogen to occur, but secondarily rely on phosphate to occur. Thus, the two states of high variability coincide with this theory.