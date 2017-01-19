####Description:
How to Integrate LinkedIn Functionality in Lytepole.
####There are two parts to integrate LinkedIn in our App.
####1.	Generate API key and secret key from LinkedIn Developer site.
####Step 1: 
We need to generate one secret key and one API key for our app to use LinkedIn Libraries and integrate LinkedIn.
####Step 2:
generate API and secret keys, goto the web page, Generate keys of LinkedIn 
####Step 3:
Login here with your credentials.
####Step 4:
Click on add new application, It will open a page like, Adding new application.
####Step 5:
Enter all details of company, names etc.
####Step 6:
Agree the form to submit and it will generate your keys and gives a message like ‘Your application was successfully created’ and gives all keys like following.
####Application Details

**_Company_**:
SkyNet Research and Development PVT Ltd.

**_Application Name_**:
 Lytepole

**_API Key_**:
 78jkhika60207n

**_Secret Key_**:
 TA6fkc7kCCNPNakU

**_OAuth User Token_**:
2a261291-8b1b-4624-977a-93b33383c2c9

**_OAuth User Secret_**:
b473fb71-1462-436c-a1e4-6e9d919da6ce

Now we have secret and api keys for our application, so we can proceed  to integrate the LinkedIn api in our app.
####2. Integrate LinkedIn API in our app with the above generated keys:
####Step 1: 
To integrate linkedIn in any IOS app we need to import one linkedIn library in our app.It includes everything like, categories, crypto, Json, Login view and OAuth. All these are having required files and integrations to use linkedIn api.
####Step 2: 
Take above generated both api and secret keys and integrate in api. Open OAuthLoginView.m class in api and add as following code.

**_Code:_**
	
```
- (void)initLinkedInApi
{
    apikey = @"78jkhika60207n";
    secretkey = @"TA6fkc7kCCNPNakU";
    
    self.consumer = [[OAConsumer alloc] initWithKey:apikey
                                             secret:secretkey
                                              realm:@"http://api.linkedin.com/"];
    //?scope=r_basicprofile+r_emailaddress
    //?scope=r_fullprofile%2Brw_nus%2Br_network
    requestTokenURLString = @"https://api.linkedin.com/uas/oauth/requestToken";
    accessTokenURLString = @"https://api.linkedin.com/uas/oauth/accessToken";
    userLoginURLString = @"https://www.linkedin.com/uas/oauth/authorize";
    linkedInCallbackURL = @"hdlinked://linkedin/oauth";
    
    requestTokenURL = [[NSURL URLWithString:requestTokenURLString] retain];
    accessTokenURL = [[NSURL URLWithString:accessTokenURLString] retain];
    userLoginURL = [[NSURL URLWithString:userLoginURLString] retain];
}

```
####Step 3:
In our app following LinkedIn functionalities are included.
* Login to LinkedIn.<br />
* Post job to LinkedIn wall.<br />
* Post job to LinkedIn user groups.<br />

####Step 4:
App Flow to Post Job to LinkedIn Wall/Groups:
* If we are already logged in mobile app of LinkedIn in our mobiles also, we need to login via api in our app to post jobs/anything else.<br />
* If we create a local object we need to login every time to LinkedIn to post job to wall/Post job in group.<br />
* So we are creating a global variable for api login, to take its session until we close our app(we close the process of app).<br />
* So, we are declaring its variable OAuthLoginView in App delegate’s file.<br />
* In Job creation there is a option called ‘LinkedIn’ like in adding skills, location etc.<br />
* By clicking on that ‘LinkedIn’ we are navigating one page where we can able to select options of LinkedIn Posts like ‘Post on wall’, ‘Post in a group’ etc.<br />
* First if we click on ‘LinkedIn’ it will navigates to one page where we can able to see one ‘Login LinkedIn’ with a switch.<br />
* On selecting that switch we will be navigate to LinkedIn Login web page.<br />
* On successful login it will give us options of all the groups including ‘Post to wall’ like,<br />
..* 













