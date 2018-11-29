Should be updated with list of domains that offer disposable / junk / temporary email accounts. 
These are a huge problem for mail servers, they cause too many bounces, decrease mail server reputation and so on.

This list was made unique and sorted alphabetically with simple tools from http://app.tntcode.com/tools/ 

Currently there are over 700 domains.

The actual list is the */raw* file: https://raw.githubusercontent.com/adrianTNT/junk-email-domains/master/raw

Sample PHP code to test user email and exit if needed, not libraries or dependencies to install.
```php
<?php 

$email = $_GET['email'];

$junk_email_domains_list = file_get_contents("https://raw.githubusercontent.com/adrianTNT/junk-email-domains/master/raw");

// make list lowercase for better comparison
$junk_email_domains_list = strtolower($junk_email_domains_list);

$junk_email_domains_array = explode("\n", $junk_email_domains_list);

$email_domain = trim(substr($email, 1+stripos($email, "@")));

// make email_domain lowercase before comparing it in our list of banned emails
if(in_array(strtolower($email_domain), $junk_email_domains_array)){
	
	echo "Hello smarty-pants, you cannot emails from ".$email_domain;
	exit;
	
}

?>
```


You might also want to exit at the very start if the provided email is an invalid one

```php
<?php

$email = $_GET['email'];

if(!filter_var($email, FILTER_VALIDATE_EMAIL)){
	echo $email." doesn't seem to be a valid email";
	exit;
}

?>
