# Python - Part II

*Session 3 Mini-Tutorial*

After completing the [Python - Part I tutorial](/session3/tutorial_python_partI.md), you should have two python files: ```application.py``` and ```dataprocessing.py```.

Let's now add the ability to pull the correct data from our csv and return it with the function in ```dataprocessing.py```

## Adding data extraction to ```dataprocessing.py```

**Use Boolean operators to extract relevant information from the dataset**

As we discussed in Part I, we need to (i) extract the rows from the dataset that correspond to the country our user is in and (ii) extract the row that refers to the walking requests and row that refers to the driving requests.

*1) Extracting the rows that correspond to a given country*

We've discussed previously that you can subset a Pandas Dataframe by column or row (e.g., ```data["columnname"]``` or ```data.iloc[3]```). If you want to subset a Dataframe based on a boolean expression, i.e., filter based on whether or not a row is equal to certain value you can use the following syntax: ```data.loc[data[columnname]==specifiedvalue]```. Given this how could you generate a new Dataframe that contains only the rows where the ```region``` column is equal to ```country```, i.e., the country identifed by the geopy package?

> Potential solution
```
mobility_location_df = mobility_df.loc[mobility_df["Region"]==country]
```

> Hint

Always start by identifying the boolean expression, i.e., what is the true/false check that you want to run on each row? To get a better intuition it may help to run the following command ```print(mobility_df["Region"]==country)``` - does that help you understand the solution?

*2) Extracting the rows that correspond to driving/walking requests*

Applying a similar logic as you did above, how could you create two new Dataframes - one containing the walking requests for the chosen country, the other one containing the driving requests for the chosen country?

> Potential solution

```
walking     =  mobility_location_df.loc[mobility_location_df["Transportation"] == "walking"]
driving     =  mobility_location_df.loc[mobility_location_df["Transportation"] == "driving"]
```

*3) Calculating the % change in requests between January 13th and April 14th*

Finally, using the ```walking``` and ```driving``` Dataframes which you generated in the previous step - how can you derive two variables (```walking_chg``` and ```driving_ch```) that represent the % change in the number of direction calls for each transport medium?

#### Example result for the ```dataprocessing.py``` script:

```
def location_mobility_data(longitude, latitude):

	# Load the data
	mobility_df = pd.read_csv("backend/data/CoronaData.csv", encoding="utf-8")

	# Geocode the longitude/latitude data if not provided with country

	## Initialize the geocoder
	locator      = gp.geocoders.Nominatim(user_agent="myGeocoder")

	## Reverse geocode (longitude, latitude > country)
	coordinates  = str(latitude) + ", " + str(longitude)
	geocode_data = locator.reverse(coordinates)
	country      = geocode_data.raw['address']['country']

	## Extract data for country
	mobility_location_df = mobility_df[mobility_df["Region"]==country]

	## Extract data for walking & calculate change in # of walking calls
	walking     =  mobility_location_df[mobility_location_df["Transportation"] == "walking"]
	walking_chg = 1 - walking["Requests_4/14/2020"]/walking["Requests_1/13/2020"]
	walking_chg = int(walking_chg*100)

	## Extract data for driving & calculate change in # of driving calls
	driving     =  mobility_location_df[mobility_location_df["Transportation"] == "driving"]
	driving_chg = 1 - driving["Requests_4/14/2020"]/driving["Requests_1/13/2020"]
	driving_chg = int(driving_chg*100)

	# Return the results
	return([country, walking_chg, driving_chg])

```

<hr>

## Adding a 'for' loop to ```application.py```

We will now initiate multiple country data requests from the ```application.py``` script using a 'for' loop.

When starting out, your code for the ```application.py``` script should look like the following:
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
# ------------------------------------------------------------------------

## Try the location_mobility_data() function
## Note: Longitude,latitude refer to the United States
data = dp.location_mobility_data(longitude = -71.08328259999999,
	latitude = 42.3662154)
print("Country name: ", data[0])
print("Decrease in # of walking calls (%): " + str(data[1]))
print("Decrease in # of driving calls (%):" + str(data[2]))

```

*1) Initiating the for loop*

Let's go to the '#Test Functions' section. This is where data is being collected by calling the "location_mobility_data" function and is where we would like the loop to occur.

Start a 'for' loop around the function using the proper 'for' notation. Since the 'location_mobility_data' function input takes two coordinate values, we will need each list element to cotain two numbers. For example:

```
for i in [[a,b], [c,d]]:
```

If we have two sets of coordinates, the function will run two times and so on. Pick 3 different sets of coordinates that correspond to three countries. Use google maps to identify these.

*2) Writing the code to be looped*

All the code within the loop should be indented with either a tab or 3 spaces. To exit the loop, simply go back to no indentations.

During the loop, the first set of values stored in 'i' will be [a,b]. Take this data from the i variable and store it in new separate variables so we can place it into our our function:
```
long = i[0]
lat = i[1]
```
Now we can plug it into our function the same way we did before except we replace the numbers with these variables:

```
data = dp.location_mobility_data(longitude = long, latitude = lat)
```

Now put your print statements into the loop and make sure the are properly indented in order to be executed with each run of the loop.

Save and execute your code from the terminal!

*3) Optional extension*

See what happens if you enter coordinates that don't correspond to a country eg. the ocean. Can you think of a way to fix this? One approach is the "try:-except:" block. It operates like an if statement, but instead if the code under the "try:" block reaches an error, the interpreter moves to the "except:" block and executes there. This is a useful way to give error statements and prevent the script from stopping entirely.

#### Example result for the ```application.py``` script:

```
# ------------------------------------------------------------------------ #
# Initialization
# ------------------------------------------------------------------------ #

# Load internal dependencies
# ---------------------------------------------#
import sys
sys.path.append('backend')
import DataProcessing as dp

# ------------------------------------------------------------------------ #
# Test Functions
# ------------------------------------------------------------------------ #

## Note: Try with US, Germany, UK
for i in [[-71.08328259999999, 42.3662154],[10.48328259999999, 51.3662154],[-1.78328259999999, 52.4662154]]:
	try:
		long = i[0]
		lat  = i[1]
		data = dp.location_mobility_data(longitude = long, latitude = lat)
		print("Country name: ", data[0])
		print("Decrease in # of walking calls (%): " + str(data[1]))
		print("Decrease in # of driving calls (%): " + str(data[2]))

	except:
		print("Country not found.")

# ------------------------------------------------------------------------ #
# ------------------------------------------------------------------------ #
```
