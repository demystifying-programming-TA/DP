# Setting Up Your Terminal
*Session 1 Setup Guide*

**Step 1: Install x-code, if you already haven't.**

-Command + Spacebar -> type in 'Terminal', and open the app
-Inside the Terminal window, copy and paste (or type) the following lines of code:

`xcode-select --install`

-You should follow the prompted instructions to install the command line developer tools.

**Step 2: Installing Homebrew**

-What is Homebrew? 

It's a package manager for Mac OS and Linux operating systems. Essentially, it helps a user easily download and install hundreds of open source tools for developers on these machine - all with just a few scripts. We are going to use Homebrew to download just a few tools, but if you are curious and would like to read the official Homebrew documentation, just click [here](https://docs.brew.sh/)

To install Homebrew, please copy paste the following (please don't try to type this out) into your terminal, and press 'return':

` /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"`

Follow the instructions on your terminal. At some point, Terminal may ask you for your password. When typing in your password, please note that Terminal does not provide any visual feedback when typing. Just type it slowly, and press 'return'.

Once the installation is successful, run the following command:

`brew doctor`

If you get the following message: "Your system is ready to brew", then move on to the next step. If you run into errors, please let us know.


**Step 3: Install Git and cURL**

Type in the following commands:

```
brew update
brew install git
brew install npm
brew install curl
```

We just installed brew, so we could have skipped 'brew update'. However, it's generally good practice to run it before installing anything, since Homebrew is updated regularly.
