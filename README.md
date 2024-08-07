# <p align="center"> Active Directory Home Lab

## Introduction

Setting up a home lab environment for Active Directory is an excellent way to gain hands-on experience with directory services, user management, and network configuration. This project outlines a step-by-step process to create a basic home lab running Active Directory using VirtualBox. The setup includes the installation of Windows Server 2019 as a domain controller and Windows 10 as a client machine. This guide also covers the automation of user account creation using PowerShell script.

## Overview

This project outlines the steps to set up a basic home lab running Active Directory using VirtualBox and to add users with PowerShell.

## Steps Covered

1. Download and install Oracle VirtualBox.
2. Download Windows 10 and Server 2019 ISOs.
3. Create and configure a domain controller virtual machine.
4. Install and configure Server 2019 and Active Directory.
5. Create and configure a client virtual machine running Windows 10.

## Topology

![Picture1](images/Picture1.jpg)

## Lab Configuration

**Virtual Machine Configuration**

- *Server VM Configuration:*
  - ***Name:*** DC
  - ***Type:*** Windows
  - ***Version:*** Other Windows (64-bit)
  - ***Network:*** Two adapters (NAT and internal)
- *Client VM configuration:*
  - ***Name:*** CLIENT1
  - ***Network*** Internal
 
  ***

**Server Configuration**

- *Install Windows Server 2019:*
  - Install *Windows Sever 2019 Standard Evaluation* (Desktop Experience)
  - Set up the administrator account
- *IP Address Configuration:*
  - ***Internal NIC:*** 172.16.0.1
  - ***Subnet Mask:*** 255.255.255.0
  - ***DNS:*** 127.0.0.1
- *Active Directory Setup:*
  - Add Active Directory Domain Services role
  - Create a new forest and domain (mydomain.com)
- *NAT and DHCP Configuration:*
  - Install and configure Routing and Remote Access for NAT
  - Set up DHCP with a scope  

## Step-by-Step Deployment

***Step 1: Download and Install VirtualBox***

<div align="center"> Download and install Oracle VirtualBox along with the VirtualBox Extension Pack.</div>

<p align="center"><img src=images/Picture2.png></p>  

***Step 2: Download ISOs***

<div align="center"> Download the Windows 10 ISO and Server 2019 ISO.</div>

<p align="center">
  <img src=images/Picture3.png> 
  <img src=images/Picture4.png> 
  <img src=images/Picture5.png>
  <img src=images/Picture6.png> 
  <img src=images/Picture7.png>
  <img src=images/Picture8.png>
  <img src=images/Picture9.png>
  <img src=images/Picture10.png>
</p> 

***Step 3: Create and configure a domain controller virtual machine***

<div align="center">Open VirtualBox and select new</div>

<p align="center"><img src=images/Picture11.png></p>

<p align="center"><img src=images/Picture12.png></p>

<div align="center">Create the Server 2019 Virtual Machine (VM). Name the VM "DC". Select the type as "Windows". Select version "Other Windows (64-bit)" and select next</div>

<p align="center"><img src=images/Picture13.png></p>

<div align="center">Select the amount of RAM and CPU to assign to the VM</div>

<p align="center"><img src=images/Picture14.png></p>

<div align="center">Select "Create a Virtual Hard Disk Now", assign Disk Size, and select next</div>

<p align="center"><img src=images/Picture15.png></p>

<div align="center">Review VM summary and select Finish to create</div>

<p align="center"><img src=images/Picture16.png></p>

<div align="center">Select the DC virtual machine and select Settings</div>

<p align="center"><img src=images/Picture17.png></p>

<div align="center">Select Network and select Adapter 2. Check the box to Enable Network Adapter. Attach it to Internal Network and select OK. We are creating the domain controller now and we want to have two NICs. We want one that’s dedicated for the internet that will be running NAT (Adapter 1) and then we will have one that is dedicated for the internal VMWare network (Adapter 2)</div>

<p align="center"><img src=images/Picture18.png></p>

***Step 4: Install and configure Server 2019 and Active Directory***

<div align="center">Start the DC virtual machine</div>

<p align="center"><img src=images/Picture19.png></p>

<div align="center">Mount the Server2019 to the DC virtual machine. Select the DVD drop down menu and select the “Server2019.iso” file we downloaded. Select “Mount and Retry Boot”</div>

