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

<!--<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4
-->
<h2>Deployment and Configuration Steps</h2>


<h2>Create a Resource Group</h2>

- Head over to the Azure Portal and sign in (create an account and start a subscription if needed).
- Now head over to the Resource Group section (in the search bar type "Resource Group") than click "Create".
- Resource Group name: "Active-Directory-RG"
- Click Review + create -> Create

<p>
<img <img width="618" height="638" alt="RG Creation" src="https://github.com/user-attachments/assets/26bc6b1c-8eca-43f7-ade7-cd71afa9c1e2" />
</p>

<b />

<h2>Create a Virtual Network</h2>

- Head over to the Virtual Network section (in the search bar type "Virtual Network") than click "Create".
- Resource Group name: "Active-Directory-RG"
- Virtual Network name: "Active-Directory-VNet"
- Make sure the region is the same region as Resource Group (Active-Directory-RG).
- Click Review + create -> Create
- Create a Virtual Network called " " 
   - Make sure the region is same as Resource Group (Active-Directory-RG).
  
<p>
<img <img width="618" height="638" alt="Virtual Network Creation" src="https://github.com/user-attachments/assets/6f7f9063-4f82-444c-9bfc-ba6d523e85a5" />
</p>

<b />

<p>
<img <img width="844" height="638" alt="DC-1 VM Creation" src="https://github.com/user-attachments/assets/b0376d29-f89a-4b03-b979-aa3d86fecf78" />
</p>

<br />

<h1><a href="https://github.com/darwyn123/azure-vm">Create 2 Microsoft Azure Virtual Machine</a></h1>

- Azure Virtual Machine 1:
   - Resource Group: New one you created (Active-Directory-RG)
   - Virtual Machine Name: "DC-1" running Windows Server 2025 Datacenter Azure Edition - x64 Gen2
   - Virtual Network: New one you created ( )
<p>
<img <img width="844" height="638" alt="DC-1 VM Creation" src="https://github.com/user-attachments/assets/b0376d29-f89a-4b03-b979-aa3d86fecf78" />
</p>

- Azure Virtual Machine 2:
   - Resource Group: New one you created (Active-Directory-RG)
   - Virtual Machine Name: "Client-1" running Windows 10 Pro, version 22H2 - x64 Gen2
   - Virtual Network: New one you created ( )
<p>
<img <img width="1143" height="665" alt="IIS_CGI" src="https://github.com/user-attachments/assets/0874ff79-26cb-4c5a-a03b-c99bb76a702b" />
</p>

<br />

<h2>Configure static IP address on Domain Controller 1 (DC-1)</h2>

- ..

<h2>Disable the Firewall</h2>

- ..

<h2>Configure DNS settings on Client-1</h2>

- ..

<h2>Install Active Directory on DC-1</h2>

- ..

<h2>Create a Domain Admin User with the Domain</h2>

- ..

<h2>Join Client-1 to your Domain(mydomain.com)</h2>

- ..


<h2>Setup Remote Desktop for non-administrative users on Client-1</h2>

- ..

<h2>Join Client-1 to your Domain(mydomain.com)</h2>

- ..

<h2>Add Organizational Units for Employees & Admins</h2>

- ..

<h2>Add a new admin named Jane Doe</h2>

- ..




  


