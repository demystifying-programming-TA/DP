# Dynamic Frontend Development - Part I 
#### JavaScript + Web Developer Tools

*Session 2 Mini-Tutorial*


**This guide assumes that you have already installed/set-up the [Terminal](/session1/setup_terminal.md) or [Windows PowerShell](/session1/setup_windows_powershell.md) and [Sublime Text](/session1/setup_sublime.md). It also assumes you've completed the [HTML](/session2/tutorial_html_webserver.md) and [CSS](/session2/tutorial_css.md) portion skeleton from the previous exercise**

*To help you build your confidence, we suggest you tackle each of the below steps on your own before you look at the sample code.*

**Step 0: Open your ```index.html``` file**

Open your  ```index.html``` folder by going into Sublime --> File --> Open. Go to your Frontend Folder and open your ```index.html``` file. 

**[Optional] Explore the Web Developer Tools**

To practice your Web Developer skills, try:
* Looking at the source code for your website
* Using the element inspector to edit elements of your website on the fly
* Entering (i) some JavaScript commands into the console (interactive JavaScript coding) and (ii) inserting a ```<script type="text/javascript">console.log("Hello World")</script>``` into the body of your ```index.html``` file (loggging)

**Step 0: Link your JS page to your HTML page**

Connect your JS file with your ```index.html ``` page by using the following  tag  ```<script type="text/javascript" src="function.js"></script>  ``` in between your <head> </head> tags. If your html page is not in the same directory or subdirectory as your function.js file state the name of the directory within the href tag. (i.e.  ```src="Desktop/function.js" ``` ) 


**Step 1: Load (and initialize) the JavaScript libraries you will use (jQuery and Google Charts)**

Load jquery and Google Charts by adding the following in between your <head> </head> tags in your ```index.html``` file:

```
<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
<script type="text/javascript"> google.charts.load('current', {packages: ['corechart', 'bar']});</script>
<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

```

**Step 2: Create an ```InitializeGraph``` function that obtains the user's location**

```
// InitializeGraph
function InitializeGraph() {

  // Make a client-side API call to obtain the user's location
  $.getJSON("http://ip-api.com/json", function (data, status) {

  // Inspect the data returned from the API
  console.log(data)

  // Extract the user's longitude and latitude from the data that the API returns
  user_longitude = data.lon;
  user_latitude  = data.lat;

  // Log the longitude and latitude to the console
  console.log("Longitude: " + user_longitude)
  console.log("Latitude: " + user_latitude)
     
  // Update the interface the user sees with their location
  document.getElementById("location").innerHTML = "Your location:<br> Latitude: " + user_latitude + "<br>Longitude: " + user_longitude;

}
```


**Step 3: Link your html button to the ```InitializeGraph``` function **

Ensure that your ```InitializeGraph``` function is triggered when the button is pressed by inserting the an ```onclick``` property into your ```button``` tag. Your ```button``` tag should now look something like this : ```<button onclick="InitializeGraph()">See the number of infections and deaths in my area</button>```.

**Step 4: Create an ```DrawGraph``` function that visualizes a given set of location-specific data**

```
// DrawGraph
function DrawGraph(country, infection, death) {

  // Generate and format the data
  var data = google.visualization.arrayToDataTable([
    ['Country', 'Infections', 'Deaths'],
    [country, infection, death]
  ]);

  // Customize the graph
  var options = {
    colors: ['#b0120a', '#ffab91'],
    chartArea: {width: '50%'},
    hAxis: {
      title: 'Number of infections and deaths'
    }
  };

  // Generate the graph
  var chart = new google.visualization.BarChart(document.getElementById('chart'));

  // Display the graph
  chart.draw(data, options);

}
```

**Step 5: Link your two functions, substituting hard-coded data for an API call to the backend**

Add in a call to your ```DrawGraph``` function at the end of your ```InitializeGraph``` function passing to the ```DrawGraph``` function a hard-coded set of values for the ```country```, ```infection```, and ```death``` parameters. We will build the backend that can generate these values based on the users' longitude and latitude in session #3. 

```
// Draw the graph
// ** Note: Data is hard-coded > next step: Replace hard-coded data with an API call to the server, i.e., backend 
// ** API call specification: Send to server: Longitude, latitude / Receive from server: Corresponding country, # of infections/deaths in that country
DrawGraph("United States",852000, 43000);
```

**Step 6: Save and exit the file and launch index.html again**

Ensure your server is up and running and refresh or relaunch index.html. You should now see content within the webpage.

**Step 7: Commit your updated repository to Github**

Follow the steps outlined in the [Github Command Line](/session1/tutorial_githubcommandline.md) tutorial to commit your code to Github. 

<br>