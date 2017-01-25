####Description

To know how to configure the Process Manger to work with Scheduler.

####Step 1:

Login as admin, Click on admin and click on **Scheduler** under System section.

####Step 2: 

Click on Create Scheduler. Here give the details like job name, status, job (Please select runProcessManager for this field). And set the time interval that this job has to be run. Finally click on save button.

####Step 3: 

Now go to list view of the scheduler, at the bottom you can see the path to setup the scheduler to the OS. You need to copy the path and past in the crontab file.

For example:

          * * * * *  cd  /var/www/indusmd/sales; php -f cron.php > /dev/null 2 > &1
          This line of code tell the os about the path where the php file exists as well as the time interval to run the task.
          Here * represents - “ for every time interval“.

####Note: 
The above line of code need to be placed in the crontab file. Which exists in the path in the linux server.
         <br />  Path for crontab file :   var/spool/cron/crontab -e       
           
           
####**Important Note**: 
After setting cron job apache server should be restarted.         
