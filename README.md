# Configuring Active Directory

# Setup Resources in Azure
- Create a (Windows Server 2022) Domain Controller VM and name it (DC01)
- Note the Resource Group and Virtual Network (Vnet) that got created.
- Set Domain Controller’s NIC Private IP address to be static.
- Create the Client VM (Windows 10) named “Client-1”. Put it in the same Resource Group and Vnet that was created for DC01

![image](https://github.com/user-attachments/assets/451e7fcc-0328-41df-be04-cf906d9ea497)

- Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher
Ensure Connectivity between the client and Domain Controller
- Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
- Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall

![image](https://github.com/user-attachments/assets/df59b95c-841e-4865-8ba0-caab633d6281)
- Check back at Client-1 to see the ping succeed
![image](https://github.com/user-attachments/assets/f5bdeefd-b824-4d3b-8df6-981d3737f6da)


# Install Active Directory
- Login to DC-1 and install Active Directory Domain Services
![image](https://github.com/user-attachments/assets/79806d6a-cae8-47ba-b2a9-ffd088782c78)

- Promote as a DC: Setup a new forest as mydomain.com 
- Restart and then log back into DC-1 as user: mydomain.com\username

# Create an Admin and Normal User Account in AD
- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
- Create a new OU named “_ADMINS”
- Create a new employee named “Jeff Bezos” (same password) with the username of “jeff_admin”
- Add jeff_admin to the “Domain Admins” Security Group
- Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jeff_admin”
- Use jeff_admin as your admin account from now on


# Join Client-1 to your domain (mydomain.com)
- From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address

![image](https://github.com/user-attachments/assets/d4fa3df1-308d-4712-9e4d-f8d4f4505011)


- From the Azure Portal, restart Client-1
- Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
- Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
- Create a new OU named “_CLIENTS” and drag Client-1 into there (Step is not really necessary, just for organizational purposes. I guess I skipped this in the lab!)


# Setup Remote Desktop for non-administrative users on Client-1
- Log into Client-1 as mydomain.com\jane_admin and open system properties
- Click “Remote Desktop”
- Allow “domain users” access to remote desktop
- You can now log into Client-1 as a normal, non-administrative user now


#  Create a bunch of additional users and attempt to log into client-1 with one of the users
- Login to DC-1 as jane_admin
- Open PowerShell_ise as an administrator
- Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
- Run the script and observe the accounts being created
- When finished, open ADUC and observe the accounts in the appropriate OU
attempt to log into Client-1 with one of the accounts (take note of the password in the script)

You've now successfully setup Active Directory!!!
