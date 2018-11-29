# junk-email-domains
Should be updated with list of domains that offer disposable / junk / temporary email accounts. 
These are a huge problem for mail servers, they cause too many bounces, decrease mail server reputation and so on.

This list was made unique and sorted alphabetically with simple tools from http://app.tntcode.com/tools/ 

Currently there are over 700 domains.

The actual list is the */raw* file: https://raw.githubusercontent.com/adrianTNT/junk-email-domains/master/raw

Sample PHP code

<?php 
$junk_email_domains_list = file_get_contents("https://raw.githubusercontent.com/adrianTNT/junk-email-domains/master/raw");

// make list lowercase for better comparison
$junk_email_domains_list = strtolower($junk_email_domains_list);

$junk_email_domains_array = explode("\n", $junk_email_domains_list);


if(!filter_var($_GET['email'], FILTER_VALIDATE_EMAIL)){
	echo $_GET['email']." doesn't seem to be a valid email";
	exit;
}

$email_domain = trim(substr($_GET['email'], 1+stripos($_GET['email'], "@")));

// make email_domain lowercase before comparing it in our list of banned emails
if(in_array(strtolower($email_domain), $junk_email_domains_array)){
	
	echo "Hello smarty-pants, you cannot emails from ".$email_domain;
	exit;
	
}
?>
