####Below is the Step wise Process Flow of New Instance Creation:

####Step 1:

User Visits www.indusmd.com.<br />
* User Clicks on Sign Up Button.<br />
*	User redirected to Sign Up form.<br />

####Step 2:

User fills the required information regarding the Personal information and Facility Information.
Fields:
*	First Name.
*	Last Name.
*	Email
*	Phone
*	Facility Name
*	Subdomain: http://indusmdemr.com/<facility_name>

####Step 3:

Once the User completes the Sign Up process , the data of particular user get saved into the  www.indusmd.com/sales  (Leads Module).
Necessary fields for saving User data:
*	Name
*	Website.(The User instance URL coming from Subdomain field).

####Step 4:

After the data of user gets saved in the www.indusmd.com/sales using Web Services, Process manager is triggered and an Email is sent to the IndusMD admin about a new user login request.
*	The Email to Admin will have the Link of particular user record .
*	Clickingthe link, Admin can directly access the User Information.

####Step 4.1:

The data of user gets saved in the www.indusmd.com/sales using Web Services, P
The following process  runs after  this :<br />
1.	A web service call is made and the  data   gets  saved in   Master  Instance.<br />
2.	A new account record is created with following fields detail.
      
Fields:
* Account Name (Facility name).
*	 Website (Clients Instance URL).
*	 Facility  ID.(eg Faciltyname_2012).

<br />3. A new record with Admin username  should be created in Contacts with relation to Accounts.

####Step 5:

Admin visits the particular user record and creates login credentials for the requested user.<br />
1.	A new instance is created by our Manual Process of Instance creation.

####Step 5.1:

Once we get the Accounts record created in Master it calls the following Process.
*	Copying an existing stable directory to a new directory(ie. Subdomain Name).
*	For eg : It will be copied to var/www/emr/<subdmain_name>.
*	Here we will be having the full copy of the instance.
*	Creating the database with name as (eg. subdomain_name_db);
*	Importing the tables through sql file to the following database.
*	This sql file will be a fresh one and will be in server itself.
*	Rewriting the config file of created instance.
*	Once the directory is created we can get the new dir path and the config too.
*	Writing Necessary data to config.

####Step 6:

Meanwhile after creation of Accounts record Process Manager  would run and send an email to User with  login credentials and URL.

####Step 6.1:

Once the Instance for requested user is created, IndusMD Admin performs following process:
*	An entry of the particular User data is made in the Master Database of IndusMD.
*	An Email is sent to the requested user along with the instance link and Login Credentials.

####Step 7:

User receives their Instance link and Login credentials and can access their IndusMD instance.

####Step 8:

The Instance received by the User will be a 30 day trial account.
*	There will be a series of Email triggered to the user within the 30 day period on different interval of time. 
*	The Email will intimate the User about the Link expiry date of their Instance.

####Step 9:

a). If User responds for confirmation:
*	If User Confirms for Continuing the Instance, the instance remains activated.

	b).If no response:
*	If User do not responds to the Email, the instance will be deactivated.
*	Deactivating the instance will only change the access or redirecting the active link to some other custom link.
*	The User related data and information will not be affected.



