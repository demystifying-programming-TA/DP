# Installing The Most Common Python Packages

*Session 3 Setup Guide*

*This guide assumes that you have already installed/set-up [Python 3](/session2/setup_python.md)*

To install a Python package, you can use the command ```pip3``` *(Mac)* or ```pip``` *(Windows)* - a Python package manager. 

***Install a single package***

Simply enter the following command into your Terminal - ```pip3 install [packagename]``` *(Mac)* or ```pip install [packagename]``` *(Windows)*

Replace ```[packagename]``` with the name of the package you are installing, e.g., ````pip3 install pandas```` *(Mac)* or ```pip install pandas``` *(Windows)* to install the ```pandas``` package. 

To confirm that a package has been installed, launch Python (enter ```python3``` *(Mac)* or ```python``` *(Windows)* into the Terminal), and execute the following Python command ```import [packagename]```, e.g., ```import pandas```. If you don't receive a error message, that means you are all set.  

***Install multiple packages at once***

Sometimes it may be easier to install multiple packages at once, e.g., after setting up Python 3 for the first time you may want to install the most commmon Python packages all in one go. 

To do so, simply follow the below steps: 

1) Create a new text file called 'requirements.txt'

2) List the packages you want to install in this text file following the below format:

```
# Data
pandas
numpy

# Plotting
matplotlib

# Modelling
scikit-learn

# Web Development
flask

# Interactive Coding
jupyter

# Domain-Specific Packages
## Geocoding
geopy
```
*Note: We will be using pandas, numpy, flask and geopy in Session #3 and Session #4*


3) Execute the following command in the Terminal (after navigating to the folder in which you saved your 'requirements.txt' file): ```pip3 install -r requirements.txt``` *(Mac)* or ```pip install -r requirements.txt``` *(Windows)*

***(Optional) Upgrade a package***

If you want to/need to upgrade a specific package you can use the following Terminal command: ```pip3 install [packagename] --upgrade```, e.g., ```pip3 install pandas --upgrade```. The command ```pip3 show [packagename]``` (e.g., ```pip3 show pandas```) in turn will show you which version you have installed. *For Windows just remove the '3' in 'pip3'.*





