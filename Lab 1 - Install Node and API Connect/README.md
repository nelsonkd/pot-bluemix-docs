# Lab 1 - Introduction to IBM API Connect 
In this lab, you’ll start from scratch to install Node.js and the components of the API Connect Developer toolkit.  Once you have the toolkit installed, you’ll get a chance to use the APIC command line interface for creating LoopBack applications, the intuitive Web-based user interface, and explore the various aspects associated with solution’s configuration of RESTful based services as well as their operation.

---
# Lab 1 - Objective 
In the following lab, you will learn:

+ How to install Node.js on to your machine
+ How to install the APIC Developer Toolkit
+ How to create a simple LoopBack application
+ How to create a Representational State Transfer (REST) API definition 
+ How to test a REST API
+ How to publish an API to the Developer Portal

---
# Lab 1 - Case Study used in this tutorial
In this tutorial, you will be starting from scratch to set up your development environment on your local machine, and then you will test the components of the toolkit by creating the default Hello World LoopBack application. We will look at the created artifacts to get a better understanding of what is created for you. The hello-world application is a simple RESTful service that holds a set of "notes" in memory. In this lab we may be creating a new RESTful service and API, but in future labs you'll be creating APIs with existing services.

---
# Lab 1	- Before you begin
For this lab, you will be starting with your local image and installing node.js and the developer toolkit.  The instructions you will follow will vary by the host operating system you are using. The three host OS's supported by this are `Windows`, `Linux - Intel` and `Linux - Mac`.  Skip to the section for your appropriate operating system.

---
# Lab 1	- Step by Step Lab Instructions

# 1.0a - Install Node.js on Windows

1. Installing Node on Windows based machines (Tested on Windows 7):
	
1. The following are pre-requisites that need to be installed before installing node:

	1. Install Python
		1. version 2.7 is required.  You can download it here:  `https://www.python.org/download/releases/2.7/`
		2. Note the location where it is installed.  You will need to add this location to your path later on.
	2. Install .Net Frameworks SDK 2.0 (`https://www.microsoft.com/en-us/download/confirmation.aspx?id=19988`)
	3. Install Visual Studio Express (`https://www.microsoft.com/en-us/download/confirmation.aspx?id=44914`)
	3. Add Python to the System Path in Windows 7 to the System Path.
		1. Go to `Control Panel` -> `System` -> `Advanced System Settings`
![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/1.png)

		2. Click `Environment Variables`.

![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/2.png)

		3. Click `Edit` Append ;C:\python27 (or wherever you installed python) to the Path variable.

![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/3.png)



1. Install Node.JS.
	1. Go to this link to install Node `https://nodejs.org/en/download/`
	2. Select the "LTS version - Recommended for most users".  Version at the top should depict v4.4.7 - includes npm 2.15.8.

![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/4.png)

	3. Select the Windows Installer .msi binary and then follow the prompts to install on your machine

1. Install API Connect on to your machine by starting up a command line window as Administrator and issue this command - `npm install -g apiconnect`.
2. Once complete start up a new terminal window - enter in `apic -v`.  It should show you output that looks similar to below (the version numbers might be different).

![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/master/img/lab1/5.png)

# 1.0b - Install Node.js on Linux

1. install the essentials to run node.js `sudo apt-get install build-essential libssl-dev curl git-core`
2. install Node Version Manager aka "nvm" by issuing this command here: `curl https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash`
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

7. Install API Connect by issuing this command `npm install -g apiconnect` it will take several minutes to complete
8. Run this command to ensure all is set up properly.  `apic -v` You might be asked to accept the license.  Select the default `yes` and hit enter.

# 1.0c - Install Node.js on Mac- Linux

# 1.1 - Create your Bluemix account

# 1.2	- Creating a `hello-world` Application

1.	We will use the API Connect Developer Toolkit command line interface to create the initial application and explore the created artifacts.

