####Description

Provide an option to the user for view the attached file in the notes subpanel related to any module.

####Procedure:

1.	Go to the module->Notes->metadata->subpanels->default.php
2.	Add the following code into the default.php  <br />
    under the 'list_fields'  array add the following array field.
    
    **_Code:_**
	
```

    'eontek_new_field'=> array(
                               'vname' => 'LBL_EONTEK_VIEW_FIELD',
                               'widget_class' => 'SubPanelEontekViewField',
                               'width' => '10%',
                               'custom_link_only' => true,
                               'displayHeaderCell' => false,
                               ),
                               
                              
```

<br />3.   Create a New file into 
<br />     Inculde/generic/SugarWidgets/SugarWidgetSubPanelEontekViewField.php

     STEP 1:Put a JavaScript for open the popup window
     
   **_Code:_**
	
```     
                                   <script type="text/javascript">
                                   var newWindow;
                                   function popwindow(url) {
                                   if (parseInt(navigator.appVersion)>3) 
                                   {
   	                               if (navigator.appName=="Netscape") 
                                   {
   		                             winW = window.innerWidth;
   		                             winH = window.innerHeight;
   	                               }
   	                               if (navigator.appName.indexOf("Microsoft")!=-1)
                                   {
   		                             winW = document.body.offsetWidth;
   		                             winH = document.body.offsetHeight;
   	                               }
                                   }
                                   var scrollbars = ",scrollbars=0,";
                                   if(winW<(winWidth+5) || winH<(winHeight+5))
                                   {
                          	       scrollbars = ",scrollbars=1,";
   	                               winWidth = 400;
   	                               winHeight = 300;
                                   }
                                   var data = 'height='+winHeight+',width='+winWidth+scrollbars+'location=0,status=0,directories=0,toolbar=0,menubar=0,resizable=1';
                                   newWindow=window.open(url,'name',data);
                                   if (window.focus) {newWindow.focus()}
                                   }

                                   function MM_openBrWindow(theURL,winName,features)
                                   {
                                   window.open(theURL,winName,features);
                                                                                                                                             }

                                              </script>
                                              
                                              
``` 

     STEP 2: Put the following code into the new file
     
**_Code:_**
	
```     
     
                   <?php
                   if(!defined('sugarEntry') || !sugarEntry) die('Not A Valid Entry Point');

                   require_once('include/generic/SugarWidgets/SugarWidgetField.php');
                   //TODO Rename this to edit link
                   class SugarWidgetSubPanelEontekViewField extends SugarWidgetField
                   {
                   function displayHeaderCell(&$layout_def)
                   {
   	               return '&nbsp;';
                   }

                   function displayList(&$layout_def)
                   {
                   return '<a onclick="MM_openBrWindow(\'index.php?entryPoint=viewdoc&id='.$layout_def['fields']['ID'].'&type=Note\',\'\',\'toolbar=no,location=no,status=no,menubar=yes,scrollbars=yes,resizable=yes,width=800,height=400,top=200,left=400\');return false;"><img id="'.$layout_def['fields']['ID'].'" src="custom/themes/default/images/open_inline.gif"></a>';//.print_r($layout_def).'<br>'.print_r($res);
                   }
   	 
                   }

                   ?>

```  

<br />4.  Now open the file custom=>modules=>Documents=>viewDocument.php
<br />Now add this code into the file where 

**_Code:_**
	
```    

                   if($_REQUEST['type']=='Note')
                   {
                   $query = "SELECT  filename FROM notes where id =   '".$_REQUEST['id']."'";         
                   $res[] = '';
   		             $rs = $GLOBALS['db']->query($query);   		 
   		             $row = $GLOBALS['db']->fetchByAssoc($rs);
   		             $name = $row['filename'];
                   $namelen=strlen($name);
                   $extstr=strpos($name,’.’);
                   $ext=substr($name,$extstr+1,$namelen-$extstr);
                   }
                   Now Under the IF ELSE condition into the file code add this condition with in if else or                    
                   create a new condition with this code
                   else if($ext=='jpeg' || $ext=='jpg' || $ext=='gif' || $ext=='png')
             	     {
   			           echo "<img src='".$GLOBALS['sugar_config']['upload_dir'].$_GET['id']."' />";
			             }

```


               
