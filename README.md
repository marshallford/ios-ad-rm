# What is it?

Ad Rm is a small bash script run from SSH or Terminal on a Jailbroken iDevice. It provides a basic GUI for users that wish to remove ads from their system.

Works with:
* Installous
* Google Ads
* Flash Banners
* Malicious sites
* Spam sites
* Large and obtrusive ads

# Author Notes

1. Do not be alarmed at the warning message - It is required by Bigboss.

2. Bash was my first programming experience and this was my first "project", I can remember working on this for 4 hours straight. It is old news now, but I keep the repository up to remind myself were it all started.

# Change Log

### 1.3.2 - 6/19/11

1. Minor Changes
2. Using S3 to host the patch file
3. Includes Wget

### 1.3.1 - 4/10/11

1. # of lines in the control file FIX
2. Added to github

### 1.3.0 - 1/8/11

1. Restore to default option
2. Doesn't require a reboot
3. Hopefully some permission fixes ==> Does anyone have a fix?
4. Improved logging ==> 1.3.1
5. Add a custom source
6. Fix deb package issue
7. Adds a warning message

### 1.2.1 - First Public Release

1. Full menu system
2. Minimum bugs 

# Step to fix file permissions

1. Open up mobile terminal/SSH
2. Type "su"
3. Fill in password ( default is "alpine" )
4. Type "cd /usr/bin"
5. Type "chmod 777 adremover"
6. click enter
7. Type "chmod 777 adremover.sh"
8. Finally, Type "cd /var/mobile/Media/Downloads"
9. Then type, "chmod 777 hosts"
10. Now type "adremover" to start removing Ads!

**NOTE: Every time you load the script it requires root permissions**