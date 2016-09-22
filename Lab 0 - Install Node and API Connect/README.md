# Lab 0 - Setup IBM API Connect 
In this lab, you’ll start from scratch to install Node.js and the components of the API Connect Developer toolkit.  Once you have the toolkit installed, you’ll get a chance to use the APIC command line interface for creating LoopBack applications, the intuitive Web-based user interface, and explore the various aspects associated with solution’s configuration of RESTful based services as well as their operation.

---
# Lab 0 - Objective 
In the following lab, you will learn:

+ How to install Node.js on to your machine
+ How to enable API Connect on your Bluemix account
+ How to install the APIC Developer Toolkit

---
# Lab 0 - Case Study used in this tutorial
In this tutorial, you will be starting from scratch to set up your development environment on your local machine.

---
# Lab 0	- Before you begin
For this lab, you will be starting with your local image and installing node.js and the developer toolkit.  After that, if you do not already have a Bluemix account, you will be creating one for you and enabling the API Connect Essentials service on your account. The instructions you will follow will vary by the host operating system you are using. The three host OS's supported by this are `Windows`, `Linux - Intel` and `Linux - Mac`.  Skip to the section for your appropriate operating system.

---
# Lab 0	- Step by Step Lab Instructions

# 0.0a - Install Node.js on Windows

1. If you don't have node already installed on your machine, then please proceed.  Otherwise, move on to section 1.1  

1. Installing Node on Windows based machines (Tested on Windows 7):
	
1. The following are pre-requisites that need to be installed before installing node:

	1. Install Python
		1. version 2.7 is required.  You can download it here:  `https://www.python.org/download/releases/2.7/`
		2. Note the location where it is installed.  You will need to add this location to your path later on.
	2. Install .Net Frameworks SDK 2.0 (`https://www.microsoft.com/en-us/download/confirmation.aspx?id=19988`)
	3. Install Visual Studio Express (`https://www.microsoft.com/en-us/download/confirmation.aspx?id=44914`)
	4. Add Python to the System Path in Windows 7 to the System Path.
		1. Go to `Control Panel` -> `System` -> `Advanced System Settings`

		![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/1.png)

		2. Click `Environment Variables`.

		![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/2.png)

		3. Click `Edit` and append `;C:\python27` (or wherever you installed python) to the Path variable.

		![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/3.png)


1. Install Node.js
	1. Go to this link to install Node `https://nodejs.org/en/download/`

	2. Select the "LTS version - Recommended for most users".  Version at the top should depict v4.4.7 - includes npm 2.15.8.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/4.png)

	3. Select the Windows Installer .msi binary and then follow the prompts to install on your machine

1. Install API Connect on to your machine by starting up a command line window as Administrator and issue this command - `npm install -g apiconnect`.

1. Once complete start up a new terminal window - enter in `apic -v`.  It should show you output that looks similar to below (the version numbers might be different).

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/5.png)

1. You are now ready to move on to section 1.1 below.

# 0.0b - Install Node.js on Linux

1. Install the essentials to run node.js `sudo apt-get install build-essential libssl-dev curl git-core`

2. Install Node Version Manager aka "nvm" by issuing this command here: `curl https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash`

	> ![][info]
	> 
	> When you install `nvm` it will also install `npm` which is the node package manager.
	> npm is used to install node.js based software packages including the API Connect
	> Developer Toolkit

3. close and restart your terminal as indicated in the terminal window or run this command `source ~/.profile`.
4. Run this command to confirm your version `nvm --version`
5. This command will provide documentation on nvm if you wish to learn more about it `nvm help`.  NVM is exceptionally useful as it will allow you to support multiple installations of node.js on your machine, and select the version you want to use.  For our lab today, we only need the one version as indicated in the steps below.
6. To check and see which versions of node are available, issue this command `nvm ls-remote`.  It will provide a very long list.  For API Connect, we will use a specific version of node.  That is version 4.4.7
6. To install node 4.4.7 issue this command `nvm install 4.4.7`

	```bash
	student@ubuntu:~$ nvm install 4.4.7
	Downloading https://nodejs.org/dist/v4.4.7/node-v4.4.7-linux-x64.tar.xz...
	Now using node v4.4.7 (npm v2.15.8)
	```

7. Install API Connect by issuing this command `npm install -g apiconnect` it will take several minutes to complete.
8. Run this command to ensure all is set up properly.  `apic -v` You might be asked to accept the license.  Select the default `yes` and hit enter. You are now ready to move on to section 1.1 below.

# 0.0c - Install Node.js on Mac

1. Check to see if node is already installed.

	```bash
	node -v
	```
2. Check the version, if it is version 4.4.7 then you can move on to section 1.1 - Create your Bluemix account. However if you would prefer to uninstall and reinstall node using Node Version Manager or if node was not found then please continue.
3. Remove any existing versions of node. You will only need to complete these steps if node current exists. To remove node completely from your Mac OSX environment run each of the following commands indvidually via terminal. Open a terminal session and type each of the commands below individually. 
 
	```bash
	sudo rm /usr/local/bin/npm
	sudo rm /usr/local/share/man/man1/node.1
	sudo rm /usr/local/lib/dtrace/node.d
	sudo rm -rf ~/.npm
	sudo rm -rf ~/.node-gyp
	sudo rm /opt/local/bin/node
	sudo rm /opt/local/include/node
	sudo rm -rf /opt/local/lib/node_modules
	sudo rm -rf /usr/local/include/node/
	```

4. Install Xcode Command Line Tools. Open a terminal and type

	```
	xcode-select --install
	```

1. This will open a dialog informing you that the comannd linde developer tools are required for install. Press the Install button.

	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-xcode-tools-confirm-install.png)
