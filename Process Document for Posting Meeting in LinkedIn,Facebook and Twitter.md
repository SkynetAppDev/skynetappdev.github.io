####The following are the steps:-

####Step 1:

All the Meeting Users data will be first saved in the New Meeting User module. Once the record is created in this module using after save logic hook we will replicate the data in the default Users module.

####Step 2:

The Meeting User module is related to Videos,Images,Dictation module where the User can add his images and videos related to him.

####Step 3:

All the Meeting related users,images,videos,dictation and messages are added under the respective modules which are related with the Meetings module.

####Step 4:

When a Meeting is created, the User selects(checks) the social networking sites in which he want to post the meeting.

####Step 5:

For a meeting to be posted on Social Networking sites, first we have to register our account in their portal in which we have to provide the app details along with the Call back url and will be getting the app key and app secret values by which we can access the respective Social Networking site.

####Step 6:

When the User clicks on Post Meeting, the selected sites to which the meeting to be posted is attached to url and is processed.<br />
E.g. : localhost/entryPoint=PostTo&mode=twitter+facebook+twitter

####Step 7:

The posting of meeting will be processed in the order of mode values which are send in the url through an entry point for post meeting. The mode value in the entrypoint will be updated every time the meeting is posted.

####Step 8:

For the first time login, the user have to sign in to the site by providing their credentials which will be saved in a session and his access token which will be saved in the database, by which he can directly post the meeting to the social networking site without logging in from the next time.

####Step 9:

Once the  posting is done the page is redirected to the final page where it shows in which sites the posting of meeting is successful.