<p align="center"><img src=images/Picture20.png></p>

<div align="center">Select Next to begin Windows Server 2019 Installation</div>

<p align="center">
  <img src=images/Picture21.png>
  <img src=images/Picture22.png>
</p>

<div align="center">Next select the ‘Windows Server2019 Standard Evaluation (Desktop Experience). This option installs the full Windows graphical environment</div>

<p align="center"><img src=images/Picture23.png></p>

<div align="center">Accept the license terms and select next</div>

<p align="center"><img src=images/Picture24.png></p>

<div align="center">Next select “Custom: Install Windows only (advanced)”</div>

<p align="center"><img src=images/Picture25.png></p>

<div align="center">Select Next to install windows server2019 on the virtual machine hard drive</div> 

<p align="center"><img src=images/Picture26.png></p>

<div align="center">The installation process may take a while. Also, the server is going to restart several times during this phase. It will get to a black screen where it says “Press any key to boot from CD or DVD” you do not want to do that because you do not want to boot into the setup again. Just don’t touch it and it will end up booting into Windows</div> 

<p align="center"><img src=images/Picture27.png></p>

<div align="center">Sever2019 has been installed. This is the built-in default administrator account. Assign a password to this account and select Finish</div>

<p align="center"><img src=images/Picture28.png></p>

<div align="center">We have successfully installed Windows Server2019</div>

<p align="center"><img src=images/Picture29.png></p>

<div align="center">Next, we need to press Ctrl + Alt + Delete to unlock. To do this navigate to the Input tab in VirtualBox menu and select Keyboard -> Inset Ctrl-Alt-Del (If you try to unlock using your keyboard you will need to use Host + Del)</div>

<p align="center"><img src=images/Picture30.png></p>

<div align="center">Log in to the Administrator account with the password created earlier</div>

<p align="center"><img src=images/Picture31.png></p>

<div align="center">Let the server start up for the first time. Once startup is completed close any pop-up windows until you are at the Server Manager Dashboard</div>

<p align="center"><img src=images/Picture32.png></p>

<div align="center">The first thing we are going to do is install the VM guest additions. This will help give us a better experience (help with mouse lag and screen re-size). Go to Devices -> Insert Guest Additions CD image</div>

<p align="center"><img src=images/Picture33.png></p>

<div align="center">Next select file explore</div>

<p align="center"><img src=images/Picture34.png></p>

<div align="center">Next select This PC</div>

<p align="center"><img src=images/Picture35.png></p>

<div align="center">Next select CD Drive (D:) VirtualBox Guest Additions</div>

<p align="center"><img src=images/Picture36.png></p>

<div align="center">Next select and run the VBoxWindowsAdditions-amd64</div>

<p align="center">
  <img src=images/Picture37.png>
  <img src=images/Picture38.png>
  <img src=images/Picture39.png>
  <img src=images/Picture40.png>
  <img src=images/Picture41.png>
</p>

<div align="center">Next unlock and sign in Administrator account</div>

<p align="center">
  <img src=images/Picture42.png>
  <img src=images/Picture43.png>
  <img src=images/Picture44.png>
</p>

<div align="center">Next let’s set up our IP addressing. We have two NICs. We have one that is dedicated to the internet, and we have the internal one that is going to be used for the internal network. The NIC on the internet will automatically get an IP address from the router so no need to make any changes to that one but for the internal one we need to set it up manually.  In the VM go to Network to view Network & Internet Settings</div>

<p align="center"><img src=images/Picture45.png></p>

<div align="center">Select Change adapter options</div>

<p align="center"><img src=images/Picture46.png></p>
  
 <p align="center"><img src=images/Picture47.png></p>

<div align="center">We have two adapters. We will rename them appropriately because we will use these later when setting up routing. Ethernet is our Adapter 1 in the VM which is the NIC (Internet) and Ethernet 2 is Adapter 2 in the VM which is NIC (Internal). Right click each adapter and rename it</div>

<p align="center">
  <img src=images/Picture48.png>
  <img src=images/Picture49.png>
  <img src=images/Picture50.png>
  <img src=images/Picture51.png>
</p>