1.	From the terminal command line type:

	```bash
	apic loopback hello-world
	```
	
	This command starts the application generator, Yeoman, to help scaffold the new project. Just press enter for each of the three questions.
	
	```
	     _-----_
	    |       |    .--------------------------.
	    |--(o)--|    |  Let's create a LoopBack |
	   `---------´   |       application!       |
	    ( _´U`_ )    '--------------------------'
	    /___A___\
	     |  ~  |
	   __'.___.'__
	 ´   `  |° ´ Y `
	
	? What's the name of your application? hello-world
	? Enter name of the directory to contain the project: hello-world
	   create hello-world/
	     info change the working directory to hello-world
	
	? What kind of application do you have in mind? hello-world (A project containing a basic working e
	xample, including a memory database)
	```
	
	This creates an application named "hello-world" in a directory of the same name. The application is a basic Hello World application. You will see a lot of messages printed to the command line window. It is creating a few resources for you and installing the various node modules. Once the node modules are loaded you'll notice that the process creates swagger and product definitions for you. Finally, the process displays some hints about what to do next. Since we've been given such lovely suggestions about what to do next, we may as well follow the first one at least.

1. Change directories to the project directory:
	
	```bash
	cd hello-world
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
|definitions/hello-world-product.yaml|YAML file for the the hello-world product. Which includes default plans for testing locally.|
|definitions/hello-world.yaml|Swagger definition file for the hello-world API. Includes information about the REST paths and operations, schemas for data models, security requirements, etc.|
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

# 1.3	- Launching the `hello-world` Application

1. Now that we've explored what is created by the application generator, let's move on to the API Designer. From the command line:

	```bash
	apic edit
	```
Alternatively, if you'd rather not login to bluemix:

	```bash
	SKIP_LOGIN=true apic edit
	```

	```text
	TODO: add instructions for signing in to bluemix
	```

1. To test our hello-world services, click on the `run` button to open the application launcher.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/run.png)
	
1. Next, click on the `start` button to launch the `hello-world` application.
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/start.png)
	
1. Once start completes, you should see a screen similar to this:
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/app-running.png)
	
1. Notice that once the application is up and running, stop and restart buttons will appear on the right side of the screen:
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/stop-restart.png)
	
	At this point we're ready to Explore and test our services.

	> ![][info]
	> 
	> We used the web-based editor to launch the application. There's also a command provided with the API Connect Developer Toolkit that can be utilized from the terminal to lauch the application: `apic start`

# 1.4	- Testing the `hello-world` Application

1. Click the `Explore` button to switch to the API Explorer view.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/explore.png)
	
	You will see all the exposed service paths displayed.
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/exploreScreen.png)

1. Now we're going to test the services using the GUI presented on the explore screen. You'll notice that on the left several REST services are defined for us. In particular, take a look `POST /notes` and `GET /notes`.

	If you're not familiar with GET and POST, they are HTTP methods (sometimes called verbs). The POST method is used for creation calls to the service. The GET method is used to retrieve information from a service. In this case, we see that both methods are used against the `/notes` path. So, POST will create a `note` and GET will retrieve all the `notes` that have been created.
	
1. Start by creating a couple of notes. Click the `POST /notes` link in the left column. The other columns will scroll so that you're looking at information and controls pertaining to the `POST /notes` service.

1. To test creation of a note, scroll down in the right hand column until the `Call operation` button is visible at the bottom. Just above the `Call operation` button you'll see a `Generate` link. This link will generate dummy data for you to create a test call to this service.

1. Press the `Generate` link to generate some sample data.
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/generate-data.png)
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/generate.png)
	
	Your data will look different, but you're ready to test the service.
	
1. Go ahead and press the `Call operation` button and scroll down to the `Response` section to see the results.
	
	In the results, you should see a `Code: 200 OK` which indicates that a new `note` was created. If you received a different response, see the troubleshooting steps below.
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/POST-results.png)
	
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
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/GET-results.png)
		
	You should see all the notes that you generated in the result set.
		
	> ![][important]
	> 
	> If you see an empty array, `[]`, as your result, then you've not successfully created any notes. This is also true if you stop the application and restart it. With the hello-world example, we're using an in-memory database which means that nothing is persisted to disk. So, it is lost when the server is stopped and restarted. Lab 2 will walk through how to connect to your application to a persistent data source.

1. At this point, we are done testing the app locally. Click on the `Run` button again to return to the application launch screen.

1. Click on the `Stop` button to stop the application.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/stop-app.png)

# 1.5	- Publishing the API to the Developer Portal

1. Click the `Publish` icon.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publishButton.png)

1. Select `Add and Manage Targets` from the menu.

1. Select `Add a different target`.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/add-target.png)

1. Provide connection information to sign into the IBM API Connect management server, then click the `Sign in` button:

	> API Connect host address: `mgr.think.ibm`
	
	> Username: `student@think.ibm`
	
	> Password: `Passw0rd!`  
	
	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publish-target-signin.png)

1. On the "Select an organization and catalog" screen, choose the `Sandbox` catalog and click the `Next` button.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publish-sandbox-catalog.png)

1. On the "Select an App" screen, choose `None` application and click the `Save` button.

	Our offline toolkit environment is now configured to speak to the central management server.

1. Click `Publish` button once more and select our target, indicated by the grey highlighting:

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publish-target.png)

1. Here we have the opportunity to select what gets published. If we were working on multiple API products as part of this project, we could choose specific ones to publish.
	
	Also, the option exists to only Stage the product. A Stage-only action implies that we'll push the configuration to the Management server, but not actually make it available for consumption yet. The reason for doing this may be because your user permissions only allow staging, or that a different group is in charge of publishing Products.
	
	Click the `Publish` button:

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publish-api.png)

1. Click the `Publish` button to make the API available in the Developer Portal.

1. Wait a moment while the Product is published, a Success message will appear letting you know the step is complete:

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publish-success.png)

# 1.6	- Browsing the API in the Developer Portal

1. Open a new tab in the Firefox web browser by clicking on the new tab `+` button.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/new-tab.png)

1. A bookmark is already saved for the `Portal`, click on the bookmark to open the portal home page.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/portal-bookmark.png)

1. Click on the `API Products` link to see the available products published to the portal.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/api-products-link.png)

1. You should see the published `hello-world` API in the list of products.

  ![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/publishedAPI.png)

	It should be noted that the hello-world application has more to it than we've shown in this lab. You're encouraged to dig in and discover the custom method that's implemented. In future labs, we'll be doing more work in the Developer Portal. For instance we'll be customizing the portal theme, registering an application, subscribing to APIs and testing them from a separate consumer application.

1. Close the `Firefox` web browser. If a warning is presented about closing multiple tabs, deselect the option to notify you in the future and click the `Close Tabs` button.

	![](https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/lab1/close-firefox.png)

1. In the terminal, use the `control+c` keyboard command to quit the API Designer program.

# Lab 1 - Conclusion

**Congratulations!** You have developed and published your first API!

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