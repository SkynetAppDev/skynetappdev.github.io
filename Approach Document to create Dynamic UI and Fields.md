####Description:
When a user login into iPad using his login credentials, a request (uisng SOAP or HTTP) is sent to web server.Depending upon the user type web server responses with few details mentioned below:

*UI interface(Ex: Tab View, Split View, Modal View...) of the App.<br />
*View(Ex: View, Table View....) of each page.<br />
*Number of Fields in each page/tab.<br />
*Accessibility of each field.<br />
####Approach:
Web server sends the type of UI and the number of items/pages in UI is send through XML. Need to parse the XML response and display UI interface and its related fields.<br />

**_Code:_**
```
<?xml version="1.0" encoding="UTF-8" ?>
<MangoUserDataFile>
    <Device>iPad</Device>
    <Version>3.0</Version>
	<UserName>XYZ</UserName>
	<UserType>Admin</UserType>
    <Module>TabView</Module>
    <tab id="1">
   	 <item>
          	<name>Home</name>
          	<value>WebView</value>
          	</item> 	 
    </tab>
    <tab id="2">
   	 <item>
          	<name>Search</name>
          	<value>view</value>
          	</item>	 
    </tab>
</MangoUserDataFile>

```
In the above XML, the attribute “tab” represents the Tab and “id” represent the order of the tab. “name” is the name of the tab and “value” represents the type of view.<br />
When a particular page/Tab is clicked then a new request is sent to web server and the response will contains the number of fields and its accessibility. 

**_Code:_**
```
<?xml version="1.0" encoding="UTF-8" ?>
<MangoUserDataFile>
    <Device>iPad</Device>
    <Version>3.0</Version>
	<UserName>XYZ</UserName>
	<UserType>Admin</UserType>
    <Module>Page1</Module>
    <property id="textfield">
   	 <item>
          	<name>Field1</name>
          	<value>Admin</value>
          	<length>20</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
     	<item>
          	<name>Field2</name>
          	<value>text2</value>
          	<length>20</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
     	<item>
          	<name>Field3</name>
          	<value>text3</value>
          	<length>20</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
     	<item>
          	<name>Field4</name>
          	<value>text4</value>
          	<length>20</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
     	<item>
          	<name>Field5</name>
          	<value>text5</value>
          	<length>20</length>
          	<editable>False</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
    </property>
    <property id="button">
   	 <item>
          	<name>button1</name>
          	<value>button1</value>
          	<length>20</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
     	<item>
          	<name>button2</name>
          	<value>button2</value>
          	<length>20</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
     	<item>
          	<name>button3</name>
          	<value>button3</value>
          	<length>20</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
    </property>
    <property id="barbutton">
   	 <item>
          	<name>right</name>
          	<value>next</value>
          	<length>6</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
    </property>
    <property id="bool">
   	 <item>
          	<name>Field1</name>
          	<value>1</value>
          	<length>1</length>
          	<editable>True</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
    </property>
	<property id="switch">
   	 <item>
          	<name>India Wins</name>
          	<value>YES</value>
          	<length>1</length>
          	<editable>NO</editable>
          	<sequence>1</sequence>
          	<section>1</section>
     	</item>
    </property>
</MangoUserDataFile>

```
In above XML,”id” in property will represents type of field and the remaining will tells about its functionality.

####Functionality:
Using NSXML parser we will parse teh XML and store it in a mutable array. This array contains dictionary.<br />
Note: We need to create all views or fields progmatically. We can't use Interface builder to create UI or fields.<br />
####Create Tab view programmatically:

tab=[[UITabBarController alloc]init];<br />
 NSMutableArray *tabViewControl = [[NSMutableArray alloc]init];<br />
.<br />
.<br />
.<br />
[tabViewControl addObject:viewNav];<br />
[tab setViewControllers:tabViewControl];<br />
[self.view addSubview:tab.view];<br />

####Create Text Field programmatically:

UILabel *lblMyLable = [[[UILabel alloc] initWithFrame:CGRectMake(10 + k, (j* 100) + 100, 150, 40)]autorelease];<br />
 llblMyLable.lineBreakMode = UILineBreakModeWordWrap;<br />
 llblMyLable.numberOfLines = 0;//Dynamic<br />
 llblMyLable.tag=1301;<br />
 llblMyLable.backgroundColor = [UIColor clearColor];<br />
 llblMyLable.text = fieldsDict.name;<br />
  [[self.view addSubview:lblMyLable];<br />
  
  UITextField * textFieldRounded = [[UITextField alloc] initWithFrame:CGRectMake(80 + k,(j * 100)+ 100, 150, 40)];<br />
  textFieldRounded.borderStyle = UITextBorderStyleRoundedRect;<br />
   textFieldRounded.textColor = [UIColor blackColor]; //text color<br />
   textFieldRounded.font = [UIFont systemFontOfSize:17.0];  //font size<br />
    //textFieldRounded.placeholder = @"<enter text>";  //place holder<br />
    textFieldRounded.text = fieldsDict.value;<br />
     textFieldRounded.userInteractionEnabled=NO;<br />
 textFieldRounded.backgroundColor = [UIColor greenColor]; //background color textFieldRounded.autocorrectionType =<br /> UITextAutocorrectionTypeNo;    // no auto correction support<br />
 textFieldRounded.keyboardType = UIKeyboardTypeDefault;  // type of the keyboard<br />
 textFieldRounded.returnKeyType = UIReturnKeyDone;  // type of the return key<br />
  textFieldRounded.clearButtonMode = UITextFieldViewModeWhileEditing;    // has a clear 'x' button to the right<br />
  
####Create Button programmatically:
  
  UIButton *myButton = [UIButton buttonWithType:UIButtonTypeRoundedRect];<br />
   myButton.frame = CGRectMake((j *200) + 50, 750, 150, 40);<br />
   [myButton setTitle:fieldsDict.value forState:UIControlStateNormal];<br />
   [self.view addSubview:myButton];<br />
   
   UILabel *lblMyLable2 = [[[UILabel alloc] initWithFrame:CGRectMake(50,10, 130, 30)]autorelease];<br />
    //lblMyLable2.lineBreakMode = UILineBreakModeWordWrap;<br />
    lblMyLable2.backgroundColor = [UIColor clearColor];<br />
   llblMyLable2.text = fieldsDict.name;<br />
    [self.view addSubview:lblMyLable2];<br />
    
####Create Switch programmatically:
    
       UISwitch *switchBtn;<br />
    switchBtn=[[UISwitch alloc]initWithFrame:CGRectMake(150, 10, 130, 40)];<br />
    BOOL status = [fieldsDict.value boolValue];<br />
    [switchBtn setOn:status animated:YES];<br />
    switchBtn.enabled = [fieldsDict.editable boolValue];<br />
    [self.view addSubview:switchBtn];<br />










