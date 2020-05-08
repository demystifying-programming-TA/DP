# Flask 

*Session 4 Mini-Tutorial*

**This guide assumes that you have completed all tutorials in session 1-4 aswell as the [Flask Setup Guide](/session4/setup_flask.md)**


**Step 1: Initialize and launch your Flask App**

Let's begin by initializing your Flask app at the top of your ```application.py``` script. 

We will begin by importing the Flask package  in your 'Initialization Section', i.e., at the top of your script, using the command ```import flask```. 

Once you have imported flask we will initialize your flask application using the following command: 
```
application = flask.Flask(__name__,template_folder = 'frontend', static_folder = 'frontend')
```
The command creates a flask app which we can refer to using the ```application``` object^  and provides flask with the path to our frontend folder (```frontend```) where we have stored our *templates* (i.e., html files) and *static files* (i.e., CSS and JS files). 

^ *Applying our object-orientated programming framework: ```application``` is an object of class ```Flask```, a class that is defined within the ```flask``` library*

#### *This is what the beginning of your ```application.py``` may look like now:*
```
# Load external dependencies
# ---------------------------------------------#
import flask

# Initialize the flask application
# ---------------------------------------------#
application = flask.Flask(__name__, 
	template_folder = 'frontend', 
	static_folder = 'frontend')
```

Once we have initialized our app at the top of our ```application.py``` script we need to ensure that the app is launched, i.e., run. We can achieve this by adding the following command at the end of your ```application.py``` script: ```application.run()```^

^ *Applying our object-orientated programming framework: The function ```run``` is an attribute of the ```application``` object, i.e., a function that is defined within the class ```Flask```*


<hr>

**Step 2: Define your homepage view**

To make our app functional, we need to link our frontend (i.e., our ```index.html``` page) to our backend (i.e., our ```application.py``` script). Using flask, we can accomplish this by defining a view, i.e., a view essentially being a set of commands that tell our Flask application which HTML page to display when a user requests a given URL. 

In our case, let's begin by creating a 'home view', i.e., a view that ensures that our Flask application displays our ```index.html``` page when a user navigates to ```https://[domain name]/home``` where ```[domain name]``` will be ```127.0.0.1:5000``` (mac) or ```localhost:5000``` (windows) for the time-being given that we are hosting the page locally. 

The syntax for defining a view is best understood by taking a look at an example. The below code snippet (to be inserted into you ```application.py``` script after the for-loop created in Session 3) illustrates how you can construct a `home view` for your application. 

```
# ------------------------------------------------------------------------ #
# Define views
# ------------------------------------------------------------------------ #

# home
# ---------------------------------------------#
@application.route('/home')
def home_view():

	# Render the home page
	return flask.render_template('index.html')
	
```

One last thing we need to do before we can test our application is to update the paths in our ```index.html``` file that link to our ```style.css``` and ```function.js``` modules. Using the ```static_folder``` path that we defined in Step 1 while initializing our Flask application we can replace the links to our style-sheet and JS file (within our ```index.html``` script) with the following lines: 

```
<link rel=stylesheet type=text/css href="{{ url_for('static', filename='style.css') }}"">
<script src="{{ url_for('static', filename='function.js') }}"></script>
```

<hr>

**Step 3: Test your application**

Launching your Flask app is simple: 

1. Enter the following command into your Terminal to execute your ```application.py``` script: ```python3 application.py``` (```python application.py``` on windows)


2. Open http://127.0.0.1:5000/home in your browser (http://localhost:5000/ for windows)


<hr>


**Step 4: Requests/Response**


***Step 4 (a): Make request (Frontend - ```function.js```)***

In session 3 we hard-coded the data (country, decrease in the # of walking requests for that country, and decrease in the number of driving requests for that country) that we passed to our ```DrawGraph``` function - at the end of the session your ```function.js``` script should have contained a section like the one below at the end of your ```InitializeGraph``` function:

```
// Draw the graph
// ** Note: Data is hard-coded > next step: Replace hard-coded data with an API call to the server, i.e., backend 
// ** API call specification: Send to server: Longitude, latitude / Receive from server: Corresponding country, decrease in walking direction requests, decrease in driving direction requests
DrawGraph("United States of America",20,30);
```

In this tutorial, we will replace these hard-coded placeholder values with actual values from our dataset. To do that, we will need to make a call to our backend. 

[@Aparna: Explanation to be added]

#### *This is what the middle of your ```application.py``` script (i.e., the section after your ```home _view``` definition) may look like now:*
``` 
// Make API call to backend & draw graph
$.getJSON("/update_country", {longitude: user_longitude, latitude:user_latitude}, 
  function (data, status) {

    // Inspect the data returned from the API
    console.log(data)

    // Draw graph
    DrawGraph(data.Country,data.WalkingDecrease, data.DrivingDecrease);
  }
)

```


***Step 4 (b): Respond to request (Backend - ```application.py```)***

To complete our frontend-backend integration we will need to ensure that our backend is set-up to respond to the request we are placing from the frontend. 

[@Aparna: Explanation to be added]


#### *This is what the middle of your ```application.py``` script (i.e., the section after your ```home _view``` definition) may look like now:*

```
# update_country
# ---------------------------------------------#
@application.route('/update_country')
def update_country_view():

	# Extract the data received from frontend
	long = flask.request.args.get('longitude')
	lat  = flask.request.args.get('latitude')

	# Retrieve the location-specific data
	location_data = dp.location_mobility_data(longitude = long, latitude = lat)

	# Pass the data to the home page & updated page
	return flask.jsonify({"Country":location_data[0], "WalkingDecrease":location_data[1], 
		"DrivingDecrease":location_data[2]})

```





