####Description:
Approach Document for installing a new SugarCRM instance on AWS.
####Below is the Step wise Process Flow of :
####Steps for Connecting to AWS:
The following screen is the start up screen for putty where we need to give the host url to connect to:

![g](https://cloud.githubusercontent.com/assets/17013436/22283856/60e1093e-e30a-11e6-991d-a6b783347b6e.PNG)

After entering the url, in the category panel under connection subsection, we need click on SSH option to upload the authentication ppk 
file as shown in the below screen and click open that opens the putty window.

![g2](https://cloud.githubusercontent.com/assets/17013436/22283903/a04a182c-e30a-11e6-8b10-357af299e26e.PNG)

Below screen is the putty start screen where we need to login by giving the user name which is ‘ubuntu’ and press enter.

![g3](https://cloud.githubusercontent.com/assets/17013436/22283981/08eb7f88-e30b-11e6-8d45-cf2e2a75e17d.PNG)

####Steps for create new database for the instance:

![g4](https://cloud.githubusercontent.com/assets/17013436/22284023/45ed7148-e30b-11e6-95f4-01255b26d87b.PNG)

* Create a database using create command “Create database <database name>”. as shown in above.<br />
* Now import the data into database as shown in the below picture.

![g5](https://cloud.githubusercontent.com/assets/17013436/22284057/6f60a7f2-e30b-11e6-8724-21ad2171957e.PNG)

* After importing data is finished, we have a database ready to be used by a sugar instance.

####Steps to move instance code and set it up:

* Using export command you can take an export of  the required instance from SVN to your required directory in the AWS.

             sudo svn export <SVN url> <directory structure>  
             
* After authentication details entered, code is exported from  SVN to your AWS required directory structure.
* Now using FTP open the instance’s config.php file and give the appropriate site_url and db values (db name, pwd) and save this file back on AWS.
* Set the crontab for this instance from root user.
(please see the respective documents for setting up a cron job).
* Test the instance from browser and Soap and then instance is ready to use.



