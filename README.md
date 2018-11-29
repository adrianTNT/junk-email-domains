Should be updated with list of domains that offer disposable / junk / temporary email accounts. 
These are a huge problem for mail servers, they cause too many bounces, decrease mail server reputation and so on.

This list was made unique and sorted alphabetically with simple tools from http://app.tntcode.com/tools/ 

Currently there are over 700 domains.
```
0-mail.com
0815.ru
0clickemail.com
0wnd.net
0wnd.org
10minutemail.co.za
10minutemail.com
123-m.com
1fsdfdsfsdf.tk
1pad.de
20minutemail.com
21cn.com
2fdgdfgdfgdf.tk
2prong.com
30minutemail.com
[...]
```
The actual list is the */raw* file: https://raw.githubusercontent.com/adrianTNT/junk-email-domains/master/raw

## Sample PHP code to test user email and exit if needed, no libraries or dependencies to install.
```php
<?php 

$email = $_GET['email'];

// get the list of bad domains from github
$junk_email_domains_list = file_get_contents("https://raw.githubusercontent.com/adrianTNT/junk-email-domains/master/raw");

// make list lowercase for better comparison
$junk_email_domains_list = strtolower($junk_email_domains_list);

// make the list into an array so we can easy search in it
$junk_email_domains_array = explode("\n", $junk_email_domains_list);

// detect email domain from the email address
$email_domain = trim(substr($email, 1+stripos($email, "@")));

// make email_domain lowercase before comparing it in our list of banned emails
if($email_domain!='' and in_array(strtolower($email_domain), $junk_email_domains_array)){
	
	echo "Hello smarty-pants, you cannot emails from ".$email_domain;
	exit;
	
}

// if there are no evil matches then we are here, continuing with the code

?>
```


## exit if email was invalid in the first place

```php
<?php

$email = $_GET['email'];

if(!filter_var($email, FILTER_VALIDATE_EMAIL)){
	echo $email." doesn't seem to be a valid email";
	exit;
}

?>

## modify code to cache the code from github for a few days

```php
<?php 
// if we have a local copy of the file and it is newer than few days, use that one
if(@filemtime("junk_email_domains.txt") > time()-60*60*24*7){
	
	$junk_email_domains_list = @file_get_contents("junk_email_domains.txt");

} else {
	
	// get the list of bad domains from github
	$junk_email_domains_list = file_get_contents("https://raw.githubusercontent.com/adrianTNT/junk-email-domains/master/raw");
	
	// save our local cached file
	file_put_contents("junk_email_domains.txt", $junk_email_domains_list);
	
}
?>
```
