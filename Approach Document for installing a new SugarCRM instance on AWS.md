####Description:
Approach Document for installing a new SugarCRM instance on AWS
####Below is the Step wise Process Flow of :
####Steps for Connecting to AWS:
The following screen is the start up screen for putty where we need to give the host url to connect to:

![sugar](https://cloud.githubusercontent.com/assets/25039079/22282164/c76bde36-e300-11e6-8465-6f15f9028e3c.png)

After entering the url, in the category panel under connection subsection, we need click on SSH option to upload the authentication ppk file as shown in the below screen and click open that opens the putty window.

![sugar 1](https://cloud.githubusercontent.com/assets/25039079/22282247/30b82c28-e301-11e6-997f-99c433597d4d.png)

Below screen is the putty start screen where we need to login by giving the user name which is ‘ubuntu’ and press enter.

![sugar 2](https://cloud.githubusercontent.com/assets/25039079/22282284/71a1c62c-e301-11e6-9f60-027aa35d0e94.png)

####Steps for create new database for the instance:

![sugar 3](https://cloud.githubusercontent.com/assets/25039079/22282353/cab474ee-e301-11e6-930b-2933f06fc0d8.png)

* Create a database using create command “Create database <database name>”. as shown in above.<br />
* Now import the data into database as shown in the below picture.

![sugar 4](https://cloud.githubusercontent.com/assets/25039079/22282410/1c9c6140-e302-11e6-98b2-8f42458bb265.png)

* After importing data is finished, we have a database ready to be used by a sugar instance.

####Steps to move instance code and set it up:

* Using export command you can take an export of  the required instance from SVN to your required directory in the AWS.

             sudo svn export <SVN url> <directory structure>  
             
* After authentication details entered, code is exported from  SVN to your AWS required directory structure.
* Now using FTP open the instance’s config.php file and give the appropriate site_url and db values (db name, pwd) and save this file back on AWS.
* Set the crontab for this instance from root user.
(please see the respective documents for setting up a cron job).
* Test the instance from browser and Soap and then instance is ready to use.



