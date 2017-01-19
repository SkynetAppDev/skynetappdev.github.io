####Description
To analyse and propose development of a Wordpress plugin for SugarCRM

####Composition of a Plugin:

The following files in a folder comprise a Wordpress plugin

1. Main PHP file - which handles the core functionality.<br />
2. Helper files - could be any files which help(PHP, images etc..)<br />
3. Read Me file - to give a description and notes about the plugin.<br />
4. CSS file - handles any CSS for the plugin.<br />
5. Javascript file - handles any Javascript for the plugin.<br />

####Plugin Files:

For our plugin the following are the files

1. sugar_wordpress.php(Main file)
2. functions.php(Helper classes)
<br />  ● HTML_Generator(To generate HTML elements)<br />
        ● SW_Plugin_Admin(To control the admin controls).<br />
3. readme.txt(description)
4. sugar_wordpress.css(CSS file)
5. sugar_wordpress.js(Javascript file)

####Approach:

1. We are going to use the method used in Web-to-Lead forms.<br />
2. A HTTP request is used to submit the form contents to an entry point.<br />
3. The entry point is a PHP file which handles the arguments passed and creates new
Leads in Sugar and returns the result.<br />
4. Based on the HTTP response received, appropriate message is displayed to the user.<br />

####References:

1. http://codex.wordpress.org/Writing_a_Plugin
2. http://codex.wordpress.org/Plugin_API
3. http://planetozh.com/blog/2009/08/how-to-make-http-requests-with-wordpress/
4. http://codex.wordpress.org/HTTP_API
5. http://www.sugarcrm.com/wiki/index.php?title=Creating_a_lead_capture_form_for_your_website






   





