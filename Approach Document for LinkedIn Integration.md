####Description

How to Integrate LinkedIn Functionality in Lytepolev

####Procedure:

There are two parts to integrate LinkedIn in our app<br />
     1.	Generate api key and secret key from LInkedIn Developer site<br />
     2.	Integrate LinkedIn API in our app with the above generated keys
     
**1. Generate API and Secret Keys from LinkedIn developer site:**

     Step 1: We need to generate one secret key and one api key for our app to use LinkedIn Libraries and integrate LinkedIn.<br />
     Step 2: To generate api and secret keys, goto the web page, Generate keys of LinkedIn<br />
     Step 3: Login here with your credentials.<br />
     Step 4: Click on add new application, It will open a page like, Adding new application<br />
     Step 5: Enter all details of company, names etc.<br />
     Step 6: Agree the form to submit and it will generate your keys and gives a message like ‘Your application was successfully created’ and gives all keys like following.       
                                         
  
####Application Details
**●	Company:<br />**
            SkyNet Research and Development PVT Ltd.<br />
            
**●	Application Name:<br />**
            Lytepole<br />
            
**●	API Key:<br />**
            78jkhika60207n<br />
            
**●	Secret Key:<br />**
             TA6fkc7kCCNPNakU<br />
             
**●	OAuth User Token:<br />**
2a261291-8b1b-4624-977a-93b33383c2c9<br />

**●	OAuth User Secret:<br />**
b473fb71-1462-436c-a1e4-6e9d919da6ce<br />

Now we have secret and API keys for our application, so we can proceed to integrate the LinkedIn API in our app.

