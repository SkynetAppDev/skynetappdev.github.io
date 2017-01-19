####Below is the Step wise Process Flow of hiding sub panels:
1.	We need to write a custom script file in the path

**_Code:_**
	
```
      custom/extension/modules/<required module>/Ext/Layoutdefs/<filename.php>
               
```

<br />2.	In the above path file could be given any name as per developer wish.
<br />3.	Define the layout definition as unset for the sub panel that we want to hide.
<br />4.	Syntax of the layout definition for hiding subpanel is:

**_Code:_**
	
```

      unset($layout_defs[<parent module>]['subpanel_setup'][<sub panel module name>]);

```

<br />5.	Save this php file and run repair and rebuilt from the admin section of sugar.


