# Lab 1 - Introduction to IBM API Connect 
In this lab, you’ll start from scratch to install Node.js and the components of the API Connect Developer toolkit.  Once you have the toolkit installed, you’ll get a chance to use the APIC command line interface for creating LoopBack applications, the intuitive Web-based user interface, and explore the various aspects associated with solution’s configuration of RESTful based services as well as their operation.

---
# Lab 1 - Objective 
In the following lab, you will learn:

+ How to install Node.js on to your machine
+ How to enable API Connect on your Bluemix account
+ How to install the APIC Developer Toolkit
+ How to create a simple LoopBack application
+ How to create a Representational State Transfer (REST) API definition 
+ How to test a REST API
+ How to publish an API to the Developer Portal

---
# Lab 1 - Case Study used in this tutorial
In this tutorial, you will be starting from scratch to set up your development environment on your local machine, and then you will test the components of the toolkit by creating the default Notes LoopBack application. We will look at the created artifacts to get a better understanding of what is created for you. The notes application is a simple RESTful service that holds a set of "notes" in memory. In this lab we may be creating a new RESTful service and API, but in future labs you'll be creating APIs with existing services.

---
# Lab 1	- Before you begin
For this lab, you will be starting with your local image and installing node.js and the developer toolkit.  After that, if you do not already have a Bluemix account, you will be creating one for you and enabling the API Connect Essentials service on your account. The instructions you will follow will vary by the host operating system you are using. The three host OS's supported by this are `Windows`, `Linux - Intel` and `Linux - Mac`.  Skip to the section for your appropriate operating system.

---
# Lab 1	- Step by Step Lab Instructions

# 1.0a - Install Node.js on Windows

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

# 1.0b - Install Node.js on Linux

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

# 1.0c - Install Node.js on Mac

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

# 1.1 - Create your Bluemix account

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

# 1.1a - Enable the API Connect Service on your Bluemix Account

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

# 1.2	- Creating a `notes` Application

1.	We will use the API Connect Developer Toolkit command line interface to create the initial application and explore the created artifacts.

1.	From the terminal command line type:

	```bash
	apic loopback
	```
	
	This command starts the application generator, Yeoman, to help scaffold the new project. Just press enter for first two questions and then select **notes** for the kind of application.
	
	```
	? What's the name of your application? notes
	? Enter name of the directory to contain the project: notes
	? What kind of application do you have in mind? 
	empty-server (An empty LoopBack API, without any configured models or datasources) 
	hello-world (A project containing a controller, including a single vanilla Message and a single remote method) 
	❯ notes (A project containing a basic working example, including a memory database)
```
	
	This creates an application named "notes" in a directory of the same name. The application is a basic Notes application. You will see a lot of messages printed to the command line window. It is creating a few resources for you and installing the various node modules. Once the node modules are loaded you'll notice that the process creates swagger and product definitions for you. Finally, the process displays some hints about what to do next. Since we've been given such lovely suggestions about what to do next, we may as well follow the first one at least.

1. Change directories to the project directory:
	
	```bash
	cd notes
	```

1. List the directory:

	```bash
	$ ls
	client  common  definitions  node_modules  package.json  server
	```
	
	If you're familiar with LoopBack or Node.js applications, some of the directories may be familiar to you. If not, here is a description of some of what is created.

|Directory or file|Description|
|-----------------|-----------|
|client|If the application has a front end, this is where the HTML, CSS, JavaScript, etc would be located. For our sample application there is only a stubbed out README.md.|
|common|Files common to both the server and the client application.|
|common/models|This sub-directory contains all the model JSON and JavaScript files. By model we're referring to a data model.|
|common/models/note.js|Custom script for the note data model. This file contains the implementation of the methods defined by the model definition file.|
|common/models/note.json|The note model definition file. This file contains the definition of the properties and methods for this model.|
|definitions|This directory contains the definitions for the APIs and the product contained in this application.|
|definitions/notes-product.yaml|YAML file for the the notes product. Which includes default plans for testing locally.|
|definitions/notes.yaml|Swagger definition file for the notes API. Includes information about the REST paths and operations, schemas for data models, security requirements, etc.|
|node_modules|Directory containing all the required node modules for the default application.|
|package.json|Standard Node.js package specification. Most importantly it contains the application package dependencies.|
|server|This directory contains the Node.js application and configuration files. We'll not look at them all in this tutorial, but here are a few.|
|server/server.js|The main appication script for this application. **Note:** this is defined in the package.json file.|
|server/config.json|This file contains the global application settings, such as REST API root, hostname and port.|
|server/model-config.json|This file binds models to data sources and specifies whether a model is exposed over REST, among other things.|
|server/datasources.json|This file is the data source configuration file.|

