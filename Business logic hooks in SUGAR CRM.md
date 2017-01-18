####There are basically 3 types of hooks in sugarCRM:

1.	Application hooks, e.g. after_ui_frame, after_ui_footer etc<br />
2.	User hooks, e.g. before_login, before_logout, after_login, after_logout etc.<br />
3.	Module hooks, e.g. after_save, before_save, after_retrieve, before_retrieve etc.<br />

####Adding hooks to sugarcrm:

####Step 1:

There is an empty folder named custom in root folder of sugarcrm application. The custom hooks are separate from core sugarcrm business logic.

####Step 2:

Let's say we need to create a business hooks for Accounts module, create a folder called modules in custom folder. Create a folder with module name Accounts in module folder.

####Step 3:

Create a php file called logic_hooks.php in Accounts folder. The code in the file looks as shown below

**_Code:_**
	
```

          < ?php
          if (!defined('sugarEntry') || !sugarEntry) die('Not A Valid Entry Point');
          $hook_array = array();
          $hook_array['after_save'] = array();
          $hook_array['after_save'][] = array(1, 'sav', 'custom/modules/ Accounts/sav.php', 'sav', 'sav');
          ?>
          
```

The $hook_array variable stores the event for which you want to apply a particular hook. Here the event is **after_save**

####The array() declaration above has 5 parameters:

1st parameter is a processing index.<br />
2nd parameter is string to identify the hook.<br />
3rd parameter is a php file where logic is present.<br />
4th parameter is a class name in the php file.<br />
5th parameter is a method name in the class which has the logic.<br />

####Step 4:

Create the file sav.php which has business logic in it as shown below:

**_Code:_**
	
```

          < ?php
          if (!defined('sugarEntry') || !sugarEntry) die('Not A Valid Entry Point'); 
          class sav{
          function sav(&$bean, $event, $arguments){
          //simple alert box pops up for the hook event
          die('<script language="javascript">alert("Account hook by Docfiles")</script>;');
          }
          }
     
```

The class name is sav which has a method sav.

The method signature for business logic is **method_name(&$bean,$event,$arguments)**.

1st parameter is the reference to the $this bean.<br />
2nd parameter is the string for the current event (e.g.: before_save etc.)<br /> 
3rd parameter is the array of arguments for the event.<br />

####Step 5:

Make sure the permissions are changed for logic_hooks.php and the business logic class file so that it is accessed by the web server or else sugarcrm can't read these files.

