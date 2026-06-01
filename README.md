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
  
<p>
<img <img width="618" height="638" alt="Virtual Network Creation" src="https://github.com/user-attachments/assets/6f7f9063-4f82-444c-9bfc-ba6d523e85a5" />
</p>

<br />

<h1><a href="https://github.com/darwyn123/azure-vm">Create 2 Microsoft Azure Virtual Machine</a></h1>

- Azure Virtual Machine 1:
   - Resource Group: New one you created (Active-Directory-RG)
   - Virtual Machine Name: "DC-1" running Windows Server 2025 Datacenter Azure Edition - x64 Gen2
   - Virtual Network: New one you created (Active-Directory-VNet)
  
<p>
<img <img width="618" height="638" alt="DC-1 VM Creation Part 1" src="https://github.com/user-attachments/assets/d0848ba9-b577-4d80-a70b-b287e82e9fdc" />
</p>
<p>
<img <img width="618" height="638" alt="DC-1 VM Creation 2" src="https://github.com/user-attachments/assets/d7224a94-5b5d-47d2-bbb0-1d5afce4dc21" />
</p>

<br />

- Azure Virtual Machine 2:
   - Resource Group: New one you created (Active-Directory-RG)
   - Virtual Machine Name: "Client-1" running Windows 10 Pro, version 22H2 - x64 Gen2
   - Virtual Network: New one you created (Active-Directory-VNet)
  
<p>
<img <img width="618" height="638" alt="Client-1 VM Creation 1" src="https://github.com/user-attachments/assets/915c0fa6-6aba-4ad1-9ea3-221ac5c45d1f" />
</p>
<p>
<img <img width="618" height="638" alt="Client-1 VM Creation 2" src="https://github.com/user-attachments/assets/cdbd68f0-839d-471a-983c-c679d6025c9e" />
</p>

<br />

<h2>Configure static IP address on Domain Controller 1 (DC-1)</h2>

- Head over to Virtual Machine section in Azure Portal, and click on DC-1 to open Virtual Machine.
- Navigate to Network -> Network Settings -> The name of the network interface (Under Network interface / IP configuration) in this case it's "dc-1234 (primary) / ipconfig1 (primary)" -> ipconfig1 (Under Name)

<p>
<img <img width="764" height="420" alt="NIC (Interface)" src="https://github.com/user-attachments/assets/229c2c2a-1816-44ce-abe3-c970e2cb9b64" />
</p>
<p>
<img <img width="938" height="310" alt="Ipconfig1(NIC)" src="https://github.com/user-attachments/assets/c5cc79a5-8204-4048-ac4d-5919b589aed2" />
</p>

- Change Dynamic to Static
- Click "Save"

<p>
<img <img width="1229" height="560" alt="Dynamic to Static" src="https://github.com/user-attachments/assets/bd677cd9-f5ca-4783-9c74-43372fc80679" />
</p>

<br />

<h2>For Testing Purpose Disable the Firewall</h2>

- RDP into DC-1 Virtual Machine 
- Minimize the Server Manager window for now.
- Use windows search and type wf.msc to open "Windows Defender Firewall"
- Click on "Windows Defender Firewall Properties"
- Domain Profile Tap:
    - Put Firewall state: Off
  
<p>
<img <img width="901" height="516" alt="Domain Profile" src="https://github.com/user-attachments/assets/c2c5de33-f81c-41d5-9511-6fc143b9e735" />
</p>

- Private Profile Tap:
    - Put Firewall state: Off
  
<p>
<img <img width="901" height="516" alt="Private Profile" src="https://github.com/user-attachments/assets/e7a50b62-74ae-4b41-afc1-f776ec60319a" />
</p>

- Public Profile Tap:
    - Put Firewall state: Off
  
<p>
<img <img width="901" height="516" alt="Public Profile" src="https://github.com/user-attachments/assets/6d880a45-561a-457f-b13b-df237be4bc68" />
</p>

- Click Apply -> OK 

<br />

<h2>Configure DNS settings on Client-1</h2>

- Open DC-1 Virtual Machine in Azure Portal, and copy DC-1 Private IP address.

<p>
<img <img width="1070" height="579" alt="DC-1 IP Address" src="https://github.com/user-attachments/assets/fd842528-61a3-40ff-8e45-ddd4fc41be34" />
</p>

- Than Open Client-1 Virtual Machine in Azure Portal, navigate to Network -> Network Settings -> The name of the network interface (Under Network interface / IP configuration) in this case it's "client-1741 (primary) / ipconfig1 (primary)" -> Settings -> DNS servers
- Click on "Custom"
- Under DNS server paste DC-1 Private IP Address
- Click Save

<p>
<img <img width="1070" height="579" alt="Client-1 Nic" src="https://github.com/user-attachments/assets/9ec967b6-a173-4ffa-962b-cc6157af73c8" />
</p>
<p>
<img <img width="575" height="579" alt="DNS server paste ip address" src="https://github.com/user-attachments/assets/cd9e546e-0fe7-4e6c-b1e3-1df106788e40" />
</p>