> ![][info]
>
> `*.md` files, such as that found in the client directory, are markdown files used for internal documentation.

# 1.3	- Launching the `notes` Application

1. Now that we've explored what is created by the application generator, let's move on to the API Designer. From the command line:

	```bash
	apic edit
	```
	
	> **Note:** You may be asked to login to your Bluemix account. You can overt this step prepending the previous command with SKIP_LOGIN=true. Example:

	```
	bash
	SKIP_LOGIN=true apic edit
	```

1. Next, click on the `start` button located on the bottom panel of the API Designer to launch the `notes` application.  On a Windows environment, you might see 2 node windows pop up on your screen.  Minimize, but do not close these windows.
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/6.png)
	
1. Once start completes, you should see a screen similar to this:
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/7.png)
	
1. Notice that once the application is up and running, stop and restart buttons will appear on the bottom side of the screen:
	
	At this point we're ready to Explore and test our services.

	> ![][info]
	> 
	> We used the web-based editor to launch the application. There's also a command provided with the API Connect Developer Toolkit that can be utilized from the terminal to lauch the application: `apic start`

# 1.4	- Testing the `notes` Application

1. Click the `Explore` button to switch to the API Explorer view.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/8.png)
	
	You will see all the exposed service paths displayed.
	
	![](https://github.com/kenatibm/pot-bluemix-docs/blob/master/img/lab1/exploreScreen.png)

1. Now we're going to test the services using the GUI presented on the explore screen. You'll notice that on the left several REST services are defined for us. In particular, take a look `POST /notes` and `GET /notes`.

	If you're not familiar with GET and POST, they are HTTP methods (sometimes called verbs). The POST method is used for creation calls to the service. The GET method is used to retrieve information from a service. In this case, we see that both methods are used against the `/notes` path. So, POST will create a `note` and GET will retrieve all the `notes` that have been created.
	
1. Start by creating a couple of notes. Click the `POST /notes` link in the left column. The other columns will scroll so that you're looking at information and controls pertaining to the `POST /notes` service.

1. To test creation of a note, scroll down in the right hand column until the `Call operation` button is visible at the bottom. Just above the `Call operation` button you'll see a `Generate` link. This link will generate dummy data for you to create a test call to this service.

1. Press the `Generate` link to generate some sample data.
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/generate-data.png)
	
	![](https://github.com/kenatibm/pot-bluemix-docs/blob/master/img/lab1/generate.png)
	
	Your data will look different, but you're ready to test the service.
	
1. Go ahead and press the `Call operation` button and scroll down to the `Response` section to see the results.
	
	In the results, you should see a `Code: 200 OK` which indicates that a new `note` was created. If you received a different response, see the troubleshooting steps below.
	
	![](https://github.com/kenatibm/pot-bluemix-docs/blob/master/img/lab1/POST-results.png)
	
	> ![][troubleshooting]
	>
	> You may see an error displayed that mentions a CORS issue. This has to do with certificates in your browser. Go ahead an click the given link to rectify this, accept any certificate, close the opened tab, and press the `Call operation` button again.  Additionally, be sure not to skip step 5, as doing a `POST` operation without generating payload will cause an error.
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/CORS-support-error.png)
	
	> ![][troubleshooting]
  >
  > If you see a 500 error like the one below, make sure you press the `Generate` button before you press the `Call operation` button again. Otherwise, you're trying to create a duplicate note.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/duplicateRecordError.png)


1. Once you have created one note, go ahead and create another one or two.

	> ![][info]
	> 
	> It should be noted that you don't need to use the `Generate` link. You can type data directly into the `Parameters`. You can also use `Generate` to create a template for you to use and then change the generated parameters. You may also notice that not all the parameters are always generated. This is because only the `title` parameter is required. Try pressing `Generate` several times to get a feel for how it works.
	
1. Finally, let's test the `GET /notes` service. We should have two, three, or more notes created at this point. In the left hand column click the `GET /notes` link.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/get-notes.png)

1. Scroll down to the `Call operation` button and press it. Then scroll down to the results.
	
	![](https://github.com/kenatibm/pot-bluemix-docs/blob/master/img/lab1/GET-results.png)
		
	You should see all the notes that you generated in the result set.
		
	> ![][important]
	> 
	> If you see an empty array, `[]`, as your result, then you've not successfully created any notes. This is also true if you stop the application and restart it. With the notes example, we're using an in-memory database which means that nothing is persisted to disk. So, it is lost when the server is stopped and restarted. Lab 2 will walk through how to connect to your application to a persistent data source.

1. At this point, we are done testing the app locally. Click on the `Run` button again to return to the application launch screen.

1. Click on the `Stop` button to stop the application.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/9.png)

# 1.5	- Publishing the API to the Developer Portal

1. Click the `Publish` icon.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publishButton.png)

