<h1>Foundation: Azure VM setup and Network Configuration</h1>

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
  <img src="https://s3.amazonaws.com/dev.assets.neo4j.com/wp-content/uploads/20180821105618/Microsoft_Azure_Logo.png" alt="Microsoft Active Directory Logo"/>
</p>




<p>Welcome to the first tutorial in our Active Directory series. This project establishes the foundation for future tutorials, aiming to create a simple lab environment on Azure that simulates the use of Active Directory in an enterprise setting.
</p>

<h2>Overview </h2>

<p>In this project, I will set up and connect two virtual machines in Azure: one as the Domain Controller and the other as the Client.</p>

<h2>Key Objectives</h2>
<h3>Virtual Machine Setup</h3>

- Virtual network creation
- Configure the virtual machine for the Domain Controller.  
- Set up the virtual machine for the Client

<h3>Remote Connectivity</h3>

- Establish a connection using Remote Desktop Connection.

<h3> Traffic Inspection</h3>

- Undertake a basic inspection of the network traffic between the Domain Controller and Client virtual machines.



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows (Windows Server 2019 Datacenter)
- Windows 10 (21H2)


<h2>Configuration Steps</h2>

<h3>&#9312; Virtual network configuration</h3>

- Create a virtual network with the below specifications
  
  ![v1](https://github.com/user-attachments/assets/d0bae1c7-8e0f-44b4-9622-29505437388e)
  ![v2](https://github.com/user-attachments/assets/44351d1d-f474-4c3a-8392-a2597ae6355f)
  
<h3>&#9313; Domain controller VM setup</h3>

- Set up the first virtual machine (VM) to serve as the domain controller.
  
  ![VM1](https://github.com/user-attachments/assets/b2647f4c-c676-48ee-993c-0f9715143069)
  ![VM2](https://github.com/user-attachments/assets/65e1ca6a-9f58-4bf5-b44c-0a4a56c11764)

* For the network interface,select the virtual network already created 
  
  ![VM3](https://github.com/user-attachments/assets/0071d412-02d9-427a-8517-3de905c662ab)
* After reviewing your settings, click on "Review + Create," and then select "Create" once the validation is complete to set up your virtual machine.

  <h3>&#9314; Domain controller network settings</h3>
  
  ![VM4](https://github.com/user-attachments/assets/c7a5a28f-5753-42bf-b73b-54d33bd25609)
- Select Windows Server 2022: Azure Edition - x64 Gen2 as the image


<p>
<img width="776" alt="VM image" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/f072cd7b-b547-4006-9ddb-ae6ba39c497e">
</p>
<p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<strong> NOTE: Make sure to select at least 2 vcpus and 16 GiB memory and take note of the vnet that the VM has created.</strong>
</p>
<br />

<p>
<img width="736" alt="DC-vm" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/323e78b9-4e86-46e3-b021-6ac529ccb600">
</p>
<p>
</p>
<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9313; Set the Domain Controller's Private IP to static </h3>

-  Once the VM has been deployed, proceed to the VM overview page and select "Networking" on the left side. 
<img width="692" alt="networking" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/a35e1aad-57e1-4c1c-9e4e-aefa4fcf31ea">
<br>
<br>
<br>

-  Select Network Interface Card -> IP configurations -> ipconfig1 and set Private IP address allocation to static.

<br>

<p>
<img width="518" alt="static" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/8629a747-9809-4329-859f-2d38896ec484">
</p>

<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9314; Create the client VM </h3>

- Once again create a new VM and we'll name it Client-01. We'll select Windows 10 as the image and make sure to select at least 2 vcpus and 16 GiB memory.
<img width="717" alt="VM 2 name " src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/a3005b2a-cc0a-49f6-8b9e-c6a594c2aba9">

<br>
<br>
<br>

<p><strong> NOTE: Make sure to select the same resource group and vnet from the DC-01 VM </strong></p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="731" alt="VM2 vnet" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/d591d9b0-ce68-4e74-a466-cdd34886c74b">\

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

- Now finalize everything and wait for its deployment.

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9315; Ensure connectivity between Domain Controller and Client  </h3>

<p>To ensure connectivity between the two VM's, we will ping the domain controller from the client.</p>

- First login to the Client-01 using it's public ip address and remote desktop

<img width="993" alt="client 1 public ip" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/c12a5300-fd26-4ae7-b15b-b4fee053bece">


<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="297" alt="remote desktop first login" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/97467245-a6b9-4922-a668-71fdf6f77989">

<br>
<br>
<br>
<br>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Find DC-01's private ip address in the Azure Portal and copy it. Proceed to Client-01 and open the terminal and type "ping -t (DC-01 private ip address)" </strong></p>


<img width="668" alt="perpetual ping" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/d83a1cbf-2619-4382-bc3c-7025ed246119">


<br>
<br>

<p> <strong> Now notice how the request timed out, this is because ICMP v4 traffic is blocked by default on DC-01's firewall. So we will have to enable inbound ICMP traffic to allow for Client-01's ping.</strong> </p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Login to DC-01 using remote desktop and open windows defender firewall and select advanced settings. Sort by protocol and find both ICMP echo requests and enable both these rules by right clicking and selecting enable rule.</strong></p>

<br>

<img width="668" alt="firewall" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/818f7ebe-2ec3-4bd5-b59a-2bc55c24a567">

<br>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Now once the traffic has been enabled, you can check back with Client-01 and notice that the ping is now successful.</strong> </p>

<img width="334" alt="ping 2" src="https://github.com/kirkgacias/ad-and-azuresetup/assets/158519921/ede5ce46-2d9d-49c6-82d7-5afc9796294b">

<h2> Final Thoughts </h2>

<p> We've completed the foundational setup for our Azure and Active Directory project series. By configuring two virtual machines, we've laid the groundwork for implementing the subsequent set of projects. In this project, we focused on establishing a Domain Controller and a Client machine, enabling remote access, and briefly examining network traffic between them. Moving forward, this foundation will help implement more advanced configurations and practical scenarios in Azure and Active Directory. </p>









