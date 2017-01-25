####Description

Approach Document for Theme Integration in IndusMD EMR

Note 1: Theme integration is explained in the traditional UI layout manner ie. header, content and footer<br />
Note 2: The default css location is <root>/themes/Sugar5/ css/style.css<br />
Note 3: The default images location is <root>/themes/Sugar5/ images/<br />

####Header:

![5 1](https://cloud.githubusercontent.com/assets/17013436/22284547/d17e8b0a-e30d-11e6-9b00-eee6b458e610.PNG)

**_Code:_**
	
```

Logo:  <root>/themes/Sugar5/tpls/_companyLogo.tpl
CSS Class: companyLogo

Global Links: <root>/themes/Sugar5/tpls/_globalLinks.tpl
CSS Class: globalLinks

```

####Top Navigation:

![5 2](https://cloud.githubusercontent.com/assets/17013436/22284614/1df447e0-e30e-11e6-8d6d-e1ac3e99acb7.PNG)

**_Code:_**
	
```

Module List : <root>/themes/Sugar5/tpls/_headerModuleList.tpl
CSS Classes: moduleList, notCurrentTabLeft, notCurrentTabRight, noBorder and notCurrentTab

```

####Footer:

![5 3](https://cloud.githubusercontent.com/assets/17013436/22284664/4835ce7a-e30e-11e6-9687-38dba54e1116.PNG)

**_Code:_**
	
```

Logo: <root>themes/Sugar5/images/certification-icons.png
CSS Classes: footer and copyright 

```

####Shortcuts:

![5 4](https://cloud.githubusercontent.com/assets/17013436/22284703/7b40f722-e30e-11e6-9129-df6baae3bcb7.PNG)

**_Code:_**
	
```

 Logo paths : <root>themes/Sugar5/images/
 CSS Classes: shortcuts and headerList

```

####Module Title:

![5 5](https://cloud.githubusercontent.com/assets/17013436/22284779/c15ffbae-e30e-11e6-80ef-101c136fd7ec.PNG)

**_Code:_**
	
```

File path: <root>/include/MVC/View/SugarView.php
CSS Classes : moduleTitle,  h2Row_2, icon_h2, pointer,  patient_wizard_left_shadow and  patient_wizard_left_shadow

```

####Module List View:

![5 6](https://cloud.githubusercontent.com/assets/17013436/22284834/ff571190-e30e-11e6-9f30-8afdf7a8f661.PNG)

**_Code:_**
	
```

CSS Classes: oddListRowS1, evenListRowS1, pagination and view

```

####Module Subpanels:

![5 7](https://cloud.githubusercontent.com/assets/17013436/22284919/679ec93c-e30f-11e6-8957-7e6377af1661.PNG)

**_Code:_**
	
```

File Path: <root>include/Dashlets/Dashlet.php
CSS Classes : patient_wizard_left_shadow, patient_wizard_right_shadow, dashletBorder

```

####Miscellaneous:
Ajax Pop Up window:

![5 8](https://cloud.githubusercontent.com/assets/17013436/22284956/a70bbd00-e30f-11e6-9e53-e4ba56b64476.PNG)

**_Code:_**
	
```

CSS Classes: hd, loading_c, container-close 

```