<div align="center">Next assign the IP address to the Internal Adapter. Right click on Internal and select Properties</div>

<p align="center"><img src=images/Picture52.png></p>

<div align="center">Select Internet Protocol Version 4 (TCP/IPV4) and select Properties</div>

<p align="center"><img src=images/Picture53.png></p>

<div align="center">Select Use the following IP address and enter IP address 172.16.0.1 and Subnet mask 255.255.255.0. Default Gateway will be empty because the domain controller itself is going to serve as the default gateway. It has two NICs one is on the internet, and one is on the internal. For the DNS server when we install Active Directory it automatically installs DNS, so this server is going to use itself as the DNS server. To do that we will use IP 127.0.0.1 which is the loopback address</div>

<p align="center"><img src=images/Picture54.png></p>

<div align="center">Next, we are going to rename this PC. Right click the start menu and go to System and select Rename this PC and name it DC</div>

<p align="center"><img src=images/Picture55.png></p>

<p align="center"><img src=images/Picture56.png></p>
  
<p align="center">  
  <img src=images/Picture57.png>
  <img src=images/Picture58.png>
</p>

<div align="center">Next unlock and sign in Administrator account</div>

<p align="center"><img src=images/Picture59.png></p>
<p align="center"><img src=images/Picture60.png></p>
<p align="center"><img src=images/Picture61.png></p>

<div align="center">The next thing we are going to do is install Active Directory Domain Services and create a domain. Select Add roles and features</div>

<p align="center">  
  <img src=images/Picture62.png>
  <img src=images/Picture63.png>
</p>

<div align="center">Select Role-based or feature-based installation</div>

<p align="center"><img src=images/Picture64.png></p>

<div align="center">Select DC server we created as the Select destination server to install the Active Directory Domain Services on it</div>

<p align="center"><img src=images/Picture65.png></p>

<div align="center">Select Active Directory Domain Services</div>

<p align="center">
  <img src=images/Picture66.png>
  <img src=images/Picture67.png>
  <img src=images/Picture68.png>
  <img src=images/Picture69.png>
  <img src=images/Picture70.png>
  <img src=images/Picture71.png>
</p>

<div align="center">Now that the role has been installed, we can close the Add Roles and Feature Wizard</div>

<p align="center"><img src=images/Picture72.png></p>

<div align="center">Next check notifications, we need to do our post deployment configuration (we installed the software for active directory domain services, but we did not actually create the domain yet). Select Promote this server to domain controller</div>

<p align="center"><img src=images/Picture73.png></p>

<div align="center">Next select Add a new forest. For the Domain name enter mydomain.com and select next</div>

<p align="center"><img src=images/Picture74.png></p>

<div align="center">Next enter a password for Directory Services Restore Mode (DSRM)</div>

<p align="center">
  <img src=images/Picture75.png>
  <img src=images/Picture76.png>
  <img src=images/Picture77.png>
  <img src=images/Picture78.png>
  <img src=images/Picture79.png>
  <img src=images/Picture80.png>
</p>

<div align="center">Now that it has finished installing it is going to automatically restart the computer for us (This may take a while to complete restart)</div>

<p align="center"><img src=images/Picture81.png></p>

<div align="center">Next unlock and sign into our built-in Administrator account. You will notice we now have MYDOMAIN\Administrator</div>

<p align="center"><img src=images/Picture82.png></p>
<p align="center"><img src=images/Picture83.png></p>
<p align="center"><img src=images/Picture84.png></p>

<div align="center">Now we are going to create our own dedicated Domain Admin Account instead of using the built-in administrator account. To do this go to Start -> Windows Administrative Tools -> Active Directory Users and Computers</div>

<p align="center"><img src=images/Picture85.png></p>

<div align="center">We can see this mydomian.com is our newly created domain it’s all fresh</div>

<p align="center"><img src=images/Picture86.png></p>

<div align="center">Next, we will create an organizational unit to put our admin account in. Right click mydomain.com -> New -> Organizational Unit</div>

<p align="center"><img src=images/Picture87.png></p>

<div align="center">Next, we will give a name to the new Organizational Unit. Name it _ADMINS</div>

<p align="center"><img src=images/Picture88.png></p>

<div align="center">Next, we will need to create a new user in the _ADMINS Organizational Unit. Right click on _ADMINS -> New -> User</div>

