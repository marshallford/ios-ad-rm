#!/bin/sh
# iOS-Ad-Remover ( AdRm )
# M Ford @ admin@fordinary.com
# This project is hosted @ https://github.com/Fordinary/ios-ad-rm
# Under the GNU GPL open source license

Warning() {
if [ -f "/tmp/adrmwarning.tmp" ]; then
:
else
clear
cd /tmp
touch adrmwarning.tmp
cd /var/mobile
echo "WARNING: AdRm will modify a system file"
echo "Time: 5"
sleep 1
clear
echo "WARNING: AdRm will modify a system file"
echo "Time: 4"
sleep 1
clear
echo "WARNING: AdRm will modify a system file"
echo "Time: 3"
sleep 1
clear
echo "WARNING: AdRm will modify a system file"
echo "Time: 2"
sleep 1
clear
echo "WARNING: AdRm will modify a system file"
echo "Time: 1"
sleep 1
clear
echo "WARNING: AdRm will modify a system file"
echo
echo "Click \"return\""
read systemreturnwarning
fi
}

Systemcheck() {
clear
# unset variables
unset systemreturn
unset systemreturntwo
unset systemreturnthree
unset systemreturnfour
unset systemreturnfive
## unset usedwget 
unset mainmenu
unset download

# Constants
date=`date +%d_%m_%y`
datetime=`date +%c_%p`
versionnumber="1.3.1"
hostv="1.4"


if [ `id -u` != 0 ]; then echo "You need to be root (su) to run this script."; exit 0; # required by Reboot command
echo
fi
## Logname and log info

cd /var/mobile
if [ -d "/var/log/adremover" ]; then
:
else
mkdir /var/log/adremover
fi

if [ -f "/var/log/adremover/adrm-$date.log" ]; then
cd /var/log/adremover
rm adrm-$date.log
cd /var/mobile
fi

logname=/var/log/adremover/adrm-$date.log
echo "iOS-Ad-Remover Log File" >> $logname
echo "$datetime" >> $logname
deviceinfo="Device: "`deviceinfo -p`
echo "$deviceinfo" >> $logname

logscriptv="Script Version: $versionnumber"
echo "$logscriptv" >> $logname

loghostv="Host file Version: $hostv"
echo "$loghostv" >> $logname
if [ -f "/usr/bin/adremover" ]; then #  location check
:
else
echo "This script is not called \"adremover\" or is not located at /usr/bin"
echo "Error: Script name or location not correct" >> $logname
sleep 4
exit
fi

if [ -f "/var/lib/dpkg/info/com.ericasadun.utilities.list" ]; then # Erica Utilities check
echo "Erica Utilities installed" >> $logname
else
echo "Erica Utilities not installed" >> $logname
echo "Error: You need to install Erica Utilities from Cydia"
sleep 5
exit
fi
}
Mainmenu() {
echo "   iOS Ad Remover $versionnumber"  
echo "============================================="
echo "   1) Download the Host file"
echo
echo "   2) Remove ads (change host file)"
echo
echo "   3) Restore to default"
echo
echo "   4) Add a custom address"
echo
echo "   5) Help"
echo
echo "   6) Exit"
echo
read mainmenu
}

## Download Options
Goback() {
clear
cd /usr/bin
./adremover.sh
}

Wget() {
clear
cd /var/mobile/Media/Downloads
if [ -f "/var/mobile/Media/Downloads/hosts" ]; then
rm hosts
fi
wget -O hosts http://sourceforge.net/projects/ios-ad-remover/files/Hosts/hosts%281.4%29/download
usedwget=1 
clear
echo "Host file downloaded."
echo "$hostv Host file downloaded from wget." >> $logname
echo
cd /var/mobile
echo "Click \"return\""
read systemreturn
Goback
}
Website() {
clear
echo "Opening Safari..."
sleep 2
openURL http://sourceforge.net/projects/ios-ad-remover/files/Hosts
clear
exit
}

Usehost() {
clear
echo "When you remove ads, 
This script will use the $hostv version of the host file"
sleep 1
echo
echo "Click \"return\""
read systemreturn
clear
Goback
}

## End Download options

Download() {
if [ -f "/usr/bin/wget" ]; then
## Download Menu WGET
echo "----Download Menu----"
echo
echo "   1) Open Website (Download Manually)"
echo
echo "   2) WGET (download) the Host file"
echo
echo "   3) Use bulit in $hostv Host file"
echo
echo "   4) Go Back"
echo
read download
if [ $download == 1 ]; then
Website
elif [ $download == 2 ]; then
Wget
elif [ $download == 3 ]; then
Usehost
elif [ $download == 4 ]; then
Goback
fi
fi
## Download Menu (normal)
if [ -f "/usr/bin/wget" ]; then
:
else
echo "----Download Menu----"
echo
echo "   1) Open Website (Download Manually)"
echo
echo "   2) Use bulit in $hostv Host file"
echo
echo "   3) Go Back"
echo
read download
if [ $download == 1 ]; then
Website
elif [ $download == 2 ]; then
Usehost
elif [ $download == 3 ]; then
Goback
fi
fi
}

