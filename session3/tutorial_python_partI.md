# Python - Part I 

*Session 3 Mini-Tutorial*


**Step 1: Define a skeleton function (```location_mobility_data```) in your ```dataprocessing.py``` script**

> Hint

* **Start by thinking about the inputs and outputs**   
You want to define a function that takes as input the longitude and latitude of a user, and outputs (i) their country, (ii) the % change in walking direction calls (%) and (iii) the % change in driving direction calls. 

* **Identify the steps that will need to take place**   
The function will need to (i) import the dataset, (ii) reverse geocode the longitude and latitude to obtain the country, (iii) extract the data for the specific country from the dataset, (iv) extract the driving and walking direction call data, calculating the % change in each. *You know how to import a Pandas Dataframe, feel free to 'hard-code' the results of the other steps - we will build them out as we go.*

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
	country = "United States of America"
	
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

> Hint

* **Start by importing the 'dataprocessing' module**  
Think back to the modules/packages/libraries we discussed  - how did we import them into our main script? Was there anything unique about importing local modules?

* **Work out how to reference the ```location_mobility_data``` function**  
Think back to the modules we discussed  - how did we reference functions (defined within a module?


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
print("Decrease in # of driving calls (%): " + str(data[2]))

# ------------------------------------------------------------------------ #
# ------------------------------------------------------------------------ #
```

<hr>

**Step 3: Use the ```geopy``` package to 'reverse geocode' the country based on the longitude/latitude**

> Hint

* **Leverage your 'what to do when stuck skills?' to work out how the geopy package works**  
Try searching for e.g., the following keywords: "Python geopy package tutorial reverse geocoding". Your hits should include e.g., [this tutorial](https://towardsdatascience.com/reverse-geocoding-in-python-a915acf29eb6"). 

* **Apply the class, object, attribute framework to any sample code**  
Is it clear to you what each of the lines of code means?


> Potential solution (relevant section of your ```dataprocessing.py``` script)

```
	import geopy as gp


	# Reverse geocode (longitude, latitude > country)
	locator      = gp.geocoders.Nominatim(user_agent="myGeocoder")       
	coordinates  = str(latitude) + ", " + str(longitude)    
	geocode_data = locator.reverse(coordinates)             
	country      = geocode_data.raw['address']['country']   
```