**2. Integrate LinkedIn API in our app with the above generated keys:**

    Step 1: To integrate linkedIn in any IOS app we need to import one linkedIn library in our app.It includes everything like,categories,crypto,Json,Login view and OAuth. All these are having required files and integrations to use linkedIn api.
    Step 2: Take above generated both api and secret keys and integrate in api. Open OAuthLoginView.m class in api and add as following code 

    - (void)initLinkedInApi
    {
    apikey = @"78jkhika60207n";
    secretkey = @"TA6fkc7kCCNPNakU";
    self.consumer = [[OAConsumer alloc] initWithKey:apikey secret:secretkey realm:@"http://api.linkedin.com/"];
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
   
    Step 3:
    In our app following LinkedIn functionalities are included .
         ●	Login to LinkedIn
         ●	Post job to LinkedIn wall
         ●	Post job to LinkedIn user groups
    
    Step 4: App Flow to Post Job to LinkedIn Wall/Groups:

         ●	If we are already logged in mobile app of linkedIn in our mobiles also, we need to login via API in our app to post jobs/anything else
         ●	If we create a local object we need to login every time to LinkedIn to post job to wall/Post job in group.
         ●	So we are creating a global variable for API login, to take its session until we close our app (we close the process of app).
         ●	So, we are declaring its variable OAuthLoginView in Appdelegate.h file.
         ●	In Job creation there is an option called ‘LinkedIn’ like in adding skills, location etc.
         ●	By clicking on that ‘LinkedIn’ we are navigating one page where we can able to select options of LinkedIn Posts like ‘Post on wall’, ‘Post in a group’ etc.
         ●	First if we click on ‘LinkedIn’ it will navigates to one page where we can able to see one ‘Login LinkedIn’ with a switch
         ●	On selecting that switch we will be navigate to LinkedIn Login web page
         ●	On successful login it will give us options of all the groups including ‘Post to wall’ like,

                         ○	Post to LinkedIn wall
                         ○	Group1 
                         ○	Group 2
                         ○	Group 3 …. etc.
     
         ●	We can select one /many from the list.
         ●	If we select ‘Post to LinkedIn wall’ and all groups, the job will post on user’s wall as well as on selected groups
         ●	We select options and click on done, it will redirect the page to add job page with selected options
         ●	After entering all the other details of job and click on next, it will show all the selected details in summary page
         ●	When click on save it will show all the options along with LinkedIn
         ●	The job will save to EMR as well as posted on LinkedIn page.


    Step 5: Code Flow of LinkedIn:
            We need following urls to login/to post on wall/to post on groups/to fetch groups,
            
            //To post the job on wall
               linkedInWallPostUrl = @"http://api.linkedin.com/v1/people/~/shares";

            //To Fetch user groups of LinkedIn
               linkedInGroupsUrl = @"https://api.linkedin.com/v1/people/~/group-memberships:(group:(id,name))?count=100&start=0";

            //To post job on groups of LinkedIn
               linkedInGroupsPosrUrl = @"https://api.linkedin.com/v1/groups/@id@/posts";

            //To post the job with any reference image
               linkedInImage = @"https://www.lytepole.com/web/prod/images/linkedinimage.png";

         ●	First to login to linkedIn we are navigating to ‘OAuthLoginView’ controller. It is with in the LinkedIn api. It will redirect to web page to login with our credentials
         ●	If successful login following method will call to pick user groups

           -(void)getLinkedInGroups
           {
           MNGLang *_MNGLang = [MNGLang sharedGlobals];
           NSURL *url = [NSURL URLWithString:_MNGLang.linkedInGroupsUrl];
           OAMutableURLRequest *request =
           [[OAMutableURLRequest alloc] initWithURL:url
                                    consumer:oAuthLoginView.consumer
                                    token:oAuthLoginView.accessToken
                                    callback:nil
                                    signatureProvider:nil];
           [request setValue:@"json" forHTTPHeaderField:@"x-li-format"];
           OADataFetcher *fetcher = [[OADataFetcher alloc] init];
           [fetcher fetchDataWithRequest:request
                                   delegate:self
                                   didFinishSelector:@selector(connectionsGroupsApiCallResult:didFinish:)
                                  didFailSelector:@selector(onnectionsGroupsApiCallResult:didFail:)];
           }

         ● Now we have user groups with us. Show all the groups list with Post on wall option in list view to select where to post the job
         ● If user selects the ‘Post on wall’ and some groups and save button clicked the job will post on Linked in wall as well as in groups. The following is code flow.


          #pragma mark - Posting LinkedIn Wall
          //Method to post on LinkedIn wall
          - (void)buttonPostStatusClick
          {
          NSString *jobSub = [_LYTDiscussionListParameters getSubject];
          NSString *jobDesc = [_LYTDiscussionListParameters getDescription];
          MNGLang *_MNGLang = [MNGLang sharedGlobals];
          NSURL *linkedInImageUrl = [NSURL URLWithString:_MNGLang.linkedInImage];
          NSURL *url = [NSURL URLWithString:_MNGLang.linkedInWallPostUrl];
          OAMutableURLRequest *request = [[OAMutableURLRequest alloc] initWithURL:url consumer:oAuthLoginView.consumer
                                         token:oAuthLoginView.accessToken
                                         callback:nil
                                         signatureProvider:nil];

          //Creating job post format
          NSDictionary *update = [[NSDictionary alloc] initWithObjectsAndKeys:
                                 [[NSDictionary alloc]
                                 initWithObjectsAndKeys:
                                 @"anyone",@"code",nil], @"visibility",
                                 @"Job posted by LytePole App", @"comment",
                                 [[NSDictionary alloc]
                                 initWithObjectsAndKeys:
                                 jobDesc,@"description",
                                 @"https://lytepole.com/",@"submittedUrl",
                                 jobSub,@"title",
                                 @"http://dev.lytepole.com/lytepole/images/linkedinimage.png",@"submittedImageUrl",nil],@"content",
                                 nil];
    
          [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
          NSString *updateString = [update JSONString];
          [request setHTTPBodyWithString:updateString];
          [request setHTTPMethod:@"POST"];
          OADataFetcher *fetcher = [[OADataFetcher alloc] init];
          [fetcher fetchDataWithRequest:request
                                delegate:self
                                didFinishSelector:@selector(postUpdateApiCallResult:didFinish:)
                                didFailSelector:@selector(postUpdateApiCallResult:didFail:)];
          }

          //Delegate of Post on wall did finish
          - (void)postUpdateApiCallResult:(OAServiceTicket *)ticket didFinish:(NSData *)data
          {
          NSString *resStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
          [MNGLog log:@"post Success response" :resStr];
          MNGLang *_MNGLang = [MNGLang sharedGlobals];
         if ([resStr rangeOfString:@"update-key>UPDATE"].location != NSNotFound)
         {
         if (dontShowAlert == NO && [postNameAry containsObject:@"Post to LinkedIn Wall"] && [postNameAry count]==1)
         {
         showWallPostAlert = YES;
         //  [MNGGlobal alertDisplay:_MNGLang.linkedInjobPostSuccess];
         }
         }
    
         if ([resStr rangeOfString:@"Do not post duplicate content"].location != NSNotFound)
        {
        [MNGGlobal alertDisplay:_MNGLang.linkedInjobPostFail];
        }
        [self postToLinkedInGroups:postIdsAry];
        }
       // Delegate of Post on wall did Fail
       - (void)postUpdateApiCallResult:(OAServiceTicket *)ticket didFail:(NSData *)data
       {
       NSString *resStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
       [MNGLog log:@"post Fail response" :resStr];
       }
       #pragma mark - Posting LinkedIn Groups
       //Method to post in Groups
      - (void)postJobOnGroup :(NSString *)groupId
      {
      NSString *jobSub = [_LYTDiscussionListParameters getSubject];
      NSString *jobDesc = [_LYTDiscussionListParameters getDescription];
      //8229548
      MNGLang *_MNGLang = [MNGLang sharedGlobals];
      NSURL *linkedInImageUrl = [NSURL URLWithString:_MNGLang.linkedInImage];
      NSString *groupPostUrl = _MNGLang.linkedInGroupdPosrUrl;
      groupPostUrl = [groupPostUrl stringByReplacingOccurrencesOfString:@"@id@"withString:groupId];
      NSURL *url = [NSURL URLWithString:groupPostUrl];
      OAMutableURLRequest *request = [[OAMutableURLRequest alloc] initWithURL:url
                                                                  consumer:oAuthLoginView.consumer
                                                                  token:oAuthLoginView.accessToken
                                                                  callback:nil
                                                                  signatureProvider:nil];
      //Creating job post format
      NSDictionary *update = [[NSDictionary alloc] initWithObjectsAndKeys:
                            @"Job posted by LytePole App", @"title",
                            @"", @"summary",
                            [[NSDictionary alloc]
                             initWithObjectsAndKeys:
                             jobDesc,@"description",
                             @"https://lytepole.com/",@"submittedUrl",
                             jobSub,@"title",
                             @"http://dev.lytepole.com/lytepole/images/linkedinimage.png",@"submittedImageUrl",nil],@"content",
                            nil];
    
      [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
      NSString *updateString = [update JSONString];
      [request setHTTPBodyWithString:updateString];
      [request setHTTPMethod:@"POST"];
      OADataFetcher *fetcher = [[OADataFetcher alloc] init];
      [fetcher fetchDataWithRequest:request
                                    delegate:self
                                    didFinishSelector:@selector(postToLinkedInGroupsApiResponse:didFinish:)
                                    didFailSelector:@selector(postToLinkedInGroupsApiResponse:didFail:)];
      }

      // Delegate of Post in groups did Finish
      - (void)postToLinkedInGroupsApiResponse:(OAServiceTicket *)ticket didFinish:(NSData *)data
      {
      //NSString *resStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
 
      }
      // Delegate of Post in groups did Fail
      - (void)postToLinkedInGroupsApiResponse:(OAServiceTicket *)ticket didFail:(NSData *)data
      {
      // NSString *resStr = [[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding];
      }


####Conclusion:

The job will post on wall as well as on selected groups. Alerts will show according to app flow like in adding job/editing job.







   
