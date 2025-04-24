# azure-network-protocols<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

High-Level Steps
Create Virtual Machines in Azure.
Observe ICMP traffic between Virtual Machines using Wireshark.
Configure a Firewall (Network Security Group) and analyze its impact on network traffic.
Observe various protocol traffic (SSH, DHCP, DNS, RDP) using Wireshark.
Part 1: Create Virtual Machines
Log in to Azure Portal.
Create a Resource Group:
Navigate to "Resource Groups" and click "Create."
Provide a name for your Resource Group and select a region.
Click "Review + Create," then "Create."
image

Create a Windows 10 Virtual Machine:
Navigate to "Virtual Machines" and click "Create."
Select the Resource Group you just created.
Configure the Virtual Machine:
OS: Windows 10
Create username and password
Head to the Networking section, then create a new virtual network titled "Lab2-vnet"
Complete the setup and deploy the VM.
image

image

image

image

Create a Linux (Ubuntu) Virtual Machine:
Navigate to "Virtual Machines" and click "Create."
Select the same Resource Group and Virtual Network used for the Windows 10 VM.
Configure the Virtual Machine:
OS: Ubuntu Server 24.04
Authentication: Username/Password.
Ensure both VMs are in the same Virtual Network and Subnet as the Windows 10 VM.
Complete the setup and deploy the VM.
image

image

image

image

Part 2: Observe ICMP Traffic
Use Microsoft Remote Desktop to connect to your Windows 10 Virtual Machine (if on Mac, install the client first).
Install Wireshark on the Windows 10 VM:
Download and install Wireshark from https://www.wireshark.org/.
Open Wireshark and start a packet capture.
Filter for ICMP traffic in Wireshark.
Retrieve the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM:
Open Command Prompt or PowerShell and run: ping <Ubuntu VM Private IP>.
Observe the ping requests and replies in Wireshark.
From the Windows 10 VM, ping a public website (e.g., www.google.com) and observe the ICMP traffic in Wireshark.
image

image

image
Part 3: Configure a Firewall (Network Security Group)
Observe ICMP Traffic with Firewall Changes
Initiate a continuous ping from your Windows 10 VM to the Ubuntu VM:
Command: ping <Ubuntu VM Private IP> -t.
Open the Network Security Group associated with the Ubuntu VM.
Disable inbound ICMP traffic in the Network Security Group.
Observe the ICMP traffic in Wireshark and the command line Ping activity (should stop).
Re-enable ICMP traffic in the Network Security Group.
Observe the ICMP traffic in Wireshark and the command line Ping activity (should resume).
Stop the ping activity.
image

image

image

image

image

image

image

Observe SSH Traffic
In Wireshark, start a new packet capture and filter for SSH traffic.
From the Windows 10 VM, SSH into the Ubuntu VM:
Command: ssh <username>@<Ubuntu VM Private IP>.
Enter the password when prompted (the password will not be visible).
Type commands within the SSH session and observe the SSH traffic in Wireshark.
Exit the SSH session: exit.
image

image

image

Observe DHCP Traffic
In Wireshark, filter for DHCP traffic.
From the Windows 10 VM, issue a new IP address:
Open PowerShell as admin and run: ipconfig /renew.
Observe the DHCP traffic in Wireshark.
In this case our vm maintains the same IP. If we were to release our IP address (ipconfig /release) then renew it (ipconfig /renew) we would see the complete DHCP cycle in wireshark.
image

Observing the full DHCP Cycle

Open notepad and type the release and renew commands image

Choose a location to save the program. Here we chose c:\program data

You can name the file whatever you want but make sure to save it as a .bat file (this turns it into a simple script that we can run)

Make sure to change the 'save as type' to all files image

Change the directory that PowerShell is accessing to the location of the your .bat file by entering 'cd c:(filelocation)'

In this case I will change the directory to c:\programdata image

Run the DHCP.bat script that was just created by entering '.\dhcp.bat'

This program should temporarily disconnect you from the vm because the IPv4 address is being released and renewed image

Observe the Release - Discover - Offer - Request - Acknowledge steps in the DHCP process image

Observe DNS Traffic
In Wireshark, filter for DNS traffic.
From the Windows 10 VM, use nslookup to find IP addresses for websites:
Example: nslookup www.bing.com.
Observe the DNS traffic in Wireshark.
image

Observe RDP Traffic
In Wireshark, filter for RDP traffic:
Use the filter: tcp.port == 3389.
Observe the continuous RDP traffic between the Windows 10 VM and your local machine.
image

About
No description, website, or topics provided.
Resources
 Readme
 Activity
Stars
 0 stars
Watchers
 1 watching
Forks
 0 forks
Report repository
Releases
No releases published
Packages
No packages published
Footer
© 2025 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Statu
