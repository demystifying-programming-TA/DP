# Python - Part I 

*Session 3 Mini-Tutorial*


**Step 1: Define a skeleton function (```location_mobility_data```) in your ```dataprocessing.py``` script**

> Potential solution (your ```dataprocessing.py``` script)


```
# ------------------------------------------------------------------------ #
# Initialization
# ------------------------------------------------------------------------ #

# Load dependencies
# ---------------------------------------------#
import pandas as pd

# ------------------------------------------------------------------------ #
# Define Functions
# ------------------------------------------------------------------------ #

# location_mobility_data
# ----------------------------
def location_mobility_data(longitude, latitude):

	# Load the data
	mobility_df = pd.read_csv("backend/data/CoronaData.csv", 
		encoding="utf-8")

	# Reverse geocode (longitude, latitude > country)
	country = "United States"
	# Extract data for country

	# Extract data for walking & calculate change in # of walking calls
	walking_chg = 20
	
	# Extract data for driving & calculate change in # of driving calls
	driving_chg = 30
	
	# Return the results
	return([country, walking_chg, driving_chg])
```

<hr>

**Step 2: Import the ```dataprocessing.py``` script + execute the ```location_mobility_data``` function in your ```application.py``` script**

> Potential solution (your ```application.py``` script)

```
# ------------------------------------------------------------------------ #
# Initialization
# ------------------------------------------------------------------------ #

# Load dependencies
# ---------------------------------------------#
import sys
sys.path.append('Backend')
import dataprocessing as dp

# ------------------------------------------------------------------------ #
# Test Functions
# ------------------------------------------------------------------------ #

## Try the location_mobility_data() function
## Note: Longitude,latitude refer to the United States
data = dp.location_mobility_data(longitude = -71.08328259999999, 
	latitude = 42.3662154)
print("Country name: ", data[0])
print("Decrease in # of walking calls (%): " + str(data[1]))
print("Decrease in # of driving calls (%):" + str(data[2]))

# ------------------------------------------------------------------------ #
# ------------------------------------------------------------------------ #
```

<hr>

**Step 3: Use the ```geopy``` package to 'reverse geocode' the country based on the longitude/latitude**

> Potential solution (relevant section of your ```dataprocessing.py``` script)

```
	import geopy as gp


	# Reverse geocode (longitude, latitude > country)
	locator      = gp.geocoders.Nominatim(user_agent="myGeocoder")       
	coordinates  = str(latitude) + ", " + str(longitude)    
	geocode_data = locator.reverse(coordinates)             
	country      = geocode_data.raw['address']['country']   
```