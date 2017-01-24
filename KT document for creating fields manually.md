####Below is the Step wise Process Flow of:

####Steps for creating a custom field manually:
*	To create a custom field manually, its definition has to be added in vardefs.php file.
*	Go to <root>/modules/meetings/vardefs.php file to add an array of elements containing definition to your custom field.
*	In the list of arrays of vardefs.php file where each field is defined in each array, we need to add a new array with elements that define our required custom field as follows:
	Below piece of code, creates a custom field called 'userfriendly_meeting_id'
	'userfriendly_meeting_id' =>

**_Code:_**
	
```

      array (
	  'name' => 'userfriendly_meeting_id',
   	  'vname' => 'LBL_FRIENDLY_ID',
	  'type' => 'varchar',
  	  'len' => '10',
    ),

```

*	The above code creates a custom field userfriendly_meeting_id which is seen in the database after doing a repair and rebuild in repair option of Admin section.

####Steps for creating a label name for a custom field manually:
*	Whenever we display this custom field (userfriendly_meeting_id in this case) , it should be visible with a label name, this label name can be set at <root>/custom/modules/<your_module>/language/en_us.lang.php
*	Adding an array element under $mod_strings array in en_us.lang.php file will give it a label name.
*	our custom field is userfriendly_meeting_id created in meetings module, so file that needs to be modified is at <root>/custom/modules/<meetings>/language/en_us.lang.php
*	'LBL_FRIENDLY_ID' => 'Friendly Id', is array element that should be added in $mod_strings array in en_us.lang.php file of meetings module.

####Steps for displaying a custom field in detail view:
*	To view a custom field in the detail view of its module, field should be added in a file located at <root>/custom/modules/<your module>/metadata/detailviewdefs.php.
*	Our custom field is added in meetings module, so following is array definition that should be added in detailviewdefs.php file in meetings module after whichever field definition we feel our custom field should be visible

**_Code:_**
	
```

           array(
  		  'name' => 'userfriendly_meeting_id',
  		  'label' => 'LBL_FRIENDLY_ID',   		 
  		  ),	

```

####Steps for displaying a custom field in edit view:
*	To view a custom field in the edit view of its module, field should be added in a file located at <root>/custom/modules/<your module>/metadata/editviewdefs.php.
*	Our custom field is added in meetings module, so following is array definition that should be added in editviewdefs.php file in meetings module after whichever field definition we feel our custom field should be visible.

**_Code:_**
	
```

         array(
  		  'name' => 'userfriendly_meeting_id',
  		  'label' => 'LBL_FRIENDLY_ID',   		 
  		   ),	

```

