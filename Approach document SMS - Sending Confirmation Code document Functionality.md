####Description

This document will explain the process of Sending Confirmation Code (SMS) Functionally

####Step 1:(Prerequisites)

●	First we need to include the following SMS Library files.

          ○	require_once("MangoLib/smsLib/NexmoResponseArray.php");
          ○	require_once("MangoLib/smsLib/NexmoMessage.php");
          ○	require_once("MangoLib/smsLib/MvaayooMessage.php");

●	Second we need to declare SMS Gateway Providers credentials in sugar config.php file. Like the following.

**_Code:_**
	
```

                        'smsGateway' => 
                        array (
                        'Nexmo' => 
                        array (
                        'ApiKey' => 'e3194c05',
                        'ApiSecret' => 'b6473c3d',
                        //'FromUS' => '19705500049',
                        'FromUS' => '12184141097',
                        ),
                        'Mvaayoo' => 
                        array (
                        'ApiKey' => 'withcheer.venky@gmail.com',
                        'ApiSecret' => '123456',
                        'FromId' => 'TEST SMS',
                        ),
                        )

```

●	Third we need to save confirmation code message in sugar config.php file. Like the following.

**_Code:_**
	
```

                        'text_msg' => 
                        array (		  
                        'conf_code_msg' => 'Login code: $conf_code - sent from LytePole iPhone app',  		  
                        ),
                        )
                        
```

####Step 2:(Implementation)

●	We are sending SMS confirmation code to user when two actions occurred in mng_userd_devices module, the two actions are as follows.

          ○	When new record inserted into mng_user_devices module.
          ○	When we set reset_flag to one.
          
●	When the above two actions occurs we are triggering logic hooks file in mng_userd_devices module.

          ○	The logic hooks file location was MangoLib/logichooks/HandleUserDeviceSave.php
          
####Step 3:(Sending SMS)  

● For sending SMS to user’s phone, we are two SMS Gateways based on the user's country code
          
          ○	Mvaayoo (For only India Numbers).
          ○	Nexmo (For Countries Other than India).

####Mvaayoo SMS Gateway

●	If users country code was 91(India), we are invoking Mvaayoo API to send SMS to India phone number. and the code as follows

**_Code:_**
	
```

                     $smsObject = new 
                     MvaayooMessage($GLOBALS['sugar_config']['smsGateway']['Mvaayoo']['ApiKey'],$GLOBALS['sugar_config']['smsGateway']['Mvaayoo']['ApiSecret']); 
                     $smsTo = '+'.$bean->country_code.$user_phonenumber;
                     $info = $smsObject-
                     ->sendText($smsTo,$GLOBALS['sugar_config']['smsGateway']['Mvaayoo']['FromId'], $message );
                     
```

####Nexmo SMS Gateway

●	If users country code was other than 91(India), we are invoking Nexmo API to send SMS outside India. And the code as follows

**_Code:_**
	
```

                     $smsObject = new 
                     NexmoMessage($GLOBALS['sugar_config']['smsGateway']['Nexmo']['ApiKey'],$GLOBALS['sugar_config']['smsGateway']['Nexmo']['ApiSecret']);
                     $smsTo = '+'.$bean->country_code.$user_phonenumber;
                     $info = $smsObject-
                     ->sendText($smsTo,$GLOBALS['sugar_config']['smsGateway']['Nexmo']['FromUS'],$message);
                     
```



