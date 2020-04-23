# Setting Up Your DP Project Structure
*Session 1 Mini-Tutorial*

**This guide assumes that you have are comfortable with the Command Line and the Github Command Line Tool, if you need a refresher - take a look at the [Command Line](/session1/tutorial_commandline.md) and [Github Command Line Tool](/session1/tutorial_githubcommandline.md) tutorials**

*To help you build your confidence, we suggest you tackle each of the below steps on your own before you look at the sample code.*

**Step 0: Create your DP Directory Structure**

In this section we will create your ```DPProject``` folder, and within this folder create dedicated ```frontend``` and ```backend``` folders. *Note that you will need create your ```DPProject``` within the folder within which you initialized Git in the [Github Command Line Tool](/session1/tutorial_githubcommandline.md) tutorial.*

````
mkdir DPProject
cd DPProject
mkdir frontend
mkdir backend
ls
````

**Step 1: Create placeholder files**

In this section we will create:
* A ```README.md``` file (it's good practice to always create a README file which gives a brief description of the project)
* Three placeholder files which will form the basis for the Frontend we will build in session #2 (```index.html``` (HTML), ```style.css``` (CSS), and ```function.js``` (JavaScript))
* A placeholder file which will form the basis for the Backend we will build in session #3 (```dataprocessing.py``` (Python))


````
cd DPProject
touch README.md
cd frontend
touch index.html
touch style.css
touch function.js
cd ..
cd backend
touch dataprocessing.py
ls
````

*Note: If you are using Windows PowerShell you will use the ```ni``` command in place of the ```touch``` command*

**Step 2: Commit your DP Project Folder to Github**

In this section we will commit your DP Project Folder to Github. 

````
cd DPProject
git add .
git commit -m "DP Project Structure"
git push -u origin master
````

To check that everything was properly committed you can visit your Github account via your browser - your repository should look something like [this sample repository](https://github.com/demystifying-programming-TA/DP2020/tree/master/DemoProject/Session1_Intro) 


