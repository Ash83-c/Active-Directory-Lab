# Active-Directory-Lab
## Youtube Walkthrough
youtubelink
## Description
In this lab, I will walk you through creating an Active Directory home lab environment using Oracle VirtualBox. Through the configuration and operation of this lab, we will understand how Active Directory and Windows networking work.
## Languages and Utilities Used
PowerShell

Oracle VirtualBox
## Environments Used

Windows 10 Enterprise

Windows Server 2022

## Project Overview:
![Image](https://github.com/user-attachments/assets/ed6af144-aa59-40a4-bbe5-f288aadbee69)
## Walk-through
## Setting up Server Template
This is done because we will need this will simulate a real-world corporate where they have a standardised VM template This reduces # Active Directory Lab

## YouTube Walkthrough
[YouTube Link](youtubelink)

## Description
In this lab, I will guide you through creating an Active Directory home lab environment using Oracle VirtualBox. By configuring and operating this lab, we will gain a better understanding of how Active Directory and Windows networking function.

## Languages and Utilities Used
- PowerShell
- Oracle VirtualBox

## Environments Used
- Windows 10 Enterprise
- Windows Server 2022

## Walkthrough

### Setting up the Server Template
In this section, we will establish a server template to simulate a real-world corporate environment with a standardized VM template. This approach reduces the chance of errors and saves time. We will use Sysprep to ensure that cloned machines do not share the same Security Identifier (SID). If we create the domain controller and then clone it to make a DHCP server, both will have the same SID, preventing us from adding the DHCP server to the domain.

We will configure the server with 4 GB of RAM, 2 CPU cores, and 50 GB of storage.
![VM Template creation](https://github.com/user-attachments/assets/9c5cfb93-0587-43d2-8b0d-cb3036ae988a)

We will go to settings and to update and security and make sure to check for any updates to ensure  latest  patches are installed



After this, we will run Sysprep using the options OOBE (Out-of-Box Experience) and "Generalize," followed by a shutdown.







Next, we will use the template called "VM Template" to create a clone named "DC (Domain Controller)." Ensure to select the options generate a new MAC address and select the option for a full clone.
![image](https://github.com/user-attachments/assets/ca05dea2-8662-4d04-a3e3-498cc5aa7a89)
![image](https://github.com/user-attachments/assets/d0ccd8e5-58ce-4733-88a8-31aa09fbe8bc)


Afterward, right-click on the DC server, go to **Settings**, navigate to the **Expert** tab, then to genral and then advanced to enable    enable Bi-directional Sharing for both shared clipoard and drag and drop option. This will allow us to drag and drop our PowerShell script onto the DC server. 
![image](https://github.com/user-attachments/assets/f556cc01-d7a5-4574-bc61-4809bd970882)

Finally, in the network settings, enable Adapter 2 and select the option for the Internal Network, naming it "Lab Internal." Click OK to save the settings.
![image](https://github.com/user-attachments/assets/27799ec9-0fef-431f-b842-2a33cf8755cd)

Start the DC and go through setup process choose custom installation and make passwordfor are example we use Secure123.![image](https://github.com/user-attachments/assets/21f05710-32bb-4f81-8809-6ae6aecebd2b)


After this we will download guest additon of virtualbox using device options and we will download and install adn restartit. This will alllows us to drag and drop our powershelll script later on.
![image](https://github.com/user-attachments/assets/28217b84-130e-4283-b4d4-6b2bd9707c04)
![image](https://github.com/user-attachments/assets/2e2887b4-37b0-4dea-a7ec-da008970fad0)
![image](https://github.com/user-attachments/assets/7c88e902-4644-4f06-a192-864e572175e2)


After installation, open Control Panel and navigate to Network and Internet → Network and Sharing Center, then click Change adapter settings. 
![image](https://github.com/user-attachments/assets/b0b76319-85ed-4483-b236-3f4125a1d927)
You’ll see two adapters—right-click the one without Internet access, select Status → Details, and confirm it has an APIPA address (169.x.x.x).
![image](https://github.com/user-attachments/assets/dc8d48f8-ea0a-457b-a76e-8283b2ff3fdc)
![image](https://github.com/user-attachments/assets/ec48c245-12f8-4e35-83da-0cdc3211f237)

Close the details window, choose Properties, double-click Internet Protocol Version 4 (TCP/IPv4), select “Use the following IP address,” and enter the address from your network diagram. Click OK to save, then rename this adapter to Lab-Internal and the other to Lab-External.
![image](https://github.com/user-attachments/assets/bdf89300-09b1-49ba-b225-6b087daf53f8)
![image](https://github.com/user-attachments/assets/4b8aadb2-886f-462f-820b-dce3f1a745c4)

Next we will go on Search and look for search advanced system properties and  then we  go onto computer name and then change and change it to DC and then press ok and then restart.
![image](https://github.com/user-attachments/assets/9160938a-01c2-432b-a055-a2016978d8fc)

## Downloading Active Directory
After signing back in, open Server Manager and click Add Roles and Features. Role-Based or feature-based installation select a server from the server pool 'DC Keep clicking Next until you reach the server roles list, check Active Directory Domain Services, click Add Features, then continue through the wizard and click Install. When installation finishes, close the wizard, click the flag icon next to Tools, choose Promote this server to a domain controller, select Add a new forest named lablocal.com, uncheck DNS delegation, and click Install. The server will restart automatically.
![image](https://github.com/user-attachments/assets/84d65a63-abfe-4000-9ac0-876c5abfd638)

