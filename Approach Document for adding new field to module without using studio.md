####Description
To add new fields to any module without using studio
####Assumption: Assuming XYZ is the module name

####Step 1:
* Open the vardefs.php file of XYZ module
* Navigation: <root>modules/xyz/vardefs.php

####Step 2:

####Assuming new_field is to be added in module

* Append the following array in vardefs.php

**_Code_**:

```
'new_field' => 
  	array (
    	'required' => false, 
    	'name' => 'new_field',
    	'vname' => 'LBL_NEW_FIELD',
    	'type' => 'varchar',
    	'massupdate' => 0,
    	'comments' => '',
    	'help' => '',
    	'importable' => 'true',
    	'duplicate_merge' => 'disabled',
    	'duplicate_merge_dom_value' => '0',
    	'audited' => false,
    	'reportable' => true,
    	'len' => '40',
    	'size' => '20',
  	),
    
 ```
 
####Step 3:
 
* Navigate to <root>/modules/xyz/language/en_us.lang.php<br />
* Append the follwoing to existing array<br />
          'LBL_NEW_FIELD' =>   ' New Field Name' 
          
####Step 4:

* Quick repair and rebuild sugarcrm from the Admin panel.

####Step 5:

* We need to then add the below arrays to file of editviewdefs of particular module.
	Location of file: custom/modules/<module name>/metadata/editviewdefs.php


**_Code:_**
          
```
array (
  0 =>
       	array (
        	'name' => '<field_name>',
        	'studio' => 'visible',
        	'label' => <field_label>',
      	),
 ),

```

####Step 6:

* We also need to add below arrays to the file of detailviewdefs of particular module.
	Location of file :  custom/modules/<module name>/metadata/detailviewdefs.php.
  
**_Code:_**

```
array (
  0 =>
       	array (
        	'name' => '<field_name>',
        	'studio' => 'visible',
        	'label' => '<field_label>,
      	),
 ),

```




