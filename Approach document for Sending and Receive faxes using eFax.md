####Description:
Sending and Receive faxes using eFax.

####Overview:
eFax is a company that let's you send and receive faxes via the Internet. The faxes can be sent to a standard paper fax or to a virtual fax machine (i.e. to your eFax account.) There are two interfaces:

1. An email interface used to send and receive documents from a set of standard email addresses.<br />
2. A secure HTTPS API called eFax Developer or business eFax. It can be used in a totally automated way to send and receive faxes via a web interface using the standard HTTPS protocol for communication.<br />

####Sending a Fax:
* First Include The efax class into the script ,then create the object of the class.<br />
* Then will need to set of functions to our specific needs.<br />
* Those functions are like set_account_id(“ ”),set_user_name(“ ”),set_user_password(“ ”),
     add_file,add_recipient<br />
* Then will use set_outbound_url("https://secure.efaxdeveloper.com/EFax_WebFax.serv");this url need not to modify.<br />
* In the similar way we write several functions basis upon our requirements.<br />
* Finally use send function for sending fax

####Important Note:
* For this efax class runs in windows/linux we need pecl extensions like dll files needed into php.ini.<br />
* If we want efax class we need to payment to efax.

**_Implementation Code:_**

```
$efax = new eFax;

    // mandatory parameters
    $efax->set_account_id("9169881450");
    $efax->set_user_name("made_to_order_software");
    $efax->set_user_password("TopSecret");
    $efax->add_file("txt", "This is the content of my text file");
    $efax->add_recipient("Alexis Wilke", "Made to Order Software", "9169881450");

    // Though this is mandatory, the constructor sets the default that
    // you should not need to modify.
    $efax->set_outbound_url("https://secure.efaxdeveloper.com/EFax_WebFax.serv");

    // mandatory if set_duplicated_id(false);
    $efax->set_fax_id("Fax #123456");

    // mandatory if set_disposition_method("EMAIL");
    $efax->add_disposition_email("Alexis Wilke", "alexis@m2osw.com");

    // mandatory if set_disposition_method("POST");
    $efax->set_disposition_url("https://secure.m2osw.com/fax-disposition.php");

    // optional flags
    $efax->set_disposition_level(eFax::RESPOND_ERROR | eFax::RESPOND_SUCCESS);
    $efax->set_disposition_method("POST");
    $efax->set_duplicate_id(false);
    $efax->set_fax_header("   @DATE @TIME Made to Order Software Corporation");
    $efax->set_priority("HIGH");
    $efax->set_resolution("STANDARD");
    $efax->set_self_busy(true);

    // ready to send the fax
    $result = $efax->send($efax->message());
    if($result)
    {
        ... // handle success
    }
    else
    {
        ... // handle failure
    }
    
  ```
  
  This is the way of connecting set_outbound_url,set_disposition_url of these methods and Implementation details.


