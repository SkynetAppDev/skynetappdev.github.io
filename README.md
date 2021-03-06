[NEXT](Approach Document SMTP Mail configuration in Sugar.README.md)
## Welcome to GitHub Pages
#### Date: 21-10-2016
#### Description: This document aims to define the Bluemix Tone Analyzer API coding 

[Approach Document SMTP Mail configuration in Sugar](Approach Document SMTP Mail configuration in Sugar.README.md)
<br>
[Approach Document SMTP Mail configuration in Sugar](Approach Document SMTP Mail configuration in Sugar.README.md)
<br>
[Approach Document for Facebook , LinkedIn Integration to Patient App](Approach Document for Facebook , LinkedIn Integration to Patient App.md)
<br>
[Approach Document for LinkedIn Integration](Approach Document for LinkedIn Integration copy.md)
<br>
[Approach Document for Removing Create-Select Buttons from the Sub Panels](Approach Document for Removing Create-Select Buttons from the Sub Panels.md)
<br>
[Approach Document for setting up SSL on EC2](Approach Document for setting up SSL on EC2.md)

#### The Folder Structure is as follows:
   
   
   Root Directory | Sub Directory | Sub Directory 
------------ | ------------- | -------------
index.php | | |
Global | DBmongo(Mongo Connection),DBmysql(MySQL Connection), BlueMixToneAnalyzerAPI(Tone Analyzer Connection)  | 
Lib | Smarty,Common functions | |
Modules | BluemixToneAnalyzer | Tone Analyzer Controller, Tone Analyzer Action, Tone Analyzer MySql, Tone Analyzer View, Tone Analyzer API Call, Tone Analyzer DB Mongo|
Views | BluemixToneAnalyzer | header.tpl, footer.tpl(Common files), masterList.tpl,detailList.tpl|

#### Code Flows as follows:
   * To insert or get data from DB code flows.. index.php -> Controller -> Action -> MySql.
   * To view the data code flows.. index.php -> Controller -> View.
   
 
#### Step 1:
  Add the created Url, Username and Password in the config.php under bluemix2.0 folder.we can get the Tone Analyzer API Username and password by logging into IBM Bluemix. 
	
**_Code:_**
	
```
	
	$GLOBALS['bluemix_toneanalyzer_username']='xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';
	$GLOBALS['bluemix_toneanalyzer_password']='xxxxxxxxxxxx';
	$GLOBALS['bluemix_toneanalyzer_url']='https://gateway.watsonplatform.net/tone-analyzer/api/v3/tone?version=2016-05-19';
	
```
	
  
#### Step 2:
  Create a module name as 'toneAnalyzer' in index.php and respective actions will be performed accordingly.
  
**_Code:_**

```
<?php
if($_REQUEST['module']=='toneAnalyzer'){  
    switch ($_REQUEST['action']){
	    case 'GetList':
        {
          $bluemixToneAnalyzerController = BluemixToneAnalyzerController::getInstance();
          $bluemixToneAnalyzerController->getMasterDataFromMySQL();
          break;
        }
              {
          $bluemixToneAnalyzerController = BluemixToneAnalyzerController::getInstance();
          $bluemixToneAnalyzerController->getChildDataFromMySQL($_REQUEST);
          break;
        }
		 case 'InsertList':
        {
          $bluemixToneAnalyzerController = BluemixToneAnalyzerController::getInstance();
          $bluemixToneAnalyzerController->insertBlueMixToneAnalyzerResponseIntoDB();
          break;
        }
		
    }
}
?>

```

#### Step 3:
   In the server normally we will be able to see existing Master list data. When we click on the update button 'InsertList' action will be performed from index page and **insertBlueMixToneAnalyzerResponseIntoDB()** will be called.
   
#### Step 4:
   From index.php, **BluemixToneAnalyzerController** class will be called which controlles all the operations of Tone Analyzer module. Here function **insertBlueMixToneAnalyzerResponseIntoDB()** will be executed.
   
#### Step 5:
   This **getTextData()** function gets the multiple records data from Request table and sends request to Tone Analyzer Curl response function **getBlueMixCURLResponse($text)** one by one using for loop.
   
#### Step 6:
   On receiving response from API, the JSON response will be stored in Mongo DB by calling function  **insertBlueMixJSONResponseIntoMongo($data)**.
   
#### Step 7:
   The JSON response result will be converted into Array by calling function **transformJSONToArray($data)**.
   
**_Code:_**

