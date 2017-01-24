####Description:
Tinymce editor for textarea field in sugarcrm modules.

####Overview
Tinymce Editor Provides advanced compose functionality like (font style,font size,bold,italic etc.;), In write the text
in textarea type.

####How To Show tinymce editor for textarea type in sugarcrm modules:

####Step 1:
In metadata/modulename/editviewdefs.php

**_Code:_**

```
require_once("include/SugarTinyMCE.php");

$tiny = new SugarTinyMCE();

$tiny->defaultConfig['cleanup_on_startup']=true;

$tiny->defaultConfig['height']=300;

$tinyHtml = $tiny->getInstance('description');

//$xtpl->assign("tiny", $tinyHtml);

```

####Step 2:
For displaying tinymce editor in text area type we need to add custom code for particular field.

**_Code:_**

```
'customCode'=>'<textarea tabindex="104" title="" cols="40" rows="4" name="description"

id="description">{$fields.description.value}</textarea>{literal}'.$tinyHtml.'{/literal}',

Step 3:

Displaying advance compose text in detail view we need to add file views/view.detail.php

$des=$this->bean->description;

$des1=from_html($des);

$this->ss->assign("DESCR", $des1);

```
####Step 3:
Displaying advance compose text in list view we need to add file some code to module bean file like modulename.php file.

**_Code:_**

```
function retrieve($id){



$object=parent::retrieve($id);

$this->description = from_html($this->description);

return $this;

}

//Description field for listview.

function get_list_view_array(){

$array=parent::get_list_view_array();

$array['DESCRIPTION']=from_html($array['DESCRIPTION']);

return $array;


}

```

These Steps are needed for display tinymce editor in textarea type in any module.














