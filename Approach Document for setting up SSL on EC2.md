####Description:
To setup SSL on EC2 Environment.
####Step 1:
* Login to ssh/terminal on your server and enable SSL for WebServer(Apache2)
             command: sudo a2enmod ssl
             
####Step 2:
* Create the server SSL Key
 command: sudo bash<br />
**Note 1**: On Ubuntu this changes you to the root user as you cannot access the directory on the next step.<br />
 command: cd /etc/ssl/private<br />
            command: openssl genrsa -des3 -out indusmdemr.com.key 2048<br />
 **Note 2**: Make sure its 2048 and not 1024 bit as this would be required later on GoDaddy.<br />
  Enter keyphrase {in terminal you need to enter a keyphrase, it is a temporary passcode}<br />
  
####Step 3:
* Create the CSR (Certificate Service Request) to be entered on GoDaddy<br />
command : openssl req -new -key indusmdemr.com.key -out indusmdemr.com.csr<br />

####Step 4:
* View the generated CSR and copy. Paste it later to your GoDaddy SSL Certificate Management Tool

####Step 5:
* Install your certificate gd_bundle.crt and indusmdemr.com.crt to your server. Upload them to the server and  execute the following <br />
command : mv gd_bundle.crt /etc/ssl/gd_bundle.crt<br />
command : mv indusmdemr.com.crt /etc/ssl/certs/indusmdemr.com.crt<br />

####Step 6:
* Edit the default Apache2 values at /etc/apache2/sites-available/default. Create a new virtualhost.<br />
NameVirtualHost *:443<br />
DocumentRoot /var/www/<br />
SSLEngine on<br />
SSLOptions +FakeBasicAuth +ExportCertData +StrictRequire<br />
SSLCertificateFile /etc/ssl/certs/indusdmemr.com.crt<br />
SSLCertificateKeyFile /etc/ssl/private/indusmdemr.com.key<br />
SSLCertificateChainFile /etc/ssl/gd_bundle.crt<br />

####Step 7:
* Make sure Apache2 to listen on port 443, edit the /etc/apache2/ports.conf  and restart Apache
command : /etc/init.d/apache2 restart

 **Note 3**: If all went well you should be able to access https. For EC2 make sure Port 443 is enabled as well on the AWS Console


####Step 8:
* Create an htaccess file and upload to your root www folder<br />
RewriteEngine On<br />
RewriteCond %{SERVER_PORT} 80<br />
RewriteRule ^(.*)$ https://www.indusmdemr.com/$1 [R,L]<br />

By following the above steps one can install the SSL certificate  on EC2 environment.





  
  


