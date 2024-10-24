<h1 align="center">Foundation: Azure VM setup and Network Configuration</h1>

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
- Windows (Windows 10 Pro)


<h2>Configuration Steps</h2>

<h3>&#9312; Virtual network configuration</h3>

- Create a virtual network with the below specifications
  
  ![v1](https://github.com/user-attachments/assets/d0bae1c7-8e0f-44b4-9622-29505437388e)
  
- You can change the IP addresses, but for this exercise we will maintain the default IP addresses
  

  ![v2](https://github.com/user-attachments/assets/44351d1d-f474-4c3a-8392-a2597ae6355f)

 * After reviewing your settings, click "Review + Create," then select "Create" once the validation is complete to create your virtual network
<br>
<br>
<br>

<h3>&#9313; Domain controller VM setup</h3>

- Set up the first virtual machine (VM) to serve as the domain controller.
  
  ![VM1](https://github.com/user-attachments/assets/b2647f4c-c676-48ee-993c-0f9715143069)
  ![VM2](https://github.com/user-attachments/assets/65e1ca6a-9f58-4bf5-b44c-0a4a56c11764)

* For the network interface, select the virtual network already created 
  
  ![VM3](https://github.com/user-attachments/assets/0071d412-02d9-427a-8517-3de905c662ab)
* After reviewing your settings, click "Review + Create," then select "Create" once the validation is complete to set up your virtual machine.

<br>

- You can now access your VM with Remote Desktop and your public IP address

  
  ![PD1](https://github.com/user-attachments/assets/41a5d32e-1257-4f45-8312-6207f4bfc2bd)
![R2](https://github.com/user-attachments/assets/5da08d2b-eda7-4091-86a3-286a046171f1)

<br>
<br>
<br>
  <h3>&#9314; Change domain controller private IP address to static</h3>
  
  - Inside the VM, Select "Network Settings", and click on the network interface card

  
![n1](https://github.com/user-attachments/assets/b1cb35d5-a772-4d58-a1bc-efe0b5b69b82)

- Select  IP configuration -> ipconfig1, and change the Private IP address allocation to static.
  
  ![n2](https://github.com/user-attachments/assets/90d2db55-cdf6-4bfd-aeed-23d071e9d233)
<br>
<br>
<br>

   <h3>&#9315; Client VM setup</h3>
   
  - Setting up a client VM follows the same process as setting up the domain controller VM. The only differences are:<br>
   I. Use of different name for client VM <br>
   II. Use of different disk image: specifically Windows (Windows 10 Pro)<br>
   III. Use of different credentials for the administrator account

  
![CL1](https://github.com/user-attachments/assets/54b77773-519d-4ccc-8289-79c0eee22f0d)
 ![C2](https://github.com/user-attachments/assets/8d2a41a7-743d-455e-9427-42a04b28cdcd)

<br>

 - Because we used the same virtual network for this VM, the VM takes the next available private IP address in the virtual network's address space.


![CL2](https://github.com/user-attachments/assets/cb3ee024-f022-44db-98be-d350275641c5)

* After reviewing your settings, click "Review + Create," then select "Create" once the validation is complete to set up your virtual machine.


- Just like the domain controller VM, you can access the client VM with Remote Desktop and the public IP address
<br>
<br>
<br>

 <h3>&#9315; 
 Establish a connection between the domain controller and client VMs
</h3>

- At this point, you should be logged into the domain controller and client VM


- From the client VM ping the domain controller VM to test connectivity

  
  ![Ping1](https://github.com/user-attachments/assets/54b6a6b7-5d29-4c5e-a865-a0097c81861d)


<br>

- We can see the request timed out without receiving a response. This is because the domain controller VM's firewall blocks ICMPv4 traffic.
    To allow ICMPv4 traffic, follow the following steps: <br>

    Inside the domain controller VM access the Windows firewall advanced settings -> Select "Inbound Rules" -> Virtual Machine Monitoring(Echo Request-ICMPv4-In) -> Select "Enable Rule"

    ![C2](https://github.com/user-attachments/assets/4aa39d72-59d9-47aa-949d-dd734ec192e5)

  <br>

- Now go back to the client machine and try to ping the domain controller machine again. Echo responses should be received, indicating a successful connection



    ![PING2](https://github.com/user-attachments/assets/d8a15c70-3208-4d74-bed1-dfd42fe44dfd)
<br>
<br>

<h3>Conclusion</h3>

We have completed the foundational setup for our Active Directory projects by configuring two virtual machines. This phase involved setting up one machine to serve as a Domain Controller and another as a Client machine. In this setup, we enabled remote access and  examined network traffic. This groundwork will support more advanced configurations and scenarios in future projects






