# Flask 

*Session 4 Mini-Tutorial*

**Step 1: Initialize your Flask App**

```
# application.py

# Load external dependencies
# ---------------------------------------------#
import flask

# Initialize the flask application
# ---------------------------------------------#
application = flask.Flask(__name__, 
	template_folder = 'frontend', 
	static_folder = 'frontend')
```

```
# application.py

# ------------------------------------------------------------------------ #
# Launch the  application
# ------------------------------------------------------------------------ #
if __name__ == "__main__":
	application.run()
```


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






