####Description

Removing Create/Select buttons from the Sup Panels.

####Step 1:

Copy the default.php file from the modules/<UrModule>/metadata/subpanels and paste it in the respective custom folder (this is for safe upgrade).

####Step 2:

Remove the ‘top_buttons’ array from the file and change the filename from default.php to some other name which is not existing. 

####Step 3:

Move to custom/extension/modules/<parent module>/Ext/Layoutdefs relationship file (parent module refers to the module from which the relation is set).<br />
In this file, remove the ‘top_buttons’ array and change the value of ‘subpanel name’ from default to the name you have given in the step 2.

####Step 4:

Go to the admin section and run Quick Repair and Rebuilt.

**Example**: Removing Create/Select buttons from the Allergy Sup Panels.

#####1. modules/mango_alg/metadata/subpanel/default.php

**_Code:_**
	
```


           $module_name='mango_alg';
           $subpanel_layout = array(
	         'top_buttons' => array(
		       array('widget_class' => 'SubPanelTopCreateButton'),
		       array('widget_class' => 'SubPanelTopSelectButton', 'popup_module' => $module_name),
	         ),

	         'where' => '',

	         'list_fields' => array(
		       'name'=>array(
	 		     'vname' => 'LBL_NAME',
			     'widget_class' => 'SubPanelDetailViewLink',
	 		     'width' => '45%',
		       ),
		       'date_modified'=>array(
	 		     'vname' => 'LBL_DATE_MODIFIED',
	 		     'width' => '45%',
		       ),
		       'edit_button'=>array(
			     'widget_class' => 'SubPanelEditButton',
		 	     'module' => $module_name,
	 		     'width' => '4%',
		       ),
		       'remove_button'=>array(
			     'widget_class' => 'SubPanelRemoveButton',
		 	     'module' => $module_name,
			     'width' => '5%',
		       ),
	         ),
           );
           
```

####2. Custom/modules/mango_alg/metadata/subpanel/ForAllergy.php<br />
Here the default.php is renamed as ForAllergy.php

**_Code:_**
	
```
         
          $module_name='mango_alg';
          $subpanel_layout = array(
	        'top_buttons' => array(
		      ),           ----------> { The two values are removed}

	        'where' => '',

	        'list_fields' => array(
		      'name'=>array(
	 		    'vname' => 'LBL_NAME',
			    'widget_class' => 'SubPanelDetailViewLink',
	 		    'width' => '45%',
		      ),
		      'date_modified'=>array(
	 		    'vname' => 'LBL_DATE_MODIFIED',
	 		    'width' => '45%',
		      ),
		
	        ),
          );
          
 ```
 
####3. Custom/Ext/modules/mango_patients/Ext/Layoutdefs/ relationship file.

**_Code:_**
	
```

          $layout_defs["mango_Patients"]["subpanel_setup"]["mango_patients_mango_alg"] = array (
         'order' => 60,
         'module' => 'mango_alg',
         'subpanel_name' => 'ForAllergy', --------> changed from default
         'sort_order' => 'asc',
         'sort_by' => 'id',
         'title_key' => 'LBL_MANGO_PATIENTS_MANGO_ALG_FROM_MANGO_ALG_TITLE',
         'get_subpanel_data' => 'mango_patients_mango_alg',
         -------------------> Removed the ‘top_button’ array
         );
         
```  

####4. Run Quick Repair and Rebuild.
          
