# Setting Up Postman, and using it to hit your own local API
*Session 1 Setup Guide*

Here's what we're going to be doing in this mini tutorial:

First, you're going to download the Postman client. Postman is an easy to use UI that allows you to send out your own API requests. In real software, API requests are made through code - obiously! In this example, we're going to use Postman so that we don't have to write all of that. That being said, Postman is used widely in industry  by developers in order to test their own APIs. So it's useful!

Second, you're going to start up your very own local webserver! What does this mean? Well, just like when you go to www.facebook.com and you call Facebook's web server, we're going to go through a simple example that allows you to create your own webserver on your own machine.

Third, we're going to use Postman to call APIs that hit your own web server, such that they retrieve and update data.


**1. Download Postman**

API Client ([Postman](https://www.postman.com/)). Please be sure to download the proper one based on your operating system. If you're on Windows and don't know whether you are 32 bit or 64 bit, check here:

Is my OS 32 bit or 64 bit? (Windows only): https://support.microsoft.com/en-us/help/15056/windows-32-64-bit-faq

**2. Start up your own local webserver**

In order to do this, you are first going to need to download npm. This stands for node package manager. This is a package for the JavaScript programming language Node.js. It also contains a command line client called npm that allows you to install and share Javascript software.

*Step 1: Install Homebrew, if you haven't already. If you have not installed Homebrew already, please go [here](/session1/setup_terminal.md)*

*Step 2: Install Node, if you haven't already. Use this command:*

`brew install node`

*Step 3: Start your local webserver! In order to do this, let's first create a folder in your filesystem where you will keep your data. To keep it simple, we will put it on your desktop, and call the folder name 'test_api'.*

Enter the folder by navigating through the terminal:

`cd /Desktop/test_api'

Once inside the folder, you will need to then install the json-server package. Please do so here:

`npm install -g json-server`

If you are running into issues or errors, try this:

`sudo npm install -g json-server`. This will prompt you for your system password, which you then have to type in.

*Step 4: The ‘json-server’ documentation says to create a ‘db.json’ file to store the data, so that is the next step.*

`touch db.json`

*Step 5: You then start the server with the following command*

`json-server --watch db.json`

At this point the server should be running and by default it runs on port 3000. So if you browse to http://localhost:3000, you should see a congratulations message from json-server.

**3. Use Postman to retrieve and modify data.**

*Step 6: Note that no resources were found because our ‘db.json’ file is empty. We should change that.*

I’ll create a JSON object with a key of ‘contacts’ and a value of an array of contact information. So, the db.json file now looks like this.


`//db.json
{
  "contacts": [
    {
      "id": 1,
      "firstName": "Jason",
      "lastName": "Arnold",
      "location": "NYC",
      "email": "jason@test.com"
    }
  ]
}`

Once this is done and you refresh the page, you should now see resources listed, and if you click on the resource link you should see the JSON object displayed in your browser.


** Step 7: Testing with Postman **

First I want to make sure that Postman can also see our data, so with the server still running, I send a GET request to http://localhost:3000/contacts and see the data returned.

![postlogo](./assets/Postman1.png)


Assuming we're good here, you just completed your first GET request! Well done. 

Now, let's try a POST request. With a POST, request we need to provide all of the data we want included in our resource. In this case, that would be the id, first and last names, location, and email. In Postman, change the method next to the URL to ‘POST’, and under the ‘Body’ tab choose the ‘raw’ radio button and then ‘JSON (application/json)’ from the drop down. You can now type in the JSON you want to send along with the POST request. (Please follow along with the screen of your team leader). Let's use this as the body of your second request:

![Postman2](assets/Postman2.png)

`{
  "id": 2,
  "firstName": "{Please fill in your first name here}",
  "lastName": "{Please fill in your last name here}",
  "location": "{Please fill in the city you are currently in here}",
  "email": "{Please fill in your email address here}"
}`

![Postman3](assets/Postman3.png)


Once you submit the request, if it is successful, you should actually see your new data in your db.json file locally. So please refresh that file and take a look!

Lastly, just to close it out, let's run another GET request in your Postman, and you should see all the new data.


Send a GET request to http://localhost:3000/contacts

![Postman4](assets/Postman4.png)

![logo](assets/DPIcon.png)



Congratulations! You have successfully just built your first API, called that API with a GET request, and created a resource using a POST request. Every single app you use today, at the most base level, uses this form to send and retrieve data.