<p align="center"><img src=images/Picture89.png></p>

<div align="center">Next we will enter the information for the new user</div>

<p align="center"><img src=images/Picture90.png></p>

<div align="center">Next enter a password for the new user</div>

<p align="center">
  <img src=images/Picture91.png>
  <img src=images/Picture92.png>
</p>

<div align="center">We now have an account but it’s not an admin yet even though we named it a-fabdelrahim</div>

<p align="center"><img src=images/Picture93.png></p>

<div align="center">To make a domain admin right click the user and select properties</div>

<p align="center"><img src=images/Picture94.png></p>

<div align="center">Next select Member Of -> Add</div>

<p align="center">
  <img src=images/Picture95.png>
  <img src=images/Picture96.png>
</p>

<div align="center">Next, we will enter Domain Admins in the Enter the object names to select to resolve to domain admin</div>

<p align="center">
  <img src=images/Picture97.png>
  <img src=images/Picture98.png>
  <img src=images/Picture99.png>
</p>

<div align="center">Now we have our very own domain admin account. To use this, go ahead and log out of the Domain Controller</div>

<p align="center"><img src=images/Picture100.png></p>

<div align="center">Unlock the lock screen</div>

<p align="center"><img src=images/Picture101.png></p>

<div align="center">Instead of logging into this administrator one we are going to select Other user and we see it says sign into MYDOMAIN. We are going to use our domain admin account here (a-fabdelrahim) to log in</div>

<p align="center"><img src=images/Picture102.png></p>
<p align="center"><img src=images/Picture103.png></p>

<div align="center">Next, we are going to install RAS/NAT, that is like remote access server (RAS) network address and network address translation (NAT). The purpose of this is to allow us when we create our Windows 10 client, it is going to allow this client to be on this private virtual network but still be able to access the internet through the domain controller. So, we are going to install RAS and NAT on the domain controller to allow our clients to do that. To do this we will go to Add roles and features</div>

<p align="center">
  <img src=images/Picture104.png>
  <img src=images/Picture105.png>
  <img src=images/Picture106.png>
  <img src=images/Picture107.png>
</p>

<div align="center">Select Remote Access</div>

<p align="center">
  <img src=images/Picture108.png>
  <img src=images/Picture109.png>
  <img src=images/Picture110.png>
</p>

<div align="center">Next, we are going to install Routing and DirectAccess and VPN (RAS). RAS will be checked automatically once you select Routing and select Add Features</div>

<p align="center">
  <img src=images/Picture111.png>
  <img src=images/Picture112.png>
  <img src=images/Picture113.png>
  <img src=images/Picture114.png>
  <img src=images/Picture115.png>
  <img src=images/Picture116.png>
  <img src=images/Picture117.png>
</p>

<div align="center">Next, we will go to tools and select Routing and Remote Access</div>

<p align="center"><img src=images/Picture118.png></p>

<div align="center">Next, right click on DC (local) and select Configure and Enable Routing and Remote Access</div>

<p align="center">
  <img src=images/Picture119.png>
  <img src=images/Picture120.png>
</p>

<div align="center">Select Network address translation (NAT). This allows internal clients to connect to the Internet using one public IP address</div>

<p align="center"><img src=images/Picture121.png></p>

<div align="center">Next, we will select the Internet Network Interfaces to use this public interface to connect to the internet</div>

<p align="center"><img src=images/Picture122.png></p>
<p align="center"><img src=images/Picture123.png></p>

<div align="center">Once it finishes the Routing and Remote Access Server Setup, we can see a green up arrow displayed next to DC (local) which means it is completely configured</div>

<p align="center"><img src=images/Picture124.png></p>

<div align="center">The next step we are going to do is setup a DHCP server on our domain controller. This is going to allow our Windows 10 clients to get an IP address that will allow them to get on the internet and browse the internet even though they are on this private internal network. To setup our DHCP we will go to Add roles and features</div>

<p align="center">
  <img src=images/Picture125.png>
  <img src=images/Picture126.png>
  <img src=images/Picture127.png>
  <img src=images/Picture128.png>
  <img src=images/Picture129.png>
  <img src=images/Picture130.png>
  <img src=images/Picture131.png>
  <img src=images/Picture132.png>
  <img src=images/Picture133.png>
  <img src=images/Picture134.png>
  <img src=images/Picture135.png>
