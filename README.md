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


After installation, open Control Panel and navigate to Network and Internet,Network and Sharing Center, then click Change adapter settings. 
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
After signing back in, open Server Manager and click Add Roles and Features. Role-Based or feature-based installation select a server from the server pool 'DC Keep clicking Next until you reach the server roles list, check Active Directory Domain Services, click Add Features, then continue through the wizard and click Install. 
![image](https://github.com/user-attachments/assets/84d65a63-abfe-4000-9ac0-876c5abfd638)
![image](https://github.com/user-attachments/assets/26e81f0e-be22-4cbd-a58b-f7520117af41)
![image](https://github.com/user-attachments/assets/3b770d80-2cc1-4eac-b504-4c3793097ff1)


When installation finishes, close the wizard, click the flag icon next to Manage, choose Promote this server to a domain controller, select Add a new forest named lablocal.com, uncheck DNS delegation, and click Install. The server will restart automatically.
![image](https://github.com/user-attachments/assets/ee1f42b9-c2f6-4fb9-a7be-5dd29124aba2)
![image](https://github.com/user-attachments/assets/2dec8288-79d5-4e8c-b8cd-fea36d2f2939)

## Downloading RAS/NAT

Next we will be downloading RAT/NAT and this will act as a gateway for our internal network. We will go to server manager and add roles and sevices lick 'Role-based or feature-based installation and Select our server from the server pool  And we will go next and till we get to services and we will chose remote access services and we will press next till we get to the we to the options and wil choose routing choose add options and press next until we get to install. After the installation completes we can close it.  
![image](https://github.com/user-attachments/assets/7e88c25b-fd9b-4841-a907-6842c2426c42)
![image](https://github.com/user-attachments/assets/070f7cba-a12a-48ce-a41b-bc9fda1db567)
![image](https://github.com/user-attachments/assets/ac0f5b0c-237a-40fd-8f02-9284ebac29e5)
![image](https://github.com/user-attachments/assets/68375340-fef0-4a43-80a3-cfd23a590e79)
![image](https://github.com/user-attachments/assets/0a966608-55d0-4a70-a45e-e2b40d4f3d7c)


Go to tools on server manager and then on routing and remote services. Once we are on we right click and press configure and the we right click new som and we should see option for routing with nat and we will choose that and then will will use the public lab external ip interface for the nat and press next until we get to the end refresh by rigth clicking and wes should  see a green arrow.

![image](https://github.com/user-attachments/assets/55608d7d-48ee-49cc-9261-148ed0b8b3e9)
![image](https://github.com/user-attachments/assets/769e69e9-e53b-4b3c-9ed6-280985a333f4)
![image](https://github.com/user-attachments/assets/0bbc9623-8c41-4bd4-b9ff-06781378949b)

NOTE: If you dont see our networks that we configured, restart the routing and remote access wizard:
![image](https://github.com/user-attachments/assets/ce52a972-e175-43d9-8d82-49ba05cb29d2)
![image](https://github.com/user-attachments/assets/7e1c73d9-9000-46e5-b3a4-bd197a5ca451)

Use this public interface to connect to the internet > click on our adaptor lab external then next:
![image](https://github.com/user-attachments/assets/9d45a0a9-9297-446d-9a28-04c81e595cba)
After we finish refresh by right clickingand we should see a green arrow.
![image](https://github.com/user-attachments/assets/e07d79be-8f57-402b-b1c1-0f194aaee65e)


## Creating Dedicated Admin account

We will need to authorise the dhcp server to so this we will need an admin account with domain admin rights. We we can go active directory users and computers by clicking the tool option on server manager and then going to our domain lablocal.com and then we can right click and create a new ou we will name it _ADMIN and we uncheck the accidental deletion option. 
![image](https://github.com/user-attachments/assets/ef5a8923-b95e-4107-9009-25c996586689)
![image](https://github.com/user-attachments/assets/f1bf0920-f439-42c0-95e2-4bb8afbe3660)


Then press next and the ou will be created. 
![image](https://github.com/user-attachments/assets/f5cb4937-d1b4-4b8d-bc9f-0388f94a40ca)


The we can right click on it on create new and there will option for new user. We will name our user Ahmed Shego and then will use the name username a-ashego this is similar to what is used in real life and we will go to next. 
![image](https://github.com/user-attachments/assets/3efd511a-3b64-4be2-9482-95c48c4a1620)
![image](https://github.com/user-attachments/assets/bb3ec637-fe51-4f05-a8a4-959f93e3834f)


Then will use the option password never expries and  deseleect the option change password at next login and then after we created the user we will right click onto properties and then onto members of tab  and then we will search for domain admin and then add them to that group this will allow us to use admins rights.

![image](https://github.com/user-attachments/assets/613d3e8b-f1d4-4907-9913-9afaa1d32fa2)
![image](https://github.com/user-attachments/assets/488c64ba-6e14-4816-b46d-7bda70650038)
Then press ok
![image](https://github.com/user-attachments/assets/dcc5b4c2-c619-463d-9d8a-b76cae700490)

Log in with the new admin Account
![image](https://github.com/user-attachments/assets/10c9ff08-8155-45bf-9511-d620a2244594)

## Executing Powershell script on DC
Make sure you’re signed in as Domain Admin.
Copy your PowerShell script and notes.txt from your desktop onto the DC’s desktop, then launch PowerShell ISE “Run as Administrator.” 
![image](https://github.com/user-attachments/assets/400ab623-a60f-4a65-8ca9-4fd11bca9f71)
![image](https://github.com/user-attachments/assets/e7d58c09-deb8-4445-804a-20330db3284c)
![image](https://github.com/user-attachments/assets/bbc1c697-3664-435f-9bc6-f44c60f9f60d)
Use cd to navigate to the folder containing your script and notes.txt, open the script in ISE, and press Run. 
![image](https://github.com/user-attachments/assets/e6d3c86f-6a2c-4033-94eb-2141dfef2240)




When it finishes, open Active Directory Users and Computers, locate the target OU, and verify that all 50 users have been created.
![image](https://github.com/user-attachments/assets/44d10946-236d-4fc6-bab8-c8b6a6c72bc6)

## Setting up DHCP server 

Next we will clone our template with the same settings we used for the DC sever but naming it DHCP.
![image](https://github.com/user-attachments/assets/059a209c-f9cc-49e5-b940-419820457d2a)

Next we will right click and go on to settings and then onto network and change our adaptor from nat to internal and theN  press ok.
![image](https://github.com/user-attachments/assets/3a05b6bb-4f2c-433d-bfb4-bc2065c11b13)
After going through installtion process which will be the same as the DC server we will also use the same password for the administrator
![image](https://github.com/user-attachments/assets/81729613-c71c-48ae-a6c0-c716fcb33f53)

After installation, open Control Panel and navigate to Network and Internet,Network and Sharing Center, then click Change adapter settings. Right click on the adaptor choose Properties, double-click Internet Protocol Version 4 (TCP/IPv4), select “Use the following IP address,” and enter the address from your network diagram. Click OK to save.
![image](https://github.com/user-attachments/assets/c1ec2236-2705-4ba2-b6e9-9d084c20fb92)

Next we will go on Search and look for search advanced system properties and  then we  go onto computer name and then change and change the it to DHCP and then we will add it the domain by adding the domain name lablocal.com.
![image](https://github.com/user-attachments/assets/22a4175f-9d32-4dd1-9cc4-0b70b0dc2776)


after pressing ok it will ask for the domain admin account and we will use the admin we created and if we are successful it should say welcome lablocal.com domain after this we it should restart.
![image](https://github.com/user-attachments/assets/b67e2de6-698e-4b48-b6f6-7f0c657ae428)
![image](https://github.com/user-attachments/assets/33ca614a-fbb5-480f-98cf-d36e79cebdfc)

Just like we did before, we will go to Server Manager Dashboard , Add roles and features , Role-based or feature-based installation , Select our server , Select DHCP and add features and then install.
![image](https://github.com/user-attachments/assets/bc609eae-8698-4250-b4f1-c5fb404ce072)
![image](https://github.com/user-attachments/assets/a2d10a65-47c0-4577-865a-774d5f7e3b71)


Once the DHCP role is installed, close the wizard and open Tools , DHCP. Right-click your server’s icon and choose Authorize. Then expand IPv4, right-click it, and select New Scope. Name it (for example, “172.16.0.100-200”) and click Next through the introductory screens until you reach the IP address range page. Enter 172.16.0.100 to 172.16.0.200 with a /24 subnet mask, then click Next. When prompted for the default gateway, enter your domain controller’s IP (172.16.0.10). Continue clicking Next, choose Activate this scope now, and finish. The DHCP service will start and your scope will be live
![image](https://github.com/user-attachments/assets/52c7e05e-2484-4676-8fcf-fb0fb2c96136)
![image](https://github.com/user-attachments/assets/3e166731-6f99-493c-9822-c76edec44e5a)
![image](https://github.com/user-attachments/assets/0b11324b-f9e7-418e-8728-2008833e61cf)
![image](https://github.com/user-attachments/assets/784d7293-7dc6-4130-a2da-85bfd0762a6d)
![image](https://github.com/user-attachments/assets/ed7ed1fc-3573-4eae-b24d-7d5a029cb11d)
We will not be setting any Exlcusions and we can leave the lease on 8 days.
![image](https://github.com/user-attachments/assets/7b98bee4-5fa2-4f85-b3c4-465c74b2720e)
![image](https://github.com/user-attachments/assets/2af6668a-471d-4265-a84e-9089329522ff)
![image](https://github.com/user-attachments/assets/6f720f4c-24ed-4ec4-b0d2-3e9dba292fca)
Skip Win Servers and press Activate now and finish.
![image](https://github.com/user-attachments/assets/727d0128-1aac-4376-97cd-1202183f2cc0)
Right click on the server and refresh and you should see a Green Tick.
![image](https://github.com/user-attachments/assets/47c95431-e3c3-49a0-bb04-201b4cf6bba9)

## Setting Up the Windows 10 Client VM

In VirtualBox, create a new VM named Client, then attach your Windows 10 ISO and skip the unattended-installation options. Assign the same hardware profile as your servers—such as 4 GB of RAM, 2 CPU cores, and a 50 GB virtual disk—to keep consistency across the lab. 
![image](https://github.com/user-attachments/assets/198e1541-98de-49a5-8785-c4af13a04f42)


Once the VM is created, right-click Client, choose Settings, go to the Network tab, and switch the network adapter from NAT to Internal Network so the client resides on your isolated lab network.
![image](https://github.com/user-attachments/assets/160b35ce-55a4-49cf-83bc-4dd86f20be34)

After starting up the Win10 Client VM and going through the installation process which will be the similar to the DC and DHCP server.
![image](https://github.com/user-attachments/assets/0ffc4c8d-9e1c-43d9-8f08-3462a2043e38)
Once it restarts, make sure to use the following options. 'I dont have internet' 'Continue with limited setup
![image](https://github.com/user-attachments/assets/d300b013-1266-41db-b84b-8dc145da4686)
![image](https://github.com/user-attachments/assets/1188a355-21c8-408c-bd48-2f9f3ee50bd1)
Create any username and password will be using User and the same password.  Put in any answer for the security questions and select not now.
![image](https://github.com/user-attachments/assets/9743ca7e-0076-4c6b-a2fe-2aa9c30f2875)
![image](https://github.com/user-attachments/assets/50ee6651-fa3c-413b-97c5-09ebc14bcdfe)



After signing in to the client VM, open Command Prompt and run ipconfig to confirm you’ve received an IP address (it should be 172.16.0.100) from the DHCP server; then run ping lablocal.com to verify DNS resolution and domain connectivity. 
![image](https://github.com/user-attachments/assets/04080306-e669-42d1-9a61-b1eff708a51e)


On the DHCP server, open the DHCP console and check the IPv4 Leases list to ensure the client’s lease is registered.
![image](https://github.com/user-attachments/assets/9aaaa1f6-b1cd-4ae4-b16e-e61917ff9487)

## Joining Client to Domain
Next we will go on Search and look for search advanced system properties and  then we  go onto computer name and then change and change the it to Client and then we will add it the domain by adding the domain name lablocal.com.
![image](https://github.com/user-attachments/assets/56d923fc-9894-4667-8dc8-e75a86eef2a7)
Use Domain Admin Account to authorise domain joining. Then restart.
![image](https://github.com/user-attachments/assets/e4b97d2d-ca87-453f-8759-a0d8b41a3ea0)

## Setting up Group polocies on DC

### Setting Shared Folder

First, create a folder on the DC Local Disk called shared. Right-click it, choose Properties, then go to the Sharing tab ,Advanced Sharing. Remove Everyone, add Domain Users, and grant them Read permission and aplly and press ok.
![image](https://github.com/user-attachments/assets/221630dd-6bbe-4766-b853-19e030bcc87e)
![image](https://github.com/user-attachments/assets/f83929e6-2c64-4f9e-90ce-84ad7762fbab)
![image](https://github.com/user-attachments/assets/770c4a6d-6392-4667-ba01-080e55f8d320)
![image](https://github.com/user-attachments/assets/5a45a06b-4ca4-4841-9677-aac1f62eac82)
![image](https://github.com/user-attachments/assets/4f3b65f1-9f3f-44ba-8b26-85ffab685171)
![image](https://github.com/user-attachments/assets/0682dfbe-a1d6-4fbc-b381-9759d9d4d620)
 Next, switch to the Security tab, add Domain Users, and give Read & Execute rightsand then apply and press ok. Copy the UNC path (e.g. \\DC\Shared)—you’ll need this for the GPO.
 ![image](https://github.com/user-attachments/assets/8a172966-c670-45d9-bb0d-ce7cff284959)
![image](https://github.com/user-attachments/assets/793d2f1c-192a-4cc3-9e25-f9ed775add07)

Open Server Manager → Tools → Group Policy Management, navigate to your Users OU, right-click it and select Link an Existing GPO → name it Shared-Drive. Edit the GPO:
![image](https://github.com/user-attachments/assets/c59e5804-ef75-448b-90f7-8a5f270f27a6)
![image](https://github.com/user-attachments/assets/37770d75-9bfe-444e-9312-f140d4cc8f19)
![image](https://github.com/user-attachments/assets/c4c79b47-53d2-40b1-b32e-a05e2ff1fcd5)
![image](https://github.com/user-attachments/assets/50ea333f-a5e6-46e7-9f95-f82e80adf294)

User Configuration , Preferences , Windows Settings , Drive Maps
Right-click Drive Maps → New → Mapped Drive
Action: Create
Location: \\DC\shared
Drive Letter: S:
Reconnect
Show this drive
Save and close.
![image](https://github.com/user-attachments/assets/25c1327d-bd7a-423d-98b7-c9ddb8a00045)


### Restrict Registry Editing Tools

Create & link a GPO named Restrict-Registry. Make sure to right click and choose enforced.
![image](https://github.com/user-attachments/assets/038e7297-e720-4b6e-a5b7-2eef159e5563)
![image](https://github.com/user-attachments/assets/996038d6-f491-43ca-9cb3-19eaca488da9)

Edit it: User Configuration → Policies → Administrative Templates → System
![image](https://github.com/user-attachments/assets/1ade6db0-5444-4622-aee1-9068dc6f5669)

Double-click Prevent access to registry editing tools → Enabled
Click Apply and then OK.
![image](https://github.com/user-attachments/assets/463e44f4-3862-4c26-b1f4-250f116cef1c)



### Restrict Command Prompt

Create & link a GPO named Restrict-CMD. Right-click it, choose Enforced, then Edit:
![image](https://github.com/user-attachments/assets/975848f2-a1ca-4f76-8fdb-5247fd245ecc)
![image](https://github.com/user-attachments/assets/819ba92b-30c9-49ff-8f6d-c663eca62fda)


User Configuration → Policies → Administrative Templates → System
![image](https://github.com/user-attachments/assets/e6271b3f-fc6f-45a2-9d29-f90f2d3733f0)

Double-click Prevent access to the command prompt → Enabled

Under “Disable the command prompt script processing also?”, select Yes

Click Apply → OK.
![image](https://github.com/user-attachments/assets/f17931fc-26b5-4819-8d36-fd01e34cfa64)



# Restrict Control Panel & Settings

Create & link a GPO named Restrict-Control-Panel and also right click and enforce and then Edit it:
![image](https://github.com/user-attachments/assets/4eb1fc35-acad-43ff-adcc-4d9028b22f73)
![image](https://github.com/user-attachments/assets/c6808309-1ea6-4b8b-9a70-2ee31001249a)

User Configuration → Policies → Administrative Templates → Control Panel
![image](https://github.com/user-attachments/assets/197c5391-3c68-4f28-81d0-48193c93b857)

Double-click Prohibit access to Control Panel and PC settings → Enabled
Click Apply → OK.
![image](https://github.com/user-attachments/assets/e262a383-3a3a-4f05-9d3a-6409168d3d95)

We should have Four Group Policys overall
## Checking If Group Policies have Applied

Go on the Client and Sign in with User Account in my example I will sign in with lsmith. We will go to cmd and then type gpupdate /force then we restart and check each policy to see if works.
![image](https://github.com/user-attachments/assets/402ec3c5-fa3f-4db0-a9fb-0640cad959fe)

![image](https://github.com/user-attachments/assets/881cae28-6b85-436e-9d83-c345db182664)



