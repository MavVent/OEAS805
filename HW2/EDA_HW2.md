# OEAS805 Homework 2: EDA and environments

A new folder was created 'HW2' in C:\OEAS805\HW2

A environment was created called 'hw2_env'

## Part 1: EDA
### Size
The dataset has **77 rows** and **53 columns**
These cleanups took place over 36 sites in the Norfolk Area from September 2016 and October 2023
### Types
The variables were a mix of Strings, Floats, and Integers
Several columns were initially read as text due to large values containing commas. This was fixed loading with...
>thousands=','
### Missing Data
**No missing values** were discovered in any of the columns. Some 0's were observed and may be missing values stored as zeros.
### Descriptive stats
For total pounds, volunteer hours, and miles mean is well above median and skew is above 3.
The skew is strongly right, meaning most cleanups were small and a few large ones pulled the mean upwards. In this case, when looking at the data in summary the median would likely be a better measure of a typical cleanup.
Cigarette butts are most common item ~37,000 and ~20% of all items collected.
### Outliers
above 1.5 standard deviations there are outliers in all summary variables:
7 above average cleanups in Total Pounds of Litter Collected
8 above average cleanups in Volunteer hours
The largest of cleanups was Barraud Park at 2,545 lbs taking 132 volunteers in 2017.
### Between Variable relations
Volunteer hours and number of volunteers strongly correlated (0.91) which was expected assuming cleanups lasted the same amount of time.
Numver of miles is very weakly correlated with litter collected ~0.2 which was *UNEXPECTED* meaning site litter density varies vastly.
### Initial conclusions
Litter collected mainly reflects effort. To compare sites fairly we must normalize to effort like pounds/volunteer_hours.
Small items dominate, ie cigarette butts.
A few large scale (lots of volunteers) cleanups (mainly at Barraud Park) drive **Total** values disproportionatly.
Uneven visits to each site would make time based comparison highly untrustworthy.