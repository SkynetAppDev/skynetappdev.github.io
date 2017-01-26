####Description:
This document comprise of total flow of moving code to AWS.<br />
The following screen is the startup screen for putty where we need to give the host url which is:

**_Code:_**

```
ec2-174-129-147-183.compute-1.amazonaws.com

```
![g1 1](https://cloud.githubusercontent.com/assets/25039079/22320314/3b2e475e-e3b1-11e6-90f1-1bb9cf805e48.png)

After entering the url, in the category panel under connection subsection, we need click on SSH option to upload the authentication ppk file as shown in the below screen and click open that opens the putty window.

![g2](https://cloud.githubusercontent.com/assets/25039079/22320242/76b62478-e3b0-11e6-94a1-8a7476509834.png)

Below screen is the putty start screen where we need to login by giving the user name which is ‘ubuntu’ and press enter

![g3](https://cloud.githubusercontent.com/assets/25039079/22320286/d2489b72-e3b0-11e6-9ae6-59d641d905ea.png)

After login, we need to enter cd .. command twice which takes us to the root directory in the AWS. We can see the list of directories in the below screen that were displayed after giving an command.

![g4](https://cloud.githubusercontent.com/assets/25039079/22320298/0ca390a6-e3b1-11e6-8d8e-57a1fe36249a.png)

Now we need to navigate to the directory sturcture var/www/indusmd/scheduler.
####To move code to AWS from SVN the command:

**_Code_:**

```
svn export <svn url where code is reciding> <destination folder>

```
####To remove code from Aws the command:

**_Code_:**

```
sudo rm -rf <directory name>

```
