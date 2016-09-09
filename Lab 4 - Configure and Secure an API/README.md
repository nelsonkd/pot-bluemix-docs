# Lab 4 - Configure and Secure an API

In this lab, you will learn how to configure and secure the `inventory` API created during loopback application generation. Using the graphical design tools in API Designer, you will create an OAuth 2.0 provider API called `oauth` and then update the `inventory` API to use this provider. You will use the API Editor assembly view to specify the API's runtime behavior.

---
# Lab 4 - Objective

In the following lab, you will learn:

+ How to create an OAuth 2.0 Provider, specifically using the Resource Owner Password grant type.
+ How to secure an existing API using the newly created OAuth 2.0 Provider.
+ How to add catalog-specific properties to an API.
+ How to assemble an API implementation using the activity-log, set-variable and proxy policies

---
# Lab 4 - Case Study Used in this Tutorial

In this tutorial, you will secure the Inventory API to protect the resources exposed by **ThinkIBM**. Consumers of your API will be required to obtain & provide a valid OAuth token before they can invoke the Inventory API.

---
# Lab 4	- Step by Step Lab Instructions

## 4.1 - Working with the Inventory API in API Designer

1. First, launch API Designer by typing the following commands from your project directory:

	```bash
	cd ~/ThinkIBM/inventory/
	apic edit
	```

	API Designer will open in your browser. You may see an informational message about Draft APIs. (This message appears the very first time you launch the API Designer.) If so, click the `Got it!` button, when you are ready to proceed to creating an API.

	You should see the APIs view, and a single API listed. The `inventory` API was automatically created during loopback app generation. We will edit this API at a later step.
	
	![alt text](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/startapidesigner.png)

## 4.2 - Adding a New OAuth 2.0 Provider API

1. Click the `+ Add` button and select `OAuth 2.0 Provider API` from the menu.

1. Specify the following properties and click the `Add` button to continue.

	> Title: `oauth`
	
	> Name: `oauth`
	
	> Add to an existing product: `inventory 1.0.0`
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/newoauthprops.png)

1. The API Editor will launch. If this is your first time using the API Editor, you will see an informational message. When you are ready to proceed, click the `Got it!` button to dismiss the message.  
	
	The API Editor opens to the newly created `oauth` API. The left hand side of the view provides shortcuts to various elements within the API definition: Info, Host, Base Path, etc. By default, the API Editor opens to the `Design` view, which provides a user-friendly way to view and edit your APIs. You may notice additional tabs labeled `Source` and `Assemble`. We will work with these views as well.
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/newoauth-start.png)

1. Navigate to the `OAuth 2` section.

	Over the next several steps, we will set up OAuth-specific options, such as client type (public vs confidential), valid access token scopes, supported authorization grant types, etc. The [OAuth 2.0 Specification](http://tools.ietf.org/html/rfc6749) has detailed descriptions of each of the properties we are configuring here.

1. For the Client type field, click the drop down twisty and select `Confidential`.

1. Three scopes were generated for you when the OAuth API Provider was generated: `scope1`, `scope2`, `scope3`.

1.  Modify the values for `scope1`, set the following fields:

	> Name: `inventory`
	
	> Description: `Access to Inventory API`

1. Delete `scope2` and `scope3` by clicking the trashcan icons to the right of the scope definitions.

1. We want to configure this provider to *only* support the Resource Owner Password Credentials grant type. Deselect the `Implicit`, `Application` and `Access Code` Grants, but leave `Password` checked.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/oauthgranttypes.png)

1. Set the remaining OAuth 2 settings as follows:

	> Collect credentials using: `basic`
	
	> Authenticate application users using: `Authentication URL`
	
	> Authentication URL: `https://thinkibm-services.mybluemix.net/auth`
	
	> Turn off the `Enable revocation` option
	
	When complete, your settings should look like this:
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/1.png)

	> ![][important]
	> 
	> The scope defined here must be identical to the scope that we define later when telling the `inventory` API to use this OAuth config. A common mistake is around case sensitivity. To avoid running into an error later, make sure that your scope is set to all **lowercase**.

