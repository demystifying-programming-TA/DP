# Python - Part II 

*Session 3 Mini-Tutorial*

After completing Part I of the Python tutorial, you should have two python files: "Application.py" and "DataProcessing.py". 

We will now initiate multiple country data requests from the Application.py script using a for loop.

Your code for the "Application.py" script should look like the following:
```
# Path
# ---------------------------------------------#
import os, sys
app_root = os.path.normpath(os.path.dirname(os.path.abspath(__file__)))   

# Load internal dependencies
# ---------------------------------------------#
sys.path.append(os.path.normpath(os.path.join(app_root,'Backend')))
from DataProcessing import *

# ------------------------------------------------------------------------ #
# Test Functions
# ------------------------------------------------------------------------ #

# update_owncountry
# ---------------------------------------------#
data = location_mobility_data(longitude = -71.08328259999999, latitude = 42.3662154)
print("Country name: ", data[0])
print("% decrease in walking: ",data[1])
print("% decrease in driving ",data[2])
```

Let's go to the #update_owncountry section. This is where data is being called using the location_mobility_data function and where we would like the loop to occur. 

Start a 'for' loop around the function using the 'for' notation. Since the 'location_mobility_data' function input takes two coordinate values, we will need each list element to cotain two numbers. For example:

```for i in [[a,b], [c,d]]:```

If we have two sets of coordinates, the function will run two times and so on. Pick 3 different sets of coordinates that correspond to three countries. Use google maps to identify these.

All the code within the loop should be indented with either a tab or 3 spaces. To exit the loop, simply go back to no identations. During the loop, the first set of values stored in 'i' will be [a,b]. Pull this data from the i variable and label this data so we can place it into our our function:
```
long = i[0]
lat = i[1]
```
Now we can plug it into our function the same way we did before except we replace the numbers with these variables:
```data = location_mobility_data(longitude = long, latitude = lat)```

Now put your print statements back into the loop and make sure the are properly indented in order to be executed with each run of the loop.

Save and execute your code from the terminal!

Extra:
See what happens if you enter coordinates that don't correspond to a country eg. the ocean. Can you think of a way to fix this? One approach is the "try:-except:" block. It operates like an if statement, but instead if the code under the "try:" block reaches an error, the interpreter moves to the "except:" block and executes there. This is a useful way to give error statements and prevent the script from stopping entirely.
