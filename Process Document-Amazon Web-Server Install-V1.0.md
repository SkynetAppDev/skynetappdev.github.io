Launching new webserver using existing 'Base Web-Server'.
####Description:
Following steps invloved to create Web-Server instance using existing AMI( ami-1fc4af76 ).

1.Choose an AMI<br />
2. Instance details<br />
3. Create key pair<br />
4. Configure firewall<br />
5. Review<br />

####Procedure:
Lunching new instance using 'Base Web-Server Reference' instance.

####Step 1: Choose an AMI

* Click on launch instance.
![pic 1 1](https://cloud.githubusercontent.com/assets/25039079/22278959/5758c28e-e2ed-11e6-9cd8-2a605b31cf1b.png)
* Click on my AMIs
* Select BaseWeb-Server(ami-1tc4af76)
* Select BaseWeb-Server(ami-1tc4af76)

![pic 2](https://cloud.githubusercontent.com/assets/25039079/22279032/0575afc6-e2ee-11e6-869b-4e47342be9e9.png)

####Step2 : Instance details
* Select instance type based on server requirements.
* Here I'm selecting M1 Medium with 2 ECUs,1 CPU Core with 3.7 GiB.
* Click on 'Continue' button then it will redirect to 'Advanced Instance Options'.
* Use default options and click on continue.

 ![pic 3 1](https://cloud.githubusercontent.com/assets/25039079/22279231/6136faee-e2ef-11e6-8aa5-bd7397fb3e6e.png)
 
 ![pic 4 2](https://cloud.githubusercontent.com/assets/25039079/22279630/d1b19df4-e2f1-11e6-8dbd-db15d0953e7f.png)
    
 ![pic 5 2](https://cloud.githubusercontent.com/assets/25039079/22279709/5cb87ff8-e2f2-11e6-87c1-d7ed4473e5d8.png)

####Step3 : Create key pair

* Enter the name for keypair.<br />
* Download keypair.<br />
* Click on 'continue'.Please the below images.<br />

![pic 6 2](https://cloud.githubusercontent.com/assets/25039079/22280069/87e32d3e-e2f4-11e6-94ec-51fcd5387047.png)

####Step4 : Configure FireWall Settings

* Create new security group.
* Enter name and description.
* Set inbound rules.
* Click on continue button.

![pic 7](https://cloud.githubusercontent.com/assets/25039079/22280149/fa32c41c-e2f4-11e6-8cc5-bf9be3cd7e2f.png)

####Step5 : Review

* Review all setting and configurations.
* If anything wrong go back and configure again.
* If everthing fine Click on Luanch button.It will launch new instance.
* Check the status in dashboard.

![pic 8](https://cloud.githubusercontent.com/assets/25039079/22280200/4f4d0bce-e2f5-11e6-9952-00e90b2c7a0b.png)


  

