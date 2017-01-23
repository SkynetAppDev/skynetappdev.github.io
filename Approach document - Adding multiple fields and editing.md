####Description:
To know how to implement multiple text field functionality in Sugar CRM.
####Step 1:
 Create a custom field using studio with the data type text field. In this case i have created a text field named ‘multi’ in custom module multifields.

####Step 2:
 Create a file Save.php in modules/<module name>/ directory. 
 
**_Code:_**

```
<?php 
           if(!defined('sugarEntry') || !sugarEntry) die('Not A Valid Entry Point');

           require_once('modules/<module name>/<module name>FormBase.php');

           $multiForm = new <module name>FormBase();
           $prefix = empty($_REQUEST['dup_checked']) ? '' : '<module name>';
           $multiForm>handleSave($prefix, true, false);
     ?>

```

Here we are calling handleSave function to customize the saving functionality.

####Step 3:
Now we have to create a file named  <module name>FormBase.php

**_Code:_**

```
<?php 

class phani_multifieldsFormBase {

function handleSave($prefix, $redirect=true, $useRequired=false){
    
    global $theme, $current_user;
    
    require_once('include/formbase.php');
    
    global $timedate;
    
    $focus = new phani_multifields();
    
	$con='';
    
    // Here we are generating a ',' separated string with all the muilti fields
	if(isset($_POST[multi])){
   	   for($i=0;$i<count($_POST[multi]);$i++)
         	if($_POST[multi][$i]!=''&&$con=='')
   		 	$con=$_POST[multi][$i];
   	  	else if($_POST[multi][$i]!='')     
   		 	$con=$con.','.$_POST[multi][$i];
   		if($con!='')    
   		  $focus->multi=$con;
   	 }
     	 
      // Needs to get remaining fields data   
     $focus->name=$_POST[name];    
     $focus->description=$_POST[description];
     $focus->assigned_user_name=$_POST[assigned_user_name];
     $focus->assigned_user_id=$_POST[assigned_user_id];
     $focus->id=$_POST[record];
    
    if (isset($GLOBALS['check_notify'])) {
   	 $check_notify = $GLOBALS['check_notify'];
    }
    else {
   	 $check_notify = FALSE;
    }    
    
    $focus->save($check_notify);
    $return_id = $focus->id;    
    if(!$focus->ACLAccess('Save')){
   		 ACLController::displayNoAccess(true);
   		 sugar_cleanup(true);
    }
    if($redirect){
   	 $this->handleRedirect($return_id);
    }else{
   	 return $focus;
    }    
}

function handleRedirect($return_id){
    if(isset($_POST['return_module']) && $_POST['return_module'] != "") {
   	 $return_module = $_POST['return_module'];
    }
    else {
   	 $return_module = "phani_multifields";
    }

    if(isset($_POST['return_action']) && $_POST['return_action'] != "") {
   	 if($_REQUEST['return_module'] == 'Emails') {
   		 $return_action = $_REQUEST['return_action'];
   	 }
   	 // if we create a new record "Save", we want to redirect to the DetailView
   	 elseif($_REQUEST['action'] == "Save" && $_REQUEST['return_module'] != "Home") {
   		 $return_action = 'DetailView';
   	 } else {
   		 // if we "Cancel", we go back to the list view.
   		 $return_action = $_REQUEST['return_action'];
   	 }
    }
    else {
   	 $return_action = "DetailView";
    }

    if(isset($_POST['return_id']) && $_POST['return_id'] != "") {
    	$return_id = $_POST['return_id'];
    }

header("Location: index.php?action=$return_action&module=$return_module&record=$return_id");
 }

}

?>

```

####Note:
* handleSave function code varies according to the fields we have in the module. 
* In the above code phani_multifields need to replace with the module name

####Step 4:
From this point we have to do customisations in the custom directory. Place below code at the custom field we have created in the first step in the below mentioned file
custom/modules/<module name>/metadata/editviewdefs.php

**_Code:_**

```
'customCode' => '<input type=\'button\' id=\'addbutton\' value=\'+\' onclick=\'showfield();\'>
                             <table width=\'100%\' border=\'0\' cellspacing=\'0\' cellpadding=\'0\' 
                             id=\'productLine1\'> </table>',
                             
```

####Step 5:
Now past the below javascript function showfield code in the same file outside the php tags.

**_Code:_**

```
<script type="application/javascript">

// This function adds the text field with remove button dyanmically

function showfield()
	{
    	var btn=document.getElementById('addbutton');
    	var x=document.getElementById('productLine1').insertRow(-1);
    	var dd=x.insertCell(0);
    	dd.innerHTML='<input type=\'text\' id=\'multi\' name=\'multi[]\'><input type=\'button\' value=\'-\' onclick=\'cancel(this)\'>';
	}

// This function removes the text field dynamically

function cancel(ln){
	var obj = ln.parentNode.parentNode.rowIndex;
	document.getElementById('productLine1').deleteRow(obj);
	var btn=document.getElementById('addbutton');
	btn.disabled='';
}

// This function will be called on body onload event of edit view page
function addmulti(vardata){
    	fields=vardata.split(','); // Here we are splitting data seperated with comma as delimeter.
   		 for(var i=0;i<fields.length;i++) // This will appends text fields 
   		 {
   			 var xy=document.getElementById('productLine1').insertRow(-1);
   			 var inval=xy.insertCell(0);
   			 inval.innerHTML='<input type=\'text\' id=\'multi[]\' name=\'multi[]\'     value=\''+fields[i] +'\'><input type=\'button\' value=\'-\' onclick=\'cancel(this)\'>';   	 
   		 }
}    
</script>

```
####Note:
After completion of these customisations make sure to delete file editview.tpl in catche/modules/<module name>
This completes the customisation for multiple text fields.




