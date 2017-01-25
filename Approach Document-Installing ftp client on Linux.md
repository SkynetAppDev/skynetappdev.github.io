####Description:
Installing ftp server on Linux(Ubuntu)

####Installing ftp
1. Use following commands to install ftp client.<br />
2. Sudo apt-get install vsftpd.<br />
3. To configure vsftpd to authenticate system users and allow them to upload files edit /etc/vsftpd.conf:<br />
4. Sudo vi /etc/vsftpd.conf <br />
5. Then edit/change following lines like below.

**_Code:_**

```
              local_enable=YES
                  write_enable=YES
                  
```               
                  
6.Now restart vsftpd

**_Code:_**

```

              sudo /etc/init.d/vsftpd restart
            
  ```
  
####Securing FTP:

1. There are options in /etc/vsftpd.conf to help make vsftpd more secure. For example  
      users can be limited to their home directories by uncommenting
      
**_Code:_**

```

             chroot_local_user=YES
   
 ```
 
2.Limit a specific list of users to just their home directories.

**_Code:_**

```
            chroot_list_enable=YES
            chroot_list_file=/etc/vsftpd.chroot_list
      
 ```
      
####SSL Configuration:
 
1.To configure FTPS, edit /etc/vsftpd.conf and at the bottom add

**_Code:_**

 ```    
             ssl_enable=Yes
       
 ```
2.Notice the certificate and key related options.<br />

**_Example_** **_Code:_**

 ```

             rsa_cert_file=/etc/ssl/certs/ssl-cert- snakeoil.pem
             rsa_private_key_file=/etc/ssl/private/ssl-cert- snakeoil.key
   
 ```
