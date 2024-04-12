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

-<b>Create a new employee named "John Doe" (username:john_admin) with the same password, adding the account to "Domain Admins" Security Group</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/3ccb3d64-6c75-427d-920a-5f6ef1a38f07)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/e41a17fe-ad76-47ee-a186-a09040b28ccb)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/dfe743bd-7ad0-4580-927f-44ece9beda09)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/46e0c8bb-4efa-41f1-b90f-ed1a9c41a038)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/e4fdb2e7-2e92-4145-a940-1d64cfc2481a)

-<b>Log in as "mydomain.com\john_admin"</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/ef589a07-07fd-4693-b792-8401b7167237)

<h3>Join Client-1 to Domain (mydomain.com)</h3>
-<b>Set Client-1's DNS settings to DC's Private IP address</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/85192f67-bd9d-4121-b72b-a2ce4197f9e3)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/1120b0d9-70c5-4bec-921a-2a43f076537c)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/c68a79ae-8dd7-4db8-abd6-1a9750c7ed74)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/781da87b-1ee7-4439-a57a-5e836f81e67d)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/f118f2ae-7e0a-40a5-8b99-f9fc2c33c62c)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/d2f7ced1-2812-4d2b-a4e7-1c8d556c8628)

-<b>Note:If you still cant join the domain, then make sure that the domain controller is using its own private ip as its dns server</b>

-<b>Restart Client-1 and join it to the domain</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/ab0f4f5f-1d64-440f-9d69-b3a5cb710298)

-<b>Verify Client-1 shows up in Active Directory Users and Computers (ADUC)</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/2839a4fc-7667-4cc8-8c46-8bf46ab697d9)

<h3>Setup Remote Desktop for non-administrative users on Client-1</h3>
-<b>Log in as mydomain.com\john_admin on Client-1</b>
-<b>Enable Remote Desktop for domain users</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/9163fe43-cfa5-4a38-b24e-b98307a19c6d)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/dd070f2a-8994-46a8-bb1c-b1b02dffded5)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/7c3646c6-08e7-4581-b820-785e13391dd7)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/0625f805-8d92-44fc-94f9-4bb35691e8e0)

<h3>Create Additional Users and Attempt Login on Client-1</h3>
-<b>Log in as john_admin on DC-1 and run PowerShell_ise as a admin(or the script wont work) to create additional users using a provided script(https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)</b>

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/03d14dbf-28e5-4ef2-a630-6b3a18d285cb)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/4361f918-8826-4ad6-8940-a7505cd87856)

- <b>Click on raw and copy the script and paste it in Powershell</b>
![image](https://github.com/Postmoedev/configure-ad/assets/150564271/19c7b38c-6dfd-4bf0-8f26-b515835bfd6f)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/a3af4a71-91b3-4841-a911-0abc2f3ec8be)

-<b>Run the script and observe the accounts being created</b>
![image](https://github.com/Postmoedev/configure-ad/assets/150564271/602ec3f9-85ce-473a-a918-e3eae5f84307)

-<b>When finished, open ADUC and observe the accounts in the appropriate OU
attempt to log into Client-1 with one of the accounts (take note of the password in the script)</b>
![image](https://github.com/Postmoedev/configure-ad/assets/150564271/8ff53946-5e1b-4c8b-8844-857f163c7002)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/3011daf4-85fe-4c62-a231-ded626eb3ef1)

![image](https://github.com/Postmoedev/configure-ad/assets/150564271/119758d5-ade8-4093-8f6f-d88dca301ee5)
