# flowroute-numbers-php

**flowroute-numbers-php** is a PHP API Wrapper that provides methods for interacting with **v1** (version 1) of the [Flowroute](https://www.flowroute.com) API. These methods can be used to accomplish the following:

* Search for purchasable phone numbers
* Purchase phone numbers
* View your owned phone numbers and their related details
* Create new inbound routes
* Update the primary and failover route on a phone number

### Documentation 
The full documentation for the v1 Flowroute API is available [here](https://developer.flowroute.com/v1.0/docs).

##Before you begin

The following are required before you can deploy the SDK.

### Have your API credentials

You will need your Flowroute API credentials (Access Key and Secret Key). These can be found on the **Preferences > API Control** page of the [Flowroute](https://manage.flowroute.com/accounts/preferences/api/) portal. If you do not have API credentials, contact <mailto:support@flowroute.com>.

### Get a code text editor

Steps in this SDK describe creating one or more script files that allow you to execute the methods. Script files can be created either using a terminal window shell or through using a code text editor. For example, *Sublime Text*. 

### Download Composer

Composer is used to manage the dependencies for the PHP SDK. The Composer installation file, **composer.phar**, can be downloaded from Composer's web site [here](https://getcomposer.org/download). Download, but do not install it; only after first installing the libraries will you install Composer.

## Install the libraries

> **Note:** You must be connected to the Internet in order to install the required libraries.

1. Open a terminal session. 

2. If needed, create a parent directory where you want to install the SDK.
 
3. Change directories to the newly created directory, and from the command line run:

 	`git clone https://github.com/flowroute/flowroute-numbers-php.git`
 	
 	The `git clone` command clones the **flowroute-numbers-php** respository as a sub directory within the parent folder.
 	
4.	Change directories to the newly created **flowroute-numbers-php** directory.

##Install Composer

1.	Move the downloaded **composer.phar** file to the **flowroute-numbers-php** directory.

	>**Note:** **composer.phar** must be in the **flowroute-numbers-php** directory in order to install correctly. Composer requires a **composer.json** file, which is included in the imported SDK to help manage dependencies.

2. 	From a terminal window, run:

		php composer.phar install

 	Composer sets up the required file structure.

3. Next, set up **flowroute-numbers-php** to use your API credentials. 

##Set up your API credentials<a name=credentials></a>

1.	From the **flowroute-numbers-php** directory change directories to **src**. 

2.	Using a code text editor, open **Configuration.php**.

3.	In **Configure.php** replace the AccessKey and SecretKey variables with your Flowroute API credentials. The file should resemble the following:

	```sh
		<?php
		/*
		 * FlowrouteNumbersLib
		 *
		 * This file was automatically generated for flowroute by APIMATIC BETA v2.0 on 02/12/2016
		 */
	
		namespace FlowrouteNumbersLib;
	
		class Configuration {
 			//The base Uri for API calls
   			public static $BASEURI = 'https://api.flowroute.com/v1';
	
			//Tech Prefix
    		//TODO: Replace the $username with an appropriate value
			public static $username = 'AccessKey';

			//API Secret Key
			//TODO: Replace the $password with an appropriate value
			public static $password = 'SecretKey';
		}
```

4.	Save the file.

	The Controllers point automatically to **Configuration.php**, so there is no need to do anything else with this file.
	
5.	With the libraries set up and your API credentials added, you can now run the methods to perform functions within the SDK. There are two ways of doing this.

	*	[Use demo.php](#usedemo)
	*	[Create a PHP file](#createphp)

## Use demo.php<a name=usedemo></a>

A demo PHP file, **demo.php**, is included with the installed libraries. This file contains a list of the methods and parameters.  You can use this file to run with your API credentials, instantiate all Controllers, and invoke all methods.

To use **demo.php**, open the file with a code text editor and modify parameters if needed or comment out lines. Whether or not you add any parameters or comment out lines, the file can be run as-is by running the following on the command line:

	run demo.php

For information on the parameters within the file, see the applicable Controller information:

*	[`PurchasablePhoneNumbersController`](#purchaseno)

*	[`TelephoneNumbersController`](#telephoneno)

*	[`InboundRoutesController`](#inboundco) 

If you do not want to use the file, the following sections describe creating your own PHP files.

## Create a PHP file to import the Controllers and Models<a name=createphp></a>

The following describes importing the SDK and setting up your API credentials.  Importing the SDK allows you to instantiate the [Controllers](#controllers), which contain the methods used to perform tasks with the SDK. In order to do this, you will need to create and run a PHP file. You can create the file either through using a terminal shell or through a code text editor. The sample files in this SDK were created using a code text editor. In the following example, all Controllers are instantiated using a single file:

1.	Using a code text editor, create a new file.

2.	At the top of the file, add the following line:

		require_once('vendor/autoload.php');

3.	Next add the lines that instatiate the Controllers:

		use FlowrouteNumbersLib\Controllers\InboundRoutesController;
		use FlowrouteNumbersLib\Controllers\PurchasablePhoneNumbersController;
		use FlowrouteNumbersLib\Controllers\TelephoneNumbersController;
		use FlowrouteNumbersLib\APIException;

4.	Add the lines the set variables for each of the Controllers:

		$irc = new InboundRoutesController();
		$pnc = new PurchasablePhoneNumbersController();
		$tnc = new TelephoneNumbersController();

5.	Add lines that call the BillingMethod and Route models:

		use FlowrouteNumbersLib\Models\BillingMethod;
		use FlowrouteNumbersLib\Models\Route;
		
6.	Optionally at the end of the file, add a line that prints out a response after invoking a method, allowing you to see the response in the terminal window:

		print_r($response);

 >**Important:** Throughout this SDK, `response` is used in examples. `response` is a variable name that can be changed to a name of your own choosing. It can support an unlimited number of characters. If you choose to rename `response`, make sure that any method that references that variable name is also changed to use the new name. For example, you might have the following:
>
>`$blob = $pnc->listAvailableNPAs();`
>
>`print_r($blob);`

7.	Save the PHP file in your top-level **flowroute-numbers-php** directory with a .php extension. For example, *mycontrollers.php*.

8.	Add Controller methods as needed. See [Controllers](#controllers).

###Example PHP file
	
The following shows an example of a single PHP file that imports and instantiates all three Controllers:
	
		
		<?php
		require_once('vendor/autoload.php');
	
		use FlowrouteNumbersLib\Controllers\InboundRoutesController;
		use FlowrouteNumbersLib\Controllers\PurchasablePhoneNumbersController;
		use FlowrouteNumbersLib\Controllers\TelephoneNumbersController;
		use FlowrouteNumbersLib\APIException;
		
		$irc = new InboundRoutesController();
		$pnc = new PurchasablePhoneNumbersController();
		$tnc = new TelephoneNumbersController();
		
		use FlowrouteNumbersLib\Models\BillingMethod;
		use FlowrouteNumbersLib\Models\Route;
		
		print_r($response);
		
With this in mind, you can then decide the approach you want to take towards creating a file. You can create your own PHP file using any of the following options:
 
 1.	Create a single file that contains all of the Controllers and methods, then commenting out the lines for each method you don't want to run.
 
 2.	Create a unique file for each Controller, adding only those lines relevant to that Controller and related methods, and then commenting out the lines for each method you're not using. You would create three unique Controller files.
 
 3.	Create a unique file for each method. Each file will then contain the lines instantiating the relevant Controller.

This SDK describes the second option. However, whichever option you select, the file(s) should be saved in the **flowroute-numbers-php** directory. When you want to invoke a method using a PHP file, in a terminal window run the following on the command line from the **flowroute-numbers-php** directory:

		run <Controller File Name.php>

## Controllers<a name=controllers></a>

This following sections describe **flowroute-numbers-php** Controllers:

*	[`PurchasablePhoneNumbersController`](#purchaseno)

*	[`TelephoneNumbersController`](#telephoneno)

*	[`InboundRoutesController`](#inboundco) 

###Passing parameters and values in a method

When passing a method, and the method has additional parameters, you are not required to pass the parameter name in the method. For example, a method can pass parameters as follows:

	listAreaAndExchange ($limit=10,$npa=206,$page=3);
	
However, the method can also be run without passing the parameter name:

	listAreaAndExchange (10,206,3);

References to method parameters in this SDK use the latter method of not passing parameter names.

>**Important:** The SDK displays sample responses. Formatting of the responses is provided for clarity only. They are not intended to show the formatting of your own response. 

### PurchasablePhoneNumbersController<a name=purchaseno></a> (.\flowroute-numbers-php\src\Controllers)

\\flowroute-numbers-php\src\Controllers

The PurchasablePhoneNumbers Controller contains the methods necessary to search through Flowroute's phone number inventory.  The following shows a sample file named **purchase.php** file, which invokes the Controller's methods:

	<?php

	require_once('vendor/autoload.php');

	use FlowrouteNumbersLib\Controllers\PurchasablePhoneNumbersController;
	use FlowrouteNumbersLib\APIException;
	
	$pnc = new PurchasablePhoneNumbersController();

	#List Available NPAs
	$response = $pnc->listAvailableNPAs();
	
	#List Area and Exchange
	$response = $pnc->listAreaAndExchange();
	
	#Search
	$response = $pnc->search();
		
	print_r($response);	

When creating your own PHP file, add each method after `$pnc = new PurchasablePhoneNumbersController();` but before `print_r($response);`. If you do not want to execute a specific method, comment those lines out with `#`. Click each link below to see more information about that method.

*	[`listAvailableNPAs()`](#listnpa)
* 	[`listAreaAndExchange()`](#listnpanxx)
* 	[`search()`](#searchno)

You can run the file on the command line using the `php <PHP file>` command.

#### `listAvailableNPAs ($limit);`<a name=listnpa></a>

The `listAvailableNPAs` method allows you to retrieve a list of every NPA (area code) available in Flowroute's phone number inventory.
#####Usage

Add the following lines to your PHP file:

	#List Available NPAs
	$response = $pnc->listAvailableNPAs();
	
The method can take the following parameter:

| Parameter | Required |Type |Description                           |
|-----------|----------|-----|--------------------------------|
| `limit`     | False    | integer or null| Controls the number of items returned. Either a number between `1` and `200` must be used, or `null`.  If `null` is passed instead of a number, a default of ten NPANXX combinations are returned.  |

>**Note:** The method can be invoked by passing only `()`, which returns a default `limit` of ten NPAs.

##### Example usage

The following example limits the number of NPAs returned to `3`.
	
	#List Available NPAs
	$response = $pnc->listAvailableNPAs(3);

#####Example response

For the `listAvailableNPAs(3)` request, the first three NPAs are returned:

```sh
(
    [npas] => stdClass Object
        (
            [201] => stdClass Object
                (
                    [nxxs] => /v1/available-tns/npanxxs/?npa=201
                    [tns] => /v1/available-tns/tns/?npa=201
                )

            [203] => stdClass Object
                (
                    [nxxs] => /v1/available-tns/npanxxs/?npa=203
                    [tns] => /v1/available-tns/tns/?npa=203
                )

            [202] => stdClass Object
                (
                    [nxxs] => /v1/available-tns/npanxxs/?npa=202
                    [tns] => /v1/available-tns/tns/?npa=202
                )

        )

    [links] => stdClass Object
        (
            [next] => /v1/available-tns/npas/?limit=3&page=2
        )
```

##### Error response

| Error code | Message  | Description                                                 |
|------------|----------|-------------------------------------------------------|
|No error code|HTTP Response Not OK or APPLICATION/SERVER ERROR|Typically this occurs when a `limit` does not fall within the allowed range of `1` to `200`, or if a negative number was passed. |

#### `listAreaAndExchange ($limit,$npa,$page);`<a name=listnpanxx></a>

The `listAreaAndExchange` method allows you to retrieve a list of every NPANXX (area code and exchange) combination available in Flowroute's phone number inventory.

#####Usage

Add the following lines to your PHP file:

	#List NPA and NXX
	$response = $pnc->listAreaAndExchange();

The method takes the following parameters:

| Parameter | Required |Type| Description                                                         |
|-----------|----------|--------------|-------------------------------------------------|
| `limit`     | False    | integer or null| Controls the number of items returned. Either a number between `1` and `200` must be used, or `null`.  If `null` is passed instead of a number, a default of ten NPANXX combinations are returned.                 |
| `npa`       | False  | integer or null| Three-digit area code or `null` must be used. Limits results to the specified NPA. If `null` is passed, all NPAs are returned. Partial number search is also supported. For example, passing `20` returns all NPA and NXX results that include `20`. |
| `page`      | False  |integer or null  | Sets which page of the results is returned. If a number is not passed, `null` must be used. ` Next` and `Prev` URLs provided at the bottom of the response provide navigation pointers. If `null` is passed, all pages are returned.   |

>**Note:** The method can be invoked by passing only `()`, which sets `null` as the default for all parameters.

##### Example usage

In the following, a request is made to limit the results to `2`, the NPA to `203` and to display page `3`:
		
	#List NPA and NXX
	$response = $pnc->listAreaAndExchange(2,203,2);

#####Example response
Based on the example usage above, the following two NPANXX combinations are returned on page 2, organized by NPANXX. 

```sh
(
    [npanxxs] => stdClass Object
        (
            [203583] => stdClass Object
                (
                    [tns] => /v1/available-tns/tns/?npa=203&nxx=583
                )
            [203567] => stdClass Object
                (
                    [tns] => /v1/available-tns/tns/?npa=203&nxx=567
                )
        )
    [links] => stdClass Object
        (
            [prev] => /v1/available-tns/npanxxs/?npa=203&limit=2&page=2
            [next] => /v1/available-tns/npanxxs/?npa=203&limit=2&page=4
        )
)
```
The following shows an example if no results are found for the passed parameters:

	(
    [links] => stdClass Object
        (
            [prev] => /v1/available-tns/npanxxs/?npa=555&limit=2&page=1
        )

	)

##### Error response

| Error code | Message  | Description                                                 |
|------------|----------|-------------------------------------------------------|
|No error code|HTTP Response Not OK or APPLICATION/SERVER ERROR|Typically this occurs when a `limit` does not fall within the allowed range of `1` to `200`, or if a negative number was passed. |

#### `search ($limit,$npa,$nxx,$page,$ratecenter,$state,$tn);`<a name=searchno></a>

The search method is the most robust option for searching through Flowroute's purchasable phone number inventory. It allows you to search by NPA, NXX, Ratecenter, State, and TN.

#####Usage

	#Search
	$response = $pnc->search();

The method supports the following parameters:

| Parameter  | Required|   Type|          Description                                         |
|------------|----------|------|--------------------------------------------------------|
| `limit`     | False    | integer or null| Controls the number of items returned. Either a number between `1` and `200` must be used, or `null`.  If `null` is passed instead of a number, a default of ten NPANXX combinations are returned.                             |
| `npa`       | False, unless `nxx` is passed, then `True`.  | integer| Three-digit area code. Limits results to the specified NPA. If `null` is passed, all NPAs are returned. Partial number search is also supported. For example, passing `20` returns all NPA and NXX results that include `20`.|
| `nxx`       |False  | integer |Three-digit exchange. Limits the results for the specified NXX. If no `nxx` is passed, `null` is used and all results are returned. Partial search is also supported. For example, passing `'45'` for the `nxx` returns exchanges that include `45`. Note that if you pass an `nxx` you must also pass an `npa`. |
| `page`      | False   | integer |Sets which page of the results is returned.` Next` and `Prev` URLs provided at the bottom of the response provide navigation pointers. If `null` is passed, all pages are returned.   |            
| `ratecenter` | False |string   | Limits the results to the specified ratecenter.  This field is case-insensitive. |                      
| `state`      | False, unless `ratecenter` is passed, then `True`.|string | Limits results to the specified state or Canadian province. Must be formatted using the two-letter state or province/territory abbreviation. This field is case-insensitive.                           |
| `tn`         | False  |string             | Limits results to the specified telephone number. The phone number must be passed as an 11-digit number formatted as *`1NPAXXXXXX`*.  |

>**Note:** The method can be invoked by passing only `()`, which sets `null` as the default for all parameters. The number of results returned are then limited to a default of ten.

##### Example Usage

In the following example, a search request sets the `limit` to `3`, `206` for the `npa`, `641` for the `nxx`, `2` for the `page`, `seattle` for the `ratecenter`, `wa` for the `state`, and `null` for the `tn`.

	#Search
	$response = $pnc->search(3,206,641,2,seattle,wa,null);
	
##### Example response
Based on the passed parameters passed in `search()`, the response returns three results:

```sh
(
    [tns] => stdClass Object
        (
            [12066417848] => stdClass Object
                (
                    [initial_cost] => 1.00
                    [monthly_cost] => 1.25
                    [billing_methods] => Array
                        (
                            [0] => VPRI
                            [1] => METERED
                        )
                    [ratecenter] => SEATTLE
                    [state] => WA
                )
            [12066417632] => stdClass Object
                (
                    [initial_cost] => 1.00
                    [monthly_cost] => 1.25
                    [billing_methods] => Array
                        (
                            [0] => VPRI
                            [1] => METERED
                        )
                    [ratecenter] => SEATTLE
                    [state] => WA
                )
            [12066417664] => stdClass Object
                (
                    [initial_cost] => 1.00
                    [monthly_cost] => 1.25
                    [billing_methods] => Array
                        (
                            [0] => VPRI
                            [1] => METERED
                        )
                    [ratecenter] => SEATTLE
                    [state] => WA
                )
        )
    [links] => stdClass Object
        (
            [next] => /v1/available-tns/tns/?npa=206&nxx=641&state=wa&ratecenter=seattle&limit=3&page=2
        )
)
```

#####Response field descriptions	

The following information is returned in the response:

Parameter | Description                                             |
|--------|-------------------------------------------------------|
| `tns`  | Object composed of a `telephone number`, `state`, `ratecenter`, and `billing_methods`.|                           |
||	*`telephone number`*- The retrieved telephone number object, which is composed of:|
||	<ul><ul><li> `initial_cost`- The one-time fixed cost for that telephone number. The default value is USD `1.00`.</ul>|
| | <ul><ul><li>`monthly_cost`- The recurring monthly cost to maintain that telephone number. The default value is USD `1.25`.</ul>|
| |<ul><ul><li>`billing_methods`- Displays the billing methods available for the telephone number: <ul><li>`[0] VPRI`, or</ul></li> <ul><li>`[1] METERED` </ul></li>|
||	`ratecenter`- The ratecenter associated with the NPANXX.|
||	`state`- The US state or Canadian province or territory in which the NPANXX is located.</ol>|


### TelephoneNumbersController<a name=telephoneno></a>(.\flowroute-numbers-php\src\Controllers)

The TelephoneNumbersController contains the methods necessary to purchase and manage a Flowroute number. The following shows a sample file named **telephone.php** file, which invokes the Controller's methods:

	<?php

	require_once('vendor/autoload.php');

	use FlowrouteNumbersLib\Controllers\TelephoneNumbersController;
	use FlowrouteNumbersLib\APIException;
	
	$tnc = new TelephoneNumbersController();
	
	use FlowrouteNumbersLib\Models\BillingMethod;
	
	#Purchase a Telephone Number
	$billing = new BillingMethod('');
	$number = 'phone number';
	$response = $tnc->purchase($billing, $number);
		
	#List Account Telephone Numbers
	$response = $tnc->listAccountTelephoneNumbers();
	
	#Telephone Number Details
	$number = 'telephoneNumber';
	$response = $tnc->telephoneNumberDetails($number);
	
	#Update Telephone Number Routes
	$rtes = '{"routes": [{"name": "primary route name"}, {"name": "failover route name"}]}'; 
	$response = $tnc->update('number',$rtes);
		
	print_r($response);
	

Add any of the following TelephoneNumbersController methods after `use FlowrouteNumbersLib\Models\BillingMethod;`, but before `print_r($response)`. If you do not want to execute a specific method, comment out that method's lines with `#`.

The Controller supports the following methods:

*	[`purchase`](#purchaseno)
*	[`listAccountTelephoneNumbers`](#listnumbers)
*	[`telephoneNumberDetails`](#phonedetails)
*	[`update`](#updateroute)

#### `purchase ($billing, $number);`<a name=purchaseno></a>

The purchase method is used to purchase a telephone number from Flowroute's inventory. To purchase a telephone number you can first invoke the [search](#searchno) method to retrieve a list of available numbers for purchase.

#####Usage

Add the following lines to your PHP file:

	#Purchase a Telephone Number
	$billing = new BillingMethod('');
	$number = 'phone number';
	$response = $tnc->purchase($billing, $number);

First, define the variable names used in the method: 

|Variable name    |Required  |Type      |Description|
|-----------------|----------|----------|-------------------------------------------------------| 
|`$billing`      | True     | string   |The variable name assigned to the billing method. An unlimited number of characters can be used. For this example, `$billing` is the name of the variable. |
|`$number`        | True     | string   | This variable identifies the phone number to purchase. An unlimited number of characters can be used. For this example, `$number` is the name of the variable.|

Next, define the `$billing` and `number` variables:

| Parameter       | Required | Type|Description                                                 |                                                          
|-----------------|----------|--------|-------------------------------------------------------|
| `BillingMethod('')`   | True     |string  | Sets the billing method for the purchased number. This must be one of the following: <ul><li>`METERED` — unlimited concurrent calls, each billed per-minute used.</li> <li> `VPRI` — limits the number of concurrent calls to the number of VPRI channels you have, but with unlimited usage on each channel. </li></ul>|       
| `phone number` | True    | string | The telephone number to purchase, using an E.164 *`1NPANXXXXXX`* format.                |
	
##### Example Usage

In the following example, a new number is purchased using `VPRI` for the billing method:

	#Purchase a Telephone Number
	$billing = new BillingMethod('VPRI');
	$number = '12066417848';
	$response = $tnc->purchase($billing, $number);

#####Example response

If the purchase is successful, a **201 Created** and empty body are returned indicating the date on which the purchase occurred:

		(
   		 [code] => 201
       		 [raw_body] =>
   		 [body] =>
   		 [headers] => Array
     	   (
     	       [0] => HTTP/1.1 201 Created
     	       [Content-Type] => application/json
    	        [Date] => Thu, 26 May 2016 18:32:36 GMT
    	        [Server] => nginx
   	         [Content-Length] => 0
    	        [Connection] => keep-alive
  	    	  )
		)

##### Error response

| Error code | Message  | Description                                                 |
|------------|----------|-------------------------------------------------------|
|No error code.  |HTTP Response Not OK|The phone number to purchase might already have been purchased, or the number might have been entered incorrectly.|

####`listAccountTelephoneNumbers ($limit,$page,$pattern);`<a name=listnumbers></a>

The `listAccountTelephoneNumbers` method is used to retrieve a list of all of the phone numbers on your Flowroute account.

#####Usage

	#List Account Telephone Numbers
	$response = $tnc->listAccountTelephoneNumbers();

>**Note:** The method can be invoked by passing only `()`, which sets `null` as the default for all parameters. The number of results returned are then limited to a default of ten.

The method takes the following parameters:

| Parameter | Required |     Type | Description                                    |
|-----------|----------|-----------|-----------------------------------------------|
| `limit`     | False    | integer or null| Controls the number of items returned. Either a number between `1` and `200` must be used, or `null`.  If `null` is passed instead of a number, a default of ten telephone numbers are returned.                 |
| `page`      | False  |integer or null  | Sets which page of the results is returned. If a number is not passed, `null` must be used. ` Next` and `Prev` URLs provided at the bottom of the response provide navigation pointers. If `null` is passed, all pages are returned.   |
| pattern   | False | string  | The phone number on which to search. Partial number search is supported; for example, if `206` is passed the response returns all phone numbers which include `206`. If neither a number nor `null` are passed, all numbers associated with the account are returned.  |

##### Example Usage
For this example, the `limit` is `1`, the `page` is `null`, and the `pattern` includes `206`.
	
	#List Account Telephone Numbers
	$response = $tnc->listAccountTelephoneNumbers(1,null,206);

#####Example response

Based on the parameters passed above, details about the telephone number are returned in the response:

	(
    [tns] => stdClass Object
        (
            [12066417848] => stdClass Object
                (
                    [billing_method] => VPRI
                    [routes] => Array
                        (
                            [0] => stdClass Object
                                (
                                    [type] => SIP-REG
                                    [name] => sip-reg
                                )

                            [1] => stdClass Object
                                (
                                    [type] => SIP-REG
                                    [name] => sip-reg
                                )
                        )
                    [detail] => /v1/tns/12066417848
                )
        )
    [links] => stdClass Object
        (
            [next] => /v1/tns/?pattern=206&limit=1&page=2
        )
	)    
 
#####Response field descriptions	
 
The following information is returned in the response:

Parameter | Description                                             |
|--------|-------------------------------------------------------|
| `tns`  | Object composed of a `telephone number`, `billing_method`, and `routes`.|                           
||	*`telephone number`*- The retrieved telephone number object, which is composed of:|
||	<ul><ul><li> `billing_method`- The billing method assigned to the phone number when the number was purchased. This will be either `METERED` or `VPRI`.</ul>|
| |<ul><ul><li>`routes`- Displays the primary `[0]` and failover `[1]` routes for the phone number: <ul><li>`type` — Indicates the type of route: `HOST`, `PSTN`, or `URI`. If no route is assigned, `SIP-REG` is the default name assigned to the route.</ul></li> <ul><li>`name` — Name of the route. If no `name` was given to the route, `sip-reg` is the assigned default name.</ul></li> **Note:** Routes are created using the [createNewRoute](#createroute) method and existing routes can be viewed using the [mlist](#listroutes) method.|

#### `telephoneNumberDetails($number);`<a name=phonedetails></a>

The `telephoneNumberDetails` method is used to retrieve the billing method, primary route, and failover route for the specified telephone number. 

##### usage

		#Telephone Number Details
		$number = 'telephoneNumber';
		$response = $tnc->telephoneNumberDetails($number);

First, define the variable name that identifies the telephone number: 

| Parameter       | Required | Type   |Description                                    |
|-----------------|----------|--------|-------------------------------------------|
|`$number`        | True     | string   | This variable name identifies the phone number for which you want to retrieve details. An unlimited number of characters can be used. For this example, `$number` is used.|

Next, define the `number` variable:

| Parameter       | Required | Type   |Description                                    |
|-----------------|----------|--------|-------------------------------------------|
| `telephoneNumber` | True     | string |    The Flowroute telephone number on which to query. You must use an 11-digit, E.164 number, formatted as *`1NPANXXXXXX`*. Neither partial number search nor multiple number search are supported. |

##### Example Usage

In the following example, the number purchased using the [purchase](#purchaseno) method is passed in the request:

	#Telephone Number Details
	$number = '12066417848';
	$response = $tnc->telephoneNumberDetails($number);

#####Example response
	(
    [billing_method] => VPRI
    [routes] => Array
        (
            [0] => stdClass Object
                (
                    [type] => SIP-REG
                    [name] => sip-reg
                )
            [1] => stdClass Object
                (
                    [type] => SIP-REG
                    [name] => sip-reg
                )
        )
	)

#####Response field descriptions	
 
The following information is returned in the response:

Parameter | Description                                             |
|--------|-------------------------------------------------------|                       
|`billing_method`| The billing method assigned to the phone number when the number was purchased. This will be either `METERED` or `VPRI`.|
|`routes` |Displays the primary `[0]` and failover `[1]` routes for the phone number:<br> <ul><li>`type` — Indicates the type of route: `HOST`, `PSTN`, or `URI`. If no route is assigned, `SIP-REG` is the default name assigned to the route.</li> <li>`name` — Name of the route. If no `name` was given to the route, `sip-reg` is the default name.</ul></li>**Note:** Routes are created using the [createNewRoute](#createroute) method and can be assigned using the `update` method.|

#### `update ($number, $rtes);`<a name=updateroute></a>

The `update` method is used to update both the primary and failover route for a phone number. Both the primary and failover route must be specified inside of an array. See Example Usage below. The first route name specified is assigned as the primary route and the second route name specified will be assigned as the failover route. The list of available route names can be retrieved by using the list method in the InboundRoutesController.

>**Note:** In order to apply an existing route to a number, the route must first be created using the [createNewRoute](#createRoute) method. To view a list of your existing routes, use the [`mlist`](#listroutes) method.

#####Usage

	#Update Routes
	$rtes = '{"routes": [{"name": "primary route name"}, {"name": "failover route name"}]}'; 
	$response = $tnc->update('number',$rtes);

First, define the variable name that identifies the array:

| Parameter       | Required | Type |Description |                                                     
|-----------------|----------|-------|----------------------------------------------------------|
|`rtes`|True| string| Variable name that identifies the array. This field can be of unlimited characters. In this example, `rtes` is used.|

Next, define the variables that compose the array:

| Parameter       | Required | Type |Description |                                                     
|-----------------|----------|-------|----------------------------------------------------------|
|`primary/failover route name`|True| string| Name of a current route. The first `"Name"` in the array will be assigned the primary route; the second `"Name"` will be assigned the secondary, or failover, route. |
| `number` | True     | string |    The telephone number for which to update the route. You must use an 11-digit, E.164 number, formatted as *`1NPANXXXXXX`*.| 

##### Example Usage
	
	#Update Routes
	$rtes = '{"routes": [{"name": "HOSTroute1"}, {"name": "PSTNroute1"}]}'; 
	$response = $tnc->update('12064205780',$rtes);
	
#####Example response

No confirmation message is returned for a successful update. To view the route changes on the phone number, run the 
[`listAccountTelephoneNumbers()`](#inboundco) or [`telephoneNumberDetails()`](#phonedetails) methods.

#####Error response 
| Error code | Message  | Description                                           |
|------------|----------|-------------------------------------------------------|
|No error code.  |HTTP Response Not OK|This can be caused when a route does not exist, a route name has been misspelled, or an incorrect phone number was passed in the PHP file.|

###InboundRoutesController<a name=inboundco></a>(.\flowroute-numbers-php\src\Controllers)

The InboundRoutesController contains the methods required to view all of your existing inbound routes and to create new inbound routes. The following shows a sample file named **routes.php** file, which invokes the Controller's methods:

	<?php

	require_once('vendor/autoload.php');

	use FlowrouteNumbersLib\Controllers\InboundRoutesController;
	use FlowrouteNumbersLib\APIException;

	$irc = new InboundRoutesController();
	
	use FlowrouteNumbersLib\Models\Route;
	
	#List Routes
	$response = $inbound->mlist();
	
	#Create a New Route
	$response = $irc->createNewRoute('routeName','type','value');
	
	print_r($response);


Add the following InboundRoutesController methods between `use FlowrouteNumbersLib\Models\Route;` and `print_r($Response)`. If you do not want to execute a specific method, comment out that method's lines with `#`.

The Controller supports the following methods:

*	[`mlist`](#listroutes)
* 	[`createNewRoute`](#createroute)

#### `mlist ($limit,$page);`<a name=listroutes></a>

The list method is used to return all of the existing inbound routes from your Flowroute account.

#####Usage

	#List Routes
	$response = $inbound->mlist();


>**Important:**  `$inbound` and `$response` are variables that can be assigned any name of you choose, and of any length; however, you must use the names consistently within the method.

The method takes the following parameters:

| Parameter | Required | Type   |Description                                    |
|-----------|----------|---------|----------------------------------------|
| `limit`     | False    | integer| Controls the number of routes returned. The maximum number is 200. If neither a number nor `null` are passed, a default of ten routes are returned.  |                    
| `page`      | False  |integer  | Sets which page of the results is returned.` Next` and `Prev` URLs provided at the bottom of the response provide navigation pointers. If `null` is passed, all pages are returned.   |

##### Example Usage

For this example, a `limit` of `4` routes  and the `page` to return set to `null` are passed.

	$List Routes
	$inbound = new InboundRoutesController();
	$response = $inbound->mlist(4,null);
	
#####Example response

Based on the parameters passed in the request, the following is returned:

	(
    [routes] => stdClass Object
        (
            [HOSTroute1] => stdClass Object
                (
                    [type] => HOST
                    [value] => 24.239.23.40:5060
                )
            [PSTNroute1] => stdClass Object
                (
                    [type] => PSTN
                    [value] => 178
                )
            [URIroute1] => stdClass Object
                (
                    [type] => URI
                    [value] => sip:16476998778@215.122.69.152:5060
                )
            [sip-reg] => stdClass Object
                (
                    [type] => SIP-REG
                    [value] =>
                )
        )
	)

These routes can be applied to any of your purchased phone numbers using the [`update`](#updateroute) method.

#####Response field descriptions

The following information is returned in the response:

| Parameter |  Description                                                     |
|-----------|--------------------------------------------------------------------------------|
| `[routeName]` |  The name of the route assigned using the `createNewRoute` method. It is composed of:<ul> <li>`type`  The type of route created using the `createNewRoute` method. Will be `HOST`, `PSTN`, or `URI`. If no route type was assigned, `SIP-REG` is used as the default. <li>`value` Value of the route, assigned to the route `type` using the `createNewRoute` method.</ul</li>|

#### `createNewRoute ($routeName,$type,$value;)`<a name=createroute></a>
 
The `createNewRoute` method is used to create a new inbound route. A new inbound route can then be applied to a phone number using the [`update`](#updateroute) method.

#####Usage

	#Create a New Route
	$response = $irc->createNewRoute('routeName','type','value');

The method takes the following parameters:

| Parameter | Required | Type| Description                                                                        |
|-----------|----------|------|-----------------------------------------------------------------------------|
| `routeName` | True    |  string| The name of the new route. An unlimited number of alphanumeric characters is supported. There are no unrestricted characters.  |
| `type`      | True   |  string |The type of route you would like to create. Valid options are `HOST`, `PSTN`, and `URI`. |
| `value`     | True    |string |  Value of the route, dependent on the `type`: <ul><li>If `HOST`, the value must be an IP address or URL with an optional port number—for example, an IP address could be `24.239.23.40:5060` or a URL could be `myphone.com`. If no port is specified, the server will attempt to use DNS SRV records. <li>If `PSTN`, the value must be formatted as a valid E.164, 11-digit formatted North American phone number—for example,`12066417848`. You cannot use the same number as the number for which the route is created. <li>If `URI`, the value must be formatted as  `protocol:user@domain[:port][;transport=<tcp/udp>`—for example, `sip:alice@seattle.com`,  `sip:12066417848@215.122.69.152:5060;transport=tcp`, or `sips:securecall@securedserver.com`.You cannot use the same number as the number for which the route is created. </li></ul>              |

##### Example Usage

You can pass as many `createNewRoute` methods in a single operation. The following example creates new `PSTN`, `HOST`, and `URI` routes:

	#Create a New Route
	$response = $irc->createNewRoute('PSTNroute2','PSTN','12066417848');
	print_r($response);
	$response = $irc->createNewRoute('HOSTroute2','HOST','4.239.23.40:5060');
	print_r($response);
	$response = $irc->createNewRoute('URIroute2','URI','sip:12066417848@215.122.69.152:5060');
	print_r($response);

>**Note**: In the example above, `print_r($response);` is added after each line. This returns a success or error response for each line.
	
#####Example response

No response is returned for each successfully created route; no other code or message is returned. An error encountered for a specific `irc.create_new_route()` line will not prevent the other routes from being created.

#####Error response
The following error can be returned:

| Error code | Message  | Description                                           |
|------------|----------|-------------------------------------------------------|
|No error code|HTTP Response Not OK|Typically this occurs when a `value` is malformed. |