- From Azure Portal, restart Client-1 Virtual Machine
    - Head over to Virtual Machine section in Azure Portal, check box next to Client-1 Virtual Machine and click Restart

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p>

- RDP into Client-1

<p>
<img <img width="962" height="602" alt="RDP Client-1" src="https://github.com/user-attachments/assets/d79b43c1-d2ec-4ff1-88d0-577b2d8f9910" />
</p>

- Test connection:
  - Open Command Prompt
  - Ping DC-1's IP (ex: ping 10.0.1.4)
  - Verify response

<p>
<img <img width="956" height="527" alt="Test Ping " src="https://github.com/user-attachments/assets/2a8cc1c1-8b12-4fa2-9d43-0ec0c5aeb99f" />
</p>

<br />

<h2>Install Active Directory on DC-1</h2>

- RDP into DC-1 Virtual Machine
- Open Server Manager
- Click on Add Roles and Features

<p>
<img <img width="962" height="603" alt="DC-1 RDP" src="https://github.com/user-attachments/assets/3d4d691a-7bfe-4bee-99b6-092013189420" />
</p>
<p>
<img <img width="1440" height="832" alt="Server Manager Add Roles" src="https://github.com/user-attachments/assets/33b894ce-605b-4fe3-98a5-e69cd588c9c4" />
</p>

- Select "Next" 3 times to get to Server Roles -> Check box on "Active Directory Domain Services" to enable -> Add Features -> Select "Next" 3 times again -> Check box on "Restart the destination server automatically if required" -> Yes -> Install
- Once installation is finish, click "Close"

<p>
<img <img width="787" height="556" alt="ACTive Directoy" src="https://github.com/user-attachments/assets/b47e602b-dd29-41c0-87ad-2da03ba840c6" />
</p>
<p>
<img <img width="787" height="556" alt="Install Direct" src="https://github.com/user-attachments/assets/9610bfe5-00f5-434d-91ec-3fbc5382cd30" />
</p>
<p>
<img <img width="787" height="556" alt="Install Complete" src="https://github.com/user-attachments/assets/b8dcebb8-7c97-4f73-bc91-1bad4fec1c1b" />
</p>

- In the top-right of the Server Manager window:
    - Click the flag icon with a warning notification
    - Select "Promote this server to a domain controller"
      
<p>
<img <img width="1208" height="467" alt="Promote Directory" src="https://github.com/user-attachments/assets/b939ef05-5c3b-4a68-9c4e-e52bde1e9383" />
</p>

- In the Active Directory Domain Services Configuration Wizard:
    - On "Deployment Configuration" tab:
        - Check Box "Add a new forest"
        - In Root domain name: Enter "mydomain.com"
        - Click "Next"     
     
<p>
<img <img width="767" height="570" alt="Forest mydomain com" src="https://github.com/user-attachments/assets/56133906-0fbd-4de9-b613-47ef534e2c65" />
</p>

- On "Domain Controller Options" tab:
    - Set a secure password in both fields
    - Click "Next"

<p>
<img <img width="767" height="570" alt="Secure Directory Password" src="https://github.com/user-attachments/assets/2eaeff4a-465e-4e71-857c-e19e8973e000" />
</p>

- On "DNS Options" tab:
    - Ensure Check box "Create DNS delegation" is unchecked
    - Select "Next" 4 times -> After verifying Prerequisities click "Install" 

<p>
<img <img width="767" height="570" alt="Uncheck box" src="https://github.com/user-attachments/assets/3514774e-6502-4fe4-bda1-5435c326ae6f" />
</p>
<p>
<img <img width="767" height="570" alt="Install after prev" src="https://github.com/user-attachments/assets/11e95e58-1bd6-4905-aff8-d6ca99dc24ca" />
</p>

- Server will Restart:
    - You'll get signed out
    - RDP back into DC-1 using "mydomain.com\" added before your username (ex: mydomain.com\azureuser)
 
<p>
<img <img width="1172" height="717" alt="Login as mydomain" src="https://github.com/user-attachments/assets/738ebd30-3574-4e43-96b9-2afc8a31a07b" />
</p>
<p>
<img <img width="921" height="601" alt="DC-1 Login mydomain com" src="https://github.com/user-attachments/assets/af772184-9af5-497c-af6a-4eb039a62ea8" />
</p>


<br />

<h2>Add Organizational Units for Employees & Admins</h2>

- Open Start Menu -> Windows Administrative Tools -> Active Directory Users and Computers

<p>
<img <img width="1127" height="592" alt="Windows Active Directory" src="https://github.com/user-attachments/assets/8c0a7884-fe78-42d6-a15f-9635b80bef21" />
</p>

- Create Organizational Units:
  - Right click "mydomain.com" > New > Organizational Unit
 
<p>
<img <img width="755" height="531" alt="Right Click Domain" src="https://github.com/user-attachments/assets/28287ab9-424e-4317-adf9-720d7d8f0f22" />
</p>
 
  - Name field: "_EMPLOYEES"
  - Click OK

