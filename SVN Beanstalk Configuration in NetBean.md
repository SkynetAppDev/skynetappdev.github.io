####Description

Here we are creating svn project on the local system NetBean for updating and committing the server code, Using NetBean framework.

####Step 1:

If you are using window 7 so it may give error to checkout from the server svn, For fixing this error you have to  turned off indexing on the folder in window 7, for this you have to follow the below process:

	1. Click on “start” and enter “services.msc” into the search field, which will fire up the service list of all Windows 7 services.
	2. Search through the list until you find “Windows Search” (tip: press “W” and it will jump to all services starting with the letter W).
	3. Doube-click on “Windows Search” and from the dropdown field select startup type: “Disabled”.
	4. Stop the service.
<br />
![1](https://cloud.githubusercontent.com/assets/17013436/22118644/a047f9d6-de9e-11e6-8536-47f8a91ce0bb.PNG)

Now after fixing this, go for svn checkout.

####Step 2:

First open NetBean and go for:<br />
          Team->Subversion->checkout
          
####Step 3:    

On the pop window at Repository Url put your Netbean svn project url. and fill the username and password of your account on the server. Don’t go for proxy setting.

![2](https://cloud.githubusercontent.com/assets/17013436/22118998/d6ab305a-de9f-11e6-875b-dacf40b01079.PNG)

After filling all the details click next button.

####Step 4: 

Now on second page select the Repository folder and Repository version and for the location on your local system browse for your local system location.

![3](https://cloud.githubusercontent.com/assets/17013436/22119115/53a58ac4-dea0-11e6-9175-56ed624d0a0f.PNG)

Click finish to complete the svn checkout.

####Step 5:

Now from the netbean create a new php project and add this svn downloaded folder.

####SVN Commit:

Follow this menu navigation to commit the changes made to code on your local server <br />
          Team -> Commit

####Update:

Follow this menu navigation to update your code with the SVN base instance <br />
            Team -> Update
            
####Identification and meaning of icons in SVN

![4](https://cloud.githubusercontent.com/assets/17013436/22119327/29d7f280-dea1-11e6-8a5e-01b7f7ea20b8.PNG)




          
          
