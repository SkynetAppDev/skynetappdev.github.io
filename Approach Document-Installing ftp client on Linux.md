####Description:
Installing ftp server on Linux(Ubuntu)
####Installing ftp

1.Use following commands to install ftp client.<br />
2.Sudo apt-get install vsftpd.<br />
3.To configure vsftpd to authenticate system users and allow them to upload files edit /etc/vsftpd.conf:<br />
4.Sudo vi /etc/vsftpd.conf <br />
5.Then edit/change following lines like below

              local_enable=YES
                  write_enable=YES<br />
                  
6.Now restart vsftpd<br />

            sudo /etc/init.d/vsftpd restart
            
####Securing FTP:

1.There are options in /etc/vsftpd.conf to help make vsftpd more secure. For example  
      users can be limited to their home directories by uncommenting
      
      chroot_local_user=YES<br />
      
2.Limit a specific list of users to just their home directories.

      chroot_list_enable=YES<br />
      chroot_list_file=/etc/vsftpd.chroot_list
      
####SSL Configuration:
 
1.To configure FTPS, edit /etc/vsftpd.conf and at the bottom add
     
       ssl_enable=Yes

2.Notice the certificate and key related options.
Example

        rsa_cert_file=/etc/ssl/certs/ssl-cert- snakeoil.pem
        rsa_private_key_file=/etc/ssl/private/ssl-cert- snakeoil.key
