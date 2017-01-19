To setup the SVN development environment on a Windows platform for Apache, PHP and MySQL configuration.

####Requirements: 
1.	Should have installed Tortoise SVN client
2.	Should have a local server environment like WAMP,XAMPP etc.. installed. I have tried on WAMP installation.

####Description:
1.	Right click on desktop and select SVN Checkout
2.	Enter the following URL in the box for ‘URL of Repository’ svn://username@ec2-50-17-250-92.compute-1.amazonaws.com/var/svn/repository/indusmd
a.	Make sure to replace your username in the SVN URL
3.	Make a new folder indusmd in the root directory of the installed local web server. In the text box for ‘Checkout directory’, select the newly created folder. This is where the repository will be installed
4.	It downloads 98.24 MB in around 20 min
5.	Make a new database in your local instance. 
6.	Change the php.ini file to increase the upload file size to 8M
a.	upload_max_filesize = 8M
7.	Import the remote database SQL into your local database
8.	Change the database credentials in config.php to direct to the local database

**_Code:_**

```
'dbconfig' => 
  array (
    'db_host_name' => 'localhost',
    'db_host_instance' => 'SQLEXPRESS',
    'db_user_name' => 'root',
    'db_password' => '',
    'db_name' => 'DB_NAME',
    'db_type' => 'mysql',
  ),
  
 ```
 
9.Access the repository either by <br />
 
 * Browsing to the directory location like in http://localhost/indusmd/trunk<br />
 * Change the document root in httpd.conf to point to the new location like DocumentRoot "c:/wamp/www/indusmd/trunk" (assuming that the local server is installed in C directory). Then the repository can be accessed by pointing the browser to http://localhost<br />

10.	Now you can log into Sugar CRM<br />
11.	When doing a weekly commit, follow these steps<br />

 * right click on the folder indusmd and select SVN update
 * right click again on indusmd and select SVN Commit
 * When asked for auth credentials enter the username and password provided



   
 
 
 
 
 
 
 
