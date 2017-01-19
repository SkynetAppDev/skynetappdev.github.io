####Description:
To auto-populate the fields in Editview of Medication module based on selection of a
record using ‘Relate to’ field

1. Here we are adding a new code snippet which performs the functionality mentioned.<br />
2. The vardef array has the values of all fields in the module.<br />
3. Here we are mapping the fields to be returned.<br />
4. To add any more fields to be returned from the module, add another entry in the array
'field_to_name_array' with the name of the field to be returned.<br />

####Procedure:
1. Go to ‘include/SugarFields/Fields/Relate/SugarRelateField.php’<br />
2. Find the function getEditViewSmarty($parentFieldArray, $vardef, $displayParams,
$tabindex)

**_Code:_**

```
function getEditViewSmarty($parentFieldArray, $vardef, $displayParams, $tabindex) {
if(!empty($vardef['function']['returns']) && $vardef['function']['returns'] == 'html'){
return parent::getEditViewSmarty($parentFieldArray, $vardef, $displayParams,
$tabindex);
}
$call_back_function = 'set_return';
if(isset($displayParams['call_back_function'])) {
$call_back_function = $displayParams['call_back_function'];
}
$form_name = 'EditView';
if(isset($displayParams['formName'])) {
$form_name = $displayParams['formName'];
}
//Special Case for accounts; use the displayParams array and retrieve
//the key and copy indexes. 'key' is the suffix of the field we are searching
//the Account's address with. 'copy' is the suffix we are copying the addresses
//form fields into.
if(isset($vardef['module']) && preg_match('/Accounts/si',$vardef['module'])
&& isset($displayParams['key']) && isset($displayParams['copy'])) {
if(isset($displayParams['key']) && is_array($displayParams['key'])) {
$database_key = $displayParams['key'];
} else {
$database_key[] = $displayParams['key'];
}
if(isset($displayParams['copy']) && is_array($displayParams['copy'])) {
$form = $displayParams['copy'];
} else {
$form[] = $displayParams['copy'];
}
if(count($database_key) != count($form)) {
global $app_list_strings;
$this->ss-
>trigger_error($app_list_strings['ERR_SMARTY_UNEQUAL_RELATED_FIELD_PARAMETERS']
);
} //if
$copy_phone = isset($displayParams['copyPhone']) ? $displayParams['copyPhone'] :
true;
$field_to_name = array();
$field_to_name['id'] = $vardef['id_name'];
$field_to_name['name'] = $vardef['name'];
$address_fields =
array('_address_street', '_address_city', '_address_state', '_address_postalcode', '_address_coun
try');
$count = 0;
foreach($form as $f) {
foreach($address_fields as $afield) {
$field_to_name[$database_key[$count] . $afield] = $f . $afield;
}
$count++;
}
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => $field_to_name,
);
if($copy_phone) {
$popup_request_data['field_to_name_array']['phone_office'] = 'phone_work';
}
}
elseif(isset($displayParams['field_to_name_array'])) {
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => $displayParams['field_to_name_array'],
);
} else {
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => array(
'id' => $vardef['id_name'],
((empty($vardef['rname'])) ? 'name' : $vardef['rname']) => $vardef['name'],
),
);
}
$json = getJSONobj();
$displayParams['popupData'] = '{literal}'.$json->encode($popup_request_data). '{/literal}';
if(!isset($displayParams['readOnly'])) {
$displayParams['readOnly'] = '';
} else {
$displayParams['readOnly'] = $displayParams['readOnly'] == false ? '' : 'READONLY';
}
$this->setup($parentFieldArray, $vardef, $displayParams, $tabindex);
return $this->fetch('include/SugarFields/Fields/Relate/EditView.tpl');
}

function getEditViewSmarty($parentFieldArray, $vardef, $displayParams, $tabindex) {
if(!empty($vardef['function']['returns']) && $vardef['function']['returns'] == 'html'){
return parent::getEditViewSmarty($parentFieldArray, $vardef, $displayParams,
$tabindex);
}
$call_back_function = 'set_return';
if(isset($displayParams['call_back_function'])) {
$call_back_function = $displayParams['call_back_function'];
}
$form_name = 'EditView';
if(isset($displayParams['formName'])) {
$form_name = $displayParams['formName'];
}
//Special Case for accounts; use the displayParams array and retrieve
//the key and copy indexes. 'key' is the suffix of the field we are searching
//the Account's address with. 'copy' is the suffix we are copying the addresses
//form fields into.
if(isset($vardef['module']) && preg_match('/Accounts/si',$vardef['module'])
&& isset($displayParams['key']) && isset($displayParams['copy'])) {
if(isset($displayParams['key']) && is_array($displayParams['key'])) {
$database_key = $displayParams['key'];
} else {
$database_key[] = $displayParams['key'];
}
if(isset($displayParams['copy']) && is_array($displayParams['copy'])) {
$form = $displayParams['copy'];
} else {
$form[] = $displayParams['copy'];
}
if(count($database_key) != count($form)) {
global $app_list_strings;
$this->ss-
>trigger_error($app_list_strings['ERR_SMARTY_UNEQUAL_RELATED_FIELD_PARAMETERS']
);
} //if
$copy_phone = isset($displayParams['copyPhone']) ? $displayParams['copyPhone'] :
true;
$field_to_name = array();
$field_to_name['id'] = $vardef['id_name'];
$field_to_name['name'] = $vardef['name'];
$address_fields =
array('_address_street', '_address_city', '_address_state', '_address_postalcode', '_address_coun
try');
$count = 0;
foreach($form as $f) {
foreach($address_fields as $afield) {
$field_to_name[$database_key[$count] . $afield] = $f . $afield;
}
$count++;
}
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => $field_to_name,
);
if($copy_phone) {
$popup_request_data['field_to_name_array']['phone_office'] = 'phone_work';
}
}
elseif(isset($displayParams['field_to_name_array'])) {
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => $displayParams['field_to_name_array'],
);
} else {
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => array(
'id' => $vardef['id_name'],
((empty($vardef['rname'])) ? 'name' : $vardef['rname']) => $vardef['name'],
),
);
}
$json = getJSONobj();
$displayParams['popupData'] = '{literal}'.$json->encode($popup_request_data). '{/literal}';
if(!isset($displayParams['readOnly'])) {
$displayParams['readOnly'] = '';
} else {
$displayParams['readOnly'] = $displayParams['readOnly'] == false ? '' : 'READONLY';
}
$this->setup($parentFieldArray, $vardef, $displayParams, $tabindex);
return $this->fetch('include/SugarFields/Fields/Relate/EditView.tpl');
}

```

