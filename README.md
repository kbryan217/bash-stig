
###########
# Summary #
###########

This is a STIG checker for 5 of the CAT 1 STIGs for Ubuntu 20.04. This script has been tested on Ubuntu 22.04 and works on Ubuntu 22.04. There is a second 
script ("prep_stig.sh") that will make the 5 items in this STIG script non-compliant to start so you can test the detection and remediation of each of those
STIG items. 

This script will run a check on each item. It will report that an item is compliant if it is configured inline with the STIG guidance
If an item is NOT Compliant, the script will inform the user and ASK if the user would like to fix the configuration. If the user responds with a 'y' or 'Y'
the script will then make the item compliant. If ANY other entry is input, the script will SKIP that item and move to the next item.

Once the stig_check.sh script has run through its checks, it will clear the screen and re-run the check to produce a final status report. Re-running the check was a design decision to 
verify changes that should have been made by the script. this ensures items are not marked as compliant simply because the user selected to implement the STIG fix. If the script is having
errors when running, comment out the 'clear'


ALL 5 STIG items checked by this scipt are CAT 1 STIG items lited below:

1. STIG ID UBTU-20-010405
2. STIG ID UBTU-20-010406
3. STIG ID UBTU-20-010460
4. STIG ID UBTU-20-010463
5. STIG ID UBTU-20-010042

#########
# Usage #
#########

This script is designed to simply be run on the system it is checking. It will require SUDO permissions and will ask for a password.
No arguments or options are needed

./stigcheck.sh


To verify that it will find all vulnerabilities, there is an additional script that will set all 5 STIG items to NOT compliant on the system. it can be run on the system as follows:

./prep_stig.sh

######################
# Possible Error Fix #
######################

Because some of this script was edited or resaved on a Windows computer, it may throw an error when it is ran. There are two methods i have found to fix this
and I have included them just in case I made a last minute adjustment before submission. 

Medthod 1 (requires a package to be installed)
sudo apt-get install dos2unix
dos2unix your_script.sh

OR

Method 2 
sed -i 's/\r$//' your_script.sh


######################
#### MODIFICATION ####
######################
# The STIG checklist tells the user to grep for the word 'telnetd' (and other items) only. If telnetd was never on the system, the return will be empty for 
# this command so this could work, however if telnet was ever on the system even if it has already been removed, the command from the STIG checklist WILL 
# return positive/TRUE because the entry is still in the compiter file. I adjusted the command to look for the double 'i' (or 'ii') preceeding telnetd as 
# this is the indicator that the application is installed from what i can tell. Once the application has been removed the system entry changes the 'ii' to 
# a 'rc'. modifying the command in this way has allowed me to test this script many times and prevent false positives.
