
# Active Directory Home Lab

## Project Summary

In this lab, I built a Windows Active Directory environment using VirtualBox. The setup includes a Domain Controller running Windows Server 2019 configured with Active Directory Domain Services (AD DS), DNS, DHCP, and NAT. A Windows 10 client machine was deployed and joined to the domain to simulate a real enterprise environment.

---

## Technologies Used

* VirtualBox
* Windows Server 2019
* Windows 10
* Active Directory Domain Services (AD DS)
* DNS
* DHCP
* Routing and Remote Access (NAT)
* PowerShell

---


## Setup Steps

### 1. Create Domain Controller VM

* Create a Windows Server 2019 VM in VirtualBox
* Assign at least 2GB RAM
* Configure:

  * Adapter 1: NAT (internet)
  * Adapter 2: Internal Network
* Install OS with Desktop Experience



---

### 2. Configure Networking

* Rename adapters:

  * NAT → Internet
  * Internal → Internal
* Assign static IP:

  * IP: 172.16.0.1
  * Subnet: 255.255.255.0
  * DNS: 127.0.0.1

Active Directory depends on DNS, so the Domain Controller acts as the DNS server.


---

### 3. Install Active Directory

* Open Server Manager → Add Roles and Features
* Install AD DS
* Promote to Domain Controller
* Create domain: `mydomain.com`


---

### 4. Create Admin User

* Open Active Directory Users and Computers
* Create Organizational Unit (OU)
* Create user and add to **Domain Admins**


---

### 5. Configure NAT (Internet Access)

* Install Remote Access role
* Enable Routing and Remote Access
* Configure NAT using Internet adapter

NAT allows private network (172.16.x.x) to access the internet.



---

### 6. Configure DHCP

* Install DHCP role
* Create scope:

  * Range: 172.16.0.100 – 172.16.0.200
  * Gateway: 172.16.0.1
  * DNS: Domain Controller

DHCP automatically assigns IP, gateway, and DNS.


---

### 7. Automate User Creation

* Use PowerShell script to create multiple users
* Run:

```powershell
Set-ExecutionPolicy Unrestricted
```

* Execute script


---

### 8. Create Client VM

* Create Windows 10 VM
* Use Internal Network
* Install OS


---

### 9. Join Client to Domain

* Rename PC
* Join domain: `mydomain.com`
* Restart and log in with domain user


---

Verify:

* Client receives DHCP IP
* Client appears in Active Directory
* Internet connectivity works

---

## What I Learned

* Deploy Active Directory Domain Services
* Configure DNS, DHCP, and NAT
* Manage users and Organizational Units
* Automate tasks with PowerShell
* Join machines to a domain

---

## Future Improvements

* Implement Group Policy Objects (GPO)
* Add multiple clients
* Simulate enterprise security scenarios
