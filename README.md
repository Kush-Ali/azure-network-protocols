<p align="center">
  <img src="https://github.com/user-attachments/assets/a9e62984-6877-41d3-b24c-25d0460b9005" alt="Microsoft Azure Banner">
</p>

<h1>Network Security Groups (NSGs) and Inspecting Network Protocols</h1>

<p>In this lab, I demonstrated creating virtual machines in Microsoft Azure, analyzing network traffic with WireShark, and configuring Network Security Groups (NSGs) to manage traffic flow. This hands-on experience deepened my understanding of network protocols and security rules in a cloud environment.</p>

<h2>Part 1: Creating Virtual Machines</h2>

1. Logged into the Azure portal.
2. Created a resource group for this lab.
3. Set up a Windows 10 VM, selecting the new resource group and allowing Azure to auto-create the VNet and Subnet.
4. Created a Linux (Ubuntu) VM in the same resource group and VNet as the Windows 10 VM.
5. Finally, I made sure both VMs were in the same Vnet and Subnet.

<p align="center">
  <img src="https://github.com/user-attachments/assets/2f710177-e461-4681-97f7-666466b38e3b" alt="Creating Virtual Machines" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/d8ac240d-74f5-4cde-8943-31604d1a561b" alt="Creating Virtual Machines" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/9bd3848b-8671-4124-b8b9-96d693843d38" alt="Creating Virtual Machines" width="80%">
</p>

<h2>Part 2: Observing ICMP Traffic</h2>

1. I used remote desktop connection to connect to my Windows 10 VM
2. Once connected, I installed Wireshark for network analysis
3. I started a packet capture in WireShark and filtered specifically for ICMP traffic.
4. From the Windows 10 VM, I pinged my Ubuntu VM using its private IP address.
5. In WireShark, I observed the ICMP traffic flowing between the VMs.




<p align="center">
  
  <img src="https://github.com/user-attachments/assets/e94ff4f2-ef14-48ec-8a73-9a61d80b02a1" alt="Observing ICMP Traffic" width="80%">
</p>


<p align="center">
  
  <img src="https://github.com/user-attachments/assets/361c493d-d565-4474-a180-03109f51accf" alt="Observing ICMP Traffic" width="80%">
</p>

<p align="center">
  
  <img src="https://github.com/user-attachments/assets/ca8f41bf-bc62-4583-b7ae-a1fa3287e804" alt="Observing ICMP Traffic" width="80%">
</p>



<h2>Part 3: Configuring Network Security Groups (NSGs)</h2>

1. To test the effects of security rules, I started a continuous ping from my Windows 10 VM to the Ubuntu VM.
2. I then went to Azure and disabled inbound ICMP traffic in the NSG associated with the Ubuntu VM.
3. Back in WireShark, I observed the blocked ICMP traffic and noticed the ping activity had stopped.
4. Afterward, I re-enabled ICMP traffic in the NSG and observed the traffic being restored and the ping activity resuming.


<p align="center">
  <img src="https://github.com/user-attachments/assets/f8310d70-9805-466a-9ce2-c8aedc42eb42" alt="Configuring NSGs" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/385c1551-1f6c-46dd-9f0b-5129b8c8e5fa" alt="Configuring NSGs" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/52cc21f5-d0b5-4997-88ef-c777c2423c26" alt="Configuring NSGs" width="80%">
</p>


<p align="center">
  <img src="https://github.com/user-attachments/assets/d793a819-4bed-440e-a359-cbbcbcbdde97" alt="Configuring NSGs" width="80%">
</p>










<h2>Part 4: Observing Protocol Traffic</h2>

I explored different protocols and observed their behavior using WireShark:

- **SSH Traffic:** 
  <p>I captured SSH traffic in WireShark by initiating an SSH session from the Windows 10 VM to the Ubuntu VM using its private IP address (10.0.0.5).</p>
<ul>
  <li>The session was encrypted using the SSHv2 protocol, which includes key exchanges and encrypted packets as part of the secure communication between the two machines.</li>
  <li>In WireShark, I monitored the encrypted traffic as I executed commands within the Ubuntu VM via SSH. The capture confirmed that SSH provides a secure and encrypted channel for communication.</li>
</ul>
<p align="center">
 <img src="https://github.com/user-attachments/assets/92a3e7ce-1267-4ad0-b943-fcced93c8d0b" alt="Observing Protocol Traffic" width="80%">
</p>





- **DHCP Traffic:**
  - I filtered for DHCP traffic in WireShark.
  - On the Windows 10 VM, I created a batch file named `dhcp.bat` containing the commands `ipconfig /release` and `ipconfig /renew`.
  - I executed the batch file in PowerShell, then observed the DHCP handshake taking place in WireShark.


<p align="center">
  <img src="https://github.com/user-attachments/assets/b435f652-5b9f-4e18-b848-2dde78d11eb2" alt="Observing Protocol Traffic" width="80%">
</p>


<p align="center">
  <img src="https://github.com/user-attachments/assets/06da3ba4-f452-451d-906b-dd6eb685ae22" alt="Observing Protocol Traffic" width="80%">
</p>


<p align="center">
  <img src="https://github.com/user-attachments/assets/cb72735e-2e2e-4cad-99cb-b71ed4d14f4e" alt="Observing Protocol Traffic" width="80%">
</p>





- **DNS Traffic:** 
  - Filtering for DNS traffic in WireShark, I used `nslookup` to query DNS records for google.com observing the queries and responses.
 
  <p align="center">
  <img src="https://github.com/user-attachments/assets/0023b762-b965-4bfe-9c21-f2d94f1cee60" alt="Observing Protocol Traffic" width="80%">
</p>




- **RDP Traffic:** 
  - Lastly, I filtered for RDP traffic and observed the continuous flow of packets due to my active Remote Desktop session on the Windows 10 VM.


<p align="center">
  <img src="https://github.com/user-attachments/assets/6caede60-93d3-4d91-a7e4-5353354f12ed" alt="Observing Protocol Traffic" width="80%">
</p>





<h2>Conclusion</h2>

<p>By completing this lab, I gained experience in deploying VMs, analyzing network traffic, and configuring Network Security Groups in Azure. I also deepened my understanding of network protocols such as ICMP, SSH, DHCP, DNS, and RDP while using WireShark to inspect and analyse these protocols.</p>
