####1. Introduction

The purpose of this document is to provide the overview design of the mobile framework. It describes the functional flow for getting data from IndusMD EMR using web services, performing transformations upon data using XSLT and finally presenting it in the web page.

####1.1 Purpose:
The purpose of the mobile framework is to present the web view of the portal, same as in the mobile phones like iPhone.

####2. Software used – Version

####2.1 OS & Version used: 
*	Windows 7
*	PHP – 5.3
*	XSLT – 2.0
*	Webservices (Protocol - SOAP)
*	XML – 1.0 

####2.2 Tools & Version used:
*	Notepad++: 5.9.6.2
*	Altova XML Spy

####3. Main Design features:

####3.1 Implementation of login functionality
* User has to provide the username and password which are registered in the IndusMD EMR.
* These user details are checked in the EMR through web service calls and get the session id if user is authenticated.

![3 1](https://cloud.githubusercontent.com/assets/17013436/22254076/a19f0afc-e279-11e6-9109-69a9aeece6e5.PNG)

####3.2 Retrieving patient records 
*	After successful login, a web service call will be done for getting all the patient records related to the user. (Here the user can be Doctor, Front Desk person, Front Desk Emergency, Trephination).
*	The response of web service xml will be converted into a response array.
*	This array can be transformed into xml file again which is defined in the Framework format.
*	Upon this xml file style sheet can be applied. This transformation is called XSLT. 
*	Now the list of patients will be presented in the webpage.

![3 2](https://cloud.githubusercontent.com/assets/17013436/22254151/cd9cabe6-e279-11e6-953f-8d9067139459.PNG)

####3.3 Internal functioning of the framework
*	The framework is built on the MVC design pattern. 
*	The HTTP request initiates the Master controller.
*	In Master Controller, setup function will set the module and load properties from the request.
*	In the Module Controller, view will be selected from the properties object.
*	In the Module Controller, module processor lib will be initiated.
*	Module processor lib contain all RPC calls. 
*	For getting the list view of the module getEntryList function of Module Processor Lib will be called.
*	This web service call will be responded with the response xml data. This xml data will be converted in to an Array.
*	The response array will be transformed to an UI XML, with the framework defined tags.
*	This xml will be transformed to centre.xml file using the XSL style sheet, which is specific to each module.
*	Similarly XSL style sheet will be applied to all of the xml files which are specific to each module, to generate master.xml file.
*	Here the translator is used to generate the XML or HTML output using XSL style sheet.
*	 Finally the XSL translation will be applied on the master XML file to generate the final HTML page.

####4. Sequence Diagram:

![3 3](https://cloud.githubusercontent.com/assets/17013436/22254246/04dc4026-e27a-11e6-86c6-1f89718abbed.PNG)

####5. Data Base Design: N/A

####6. Files (Code Snippets):

####6.1 Master Controller:

The HTTP request reaches to the master controller. This controller contains setup function, in this setup it will initiate the module controller, its properties and the view to load.

**_Code:_**
	
```

     public function setup()
     {
		 if (empty($module) && !empty($_REQUEST['module']))
		 $module = $_REQUEST ['module'];
			 
		 //set the module name	if(!empty($module))	$this->setModule($module);
				
		 //set properties on the controller from the $_REQUEST $this->loadPropertiesFromRequest();
		 }
    /**
    * Set properties on the Controller from the $_REQUEST
    *
    */
	  private function loadPropertiesFromRequest()
    {
			if(!empty($_REQUEST['action']))
				$this->action = $_REQUEST['action'];
			if(!empty($_REQUEST['rowid']))
				$this->rowid = $_REQUEST['rowid'];
			if(!empty($_REQUEST['return_id']))
				$this->return_id = $_REQUEST['return_id'];
		}

    /**
    * This function will navigates the control to the requested module and action
    *
    */
    public function execute()
    { 
    try{
	  if(file_exists('modules/'.$this->module.'/'.$this->action.'.php'))
    {
    include('modules/'.$this->module.'/'.$this->action.'.php');
    }
	  else throw new LogWriter('INDUS-002');  
    }
	  catch(LogWriter $logWriter)
    {
	  echo "Page not found";   //Here we need to redirect the page
	  }	     
    }


```

####6.2 Module Controller:     

Module Controller initiates the processor lib. Using this processor lib object it calls the getEntryList method to get the data from the EMR. And apply transformations on it. In the first transformation it gets the UIXML.
<br />Module Controller also initiates the XSLT translator to perform transformations on each xml file. 

**_Code:_**
	
```

    /**
    *  This function first initiates PatientsProcesserLib then generates XML file from the SugarCRM EntryList array. 
    *  This SugarXML file will converst to UI XML.  
    */
    function getUIXML()
    {
		// Initiating patient processer lib
		$patientsProcesserLib  = new PatientsProcesserLib(); 
		// Initiating translator calss
		$xsltTranslator  = new XsltTranslator(); 
		// making a SOAP request
		$xmlData = $patientsProcesserLib->getEntryList();
		try
    {
		   if($xmlData!='')
			 {
			// converting the response to UI-XML
			$xsltTranslator->importStyle('lib/uixls/Patients.xsl');
			$uiXML= $xsltTranslator->applyTransformationOnXmlData($xmlData);
			// converting the UI-XML to final HTML
			$xsltTranslator->importStyle('modules/Patients/PatientsUI.xsl');
			return $xsltTranslator->applyTransformationOnXmlData($uiXML);
			}
			else 
      {
			throw new LogWriter('INDUS-008');
			}
			}
			catch(LogWriter $errorLog)
      {
			echo 'No Data Found';  	   
			}  
			}

```
      
####6.3 Module Processor Lib:    

Module Processor Lib initiates the SOAP client object. With this client object it will sends the web service requests using the function like getEntryList, setEntry, setEntryList etc. and return the response to the Module Controller.
<br />The above functions take params array and call the appropriate function in the EMR.

####Params Array: 

**_Code:_**
	
```

      $params=array(
      'session'=>$_SESSION['sessionId'], 
	    'module_name'=>'mango_Patients', 
	    'query'=>$query, 
	    'order_by'=>'',
	    ‘offset'=>'', 
		  'select_fields'=>array('id','name','patientdob'),
		  'max_results'=>'', 'deleted'=>'0'
      );

```

####6.4 Translator:

Translator will be initiated in the Module Controller. It is used to apply the transformations on the XML file to generate another XML file or the HTML file. For this it takes XSL file as input. XSL file contains the style sheet information to be applied to the XML file.

**_Code:_**
	
```

    $xslt = new xsltProcessor;
    $xslt->importStyleSheet(DomDocument::load('lib/uixls/Patients.xsl'));
    return $xslt->transformToXML(DomDocument::loadXML($xml));

```

####6.5 XML files:


Each module contains list of xml files, In which we used to define the header, footer, left panel, view (List view, Detail view, Edit View) and master XML file.
<br />We used to merge these files to generate the final master xml file by applying transformations and generate the final HTML output. 

####7. High Level Approach of Mobile Framework:

####7.1. Architecture: Data Flow Diagram:

![3 4](https://cloud.githubusercontent.com/assets/17013436/22255528/a37f6fc0-e27d-11e6-89c3-15496ea7edc6.PNG)

####7.2 Functional Flow:

####7.2.1. Login Process Functional Flow:
*	In this framework architecture any can be displayed according to the given URL.
*	By default the login page will be loaded by the master controller. And control reaches to the Login controller.
*	After giving the username and password the login controller initiates the module processor lib and calls the RPC (Web services) for authenticating the user.
*	Here XSL transformations cannot be applied. Just the web service response will be considered.
*	If the user details are correct, then the session id will be retrieved from the web service request.
*	Now the control will be redirected to the home page, here we are having the patients list as the home page.

####7.2.2. Displaying Patients List View:
*	After getting logged in the maser controller redirects the control to the home page as defined in the login controller.
*	In the present case patient list view is defined as the home page. So control reaches to the Patient module controller from the Master controller.
*	Patient module controller initiates the Patient processor lib and XML Translator.
*	The patient processor lib calls the getEntryList function to get the result set of the patient list as web service xml response.
*	Now the XSL transformation will be applied on xml web service response. This is to get the xml file with the tags defined in the web framework.
*	After getting the list view XML file, further transformation will be applied on the module specific XML files (top.xml, bottom.xml, left.xml) to generate the master XML file.
*	Finally XSL transformation will be applied to the master xml file to generate the HTML output.

####8. Assumptions:	
Following are the assumptions for Web Framework:
*	The NuSOAP library (Version 0.6.7) will be used in PHP for the web service calls.
*	PHP minimum version will be 4.5 used.




