<p>
<img <img width="755" height="531" alt="_EMPLOYEES" src="https://github.com/user-attachments/assets/677f9960-11a2-41e3-9799-17714befa511" />
</p>
<p>
<img <img width="755" height="531" alt="_EMPLOYEE 2" src="https://github.com/user-attachments/assets/8da8534b-4225-4a88-b069-293586906f23" />
</p>

  - Right click "mydomain.com" > New > Organizational Unit
  - Name field: "_ADMINS"
  - Click OK

<p>
<img <img width="755" height="531" alt="_ADMINS" src="https://github.com/user-attachments/assets/08b7bffb-94b3-4d72-9a98-ae4516b300ef" />
</p>


<br />

<h2>Adding a new Admin (Jane Doe)</h2>

- Right click on _ADMINS > New > User
- First name: Jane
- Last name: Doe
- User logon name: Jane_admin
- Click Next

<p>
<img <img width="755" height="531" alt="User Admin" src="https://github.com/user-attachments/assets/d722d978-0349-491d-a3fa-25faaca0f038" />
</p>
<p>
<img <img width="755" height="531" alt="Jane Doe" src="https://github.com/user-attachments/assets/5770dccf-7f0c-4570-a091-ba51e3840774" />
</p>

- Set password:
  - Enter secure password
  - Uncheck Box "User must change password at next logon"
  - Check Box "Password never expires"
  - Click Next -> Finish

<p>
<img <img width="755" height="531" alt="Password Admin" src="https://github.com/user-attachments/assets/02fbf7b5-6e3f-4312-a391-7299337efeed" />
</p>
<p>
<img <img width="755" height="531" alt="Finish Jane Doe" src="https://github.com/user-attachments/assets/535b82e5-b076-4ac9-8629-ed5aa1851a73" />
</p>

- Add Jane Doe to Domain Admins:
  - Right click Jane Doe -> Properties
  - Navigate to "Member of" tab
  - Click Add...

<p>
<img <img width="755" height="531" alt="Jane Doe Properties" src="https://github.com/user-attachments/assets/d038550e-e880-4d55-8c89-ee52375a46d9" />
</p>


  - Under "Enter the object names to select:"
    - Enter "domain admins"
  - Click Check Names > OK
  - Click Apply > OK

<p>
<img <img width="755" height="531" alt="Domain Name Check Name" src="https://github.com/user-attachments/assets/11cd8792-d1eb-404e-a5c5-274cb06709bc" />
</p>


- Log out and log back in as Jane Doe

<p>
<img <img width="839" height="630" alt="Jane Doe Login" src="https://github.com/user-attachments/assets/3606af88-3718-4f74-a6a9-4ca29e754cbf" />
</p>
<p>
<img <img width="839" height="630" alt="Jane Doe Login 2" src="https://github.com/user-attachments/assets/09fc672c-9a01-404e-8237-54d5bcaeb271" />
</p>

<br />

<h2>Join Client-1 to your Domain(mydomain.com)</h2>

- RDP to "Client-1"

<p>
<img <img width="848" height="617" alt="Client-1 RDP" src="https://github.com/user-attachments/assets/d810679d-9efe-4ab7-aea8-021b29512925" />
</p>
<p>
<img <img width="848" height="617" alt="Client-1 Login 2" src="https://github.com/user-attachments/assets/5c301575-9890-44a6-acf2-014c62208142" />
</p>

- Right click Start Menu -> Navigate to System -> About -> Rename this PC (advanced) -> Change...

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p>

- Under Member of: Click "Domain"
  - Enter "mydomain.com"
  - Click OK

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p>

- Enter credentials for Jane Doe Admin: "mydomain.com\Jane_admin"

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p>

- Restart Client-1

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p>

- Verify on DC-1:
  - Open Start Menu -> Windows Administrative Tools -> Active Directory Users and Computers
  - Expand mydomain.com > Computers
  - Verify Client-1 is listed

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p>

<br />

<h2>Setup Remote Desktop for non-administrative users on Client-1</h2>

- On Client-1 (as Jane_admin):
  - Right click Start Menu -> Navigate to System -> Remote Desktop
  
<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p>

  - Click "Select users that can remotely access this PC" -> Add...
  - Under "Enter the object names to select:"
    - Enter "domain users"
  - Click Check Names -> OK -> OK

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p>
<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p> 


<br />

<h2>Bulk create Active Directory with script and test</h2>

- On DC-1 (as Jane_admin):
  - Open PowerShell ISE
  - Click File > New
  - In the Untitled1.ps1 text box, write your own or paste this bulk user creation script
    
<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p> 

  - Click green Run Script button
  - Click red Stop Operation when desired users created

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p> 

- Verify users:
  - Check Active Directory Users and Computers
  - Look in _EMPLOYEES folder

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p> 


<br />

<h2>Testing a Random Newly Created User</h2>

- Attempt to RDP into Client-1 using one of the newly created Active Directory user credentials

<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p> 
<p>
<img <img width="1054" height="579" alt="Client-1 Restart" src="https://github.com/user-attachments/assets/8d9c73f5-560b-45d9-81c5-a368fe219287" />
</p> 

<br />








  


