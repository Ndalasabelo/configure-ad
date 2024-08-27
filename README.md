# Configuring Active Directory

# Setup Resources in Azure
- Create a (Windows Server 2022) Domain Controller VM and name it (DC01)
- Note the Resource Group and Virtual Network (Vnet) that got created.
- Set Domain Controller’s NIC Private IP address to be static.
- Create the Client VM (Windows 10) named “Client-1”. Put it in the same Resource Group and Vnet that was created for DC01 
- Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher
Ensure Connectivity between the client and Domain Controller
- Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
- Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
- Check back at Client-1 to see the ping succeed
# Install Active Directory
- Login to DC-1 and install Active Directory Domain Services
- Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
