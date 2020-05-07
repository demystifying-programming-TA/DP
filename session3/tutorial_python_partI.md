# Python - Part I

*Session 3 Mini-Tutorial*

First, download the CoronaData.csv file from Canvas at the [following link](https://canvas.mit.edu/courses/3133/files/416511?module_item_id=80439). You will use this for the next two tutorials.

Make two blank scripts ```application.py``` and ```dataprocessing.py```.

We will use ```dataprocessing.py``` to process the data and to ```application.py``` execute the data processing. Place your ```application.py``` file in the same directory as your backend and frontend folders and place your ```dataprocessing.py``` file in your backend directory.

By the end of this tutorial we will have these scripts working with just part of the complete functionality.

## Building dataprocessing.py

**Step 1: Define your dependencies**

We will be using Pandas and Geopy in this script. Import these by typing the following:

```
import pandas as pd
import geopy as gp
```

**Step 2: Think about using a function and its inputs and outputs**

We want to use ```dataprocessing.py``` to do the heavy lifting for our other script ```application.py```. To do this, we can create a function in ```dataprocessing.py``` that takes as input the longitude and latitude of a user, and outputs (i) their country, (ii) the % change in walking direction calls (%) and (iii) the % change in driving direction calls.

We can start by defining the function as ```location_mobility_data``` and labeling our inputs:
```
def location_mobility_data(longitude, latitude):
```

**Step 3: Identify the steps that will need to take place within your function**   

The function will need to (i) import the dataset, (ii) reverse geocode the longitude and latitude to obtain the country, (iii) extract the data for the specific country from the dataset, (iv) extract the driving and walking direction call data, calculating the % change in each.

For now, let's only do part (i) and then just manually enter in placeholder numbers for the rest. We will add these functionalities later.

Import the dataset via the following code. Make sure to include the correct path to your csv file.
```
mobility_df = pd.read_csv("backend/data/CoronaData.csv", encoding="utf-8")
```
For the placeholder numbers we will need the following three variables:
```
# Reverse geocode (longitude, latitude > country)
country = "United States of America"

# Extract data for walking & calculate change in # of walking calls
walking_chg = 20

# Extract data for driving & calculate change in # of driving calls
driving_chg = 30
```
Lastly, we want to determine which outputs will be sent whenever the function is called. We can do this using the ```return()``` command at the end of our function. Whatever is contained within these parenthesis will be returned when the function is called. In this case we want to send the country name and the change in walking and driving, so our function could look like this:

```
return([country, walking_chg, driving_chg])
```

Okay! Now your ```dataprocessing.py``` script should look like the following:

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

That's good enough for now to test with. Let's work on ```application.py```.

<hr>

## Building application.py

**Step 1: Define your dependencies**

Note that we want to import ```dataprocessing.py``` in order to use its function in this script. However, we need to make sure that Python can find this script. To do this, we will use the ```sys``` module to define the path to ```dataprocessing.py``` using the ```sys.path.append()``` function so that python can find it. See below:
```
import sys
sys.path.append('Backend')
import dataprocessing as dp
```
**Step 2: Call the function**

To call a function, we write the *parent modules local name*, a ".", and then the *name of the function with parenthesis*. Like so: ```dp.location_mobility_data()``` To save the output of this function we can simply assign it to a variable, named for example ```data```. We know from our earlier work on ```dataprocessing.py``` that the output of the function will be ```[country, walking_chg, driving_chg]``` so we can also write some statements to display this information. We can pull individual parts of the output by indexing on the assigned variable knowing that the 0 index will refer to the first element of the output. So to get the country name, we would write ```data[0]``` if we had assigned it to ```data```.

Thus our code to call the function and print the relevant data could look like:
```
data = dp.location_mobility_data(longitude = -71.08328259999999,
	latitude = 42.3662154)
print("Country name: ", data[0])
print("Decrease in # of walking calls (%): " + str(data[1]))
print("Decrease in # of driving calls (%): " + str(data[2]))
```
At this point your script should look something like this:
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

Go ahead now and test your two scripts. If you did it correctly, you should be able to run ```application.py``` in your terminal and get the following output:
```
Country name:  United States of America
Decrease in # of walking calls (%): 20
Decrease in # of driving calls (%): 30
```
Okay, let's add one more functionality before we call it quits.

## Adding reverse geocoding to application.py

**Step 1: Define your dependencies**

To do reverse geocoding, we will need the geopy module. Import it by adding the following to your ```application.py``` file:
```
import geopy as gp
```

**Step 2: Initiate the Nominatim method and use to reverse geolocate**

Next, we want to pull Nominatim method of geolocation from geopy and save it to an object.
```
locator = gp.geocoders.Nominatim(user_agent="myGeocoder")
```
Then we can prepare the coordinates that are inputted for use in the Nominatim geolocator by storing them as a string in the same variable:
```
coordinates  = str(latitude) + ", " + str(longitude)  
```
Finally, we can use Nominatim's reverse locator attribute to collect the data for these coordinates and extract the country name:
```
geocode_data = locator.reverse(coordinates)             
country      = geocode_data.raw['address']['country']
```
Now you can delete the other statement defining the 'country' variable. This code will grab the country name for you!

The added code could look like this:
```
	import geopy as gp


	# Reverse geocode (longitude, latitude > country)
	locator      = gp.geocoders.Nominatim(user_agent="myGeocoder")       
	coordinates  = str(latitude) + ", " + str(longitude)    
	geocode_data = locator.reverse(coordinates)             
	country      = geocode_data.raw['address']['country']   
```

And your ```dataprocessing.py``` script in total could look like this:
```
# ------------------------------------------------------------------------ #
# Initialization
# ------------------------------------------------------------------------ #

# Load dependencies
# ---------------------------------------------#
import pandas as pd
import geopy as gp
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
	locator      = gp.geocoders.Nominatim(user_agent="myGeocoder")       
	coordinates  = str(latitude) + ", " + str(longitude)    
	geocode_data = locator.reverse(coordinates)             
	country      = geocode_data.raw['address']['country']   

	# Extract data for country

	# Extract data for walking & calculate change in # of walking calls
	walking_chg = 20

	# Extract data for driving & calculate change in # of driving calls
	driving_chg = 30

	# Return the results
	return([country, walking_chg, driving_chg])
```

Give it a try by running your ```application.py``` script again in the terminal! What happens if you change the function input coordinates in ```application.py``` to longitude = 10.45, latitude = 51.16? Why?
> Trouble understanding what's going on?

* **Leverage your 'what to do when stuck skills?' to work out how the geopy package works**  
Try searching for e.g., the following keywords: "Python geopy package tutorial reverse geocoding". Your hits should include e.g., [this tutorial](https://towardsdatascience.com/reverse-geocoding-in-python-a915acf29eb6").

* **Apply the class, object, attribute framework to any sample code**  
Is it clear to you what each of the lines of code means?
