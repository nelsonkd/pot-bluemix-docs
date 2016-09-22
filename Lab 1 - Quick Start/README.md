# Lab 1 - Introduction to IBM API Connect
In this lab, you’ll get a chance to use the APIC command line interface for creating LoopBack applications, the intuitive Web-based user interface, and explore the various aspects associated with solution’s configuration of RESTful based services as well as their operation.

---
# Lab 1 - Objective 
In the following lab, you will learn:

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
	
	![](../img/lab1/6.png)
	
1. Once start completes, you should see a screen similar to this:
	
	![](../img/lab1/7.png)
	
1. Notice that once the application is up and running, stop and restart buttons will appear on the bottom side of the screen:
	
	At this point we're ready to Explore and test our services.

	> ![][info]
	> 
	> We used the web-based editor to launch the application. There's also a command provided with the API Connect Developer Toolkit that can be utilized from the terminal to lauch the application: `apic start`

# 1.4	- Testing the `notes` Application

1. Click the `Explore` button to switch to the API Explorer view.

	![](../img/lab1/8.png)
	
	You will see all the exposed service paths displayed.
	
	![](../img/lab1/exploreScreen.png)

1. Now we're going to test the services using the GUI presented on the explore screen. You'll notice that on the left several REST services are defined for us. In particular, take a look `POST /notes` and `GET /notes`.

	If you're not familiar with GET and POST, they are HTTP methods (sometimes called verbs). The POST method is used for creation calls to the service. The GET method is used to retrieve information from a service. In this case, we see that both methods are used against the `/notes` path. So, POST will create a `note` and GET will retrieve all the `notes` that have been created.
	
1. Start by creating a couple of notes. Click the `POST /notes` link in the left column. The other columns will scroll so that you're looking at information and controls pertaining to the `POST /notes` service.

1. To test creation of a note, scroll down in the right hand column until the `Call operation` button is visible at the bottom. Just above the `Call operation` button you'll see a `Generate` link. This link will generate dummy data for you to create a test call to this service.

1. Press the `Generate` link to generate some sample data.
	
	![](../img/lab1/generate-data.png)
	
	![](../img/lab1/generate.png)
	
	Your data will look different, but you're ready to test the service.
	
1. Go ahead and press the `Call operation` button and scroll down to the `Response` section to see the results.
	
	In the results, you should see a `Code: 200 OK` which indicates that a new `note` was created. If you received a different response, see the troubleshooting steps below.
	
	![](../img/lab1/POST-results.png)
	
	> ![][troubleshooting]
	>
	> You may see an error displayed that mentions a CORS issue. This has to do with certificates in your browser. Go ahead an click the given link to rectify this, accept any certificate, close the opened tab, and press the `Call operation` button again.  Additionally, be sure not to skip step 5, as doing a `POST` operation without generating payload will cause an error.
	
	![](../img/lab1/CORS-support-error.png)
	
	> ![][troubleshooting]
  >
  > If you see a 500 error like the one below, make sure you press the `Generate` button before you press the `Call operation` button again. Otherwise, you're trying to create a duplicate note.

	![](../img/lab1/duplicateRecordError.png)


1. Once you have created one note, go ahead and create another one or two.

	> ![][info]
	> 
	> It should be noted that you don't need to use the `Generate` link. You can type data directly into the `Parameters`. You can also use `Generate` to create a template for you to use and then change the generated parameters. You may also notice that not all the parameters are always generated. This is because only the `title` parameter is required. Try pressing `Generate` several times to get a feel for how it works.
	
1. Finally, let's test the `GET /notes` service. We should have two, three, or more notes created at this point. In the left hand column click the `GET /notes` link.

	![](../img/lab1/get-notes.png)

1. Scroll down to the `Call operation` button and press it. Then scroll down to the results.
	
	![](../img/lab1/GET-results.png)
		
	You should see all the notes that you generated in the result set.
		
	> ![][important]
	> 
	> If you see an empty array, `[]`, as your result, then you've not successfully created any notes. This is also true if you stop the application and restart it. With the notes example, we're using an in-memory database which means that nothing is persisted to disk. So, it is lost when the server is stopped and restarted. Lab 2 will walk through how to connect to your application to a persistent data source.

1. At this point, we are done testing the app locally. Click on the `Run` button again to return to the application launch screen.

1. Click on the `Stop` button to stop the application.

	![](../img/lab1/9.png)

# 1.5	- Publishing the API to the Developer Portal

1. Click the `Publish` icon.

	![](../img/lab1/publishButton.png)

1. Select `Add and Manage Targets` from the menu.

1. Select `Add IBM Bluemix target`.

	![](../img/lab1/15.png)