1. Switch to the `Assemble` tab.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/assembly.png)

1. Click the `Save` icon in the top right corner of the editor to save your changes.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/save-icon.png)

## 4.3 - Configuring and Securing the Inventory API

1. Click the `All APIs` link at the top left of the API Editor to return to list of APIs.

1. Click the `inventory` link.

	The inventory API will open in the API Editor, where we can make the necessary configuration changes. Over the next several steps you will set this API up to use the OAuth provider you just created.  
	

1. Click on the `trashcan` icon for the `x-any` Definition to remove it. Confirm the removal by clicking the `OK` button in the prompt.

1. Navigate to the `Base Path` section.

	Change the base path from `/api` to `/inventory`.

1. Navigate to the `Host` section of the API. **Remove** the `$(catalog.host)` value.

	As with the OAuth API Provider we just created, we want this value to remain empty.
	

1. Navigate to the `Security Definitions` section.

	Click the `+` icon in the **Security Definitions** section and select `OAuth` from the menu.  
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/inv-addoauthsecuritydef.png)
	
	A new security definition is created for you, called `oauth-1 (OAuth)`.

1. Scroll down slightly to edit the newly created security definition.

	Set it to have the following properties:
	
	> Name: `oauth`
	
	> Description: `Resource Owner Password Grant Type`
	
	> Flow: `Password`
	
	> Token URL: `https://api.us.apiconnect.ibmcloud.com/<yourorgname>-dev/sb/oauth20/token`

	> ![][important]
	> 
	> The Token URL will be based upon the location of your Org and Catalog running on Bluemix public.  You can find your base URL by logging into the API Manager on Bluemix and go into your catalog (the default catalog created is `Sandbox`).  From there go into `Settings`.  If you scroll down a bit you will see what your `API Endpoint` is called, simply copy and paste the contents into the token URL

![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/2.png)

1. Click the `+` icon in the **Scopes** section to create a new scope. Set the following properties.  Note the organization portion of the token URL will be different for each student. 

	> Scope Name: `inventory`
	
	> Description: `Access to all inventory resources`
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/3.png)

1. Navigate to the `Security` section and check the `oauth (OAuth)` checkbox.  

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/inv-security-addoauth.png)
	
	Now that the API is secured using our OAuth provider, we can define how the API should behave when called. In the next two sections, we will configure the `inventory` API to call our inventory application which was published at the end of Lab 3.

## 4.4 - Adding API Properties

Before we add and configure the `inventory` API processing policies, we need to set up a couple of API properties. These are used to hold parameters needed by the API, whose values vary based on which Catalog the API is running in.

For example, we will configure the `inventory` API to invoke a backend service. We want to be able to call different instances of that service based on which Catalog the API is deployed to.

1. Navigate to the `Properties` section and click the `+ Add` icon to create a new property. Give it the following attributes:

	> Name: `app-server`
	
	> Description: `Catalog-specific app server URL`
	
	> Default Value: `http://localhost/`

1. Add additional catalog-specific values by clicking the `Add value` link. Specify the following catalog name and value.  This value will be the `API Target URL` you captured from the previous lab when you published your Inventory application to bluemix.  This will be unique for each user.

	> Catalog: `Sandbox`
	
	> Value: your specific value e.g. `https://apiconnect-abcedf84-ce2f-aaaa-8ab1-6efd9f1fd6ee.someorg-dev.apic.mybluemix.net`

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/4.png)

	
	>![][important]
	> 
	> The Catalog and Value fields are strict. They are case-sensitive and must be typed exactly as shown.  You will note that the catalog drop down list will have a default entry there for `sb`. It is important that you type in the `Sandbox` name in the Catalog as indicated above, otherwise you will encounter issues.


1. Save your changes.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/save-icon.png)

## 4.5 - Defining API Processing Behavior
An API Assembly provides collection of policies which are enforced and executed on the API Gateway. Policies include actions like modifying the logging behavior and altering the message content or headers. Additionally, if the out of the box policies do not meet your specific needs, you may opt to create your own policy and have it available for API designers through the API Connect UI.

1. Switch to the `Assemble` tab. A simple assembly has been created for you.  

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/inv-assembly-start.png)

