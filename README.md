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
1. Create Virtual Machines in Azure.
2. Observe ICMP traffic between Virtual Machines using Wireshark.
3. Configure a Firewall (Network Security Group) and analyze its impact on network traffic.
4. Observe various protocol traffic (SSH, DHCP, DNS, RDP) using Wireshark.

Part 1: Create Virtual Machines
1. Log in to Azure Portal.
2. Create a Resource Group:
 - Navigate to "Resource Groups" and click "Create."
 - Provide a name for your Resource Group and select a region.
 - Click "Review + Create," then "Create."
<img src="https://i.imgur.com/80dflGm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

3. Create a Windows 10 Virtual Machine:
 - Navigate to "Virtual Machines" and click "Create."
 - Select the Resource Group you just created.
 - Configure the Virtual Machine:
  - OS: Windows 10
  - Create username and password
  - Head to the Networking section, then create a new virtual network titled "Lab2-vnet"
- Complete the setup and deploy the VM.
<img src="https://i.imgur.com/OcB5To7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/xZ3RWZ7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/jw68F2j.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/cG7egU6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Create a Linux (Ubuntu) Virtual Machine:
 - Navigate to "Virtual Machines" and click "Create."
 - Select the same Resource Group and Virtual Network used for the Windows 10 VM.
 - Configure the Virtual Machine:
  - OS: Ubuntu Server 24.04
  - Authentication: Username/Password.
 - Ensure both VMs are in the same Virtual Network and Subnet as the Windows 10 VM.
 - Complete the setup and deploy the VM.
<img src="https://i.imgur.com/d2xLa96.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/ZrMQmr6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/dBLiQZR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/juYmQgB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Part 2: Observe ICMP Traffic
1. Use Microsoft Remote Desktop to connect to your Windows 10 Virtual Machine (if on Mac, install the client first).
2. Install Wireshark on the Windows 10 VM:
 - Download and install Wireshark from https://www.wireshark.org/.
3. Open Wireshark and start a packet capture.
4. Filter for ICMP traffic in Wireshark.
5. Retrieve the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM:
 - Open Command Prompt or PowerShell and run: ping <Ubuntu VM Private IP>.
 - Observe the ping requests and replies in Wireshark.
6. From the Windows 10 VM, ping a public website (e.g., www.google.com) and observe the ICMP traffic in Wireshark.
<img src="https://i.imgur.com/7h4ljzy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/WyUYD91.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/lng3zxn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Part 3: Configure a Firewall (Network Security Group)

Observe ICMP Traffic with Firewall Changes

1. Initiate a continuous ping from your Windows 10 VM to the Ubuntu VM:
 - Command: ping <Ubuntu VM Private IP> -t.
2. Open the Network Security Group associated with the Ubuntu VM.
3. Disable inbound ICMP traffic in the Network Security Group.
4. Observe the ICMP traffic in Wireshark and the command line Ping activity (should stop).
5. Re-enable ICMP traffic in the Network Security Group.
6. Observe the ICMP traffic in Wireshark and the command line Ping activity (should resume).
7. Stop the ping activity.
<img src="https://i.imgur.com/PkDdLb0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/crq8ePa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/sW3wVKx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/hD9GxKO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/dj5aZ7b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/cpbB90D.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/6cESkod.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Observe SSH Traffic

1. In Wireshark, start a new packet capture and filter for SSH traffic.
2. From the Windows 10 VM, SSH into the Ubuntu VM:
  - Command: ssh <username>@<Ubuntu VM Private IP>.
  - Enter the password when prompted (the password will not be visible).
3. Type commands within the SSH session and observe the SSH traffic in Wireshark.
4. Exit the SSH session: exit.

<img src="https://i.imgur.com/t8pqs0n.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/KoiWbbv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/uJ3wnnA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Observe DHCP Traffic

1. In Wireshark, filter for DHCP traffic.
2. From the Windows 10 VM, issue a new IP address:
  - Open PowerShell as admin and run: ipconfig /renew.
3. Observe the DHCP traffic in Wireshark.
4. In this case our vm maintains the same IP. If we were to release our IP address
(ipconfig /release) then renew it (ipconfig /renew) we would see the complete DHCP cycle in wireshark.

<img src="https://i.imgur.com/EARKYwR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Observing the full DHCP Cycle

Open notepad and type the release and renew commands image
<img src="https://i.imgur.com/FePDY8l.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Choose a location to save the program. Here we chose c:\program data

- You can name the file whatever you want but make sure to save it as a .bat file (this turns it into a simple script that we can run)

- Make sure to change the 'save as type' to all files image
<img src="https://i.imgur.com/z6qsP2e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Change the directory that PowerShell is accessing to the location of the your .bat file by entering 'cd c:(filelocation)'

- In this case I will change the directory to c:\programdata image
<img src="https://i.imgur.com/WqI5uo2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Run the DHCP.bat script that was just created by entering '.\dhcp.bat'

- This program should temporarily disconnect you from the vm because the IPv4 address is being released and renewed image
<img src="https://i.imgur.com/vNhGono.png " height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Observe the Release - Discover - Offer - Request - Acknowledge steps in the DHCP process image
<img src="https://i.imgur.com/6oluNEM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Observe DNS Traffic

1. In Wireshark, filter for DNS traffic.
2. From the Windows 10 VM, use nslookup to find IP addresses for websites:
  - Example: nslookup www.bing.com.
3. Observe the DNS traffic in Wireshark.
<img src="https://i.imgur.com/RDCsN4k.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Observe RDP Traffic

1. In Wireshark, filter for RDP traffic:
  - Use the filter: tcp.port == 3389.
2. Observe the continuous RDP traffic between the Windows 10 VM and your local machine.
<img src="https://i.imgur.com/9eu9vAU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