3.Add the following code to make the changes

**_Code:_**

```
function getEditViewSmarty($parentFieldArray, $vardef, $displayParams, $tabindex) {
if(!empty($vardef['function']['returns']) && $vardef['function']['returns'] == 'html'){
return parent::getEditViewSmarty($parentFieldArray, $vardef, $displayParams,
$tabindex);
}
$call_back_function = 'set_return';
if(isset($displayParams['call_back_function'])) {
$call_back_function = $displayParams['call_back_function'];
}
$form_name = 'EditView';
if(isset($displayParams['formName'])) {
$form_name = $displayParams['formName'];
}
//Special Case for accounts; use the displayParams array and retrieve
//the key and copy indexes. 'key' is the suffix of the field we are searching
//the Account's address with. 'copy' is the suffix we are copying the addresses
//form fields into.
if(isset($vardef['module']) && preg_match('/Accounts/si',$vardef['module'])
&& isset($displayParams['key']) && isset($displayParams['copy'])) {
if(isset($displayParams['key']) && is_array($displayParams['key'])) {
$database_key = $displayParams['key'];
} else {
$database_key[] = $displayParams['key'];
}
if(isset($displayParams['copy']) && is_array($displayParams['copy'])) {
$form = $displayParams['copy'];
} else {
$form[] = $displayParams['copy'];
}
if(count($database_key) != count($form)) {
global $app_list_strings;
$this->ss-
>trigger_error($app_list_strings['ERR_SMARTY_UNEQUAL_RELATED_FIELD_PARAMETERS']
);
} //if
$copy_phone = isset($displayParams['copyPhone']) ? $displayParams['copyPhone'] :
true;
$field_to_name = array();
$field_to_name['id'] = $vardef['id_name'];
$field_to_name['name'] = $vardef['name'];
$address_fields =
array('_address_street', '_address_city', '_address_state', '_address_postalcode', '_address_coun
try');
$count = 0;
foreach($form as $f) {
foreach($address_fields as $afield) {
$field_to_name[$database_key[$count] . $afield] = $f . $afield;
}
$count++;
}
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => $field_to_name,
);
if($copy_phone) {
$popup_request_data['field_to_name_array']['phone_office'] = 'phone_work';
}
}
elseif($vardef['module']=='mango_Medication')
{
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => array(
'id' => $vardef['id_name'],
((empty($vardef['rname'])) ? 'name' : $vardef['rname']) => $vardef['name'],
((empty($vardef['strength'])) ? 'strength' :
$vardef['strength']) => 'strength',
((empty($vardef['mednumber'])) ?
'mednumber' : $vardef['mednumber']) => 'mednumber',
),
);
}
elseif(isset($displayParams['field_to_name_array'])) {
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => $displayParams['field_to_name_array'],
);
} else {
$popup_request_data = array(
'call_back_function' => $call_back_function,
'form_name' => $form_name,
'field_to_name_array' => array(
'id' => $vardef['id_name'],
((empty($vardef['rname'])) ? 'name' : $vardef['rname']) => $vardef['name'],
),
);
}
$json = getJSONobj();
$displayParams['popupData'] = '{literal}'.$json->encode($popup_request_data). '{/literal}';
if(!isset($displayParams['readOnly'])) {
$displayParams['readOnly'] = '';
} else {
$displayParams['readOnly'] = $displayParams['readOnly'] == false ? '' : 'READONLY';
}
$this->setup($parentFieldArray, $vardef, $displayParams, $tabindex);
return $this->fetch('include/SugarFields/Fields/Relate/EditView.tpl');
}

```

4.This will add the code to the button only for the Relate buttons for Medication Field

####Observations:

This is not a upgrade-safe method






