# Setting Up Your DP Project Structure
*Session 1 Mini-Tutorial*

**This guide assumes that you have are comfortable with the Command Line and the Github Command Line Tool, if you need a refresher - take a look at the [Command Line](/session1/tutorial_commandline.md) and [Github Command Line Tool](/session1/tutorial_githubcommandline.md) tutorials**

*To help you build your confidence, we suggest that you try to tackle each of the below steps on your own first before you look at the sample code.*

**Step 0: Creating your DP Directory Structure**

In this section we will create your ```DPProject``` folder, and within this folder create dedicated ```frontend``` and ```backend``` folders. 

````
mkdir DPProject
cd DPProject
mkdir frontend
mkdir backend
ls
````

**Step 1: Create placeholder files**

In this section we will create an empty README file (it's good practice to always create a README file which gives a brief description of the project), three placeholder script files which will form the basis for the frontend we will build in session #2 (```index.html``` (HTML), ```style.css``` (CSS), and ```function.js``` (JavaScript)), and one placeholder script file which will form the basis for the backend we will build in session #3 (```dataprocessing.py``` (Python))


````
cd DPProject
touch README.md
cd frontend
touch index.html
touch style.css
touch function.js 
cd ..
cd backend
touch dataprocessing.js
ls
````

**Step 2: Commit your DP Project Folder to Github**

In this section we will commit your DP Project Folder to Github, i.e., ensure that your project is version controlled. 

````
cd DPProject
git add .
git commit -m "DP Project Structure"
git push -u origin master
````

To check that everything was properly committed you can visit your Github account via your browser - your repository should look something like [this sample repository](https://github.com/demystifying-programming-TA/DP2020/tree/master/DemoProject/Session1_Intro) 


