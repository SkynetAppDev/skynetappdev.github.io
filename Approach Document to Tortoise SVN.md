####1.Installing SVN

1.1 Download and install the Tortoise-SVN from here http://nchc.dl.sourceforge.net/project/tortoisesvn/1.6.15/Application/TortoiseSVN-1.6.15.21042-win32-svn-1.6.16.msi.<br />
1.2. In your local host create a directory with desired name (e.g : portal).<br />
1.3. Now right click on the created folder and browse the following path on the context menu.<br />

**_SVN Checkout:_**

![svn checkout](https://cloud.githubusercontent.com/assets/25039079/22078216/4f7fbc12-dddd-11e6-936a-bb56cdfe39a5.png)

In the URL of repository give the following link<br />
https://mangoindia.svn.beanstalkapp.com/portal_v1/<br />
Note:  the checkout directory should be your working directory<br />
1.4.After clicking on the ok button all the files which are on the server will be copied on to your machine with a revision head.

####2.Adding a folder:
1.1.Create a folder / file with desired name.<br />
1.2.	Right click on the folder / file and select TortoiseSVN   ADD.<br /> 
1.3.	After adding the folder / file right click on the same folder / file and click Commit.<br /> 
The committed changes are then sending to the main server and the changes are done with a revision head.

####3.Updating your instance:
Simply right click on the working folder and click on the Update menu. The files which are modified by others only get updated at your instance and the rest of the files are left unchanged.





