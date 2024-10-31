<h1>Active Directory Deployed in Azure</h1>

- <b>This tutorial outlines the implementation of Active Directory within Azure Virtual Machines</b>

<h2>Environments and Technologies Used</h2>

- <b>Microsoft Azure</b> 
- <b>Virtual Machines</b>
- <b>Remote Desktop Connection</b>
- <b>Active Directory Domain Services</b>
- <b>PowerShell</b>

<h2>Operating Systems</h2>

- <b>Windows 10</b>
- <b>Windows Server 2022</b>

<h2>Configuration Steps</h2>

- <b>Setup Resources in Azure</b>
- <b>Ensure Connectivity between the client and Domain Controller</b>
- <b>Install Active Directory Domain Services</b>
- <b>Create an Admin and Standard User Accounts </b>
- <b>Join Client-1 to your domain (mydomain.com)</b>
- <b>Setup Remote Desktop for non-administrative users on Client-1</b>
- <b>Create a bunch of additional users and attempt to log into client-1 with one of the users</b>

<h2>Installation Steps</h2>

![image](https://github.com/user-attachments/assets/6b97c3b9-dac8-4151-bea0-faaf55c4ebf8)
- <b>Create Windows Server 2022 virtual machine</b>
- <b>Resource Group: RG-Virtual</b>
- <b>Name: DC-1</b>

![image](https://github.com/user-attachments/assets/3c5a3be5-268e-470f-802f-7b915e80cedb)
- <b>Go to the network settings on the DC-1 virtual machine and select Network Interface</b>

![image](https://github.com/user-attachments/assets/413afffb-ef6c-45a5-8b8f-2c9f9427672a)
- <b>Go to Settings>IP Configurations</b>
- <b>Select ipconfig1 and choose Static for allocation</b>
- <b>Click save</b>

![image](https://github.com/user-attachments/assets/ca1b84e8-42a7-4587-8afd-6f026a3c8c57)
- <b>Create a Windows 10 virtual machine</b>
- <b>Name: Client-1
- <b>Make sure the virtual network is DC-1-Vnet</b>

![image](https://github.com/user-attachments/assets/2bfb4c72-18d7-40a3-af25-0a9a0e8ec4a8)
- <b>Remote Desktop to the Client-1 virtual machine</b>

![image](https://github.com/user-attachments/assets/86a92307-c3f0-4e01-9643-dcb7696f4cf7)
- <b>Open the command prompt and run as administrator</b>

![image](https://github.com/user-attachments/assets/e2cda258-6df1-490c-b4c3-f0d0aade7537)
- <b>Ping the private IP Address of DC-1 virtual machine from the Client-1 virtual machine</b>

![image](https://github.com/user-attachments/assets/d5aa366b-a1fa-41f7-9373-a503f0f6ecd6)
- <b>Remote Desktop to DC-1 virtual machine</b>

![image](https://github.com/user-attachments/assets/7c6865fc-e08f-4671-ad7a-f884e8eec74a)
- <b>Open Firewall and select inbound rules</b>
- <b>Enable both Core Networking Diagnostics - ICMPv4-in</b>

![image](https://github.com/user-attachments/assets/5ef3dd72-d022-4065-86cf-85db24b56ac5)
- <b>Both virtual machines have successfully communicated</b>

![image](https://github.com/user-attachments/assets/38ce8deb-c3dd-4828-a902-c02f05efb23d)
- <b>In the DC-1 virtual machine, go to server manager</b>
- <b>Click add roles and features</b>
- <b>Under server roles, select active directory domain services and click install<b>

![image](https://github.com/user-attachments/assets/03b61344-e3ec-4d80-a628-b9d1675348ef)
- <b>Click the flag on the top right and select promote this server to a domain controller</b>

![image](https://github.com/user-attachments/assets/794d90e6-a89e-49dc-8a46-cc9ec61f4696)
- <b>Select add a new forest</b>
- <b>Root domain name: mydomain.com</b>

![image](https://github.com/user-attachments/assets/2340faaf-f706-479f-99d6-52b289a41282)
- <b>Uncheck "create DNS delegation and click install</b>

![image](https://github.com/user-attachments/assets/8e04be38-1292-45e9-9008-01aff4ef2af7)
- <b>You will be disconnected from the DC-1 virtual machine. Log back in</b>
- <b>Click tools and select active directory users and computers</b>

![image](https://github.com/user-attachments/assets/74b43f07-7838-4f25-9f41-84608e8c6c31)
- <b>Right-click mydomain.com and select new>organizational unit</b>

![image](https://github.com/user-attachments/assets/0dda1f47-6973-4ed1-a8ac-aefbbe0b6e7d)
- <b>Name: _EMPLOYEES</b>

![image](https://github.com/user-attachments/assets/065e12c4-2123-4bd2-b58a-1f75e7ef37a3)
- <b>Create another organizational unit named _ADMINS</b>

![image](https://github.com/user-attachments/assets/caed2a3f-04e7-4c9b-9891-99f518868406)
- <b>Right click admins>new>user</b>

![image](https://github.com/user-attachments/assets/389c3c3d-48dd-4be2-8bc4-43993c6c668a)
- <b>First Name: Jane</b>
- <b>Last Name: Doe</b>
- <b>User logon name: jane_admin</b>

![image](https://github.com/user-attachments/assets/67c1e9c8-5a54-4df7-9ea5-19e6afa4fbbc)
- <b>Uncheck "user must change password at next logon"</b>
- <b>Check "password never expires</b>

![image](https://github.com/user-attachments/assets/297bdc7e-300f-4cbc-b348-79667dc9ca02)
- <b>Right click jane doe and select properties</b>
- <b>Click member of add select add</b>

![image](https://github.com/user-attachments/assets/d750da38-4f61-4968-a10a-f0afff86f7df)
- <b>Type domain and click check names</b>
- <b>Select domain admins</b>
- <b>Click ok and apply</b>

![image](https://github.com/user-attachments/assets/7df12deb-9012-4ae9-85c4-2bfbce273079)
- <b>Login as jane_admin</b>

![image](https://github.com/user-attachments/assets/064ec792-8ff6-4f4c-80e1-bf257320a7a7)
- <b>Copy DC-1 Private IP Address</b>

![image](https://github.com/user-attachments/assets/2ea383b6-a3e4-480b-bbc0-9c25d21e52a9)
- <b>Go to Client-1>Network settings>Network interface>DNS servers>custom</b>
- <b>DNS server: 10.0.0.4</b>

![image](https://github.com/user-attachments/assets/c6d55e64-619d-424e-8e3b-c8c14b56f3ff)
- <b>Restart Client-1 virtual machine</b>

![image](https://github.com/user-attachments/assets/092a76af-b543-4fde-a6b4-595b4248ccf6)
- <b> Right-click the start menu and select system</b>

![image](https://github.com/user-attachments/assets/713a2ada-ef47-450d-ae9c-38d55489e5c2)
- <b>Click "Rename this PC (advanced)</b>
- <b>Click change and select domain</b>
- <b>Domain: mydomain.com</b>
- <b>Username: jane_admin</b>

![image](https://github.com/user-attachments/assets/37125caf-e321-4e61-abac-f604473a2f7b)
- <b>Click Remote Desktop</b>
- <b>Click "Select users that can remotely access this PC" and select add</b>
- <b>Type domain users and click check name</b>

![image](https://github.com/user-attachments/assets/9f08193d-acdd-4ced-a46c-e8424db3b8a2)
- <b>Login to DC-1 virtual machine as jane_admin</b>

![image](https://github.com/user-attachments/assets/7083e18f-c5b8-408e-b02c-9c3a8c95c67c)
- <b>Click tool and select active directory and computer</b>
- <b>Click the dropdown arrow on mydomain.com and select users</b>
- <b>Right click domain users and select members</b>
- <b>Jane Doe</b>

![image](https://github.com/user-attachments/assets/590c77c5-1ad2-41fc-a1b9-9759e3274b15)
- <b>Open Windows PowerShell ISE and run as administrator</b>

![image](https://github.com/user-attachments/assets/9f4d3464-1f4b-49bb-a56a-aec965dfdb9c)
- <b>Copy the code from this GitHub link: https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1</b>
- <b>Click new script and run the code</b>

![image](https://github.com/user-attachments/assets/ef6e83e3-3e33-4457-b027-18cdcd3968e8)
- <b>Go back to active directory users and computers</b>
- <b>Choose a random employee and right click>properties</b>

![image](https://github.com/user-attachments/assets/7b2004dd-7954-4557-89ab-eef892ef781f)
- <b>Sign out of the Client-1 virtual machine as jane admin</b>
- <b>Login as the employee that you have chosen</b>

![image](https://github.com/user-attachments/assets/cbf051cb-07a7-4f9d-aa58-53b90ef2a3df)
- <b>Employee have successfully logged in</b>