2. Agree to the license

	![Xcode Tools Confirm License](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-xcode-tools-confirm-license.png)
3. The software install will begin

	![Xcode Tools Installing](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-xcode-tools-progress.png)
4. The install is complete when you see the "The software was installed" message.

	![Xcode Tools Install Complete](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-xcode-tools-install-complete.png)

5. Next install git. You may already have a version, but if you want to have the latest version you will need to download the install from https://git-scm.com/download/mac

6. Once on the install page the download should start immediately. However if it does not start immediately, click the "click here to download manually" link.

	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-git-install-download.png)

7. Once the download has completed, you should have a file named similar to git-2.8.1-intel-universal-mavericks.dmg. Double-click to unpack the disk image.

8. Once the disk image is unpacked and open, double-click the git-2.8.1-intel-universal-mavericks.pkg file. Note that if you downloaded a different version the file name will be refelcted accordingly.

	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-git-install-package.png)

9. You may get a dialog box with a message stating that the file can't be opened because it is from an unidentified developer. Click the OK button. Open your System Preferences and select the Security & Privacy component. In the section called "Allow apps downloaded from:" you will notice a message that states '"git-2.8.1-..ericks.pkg" was blocked from opening because it is not from an identified developer.', press the Open Anyway button. This will open the installer for git.

	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-git-install-unsecure.png)
		
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-git-install-security.png)

	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-git-install-start.png)

10. Follow the wizard to install. The installation is complete when you see a message stating that "The installation was successful."		
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-git-install-complete.png)
11. Install Node Version Manager aka "nvm" by opening a terminal session and typing the following commands:

	```bash
	git clone git://github.com/creationix/nvm.git ~/.nvm
	printf "\n\n# NVM\nif [ -s ~/.nvm/nvm.sh ]; then\n\tNVM_DIR=~/.nvm\n\tsource ~/.nvm/nvm.sh\nfi" >> ~/.bashrc
	NVM_DIR=~/.nvm
	source ~/.nvm/nvm.sh
	nvm install 4.4.7
	nvm alias default node
	nvm use node
	```

	> **Note:** You may want to update your .bash file so you do not have to source the shell script everytime. To do that, add the following to your .bash file located in your user home directory:
	> 
	> 	```
	> export NVM_PATH=~/.nvm
	source ~/.nvm/nvm.sh

1. Install API Connect by issuing this command `npm install -g apiconnect` it will take several minutes to complete

8. Run this command to ensure all is set up properly.  `apic -v` You might be asked to accept the license.  Select the default `yes` and hit enter.

# 0.1 - Create your Bluemix account

1. Open a browser and visit http://www.bluemix.net

2. Press the SIGN UP button
 	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup.png)

3. Complete the form and press the CREATE ACCOUNT button
	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup-account-details.png)

4. Check your email for your next steps.
	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup-confirmation-email.png)

5. Open the email and click the Confirm your account link
	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup-confirmation-email-detail.png)

6. Once confirmed, you will be taken to a page that says Success! To login, click the Log In link
	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup-success.png)

7. Enter your email address and press the CONTINUE button

8. Then enter your password on the next page and press the LOG IN button

9. You will be prompted to create an organization. Enter an organization name (notice that there are suggestions for you). Also select an appropriate region. Then press the CREATE button.
	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup-create-org.png)

10. Next you will be prompted to create a space such as dev, test, prod, etc. You can name it whatever you would like (again notice the recommendations). Then press the CREATE button.
	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup-create-space.png)

11. Next you will see the Summary page where you can review your entries. Press the I'm Ready button
	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup-summary.png)

12. You're account has been created and configured once you see the following screen.
 	
	![Xcode Tools Install](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/mac-bluemix-setup-complete.png)

# 0.1a - Enable the API Connect Service on your Bluemix Account

12. The next step is to enable the API Connect service on your Bluemix account.  To start the process, click on the `CATALOG` tab in the upper right hand side of the screen

	![](http://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/27.png)

13. Type `Api connect` in the search box next to the magnifying glass icon

14. Click on the `API Connect` Icon to install a new instance of API Connect into your Bluemix space.

	![](http://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/28.png)

15. Click on the `APIs` tile.

	![](http://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/29.png)

16. Click on the `API Connect` tab.

	![](http://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/30.png)

17. Click on the `Create` button.

	![](http://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/31.png)

18. In the `Add Service` frame on the right side of the page, fill in the information based on your needs.
	- SPACE – The name of your Bluemix Space to deploy the API Connect Service
	- APP – Keep the default “Leave unbound”
	- Service Name – The name you want to give to your API Connect implementation if required
	- Selected Plan – Keep the default


17. Click on the `Create` button as shown below.

	![](http://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/32.png)

18. The API Connect service is now deployed.  To confirm the instance is properly created, click on `Launch API Manager`

	![](http://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/33.png)

18. If you are able to see your `Sandbox` catalog as shown below, this means the process of creating and setting up your Bluemix account to use API Connect is now complete.  Close your browser window and proceed to section 1.2 below

	![](http://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/34.png)


# Lab 0 - Conclusion

**Congratulations!** You have installed node.js, the API Connect developer toolkit!

In this lab you learned:

+ How to install node.js and its prerequisites and the API Connect Developer Toolkit on your native OS.
+ Set up you Bluemix Account.

**Options:** Either

- Proceed to [Lab 1 - Quick Start](../Lab%201%20-%20Quick%20Start) **or**
- Proceed to [Lab 2 - Create a LoopBack Application](../Lab%202%20-%20Create%20a%20LoopBack%20Application)

[important]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/important.png "Important!"
[info]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/info.png "Information"
[troubleshooting]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/troubleshooting.png "Troubleshooting"
