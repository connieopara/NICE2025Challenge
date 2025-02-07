#### NICE2025Challenge
My step by step work through of the NICE XP Range cybersecurity challenge
#### Configuration Management Gone Awry
Steps to complete the lab: 

# Logged into Fileshare and used ifconfig to check the network configuration. I noticed the IP address and subnet mask were incorrect. To correct this I used the command below:

sudo IP addr add 172.16.30.100/24 dev ens32

sudo IP route add default via 172.16.30.250

note: I had to use the IP link show command to confirm the right network interface name. 

# Next, I logged into the Domain controller and also checked the network configurations using ipconfig /all

this command also shows misconfiguration so to correct it, I used the command below:

netsh interface ip set address name="Ethernet0" static 172.16.30.55 255.255.255.0 172.16.30.250 

also note that I had to use the netsh interface show interface command to determine the right interface name. 

# Connecting to the Workstation over the domain was not possible, so I had to log in using local credentials instead of the domain account. I clicked on "other user" and used WORKSTATION\playerone. This gave me access to the workstation.

From the command prompt, I verified the network configurations (ipconfig /all) and discovered misconfiguration. Hence, using the command below, I manually input the right IP address, subnet mask, and default gateway. 

netsh interface IP set address name="Ethernet0" static 172.16.20.60 255.255.255.0 172.16.20.250

this established connectivity for the workstation. Note that ping to the domain controller was unsuccessful but a tracert showed the path to AD server 172.16.30.55. I suspect routing issues.

Domain controller can ping the workstation 172.16.20.60

# Finally, I logged into Prod-Joomla and checked for IP configuration using "IP addr show" command the IP address was properly configured but there was no default gateway set.

using "sudo IP route add default via 172.16.10.250" I set the default gateway.

Now a ping from joomla to workstation was successful.


![XP range Configuration Management Gone Awry](https://github.com/user-attachments/assets/422bd975-d7a0-4b59-a0b6-9a406ef98110)
