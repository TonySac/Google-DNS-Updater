# Google-DNS-Updater

⚠️ As of October 6, 2023 I no longer use or maintain this script. I have switched to DDClient on OPNSense. ⚠️

This script is designed to call the Google API to update the dynamic DNS record for domains hosted on Google Domains. Check out Google's documentation on setting up dynamic DNS here: https://support.google.com/domains/answer/6147083.

This script can be run one off in the command line or as a cron job. If you have [GNU Mailutils](https://mailutils.org) configured, this script can also be set up to send an email upon successful update of your DNS record.

## General Overview

This script finds your current WAN IP address and compares it to the last known WAN IP, saved in the `IP.txt` file. If they differ, the Google API is invoked, result is displayed in the CLI and emailed if enabled. If they are the same, "Update Not Needed" is displayed and the script exits without invoking the API.

## Setup
After downloading the repository, you will need to set the configuration file. Navigate to where you saved the files and take the following steps:

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
eMail="{eMail Address}" #Set eMail="off" to disable

#Path to "Last IP.txt"
IPtxtPath="{PATH TO}/IP.txt"
```
NOTE: You can disable email functionality by setting the variable `eMail="off"`.
Below is an example of an updated configuration file.

```shell
# Google DNS/Domain Hosting
Google_DNS_User="myusername" #Google provided username for DDNS
Google_DNS_Pass="mypassword" #Google provided password for DDNS
Google_Domain="mygoogledomain.com" #Domain name

#Email
eMail="my@myemail.com" #Set eMail="off" to disable

#Path to "Last IP.txt"
IPtxtPath="/home/pi/Google-DNS-Updater/IP.txt"
```

## Running

The script can be run once from the command line:

```shell
bash GoogleDNSUpdate.sh
```

Or it can be placed in cron to run regularly depending on your system needs. 

```shell
# Run Dynamic DNS update everyday at 0001
1 0 * * * bash /home/pi/Google-DNS-Updater/GoogleDNSUpdate.sh
```

### Plans for improvement
* Improve management of IP.txt
* Bash syntax/formatting
