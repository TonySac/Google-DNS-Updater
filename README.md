# Google-DNS-Updater

## Use
Bash script to update Google's Dynamic DNS records and send an email when done.
If Google provides your domain name, you can use this script to update the DNS record.
Check out Google's documentation on setting up dynamic DNS here: https://support.google.com/domains/answer/6147083.

## How it works
My script leverages the Google provided API to update the DNS record. It can be run one off in the command line or as a cron job.

At this time, it requires mailutils (https://mailutils.org) to be correctly configured on your system. The script sends an email upon completion/change of the IP.txt file.  

## Setup
After downloading the repository, you will need to set the configuration file. Navigate to where you clone the repository and take the following steps:

* Open the configuration file

```shell
nano config.sh
```

* Replace the curly bracketed variables `{ }` with your system specific values.

```shell
# Google DNS/Domain Hosting
Google_DNS_User="{DDNS USER NAME}" #Google provided username for DDNS
Google_DNS_Pass="{DDNS PASSWORD}" #Google provided password for DDNS
Google_Domain="{DOMAIN NAME}" #Domain name

#Email
eMail="{eMail Address}"

#Path to "Last IP.txt"
IPtxtPath="{PATH TO}/IP.txt"
```

Below is an example of an updated configuration file.

```shell
# Google DNS/Domain Hosting
Google_DNS_User="myusername" #Google provided username for DDNS
Google_DNS_Pass="mypassword" #Google provided password for DDNS
Google_Domain="mygoogledomain.com" #Domain name

#Email
eMail="my@myemail.com"

#Path to "Last IP.txt"
IPtxtPath="/home/pi/Google-DNS-Updater/IP.txt"
```

## Running

The script can be run once off from the command line:

```shell
bash GoogleDNSUpdate.sh
```
Or it can be placed in cron to run regularly depending on your system needs. 

### Plans for improvement
* Set email & command line alerts as optional
  * Removing dependency on mailutils
* Improve management of IP.txt
