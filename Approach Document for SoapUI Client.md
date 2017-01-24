####Important Topics are

   *	How to Create New SoapUI Project.<br />
   *	Login function.<br />
   *	How to set_entry and get_entry.<br />
   *	How to Set & Get Relation in SoapUI.<br />
   *	Logout function.<br /> 

####Creating New SoapUI Project:

1.	Download the SoapUI Version and Install.
2.	Create new project by giving the project name and giving the url with Extension as wsdl. 

![2 1](https://cloud.githubusercontent.com/assets/17013436/22242119/3093614a-e248-11e6-8ea1-fd0c49677edb.PNG)

<br />3. Click on Ok

####Login Function.
●	give the username and password<br />
●	Run the service<br />

![2 2](https://cloud.githubusercontent.com/assets/17013436/22242275/b7fe446a-e248-11e6-90c7-cad93d348f21.PNG)

<br />3. If the username and password is correct it will give NO Error. Else Invalid Login. 

![2 3](https://cloud.githubusercontent.com/assets/17013436/22242341/f7ee0cc2-e248-11e6-992a-da3ac6669c17.PNG)

Set Entry:<br />
*	After login we will get sessionId, with the help of that we will set the Record.<br />
*	Giving the sessionId and Module name we can set the data.<br />
*	If the SessionId and Module name is correct it will generate NoError.<br />

![2 4](https://cloud.githubusercontent.com/assets/17013436/22242411/553f3ee6-e249-11e6-8647-ea79b87299f8.PNG)

![2 5](https://cloud.githubusercontent.com/assets/17013436/22242446/6d4d9956-e249-11e6-801a-5ce197ead2bd.PNG)

Set Relation:<br />
*	Giving the SessionId and two  Module names(ex mango_Patients & Notes)With their Respective Row Id’s<br />
*	If the Session ID and Module name exists it will generate NoError.<br />


![2 6](https://cloud.githubusercontent.com/assets/17013436/22242524/a97ffe1e-e249-11e6-9878-e573825256fc.PNG)

Get Relation:<br />
*	Giving the SessionId and two  Module names(ex mango_Patients & Notes)With their Respective Row Id’s.<br />
*	If the Session ID and Module name exists it will generate NoError.<br />

![2 7](https://cloud.githubusercontent.com/assets/17013436/22242638/1a9e175c-e24a-11e6-9a11-914978ea7c50.PNG)

LogOut:<br />
*	Giving the SessionId we can logout.<br />

![2 8](https://cloud.githubusercontent.com/assets/17013436/22242680/48f75be0-e24a-11e6-84e3-d31f32be21b5.PNG)



