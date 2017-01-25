####Description

Below is the Step wise Process Flow of Fetch Email Functionality:

####Step 1:
Fetch emails supports three mail-servers
*	Gmail
*	Yahoo
*	Outlook

####Step 2:

In order to Fetch emails from his mail account ,User have to add his **mail-account** to **external-account** to module.<br />
The required options in **external-account** were
*	Username
*	Password
*	Mailserver Name

####Step 3:

Once **external-account** saved  need to call (run) **WS** named **fetch_emails**. 

####Step 4:

The **fetch_emails WS** functionality as follows.
* Get  emails(latest 14 days) from mail-server inbox and save the email in **mng_emails** module.
*	For each email one event created.
*	And while creating event from email the following process will be done
*	**From Address Looping** <br />
        1. From address email is meeting owner.<br />
        2. If From addresses email is existing user ,All TO and CC Address email accounts are come under member-accounts of Fromaddress (Meeting-owner) Account.<br />
        3. If From addresses email is non-existing user and create new user ,All TO and CC Address email accounts are come under member-accounts of Fromaddress (Meeting-owner) Account.<br />
* **TO Address Looping**<br /> 
        1. All TO-address email is meeting external invitees.<br />
        2. If TO address email is existing user ,ALL TO Address email accounts are come under member-accounts of Fromaddress (Meeting-owner) Account.<br />
        3. If TO addresses email is non-existing user and create new user ,All TO Address email accounts are come under member-accounts of Fromaddress (Meeting-owner) Account.<br />
* **CC Address Looping** <br />
        1. All CC addresses email is meeting external invitees.<br />
        2. If CC addresses email is existing user ,ALL CC Address email accounts are come under member-accounts of Fromaddress (Meeting-owner) Account.<br />
        3. If CC addresses email is non-existing user and create new user ,All CC Address email accounts are come under member-accounts of Fromaddress (Meeting-owner) Account.<br />

####Step 5:
Once fetched email completed from next-time onwards if any new email came mail server inbox ,that mail automatically fetched from mail server and create event (from ,to and cc addresses looping will be done.

####Step 6:
While fetch emails and saving meeting we are not saving email body ,if user want to see email body , need to call **fetch_email_body WS**, this will return email body (in html format).



