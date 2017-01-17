Aim
 
This document will explain the process of Configuring Your SMTP Server to Work With Sugar.
  

Setup system email settings
 
Prerequisites You must be an administrator.

Step1: Login to your SugarCRM Admin Panel as Administrator. Go to Admin > Email Settings.

![1](https://cloud.githubusercontent.com/assets/17013436/22036975/6a00e272-dd1b-11e6-8abb-a46562326605.PNG)

Step 2: On the admin page scroll down to the section Email and click on the button Email Settings:

![2](https://cloud.githubusercontent.com/assets/17013436/22037010/a0fcb008-dd1b-11e6-8788-05b7f05748e4.PNG)

Step3: On the page that opens the first section is labeled Outgoing Mail Configuration. In that section there are four buttons which allow you to choose the service that you want to use (Gmail, Yahoo, Microsoft Exchange, Other). The options that are displayed in this section depend on which of the four buttons you click. For example, if you click on Gmail you only have to specify the name of your Gmail email account, its password, and whether you want to allow users to use this account for outgoing mail when sending messages from the SugarCRM application:

![3](https://cloud.githubusercontent.com/assets/17013436/22037050/bf0418fc-dd1b-11e6-8e10-d0002ed324d6.PNG)

We also have to type the name of your organization in the From Name field, and the email address in the From Address field. The Yahoo button displays the same settings.

Now i am using following credentials to setup configuration.
username :donotreply@lytepole.com.
password : lytepole2016@

Step4: By default, the Other button is selected. You can use it to configure the settings for any outgoing email server. For example, you can use the HostKnox server hosting your account. As a matter of fact, you can also use this button to set up the outgoing mail configuration of your Gmail or Yahoo email account. The Other button displays some additional options compared to the Gmail and Yahoo buttons:

![4](https://cloud.githubusercontent.com/assets/17013436/22037078/df7a03ee-dd1b-11e6-8289-9dd5dff43c78.PNG)

Step4: In case you want registered users (including administrators) to use this same email account to send emails through the SugarCRM application, mark the checkbox for Allow users to use this account for outgoing email. If you don't mark this checkbox, the users will still be able to use the same outgoing mail server to send messages, but you have to provide them with their own email credentials.
For example, if you use the abcd server hosting your account , you have to provide your smtp servername , username and password to send email.

Save the settings
 
Step1: After you configure the settings for the outgoing email server ,need to click on the Save button to save the changes.
 
Test the outbound mail
 
Step1:  We can test whether everything is working correctly. Just click on the Send Test Email button. A window will pop out. Type the name of an email address that you want to use to receive the test message and click on Send:

![5](https://cloud.githubusercontent.com/assets/17013436/22037116/024e7396-dd1c-11e6-88c9-5f66ef02239d.PNG)
