####Description

Under contact module need to hide the projects, bugs, campaigns module through the programmatic.

####Procedure:

1. Go to the module->contacts(module name)->metadata<br />
2. Open subpaneldefs.php file.<br />
3. Comment the following code<br />

**_Code:_**
	
```
        campaigns' => array(
   		 'order' => 110,
   		 'module' => 'CampaignLog',
   		 'sort_order' => 'desc',
   		 'sort_by' => 'activity_date',
   		 'get_subpanel_data'=>'campaigns',
   		 'subpanel_name' => 'ForTargets',
   		 'title_key' => 'LBL_CAMPAIGN_LIST_SUBPANEL_TITLE',
   	    ),

       'project' => array(
   		 'order' => 100,
   		 'module' => 'Project',
   		 'sort_order' => 'asc',
   		 'sort_by' => 'name',
   		 'get_subpanel_data' => 'project',
   		 'subpanel_name' => 'default',
   		 'title_key' => 'LBL_PROJECTS_SUBPANEL_TITLE',
   		 'top_buttons' => array(
   			 array('widget_class' => 'SubPanelTopButtonQuickCreate'),
   		  ),   		 
   	       ),

            'bugs' => array(
   		 'order' => 80,
   		 'module' => 'Bugs',
   		 'sort_order' => 'desc',
   		 'sort_by' => 'bug_number',
   		 'subpanel_name' => 'default',
   		 'get_subpanel_data' => 'bugs',
   		 'add_subpanel_data' => 'bug_id',
   		 'title_key' => 'LBL_BUGS_SUBPANEL_TITLE',
   		 'top_buttons' => array(
   			 array('widget_class' => 'SubPanelTopButtonQuickCreate'),
   			 array('widget_class' => 'SubPanelTopSelectButton',        
                                     'mode'=>'MultiSelect')
   		           ),
   	              ),
```

 <br /> 4. Save the file.