Exit() {
clear
cd /tmp
rm adrmwarning.tmp
exit
}

Cleanup() {
cd /var/log/adremover
}

## MAIN Remove Ads
Rmads() {
clear
if [ -f "/var/mobile/Media/Downloads/hosts" ]; then
sleep 1
echo
echo "Backing-up"
sleep 3 
cd /var/mobile/Media/Downloads
if [ -d "/var/mobile/Media/Downloads/Backup" ]; then
:
else
mkdir Backup
fi

if [ -f "/var/mobile/Media/Downloads/Backup/$date-BakHosts" ]; then
cd /var/mobile/Media/Downloads/Backup
rm $date-BakHosts
fi

cd /etc
cp hosts /var/mobile/Media/Downloads/Backup
cd /var/mobile/Media/Downloads/Backup
mv hosts $date-BakHosts
echo
echo "Done"
echo
echo "Old host file backed-up" >> $logname # backup done
sleep 1
echo "Changing the Host file..."
sleep 3
cd /etc
rm hosts
cd /var/mobile/Media/Downloads
cp hosts /etc
rm hosts
echo
echo "You have successfully removed the majority of ads on iOS.
"
echo "You have successfully removed the majority of ads on iOS" >> $logname
sleep 3
echo "If you find an app that does not function"
echo " or bug because of the ad-removal please contact me at feedback@fordinary.com"
echo
echo "Click \"return\""
read
if [ -f "/tmp/adrmwarning.tmp" ]; then
cd /tmp
rm adrmwarning.tmp
fi
echo "Respring performed" >> $logname
respring
else
clear
echo "You do not have a downloaded host file
 in your Downloads Folder"
echo
echo "Error: Host file not found in Downloads Folder" >> $logname
echo "Click \"return\""
read systemreturnfour
Exit
fi
}

Help() {
clear
echo "          - iOS Ad Remover $versionnumber -"
echo "            Coded by Marshall"
echo
echo "This app should be run in Terminal
and requires Erica's Utilities."
echo
echo "Your log file will appear in 
/var/log/adremover."
echo
echo "The host file must be called \"hosts\"."
echo
echo "You can find the source and 
more info at http://sourceforge.net/projects/ios-ad-remover."
echo
echo "Click \"return\""
read systemreturntwo
Goback
}

Custommenu() {
clear
cd /etc
echo "---Custom Address Menu---"
echo 
echo "   1) Add Address"
echo
echo "   2) Exit"
read customaddressanswer
if [ $customaddressanswer == 1 ]; then
Custom
else
Goback
fi
}
Custom() {
clear
echo "Please Type the FULL web address not including \"http\""
echo
read customaddress
clear
echo "Are you sure you want to block $customaddress?"
echo
echo "y or n"
echo
read confirmcustom
if [ $confirmcustom = "y" ]; then
echo "User entered $customaddress as a custom address" >> $logname
echo "127.0.0.1 http://$customaddress" >> hosts
clear
echo "Done, $customaddress is now blocked"
echo
echo "Click \"return\""
read systemreturnfive
Custommenu
else
Goback
fi
}

## Restore Phase
Restore() {
clear
sleep 1
echo
echo "Backing-up"
sleep 3 
cd /var/mobile/Media/Downloads
if [ -d "/var/mobile/Media/Downloads/Backup" ]; then
:
else
mkdir Backup
fi

if [ -f "/var/mobile/Media/Downloads/Backup/$date-BakRestoreHost" ]; then
cd /var/mobile/Media/Downloads/Backup
rm $date-BakRestoreHost
fi

cd /etc
cp hosts /var/mobile/Media/Downloads/Backup
cd /var/mobile/Media/Downloads/Backup
mv hosts $date-BakRestoreHost
echo
echo "Done"
echo
echo "Host file backed-up for restore" >> $logname
echo "Restoring..."
sleep 1
cd /etc
rm hosts
cp hosts.original hosts
echo
echo "Done restoring"
echo
sleep 1
echo "Click \"return\""
read systemreturnsix
if [ -f "/tmp/adrmwarning.tmp" ]; then
cd /tmp
rm adrmwarning.tmp
fi
respring
}


Restoremenu() {
clear
cd /etc
echo "---Restore Menu---"
echo 
echo "   1) Restore to default"
echo
echo "   2) Exit"
read restoreanswer
if [ $restoreanswer == 1 ]; then
Restore
else
Goback
fi
}

## START ##

Systemcheck
Warning
clear
Mainmenu

if [ $mainmenu == 1 ]; then
clear
Download
elif [ $mainmenu == 2 ]; then
Rmads
elif [ $mainmenu == 3 ]; then
Restoremenu
elif [ $mainmenu == 4 ]; then
Custommenu
elif [ $mainmenu == 5 ]; then
Help
elif [ $mainmenu == 6 ]; then
Exit
else
clear
Goback
fi