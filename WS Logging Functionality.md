####Description

This document will explain the process of logging web service's request and response.

####Prerequisites
 
Need to create custom module named WS Logs (mng_Logs) using module builder with following custom fields. 

● ws_name (web service name)<br />
● phone_number (user phone number who call the WS, if it was admin the value was admin).<br />
● log_request (user request).<br />
● log_response (sugar response).<br />
● log_coments (comments)<br />

####How it works
 
####Step 1:

We need to declare one global variable named $sugar_config['debug'] in Sugar config.php file to turn on and off the logging.

**_Code:_**
	
```
    
         $sugar_config['debug']  => true, i.e.  WS logging was enabled.

         $sugar_config['debug']  => false, i.e. WS logging was disabled.
	 
```

####Step 2:

 Once user run any soap request, all web service's requests will hit the soap.php file in Sugar Server.

####Step 3: 

This soap.php file includes the nusoap.php file.<br />
File location was include/nusoap/nusoap.php.<br />

####Step 4: 

When requests hits soap.php file,it initiate the soap_server class in nusoap.php and calls the service function. Like the following.

	
**_Code:_**
	
```

$server = new soap_server;
$server->configureWSDL('sugarsoap', $NAMESPACE, $sugar_config['site_url'].'/soap.php');
$server->service ($HTTP_RAW_POST_DATA, $sugar_config['debug']);

```

####Step 5: 

The nusoap.php file will handle the requests, validating and send the response.<br />
Before sending the response we are logging the web services name, phone number, request and response.<br />
In function send_response () in nusaop.php file, we are initiating the LYTLog Class and passing webservice details.<br />


**_Code:_**
	
```

$lyt_log_instance = new LYTLog();
$lyt_log_instance->saveWSLog($this->methodname,$phone_number,$this->requestData,$this->formatXML($payload));

```

####Step 6:

And the LYTLog class will save int to WS Logs module.<br />
LYTLog class file path: MangoLib/errorhandling/LYTLog.php.<br />


**_Code:_**
	
```
         Function saveWSLog($ws_name,$phone_number,$request,$response)
	    {
	
		$ws_log_obj = new mng_Logs();		
		$ws_log_obj->name=$ws_name;
		$ws_log_obj->ws_name=$ws_name;
		$ws_log_obj->phone_number=$phone_number;
		$ws_log_obj->log_request=$request;
		$ws_log_obj->log_response=$response;
		$ws_log_obj->save ();
		//print_r ($ws_log_obj); exit;
		
	   }

```
<br />

