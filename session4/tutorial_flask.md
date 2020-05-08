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
```
# application.py

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

```
<!-- Index.html -->

<!-- Dependencies -->

<!-- Internal -->
  <link rel=stylesheet type=text/css href="{{ url_for('static', filename='style.css') }}"">
  <script src="{{ url_for('static', filename='function.js') }}"></script>
```

**Step 3: Test application**

1. ```python3 appliation.py``` (```python application.py``` on windows)
2. Open http://127.0.0.1:5000/home in your browser (*http://localhost:5000/ for windows*)

**Step 4: Requests/Response**


```
# application.py

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


```
// function.js
  
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






