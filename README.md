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

- Create a Resource Group: Organize all related Azure resources (VMs, networking, etc.) in a single group.
- Create a Virtual Network: Set up a dedicated network for your AD environment.
- Deploy a Domain Controller VM: Create a Windows Server virtual machine to act as the domain controller.
- Set Static Private IP for DC: Assign a static private IP to the domain controller so its address doesn’t change.
- Deploy a Client VM: Create a Windows 10 (or similar) VM to act as a domain-joined client.
- Configure DNS: Set the client’s DNS server to the domain controller’s private IP address.
- Disable Firewall (for lab testing): Temporarily disable Windows Firewall on the domain controller to allow necessary traffic.
- Verify Network Connectivity: Ensure the client can ping the DC’s private IP.
- Check DNS Settings: Confirm the client uses the DC for DNS lookups.
- Install AD Domain Services on the Domain Controller
- Log into your Windows Server (DC1).
- Promote the Server to a Domain Controller.
- Restart the Server.
- Log in with Domain Credentials.
- Create Organizational Units (OUs).
- Create Domain Admin User.
- Join Client Machine to the Domain. 
- Log into your Windows 10 client.
- Move Client to the Proper OU.

<h2>Deployment and Configuration Steps</h2>

<img width="80%" height="80%" alt="1" src="https://github.com/user-attachments/assets/794092de-b5c8-4315-b957-4b0e44bdd957" />

- Create a new resource group with these specifications.
</p>
<br />

<img width="80%" height="80%" alt="2" src="https://github.com/user-attachments/assets/420b4689-74b9-41ec-93bc-dadb4fac8b76" />

- Create a Virtual Network with these specifications.
</p>
<br />

<img width="80%" height="80%" alt="3" src="https://github.com/user-attachments/assets/3fb7b126-2956-49b1-9a69-c233f3836e81" />

- Create a new virtual machine for the domain controller with these specifications.
- Make sure the image is set to "Windows Server 2022".
</p>
<br />

<img width="80%" height="80%" alt="4" src="https://github.com/user-attachments/assets/36d33ab5-2340-4e72-84b2-8d7759b23dd0" />

- Make sure under "Size" you choose something that has at least 2 vcpus.
- Choose a username and password.
- Click create.
</p>
<br />

<img width="80%" height="80%" alt="5" src="https://github.com/user-attachments/assets/48398cad-f186-40de-850e-ea8eb5e18339" />

- Create another virtual machine for the domain-joined client with these specifications.
- Make sure the image is set to "Windows 10".
</p>
<br />

<img width="80%" height="80%" alt="6" src="https://github.com/user-attachments/assets/adf300f3-6489-4b8e-9e6b-5ad18dc4ee9a" />

- Make sure under "Size" you choose something with at least 2 vcpus.
- Choose a username and password.
- Click create.
</p>
<br />

<img width="80%" height="80%" alt="7" src="https://github.com/user-attachments/assets/e35e6b8a-f087-4e96-88ca-3e36b6934722" />

- Now you should have two virtual machines up and running.
</p>
<br />

<img width="80%" height="80%" alt="8" src="https://github.com/user-attachments/assets/a64cd015-2b56-4303-b833-cf86c8711b3d" />

- Now we are going to set Domain Controller’s NIC Private IP address to be static.
- Click on dc-1 vm and then click "Network Settings".
- Click on "Network interface / IP configuration.
</p>
<br />

<img width="80%" height="80%" alt="9" src="https://github.com/user-attachments/assets/5d92052b-7cd0-4875-a948-1eeffe70d8db" />

- Click on "ipconfig1" and change the private IP address settings from "Dynamic" to "Static".
- Click Save.
</p>
<br />

<img width="80%" height="80%" alt="10" src="https://github.com/user-attachments/assets/297860f7-dfb9-43c6-9a67-465ce71c4a36" />