1. Provide connection information to sign into the IBM API Connect Bluemix service then click the `Sign in` button: **Note you should be logged in already to Bluemix, so you should not need to reauthenticate.  It will automatically populate your information and have the `Sandbox` catalog already selected, so at this point you only need to click `Next`.
	
	![](../img/lab1/10.png)

1. On the "Select an App" screen, choose `None` application and click the `Save` button.

	![](../img/lab1/11.png)

	Our offline toolkit environment is now configured to speak to API Connect on Bluemix

1. Click `Publish` button once more and select our target:

	![](../img/lab1/12.png)

1. Here we have the opportunity to select what gets published. If we were working on multiple API products as part of this project, we could choose specific ones to publish.
	
	Also, the option exists to only Stage the product. A Stage-only action implies that we'll push the configuration to the Management server, but not actually make it available for consumption yet. The reason for doing this may be because your user permissions only allow staging, or that a different group is in charge of publishing Products.
	
	Click the `Publish` button:

	![](../img/lab1/publish-api.png)

1. Click the `Publish` button to make the API available in the Developer Portal.

1. Wait a moment while the Product is published, a Success message will appear letting you know the step is complete:

	![](../img/lab1/publish-success.png)

# 1.6	- Browsing the API in the Developer Portal

1. Open a new tab in your web browser by clicking on the new tab `+` button.

	![](../img/lab1/new-tab.png)

1. Log into your Bluemix Account using this url: `https://new-console.ng.bluemix.net/`

1. Via the dashboard, click on the `APIs` Icon.

	![](../img/lab1/16.png)

1. Click on your `API Connect` instance

	![](../img/lab1/17.png)

2. Click on `Launch API Manager` to launch your API Manager

	![](../img/lab1/18.png)

3. Click on your `Sandbox` Catalog

	![](../img/lab1/19.png)

4. Click on `Settings`

	![](../img/lab1/20.png)

5. Here you will see that you have no developer portal set up.

	![](../img/lab1/21.png)

5. Select the `IBM Developer Portal` Radio Button to create your own custom portal that is tied to your catalog and then click `Save`. It will automatically generate the portal URL and the portal as well.

	![](../img/lab1/22.png)

6. A pop up screen will let you know that the process to create your portal has started.

7. It might take some time for your developer portal to get created, but usually the process is pretty quick.  If this piece doesn't work for you right away, move on to the next lab and circle back to this lab in a bit.  Once the portal is done creating, you will receive an email.  If it still doesn't work by the time you get to the later labs, inform your instructor.

6. Once the process is complete, click on the link of the portal URL as seen in the screenshot above in step #5.  It is highly suggested that you create a bookmark for your developer portal in your browser so you can get back to it easily later.

7. This will bring you to your portal login page.  In order to view the API we have, we will need to register ourself as a developer on the portal. 

	> ![][important]
	> 
	> When you first create your developer portal it will create an `admin` user that is used to administrate the site.  This admin user cannot be used as a user to register applications and subscribe to API Products. So the next few steps will be devoted to creating a new developer user.

8. Click on `Logout` at the top right to log out of the portal as the admin user. 

8. Click on `Create an account` at the top right

	![](../img/lab1/35.png)
	
9. Enter in your account information for the developer account.  This must be a different email address than your bluemix account.  Click `Create New Account` once all the requisite data in the form has been filled out.

10. A validation email will be sent out to the email address used at sign up.  Click on the validation link and then you will have completed the sign up process and will be authenticated into the page.

10. Once you are authenticated in, you can then Browse the `API Products` and see your `notes` product that is now published to your environment.
	![](../img/lab1/26.png)

11. At this point we will stop, as we will be building additional apis and services that will be published to the portal.

	It should be noted that the notes application has more to it than we've shown in this lab. You're encouraged to dig in and discover the custom method that's implemented. In future labs, we'll be doing more work in the Developer Portal. For instance we'll be customizing the portal theme, registering an application, subscribing to APIs and testing them from a separate consumer application.


1. Close the `Firefox` web browser. If a warning is presented about closing multiple tabs, deselect the option to notify you in the future and click the `Close Tabs` button.



1. In the terminal, use the `control+c` keyboard command to quit the API Designer program.

# Lab 1 - Conclusion

**Congratulations!** You have developed and published your first API!

In this lab you learned:

+ How to create a simple LoopBack application
+ How to create a Representational State Transfer (REST) API definition
+ How to test a REST API
+ How to publish an API to the Developer Portal

Proceed to [Lab 2 - Create a LoopBack Application](../Lab%202%20-%20Create%20a%20LoopBack%20Application)




[important]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/important.png "Important!"
[info]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/info.png "Information"
[troubleshooting]: https://github.com/ibm-apiconnect/pot-onprem-docs/raw/master/lab-guide/img/common/troubleshooting.png "Troubleshooting"
