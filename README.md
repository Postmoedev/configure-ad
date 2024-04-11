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
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resource Group and Virtual Machines 
- Ensure Connectivity between Client and Domain Controller
- Install Active Directory
- Create Admin and Normal User Account in AD
- Join Client-1 to Domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create Additional Users and Attempt Login on Client-1

<h2>Deployment and Configuration Steps</h2>

<h3>Setup Resources in Azure</h3>
-<b>Create a Domain Controller VM (Windows Server 2022) named "DC-1"</b>


-<b>Set Domain Controller’s NIC Private IP address to be static</b>


-<b>Create a VM named "Client-1" using the same Resource Group and Vnet as DC-1(Ensure both VMs are in the same Vnet)</b>


<h3>Ensure Connectivity between Client and Domain Controller</h3>
-<b>Ping DC-1's private IP address from Client-1</b>


-<b>Enable ICMPv4 in the local Windows Firewall on DC-1</b>


<h3>Install Active Directory</h3>
<b>Install Active Directory Domain Services on DC-1</b>


-<b>Promote DC-1 as a Domain Controller for a new forest (e.g., mydomain.com)</b>


-<b>Log in as user: mydomain.com\labuser after restart</b>


<h3>Create Admin and Normal User Account in AD</h3>
-<b>Create an Organizational Unit (OU) named "_EMPLOYEES" and "_ADMINS"</b>


-<b>Create a new employee named "John Doe" (username:john_admin) with the same password, adding her to "Domain Admins" Security Group</b>


-<b>Log in as "mydomain.com\john_admin"</b>


<h3>Join Client-1 to Domain (mydomain.com)</h3>
-<b>Set Client-1's DNS settings to DC's Private IP address</b>


-<b>Restart Client-1 and join it to the domain</b>


-<b>Verify Client-1 shows up in Active Directory Users and Computers (ADUC)</b>


<h3>Setup Remote Desktop for non-administrative users on Client-1</h3>
-<b>Log in as mydomain.com\john_admin on Client-1</b>


-<b>Enable Remote Desktop for domain users</b>


<h3>Create Additional Users and Attempt Login on Client-1</h3>
-<b>Log in as jane_admin on DC-1 and use PowerShell_ise to create additional users using a provided script(https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)</b>


-<b>Run the script and observe the accounts being created</b>


-<b>When finished, open ADUC and observe the accounts in the appropriate OU
attempt to log into Client-1 with one of the accounts (take note of the password in the script)</b>
