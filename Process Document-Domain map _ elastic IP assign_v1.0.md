####Description:
This document will explain how to map domain to amazon instance and elastic ip assign.
####Producer:
Following steps invloved to map godadday domain to amazon instance.<br />

1.Login to amazon aws console.<br />
2. Assign elastic ip to aws instance.<br />
3. Login to godadday.<br />

####Step 1:
Login to amazon aws ec2 consol.

* Click on elastic IP's<br />
* Select elastic address which you want assign to instance.<br />
* Click on 'Associate Address' button<br />
* Select instance and click 'Yes,Associate'.<br />

####Step 2:
Login to Godadday

* Select 'My account' by clickin 'All Product' Tab.<br />
* Click on 'Domain' tab and select domain(Indusmd.com).<br />
* Click on 'Lunch' tab.<br />
* Open the 'DNS Zone' file and edit host with amazon elastic ip.<br />
* Click on 'Save' button.Note : It might be take 24 hours to made the changes.<br />
* Check the changes by entering the domain name on browser.EX: www.mydomain.com.<br />

####Note:
Even though if instance assigned elastic IP We need to assign the same Elastic IP again when restarting instance.



![document pic 1](https://cloud.githubusercontent.com/assets/25039079/22244685/911b84a2-e252-11e6-895f-aea03257fc1c.png)





![document pic 2](https://cloud.githubusercontent.com/assets/25039079/22245047/09f0b91e-e254-11e6-8f9f-6a34097f7b13.png)





![document pic 3](https://cloud.githubusercontent.com/assets/25039079/22245070/229b9a88-e254-11e6-8314-3ad237f725d2.png)





![document pic 4](https://cloud.githubusercontent.com/assets/25039079/22245206/d585fdd2-e254-11e6-974f-736fab15bd78.png)





![document pic 5](https://cloud.githubusercontent.com/assets/25039079/22245221/e86a531c-e254-11e6-9fb7-49863db717f1.png)





![document pic 6](https://cloud.githubusercontent.com/assets/25039079/22245252/0810deb6-e255-11e6-8965-1416f06ec182.png)





![document pic 7](https://cloud.githubusercontent.com/assets/25039079/22245276/21d14782-e255-11e6-827d-df7a5ecee201.png)