1. Select `Add and Manage Targets` from the menu.

1. Select `Add IBM Bluemix target`.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/15.png)

1. Provide connection information to sign into the IBM API Connect Bluemix service then click the `Sign in` button: **Note you should be logged in already to Bluemix, so you should not need to reauthenticate.  It will automatically populate your information and have the `Sandbox` catalog already selected, so at this point you only need to click `Next`.
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/10.png)

1. On the "Select an App" screen, choose `None` application and click the `Save` button.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/11.png)

	Our offline toolkit environment is now configured to speak to API Connect on Bluemix

1. Click `Publish` button once more and select our target:

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/12.png)

1. Here we have the opportunity to select what gets published. If we were working on multiple API products as part of this project, we could choose specific ones to publish.
	
	Also, the option exists to only Stage the product. A Stage-only action implies that we'll push the configuration to the Management server, but not actually make it available for consumption yet. The reason for doing this may be because your user permissions only allow staging, or that a different group is in charge of publishing Products.
	
	Click the `Publish` button:

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publish-api.png)

1. Click the `Publish` button to make the API available in the Developer Portal.

1. Wait a moment while the Product is published, a Success message will appear letting you know the step is complete:

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publish-success.png)

# 1.6	- Browsing the API in the Developer Portal

1. Open a new tab in your web browser by clicking on the new tab `+` button.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/new-tab.png)

1. Log into your Bluemix Account using this url: `https://new-console.ng.bluemix.net/`

1. Via the dashboard, click on the `APIs` Icon.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/16.png)

1. Click on your `API Connect` instance

![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/17.png)

2. Click on `Launch API Manager` to launch your API Manager

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/18.png)

3. Click on your `Sandbox` Catalog

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/19.png)

4. Click on `Settings`

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/20.png)

5. Here you will see that you have no developer portal set up.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/21.png)

5. Select the `IBM Developer Portal` Radio Button to create your own custom portal that is tied to your catalog and then click `Save`. It will automatically generate the portal URL and the portal as well.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/22.png)

6. A pop up screen will let you know that the process to create your portal has started.

7. It might take some time for your developer portal to get created, but usually the process is pretty quick.  If this piece doesn't work for you right away, move on to the next lab and circle back to this lab in a bit.  Once the portal is done creating, you will receive an email.  If it still doesn't work by the time you get to the later labs, inform your instructor.

6. Once the process is complete, click on the link of the portal URL as seen in the screenshot above in step #5.  It is highly suggested that you create a bookmark for your developer portal in your browser so you can get back to it easily later.

7. This will bring you to your portal login page.  In order to view the API we have, we will need to register ourself as a developer on the portal. 

	> ![][important]
	> 
	> When you first create your developer portal it will create an `admin` user that is used to administrate the site.  This admin user cannot be used as a user to register applications and subscribe to API Products. So the next few steps will be devoted to creating a new developer user.

8. Click on `Logout` at the top right to log out of the portal as the admin user. 

8. Click on `Create an account` at the top right

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/35.png)
	
9. Enter in your account information for the developer account.  This must be a different email address than your bluemix account.  Click `Create New Account` once all the requisite data in the form has been filled out.

10. A validation email will be sent out to the email address used at sign up.  Click on the validation link and then you will have completed the sign up process and will be authenticated into the page.

10. Once you are authenticated in, you can then Browse the `API Products` and see your `notes` product that is now published to your environment.
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/26.png)

11. At this point we will stop, as we will be building additional apis and services that will be published to the portal.

	It should be noted that the notes application has more to it than we've shown in this lab. You're encouraged to dig in and discover the custom method that's implemented. In future labs, we'll be doing more work in the Developer Portal. For instance we'll be customizing the portal theme, registering an application, subscribing to APIs and testing them from a separate consumer application.


1. Close the `Firefox` web browser. If a warning is presented about closing multiple tabs, deselect the option to notify you in the future and click the `Close Tabs` button.



1. In the terminal, use the `control+c` keyboard command to quit the API Designer program.

# Lab 1 - Conclusion

**Congratulations!** You have installed node.js, the API Connect developer toolkit and have developed and published your first API!

In this lab you learned:

+ How to install node.js and its prerequisites and the API Connect Developer Toolkit on your native OS.
+ Set up you Bluemix Account.
+ How to create a simple LoopBack application
+ How to create a Representational State Transfer (REST) API definition
+ How to test a REST API
+ How to publish an API to the Developer Portal

Proceed to [Lab 2 - Create a LoopBack Application](../Lab%202%20-%20Create%20a%20LoopBack%20Application)

[important]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/important.png "Important!"
[info]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/info.png "Information"
[troubleshooting]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/troubleshooting.png "Troubleshooting"
