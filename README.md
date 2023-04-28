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

<p> 3) Install Active Directory<br>
3.1) Login to DC-1 and install Active Directory Domain Services<br>
  -Server Manager > Add Roles and Features > Install "Active Directory Domain Services"<br>
3.2) Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)<br>
3.3) Restart and then log back into DC-1 as user: mydomain.com\labuser<br>
</p>
<p>
<img src="https://i.imgur.com/vQrGoyY.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p> 4) Create an Admin and Normal User Account in AD<br>
4.1) In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”<br>
4.2) Create a new OU named “_ADMINS”<br>
4.3) Create a new employee named “Jane Doe” (same password) with the username of “jane_admin” under "_Admins" folder<br>
4.4) Add jane_admin to the “Domain Admins” Security Group
  -Right click Properties > Member Of > Add > <br>
4.5) Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”<br>
4.6) User jane_admin as your admin account from now on<br>
</p>
<p>
<img src="https://i.imgur.com/So9JzHs.png" height="50%" width="50%" alt="Disk Sanitization Steps"/><br>
<img src="https://i.imgur.com/5hzCMto.png" height="30%" width="30%" alt="Disk Sanitization Steps"/><br>
<img src="https://i.imgur.com/Hgnn9kC.png" height="70%" width="70%" alt="Disk Sanitization Steps"/><br>
<img src="https://i.imgur.com/tSHVqdw.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p> 5) Join Client-1 to your domain (mydomain.com)<br>
5.1) From the Azure Portal, set Client-1’s DNS settings to the DC-1’s Private IP address<br>
5.2) From the Azure Portal, restart Client-1<br>
5.3) Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the DC-1 (VM Will Restart)<br>
  -Right Click Start > System > Rename this PC > Change > Domain:<br>
5.4) Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain<br>
5.5) Create a new OU named “_CLIENTS” and drag Client-1 into there<br>
</p>
<p>
<img src="https://i.imgur.com/NMfi8SP.png" height="50%" width="50%" alt="Disk Sanitization Steps"/><br>
<img src="https://i.imgur.com/NHclC24.png" height="50%" width="50%" alt="Disk Sanitization Steps"/><br>
<img src="https://i.imgur.com/hCB35Z6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br>
</p>
<br />

<p>6) Setup Remote Desktop for non-administrative users on Client-1<br>
6.1) Log into Client-1 as mydomain.com\jane_admin and open system properties<br>
6.2) Click “Remote Desktop”<br>
6.3) Allow “domain users” access to remote desktop<br>
  - System > Remote Desktop > Select users that can remotely access this PC > Add > Domain Users
6.4) You can now log into Client-1 as a normal, non-administrative user now<br>
6.5) Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)<br>
</p>
<p>
<img src="https://i.imgur.com/0EJnwKr.png" height="40%" width="40%" alt="Disk Sanitization Steps"/><br>
<img src="https://i.imgur.com/2VVE0Nr.png" height="40%" width="40%" alt="Disk Sanitization Steps"/><br>
</p>
<br />

<p>7) Create a bunch of additional users and attempt to log into client-1 with one of the users<br>
7.1) Login to DC-1 as jane_admin<br>
7.2) Open PowerShell_ise as an administrator<br>
7.3) Create a new File and paste the contents of the script into it (https://github.com/mongvang/generate-names/edit/main/README.md)<br>
7.4) Run the script and observe the accounts being created<br>
7.5) When finished, open ADUC and observe the accounts in the appropriate OU<br>
7.6) Attempt to log into Client-1 with one of the accounts (take note of the password in the script)<br>
</p>
<p>
<img src="https://i.imgur.com/Yzpyl1z.png" height="40%" width="40%" alt="Disk Sanitization Steps"/><br>
<img src="https://i.imgur.com/IT0FhPX.png" height="60%" width="60%" alt="Disk Sanitization Steps"/><br>
</p>
<br />

Finish.
