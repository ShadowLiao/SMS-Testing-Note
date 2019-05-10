# AWS SMS 

## Steps 

1.	Create an IAM role for AWS SMS
2.	Setup the SMS Connector on VMware / Hyper-V / Azure

### VMware Connector

1.	Download the OVA file to Vcenter
2.	Configure the SMS permission on Vcenter
3.	Setup the VM by using the OVA file
4.	Configure the Connector
5.	View it on the AWS web console

### Hyper-V Connector

1.	Windows configurations
* Enable WinRM
* Enable remote PowerShell
* Create a self-signed X.509 certificate, creates a WinRM HTTPS listener, and binds the certificate to the listener
* Create a firewall rule for WinRM listener
* Adds the IP address or domain name of the connector to the list of trusted hosts in the WinRM configuration
* Enable CredSSP authentication with WinRM
* Grants read and execute permissions to a pre-configured AD user on WinRM configSDDL
* Add an AD user to Hyper-V manager group
* Configure the permission for this group to read VM data

2.	Download the VHD ZIP on Hyper-V server and setup it as a VM
3.	Configure the SMS connector on the Hyper-V VM
4.	Download and install the PowerShell script for SMS
5.	Verify and run the script
6.	Configure the SMS connector on AWS web console

### Azure Connector

1.	Download the PowerShell script to a Windows server on Azure
2.	Verify and run the script
3.	Configure the SMS Connector by using browser to connect the VM private IP
4.	Replace step 1. to 2. by another method.
    Download the VHD file to run a Connector VM on Azure.
    Follow the guide to configure the VM Connector.

## Testing Note

1.	Create an Azure Linux VM as Web server
* Enter `Resource group`, `VM` name
* Select Image : Ubuntu 16.04
* Select Size : B1s (vCPU : 1, RAM : 1 GB)
* Select **Password**
> username/password
* Select `Allow selected ports` 
* Select SSH 22 port and click next
* Select standard SSD and click next
* Select inbound SSH
* Create

2.	Setup an Apache website
* Login the ubuntu VM via SSH
* Execute command
```
#sudo apt-get update
#sudo apt-get install apache2
```
* Paste the VM public IP into a browser and check the page information

3.	Setup a Azure Windows VM as AWS SMS Connector
* Select `Resource group`
* Enter VM name
* Select Image : Windows server 2016 datacenter
* Select Size : B2ms (vCPU : 2, RAM : 8 GB)
> (Aws suggestion => vCPU: 4, RAM: 8G) 
* Select **Password**
> username/password
* Select `Allow selected ports` 
* Select RDP 3389 port and click next
* Select standard HDD and click next
* Select inbound RDP
* Create

4.	Configure SMS Connector on Windows VM
* Login the Windows VM via RDP
* Open ie browser and paste connector.ps1 URL to download
* Enable Javascript on IE internet option
* Open datacenter controller console to turn off firewall
* Open powershell console and execute script
* Enter Storage account and Virtual network name
* Follow the install step and login azure account
* Checking the copy process

<p align="center">
	<img src="/SMS_01.jpg" width="1000" height="1000%">
</p>

5.	The default size of Azure VM disks is too large.
    This test will spend too much cost, so I interrupted the test. 
