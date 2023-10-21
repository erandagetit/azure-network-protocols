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

<h2>High-Level Steps</h2>

-   Create some sample files shares with various permission
1. Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
2. Connect/log into Client-1 as a normal user (mydomain\<someuser>)
3. On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
4. Set the following permissions (share the folder) for the “Domain Users” group:

  
-   Attempt to access files shares as a normal user
1. On Client-1, navigate to the shared folder (start, run, \\dc-1)
2. Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in? Does it make sense?

-   Create an “ACCOUNTANTS” Security Group, assign permissions, an test access
1. Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
2. On the “accounting” folder you created earlier, set the following permissions:
  


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/jDL8ab6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Created files with various permissions.
</p>
<br />

<p>
<img src="https://i.imgur.com/sWd1gwX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Navigating through folders i just created.
</p>
<br />

<p>
<img src="https://i.imgur.com/SIxRUAH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Created Accountants with security group and setup permissions.
</p>
<br />
