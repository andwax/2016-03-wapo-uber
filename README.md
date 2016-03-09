# 2016-03-wapo-uber

#[WaPo Title](www.wapo...) <- insert article URL
By [Jennifer A Stark](https://github.com/JAStark) and [Nick Diakopoulos](http://www.nickdiakopoulos.com)

This is a repository is meant to support transparency and reproducibility of the data analysis and visualization presented in the Washington Post article [" "](www.wapo...). <- insert article URL. 

If you have cloned this repo and downloaded the raw [Uber data](https://drive.google.com/folderview?id=0B-mutxqHY34rblhORk9raWxQQjQ&usp=sharing) (4 weeks),
you can reproduce the analysis in this [notebook](https://github.com/comp-journalism/2016-03-wapo-uber/blob/master/UberSurgePricing_OSC.ipynb). 

## The Data
### Collecting data with the Uber API
Data were collected using the Uber API with config.config and gatherUberData.py -
based on scripts of the same name from our [uberpy](https://github.com/comp-journalism/uberpy)
project. 

`config.config` was modified to collect data every 3 minutes, provided a list of 276
locations across DC, and provided a list of [Uber API](https://developer.uber.com/) keys. 

`gatherUberData.py` was modified to save data with the DC local datetime.

###Sampling the Data 
The method for determining the 276 locations in DC to sample used the following steps:
* A 22 x 22 grid of longitudes and latitudes was applied across DC
* Addresses were then associated with each point using `Nominatim` from `geopy.geocoders` (installed with `pip`). Any point not in DC was removed.
* Remaining addresses were then validated to require a house number and street prefix using `address.AddressParser` (installed with `pip`). This removed points that fell in the river or parks etc.
* Remaining points were then checked against DC census tract IDs to make sure that each tract was represented. 
* Tracts not represented were added using the census tract centerpoints provided from the Tiger Census 2010 database using `cenpy` (installed with `pip`). NB that `cenpy` only works in python2.7
* New tract center latitudes and longitudes were again address validated. Only 7 were not valid, and so those points were manually moved the smallest distance possible to a valid address. 

These points were sampled every 3 minutes for 4 weeks from February 3 to March 2, 2016.

###Data Dictionary
The following fields are available in the [data download](https://drive.google.com/folderview?id=0B-mutxqHY34rblhORk9raWxQQjQ&usp=sharing):
* **"timestamp"** : `string`, Date and Time (EST) when API was pinged
* **"surge_multiplier"**: `float`, The surge multiplier for the current time and location
* **"expected_wait_time"**: `integer`, The number of seconds rider may have to wait between requesting a car, and the car's arrival
* **"product_type"**: `string`, The type of car -
 - uberTAXI
 - UberSUV
 - UberBLACK
 - uberX + Car Seat
 - uberX
 - uberXL
 - SUV + Car Seat
 - BLACK CAR + Car Seat
* **"low_estimate"**: `integer`, lower end of an estimated price of the ride (dollars)
* **"high_estimate"**: `integer`, upper end of an estimated price of the ride (dollars)
* **"start_location_id"**: `integer`, number between 0-275 that relates to our predetermined longitudes and latitudes across DC.
* **"end_location_id"**: `integer`,  number between 0-275 that relates to our predetermined longitudes and latitudes across DC. 

#Requirements
If you use the Anaconda distribution, you're all set.

* Python 3 (does not work in python 2)
* ipython notebook / Jupyter
* pandas
* numpy
* matplotlib.pyplot
* scipy.stats  (for `pearsonr`)
* seaborn
* statsmodels.formula.api
* statsmodels.graphics.api (for `abline_plot`)

#Funding
This project was funded by a grant from the Tow Center for Digital Journalism to study computational and data journalism in the context of algorithmic accountability reporting. 

#Feedback
Email Jennifer A Stark at starkja@umd.edu
