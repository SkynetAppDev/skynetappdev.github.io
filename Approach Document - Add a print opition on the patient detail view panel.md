Add a new print option on the patient module 
####Description:
Provide a option to the user for print the patient complete information.

####Procedure:

####STEP 1: 
Open the file  module->mango_Patients->metadata->detailviewdefs.php Into the field array add this subarray

**_Code:_**

```
array (
      	0 =>
      	array (
        	'name' => 'Paitent Complete Report',
        	'label' => 'PAITENTCOMPLETEREPORT',
     	'customCode' => '<a   onclick="MM_openBrWindow(\'index.php?entryPoint=viewpdfdoc&id={$fields.id.value}&type=KB\',\'\',\'toolbar=no,location=no,status=no,menubar=yes,scrollbars=yes,resizable=yes,width=800,height=400,top=200,left=400\');return false;"><img height="16" border="0" width="16" alt="View" title="View" src="custom/themes/default/images/open_inline.gif" ></a>',
      	          ),
     	 
   		 
    	),

```

Into the same file add the JavaScript for opening the popup windows

**_Code:_**

```
<script type="text/javascript">
var newWindow;
function popwindow(url) {
    if (parseInt(navigator.appVersion)>3) {
   	 if (navigator.appName=="Netscape") {
   		 winW = window.innerWidth;
   		 winH = window.innerHeight;
   	 }
   	 if (navigator.appName.indexOf("Microsoft")!=-1) {
   		 winW = document.body.offsetWidth;
   		 winH = document.body.offsetHeight;
   	 }
    }
    var scrollbars = ",scrollbars=0,";
    if(winW<(winWidth+5) || winH<(winHeight+5)) {
   	 //alert("You will have scrollbars. Your inner height and width are as following: \n"+winW+" by "+winH);
   	 scrollbars = ",scrollbars=1,";
   	 winWidth = 400;
   	 winHeight = 300;
    }
    var data = 'height='+winHeight+',width='+winWidth+scrollbars+'location=0,status=0,directories=0,toolbar=0,menubar=0,resizable=1';
    newWindow=window.open(url,'name',data);
    if (window.focus) {newWindow.focus()}
}

function MM_openBrWindow(theURL,winName,features) { //v2.0
//alert(theURL);
  window.open(theURL,winName,features);
}

</script>

```

####Step 2:

**_Code:_**

```
Open the file  include->MVC->Controller->entry_point_registry.php
              Into the “$entry_point_registry” array add this subarray
              'viewpdfdoc' => array('file' => 'pdfprint.php', 'auth' => true)
              
```

####Step 3:
Download FPDF file from the Link (http://www.fpdf.org/), This file is for generating the pdf file from the php code.

####Step 4:
Extract the downloaded FPDF ZIP file and save all the file and document into the Sugar CRM  root directory.

####Step 5:

Create file pdfprint.php  to generate the pdf file print for the paitent complete information.
In this file I am doing the following operations 
* First get the id from the requested URL
             $id=$_REQUEST['id'];
* Include the following file into this file
                  require("fpdf.php");
              and also add this to into the file
                 global $sugar_config;            

* After that fetch the record from the database using the $id from the tables (mango_paitents, max_page1, max_page2, max_page3, notes, max_Epescreption1, mango_Medication)<br />
* Storing the records into the array.<br />
* Now create the pdf<br />

**_Code:_**

```
                    $pdf = new FPDF();  //create a object of the base class
                   $pdf->AddPage();      //add a new page
                   $pdf->SetFont('Arial','B',16); //set the font for the line
                   $pdf->Cell(0,10,'Paitent Complete Information Report'); //create cell to display the 
                   content
                   $pdf->LN(); //for changing the line
                   $pdf->LN();
                   
```

* Now at last put this code to print the pdf file content

                     $pdf->Output();
