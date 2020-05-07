# Setting Up Your Python Command Shell (iPython)

*Session 3 Setup Guide*

Depending on your computer's set-up you may run into an error when using the ```geopy``` package (which you installed in the [Python Package Installation](/session3/setup_pythonpackages.md) tutorial). 

When working through the [Python - Part II tutorial](/session3/tutorial_python_partI.md) you may see a huge error log in the Terminal - in particular, you may see this error: ```[SSL: CERTIFICATE_VERIFY_FAILED]```

If you got this error, please follow the following steps to fix it:

1. Change directory to point directly into your Python application (you will either have 3.7 or 3.8), e.g. ```cd /Applications/Python\ 3.8/```  

2. Run an ```ls``` command. You should see a file with the following name: ```Install Certificates.command```  

3. Run this certificates installation with the Terminal command: 
```./Install\ Certificates.command```