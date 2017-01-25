####Description:
Setting processes of custom modules in Process Manager.
####The following are the steps to be followed for creating processes for custom modules in PM:

####Step 1 :
Create a element of the custom module in the process_object array which is located in include/language/en_us.lang.php file.

**_Code:_**

```
$GLOBALS['app_list_strings']['process_object']=array (
                  ‘leads’ => ‘leads’,
	      ‘contacts’ => ‘contacts’,
                  ‘custom_module name’ => ‘label’,
            );

 ```
 
####Step 2:
 Browse to Process Manager module and click on Create Process. The fields available are:
 * Process Name
 * Process Status
 * Process Object -  select the module for which the process is being created.
 * Start Event  - Run the process when a record is created/modified 
 
####Step 3:
 After the Process is created, we have to create Process Stage. We can have multiple Process Stages for a Process.
 
####Step 4:
 For each Process Stage we have to define Process Stage Tasks i.e. send email/call/create task/run custom script.
 
 1.For Sending Emails we have to select one of the Email Templates.<br />
 2.For running a custom script using PM, we have to follow these steps:  
  * Filename and the class name in the file should be same.
  * Class defined in the file should have a constructor .
  * The file should be placed in the customScript folder in modules/PM_ProcessManager. 