- Now we are going to log into the dc-1 VM and disable the Windows Firewall (for testing connectivity).
- Add the new PC in the Windows app.
</p>
<br />

<img width="80%" height="80%" alt="11" src="https://github.com/user-attachments/assets/61702b90-f868-4bcc-a1ba-4289aa56df47" />

- Log into the vm.
</p>
<br />

<img width="80%" height="80%" alt="12" src="https://github.com/user-attachments/assets/69094e36-a7eb-4cc7-a53e-bb2ebe791f4e" />

- Right click the start button and click "Run"
- Enter in this prompt.
</p>
<br />

<img width="80%" height="80%" alt="13" src="https://github.com/user-attachments/assets/62e6b208-5a76-4b19-a12a-c0918196ae91" />

- Click "Windows Defender Firewall Properties".
- Turn the Firewall state to "Off".
</p>
<br />

<img width="80%" height="80%" alt="14" src="https://github.com/user-attachments/assets/5a1b7d34-93c0-48fd-9002-059c690be3f2" />

- Now we are going to set Client-1’s DNS settings to DC-1’s Private IP address.
- Go to client-1 vm and click "Network Settings".
- Click "Network interface / IP configuration.
</p>
<br />

<img width="80%" height="80%" alt="15" src="https://github.com/user-attachments/assets/cf378703-c068-45b4-9d81-3d7f3be6b212" />

- On the left click "DNS servers".
-  Change the DNS servers from "inherit from virtual network" to "Custom".
-  Copy in DC-1's Private IP address.
-  Click "Save".
</p>
<br />

<img width="80%" height="80%" alt="16" src="https://github.com/user-attachments/assets/43bb6f9d-f6ec-4633-a6bc-e2ae68c93b13" />

- In the windows app add another pc with Client-1's IP address.
</p>
<br />

<img width="80%" height="80%" alt="17" src="https://github.com/user-attachments/assets/cd072fcb-689a-4979-94db-0a85b2bb3318" />

- Log into Client-1.
</p>
<br />

<img width="80%" height="80%" alt="18" src="https://github.com/user-attachments/assets/d0bf2d90-b6eb-4d25-b400-e4adb431de75" />

- From the start menu open Powershell.
</p>
<br />

<img width="80%" height="80%" alt="19" src="https://github.com/user-attachments/assets/d9a309d7-9dbc-4b6e-ab70-2e7bf47dd436" />

- Try to ping Dc-1's private IP address.
- You should get a response.
</p>
<br />

<img width="80%" height="80%" alt="20" src="https://github.com/user-attachments/assets/f62a67c5-a8b2-4557-b166-b5e827f32778" />

- Type in ipconfig /all.
- DNS server should show DC-1's private IP address.
</p>
<br />

<img width="80%" height="80%" alt="2" src="https://github.com/user-attachments/assets/420b4689-74b9-41ec-93bc-dadb4fac8b76" />

- Create a Virtual Network with these specifications.
</p>
<br />

<img width="80%" height="80%" alt="3" src="https://github.com/user-attachments/assets/3fb7b126-2956-49b1-9a69-c233f3836e81" />

- Create a new virtual machine with these specifications.
- Mkae sure the image is set to "Windows Server 2022".
</p>
<br />

<img width="80%" height="80%" alt="1" src="https://github.com/user-attachments/assets/794092de-b5c8-4315-b957-4b0e44bdd957" />

- Create a new resource group with these specifications.
</p>
<br />

<img width="80%" height="80%" alt="2" src="https://github.com/user-attachments/assets/420b4689-74b9-41ec-93bc-dadb4fac8b76" />

- Create a Virtual Network with these specifications.
</p>
<br />

<img width="80%" height="80%" alt="3" src="https://github.com/user-attachments/assets/3fb7b126-2956-49b1-9a69-c233f3836e81" />

- Create a new virtual machine with these specifications.
- Mkae sure the image is set to "Windows Server 2022".
</p>
<br />
