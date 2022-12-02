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


<h2>Deployment and Configuration Steps</h2>

<p>
</p>
<p>
For this lab, you will create two Virtual machines in the same virtual network. One will be designated as Domain Controller, the other shall be the client machine. The domain controller will be changed to a static IP because it is offering Active Directory services to the client machine. The client machine will be joined to the domain. From there, you will be able to control the DNS settings on the client machine. The client machine will use the domain controller as its own DNS server. 
</p>
<br />

<p>
<img src="https://i.imgur.com/d22FHIm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The Domain controller or DC-1 is required to have a static Private IP Address as mentioned in the above section because it is offering Active Directory services. Client one will connect to DC-1 to ensure connectivity. You will then attempt to ping DC-1 from Client-1. Initially the ping will not work properly. You will need to enable ICMPv4 on the local firewall via DC-1. After said configuration have been made, the reattempt on the ping between the two virtual machines will be successful.
</p>
<br />

<p>
<img src="https://i.imgur.com/HvZBWzc.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/1lrrGPw.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
You will then need to log back into DC-1 to install Active Directory Domain Serivces. Setup a new forest as "mydomain.com". Reestart and then log back into DC-1 as user: "mydomain.com\labuser".
</p>
<img src="https://i.imgur.com/cGjvRke.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
</p>
Now you can start creating Organizational Units (OU). First, in Active Directory users and computers, create an OU named _EMPLOYEES. Create another OU named _ADMINS. To do so, right click on the domain area. Select new then Organizational Unit and fill out the required field. Click inside of your OU and right click, select new, select user and fill out the required information. The username will be Jane Doe, she will be designated as an Admin so her username will be Jane_admin. Add Jane to the "Domain Admins" security group. Lastly, log out of the remote desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”

</p>
<img src="https://i.imgur.com/hL7g5Y5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
</p>
<img src="https://i.imgur.com/kcgvzdE.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
From now on you can use Jane_admin as your administrator account. Moving on, you will join Client-1 to the domain (mydomain.com) from the azure portal. You will change client-1's DNS settings to the DC's Private IP address. Afterwards restart Client-1 from within the Azure portal. The image below shows verification that client-1 is on the DC-1 DNS. 
</p>
<img src="https://i.imgur.com/jbrGTXW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
</p>
<p>
Next you will need to join Client-1 to the domain. To do so, navigate to your system settings and go to about. To the right of the screen, select "Rename this PC (advanced)". From there select to change the domain. Enter "mydomain.com". Enter your credentials from mydomain.com\labuser. Your computer will restart and then client-1 will be a part of the mydomain.com
</p>
<br />
  <p>
<img src="https://i.imgur.com/Ze0Em5e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Client-1 is now a part of the domain. You will now set up remote desktop for non-administrative users on Client-1. You will need to log into Client-1 as an admin and open system properties. Click on "Remote Desktop" and allow "domain users" access to remote desktop. After completing those steps you should be able to log into Client-1 as a normal user.
</p>
<br />

<p>
  <p>
<img src="https://i.imgur.com/SApOKiE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly to verify that users can Remote Desktop into Client-1 you will use a script that will generate thousands of users into the domain. The script will then be inputed powershell. Run the script and observe the accounts being created. After the users are created you will select one and Remote Desktop into Client-1.
</p>
<br />
<img src="https://i.imgur.com/EzWG8ug.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
<p>
 
