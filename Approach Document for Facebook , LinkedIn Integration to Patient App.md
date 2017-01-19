####Description:
Facebook,LinkedIn Integration To Patient App
####Steps for creating meetings:
####Step 1:
User Visits the IPhone Patient App

1.	User enters Login ID and Password.<br />
2.	Clicks on Login.<br />

####Step 2:
1.	User click on Communication icon on the Dashboard screen.<br />
2.	User then clicks on Meetings icon on Communication screen.<br />
3.	User is now in Meeting List View.<br />

####Step 3:
1.	User clicks on Add New button on Meetings list view screen.<br />
2.	User is now redirected to the new Meeting detail view screen.<br />

####Step 4:
The Meetings Detail view is divided into Three screens.

**_Screen 1_**:

1.	General Meeting fields (This will capture  all the information of meeting to be scheduled ).<br />
2.	User clicks on Next button.<br />

**_Screen 2_**:

1.	 User see the  Invites  Screen (This will include contacts selection from Iphone ,Facebook,LinkedIn & EMR).<br />
2.	 User clicks on Post button.<br />

**_Screen 3_**:

Now user see the check boxes option for posting data.

1.   Checkbox-Facebook<br />
2.   Checkbox-EMR(This will always checked).User can not edit this<br />
3.   Checkbox-LinkedIn<br />

####Step 5:

User fills all the necessary information and clicks on Post Button.

1.	The data and contact information of invitee module saved into EMR.<br />
2.	The data is then posted into corresponding Social Network Selected by the User.<br />
3.	Eg: If user select Face book checkbox then data posted on user facebook wall.<br />

####Steps for retrieving meetings:

####Step 1:
User clicks on Meetings icon on Communication screen.

####Step 2:
User can see all the meetings of EMR.

####Step 3:
1.	 User clicks any meeting from Meetings list.<br />
2.	 User can now see the meetings detail view, each meeting will include details like invite details & invitees count etc.<br />

####Step 4:
If user invites other contacts the invite button will be active in meetings detail view.

####Step 5:
In meeting detail view, below we will show list of contacts with attending contacts who have accepted. There will be a tick mark to show that person is accepted.

####Steps for handling User Creation in EMR for External Invitees:

####Step 1:
After a User adds the Invitees through IPhone App.
1.	The Invitees gets saved in the Invitees sub panel of particular Meeting.

####Step 2:
Whenever a new entry is made in Invitees Module. An internal process runs within EMR which as follows:

1.	An Entry is will be made to Users Module, which means a user is created with the details 
	Present in Invitees record.<br />
2.  Our Users module will have two more fields to capture LinkedIn Id and Facebook ID.<br />

####Step 3:
The creation of User will be pass through a set of validations.

1.	Check Unique Email in Users Module if email present in record. (OR).<br />
2.	Check Unique Phone Number if phone number present in record.(OR).<br />
3.	Check Unique LN Id if LinkedIn id present in the record.(OR).<br />
4.	Check Unique FB Id if Facebook ID present in record.(OR).<br />

IF none of these conditions matches a new entry is made to Users. 

####Step 4:
If all the above conditions of Step 3 fail, the user will be treated as a new User and his record will be created with following set of Credentials.

1.	If Invitees record have Emails, then Username will be his Email itself.<br />
2.	if Invitees record have don’t have emails, the Username will be his First name + (some appending text).<br />
3.	In case of Passwords all will have passwords as <First Name>123.<br />

####Step 5:
When a new entry is made into Users again a internal process of EMR executes and makes an entry into Master Instance.












         
 
 

 
            




