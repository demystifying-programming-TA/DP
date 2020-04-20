# Setting Up A Local Webserver (Python)
*Session 2 Setup Guide*

You will be using Python to run a local web server - a critical tool in the local web development work flow. The below instructions will walk you through the process for setting up Python 3. 

**Mac**

*This guide assumes that you have already installed/set-up the [Terminal](/session1/setup_terminal.md)*

Mac OS X comes with Python 2.7 out of the box. Try typing ```python --version``` into the Terminal. You should see something like ```Python 2.7.16``` (the last two digits may vary depending on the date of your most recent software update). 

As of 2020, Python 2.7 has officially been deprecated which is why you should install Python 3 - while the syntax of Python 2/3 is the same for the most part, there are differences! 

To install Python 3 using Homebrew - the package manager which you installed in the [Terminal Set Up Guide](/session1/setup_terminal.md) enter ```brew install python``` into the Terminal. 

Once the installation completes, type ```python3 --version``` into the Terminal. Hopefully, you will see ```Python 3.7.7``` (*Python 3.7.7 is the most recent version at the time of writing*). 

Keeping Python up-to-date is good practice, you can upgrade Python using the Terminal command ```brew upgrade python3```. 

<hr>

**Windows**

*This guide assumes that you have already installed/set-up the [Windows PowerShell](/session1/setup_windows_powershell.md)*

As of 2020, Python 2.7 has officially been deprecated which is why you should install Python 3 - while the syntax of Python 2/3 is the same for the most part, there are differences! 

To install Python 3, download the installer for Windows for version 3.8.2 from https://www.python.org/downloads/

Run the installer and make sure that you add Python to your "PATH" by clicking this box *(note: your installer should say Python 3.8.2)*:

![python_PATH](../assets/session2/python_PATH.png)

This will allow you to run python from powershell by simply typing ```python``` instead of needing to include the 'path' to the python.exe file. (eg. ```C:\User\Zach\1337_h4ck1ng_files\python.exe```)

After installing, test your installation by running the following code in Windows Powershell: ```python --version```

Now let's try installing a module (python package) that will enhance the capability of python and give it functionalities like R. Go into Windows PowerShell and type the following: ```pip install anaconda```

This should be quick and you will get a message when it's complete. Finally, run one more command to make sure all of your modules are updated:

```pip freeze | %{$_.split('==')[0]} | %{pip install --upgrade $_}```

That might take a little bit longer to run, but after that you're ready to rock!

Other fun commands:

```pip list --outdated``` (check which modules are out of date)

```pip install --upgrade package_name``` (check and upgrade a package named: 'package_name')