```   
   public function transformJSONToArray($sampletext){
    	$response_array = json_decode($sampletext,TRUE);
    	return $response_array;
	}
  
```  

#### Step 8:
   The response array will be inserted into Master data by function **insertMasterDataIntoMySQL($bluemix_response_array)**.
   
**_Code:_**

```  
  public function insertMasterDataIntoMySQL($data){
		$this->response_array =$data;
		$masterId=$this->insertIntoMasterData();
		if($masterId>0)
		return $this->getParsedDataFromJSONResponse($masterId);
	}
  
   public function insertIntoMasterData(){
    	$sql = "INSERT INTO master_tone_analyzer_request
               (
                master_comments,
                master_reponse) VALUES (
                '$data',
                'Json Response'
                )";
		mysqli_query($this->con,$sql);
        return $this->con->insert_id;
    }

```

#### Step 9:
   Here based on the master request id, the response will be stored in Child table by function **getParsedDataFromJSONResponse($masterReqId)**.

**_Code:_**

```
    public function getParsedDataFromJSONResponse($masterReqId){
		//echo "<pre>";print_r($this->response_array);
    	foreach($this->response_array['document_tone']['tone_categories'] as $mainKey=>$mainVal){
            foreach($mainVal['tones'] as $secLKey=>$secLVal){
				$tone['score']=$secLVal['score'];
				$tone['tone_id']=$secLVal['tone_id'];
				$tone['tone_name']=$secLVal['tone_name'];
				$tone['category_id']=$mainVal['category_id'];
                $this->collectChildrenRecordData($tone,$masterReqId);
			}
        }
	return true;
    }

    public function collectChildrenRecordData($mainVal,$masterReqId){
    	$rowData = array();
        $rowData['score']=$mainVal['score'];
        $rowData['tone_id']=$mainVal['tone_id'];
        $rowData['tone_name']=$mainVal['tone_name'];
		$rowData['category_id']=$mainVal['category_id'];
        $rowData['request_id']=$masterReqId;
        return $this->insertIntoChildren($rowData);
    }

       public function insertIntoChildren($rowData){
    	//if($rowData['score']!='')
		$sql = "INSERT INTO children_tone_analyzer_request
                (tones_score,
                tones_tone_id,
                tones_tone_name,
				category_id,
                master_request_id) VALUES (
                '".$rowData['score']."',
                '".$rowData['tone_id']."',
                '".$rowData['tone_name']."',
				'".$rowData['category_id']."',
                '".$rowData['request_id']."'
                )";
        mysqli_query($this->con,$sql);
        return $this->con->insert_id;
    }
    
```

#### Step 10:
   On inserting the JSON response into master and child tables, the status and Request date will be updated for that record in the Request table by function **updateToneAnalyzerTextData($id)** in controller.


#### Step 11:
   To get the Master list function **getALLMasterDataFromMySQL** will be called from controller.
   
#### Step 12:
   To view the Master list function **showallMasterListView()** will be called from controller to View.
   
**_Code:_**

```
   function showallMasterListView($data_arr){
        $smarty = new Smarty();
        $smarty->assign('base_path',$GLOBALS['base_path']);
		$smarty->assign('cursor',$data_arr);
	    $smarty->display(''.$GLOBALS['root_path'].'/Views/BluemixToneAnalyzer/allmasterList.tpl');
    }
    
``` 

#### Step 13:
   To view the Child data based on the master id, function **getChildDataFromMySQL($post_data)** will be called from controller.
   Function **getAllChildDataFromMySQL($post_data)** will get the reocrds based on the master id using MySql query. Function **showDetailListView($bluemix_list_vo)** will be called in view. 
   
**_Controller page Code:_**

```
public function getChildDataFromMySQL($post_data){
        $bluemix_action = BluemixToneAnalyzerAction::getInstance();            
        $bluemix_list_vo = $bluemix_action->getAllChildDataFromMySQL($post_data);
		$bluemix_view = BluemixToneAnalyzerView::getInstance();            
    	$bluemix_view->showDetailListView($bluemix_list_vo);
	}
```
**_View page Code:_**

```
function showDetailListView($data_arr){
        $smarty = new Smarty();
        $smarty->assign('base_path',$GLOBALS['base_path']);
		$smarty->assign('cursor',$data_arr);
	    $smarty->display(''.$GLOBALS['root_path'].'/Views/BluemixToneAnalyzer/detailList.tpl');
    }
```
