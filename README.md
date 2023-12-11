<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

1. Create resources 
2. Observe ICMP traffic 
3. Observe SSH traffic 
4. Observe DHCP traffic
5. Observe DNS traffic
6. Observe RDP traffic 

<h2>Actions and Observations</h2>

<h3>1. Creating the resources</h3>

To start off, I logged into my Azure account and headed over to resource groups in order to create one to hold my virtual machines. For this project I created one Windows 10 pro (21H2) machine and a Linux (Ubuntu Server 20.04) machine. I made sure Azure created the Windows machine's virtual private network and subnet before creating the Ubuntu machine. This step was crucial to open the line for communication between them. For the Windows machine, I allowed port 3389 to be open to enable the remote desktop feature. In the Ubuntu machine, I enabled port 22 to enable the secure shell feature. After the creation of my resources, I verified that both machines were placed in the same virtual network. 



<h3>2. Observe ICMP traffic</h3>

Using the Windows machine's private IP address taken from my Azure Network Watcher, I connected to my Windows machine via Remote Desktop. I proceeded to downloading and installing Wireshark using my browser. Wireshark is a network protocol analyzer used to capture packets from a network connection. This is the application I utilized to observe what communications were being transmitted behind the scenes my own network connections. 

<h3>3. Observe SSH traffic</h3>

<h3>4. Observe DHCP traffic</h3>

<h3>5. Observe DNS traffic</h3>

<h3>6. Observe RDP traffic</h3>



