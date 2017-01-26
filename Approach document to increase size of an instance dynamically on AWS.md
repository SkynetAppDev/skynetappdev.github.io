####Description

Following is a detailed approach to increase size / computing capacity of an AWS instance.

####Assumption:

Before we move on to increasing size of instance, let us assume we have a site induspatient.com pointing to EC2 instance with an elastic IP.

####Step wise procedure to change instance type:
* Login into EC2 console and select the instance you want to change, in Actions button select stop option if it’s running. (Running instances cannot be changed its type).
* Select the stopped instance, in actions button click on change “instance type” link. That displays a pop up window as follows.

![6 1](https://cloud.githubusercontent.com/assets/17013436/22323564/bc304bd2-e3c9-11e6-9c8a-f125737934d2.PNG)

*	Select the appropriate kind of instance you want to change to and click on apply to reflect the change. ( in this example  we are changing from m1.small to m1.medium)
*	To increase computing power of the instance change from m1.small / m1.medium to c1.medium.
* Now start the instance by clicking on start option from actions button.
*	After restart, instance will lose its elastic IP, so we have to assign instance the same elastic IP we used earlier to make sure that our domain of application (induspatient.com) is pointing to this instance.
*	To assign elastic IP to the instance click on “Elastic IPs” link on the left panel of EC2 dashboard which displays list of available and assigned elastic IPs.
*	Select the elastic IP and click on “Associate Address” button on top that opens a pop up box to select an instance to assign this elastic IP to. As shown below and click associate button.

![6 2](https://cloud.githubusercontent.com/assets/17013436/22323939/0521b536-e3cc-11e6-8bac-b1cb211adba7.PNG)

*	Now your application hosted at induspatient.com is running with more disk space or more computing power (processing speed) according to your choice.

####Note:

All above process is clearly illustrated in the following link <br />
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-resize.html

To expand size of an existing AWS instance, follow the link below<br />
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-expand-volume.html

