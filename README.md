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

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/8a4a7f14-e7ef-4ddc-999c-f3655a517a84)

-<b>Set Domain Controller’s NIC Private IP address to be static</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/b84a171a-4d78-49b3-91b0-7e4b23767a6f)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/45001ee7-4348-4221-ac5c-e43bbb7dd9b9)

-<b>Create a VM named "Client-1" using the same Resource Group and Vnet as DC-1(Ensure both VMs are in the same Vnet)</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/639b1e64-5847-4de9-819c-117c58d313fd)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/fe2e086a-c552-4ff6-94f3-99c4b420b7a5)

<h3>Ensure Connectivity between Client and Domain Controller</h3>
-<b>Ping DC-1's private IP address from Client-1</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/7d6fb2bd-c254-4de3-8f80-0e362666b83e)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/d7a38947-7698-4280-b46c-5f824d187e71)

-<b>Enable ICMPv4 in the local Windows Firewall on DC-1</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/9163d4c2-93bf-4a38-b817-86b20b819228)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/e042a371-4be3-4531-a656-bdfe9d03c313)

<h3>Install Active Directory</h3>
<b>Install Active Directory Domain Services on DC-1</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/af1630bb-249d-4088-af1b-b1fa0cd0fd23)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/5ec68181-8139-4e99-a36b-0df37fa48f2d)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/8fe22255-b9ee-4fda-95b7-bc3c4257bc4e)

-<b>Promote DC-1 as a Domain Controller for a new forest (e.g., mydomain.com)</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/97c7e09b-8fbf-4d51-8dbc-3437eafd367f)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/e101afaa-fdb7-405f-b88d-4c5b8e5384e5)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/0cf9309a-9801-40a7-80be-3520b7ce7c5d)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/24c391a4-a5d1-49b1-bc34-7ad87348d099)

-<b>Log in as user: mydomain.com\labuser after restart</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/24c81130-1cd7-4517-a75c-61bb2466737d)

<h3>Create Admin and Normal User Account in AD</h3>
-<b>Create an Organizational Unit (OU) named "_EMPLOYEES" and "_ADMINS"</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/566391c5-c0e1-4e51-ae8f-0f61c4e35ebb)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/938adaa8-74b1-45c1-8e79-94521ad0483c)

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