1. Modify your assembly to use DataPower Gateway policies.
	
	Select the `DataPower Gateway policies` radio button.
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/filter-datapowerpolicies.png)

1. Add an `activity-log` policy to the assembly and configure it to log API payload.  

	Drag the `activity-log` policy from the list of available policies to the left of the `invoke` policy already created in your assembly.

1. Select the newly added `activity-log` step. A properties menu will open on the right of your screen.

	Under `Content` select `payload` from the drop-down list.  
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/inv-assembly-logpayload.png)

1. Click on the `X` to close the activity-log editor menu.

1. Click on the `invoke` policy to bring up the editor.

1. Replace the default `Invoke URL` path.

	Update the URL to be: `$(app-server)$(request.path)`
	
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/invoke_url.png)
	
	> ![][info]
	> 
	> The `$(request.path)` variable will automatically remove the organization and catalog components of the full API Connect request path. Additionally, the leading slash `/` is already included in the variable value.

1. Click on the `X` to close the invoke policy editor menu.

1. Save your changes.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/save-icon.png)

1. Create a new Product called `InventoryTest`. We are going to use this just to test the inventory app and make sure the Oauth handshake is working.  

2. Add the `Inventory` API to the `InventoryTest` Product.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/8.png)

2. Publish your API to Bluemix clicking on the `Publish` button

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/5.png)

2. Click on your Bluemix instance.  Note each instance name is unique and will be different than the screenshot below.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/6.png)

3.  Select `Stage or Publish products` and then `Publish`

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/7.png)

1. Move on to the next section to validate the API

# Lab 4 - Validation

We will validate the inventory application by using an Oauth test app we have running in bluemix

1. Direct your browser to your developer portal URL.  Hopefully you created a bookmark for your portal page in lab #1. If you need a reminder of where your portal URL, you can get it from the settings screen from the 

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab1/22.png))
	
1. Log into your portal with your developer credentials (not the admin user)

1. Click the `Apps` link.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab7/PortalAppsList.png)

1. Click the `Register new Application` link.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab7/RegisterNewApplication.png)

1. Enter a title and description for the application as shown below and click the `Submit` button.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab7/SubmitNewApplication.png)

1. We need to capture the Client Secret and Client ID in a text editor for later use by our web application. Select the `Show Client Secret` checkbox next to Client Secret at the top of the page and the `Show` checkbox next to Client ID.  Copy and paste both of these to a document for retrieval here in a later step

1. Click the `API Products` link.

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab7/PortalAPIProductsList.png)

1. Click the `API Products` link.
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/9.png)
2. Select the `InventoryTest` Product
	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/10.png)
3. Click the `Subscribe` button for the`InventoryTest 1.0.0` Product

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/11.png)
4. Select your app then click `Subscribe`

	![](https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/lab4/12.png)

4. To test the API, we need to use a Web App to simulate the Oauth handshake.  To do this, direct your browser to the following URL:  `https://apim-services.mybluemix.net/oauth/ro_cred`
5. Enter in the following values into the Form
	> Client Type: `Confidential`
	
	> Token URL: `https://api.us.apiconnect.ibmcloud.com/enteryourtenanthere-dev/sb/oauth2/token`  Replace your tenant name over the `enteryourtenanthere` section of the URL
	
	> Resource Owner ID:  `this can be any value`
	
	> Resource Owner Password: `this can be any value`
	> 
	> Client Id: `Client ID for your App`
	> 
	> Client Secret: `Client Secret for your App`
	> 
	> Scope: `/inventory`
6. Go ahead blah
# Lab 4 - Conclusion

**Congratulations!** You have successfully configured and secured the inventory API. You will consume this API in a later step.

Proceed to [Lab 5 - Advanced API Assembly](../Lab%205%20-%20Advanced%20API%20Assembly)

[important]: https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/common/important.png "Important!"
[info]: https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/common/info.png "Information"
[troubleshooting]: https://github.com/ibm-apiconnect/pot-bluemix-docs/raw/5030/img/common/troubleshooting.png "Troubleshooting"