</p>

<div align="center">Next go to Tools and select DHCP and setup our scope</div>

<p align="center">
  <img src=images/Picture136.png>
  <img src=images/Picture137.png>
</p>

<div align="center">The purpose of DHCP is allow client computers on the network to automatically get their IP addresses. Our scope will give IP addresses in this range 172.16.0.100-200. Go to our DHCP server and select the dc.mydomain.com. We notice they are both red which indicates they are down. Right click on IPv4 and select New Scope</div>

<p align="center"><img src=images/Picture138.png></p>
<p align="center"><img src=images/Picture139.png></p>

<div align="center">Next we will name the Scope as the IP address range 172.16.0.100-200</div>

<p align="center">
  <img src=images/Picture140.png>
  <img src=images/Picture141.png>
  <img src=images/Picture142.png>
  <img src=images/Picture143.png>
  <img src=images/Picture144.png>
</p>

<div align="center">We configured NAT on the Domain Controller, and the Domain Controller has routing configured so its job is to forward traffic from the clients to the internet. Because of this configuration the clients are going to use the internal NIC of the Domain Controller as their default gateway/router. Enter the Domain Controller IP address that has NAT</div>

<p align="center"><img src=images/Picture145.png></p>
<p align="center"><img src=images/Picture146.png></p>

<div align="center">When you install Active Directory on the Domain Controller it automatically installs DNS. Because of that we are going to use the Domain Controller as our DNS server</div>

<p align="center">
  <img src=images/Picture147.png>
  <img src=images/Picture148.png>
  <img src=images/Picture149.png>
  <img src=images/Picture150.png>
  <img src=images/Picture151.png>
  <img src=images/Picture152.png>
</p>

<div align="center">Now we have our DNS setup</div>

<p align="center"><img src=images/Picture153.png></p>

Next, we are going to create a PowerShell script. This script is designed to automate the creation of user accounts in Active Directory (AD).

<p align="center">
  <img src=images/Picture154.png>
  <img src=images/Picture155.png>
</p>

***Variables Section***

-	`$PASSWORD_FOR_USERS`: This variable specifies the default password for all new user accounts being created. In this case, it’s set to “Password1”.
-	`$NUMBER_OF_ACCOUNTS_TO_CREATE`:  This variable specifies the total number of user accounts to be created.

<p align="center"><img src=images/Picture156.png></p>

***Create Organizational Unit***

-	This line creates a new Organizational Unit (OU) named `_USERS` in Active Directory. The `-ProtectedFromAccidentalDeletion $false` parameter ensures that the OU can be deleted without any additional confirmation (this is set for easy clean up after lab)

<p align="center"><img src=images/Picture157.png></p>

***Generate Random First Name Function***

-	`generate-random-first-name`: This function returns a random name from a predefined list of first names.

<p align="center"><img src=images/Picture158.png></p>

***Generate Random Last Name Function***

-	`generate-random-last-name`: This function returns a random last name from a predefined list of last names.

<p align="center"><img src=images/Picture159.png></p>

***Main Loop for Creating User Accounts***

-	This loop iterates until the number of created (`$count`) reaches the specified number (`$NUMBER_OF_ACCOUNTS_TO_CREATE`).
-	In each iteration, it generates a random first name and last name, combines them to form a username, and sets the password.
-	`ConvertTo-SecureString $PASSWORD_FOR_USERS -AsPlainText -Force` converts the password to a secure string format required by `New-ADUser`.
-	`Write-Host “Creating user: $($username)” `outputs the username being created
-	`New-ADUser` is a cmdlet used to create a new Active Directory user. It sets various attributes such as password, given name, surname, display name, employee ID, and enables the account. 
-	The script uses a ‘try’ block to attempt to create the user account and increments the count if successful.
-	The `catch` block handles any errors that occur during the account creation and outputs an error message.
-	If there is a failure in user creation, the script catches the exception and outputs the error message.

<p align="center"><img src=images/Picture160.png></p>

Save the script as AD-Creat-Users

<p align="center">
  <img src=images/Picture161.png>
  <img src=images/Picture162.png>
