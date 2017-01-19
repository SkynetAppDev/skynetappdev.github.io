####Description

Create dynamically icons on tab bar using XMLParser.

####Step 1:

Create a view based framework/Navigation based framework. Add one UITabBarController.

**_Code:_**
	
```

      Exm:-UITabBarController * tabbarController=[[UITabBarController alloc]init];
      [tabbarController.view sizeToFit];
      CGFloat tabbarControllerHeight = [tabbarController.view frame].size.height;
      CGRect rootViewBounds = self.parentViewController.view.bounds;
      CGFloat rootViewHeight = CGRectGetHeight(rootViewBounds);
      CGFloat rootViewWidth = CGRectGetWidth(rootViewBounds);
      CGRect rectArea = CGRectMake(0, rootViewHeight -tabbarControllerHeight,
      rootViewWidth, tabbarControllerHeight);
      [tabbarController.view setFrame:rectArea];
      tabbarController.view.autoresizingMask =  UIViewAutoresizingFlexibleLeftMargin |
      UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight | 
      UIViewAutoresizingFlexibleTopMargin | UIViewAutoresizingFlexibleRightMargin;
      [tabbarController setViewControllers:mainarray];
      [self.navigationController.view addSubview:tabbarController.view];
      
```      
      
####Step 2:  

  Add an NSObject class to main frame work.<br />
	Used of NSObject class.<br />
	To store all data in this NSObject Class and Call this NSObject class where we 		need to display the data whatever data we get from XML File.<br />

####Step 3:

Add another NSObject class for XMLParser.

####Step 3.1:

Create a method For Initialized the All object which is used in this parser<br />
Ex:- In this method we Initialized one Array (for store the data), String (for store all attributes) and NSXMLParser

**_Code:_**
	
```

      -(NSMutableArray *) parseUserPage1File:(NSData *)data
      {
      arrayOfproperty = [[NSMutableArray alloc]init];
      propertyString = [[NSString alloc]init];
      xmlParser = [[NSXMLParser alloc] initWithData: data];
      [xmlParser setDelegate: self];
      [xmlParser setShouldResolveExternalEntities: YES];
      [xmlParser parse];
      }
      
```

####Step 3.2:

Default delegates methods for XMLParser.

1. This method used to start searching attributes from XMLFile and store all attributes in dictionary

**_Code:_**
	
```
      - (void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName 
      namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qualifiedName 
      attributes:(NSDictionary *)attributeDict 
      
```

<br />2. This method used once we found the string then store all the string in NSObject class.

**_Code:_**
	
```

       -(void)parser:(NSXMLParser *)parser foundCharacters:(NSString *)string 
       
```

<br />3. This method used once we get all required string and store in NSObject after that we have to stop searching attributes from XMLFile.

**_Code:_**
	
```

       -(void)parser:(NSXMLParser *)parser didEndElement:(NSString *)elementName 
       namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName 
       
            
```

####Step 4:

Once we get all the data in NSObject class then we need to store all the data in array and that array we need to add in Tabbar.

       For Exm:-[tabbarController setViewControllers:mainarray];
       
 Here tabbar Controller is the UITabBarController and mainarray is the array we store all value whatever we store in NSObject class after collecting from XMLFile.      



       
