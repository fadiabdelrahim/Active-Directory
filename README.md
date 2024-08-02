# <p align="center"> Active-Directory

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

Next unlock and sign in Administrator account

<p align="center"><img src=images/Picture59.png></p>
<p align="center"><img src=images/Picture60.png></p>
<p align="center"><img src=images/Picture61.png></p>

The next thing we are going to do is install Active Directory Domain Services and create a domain. Select Add roles and features

<p align="center">  
  <img src=images/Picture62.png>
  <img src=images/Picture63.png>
</p>

Select Role-based or feature-based installation

<p align="center"><img src=images/Picture64.png></p>

Select DC server we created as the Select destination server to install the Active Directory Domain Services on it

<p align="center"><img src=images/Picture65.png></p>

Select Active Directory Domain Services 

<p align="center">
  <img src=images/Picture66.png>
  <img src=images/Picture67.png>
  <img src=images/Picture68.png>
  <img src=images/Picture69.png>
  <img src=images/Picture70.png>
  <img src=images/Picture71.png>
</p>

Now that the role has been installed, we can close the Add Roles and Feature Wizard

<p align="center"><img src=images/Picture72.png></p>

Next check notifications, we need to do our post deployment configuration (we installed the software for active directory domain services, but we did not actually create the domain yet). Select Promote this server to domain controller

<p align="center"><img src=images/Picture73.png></p>

Next select Add a new forest. For the Domain name enter mydomain.com and select next

<p align="center"><img src=images/Picture74.png></p>

Next enter a password for Directory Services Restore Mode (DSRM)

<p align="center">
  <img src=images/Picture75.png>
  <img src=images/Picture76.png>
  <img src=images/Picture77.png>
  <img src=images/Picture78.png>
  <img src=images/Picture79.png>
  <img src=images/Picture80.png>
</p>

Now that it has finished installing it is going to automatically restart the computer for us (This may take a while to complete restart)

<p align="center"><img src=images/Picture81.png></p>

Next unlock and sign into our built-in Administrator account. You will notice we now have MYDOMAIN\Administrator 

<p align="center"><img src=images/Picture82.png></p>
<p align="center"><img src=images/Picture83.png></p>
<p align="center"><img src=images/Picture84.png></p>

Now we are going to create our own dedicated Domain Admin Account instead of using the built-in administrator account. To do this go to Start -> Windows Administrative Tools -> Active Directory Users and Computers



## 
