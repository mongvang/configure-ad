<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p> 1) Setup Resources in Azure<br>
-1.1) Create the Domain Controller VM (Windows Server 2022) named “DC-1”<br>
-1.2) Take note of the Resource Group and Virtual Network (Vnet) that get created at this time<br>
-1.3) Set Domain Controller’s NIC Private IP address to be static<br>
-1.4) Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.a<br>
-1.5) Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher)<br>
</p>
<p>
<img src="https://i.imgur.com/dBWpdp8.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p> 2) Ensure Connectivity between the client and Domain Controller<br>
2.1) Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)<br>
2.2) Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall<br>
-Windows Defender Firewall with Advanced Security > Inbound Rules > Click "Protocol" Tab > Enable Both "Core Networking Diagnostics ICMP"
2.3) Check back at Client-1 to see the ping succeed<br>
</p>
<p>
<img src="https://i.imgur.com/ZlMtJuh.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
