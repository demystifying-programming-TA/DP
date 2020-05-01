# Static Frontend Development - Part I 

*Session 2 Mini-Tutorial*

#### HTML + Web Server

In this exercise, we will set up a simple HTML page and then run it on a local web server.

**Step 0: Ensure that index.html is set up in your frontend folder**

If you don't have an index.html file in your frontend folder, create one by following the steps below:

![create html file](../assets/session2/index.png)

**Step 1: Running an http server locally**

Getting an HTTP server up and running locally is quite straightforward. We will use python to do so.

![start running server](../assets/session2/httpserver.png)

Tip: Use Ctrl + C to kill server process and get back to the command line prompt again.

**Step 2: Setting up your webpage**

Now, we move on to the HTML portion of things and set up our webpage. Open index.html in sublime. Try using right click to force index.html to open via sublime as opposed to your browser.

The following snippet of code can help you get started with your webpage. Read through the comments to make changes that you would like to see!

````
<!doctype html>

<html>

<!-- Header -->
<head>

  <title>
    <!-- Pick a title for your website! -->
  </title>

</head>

<!-- Body -->
<body>

    <!-- Provide an overview of the website -->
    <br> <br> <br>

    <p><h1>Mobility has decreased across the globe as people shelter in place. <br>The change in the number of Apple Maps direction requests (Jan 13th - April 14th) illustrates this.</h1></p>

    <br> <br> <br>
    <hr>
    <br> <br> <br>

    <!-- Let's insert a button to generate graph & placeholder for location & placeholder for graph -->
    <div>
      
      <button>See the % decrease in the number of driving and walking direction requests in my current region</button>

    </div>
 
  
</body>
</html>

````

**Step 3: Save and exit the file and launch index.html again**

Ensure your server is up and running and refresh or relaunch index.html. You should now see content within the webpage.

**Step 4: Commit your updated repository to Github**

Follow the steps outlined in the [Github Command Line](/session1/tutorial_githubcommandline.md) tutorial to commit your code to Github. 

**[Optional] Check out these tags that you can use to get a website up and going!**

To build a drop down menu:

````
<select>
    <option value="Country A">Country A</option>
    <option value="Country B">Country B</option>
    <option value="Country C">Country C</option>
</select>    
````

To add an image:

````
<img src="filepath to image" alt="An image I chose" height="42" width="42">
````

To add a hyperlink:

````
<a href="https://www.google.com">
    This is a link 
</a>
````

<br>