</p>

Next, we will have to enable the execution of all scripts on this server. In the terminal enter the following command: `Set-ExecutionPolicy Unrestricted` 

<p align="center">
  <img src=images/Picture163.png>
  <img src=images/Picture164.png>
</p>

Next, we will need to navigate to the desktop in the PowerShell terminal 

<p align="center">
  <img src=images/Picture165.png>
  <img src=images/Picture166.png>
</p>

Now we can run the PowerShell script to create new users and add them to our Active Directory under _USERS.

<p align="center">
  <img src=images/Picture167.png>
  <img src=images/Picture168.png>
</p>

The script successfully ran, and all our users have been created. We can navigate to the Active Directory, and we can see that we have our _USERS folder that the script created, and we can see a list of users inside.

<p align="center">
  <img src=images/Picture169.png>
  <img src=images/Picture170.png>
</p>

***Step 5: Create and configure a client virtual machine running Windows 10***

At this point we have almost everything setup. The internet is connected. We have the NICs setup, the domain is setup with all our users, NAT is setup, DHCP is setup, and we are connected to the internal VMWare network. The very last thing we need to do is create the Windows 10 virtual machine in VirtualBox. It will use an internal NIC and it will get its IP address from our DHCP server we configured. Go to VirtualBox and select New

<p align="center">
  <img src=images/Picture171.png>
  <img src=images/Picture172.png>
  <img src=images/Picture173.png>
  <img src=images/Picture174.png>
  <img src=images/Picture175.png>
</p>

Before we start the CLIENT1 virtual machine go to settings -> Network and select Internal Network for Attached to:

<p align="center">
  <img src=images/Picture176.png>
  <img src=images/Picture177.png>
  <img src=images/Picture178.png>
  <img src=images/Picture179.png>
  <img src=images/Picture180.png>
  <img src=images/Picture181.png>
  <img src=images/Picture182.png>
  <img src=images/Picture183.png>
  <img src=images/Picture184.png>
  <img src=images/Picture185.png>
  <img src=images/Picture186.png>
  <img src=images/Picture187.png>
  <img src=images/Picture188.png>
  <img src=images/Picture189.png>
  <img src=images/Picture190.png>
  <img src=images/Picture191.png>
  <img src=images/Picture192.png>
  <img src=images/Picture193.png>
  <img src=images/Picture194.png>
  <img src=images/Picture195.png>
  <img src=images/Picture196.png>
  <img src=images/Picture197.png>
  <img src=images/Picture198.png>
</p>

Now our Windows 10 is setup. The first thing we will check is if the internet is working. Click on start and enter cmd to open a command prompt. Type ipconfig to verify we have a connection 

<p align="center">
  <img src=images/Picture199.png>
  <img src=images/Picture200.png>
  <img src=images/Picture201.png>
</p>

Next, we will try and ping google.com to check that our DNS is working, and the internet is accessible 

<p align="center"><img src=images/Picture202.png></p>

Next, we will change the name of this Windows 10 machine and join the domain at the same time. Right click start menu and select system 

<p align="center">
  <img src=images/Picture203.png>
  <img src=images/Picture204.png>
  <img src=images/Picture205.png>
  <img src=images/Picture206.png>
</p>

Use domain admin account we created to give permission to join domain

<p align="center">
  <img src=images/Picture207.png>
  <img src=images/Picture208.png>
  <img src=images/Picture209.png>
  <img src=images/Picture210.png>
</p>

Now go back to the Domain Controller and go to DHCP and check the Address Leases to verify that our Windows 10 client has joined

<p align="center">
  <img src=images/Picture211.png>
  <img src=images/Picture212.png>
</p>

Next go to Active Directory Users and Computers to verify that the computer has been added to the domain so we can confirm that the users we created can be accessed on the windows 10 client machine

<p align="center">
  <img src=images/Picture213.png>
  <img src=images/Picture214.png>
</p>

Now go back to the Windows 10 client virtual machine and let’s log in with one of the user accounts we created

<p align="center">
  <img src=images/Picture215.png>
  <img src=images/Picture216.png>
</p>

We have successful log in with the user account we on the Windows 10 client machine

<p align="center">
  <img src=images/Picture217.png>
  <img src=images/Picture218.png>
</p>

